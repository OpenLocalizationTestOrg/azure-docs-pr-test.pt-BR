---
title: aaaHow toouse pesquisa do Azure de um aplicativo .NET | Microsoft Docs
description: Como o Azure toouse de pesquisa de um aplicativo .NET
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a>Como o Azure toouse de pesquisa de um aplicativo .NET
Este artigo é um passo a passo tooget você em funcionamento com hello [SDK .NET da pesquisa do Azure](https://aka.ms/search-sdk). Você pode usar Olá .NET SDK tooimplement uma rica experiência de pesquisa em seu aplicativo usando a pesquisa do Azure.

## <a name="whats-in-hello-azure-search-sdk"></a>O que é Olá a pesquisa do Azure SDK
Olá SDK consiste em uma biblioteca de cliente, `Microsoft.Azure.Search`. Ele permite que você toomanage seus índices, fontes de dados e indexadores, bem como carregar e gerenciar documentos e executar consultas, sem a necessidade de toodeal com detalhes de saudação do HTTP e JSON.

biblioteca de cliente Olá define classes como `Index`, `Field`, e `Document`, bem como operações como `Indexes.Create` e `Documents.Search` em Olá `SearchServiceClient` e `SearchIndexClient` classes. Essas classes são organizadas em Olá namespaces a seguir:

* [Microsoft.Azure.Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [Microsoft.Azure.Search.Models](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

versão atual de saudação do hello SDK .NET da pesquisa do Azure agora está disponível. Se você quiser tooprovide comentários para que possamos tooincorporate na próxima versão de hello, visite nosso [página de comentários](https://feedback.azure.com/forums/263029-azure-search/).

Olá SDK .NET oferece suporte à versão `2016-09-01` de saudação [API de REST de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/). Agora, essa versão inclui suporte para analisadores personalizados e suporte para indexador de Tabela do Azure e Blob do Azure. Recursos que são de visualização *não* parte desta versão, como o suporte para indexação de arquivos CSV e JSON, estão em [visualização](search-api-2015-02-28-preview.md) e disponível por meio de saudação anterior [versão 2.0-visualização do SDK .NET de saudação ](https://aka.ms/search-sdk-preview).

Esse SDK não oferece suporte a [Operações de Gerenciamento](https://docs.microsoft.com/rest/api/searchmanagement/), como criar e dimensionar os serviços de Pesquisa e gerenciar chaves de API. Se você precisar toomanage seus recursos de pesquisa de um aplicativo .NET, você pode usar o hello [Azure SDK de gerenciamento de .NET da pesquisa](https://aka.ms/search-mgmt-sdk).

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a>Atualizando a versão mais recente toohello de saudação SDK
Se você já estiver usando uma versão mais antiga do hello SDK .NET da pesquisa do Azure e você desejar tooupgrade toohello nova disponível versão, [neste artigo](search-dotnet-sdk-migration.md) explica como.

## <a name="requirements-for-hello-sdk"></a>Requisitos para Olá SDK
1. Visual Studio 2017.
2. Seu próprio serviço de Pesquisa do Azure. Saudação de toouse ordem SDK, você precisará nome de saudação do serviço e uma ou mais chaves de API. [Criar um serviço no portal de saudação](search-create-service-portal.md) ajudá-lo através dessas etapas.
3. Baixar o SDK .NET da pesquisa do Azure de saudação [pacote NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) usando "Gerenciar pacotes NuGet" no Visual Studio. Procurar nome de pacote hello `Microsoft.Azure.Search` em NuGet.org.

Olá SDK .NET da pesquisa do Azure oferece suporte a aplicativos destinados a saudação do .NET Framework 4.6 e o .NET Core.

## <a name="core-scenarios"></a>Principais cenários
Há várias coisas que você precisará toodo no seu aplicativo de pesquisa. Neste tutorial, abordaremos os principais cenários:

* Criando um índice
* Popular o índice de saudação com documentos
* Procura por documentos usando filtros e pesquisa de texto completo

código de exemplo Hello a seguir ilustra cada um deles. Sinta-se livre toouse Olá trechos de código em seu próprio aplicativo.

### <a name="overview"></a>Visão geral
Olá vamos explorar do aplicativo de exemplo cria um novo índice chamado "hotéis", preenche-o com alguns documentos, em seguida, executa algumas consultas de pesquisa. Aqui está o programa principal hello, mostrando Olá fluxo geral:

```csharp
// This sample shows how toodelete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> Você pode encontrar o código-fonte completo Olá Olá do aplicativo de exemplo usado no passo a passo no [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).
> 
>

Vamos examinar isso passo a passo. Primeiro, precisamos toocreate um novo `SearchServiceClient`. Esse objeto permite toomanage índices. Ordem tooconstruct um, é necessário tooprovide o nome do serviço de pesquisa do Azure, bem como uma chave de API de administração. Você pode inserir essas informações em Olá `appsettings.json` arquivo hello [aplicativo de exemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> Se você fornecer uma chave incorreta (por exemplo, uma chave de consulta em que foi necessária uma chave de administração), Olá `SearchServiceClient` lançará um `CloudException` com hello "Proibido" de mensagem do hello erro primeira vez que você chamar um método de operação, como `Indexes.Create`. Se isso acontecer tooyou, verifique novamente a chave de API.
> 
> 

Olá próximas linhas chamar métodos toocreate um índice nomeado "hotéis", excluí-lo pela primeira vez, se ele já existe. Abordaremos esses métodos um pouco mais tarde.

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

Em seguida, o índice Olá precisa toobe preenchido. toodo isso, será necessário um `SearchIndexClient`. Há dois tooobtain maneiras um: Criando-lo, ou chamando `Indexes.GetClient` em Olá `SearchServiceClient`. Usamos Olá último para sua conveniência.

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> Em um aplicativo típico de pesquisa, o gerenciamento e o preenchimento do índice é tratado por um componente separado das consultas de pesquisa. `Indexes.GetClient`é conveniente para preencher um índice porque poupa Olá problemas de fornecer outra `SearchCredentials`. Ele faz isso passando a chave de administração Olá Olá de toocreate usadas que você `SearchServiceClient` toohello novo `SearchIndexClient`. No entanto, em parte de saudação do aplicativo que executa consultas, é melhor Olá de toocreate `SearchIndexClient` diretamente para que você pode passar de uma chave de consulta em vez de uma chave de administração. Isso é consistente com o princípio de saudação de menos privilégios e ajudará toomake seu aplicativo mais seguro. Você pode saber mais sobre chaves de administração e chaves de consulta [aqui](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).
> 
> 

Agora que temos um `SearchIndexClient`, é possível preencher o índice de hello. Isso é feito por outro método que descreveremos mais tarde detalhadamente.

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

Por fim, podemos executar algumas consultas de pesquisa e exibir resultados de saudação. Dessa vez, usamos outro `SearchIndexClient`:

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

Nós o conduziremos detalhadamente Olá `RunQueries` método posteriormente. Aqui está o Olá Olá de toocreate código novo `SearchIndexClient`:

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

Dessa vez usamos uma chave de consulta porque não precisamos do índice de toohello de acesso de gravação. Você pode inserir essas informações em Olá `appsettings.json` arquivo hello [aplicativo de exemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

Se você executar este aplicativo com um nome de serviço válido e chaves de API, saída de hello deve ter esta aparência:

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
    Search hello entire index for hello term 'budget' and return only hello hotelName field:
    
    Name: Roach Motel
    
    Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river
    
    Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search hello entire index for hello term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key tooend application...

código-fonte completo do aplicativo hello Olá é fornecido no final deste artigo hello.

Em seguida, nós o conduziremos examinar mais detalhadamente cada um dos métodos Olá chamados pelo `Main`.

### <a name="creating-an-index"></a>Criando um índice
Depois de criar um `SearchServiceClient`, coisa Avançar Olá `Main` does é o índice de exclusão hello "hotéis" se ele já existe. Isso é feito por Olá método a seguir:

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

Esse método usa Olá dado `SearchServiceClient` toocheck se houver Olá índice e nesse caso, exclua-o.

> [!NOTE]
> código de exemplo Hello este artigo usa métodos síncronos de saudação do hello SDK .NET da pesquisa do Azure para manter a simplicidade. É recomendável que você use os métodos assíncronos Olá em seu próprios aplicativos tookeep-los, escalonáveis e responsivos. Por exemplo, no hello método anteriormente, você pode usar `ExistsAsync` e `DeleteAsync` em vez de `Exists` e `Delete`.
> 
> 

Em seguida, `Main` cria um novo índice "hotéis" chamando este método:

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

Esse método cria um novo `Index` objeto com uma lista de `Field` objetos que define o esquema de saudação do novo índice de saudação. Cada campo tem um nome, tipo de dados e vários atributos que definem seu comportamento de pesquisa. Olá `FieldBuilder` classe usa reflexão toocreate uma lista de `Field` objetos para o índice de saudação examinando Olá propriedades públicas e os atributos de saudação dado `Hotel` classe de modelo. Vamos dar uma análise detalhada Olá `Hotel` classe posteriormente.

> [!NOTE]
> Você sempre pode criar lista de saudação do `Field` objetos diretamente em vez de usar `FieldBuilder` se necessário. Por exemplo, talvez você não queira toouse uma classe de modelo ou talvez seja necessário toouse uma classe de modelo existente que você não deseja toomodify adicionando atributos.
>
> 

Além disso toofields, você pode também adicionar perfis de pontuação, sugestões ou opções de CORS toohello índice (elas são omitidas do exemplo hello para fins de brevidade). Você pode encontrar mais informações sobre o objeto de índice hello e suas partes constituintes em Olá [referência de SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), bem como no hello [referência da API de REST de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/).

### <a name="populating-hello-index"></a>Popular o índice de saudação
a próxima etapa Olá no `Main` toopopulate Olá recém-criado índice. Isso é feito no hello método a seguir:

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
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
        },
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
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

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
}
```

Este método tem quatro partes. Olá primeiro cria uma matriz de `Hotel` objetos que servirão como o índice de toohello de tooupload nossos dados de entrada. Esses dados são codificados para manter a simplicidade. Em seu próprio aplicativo, provavelmente seus dados virão de uma fonte de dados externa, como um banco de dados SQL.

Olá segunda parte cria um `IndexBatch` que contêm documentos hello. Especifique Olá operação desejada tooapply toohello lote no tempo de saudação criá-lo, nesse caso, chamando `IndexBatch.Upload`. Olá lote for carregado toohello pesquisa do Azure de índice por Olá `Documents.Index` método.

> [!NOTE]
> Neste exemplo, estamos carregando apenas documentos. Se você quisesse toomerge alterações nos documentos existentes ou excluir documentos, você pode criar lotes chamando `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, ou `IndexBatch.Delete` em vez disso. Também é possível misturar operações diferentes em um único lote chamando `IndexBatch.New`, que usa uma coleção de `IndexAction` objetos, cada um deles informa tooperform de pesquisa do Azure, uma operação específica em um documento. Você pode criar cada `IndexAction` com sua própria operação chamando o método correspondente hello como `IndexAction.Merge`, `IndexAction.Upload`e assim por diante.
> 
> 

Olá terceira parte desse método é um bloco catch que manipula um caso de erro importante para indexação. Se o serviço de pesquisa do Azure falhar tooindex alguns Olá documentos em lote hello, um `IndexBatchException` é gerada pelo `Documents.Index`. Isso pode acontecer se você estiver indexando documentos enquanto o serviço estiver sob carga pesada. **É altamente recomendável a manipulação explícita desse caso em seu código.** Você pode atrasar e repita indexação documentos Olá que falhou, ou faça e continuar como não do exemplo hello, ou você pode fazer algo diferente, dependendo dos requisitos de consistência de dados do aplicativo.

> [!NOTE]
> Você pode usar o hello `FindFailedActionsToRetry` método tooconstruct um novo lote que contém somente Olá ações falha em uma chamada anterior muito`Index`. método Hello está documentado [aqui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) e há uma discussão de como tooproperly usar [em StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).
>
>

Por fim, Olá `UploadDocuments` atrasos de método de dois segundos. A indexação ocorre assincronamente no serviço de pesquisa do Azure, para que o aplicativo de exemplo hello precisa toowait um tooensure curto período de tempo que os documentos de saudação estão disponíveis para pesquisa. Normalmente, atrasos como esses só são necessários em demonstrações, testes e exemplos de aplicativos.

#### <a name="how-hello-net-sdk-handles-documents"></a>Olá como documentos de identificadores do SDK do .NET
Você deve estar se perguntando como Olá SDK .NET da pesquisa do Azure é instâncias tooupload capaz de uma classe definida pelo usuário como `Hotel` toohello índice. toohelp responder essa pergunta, vamos examinar a saudação `Hotel` classe:

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
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
}
```

Olá primeiro toonotice é que cada propriedade pública de `Hotel` corresponde tooa campo na definição de índice hello, mas com uma diferença fundamental: nome de saudação de cada campo começa com uma letra minúscula ("concatenação com maiusculas"), ao nome de saudação de cada público propriedade de `Hotel` começa com uma letra maiuscula ("Pascal case"). Este é um cenário comum em aplicativos .NET que executem a associação de dados em que o esquema de destino Olá é controle Olá fora do desenvolvedor do aplicativo hello. Em vez de tooviolate Olá .NET diretrizes de nomenclatura, tornando o caso de ter de nomes de propriedade, você pode informar Olá SDK toomap Olá propriedade nomes toocamel caso automaticamente com hello `[SerializePropertyNamesAsCamelCase]` atributo.

> [!NOTE]
> Olá SDK .NET da pesquisa do Azure usa Olá [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize de biblioteca e desserializar o tooand de objetos de modelo personalizado do JSON. Se necessário, você pode personalizar essa serialização. Para obter mais detalhes, consulte [Serialização personalizada com JSON.NET](#JsonDotNet).
> 
> 

Olá toonotice do segundo item são Olá atributos como `IsFilterable`, `IsSearchable`, `Key`, e `Analyzer` que decorar cada propriedade pública. Esses atributos são mapeados diretamente toohello [atributos correspondentes do índice de pesquisa do Azure Olá](https://docs.microsoft.com/rest/api/searchservice/create-index#request). Olá `FieldBuilder` classe usa essas definições de campo tooconstruct para índice hello.

Olá terceiro importante sobre Olá `Hotel` classe são tipos de dados de saudação de propriedades públicas de saudação. tipos de .NET Olá dessas propriedades mapeiam tipos de campo equivalente de tootheir na definição de índice de saudação. Por exemplo, Olá `Category` mapas de propriedade de cadeia de caracteres toohello `category` campo, que é do tipo `Edm.String`. Não há mapeamentos de tipo semelhante entre `bool?` e `Edm.Boolean`, `DateTimeOffset?` e `Edm.DateTimeOffset`, as regras específicas de saudação etc. para mapeamento de tipo hello documentadas com hello `Documents.Get` método hello [SDK .NET da pesquisa do Azure referência](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_). Olá `FieldBuilder` classe cuida desse mapeamento para você, mas ainda pode ser útil toounderstand caso você precise tootroubleshoot quaisquer problemas de serialização.

Essa capacidade toouse suas próprias classes como documentos funciona em ambas as direções; Você também pode recuperar os resultados da pesquisa e ter Olá SDK automaticamente desserializá-los tooa tipo de sua escolha, como veremos na próxima seção, Olá.

> [!NOTE]
> Olá SDK .NET da pesquisa do Azure também oferece suporte a documentos digitadas dinamicamente usando Olá `Document` classe, que é um mapeamento de chave/valor nomes toofield de valores de campo. Isso é útil em cenários onde você não souber o esquema de índice Olá em tempo de design, ou onde seria classes de modelo de toospecific toobind inconveniente. Todos os métodos Olá Olá SDK que lidam com documentos têm sobrecargas que funcionam com hello `Document` classe, bem como sobrecargas fortemente tipados que usam um parâmetro de tipo genérico. Olá somente última são usados no código de exemplo hello neste tutorial. Olá `Document` classe herda de `Dictionary<string, object>`. Encontre outros detalhes [aqui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).
> 
> 

**Por que você deve usar tipos de dados anuláveis**

Durante a criação de índice de pesquisa do Azure seu próprio modelo classes toomap tooan, é recomendável declarando propriedades de tipos de valor como `bool` e `int` toobe anulável (por exemplo, `bool?` em vez de `bool`). Se você usar uma propriedade não anulável, você tem muito**garante** sem documentos no índice contêm um valor nulo para o campo correspondente do hello. Olá SDK, nem Olá serviço Azure Search ajudará você tooenforce isso.

Isso não é apenas uma preocupação hipotética: Imagine um cenário em que você adicionar um novo campo tooan índice existente que é do tipo `Edm.Int32`. Depois de atualizar a definição de índice hello, todos os documentos terá um valor nulo para esse novo campo (desde que todos os tipos são anuláveis na pesquisa do Azure). Se você usar uma classe de modelo com um não anulável `int` propriedade para esse campo, você receberá um `JsonSerializationException` assim ao tentar tooretrieve documentos:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Por esse motivo, sugerimos que você use tipos anuláveis nas suas classes de modelo como uma prática recomendada.

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a>Serialização personalizada com JSON.NET
Olá SDK utiliza JSON.NET para serialização e desserialização de documentos. Você pode personalizar a serialização e desserialização se necessário, definindo suas próprias `JsonConverter` ou `IContractResolver` (consulte Olá [JSON.NET documentação](http://www.newtonsoft.com/json/help/html/Introduction.htm) para obter mais detalhes). Isso pode ser útil quando você quiser tooadapt uma classe de modelo existente do seu aplicativo para uso com a pesquisa do Azure e outros cenários mais avançados. Por exemplo, com a serialização personalizada, você pode:

* Incluir ou excluir determinadas propriedades da sua classe de modelo para serem armazenadas como campos de documento.
* Mapear os nomes de propriedade no código aos nomes de campo no índice.
* Crie atributos personalizados que podem ser usados para mapear os campos de toodocument propriedades.

Você pode encontrar exemplos de implementação de serialização personalizada em testes de unidade Olá para Olá SDK .NET da pesquisa do Azure no GitHub. Um bom ponto de partida é [esta pasta](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models). Contém classes que são usadas pelos testes de serialização personalizada hello.

### <a name="searching-for-documents-in-hello-index"></a>Procurando documentos no índice Olá
Olá última etapa no aplicativo de exemplo hello é toosearch para alguns documentos no índice de saudação. Olá método a seguir faz isso:

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
    Console.WriteLine("and return hello hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take hello top two results, and show only hotelName and ");
    Console.WriteLine("lastRenovationDate:\n");

    parameters =
        new SearchParameters()
        {
            OrderBy = new[] { "lastRenovationDate desc" },
            Select = new[] { "hotelName", "lastRenovationDate" },
            Top = 2
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.WriteLine("Search hello entire index for hello term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

Cada vez que ele executa uma consulta, esse método cria, primeiro, um novo objeto `SearchParameters`. Isso é opções adicionais de toospecify usado para consulta hello como classificação, filtragem, paginação e facetas. Nesse método, estamos configurando Olá `Filter`, `Select`, `OrderBy`, e `Top` propriedade para consultas diferentes. Saudação de todos os `SearchParameters` propriedades são documentadas [aqui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).

Olá próxima etapa é tooactually executar a consulta de pesquisa de saudação. Isso é feito usando Olá `Documents.Search` método. Para cada consulta, passamos Olá toouse de texto de pesquisa como uma cadeia de caracteres (ou `"*"` se não houver nenhum texto de pesquisa), além de saudação pesquisar parâmetros criados anteriormente. Especificar `Hotel` como parâmetro de tipo Olá para `Documents.Search`, que informa documentos de toodeserialize SDK Olá nos resultados da pesquisa Olá em objetos do tipo `Hotel`.

> [!NOTE]
> Você pode encontrar mais informações sobre sintaxe de expressão de consulta de pesquisa Olá [aqui](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).
> 
> 

Finalmente, depois de cada consulta este método itera todas as correspondências de saudação nos resultados da pesquisa hello, imprimindo cada console toohello de documento:

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

Por sua vez, vamos examinar mais detalhadamente cada uma das consultas de saudação. Aqui está a saudação código tooexecute Olá primeira consulta:

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

Nesse caso, estamos pesquisando hotéis que coincidir palavra hello "budget", e queremos tooget volta apenas Olá hotel nomes, conforme especificado pelas Olá `Select` parâmetro. Estes são os resultados de saudação:

    Name: Roach Motel

Em seguida, podemos deseja hotéis de saudação toofind com uma taxa noturna de menor que US $150 e retornar somente Olá hotel ID e a descrição:

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

Essa consulta usa um OData `$filter` expressão, `baseRate lt 150`, documentos de saudação toofilter no índice de saudação. Você pode encontrar mais informações sobre Olá sintaxe do OData que oferece suporte à pesquisa do Azure [aqui](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).

Estes são os resultados de saudação da consulta hello:

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

Em seguida, queremos toofind Olá superior dois hotéis foram renovados mais recentemente e mostram o nome do hotel hello e a última data de renovação. Aqui está o código de saudação: 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

Nesse caso, usamos novamente saudação do OData sintaxe toospecify `OrderBy` parâmetro como `lastRenovationDate desc`. Podemos também definir `Top` too2 tooensure somente obtemos documentos de duas primeiras hello. Como antes, definimos `Select` toospecify quais campos devem ser retornados.

Estes são os resultados de saudação:

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Por fim, queremos toofind todos os hotéis que coincidir palavra hello "motel":

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

Aqui estão os resultados de hello, que incluem todos os campos porque não especificamos Olá `Select` propriedade:

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

Essa etapa conclui o tutorial hello, mas não interrompe aqui. **Próximas etapas** fornece os recursos adicionais para aprender mais sobre a Pesquisa do Azure.

## <a name="next-steps"></a>Próximas etapas
* Procurar referências Olá Olá [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) e [API REST](https://docs.microsoft.com/rest/api/searchservice/).
* Aprofunde seus conhecimentos por meio de [vídeos e outros exemplos e tutoriais](search-video-demo-tutorial-list.md).
* Revisão [convenções de nomenclatura](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn regras de saudação de nomeação de vários objetos.
* Examine os [tipos de dados com suporte](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) na Pesquisa do Azure.
