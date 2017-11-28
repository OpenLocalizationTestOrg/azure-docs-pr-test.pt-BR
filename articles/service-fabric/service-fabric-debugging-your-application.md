---
title: aaaDebug seu aplicativo no Visual Studio | Microsoft Docs
description: "Melhore Olá confiabilidade e o desempenho de seus serviços, desenvolver e depurá-los no Visual Studio em um cluster de desenvolvimento local."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="3edc8-103">Depurar seu aplicativo do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3edc8-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3edc8-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="3edc8-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="3edc8-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="3edc8-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="3edc8-106">Depurar um aplicativo local do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3edc8-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="3edc8-107">Você pode economizar tempo e dinheiro implantando e depurando seu aplicativo do Service Fabric do Azure no cluster de desenvolvimento de um computador local.</span><span class="sxs-lookup"><span data-stu-id="3edc8-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="3edc8-108">Visual Studio 2017 ou Visual Studio 2015 pode implantar aplicativos de saudação toohello cluster local e conectar-se automaticamente instâncias de tooall depurador saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3edc8-108">Visual Studio 2017 or Visual Studio 2015 can deploy hello application toohello local cluster and automatically connect hello debugger tooall instances of your application.</span></span>

1. <span data-ttu-id="3edc8-109">Iniciar um cluster de desenvolvimento local, seguindo as etapas de saudação em [configurar seu ambiente de desenvolvimento do Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3edc8-109">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="3edc8-110">Pressione **F5** ou clique em **Depurar** > **Iniciar Depuração**.</span><span class="sxs-lookup"><span data-stu-id="3edc8-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Iniciar depuração de um aplicativo][startdebugging]
3. <span data-ttu-id="3edc8-112">Definir pontos de interrupção no seu código e percorrer o aplicativo hello clicando nos comandos no hello **depurar** menu.</span><span class="sxs-lookup"><span data-stu-id="3edc8-112">Set breakpoints in your code and step through hello application by clicking commands in hello **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3edc8-113">O Visual Studio anexa tooall instâncias do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3edc8-113">Visual Studio attaches tooall instances of your application.</span></span> <span data-ttu-id="3edc8-114">Ao percorrer o código, os pontos de interrupção podem ser atingidos por vários processos, resultando em sessões simultâneas.</span><span class="sxs-lookup"><span data-stu-id="3edc8-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="3edc8-115">Tente desabilitar pontos de interrupção Olá depois que eles for atingidos, fazendo cada ponto de interrupção condicional na ID de thread de saudação ou por meio de eventos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="3edc8-115">Try disabling hello breakpoints after they're hit, by making each breakpoint conditional on hello thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="3edc8-116">Olá **eventos de diagnóstico** janela será aberta automaticamente para que você possa exibir eventos de diagnóstico em tempo real.</span><span class="sxs-lookup"><span data-stu-id="3edc8-116">hello **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![Exibir eventos de diagnóstico em tempo real][diagnosticevents]
5. <span data-ttu-id="3edc8-118">Você também pode abrir Olá **eventos de diagnóstico** janela no Pesquisador de objetos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3edc8-118">You can also open hello **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="3edc8-119">Em **Service Fabric**, clique com o botão direito do mouse em qualquer nó e escolha **Exibir Rastreamentos de Streaming**.</span><span class="sxs-lookup"><span data-stu-id="3edc8-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Janela de eventos de diagnóstico Olá aberto][viewdiagnosticevents]
   
    <span data-ttu-id="3edc8-121">Se você quiser toofilter seus rastreamentos tooa serviço ou aplicativo específico, basta habilite streaming rastreamentos em que serviço ou aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="3edc8-121">If you want toofilter your traces tooa specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="3edc8-122">eventos de diagnóstico Olá podem ser vistos no hello gerado automaticamente **ServiceEventSource.cs** de arquivos e são chamados de código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3edc8-122">hello diagnostic events can be seen in hello automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="3edc8-123">Olá **eventos de diagnóstico** janela oferece suporte à filtragem, pausando e inspecionar os eventos em tempo real.</span><span class="sxs-lookup"><span data-stu-id="3edc8-123">hello **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="3edc8-124">filtro de saudação é uma pesquisa simples de cadeia de caracteres da mensagem de evento hello, incluindo seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="3edc8-124">hello filter is a simple string search of hello event message, including its contents.</span></span>
   
    ![Filtrar, pausar e retomar ou inspecionar eventos em tempo real][diagnosticeventsactions]
