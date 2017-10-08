---
title: "aaaAzure depurador de instantâneo de informações do aplicativo para aplicativos .NET | Microsoft Docs"
description: "Depure instantâneos são coletados automaticamente quando exceções forem geradas na produção de aplicativos .NET"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="8b3c8-103">Depurar instantâneos em exceções em aplicativos .NET</span><span class="sxs-lookup"><span data-stu-id="8b3c8-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="8b3c8-104">Quando ocorrer uma exceção, você pode coletar automaticamente um Instantâneo de Depuração de seu aplicativo web ativo.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="8b3c8-105">instantâneo Olá mostra o estado de saudação do código-fonte e variáveis na exceção de saudação do momento Olá foi lançada.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-105">hello snapshot shows hello state of source code and variables at hello moment hello exception was thrown.</span></span> <span data-ttu-id="8b3c8-106">Olá depurador de instantâneo (visualização) em [Azure Application Insights](app-insights-overview.md) monitora a telemetria de exceção de seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-106">hello Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="8b3c8-107">Ele coleta instantâneos na sua parte superior-Lançando exceções para que você tenha informações Olá necessárias toodiagnose problemas em produção.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-107">It collects snapshots on your top-throwing exceptions so that you have hello information you need toodiagnose issues in production.</span></span> <span data-ttu-id="8b3c8-108">Incluir Olá [pacote de NuGet de coletor de instantâneo](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) em seu aplicativo e, opcionalmente, configurar parâmetros de coleta em [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md). Instantâneos exibidos em [exceções](app-insights-asp-net-exceptions.md) no portal do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-108">Include hello [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

