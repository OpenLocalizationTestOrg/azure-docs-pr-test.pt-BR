---
title: aaaUsing pesquisa no Azure Application Insights | Microsoft Docs
description: Pesquise e filtre telemetria bruta enviada pelo seu aplicativo Web.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="a1c6b-103">Usar a Pesquisa no Application Insights</span><span class="sxs-lookup"><span data-stu-id="a1c6b-103">Using Search in Application Insights</span></span>
<span data-ttu-id="a1c6b-104">A pesquisa é um recurso do [Application Insights](app-insights-overview.md) usar toofind e explorar os itens de telemetria individuais, como modos de exibição de página, exceções ou solicitações de web.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use toofind and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="a1c6b-105">Você também pode exibir rastreamentos de log e eventos que você tenha codificado.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="a1c6b-106">(Para consultas mais complexas sobre os dados, use o [Analytics](app-insights-analytics-tour.md).)</span><span class="sxs-lookup"><span data-stu-id="a1c6b-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="a1c6b-107">Onde você vê a Pesquisa?</span><span class="sxs-lookup"><span data-stu-id="a1c6b-107">Where do you see Search?</span></span>
### <a name="in-hello-azure-portal"></a><span data-ttu-id="a1c6b-108">No portal do Azure de saudação</span><span class="sxs-lookup"><span data-stu-id="a1c6b-108">In hello Azure portal</span></span>
<span data-ttu-id="a1c6b-109">Você pode abrir pesquisa diagnóstica explicitamente na folha de visão geral das informações do aplicativo de saudação do seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="a1c6b-109">You can open diagnostic search explicitly from hello Application Insights Overview blade of your application:</span></span>