8. <span data-ttu-id="3edc8-126">A depuração de serviços é semelhante à depuração de qualquer outro aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3edc8-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="3edc8-127">Normalmente, você define pontos de interrupção por meio do Visual Studio para fácil depuração.</span><span class="sxs-lookup"><span data-stu-id="3edc8-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="3edc8-128">Embora as Reliable Collections sejam replicadas em vários nós, elas ainda implementam IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="3edc8-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="3edc8-129">Isso significa que você pode usar Olá exibição dos resultados no Visual Studio durante a depuração toosee que é armazenado dentro.</span><span class="sxs-lookup"><span data-stu-id="3edc8-129">This means that you can use hello Results View in Visual Studio while debugging toosee what you've stored inside.</span></span> <span data-ttu-id="3edc8-130">Basta definir um ponto de interrupção em qualquer lugar em seu código.</span><span class="sxs-lookup"><span data-stu-id="3edc8-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Iniciar depuração de um aplicativo][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="3edc8-132">Depurar um aplicativo remoto do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3edc8-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="3edc8-133">Se seus aplicativos do Service Fabric estiver executando em um cluster do Service Fabric no Azure, você será capaz de tooremotely depurar esses, diretamente do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3edc8-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able tooremotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="3edc8-134">Olá recurso requer [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) e [SDK do Azure para .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3edc8-134">hello feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="3edc8-135">Depuração remota destina-se para cenários de desenvolvimento/teste e não toobe usada em ambientes de produção, devido ao impacto de saudação em Olá aplicativos em execução.</span><span class="sxs-lookup"><span data-stu-id="3edc8-135">Remote debugging is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> 
> 

1. <span data-ttu-id="3edc8-136">Navegue cluster tooyour **Cloud Explorer**, com o botão direito e escolha **Ativar depuração**</span><span class="sxs-lookup"><span data-stu-id="3edc8-136">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Habilitar depuração remota][enableremotedebugging]
   
    <span data-ttu-id="3edc8-138">Isso iniciará o processo de saudação de habilitar Olá extensão em nós do cluster de depuração remota, bem como as configurações de rede necessárias.</span><span class="sxs-lookup"><span data-stu-id="3edc8-138">This will kick off hello process of enabling hello remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="3edc8-139">Nó de cluster de saudação com o botão direito em **Cloud Explorer**e escolha **Anexar depurador**</span><span class="sxs-lookup"><span data-stu-id="3edc8-139">Right-click hello cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Anexar Depurador][attachdebugger]
