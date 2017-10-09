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
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="040c6-103">Tutorial C# de sinônimos (visualização) do Azure Search</span><span class="sxs-lookup"><span data-stu-id="040c6-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="040c6-104">Sinônimos expandir uma consulta por meio da correspondência em termos considerados termos de entrada toohello semanticamente equivalente.</span><span class="sxs-lookup"><span data-stu-id="040c6-104">Synonyms expand a query by matching on terms considered semantically equivalent toohello input term.</span></span> <span data-ttu-id="040c6-105">Por exemplo, convém documentos de toomatch "car" que contém termos hello "automóvel" ou "vehicle".</span><span class="sxs-lookup"><span data-stu-id="040c6-105">For example, you might want "car" toomatch documents containing hello terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="040c6-106">No Azure Search, os sinônimos são definidos em um *mapa de sinônimos*com *regras de mapeamento* que associam os termos equivalentes.</span><span class="sxs-lookup"><span data-stu-id="040c6-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="040c6-107">Você pode criar vários mapas de sinônimo, postá-los como um índice de tooany disponíveis do recurso de todo o serviço e faça referência a qual um toouse no nível de campo de saudação.</span><span class="sxs-lookup"><span data-stu-id="040c6-107">You can create multiple synonym maps, post them as a service-wide resource available tooany index, and then reference which one toouse at hello field level.</span></span> <span data-ttu-id="040c6-108">No momento da consulta, além de toosearching um índice, a pesquisa do Azure faz uma pesquisa em um mapa de sinônimo, se um for especificado em campos usados na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="040c6-108">At query time, in addition toosearching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="040c6-109">sinônimos Olá recurso está atualmente em visualização e somente tem suporte no hello visualização mais recente API e versões do SDK (api-version = 2016-09-01-Preview, versão do SDK 4. x-visualização).</span><span class="sxs-lookup"><span data-stu-id="040c6-109">hello synonyms feature is currently in preview and only supported in hello latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="040c6-110">Não há suporte do portal do Azure no momento.</span><span class="sxs-lookup"><span data-stu-id="040c6-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="040c6-111">As APIs de visualização não estão no SLA e os recursos da visualização podem mudar, portanto, não recomendamos usá-los nos aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="040c6-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="040c6-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="040c6-112">Prerequisites</span></span>

<span data-ttu-id="040c6-113">Requisitos do tutorial incluem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="040c6-113">Tutorial requirements include hello following:</span></span>

