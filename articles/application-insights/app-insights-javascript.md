---
title: Application Insights do Azure para aplicativos Web JavaScript | Microsoft Docs
description: "Obter contagens de sessões e exibições de páginas e dados de clientes da Web e acompanhar padrões de uso. Detecte exceções e problemas de desempenho em páginas da Web do JavaScript."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 4e8a77e3644bb726d1b8e2050dab61893ccfa3c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="e0cc6-104">Application Insights para páginas da Web</span><span class="sxs-lookup"><span data-stu-id="e0cc6-104">Application Insights for web pages</span></span>
<span data-ttu-id="e0cc6-105">Saiba mais sobre o desempenho e o uso de sua página da Web ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-105">Find out about the performance and usage of your web page or app.</span></span> <span data-ttu-id="e0cc6-106">Se adicionar o [Application Insights](app-insights-overview.md) ao script de página, você obterá intervalos de carregamentos de página e chamadas AJAX, contagens e detalhes de exceções de navegador e falhas de AJAX, bem como contagens de usuários e sessões.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-106">If you add [Application Insights](app-insights-overview.md) to your page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="e0cc6-107">Todos esses itens podem ser segmentados por página, sistema operacional cliente e versão do navegador, localização geográfica e outras dimensões.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="e0cc6-108">Você pode definir alertas para contagens de falhas ou carregamento de páginas lento.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="e0cc6-109">E inserindo chamadas de rastreamento em seu código JavaScript, você pode controlar como os diferentes recursos do seu aplicativo de página da Web são usados.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-109">And by inserting trace calls in your JavaScript code, you can track how the different features of your web page application are used.</span></span>

<span data-ttu-id="e0cc6-110">O Application Insights pode ser usado com todas as páginas da Web: basta adicionar um breve trecho de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="e0cc6-111">Se o serviço Web for [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md), você poderá integrar a telemetria de seu servidor e clientes.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![Em portal.azure.com, abra o recurso do aplicativo e clique em Navegador](./media/app-insights-javascript/03.png)

