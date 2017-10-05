---
title: "Application Insights do Azure para funções de trabalho e de servidor do Windows | Microsoft Docs"
description: Adicione manualmente o SDK do Application Insights ao aplicativo ASP.NET para analisar o uso, a disponibilidade e o desempenho.
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
ms.openlocfilehash: 4b9f8c618a69c4c157dafeb7f726aae24efad428
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="bf444-103">Configurar manualmente o Application Insights para aplicativos .NET</span><span class="sxs-lookup"><span data-stu-id="bf444-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="bf444-104">Você pode configurar o [Application Insights](app-insights-overview.md) para monitorar uma ampla variedade de aplicativos ou funções de aplicativo, componentes ou microsserviços.</span><span class="sxs-lookup"><span data-stu-id="bf444-104">You can configure [Application Insights](app-insights-overview.md) to monitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="bf444-105">Para aplicativos Web e serviços, o Visual Studio oferece [configuração em uma etapa](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="bf444-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="bf444-106">Para outros tipos de aplicativos .NET, como funções de servidor de back-end ou aplicativos de área de trabalho, você pode configurar o Application Insights manualmente.</span><span class="sxs-lookup"><span data-stu-id="bf444-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Gráficos de exemplo de monitoramento de desempenho](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="bf444-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="bf444-108">Before you start</span></span>

<span data-ttu-id="bf444-109">Você precisa de:</span><span class="sxs-lookup"><span data-stu-id="bf444-109">You need:</span></span>

