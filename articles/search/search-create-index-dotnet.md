---
title: "AAA \"criar um índice (API .NET - pesquisa do Azure) | Microsoft Docs\""
description: "Crie um índice no código usando Olá SDK .NET da pesquisa do Azure."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 3a851647-fc7b-4fb6-8506-6aaa519e77cd
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 7fa4030b8c3565bc02b1d6bb4426331657cf3a5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-net-sdk"></a>Criar um índice de pesquisa do Azure usando o SDK .NET de saudação
> [!div class="op_single_selector"]
> * [Visão geral](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

Este artigo o guiará pelo processo de saudação de criação de uma pesquisa do Azure [índice](https://docs.microsoft.com/rest/api/searchservice/Create-Index) usando Olá [SDK .NET da pesquisa do Azure](https://aka.ms/search-sdk).

Antes de seguir este guia e criar um índice, você já deverá ter [criado um serviço do Azure Search](search-create-service-portal.md).

> [!NOTE]
> Todos os códigos de exemplo neste artigo foram escritos em C#. Você pode encontrar o código-fonte completo Olá [no GitHub](http://aka.ms/search-dotnet-howto). Você também pode ler sobre Olá [SDK .NET da pesquisa do Azure](search-howto-dotnet-sdk.md) para um mais detalhado passo a passo do código de exemplo hello.


## <a name="identify-your-azure-search-services-admin-api-key"></a>Identificar a api-key do administrador de seu serviço do Azure Search
Agora que você possua um serviço de pesquisa do Azure, você está quase pronto tooissue solicitações em relação a seu ponto de extremidade de serviço usando o SDK .NET de saudação. Primeiro, você precisará tooobtain um Olá administrador chaves de api que foi gerado para o serviço de pesquisa Olá que você provisionou. Olá .NET SDK enviará esta chave de api em cada solicitação de serviço tooyour. Ter uma chave válida estabelece confiança, em uma base por solicitação, entre solicitação de envio Olá Olá aplicativo e serviço de saudação que lida com ele.

1. toofind chaves de api do serviço, entrar toohello [portal do Azure](https://portal.azure.com/)
2. Vá folha do serviço de pesquisa do Azure tooyour
3. Clique em Olá ícone "Chaves"

O serviço terá *chaves de administração* e *chaves de consulta*.

* O primário e secundário *chaves de administração* conceder direitos totais tooall operações, incluindo Olá capacidade toomanage Olá serviço, criar e excluir índices, indexadores e fontes de dados. Há duas chaves para que você possa continuar chave secundária do toouse Olá se você decidir chave primária do tooregenerate hello e vice-versa.
* O *chaves de consulta* conceder acesso somente leitura tooindexes e documentos, e são normalmente distribuídos tooclient aplicativos que emitem solicitações de pesquisa.

Para fins de saudação de criação de um índice, você pode usar a chave primária ou secundária de administração.

<a name="CreateSearchServiceClient"></a>

## <a name="create-an-instance-of-hello-searchserviceclient-class"></a>Crie uma instância da classe SearchServiceClient de saudação
toostart usando Olá SDK .NET da pesquisa do Azure, você precisará toocreate uma instância do hello `SearchServiceClient` classe. Essa classe tem vários construtores. Olá você deseja usa o nome do serviço de pesquisa e uma `SearchCredentials` objeto como parâmetros. `SearchCredentials` encapsula sua api-key.

Olá código a seguir cria um novo `SearchServiceClient` usando valores para o nome do serviço de pesquisa hello e chave de api que são armazenados no arquivo de configuração do aplicativo hello (`appsettings.json` no caso de saudação de saudação [aplicativo de exemplo](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

O `SearchServiceClient` tem uma propriedade `Indexes`. Esta propriedade fornece todos os métodos de saudação precisar toocreate, lista, atualizar ou excluir os índices de pesquisa do Azure.

> [!NOTE]
> Olá `SearchServiceClient` classe gerencia o serviço de pesquisa de tooyour de conexões. Em ordem tooavoid de abrir um número excessivo de conexões, você deve tentar tooshare uma única instância de `SearchServiceClient` em seu aplicativo, se possível. Seus métodos é thread-safe tooenable esse compartilhamento.
> 
> 

<a name="DefineIndex"></a>

## <a name="define-your-azure-search-index"></a>Defina seu índice do Azure Search
Uma única chamada toohello `Indexes.Create` método criará o índice. Esse método aceita como um parâmetro um objeto `Index` , que define o índice do seu Azure Search. Você precisa toocreate um `Index` de objeto e inicializá-lo da seguinte maneira:

1. Saudação de conjunto `Name` propriedade Olá `Index` toohello nome do índice.
2. Saudação de conjunto `Fields` propriedade Olá `Index` matriz do objeto tooan de `Field` objetos. Olá Olá toocreate da maneira mais fácil `Field` objetos é chamada hello `FieldBuilder.BuildForType` método, passando uma classe de modelo para o parâmetro de tipo hello. Uma classe de modelo tem propriedades que correspondem a campos de toohello do índice. Isso permite que você toobind documentos de seu tooinstances de índice de pesquisa de sua classe de modelo.

> [!NOTE]
> Se você não planeja toouse uma classe de modelo, você ainda pode definir seu índice criando `Field` objetos diretamente. Você pode fornecer o nome de saudação do construtor de toohello campo hello, juntamente com o tipo de dados hello (ou analisador para campos de cadeia de caracteres). Também é possível definir outras propriedades como `IsSearchable`, `IsFilterable`, etc.
>
>

É importante que você mantenha suas necessidades de negócios e experiência de usuário pesquisa em mente ao criar o índice de cada campo deve ser atribuída a saudação [apropriado propriedades](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Essas propriedades de controle que pesquisar recursos (filtragem, facetas, classificação de pesquisa de texto completo, etc.) se aplicam a campos de toowhich. Para qualquer propriedade que você não definir explicitamente, Olá `Field` classe padrões de recurso de pesquisa toodisabling Olá correspondente, a menos que especificamente habilitá-lo.

Para o nosso exemplo, nomeamos o índice "hotels" e definimos os campos usando uma classe de modelo. Cada propriedade da classe de modelo Olá tem atributos que determinam comportamentos de saudação relacionadas à pesquisa de campo de índice correspondente hello. classe de modelo de saudação é definido da seguinte maneira:

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

Escolhemos cuidadosamente atributos Olá para cada propriedade com base em como achamos que serão usados em um aplicativo. Por exemplo, é provável que as pessoas procurando hotéis estaria interessadas correspondências de palavra-chave em Olá `description` campo, portanto é habilitar pesquisa de texto completo para esse campo adicionando Olá `IsSearchable` atributo toohello `Description` propriedade.

Observação exatamente um campo no índice de tipo `string` deve ser Olá designado como Olá *chave* campo adicionando Olá `Key` atributo (consulte `HotelId` no hello exemplo acima).

definição de índice de saudação acima usa um analisador de linguagem para Olá `description_fr` campo porque ele é um texto em francês toostore pretendido. Consulte [tópico de suporte de idioma Olá](https://docs.microsoft.com/rest/api/searchservice/Language-support) , bem como Olá correspondente [postagem de blog](https://azure.microsoft.com/blog/language-support-in-azure-search/) para obter mais informações sobre os analisadores de idioma.

> [!NOTE]
> Por padrão, o nome de saudação de cada propriedade na sua classe de modelo é usado como nome de saudação de campo correspondente do hello no índice de saudação. Se você quiser toomap todos os nomes de campo toocamel caso de nomes de propriedade, marcar a classe Olá Olá `SerializePropertyNamesAsCamelCase` atributo. Se você quiser toomap tooa outro nome, você pode usar o hello `JsonProperty` atributo como Olá `DescriptionFr` propriedade acima. Olá `JsonProperty` atributo tem precedência sobre Olá `SerializePropertyNamesAsCamelCase` atributo.
> 
> 

Agora que definimos uma classe de modelo, podemos criar facilmente uma definição de índice:

```csharp
var definition = new Index()
{
    Name = "hotels",
    Fields = FieldBuilder.BuildForType<Hotel>()
};
```

## <a name="create-hello-index"></a>Criar índice Olá
Agora que você tem uma inicializado `Index` do objeto, você pode criar o índice de saudação simplesmente chamando `Indexes.Create` em seu `SearchServiceClient` objeto:

```csharp
serviceClient.Indexes.Create(definition);
```

Para uma solicitação bem-sucedida, método hello retornará normalmente. Se houver um problema com a solicitação hello como um parâmetro inválido, o método hello lançará `CloudException`.

Quando você terminar com um índice e quiser toodelete-lo, simplesmente chamar hello `Indexes.Delete` método no seu `SearchServiceClient`. Por exemplo, isso é como podemos seria Excluir índice de "hotéis" hello:

```csharp
serviceClient.Indexes.Delete("hotels");
```

> [!NOTE]
> código de exemplo Hello este artigo usa métodos síncronos de saudação do hello SDK .NET da pesquisa do Azure para manter a simplicidade. É recomendável que você use os métodos assíncronos Olá em seu próprios aplicativos tookeep-los, escalonáveis e responsivos. Por exemplo, no hello exemplos anteriormente, você podem usar `CreateAsync` e `DeleteAsync` em vez de `Create` e `Delete`.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Depois de criar um índice de pesquisa do Azure, você estará pronto muito[carregar o conteúdo no índice Olá](search-what-is-data-import.md) para que você pode começar a procurar seus dados.