![Abra a pesquisa de diagnóstico](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="a1c6b-111">Ela também é aberta quando você clica em alguns gráficos e itens de grade.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="a1c6b-112">Nesse caso, os filtros são definidos previamente toofocus no tipo de saudação do item selecionado.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-112">In this case, its filters are pre-set toofocus on hello type of item you selected.</span></span> 

<span data-ttu-id="a1c6b-113">Por exemplo, na folha de visão geral do hello, há um gráfico de barras de solicitações classificadas por tempo de resposta.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-113">For example, on hello Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="a1c6b-114">Clique em um toosee de intervalo de desempenho por meio de uma lista de solicitações individuais em que o intervalo de tempo de resposta:</span><span class="sxs-lookup"><span data-stu-id="a1c6b-114">Click through a performance range toosee a list of individual requests in that response time range:</span></span>

![Clique no desempenho de solicitação](./media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="a1c6b-116">saudação de corpo principal da pesquisa de diagnóstico é uma lista de itens de telemetria - solicitações ao servidor, página exibições, eventos personalizados que você codificou e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-116">hello main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="a1c6b-117">Em Olá parte superior da lista de saudação é um gráfico de resumo mostra as contagens de eventos ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-117">At hello top of hello list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="a1c6b-118">Clique em Atualizar tooget novos eventos.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-118">Click Refresh tooget new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="a1c6b-119">No Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a1c6b-119">In Visual Studio</span></span>

<span data-ttu-id="a1c6b-120">No Visual Studio, há também uma janela da Pesquisa do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="a1c6b-121">É mais útil para exibir eventos de telemetria gerados pelo aplicativo hello que você está depurando.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-121">It's most useful for displaying telemetry events generated by hello application that you're debugging.</span></span> <span data-ttu-id="a1c6b-122">Mas ele também pode mostrar eventos Olá coletados do seu aplicativo publicado no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-122">But it can also show hello events collected from your published app at hello Azure portal.</span></span>

<span data-ttu-id="a1c6b-123">Abra a janela de pesquisa de saudação no Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="a1c6b-123">Open hello Search window in Visual Studio:</span></span>

![O Visual Studio abre a pesquisa do Application Insights](./media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="a1c6b-125">janela de pesquisa Olá tem portal do recursos semelhantes toohello da web:</span><span class="sxs-lookup"><span data-stu-id="a1c6b-125">hello Search window has features similar toohello web portal:</span></span>

![Janela de pesquisa do Visual Studio Application Insights](./media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="a1c6b-127">Guia de faixa operação Hello está disponível quando você abrir uma solicitação ou um modo de exibição de página.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-127">hello Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="a1c6b-128">Um ' operação ' é uma sequência de eventos que está associada à exibição única tooa solicitação ou página.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-128">An 'operation' is a sequence of events that is associated with tooa single request or page view.</span></span> <span data-ttu-id="a1c6b-129">Por exemplo, chamadas de dependência, exceções, logs de rastreamento e eventos personalizados podem fazer parte de uma única operação.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="a1c6b-130">Olá operação de controle guia mostra graficamente Olá tempo e a duração esses eventos em relação toohello o modo de exibição de solicitação ou página.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-130">hello Track Operation tab shows graphically hello timing and duration of these events in relation toohello request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="a1c6b-131">Inspecionar itens individuais</span><span class="sxs-lookup"><span data-stu-id="a1c6b-131">Inspect individual items</span></span>
<span data-ttu-id="a1c6b-132">Selecione todos os campos de chave de toosee de item de telemetria e itens relacionados.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-132">Select any telemetry item toosee key fields and related items.</span></span> <span data-ttu-id="a1c6b-133">Se você quiser toosee Olá todo o conjunto de campos, clique em "...".</span><span class="sxs-lookup"><span data-stu-id="a1c6b-133">If you want toosee hello full set of fields, click "...".</span></span> 

![Clique em Novo Item de trabalho, editar campos de hello e, em seguida, clique em Okey.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="a1c6b-135">Filtrar tipos de evento</span><span class="sxs-lookup"><span data-stu-id="a1c6b-135">Filter event types</span></span>
<span data-ttu-id="a1c6b-136">Abra a folha de filtro hello e escolher os tipos de evento Olá você deseja toosee.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-136">Open hello Filter blade and choose hello event types you want toosee.</span></span> <span data-ttu-id="a1c6b-137">(Se, posteriormente, você deseja que os filtros de saudação toorestore com a qual você abriu a folha de saudação, clique em Redefinir.)</span><span class="sxs-lookup"><span data-stu-id="a1c6b-137">(If, later, you want toorestore hello filters with which you opened hello blade, click Reset.)</span></span>

![Escolha o filtro e selecione os tipos de telemetria](./media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="a1c6b-139">os tipos de evento Olá são:</span><span class="sxs-lookup"><span data-stu-id="a1c6b-139">hello event types are:</span></span>

* <span data-ttu-id="a1c6b-140">**Controlar** - [Logs de diagnóstico](app-insights-asp-net-trace-logs.md), incluindo chamadas TrackTrace, log4Net, NLog e System.Diagnostic.Trace.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="a1c6b-141">**Solicitar** -Solicitações HTTP recebidas pelo seu aplicativo para servidores, incluindo páginas, scripts, imagens, arquivos de estilo e dados.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="a1c6b-142">Esses eventos são gráficos de visão geral usado toocreate Olá solicitação e resposta.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-142">These events are used toocreate hello request and response overview charts.</span></span>
* <span data-ttu-id="a1c6b-143">**Exibição de página** - [telemetria enviada pelo cliente de web de saudação](app-insights-javascript.md), usado toocreate relatórios de modo de exibição de página.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-143">**Page View** - [Telemetry sent by hello web client](app-insights-javascript.md), used toocreate page view reports.</span></span> 
* <span data-ttu-id="a1c6b-144">**Evento personalizado** - se você inseriu chamadas tooTrackEvent() na ordem muito[monitorar o uso de](app-insights-api-custom-events-metrics.md), você pode pesquisar aqui.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-144">**Custom Event** - If you inserted calls tooTrackEvent() in order too[monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="a1c6b-145">**Exceção** - não percebida [exceções no servidor de saudação](app-insights-asp-net-exceptions.md)e aqueles que você faça logon usando trackexception ().</span><span class="sxs-lookup"><span data-stu-id="a1c6b-145">**Exception** - Uncaught [exceptions in hello server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="a1c6b-146">**Dependência** - [chamadas de seu aplicativo de servidor](app-insights-asp-net-dependencies.md) tooother os serviços, como bancos de dados ou APIs REST e chamadas AJAX de seu [código de cliente](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="a1c6b-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) tooother services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="a1c6b-147">**Disponibilidade** ‑ Resultados de [testes de disponibilidade](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="a1c6b-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="a1c6b-148">Filtrar pelos valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="a1c6b-148">Filter on property values</span></span>
<span data-ttu-id="a1c6b-149">Você pode filtrar eventos em valores de saudação de suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-149">You can filter events on hello values of their properties.</span></span> <span data-ttu-id="a1c6b-150">propriedades disponíveis Olá dependem de tipos de evento de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-150">hello available properties depend on hello event types you selected.</span></span> 

<span data-ttu-id="a1c6b-151">Por exemplo, escolha solicitações com um código de resposta específicos.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-151">For example, pick out requests with a specific response code.</span></span> 

![Expanda uma propriedade e escolha um valor](./media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="a1c6b-153">Não escolher nenhum valor de uma propriedade específica tem Olá mesmo efeito que escolher todos os valores.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-153">Choosing no values of a particular property has hello same effect as choosing all values.</span></span> <span data-ttu-id="a1c6b-154">Ele desativará a filtragem nessa propriedade.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="a1c6b-155">Reduzir o escopo de sua pesquisa</span><span class="sxs-lookup"><span data-stu-id="a1c6b-155">Narrow your search</span></span>
<span data-ttu-id="a1c6b-156">Observe que Olá contagens toohello à direita dos valores de filtro de saudação mostrar quantos ocorrências existe estão no conjunto atual de filtrado hello.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-156">Notice that hello counts toohello right of hello filter values show how many occurrences there are in hello current filtered set.</span></span> 

<span data-ttu-id="a1c6b-157">Neste exemplo, é claro que a solicitação ' Rpt/funcionários' hello resulta na maioria dos erros de saudação '500':</span><span class="sxs-lookup"><span data-stu-id="a1c6b-157">In this example, it's clear that hello 'Rpt/Employees' request results in most of hello '500' errors:</span></span>

![Expanda uma propriedade e escolha um valor](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a><span data-ttu-id="a1c6b-159">Localizar eventos com hello mesma propriedade</span><span class="sxs-lookup"><span data-stu-id="a1c6b-159">Find events with hello same property</span></span>
<span data-ttu-id="a1c6b-160">Localizar Olá a todos os itens com hello mesmo valor da propriedade:</span><span class="sxs-lookup"><span data-stu-id="a1c6b-160">Find all hello items with hello same property value:</span></span>

![Clique com o botão direito em uma propriedade](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a><span data-ttu-id="a1c6b-162">Dados de saudação de pesquisa</span><span class="sxs-lookup"><span data-stu-id="a1c6b-162">Search hello data</span></span>

> [!NOTE]
> <span data-ttu-id="a1c6b-163">toowrite consultas mais complexas, abra [ **análise** ](app-insights-analytics-tour.md) da parte superior da saudação da folha de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-163">toowrite more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from hello top of hello Search blade.</span></span>
> 

<span data-ttu-id="a1c6b-164">Você pode pesquisar termos em qualquer um dos valores de propriedade hello.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-164">You can search for terms in any of hello property values.</span></span> <span data-ttu-id="a1c6b-165">Isso será especialmente útil se você tiver gravado [eventos personalizados](app-insights-api-custom-events-metrics.md) com valores de propriedade.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="a1c6b-166">Talvez você queira tooset um intervalo de tempo, como pesquisas em um intervalo mais curto é mais rápido.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-166">You might want tooset a time range, as searches over a shorter range are faster.</span></span> 

![Abra a pesquisa de diagnóstico](./media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="a1c6b-168">Pesquisar por palavras inteiras, não subcadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="a1c6b-169">Use caracteres especiais do tooenclose aspas.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-169">Use quotation marks tooenclose special characters.</span></span>

| <span data-ttu-id="a1c6b-170">string</span><span class="sxs-lookup"><span data-stu-id="a1c6b-170">string</span></span> | <span data-ttu-id="a1c6b-171">*não* é encontrada por</span><span class="sxs-lookup"><span data-stu-id="a1c6b-171">is *not* found by</span></span> | <span data-ttu-id="a1c6b-172">porém, pode ser encontrada por</span><span class="sxs-lookup"><span data-stu-id="a1c6b-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1c6b-173">ControladorInicial.Sobre</span><span class="sxs-lookup"><span data-stu-id="a1c6b-173">HomeController.About</span></span> |<span data-ttu-id="a1c6b-174">inicial</span><span class="sxs-lookup"><span data-stu-id="a1c6b-174">home</span></span><br/><span data-ttu-id="a1c6b-175">controlador</span><span class="sxs-lookup"><span data-stu-id="a1c6b-175">controller</span></span><br/><span data-ttu-id="a1c6b-176">obre</span><span class="sxs-lookup"><span data-stu-id="a1c6b-176">out</span></span> | <span data-ttu-id="a1c6b-177">homecontroller</span><span class="sxs-lookup"><span data-stu-id="a1c6b-177">homecontroller</span></span><br/><span data-ttu-id="a1c6b-178">sobre</span><span class="sxs-lookup"><span data-stu-id="a1c6b-178">about</span></span><br/><span data-ttu-id="a1c6b-179">"homecontroller.about"</span><span class="sxs-lookup"><span data-stu-id="a1c6b-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="a1c6b-180">Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="a1c6b-180">United States</span></span>|<span data-ttu-id="a1c6b-181">Uni</span><span class="sxs-lookup"><span data-stu-id="a1c6b-181">Uni</span></span><br/><span data-ttu-id="a1c6b-182">dos</span><span class="sxs-lookup"><span data-stu-id="a1c6b-182">ted</span></span>|<span data-ttu-id="a1c6b-183">unidos</span><span class="sxs-lookup"><span data-stu-id="a1c6b-183">united</span></span><br/><span data-ttu-id="a1c6b-184">estados</span><span class="sxs-lookup"><span data-stu-id="a1c6b-184">states</span></span><br/><span data-ttu-id="a1c6b-185">estados AND unidos</span><span class="sxs-lookup"><span data-stu-id="a1c6b-185">united AND states</span></span><br/><span data-ttu-id="a1c6b-186">“estados unidos”</span><span class="sxs-lookup"><span data-stu-id="a1c6b-186">"united states"</span></span>

<span data-ttu-id="a1c6b-187">Aqui estão as expressões de pesquisa de saudação, que você pode usar:</span><span class="sxs-lookup"><span data-stu-id="a1c6b-187">Here are hello search expressions you can use:</span></span>

| <span data-ttu-id="a1c6b-188">Exemplo de consulta</span><span class="sxs-lookup"><span data-stu-id="a1c6b-188">Sample query</span></span> | <span data-ttu-id="a1c6b-189">Efeito</span><span class="sxs-lookup"><span data-stu-id="a1c6b-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="a1c6b-190">Localiza todos os eventos no intervalo de tempo de saudação cujos campos incluem palavras hello "apple"</span><span class="sxs-lookup"><span data-stu-id="a1c6b-190">Find all events in hello time range whose fields include hello word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="a1c6b-191">Encontrar eventos que contêm as duas palavras.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-191">Find events that contain both words.</span></span> <span data-ttu-id="a1c6b-192">Use "AND” em letras maiúsculas, e não "and".</span><span class="sxs-lookup"><span data-stu-id="a1c6b-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="a1c6b-193">Encontrar eventos que contêm uma das duas palavras.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-193">Find events that contain either word.</span></span> <span data-ttu-id="a1c6b-194">Use "OR", e não "or".</span><span class="sxs-lookup"><span data-stu-id="a1c6b-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="a1c6b-195">Forma abreviada.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="a1c6b-196">Localize eventos que contêm uma palavra mas não Olá outros.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-196">Find events that contain one word but not hello other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="a1c6b-197">amostragem</span><span class="sxs-lookup"><span data-stu-id="a1c6b-197">Sampling</span></span>
<span data-ttu-id="a1c6b-198">Se seu aplicativo gera muita telemetria (e você estiver usando Olá ASP.NET SDK versão 2.0.0-beta3 ou posterior), módulo de amostragem adaptável Olá automaticamente reduz o volume de saudação enviada toohello portal enviando apenas uma fração representativa de eventos.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-198">If your app generates a lot of telemetry (and you are using hello ASP.NET SDK version 2.0.0-beta3 or later), hello adaptive sampling module automatically reduces hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="a1c6b-199">No entanto, eventos que são relacionada toohello mesma solicitação são selecionado ou desmarcado como um grupo, para que você possa navegar entre eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-199">However, events that are related toohello same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="a1c6b-200">[Saiba mais sobre amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="a1c6b-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="a1c6b-201">Criar um item de trabalho</span><span class="sxs-lookup"><span data-stu-id="a1c6b-201">Create work item</span></span>
<span data-ttu-id="a1c6b-202">Você pode criar um bug no GitHub ou Visual Studio Team Services com detalhes de saudação de qualquer item de telemetria.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-202">You can create a bug in GitHub or Visual Studio Team Services with hello details from any telemetry item.</span></span> 

![Clique em Novo Item de trabalho, editar campos de hello e, em seguida, clique em Okey.](./media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="a1c6b-204">Hello primeira vez que você fizer isso, você será solicitado a tooconfigure tooyour um link do Team Services conta e de projeto.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-204">hello first time you do this, you are asked tooconfigure a link tooyour Team Services account and project.</span></span>

![Preencher Olá URL do seu servidor do Team Services e o nome do projeto hello e, em seguida, clique em autorizar](./media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="a1c6b-206">(Você também pode configurar o link de saudação na folha de itens de trabalho hello.)</span><span class="sxs-lookup"><span data-stu-id="a1c6b-206">(You can also configure hello link on hello Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="a1c6b-207">Salvar sua pesquisa</span><span class="sxs-lookup"><span data-stu-id="a1c6b-207">Save your search</span></span>
<span data-ttu-id="a1c6b-208">Quando você definiu todos os filtros de saudação desejado, você pode salvar pesquisa hello como um favorito.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-208">When you've set all hello filters you want, you can save hello search as a favorite.</span></span> <span data-ttu-id="a1c6b-209">Se você trabalha em uma conta organizacional, você pode escolher se tooshare-lo com outros membros da equipe.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-209">If you work in an organizational account, you can choose whether tooshare it with other team members.</span></span>

![Clique em favorito, Olá nome do conjunto e clique em Salvar](./media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="a1c6b-211">novamente, pesquisa de saudação toosee **folha de visão geral de toohello vá** e abrir favoritos:</span><span class="sxs-lookup"><span data-stu-id="a1c6b-211">toosee hello search again, **go toohello overview blade** and open Favorites:</span></span>

![Bloco Favoritos](./media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="a1c6b-213">Se você salvou com intervalo de tempo relativo, folha reaberto Olá tem dados mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-213">If you saved with Relative time range, hello re-opened blade has hello latest data.</span></span> <span data-ttu-id="a1c6b-214">Se você salvou com intervalo de tempo absoluto, você verá Olá mesmos dados toda vez.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-214">If you saved with Absolute time range, you see hello same data every time.</span></span> <span data-ttu-id="a1c6b-215">(Se 'Relativo' não está disponível quando você deseja toosave um favorito, clique o intervalo de tempo no cabeçalho de saudação e definir um intervalo de tempo que não é um intervalo personalizado).</span><span class="sxs-lookup"><span data-stu-id="a1c6b-215">(If 'Relative' isn't available when you want toosave a favorite, click Time Range in hello header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-tooapplication-insights"></a><span data-ttu-id="a1c6b-216">Enviar telemetria mais tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="a1c6b-216">Send more telemetry tooApplication Insights</span></span>
<span data-ttu-id="a1c6b-217">Telemetria de fora da caixa de toohello adição enviada pelo SDK do Application Insights, você pode:</span><span class="sxs-lookup"><span data-stu-id="a1c6b-217">In addition toohello out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="a1c6b-218">Capturar rastreamentos de log da sua estrutura de registros favorita no [.NET](app-insights-asp-net-trace-logs.md) ou [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a1c6b-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="a1c6b-219">Isso significa que você pode pesquisar os rastreamentos de log e correlacioná-los com outros eventos, exceções e visualizações de página.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="a1c6b-220">[Escrever código](app-insights-api-custom-events-metrics.md) toosend eventos personalizados, modos de exibição de página e as exceções.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-220">[Write code](app-insights-api-custom-events-metrics.md) toosend custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="a1c6b-221">[Saiba como toosend registra e telemetria personalizada tooApplication Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a1c6b-221">[Learn how toosend logs and custom telemetry tooApplication Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <span data-ttu-id="a1c6b-222"><a name="questions"></a>Perguntas e respostas</span><span class="sxs-lookup"><span data-stu-id="a1c6b-222"><a name="questions"></a>Q & A</span></span>
### <span data-ttu-id="a1c6b-223"><a name="limits"></a>Que quantidade de dados é mantida?</span><span class="sxs-lookup"><span data-stu-id="a1c6b-223"><a name="limits"></a>How much data is retained?</span></span>

<span data-ttu-id="a1c6b-224">Consulte Olá [resumo de limites](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="a1c6b-224">See hello [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="a1c6b-225">Como consultar dados de POSTAGEM nas minhas solicitações de servidor?</span><span class="sxs-lookup"><span data-stu-id="a1c6b-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="a1c6b-226">Nós não registrar dados de POSTAGEM Olá automaticamente, mas você pode usar [TrackTrace ou log chama](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a1c6b-226">We don't log hello POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="a1c6b-227">Colocar os dados de POSTAGEM Olá no parâmetro de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-227">Put hello POST data in hello message parameter.</span></span> <span data-ttu-id="a1c6b-228">Não é possível filtrar em uma mensagem de saudação no hello mesma forma, você pode filtrar em propriedades, mas o limite de tamanho de saudação é maior.</span><span class="sxs-lookup"><span data-stu-id="a1c6b-228">You can't filter on hello message in hello same way you can filter on properties, but hello size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="a1c6b-229">Vídeo</span><span class="sxs-lookup"><span data-stu-id="a1c6b-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <span data-ttu-id="a1c6b-230"><a name="add"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a1c6b-230"><a name="add"></a>Next steps</span></span>
* [<span data-ttu-id="a1c6b-231">Escrever consultas complexas no Analytics</span><span class="sxs-lookup"><span data-stu-id="a1c6b-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="a1c6b-232">Enviar logs e telemetria personalizada tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="a1c6b-232">Send logs and custom telemetry tooApplication Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="a1c6b-233">Configurar testes de disponibilidade e capacidade de resposta</span><span class="sxs-lookup"><span data-stu-id="a1c6b-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="a1c6b-234">Solução de problemas</span><span class="sxs-lookup"><span data-stu-id="a1c6b-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
