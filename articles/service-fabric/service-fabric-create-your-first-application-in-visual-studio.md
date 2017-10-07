---
title: "aaaCreate um serviço confiável do Azure Service Fabric com c#"
description: Crie, implante e depure um aplicativo Reliable Service baseado no Azure Service Fabric com o Visual Studio.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="050eb-103">Criar seu primeiro aplicativo Reliable Services com estado do Service Fabric em C#</span><span class="sxs-lookup"><span data-stu-id="050eb-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="050eb-104">Saiba como toodeploy seu primeiro aplicativo do Service Fabric para .NET no Windows em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="050eb-104">Learn how toodeploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="050eb-105">Quando você terminar, terá um cluster local com um aplicativo de serviço confiável.</span><span class="sxs-lookup"><span data-stu-id="050eb-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="050eb-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="050eb-106">Prerequisites</span></span>

<span data-ttu-id="050eb-107">Antes de começar, verifique se você [configurou o ambiente de desenvolvimento](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="050eb-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="050eb-108">Isso inclui a instalação Olá SDK do Service Fabric e 2017 do Visual Studio ou 2015.</span><span class="sxs-lookup"><span data-stu-id="050eb-108">This includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="050eb-109">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="050eb-109">Create hello application</span></span>

<span data-ttu-id="050eb-110">Inicie o Visual Studio como um **administrador**.</span><span class="sxs-lookup"><span data-stu-id="050eb-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="050eb-111">Criar um projeto com `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="050eb-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="050eb-112">Em Olá **novo projeto** caixa de diálogo, escolha **nuvem > aplicativo de malha do serviço**.</span><span class="sxs-lookup"><span data-stu-id="050eb-112">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="050eb-113">Nome do aplicativo hello **MyApplication** e pressione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="050eb-113">Name hello application **MyApplication** and press **OK**.</span></span>

   
![Caixa de diálogo Novo projeto no Visual Studio][1]

<span data-ttu-id="050eb-115">Você pode criar qualquer tipo de aplicativo de malha do serviço na próxima caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="050eb-115">You can create any type of Service Fabric application from hello next dialog.</span></span> <span data-ttu-id="050eb-116">Para este guia de início rápido, escolha **Serviço com Estado**.</span><span class="sxs-lookup"><span data-stu-id="050eb-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="050eb-117">Nome do serviço de saudação **MyStatefulService** e pressione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="050eb-117">Name hello service **MyStatefulService** and press **OK**.</span></span>

![Caixa de diálogo Novo serviço no Visual Studio][2]


<span data-ttu-id="050eb-119">Visual Studio cria o projeto de aplicativo hello e projeto de serviço com monitoração de estado hello e exibe-os no Gerenciador de soluções.</span><span class="sxs-lookup"><span data-stu-id="050eb-119">Visual Studio creates hello application project and hello stateful service project and displays them in Solution Explorer.</span></span>

![Gerenciador de Soluções seguindo a criação de aplicativo com serviço com estado][3]

<span data-ttu-id="050eb-121">projeto de aplicativo Hello (**MyApplication**) não contém qualquer código diretamente.</span><span class="sxs-lookup"><span data-stu-id="050eb-121">hello application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="050eb-122">Em vez disso, ele faz referência a um conjunto de projetos de serviço.</span><span class="sxs-lookup"><span data-stu-id="050eb-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="050eb-123">Além disso, ele contém três outros tipos de conteúdo:</span><span class="sxs-lookup"><span data-stu-id="050eb-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="050eb-124">**Perfis de publicação**</span><span class="sxs-lookup"><span data-stu-id="050eb-124">**Publish profiles**</span></span>  
<span data-ttu-id="050eb-125">Perfis para a implantação de ambientes de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="050eb-125">Profiles for deploying toodifferent environments.</span></span>

* <span data-ttu-id="050eb-126">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="050eb-126">**Scripts**</span></span>  
<span data-ttu-id="050eb-127">Script do PowerShell para a implantação/atualização de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="050eb-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="050eb-128">**Definição de aplicativo**</span><span class="sxs-lookup"><span data-stu-id="050eb-128">**Application definition**</span></span>  
<span data-ttu-id="050eb-129">Inclui o arquivo applicationmanifest. XML de saudação em *ApplicationPackageRoot* que descreve a composição do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="050eb-129">Includes hello ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="050eb-130">Arquivos de parâmetro de aplicativo associados estão sob *ApplicationParameters*, que pode ser usado toospecify parâmetros específicos do ambiente.</span><span class="sxs-lookup"><span data-stu-id="050eb-130">Associated application parameter files are under *ApplicationParameters*, which can be used toospecify environment-specific parameters.</span></span> <span data-ttu-id="050eb-131">Perfil de publicação do Visual seleciona Studio associado de um arquivo de parâmetro de aplicativo que é especificado no hello durante o ambiente específico de tooa de implantação.</span><span class="sxs-lookup"><span data-stu-id="050eb-131">Visual Studio selects an application parameter file that's specified in hello associated publish profile during deployment tooa specific environment.</span></span>
    
<span data-ttu-id="050eb-132">Para obter uma visão geral do conteúdo de saudação do projeto de serviço hello, consulte [Introdução aos serviços confiável](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="050eb-132">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-hello-application"></a><span data-ttu-id="050eb-133">Implantar e depurar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="050eb-133">Deploy and debug hello application</span></span>

<span data-ttu-id="050eb-134">Agora que você tem um aplicativo, execute-o.</span><span class="sxs-lookup"><span data-stu-id="050eb-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="050eb-135">No Visual Studio, pressione `F5` toodeploy aplicativo de saudação para depuração.</span><span class="sxs-lookup"><span data-stu-id="050eb-135">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="050eb-136">Olá a primeira vez que você executar e implanta o aplicativo hello localmente, o Visual Studio cria um cluster local para depuração.</span><span class="sxs-lookup"><span data-stu-id="050eb-136">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="050eb-137">Isso pode levar algum tempo.</span><span class="sxs-lookup"><span data-stu-id="050eb-137">This may take some time.</span></span> <span data-ttu-id="050eb-138">status de criação de cluster Olá é exibido na janela de saída do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="050eb-138">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="050eb-139">Quando o cluster Olá estiver pronto, você obtém uma notificação de aplicativo hello cluster local system bandeja manager acompanha Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="050eb-139">When hello cluster is ready, you get a notification from hello local cluster system tray manager application included with hello SDK.</span></span>
   
![Notificação de bandeja do sistema de cluster local][4]

<span data-ttu-id="050eb-141">Uma vez iniciado do aplicativo hello, Visual Studio fornece automaticamente Olá **Visualizador de eventos de diagnóstico**, onde você pode ver a saída de rastreamento de seus serviços.</span><span class="sxs-lookup"><span data-stu-id="050eb-141">Once hello application starts, Visual Studio automatically brings up hello **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Visualizador de eventos de diagnóstico][5]

<span data-ttu-id="050eb-143">Olá modelo de serviço com monitoração de estado que usamos simplesmente mostra um incremento de valor de contador em Olá `RunAsync` método **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="050eb-143">hello stateful service template we used simply shows a counter value incrementing in hello `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="050eb-144">Expanda uma saudação eventos toosee obter mais detalhes, incluindo Olá nó onde o código hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="050eb-144">Expand one of hello events toosee more details, including hello node where hello code is running.</span></span> <span data-ttu-id="050eb-145">Nesse caso, é o \_Node\_2, que pode ser diferente em seu computador.</span><span class="sxs-lookup"><span data-stu-id="050eb-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Detalhe do visualizador de eventos de diagnóstico][6]

<span data-ttu-id="050eb-147">o cluster local Olá contém cinco nós hospedado em um único computador.</span><span class="sxs-lookup"><span data-stu-id="050eb-147">hello local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="050eb-148">Em um ambiente de produção, cada nó está hospedado em uma máquina virtual ou física distinta.</span><span class="sxs-lookup"><span data-stu-id="050eb-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="050eb-149">depurador de perda de saudação toosimulate de uma máquina ao exercer Olá Visual Studio em hello mesmo tempo, vamos dar um de nós de saudação no cluster local hello.</span><span class="sxs-lookup"><span data-stu-id="050eb-149">toosimulate hello loss of a machine while exercising hello Visual Studio debugger at hello same time, let's take down one of hello nodes on hello local cluster.</span></span>

<span data-ttu-id="050eb-150">Em Olá **Solution Explorer** janela, abra **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="050eb-150">In hello **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="050eb-151">Localize Olá `RunAsync` método e defina um ponto de interrupção na primeira linha de saudação do método hello.</span><span class="sxs-lookup"><span data-stu-id="050eb-151">Find hello `RunAsync` method and set a breakpoint on hello first line of hello method.</span></span>

![Ponto de interrupção no método RunAsync de serviço com estado][7]

<span data-ttu-id="050eb-153">Iniciar Olá **Service Fabric Explorer** ferramenta clicando em Olá **Gerenciador de Cluster Local** aplicativo de bandeja do sistema e escolha **gerenciar o Cluster Local**.</span><span class="sxs-lookup"><span data-stu-id="050eb-153">Launch hello **Service Fabric Explorer** tool by right-clicking on hello **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Inicie o Gerenciador do Service Fabric Olá Gerenciador de Cluster Local][systray-launch-sfx]

<span data-ttu-id="050eb-155">O [**Service Fabric Explorer** ](service-fabric-visualizing-your-cluster.md) oferece uma representação visual de um cluster.</span><span class="sxs-lookup"><span data-stu-id="050eb-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="050eb-156">Ele inclui o conjunto de saudação de tooit aplicativos implantados e conjunto Olá nós físicos que compõem-lo.</span><span class="sxs-lookup"><span data-stu-id="050eb-156">It includes hello set of applications deployed tooit and hello set of physical nodes that make it up.</span></span>

<span data-ttu-id="050eb-157">No painel esquerdo do hello, expanda **Cluster > nós** e localizar Olá nó onde seu código está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="050eb-157">In hello left pane, expand **Cluster > Nodes** and find hello node where your code is running.</span></span>

<span data-ttu-id="050eb-158">Clique em **ações > desativar (reinicialização)** toosimulate uma reinicialização do computador.</span><span class="sxs-lookup"><span data-stu-id="050eb-158">Click **Actions > Deactivate (Restart)** toosimulate a machine restarting.</span></span>

![Parar um nó no Service Fabric Explorer][sfx-stop-node]

<span data-ttu-id="050eb-160">Temporariamente, você deve ver o ponto de interrupção que você estava fazendo diretamente em um nó de computação de saudação failover tooanother de ocorrências no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="050eb-160">Momentarily, you should see your breakpoint hit in Visual Studio as hello computation you were doing on one node seamlessly fails over tooanother.</span></span>


<span data-ttu-id="050eb-161">Em seguida, retornar toohello Visualizador de eventos de diagnóstico e observar as mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="050eb-161">Next, return toohello Diagnostic Events Viewer and observe hello messages.</span></span> <span data-ttu-id="050eb-162">contador de saudação continua aumentando, mesmo que eventos de saudação realmente são provenientes de um nó diferente.</span><span class="sxs-lookup"><span data-stu-id="050eb-162">hello counter has continued incrementing, even though hello events are actually coming from a different node.</span></span>

![Visualizador de eventos de diagnóstico após o failover][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a><span data-ttu-id="050eb-164">Limpando o cluster local da saudação (opcional)</span><span class="sxs-lookup"><span data-stu-id="050eb-164">Cleaning up hello local cluster (optional)</span></span>

<span data-ttu-id="050eb-165">Lembre-se de que esse cluster local é real.</span><span class="sxs-lookup"><span data-stu-id="050eb-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="050eb-166">Parar o depurador Olá remove a instância do aplicativo e cancela o registro de tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="050eb-166">Stopping hello debugger removes your application instance and unregisters hello application type.</span></span> <span data-ttu-id="050eb-167">No entanto, o cluster de saudação continua toorun no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="050eb-167">However, hello cluster continues toorun in hello background.</span></span> <span data-ttu-id="050eb-168">Quando você estiver cluster local do toostop pronto hello, há duas opções.</span><span class="sxs-lookup"><span data-stu-id="050eb-168">When you're ready toostop hello local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="050eb-169">Manter os dados de aplicativo e rastreamento</span><span class="sxs-lookup"><span data-stu-id="050eb-169">Keep application and trace data</span></span>

<span data-ttu-id="050eb-170">Desligue o cluster de saudação clicando em Olá **Gerenciador de Cluster Local** aplicativo de bandeja do sistema e, em seguida, escolha **parar Cluster Local**.</span><span class="sxs-lookup"><span data-stu-id="050eb-170">Shut down hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-hello-cluster-and-all-data"></a><span data-ttu-id="050eb-171">Excluir o cluster hello e todos os dados</span><span class="sxs-lookup"><span data-stu-id="050eb-171">Delete hello cluster and all data</span></span>

<span data-ttu-id="050eb-172">Remover cluster Olá clicando em Olá **Gerenciador de Cluster Local** aplicativo de bandeja do sistema e, em seguida, escolha **remover Cluster Local**.</span><span class="sxs-lookup"><span data-stu-id="050eb-172">Remove hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="050eb-173">Se você escolher essa opção, o Visual Studio será reimplantar Olá Olá de cluster próxima vez Olá a execução do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="050eb-173">If you choose this option, Visual Studio will redeploy hello cluster hello next time your run hello application.</span></span> <span data-ttu-id="050eb-174">Escolha esta opção se você não pretende cluster local do toouse Olá por algum tempo ou se você precisar de recursos de tooreclaim.</span><span class="sxs-lookup"><span data-stu-id="050eb-174">Choose this option if you don't intend toouse hello local cluster for some time or if you need tooreclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="050eb-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="050eb-175">Next steps</span></span>
<span data-ttu-id="050eb-176">Leia mais sobre [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="050eb-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