<span data-ttu-id="8b3c8-109">Você pode exibir instantâneos de depuração na pilha de chamadas de Olá Olá toosee portal e inspecionar variáveis em cada quadro de pilha de chamadas.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-109">You can view debug snapshots in hello portal toosee hello call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="8b3c8-110">tooget uma experiência de depuração mais eficiente com o código-fonte, abra instantâneos com Visual Studio 2017 Enterprise por [baixar a extensão de depurador instantâneo Olá para Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="8b3c8-110">tooget a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="8b3c8-111">Coleta de instantâneo está disponível para:</span><span class="sxs-lookup"><span data-stu-id="8b3c8-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="8b3c8-112">Aplicativos ASP.NET e do .NET framework com o .NET Framework 4.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="8b3c8-113">Aplicativos do .NET Core 2.0 e Núcleo do ASP.NET Core 2.0 em execução no Windows.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="8b3c8-114">Configurar a coleta de instantâneo para aplicativos ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8b3c8-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="8b3c8-115">[Habilite o Application Insights no seu aplicativo web](app-insights-asp-net.md), se você ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="8b3c8-116">Incluir Olá [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pacote NuGet em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-116">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="8b3c8-117">Examinar opções padrão Olá Olá pacote adicionado muito[Applicationinsights](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="8b3c8-117">Review hello default options that hello package added too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="8b3c8-118">Os instantâneos são coletados apenas em exceções que são relatados tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-118">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="8b3c8-119">Em alguns casos (por exemplo, versões mais antigas da plataforma de .NET Olá), talvez seja necessário muito[configurar coleta de exceção](app-insights-asp-net-exceptions.md#exceptions) toosee exceções com instantâneos no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-119">In some cases (for example, older versions of hello .NET platform), you might need too[configure exception collection](app-insights-asp-net-exceptions.md#exceptions) toosee exceptions with snapshots in hello portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="8b3c8-120">Configurar a coleta de instantâneo para aplicativos do Núcleo do ASP.NET 2.0</span><span class="sxs-lookup"><span data-stu-id="8b3c8-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="8b3c8-121">[Habilite o Application Insights no seu aplicativo web Núcleo do ASP.NET](app-insights-asp-net-core.md), se você ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="8b3c8-122">Incluir Olá [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pacote NuGet em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-122">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="8b3c8-123">Modificar Olá `ConfigureServices` método em seu aplicativo `Startup` classe processador de telemetria do coletor do instantâneo tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-123">Modify hello `ConfigureServices` method in your application's `Startup` class tooadd hello Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="8b3c8-124">código Hello, você deve adicionar depende da versão referenciada Olá Olá pacote Microsoft.ApplicationInsights.ASPNETCore NuGet.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-124">hello code you should add depends on hello referenced version of hello Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="8b3c8-125">Para Microsoft.ApplicationInsights.AspNetCore 2.1.0, adicione:</span><span class="sxs-lookup"><span data-stu-id="8b3c8-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="8b3c8-126">Para Microsoft.ApplicationInsights.AspNetCore 2.1.1, adicione:</span><span class="sxs-lookup"><span data-stu-id="8b3c8-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="8b3c8-127">Configurar a coleta de instantâneo para outros aplicativos .NET</span><span class="sxs-lookup"><span data-stu-id="8b3c8-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="8b3c8-128">Se seu aplicativo já não está instrumentado com o Application Insights, começar por [habilitando o Application Insights e chave de instrumentação Olá configuração](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="8b3c8-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting hello instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="8b3c8-129">Adicionar Olá [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pacote NuGet em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-129">Add hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="8b3c8-130">Os instantâneos são coletados apenas em exceções que são relatados tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-130">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="8b3c8-131">Talvez seja necessário toomodify tooreport seu código-los.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-131">You may need toomodify your code tooreport them.</span></span> <span data-ttu-id="8b3c8-132">código de tratamento de exceção de saudação depende da estrutura de saudação do seu aplicativo, mas é um exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="8b3c8-132">hello exception handling code depends on hello structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="8b3c8-133">Conceder permissões</span><span class="sxs-lookup"><span data-stu-id="8b3c8-133">Grant permissions</span></span>

<span data-ttu-id="8b3c8-134">Os proprietários de saudação assinatura do Azure podem inspecionar instantâneos.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-134">Owners of hello Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="8b3c8-135">Outros usuários devem ter permissão de um proprietário.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="8b3c8-136">permissão toogrant, atribuir Olá `Application Insights Snapshot Debugger` toousers de função que irá inspecionar instantâneos.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-136">toogrant permission, assign hello `Application Insights Snapshot Debugger` role toousers who will inspect snapshots.</span></span> <span data-ttu-id="8b3c8-137">Essa função pode ser atribuída tooindividual usuários ou grupos através de proprietários de assinatura de destino Olá recurso do Application Insights ou seu grupo de recursos ou a assinatura.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-137">This role can be assigned tooindividual users or groups by subscription owners for hello target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="8b3c8-138">Abra a folha de controle de acesso (IAM) hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-138">Open hello Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="8b3c8-139">Clique em Olá + botão Adicionar.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-139">Click hello +Add button.</span></span>
1. <span data-ttu-id="8b3c8-140">Selecione depurador de instantâneo de informações do aplicativo na lista suspensa de funções da saudação.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-140">Select Application Insights Snapshot Debugger from hello Roles drop-down list.</span></span>
1. <span data-ttu-id="8b3c8-141">Procure e insira um nome para Olá tooadd de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-141">Search for and enter a name for hello user tooadd.</span></span>
1. <span data-ttu-id="8b3c8-142">Clique em Olá Salvar botão tooadd Olá usuário toohello função.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-142">Click hello Save button tooadd hello user toohello role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="8b3c8-143">Os instantâneos potencialmente podem conter informações pessoais e outras informações confidenciais em valores de parâmetro e variável.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-hello-application-insights-portal"></a><span data-ttu-id="8b3c8-144">Depurar instantâneos no portal do Application Insights Olá</span><span class="sxs-lookup"><span data-stu-id="8b3c8-144">Debug snapshots in hello Application Insights portal</span></span>

<span data-ttu-id="8b3c8-145">Se um instantâneo está disponível para uma determinada exceção ou uma ID do problema, um **abrir instantâneo depurar** botão aparece no hello [exceção](app-insights-asp-net-exceptions.md) no portal do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on hello [exception](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

![Botão Abrir Instantâneo de Depuração na exceção](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="8b3c8-147">Olá exibição de instantâneo de depuração, verá uma pilha de chamadas e um painel variáveis.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-147">In hello Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="8b3c8-148">Quando você seleciona quadros de chamada de saudação de pilha no painel de pilha de chamada hello, você pode exibir as variáveis locais e parâmetros para essa função é chamada no painel de variáveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-148">When you select frames of hello call stack in hello call stack pane, you can view local variables and parameters for that function call in hello variables pane.</span></span>

![Exibir instantâneo depurar no portal de saudação](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="8b3c8-150">Os instantâneos podem conter informações confidenciais e, por padrão, não estão visíveis.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="8b3c8-151">tooview instantâneos, você deve ter Olá `Application Insights Snapshot Debugger` tooyou função atribuída.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-151">tooview snapshots, you must have hello `Application Insights Snapshot Debugger` role assigned tooyou.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="8b3c8-152">Depurar instantâneos com o Visual Studio 2017 Enterprise</span><span class="sxs-lookup"><span data-stu-id="8b3c8-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="8b3c8-153">Clique em Olá **baixar instantâneo** toodownload botão um `.diagsession` arquivo, que pode ser aberto pelo Visual Studio Enterprise de 2017.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-153">Click hello **Download Snapshot** button toodownload a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="8b3c8-154">Olá tooopen `.diagsession` arquivo, você deve primeiro [baixar e instalar a extensão de depurador de instantâneo de saudação do Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="8b3c8-154">tooopen hello `.diagsession` file, you must first [download and install hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="8b3c8-155">Depois de abrir o arquivo de instantâneo hello, página de depuração de minidespejo Olá no Visual Studio é exibida.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-155">After you open hello snapshot file, hello Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="8b3c8-156">Clique em **depurar código gerenciado** toostart depuração instantâneo hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-156">Click **Debug Managed Code** toostart debugging hello snapshot.</span></span> <span data-ttu-id="8b3c8-157">instantâneo Olá abre toohello de linha de código onde a exceção de saudação foi gerada para que você pode depurar o estado atual de saudação do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-157">hello snapshot opens toohello line of code where hello exception was thrown so that you can debug hello current state of hello process.</span></span>

    ![Exibir instantâneo de depuração no Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="8b3c8-159">instantâneo baixados Olá contém os arquivos de símbolo que foram encontrados no servidor de aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-159">hello downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="8b3c8-160">Esses arquivos de símbolo são dados de instantâneo tooassociate necessárias ao código-fonte.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-160">These symbol files are required tooassociate snapshot data with source code.</span></span> <span data-ttu-id="8b3c8-161">Para aplicativos de serviço de aplicativo, tornam a implantação de símbolo de tooenable-se de que quando você publicar seus aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-161">For App Service apps, make sure tooenable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="8b3c8-162">Como os instantâneos funcionam</span><span class="sxs-lookup"><span data-stu-id="8b3c8-162">How snapshots work</span></span>

<span data-ttu-id="8b3c8-163">Quando seu aplicativo é iniciado, é criado um processo separado de carregador de instantâneos que monitora seu aplicativo quanto a solicitações de instantâneos.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="8b3c8-164">Quando um instantâneo é solicitado, é feita uma cópia de sombra de saudação executando o processo em cerca de 10 minutos de too20.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-164">When a snapshot is requested, a shadow copy of hello running process is made in about 10 too20 minutes.</span></span> <span data-ttu-id="8b3c8-165">processo de sombra Olá é analisado e um instantâneo é criado durante o processo principal Olá continua toorun e servir toousers de tráfego.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-165">hello shadow process is then analyzed, and a snapshot is created while hello main process continues toorun and serve traffic toousers.</span></span> <span data-ttu-id="8b3c8-166">Olá instantâneo for carregado tooApplication Insights junto com todos os arquivos relevantes de símbolo (. PDB) que são necessárias tooview instantâneo hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-166">hello snapshot is then uploaded tooApplication Insights along with any relevant symbol (.pdb) files that are needed tooview hello snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="8b3c8-167">Limitações atuais</span><span class="sxs-lookup"><span data-stu-id="8b3c8-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="8b3c8-168">Publicar símbolos</span><span class="sxs-lookup"><span data-stu-id="8b3c8-168">Publish symbols</span></span>
<span data-ttu-id="8b3c8-169">Olá depurador instantâneo requer arquivos de símbolo em variáveis de toodecode de servidor de produção de hello e tooprovide uma experiência de depuração no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-169">hello Snapshot Debugger requires symbol files on hello production server toodecode variables and tooprovide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="8b3c8-170">versão de Hello 15.2 do Visual Studio de 2017 publica símbolos para compilações de versão por padrão quando ele é publicado tooApp serviço.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-170">hello 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes tooApp Service.</span></span> <span data-ttu-id="8b3c8-171">Em versões anteriores, você precisa fazer tooadd Olá seguinte perfil de publicação de linha tooyour `.pubxml` arquivos de forma que os símbolos são publicados no modo de liberação:</span><span class="sxs-lookup"><span data-stu-id="8b3c8-171">In prior versions, you need tooadd hello following line tooyour publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="8b3c8-172">Para outros tipos e computação do Azure, verifique se os arquivos de símbolo de saudação estão em Olá mesma pasta do. dll do aplicativo principal hello (normalmente, `wwwroot/bin`) ou estão disponíveis no caminho atual hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-172">For Azure Compute and other types, ensure that hello symbol files are in hello same folder of hello main application .dll (typically, `wwwroot/bin`) or are available on hello current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="8b3c8-173">Builds otimizados</span><span class="sxs-lookup"><span data-stu-id="8b3c8-173">Optimized builds</span></span>
<span data-ttu-id="8b3c8-174">Em alguns casos, variáveis locais não podem ser exibidas nas compilações de lançamento devido a otimizações que são aplicadas durante o processo de compilação hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during hello build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8b3c8-175">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="8b3c8-175">Troubleshooting</span></span>

<span data-ttu-id="8b3c8-176">Estas dicas ajudarão-lo a solucionar problemas com hello depurador de instantâneo.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-176">These tips help you troubleshoot problems with hello Snapshot Debugger.</span></span>

### <a name="verify-hello-instrumentation-key"></a><span data-ttu-id="8b3c8-177">Verifique se a chave de instrumentação Olá</span><span class="sxs-lookup"><span data-stu-id="8b3c8-177">Verify hello instrumentation key</span></span>

<span data-ttu-id="8b3c8-178">Certifique-se de que você está usando a chave de instrumentação correto de saudação em seu aplicativo publicado.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-178">Make sure that you're using hello correct instrumentation key in your published application.</span></span> <span data-ttu-id="8b3c8-179">Geralmente, Application Insights lê chave de instrumentação de saudação do arquivo applicationinsights. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-179">Usually, Application Insights reads hello instrumentation key from hello ApplicationInsights.config file.</span></span> <span data-ttu-id="8b3c8-180">Verifique se que o valor de saudação é Olá mesmo como chave de instrumentação de saudação do recurso do Application Insights Olá que você vê no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-180">Verify that hello value is hello same as hello instrumentation key for hello Application Insights resource that you see in hello portal.</span></span>

### <a name="check-hello-uploader-logs"></a><span data-ttu-id="8b3c8-181">Verifique os logs de carregador Olá</span><span class="sxs-lookup"><span data-stu-id="8b3c8-181">Check hello uploader logs</span></span>

<span data-ttu-id="8b3c8-182">Depois que um instantâneo é criado, um arquivo de minidespejo (. dmp) é criado no disco.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="8b3c8-183">Um processo separado do carregador usa esse arquivo de minidespejo e carrega, juntamente com qualquer PDBs associados, tooApplication armazenamento de Insights instantâneo depurador.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, tooApplication Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="8b3c8-184">Após o minidespejo Olá foi carregado com êxito, ele é excluído do disco.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-184">After hello minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="8b3c8-185">arquivos de log de saudação de carregador de minidespejo Olá são mantidos em disco.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-185">hello log files for hello minidump uploader are retained on disk.</span></span> <span data-ttu-id="8b3c8-186">Em um ambiente de Serviço de Aplicativo, você pode encontrar esses logs em `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="8b3c8-187">Site de gerenciamento do uso Olá Kudu para o serviço de aplicativo toofind esses arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-187">Use hello Kudu management site for App Service toofind these log files.</span></span>

1. <span data-ttu-id="8b3c8-188">Abra o aplicativo de serviço de aplicativo em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-188">Open your App Service application in hello Azure portal.</span></span>

2. <span data-ttu-id="8b3c8-189">Selecione Olá **ferramentas avançadas de** folha ou procurar **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-189">Select hello **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="8b3c8-190">Clique em **Ir**.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-190">Click **Go**.</span></span>
4. <span data-ttu-id="8b3c8-191">Em Olá **console de depuração** caixa de listagem suspensa, selecione **CMD**.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-191">In hello **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="8b3c8-192">Clique em **Arquivos de Log**.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-192">Click **LogFiles**.</span></span>

<span data-ttu-id="8b3c8-193">Você deverá ver pelo menos um arquivo com um nome que começa com `Uploader_` e uma extensão `.log`.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="8b3c8-194">Clique em toodownload de ícone apropriado Olá os arquivos de log ou abri-los em um navegador.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-194">Click hello appropriate icon toodownload any log files or open them in a browser.</span></span>
<span data-ttu-id="8b3c8-195">nome de arquivo Hello inclui o nome da máquina hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-195">hello file name includes hello machine name.</span></span> <span data-ttu-id="8b3c8-196">Se a instância do Serviço de Aplicativo é hospedada em mais de uma máquina, há arquivos de log separados para cada máquina.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="8b3c8-197">Quando o carregador de saudação detecta um novo arquivo de minidespejo, ele será registrado no arquivo de log de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-197">When hello uploader detects a new minidump file, it is recorded in hello log file.</span></span> <span data-ttu-id="8b3c8-198">Aqui está um exemplo de um upload bem-sucedido:</span><span class="sxs-lookup"><span data-stu-id="8b3c8-198">Here's an example of a successful upload:</span></span>

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

<span data-ttu-id="8b3c8-199">No exemplo anterior de saudação, chave de instrumentação Olá é `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-199">In hello previous example, hello instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="8b3c8-200">Esse valor deve corresponder a chave de instrumentação Olá para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-200">This value should match hello instrumentation key for your application.</span></span>
<span data-ttu-id="8b3c8-201">minidespejo Hello está associado um instantâneo com a ID de saudação `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-201">hello minidump is associated with a snapshot with hello ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="8b3c8-202">Você pode usar essa ID posterior Olá de toolocate associados a telemetria de exceção no Application Insights análise.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-202">You can use this ID later toolocate hello associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="8b3c8-203">carregador de saudação procura novos PDBs sobre uma vez a cada 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-203">hello uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="8b3c8-204">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="8b3c8-204">Here's an example:</span></span>

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

<span data-ttu-id="8b3c8-205">Para aplicativos que são _não_ hospedado no serviço de aplicativo, logs de carregador Olá estão em Olá mesma pasta Olá minidespejos: `%TEMP%\Dumps\<ikey>` (onde `<ikey>` é a sua chave de instrumentação).</span><span class="sxs-lookup"><span data-stu-id="8b3c8-205">For applications that are _not_ hosted in App Service, hello uploader logs are in hello same folder as hello minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a><span data-ttu-id="8b3c8-206">Use o Application Insights pesquisar exceções toofind com instantâneos</span><span class="sxs-lookup"><span data-stu-id="8b3c8-206">Use Application Insights search toofind exceptions with snapshots</span></span>

<span data-ttu-id="8b3c8-207">Quando um instantâneo é criado, Olá lançando a exceção é marcado com uma ID de instantâneo.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-207">When a snapshot is created, hello throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="8b3c8-208">Quando a telemetria de exceção Olá é relatado tooApplication Insights, essa ID de instantâneo é incluída como uma propriedade personalizada.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-208">When hello exception telemetry is reported tooApplication Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="8b3c8-209">Usando a folha de pesquisa Olá no Application Insights, você pode localizar toda a telemetria com hello `ai.snapshot.id` propriedade personalizada.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-209">Using hello Search blade in Application Insights, you can find all telemetry with hello `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="8b3c8-210">Procure o recurso Application Insights tooyour Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-210">Browse tooyour Application Insights resource in hello Azure portal.</span></span>
2. <span data-ttu-id="8b3c8-211">Clique em **Pesquisar**.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-211">Click **Search**.</span></span>
3. <span data-ttu-id="8b3c8-212">Tipo `ai.snapshot.id` em Olá caixa de texto de pesquisa e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-212">Type `ai.snapshot.id` in hello Search text box and press Enter.</span></span>

![Pesquisar telemetria com uma ID de instantâneo no portal de saudação](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="8b3c8-214">Se a pesquisa não retornar resultados, nenhum instantâneo foi relatado tooApplication Insights para seu aplicativo no intervalo de tempo de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-214">If this search returns no results, then no snapshots were reported tooApplication Insights for your application in hello selected time range.</span></span>

<span data-ttu-id="8b3c8-215">toosearch para uma ID de instantâneo específicos de logs de carregador hello, digite o ID na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-215">toosearch for a specific snapshot ID from hello Uploader logs, type that ID in hello Search box.</span></span> <span data-ttu-id="8b3c8-216">Se você não conseguir localizar telemetria para um instantâneo que você sabe que foi carregado, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="8b3c8-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="8b3c8-217">Verifique que você está olhando de recurso do Application Insights correta Olá verificando a chave de instrumentação hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-217">Double-check that you're looking at hello right Application Insights resource by verifying hello instrumentation key.</span></span>

2. <span data-ttu-id="8b3c8-218">Usando Olá timestamp do log de carregador hello, ajuste o filtro de intervalo de tempo de saudação do hello pesquisa toocover esse intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-218">Using hello timestamp from hello Uploader log, adjust hello Time Range filter of hello search toocover that time range.</span></span>

<span data-ttu-id="8b3c8-219">Se você não vir uma exceção com essa ID de instantâneo, telemetria de exceção Olá não foi relatado tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-219">If you still don't see an exception with that snapshot ID, then hello exception telemetry wasn't reported tooApplication Insights.</span></span> <span data-ttu-id="8b3c8-220">Essa situação pode ocorrer se o aplicativo falhou após levou instantâneo hello, mas antes de ela relatou a telemetria de exceção de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-220">This situation can happen if your application crashed after it took hello snapshot but before it reported hello exception telemetry.</span></span> <span data-ttu-id="8b3c8-221">Nesse caso, verifique Olá logs de serviço de aplicativo em `Diagnose and solve problems` toosee se houvesse inesperado reinicia ou exceções sem tratamento.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-221">In this case, check hello App Service logs under `Diagnose and solve problems` toosee if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b3c8-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b3c8-222">Next steps</span></span>

* <span data-ttu-id="8b3c8-223">[Definir snappoints em seu código](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget instantâneos sem esperar por uma exceção.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="8b3c8-224">[Diagnosticar exceções em seus aplicativos web](app-insights-asp-net-exceptions.md) explica como toomake tooApplication visíveis de exceções mais informações.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how toomake more exceptions visible tooApplication Insights.</span></span> 
* <span data-ttu-id="8b3c8-225">A [Detecção Inteligente](app-insights-proactive-diagnostics.md) descobre automaticamente anomalias de desempenho.</span><span class="sxs-lookup"><span data-stu-id="8b3c8-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
