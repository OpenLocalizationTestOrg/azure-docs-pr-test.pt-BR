---
title: aaaOpen portas tooa VM do Linux com o Azure CLI 1.0 | Microsoft Docs
description: "Saiba como tooopen uma porta / criar um ponto de extremidade tooyour VM do Linux usando a implantação do Gerenciador de recursos do Azure de saudação do modelo e Olá 1.0 da CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a><span data-ttu-id="1d436-103">Abrindo portas e os pontos de extremidade tooa VM do Linux no Azure usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1d436-103">Opening ports and endpoints tooa Linux VM in Azure using hello Azure CLI 1.0</span></span>
<span data-ttu-id="1d436-104">Abrir uma porta, ou criar um ponto de extremidade, tooa máquina virtual (VM) no Azure, criando um filtro de rede em uma sub-rede ou interface de rede VM.</span><span class="sxs-lookup"><span data-stu-id="1d436-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="1d436-105">Você pode colocar esses filtros, que controlam o tráfego de entrada e saído, em um recurso de toohello do grupo de segurança de rede conectados que recebe o tráfego de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d436-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="1d436-106">Vamos usar um exemplo comum de tráfego da Web na porta 80.</span><span class="sxs-lookup"><span data-stu-id="1d436-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="1d436-107">Este artigo mostra como tooopen uma porta tooa VM usando Olá 1.0 da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d436-107">This article shows you how tooopen a port tooa VM using hello Azure CLI 1.0.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="1d436-108">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="1d436-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="1d436-109">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="1d436-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="1d436-110">[1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="1d436-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1d436-111">[2.0 do CLI do Azure](nsg-quickstart.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="1d436-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="1d436-112">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="1d436-112">Quick commands</span></span>
<span data-ttu-id="1d436-113">toocreate um grupo de segurança de rede e as regras é necessário [hello Azure CLI 1.0](../../cli-install-nodejs.md) instalado e usando modo de Gerenciador de recursos:</span><span class="sxs-lookup"><span data-stu-id="1d436-113">toocreate a Network Security Group and rules you need [hello Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1d436-114">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="1d436-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1d436-115">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="1d436-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="1d436-116">Crie o Grupo de Segurança de Rede da seguinte forma, inserindo seus próprios nomes e localização adequadamente.</span><span class="sxs-lookup"><span data-stu-id="1d436-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="1d436-117">Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="1d436-117">hello following example creates a Network Security Group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="1d436-118">Adicionar um servidor da Web regra tooallow HTTP tráfego tooyour (ou ajustar para seu próprio cenário, como conectividade de banco de dados ou acesso SSH).</span><span class="sxs-lookup"><span data-stu-id="1d436-118">Add a rule tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="1d436-119">Olá, exemplo a seguir cria uma regra denominada *myNetworkSecurityGroupRule* tooallow TCP de tráfego na porta 80:</span><span class="sxs-lookup"><span data-stu-id="1d436-119">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="1d436-120">Saudação de associar o grupo de segurança de rede com interface de rede da VM (NIC).</span><span class="sxs-lookup"><span data-stu-id="1d436-120">Associate hello Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="1d436-121">Olá, exemplo a seguir associa um NIC existente denominado *myNic* com hello grupo de segurança de rede denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="1d436-121">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="1d436-122">Como alternativa, você pode associar seu grupo de segurança de rede com uma sub-rede da rede virtual em vez de apenas toohello interface de rede em uma única VM.</span><span class="sxs-lookup"><span data-stu-id="1d436-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="1d436-123">Olá, exemplo a seguir associa uma sub-rede existente denominada *mySubnet* em Olá *myVnet* rede virtual com hello grupo de segurança de rede denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="1d436-123">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="1d436-124">Mais informações sobre os Grupos de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="1d436-124">More information on Network Security Groups</span></span>
<span data-ttu-id="1d436-125">Olá aqui rápido comandos permitem que você tooget para cima e em execução com tooyour de fluxo de tráfego VM.</span><span class="sxs-lookup"><span data-stu-id="1d436-125">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="1d436-126">Grupos de segurança de rede fornecem vários recursos excelentes e granularidade para controlar recursos tooyour de acesso.</span><span class="sxs-lookup"><span data-stu-id="1d436-126">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="1d436-127">Você pode ler mais sobre a [criação de um Grupo de Segurança de Rede e as regras ACL aqui](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1d436-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="1d436-128">Você pode definir Grupos de Segurança de Rede e regras de ACL como parte dos modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d436-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="1d436-129">Leia mais sobre a [criação de Grupos de Segurança de Rede com modelos](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="1d436-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="1d436-130">Se você precisar toomap de encaminhamento de porta toouse uma porta interna de tooan porta externa exclusivo na sua VM, use um balanceador de carga e regras de conversão de endereço de rede (NAT).</span><span class="sxs-lookup"><span data-stu-id="1d436-130">If you need toouse port-forwarding toomap a unique external port tooan internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="1d436-131">Por exemplo, você pode desejar tooexpose TCP porta 8080 externamente e ter tráfego direcionado tooTCP porta 80 em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1d436-131">For example, you may want tooexpose TCP port 8080 externally and have traffic directed tooTCP port 80 on a VM.</span></span> <span data-ttu-id="1d436-132">Você pode aprender sobre a [criação de um balanceador de carga para a Internet](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1d436-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d436-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1d436-133">Next steps</span></span>
<span data-ttu-id="1d436-134">Neste exemplo, você criou um tráfego HTTP de tooallow regra simples.</span><span class="sxs-lookup"><span data-stu-id="1d436-134">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="1d436-135">Você pode encontrar informações sobre como criar ambientes mais detalhadas no hello artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1d436-135">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="1d436-136">Visão geral do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d436-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="1d436-137">O que é um NSG (grupo de segurança de rede)?</span><span class="sxs-lookup"><span data-stu-id="1d436-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="1d436-138">Visão Geral do Azure Resource Manager para Balanceadores de Carga</span><span class="sxs-lookup"><span data-stu-id="1d436-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

