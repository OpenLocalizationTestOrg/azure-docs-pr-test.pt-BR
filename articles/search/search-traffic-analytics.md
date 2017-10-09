---
title: "aaaSearch análise de tráfego de pesquisa do Azure | Microsoft Docs"
description: "Habilite a análise de tráfego de pesquisa para pesquisa do Azure, um serviço de pesquisa de nuvem hospedado no Microsoft Azure, toounlock insights sobre seus usuários e seus dados."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="939d4-103">O que é análise de tráfego de pesquisa</span><span class="sxs-lookup"><span data-stu-id="939d4-103">What is search traffic analytics</span></span>
<span data-ttu-id="939d4-104">Análise de tráfego de pesquisa é um padrão de implementação de um loop de comentários para seu serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="939d4-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="939d4-105">Esse padrão descreve os dados necessários hello e como toocollect-lo usando o Application Insights, líder de mercado para monitorar serviços em várias plataformas.</span><span class="sxs-lookup"><span data-stu-id="939d4-105">This pattern describes hello necessary data and how toocollect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="939d4-106">A análise de tráfego de pesquisa permite que você ganhe visibilidade em seu serviço de pesquisa e tenha ideias sobre os usuários e seus comportamentos.</span><span class="sxs-lookup"><span data-stu-id="939d4-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="939d4-107">Por meio de dados sobre o que seus usuários escolhem, é possível toomake decisões que melhoram a experiência de pesquisa e tooback off quando os resultados de saudação não são o que esperava.</span><span class="sxs-lookup"><span data-stu-id="939d4-107">By having data about what your users choose, it's possible toomake decisions that further improve your search experience, and tooback off when hello results are not what expected.</span></span>

<span data-ttu-id="939d4-108">A pesquisa do Azure oferece uma solução de telemetria que integra o Power BI e o Azure Application Insights tooprovide detalhada monitoramento e controle.</span><span class="sxs-lookup"><span data-stu-id="939d4-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI tooprovide in-depth monitoring and tracking.</span></span> <span data-ttu-id="939d4-109">Como a interação com a pesquisa do Azure é por meio de APIs, telemetria Olá deve ser implementada por desenvolvedores hello usando a pesquisa, seguindo as instruções de saudação nesta página.</span><span class="sxs-lookup"><span data-stu-id="939d4-109">Because interaction with Azure Search is only through APIs, hello telemetry must be implemented by hello developers using search, following hello instructions in this page.</span></span>

## <a name="identify-hello-relevant-search-data"></a><span data-ttu-id="939d4-110">Identificar dados de pesquisa relevantes Olá</span><span class="sxs-lookup"><span data-stu-id="939d4-110">Identify hello relevant search data</span></span>

<span data-ttu-id="939d4-111">métricas de pesquisa úteis do toohave, é necessário toolog alguns sinais de usuários Olá Olá do aplicativo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="939d4-111">toohave useful search metrics, it's necessary toolog some signals from hello users of hello search application.</span></span> <span data-ttu-id="939d4-112">Estes sinais significam conteúdo que os usuários estão interessados em e que eles considerem precisa tootheir relevante.</span><span class="sxs-lookup"><span data-stu-id="939d4-112">These signals signify content that users are interested in and that they consider relevant tootheir needs.</span></span>

<span data-ttu-id="939d4-113">Há dois sinais necessários para a Análise do Tráfego de Pesquisa:</span><span class="sxs-lookup"><span data-stu-id="939d4-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="939d4-114">Eventos de pesquisa gerados pelo usuário: somente as consultas de pesquisa iniciadas por um usuário são interessantes.</span><span class="sxs-lookup"><span data-stu-id="939d4-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="939d4-115">Pesquisar solicitações usadas toopopulate facetas, o conteúdo adicional ou qualquer informação interna, não são importantes e afetar e influenciar os resultados.</span><span class="sxs-lookup"><span data-stu-id="939d4-115">Search requests used toopopulate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="939d4-116">Eventos de clique gerado pelo usuário: por cliques neste documento, nos referimos tooa usuário selecionar um resultado de pesquisa específica retornado de uma consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="939d4-116">User generated click events: By clicks in this document, we refer tooa user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="939d4-117">Um clique geralmente significa que um documento é um resultado relevante para uma consulta de pesquisa específica.</span><span class="sxs-lookup"><span data-stu-id="939d4-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="939d4-118">Vinculando a pesquisa e clique em eventos com uma id de correlação, é possível tooanalyze comportamentos de saudação de usuários em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="939d4-118">By linking search and click events with a correlation id, it's possible tooanalyze hello behaviors of users on your application.</span></span> <span data-ttu-id="939d4-119">Essas informações de pesquisa são tooobtain impossível com apenas os logs de tráfego de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="939d4-119">These search insights are impossible tooobtain with only search traffic logs.</span></span>

