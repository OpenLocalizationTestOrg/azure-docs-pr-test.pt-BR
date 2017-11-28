---
title: "Tipos de nós do Service Fabric e Conjuntos de Dimensionamento de VMs | Microsoft Docs"
description: "Descreve como os tipos de nó do Service Fabric se relacionam com os conjuntos de escala da VM e como fazer a conexão remota com uma instância de conjunto de escala da VM ou um nó de cluster."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 3b1a22bb3653abb68fc73645ad2cb623fabc7736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="the-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="2fb52-103">A relação entre os tipos de nó do Service Fabric e os conjuntos de escala da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2fb52-103">The relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="2fb52-104">Os conjuntos de dimensionamento de máquina virtual são um recurso de Computação do Azure que você pode usar para implantar e gerenciar uma coleção de máquinas virtuais como um conjunto.</span><span class="sxs-lookup"><span data-stu-id="2fb52-104">Virtual Machine Scale Sets are an Azure Compute resource you can use to deploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="2fb52-105">Cada tipo de nó definido em um cluster do Service Fabric é configurado como um Conjunto de Escala de VM separado.</span><span class="sxs-lookup"><span data-stu-id="2fb52-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="2fb52-106">Cada tipo de nó pode ser escalado verticalmente para cima ou para baixo de forma independente, tem conjuntos diferentes de portas abertas e pode ter métricas de capacidade diferente.</span><span class="sxs-lookup"><span data-stu-id="2fb52-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="2fb52-107">A captura de tela abaixo mostra um cluster com dois tipos de nó: FrontEnd e BackEnd.</span><span class="sxs-lookup"><span data-stu-id="2fb52-107">The following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="2fb52-108">Cada tipo de nó tem cinco nós.</span><span class="sxs-lookup"><span data-stu-id="2fb52-108">Each node type has five nodes each.</span></span>

![Captura de tela de um cluster com dois tipos de nó][NodeTypes]

## <a name="mapping-vm-scale-set-instances-to-nodes"></a><span data-ttu-id="2fb52-110">Mapeando instâncias de conjunto de escala de VM para nós</span><span class="sxs-lookup"><span data-stu-id="2fb52-110">Mapping VM Scale Set instances to nodes</span></span>
<span data-ttu-id="2fb52-111">Como você pode ver acima, as instâncias de conjunto de escala da VM começam da instância 0 e vão subindo.</span><span class="sxs-lookup"><span data-stu-id="2fb52-111">As you can see above, the VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="2fb52-112">A numeração está refletida nos nomes.</span><span class="sxs-lookup"><span data-stu-id="2fb52-112">The numbering is reflected in the names.</span></span> <span data-ttu-id="2fb52-113">Por exemplo, BackEnd_0 é a instância 0 do conjunto de dimensionamento da VM de BackEnd.</span><span class="sxs-lookup"><span data-stu-id="2fb52-113">For example, BackEnd_0 is instance 0 of the BackEnd VM Scale Set.</span></span> <span data-ttu-id="2fb52-114">Esse conjunto de escala da VM específico tem cinco instâncias, chamadas BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 e BackEnd_4.</span><span class="sxs-lookup"><span data-stu-id="2fb52-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="2fb52-115">Quando você escala um conjunto de escala de VM verticalmente, uma nova instância é criada.</span><span class="sxs-lookup"><span data-stu-id="2fb52-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="2fb52-116">O novo nome da instância do conjunto de escala da VM geralmente será o nome do conjunto de escala da VM mais o número de instância seguinte.</span><span class="sxs-lookup"><span data-stu-id="2fb52-116">The new VM Scale Set instance name will typically be the VM Scale Set name + the next instance number.</span></span> <span data-ttu-id="2fb52-117">Em nosso exemplo, é BackEnd_5.</span><span class="sxs-lookup"><span data-stu-id="2fb52-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-to-each-node-typevm-scale-set"></a><span data-ttu-id="2fb52-118">Mapeamento de balanceadores de carga de conjunto de escala da VM para cada tipo de nó/conjunto de escala da VM</span><span class="sxs-lookup"><span data-stu-id="2fb52-118">Mapping VM scale set load balancers to each node type/VM Scale Set</span></span>
<span data-ttu-id="2fb52-119">Se você tiver implantado o cluster do portal ou usado o modelo do Resource Manager de exemplo que fornecemos, quando obtiver uma lista de todos os recursos em um Grupo de Recursos, verá os balanceadores de carga para cada tipo de nó ou Conjunto de Escala de VM.</span><span class="sxs-lookup"><span data-stu-id="2fb52-119">If you have deployed your cluster from the portal or have used the sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see the load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="2fb52-120">O nome seria algo como: **LB-&lt;nome do NodeType&gt;**.</span><span class="sxs-lookup"><span data-stu-id="2fb52-120">The name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="2fb52-121">Por exemplo, LB-sfcluster4doc-0, conforme mostrado nesta captura de tela:</span><span class="sxs-lookup"><span data-stu-id="2fb52-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Recursos][Resources]

