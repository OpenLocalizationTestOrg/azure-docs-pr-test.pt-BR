---
title: aaaDebug aplicativos com o Azure Application Insights no Visual Studio | Microsoft Docs
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
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="b04f5-103">Depure seus aplicativos com o Azure Application Insights no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b04f5-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="b04f5-104">No Visual Studio (2015 e posterior), você pode analisar o desempenho e diagnosticar problemas em seu aplicativo Web ASP.NET na depuração e na produção usando a telemetria do [Application Insights do Azure](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b04f5-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="b04f5-105">Se você criou seu aplicativo web do ASP.NET usando o Visual Studio de 2017 ou posterior, ela já tem Olá SDK do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b04f5-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has hello Application Insights SDK.</span></span> <span data-ttu-id="b04f5-106">Caso contrário, se você ainda não fez isso, [adicionar Application Insights tooyour aplicativo](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="b04f5-106">Otherwise, if you haven't done so already, [add Application Insights tooyour app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="b04f5-107">toomonitor seu aplicativo quando ele estiver em produção, você normalmente exibir telemetria do Application Insights Olá no hello [portal do Azure](https://portal.azure.com), onde você pode definir alertas e aplicar as avançadas ferramentas de monitoramentos.</span><span class="sxs-lookup"><span data-stu-id="b04f5-107">toomonitor your app when it's in live production, you normally view hello Application Insights telemetry in hello [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="b04f5-108">Mas, para depuração, você também pode pesquisar e analisar a telemetria Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b04f5-108">But for debugging, you can also search and analyze hello telemetry in Visual Studio.</span></span> <span data-ttu-id="b04f5-109">Você pode usar a telemetria do Visual Studio tooanalyze do seu site de produção e de depuração é executado no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="b04f5-109">You can use Visual Studio tooanalyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="b04f5-110">Olá caso, você pode analisar execuções de depuração mesmo se você ainda não tiver configurado Olá SDK toosend telemetria toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b04f5-110">In hello latter case, you can analyze debugging runs even if you haven't yet configured hello SDK toosend telemetry toohello Azure portal.</span></span> 

## <span data-ttu-id="b04f5-111"><a name="run"></a> Depurar seu projeto</span><span class="sxs-lookup"><span data-stu-id="b04f5-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="b04f5-112">Execute seu aplicativo Web no modo de depuração local usando F5.</span><span class="sxs-lookup"><span data-stu-id="b04f5-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="b04f5-113">Abra páginas diferentes toogenerate alguns telemetria.</span><span class="sxs-lookup"><span data-stu-id="b04f5-113">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="b04f5-114">No Visual Studio, você vê uma contagem de eventos de saudação que foram registrados pelo módulo do Application Insights Olá em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="b04f5-114">In Visual Studio, you see a count of hello events that have been logged by hello Application Insights module in your project.</span></span>

![No Visual Studio, o botão do Application Insights Olá mostra durante a depuração.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="b04f5-116">Clique neste botão toosearch sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="b04f5-116">Click this button toosearch your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="b04f5-117">Pesquisa do Application Insights</span><span class="sxs-lookup"><span data-stu-id="b04f5-117">Application Insights search</span></span>
<span data-ttu-id="b04f5-118">janela de pesquisa do Application Insights Olá mostra eventos que foram registrados.</span><span class="sxs-lookup"><span data-stu-id="b04f5-118">hello Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="b04f5-119">(Se você entrou tooAzure ao configurar o Application Insights, você pode pesquisar Olá eventos mesmo Olá portal do Azure.)</span><span class="sxs-lookup"><span data-stu-id="b04f5-119">(If you signed in tooAzure when you set up Application Insights, you can search hello same events in hello Azure portal.)</span></span>

![Clique com botão direito hello e escolha o Application Insights, pesquisa](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="b04f5-121">Depois que você marque ou desmarque os filtros, clique botão de pesquisa de Olá Olá final do campo de pesquisa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="b04f5-121">After you select or deselect filters, click hello Search button at hello end of hello text search field.</span></span>
>

<span data-ttu-id="b04f5-122">pesquisa de texto livre Olá funciona em todos os campos em eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b04f5-122">hello free text search works on any fields in hello events.</span></span> <span data-ttu-id="b04f5-123">Por exemplo, procurar por parte da URL de saudação de uma página. Olá valor ou de uma propriedade, como cidade do cliente; ou palavras específicas em um log de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="b04f5-123">For example, search for part of hello URL of a page; or hello value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="b04f5-124">Clique em qualquer evento toosee suas propriedades detalhadas.</span><span class="sxs-lookup"><span data-stu-id="b04f5-124">Click any event toosee its detailed properties.</span></span>

<span data-ttu-id="b04f5-125">Para solicitações tooyour web app, você pode clicar toohello código.</span><span class="sxs-lookup"><span data-stu-id="b04f5-125">For requests tooyour web app, you can click through toohello code.</span></span>

![Em detalhes da solicitação, clique em código toohello](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="b04f5-127">Você também pode abrir itens relacionados toohelp diagnosticar solicitações com falha ou exceções.</span><span class="sxs-lookup"><span data-stu-id="b04f5-127">You can also open related items toohelp diagnose failed requests or exceptions.</span></span>

![Em detalhes da solicitação, role para baixo toorelated itens](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="b04f5-129">Exibir exceções e solicitações com falha</span><span class="sxs-lookup"><span data-stu-id="b04f5-129">View exceptions and failed requests</span></span>
<span data-ttu-id="b04f5-130">Mostrar relatórios de exceção na janela de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="b04f5-130">Exception reports show in hello Search window.</span></span> <span data-ttu-id="b04f5-131">(Em alguns tipos mais antigos do aplicativo ASP.NET, você tem muito[configurar monitoramento de exceção](app-insights-asp-net-exceptions.md) toosee exceções que são manipuladas pelo framework hello.)</span><span class="sxs-lookup"><span data-stu-id="b04f5-131">(In some older types of ASP.NET application, you have too[set up exception monitoring](app-insights-asp-net-exceptions.md) toosee exceptions that are handled by hello framework.)</span></span>

<span data-ttu-id="b04f5-132">Clique em uma exceção tooget um rastreamento de pilha.</span><span class="sxs-lookup"><span data-stu-id="b04f5-132">Click an exception tooget a stack trace.</span></span> <span data-ttu-id="b04f5-133">Se o código de saudação do aplicativo hello é aberto no Visual Studio, você pode clicar Olá pilha rastreamento toohello relevantes linha do código de saudação.</span><span class="sxs-lookup"><span data-stu-id="b04f5-133">If hello code of hello app is open in Visual Studio, you can click through from hello stack trace toohello relevant line of hello code.</span></span>

![Rastreamento de pilha de exceção](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a><span data-ttu-id="b04f5-135">Exibir resumos de solicitação e a exceção no código Olá</span><span class="sxs-lookup"><span data-stu-id="b04f5-135">View request and exception summaries in hello code</span></span>
<span data-ttu-id="b04f5-136">Olá linha Lente de código acima cada método de manipulador, você verá uma contagem de solicitações de saudação e exceções conectadas pelo Application Insights Olá últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="b04f5-136">In hello Code Lens line above each handler method, you see a count of hello requests and exceptions logged by Application Insights in hello past 24 h.</span></span>

![Rastreamento de pilha de exceção](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="b04f5-138">Lente de código mostra apenas os dados do Application Insights, se você tiver [configurado seu portal do Application Insights do aplicativo toosend telemetria toohello](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="b04f5-138">Code Lens shows Application Insights data only if you have [configured your app toosend telemetry toohello Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="b04f5-139">Saiba mais sobre o Application Insights no CodeLens</span><span class="sxs-lookup"><span data-stu-id="b04f5-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="b04f5-140">Tendências</span><span class="sxs-lookup"><span data-stu-id="b04f5-140">Trends</span></span>
<span data-ttu-id="b04f5-141">Tendências é uma ferramenta para visualizar como o seu aplicativo se comporta ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="b04f5-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="b04f5-142">Escolha **explorar tendências de telemetria** do botão de barra de ferramentas do Application Insights hello ou janela de pesquisa do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b04f5-142">Choose **Explore Telemetry Trends** from hello Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="b04f5-143">Escolha um dos cinco tooget de consultas comuns iniciado.</span><span class="sxs-lookup"><span data-stu-id="b04f5-143">Choose one of five common queries tooget started.</span></span> <span data-ttu-id="b04f5-144">Você pode analisar conjuntos de dados diferentes com base em tipos de telemetria, intervalos de tempo e outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="b04f5-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="b04f5-145">toofind anomalias em seus dados, escolha uma das opções de anomalias de saudação no menu suspenso de "Tipo de exibição" hello.</span><span class="sxs-lookup"><span data-stu-id="b04f5-145">toofind anomalies in your data, choose one of hello anomaly options under hello "View Type" dropdown.</span></span> <span data-ttu-id="b04f5-146">Opções de filtragem de saudação na parte inferior da saudação da janela Olá tornam fácil toohone em subconjuntos específicos de sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="b04f5-146">hello filtering options at hello bottom of hello window make it easy toohone in on specific subsets of your telemetry.</span></span>

![Tendências](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="b04f5-148">[Mais sobre tendências](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="b04f5-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="b04f5-149">Monitoramento local</span><span class="sxs-lookup"><span data-stu-id="b04f5-149">Local monitoring</span></span>
<span data-ttu-id="b04f5-150">(A partir do Visual Studio 2015 atualização 2) Se você ainda não configurou o portal do Application Insights toohello de telemetria do hello SDK toosend (de forma que não há nenhuma chave de instrumentação no applicationinsights. config), em seguida, janela de diagnóstico Olá exibe Telemetria da sessão de depuração mais recente.</span><span class="sxs-lookup"><span data-stu-id="b04f5-150">(From Visual Studio 2015 Update 2) If you haven't configured hello SDK toosend telemetry toohello Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then hello diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="b04f5-151">Isso será desejável se você já tiver publicado uma versão anterior do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b04f5-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="b04f5-152">Você não quer a telemetria de saudação do seu toobe de sessões de depuração misturados com a telemetria em Olá Olá portal do Application Insights do aplicativo publicado hello.</span><span class="sxs-lookup"><span data-stu-id="b04f5-152">You don't want hello telemetry from your debugging sessions toobe mixed up with hello telemetry on hello Application Insights portal from hello published app.</span></span>

<span data-ttu-id="b04f5-153">Também é útil se você tiver algumas [telemetria personalizada](app-insights-api-custom-events-metrics.md) que você deseja toodebug antes de enviar o portal de toohello de telemetria.</span><span class="sxs-lookup"><span data-stu-id="b04f5-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want toodebug before sending telemetry toohello portal.</span></span>

* <span data-ttu-id="b04f5-154">*Primeiro, configurei totalmente portal do Application Insights toosend telemetria toohello. Mas agora gostaria de telemetria de saudação toosee apenas no Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="b04f5-154">*At first, I fully configured Application Insights toosend telemetry toohello portal. But now I'd like toosee hello telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="b04f5-155">Em configurações da janela de pesquisa hello, há um diagnóstico de local de toosearch opção mesmo se seu aplicativo envia o portal de toohello de telemetria.</span><span class="sxs-lookup"><span data-stu-id="b04f5-155">In hello Search window's Settings, there's an option toosearch local diagnostics even if your app sends telemetry toohello portal.</span></span>
  * <span data-ttu-id="b04f5-156">Telemetria toostop enviada toohello portal, comente a linha hello `<instrumentationkey>...` de applicationinsights. config. Quando estiver pronto toosend portal de toohello de telemetria, remova-os.</span><span class="sxs-lookup"><span data-stu-id="b04f5-156">toostop telemetry being sent toohello portal, comment out hello line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready toosend telemetry toohello portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b04f5-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b04f5-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="b04f5-158">**[Adicionar mais dados](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="b04f5-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="b04f5-159">Monitorar o uso, a disponibilidade, as dependências e as exceções.</span><span class="sxs-lookup"><span data-stu-id="b04f5-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="b04f5-160">Integrar rastreamentos de estruturas de logs.</span><span class="sxs-lookup"><span data-stu-id="b04f5-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="b04f5-161">Escrever telemetria personalizada.</span><span class="sxs-lookup"><span data-stu-id="b04f5-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="b04f5-163">**[Trabalhando com o portal do Application Insights Olá](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="b04f5-163">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="b04f5-164">Exiba painéis, poderosas ferramentas de diagnóstico e análise, alertas, um mapa de dependências em tempo real de seu aplicativo e os dados telemétricos exportados.</span><span class="sxs-lookup"><span data-stu-id="b04f5-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

