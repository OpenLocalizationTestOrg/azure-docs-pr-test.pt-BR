---
title: aaaMonitor o desempenho do aplicativo web do Azure | Microsoft Docs
description: "Monitoramento do desempenho do aplicativo de para aplicativos Web do Azure. Tempo de resposta e de carga, informações de dependência e alertas definidos sobre o desempenho do gráfico."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="e68cd-104">Monitorar o desempenho do aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="e68cd-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="e68cd-105">Em Olá [Portal do Azure](https://portal.azure.com) você pode configurar o monitoramento de desempenho do aplicativo para o [aplicativos web do Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e68cd-105">In hello [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="e68cd-106">[Informações de aplicativo do Azure](app-insights-overview.md) instrumenta telemetria do toosend seu aplicativo sobre seu toohello atividades serviço Application Insights, onde é armazenado e analisado.</span><span class="sxs-lookup"><span data-stu-id="e68cd-106">[Azure Application Insights](app-insights-overview.md) instruments your app toosend telemetry about its activities toohello Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="e68cd-107">Lá, os gráficos de métricas e ferramentas de pesquisa podem ser usadas toohelp diagnosticar problemas, melhorar o desempenho e avaliar o uso.</span><span class="sxs-lookup"><span data-stu-id="e68cd-107">There, metric charts and search tools can be used toohelp diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="e68cd-108">Tempo de execução ou tempo de compilação</span><span class="sxs-lookup"><span data-stu-id="e68cd-108">Run time or build time</span></span>
<span data-ttu-id="e68cd-109">Você pode configurar o monitoramento por instrumentação aplicativo hello em qualquer uma das duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="e68cd-109">You can configure monitoring by instrumenting hello app in either of two ways:</span></span>

* <span data-ttu-id="e68cd-110">**Tempo de execução** - você pode selecionar um desempenho extensão de monitoramento quando seu aplicativo Web já está ativo.</span><span class="sxs-lookup"><span data-stu-id="e68cd-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="e68cd-111">Ele não é necessário toorebuild ou reinstale o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e68cd-111">It isn't necessary toorebuild or re-install your app.</span></span> <span data-ttu-id="e68cd-112">Obtenha um conjunto padrão de pacotes que monitoram os tempos de resposta, taxas de êxito, exceções, dependências e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="e68cd-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="e68cd-113">**Tempo de compilação** - você pode instalar um pacote em seu aplicativo em desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e68cd-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="e68cd-114">Essa opção é mais versátil.</span><span class="sxs-lookup"><span data-stu-id="e68cd-114">This option is more versatile.</span></span> <span data-ttu-id="e68cd-115">Em adição toohello mesmo pacotes padrão, você pode escrever telemetria de saudação do código toocustomize ou toosend sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="e68cd-115">In addition toohello same standard packages, you can write code toocustomize hello telemetry or toosend your own telemetry.</span></span> <span data-ttu-id="e68cd-116">Você pode registrar eventos de registro de acordo com a semântica toohello do seu domínio de aplicativo ou de atividades específicas.</span><span class="sxs-lookup"><span data-stu-id="e68cd-116">You can log specific activities or record events according toohello semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="e68cd-117">Execute a instrumentação de tempo com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="e68cd-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="e68cd-118">Se você já estiver executando um aplicativo Web no Azure, então já está sendo monitorado: taxas de erro e de solicitação.</span><span class="sxs-lookup"><span data-stu-id="e68cd-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="e68cd-119">Adicione Application Insights tooget mais, como tempos de resposta, monitoramento toodependencies de chamadas, detecção inteligente e poderosa linguagem de consulta de análise de Log hello.</span><span class="sxs-lookup"><span data-stu-id="e68cd-119">Add Application Insights tooget more, such as response times, monitoring calls toodependencies, smart detection, and hello powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="e68cd-120">**Selecione o Application Insights** no painel de controle do Azure de saudação para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e68cd-120">**Select Application Insights** in hello Azure control panel for your web app.</span></span>
   
    ![Em Monitoramento, selecione Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="e68cd-122">Escolha toocreate um novo recurso, a menos que você configurou um recurso do Application Insights para esse aplicativo por outra rota.</span><span class="sxs-lookup"><span data-stu-id="e68cd-122">Choose toocreate a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="e68cd-123">**Instrumente seu aplicativo Web** após a instalação do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e68cd-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Instrumentar seu aplicativo Web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="e68cd-125">**Habilite o monitoramento do lado do cliente** para telemetria de usuário e exibição de página.</span><span class="sxs-lookup"><span data-stu-id="e68cd-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="e68cd-126">Selecione Configurações > Configurações do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="e68cd-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="e68cd-127">Em configurações do aplicativo, adicione um novo par de chave/valor:</span><span class="sxs-lookup"><span data-stu-id="e68cd-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="e68cd-128">Chave: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="e68cd-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="e68cd-129">Valor: `true`</span><span class="sxs-lookup"><span data-stu-id="e68cd-129">Value: `true`</span></span>
   * <span data-ttu-id="e68cd-130">**Salvar** Olá configurações e **reiniciar** seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e68cd-130">**Save** hello settings and **Restart** your app.</span></span>
3. <span data-ttu-id="e68cd-131">**Monitore o seu aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e68cd-131">**Monitor your app**.</span></span>  <span data-ttu-id="e68cd-132">[Dados de saudação Expore](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="e68cd-132">[Expore hello data](#explore-the-data).</span></span>

<span data-ttu-id="e68cd-133">Posteriormente, você pode criar aplicativo hello com o Application Insights se desejar.</span><span class="sxs-lookup"><span data-stu-id="e68cd-133">Later, you can build hello app with Application Insights if you want.</span></span>

<span data-ttu-id="e68cd-134">*Como remover o Application Insights, ou alternar toosending tooanother recurso?*</span><span class="sxs-lookup"><span data-stu-id="e68cd-134">*How do I remove Application Insights, or switch toosending tooanother resource?*</span></span>

* <span data-ttu-id="e68cd-135">No Azure, folha de controle de aplicativo de web hello aberta e em ferramentas de desenvolvimento, abra **extensões**.</span><span class="sxs-lookup"><span data-stu-id="e68cd-135">In Azure, open hello web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="e68cd-136">Exclua extensão do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="e68cd-136">Delete hello Application Insights extension.</span></span> <span data-ttu-id="e68cd-137">Em seguida, em monitoramento, escolha Application Insights e crie ou selecione recurso Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="e68cd-137">Then under Monitoring, choose Application Insights and create or select hello resource you want.</span></span>

## <a name="build-hello-app-with-application-insights"></a><span data-ttu-id="e68cd-138">Criar aplicativo hello com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="e68cd-138">Build hello app with Application Insights</span></span>
<span data-ttu-id="e68cd-139">O Application Insights pode fornecer dados de telemetria mais detalhados instalando um SDK em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e68cd-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="e68cd-140">Em particular, você pode coletar logs de rastreamento, [escrever telemetria personalizada](app-insights-api-custom-events-metrics.md) e obter relatórios de exceção mais detalhados.</span><span class="sxs-lookup"><span data-stu-id="e68cd-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="e68cd-141">**No Visual Studio** (2013 atualização 2 ou posterior), adicione o Application Insights ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="e68cd-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="e68cd-142">Clique com botão direito Olá web e selecione **Adicionar > Application Insights** ou **configurar o Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="e68cd-142">Right-click hello web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Clique com botão direito Olá web e escolha Adicionar ou configurar o Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="e68cd-144">Se você for questionado toosign em, use credenciais de saudação para sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e68cd-144">If you're asked toosign in, use hello credentials for your Azure account.</span></span>
   
    <span data-ttu-id="e68cd-145">operação de saudação tem dois efeitos:</span><span class="sxs-lookup"><span data-stu-id="e68cd-145">hello operation has two effects:</span></span>
   
   1. <span data-ttu-id="e68cd-146">Cria um recurso do Application Insights no Azure, onde a telemetria é armazenada, analisada e exibida.</span><span class="sxs-lookup"><span data-stu-id="e68cd-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="e68cd-147">Adiciona a saudação do Application Insights NuGet tooyour código de pacote (se ele não estiver lá já) e o configura toosend telemetria toohello recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e68cd-147">Adds hello Application Insights NuGet package tooyour code (if it isn't there already), and configures it toosend telemetry toohello Azure resource.</span></span>
2. <span data-ttu-id="e68cd-148">**Testar a telemetria Olá** pelo aplicativo hello em execução no computador de desenvolvimento (F5).</span><span class="sxs-lookup"><span data-stu-id="e68cd-148">**Test hello telemetry** by running hello app in your development machine (F5).</span></span>
3. <span data-ttu-id="e68cd-149">**Publicar o aplicativo hello** tooAzure em Olá maneira normal.</span><span class="sxs-lookup"><span data-stu-id="e68cd-149">**Publish hello app** tooAzure in hello usual way.</span></span> 

<span data-ttu-id="e68cd-150">*Como alternar o recurso de diferentes do Application Insights toosending tooa?*</span><span class="sxs-lookup"><span data-stu-id="e68cd-150">*How do I switch toosending tooa different Application Insights resource?*</span></span>

* <span data-ttu-id="e68cd-151">No Visual Studio, o projeto de Olá do botão direito do mouse, escolha **configurar o Application Insights** e escolha Olá recurso desejado.</span><span class="sxs-lookup"><span data-stu-id="e68cd-151">In Visual Studio, right-click hello project, choose **Configure Application Insights** and choose hello resource you want.</span></span> <span data-ttu-id="e68cd-152">Você obtém Olá opção toocreate um novo recurso.</span><span class="sxs-lookup"><span data-stu-id="e68cd-152">You get hello option toocreate a new resource.</span></span> <span data-ttu-id="e68cd-153">Recompilar e reimplantar.</span><span class="sxs-lookup"><span data-stu-id="e68cd-153">Rebuild and redeploy.</span></span>

## <a name="explore-hello-data"></a><span data-ttu-id="e68cd-154">Explorar dados Olá</span><span class="sxs-lookup"><span data-stu-id="e68cd-154">Explore hello data</span></span>
1. <span data-ttu-id="e68cd-155">Na folha do Application Insights saudação do painel de controle de aplicativo web, você visualiza em métricas em tempo real, que mostra a falhas e solicitações em um segundo ou dois deles ocorrendo.</span><span class="sxs-lookup"><span data-stu-id="e68cd-155">On hello Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="e68cd-156">É muito útil exibir quando você estiver republicando seu aplicativo – você poderá ver todos os problemas imediatamente.</span><span class="sxs-lookup"><span data-stu-id="e68cd-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="e68cd-157">Clique em toohello completo de recursos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e68cd-157">Click through toohello full Application Insights resource.</span></span>

    ![Clique para o](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="e68cd-159">Você também pode ir lá diretamente da navegação de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e68cd-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="e68cd-160">Clique nas tooget qualquer gráfico mais detalhes:</span><span class="sxs-lookup"><span data-stu-id="e68cd-160">Click through any chart tooget more detail:</span></span>
   
    ![Na folha de visão geral do Application Insights hello, clique em um gráfico](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="e68cd-162">Você pode [personalizar folhas de métricas](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="e68cd-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="e68cd-163">Clique nas mais toosee eventos individuais e suas propriedades:</span><span class="sxs-lookup"><span data-stu-id="e68cd-163">Click through further toosee individual events and their properties:</span></span>
   
    ![Clique em um tooopen de tipo de evento filtrada de uma pesquisa no tipo](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="e68cd-165">Observe que "…" hello link tooopen todas as propriedades.</span><span class="sxs-lookup"><span data-stu-id="e68cd-165">Notice hello "..." link tooopen all properties.</span></span>
   
    <span data-ttu-id="e68cd-166">Você pode [personalizar pesquisas](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="e68cd-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="e68cd-167">Para pesquisas mais eficientes em sua telemetria, use Olá [linguagem de consulta de análise de Log](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="e68cd-167">For more powerful searches over your telemetry, use hello [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="e68cd-168">Mais telemetria</span><span class="sxs-lookup"><span data-stu-id="e68cd-168">More telemetry</span></span>

* [<span data-ttu-id="e68cd-169">Carregar dados da página da Web</span><span class="sxs-lookup"><span data-stu-id="e68cd-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="e68cd-170">Telemetria personalizada</span><span class="sxs-lookup"><span data-stu-id="e68cd-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="e68cd-171">Vídeo</span><span class="sxs-lookup"><span data-stu-id="e68cd-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="e68cd-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e68cd-172">Next steps</span></span>
* <span data-ttu-id="e68cd-173">[Executar o criador de perfil de saudação em seu live app](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="e68cd-173">[Run hello profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="e68cd-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) – monitorar o Azure Functions com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="e68cd-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="e68cd-175">[Habilitar o diagnóstico do Azure](app-insights-azure-diagnostics.md) tooApplication toobe enviado Insights.</span><span class="sxs-lookup"><span data-stu-id="e68cd-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) toobe sent tooApplication Insights.</span></span>
* <span data-ttu-id="e68cd-176">[Monitorar as métricas de integridade do serviço](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake-se de que o serviço está disponível e respondendo.</span><span class="sxs-lookup"><span data-stu-id="e68cd-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="e68cd-177">[Receba notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) sempre que ocorrerem eventos operacionais ou métricas ultrapassarem um limite.</span><span class="sxs-lookup"><span data-stu-id="e68cd-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="e68cd-178">Use [Application Insights para páginas da web e aplicativos JavaScript](app-insights-javascript.md) tooget telemetria de cliente de navegadores Olá que visita uma página da web.</span><span class="sxs-lookup"><span data-stu-id="e68cd-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) tooget client telemetry from hello browsers that visit a web page.</span></span>
* <span data-ttu-id="e68cd-179">[Configurar testes da web de disponibilidade](app-insights-monitor-web-app-availability.md) toobe alertado se seu site está inativo.</span><span class="sxs-lookup"><span data-stu-id="e68cd-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) toobe alerted if your site is down.</span></span>

