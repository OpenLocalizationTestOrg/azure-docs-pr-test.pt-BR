---
title: "Adicionar ou remover nós de um cluster autônomo do Service Fabric | Microsoft Docs"
description: "Saiba como adicionar ou remover nós de um cluster do Azure Service Fabric em um computador físico ou virtual executando o Windows Server, que pode ser local ou em qualquer nuvem."
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
ms.openlocfilehash: 9c6035e97de38ff63ef074109afd9f3c7484f828
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="add-or-remove-nodes-to-a-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="c0ba0-103">Adicionar ou remover nós de um cluster do Service Fabric autônomo em execução no Windows Server</span><span class="sxs-lookup"><span data-stu-id="c0ba0-103">Add or remove nodes to a standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="c0ba0-104">Depois de ter [criado seu cluster autônomo do Service Fabric em computadores com Windows Server](service-fabric-cluster-creation-for-windows-server.md), suas necessidades de negócios podem mudar e você talvez precise adicionar ou remover nós do seu cluster.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need to add or remove nodes to your cluster.</span></span> <span data-ttu-id="c0ba0-105">Este artigo fornece as etapas detalhadas para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-105">This article provides detailed steps to achieve this.</span></span> <span data-ttu-id="c0ba0-106">Observe que não há suporte para a funcionalidade de adicionar/remover nó em clusters de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-to-your-cluster"></a><span data-ttu-id="c0ba0-107">Adicionar nós ao cluster</span><span class="sxs-lookup"><span data-stu-id="c0ba0-107">Add nodes to your cluster</span></span>
1. <span data-ttu-id="c0ba0-108">Preparar a VM/computador que você deseja adicionar ao cluster, seguindo as etapas mencionadas na seção [Preparar as máquinas para atender aos pré-requisitos para implantação de cluster](service-fabric-cluster-creation-for-windows-server.md)</span><span class="sxs-lookup"><span data-stu-id="c0ba0-108">Prepare the VM/machine you want to add to your cluster by following the steps mentioned in the [Prepare the machines to meet the prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="c0ba0-109">Identifique a qual domínio de falha e domínio de atualização você vai adicionar essa VM/computador</span><span class="sxs-lookup"><span data-stu-id="c0ba0-109">Identify which fault domain and upgrade domain you are going to add this VM/machine to</span></span>
3. <span data-ttu-id="c0ba0-110">Área de rrabalho remota (RDP) na VM/computador que você deseja adicionar ao cluster</span><span class="sxs-lookup"><span data-stu-id="c0ba0-110">Remote desktop (RDP) into the VM/machine that you want to add to the cluster</span></span>
4. <span data-ttu-id="c0ba0-111">Copie ou [baixe o pacote autônomo do Service Fabric para Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) para esta VM/computador e descompacte o pacote</span><span class="sxs-lookup"><span data-stu-id="c0ba0-111">Copy or [download the standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) to the VM/machine and unzip the package</span></span>
5. <span data-ttu-id="c0ba0-112">Execute o Powershell com privilégios elevados e navegue até o local do pacote descompactado</span><span class="sxs-lookup"><span data-stu-id="c0ba0-112">Run Powershell with elevated privileges, and navigate to the location of the unzipped package</span></span>
6. <span data-ttu-id="c0ba0-113">Execute o script *AddNode.ps1* com os parâmetros que descrevem o novo nó a adicionar.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-113">Run the *AddNode.ps1* script with the parameters describing the new node to add.</span></span> <span data-ttu-id="c0ba0-114">O exemplo abaixo adiciona um novo nó chamado VM5, com o tipo NodeType0 e endereço IP 182.17.34.52 em UD1 e fd:/dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-114">The example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="c0ba0-115">O *ExistingClusterConnectionEndPoint* é um ponto de extremidade de conexão para um nó em um cluster existente, que pode ser o endereço IP de *qualquer* nó no cluster.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-115">The *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in the existing cluster, which can be the IP address of *any* node in the cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="c0ba0-116">Depois que o script terminar a execução, você pode verificar se o novo nó foi adicionado executando o cmdlet [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="c0ba0-116">Once the script finishes running, you can check if the new node has been added by running the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="c0ba0-117">Para garantir a consistência em diferentes nós do cluster, você deve iniciar uma atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-117">To ensure consistency across different nodes in the cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="c0ba0-118">Execute [ServiceFabricClusterConfiguration Get](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) para obter o arquivo de configuração mais recente e adicionar o nó recém-adicionado à seção "Nós".</span><span class="sxs-lookup"><span data-stu-id="c0ba0-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) to get the latest configuration file and add the newly added node to "Nodes" section.</span></span> <span data-ttu-id="c0ba0-119">Também é recomendável sempre ter a configuração de cluster mais recente disponível no caso de precisar reimplantar um cluster com a mesma configuração.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-119">It is also recommended to always have the latest cluster configuration available in the case that you need to redploy a cluster with the same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="c0ba0-120">Execute [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) para iniciar a atualização.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

    ```
    <span data-ttu-id="c0ba0-121">Você pode monitorar o andamento da atualização no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-121">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="c0ba0-122">Como alternativa, você pode executar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="c0ba0-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-to-clusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="c0ba0-123">Adicionar nós aos clusters configurados com a Segurança do Windows usando a gMSA</span><span class="sxs-lookup"><span data-stu-id="c0ba0-123">Add nodes to clusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="c0ba0-124">Para clusters configurados com a Conta de Serviço Gerenciado de Grupo (gMSA) (https://technet.microsoft.com/library/hh831782.aspx), um novo nó pode ser adicionado usando uma atualização de configuração:</span><span class="sxs-lookup"><span data-stu-id="c0ba0-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="c0ba0-125">Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) em qualquer um dos nós existentes para obter o arquivo de configuração mais recente e adicione os detalhes sobre o novo nó que você deseja adicionar na seção "Nós".</span><span class="sxs-lookup"><span data-stu-id="c0ba0-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of the existing nodes to get the latest configuration file and add details about the new node you want to add in the "Nodes" section.</span></span> <span data-ttu-id="c0ba0-126">Verifique se que o novo nó é parte da mesma conta gerenciada de grupo.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-126">Make sure the new node is part of the same group managed account.</span></span> <span data-ttu-id="c0ba0-127">Essa conta deve ser um Administrador em todos os computadores.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="c0ba0-128">Execute [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) para iniciar a atualização.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>
    ```
    <span data-ttu-id="c0ba0-129">Você pode monitorar o andamento da atualização no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-129">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="c0ba0-130">Como alternativa, você pode executar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="c0ba0-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-to-your-cluster"></a><span data-ttu-id="c0ba0-131">Adicionar tipos de nós ao cluster</span><span class="sxs-lookup"><span data-stu-id="c0ba0-131">Add node types to your cluster</span></span>
<span data-ttu-id="c0ba0-132">Para adicionar um novo tipo de nó, modifique a configuração para incluir o novo tipo de na seção "Tipos de Nós" em "Propriedades" e comece uma atualização de configuração usando [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="c0ba0-132">In order to add a new node type, modify your configuration to include the new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="c0ba0-133">Quando a atualização for concluída, você pode adicionar novos nós ao cluster com esse tipo de nó.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-133">Once the upgrade completes, you can add new nodes to your cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="c0ba0-134">Remover nós do cluster</span><span class="sxs-lookup"><span data-stu-id="c0ba0-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="c0ba0-135">Um nó pode ser removido de um cluster usando uma atualização de configuração, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c0ba0-135">A node can be removed from a cluster using a configuration upgrade, in the following manner:</span></span>

1. <span data-ttu-id="c0ba0-136">Execute [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) para obter o arquivo de configuração mais recente e *remover* o nó da seção "Nós".</span><span class="sxs-lookup"><span data-stu-id="c0ba0-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) to get the latest configuration file and *remove* the node from "Nodes" section.</span></span>
<span data-ttu-id="c0ba0-137">Adicione o parâmetro "NodesToBeRemoved" na seção "Configurar" dentro da seção "Configurações do Fabric".</span><span class="sxs-lookup"><span data-stu-id="c0ba0-137">Add the "NodesToBeRemoved" parameter to "Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="c0ba0-138">O "valor" deve ser uma lista separada por vírgulas de nomes de nó de nós que devem ser removidos.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-138">The "value" should be a comma separated list of node names of nodes that need to be removed.</span></span>

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
2. <span data-ttu-id="c0ba0-139">Execute [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) para iniciar a atualização.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

    ```
    <span data-ttu-id="c0ba0-140">Você pode monitorar o andamento da atualização no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-140">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="c0ba0-141">Como alternativa, você pode executar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="c0ba0-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="c0ba0-142">A remoção de nós pode iniciar várias atualizações.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="c0ba0-143">Alguns nós são marcados com a marca `IsSeedNode=”true”` e podem ser identificadas consultando o manifesto do cluster usando `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying the cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="c0ba0-144">A remoção desses nós pode levar mais tempo do que outros, pois os nós de propagação terão de ser movidos nesses cenários.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-144">Removal of such nodes may take longer than others since the seed nodes will have to be moved around in such scenarios.</span></span> <span data-ttu-id="c0ba0-145">O cluster deve manter um mínimo de 3 nós do tipo de nó primário.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-145">The cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="c0ba0-146">Remover tipos de nó do cluster</span><span class="sxs-lookup"><span data-stu-id="c0ba0-146">Remove node types from your cluster</span></span>
<span data-ttu-id="c0ba0-147">Antes de remover um tipo de nó, verifique novamente se há qualquer nó fazendo referência ao tipo de nó.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-147">Before removing a node type, please double check if there are any nodes referencing the node type.</span></span> <span data-ttu-id="c0ba0-148">Remova esses nós antes de remover o tipo de nó correspondente.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-148">Remove these nodes before removing the corresponding node type.</span></span> <span data-ttu-id="c0ba0-149">Depois que todos os nós correspondentes são removidos, você pode remover o Tipo de Nó da configuração do cluster e começar uma configuração de atualização usando [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="c0ba0-149">Once all corresponding nodes are removed, you can remove the NodeType from the cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="c0ba0-150">Substituir nós primários de seu cluster</span><span class="sxs-lookup"><span data-stu-id="c0ba0-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="c0ba0-151">A substituição de nós primários deve ser realizada um nó após o outro, em vez de remover e depois adicionar em lotes.</span><span class="sxs-lookup"><span data-stu-id="c0ba0-151">The replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c0ba0-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c0ba0-152">Next steps</span></span>
* [<span data-ttu-id="c0ba0-153">Definições de configuração para o cluster autônomo no Windows</span><span class="sxs-lookup"><span data-stu-id="c0ba0-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="c0ba0-154">Proteger um cluster autônomo no Windows usando os certificados X509</span><span class="sxs-lookup"><span data-stu-id="c0ba0-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="c0ba0-155">Criar um cluster do Service Fabric autônomo com VMs do Azure executando o Windows</span><span class="sxs-lookup"><span data-stu-id="c0ba0-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

