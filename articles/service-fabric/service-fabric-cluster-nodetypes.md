---
title: "aaaService malha tipos de nó e conjuntos de escala de VM | Microsoft Docs"
description: "Descreve como os tipos de nós do Service Fabric se relacionam tooVM conjuntos de escala e como tooremote conecte-se a instância de conjunto de escala de tooa ou um nó de cluster."
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
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="e7902-103">relação de saudação entre tipos de nós do Service Fabric e conjuntos de escala de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="e7902-103">hello relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="e7902-104">Conjuntos de escala de máquinas virtuais são um recurso de computação do Azure, você pode usar toodeploy e gerenciar uma coleção de máquinas virtuais como um conjunto.</span><span class="sxs-lookup"><span data-stu-id="e7902-104">Virtual Machine Scale Sets are an Azure Compute resource you can use toodeploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="e7902-105">Cada tipo de nó definido em um cluster do Service Fabric é configurado como um Conjunto de Escala de VM separado.</span><span class="sxs-lookup"><span data-stu-id="e7902-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="e7902-106">Cada tipo de nó pode ser escalado verticalmente para cima ou para baixo de forma independente, tem conjuntos diferentes de portas abertas e pode ter métricas de capacidade diferente.</span><span class="sxs-lookup"><span data-stu-id="e7902-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="e7902-107">Olá captura de tela a seguir mostra um cluster que tem dois tipos de nó: front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="e7902-107">hello following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="e7902-108">Cada tipo de nó tem cinco nós.</span><span class="sxs-lookup"><span data-stu-id="e7902-108">Each node type has five nodes each.</span></span>

