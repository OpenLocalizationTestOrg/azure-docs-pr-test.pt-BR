---
title: "AAA \"consultar um índice (API .NET - pesquisa do Azure) | Microsoft Docs\""
description: "Criar uma consulta de pesquisa na pesquisa do Azure e usar os resultados da pesquisa pesquisa parâmetros toofilter e classificação."
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 8b3ba1cd1270aad038fb48d9053fcff35d243e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a>Consultar seu índice de pesquisa do Azure usando o SDK .NET de saudação
> [!div class="op_single_selector"]
> * [Visão geral](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Este artigo mostra como tooquery um índice usando Olá [SDK .NET da pesquisa do Azure](https://aka.ms/search-sdk).

Antes de começar este passo a passo, você já deve ter [criado um índice do Azure Search](search-what-is-an-index.md), e este já deve estar [preenchido com os dados](search-what-is-data-import.md).

> [!NOTE]
> Todos os códigos de exemplo neste artigo foram escritos em C#. Você pode encontrar o código-fonte completo Olá [no GitHub](http://aka.ms/search-dotnet-howto). Você também pode ler sobre Olá [SDK .NET da pesquisa do Azure](search-howto-dotnet-sdk.md) para um mais detalhado passo a passo do código de exemplo hello.

## <a name="identify-your-azure-search-services-query-api-key"></a>Identificar sua api-key de consulta do serviço de Pesquisa do Azure
Agora que você criou um índice de pesquisa do Azure, você está quase pronto tooissue consultas usando Olá SDK do .NET. Primeiro, você precisará tooobtain uma saudação consulta chaves de api que foi gerado para o serviço de pesquisa Olá que você provisionou. Olá .NET SDK enviará esta chave de api em cada solicitação de serviço tooyour. Ter uma chave válida estabelece confiança, em uma base por solicitação, entre solicitação de envio Olá Olá aplicativo e serviço de saudação que lida com ele.

1. toofind chaves do serviço de api pode entrar toohello [portal do Azure](https://portal.azure.com/)
2. Vá folha do serviço de pesquisa do Azure tooyour
3. Clique em Olá ícone "Chaves"

O serviço terá *chaves de administração* e *chaves de consulta*.

* O primário e secundário *chaves de administração* conceder direitos totais tooall operações, incluindo Olá capacidade toomanage Olá serviço, criar e excluir índices, indexadores e fontes de dados. Há duas chaves para que você possa continuar chave secundária do toouse Olá se você decidir chave primária do tooregenerate hello e vice-versa.
* O *chaves de consulta* conceder acesso somente leitura tooindexes e documentos, e são normalmente distribuídos tooclient aplicativos que emitem solicitações de pesquisa.

Para fins de saudação de consultar um índice, você pode usar uma de suas chaves de consulta. As chaves de administração também podem ser usadas para consultas, mas você deve usar uma chave de consulta no código do aplicativo, isso melhor da seguinte maneira Olá [princípio de menos privilégios](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Crie uma instância da classe SearchIndexClient de saudação
consultas de tooissue com hello SDK .NET da pesquisa do Azure, você precisará toocreate uma instância de saudação `SearchIndexClient` classe. Essa classe tem vários construtores. Olá você deseja usa o nome do serviço de pesquisa, o nome do índice e uma `SearchCredentials` objeto como parâmetros. `SearchCredentials` encapsula sua api-key.

Olá código a seguir cria um novo `SearchIndexClient` para índice de "hotéis" hello (criado em [criar um índice de pesquisa do Azure usando o SDK .NET de saudação](search-create-index-dotnet.md)) usando valores para o nome do serviço de pesquisa hello e chave de api que são armazenados na configuração do aplicativo hello arquivo (`appsettings.json` no caso de saudação de saudação [aplicativo de exemplo](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

`SearchIndexClient` tem uma propriedade `Documents`. Esta propriedade fornece que todos os Olá métodos que você precisa tooquery índices de pesquisa do Azure.

## <a name="query-your-index"></a>Consultar o índice
Pesquisando com hello .NET SDK é tão simple quanto Olá chamada `Documents.Search` método no seu `SearchIndexClient`. Este método usa alguns parâmetros, incluindo o texto de pesquisa hello, juntamente com um `SearchParameters` objeto que pode ser usado toofurther refinar Olá consulta.

#### <a name="types-of-queries"></a>Tipos de Consultas
principal Olá dois [tipos de consulta](search-query-overview.md#types-of-queries) você usará são `search` e `filter`. Uma consulta `search` procura um ou mais termos em todos os campos *pesquisáveis* no índice. Uma consulta `filter` avalia uma expressão booliana em todos os campos *filtráveis* em um índice.

Pesquisa e filtros são executados usando Olá `Documents.Search` método. Uma consulta de pesquisa pode ser passada no hello `searchText` parâmetro, enquanto uma expressão de filtro pode ser passada em Olá `Filter` propriedade Olá `SearchParameters` classe. toofilter sem procurando, basta passar `"*"` para Olá `searchText` parâmetro. toosearch sem filtragem, deixe Olá `Filter` propriedade unset, ou não passar um `SearchParameters` instância em todos os.

#### <a name="example-queries"></a>Consultas de Exemplo
Olá, código de exemplo a seguir mostra algumas maneiras diferentes tooquery hello "hotéis" índice definido na [criar um índice de pesquisa do Azure usando o SDK .NET de saudação](search-create-index-dotnet.md#DefineIndex). Observe que os documentos Olá retornados com os resultados da pesquisa Olá são instâncias de saudação `Hotel` classe, que foi definida no [importação de dados de pesquisa do Azure usando Olá .NET SDK](search-import-data-dotnet.md#HotelClass). Olá código de exemplo usa um `WriteDocuments` console toohello resultados de pesquisa do método toooutput hello. Esse método é descrito na próxima seção, Olá.

```csharp
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
```

## <a name="handle-search-results"></a>Controlar os resultados da pesquisa
Olá `Documents.Search` método retorna um `DocumentSearchResult` objeto que contém Olá resultados de consulta de saudação. exemplo Hello na seção anterior Olá usado um método chamado `WriteDocuments` console toohello de resultados de pesquisa do toooutput hello:

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

Aqui está o que os resultados de saudação aparência para consultas de saudação na seção anterior hello, assumindo índice de hotéis"hello" é populado com dados de exemplo hello no [importação de dados de pesquisa do Azure usando Olá .NET SDK](search-import-data-dotnet.md):

```
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
```

Olá exemplo de código acima usa os resultados da pesquisa Olá console toooutput. Da mesma forma, você precisará toodisplay resultados da pesquisa em seu próprio aplicativo. Consulte [Este exemplo no GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) para obter um exemplo de como os resultados de pesquisa toorender em um aplicativo web do ASP.NET MVC.

