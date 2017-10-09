---
title: aaaAvailability e a escala em modelos do Gerenciador de recursos do Azure | Microsoft Docs
description: "Tutorial principal de DotNet da máquina virtual do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="0098f-103">Disponibilidade e escala em modelos do Azure Resource Manager para VMs Linux</span><span class="sxs-lookup"><span data-stu-id="0098f-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="0098f-104">Disponibilidade e escalabilidade consulte toouptime e hello demanda de toomeet de capacidade.</span><span class="sxs-lookup"><span data-stu-id="0098f-104">Availability and scale refer toouptime and hello ability toomeet demand.</span></span> <span data-ttu-id="0098f-105">Se um aplicativo deve ser o 99,9% de tempo de saudação, ele precisa toohave uma arquitetura que permite que vários recursos de computação simultâneas.</span><span class="sxs-lookup"><span data-stu-id="0098f-105">If an application must be up 99.9% of hello time, it needs toohave an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="0098f-106">Por exemplo, em vez de um único site, uma configuração com um nível mais alto de disponibilidade inclui várias instâncias do mesmo site, com a tecnologia na frente de balanceamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="0098f-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of hello same site, with balancing technology in front of them.</span></span> <span data-ttu-id="0098f-107">Nessa configuração, uma instância do aplicativo hello pode ser desativada para manutenção, enquanto Olá restantes continuar toofunction.</span><span class="sxs-lookup"><span data-stu-id="0098f-107">In this configuration, one instance of hello application can be taken down for maintenance, while hello remaining continue toofunction.</span></span> <span data-ttu-id="0098f-108">Escala em Olá outro lado refere-se por demanda de tooserve de capacidade de aplicativos tooan.</span><span class="sxs-lookup"><span data-stu-id="0098f-108">Scale on hello other hand refers tooan applications ability tooserve demand.</span></span> <span data-ttu-id="0098f-109">Com uma carga aplicativo equilibrado, adicionando ou removendo instâncias de pool de saudação permite que um aplicativo tooscale toomeet na demanda.</span><span class="sxs-lookup"><span data-stu-id="0098f-109">With a load balanced application, adding or removing instances from hello pool allows an application tooscale toomeet demand.</span></span>