<span data-ttu-id="e0cc6-113">Você precisa de uma assinatura do [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="e0cc6-113">You need a subscription to [Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="e0cc6-114">Se sua equipe tiver uma assinatura organizacional, peça ao proprietário que adicione sua Conta da Microsoft a ela.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-114">If your team has an organizational subscription, ask the owner to add your Microsoft Account to it.</span></span> <span data-ttu-id="e0cc6-115">O desenvolvimento e o uso em pequena escala não custam nada.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="e0cc6-116">Configurar o Application Insights para sua página da Web</span><span class="sxs-lookup"><span data-stu-id="e0cc6-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="e0cc6-117">Adicione o trecho de código do carregador para suas páginas da Web, conforme demonstrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-117">Add the loader code snippet to your web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="e0cc6-118">Abrir ou criar um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="e0cc6-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="e0cc6-119">O recurso Application Insights é onde os dados sobre o desempenho e o uso da página são exibidos.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-119">The Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="e0cc6-120">Entre no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e0cc6-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="e0cc6-121">Se tiver configurado o monitoramento do lado do servidor de seu aplicativo, você já terá um recurso:</span><span class="sxs-lookup"><span data-stu-id="e0cc6-121">If you already set up monitoring for the server side of your app, you already have a resource:</span></span>

![Escolha Procurar, Serviços de Desenvolvedor, Application Insights.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="e0cc6-123">Se não tiver um, crie-o:</span><span class="sxs-lookup"><span data-stu-id="e0cc6-123">If you don't have one, create it:</span></span>

![Escolha Novo, Serviços de Desenvolvedor, Application Insights.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="e0cc6-125">*Tem dúvidas?*</span><span class="sxs-lookup"><span data-stu-id="e0cc6-125">*Questions already?*</span></span> <span data-ttu-id="e0cc6-126">[Mais informações sobre a criação de um recurso](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e0cc6-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-the-sdk-script-to-your-app-or-web-pages"></a><span data-ttu-id="e0cc6-127">Adicione o script do SDK a seu aplicativo ou às suas páginas da Web</span><span class="sxs-lookup"><span data-stu-id="e0cc6-127">Add the SDK script to your app or web pages</span></span>
<span data-ttu-id="e0cc6-128">Em Início Rápido, obtenha o script para páginas da Web:</span><span class="sxs-lookup"><span data-stu-id="e0cc6-128">In Quick Start, get the script for web pages:</span></span>

![Na folha de visão geral de seu aplicativo, escolha Início Rápido, Obter o código para monitorar minhas páginas da Web.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="e0cc6-131">Insira o script antes da marca `</head>` de cada página que você deseja acompanhar. Se seu site possui uma página mestra, você poderá colocar o script lá.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-131">Insert the script just before the `</head>` tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="e0cc6-132">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0cc6-132">For example:</span></span>

* <span data-ttu-id="e0cc6-133">Em um projeto MVC ASP.NET, você deve colocá-lo em `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="e0cc6-133">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="e0cc6-134">Em um site do SharePoint, no painel de controle, abra [Configurações do Site/Página Mestra](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e0cc6-134">In a SharePoint site, on the control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="e0cc6-135">O script contém a chave de instrumentação que direciona os dados para o recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-135">The script contains the instrumentation key that directs the data to your Application Insights resource.</span></span> 

<span data-ttu-id="e0cc6-136">([Explicação mais detalhada do script](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/)).</span><span class="sxs-lookup"><span data-stu-id="e0cc6-136">([Deeper explanation of the script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="e0cc6-137">*(Se você estiver usando uma estrutura de página da Web conhecida, procure adaptadores do Application Insights. Por exemplo, há [um módulo AngularJS](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="e0cc6-137">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="e0cc6-138">Configuração detalhada</span><span class="sxs-lookup"><span data-stu-id="e0cc6-138">Detailed configuration</span></span>
<span data-ttu-id="e0cc6-139">Há vários [parâmetros](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) que você pode definir, embora, na maioria dos casos, isso não seja preciso.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-139">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="e0cc6-140">Por exemplo, você pode desabilitar ou limitar o número de chamadas Ajax relatadas por exibição de página (para reduzir o tráfego).</span><span class="sxs-lookup"><span data-stu-id="e0cc6-140">For example, you can disable or limit the number of Ajax calls reported per page view (to reduce traffic).</span></span> <span data-ttu-id="e0cc6-141">Ou então, você pode definir o modo de depuração para que a telemetria se mova rapidamente pelo pipeline sem sendo colocada em lotes.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-141">Or you can set debug mode to have telemetry move rapidly through the pipeline without being batched.</span></span>

<span data-ttu-id="e0cc6-142">Para definir esses parâmetros, procure esta linha no trecho de código e adicione mais itens separados por vírgula depois dela:</span><span class="sxs-lookup"><span data-stu-id="e0cc6-142">To set these parameters, look for this line in the code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="e0cc6-143">Os [parâmetros disponíveis](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) incluem:</span><span class="sxs-lookup"><span data-stu-id="e0cc6-143">The [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember to remove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, to reduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up to execution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="e0cc6-144"><a name="run"></a>Executar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="e0cc6-144"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="e0cc6-145">Execute seu aplicativo Web, use-o por algum tempo para gerar telemetria e aguarde alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-145">Run your web app, use it a while to generate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="e0cc6-146">Você pode executá-lo usando a tecla **F5** em seu computador de desenvolvimento ou publicá-lo e permitir que os usuários o utilizem.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-146">You can either run it using the **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="e0cc6-147">Se desejar verificar a telemetria que um aplicativo Web está enviando ao Application Insights, use as ferramentas de depuração de seu navegador (**F12** em muitos navegadores).</span><span class="sxs-lookup"><span data-stu-id="e0cc6-147">If you want to check the telemetry that a web app is sending to Application Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="e0cc6-148">Os dados são enviados a dc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-148">Data is sent to dc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="e0cc6-149">Explorar seus dados de desempenho do navegador</span><span class="sxs-lookup"><span data-stu-id="e0cc6-149">Explore your browser performance data</span></span>
<span data-ttu-id="e0cc6-150">Abra a folha Navegador para exibir dados de desempenho agregados dos navegadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-150">Open the Browser blade to show aggregated performance data from your users' browsers.</span></span>

![Em portal.azure.com, abra o recurso do aplicativo e clique em Configurações, Navegador](./media/app-insights-javascript/03.png)

<span data-ttu-id="e0cc6-152">*Não há dados ainda? Clique em **Atualizar** na parte superior da página. Nada mesmo assim? Consulte [Solução de problemas](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="e0cc6-152">*No data yet? Click **Refresh** at the top of the page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="e0cc6-153">A folha Navegadores é uma [folha do Metrics Explorer](app-insights-metrics-explorer.md) com filtros predefinidos e opções de gráfico.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-153">The Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="e0cc6-154">Você poderá editar o intervalo de tempo, os filtros e a configuração do gráfico, se desejar, e salvar o resultado como um favorito.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-154">You can edit the time range, filters, and chart configuration if you want, and save the result as a favorite.</span></span> <span data-ttu-id="e0cc6-155">Clique em **Restaurar padrões** para voltar para a configuração original da folha.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-155">Click **Restore defaults** to get back to the original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="e0cc6-156">Desempenho de carregamento de página</span><span class="sxs-lookup"><span data-stu-id="e0cc6-156">Page load performance</span></span>
<span data-ttu-id="e0cc6-157">Na parte superior, há um gráfico segmentado de tempos de carregamento de página.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-157">At the top is a segmented chart of page load times.</span></span> <span data-ttu-id="e0cc6-158">A altura total do gráfico representa o tempo médio para carregar e exibir páginas de seu aplicativo nos navegadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-158">The total height of the chart represents the average time to load and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="e0cc6-159">O tempo é medido desde quando o navegador envia a solicitação HTTP inicial até que os todos os eventos de carregamento síncronos tenham sido processados, incluindo layout e execução de scripts.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-159">The time is measured from when the browser sends the initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="e0cc6-160">Ele não inclui tarefas assíncronas, como carregar Web parts de chamadas AJAX.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-160">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="e0cc6-161">O gráfico segmenta o tempo de carregamento total da página nos [intervalos padrão definidos pelo W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="e0cc6-161">The chart segments the total page load time into the [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="e0cc6-162">Observe que o tempo de *conexão de rede* é frequentemente menor do que o esperado, pois ele é uma média sobre todas as solicitações do navegador para o servidor.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-162">Note that the *network connect* time is often lower than you might expect, because it's an average over all requests from the browser to the server.</span></span> <span data-ttu-id="e0cc6-163">Muitas solicitações individuais têm um tempo de conexão igual a 0 porque já existe uma conexão ativa com o servidor.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-163">Many individual requests have a connect time of 0 because there is already an active connection to the server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="e0cc6-164">Carregamento lento?</span><span class="sxs-lookup"><span data-stu-id="e0cc6-164">Slow loading?</span></span>
<span data-ttu-id="e0cc6-165">O carregamento de página lento é uma grande fonte de insatisfação para seus usuários.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-165">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="e0cc6-166">Se o gráfico indicar o carregamento de página lento, será fácil fazer algumas pesquisas de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-166">If the chart indicates slow page loads, it's easy to do some diagnostic research.</span></span>

<span data-ttu-id="e0cc6-167">O gráfico mostra a média de todos os carregamentos de página em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-167">The chart shows the average of all page loads in your app.</span></span> <span data-ttu-id="e0cc6-168">Para ver se o problema é restrito a páginas específicas, observe mais adiante na folha, onde há uma grade segmentada por URL de página:</span><span class="sxs-lookup"><span data-stu-id="e0cc6-168">To see if the problem is confined to particular pages, look further down the blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="e0cc6-169">Observe a contagem de exibições de páginas e o desvio padrão.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-169">Notice the page view count and standard deviation.</span></span> <span data-ttu-id="e0cc6-170">Se a contagem de páginas for muito baixa, o problema não está afetando muito os usuários.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-170">If the page count is very low, then the issue isn't affecting users much.</span></span> <span data-ttu-id="e0cc6-171">Um desvio padrão alto (comparável à média em si) indica muita variação entre medidas individuais.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-171">A high standard deviation (comparable to the average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="e0cc6-172">**Aplicar zoom em uma URL e uma exibição de página.**</span><span class="sxs-lookup"><span data-stu-id="e0cc6-172">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="e0cc6-173">Clique em qualquer nome de página para ver uma folha de gráficos de navegador filtrados apenas para essa URL e, em seguida, em uma instância de uma exibição de página.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-173">Click any page name to see a blade of browser charts filtered just to that URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="e0cc6-174">Clique em `...` para obter uma lista completa das propriedades do evento ou inspecionar as chamadas Ajax e os eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-174">Click `...` for a full list of properties for that event, or inspect the Ajax calls and related events.</span></span> <span data-ttu-id="e0cc6-175">Chamadas Ajax lentas afetam o tempo de carregamento de página geral se são síncronas.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-175">Slow Ajax calls affect the overall page load time if they are synchronous.</span></span> <span data-ttu-id="e0cc6-176">Eventos relacionados incluem solicitações do servidor para a mesma URL (se você configurou o Application Insights em seu servidor Web).</span><span class="sxs-lookup"><span data-stu-id="e0cc6-176">Related events include server requests for the same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="e0cc6-177">**Desempenho da página ao longo do tempo.**</span><span class="sxs-lookup"><span data-stu-id="e0cc6-177">**Page performance over time.**</span></span> <span data-ttu-id="e0cc6-178">De volta à folha Navegadores, altere a grade de Tempo de Carregamento de Exibição de Página para um gráfico de linhas para ver se houve picos em determinados horários:</span><span class="sxs-lookup"><span data-stu-id="e0cc6-178">Back at the Browsers blade, change the Page View Load Time grid into a line chart to see if there were peaks at particular times:</span></span>

![Clique no cabeçalho da grade e selecione um novo tipo de gráfico](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="e0cc6-180">**Segmentar por outras dimensões.**</span><span class="sxs-lookup"><span data-stu-id="e0cc6-180">**Segment by other dimensions.**</span></span> <span data-ttu-id="e0cc6-181">Será que as páginas têm carregamento mais lento em determinado navegador, sistema operacional cliente ou localidade do usuário?</span><span class="sxs-lookup"><span data-stu-id="e0cc6-181">Maybe your pages are slower to load on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="e0cc6-182">Adicione um novo gráfico e experimente a dimensão **Agrupar por** .</span><span class="sxs-lookup"><span data-stu-id="e0cc6-182">Add a new chart and experiment with the **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="e0cc6-183">Desempenho do AJAX</span><span class="sxs-lookup"><span data-stu-id="e0cc6-183">AJAX Performance</span></span>
<span data-ttu-id="e0cc6-184">Verifique se chamadas AJAX em páginas da Web estão tendo um bom desempenho.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-184">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="e0cc6-185">Elas geralmente são usadas para preencher partes da página de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-185">They are often used to fill parts of your page asynchronously.</span></span> <span data-ttu-id="e0cc6-186">Embora a página geral possa ser carregada imediatamente, seus usuários podem ficar frustrados ao observar Web parts em branco, aguardando até que os dados apareçam nelas.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-186">Although the overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data to appear in them.</span></span>

<span data-ttu-id="e0cc6-187">As chamadas AJAX feitas de sua página da Web são mostradas na folha Navegadores como dependências.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-187">AJAX calls made from your web page are shown on the Browsers blade as dependencies.</span></span>

<span data-ttu-id="e0cc6-188">Há gráficos de resumo na parte superior da folha:</span><span class="sxs-lookup"><span data-stu-id="e0cc6-188">There are summary charts in the upper part of the blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="e0cc6-189">e grades detalhadas mais abaixo:</span><span class="sxs-lookup"><span data-stu-id="e0cc6-189">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="e0cc6-190">Clique em qualquer linha para obter detalhes específicos.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-190">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="e0cc6-191">Se você excluir o filtro Navegadores na folha, as dependências de servidor e AJAX serão incluídas nesses gráficos.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-191">If you delete the Browsers filter on the blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="e0cc6-192">Clique em Restaurar padrões para reconfigurar o filtro.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-192">Click Restore Defaults to reconfigure the filter.</span></span>
> 
> 

<span data-ttu-id="e0cc6-193">**Para analisar detalhadamente as falhas de chamadas Ajax** , role para baixo até a grade Falhas de dependência e clique em uma linha para ver as instâncias específicas.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-193">**To drill into failed Ajax calls** scroll down to the Dependency failures grid, and then click a row to see specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="e0cc6-194">Clique em `...` para ver a telemetria completa de uma chamada Ajax.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-194">Click `...` for the full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="e0cc6-195">Nenhuma chamada Ajax foi relatada?</span><span class="sxs-lookup"><span data-stu-id="e0cc6-195">No Ajax calls reported?</span></span>
<span data-ttu-id="e0cc6-196">As chamadas Ajax incluem todas as chamadas HTTP feitas do script da página da Web.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-196">Ajax calls include any HTTP/HTTPS  calls made from the script of your web page.</span></span> <span data-ttu-id="e0cc6-197">Se elas não forem relatadas, verifique se o trecho de código não define os [parâmetros](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableAjaxTracking` ou `maxAjaxCallsPerView`.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-197">If you don't see them reported, check that the code snippet doesn't set the `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="e0cc6-198">Exceções de navegador</span><span class="sxs-lookup"><span data-stu-id="e0cc6-198">Browser exceptions</span></span>
<span data-ttu-id="e0cc6-199">Na folha Navegadores, há um gráfico de resumo de exceções e uma grade dos tipos de exceção mais abaixo na folha.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-199">On the Browsers blade, there's an exceptions summary chart, and a grid of exception types further down the blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="e0cc6-200">Se não forem relatadas exceções de navegador, verifique se o trecho de código não define o [parâmetro](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableExceptionTracking`.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-200">If you don't see browser exceptions reported, check that the code snippet doesn't set the `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="e0cc6-201">Inspecionar eventos de exibição de páginas individuais</span><span class="sxs-lookup"><span data-stu-id="e0cc6-201">Inspect individual page view events</span></span>

<span data-ttu-id="e0cc6-202">Normalmente a telemetria de exibição da página é analisada pelo Application Insights e você vê somente relatórios cumulativos, calculados sobre todos os seus usuários.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-202">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="e0cc6-203">Mas para a finalidade de depuração, você também pode olhar para os eventos de exibição da página individua.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-203">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="e0cc6-204">Na folha de Pesquisa de Diagnóstico, defina Filtros para Exibição da Página.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-204">In the Diagnostic Search blade, set Filters to Page View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="e0cc6-205">Selecione qualquer evento para ver mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-205">Select any event to see more detail.</span></span> <span data-ttu-id="e0cc6-206">Na página de detalhes, clique em "..." para ver mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-206">In the details page, click "..." to see even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="e0cc6-207">Se você usar [Pesquisar](app-insights-diagnostic-search.md), observe que precisa fazer a correspondência de palavras inteiras: "Sobr" e "obre" não correspondem a "Sobre".</span><span class="sxs-lookup"><span data-stu-id="e0cc6-207">If you use [Search](app-insights-diagnostic-search.md), notice that you have to match whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="e0cc6-208">Você também pode usar a poderosa [linguagem de consulta do Log Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) para pesquisar exibições de página.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-208">You can also use the powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) to search page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="e0cc6-209">Propriedades de exibição de página</span><span class="sxs-lookup"><span data-stu-id="e0cc6-209">Page view properties</span></span>
* <span data-ttu-id="e0cc6-210">**Duração do modo de exibição de página**</span><span class="sxs-lookup"><span data-stu-id="e0cc6-210">**Page view duration**</span></span> 
  
  * <span data-ttu-id="e0cc6-211">Por padrão, o tempo necessário para carregar a página, desde a solicitação do cliente até o carregamento completo (incluindo arquivos auxiliares, mas excluindo tarefas assíncronas, como chamadas do Ajax).</span><span class="sxs-lookup"><span data-stu-id="e0cc6-211">By default, the time it takes to load the page, from client request to full load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="e0cc6-212">Se você definir `overridePageViewDuration` no [configuração de página](#detailed-configuration), o intervalo entre a solicitação do cliente e a execução do primeiro `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-212">If you set `overridePageViewDuration` in the [page configuration](#detailed-configuration), the interval between client request to execution of the first `trackPageView`.</span></span> <span data-ttu-id="e0cc6-213">Se você moveu trackPageView da sua posição normal após a inicialização do script, ele refletirá um valor diferente.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-213">If you moved trackPageView from its usual position after the initialization of the script, it will reflect a different value.</span></span>
  * <span data-ttu-id="e0cc6-214">Se `overridePageViewDuration` for definido e um argumento de duração for fornecido na chamada `trackPageView()`, o valor do argumento será usado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-214">If `overridePageViewDuration` is set and a duration argument is provided in the `trackPageView()` call, then the argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="e0cc6-215">Contagens da página personalizada</span><span class="sxs-lookup"><span data-stu-id="e0cc6-215">Custom page counts</span></span>
<span data-ttu-id="e0cc6-216">Por padrão, uma contagem de página ocorre todas as vezes que uma nova página carrega no navegador do cliente.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-216">By default, a page count occurs each time a new page loads into the client browser.</span></span>  <span data-ttu-id="e0cc6-217">Por exemplo, você talvez queira contar visualizações de página adicionais.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-217">But you might want to count additional page views.</span></span> <span data-ttu-id="e0cc6-218">Por exemplo, uma página pode exibir seu conteúdo em guias e você quer contar uma página quando o usuário muda as guias.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-218">For example, a page might display its content in tabs and you want to count a page when the user switches tabs.</span></span> <span data-ttu-id="e0cc6-219">Ou o código do JavaScript na página pode carregar novo conteúdo sem mudar a URL do navegador.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-219">Or JavaScript code in the page might load new content without changing the browser's URL.</span></span>

<span data-ttu-id="e0cc6-220">Insira uma chamada do JavaScript como essa no ponto apropriado no código do seu cliente:</span><span class="sxs-lookup"><span data-stu-id="e0cc6-220">Insert a JavaScript call like this at the appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="e0cc6-221">O nome da página pode conter os mesmos caracteres da URL, mas nada após o "#" ou "?" é ignorado.</span><span class="sxs-lookup"><span data-stu-id="e0cc6-221">The page name can contain the same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="e0cc6-222">Acompanhamento de uso</span><span class="sxs-lookup"><span data-stu-id="e0cc6-222">Usage tracking</span></span>
<span data-ttu-id="e0cc6-223">Quer saber o que os usuários fazem com seu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="e0cc6-223">Want to find out what your users do with your app?</span></span>

* [<span data-ttu-id="e0cc6-224">Saiba mais sobre acompanhamento de uso</span><span class="sxs-lookup"><span data-stu-id="e0cc6-224">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="e0cc6-225">[Saiba mais sobre os eventos e as métricas personalizados de API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e0cc6-225">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="e0cc6-226"><a name="video"></a> Vídeo</span><span class="sxs-lookup"><span data-stu-id="e0cc6-226"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="e0cc6-227"><a name="next"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0cc6-227"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="e0cc6-228">Acompanhar uso</span><span class="sxs-lookup"><span data-stu-id="e0cc6-228">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="e0cc6-229">Eventos e métricas personalizados</span><span class="sxs-lookup"><span data-stu-id="e0cc6-229">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="e0cc6-230">Build-measure-learn</span><span class="sxs-lookup"><span data-stu-id="e0cc6-230">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