* <span data-ttu-id="bf444-110">Uma assinatura do [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="bf444-110">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="bf444-111">Se sua equipe ou organização tem uma assinatura do Azure, o proprietário pode adicioná-lo a ela, usando sua [Conta da Microsoft](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="bf444-111">If your team or organization has an Azure subscription, the owner can add you to it, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="bf444-112">Visual Studio 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bf444-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="bf444-113"><a name="add"></a>1. Escolher um recurso Application Insights</span><span class="sxs-lookup"><span data-stu-id="bf444-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="bf444-114">O ‘recurso’ é onde os dados são coletados e exibidos no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf444-114">The 'resource' is where your data is collected and displayed in the Azure portal.</span></span> <span data-ttu-id="bf444-115">Você precisa decidir se deseja criar um recurso novo ou compartilhar um existente.</span><span class="sxs-lookup"><span data-stu-id="bf444-115">You need to decide whether to create a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="bf444-116">Parte de um aplicativo maior: usar o recurso existente</span><span class="sxs-lookup"><span data-stu-id="bf444-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="bf444-117">Se seu aplicativo Web tem vários componentes, por exemplo, um aplicativo Web de front-end e um ou mais serviços de back-end, você deve enviar telemetria de todos os componentes para o mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="bf444-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all the components to the same resource.</span></span> <span data-ttu-id="bf444-118">Isso permite que sejam exibidos em um mapa de aplicativo único e possibilita rastrear uma solicitação de um componente para outro.</span><span class="sxs-lookup"><span data-stu-id="bf444-118">This will enable them to be displayed on a single Application Map, and make it possible to trace a request from one component to another.</span></span>

<span data-ttu-id="bf444-119">Assim, se você já estiver monitorando outros componentes desse aplicativo, use o mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="bf444-119">So, if you're already monitoring other components of this app, then just use the same resource.</span></span>

<span data-ttu-id="bf444-120">Abra o grupo de recursos no [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bf444-120">Open the resource in the [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="bf444-121">Aplicativo independente: criar um novo recurso</span><span class="sxs-lookup"><span data-stu-id="bf444-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="bf444-122">Se o novo aplicativo não está relacionado a outros aplicativos, ele deve ter seu próprio recurso.</span><span class="sxs-lookup"><span data-stu-id="bf444-122">If the new app is unrelated to other applications, then it should have its own resource.</span></span>

<span data-ttu-id="bf444-123">Entre no [Portal do Azure](https://portal.azure.com/)e crie um novo recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bf444-123">Sign in to the [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="bf444-124">Escolha ASP.NET como o tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf444-124">Choose ASP.NET as the application type.</span></span>

![Clique em Novo, Application Insights](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="bf444-126">A escolha do tipo de aplicativo define o conteúdo padrão das folhas do recurso.</span><span class="sxs-lookup"><span data-stu-id="bf444-126">The choice of application type sets the default content of the resource blades.</span></span>

## <a name="2-copy-the-instrumentation-key"></a><span data-ttu-id="bf444-127">2. Copiar a chave de instrumentação</span><span class="sxs-lookup"><span data-stu-id="bf444-127">2. Copy the Instrumentation Key</span></span>
<span data-ttu-id="bf444-128">A chave identifica o recurso.</span><span class="sxs-lookup"><span data-stu-id="bf444-128">The key identifies the resource.</span></span> <span data-ttu-id="bf444-129">Você instalará em breve no SDK a fim de direcionar os dados para o recurso.</span><span class="sxs-lookup"><span data-stu-id="bf444-129">You'll install it soon in the SDK, in order to direct data to the resource.</span></span>

![Clique em Propriedades, selecione a chave e pressione ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="bf444-131"><a name="sdk"></a>3. Instale o pacote do Application Insights em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="bf444-131"><a name="sdk"></a>3. Install the Application Insights package in your application</span></span>
<span data-ttu-id="bf444-132">A instalação e a configuração do pacote do Application Insights varia dependendo da plataforma em que você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="bf444-132">Installing and configuring the Application Insights package varies depending on the platform you're working on.</span></span> 

1. <span data-ttu-id="bf444-133">No Visual Studio, clique com o botão direito do mouse em seu projeto e escolha **Gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="bf444-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Clique com o botão direito no projeto e selecione Gerenciar Pacotes Nuget](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="bf444-135">Instale o pacote do Application Insights para aplicativos do Windows Server, "Microsoft.ApplicationInsights.WindowsServer".</span><span class="sxs-lookup"><span data-stu-id="bf444-135">Install the Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![Pesquise “Application Insights”](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="bf444-137">*Qual versão?*</span><span class="sxs-lookup"><span data-stu-id="bf444-137">*Which version?*</span></span>

    <span data-ttu-id="bf444-138">Marque a opção **Incluir pré-lançamento** se você quiser experimentar nossos recursos mais recentes.</span><span class="sxs-lookup"><span data-stu-id="bf444-138">Check **Include prerelease** if you want to try our latest features.</span></span> <span data-ttu-id="bf444-139">Os documentos relevantes ou blogs indicam se você precisa de uma versão de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="bf444-139">The relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="bf444-140">*É possível usar outros pacotes?*</span><span class="sxs-lookup"><span data-stu-id="bf444-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="bf444-141">Sim.</span><span class="sxs-lookup"><span data-stu-id="bf444-141">Yes.</span></span> <span data-ttu-id="bf444-142">Escolha “Microsoft.ApplicationInsights” se deseja usar a API para enviar sua próprias telemetrias.</span><span class="sxs-lookup"><span data-stu-id="bf444-142">Choose "Microsoft.ApplicationInsights" if you only want to use the API to send your own telemetry.</span></span> <span data-ttu-id="bf444-143">O pacote do Windows Server inclui a API e vários outros pacotes, como coleta do contador de desempenho e monitoramento de dependência.</span><span class="sxs-lookup"><span data-stu-id="bf444-143">The Windows Server package includes the API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="to-upgrade-to-future-package-versions"></a><span data-ttu-id="bf444-144">Para atualizar para versões futuras do pacote</span><span class="sxs-lookup"><span data-stu-id="bf444-144">To upgrade to future package versions</span></span>
<span data-ttu-id="bf444-145">Lançamos uma nova versão do SDK de tempos em tempos.</span><span class="sxs-lookup"><span data-stu-id="bf444-145">We release a new version of the SDK from time to time.</span></span>

<span data-ttu-id="bf444-146">Para atualizar para uma [nova versão do pacote](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), abra o Gerenciador de pacotes do NuGet e filtre os pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="bf444-146">To upgrade to a [new release of the package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="bf444-147">Selecione **Microsoft.ApplicationInsights.WindowsServer** e **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="bf444-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="bf444-148">Se você fez todas as personalizações no ApplicationInsights.config, salve uma cópia antes de atualizar e, depois, mescle suas alterações à nova versão.</span><span class="sxs-lookup"><span data-stu-id="bf444-148">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into the new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="bf444-149">4. Enviar telemetria</span><span class="sxs-lookup"><span data-stu-id="bf444-149">4. Send telemetry</span></span>
<span data-ttu-id="bf444-150">**Se você instalou apenas o pacote de API:**</span><span class="sxs-lookup"><span data-stu-id="bf444-150">**If you installed only the API package:**</span></span>

* <span data-ttu-id="bf444-151">Defina a chave de instrumentação no código, por exemplo, em `main()`:</span><span class="sxs-lookup"><span data-stu-id="bf444-151">Set the instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="bf444-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *sua chave* `";`</span><span class="sxs-lookup"><span data-stu-id="bf444-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="bf444-153">[Escreva sua própria telemetria usando a API](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="bf444-153">[Write your own telemetry using the API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="bf444-154">**Se tiver instalado outros pacotes do Application Insights,** se preferir, você poderá usar o arquivo .config para definir a chave de instrumentação:</span><span class="sxs-lookup"><span data-stu-id="bf444-154">**If you installed other Application Insights packages,** you can, if you prefer, use the .config file to set the instrumentation key:</span></span>

* <span data-ttu-id="bf444-155">Edite o ApplicationInsights.config (que foi adicionado pela instalação do NuGet).</span><span class="sxs-lookup"><span data-stu-id="bf444-155">Edit ApplicationInsights.config (which was added by the NuGet install).</span></span> <span data-ttu-id="bf444-156">Insira isto logo antes da marca de fechamento:</span><span class="sxs-lookup"><span data-stu-id="bf444-156">Insert this just before the closing tag:</span></span>
  
    <span data-ttu-id="bf444-157">`<InstrumentationKey>` *a chave de instrumentação que você copiou* `</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="bf444-157">`<InstrumentationKey>` *the instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="bf444-158">Verifique se as propriedades de ApplicationInsights.config no Gerenciador de Soluções estão definidas como **Ação de Compilação = Conteúdo, Copiar para Diretório de Saída = Copiar**.</span><span class="sxs-lookup"><span data-stu-id="bf444-158">Make sure that the properties of ApplicationInsights.config in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>

<span data-ttu-id="bf444-159">A definição da chave de instrumentação no código será útil se você quiser [alternar a chave para configurações de compilação diferentes](app-insights-separate-resources.md).</span><span class="sxs-lookup"><span data-stu-id="bf444-159">It's useful to set the instrumentation key in code if you want to [switch the key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="bf444-160">Se você definir a chave no código, não será necessário defini-la no arquivo `.config`.</span><span class="sxs-lookup"><span data-stu-id="bf444-160">If you set the key in code, you don't have to set it in the `.config` file.</span></span>

## <span data-ttu-id="bf444-161"><a name="run"></a> Execute seu projeto</span><span class="sxs-lookup"><span data-stu-id="bf444-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="bf444-162">Use a tecla **F5** para executar o aplicativo e experimente: abrir páginas diferentes para gerar telemetria.</span><span class="sxs-lookup"><span data-stu-id="bf444-162">Use the **F5** to run your application and try it out: open different pages to generate some telemetry.</span></span>

<span data-ttu-id="bf444-163">No Visual Studio, você verá uma contagem dos eventos que foram recebidos.</span><span class="sxs-lookup"><span data-stu-id="bf444-163">In Visual Studio, you'll see a count of the events that have been sent.</span></span>

![Contagem de eventos no Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="bf444-165"><a name="monitor"></a> Exibir sua telemetria</span><span class="sxs-lookup"><span data-stu-id="bf444-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="bf444-166">Volte para o [Portal do Azure](https://portal.azure.com/) e navegue até o seu recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bf444-166">Return to the [Azure portal](https://portal.azure.com/) and browse to your Application Insights resource.</span></span>

<span data-ttu-id="bf444-167">Procure dados nos gráficos de Visão Geral.</span><span class="sxs-lookup"><span data-stu-id="bf444-167">Look for data in the Overview charts.</span></span> <span data-ttu-id="bf444-168">Primeiro, você apenas verá um ou dois pontos.</span><span class="sxs-lookup"><span data-stu-id="bf444-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="bf444-169">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bf444-169">For example:</span></span>

![Clique por mais dados](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="bf444-171">Clique em qualquer gráfico para ver métricas mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="bf444-171">Click through any chart to see more detailed metrics.</span></span> [<span data-ttu-id="bf444-172">Saiba mais sobre métricas.</span><span class="sxs-lookup"><span data-stu-id="bf444-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="bf444-173">Não há dados?</span><span class="sxs-lookup"><span data-stu-id="bf444-173">No data?</span></span>
* <span data-ttu-id="bf444-174">Use o aplicativo abrindo páginas diferentes, para que ele gere alguma telemetria.</span><span class="sxs-lookup"><span data-stu-id="bf444-174">Use the application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="bf444-175">Abra o bloco [Pesquisar](app-insights-diagnostic-search.md) para ver eventos individuais.</span><span class="sxs-lookup"><span data-stu-id="bf444-175">Open the [Search](app-insights-diagnostic-search.md) tile, to see individual events.</span></span> <span data-ttu-id="bf444-176">Às vezes, os eventos demoram um pouco mais para passar pelo pipeline de métricas.</span><span class="sxs-lookup"><span data-stu-id="bf444-176">Sometimes it takes events a little while longer to get through the metrics pipeline.</span></span>
* <span data-ttu-id="bf444-177">Aguarde alguns segundos e clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="bf444-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="bf444-178">Os gráficos se atualizam periodicamente, mas você pode atualizá-los manualmente se estiver aguardando para alguns dados serem exibidos.</span><span class="sxs-lookup"><span data-stu-id="bf444-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data to show up.</span></span>
* <span data-ttu-id="bf444-179">Consulte [Solucionar problemas](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="bf444-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="bf444-180">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="bf444-180">Publish your app</span></span>
<span data-ttu-id="bf444-181">Agora, implante o aplicativo em seu servidor ou no Azure e veja os dados se acumularem.</span><span class="sxs-lookup"><span data-stu-id="bf444-181">Now deploy your application to your server or to Azure and watch the data accumulate.</span></span>

![Usar o Visual Studio para publicar seu aplicativo](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="bf444-183">Quando você executa no modo de depuração, a telemetria é expressa através da pipeline, de modo que voc~e deve ver dados aparecendo dentro de segundos.</span><span class="sxs-lookup"><span data-stu-id="bf444-183">When you run in debug mode, telemetry is expedited through the pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="bf444-184">Quando você implanta seu aplicativo na configuração de Versão, os dados acumulam mais lentamente.</span><span class="sxs-lookup"><span data-stu-id="bf444-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-to-your-server"></a><span data-ttu-id="bf444-185">Nenhum dado depois de publicar no servidor?</span><span class="sxs-lookup"><span data-stu-id="bf444-185">No data after you publish to your server?</span></span>
<span data-ttu-id="bf444-186">Abra estas portas para tráfego de saída no firewall do servidor.</span><span class="sxs-lookup"><span data-stu-id="bf444-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="bf444-187">Confira [essa página](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) para obter a lista de endereços necessários</span><span class="sxs-lookup"><span data-stu-id="bf444-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for the list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="bf444-188">Problemas no servidor de compilação?</span><span class="sxs-lookup"><span data-stu-id="bf444-188">Trouble on your build server?</span></span>
<span data-ttu-id="bf444-189">Consulte [este item de solução de problemas](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="bf444-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="bf444-190">Se o seu aplicativo gerar muita telemetria, o módulo de amostragem adaptável reduzirá automaticamente o volume enviado ao portal, enviando apenas uma fração representativa de eventos.</span><span class="sxs-lookup"><span data-stu-id="bf444-190">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="bf444-191">No entanto, os eventos relacionados à mesma solicitação serão selecionadas ou desmarcadas como um grupo, para que você possa navegar entre os eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="bf444-191">However, events that are related to the same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="bf444-192">[Saiba mais sobre amostragem](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="bf444-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="bf444-193">Vídeo</span><span class="sxs-lookup"><span data-stu-id="bf444-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="bf444-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf444-194">Next steps</span></span>
* <span data-ttu-id="bf444-195">[Adicione mais telemetria](app-insights-asp-net-more.md) para obter uma visão de 360 graus completa de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf444-195">[Add more telemetry](app-insights-asp-net-more.md) to get the full 360-degree view of your application.</span></span>

