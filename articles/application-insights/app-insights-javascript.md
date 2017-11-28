---
title: aplicativos web do aaaAzure Application Insights para JavaScript | Microsoft Docs
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
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="a2207-104">Application Insights para páginas da Web</span><span class="sxs-lookup"><span data-stu-id="a2207-104">Application Insights for web pages</span></span>
<span data-ttu-id="a2207-105">Saiba mais sobre o desempenho de saudação e o uso de seu aplicativo ou página da web.</span><span class="sxs-lookup"><span data-stu-id="a2207-105">Find out about hello performance and usage of your web page or app.</span></span> <span data-ttu-id="a2207-106">Se você adicionar [Application Insights](app-insights-overview.md) tooyour script de página, você obter intervalos de página for carregada e chamadas AJAX, contagens e detalhes de exceções de navegador e falhas de AJAX, bem como os usuários e contagens de sessão.</span><span class="sxs-lookup"><span data-stu-id="a2207-106">If you add [Application Insights](app-insights-overview.md) tooyour page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="a2207-107">Todos esses itens podem ser segmentados por página, sistema operacional cliente e versão do navegador, localização geográfica e outras dimensões.</span><span class="sxs-lookup"><span data-stu-id="a2207-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="a2207-108">Você pode definir alertas para contagens de falhas ou carregamento de páginas lento.</span><span class="sxs-lookup"><span data-stu-id="a2207-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="a2207-109">E inserindo chamadas de rastreamento no seu código JavaScript, você pode controlar como os diferentes recursos de saudação do seu aplicativo de página da web são usados.</span><span class="sxs-lookup"><span data-stu-id="a2207-109">And by inserting trace calls in your JavaScript code, you can track how hello different features of your web page application are used.</span></span>

<span data-ttu-id="a2207-110">O Application Insights pode ser usado com todas as páginas da Web: basta adicionar um breve trecho de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a2207-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="a2207-111">Se o serviço Web for [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md), você poderá integrar a telemetria de seu servidor e clientes.</span><span class="sxs-lookup"><span data-stu-id="a2207-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![Em portal.azure.com, abra o recurso do aplicativo e clique em Navegador](./media/app-insights-javascript/03.png)

