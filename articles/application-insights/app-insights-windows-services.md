---
title: "as funções de servidor e de trabalho de Insights do aplicativo para Windows aaaAzure | Microsoft Docs"
description: Adicione manualmente o desempenho, disponibilidade e uso de tooanalyze de aplicativo hello SDK do Application Insights tooyour ASP.NET.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="41243-103">Configurar manualmente o Application Insights para aplicativos .NET</span><span class="sxs-lookup"><span data-stu-id="41243-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="41243-104">Você pode configurar [Application Insights](app-insights-overview.md) toomonitor uma ampla variedade de aplicativos ou funções de aplicativo, componentes ou microservices.</span><span class="sxs-lookup"><span data-stu-id="41243-104">You can configure [Application Insights](app-insights-overview.md) toomonitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="41243-105">Para aplicativos Web e serviços, o Visual Studio oferece [configuração em uma etapa](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="41243-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="41243-106">Para outros tipos de aplicativos .NET, como funções de servidor de back-end ou aplicativos de área de trabalho, você pode configurar o Application Insights manualmente.</span><span class="sxs-lookup"><span data-stu-id="41243-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Gráficos de exemplo de monitoramento de desempenho](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="41243-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="41243-108">Before you start</span></span>

<span data-ttu-id="41243-109">Você precisa de:</span><span class="sxs-lookup"><span data-stu-id="41243-109">You need:</span></span>