## <a name="remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="2fb52-123">Conexão remota a uma instância de conjunto de escala da VM ou a um nó de cluster</span><span class="sxs-lookup"><span data-stu-id="2fb52-123">Remote connect to a VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="2fb52-124">Cada tipo de Nó definido em um cluster é configurado como um Conjunto de Escala de VM separado.</span><span class="sxs-lookup"><span data-stu-id="2fb52-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="2fb52-125">Isso significa que os tipos de nó podem ser escalados verticalmente para cima ou para baixo de forma independente e podem ser compostos por diferentes SKUs de VM.</span><span class="sxs-lookup"><span data-stu-id="2fb52-125">That means the node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="2fb52-126">Ao contrário das máquinas virtuais de instância única, as instâncias de conjunto de escala da VM não recebem um endereço IP virtual próprio.</span><span class="sxs-lookup"><span data-stu-id="2fb52-126">Unlike single instance VMs, the VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="2fb52-127">Assim, pode ser complicado procurar um endereço IP e uma porta que você queira usar para fazer a conexão remota com uma instância específica.</span><span class="sxs-lookup"><span data-stu-id="2fb52-127">So it can be a bit challenging when you are looking for an IP address and port that you can use to remote connect to a specific instance.</span></span>

<span data-ttu-id="2fb52-128">Aqui estão as etapas que você pode seguir para descobri-los.</span><span class="sxs-lookup"><span data-stu-id="2fb52-128">Here are the steps you can follow to discover them.</span></span>

### <a name="step-1-find-out-the-virtual-ip-address-for-the-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="2fb52-129">Etapa 1: descobrir o endereço IP virtual do tipo de nó e as regras NAT de entrada para RDP</span><span class="sxs-lookup"><span data-stu-id="2fb52-129">Step 1: Find out the virtual IP address for the node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="2fb52-130">Para obtê-lo, você precisa obter os valores de regras NAT de entrada definidos como parte da definição de recurso para **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="2fb52-130">In order to get that, you need to get the inbound NAT rules values that were defined as a part of the resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="2fb52-131">No portal, navegue até a folha Balanceador de carga e então até **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="2fb52-131">In the portal, navigate to the Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="2fb52-133">Em **Configurações**, clique em **Regras NAT de entrada**.</span><span class="sxs-lookup"><span data-stu-id="2fb52-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="2fb52-134">Isso lhe dá o endereço IP e a porta que você pode usar para fazer a conexão remota com a instância de conjunto de escala da VM.</span><span class="sxs-lookup"><span data-stu-id="2fb52-134">This now gives you the IP address and port that you can use to remote connect to the first VM Scale Set instance.</span></span> <span data-ttu-id="2fb52-135">Na captura de tela a seguir, é **104.42.106.156** e **3389**</span><span class="sxs-lookup"><span data-stu-id="2fb52-135">In the screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-the-port-that-you-can-use-to-remote-connect-to-the-specific-vm-scale-set-instancenode"></a><span data-ttu-id="2fb52-137">Etapa 2: descobrir a porta que você pode usar para fazer conexão remota com o nó/instância do conjunto de escala de VM específico</span><span class="sxs-lookup"><span data-stu-id="2fb52-137">Step 2: Find out the port that you can use to remote connect to the specific VM Scale Set instance/node</span></span>
<span data-ttu-id="2fb52-138">Neste documento, falei sobre como as instâncias de escala da VM mapeiam para os nós.</span><span class="sxs-lookup"><span data-stu-id="2fb52-138">Earlier in this document, I talked about how the VM Scale Set instances map to the nodes.</span></span> <span data-ttu-id="2fb52-139">Nós usaremos isso para descobrir a porta exata.</span><span class="sxs-lookup"><span data-stu-id="2fb52-139">We will use that to figure out the exact port.</span></span>

<span data-ttu-id="2fb52-140">As portas são alocadas em ordem crescente de instância do Conjunto de Escala de VM.</span><span class="sxs-lookup"><span data-stu-id="2fb52-140">The ports are allocated in ascending order of the VM Scale Set instance.</span></span> <span data-ttu-id="2fb52-141">Portanto, em meu exemplo, para o tipo de nó FrontEnd, as portas para cada uma das cinco instâncias são as mostradas a seguir.</span><span class="sxs-lookup"><span data-stu-id="2fb52-141">so in my example for the FrontEnd node type, the ports for each of the five instances are the following.</span></span> <span data-ttu-id="2fb52-142">Agora, você precisa fazer o mesmo mapeamento para a instância do Conjunto de Escala de VM.</span><span class="sxs-lookup"><span data-stu-id="2fb52-142">you now need to do the same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="2fb52-143">**Instância do Conjunto de Escala de VM**</span><span class="sxs-lookup"><span data-stu-id="2fb52-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="2fb52-144">**Porta**</span><span class="sxs-lookup"><span data-stu-id="2fb52-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="2fb52-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="2fb52-145">FrontEnd_0</span></span> |<span data-ttu-id="2fb52-146">3389</span><span class="sxs-lookup"><span data-stu-id="2fb52-146">3389</span></span> |
| <span data-ttu-id="2fb52-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="2fb52-147">FrontEnd_1</span></span> |<span data-ttu-id="2fb52-148">3390</span><span class="sxs-lookup"><span data-stu-id="2fb52-148">3390</span></span> |
| <span data-ttu-id="2fb52-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="2fb52-149">FrontEnd_2</span></span> |<span data-ttu-id="2fb52-150">3391</span><span class="sxs-lookup"><span data-stu-id="2fb52-150">3391</span></span> |
| <span data-ttu-id="2fb52-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="2fb52-151">FrontEnd_3</span></span> |<span data-ttu-id="2fb52-152">3392</span><span class="sxs-lookup"><span data-stu-id="2fb52-152">3392</span></span> |
| <span data-ttu-id="2fb52-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="2fb52-153">FrontEnd_4</span></span> |<span data-ttu-id="2fb52-154">3393</span><span class="sxs-lookup"><span data-stu-id="2fb52-154">3393</span></span> |
| <span data-ttu-id="2fb52-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="2fb52-155">FrontEnd_5</span></span> |<span data-ttu-id="2fb52-156">3394</span><span class="sxs-lookup"><span data-stu-id="2fb52-156">3394</span></span> |

