---
title: AAA "carregar dados (.NET - pesquisa do Azure) | Microsoft Docs"
description: "Saiba como o índice de tooan tooupload dados na pesquisa do Azure usando Olá .NET SDK."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a>Carregar dados tooAzure pesquisa usando Olá SDK .NET
> [!div class="op_single_selector"]
> * [Visão geral](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

Este artigo mostra como Olá toouse [SDK .NET da pesquisa do Azure](https://aka.ms/search-sdk) tooimport dados em um índice de pesquisa do Azure.

Antes de começar este passo a passo, você já deve ter [criado um índice de Pesquisa do Azure](search-what-is-an-index.md). Este artigo também pressupõe que você já tenha criado um `SearchServiceClient` do objeto, como mostrado na [criar um índice de pesquisa do Azure usando o SDK .NET de saudação](search-create-index-dotnet.md#CreateSearchServiceClient).

> [!NOTE]
> Todos os códigos de exemplo neste artigo foram escritos em C#. Você pode encontrar o código-fonte completo Olá [no GitHub](http://aka.ms/search-dotnet-howto). Você também pode ler sobre Olá [SDK .NET da pesquisa do Azure](search-howto-dotnet-sdk.md) para um mais detalhado passo a passo do código de exemplo hello.

Em documentos de toopush ordem pra o índice usando Olá .NET SDK, você precisará:

1. Criar um `SearchIndexClient` objeto tooconnect tooyour índice de pesquisa.
2. Criar um `IndexBatch` contendo Olá documentos toobe adicionada, modificada ou excluída.
3. Chamar hello `Documents.Index` método de sua `SearchIndexClient` toosend Olá `IndexBatch` tooyour índice de pesquisa.

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Crie uma instância da classe SearchIndexClient de saudação
tooimport dados usando seu índice Olá SDK .NET da pesquisa do Azure, você precisará toocreate uma instância do hello `SearchIndexClient` classe. Você pode construir essa instância por conta própria, mas é mais fácil se você já tiver um `SearchServiceClient` toocall instância seu `Indexes.GetClient` método. Por exemplo, aqui está como você poderia obter um `SearchIndexClient` índice Olá denominado "hotéis" de um `SearchServiceClient` chamado `serviceClient`:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> Em um aplicativo típico de pesquisa, o gerenciamento e o preenchimento do índice é tratado por um componente separado das consultas de pesquisa. `Indexes.GetClient`é conveniente para preencher um índice porque poupa Olá problemas de fornecer outra `SearchCredentials`. Ele faz isso passando a chave de administração Olá Olá de toocreate usadas que você `SearchServiceClient` toohello novo `SearchIndexClient`. No entanto, em parte de saudação do aplicativo que executa consultas, é melhor Olá de toocreate `SearchIndexClient` diretamente para que você pode passar de uma chave de consulta em vez de uma chave de administração. Isso é consistente com hello [princípio de menos privilégios](https://en.wikipedia.org/wiki/Principle_of_least_privilege) e ajudará toomake seu aplicativo mais seguro. Você pode encontrar mais informações sobre chaves de administração e as chaves de consulta Olá [referência da API de REST de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/).
> 
> 

`SearchIndexClient` tem uma propriedade `Documents`. Esta propriedade fornece todos os métodos de saudação tooadd, você precisa modificar, excluir ou consultar documentos no índice.

## <a name="decide-which-indexing-action-toouse"></a>Decidir quais indexação toouse de ação
dados tooimport usando Olá .NET SDK, você precisará toopackage backup de seus dados em um `IndexBatch` objeto. Um `IndexBatch` encapsula uma coleção de `IndexAction` objetos, cada qual contendo um documento e uma propriedade que indica a pesquisa do Azure que tooperform ação nesse documento (carregar, mesclar, excluir, etc.). Dependendo de qual dos Olá ações que você escolher abaixo, somente determinados campos devem ser incluídos para cada documento:

| Ação | Descrição | Campos necessários para cada documento | Observações |
| --- | --- | --- | --- |
| `Upload` |Um `Upload` ação é similar tooan "upsert" onde documento hello será inserido se for novo e atualizado/substituído se ele existir. |chave, além de quaisquer outros campos que você deseja toodefine |Ao atualizar/substituir um documento existente, qualquer campo que não está especificado na solicitação de saudação terá seu campo definido muito`null`. Isso ocorre mesmo quando o campo Olá tiver sido definido anteriormente tooa valor de não-nulo. |
| `Merge` |Atualizações de uma existente de documento com hello especificado campos. Se o documento de saudação não existe no índice hello, mesclagem Olá falhará. |chave, além de quaisquer outros campos que você deseja toodefine |Qualquer campo que você especificar em uma mesclagem substituirá o campo de saudação existente no documento de saudação. Isso inclui campos do tipo `DataType.Collection(DataType.String)`. Por exemplo, se hello documento contém um campo `tags` com valor `["budget"]` e executar uma mesclagem com valor `["economy", "pool"]` para `tags`, Olá valor final do hello `tags` campo será `["economy", "pool"]`. Ele não será `["budget", "economy", "pool"]`. |
| `MergeOrUpload` |Esta ação se comporta como `Merge` se um documento com hello atribuída a chave já existe no índice hello. Se o documento de saudação não existir, ele se comporta como `Upload` com um novo documento. |chave, além de quaisquer outros campos que você deseja toodefine |- |
| `Delete` |Remove o documento especificado Olá do índice de saudação. |somente chave |Todos os campos que você especificar que o campo de chave hello será ignorado. Se você quiser tooremove um campo individual de um documento, use `Merge` em vez disso e basta definir campo Olá explicitamente toonull. |

Você pode especificar a ação que você deseja toouse com hello vários métodos estáticos da saudação `IndexBatch` e `IndexAction` classes, conforme mostrado na próxima seção, Olá.

## <a name="construct-your-indexbatch"></a>Construa seu IndexBatch
Agora que você sabe quais ações tooperform em seus documentos, você está pronto tooconstruct Olá `IndexBatch`. Olá o exemplo a seguir mostra como toocreate um lote com algumas ações diferentes. Observe que o nosso exemplo usa uma classe personalizada chamada `Hotel` que mapeia tooa documento no índice de "hotéis" hello.

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "1",
                BaseRate = 199.0,
                Description = "Best hotel in town",
                DescriptionFr = "Meilleur hôtel en ville",
                HotelName = "Fancy Stay",
                Category = "Luxury",
                Tags = new[] { "pool", "view", "wifi", "concierge" },
                ParkingIncluded = false,
                SmokingAllowed = false,
                LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero),
                Rating = 5,
                Location = GeographyPoint.Create(47.678581, -122.131577)
            }),
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "2",
                BaseRate = 79.99,
                Description = "Cheapest hotel in town",
                DescriptionFr = "Hôtel le moins cher en ville",
                HotelName = "Roach Motel",
                Category = "Budget",
                Tags = new[] { "motel", "budget" },
                ParkingIncluded = true,
                SmokingAllowed = true,
                LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
                Rating = 1,
                Location = GeographyPoint.Create(49.678581, -122.131577)
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

Nesse caso, estamos usando `Upload`, `MergeOrUpload`, e `Delete` como nossas ações de pesquisa, conforme especificado por métodos Olá chamados hello `IndexAction` classe.

Suponha que o índice de exemplo "hotels" já esteja preenchido com vários documentos. Observe como não tínhamos toospecify todos os campos de documento possíveis Olá ao usar `MergeOrUpload` e como podemos só especificado de chave de documento hello (`HotelId`) ao usar `Delete`.

Além disso, observe que você só pode incluir documentos too1000 em uma única solicitação de indexação.

> [!NOTE]
> Neste exemplo, estamos aplicando documentos de toodifferent ações diferentes. Se você quisesse tooperform Olá ações mesmo em todos os documentos em lote hello, em vez de chamar `IndexBatch.New`, você pode usar Olá outros métodos estáticos de `IndexBatch`. Por exemplo, você poderia criar lotes chamando `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` ou `IndexBatch.Delete`. Esses métodos usam um conjunto de documentos (objetos do tipo `Hotel` neste exemplo) em vez de objetos `IndexAction`.
> 
> 

## <a name="import-data-toohello-index"></a>Índice de toohello de dados de importação
Agora que você tem uma inicializado `IndexBatch` do objeto, você pode enviá-lo toohello índice chamando `Documents.Index` em seu `SearchIndexClient` objeto. Olá mostrado no exemplo a seguir como toocall `Index`, bem como algumas etapas adicionais que você precisará tooperform:

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
    // hello batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log hello failed document keys and continue.
    Console.WriteLine(
        "Failed tooindex some of hello documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents toobe indexed...\n");
Thread.Sleep(2000);
```

Saudação de Observação `try` / `catch` ao redor Olá chamada toohello `Index` método. bloco catch de saudação trata um caso de erro importante para indexação. Se o serviço de pesquisa do Azure falhar tooindex alguns Olá documentos em lote hello, um `IndexBatchException` é gerada pelo `Documents.Index`. Isso pode acontecer se você estiver indexando documentos enquanto o serviço estiver sob carga pesada. **É altamente recomendável a manipulação explícita desse caso em seu código.** Você pode atrasar e repita indexação documentos Olá que falhou, ou faça e continuar como não do exemplo hello, ou você pode fazer algo diferente, dependendo dos requisitos de consistência de dados do aplicativo.

Por fim, Olá código exemplo hello acima atrasos por dois segundos. A indexação ocorre assincronamente no serviço de pesquisa do Azure, para que o aplicativo de exemplo hello precisa toowait um tooensure curto período de tempo que os documentos de saudação estão disponíveis para pesquisa. Normalmente, atrasos como esses só são necessários em demonstrações, testes e exemplos de aplicativos.

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a>Olá como documentos de identificadores do SDK do .NET
Você deve estar se perguntando como Olá SDK .NET da pesquisa do Azure é instâncias tooupload capaz de uma classe definida pelo usuário como `Hotel` toohello índice. toohelp responder essa pergunta, vamos examinar a saudação `Hotel` classe, que mapeia o esquema de índice toohello definido em [criar um índice de pesquisa do Azure usando o SDK .NET de saudação](search-create-index-dotnet.md#DefineIndex):

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }

    // ToString() method omitted for brevity...
}
```

Olá primeiro toonotice é que cada propriedade pública de `Hotel` corresponde tooa campo na definição de índice hello, mas com uma diferença fundamental: nome de saudação de cada campo começa com uma letra minúscula ("concatenação com maiusculas"), ao nome de saudação de cada público propriedade de `Hotel` começa com uma letra maiuscula ("Pascal case"). Este é um cenário comum em aplicativos .NET que executem a associação de dados em que o esquema de destino Olá é controle Olá fora do desenvolvedor do aplicativo hello. Em vez de tooviolate Olá .NET diretrizes de nomenclatura, tornando o caso de ter de nomes de propriedade, você pode informar Olá SDK toomap Olá propriedade nomes toocamel caso automaticamente com hello `[SerializePropertyNamesAsCamelCase]` atributo.

> [!NOTE]
> Olá SDK .NET da pesquisa do Azure usa Olá [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize de biblioteca e desserializar o tooand de objetos de modelo personalizado do JSON. Se necessário, você pode personalizar essa serialização. Encontre mais detalhes em [Serialização personalizada com JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet). Um exemplo disso é o uso de saudação do hello `[JsonProperty]` atributo Olá `DescriptionFr` propriedade no código de exemplo hello acima.
> 
> 

Olá segundo importante sobre Olá `Hotel` classe são tipos de dados de saudação de propriedades públicas de saudação. tipos de .NET Olá dessas propriedades mapeiam tipos de campo equivalente de tootheir na definição de índice de saudação. Por exemplo, Olá `Category` mapas de propriedade de cadeia de caracteres toohello `category` campo, que é do tipo `DataType.String`. Há mapeamentos de tipo semelhantes entre `bool?` e `DataType.Boolean`, `DateTimeOffset?` e `DataType.DateTimeOffset` etc. regras específicas de saudação para mapeamento de tipo hello documentadas com hello `Documents.Get` método hello [referência de SDK .NET da pesquisa do Azure](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).

Essa capacidade toouse suas próprias classes como documentos funciona em ambas as direções; Você também pode recuperar os resultados da pesquisa e ter Olá SDK automaticamente desserializá-los tooa tipo de sua escolha, conforme mostrado no hello [próximo artigo](search-query-dotnet.md).

> [!NOTE]
> Olá SDK .NET da pesquisa do Azure também oferece suporte a documentos digitadas dinamicamente usando Olá `Document` classe, que é um mapeamento de chave/valor nomes toofield de valores de campo. Isso é útil em cenários onde você não souber o esquema de índice Olá em tempo de design, ou onde seria classes de modelo de toospecific toobind inconveniente. Todos os métodos Olá Olá SDK que lidam com documentos têm sobrecargas que funcionam com hello `Document` classe, bem como sobrecargas fortemente tipados que usam um parâmetro de tipo genérico. Olá somente última são usados no código de exemplo hello neste artigo.
> 
> 

**Por que você deve usar tipos de dados anuláveis**

Durante a criação de índice de pesquisa do Azure seu próprio modelo classes toomap tooan, é recomendável declarando propriedades de tipos de valor como `bool` e `int` toobe anulável (por exemplo, `bool?` em vez de `bool`). Se você usar uma propriedade não anulável, você tem muito**garante** sem documentos no índice contêm um valor nulo para o campo correspondente do hello. Olá SDK, nem Olá serviço Azure Search ajudará você tooenforce isso.

Isso não é apenas uma preocupação hipotética: Imagine um cenário em que você adicionar um novo campo tooan índice existente que é do tipo `DataType.Int32`. Depois de atualizar a definição de índice hello, todos os documentos terá um valor nulo para esse novo campo (desde que todos os tipos são anuláveis na pesquisa do Azure). Se você usar uma classe de modelo com um não anulável `int` propriedade para esse campo, você receberá um `JsonSerializationException` assim ao tentar tooretrieve documentos:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Por esse motivo, sugerimos que você use tipos anuláveis nas suas classes de modelo como uma prática recomendada.

## <a name="next-steps"></a>Próximas etapas
Depois de preencher o índice de pesquisa do Azure, você será toostart pronto emitir consultas toosearch para documentos. Veja [Consultar seu Índice de Pesquisa do Azure](search-query-overview.md) para obter detalhes.

