---
title: "aaaTroubleshoot sua instalação local do cluster do Service Fabric | Microsoft Docs"
description: "Este artigo aborda um conjunto de sugestões para a solução de problemas do cluster de desenvolvimento local"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="7870a-103">Solucionar problemas de configuração do cluster de desenvolvimento local</span><span class="sxs-lookup"><span data-stu-id="7870a-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="7870a-104">Se você encontrar um problema ao interagir com o cluster de desenvolvimento local do Azure Service Fabric, examine Olá sugestões para possíveis soluções a seguir.</span><span class="sxs-lookup"><span data-stu-id="7870a-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review hello following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="7870a-105">Falhas de configuração do cluster</span><span class="sxs-lookup"><span data-stu-id="7870a-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="7870a-106">Não é possível limpar os logs da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="7870a-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="7870a-107">Problema</span><span class="sxs-lookup"><span data-stu-id="7870a-107">Problem</span></span>
<span data-ttu-id="7870a-108">Ao executar o script de DevClusterSetup hello, você vir um erro como este:</span><span class="sxs-lookup"><span data-stu-id="7870a-108">While running hello DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="7870a-109">Solução</span><span class="sxs-lookup"><span data-stu-id="7870a-109">Solution</span></span>
<span data-ttu-id="7870a-110">Feche Olá janela atual do PowerShell e abra uma nova janela do PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="7870a-110">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="7870a-111">Agora você deve ser capaz de toosuccessfully executar script hello.</span><span class="sxs-lookup"><span data-stu-id="7870a-111">You should now be able toosuccessfully run hello script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="7870a-112">Falhas de conexão do cluster</span><span class="sxs-lookup"><span data-stu-id="7870a-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="7870a-113">Cmdlets do PowerShell do Service Fabric não são reconhecidos no Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7870a-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="7870a-114">Problema</span><span class="sxs-lookup"><span data-stu-id="7870a-114">Problem</span></span>
<span data-ttu-id="7870a-115">Se você tentar toorun qualquer Olá cmdlets do PowerShell de malha do serviço, como `Connect-ServiceFabricCluster` em uma janela do PowerShell do Azure, ele falhar, indicando que esse cmdlet Olá não é reconhecido.</span><span class="sxs-lookup"><span data-stu-id="7870a-115">If you try toorun any of hello Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that hello cmdlet is not recognized.</span></span> <span data-ttu-id="7870a-116">motivo Olá para isso é que PowerShell do Azure usa a versão de 32 bits de saudação do Windows PowerShell (mesmo em versões de sistema operacional de 64 bits), enquanto Olá cmdlets do Service Fabric só funcionam em ambientes de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="7870a-116">hello reason for this is that Azure PowerShell uses hello 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas hello Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="7870a-117">Solução</span><span class="sxs-lookup"><span data-stu-id="7870a-117">Solution</span></span>
<span data-ttu-id="7870a-118">Sempre execute os cmdlets do Service Fabric diretamente do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7870a-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="7870a-119">versão mais recente de saudação do PowerShell do Azure não cria um atalho especial, para que isso não deve ocorrer.</span><span class="sxs-lookup"><span data-stu-id="7870a-119">hello latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="7870a-120">Exceção de Inicialização de Tipo</span><span class="sxs-lookup"><span data-stu-id="7870a-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="7870a-121">Problema</span><span class="sxs-lookup"><span data-stu-id="7870a-121">Problem</span></span>
<span data-ttu-id="7870a-122">Quando você se conectar a cluster toohello no PowerShell, você verá o erro Olá TypeInitializationException para System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="7870a-122">When you are connecting toohello cluster in PowerShell, you see hello error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="7870a-123">Solução</span><span class="sxs-lookup"><span data-stu-id="7870a-123">Solution</span></span>
<span data-ttu-id="7870a-124">A variável do caminho não foi definida corretamente durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="7870a-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="7870a-125">Saia do Windows e entre novamente.</span><span class="sxs-lookup"><span data-stu-id="7870a-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="7870a-126">Isso atualiza o caminho.</span><span class="sxs-lookup"><span data-stu-id="7870a-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="7870a-127">Falha de conexão do cluster com “O objeto está fechado”</span><span class="sxs-lookup"><span data-stu-id="7870a-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="7870a-128">Problema</span><span class="sxs-lookup"><span data-stu-id="7870a-128">Problem</span></span>
<span data-ttu-id="7870a-129">Uma chamada tooConnect-ServiceFabricCluster falhará com um erro como este:</span><span class="sxs-lookup"><span data-stu-id="7870a-129">A call tooConnect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="7870a-130">Solução</span><span class="sxs-lookup"><span data-stu-id="7870a-130">Solution</span></span>
<span data-ttu-id="7870a-131">Feche Olá janela atual do PowerShell e abra uma nova janela do PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="7870a-131">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="7870a-132">Agora você deve ser capaz de conectar-se toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="7870a-132">You should now be able toosuccessfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="7870a-133">Exceção de Conexão ao Fabric Negada</span><span class="sxs-lookup"><span data-stu-id="7870a-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="7870a-134">Problema</span><span class="sxs-lookup"><span data-stu-id="7870a-134">Problem</span></span>
<span data-ttu-id="7870a-135">Ao depurar no Visual Studio, você obtém um erro FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="7870a-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="7870a-136">Solução</span><span class="sxs-lookup"><span data-stu-id="7870a-136">Solution</span></span>
<span data-ttu-id="7870a-137">Esse erro normalmente ocorre quando você tentar toostart um processo de host de serviço manualmente, em vez de permitir toostart de tempo de execução do Service Fabric Olá para você.</span><span class="sxs-lookup"><span data-stu-id="7870a-137">This error usually occurs when you try toostart a service host process manually, rather than allowing hello Service Fabric runtime toostart it for you.</span></span>

<span data-ttu-id="7870a-138">Verifique se você não possui um projeto de serviço definido como projeto de inicialização na sua solução.</span><span class="sxs-lookup"><span data-stu-id="7870a-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="7870a-139">Somente projetos de aplicativo da Malha do Serviço devem ser definidos como projetos de inicialização.</span><span class="sxs-lookup"><span data-stu-id="7870a-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="7870a-140">Se, após a instalação, o cluster local começa toobehave anormal, você poderá redefini-lo usando o aplicativo de bandeja de sistema do hello cluster local manager.</span><span class="sxs-lookup"><span data-stu-id="7870a-140">If, following setup, your local cluster begins toobehave abnormally, you can reset it using hello local cluster manager system tray application.</span></span> <span data-ttu-id="7870a-141">Isso remove Olá cluster existente e configure um novo.</span><span class="sxs-lookup"><span data-stu-id="7870a-141">This removes hello existing cluster and set up a new one.</span></span> <span data-ttu-id="7870a-142">Observe que todos os aplicativos implantados e os dados associados são removidos.</span><span class="sxs-lookup"><span data-stu-id="7870a-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7870a-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7870a-143">Next steps</span></span>
* [<span data-ttu-id="7870a-144">Entender e solucionar problemas de cluster com relatórios de integridade do sistema</span><span class="sxs-lookup"><span data-stu-id="7870a-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="7870a-145">Visualizando o cluster com o Explorador do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7870a-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

