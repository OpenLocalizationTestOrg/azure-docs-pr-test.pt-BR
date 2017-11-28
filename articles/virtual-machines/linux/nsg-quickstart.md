---
title: aaaOpen portas tooa VM do Linux com o Azure CLI 2.0 | Microsoft Docs
description: "Saiba como tooopen uma porta / criar um ponto de extremidade tooyour VM do Linux usando a implantação do Gerenciador de recursos do Azure de saudação do modelo e Olá 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="7a31a-103">Abrir portas e os pontos de extremidade tooa VM do Linux com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7a31a-103">Open ports and endpoints tooa Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="7a31a-104">Abrir uma porta, ou criar um ponto de extremidade, tooa máquina virtual (VM) no Azure, criando um filtro de rede em uma sub-rede ou interface de rede VM.</span><span class="sxs-lookup"><span data-stu-id="7a31a-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="7a31a-105">Você pode colocar esses filtros, que controlam o tráfego de entrada e saído, em um recurso de toohello do grupo de segurança de rede conectados que recebe o tráfego de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a31a-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="7a31a-106">Vamos usar um exemplo comum de tráfego da Web na porta 80.</span><span class="sxs-lookup"><span data-stu-id="7a31a-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="7a31a-107">Este artigo mostra como tooopen tooa uma porta VM com hello 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a31a-107">This article shows you how tooopen a port tooa VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="7a31a-108">Você também pode executar essas etapas com hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7a31a-108">You can also perform these steps with hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="7a31a-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="7a31a-109">Quick commands</span></span>
<span data-ttu-id="7a31a-110">Grupo de segurança de rede toocreate e regras que você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="7a31a-110">toocreate a Network Security Group and rules you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="7a31a-111">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="7a31a-111">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="7a31a-112">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="7a31a-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="7a31a-113">Criar grupo de segurança de rede Olá com [criar az rede nsg](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="7a31a-113">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="7a31a-114">Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="7a31a-114">hello following example creates a network security group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="7a31a-115">Adicionar uma regra com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) tooallow HTTP tráfego tooyour webserver (ou ajustar para seu próprio cenário, como conectividade de banco de dados ou acesso SSH).</span><span class="sxs-lookup"><span data-stu-id="7a31a-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="7a31a-116">Olá, exemplo a seguir cria uma regra denominada *myNetworkSecurityGroupRule* tooallow TCP de tráfego na porta 80:</span><span class="sxs-lookup"><span data-stu-id="7a31a-116">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="7a31a-117">Associar Olá grupo de segurança de rede com interface de rede da VM (NIC) [atualização da nic de rede az](/cli/azure/network/nic#update).</span><span class="sxs-lookup"><span data-stu-id="7a31a-117">Associate hello Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="7a31a-118">Olá, exemplo a seguir associa um NIC existente denominado *myNic* com hello grupo de segurança de rede denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="7a31a-118">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="7a31a-119">Como alternativa, você pode associar seu grupo de segurança de rede com uma sub-rede de rede virtual com [atualização de sub-rede da rede virtual de rede az](/cli/azure/network/vnet/subnet#update) em vez de apenas toohello interface de rede em uma única VM.</span><span class="sxs-lookup"><span data-stu-id="7a31a-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="7a31a-120">Olá, exemplo a seguir associa uma sub-rede existente denominada *mySubnet* em Olá *myVnet* rede virtual com hello grupo de segurança de rede denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="7a31a-120">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="7a31a-121">Mais informações sobre os Grupos de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="7a31a-121">More information on Network Security Groups</span></span>
<span data-ttu-id="7a31a-122">Olá aqui rápido comandos permitem que você tooget para cima e em execução com tooyour de fluxo de tráfego VM.</span><span class="sxs-lookup"><span data-stu-id="7a31a-122">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="7a31a-123">Grupos de segurança de rede fornecem vários recursos excelentes e granularidade para controlar recursos tooyour de acesso.</span><span class="sxs-lookup"><span data-stu-id="7a31a-123">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="7a31a-124">Você pode ler mais sobre a [criação de um Grupo de Segurança de Rede e as regras ACL aqui](tutorial-virtual-network.md#secure-network-traffic).</span><span class="sxs-lookup"><span data-stu-id="7a31a-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="7a31a-125">Para aplicativos Web altamente disponíveis, você deve colocar suas VMs atrás de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a31a-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="7a31a-126">Balanceador de carga Olá distribui tráfego tooVMs, com um grupo de segurança de rede que fornece filtragem.</span><span class="sxs-lookup"><span data-stu-id="7a31a-126">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="7a31a-127">Para obter mais informações, consulte [como balancear tooload Linux virtual máquinas no Azure toocreate um aplicativo altamente disponível](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="7a31a-127">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a31a-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7a31a-128">Next steps</span></span>
<span data-ttu-id="7a31a-129">Neste exemplo, você criou um tráfego HTTP de tooallow regra simples.</span><span class="sxs-lookup"><span data-stu-id="7a31a-129">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="7a31a-130">Você pode encontrar informações sobre como criar ambientes mais detalhadas no hello artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a31a-130">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="7a31a-131">Visão geral do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7a31a-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="7a31a-132">O que é um NSG (grupo de segurança de rede)?</span><span class="sxs-lookup"><span data-stu-id="7a31a-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