* <span data-ttu-id="41243-110">Uma assinatura muito[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="41243-110">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="41243-111">Se sua equipe ou organização tiver uma assinatura do Azure, Olá proprietário pode adicionar tooit, usando o [conta da Microsoft](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="41243-111">If your team or organization has an Azure subscription, hello owner can add you tooit, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="41243-112">Visual Studio 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="41243-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="41243-113"><a name="add"></a>1. Escolher um recurso Application Insights</span><span class="sxs-lookup"><span data-stu-id="41243-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="41243-114">Olá 'recurso' é onde os dados são coletados e exibidos no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="41243-114">hello 'resource' is where your data is collected and displayed in hello Azure portal.</span></span> <span data-ttu-id="41243-115">Se precisar toodecide toocreate um novo, ou compartilhar uma existente.</span><span class="sxs-lookup"><span data-stu-id="41243-115">You need toodecide whether toocreate a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="41243-116">Parte de um aplicativo maior: usar o recurso existente</span><span class="sxs-lookup"><span data-stu-id="41243-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="41243-117">Se seu aplicativo da web tem vários componentes - por exemplo, um aplicativo web front-end e um ou mais serviços de back-end - em seguida, você deve enviar telemetria de todos os toohello de componentes de saudação mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="41243-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all hello components toohello same resource.</span></span> <span data-ttu-id="41243-118">Isso habilitá-las toobe exibido em um mapa de aplicativo único e torná-lo possível tootrace uma solicitação de um componente tooanother.</span><span class="sxs-lookup"><span data-stu-id="41243-118">This will enable them toobe displayed on a single Application Map, and make it possible tootrace a request from one component tooanother.</span></span>

<span data-ttu-id="41243-119">Portanto, se você já estiver monitorando outros componentes deste aplicativo, em seguida, basta usar Olá mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="41243-119">So, if you're already monitoring other components of this app, then just use hello same resource.</span></span>

<span data-ttu-id="41243-120">Abrir o recurso de saudação em Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="41243-120">Open hello resource in hello [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="41243-121">Aplicativo independente: criar um novo recurso</span><span class="sxs-lookup"><span data-stu-id="41243-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="41243-122">Se aplicativos tooother relacionados Olá novo aplicativo, ele deve ter seu próprio recurso.</span><span class="sxs-lookup"><span data-stu-id="41243-122">If hello new app is unrelated tooother applications, then it should have its own resource.</span></span>

<span data-ttu-id="41243-123">Entrar toohello [portal do Azure](https://portal.azure.com/)e criar um novo recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="41243-123">Sign in toohello [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="41243-124">Escolha o ASP.NET como o tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="41243-124">Choose ASP.NET as hello application type.</span></span>

![Clique em Novo, Application Insights](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="41243-126">Escolha de saudação do tipo de aplicativo define o conteúdo de padrão de saudação de folhas de recurso hello.</span><span class="sxs-lookup"><span data-stu-id="41243-126">hello choice of application type sets hello default content of hello resource blades.</span></span>

## <a name="2-copy-hello-instrumentation-key"></a><span data-ttu-id="41243-127">2. Copiar Olá chave de instrumentação</span><span class="sxs-lookup"><span data-stu-id="41243-127">2. Copy hello Instrumentation Key</span></span>
<span data-ttu-id="41243-128">chave de saudação identifica o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="41243-128">hello key identifies hello resource.</span></span> <span data-ttu-id="41243-129">Você vai instalá-lo em breve no hello SDK, no recurso de toohello ordem toodirect dados.</span><span class="sxs-lookup"><span data-stu-id="41243-129">You'll install it soon in hello SDK, in order toodirect data toohello resource.</span></span>

![Clique em propriedades, selecione a chave de saudação e pressione ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="41243-131"><a name="sdk"></a>3. Instalar o pacote do Application Insights de saudação em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="41243-131"><a name="sdk"></a>3. Install hello Application Insights package in your application</span></span>
<span data-ttu-id="41243-132">Instalando e configurando Olá Application Insights pacote varia dependendo plataforma Olá que você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="41243-132">Installing and configuring hello Application Insights package varies depending on hello platform you're working on.</span></span> 

1. <span data-ttu-id="41243-133">No Visual Studio, clique com o botão direito do mouse em seu projeto e escolha **Gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="41243-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Clique com botão direito hello e selecione Gerenciar pacotes Nuget](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="41243-135">Instalar o pacote do Application Insights Olá para aplicativos do Windows server, "Microsoft.ApplicationInsights.WindowsServer".</span><span class="sxs-lookup"><span data-stu-id="41243-135">Install hello Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![Pesquise “Application Insights”](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="41243-137">*Qual versão?*</span><span class="sxs-lookup"><span data-stu-id="41243-137">*Which version?*</span></span>

    <span data-ttu-id="41243-138">Verificar **incluir pré-lançamento** se você quiser tootry nossos recursos mais recentes.</span><span class="sxs-lookup"><span data-stu-id="41243-138">Check **Include prerelease** if you want tootry our latest features.</span></span> <span data-ttu-id="41243-139">documentos relevantes Hello ou blogs Observe se você precisa de uma versão de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="41243-139">hello relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="41243-140">*É possível usar outros pacotes?*</span><span class="sxs-lookup"><span data-stu-id="41243-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="41243-141">Sim.</span><span class="sxs-lookup"><span data-stu-id="41243-141">Yes.</span></span> <span data-ttu-id="41243-142">Escolha "Microsoft.ApplicationInsights" se quiser apenas toouse Olá API toosend sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="41243-142">Choose "Microsoft.ApplicationInsights" if you only want toouse hello API toosend your own telemetry.</span></span> <span data-ttu-id="41243-143">pacote do Windows Server Olá inclui Olá API mais um número de outros pacotes, como a coleta do contador de desempenho e monitoramento de dependência.</span><span class="sxs-lookup"><span data-stu-id="41243-143">hello Windows Server package includes hello API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="tooupgrade-toofuture-package-versions"></a><span data-ttu-id="41243-144">versões do pacote toofuture tooupgrade</span><span class="sxs-lookup"><span data-stu-id="41243-144">tooupgrade toofuture package versions</span></span>
<span data-ttu-id="41243-145">Podemos lançar uma nova versão do hello SDK de tootime de tempo.</span><span class="sxs-lookup"><span data-stu-id="41243-145">We release a new version of hello SDK from time tootime.</span></span>

<span data-ttu-id="41243-146">tooupgrade tooa [nova versão do pacote de saudação](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), abra o Gerenciador de pacotes do NuGet e filtrar pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="41243-146">tooupgrade tooa [new release of hello package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="41243-147">Selecione **Microsoft.ApplicationInsights.WindowsServer** e **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="41243-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="41243-148">Se você fez tooApplicationInsights.config quaisquer personalizações, salve uma cópia dele antes de atualizar e posteriormente mesclar suas alterações na nova versão de hello.</span><span class="sxs-lookup"><span data-stu-id="41243-148">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into hello new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="41243-149">4. Enviar telemetria</span><span class="sxs-lookup"><span data-stu-id="41243-149">4. Send telemetry</span></span>
<span data-ttu-id="41243-150">**Se você instalou somente o pacote hello API:**</span><span class="sxs-lookup"><span data-stu-id="41243-150">**If you installed only hello API package:**</span></span>

* <span data-ttu-id="41243-151">Defina a chave de instrumentação Olá no código, por exemplo `main()`:</span><span class="sxs-lookup"><span data-stu-id="41243-151">Set hello instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="41243-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *sua chave* `";`</span><span class="sxs-lookup"><span data-stu-id="41243-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="41243-153">[Gravar seu próprio telemetria usando a API de saudação](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="41243-153">[Write your own telemetry using hello API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="41243-154">**Se você tiver instalado outros pacotes do Application Insights,** você pode usar de se você preferir, chave de instrumentação de Olá Olá. config arquivo tooset:</span><span class="sxs-lookup"><span data-stu-id="41243-154">**If you installed other Application Insights packages,** you can, if you prefer, use hello .config file tooset hello instrumentation key:</span></span>

* <span data-ttu-id="41243-155">Edite applicationinsights. config (que foi adicionado pelo Olá instalar NuGet).</span><span class="sxs-lookup"><span data-stu-id="41243-155">Edit ApplicationInsights.config (which was added by hello NuGet install).</span></span> <span data-ttu-id="41243-156">Coloque-a antes Olá marca de fechamento:</span><span class="sxs-lookup"><span data-stu-id="41243-156">Insert this just before hello closing tag:</span></span>
  
    <span data-ttu-id="41243-157">`<InstrumentationKey>`*chave de instrumentação Olá copiado*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="41243-157">`<InstrumentationKey>` *hello instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="41243-158">Certifique-se de que Olá definir propriedades de applicationinsights. config no Solution Explorer são muito**Build Action = conteúdo, cópia tooOutput Directory = copiar**.</span><span class="sxs-lookup"><span data-stu-id="41243-158">Make sure that hello properties of ApplicationInsights.config in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>

<span data-ttu-id="41243-159">É chave de instrumentação Olá tooset úteis no código se você quiser muito[comutador hello chave para as configurações de compilação diferente](app-insights-separate-resources.md).</span><span class="sxs-lookup"><span data-stu-id="41243-159">It's useful tooset hello instrumentation key in code if you want too[switch hello key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="41243-160">Se você definir a chave de saudação no código, você não tem tooset no hello `.config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="41243-160">If you set hello key in code, you don't have tooset it in hello `.config` file.</span></span>

## <span data-ttu-id="41243-161"><a name="run"></a> Execute seu projeto</span><span class="sxs-lookup"><span data-stu-id="41243-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="41243-162">Saudação de uso **F5** toorun seu aplicativo e experimente-o: abrir diferente páginas toogenerate alguns telemetria.</span><span class="sxs-lookup"><span data-stu-id="41243-162">Use hello **F5** toorun your application and try it out: open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="41243-163">No Visual Studio, você verá uma contagem de eventos de saudação que foram enviadas.</span><span class="sxs-lookup"><span data-stu-id="41243-163">In Visual Studio, you'll see a count of hello events that have been sent.</span></span>

![Contagem de eventos no Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="41243-165"><a name="monitor"></a> Exibir sua telemetria</span><span class="sxs-lookup"><span data-stu-id="41243-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="41243-166">Retornar toohello [portal do Azure](https://portal.azure.com/) e procure o recurso do Application Insights tooyour.</span><span class="sxs-lookup"><span data-stu-id="41243-166">Return toohello [Azure portal](https://portal.azure.com/) and browse tooyour Application Insights resource.</span></span>

<span data-ttu-id="41243-167">Procure dados em gráficos de visão geral de saudação.</span><span class="sxs-lookup"><span data-stu-id="41243-167">Look for data in hello Overview charts.</span></span> <span data-ttu-id="41243-168">Primeiro, você apenas verá um ou dois pontos.</span><span class="sxs-lookup"><span data-stu-id="41243-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="41243-169">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="41243-169">For example:</span></span>

![Clicar em dados toomore](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="41243-171">Clique em por meio de qualquer gráfico toosee métricas mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="41243-171">Click through any chart toosee more detailed metrics.</span></span> [<span data-ttu-id="41243-172">Saiba mais sobre métricas.</span><span class="sxs-lookup"><span data-stu-id="41243-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="41243-173">Não há dados?</span><span class="sxs-lookup"><span data-stu-id="41243-173">No data?</span></span>
* <span data-ttu-id="41243-174">Use o aplicativo hello, páginas diferentes de abertura para que ele gera algumas telemetria.</span><span class="sxs-lookup"><span data-stu-id="41243-174">Use hello application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="41243-175">Olá abrir [pesquisa](app-insights-diagnostic-search.md) bloco eventos individuais toosee.</span><span class="sxs-lookup"><span data-stu-id="41243-175">Open hello [Search](app-insights-diagnostic-search.md) tile, toosee individual events.</span></span> <span data-ttu-id="41243-176">Às vezes é preciso eventos tooget um pouco enquanto mais por meio do pipeline de métricas de saudação.</span><span class="sxs-lookup"><span data-stu-id="41243-176">Sometimes it takes events a little while longer tooget through hello metrics pipeline.</span></span>
* <span data-ttu-id="41243-177">Aguarde alguns segundos e clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="41243-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="41243-178">Gráficos de se atualizar periodicamente, mas você pode atualizar manualmente, se você estiver esperando por tooshow alguns dados para cima.</span><span class="sxs-lookup"><span data-stu-id="41243-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data tooshow up.</span></span>
* <span data-ttu-id="41243-179">Consulte [Solucionar problemas](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="41243-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="41243-180">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="41243-180">Publish your app</span></span>
<span data-ttu-id="41243-181">Agora, implante aplicativos tooyour servidor ou Olá tooAzure e inspecionar dados acumulam.</span><span class="sxs-lookup"><span data-stu-id="41243-181">Now deploy your application tooyour server or tooAzure and watch hello data accumulate.</span></span>

![Usar o Visual Studio toopublish seu aplicativo](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="41243-183">Quando você executa em modo de depuração, telemetria é acelerada por meio do pipeline Olá, para que você deve ver os dados que aparecem dentro de segundos.</span><span class="sxs-lookup"><span data-stu-id="41243-183">When you run in debug mode, telemetry is expedited through hello pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="41243-184">Quando você implanta seu aplicativo na configuração de Versão, os dados acumulam mais lentamente.</span><span class="sxs-lookup"><span data-stu-id="41243-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-tooyour-server"></a><span data-ttu-id="41243-185">Nenhum dado após a publicação de servidor tooyour?</span><span class="sxs-lookup"><span data-stu-id="41243-185">No data after you publish tooyour server?</span></span>
<span data-ttu-id="41243-186">Abra estas portas para tráfego de saída no firewall do servidor.</span><span class="sxs-lookup"><span data-stu-id="41243-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="41243-187">Consulte [essa página](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) para lista de saudação de endereços necessários</span><span class="sxs-lookup"><span data-stu-id="41243-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for hello list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="41243-188">Problemas no servidor de compilação?</span><span class="sxs-lookup"><span data-stu-id="41243-188">Trouble on your build server?</span></span>
<span data-ttu-id="41243-189">Consulte [este item de solução de problemas](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="41243-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="41243-190">Se seu aplicativo gera um lote de telemetria, módulo de amostragem adaptável Olá automaticamente reduzirá o volume Olá enviada toohello portal enviando apenas uma fração representativa de eventos.</span><span class="sxs-lookup"><span data-stu-id="41243-190">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="41243-191">No entanto, eventos que são relacionada toohello mesma solicitação será marcada ou desmarcada como um grupo, para que você possa navegar entre eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="41243-191">However, events that are related toohello same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="41243-192">[Saiba mais sobre amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="41243-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="41243-193">Vídeo</span><span class="sxs-lookup"><span data-stu-id="41243-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="41243-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41243-194">Next steps</span></span>
* <span data-ttu-id="41243-195">[Adicionar telemetria mais](app-insights-asp-net-more.md) tooget Olá visão de 360 graus completo do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41243-195">[Add more telemetry](app-insights-asp-net-more.md) tooget hello full 360-degree view of your application.</span></span>

