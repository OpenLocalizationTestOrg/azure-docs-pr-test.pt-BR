---
title: "Análise de tráfego de pesquisa para o Azure Search | Microsoft Docs"
description: "Habilite a análise de tráfego de pesquisa para a pesquisa do Azure, um serviço de pesquisa hospedado na nuvem no Microsoft Azure, para ter ideias sobre os usuários e seus dados."
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
ms.openlocfilehash: 303ca5c820f573dc0b58f1910f258403c3baad2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="3629f-103">O que é análise de tráfego de pesquisa</span><span class="sxs-lookup"><span data-stu-id="3629f-103">What is search traffic analytics</span></span>
<span data-ttu-id="3629f-104">Análise de tráfego de pesquisa é um padrão de implementação de um loop de comentários para seu serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3629f-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="3629f-105">Esse padrão descreve os dados necessários e como coletá-los usando o Application Insights, líder no setor de serviços de monitoramento em várias plataformas.</span><span class="sxs-lookup"><span data-stu-id="3629f-105">This pattern describes the necessary data and how to collect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="3629f-106">A análise de tráfego de pesquisa permite que você ganhe visibilidade em seu serviço de pesquisa e tenha ideias sobre os usuários e seus comportamentos.</span><span class="sxs-lookup"><span data-stu-id="3629f-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="3629f-107">A coleta de dados sobre as escolhas dos usuários permite que você tome decisões que melhoram ainda mais sua experiência de pesquisa e recue quando os resultados não forem o esperado.</span><span class="sxs-lookup"><span data-stu-id="3629f-107">By having data about what your users choose, it's possible to make decisions that further improve your search experience, and to back off when the results are not what expected.</span></span>

<span data-ttu-id="3629f-108">O Azure Search oferece uma solução de telemetria que integra o Azure Application Insights e o Power BI para fornecer monitoramento e rastreamento detalhado.</span><span class="sxs-lookup"><span data-stu-id="3629f-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI to provide in-depth monitoring and tracking.</span></span> <span data-ttu-id="3629f-109">Como a interação com o Azure Search ocorre apenas por meio de APIs, a telemetria deve ser implementada pelos desenvolvedores usando a pesquisa, seguindo as instruções nesta página.</span><span class="sxs-lookup"><span data-stu-id="3629f-109">Because interaction with Azure Search is only through APIs, the telemetry must be implemented by the developers using search, following the instructions in this page.</span></span>

## <a name="identify-the-relevant-search-data"></a><span data-ttu-id="3629f-110">Identificar os dados de pesquisa relevantes</span><span class="sxs-lookup"><span data-stu-id="3629f-110">Identify the relevant search data</span></span>

<span data-ttu-id="3629f-111">Para ter métricas de pesquisa úteis, é necessário registrar alguns sinais dos usuários do aplicativo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3629f-111">To have useful search metrics, it's necessary to log some signals from the users of the search application.</span></span> <span data-ttu-id="3629f-112">Esses sinais indicam o conteúdo no qual os usuários estão interessados e que eles consideraram relevantes para suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="3629f-112">These signals signify content that users are interested in and that they consider relevant to their needs.</span></span>

<span data-ttu-id="3629f-113">Há dois sinais necessários para a Análise do Tráfego de Pesquisa:</span><span class="sxs-lookup"><span data-stu-id="3629f-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="3629f-114">Eventos de pesquisa gerados pelo usuário: somente as consultas de pesquisa iniciadas por um usuário são interessantes.</span><span class="sxs-lookup"><span data-stu-id="3629f-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="3629f-115">Solicitações de pesquisa usadas para preencher facetas, conteúdo adicional ou qualquer informação interna, não são importantes e distorcem e influenciam seus resultados.</span><span class="sxs-lookup"><span data-stu-id="3629f-115">Search requests used to populate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="3629f-116">Eventos de clique gerados pelo usuário: neste documento, cliques se referem a um usuário que seleciona um resultado de pesquisa específico retornado de uma consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3629f-116">User generated click events: By clicks in this document, we refer to a user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="3629f-117">Um clique geralmente significa que um documento é um resultado relevante para uma consulta de pesquisa específica.</span><span class="sxs-lookup"><span data-stu-id="3629f-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="3629f-118">Ao vincular eventos de pesquisa e de clique a uma ID de correlação, é possível analisar os comportamentos dos usuários em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3629f-118">By linking search and click events with a correlation id, it's possible to analyze the behaviors of users on your application.</span></span> <span data-ttu-id="3629f-119">Essas informações de pesquisa são impossíveis de obter apenas com os logs de tráfego de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3629f-119">These search insights are impossible to obtain with only search traffic logs.</span></span>

