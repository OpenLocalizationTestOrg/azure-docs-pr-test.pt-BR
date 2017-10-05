---
title: Depurar seu aplicativo no Visual Studio | Microsoft Docs
description: "Melhore a confiabilidade e o desempenho dos seus serviços desenvolvendo e depurando-os no Visual Studio em um cluster de desenvolvimento local."
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
ms.openlocfilehash: 2459025899a7f5ffebf44fa104ed112c0eb99dfa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="5bf60-103">Depurar seu aplicativo do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5bf60-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5bf60-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="5bf60-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="5bf60-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="5bf60-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="5bf60-106">Depurar um aplicativo local do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5bf60-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="5bf60-107">Você pode economizar tempo e dinheiro implantando e depurando seu aplicativo do Service Fabric do Azure no cluster de desenvolvimento de um computador local.</span><span class="sxs-lookup"><span data-stu-id="5bf60-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="5bf60-108">O Visual Studio 2015 ou 2017 pode implantar o aplicativo no cluster local e conectar o depurador automaticamente a todas as instâncias do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-108">Visual Studio 2017 or Visual Studio 2015 can deploy the application to the local cluster and automatically connect the debugger to all instances of your application.</span></span>

1. <span data-ttu-id="5bf60-109">Inicie um cluster de desenvolvimento local seguindo as etapas em [Configurando o ambiente de desenvolvimento do Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5bf60-109">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="5bf60-110">Pressione **F5** ou clique em **Depurar** > **Iniciar Depuração**.</span><span class="sxs-lookup"><span data-stu-id="5bf60-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Iniciar depuração de um aplicativo][startdebugging]
3. <span data-ttu-id="5bf60-112">Defina os pontos de interrupção em seu código e explore o aplicativo clicando nos comandos do menu **Depurar** .</span><span class="sxs-lookup"><span data-stu-id="5bf60-112">Set breakpoints in your code and step through the application by clicking commands in the **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5bf60-113">O Visual Studio se conecta a todas as instâncias do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-113">Visual Studio attaches to all instances of your application.</span></span> <span data-ttu-id="5bf60-114">Ao percorrer o código, os pontos de interrupção podem ser atingidos por vários processos, resultando em sessões simultâneas.</span><span class="sxs-lookup"><span data-stu-id="5bf60-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="5bf60-115">Tente desabilitar os pontos de interrupção depois que eles forem atingidos, tornando o ponto de interrupção condicional na ID do thread, ou usando eventos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5bf60-115">Try disabling the breakpoints after they're hit, by making each breakpoint conditional on the thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="5bf60-116">A janela **Eventos de Diagnóstico** abrirá automaticamente para exibir eventos de diagnóstico em tempo real.</span><span class="sxs-lookup"><span data-stu-id="5bf60-116">The **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![Exibir eventos de diagnóstico em tempo real][diagnosticevents]
5. <span data-ttu-id="5bf60-118">Você também pode abrir a janela **Eventos de Diagnóstico** no Gerenciador de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="5bf60-118">You can also open the **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="5bf60-119">Em **Service Fabric**, clique com o botão direito do mouse em qualquer nó e escolha **Exibir Rastreamentos de Streaming**.</span><span class="sxs-lookup"><span data-stu-id="5bf60-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Abrir a janela de eventos de diagnóstico][viewdiagnosticevents]
   
    <span data-ttu-id="5bf60-121">Se quiser filtrar os rastreamentos para um serviço ou aplicativo específico, basta habilitar a transmissão de rastreamentos nesse serviço ou aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="5bf60-121">If you want to filter your traces to a specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="5bf60-122">Os eventos de diagnóstico podem ser vistos no arquivo **ServiceEventSource.cs** gerado automaticamente e são chamados do código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-122">The diagnostic events can be seen in the automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="5bf60-123">A janela **Eventos de Diagnóstico** permite filtragem, pausa e eventos de inspeção em tempo real.</span><span class="sxs-lookup"><span data-stu-id="5bf60-123">The **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="5bf60-124">O filtro é uma pesquisa simples de cadeia de caracteres da mensagem do evento, incluindo seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-124">The filter is a simple string search of the event message, including its contents.</span></span>
   
    ![Filtrar, pausar e retomar ou inspecionar eventos em tempo real][diagnosticeventsactions]
