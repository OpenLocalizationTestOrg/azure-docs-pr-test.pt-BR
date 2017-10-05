---
title: Usar a Pesquisa no Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: e2d12f807756b778a64920b12a66fba184a99844
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="b2e61-103">Usar a Pesquisa no Application Insights</span><span class="sxs-lookup"><span data-stu-id="b2e61-103">Using Search in Application Insights</span></span>
<span data-ttu-id="b2e61-104">A Pesquisa é um recurso do [Application Insights](app-insights-overview.md) que você usa para localizar e explorar itens individuais de telemetria, como exibições de página, exceções ou solicitações da Web.</span><span class="sxs-lookup"><span data-stu-id="b2e61-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use to find and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="b2e61-105">Você também pode exibir rastreamentos de log e eventos que você tenha codificado.</span><span class="sxs-lookup"><span data-stu-id="b2e61-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="b2e61-106">(Para consultas mais complexas sobre os dados, use o [Analytics](app-insights-analytics-tour.md).)</span><span class="sxs-lookup"><span data-stu-id="b2e61-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="b2e61-107">Onde você vê a Pesquisa?</span><span class="sxs-lookup"><span data-stu-id="b2e61-107">Where do you see Search?</span></span>
### <a name="in-the-azure-portal"></a><span data-ttu-id="b2e61-108">No portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b2e61-108">In the Azure portal</span></span>
<span data-ttu-id="b2e61-109">Você pode abrir a pesquisa de diagnóstico explicitamente na folha Visão Geral do Application Insights do seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="b2e61-109">You can open diagnostic search explicitly from the Application Insights Overview blade of your application:</span></span>