## <a name="how-to-implement-search-traffic-analytics"></a><span data-ttu-id="3629f-120">Como implementar a análise de tráfego de pesquisa</span><span class="sxs-lookup"><span data-stu-id="3629f-120">How to implement search traffic analytics</span></span>

<span data-ttu-id="3629f-121">Os sinais mencionados na seção anterior devem ser coletados do aplicativo de pesquisa à medida que o usuário interage com ele.</span><span class="sxs-lookup"><span data-stu-id="3629f-121">The signals mentioned in the preceding section must be gathered from the search application as the user interacts with it.</span></span> <span data-ttu-id="3629f-122">O Application Insights é uma solução monitoramento extensível, disponível para várias plataformas e com opções flexíveis de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="3629f-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="3629f-123">O uso do Application Insights permite que você aproveite os relatórios de pesquisa do Power BI criados pelo Azure Search para facilitar a análise de dados.</span><span class="sxs-lookup"><span data-stu-id="3629f-123">Usage of Application Insights lets you take advantage of the Power BI search reports created by Azure Search to make the analysis of data easier.</span></span>

<span data-ttu-id="3629f-124">Na página do [Portal](https://portal.azure.com) de seu serviço Azure Search, a folha Análise de Tráfego de Pesquisa contém uma folha de consulta para seguir este padrão de telemetria.</span><span class="sxs-lookup"><span data-stu-id="3629f-124">In the [portal](https://portal.azure.com) page for your Azure Search service, the Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="3629f-125">Também é possível selecionar ou criar um recurso do Application Insights e ver os dados necessários, tudo em um só lugar.</span><span class="sxs-lookup"><span data-stu-id="3629f-125">You can also select or create an Application Insights resource, and see the necessary data, all in one place.</span></span>

![Instruções da Análise do Tráfego de Pesquisa][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="3629f-127">1. Selecione um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="3629f-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="3629f-128">Você precisa selecionar um recurso do Application Insights para uso ou criar um, caso você não tenha um.</span><span class="sxs-lookup"><span data-stu-id="3629f-128">You need to select an Application Insights resource to use or create one if you don't have one already.</span></span> <span data-ttu-id="3629f-129">Você pode usar um recurso que já está sendo usado para registrar os eventos personalizados necessários.</span><span class="sxs-lookup"><span data-stu-id="3629f-129">You can use a resource that's already in use to log the required custom events.</span></span>

<span data-ttu-id="3629f-130">Ao criar um novo recurso do Application Insights, todos os tipos de aplicativo são válidos para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="3629f-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="3629f-131">Selecione aquele que melhor se adapta a plataforma que você está usando.</span><span class="sxs-lookup"><span data-stu-id="3629f-131">Select the one that best fits the platform you are using.</span></span>

<span data-ttu-id="3629f-132">Você precisa da chave de instrumentação para criar o cliente de telemetria para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3629f-132">You need the instrumentation key for creating the telemetry client for your application.</span></span> <span data-ttu-id="3629f-133">Você pode obtê-la no painel do portal do Application Insights, ou você pode obtê-la na página da Análise do Tráfego de Pesquisa, selecionando a instância que você quer usar.</span><span class="sxs-lookup"><span data-stu-id="3629f-133">You can get it from the Application Insights portal dashboard, or you can get it from the Search Traffic Analytics page, selecting the instance you want to use.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="3629f-134">2. Instrumentar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="3629f-134">2. Instrument your application</span></span>

<span data-ttu-id="3629f-135">É nessa fase que você instrumenta seu próprio aplicativo de pesquisa, usando o recurso Application Insights criado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="3629f-135">This phase is where you instrument your own search application, using the Application Insights resource your created in the step above.</span></span> <span data-ttu-id="3629f-136">Há quatro etapas nesse processo:</span><span class="sxs-lookup"><span data-stu-id="3629f-136">There are four steps to this process:</span></span>

<span data-ttu-id="3629f-137">**I. Criar um cliente de telemetria** Esse é o objeto que envia eventos ao recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3629f-137">**I. Create a telemetry client** This is the object that sends events to the Application Insights Resource.</span></span>

<span data-ttu-id="3629f-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="3629f-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="3629f-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3629f-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="3629f-140">Para outras plataformas e linguagens, consulte a [lista completa](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="3629f-140">For other languages and platforms, see the complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="3629f-141">**II. Solicitar uma ID de Pesquisa para correlação** Para correlacionar as solicitações de pesquisa com cliques, é necessário ter uma ID de correlação que relacione esses dois eventos distintos.</span><span class="sxs-lookup"><span data-stu-id="3629f-141">**II. Request a Search ID for correlation** To correlate search requests with clicks, it's necessary to have a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="3629f-142">O Azure Search fornece uma ID de Pesquisa quando você a solicita com um cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="3629f-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="3629f-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="3629f-143">*C#*</span></span>

    // This sample uses the Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="3629f-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3629f-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="3629f-145">**III. Registrar eventos de pesquisa**</span><span class="sxs-lookup"><span data-stu-id="3629f-145">**III. Log Search events**</span></span>

<span data-ttu-id="3629f-146">Sempre que uma solicitação de pesquisa é emitida por um usuário, você deve registrá-la como um evento de pesquisa com o esquema a seguir em um evento personalizado do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="3629f-146">Every time that a search request is issued by a user, you should log that as a search event with the following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="3629f-147">**ServiceName**: (cadeia de caracteres) nome do serviço de pesquisa **SearchId**: (guid) identificador exclusivo da consulta de pesquisa (aparece na resposta da pesquisa) **IndexName**: (cadeia de caracteres) índice do serviço de pesquisa a ser consultado **QueryTerms**: (cadeia de caracteres) termos de pesquisa inseridos pelo usuário **ResultCount**: (int) número de documentos retornados (aparece na resposta da pesquisa) **ScoringProfile**: (cadeia de caracteres) nome do perfil de pontuação usado, se houver algum</span><span class="sxs-lookup"><span data-stu-id="3629f-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the search query (comes in the search response) **IndexName**: (string) search service index to be queried **QueryTerms**: (string) search terms entered by the user **ResultCount**: (int) number of documents that were returned (comes in the search response) **ScoringProfile**: (string) name of the scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="3629f-148">Solicite a contagem de consultas geradas pelo usuário adicionando $count=true à consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3629f-148">Request count on user generated queries by adding $count=true to your search query.</span></span> <span data-ttu-id="3629f-149">Confira mais informações [aqui](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span><span class="sxs-lookup"><span data-stu-id="3629f-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="3629f-150">Lembre-se de registrar apenas as consultas de pesquisa geradas pelos usuários.</span><span class="sxs-lookup"><span data-stu-id="3629f-150">Remember to only log search queries that are generated by users.</span></span>
>

<span data-ttu-id="3629f-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="3629f-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="3629f-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3629f-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="3629f-153">**IV. Registrar eventos de clique**</span><span class="sxs-lookup"><span data-stu-id="3629f-153">**IV. Log Click events**</span></span>

<span data-ttu-id="3629f-154">Sempre que um usuário clica em um documento, esse é um sinal que deve ser registrado para fins de análise de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3629f-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="3629f-155">Use os eventos personalizados do Application Insights para registrar esses eventos com o esquema a seguir:</span><span class="sxs-lookup"><span data-stu-id="3629f-155">Use Application Insights custom events to log these events with the following schema:</span></span>

<span data-ttu-id="3629f-156">**ServiceName**: (cadeia de caracteres) nome do serviço de pesquisa **SearchId**: (guid) identificador exclusivo da consulta de pesquisa relacionada **DocId**: (cadeia de caracteres) identificador do documento **Position**: (int) classificação do documento na página de resultados da pesquisa</span><span class="sxs-lookup"><span data-stu-id="3629f-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the related search query **DocId**: (string) document identifier **Position**: (int) rank of the document in the search results page</span></span>

> [!NOTE]
> <span data-ttu-id="3629f-157">Position refere-se à ordem cardinal em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3629f-157">Position refers to the cardinal order in your application.</span></span> <span data-ttu-id="3629f-158">Você tem a liberdade para definir esse número, desde que seja sempre o mesmo, para permitir a comparação.</span><span class="sxs-lookup"><span data-stu-id="3629f-158">You are free to set this number, as long as it's always the same, to allow for comparison.</span></span>
>

<span data-ttu-id="3629f-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="3629f-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="3629f-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3629f-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="3629f-161">3. Analisar com o Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="3629f-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="3629f-162">Depois de instrumentar seu aplicativo e verificar se ele está conectado corretamente ao Application Insights, use um modelo predefinido criado pelo Azure Search para a área de trabalho do Power BI.</span><span class="sxs-lookup"><span data-stu-id="3629f-162">After you have instrumented your app and verified your application is correctly connected to Application Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="3629f-163">Este modelo contém gráficos e tabelas que ajudam você a tomar decisões mais informadas a fim de melhorar o desempenho e a relevância da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3629f-163">This template contains charts and tables that help you make more informed decisions to improve your search performance and relevance.</span></span>

<span data-ttu-id="3629f-164">Para instanciar o modelo de área de trabalho do Power BI, você precisa de três informações sobre o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3629f-164">To instantiate the Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="3629f-165">Esses dados podem ser encontrados na página da Análise do Tráfego de Pesquisa, quando você seleciona o recurso a ser usado</span><span class="sxs-lookup"><span data-stu-id="3629f-165">This data can be found in the Search Traffic Analytics page, when you select the resource to use</span></span>

![Dados do Aplicativo Insights na folha de Análise do Tráfego de Pesquisa][2]

<span data-ttu-id="3629f-167">Métricas incluídas no modelo de área de trabalho do Power BI:</span><span class="sxs-lookup"><span data-stu-id="3629f-167">Metrics included in the Power BI desktop template:</span></span>

*   <span data-ttu-id="3629f-168">Taxa de cliques (CTR): proporção de usuários que clicam em um documento específico com relação ao número total de pesquisas.</span><span class="sxs-lookup"><span data-stu-id="3629f-168">Click through Rate (CTR): ratio of users who click on a specific document to the number of total searches.</span></span>
*   <span data-ttu-id="3629f-169">Pesquisa sem cliques: termos das principais consultas que não registraram nenhum clique</span><span class="sxs-lookup"><span data-stu-id="3629f-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="3629f-170">Documentos mais clicados: documentos mais clicados por ID nas últimas 24 horas, sete dias e 30 dias.</span><span class="sxs-lookup"><span data-stu-id="3629f-170">Most clicked documents: most clicked documents by ID in the last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="3629f-171">Pares de documento/termo populares: termos que resultam no mesmo documento clicado, ordenados por cliques.</span><span class="sxs-lookup"><span data-stu-id="3629f-171">Popular term-document pairs: terms that result in the same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="3629f-172">Hora do clique: cliques classificados por tempo desde a consulta de pesquisa</span><span class="sxs-lookup"><span data-stu-id="3629f-172">Time to click: clicks bucketed by time since the search query</span></span>

![Modelo do Power BI para leitura do Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="3629f-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3629f-174">Next Steps</span></span>
<span data-ttu-id="3629f-175">Instrumente seu aplicativo de pesquisa para obter dados informativos e avançados sobre o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3629f-175">Instrument your search application to get powerful and insightful data about your search service.</span></span>

<span data-ttu-id="3629f-176">Encontre mais informações sobre o Application Insights [aqui](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="3629f-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="3629f-177">Visite a [página de preços](https://azure.microsoft.com/pricing/details/application-insights/) do Application Insights para saber mais sobre seus tipos de serviço diferentes.</span><span class="sxs-lookup"><span data-stu-id="3629f-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) to learn more about their different service tiers.</span></span>

<span data-ttu-id="3629f-178">Saiba mais sobre como criar relatórios incríveis.</span><span class="sxs-lookup"><span data-stu-id="3629f-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="3629f-179">Confira [Introdução ao Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) para obter detalhes</span><span class="sxs-lookup"><span data-stu-id="3629f-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