<span data-ttu-id="0098f-110">Este documento detalha como Olá implantação de exemplo do repositório de música está configurado para disponibilidade e escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="0098f-110">This document details how hello Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="0098f-111">Todas as dependências e configurações exclusivas são realçadas.</span><span class="sxs-lookup"><span data-stu-id="0098f-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="0098f-112">Para melhor experiência de hello, pré-implante uma instância do hello solução tooyour assinatura do Azure e trabalha junto com o modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="0098f-112">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="0098f-113">modelo completo Olá pode ser encontrado aqui – [implantação de repositório de música no Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="0098f-113">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="0098f-114">Conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="0098f-114">Availability Set</span></span>
<span data-ttu-id="0098f-115">Logicamente, um conjunto de disponibilidade abrange as máquinas virtuais do Azure em hosts físicos e outros componentes de infraestrutura, como fontes de alimentação e hardware de rede física.</span><span class="sxs-lookup"><span data-stu-id="0098f-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="0098f-116">Conjuntos de disponibilidade garantem que, durante a manutenção, a falha de dispositivo ou outro tempo de inatividade, nem todas as máquinas virtuais sejam afetadas.</span><span class="sxs-lookup"><span data-stu-id="0098f-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="0098f-117">Um conjunto de disponibilidade podem ser adicionado tooan Azure Resource Manager modelo usando o Visual Studio novo Assistente para adicionar recurso de saudação ou inserindo um JSON válido em um modelo.</span><span class="sxs-lookup"><span data-stu-id="0098f-117">An Availability Set can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="0098f-118">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [conjunto de disponibilidade](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span><span class="sxs-lookup"><span data-stu-id="0098f-118">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

<span data-ttu-id="0098f-119">Um conjunto de disponibilidade é declarado como uma propriedade de um recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0098f-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="0098f-120">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [associação de conjunto de disponibilidade com a máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span><span class="sxs-lookup"><span data-stu-id="0098f-120">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="0098f-121">disponibilidade de saudação definida como visto no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0098f-121">hello availability set as seen from hello Azure portal.</span></span> <span data-ttu-id="0098f-122">Cada máquina virtual e os detalhes sobre a configuração de saudação são descritos aqui.</span><span class="sxs-lookup"><span data-stu-id="0098f-122">Each virtual machine and details about hello configuration are detailed here.</span></span>

![Conjunto de disponibilidade](./media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="0098f-124">Para obter informações detalhadas sobre conjuntos de disponibilidade, consulte [Gerenciar a disponibilidade das máquinas virtuais](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0098f-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="0098f-125">Balanceador de carga de rede</span><span class="sxs-lookup"><span data-stu-id="0098f-125">Network Load Balancer</span></span>
<span data-ttu-id="0098f-126">Enquanto um conjunto de disponibilidade fornece tolerância a falhas de aplicativo, um balanceador de carga disponibiliza muitas instâncias do aplicativo hello em um único endereço de rede.</span><span class="sxs-lookup"><span data-stu-id="0098f-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of hello application available on a single network address.</span></span> <span data-ttu-id="0098f-127">Várias instâncias de um aplicativo podem ser hospedadas em muitas máquinas virtuais, cada um deles conectado tooa balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="0098f-127">Multiple instances of an application can be hosted on many virtual machines, each one connected tooa load balancer.</span></span> <span data-ttu-id="0098f-128">Como o aplicativo hello é acessado, rotas de Balanceador de carga Olá Olá solicitação de entrada entre os membros da saudação anexado.</span><span class="sxs-lookup"><span data-stu-id="0098f-128">As hello application is accessed, hello load balancer routes hello incoming request across hello attached members.</span></span> <span data-ttu-id="0098f-129">Um balanceador de carga podem ser adicionado usando Olá Visual Studio novo Assistente para adicionar recurso, ou inserindo corretamente formatado recursos JSON no modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="0098f-129">A Load Balancer can be added using hello Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into hello Azure Resource Manager template.</span></span>

<span data-ttu-id="0098f-130">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [balanceador de carga de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="0098f-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

<span data-ttu-id="0098f-131">Porque o aplicativo de exemplo hello toohello exposto à internet com um endereço IP público, esse endereço é associado ao balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="0098f-131">Because hello sample application is exposed toohello internet with a public IP address, this address is associated with hello load balancer.</span></span> 

<span data-ttu-id="0098f-132">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [associação de Balanceador de carga de rede com endereço IP público](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span><span class="sxs-lookup"><span data-stu-id="0098f-132">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="0098f-133">De Olá portal do Azure, hello visão geral do balanceador de carga de rede exibe associação Olá com endereço IP público de saudação.</span><span class="sxs-lookup"><span data-stu-id="0098f-133">From hello Azure portal, hello network load balancer overview shows hello association with hello public IP address.</span></span>

![Balanceador de carga de rede](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="0098f-135">Regra do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="0098f-135">Load Balancer Rule</span></span>
<span data-ttu-id="0098f-136">Ao usar um balanceador de carga, regras são configuradas que controlam como o tráfego é balanceado em todos os recursos de saudação que se destina.</span><span class="sxs-lookup"><span data-stu-id="0098f-136">When using a load balancer, rules are configured that control how traffic is balanced across hello intended resources.</span></span> <span data-ttu-id="0098f-137">Com o aplicativo de repositório de música do exemplo hello, o tráfego chega na porta 80 do endereço IP público de saudação e é distribuído entre a porta 80 de todas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="0098f-137">With hello sample Music Store application, traffic arrives on port 80 of hello public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="0098f-138">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [regra de Balanceador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="0098f-138">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

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

<span data-ttu-id="0098f-139">Uma exibição da rede Olá carregar regra do balanceador do portal hello.</span><span class="sxs-lookup"><span data-stu-id="0098f-139">A view of hello network load balancer rule from hello portal.</span></span>

![Regra do balanceador de carga de rede](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="0098f-141">Investigação do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="0098f-141">Load Balancer Probe</span></span>
<span data-ttu-id="0098f-142">Olá balanceador de carga também precisa toomonitor cada máquina virtual para que somente os sistemas de toorunning as solicitações sejam atendidas.</span><span class="sxs-lookup"><span data-stu-id="0098f-142">hello load balancer also needs toomonitor each virtual machine so that requests are served only toorunning systems.</span></span> <span data-ttu-id="0098f-143">Esse monitoramento é feito por meio da investigação constante de uma porta predefinida.</span><span class="sxs-lookup"><span data-stu-id="0098f-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="0098f-144">implantação do repositório de música Olá é configurado tooprobe máquinas de virtuais de porta 80 em todos os incluídos.</span><span class="sxs-lookup"><span data-stu-id="0098f-144">hello Music Store deployment is configured tooprobe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="0098f-145">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [investigação do balanceador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span><span class="sxs-lookup"><span data-stu-id="0098f-145">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

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

<span data-ttu-id="0098f-146">investigação do balanceador de carga Olá Vista de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0098f-146">hello load balancer probe seen from hello Azure portal.</span></span>

![Investigação do balanceador de carga de rede](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="0098f-148">Regras NAT de Entrada</span><span class="sxs-lookup"><span data-stu-id="0098f-148">Inbound NAT Rules</span></span>
<span data-ttu-id="0098f-149">Ao usar um balanceador de carga, regras necessário toobe colocados em prática que fornecem acesso com balanceamento de carga não tooeach Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="0098f-149">When using a Load Balancer, rules need toobe put into place that provide non-load balanced access tooeach Virtual Machine.</span></span> <span data-ttu-id="0098f-150">Por exemplo, ao criar uma conexão SSH com cada máquina virtual, esse tráfego não deve ter o balanceamento de carga, em vez disso, um caminho predeterminado deve ser configurado.</span><span class="sxs-lookup"><span data-stu-id="0098f-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="0098f-151">Caminhos predeterminados são configurados usando um recurso de regra NAT de entrada.</span><span class="sxs-lookup"><span data-stu-id="0098f-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="0098f-152">Usando esse recurso, a comunicação de entrada pode ser mapeada tooindividual máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="0098f-152">Using this resource, inbound communication can be mapped tooindividual Virtual Machines.</span></span> 

<span data-ttu-id="0098f-153">Com hello aplicativo de repositório de música, uma porta começando em 5000 é mapeada tooport 22 em cada máquina Virtual para acesso SSH.</span><span class="sxs-lookup"><span data-stu-id="0098f-153">With hello Music Store application, a port starting at 5000 is mapped tooport 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="0098f-154">Olá `copyindex()` função é usada tooincrement Olá porta de entrada, como aquela Olá segunda máquina Virtual recebe uma porta de entrada de 5001, Olá 5002 terceiro e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="0098f-154">hello `copyindex()` function is used tooincrement hello incoming port, such that hello second Virtual Machine receives an incoming port of 5001, hello third 5002, and so on.</span></span> 

<span data-ttu-id="0098f-155">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [regras de NAT de entrada](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="0098f-155">Follow this link toosee hello JSON sample within hello Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
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
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="0098f-156">Um exemplo de regra NAT de entrada como Olá visto no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0098f-156">One example inbound NAT rule as seen in hello Azure portal.</span></span> <span data-ttu-id="0098f-157">Uma regra de NAT SSH é criada para cada máquina virtual na implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0098f-157">An SSH NAT rule is created for each virtual machine in hello deployment.</span></span>

![Regra NAT de entrada](./media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="0098f-159">Para obter informações detalhadas sobre Olá balanceador de carga de rede do Azure, consulte [balanceamento de carga para serviços de infraestrutura do Azure](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0098f-159">For in-depth information on hello Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="0098f-160">Implantar várias VMs</span><span class="sxs-lookup"><span data-stu-id="0098f-160">Deploy multiple VMs</span></span>
<span data-ttu-id="0098f-161">Por fim, para uma função de tooeffectively conjunto de disponibilidade ou o balanceador de carga, várias máquinas virtuais são necessárias.</span><span class="sxs-lookup"><span data-stu-id="0098f-161">Finally, for an Availability Set or Load Balancer tooeffectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="0098f-162">Várias VMs podem ser implantadas usando a função de cópia de modelo hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0098f-162">Multiple VMs can be deployed using hello Azure Resource Manager template copy function.</span></span> <span data-ttu-id="0098f-163">Usando a função de cópia hello, não é necessário toodefine um número finito de máquinas virtuais, em vez disso, esse valor pode ser fornecido dinamicamente em tempo de saudação da implantação.</span><span class="sxs-lookup"><span data-stu-id="0098f-163">Using hello copy function, it is not necessary toodefine a finite number of Virtual Machines, rather this value can be dynamically provided at hello time of deployment.</span></span> <span data-ttu-id="0098f-164">função de cópia Olá consome Olá inúmeros toocreated instâncias e identificadores de implantar o número adequado de saudação de máquinas virtuais e recursos associados.</span><span class="sxs-lookup"><span data-stu-id="0098f-164">hello copy function consumes hello number of instances toocreated and handles deploying hello proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="0098f-165">No modelo de exemplo do repositório de música hello, um parâmetro é definido em uma contagem de instâncias.</span><span class="sxs-lookup"><span data-stu-id="0098f-165">In hello Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="0098f-166">Esse número é usado em todo o modelo de saudação durante a criação de máquinas virtuais e recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="0098f-166">This number is used throughout hello template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

<span data-ttu-id="0098f-167">Em Olá recurso de máquina Virtual, loop de cópia Olá recebe um nome e número de saudação do parâmetro de instâncias utilizado toocontrol número de saudação de cópias resultantes.</span><span class="sxs-lookup"><span data-stu-id="0098f-167">On hello Virtual Machine resource, hello copy loop is given a name and hello number of instances parameter used toocontrol hello number of resulting copies.</span></span>

<span data-ttu-id="0098f-168">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [função de cópia de máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span><span class="sxs-lookup"><span data-stu-id="0098f-168">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

<span data-ttu-id="0098f-169">a iteração atual Olá da função de cópia de saudação pode ser acessada com hello `copyIndex()` função.</span><span class="sxs-lookup"><span data-stu-id="0098f-169">hello current iteration of hello copy function can be accessed with hello `copyIndex()` function.</span></span> <span data-ttu-id="0098f-170">valor de saudação da função de índice de cópia de saudação pode ser usado tooname máquinas de virtuais e outros recursos.</span><span class="sxs-lookup"><span data-stu-id="0098f-170">hello value of hello copy index function can be used tooname virtual machines and other resources.</span></span> <span data-ttu-id="0098f-171">Por exemplo, se duas instâncias de uma máquina virtual forem implantadas, elas terão nomes diferentes.</span><span class="sxs-lookup"><span data-stu-id="0098f-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="0098f-172">Olá `copyIndex()` função pode ser usada como parte da máquina virtual de saudação nome toocreate um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="0098f-172">hello `copyIndex()` function can be used as part of hello virtual machine name toocreate a unique name.</span></span> <span data-ttu-id="0098f-173">Um exemplo de hello `copyindex()` função usada para fins de nomenclatura pode ser vista no hello recurso de máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="0098f-173">An example of hello `copyindex()` function used for naming purposes can be seen in hello Virtual Machine resource.</span></span> <span data-ttu-id="0098f-174">Aqui, o nome do computador Olá é uma concatenação do hello `vmName` parâmetro e hello `copyIndex()` função.</span><span class="sxs-lookup"><span data-stu-id="0098f-174">Here, hello computer name is a concatenation of hello `vmName` parameter, and hello `copyIndex()` function.</span></span> 

<span data-ttu-id="0098f-175">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [função de cópia do índice](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span><span class="sxs-lookup"><span data-stu-id="0098f-175">Follow this link toosee hello JSON sample within hello Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

<span data-ttu-id="0098f-176">Olá `copyIndex` função é usada várias vezes no modelo de exemplo do repositório de música hello.</span><span class="sxs-lookup"><span data-stu-id="0098f-176">hello `copyIndex` function is used several times in hello Music Store sample template.</span></span> <span data-ttu-id="0098f-177">Uso de funções e recursos `copyIndex` incluir qualquer coisa específica tooa única instância de máquina virtual de saudação como interface de rede, regras de Balanceador de carga, e qualquer depende de funções.</span><span class="sxs-lookup"><span data-stu-id="0098f-177">Resources and functions utilizing `copyIndex` include anything specific tooa single instance of hello virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="0098f-178">Para obter mais informações sobre a função de cópia hello, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="0098f-178">For more information on hello copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="0098f-179">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="0098f-179">Next step</span></span>
<hr>

[<span data-ttu-id="0098f-180">Etapa 4 – Implantação de aplicativos com modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0098f-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

