---
title: "aaaAdd ou remover nós tooa autônomo serviço cluster do Fabric | Microsoft Docs"
description: "Saiba como tooadd ou remover nós tooan Azure Service Fabric do cluster em um computador físico ou virtual executando o Windows Server, que pode ser local ou em qualquer nuvem."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="bb01a-103">Adicionar ou remover nós tooa autônomo do Service Fabric cluster em execução no Windows Server</span><span class="sxs-lookup"><span data-stu-id="bb01a-103">Add or remove nodes tooa standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="bb01a-104">Depois de ter [criado o cluster do Service Fabric independentes em máquinas do Windows Server](service-fabric-cluster-creation-for-windows-server.md), suas necessidades de negócios podem ser alterados e, talvez você precise tooadd ou remover nós tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="bb01a-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need tooadd or remove nodes tooyour cluster.</span></span> <span data-ttu-id="bb01a-105">Este artigo fornece etapas detalhadas tooachieve isso.</span><span class="sxs-lookup"><span data-stu-id="bb01a-105">This article provides detailed steps tooachieve this.</span></span> <span data-ttu-id="bb01a-106">Observe que não há suporte para a funcionalidade de adicionar/remover nó em clusters de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="bb01a-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-tooyour-cluster"></a><span data-ttu-id="bb01a-107">Adicionar nós tooyour cluster</span><span class="sxs-lookup"><span data-stu-id="bb01a-107">Add nodes tooyour cluster</span></span>
1. <span data-ttu-id="bb01a-108">Preparar Olá VM/máquina que deseja tooadd tooyour cluster seguindo as etapas Olá mencionadas Olá [Olá preparar máquinas pré-requisitos do toomeet Olá para implantação de cluster](service-fabric-cluster-creation-for-windows-server.md) seção</span><span class="sxs-lookup"><span data-stu-id="bb01a-108">Prepare hello VM/machine you want tooadd tooyour cluster by following hello steps mentioned in hello [Prepare hello machines toomeet hello prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="bb01a-109">Identificar qual domínio de falha e o domínio de atualização que você está indo tooadd dessa VM/máquina para</span><span class="sxs-lookup"><span data-stu-id="bb01a-109">Identify which fault domain and upgrade domain you are going tooadd this VM/machine to</span></span>
3. <span data-ttu-id="bb01a-110">Área de trabalho remota (RDP) Olá VM/máquina que você deseja que o cluster de toohello tooadd</span><span class="sxs-lookup"><span data-stu-id="bb01a-110">Remote desktop (RDP) into hello VM/machine that you want tooadd toohello cluster</span></span>
4. <span data-ttu-id="bb01a-111">Copiar ou [baixar pacote autônomo de saudação de malha do serviço para o Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/máquina e descompacte o pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="bb01a-111">Copy or [download hello standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine and unzip hello package</span></span>
5. <span data-ttu-id="bb01a-112">Execute o Powershell com privilégios elevados e navegue toohello local do pacote de saudação descompactado</span><span class="sxs-lookup"><span data-stu-id="bb01a-112">Run Powershell with elevated privileges, and navigate toohello location of hello unzipped package</span></span>
6. <span data-ttu-id="bb01a-113">Executar Olá *AddNode.ps1* script com os parâmetros de saudação descrevendo Olá novo nó tooadd.</span><span class="sxs-lookup"><span data-stu-id="bb01a-113">Run hello *AddNode.ps1* script with hello parameters describing hello new node tooadd.</span></span> <span data-ttu-id="bb01a-114">Olá exemplo a seguir adiciona um novo nó denominado VM5, com tipo NodeType0 e endereço IP 182.17.34.52, UD1 e fd: / dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="bb01a-114">hello example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="bb01a-115">Olá *ExistingClusterConnectionEndPoint* já está um ponto de extremidade de conexão para um nó no cluster existente do hello, que pode ser um endereço IP de saudação do *qualquer* nó no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bb01a-115">hello *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in hello existing cluster, which can be hello IP address of *any* node in hello cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="bb01a-116">Depois que o script hello concluir a execução, você pode verificar se o novo nó de saudação foi adicionado executando Olá [ServiceFabricNode Get](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bb01a-116">Once hello script finishes running, you can check if hello new node has been added by running hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="bb01a-117">consistência de tooensure em diferentes nós de cluster hello, você deve iniciar uma atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="bb01a-117">tooensure consistency across different nodes in hello cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="bb01a-118">Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget Olá último arquivo de configuração e adicione Olá recém-adicionado nó muito seção "Nós".</span><span class="sxs-lookup"><span data-stu-id="bb01a-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and add hello newly added node too"Nodes" section.</span></span> <span data-ttu-id="bb01a-119">Também é recomendável tooalways ter Olá última configuração de cluster disponível no caso de Olá que você precisa tooredploy um cluster com hello mesma configuração.</span><span class="sxs-lookup"><span data-stu-id="bb01a-119">It is also recommended tooalways have hello latest cluster configuration available in hello case that you need tooredploy a cluster with hello same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="bb01a-120">Executar [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb01a-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="bb01a-121">Você pode monitorar o progresso de saudação da atualização Olá no Gerenciador do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bb01a-121">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="bb01a-122">Como alternativa, você pode executar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="bb01a-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="bb01a-123">Adicionar nós tooclusters configurado com a segurança do Windows usando a gMSA</span><span class="sxs-lookup"><span data-stu-id="bb01a-123">Add nodes tooclusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="bb01a-124">Para clusters configurados com a Conta de Serviço Gerenciado de Grupo (gMSA) (https://technet.microsoft.com/library/hh831782.aspx), um novo nó pode ser adicionado usando uma atualização de configuração:</span><span class="sxs-lookup"><span data-stu-id="bb01a-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="bb01a-125">Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) em qualquer um de nós existentes Olá tooget Olá último arquivo de configuração e adicionar detalhes sobre o novo nó de saudação você deseja tooadd na seção de nós"Olá".</span><span class="sxs-lookup"><span data-stu-id="bb01a-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of hello existing nodes tooget hello latest configuration file and add details about hello new node you want tooadd in hello "Nodes" section.</span></span> <span data-ttu-id="bb01a-126">Verifique se o nó novo Olá faz parte da saudação mesma conta gerenciada de grupo.</span><span class="sxs-lookup"><span data-stu-id="bb01a-126">Make sure hello new node is part of hello same group managed account.</span></span> <span data-ttu-id="bb01a-127">Essa conta deve ser um Administrador em todos os computadores.</span><span class="sxs-lookup"><span data-stu-id="bb01a-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="bb01a-128">Executar [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb01a-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    <span data-ttu-id="bb01a-129">Você pode monitorar o progresso de saudação da atualização Olá no Gerenciador do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bb01a-129">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="bb01a-130">Como alternativa, você pode executar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="bb01a-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-tooyour-cluster"></a><span data-ttu-id="bb01a-131">Adicionar nó tipos tooyour cluster</span><span class="sxs-lookup"><span data-stu-id="bb01a-131">Add node types tooyour cluster</span></span>
<span data-ttu-id="bb01a-132">Ordenar tooadd um novo tipo de nó, modificar sua configuração tooinclude Olá novo tipo de nó na seção de "NodeTypes" em "Propriedades" e começar a uma configuração de atualização usando [ServiceFabricClusterConfigurationUpgrade início](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="bb01a-132">In order tooadd a new node type, modify your configuration tooinclude hello new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="bb01a-133">Depois de concluir a atualização Olá, você pode adicionar o novo cluster tooyour de nós com esse tipo de nó.</span><span class="sxs-lookup"><span data-stu-id="bb01a-133">Once hello upgrade completes, you can add new nodes tooyour cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="bb01a-134">Remover nós do cluster</span><span class="sxs-lookup"><span data-stu-id="bb01a-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="bb01a-135">Um nó pode ser removido de um cluster usando uma atualização de configuração, no hello maneira a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb01a-135">A node can be removed from a cluster using a configuration upgrade, in hello following manner:</span></span>

1. <span data-ttu-id="bb01a-136">Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) arquivo de configuração mais recente do tooget hello e *remover* nó Olá da seção "Nós".</span><span class="sxs-lookup"><span data-stu-id="bb01a-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and *remove* hello node from "Nodes" section.</span></span>
<span data-ttu-id="bb01a-137">Adicionar hello "NodesToBeRemoved" parâmetro muito "configurar" seção na seção "FabricSettings".</span><span class="sxs-lookup"><span data-stu-id="bb01a-137">Add hello "NodesToBeRemoved" parameter too"Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="bb01a-138">Olá "valor" deve ser uma lista separada por vírgulas de nomes de nó de nós que precisam toobe removido.</span><span class="sxs-lookup"><span data-stu-id="bb01a-138">hello "value" should be a comma separated list of node names of nodes that need toobe removed.</span></span>

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. <span data-ttu-id="bb01a-139">Executar [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb01a-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="bb01a-140">Você pode monitorar o progresso de saudação da atualização Olá no Gerenciador do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bb01a-140">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="bb01a-141">Como alternativa, você pode executar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="bb01a-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="bb01a-142">A remoção de nós pode iniciar várias atualizações.</span><span class="sxs-lookup"><span data-stu-id="bb01a-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="bb01a-143">Alguns nós são marcados com `IsSeedNode=”true”` marca e podem ser identificados consultando cluster Olá manifesto usando `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="bb01a-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying hello cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="bb01a-144">Remoção de tais nós pode levar mais tempo do que outros, como nós de propagação Olá terá toobe movido nesses cenários.</span><span class="sxs-lookup"><span data-stu-id="bb01a-144">Removal of such nodes may take longer than others since hello seed nodes will have toobe moved around in such scenarios.</span></span> <span data-ttu-id="bb01a-145">cluster Olá deve manter um mínimo de 3 nós de tipo de nó primário.</span><span class="sxs-lookup"><span data-stu-id="bb01a-145">hello cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="bb01a-146">Remover tipos de nó do cluster</span><span class="sxs-lookup"><span data-stu-id="bb01a-146">Remove node types from your cluster</span></span>
<span data-ttu-id="bb01a-147">Antes de remover um tipo de nó, verifique se há quaisquer nós fazendo referência ao tipo de nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb01a-147">Before removing a node type, please double check if there are any nodes referencing hello node type.</span></span> <span data-ttu-id="bb01a-148">Remova esses nós antes de remover o tipo de nó correspondente hello.</span><span class="sxs-lookup"><span data-stu-id="bb01a-148">Remove these nodes before removing hello corresponding node type.</span></span> <span data-ttu-id="bb01a-149">Depois que todos os nós correspondentes são removidos, você pode remover o Olá NodeType de configuração de cluster de saudação e começar a uma configuração de atualização usando [ServiceFabricClusterConfigurationUpgrade início](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="bb01a-149">Once all corresponding nodes are removed, you can remove hello NodeType from hello cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="bb01a-150">Substituir nós primários de seu cluster</span><span class="sxs-lookup"><span data-stu-id="bb01a-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="bb01a-151">substituição de saudação de nós primários deve ser executada de um nó após o outro, em vez de remover e, em seguida, adicionar em lotes.</span><span class="sxs-lookup"><span data-stu-id="bb01a-151">hello replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bb01a-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb01a-152">Next steps</span></span>
* [<span data-ttu-id="bb01a-153">Definições de configuração para o cluster autônomo no Windows</span><span class="sxs-lookup"><span data-stu-id="bb01a-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="bb01a-154">Proteger um cluster autônomo no Windows usando os certificados X509</span><span class="sxs-lookup"><span data-stu-id="bb01a-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="bb01a-155">Criar um cluster do Service Fabric autônomo com VMs do Azure executando o Windows</span><span class="sxs-lookup"><span data-stu-id="bb01a-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