8. <span data-ttu-id="5bf60-126">A depuração de serviços é semelhante à depuração de qualquer outro aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="5bf60-127">Normalmente, você define pontos de interrupção por meio do Visual Studio para fácil depuração.</span><span class="sxs-lookup"><span data-stu-id="5bf60-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="5bf60-128">Embora as Reliable Collections sejam replicadas em vários nós, elas ainda implementam IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="5bf60-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="5bf60-129">Isso significa que você pode usar o Modo de Exibição Resultados no Visual Studio durante a depuração para ver o que foi armazenado.</span><span class="sxs-lookup"><span data-stu-id="5bf60-129">This means that you can use the Results View in Visual Studio while debugging to see what you've stored inside.</span></span> <span data-ttu-id="5bf60-130">Basta definir um ponto de interrupção em qualquer lugar em seu código.</span><span class="sxs-lookup"><span data-stu-id="5bf60-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Iniciar depuração de um aplicativo][breakpoint]

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="5bf60-132">Depurar um aplicativo remoto do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5bf60-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="5bf60-133">Se seus aplicativos do Service Fabric estiverem em execução em um cluster do Service Fabric no Azure, é possível depurá-los remotamente, diretamente do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5bf60-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able to remotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="5bf60-134">O recurso requer [SDK do Service Fabric 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) e [SDK do Azure para .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5bf60-134">The feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="5bf60-135">A depuração remota é destinada a cenários de desenvolvimento/teste e não para uso em ambientes de produção, devido ao impacto nos aplicativos em execução.</span><span class="sxs-lookup"><span data-stu-id="5bf60-135">Remote debugging is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.</span></span>
> 
> 

1. <span data-ttu-id="5bf60-136">Navegue até o cluster em **Gerenciador de Nuvem**, clique com o botão direito do mouse e escolha **Habilitar Depuração**</span><span class="sxs-lookup"><span data-stu-id="5bf60-136">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Habilitar depuração remota][enableremotedebugging]
   
    <span data-ttu-id="5bf60-138">Isso iniciará o processo de habilitar a extensão de depuração remota em seus nós de cluster, bem como as configurações de rede necessárias.</span><span class="sxs-lookup"><span data-stu-id="5bf60-138">This will kick off the process of enabling the remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="5bf60-139">Clique com o botão direito do mouse no nó de cluster em **Gerenciador de Nuvem** e escolha **Anexar Depurador**</span><span class="sxs-lookup"><span data-stu-id="5bf60-139">Right-click the cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Anexar Depurador][attachdebugger]