## <a name="how-tooimplement-search-traffic-analytics"></a><span data-ttu-id="939d4-120">Como tooimplement a pesquisa de análise de tráfego</span><span class="sxs-lookup"><span data-stu-id="939d4-120">How tooimplement search traffic analytics</span></span>

<span data-ttu-id="939d4-121">Olá sinais mencionado Olá anterior seção deve ser obtida do aplicativo de pesquisa hello como Olá usuário interagisse com ele.</span><span class="sxs-lookup"><span data-stu-id="939d4-121">hello signals mentioned in hello preceding section must be gathered from hello search application as hello user interacts with it.</span></span> <span data-ttu-id="939d4-122">O Application Insights é uma solução monitoramento extensível, disponível para várias plataformas e com opções flexíveis de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="939d4-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="939d4-123">Uso do Application Insights permite aproveitar os relatórios de pesquisa do Power BI Olá criado pela análise de saudação toomake pesquisa do Azure de dados.</span><span class="sxs-lookup"><span data-stu-id="939d4-123">Usage of Application Insights lets you take advantage of hello Power BI search reports created by Azure Search toomake hello analysis of data easier.</span></span>

<span data-ttu-id="939d4-124">Em Olá [portal](https://portal.azure.com) página para seu serviço de pesquisa do Azure, folha de análise de tráfego de pesquisa Olá contém um roteiro para esse padrão de telemetria.</span><span class="sxs-lookup"><span data-stu-id="939d4-124">In hello [portal](https://portal.azure.com) page for your Azure Search service, hello Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="939d4-125">Também pode selecionar ou criar um recurso do Application Insights e ver os dados necessários hello, em um só lugar.</span><span class="sxs-lookup"><span data-stu-id="939d4-125">You can also select or create an Application Insights resource, and see hello necessary data, all in one place.</span></span>

![Instruções da Análise do Tráfego de Pesquisa][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="939d4-127">1. Selecione um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="939d4-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="939d4-128">Você precisa tooselect um toouse de recurso do Application Insights ou cria um se você não tiver uma.</span><span class="sxs-lookup"><span data-stu-id="939d4-128">You need tooselect an Application Insights resource toouse or create one if you don't have one already.</span></span> <span data-ttu-id="939d4-129">Você pode usar um recurso que já tem em uso toolog Olá necessário eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="939d4-129">You can use a resource that's already in use toolog hello required custom events.</span></span>

<span data-ttu-id="939d4-130">Ao criar um novo recurso do Application Insights, todos os tipos de aplicativo são válidos para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="939d4-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="939d4-131">Selecione Olá um que melhor se adapta plataforma Olá que você está usando.</span><span class="sxs-lookup"><span data-stu-id="939d4-131">Select hello one that best fits hello platform you are using.</span></span>

<span data-ttu-id="939d4-132">Você precisa chave de instrumentação Olá para criar o cliente de telemetria Olá para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="939d4-132">You need hello instrumentation key for creating hello telemetry client for your application.</span></span> <span data-ttu-id="939d4-133">Você pode obtê-lo do painel do portal do Application Insights hello, ou você poderá obtê-lo na página de análise de tráfego de pesquisa hello, selecionando Olá instância toouse.</span><span class="sxs-lookup"><span data-stu-id="939d4-133">You can get it from hello Application Insights portal dashboard, or you can get it from hello Search Traffic Analytics page, selecting hello instance you want toouse.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="939d4-134">2. Instrumentar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="939d4-134">2. Instrument your application</span></span>

<span data-ttu-id="939d4-135">Essa fase é onde você instrumentar seu próprio aplicativo de pesquisa, usando o recurso do Application Insights Olá seu Olá criado na etapa acima.</span><span class="sxs-lookup"><span data-stu-id="939d4-135">This phase is where you instrument your own search application, using hello Application Insights resource your created in hello step above.</span></span> <span data-ttu-id="939d4-136">Há quatro etapas toothis processo:</span><span class="sxs-lookup"><span data-stu-id="939d4-136">There are four steps toothis process:</span></span>

<span data-ttu-id="939d4-137">**I. Criar um cliente de telemetria** é objeto Olá que envia eventos toohello recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="939d4-137">**I. Create a telemetry client** This is hello object that sends events toohello Application Insights Resource.</span></span>

<span data-ttu-id="939d4-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="939d4-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="939d4-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="939d4-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="939d4-140">Para outros idiomas e plataformas, consulte Olá completa [lista](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="939d4-140">For other languages and platforms, see hello complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="939d4-141">**II. Uma ID de pesquisa para correlação da solicitação** toocorrelate pesquisa solicitações com cliques, é necessário toohave uma id de correlação que relaciona esses dois eventos.</span><span class="sxs-lookup"><span data-stu-id="939d4-141">**II. Request a Search ID for correlation** toocorrelate search requests with clicks, it's necessary toohave a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="939d4-142">O Azure Search fornece uma ID de Pesquisa quando você a solicita com um cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="939d4-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="939d4-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="939d4-143">*C#*</span></span>

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="939d4-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="939d4-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="939d4-145">**III. Registrar eventos de pesquisa**</span><span class="sxs-lookup"><span data-stu-id="939d4-145">**III. Log Search events**</span></span>

<span data-ttu-id="939d4-146">Toda vez que uma solicitação de pesquisa é emitida por um usuário, você deveria registrar que um evento de pesquisa com hello esquema a seguir em um evento personalizado do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="939d4-146">Every time that a search request is issued by a user, you should log that as a search event with hello following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="939d4-147">**ServiceName**: nome do serviço de pesquisa (string) **SearchId**: o identificador exclusivo (guid) da consulta de pesquisa de saudação (vem na resposta da pesquisa Olá) **IndexName**: índice de serviço de pesquisa (string) toobe consultado **QueryTerms**: termos de pesquisa (string) inseridos pelo usuário Olá **ResultCount**: (int) o número de documentos que foram retornados (vem na resposta da pesquisa Olá)  **ScoringProfile**: nome (string) de saudação pontuação perfil usado, se houver</span><span class="sxs-lookup"><span data-stu-id="939d4-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello search query (comes in hello search response) **IndexName**: (string) search service index toobe queried **QueryTerms**: (string) search terms entered by hello user **ResultCount**: (int) number of documents that were returned (comes in hello search response) **ScoringProfile**: (string) name of hello scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="939d4-148">Solicitar contagem em consultas de usuário gerado adicionando $count = true tooyour consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="939d4-148">Request count on user generated queries by adding $count=true tooyour search query.</span></span> <span data-ttu-id="939d4-149">Confira mais informações [aqui](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span><span class="sxs-lookup"><span data-stu-id="939d4-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="939d4-150">Lembre-se de consultas de pesquisa de log de tooonly que são geradas pelos usuários.</span><span class="sxs-lookup"><span data-stu-id="939d4-150">Remember tooonly log search queries that are generated by users.</span></span>
>

<span data-ttu-id="939d4-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="939d4-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="939d4-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="939d4-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="939d4-153">**IV. Registrar eventos de clique**</span><span class="sxs-lookup"><span data-stu-id="939d4-153">**IV. Log Click events**</span></span>

<span data-ttu-id="939d4-154">Sempre que um usuário clica em um documento, esse é um sinal que deve ser registrado para fins de análise de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="939d4-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="939d4-155">Use toolog de eventos personalizados do Application Insights esses eventos com hello esquema a seguir:</span><span class="sxs-lookup"><span data-stu-id="939d4-155">Use Application Insights custom events toolog these events with hello following schema:</span></span>

<span data-ttu-id="939d4-156">**ServiceName**: nome do serviço de pesquisa (string) **SearchId**: o identificador exclusivo (guid) de consulta de pesquisa relacionada Olá **DocId**: identificador de documento (string) **posição** : página de resultados de classificação (int) do documento hello na pesquisa de saudação</span><span class="sxs-lookup"><span data-stu-id="939d4-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello related search query **DocId**: (string) document identifier **Position**: (int) rank of hello document in hello search results page</span></span>

> [!NOTE]
> <span data-ttu-id="939d4-157">Posição refere-se a ordem de toohello cardeal em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="939d4-157">Position refers toohello cardinal order in your application.</span></span> <span data-ttu-id="939d4-158">Você é livre tooset esse número, desde que ele sempre tem Olá mesmo, tooallow para comparação.</span><span class="sxs-lookup"><span data-stu-id="939d4-158">You are free tooset this number, as long as it's always hello same, tooallow for comparison.</span></span>
>

<span data-ttu-id="939d4-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="939d4-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="939d4-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="939d4-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="939d4-161">3. Analisar com o Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="939d4-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="939d4-162">Após ter instrumentado seu aplicativo e verificar que seu aplicativo está conectado corretamente tooApplication Insights, você pode usar um modelo predefinido criado pela pesquisa do Azure para o Power BI desktop.</span><span class="sxs-lookup"><span data-stu-id="939d4-162">After you have instrumented your app and verified your application is correctly connected tooApplication Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="939d4-163">Este modelo contém gráficos e tabelas que ajudarão a fazem tooimprove de decisões mais fundamentada o desempenho da pesquisa e a relevância.</span><span class="sxs-lookup"><span data-stu-id="939d4-163">This template contains charts and tables that help you make more informed decisions tooimprove your search performance and relevance.</span></span>

<span data-ttu-id="939d4-164">modelo da área de trabalho do tooinstantiate Olá Power BI, você precisará de três informações sobre o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="939d4-164">tooinstantiate hello Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="939d4-165">Esses dados podem ser encontrados na página de análise de tráfego de pesquisa hello, quando você seleciona Olá recursos toouse</span><span class="sxs-lookup"><span data-stu-id="939d4-165">This data can be found in hello Search Traffic Analytics page, when you select hello resource toouse</span></span>

![Dados do Application Insights na folha de análise de tráfego de pesquisa Olá][2]

<span data-ttu-id="939d4-167">Métricas incluídas no modelo da área de trabalho do Power BI hello:</span><span class="sxs-lookup"><span data-stu-id="939d4-167">Metrics included in hello Power BI desktop template:</span></span>

*   <span data-ttu-id="939d4-168">Clique em por meio de taxa (CTR): taxa de usuários que clicar em um número de toohello de documento específico de pesquisas de total.</span><span class="sxs-lookup"><span data-stu-id="939d4-168">Click through Rate (CTR): ratio of users who click on a specific document toohello number of total searches.</span></span>
*   <span data-ttu-id="939d4-169">Pesquisa sem cliques: termos das principais consultas que não registraram nenhum clique</span><span class="sxs-lookup"><span data-stu-id="939d4-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="939d4-170">Clicado mais documentos: clicado mais documentos por ID em Olá últimas 24 horas, 7 dias e 30 dias.</span><span class="sxs-lookup"><span data-stu-id="939d4-170">Most clicked documents: most clicked documents by ID in hello last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="939d4-171">Pares de documento de termo populares: termos que resultam em Olá mesmo documento é clicado, ordenados por cliques.</span><span class="sxs-lookup"><span data-stu-id="939d4-171">Popular term-document pairs: terms that result in hello same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="939d4-172">Tempo tooclick: cliques classificados pelo tempo desde a consulta de pesquisa Olá</span><span class="sxs-lookup"><span data-stu-id="939d4-172">Time tooclick: clicks bucketed by time since hello search query</span></span>

![Modelo do Power BI para leitura do Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="939d4-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="939d4-174">Next Steps</span></span>
<span data-ttu-id="939d4-175">Instrumentar seu aplicativo tooget avançado e criteriosos dados de pesquisa sobre o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="939d4-175">Instrument your search application tooget powerful and insightful data about your search service.</span></span>

<span data-ttu-id="939d4-176">Encontre mais informações sobre o Application Insights [aqui](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="939d4-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="939d4-177">Visite o Application Insights [página de preços](https://azure.microsoft.com/pricing/details/application-insights/) toolearn mais informações sobre seus diferentes camadas de serviço.</span><span class="sxs-lookup"><span data-stu-id="939d4-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) toolearn more about their different service tiers.</span></span>

<span data-ttu-id="939d4-178">Saiba mais sobre como criar relatórios incríveis.</span><span class="sxs-lookup"><span data-stu-id="939d4-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="939d4-179">Confira [Introdução ao Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) para obter detalhes</span><span class="sxs-lookup"><span data-stu-id="939d4-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
