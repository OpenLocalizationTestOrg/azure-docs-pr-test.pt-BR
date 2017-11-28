---
title: "balanceamento de carga de aaaAzure exemplo de Script CLI - vários sites com hello CLI do Azure | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - toohello de vários sites o balanceamento de carga mesma máquina virtual"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="55134-103">Balanceamento de carga de vários sites</span><span class="sxs-lookup"><span data-stu-id="55134-103">Load balance multiple websites</span></span>

<span data-ttu-id="55134-104">Este exemplo de script cria uma rede virtual com duas VMs (máquinas virtuais) que são membros de um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="55134-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="55134-105">Um balanceador de carga direcione o tráfego para separar duas toohello duas VMs de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="55134-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="55134-106">Após o script hello em execução, você pode implantar web server software toohello VMs e hospedar vários sites, cada qual com seu próprio endereço IP.</span><span class="sxs-lookup"><span data-stu-id="55134-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="55134-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="55134-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="55134-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="55134-108">Clean up deployment</span></span> 

<span data-ttu-id="55134-109">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="55134-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="55134-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="55134-110">Script explanation</span></span>

<span data-ttu-id="55134-111">Esse script usa Olá comandos toocreate um grupo de recursos de rede virtual, o balanceador de carga e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="55134-111">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="55134-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="55134-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="55134-113">Command</span><span class="sxs-lookup"><span data-stu-id="55134-113">Command</span></span> | <span data-ttu-id="55134-114">Observações</span><span class="sxs-lookup"><span data-stu-id="55134-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="55134-115">az group create</span><span class="sxs-lookup"><span data-stu-id="55134-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="55134-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="55134-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="55134-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="55134-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="55134-118">Cria uma sub-rede e uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="55134-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="55134-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="55134-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="55134-120">Cria um endereço IP público com um endereço IP estático e um nome DNS associado.</span><span class="sxs-lookup"><span data-stu-id="55134-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="55134-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="55134-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="55134-122">Cria um Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="55134-122">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="55134-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="55134-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="55134-124">Cria uma investigação do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="55134-124">Creates a load balancer probe.</span></span> <span data-ttu-id="55134-125">Uma investigação do balanceador de carga é usado toomonitor cada VM no conjunto de Balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="55134-125">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="55134-126">Se qualquer VM ficar inacessível, o tráfego não é roteado toohello VM.</span><span class="sxs-lookup"><span data-stu-id="55134-126">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="55134-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="55134-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="55134-128">Cria uma regra de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="55134-128">Creates a load balancer rule.</span></span> <span data-ttu-id="55134-129">Neste exemplo, uma regra é criada para a porta 80.</span><span class="sxs-lookup"><span data-stu-id="55134-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="55134-130">Como o tráfego HTTP chega ao balanceador de carga Olá, é roteado tooport 80 uma saudação VMs no conjunto de Balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="55134-130">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello load balancer set.</span></span> |
| [<span data-ttu-id="55134-131">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="55134-131">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="55134-132">Crie um endereço IP de front-end para Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="55134-132">Create a frontend IP address for hello Load Balancer.</span></span> |
| [<span data-ttu-id="55134-133">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="55134-133">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="55134-134">Cria um pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="55134-134">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="55134-135">az network nic create</span><span class="sxs-lookup"><span data-stu-id="55134-135">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="55134-136">Cria uma placa de rede virtual e anexa-rede virtual toohello e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="55134-136">Creates a virtual network card and attaches it toohello virtual network, and subnet.</span></span> |
| [<span data-ttu-id="55134-137">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="55134-137">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="55134-138">Cria um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="55134-138">Creates an availability set.</span></span> <span data-ttu-id="55134-139">Conjuntos de disponibilidade garantem o funcionamento do aplicativo distribuindo as máquinas virtuais de saudação em recursos físicos, de modo que se ocorrer falha, todo o conjunto de saudação não é afetado.</span><span class="sxs-lookup"><span data-stu-id="55134-139">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="55134-140">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="55134-140">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="55134-141">Cria uma configuração de IP.</span><span class="sxs-lookup"><span data-stu-id="55134-141">Creates an IP confiuration.</span></span> <span data-ttu-id="55134-142">Você deve ter o recurso de Microsoft.Network/AllowMultipleIpConfigurationsPerNic Olá habilitado para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="55134-142">You must have hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="55134-143">Somente uma configuração pode ser designada como a configuração de IP primário Olá por NIC, usando hello – sinalizador tornar primário.</span><span class="sxs-lookup"><span data-stu-id="55134-143">Only one configuration may be designated as hello primary IP configuration per NIC, using hello --make-primary flag.</span></span> |
| [<span data-ttu-id="55134-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="55134-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="55134-145">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="55134-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="55134-146">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="55134-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="55134-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="55134-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="55134-148">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="55134-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="55134-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="55134-149">Next steps</span></span>

<span data-ttu-id="55134-150">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="55134-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="55134-151">Exemplos de script CLI rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="55134-151">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
