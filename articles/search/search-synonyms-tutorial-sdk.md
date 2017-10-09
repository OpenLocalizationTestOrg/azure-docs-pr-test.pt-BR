---
title: aaaSynonyms visualizar tutorial na pesquisa do Azure | Microsoft Docs
description: "Adicione o índice de tooan de recurso de visualização do hello sinônimos na pesquisa do Azure."
services: search
manager: jhubbard
documentationcenter: 
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 055c1cbafb945823a3dc4da0c522db236b1d192c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a>Tutorial C# de sinônimos (visualização) do Azure Search

Sinônimos expandir uma consulta por meio da correspondência em termos considerados termos de entrada toohello semanticamente equivalente. Por exemplo, convém documentos de toomatch "car" que contém termos hello "automóvel" ou "vehicle".

No Azure Search, os sinônimos são definidos em um *mapa de sinônimos*com *regras de mapeamento* que associam os termos equivalentes. Você pode criar vários mapas de sinônimo, postá-los como um índice de tooany disponíveis do recurso de todo o serviço e faça referência a qual um toouse no nível de campo de saudação. No momento da consulta, além de toosearching um índice, a pesquisa do Azure faz uma pesquisa em um mapa de sinônimo, se um for especificado em campos usados na consulta de saudação.

> [!NOTE]
> sinônimos Olá recurso está atualmente em visualização e somente tem suporte no hello visualização mais recente API e versões do SDK (api-version = 2016-09-01-Preview, versão do SDK 4. x-visualização). Não há suporte do portal do Azure no momento. As APIs de visualização não estão no SLA e os recursos da visualização podem mudar, portanto, não recomendamos usá-los nos aplicativos de produção.

## <a name="prerequisites"></a>Pré-requisitos

Requisitos do tutorial incluem o seguinte hello:

* [Visual Studio](https://www.visualstudio.com/downloads/)
* [Serviço do Azure Search](search-create-service-portal.md)
* [Versão de visualização da biblioteca Microsoft.Azure.Search.NET](https://aka.ms/search-sdk-preview)
* [Como o Azure toouse de pesquisa de um aplicativo .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a>Visão geral

Consultas antes e depois demonstram o valor de saudação de sinônimos. Neste tutorial, usamos um aplicativo de exemplo que executa as consultas e retorna os resultados em um índice de exemplo. aplicativo de exemplo Hello cria um índice pequeno denominado "hotéis" preenchidos com dois documentos. aplicativo Hello executa consultas de pesquisa de termos e expressões que não aparecem no índice de saudação de uso, habilita o recurso de sinônimos Olá, e problemas Olá pesquisas mesmo novamente. Olá código a seguir demonstra Olá fluxo geral.

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for hello changes toopropagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");

      Console.ReadKey();
  }
```
Olá toocreate etapas e popular o índice de exemplo hello são explicadas em [como toouse Azure pesquisa de um aplicativo .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).

## <a name="before-queries"></a>Consultas "antes"

Em `RunQueriesWithNonExistentTermsInIndex`, emitimos as consultas de pesquisa com "cinco estrelas", "Internet" e "economia e hotel".
```csharp
Console.WriteLine("Search hello entire index for hello phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
Nenhum dos dois documentos de indexada Olá contêm termos Olá, portanto obtemos seguinte Olá saída de hello primeiro `RunQueriesWithNonExistentTermsInIndex`.
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a>Habilitar sinônimos

A habilitação dos sinônimos é um processo com duas etapas. Vamos primeiro definir e carregar regras do sinônimo e, em seguida, configurar campos toouse-los. Olá processo é descrito em `UploadSynonyms` e `EnableSynonymsInHotelsIndex`.

1. Adicione um serviço de pesquisa de tooyour de mapa de sinônimo. Em `UploadSynonyms`, definimos quatro regras no map sinônimo 'desc synonymmap' e carregar o serviço toohello.
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
Um mapa de sinônimo deve estar de acordo com padrão de código-fonte aberto toohello `solr` formato. formato de saudação é explicado em [sinônimos na pesquisa do Azure](search-synonyms.md) na seção Olá `Apache Solr synonym format`.

2. Configure campos pesquisáveis toouse Olá sinônimo mapa na definição de índice de saudação. Em `EnableSynonymsInHotelsIndex`, habilitamos sinônimos em dois campos `category` e `tags` por configuração Olá `synonymMaps` toohello nome da saudação recentemente carregado mapa de sinônimo.
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
Quando você adiciona um mapa de sinônimos, as recompilações do índice não são necessárias. Você pode adicionar um serviço do sinônimo mapa tooyour e, em seguida, modifique as definições de campo existente em qualquer índice toouse Olá novo sinônimo mapa. adição de saudação de novos atributos não terá impacto na disponibilidade de índice. Olá que mesmo se aplica no desativando sinônimos para um campo. Você pode simplesmente definir Olá `synonymMaps` lista vazia de tooan de propriedade.
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a>Consultas "depois"

Depois de mapa de sinônimo Olá é carregado e índice Olá é mapa de sinônimo Olá toouse atualizado, Olá segundo `RunQueriesWithNonExistentTermsInIndex` chamada produz o seguinte hello:

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
primeira consulta de saudação localiza Olá documento da regra Olá `five star=>luxury`. consulta segundo Olá expande Olá pesquisa com `internet,wifi` e Olá terceiro usando `hotel, motel` e `economy,inexpensive=>budget` na localização de documentos Olá eles correspondentes.

Adicionar sinônimos completamente altera a experiência de pesquisa de saudação. Neste tutorial, consultas original Olá falha resultados significativos tooreturn, mesmo que os documentos de saudação do nosso índice foram relevantes. Habilitando sinônimos, é possível expandir um tooinclude índice termos de uso comum, sem dados de toounderlying alterações no índice de saudação.

## <a name="sample-application-source-code"></a>Código-fonte do aplicativo de exemplo
Você pode encontrar o código-fonte completo Olá Olá do aplicativo de exemplo usado no passo a passo no [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).

## <a name="next-steps"></a>Próximas etapas

* Revisão [como sinônimos toouse na pesquisa do Azure](search-synonyms.md)
* Examine [Documentação API REST dos sinônimos](https://aka.ms/rgm6rq)
* Procurar referências Olá Olá [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) e [API REST](https://docs.microsoft.com/rest/api/searchservice/).
