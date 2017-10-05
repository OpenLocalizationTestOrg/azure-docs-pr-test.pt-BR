---
title: "Solucionar problemas de sua configuração de cluster do Service Fabric local | Microsoft Docs"
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
ms.openlocfilehash: aa393f884b564cee81fcf75cc2eff895efea9471
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="375f0-103">Solucionar problemas de configuração do cluster de desenvolvimento local</span><span class="sxs-lookup"><span data-stu-id="375f0-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="375f0-104">Se você tiver um problema ao interagir com o cluster de desenvolvimento local do Service Fabric do Azure, examine as sugestões a seguir para ver as possíveis soluções.</span><span class="sxs-lookup"><span data-stu-id="375f0-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="375f0-105">Falhas de configuração do cluster</span><span class="sxs-lookup"><span data-stu-id="375f0-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="375f0-106">Não é possível limpar os logs da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="375f0-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="375f0-107">Problema</span><span class="sxs-lookup"><span data-stu-id="375f0-107">Problem</span></span>
<span data-ttu-id="375f0-108">Ao executar o script DevClusterSetup, você vê um erro como este:</span><span class="sxs-lookup"><span data-stu-id="375f0-108">While running the DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="375f0-109">Solução</span><span class="sxs-lookup"><span data-stu-id="375f0-109">Solution</span></span>
<span data-ttu-id="375f0-110">Feche a janela atual do PowerShell e inicie uma nova janela como um administrador.</span><span class="sxs-lookup"><span data-stu-id="375f0-110">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="375f0-111">Agora você pode executar o script com êxito.</span><span class="sxs-lookup"><span data-stu-id="375f0-111">You should now be able to successfully run the script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="375f0-112">Falhas de conexão do cluster</span><span class="sxs-lookup"><span data-stu-id="375f0-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="375f0-113">Cmdlets do PowerShell do Service Fabric não são reconhecidos no Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="375f0-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="375f0-114">Problema</span><span class="sxs-lookup"><span data-stu-id="375f0-114">Problem</span></span>
<span data-ttu-id="375f0-115">Se você tentar executar qualquer um dos cmdlets do PowerShell do Service Fabric, como `Connect-ServiceFabricCluster` em uma janela do Azure PowerShell, ele falhará, dizendo que o cmdlet não é reconhecido.</span><span class="sxs-lookup"><span data-stu-id="375f0-115">If you try to run any of the Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that the cmdlet is not recognized.</span></span> <span data-ttu-id="375f0-116">A razão para isso é que o Azure PowerShell usa a versão de 32 bits do Windows PowerShell (mesmo em versões de sistema operacional de 64 bits), enquanto os cmdlets do Service Fabric só funcionam em ambientes de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="375f0-116">The reason for this is that Azure PowerShell uses the 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas the Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="375f0-117">Solução</span><span class="sxs-lookup"><span data-stu-id="375f0-117">Solution</span></span>
<span data-ttu-id="375f0-118">Sempre execute os cmdlets do Service Fabric diretamente do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="375f0-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="375f0-119">A versão mais recente do Azure PowerShell não cria um atalho especial, então isso não deverá mais ocorrer.</span><span class="sxs-lookup"><span data-stu-id="375f0-119">The latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="375f0-120">Exceção de Inicialização de Tipo</span><span class="sxs-lookup"><span data-stu-id="375f0-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="375f0-121">Problema</span><span class="sxs-lookup"><span data-stu-id="375f0-121">Problem</span></span>
<span data-ttu-id="375f0-122">Ao conectar-se com o cluster no PowerShell, você vê o erro TypeInitializationException para System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="375f0-122">When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="375f0-123">Solução</span><span class="sxs-lookup"><span data-stu-id="375f0-123">Solution</span></span>
<span data-ttu-id="375f0-124">A variável do caminho não foi definida corretamente durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="375f0-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="375f0-125">Saia do Windows e entre novamente.</span><span class="sxs-lookup"><span data-stu-id="375f0-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="375f0-126">Isso atualiza o caminho.</span><span class="sxs-lookup"><span data-stu-id="375f0-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="375f0-127">Falha de conexão do cluster com “O objeto está fechado”</span><span class="sxs-lookup"><span data-stu-id="375f0-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="375f0-128">Problema</span><span class="sxs-lookup"><span data-stu-id="375f0-128">Problem</span></span>
<span data-ttu-id="375f0-129">Uma chamada para Connect-ServiceFabricCluster falha com um erro parecido com este:</span><span class="sxs-lookup"><span data-stu-id="375f0-129">A call to Connect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : The object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="375f0-130">Solução</span><span class="sxs-lookup"><span data-stu-id="375f0-130">Solution</span></span>
<span data-ttu-id="375f0-131">Feche a janela atual do PowerShell e inicie uma nova janela como um administrador.</span><span class="sxs-lookup"><span data-stu-id="375f0-131">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="375f0-132">Agora você pode se conectar com êxito.</span><span class="sxs-lookup"><span data-stu-id="375f0-132">You should now be able to successfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="375f0-133">Exceção de Conexão ao Fabric Negada</span><span class="sxs-lookup"><span data-stu-id="375f0-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="375f0-134">Problema</span><span class="sxs-lookup"><span data-stu-id="375f0-134">Problem</span></span>
<span data-ttu-id="375f0-135">Ao depurar no Visual Studio, você obtém um erro FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="375f0-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="375f0-136">Solução</span><span class="sxs-lookup"><span data-stu-id="375f0-136">Solution</span></span>
<span data-ttu-id="375f0-137">Geralmente, esse erro ocorre quando você tenta iniciar um processo de host de serviço manualmente, em vez de permitir que o tempo de execução do Service Fabric inicie-o para você.</span><span class="sxs-lookup"><span data-stu-id="375f0-137">This error usually occurs when you try to start a service host process manually, rather than allowing the Service Fabric runtime to start it for you.</span></span>

<span data-ttu-id="375f0-138">Verifique se você não possui um projeto de serviço definido como projeto de inicialização na sua solução.</span><span class="sxs-lookup"><span data-stu-id="375f0-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="375f0-139">Somente projetos de aplicativo da Malha do Serviço devem ser definidos como projetos de inicialização.</span><span class="sxs-lookup"><span data-stu-id="375f0-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="375f0-140">Se, após a instalação, o cluster local começar a se comportar de forma anormal, você poderá redefini-lo usando o aplicativo de bandeja de sistema de gerenciador de cluster local.</span><span class="sxs-lookup"><span data-stu-id="375f0-140">If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application.</span></span> <span data-ttu-id="375f0-141">Isso remove o cluster existente e configura um novo.</span><span class="sxs-lookup"><span data-stu-id="375f0-141">This removes the existing cluster and set up a new one.</span></span> <span data-ttu-id="375f0-142">Observe que todos os aplicativos implantados e os dados associados são removidos.</span><span class="sxs-lookup"><span data-stu-id="375f0-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="375f0-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="375f0-143">Next steps</span></span>
* [<span data-ttu-id="375f0-144">Entender e solucionar problemas de cluster com relatórios de integridade do sistema</span><span class="sxs-lookup"><span data-stu-id="375f0-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="375f0-145">Visualizando o cluster com o Explorador do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="375f0-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