![Abra a pesquisa de diagnóstico](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="b2e61-111">Ela também é aberta quando você clica em alguns gráficos e itens de grade.</span><span class="sxs-lookup"><span data-stu-id="b2e61-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="b2e61-112">Nesse caso, os filtros dessa pesquisa são predefinidos para concentrar-se no tipo de item selecionado por você.</span><span class="sxs-lookup"><span data-stu-id="b2e61-112">In this case, its filters are pre-set to focus on the type of item you selected.</span></span> 

<span data-ttu-id="b2e61-113">Por exemplo, na folha Visão Geral, há um gráfico de barras das solicitações classificadas pelo tempo de resposta.</span><span class="sxs-lookup"><span data-stu-id="b2e61-113">For example, on the Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="b2e61-114">Clique em um intervalo de desempenho para ver uma lista de solicitações individuais desse intervalo de tempo de resposta:</span><span class="sxs-lookup"><span data-stu-id="b2e61-114">Click through a performance range to see a list of individual requests in that response time range:</span></span>

![Clique no desempenho de solicitação](./media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="b2e61-116">O corpo principal da Pesquisa de diagnóstico é uma lista de itens de telemetria - solicitações ao servidor, visualizações de página, eventos personalizados que você codificou e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="b2e61-116">The main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="b2e61-117">Na parte superior da lista, há um gráfico de resumo mostrando contagens de eventos ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="b2e61-117">At the top of the list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="b2e61-118">Clique em Atualizar para obter novos eventos.</span><span class="sxs-lookup"><span data-stu-id="b2e61-118">Click Refresh to get new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="b2e61-119">No Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b2e61-119">In Visual Studio</span></span>

<span data-ttu-id="b2e61-120">No Visual Studio, há também uma janela da Pesquisa do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b2e61-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="b2e61-121">É mais útil exibir eventos de telemetria gerados pelo aplicativo que você está depurando.</span><span class="sxs-lookup"><span data-stu-id="b2e61-121">It's most useful for displaying telemetry events generated by the application that you're debugging.</span></span> <span data-ttu-id="b2e61-122">Contudo, ele também pode mostrar os eventos coletados do seu aplicativo publicado no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2e61-122">But it can also show the events collected from your published app at the Azure portal.</span></span>

<span data-ttu-id="b2e61-123">Abra a janela Pesquisar no Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="b2e61-123">Open the Search window in Visual Studio:</span></span>

![O Visual Studio abre a pesquisa do Application Insights](./media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="b2e61-125">A janela Pesquisar tem os mesmos recursos que o portal da Web:</span><span class="sxs-lookup"><span data-stu-id="b2e61-125">The Search window has features similar to the web portal:</span></span>

![Janela de pesquisa do Visual Studio Application Insights](./media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="b2e61-127">A guia Controlar Operação está disponível ao abrir uma solicitação ou uma exibição de página.</span><span class="sxs-lookup"><span data-stu-id="b2e61-127">The Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="b2e61-128">Uma “operação” é uma sequência de eventos associada a uma única solicitação ou exibição de página.</span><span class="sxs-lookup"><span data-stu-id="b2e61-128">An 'operation' is a sequence of events that is associated with to a single request or page view.</span></span> <span data-ttu-id="b2e61-129">Por exemplo, chamadas de dependência, exceções, logs de rastreamento e eventos personalizados podem fazer parte de uma única operação.</span><span class="sxs-lookup"><span data-stu-id="b2e61-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="b2e61-130">A guia Controlar Operação mostra graficamente o tempo e a duração desses eventos em relação à exibição de solicitação ou página.</span><span class="sxs-lookup"><span data-stu-id="b2e61-130">The Track Operation tab shows graphically the timing and duration of these events in relation to the request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="b2e61-131">Inspecionar itens individuais</span><span class="sxs-lookup"><span data-stu-id="b2e61-131">Inspect individual items</span></span>
<span data-ttu-id="b2e61-132">Selecione qualquer item de telemetria para ver os campos-chave e itens relacionados.</span><span class="sxs-lookup"><span data-stu-id="b2e61-132">Select any telemetry item to see key fields and related items.</span></span> <span data-ttu-id="b2e61-133">Se você quiser ver o conjunto completo de campos, clique em "...".</span><span class="sxs-lookup"><span data-stu-id="b2e61-133">If you want to see the full set of fields, click "...".</span></span> 

![Clique em Novo Item de Trabalho, edite os campos e, em seguida, clique em OK.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="b2e61-135">Filtrar tipos de evento</span><span class="sxs-lookup"><span data-stu-id="b2e61-135">Filter event types</span></span>
<span data-ttu-id="b2e61-136">Abrir a folha de filtro e escolha os tipos de eventos que você deseja ver.</span><span class="sxs-lookup"><span data-stu-id="b2e61-136">Open the Filter blade and choose the event types you want to see.</span></span> <span data-ttu-id="b2e61-137">(Se posteriormente, você desejar restaurar os filtros com os quais você abriu a folha, clique em Redefinir.)</span><span class="sxs-lookup"><span data-stu-id="b2e61-137">(If, later, you want to restore the filters with which you opened the blade, click Reset.)</span></span>

![Escolha o filtro e selecione os tipos de telemetria](./media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="b2e61-139">Os tipos de evento são:</span><span class="sxs-lookup"><span data-stu-id="b2e61-139">The event types are:</span></span>

* <span data-ttu-id="b2e61-140">**Controlar** - [Logs de diagnóstico](app-insights-asp-net-trace-logs.md), incluindo chamadas TrackTrace, log4Net, NLog e System.Diagnostic.Trace.</span><span class="sxs-lookup"><span data-stu-id="b2e61-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="b2e61-141">**Solicitar** -Solicitações HTTP recebidas pelo seu aplicativo para servidores, incluindo páginas, scripts, imagens, arquivos de estilo e dados.</span><span class="sxs-lookup"><span data-stu-id="b2e61-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="b2e61-142">Esses eventos são usados para criar os gráficos de visão geral de solicitação e de resposta.</span><span class="sxs-lookup"><span data-stu-id="b2e61-142">These events are used to create the request and response overview charts.</span></span>
* <span data-ttu-id="b2e61-143">**Exibição da página** - [Telemetria enviada pelo cliente da Web](app-insights-javascript.md), usada para criar relatórios de exibição de página.</span><span class="sxs-lookup"><span data-stu-id="b2e61-143">**Page View** - [Telemetry sent by the web client](app-insights-javascript.md), used to create page view reports.</span></span> 
* <span data-ttu-id="b2e61-144">**Evento Personalizado** ‑ Se você tiver inserido chamadas TrackEvent() para [monitorar o uso](app-insights-api-custom-events-metrics.md), você poderá pesquisá-las aqui.</span><span class="sxs-lookup"><span data-stu-id="b2e61-144">**Custom Event** - If you inserted calls to TrackEvent() in order to [monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="b2e61-145">**Exceção** ‑ [Exceções não percebidas no servidor](app-insights-asp-net-exceptions.md) e aquelas que você registra usando TrackException().</span><span class="sxs-lookup"><span data-stu-id="b2e61-145">**Exception** - Uncaught [exceptions in the server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="b2e61-146">**Dependência** - [Chamadas do aplicativo para servidores](app-insights-asp-net-dependencies.md) para outros serviços, como APIs REST ou bancos de dados e chamadas AJAX do seu [código de cliente](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="b2e61-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) to other services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="b2e61-147">**Disponibilidade** ‑ Resultados de [testes de disponibilidade](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="b2e61-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="b2e61-148">Filtrar pelos valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="b2e61-148">Filter on property values</span></span>
<span data-ttu-id="b2e61-149">Você pode filtrar eventos pelos valores de suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="b2e61-149">You can filter events on the values of their properties.</span></span> <span data-ttu-id="b2e61-150">As propriedades disponíveis dependem dos tipos de evento que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="b2e61-150">The available properties depend on the event types you selected.</span></span> 

<span data-ttu-id="b2e61-151">Por exemplo, escolha solicitações com um código de resposta específicos.</span><span class="sxs-lookup"><span data-stu-id="b2e61-151">For example, pick out requests with a specific response code.</span></span> 

![Expanda uma propriedade e escolha um valor](./media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="b2e61-153">Não escolher nenhum valor para uma determinada propriedade tem o mesmo efeito que escolher todos os valores.</span><span class="sxs-lookup"><span data-stu-id="b2e61-153">Choosing no values of a particular property has the same effect as choosing all values.</span></span> <span data-ttu-id="b2e61-154">Ele desativará a filtragem nessa propriedade.</span><span class="sxs-lookup"><span data-stu-id="b2e61-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="b2e61-155">Reduzir o escopo de sua pesquisa</span><span class="sxs-lookup"><span data-stu-id="b2e61-155">Narrow your search</span></span>
<span data-ttu-id="b2e61-156">Observe que as contagens à direita dos valores de filtro mostram quantas ocorrências existem no atual conjunto filtrado.</span><span class="sxs-lookup"><span data-stu-id="b2e61-156">Notice that the counts to the right of the filter values show how many occurrences there are in the current filtered set.</span></span> 

<span data-ttu-id="b2e61-157">Neste exemplo, está claro que a solicitação “Rpt/Employees” resulta na maioria dos 500 erros:</span><span class="sxs-lookup"><span data-stu-id="b2e61-157">In this example, it's clear that the 'Rpt/Employees' request results in most of the '500' errors:</span></span>

![Expanda uma propriedade e escolha um valor](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-the-same-property"></a><span data-ttu-id="b2e61-159">Encontrar eventos com a mesma propriedade</span><span class="sxs-lookup"><span data-stu-id="b2e61-159">Find events with the same property</span></span>
<span data-ttu-id="b2e61-160">Localize todos os itens com o mesmo valor da propriedade:</span><span class="sxs-lookup"><span data-stu-id="b2e61-160">Find all the items with the same property value:</span></span>

![Clique com o botão direito em uma propriedade](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-the-data"></a><span data-ttu-id="b2e61-162">Pesquisar os dados</span><span class="sxs-lookup"><span data-stu-id="b2e61-162">Search the data</span></span>

> [!NOTE]
> <span data-ttu-id="b2e61-163">Para escrever consultas mais complexas, abra o [**Analytics**](app-insights-analytics-tour.md) na parte superior da folha Pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b2e61-163">To write more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from the top of the Search blade.</span></span>
> 

<span data-ttu-id="b2e61-164">Você pode pesquisar termos em qualquer um dos valores de propriedade.</span><span class="sxs-lookup"><span data-stu-id="b2e61-164">You can search for terms in any of the property values.</span></span> <span data-ttu-id="b2e61-165">Isso será especialmente útil se você tiver gravado [eventos personalizados](app-insights-api-custom-events-metrics.md) com valores de propriedade.</span><span class="sxs-lookup"><span data-stu-id="b2e61-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="b2e61-166">Você talvez queira definir um tempo de intervalo, já que pesquisas em um intervalo mais curto são mais rápidas.</span><span class="sxs-lookup"><span data-stu-id="b2e61-166">You might want to set a time range, as searches over a shorter range are faster.</span></span> 

![Abra a pesquisa de diagnóstico](./media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="b2e61-168">Pesquisar por palavras inteiras, não subcadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b2e61-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="b2e61-169">Use aspas para delimitar caracteres especiais.</span><span class="sxs-lookup"><span data-stu-id="b2e61-169">Use quotation marks to enclose special characters.</span></span>

| <span data-ttu-id="b2e61-170">string</span><span class="sxs-lookup"><span data-stu-id="b2e61-170">string</span></span> | <span data-ttu-id="b2e61-171">*não* é encontrada por</span><span class="sxs-lookup"><span data-stu-id="b2e61-171">is *not* found by</span></span> | <span data-ttu-id="b2e61-172">porém, pode ser encontrada por</span><span class="sxs-lookup"><span data-stu-id="b2e61-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2e61-173">ControladorInicial.Sobre</span><span class="sxs-lookup"><span data-stu-id="b2e61-173">HomeController.About</span></span> |<span data-ttu-id="b2e61-174">inicial</span><span class="sxs-lookup"><span data-stu-id="b2e61-174">home</span></span><br/><span data-ttu-id="b2e61-175">controlador</span><span class="sxs-lookup"><span data-stu-id="b2e61-175">controller</span></span><br/><span data-ttu-id="b2e61-176">obre</span><span class="sxs-lookup"><span data-stu-id="b2e61-176">out</span></span> | <span data-ttu-id="b2e61-177">homecontroller</span><span class="sxs-lookup"><span data-stu-id="b2e61-177">homecontroller</span></span><br/><span data-ttu-id="b2e61-178">sobre</span><span class="sxs-lookup"><span data-stu-id="b2e61-178">about</span></span><br/><span data-ttu-id="b2e61-179">"homecontroller.about"</span><span class="sxs-lookup"><span data-stu-id="b2e61-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="b2e61-180">Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="b2e61-180">United States</span></span>|<span data-ttu-id="b2e61-181">Uni</span><span class="sxs-lookup"><span data-stu-id="b2e61-181">Uni</span></span><br/><span data-ttu-id="b2e61-182">dos</span><span class="sxs-lookup"><span data-stu-id="b2e61-182">ted</span></span>|<span data-ttu-id="b2e61-183">unidos</span><span class="sxs-lookup"><span data-stu-id="b2e61-183">united</span></span><br/><span data-ttu-id="b2e61-184">estados</span><span class="sxs-lookup"><span data-stu-id="b2e61-184">states</span></span><br/><span data-ttu-id="b2e61-185">estados AND unidos</span><span class="sxs-lookup"><span data-stu-id="b2e61-185">united AND states</span></span><br/><span data-ttu-id="b2e61-186">“estados unidos”</span><span class="sxs-lookup"><span data-stu-id="b2e61-186">"united states"</span></span>

<span data-ttu-id="b2e61-187">Estas são algumas expressões de pesquisa que você pode usar:</span><span class="sxs-lookup"><span data-stu-id="b2e61-187">Here are the search expressions you can use:</span></span>

| <span data-ttu-id="b2e61-188">Exemplo de consulta</span><span class="sxs-lookup"><span data-stu-id="b2e61-188">Sample query</span></span> | <span data-ttu-id="b2e61-189">Efeito</span><span class="sxs-lookup"><span data-stu-id="b2e61-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="b2e61-190">Encontrar todos os eventos no período cujos campos incluem a palavra “maçã”</span><span class="sxs-lookup"><span data-stu-id="b2e61-190">Find all events in the time range whose fields include the word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="b2e61-191">Encontrar eventos que contêm as duas palavras.</span><span class="sxs-lookup"><span data-stu-id="b2e61-191">Find events that contain both words.</span></span> <span data-ttu-id="b2e61-192">Use "AND” em letras maiúsculas, e não "and".</span><span class="sxs-lookup"><span data-stu-id="b2e61-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="b2e61-193">Encontrar eventos que contêm uma das duas palavras.</span><span class="sxs-lookup"><span data-stu-id="b2e61-193">Find events that contain either word.</span></span> <span data-ttu-id="b2e61-194">Use "OR", e não "or".</span><span class="sxs-lookup"><span data-stu-id="b2e61-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="b2e61-195">Forma abreviada.</span><span class="sxs-lookup"><span data-stu-id="b2e61-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="b2e61-196">Encontre eventos que contêm uma das palavras, mas não a outra.</span><span class="sxs-lookup"><span data-stu-id="b2e61-196">Find events that contain one word but not the other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="b2e61-197">amostragem</span><span class="sxs-lookup"><span data-stu-id="b2e61-197">Sampling</span></span>
<span data-ttu-id="b2e61-198">Se o seu aplicativo gerar muita telemetria (e você estiver usando o SDK do ASP.NET versão 2.0.0-beta3 ou posterior), o módulo de amostragem adaptável reduzirá automaticamente o volume enviado ao portal, enviando apenas uma fração representativa de eventos.</span><span class="sxs-lookup"><span data-stu-id="b2e61-198">If your app generates a lot of telemetry (and you are using the ASP.NET SDK version 2.0.0-beta3 or later), the adaptive sampling module automatically reduces the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="b2e61-199">No entanto, os eventos relacionados à mesma solicitação serão selecionadas ou desmarcadas como um grupo, para que você possa navegar entre os eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="b2e61-199">However, events that are related to the same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="b2e61-200">[Saiba mais sobre amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="b2e61-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="b2e61-201">Criar um item de trabalho</span><span class="sxs-lookup"><span data-stu-id="b2e61-201">Create work item</span></span>
<span data-ttu-id="b2e61-202">Você pode criar um bug no GitHub ou Visual Studio Team Services com os detalhes de qualquer item de telemetria.</span><span class="sxs-lookup"><span data-stu-id="b2e61-202">You can create a bug in GitHub or Visual Studio Team Services with the details from any telemetry item.</span></span> 

![Clique em Novo Item de Trabalho, edite os campos e, em seguida, clique em OK.](./media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="b2e61-204">Na primeira vez que fizer isso, será solicitado que você configure um link para sua conta e projeto do Team Services.</span><span class="sxs-lookup"><span data-stu-id="b2e61-204">The first time you do this, you are asked to configure a link to your Team Services account and project.</span></span>

![Preencha a URL do servidor do Team Services e o Nome do projeto e, em seguida, clique em Autorizar](./media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="b2e61-206">(Você também pode configurar o link na folha Itens de Trabalho.)</span><span class="sxs-lookup"><span data-stu-id="b2e61-206">(You can also configure the link on the Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="b2e61-207">Salvar sua pesquisa</span><span class="sxs-lookup"><span data-stu-id="b2e61-207">Save your search</span></span>
<span data-ttu-id="b2e61-208">Quando você definiu todos os filtros que deseja, você pode salvar a pesquisa como um favorito.</span><span class="sxs-lookup"><span data-stu-id="b2e61-208">When you've set all the filters you want, you can save the search as a favorite.</span></span> <span data-ttu-id="b2e61-209">Se você trabalha em uma conta organizacional, você pode optar por compartilhá-la com outros membros da equipe.</span><span class="sxs-lookup"><span data-stu-id="b2e61-209">If you work in an organizational account, you can choose whether to share it with other team members.</span></span>

![Clique em Favorito, defina o nome e clique em Salvar](./media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="b2e61-211">Para ver a pesquisa novamente, **vá até a folha de visão geral** e abra Favoritos:</span><span class="sxs-lookup"><span data-stu-id="b2e61-211">To see the search again, **go to the overview blade** and open Favorites:</span></span>

![Bloco Favoritos](./media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="b2e61-213">Se você os salvou com o intervalo de tempo Relativo, a folha reaberta contém os dados mais recentes.</span><span class="sxs-lookup"><span data-stu-id="b2e61-213">If you saved with Relative time range, the re-opened blade has the latest data.</span></span> <span data-ttu-id="b2e61-214">Se você os salvou com o intervalo de tempo Absoluto, consulte os mesmos dados, sempre.</span><span class="sxs-lookup"><span data-stu-id="b2e61-214">If you saved with Absolute time range, you see the same data every time.</span></span> <span data-ttu-id="b2e61-215">(Se “Intervalo de Tempo” não estiver disponível quando você desejar salvar um favorito, clique em Intervalo de tempo no cabeçalho e defina um período que não seja um intervalo personalizado.)</span><span class="sxs-lookup"><span data-stu-id="b2e61-215">(If 'Relative' isn't available when you want to save a favorite, click Time Range in the header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-to-application-insights"></a><span data-ttu-id="b2e61-216">Enviar mais telemetria para o Application Insights</span><span class="sxs-lookup"><span data-stu-id="b2e61-216">Send more telemetry to Application Insights</span></span>
<span data-ttu-id="b2e61-217">Além de telemetria da caixa enviada pelo SDK do Application Insights, você pode:</span><span class="sxs-lookup"><span data-stu-id="b2e61-217">In addition to the out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="b2e61-218">Capturar rastreamentos de log da sua estrutura de registros favorita no [.NET](app-insights-asp-net-trace-logs.md) ou [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b2e61-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="b2e61-219">Isso significa que você pode pesquisar os rastreamentos de log e correlacioná-los com outros eventos, exceções e visualizações de página.</span><span class="sxs-lookup"><span data-stu-id="b2e61-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="b2e61-220">[Escrever código](app-insights-api-custom-events-metrics.md) para enviar eventos personalizados, visualizações de página e exceções.</span><span class="sxs-lookup"><span data-stu-id="b2e61-220">[Write code](app-insights-api-custom-events-metrics.md) to send custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="b2e61-221">[Saiba como enviar logs e telemetria personalizada para o Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b2e61-221">[Learn how to send logs and custom telemetry to Application Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <span data-ttu-id="b2e61-222"><a name="questions"></a>Perguntas e respostas</span><span class="sxs-lookup"><span data-stu-id="b2e61-222"><a name="questions"></a>Q & A</span></span>
### <span data-ttu-id="b2e61-223"><a name="limits"></a>Que quantidade de dados é mantida?</span><span class="sxs-lookup"><span data-stu-id="b2e61-223"><a name="limits"></a>How much data is retained?</span></span>

<span data-ttu-id="b2e61-224">Veja o [Resumo de limites](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="b2e61-224">See the [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="b2e61-225">Como consultar dados de POSTAGEM nas minhas solicitações de servidor?</span><span class="sxs-lookup"><span data-stu-id="b2e61-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="b2e61-226">Nós não registramos os dados de POST automaticamente, mas você pode usar [chamadas de log ou TrackTrace](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b2e61-226">We don't log the POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="b2e61-227">Coloque os dados de POSTAGEM no parâmetro de mensagem.</span><span class="sxs-lookup"><span data-stu-id="b2e61-227">Put the POST data in the message parameter.</span></span> <span data-ttu-id="b2e61-228">Não é possível filtrar a mensagem da mesma maneira que as propriedades, mas o limite de tamanho é maior.</span><span class="sxs-lookup"><span data-stu-id="b2e61-228">You can't filter on the message in the same way you can filter on properties, but the size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="b2e61-229">Vídeo</span><span class="sxs-lookup"><span data-stu-id="b2e61-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <span data-ttu-id="b2e61-230"><a name="add"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b2e61-230"><a name="add"></a>Next steps</span></span>
* [<span data-ttu-id="b2e61-231">Escrever consultas complexas no Analytics</span><span class="sxs-lookup"><span data-stu-id="b2e61-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="b2e61-232">Enviar logs e telemetria personalizada para o Application Insights</span><span class="sxs-lookup"><span data-stu-id="b2e61-232">Send logs and custom telemetry to Application Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="b2e61-233">Configurar testes de disponibilidade e capacidade de resposta</span><span class="sxs-lookup"><span data-stu-id="b2e61-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="b2e61-234">Solução de problemas</span><span class="sxs-lookup"><span data-stu-id="b2e61-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