![Captura de tela de um cluster com dois tipos de nó][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a><span data-ttu-id="e7902-110">Mapeamento de conjunto de escala de VM toonodes de instâncias</span><span class="sxs-lookup"><span data-stu-id="e7902-110">Mapping VM Scale Set instances toonodes</span></span>
<span data-ttu-id="e7902-111">Como você pode ver acima, Olá conjunto de escala de VM iniciar instâncias de instância 0 e, em seguida, aumenta.</span><span class="sxs-lookup"><span data-stu-id="e7902-111">As you can see above, hello VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="e7902-112">Olá numeração é refletido nos nomes de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7902-112">hello numbering is reflected in hello names.</span></span> <span data-ttu-id="e7902-113">Por exemplo, BackEnd_0 é instância 0 da saudação conjunto de escala de VM back-end.</span><span class="sxs-lookup"><span data-stu-id="e7902-113">For example, BackEnd_0 is instance 0 of hello BackEnd VM Scale Set.</span></span> <span data-ttu-id="e7902-114">Esse conjunto de escala da VM específico tem cinco instâncias, chamadas BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 e BackEnd_4.</span><span class="sxs-lookup"><span data-stu-id="e7902-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="e7902-115">Quando você escala um conjunto de escala de VM verticalmente, uma nova instância é criada.</span><span class="sxs-lookup"><span data-stu-id="e7902-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="e7902-116">Olá novo conjunto de escala de VM nome da instância normalmente é nome do conjunto de escala de VM Olá + próximo número de instância hello.</span><span class="sxs-lookup"><span data-stu-id="e7902-116">hello new VM Scale Set instance name will typically be hello VM Scale Set name + hello next instance number.</span></span> <span data-ttu-id="e7902-117">Em nosso exemplo, é BackEnd_5.</span><span class="sxs-lookup"><span data-stu-id="e7902-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a><span data-ttu-id="e7902-118">Mapeamento de VM carregar o conjunto de escala balanceadores tooeach nó tipo VM conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="e7902-118">Mapping VM scale set load balancers tooeach node type/VM Scale Set</span></span>
<span data-ttu-id="e7902-119">Se você tiver implantado o cluster do portal de saudação ou ter usado o modelo de Gerenciador de recursos do exemplo hello fornecemos, em seguida, quando você obter uma lista de todos os recursos em um grupo de recursos, em seguida, você verá balanceadores de carga Olá para cada tipo de conjunto de escala de VM ou nó.</span><span class="sxs-lookup"><span data-stu-id="e7902-119">If you have deployed your cluster from hello portal or have used hello sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see hello load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="e7902-120">Olá nome seria algo como: **LB -&lt;nome de NodeType&gt;**.</span><span class="sxs-lookup"><span data-stu-id="e7902-120">hello name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="e7902-121">Por exemplo, LB-sfcluster4doc-0, conforme mostrado nesta captura de tela:</span><span class="sxs-lookup"><span data-stu-id="e7902-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Recursos][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="e7902-123">Conexão remota tooa instância de conjunto de escala de VM ou um nó de cluster</span><span class="sxs-lookup"><span data-stu-id="e7902-123">Remote connect tooa VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="e7902-124">Cada tipo de Nó definido em um cluster é configurado como um Conjunto de Escala de VM separado.</span><span class="sxs-lookup"><span data-stu-id="e7902-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="e7902-125">Significa Olá tipos de nó pode ser dimensionada para cima ou independentemente e podem ser feitas de SKUs de VM diferente.</span><span class="sxs-lookup"><span data-stu-id="e7902-125">That means hello node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="e7902-126">Ao contrário de única instância VMs, instâncias de conjunto de escala de VM Olá não obtém um endereço IP virtual de seus próprios.</span><span class="sxs-lookup"><span data-stu-id="e7902-126">Unlike single instance VMs, hello VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="e7902-127">Para que ele possa ser um pouco difícil quando você estiver procurando um IP endereço e porta que você pode usar tooremote conectarem instância específica do tooa.</span><span class="sxs-lookup"><span data-stu-id="e7902-127">So it can be a bit challenging when you are looking for an IP address and port that you can use tooremote connect tooa specific instance.</span></span>

<span data-ttu-id="e7902-128">Aqui estão Olá etapas que você pode seguir toodiscovê-los.</span><span class="sxs-lookup"><span data-stu-id="e7902-128">Here are hello steps you can follow toodiscover them.</span></span>

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="e7902-129">Etapa 1: Localizar o endereço IP virtual Olá para o tipo de nó hello e, em seguida, regras de NAT de entrada para RDP</span><span class="sxs-lookup"><span data-stu-id="e7902-129">Step 1: Find out hello virtual IP address for hello node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="e7902-130">Em ordem tooget, é necessária tooget Olá NAT de entrada regras valores que foram definidos como parte da definição de recurso Olá para **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="e7902-130">In order tooget that, you need tooget hello inbound NAT rules values that were defined as a part of hello resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="e7902-131">No portal de hello, navegue até toohello folha de Balanceador de carga e, em seguida, **configurações**.</span><span class="sxs-lookup"><span data-stu-id="e7902-131">In hello portal, navigate toohello Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="e7902-133">Em **Configurações**, clique em **Regras NAT de entrada**.</span><span class="sxs-lookup"><span data-stu-id="e7902-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="e7902-134">Agora fornece Olá endereço IP e porta que você pode usar tooremote conectar toohello primeira instância do conjunto de escala de VM.</span><span class="sxs-lookup"><span data-stu-id="e7902-134">This now gives you hello IP address and port that you can use tooremote connect toohello first VM Scale Set instance.</span></span> <span data-ttu-id="e7902-135">Olá captura de tela abaixo, é **104.42.106.156** e **3389**</span><span class="sxs-lookup"><span data-stu-id="e7902-135">In hello screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a><span data-ttu-id="e7902-137">Etapa 2: Descobrir porta Olá que você pode usar tooremote conectar toohello conjunto de escala de VM instância/nó específico</span><span class="sxs-lookup"><span data-stu-id="e7902-137">Step 2: Find out hello port that you can use tooremote connect toohello specific VM Scale Set instance/node</span></span>
<span data-ttu-id="e7902-138">No início deste documento, eu falou sobre como instâncias de conjunto de escala de VM Olá mapeiam toohello nós.</span><span class="sxs-lookup"><span data-stu-id="e7902-138">Earlier in this document, I talked about how hello VM Scale Set instances map toohello nodes.</span></span> <span data-ttu-id="e7902-139">Usaremos esse toofigure porta exata Olá de saída.</span><span class="sxs-lookup"><span data-stu-id="e7902-139">We will use that toofigure out hello exact port.</span></span>

<span data-ttu-id="e7902-140">Olá portas são alocadas em ordem crescente da instância de conjunto de escala de VM hello.</span><span class="sxs-lookup"><span data-stu-id="e7902-140">hello ports are allocated in ascending order of hello VM Scale Set instance.</span></span> <span data-ttu-id="e7902-141">portanto em meu exemplo de saudação tipo de nó de front-end, portas de Olá para cada um dos cinco instâncias de saudação são seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="e7902-141">so in my example for hello FrontEnd node type, hello ports for each of hello five instances are hello following.</span></span> <span data-ttu-id="e7902-142">Você agora precisa toodo Olá mesmo mapeamento para a instância do conjunto de escala de VM.</span><span class="sxs-lookup"><span data-stu-id="e7902-142">you now need toodo hello same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="e7902-143">**Instância do Conjunto de Escala de VM**</span><span class="sxs-lookup"><span data-stu-id="e7902-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="e7902-144">**Porta**</span><span class="sxs-lookup"><span data-stu-id="e7902-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="e7902-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="e7902-145">FrontEnd_0</span></span> |<span data-ttu-id="e7902-146">3389</span><span class="sxs-lookup"><span data-stu-id="e7902-146">3389</span></span> |
| <span data-ttu-id="e7902-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="e7902-147">FrontEnd_1</span></span> |<span data-ttu-id="e7902-148">3390</span><span class="sxs-lookup"><span data-stu-id="e7902-148">3390</span></span> |
| <span data-ttu-id="e7902-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="e7902-149">FrontEnd_2</span></span> |<span data-ttu-id="e7902-150">3391</span><span class="sxs-lookup"><span data-stu-id="e7902-150">3391</span></span> |
| <span data-ttu-id="e7902-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="e7902-151">FrontEnd_3</span></span> |<span data-ttu-id="e7902-152">3392</span><span class="sxs-lookup"><span data-stu-id="e7902-152">3392</span></span> |
| <span data-ttu-id="e7902-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="e7902-153">FrontEnd_4</span></span> |<span data-ttu-id="e7902-154">3393</span><span class="sxs-lookup"><span data-stu-id="e7902-154">3393</span></span> |
| <span data-ttu-id="e7902-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="e7902-155">FrontEnd_5</span></span> |<span data-ttu-id="e7902-156">3394</span><span class="sxs-lookup"><span data-stu-id="e7902-156">3394</span></span> |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a><span data-ttu-id="e7902-157">Etapa 3: Instância de conjunto de escala específica toohello de conexão remota</span><span class="sxs-lookup"><span data-stu-id="e7902-157">Step 3: Remote connect toohello specific VM Scale Set instance</span></span>
<span data-ttu-id="e7902-158">Na captura de tela de saudação abaixo uso Conexão de área de trabalho remota tooconnect toohello FrontEnd_1:</span><span class="sxs-lookup"><span data-stu-id="e7902-158">In hello screenshot below I use Remote Desktop Connection tooconnect toohello FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a><span data-ttu-id="e7902-160">Como valores do intervalo de saudação toochange porta do RDP</span><span class="sxs-lookup"><span data-stu-id="e7902-160">How toochange hello RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="e7902-161">Antes da implantação de cluster</span><span class="sxs-lookup"><span data-stu-id="e7902-161">Before cluster deployment</span></span>
<span data-ttu-id="e7902-162">Quando você estiver configurando o cluster hello usando um modelo do Gerenciador de recursos, você pode especificar o intervalo de saudação em Olá **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="e7902-162">When you are setting up hello cluster using an Resource Manager template, you can specify hello range in hello **inboundNatPools**.</span></span>

<span data-ttu-id="e7902-163">Vá para consultar a definição de recurso toohello **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="e7902-163">Go toohello resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="e7902-164">Em que você encontrar descrição Olá para **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="e7902-164">Under that you find hello description for **inboundNatPools**.</span></span>  <span data-ttu-id="e7902-165">Substituir saudação *frontendPortRangeStart* e *frontendPortRangeEnd* valores.</span><span class="sxs-lookup"><span data-stu-id="e7902-165">Replace hello *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="e7902-167">Depois da implantação de cluster</span><span class="sxs-lookup"><span data-stu-id="e7902-167">After cluster deployment</span></span>
<span data-ttu-id="e7902-168">Isso é um pouco mais envolvido e pode resultar em VMs Olá recicladas.</span><span class="sxs-lookup"><span data-stu-id="e7902-168">This is a bit more involved and may result in hello VMs getting recycled.</span></span> <span data-ttu-id="e7902-169">Agora, você terá tooset novos valores usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7902-169">You will now have tooset new values using Azure PowerShell.</span></span> <span data-ttu-id="e7902-170">Verifique se o Azure PowerShell versão 1.0 ou posterior está instalado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e7902-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="e7902-171">Se você não tiver feito isso antes, sugiro que você siga etapas Olá descritas em [como tooinstall e configurar o Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="e7902-171">If you have not done this before, I strongly suggest that you follow hello steps outlined in [How tooinstall and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="e7902-172">Entre tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7902-172">Sign in tooyour Azure account.</span></span> <span data-ttu-id="e7902-173">Se o comando do PowerShell falhar por algum motivo, verifique se o Azure PowerShell foi instalado corretamente.</span><span class="sxs-lookup"><span data-stu-id="e7902-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="e7902-174">Executar Olá tooget detalhes no balanceador de carga a seguir e consulte valores hello para descrição Olá para **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="e7902-174">Run hello following tooget details on your load balancer and you see hello values for hello description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="e7902-175">Agora definido *frontendPortRangeEnd* e *frontendPortRangeStart* toohello valores desejados.</span><span class="sxs-lookup"><span data-stu-id="e7902-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* toohello values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="e7902-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e7902-176">Next steps</span></span>
* [<span data-ttu-id="e7902-177">Visão geral do recurso de "Implantar em qualquer lugar" hello e uma comparação com clusters gerenciado do Azure</span><span class="sxs-lookup"><span data-stu-id="e7902-177">Overview of hello "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="e7902-178">Segurança de cluster</span><span class="sxs-lookup"><span data-stu-id="e7902-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="e7902-179"> SDK do Service Fabric e introdução</span><span class="sxs-lookup"><span data-stu-id="e7902-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