<span data-ttu-id="a2207-113">Você precisa de uma assinatura muito[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2207-113">You need a subscription too[Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="a2207-114">Se sua equipe tem uma assinatura organizacional, peça ao Olá proprietário tooadd seu tooit Account da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a2207-114">If your team has an organizational subscription, ask hello owner tooadd your Microsoft Account tooit.</span></span> <span data-ttu-id="a2207-115">O desenvolvimento e o uso em pequena escala não custam nada.</span><span class="sxs-lookup"><span data-stu-id="a2207-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="a2207-116">Configurar o Application Insights para sua página da Web</span><span class="sxs-lookup"><span data-stu-id="a2207-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="a2207-117">Adicione páginas Olá carregador código trecho tooyour da web, da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="a2207-117">Add hello loader code snippet tooyour web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="a2207-118">Abrir ou criar um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="a2207-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="a2207-119">saudação de recurso do Application Insights é onde os dados sobre o desempenho e o uso da página são exibidos.</span><span class="sxs-lookup"><span data-stu-id="a2207-119">hello Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="a2207-120">Entre no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2207-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="a2207-121">Se você definiu o monitoramento do lado do servidor de saudação do seu aplicativo, você já tem um recurso:</span><span class="sxs-lookup"><span data-stu-id="a2207-121">If you already set up monitoring for hello server side of your app, you already have a resource:</span></span>

![Escolha Procurar, Serviços de Desenvolvedor, Application Insights.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="a2207-123">Se não tiver um, crie-o:</span><span class="sxs-lookup"><span data-stu-id="a2207-123">If you don't have one, create it:</span></span>

![Escolha Novo, Serviços de Desenvolvedor, Application Insights.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="a2207-125">*Tem dúvidas?*</span><span class="sxs-lookup"><span data-stu-id="a2207-125">*Questions already?*</span></span> <span data-ttu-id="a2207-126">[Mais informações sobre a criação de um recurso](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="a2207-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a><span data-ttu-id="a2207-127">Adicionar Olá SDK script tooyour aplicativo ou páginas da web</span><span class="sxs-lookup"><span data-stu-id="a2207-127">Add hello SDK script tooyour app or web pages</span></span>
<span data-ttu-id="a2207-128">No início rápido, obter o script hello para páginas da web:</span><span class="sxs-lookup"><span data-stu-id="a2207-128">In Quick Start, get hello script for web pages:</span></span>

![Na folha de visão geral sobre seu aplicativo, selecione início rápido, obter código toomonitor minhas páginas da web.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="a2207-131">Inserir o script hello antes Olá `</head>` marca de cada página que você deseja tootrack.</span><span class="sxs-lookup"><span data-stu-id="a2207-131">Insert hello script just before hello `</head>` tag of every page you want tootrack.</span></span> <span data-ttu-id="a2207-132">Se o site tiver uma página mestre, você pode colocar o script hello existe.</span><span class="sxs-lookup"><span data-stu-id="a2207-132">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="a2207-133">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a2207-133">For example:</span></span>

* <span data-ttu-id="a2207-134">Em um projeto MVC ASP.NET, você deve colocá-lo em `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="a2207-134">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="a2207-135">Em um site do SharePoint, no painel de controle do hello, abra [configurações do Site / página mestra](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="a2207-135">In a SharePoint site, on hello control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="a2207-136">script Hello contém a chave de instrumentação Olá que direciona o recurso do Application Insights do hello dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2207-136">hello script contains hello instrumentation key that directs hello data tooyour Application Insights resource.</span></span> 

<span data-ttu-id="a2207-137">([Explicação mais profunda sobre script hello. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="a2207-137">([Deeper explanation of hello script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="a2207-138">*(Se você estiver usando uma estrutura de página da Web conhecida, procure adaptadores do Application Insights. Por exemplo, há [um módulo AngularJS](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="a2207-138">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="a2207-139">Configuração detalhada</span><span class="sxs-lookup"><span data-stu-id="a2207-139">Detailed configuration</span></span>
<span data-ttu-id="a2207-140">Há vários [parâmetros](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) que você pode definir, embora, na maioria dos casos, isso não seja preciso.</span><span class="sxs-lookup"><span data-stu-id="a2207-140">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="a2207-141">Por exemplo, você pode desabilitar ou limitar o número de saudação de chamadas Ajax relatado por modo de exibição de página (tooreduce tráfego).</span><span class="sxs-lookup"><span data-stu-id="a2207-141">For example, you can disable or limit hello number of Ajax calls reported per page view (tooreduce traffic).</span></span> <span data-ttu-id="a2207-142">Ou você pode configurar depuração modo toohave telemetria mover rapidamente por meio do pipeline de saudação sem sendo processadas em lotes.</span><span class="sxs-lookup"><span data-stu-id="a2207-142">Or you can set debug mode toohave telemetry move rapidly through hello pipeline without being batched.</span></span>

<span data-ttu-id="a2207-143">tooset esses parâmetros, pesquisar esta linha no trecho de código hello e adicionar mais itens separados por vírgula após:</span><span class="sxs-lookup"><span data-stu-id="a2207-143">tooset these parameters, look for this line in hello code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="a2207-144">Olá [parâmetros disponíveis](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) incluem:</span><span class="sxs-lookup"><span data-stu-id="a2207-144">hello [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="a2207-145"><a name="run"></a>Executar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="a2207-145"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="a2207-146">Executar seu aplicativo web, usam um enquanto toogenerate telemetria e aguarde um pouco.</span><span class="sxs-lookup"><span data-stu-id="a2207-146">Run your web app, use it a while toogenerate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="a2207-147">Você pode executar usando Olá **F5** da chave no computador de desenvolvimento, ou publicá-lo e permitir que os usuários brincar com ele.</span><span class="sxs-lookup"><span data-stu-id="a2207-147">You can either run it using hello **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="a2207-148">Se você quiser toocheck telemetria de saudação que um aplicativo web está enviando tooApplication Insights, use as ferramentas de depuração do seu navegador (**F12** em muitos navegadores).</span><span class="sxs-lookup"><span data-stu-id="a2207-148">If you want toocheck hello telemetry that a web app is sending tooApplication Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="a2207-149">Dados são enviados toodc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="a2207-149">Data is sent toodc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="a2207-150">Explorar seus dados de desempenho do navegador</span><span class="sxs-lookup"><span data-stu-id="a2207-150">Explore your browser performance data</span></span>
<span data-ttu-id="a2207-151">Olá abrir navegador folha tooshow agregados dados de desempenho de navegadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="a2207-151">Open hello Browser blade tooshow aggregated performance data from your users' browsers.</span></span>

![Em portal.azure.com, abra o recurso do aplicativo e clique em Configurações, Navegador](./media/app-insights-javascript/03.png)

<span data-ttu-id="a2207-153">*Não há dados ainda? Clique em **atualização** no início de saudação da página de saudação. Nada mesmo assim? Consulte [Solução de problemas](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="a2207-153">*No data yet? Click **Refresh** at hello top of hello page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="a2207-154">Olá navegador folha é um [folha do Metrics Explorer](app-insights-metrics-explorer.md) com filtros predefinidos e as opções de gráfico.</span><span class="sxs-lookup"><span data-stu-id="a2207-154">hello Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="a2207-155">Você pode editar o intervalo de tempo de saudação, filtros e configuração de gráfico se desejar e salvar o resultado da saudação como um favorito.</span><span class="sxs-lookup"><span data-stu-id="a2207-155">You can edit hello time range, filters, and chart configuration if you want, and save hello result as a favorite.</span></span> <span data-ttu-id="a2207-156">Clique em **restaurar padrões** configuração de folha tooget toohello back original.</span><span class="sxs-lookup"><span data-stu-id="a2207-156">Click **Restore defaults** tooget back toohello original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="a2207-157">Desempenho de carregamento de página</span><span class="sxs-lookup"><span data-stu-id="a2207-157">Page load performance</span></span>
<span data-ttu-id="a2207-158">Em Olá superior é um gráfico segmentado de tempos de carregamento de página.</span><span class="sxs-lookup"><span data-stu-id="a2207-158">At hello top is a segmented chart of page load times.</span></span> <span data-ttu-id="a2207-159">altura total de saudação do gráfico de saudação representa Olá tempo médio tooload e exibir páginas de seu aplicativo nos navegadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="a2207-159">hello total height of hello chart represents hello average time tooload and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="a2207-160">tempo de saudação é medido a partir quando navegador Olá envia a solicitação HTTP inicial de saudação até que a carga síncrona todos os eventos tiverem sido processados, incluindo o layout e a execução de scripts.</span><span class="sxs-lookup"><span data-stu-id="a2207-160">hello time is measured from when hello browser sends hello initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="a2207-161">Ele não inclui tarefas assíncronas, como carregar Web parts de chamadas AJAX.</span><span class="sxs-lookup"><span data-stu-id="a2207-161">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="a2207-162">gráfico de saudação segmentos tempo de carregamento de página total Olá em hello [intervalos padrão definidos pelo W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="a2207-162">hello chart segments hello total page load time into hello [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="a2207-163">Observe que Olá *de conexão de rede* tempo geralmente é menor do que o esperado, pois é uma média sobre todas as solicitações do servidor de toohello navegador hello.</span><span class="sxs-lookup"><span data-stu-id="a2207-163">Note that hello *network connect* time is often lower than you might expect, because it's an average over all requests from hello browser toohello server.</span></span> <span data-ttu-id="a2207-164">Muitas solicitações individuais têm um tempo de conexão de 0 porque já existe um servidor de toohello conexão ativa.</span><span class="sxs-lookup"><span data-stu-id="a2207-164">Many individual requests have a connect time of 0 because there is already an active connection toohello server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="a2207-165">Carregamento lento?</span><span class="sxs-lookup"><span data-stu-id="a2207-165">Slow loading?</span></span>
<span data-ttu-id="a2207-166">O carregamento de página lento é uma grande fonte de insatisfação para seus usuários.</span><span class="sxs-lookup"><span data-stu-id="a2207-166">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="a2207-167">Se o gráfico de saudação indica carregamentos de página lento, é fácil toodo algumas pesquisas de diagnóstica.</span><span class="sxs-lookup"><span data-stu-id="a2207-167">If hello chart indicates slow page loads, it's easy toodo some diagnostic research.</span></span>

<span data-ttu-id="a2207-168">gráfico de saudação mostra a média de saudação de todas as cargas de página em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a2207-168">hello chart shows hello average of all page loads in your app.</span></span> <span data-ttu-id="a2207-169">toosee se o problema de saudação confinados tooparticular páginas, aparência ainda mais para baixo folha hello, onde há uma grade segmentada por URL da página:</span><span class="sxs-lookup"><span data-stu-id="a2207-169">toosee if hello problem is confined tooparticular pages, look further down hello blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="a2207-170">Observe a contagem de exibição de página hello e o desvio padrão.</span><span class="sxs-lookup"><span data-stu-id="a2207-170">Notice hello page view count and standard deviation.</span></span> <span data-ttu-id="a2207-171">Se a contagem de páginas de saudação é muito baixa, em seguida, problema de saudação não está afetando usuários muito.</span><span class="sxs-lookup"><span data-stu-id="a2207-171">If hello page count is very low, then hello issue isn't affecting users much.</span></span> <span data-ttu-id="a2207-172">Desvio padrão (média de toohello comparável em si) alta indica muita variação entre medidas individuais.</span><span class="sxs-lookup"><span data-stu-id="a2207-172">A high standard deviation (comparable toohello average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="a2207-173">**Aplicar zoom em uma URL e uma exibição de página.**</span><span class="sxs-lookup"><span data-stu-id="a2207-173">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="a2207-174">Clique em qualquer nome de página toosee uma folha de navegador gráficos filtrados toothat apenas URL; e, em seguida, em uma instância de uma exibição de página.</span><span class="sxs-lookup"><span data-stu-id="a2207-174">Click any page name toosee a blade of browser charts filtered just toothat URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="a2207-175">Clique em `...` para obter uma lista completa de propriedades para esse evento, ou inspecionar chamadas Ajax de saudação e eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="a2207-175">Click `...` for a full list of properties for that event, or inspect hello Ajax calls and related events.</span></span> <span data-ttu-id="a2207-176">Chamadas lentas do Ajax afetam Olá tempo de carregamento de página geral, se eles são síncronos.</span><span class="sxs-lookup"><span data-stu-id="a2207-176">Slow Ajax calls affect hello overall page load time if they are synchronous.</span></span> <span data-ttu-id="a2207-177">Relacionados a eventos incluem solicitações do servidor de saudação mesma URL (se você configurou o Application Insights no seu servidor web).</span><span class="sxs-lookup"><span data-stu-id="a2207-177">Related events include server requests for hello same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="a2207-178">**Desempenho da página ao longo do tempo.**</span><span class="sxs-lookup"><span data-stu-id="a2207-178">**Page performance over time.**</span></span> <span data-ttu-id="a2207-179">Na folha de navegadores hello, altere grade de tempo de carregamento da exibição de página de saudação em uma toosee de gráfico de linha se houvesse picos em momentos específicos:</span><span class="sxs-lookup"><span data-stu-id="a2207-179">Back at hello Browsers blade, change hello Page View Load Time grid into a line chart toosee if there were peaks at particular times:</span></span>

![Clique em cabeçalho Olá da grade de saudação e selecione um novo tipo de gráfico](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="a2207-181">**Segmentar por outras dimensões.**</span><span class="sxs-lookup"><span data-stu-id="a2207-181">**Segment by other dimensions.**</span></span> <span data-ttu-id="a2207-182">Talvez as páginas estão tooload mais lento em uma localidade específica do navegador, do sistema operacional cliente ou usuário?</span><span class="sxs-lookup"><span data-stu-id="a2207-182">Maybe your pages are slower tooload on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="a2207-183">Adicionar um novo gráfico e fazer experiências com hello **Agrupar por** dimensão.</span><span class="sxs-lookup"><span data-stu-id="a2207-183">Add a new chart and experiment with hello **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="a2207-184">Desempenho do AJAX</span><span class="sxs-lookup"><span data-stu-id="a2207-184">AJAX Performance</span></span>
<span data-ttu-id="a2207-185">Verifique se chamadas AJAX em páginas da Web estão tendo um bom desempenho.</span><span class="sxs-lookup"><span data-stu-id="a2207-185">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="a2207-186">Elas geralmente são usados toofill partes da página de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="a2207-186">They are often used toofill parts of your page asynchronously.</span></span> <span data-ttu-id="a2207-187">Embora hello página geral pode carregar imediatamente, os usuários podem ser frustrados diante de partes da web em branco, aguardando tooappear dados neles.</span><span class="sxs-lookup"><span data-stu-id="a2207-187">Although hello overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data tooappear in them.</span></span>

<span data-ttu-id="a2207-188">Chamadas AJAX feitas na página da web são mostradas na folha de navegadores hello como dependências.</span><span class="sxs-lookup"><span data-stu-id="a2207-188">AJAX calls made from your web page are shown on hello Browsers blade as dependencies.</span></span>

<span data-ttu-id="a2207-189">Gráficos de resumo na parte superior de saudação da folha de saudação são:</span><span class="sxs-lookup"><span data-stu-id="a2207-189">There are summary charts in hello upper part of hello blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="a2207-190">e grades detalhadas mais abaixo:</span><span class="sxs-lookup"><span data-stu-id="a2207-190">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="a2207-191">Clique em qualquer linha para obter detalhes específicos.</span><span class="sxs-lookup"><span data-stu-id="a2207-191">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="a2207-192">Se você excluir o filtro de navegadores Olá na folha hello, servidor e dependências de AJAX inclusos nesses gráficos.</span><span class="sxs-lookup"><span data-stu-id="a2207-192">If you delete hello Browsers filter on hello blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="a2207-193">Clique em filtro de saudação tooreconfigure restaurar padrões.</span><span class="sxs-lookup"><span data-stu-id="a2207-193">Click Restore Defaults tooreconfigure hello filter.</span></span>
> 
> 

<span data-ttu-id="a2207-194">**toodrill em chamadas Ajax com falha** Role para baixo da grade de falhas de dependência de toohello e, em seguida, clique em um instâncias específicas de toosee de linha.</span><span class="sxs-lookup"><span data-stu-id="a2207-194">**toodrill into failed Ajax calls** scroll down toohello Dependency failures grid, and then click a row toosee specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="a2207-195">Clique em `...` de telemetria de saudação completo para uma chamada Ajax.</span><span class="sxs-lookup"><span data-stu-id="a2207-195">Click `...` for hello full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="a2207-196">Nenhuma chamada Ajax foi relatada?</span><span class="sxs-lookup"><span data-stu-id="a2207-196">No Ajax calls reported?</span></span>
<span data-ttu-id="a2207-197">Chamadas AJAX incluem todas as chamadas HTTP/HTTPS feitas do script hello da página da web.</span><span class="sxs-lookup"><span data-stu-id="a2207-197">Ajax calls include any HTTP/HTTPS  calls made from hello script of your web page.</span></span> <span data-ttu-id="a2207-198">Se você não vê-los relatado, verifique desse trecho de código Olá não definida Olá `disableAjaxTracking` ou `maxAjaxCallsPerView` [parâmetros](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="a2207-198">If you don't see them reported, check that hello code snippet doesn't set hello `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="a2207-199">Exceções de navegador</span><span class="sxs-lookup"><span data-stu-id="a2207-199">Browser exceptions</span></span>
<span data-ttu-id="a2207-200">Na folha de navegadores hello, há um gráfico de resumo de exceções e uma grade dos tipos de exceção ainda mais para baixo de folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2207-200">On hello Browsers blade, there's an exceptions summary chart, and a grid of exception types further down hello blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="a2207-201">Se você não vir as exceções de navegador relatadas, verifique desse trecho de código Olá não define Olá `disableExceptionTracking` [parâmetro](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="a2207-201">If you don't see browser exceptions reported, check that hello code snippet doesn't set hello `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="a2207-202">Inspecionar eventos de exibição de páginas individuais</span><span class="sxs-lookup"><span data-stu-id="a2207-202">Inspect individual page view events</span></span>

<span data-ttu-id="a2207-203">Normalmente a telemetria de exibição da página é analisada pelo Application Insights e você vê somente relatórios cumulativos, calculados sobre todos os seus usuários.</span><span class="sxs-lookup"><span data-stu-id="a2207-203">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="a2207-204">Mas para a finalidade de depuração, você também pode olhar para os eventos de exibição da página individua.</span><span class="sxs-lookup"><span data-stu-id="a2207-204">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="a2207-205">Na folha de diagnóstico pesquisa hello, defina filtros tooPage exibição.</span><span class="sxs-lookup"><span data-stu-id="a2207-205">In hello Diagnostic Search blade, set Filters tooPage View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="a2207-206">Selecione qualquer evento toosee mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="a2207-206">Select any event toosee more detail.</span></span> <span data-ttu-id="a2207-207">Na página de detalhes do hello, clique em "…" toosee ainda mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="a2207-207">In hello details page, click "..." toosee even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="a2207-208">Se você usar [pesquisa](app-insights-diagnostic-search.md), observe que você tenha palavras inteiras toomatch: "Sobre" e "sobre" não coincidem "Sobre".</span><span class="sxs-lookup"><span data-stu-id="a2207-208">If you use [Search](app-insights-diagnostic-search.md), notice that you have toomatch whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="a2207-209">Você também pode usar Olá poderoso [linguagem de consulta de análise de Log](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch modos de exibição de página.</span><span class="sxs-lookup"><span data-stu-id="a2207-209">You can also use hello powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="a2207-210">Propriedades de exibição de página</span><span class="sxs-lookup"><span data-stu-id="a2207-210">Page view properties</span></span>
* <span data-ttu-id="a2207-211">**Duração do modo de exibição de página**</span><span class="sxs-lookup"><span data-stu-id="a2207-211">**Page view duration**</span></span> 
  
  * <span data-ttu-id="a2207-212">Por padrão, Olá tempo que demora tooload Olá página, carga de toofull de solicitação de cliente (incluindo arquivos auxiliares, mas excluindo tarefas assíncronas, como chamadas Ajax).</span><span class="sxs-lookup"><span data-stu-id="a2207-212">By default, hello time it takes tooload hello page, from client request toofull load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="a2207-213">Se você definir `overridePageViewDuration` em Olá [configuração de página](#detailed-configuration), Olá intervalo entre tooexecution de solicitação de cliente de saudação primeiro `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="a2207-213">If you set `overridePageViewDuration` in hello [page configuration](#detailed-configuration), hello interval between client request tooexecution of hello first `trackPageView`.</span></span> <span data-ttu-id="a2207-214">Se você tiver movido trackPageView de sua posição normal após a inicialização de saudação do script hello, ele refletirá um valor diferente.</span><span class="sxs-lookup"><span data-stu-id="a2207-214">If you moved trackPageView from its usual position after hello initialization of hello script, it will reflect a different value.</span></span>
  * <span data-ttu-id="a2207-215">Se `overridePageViewDuration` é definido e uma duração argumento for fornecido no hello `trackPageView()` chamar, em seguida, o valor do argumento Olá é usado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="a2207-215">If `overridePageViewDuration` is set and a duration argument is provided in hello `trackPageView()` call, then hello argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="a2207-216">Contagens da página personalizada</span><span class="sxs-lookup"><span data-stu-id="a2207-216">Custom page counts</span></span>
<span data-ttu-id="a2207-217">Por padrão, uma contagem de página ocorre sempre que uma nova página carrega no navegador de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="a2207-217">By default, a page count occurs each time a new page loads into hello client browser.</span></span>  <span data-ttu-id="a2207-218">Mas talvez você queira toocount exibições de página adicionais.</span><span class="sxs-lookup"><span data-stu-id="a2207-218">But you might want toocount additional page views.</span></span> <span data-ttu-id="a2207-219">Por exemplo, uma página pode exibir seu conteúdo de guias e desejar toocount uma página quando o usuário Olá alterna guias.</span><span class="sxs-lookup"><span data-stu-id="a2207-219">For example, a page might display its content in tabs and you want toocount a page when hello user switches tabs.</span></span> <span data-ttu-id="a2207-220">Ou código JavaScript na página Olá pode carregar um novo conteúdo sem alterar a URL do navegador hello.</span><span class="sxs-lookup"><span data-stu-id="a2207-220">Or JavaScript code in hello page might load new content without changing hello browser's URL.</span></span>

<span data-ttu-id="a2207-221">Inserir uma chamada de JavaScript como esta no ponto de apropriado Olá no código do cliente:</span><span class="sxs-lookup"><span data-stu-id="a2207-221">Insert a JavaScript call like this at hello appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="a2207-222">nome da página Olá pode conter Olá mesmo caracteres como uma URL, mas nada após "#" ou "?" será ignorado.</span><span class="sxs-lookup"><span data-stu-id="a2207-222">hello page name can contain hello same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="a2207-223">Acompanhamento de uso</span><span class="sxs-lookup"><span data-stu-id="a2207-223">Usage tracking</span></span>
<span data-ttu-id="a2207-224">Deseja toofind out que seus usuários fazem com seu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="a2207-224">Want toofind out what your users do with your app?</span></span>

* [<span data-ttu-id="a2207-225">Saiba mais sobre acompanhamento de uso</span><span class="sxs-lookup"><span data-stu-id="a2207-225">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="a2207-226">[Saiba mais sobre os eventos e as métricas personalizados de API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="a2207-226">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="a2207-227"><a name="video"></a> Vídeo</span><span class="sxs-lookup"><span data-stu-id="a2207-227"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="a2207-228"><a name="next"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a2207-228"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="a2207-229">Acompanhar uso</span><span class="sxs-lookup"><span data-stu-id="a2207-229">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="a2207-230">Eventos e métricas personalizados</span><span class="sxs-lookup"><span data-stu-id="a2207-230">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="a2207-231">Build-measure-learn</span><span class="sxs-lookup"><span data-stu-id="a2207-231">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