* [<span data-ttu-id="040c6-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="040c6-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="040c6-115">Serviço do Azure Search</span><span class="sxs-lookup"><span data-stu-id="040c6-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="040c6-116">Versão de visualização da biblioteca Microsoft.Azure.Search.NET</span><span class="sxs-lookup"><span data-stu-id="040c6-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="040c6-117">Como o Azure toouse de pesquisa de um aplicativo .NET</span><span class="sxs-lookup"><span data-stu-id="040c6-117">How toouse Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="040c6-118">Visão geral</span><span class="sxs-lookup"><span data-stu-id="040c6-118">Overview</span></span>

<span data-ttu-id="040c6-119">Consultas antes e depois demonstram o valor de saudação de sinônimos.</span><span class="sxs-lookup"><span data-stu-id="040c6-119">Before-and-after queries demonstrate hello value of synonyms.</span></span> <span data-ttu-id="040c6-120">Neste tutorial, usamos um aplicativo de exemplo que executa as consultas e retorna os resultados em um índice de exemplo.</span><span class="sxs-lookup"><span data-stu-id="040c6-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="040c6-121">aplicativo de exemplo Hello cria um índice pequeno denominado "hotéis" preenchidos com dois documentos.</span><span class="sxs-lookup"><span data-stu-id="040c6-121">hello sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="040c6-122">aplicativo Hello executa consultas de pesquisa de termos e expressões que não aparecem no índice de saudação de uso, habilita o recurso de sinônimos Olá, e problemas Olá pesquisas mesmo novamente.</span><span class="sxs-lookup"><span data-stu-id="040c6-122">hello application executes search queries using terms and phrases that do not appear in hello index, enables hello synonyms feature, then issues hello same searches again.</span></span> <span data-ttu-id="040c6-123">Olá código a seguir demonstra Olá fluxo geral.</span><span class="sxs-lookup"><span data-stu-id="040c6-123">hello code below demonstrates hello overall flow.</span></span>

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
<span data-ttu-id="040c6-124">Olá toocreate etapas e popular o índice de exemplo hello são explicadas em [como toouse Azure pesquisa de um aplicativo .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="040c6-124">hello steps toocreate and populate hello sample index are explained in [How toouse Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="040c6-125">Consultas "antes"</span><span class="sxs-lookup"><span data-stu-id="040c6-125">"Before" queries</span></span>

<span data-ttu-id="040c6-126">Em `RunQueriesWithNonExistentTermsInIndex`, emitimos as consultas de pesquisa com "cinco estrelas", "Internet" e "economia e hotel".</span><span class="sxs-lookup"><span data-stu-id="040c6-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
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
<span data-ttu-id="040c6-127">Nenhum dos dois documentos de indexada Olá contêm termos Olá, portanto obtemos seguinte Olá saída de hello primeiro `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="040c6-127">Neither of hello two indexed documents contain hello terms, so we get hello following output from hello first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="040c6-128">Habilitar sinônimos</span><span class="sxs-lookup"><span data-stu-id="040c6-128">Enable synonyms</span></span>

<span data-ttu-id="040c6-129">A habilitação dos sinônimos é um processo com duas etapas.</span><span class="sxs-lookup"><span data-stu-id="040c6-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="040c6-130">Vamos primeiro definir e carregar regras do sinônimo e, em seguida, configurar campos toouse-los.</span><span class="sxs-lookup"><span data-stu-id="040c6-130">We first define and upload synonym rules and then configure fields toouse them.</span></span> <span data-ttu-id="040c6-131">Olá processo é descrito em `UploadSynonyms` e `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="040c6-131">hello process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="040c6-132">Adicione um serviço de pesquisa de tooyour de mapa de sinônimo.</span><span class="sxs-lookup"><span data-stu-id="040c6-132">Add a synonym map tooyour search service.</span></span> <span data-ttu-id="040c6-133">Em `UploadSynonyms`, definimos quatro regras no map sinônimo 'desc synonymmap' e carregar o serviço toohello.</span><span class="sxs-lookup"><span data-stu-id="040c6-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload toohello service.</span></span>
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
<span data-ttu-id="040c6-134">Um mapa de sinônimo deve estar de acordo com padrão de código-fonte aberto toohello `solr` formato.</span><span class="sxs-lookup"><span data-stu-id="040c6-134">A synonym map must conform toohello open source standard `solr` format.</span></span> <span data-ttu-id="040c6-135">formato de saudação é explicado em [sinônimos na pesquisa do Azure](search-synonyms.md) na seção Olá `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="040c6-135">hello format is explained in [Synonyms in Azure Search](search-synonyms.md) under hello section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="040c6-136">Configure campos pesquisáveis toouse Olá sinônimo mapa na definição de índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="040c6-136">Configure searchable fields toouse hello synonym map in hello index definition.</span></span> <span data-ttu-id="040c6-137">Em `EnableSynonymsInHotelsIndex`, habilitamos sinônimos em dois campos `category` e `tags` por configuração Olá `synonymMaps` toohello nome da saudação recentemente carregado mapa de sinônimo.</span><span class="sxs-lookup"><span data-stu-id="040c6-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting hello `synonymMaps` property toohello name of hello newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="040c6-138">Quando você adiciona um mapa de sinônimos, as recompilações do índice não são necessárias.</span><span class="sxs-lookup"><span data-stu-id="040c6-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="040c6-139">Você pode adicionar um serviço do sinônimo mapa tooyour e, em seguida, modifique as definições de campo existente em qualquer índice toouse Olá novo sinônimo mapa.</span><span class="sxs-lookup"><span data-stu-id="040c6-139">You can add a synonym map tooyour service, and then amend existing field definitions in any index toouse hello new synonym map.</span></span> <span data-ttu-id="040c6-140">adição de saudação de novos atributos não terá impacto na disponibilidade de índice.</span><span class="sxs-lookup"><span data-stu-id="040c6-140">hello addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="040c6-141">Olá que mesmo se aplica no desativando sinônimos para um campo.</span><span class="sxs-lookup"><span data-stu-id="040c6-141">hello same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="040c6-142">Você pode simplesmente definir Olá `synonymMaps` lista vazia de tooan de propriedade.</span><span class="sxs-lookup"><span data-stu-id="040c6-142">You can simply set hello `synonymMaps` property tooan empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="040c6-143">Consultas "depois"</span><span class="sxs-lookup"><span data-stu-id="040c6-143">"After" queries</span></span>

<span data-ttu-id="040c6-144">Depois de mapa de sinônimo Olá é carregado e índice Olá é mapa de sinônimo Olá toouse atualizado, Olá segundo `RunQueriesWithNonExistentTermsInIndex` chamada produz o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="040c6-144">After hello synonym map is uploaded and hello index is updated toouse hello synonym map, hello second `RunQueriesWithNonExistentTermsInIndex` call outputs hello following:</span></span>

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="040c6-145">primeira consulta de saudação localiza Olá documento da regra Olá `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="040c6-145">hello first query finds hello document from hello rule `five star=>luxury`.</span></span> <span data-ttu-id="040c6-146">consulta segundo Olá expande Olá pesquisa com `internet,wifi` e Olá terceiro usando `hotel, motel` e `economy,inexpensive=>budget` na localização de documentos Olá eles correspondentes.</span><span class="sxs-lookup"><span data-stu-id="040c6-146">hello second query expands hello search using `internet,wifi` and hello third using both `hotel, motel` and `economy,inexpensive=>budget` in finding hello documents they matched.</span></span>

<span data-ttu-id="040c6-147">Adicionar sinônimos completamente altera a experiência de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="040c6-147">Adding synonyms completely changes hello search experience.</span></span> <span data-ttu-id="040c6-148">Neste tutorial, consultas original Olá falha resultados significativos tooreturn, mesmo que os documentos de saudação do nosso índice foram relevantes.</span><span class="sxs-lookup"><span data-stu-id="040c6-148">In this tutorial, hello original queries failed tooreturn meaningful results even though hello documents in our index were relevant.</span></span> <span data-ttu-id="040c6-149">Habilitando sinônimos, é possível expandir um tooinclude índice termos de uso comum, sem dados de toounderlying alterações no índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="040c6-149">By enabling synonyms, we can expand an index tooinclude terms in common use, with no changes toounderlying data in hello index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="040c6-150">Código-fonte do aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="040c6-150">Sample application source code</span></span>
<span data-ttu-id="040c6-151">Você pode encontrar o código-fonte completo Olá Olá do aplicativo de exemplo usado no passo a passo no [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="040c6-151">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="040c6-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="040c6-152">Next steps</span></span>

* <span data-ttu-id="040c6-153">Revisão [como sinônimos toouse na pesquisa do Azure](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="040c6-153">Review [How toouse synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="040c6-154">Examine [Documentação API REST dos sinônimos](https://aka.ms/rgm6rq)</span><span class="sxs-lookup"><span data-stu-id="040c6-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="040c6-155">Procurar referências Olá Olá [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) e [API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="040c6-155">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
