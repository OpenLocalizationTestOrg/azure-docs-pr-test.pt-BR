---
title: Disponibilidade e Escala em modelos do Azure Resource Manager | Microsoft Docs
description: "Tutorial principal de DotNet da máquina virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 494724b5-06af-4dea-a774-ba580cf27527
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c351950fa3fc1023e339c0dc63b034c5e0d910f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="cb8e4-103">Disponibilidade e escala em modelos do Azure Resource Manager para VMs Windows</span><span class="sxs-lookup"><span data-stu-id="cb8e4-103">Availability and scale in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="cb8e4-104">Disponibilidade e escala referem-se ao tempo de atividade e à capacidade de atender à demanda.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-104">Availability and scale refer to uptime and the ability to meet demand.</span></span> <span data-ttu-id="cb8e4-105">Se um aplicativo deve estar ativo 99,9% do tempo, ele precisa ter uma arquitetura que permite vários recursos de computação simultâneos.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-105">If an application must be up 99.9% of the time, it needs to have an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="cb8e4-106">Por exemplo, em vez de ter um único site, uma configuração com um nível mais alto de disponibilidade inclui várias instâncias do mesmo site, com tecnologia de balanceamento na frente delas.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of the same site, with balancing technology in front of them.</span></span> <span data-ttu-id="cb8e4-107">Nessa configuração, uma instância do aplicativo pode ser desativada para manutenção, enquanto o restante continua a funcionar.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-107">In this configuration, one instance of the application can be taken down for maintenance, while the remaining continue to function.</span></span> <span data-ttu-id="cb8e4-108">Por outro lado, a escala se refere à capacidade de aplicativos para atender à demanda.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-108">Scale on the other hand refers to an applications ability to serve demand.</span></span> <span data-ttu-id="cb8e4-109">Com um aplicativo de balanceamento de carga, adicionar ou remover instâncias do pool permite que um aplicativo seja dimensionado para atender à demanda.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-109">With a load balanced application, adding or removing instances from the pool allows an application to scale to meet demand.</span></span>

<span data-ttu-id="cb8e4-110">Este documento detalha como a implantação de exemplo de Loja de Música é configurada para disponibilidade e escala.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-110">This document details how the Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="cb8e4-111">Todas as dependências e configurações exclusivas são realçadas.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="cb8e4-112">Para obter a melhor experiência, pré-implante uma instância da solução em sua assinatura do Azure e trabalhe com o modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-112">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="cb8e4-113">O modelo completo pode ser encontrado aqui – [Implantação de Loja de Música no Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-113">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="availability-set"></a><span data-ttu-id="cb8e4-114">Conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="cb8e4-114">Availability Set</span></span>
<span data-ttu-id="cb8e4-115">Logicamente, um conjunto de disponibilidade abrange as máquinas virtuais do Azure em hosts físicos e outros componentes de infraestrutura, como fontes de alimentação e hardware de rede física.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="cb8e4-116">Conjuntos de disponibilidade garantem que, durante a manutenção, a falha de dispositivo ou outro tempo de inatividade, nem todas as máquinas virtuais sejam afetadas.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="cb8e4-117">Um conjunto de disponibilidade pode ser adicionado a um modelo do Azure Resource Manager usando o Assistente para Adicionar Novos Recursos do Visual Studio ou inserindo JSON válido em um modelo.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-117">An Availability Set can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="cb8e4-118">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Conjunto de disponibilidade](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-118">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "availability-set"
  },
  "properties": {
  }
}
```

<span data-ttu-id="cb8e4-119">Um conjunto de disponibilidade é declarado como uma propriedade de um recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="cb8e4-120">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Associação de conjunto de disponibilidade com máquina virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-120">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="cb8e4-121">O conjunto de disponibilidade como visto no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-121">The availability set as seen from the Azure portal.</span></span> <span data-ttu-id="cb8e4-122">Cada máquina virtual e detalhes sobre a configuração são descritos aqui.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-122">Each virtual machine and details about the configuration are detailed here.</span></span>

![Conjunto de disponibilidade](./media/dotnet-core-4-availability-scale/ase-win.png)

<span data-ttu-id="cb8e4-124">Para obter informações detalhadas sobre conjuntos de disponibilidade, consulte [Gerenciar a disponibilidade das máquinas virtuais](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="cb8e4-125">Balanceador de carga de rede</span><span class="sxs-lookup"><span data-stu-id="cb8e4-125">Network Load Balancer</span></span>
<span data-ttu-id="cb8e4-126">Enquanto um conjunto de disponibilidade fornece tolerância a falhas do aplicativo, um balanceador de carga disponibiliza várias instâncias do aplicativo em um único endereço de rede.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of the application available on a single network address.</span></span> <span data-ttu-id="cb8e4-127">Várias instâncias de um aplicativo podem ser hospedadas em várias máquinas virtuais, cada uma conectada a um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-127">Multiple instances of an application can be hosted on many virtual machines, each one connected to a load balancer.</span></span> <span data-ttu-id="cb8e4-128">Quando o aplicativo é acessado, o balanceador de carga encaminha a solicitação de entrada entre os membros anexados.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-128">As the application is accessed, the load balancer routes the incoming request across the attached members.</span></span> <span data-ttu-id="cb8e4-129">Um balanceador de carga pode ser adicionado usando o Assistente para Adicionar Novos Recursos do Visual Studio ou inserindo recurso JSON formatado adequadamente no modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-129">A Load Balancer can be added using the Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into the Azure Resource Manager template.</span></span>

<span data-ttu-id="cb8e4-130">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Balanceador de carga de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-130">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer"
  },
  ........<truncated>
}
```

