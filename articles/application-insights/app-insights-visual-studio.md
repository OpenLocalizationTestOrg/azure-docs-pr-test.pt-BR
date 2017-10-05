---
title: Depurar aplicativos com o Azure Application Insights no Visual Studio | Microsoft Docs
description: "Análise de desempenho do aplicativo Web e diagnóstico durante a depuração e na produção."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: e0ac2bf01992520cdbea22a232dc42d678d77c7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="39774-103">Depure seus aplicativos com o Azure Application Insights no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="39774-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="39774-104">No Visual Studio (2015 e posterior), você pode analisar o desempenho e diagnosticar problemas em seu aplicativo Web ASP.NET na depuração e na produção usando a telemetria do [Application Insights do Azure](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39774-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="39774-105">Se você criou seu aplicativo Web ASP.NET usando o Visual Studio 2017 ou posterior, ele já terá o SDK do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="39774-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has the Application Insights SDK.</span></span> <span data-ttu-id="39774-106">Caso contrário, se ainda tiver feito isso, [adicione o Application Insights ao seu aplicativo](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="39774-106">Otherwise, if you haven't done so already, [add Application Insights to your app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="39774-107">Para monitorar seu aplicativo quando ele está em produção, você normalmente exibe o Application Insights Telemetry no [Portal do Azure](https://portal.azure.com), onde você pode definir alertas e aplicar ferramentas de monitoramento avançadas.</span><span class="sxs-lookup"><span data-stu-id="39774-107">To monitor your app when it's in live production, you normally view the Application Insights telemetry in the [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="39774-108">Mas, para depuração, também é possível pesquisar e analisar a telemetria no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="39774-108">But for debugging, you can also search and analyze the telemetry in Visual Studio.</span></span> <span data-ttu-id="39774-109">Use o Visual Studio para analisar a telemetria de seu site de produção e de execuções de depuração em seu computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="39774-109">You can use Visual Studio to analyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="39774-110">No último caso, você pode analisar execuções de depuração mesmo se ainda não tiver configurado o SDK para enviar telemetria ao Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="39774-110">In the latter case, you can analyze debugging runs even if you haven't yet configured the SDK to send telemetry to the Azure portal.</span></span> 

## <span data-ttu-id="39774-111"><a name="run"></a> Depurar seu projeto</span><span class="sxs-lookup"><span data-stu-id="39774-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="39774-112">Execute seu aplicativo Web no modo de depuração local usando F5.</span><span class="sxs-lookup"><span data-stu-id="39774-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="39774-113">Abra páginas diferentes para gerar alguma telemetria.</span><span class="sxs-lookup"><span data-stu-id="39774-113">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="39774-114">No Visual Studio, você vê uma contagem dos eventos registrados pelo módulo do Application Insights em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="39774-114">In Visual Studio, you see a count of the events that have been logged by the Application Insights module in your project.</span></span>

![No Visual Studio, no botão Application Insights é exibido durante a depuração.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="39774-116">Clique neste botão para pesquisar na telemetria.</span><span class="sxs-lookup"><span data-stu-id="39774-116">Click this button to search your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="39774-117">Pesquisa do Application Insights</span><span class="sxs-lookup"><span data-stu-id="39774-117">Application Insights search</span></span>
<span data-ttu-id="39774-118">A Janela de pesquisa do Application Insights mostra eventos que foram registrados.</span><span class="sxs-lookup"><span data-stu-id="39774-118">The Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="39774-119">(Se você tiver entrado no Azure ao configurar o Application Insights, você poderá pesquisar os mesmos eventos no Portal do Azure.)</span><span class="sxs-lookup"><span data-stu-id="39774-119">(If you signed in to Azure when you set up Application Insights, you can search the same events in the Azure portal.)</span></span>

![Clique com o botão direito no projeto e escolha Application Insights, Pesquisar.](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="39774-121">Depois de marcar ou desmarcar filtros, clique no botão Pesquisar no final do campo de pesquisa de texto.</span><span class="sxs-lookup"><span data-stu-id="39774-121">After you select or deselect filters, click the Search button at the end of the text search field.</span></span>
>

<span data-ttu-id="39774-122">A pesquisa de texto livre funciona em todos os campos dos eventos.</span><span class="sxs-lookup"><span data-stu-id="39774-122">The free text search works on any fields in the events.</span></span> <span data-ttu-id="39774-123">Por exemplo, pesquise por parte da URL de uma página; ou pelo valor de uma propriedade, como cidade do cliente; ou por palavras específicas em um log de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="39774-123">For example, search for part of the URL of a page; or the value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="39774-124">Clique em qualquer evento para ver suas propriedades detalhadas.</span><span class="sxs-lookup"><span data-stu-id="39774-124">Click any event to see its detailed properties.</span></span>

<span data-ttu-id="39774-125">Para solicitações ao seu aplicativo Web, clique até chegar ao código.</span><span class="sxs-lookup"><span data-stu-id="39774-125">For requests to your web app, you can click through to the code.</span></span>

![Em Detalhes da Solicitação, clique até chegar ao código](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="39774-127">Você também pode abrir itens relacionados para ajudar a diagnosticar as solicitações com falha ou as exceções.</span><span class="sxs-lookup"><span data-stu-id="39774-127">You can also open related items to help diagnose failed requests or exceptions.</span></span>

![Em Detalhes da Solicitação, role a tela para baixo até os itens relacionados](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="39774-129">Exibir exceções e solicitações com falha</span><span class="sxs-lookup"><span data-stu-id="39774-129">View exceptions and failed requests</span></span>
<span data-ttu-id="39774-130">Os relatórios de exceção aparecem na Janela de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="39774-130">Exception reports show in the Search window.</span></span> <span data-ttu-id="39774-131">(Em alguns tipos mais antigos do aplicativo ASP.NET, você precisa [configurar o monitoramento de exceção](app-insights-asp-net-exceptions.md) para ver as exceções manipuladas pela estrutura.)</span><span class="sxs-lookup"><span data-stu-id="39774-131">(In some older types of ASP.NET application, you have to [set up exception monitoring](app-insights-asp-net-exceptions.md) to see exceptions that are handled by the framework.)</span></span>

<span data-ttu-id="39774-132">Clique em uma exceção para obter um rastreamento de pilha.</span><span class="sxs-lookup"><span data-stu-id="39774-132">Click an exception to get a stack trace.</span></span> <span data-ttu-id="39774-133">Se o código do aplicativo for aberto no Visual Studio, você poderá clicar desde o rastreamento de pilha até a linha relevante no código.</span><span class="sxs-lookup"><span data-stu-id="39774-133">If the code of the app is open in Visual Studio, you can click through from the stack trace to the relevant line of the code.</span></span>

![Rastreamento de pilha de exceção](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-the-code"></a><span data-ttu-id="39774-135">Exibir resumos de solicitação e exceção no código</span><span class="sxs-lookup"><span data-stu-id="39774-135">View request and exception summaries in the code</span></span>
<span data-ttu-id="39774-136">Na linha de CodeLens acima de cada método manipulador, você verá uma contagem das solicitações e exceções registradas pelo Application Insights nas últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="39774-136">In the Code Lens line above each handler method, you see a count of the requests and exceptions logged by Application Insights in the past 24 h.</span></span>

![Rastreamento de pilha de exceção](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="39774-138">O CodeLens mostrará dados do Application Insights somente se você tiver [configurado seu aplicativo para enviar telemetria ao portal do Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="39774-138">Code Lens shows Application Insights data only if you have [configured your app to send telemetry to the Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="39774-139">Saiba mais sobre o Application Insights no CodeLens</span><span class="sxs-lookup"><span data-stu-id="39774-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="39774-140">Tendências</span><span class="sxs-lookup"><span data-stu-id="39774-140">Trends</span></span>
<span data-ttu-id="39774-141">Tendências é uma ferramenta para visualizar como o seu aplicativo se comporta ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="39774-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="39774-142">Escolha **Explorar Tendências de Telemetria** no botão de barra de ferramentas do Application Insights ou da janela Pesquisa do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="39774-142">Choose **Explore Telemetry Trends** from the Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="39774-143">Escolha uma das cinco consultas comuns para começar.</span><span class="sxs-lookup"><span data-stu-id="39774-143">Choose one of five common queries to get started.</span></span> <span data-ttu-id="39774-144">Você pode analisar conjuntos de dados diferentes com base em tipos de telemetria, intervalos de tempo e outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="39774-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="39774-145">Para encontrar anomalias em seus dados, escolha uma das opções de anomalias na lista suspensa "Tipo de Exibição".</span><span class="sxs-lookup"><span data-stu-id="39774-145">To find anomalies in your data, choose one of the anomaly options under the "View Type" dropdown.</span></span> <span data-ttu-id="39774-146">As opções de filtragem na parte inferior da janela facilitam o aprimoramento de subconjuntos específicos de sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="39774-146">The filtering options at the bottom of the window make it easy to hone in on specific subsets of your telemetry.</span></span>

![Tendências](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="39774-148">[Mais sobre tendências](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="39774-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="39774-149">Monitoramento local</span><span class="sxs-lookup"><span data-stu-id="39774-149">Local monitoring</span></span>
<span data-ttu-id="39774-150">(Do Visual Studio 2015 Atualização 2) Se você não tiver configurado o SDK para enviar telemetria ao portal do Application Insights (de modo que não haja nenhuma chave de instrumentação em ApplicationInsights.config), então a janela de diagnóstico exibirá a telemetria da sua sessão de depuração mais recente.</span><span class="sxs-lookup"><span data-stu-id="39774-150">(From Visual Studio 2015 Update 2) If you haven't configured the SDK to send telemetry to the Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then the diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="39774-151">Isso será desejável se você já tiver publicado uma versão anterior do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="39774-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="39774-152">Você não deseja que a telemetria de suas sessões de depuração se misturem à telemetria no portal do Application Insights do aplicativo publicado.</span><span class="sxs-lookup"><span data-stu-id="39774-152">You don't want the telemetry from your debugging sessions to be mixed up with the telemetry on the Application Insights portal from the published app.</span></span>

<span data-ttu-id="39774-153">Também será particularmente útil se você tiver [telemetria personalizada](app-insights-api-custom-events-metrics.md) que queira depurar antes de enviar a telemetria ao portal.</span><span class="sxs-lookup"><span data-stu-id="39774-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want to debug before sending telemetry to the portal.</span></span>

* <span data-ttu-id="39774-154">*Primeiro, configurei totalmente o Application Insights para enviar a telemetria ao portal. Mas agora eu quero ver a telemetria apenas no Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="39774-154">*At first, I fully configured Application Insights to send telemetry to the portal. But now I'd like to see the telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="39774-155">Nas Configurações da janela Pesquisar, há uma opção para pesquisar o diagnóstico local, mesmo se o seu aplicativo enviar telemetria para o portal.</span><span class="sxs-lookup"><span data-stu-id="39774-155">In the Search window's Settings, there's an option to search local diagnostics even if your app sends telemetry to the portal.</span></span>
  * <span data-ttu-id="39774-156">Para que a telemetria deixe de ser enviada ao portal, comente a linha `<instrumentationkey>...` de ApplicationInsights.config. Quando estiver pronto para enviar novamente a telemetria ao portal, remova os comentários.</span><span class="sxs-lookup"><span data-stu-id="39774-156">To stop telemetry being sent to the portal, comment out the line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready to send telemetry to the portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="39774-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="39774-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="39774-158">**[Adicionar mais dados](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="39774-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="39774-159">Monitorar o uso, a disponibilidade, as dependências e as exceções.</span><span class="sxs-lookup"><span data-stu-id="39774-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="39774-160">Integrar rastreamentos de estruturas de logs.</span><span class="sxs-lookup"><span data-stu-id="39774-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="39774-161">Escrever telemetria personalizada.</span><span class="sxs-lookup"><span data-stu-id="39774-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="39774-163">**[Trabalhando com o portal do Application Insights](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="39774-163">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="39774-164">Exiba painéis, poderosas ferramentas de diagnóstico e análise, alertas, um mapa de dependências em tempo real de seu aplicativo e os dados telemétricos exportados.</span><span class="sxs-lookup"><span data-stu-id="39774-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