### <a name="step-3-remote-connect-to-the-specific-vm-scale-set-instance"></a><span data-ttu-id="2fb52-157">Etapa 3: conectar-se remotamente à instância do conjunto de escala da VM específica</span><span class="sxs-lookup"><span data-stu-id="2fb52-157">Step 3: Remote connect to the specific VM Scale Set instance</span></span>
<span data-ttu-id="2fb52-158">Na captura de tela abaixo, usei a conexão de área de trabalho remota para me conectar com o FrontEnd_1:</span><span class="sxs-lookup"><span data-stu-id="2fb52-158">In the screenshot below I use Remote Desktop Connection to connect to the FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-to-change-the-rdp-port-range-values"></a><span data-ttu-id="2fb52-160">Como alterar os valores de intervalo da porta RDP</span><span class="sxs-lookup"><span data-stu-id="2fb52-160">How to change the RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="2fb52-161">Antes da implantação de cluster</span><span class="sxs-lookup"><span data-stu-id="2fb52-161">Before cluster deployment</span></span>
<span data-ttu-id="2fb52-162">Quando você estiver configurando o cluster usando um modelo do Resource Manager, poderá especificar o intervalo em **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="2fb52-162">When you are setting up the cluster using an Resource Manager template, you can specify the range in the **inboundNatPools**.</span></span>

<span data-ttu-id="2fb52-163">Vá para a definição de recurso para **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="2fb52-163">Go to the resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="2fb52-164">Lá, você encontra a descrição de **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="2fb52-164">Under that you find the description for **inboundNatPools**.</span></span>  <span data-ttu-id="2fb52-165">Substitua os valores *frontendPortRangeStart* e *frontendPortRangeEnd*.</span><span class="sxs-lookup"><span data-stu-id="2fb52-165">Replace the *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="2fb52-167">Depois da implantação de cluster</span><span class="sxs-lookup"><span data-stu-id="2fb52-167">After cluster deployment</span></span>
<span data-ttu-id="2fb52-168">Isso é um pouco mais complicado e pode resultar na reciclagem das VMs.</span><span class="sxs-lookup"><span data-stu-id="2fb52-168">This is a bit more involved and may result in the VMs getting recycled.</span></span> <span data-ttu-id="2fb52-169">Agora, você terá que definir novos valores usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2fb52-169">You will now have to set new values using Azure PowerShell.</span></span> <span data-ttu-id="2fb52-170">Verifique se o Azure PowerShell versão 1.0 ou posterior está instalado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="2fb52-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="2fb52-171">Se não tiver feito isso antes, sugiro fortemente que você execute as etapas descritas em [Como instalar e configurar o Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="2fb52-171">If you have not done this before, I strongly suggest that you follow the steps outlined in [How to install and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="2fb52-172">Entre na sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fb52-172">Sign in to your Azure account.</span></span> <span data-ttu-id="2fb52-173">Se o comando do PowerShell falhar por algum motivo, verifique se o Azure PowerShell foi instalado corretamente.</span><span class="sxs-lookup"><span data-stu-id="2fb52-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="2fb52-174">Execute o seguinte para obter detalhes sobre o balanceador de carga e ver os valores para a descrição de **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="2fb52-174">Run the following to get details on your load balancer and you see the values for the description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="2fb52-175">Agora defina os valores desejados para *frontendPortRangeEnd* e *frontendPortRangeStart*.</span><span class="sxs-lookup"><span data-stu-id="2fb52-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* to the values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use the API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="2fb52-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2fb52-176">Next steps</span></span>
* [<span data-ttu-id="2fb52-177">Visão geral do recurso "Implantar em qualquer lugar" e comparação com clusters gerenciados do Azure</span><span class="sxs-lookup"><span data-stu-id="2fb52-177">Overview of the "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="2fb52-178">Segurança de cluster</span><span class="sxs-lookup"><span data-stu-id="2fb52-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="2fb52-179"> SDK do Service Fabric e introdução</span><span class="sxs-lookup"><span data-stu-id="2fb52-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