<span data-ttu-id="cb8e4-131">Como o aplicativo de exemplo é exposto à Internet com um endereço IP público, esse endereço é associado com o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-131">Because the sample application is exposed to the internet with a public IP address, this address is associated with the load balancer.</span></span> 

<span data-ttu-id="cb8e4-132">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Associação de balanceador de carga de rede com endereço IP público](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-132">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="cb8e4-133">No portal do Azure, a visão de geral do balanceador de carga de rede mostra a associação com o endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-133">From the Azure portal, the network load balancer overview shows the association with the public IP address.</span></span>

![Balanceador de carga de rede](./media/dotnet-core-4-availability-scale/nlb-win.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="cb8e4-135">Regra do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="cb8e4-135">Load Balancer Rule</span></span>
<span data-ttu-id="cb8e4-136">Ao usar um balanceador de carga, regras são configuradas que controlam como o tráfego é balanceado entre recursos planejados.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-136">When using a load balancer, rules are configured that control how traffic is balanced across the intended resources.</span></span> <span data-ttu-id="cb8e4-137">Com o aplicativo de Loja de Música de exemplo, o tráfego chega à porta 80 do endereço IP público e é distribuído pela porta 80 de todas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-137">With the sample Music Store application, traffic arrives on port 80 of the public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="cb8e4-138">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Regra do balanceador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-138">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span></span>

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

<span data-ttu-id="cb8e4-139">Uma exibição da regra do balanceador de carga de rede do portal.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-139">A view of the network load balancer rule from the portal.</span></span>

![Regra do balanceador de carga de rede](./media/dotnet-core-4-availability-scale/lbrule-win.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="cb8e4-141">Investigação do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="cb8e4-141">Load Balancer Probe</span></span>
<span data-ttu-id="cb8e4-142">O balanceador de carga também precisa monitorar cada máquina virtual para que as solicitações sejam atendidas apenas a sistemas em execução.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-142">The load balancer also needs to monitor each virtual machine so that requests are served only to running systems.</span></span> <span data-ttu-id="cb8e4-143">Esse monitoramento é feito por meio da investigação constante de uma porta predefinida.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="cb8e4-144">A implantação da Loja de Música está configurada para a porta de investigação 80 em todas as máquinas virtuais incluídas.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-144">The Music Store deployment is configured to probe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="cb8e4-145">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Investigação do balanceador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-145">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span></span>

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

<span data-ttu-id="cb8e4-146">A investigação do balanceador de carga vista no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-146">The load balancer probe seen from the Azure portal.</span></span>

![Investigação do balanceador de carga de rede](./media/dotnet-core-4-availability-scale/lbprobe-win.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="cb8e4-148">Regras NAT de Entrada</span><span class="sxs-lookup"><span data-stu-id="cb8e4-148">Inbound NAT Rules</span></span>
<span data-ttu-id="cb8e4-149">Ao usar um Balanceador de Carga, regras precisam ser colocadas em prática que fornecem acesso sem balanceamento de carga a cada Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-149">When using a Load Balancer, rules need to be put into place that provide non-load balanced access to each Virtual Machine.</span></span> <span data-ttu-id="cb8e4-150">Por exemplo, ao criar uma conexão RDP com cada máquina virtual, esse tráfego não deve ter o balanceamento de carga, em vez disso, deve ser configurado um caminho predeterminado.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-150">For instance, when creating an RDP connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="cb8e4-151">Caminhos predeterminados são configurados usando um recurso de Regra NAT de entrada.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-151">Pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="cb8e4-152">Usando esse recurso, a comunicação de entrada pode ser mapeada para máquinas virtuais individuais.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-152">Using this resource, inbound communication can be mapped to individual Virtual Machines.</span></span> 

<span data-ttu-id="cb8e4-153">Com o aplicativo de Loja de Música, uma porta começando em 5000 é mapeada para a porta 3389 em cada máquina virtual para acesso do RDP.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-153">With the Music Store application, a port starting at 5000 is mapped to port 3389 on each Virtual Machine for RDP access.</span></span> <span data-ttu-id="cb8e4-154">A função `copyindex()` é usada para incrementar a porta de entrada, de modo que a segunda máquina virtual recebe uma porta de entrada de 5001, a terceiro 5002 e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-154">The `copyindex()` function is used to increment the incoming port, such that the second Virtual Machine receives an incoming port of 5001, the third 5002, and so on.</span></span>

<span data-ttu-id="cb8e4-155">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Regras NAT de entrada](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-155">Follow this link to see the JSON sample within the Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'RDP-VM', copyIndex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 3389,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="cb8e4-156">Um exemplo de regra NAT de entrada como visto no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-156">One example inbound NAT rule as seen in the Azure portal.</span></span> <span data-ttu-id="cb8e4-157">Uma regra NAT RDP é criada para cada máquina virtual na implantação.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-157">An RDP NAT rule is created for each virtual machine in the deployment.</span></span>

![Regra NAT de entrada](./media/dotnet-core-4-availability-scale/natrule-win.png)

<span data-ttu-id="cb8e4-159">Para obter informações detalhadas sobre o balanceador de carga de rede do Azure, consulte [Balanceamento de carga para serviços de infraestrutura do Azure](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-159">For in-depth information on the Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="cb8e4-160">Implantar várias VMs</span><span class="sxs-lookup"><span data-stu-id="cb8e4-160">Deploy multiple VMs</span></span>
<span data-ttu-id="cb8e4-161">Por fim, para que um conjunto de disponibilidade ou balanceador de carga funcione com eficácia, várias máquinas virtuais são necessárias.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-161">Finally, for an Availability Set or Load Balancer to effectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="cb8e4-162">Várias VMs podem ser implantadas usando a função de cópia de modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-162">Multiple VMs can be deployed using the Azure Resource Manager template copy function.</span></span> <span data-ttu-id="cb8e4-163">Usando a função de cópia, não é necessário definir um número finito de máquinas virtuais, em vez disso, esse valor pode ser fornecido dinamicamente no momento da implantação.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-163">Using the copy function, it is not necessary to define a finite number of Virtual Machines, rather this value can be dynamically provided at the time of deployment.</span></span> <span data-ttu-id="cb8e4-164">A função de cópia consome o número de instâncias a serem criadas e lida com a implantação do número adequado de máquinas virtuais e recursos associados.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-164">The copy function consumes the number of instances to be created and handles deploying the proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="cb8e4-165">No modelo de exemplo de Loja de Música, um parâmetro definido usa uma contagem de instância.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-165">In the Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="cb8e4-166">Esse número é usado em todo o modelo ao criar máquinas virtuais e recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-166">This number is used throughout the template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 2,
  "metadata": {
    "description": "Number of VM instances to be created behind load balancer."
  }
},
```

<span data-ttu-id="cb8e4-167">No recurso de máquina virtual, o loop de cópia recebe um nome e o número do parâmetro de instâncias usado para controlar o número de cópias resultantes.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-167">On the Virtual Machine resource, the copy loop is given a name and the number of instances parameter used to control the number of resulting copies.</span></span>

<span data-ttu-id="cb8e4-168">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Função de cópia de máquina virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-168">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  }
```

<span data-ttu-id="cb8e4-169">A iteração atual da função de cópia pode ser acessada com a função `copyIndex()` .</span><span class="sxs-lookup"><span data-stu-id="cb8e4-169">The current iteration of the copy function can be accessed with the `copyIndex()` function.</span></span> <span data-ttu-id="cb8e4-170">O valor da função de índice de cópia pode ser usado para nomear as máquinas virtuais e outros recursos.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-170">The value of the copy index function can be used to name virtual machines and other resources.</span></span> <span data-ttu-id="cb8e4-171">Por exemplo, se duas instâncias de uma máquina virtual forem implantadas, elas terão nomes diferentes.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="cb8e4-172">A função `copyIndex()` pode ser usada como parte do nome da máquina virtual para criar um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-172">The `copyIndex()` function can be used as part of the virtual machine name to create a unique name.</span></span> <span data-ttu-id="cb8e4-173">Um exemplo da função `copyindex()` usada para fins de nomenclatura pode ser vista no recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-173">An example of the `copyindex()` function used for naming purposes can be seen in the Virtual Machine resource.</span></span> <span data-ttu-id="cb8e4-174">Aqui, o nome do computador é uma concatenação do parâmetro `vmName` e da função `copyIndex()`.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-174">Here, the computer name is a concatenation of the `vmName` parameter, and the `copyIndex()` function.</span></span> 

<span data-ttu-id="cb8e4-175">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Função de índice de cópia](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-175">Follow this link to see the JSON sample within the Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(variables('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "adminPassword": "[parameters('adminPassword')]"
}
```

<span data-ttu-id="cb8e4-176">A função `copyIndex` é usada várias vezes no modelo de exemplo da Loja de Música.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-176">The `copyIndex` function is used several times in the Music Store sample template.</span></span> <span data-ttu-id="cb8e4-177">Recursos e funções utilizando `copyIndex` incluem qualquer coisa específica a uma única instância da máquina virtual como adaptador de rede, regras de balanceador de carga e qualquer uma depende de funções.</span><span class="sxs-lookup"><span data-stu-id="cb8e4-177">Resources and functions utilizing `copyIndex` include anything specific to a single instance of the virtual machine such and network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="cb8e4-178">Para obter mais informações sobre a função de cópia, consulte [Criar várias instâncias de recursos no Azure Resource Manager](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="cb8e4-178">For more information on the copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="cb8e4-179">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="cb8e4-179">Next step</span></span>
<hr>

[<span data-ttu-id="cb8e4-180">Etapa 4 – Implantação de aplicativos com modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cb8e4-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