3. <span data-ttu-id="5bf60-141">Na caixa de diálogo **Anexar ao processo**, escolha o processo que deseja depurar e, em seguida, clique em **Anexar**</span><span class="sxs-lookup"><span data-stu-id="5bf60-141">In the **Attach to process** dialog, choose the process you want to debug, and click **Attach**</span></span>
   
    ![Escolher processo][chooseprocess]
   
    <span data-ttu-id="5bf60-143">O nome do processo ao qual você quer anexar é igual ao nome do assembly do seu projeto de serviço.</span><span class="sxs-lookup"><span data-stu-id="5bf60-143">The name of the process you want to attach to, equals the name of your service project assembly name.</span></span>
   
    <span data-ttu-id="5bf60-144">O depurador vai anexar a todos os nós que estão executando o processo.</span><span class="sxs-lookup"><span data-stu-id="5bf60-144">The debugger will attach to all nodes running the process.</span></span>
   
   * <span data-ttu-id="5bf60-145">No caso em que você estiver depurando um serviço sem estado, todas as instâncias do serviço em todos os nós farão parte da sessão de depuração.</span><span class="sxs-lookup"><span data-stu-id="5bf60-145">In the case where you are debugging a stateless service, all instances of the service on all nodes are part of the debug session.</span></span>
   * <span data-ttu-id="5bf60-146">Se estiver depurando um serviço com estado, somente a réplica primária de qualquer partição estará ativa e, portanto, a que será capturada pelo depurador.</span><span class="sxs-lookup"><span data-stu-id="5bf60-146">If you are debugging a stateful service, only the primary replica of any partition will be active and therefore caught by the debugger.</span></span> <span data-ttu-id="5bf60-147">Se a réplica primária for movida durante a sessão de depuração, o processamento de tal réplica ainda fará parte da sessão de depuração.</span><span class="sxs-lookup"><span data-stu-id="5bf60-147">If the primary replica moves during the debug session, the processing of that replica will still be part of the debug session.</span></span>
   * <span data-ttu-id="5bf60-148">Para capturar apenas as partições ou instâncias relevantes de um determinado serviço, você pode usar pontos de interrupção condicionais para interromper apenas uma partição ou instância específica.</span><span class="sxs-lookup"><span data-stu-id="5bf60-148">In order to only catch relevant partitions or instances of a given service, you can use conditional breakpoints to only break a specific partition or instance.</span></span>
     
     ![Ponto de interrupção condicional][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="5bf60-150">Atualmente, não permitimos a depuração de um cluster do Service Fabric com várias instâncias de mesmo nome do executável de serviço.</span><span class="sxs-lookup"><span data-stu-id="5bf60-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of the same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="5bf60-151">Depois de concluir a depuração do aplicativo, você pode desabilitar a extensão de depuração remota clicando com o botão direito do mouse em **Gerenciador de Nuvem** e escolhendo **Desabilitar Depuração**</span><span class="sxs-lookup"><span data-stu-id="5bf60-151">Once you finish debugging your application, you can disable the remote debugging extension by right-clicking the cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Desabilitar depuração remota][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="5bf60-153">Transmitindo rastreamentos de um nó de cluster remoto</span><span class="sxs-lookup"><span data-stu-id="5bf60-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="5bf60-154">Você também pode transmitir rastreamentos diretamente de um nó de cluster remoto para o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5bf60-154">You are also able to stream traces directly from a remote cluster node to Visual Studio.</span></span> <span data-ttu-id="5bf60-155">Esse recurso permite transmitir eventos de rastreamento ETW gerados em um nó de cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5bf60-155">This feature allows you to stream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="5bf60-156">O recurso requer o [SDK do Service Fabric 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) e o [SDK do Azure para .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5bf60-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="5bf60-157">Esse recurso só oferece suporte a clusters em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="5bf60-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="5bf60-158">A transmissão de rastreamentos destina-se a cenários de desenvolvimento/teste e não ao uso em ambientes de produção, devido ao impacto nos aplicativos em execução.</span><span class="sxs-lookup"><span data-stu-id="5bf60-158">Streaming traces is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.</span></span>
> <span data-ttu-id="5bf60-159">Em um cenário de produção, você deve confiar nos eventos de encaminhamento usando o Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bf60-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="5bf60-160">Navegue até seu cluster no **Gerenciador de Nuvem**, clique com o botão direito do mouse e escolha **Habilitar Transmissão de Rastreamentos**</span><span class="sxs-lookup"><span data-stu-id="5bf60-160">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Habilitar transmissão remota de rastreamentos][enablestreamingtraces]
   
    <span data-ttu-id="5bf60-162">Isso iniciará o processo de habilitar a extensão de rastreamentos de streaming em seus nós de cluster, bem como as configurações de rede necessárias.</span><span class="sxs-lookup"><span data-stu-id="5bf60-162">This will kick off the process of enabling the streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="5bf60-163">Expanda o elemento **Nós** no **Gerenciador de Nuvem**, clique com o botão direito do mouse no nó do qual deseja transmitir rastreamentos e escolha **Exibir Transmissão de Rastreamentos**</span><span class="sxs-lookup"><span data-stu-id="5bf60-163">Expand the **Nodes** element in **Cloud Explorer**, right-click the node you want to stream traces from and choose **View Streaming Traces**</span></span>
   
    ![Exibir transmissão remota de rastreamentos][viewremotestreamingtraces]
   
    <span data-ttu-id="5bf60-165">Repita a etapa 2 para o número de nós dos quais você quer ver os rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="5bf60-165">Repeat step 2 for as many nodes as you want to see traces from.</span></span> <span data-ttu-id="5bf60-166">Cada fluxo de nó será mostrado em uma janela dedicada.</span><span class="sxs-lookup"><span data-stu-id="5bf60-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="5bf60-167">Agora você poderá ver os rastreamentos emitidos pelo Service Fabric e seus serviços.</span><span class="sxs-lookup"><span data-stu-id="5bf60-167">You are now able to see the traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="5bf60-168">Se quiser filtrar os eventos para mostrar somente um aplicativo específico, basta digitar o nome do aplicativo no filtro.</span><span class="sxs-lookup"><span data-stu-id="5bf60-168">If you want to filter the events to only show a specific application, simply type in the name of the application in the filter.</span></span>
   
    ![Exibindo transmissão de rastreamentos][viewingstreamingtraces]
3. <span data-ttu-id="5bf60-170">Depois de terminar a transmissão de rastreamentos do seu cluster, é possível desabilitar a transmissão remota de rastreamentos clicando com o botão direito do mouse no cluster em **Gerenciador de Nuvem** e escolhendo **Desabilitar Rastreamentos de Streaming**</span><span class="sxs-lookup"><span data-stu-id="5bf60-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking the cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Desabilitar transmissão remota de rastreamentos][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="5bf60-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5bf60-172">Next steps</span></span>
* <span data-ttu-id="5bf60-173">[Testar um serviço da Malha do Serviço](service-fabric-testability-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5bf60-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="5bf60-174">[Gerenciar seu aplicativo do Service Fabric no Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="5bf60-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

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