3. <span data-ttu-id="3edc8-141">Em Olá **anexar tooprocess** caixa de diálogo, escolha o processo de saudação desejado toodebug e clique em **anexar**</span><span class="sxs-lookup"><span data-stu-id="3edc8-141">In hello **Attach tooprocess** dialog, choose hello process you want toodebug, and click **Attach**</span></span>
   
    ![Escolher processo][chooseprocess]
   
    <span data-ttu-id="3edc8-143">nome de saudação do processo de saudação desejado tooattach para, equals Olá nome do seu nome de assembly do projeto de serviço.</span><span class="sxs-lookup"><span data-stu-id="3edc8-143">hello name of hello process you want tooattach to, equals hello name of your service project assembly name.</span></span>
   
    <span data-ttu-id="3edc8-144">Olá depurador se anexará tooall nós executando o processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3edc8-144">hello debugger will attach tooall nodes running hello process.</span></span>
   
   * <span data-ttu-id="3edc8-145">No caso de Olá onde você está depurando um serviço sem monitoração de estado, todas as instâncias do serviço de saudação em todos os nós são parte da sessão de depuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="3edc8-145">In hello case where you are debugging a stateless service, all instances of hello service on all nodes are part of hello debug session.</span></span>
   * <span data-ttu-id="3edc8-146">Se você estiver depurando um serviço com monitoração de estado, apenas Olá réplica primária de qualquer partição será ativo e, portanto, capturada pelo depurador hello.</span><span class="sxs-lookup"><span data-stu-id="3edc8-146">If you are debugging a stateful service, only hello primary replica of any partition will be active and therefore caught by hello debugger.</span></span> <span data-ttu-id="3edc8-147">Se a réplica primária Olá move durante a sessão de depuração Olá, processamento de saudação da réplica ainda farão parte da sessão de depuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="3edc8-147">If hello primary replica moves during hello debug session, hello processing of that replica will still be part of hello debug session.</span></span>
   * <span data-ttu-id="3edc8-148">Em partições relevantes da ordem tooonly catch ou instâncias de um determinado serviço, você pode usar pontos de interrupção condicionais tooonly quebra uma partição específica ou instância.</span><span class="sxs-lookup"><span data-stu-id="3edc8-148">In order tooonly catch relevant partitions or instances of a given service, you can use conditional breakpoints tooonly break a specific partition or instance.</span></span>
     
     ![Ponto de interrupção condicional][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="3edc8-150">Atualmente não há suporte para depuração de um cluster do Service Fabric com várias instâncias do hello mesmo nome executável do serviço.</span><span class="sxs-lookup"><span data-stu-id="3edc8-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of hello same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="3edc8-151">Depois de concluir a depuração do seu aplicativo, você pode desabilitar a extensão de depuração remota Olá clicando com o cluster de saudação em **Cloud Explorer** e escolha **Desabilitar depuração**</span><span class="sxs-lookup"><span data-stu-id="3edc8-151">Once you finish debugging your application, you can disable hello remote debugging extension by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Desabilitar depuração remota][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="3edc8-153">Transmitindo rastreamentos de um nó de cluster remoto</span><span class="sxs-lookup"><span data-stu-id="3edc8-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="3edc8-154">Também é possível toostream rastreamentos diretamente de um nó de cluster remoto tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="3edc8-154">You are also able toostream traces directly from a remote cluster node tooVisual Studio.</span></span> <span data-ttu-id="3edc8-155">Esse recurso permite que você toostream os eventos de rastreamento do ETW, produzidos em um nó de cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3edc8-155">This feature allows you toostream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="3edc8-156">O recurso requer o [SDK do Service Fabric 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) e o [SDK do Azure para .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3edc8-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="3edc8-157">Esse recurso só oferece suporte a clusters em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="3edc8-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="3edc8-158">Streaming rastreamentos destina-se para cenários de desenvolvimento/teste e não toobe usada em ambientes de produção, devido ao impacto de saudação em Olá aplicativos em execução.</span><span class="sxs-lookup"><span data-stu-id="3edc8-158">Streaming traces is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> <span data-ttu-id="3edc8-159">Em um cenário de produção, você deve confiar nos eventos de encaminhamento usando o Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="3edc8-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="3edc8-160">Navegue cluster tooyour **Cloud Explorer**, com o botão direito e escolha **habilitar rastreamentos de Streaming**</span><span class="sxs-lookup"><span data-stu-id="3edc8-160">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Habilitar transmissão remota de rastreamentos][enablestreamingtraces]
   
    <span data-ttu-id="3edc8-162">Isso iniciará o processo de saudação de habilitar Olá streaming extensão rastreamentos em nós do cluster, bem como as configurações de rede necessárias.</span><span class="sxs-lookup"><span data-stu-id="3edc8-162">This will kick off hello process of enabling hello streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="3edc8-163">Expanda Olá **nós** elemento **Cloud Explorer**, nó de saudação com o botão direito você deseja toostream rastreamentos do e escolha **rastreamentos de Streaming de exibição**</span><span class="sxs-lookup"><span data-stu-id="3edc8-163">Expand hello **Nodes** element in **Cloud Explorer**, right-click hello node you want toostream traces from and choose **View Streaming Traces**</span></span>
   
    ![Exibir transmissão remota de rastreamentos][viewremotestreamingtraces]
   
    <span data-ttu-id="3edc8-165">Repita a etapa 2 para nós quantos desejar toosee rastreamentos do.</span><span class="sxs-lookup"><span data-stu-id="3edc8-165">Repeat step 2 for as many nodes as you want toosee traces from.</span></span> <span data-ttu-id="3edc8-166">Cada fluxo de nó será mostrado em uma janela dedicada.</span><span class="sxs-lookup"><span data-stu-id="3edc8-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="3edc8-167">Agora você está toosee capaz de rastreamentos de saudação emitidos pelo serviço de malha e seus serviços.</span><span class="sxs-lookup"><span data-stu-id="3edc8-167">You are now able toosee hello traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="3edc8-168">Se você quiser toofilter Olá eventos tooonly mostrar um aplicativo específico, basta digite nome de saudação do aplicativo hello no filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="3edc8-168">If you want toofilter hello events tooonly show a specific application, simply type in hello name of hello application in hello filter.</span></span>
   
    ![Exibindo transmissão de rastreamentos][viewingstreamingtraces]
3. <span data-ttu-id="3edc8-170">Depois de terminar de rastreamentos de streaming do cluster, você pode desabilitar remotos rastreamentos de streaming, clicando com o cluster Olá **Cloud Explorer** e escolha **desabilitar rastreamentos de Streaming**</span><span class="sxs-lookup"><span data-stu-id="3edc8-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Desabilitar transmissão remota de rastreamentos][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="3edc8-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3edc8-172">Next steps</span></span>
* <span data-ttu-id="3edc8-173">[Testar um serviço da Malha do Serviço](service-fabric-testability-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3edc8-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="3edc8-174">[Gerenciar seu aplicativo do Service Fabric no Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="3edc8-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
