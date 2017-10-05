---
title: "Exemplo de script da CLI do Azure - Balanceamento de carga de vários sites com a CLI do Azure | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Balanceamento de carga de vários sites para a mesma máquina virtual"
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
ms.openlocfilehash: c5a584b33025122033b930822ae0a0864a7ec1cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="e726c-103">Balanceamento de carga de vários sites</span><span class="sxs-lookup"><span data-stu-id="e726c-103">Load balance multiple websites</span></span>

<span data-ttu-id="e726c-104">Este exemplo de script cria uma rede virtual com duas VMs (máquinas virtuais) que são membros de um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="e726c-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="e726c-105">Um balanceador de carga direciona o tráfego para dois endereços IP separados para as duas VMs.</span><span class="sxs-lookup"><span data-stu-id="e726c-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="e726c-106">Depois de executar o script, você pode implantar software do servidor Web para as VMs e hospedar vários sites, cada um com seu próprio endereço IP.</span><span class="sxs-lookup"><span data-stu-id="e726c-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e726c-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e726c-107">Sample script</span></span>


<span data-ttu-id="e726c-108">[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Balancear a carga de vários sites")]</span><span class="sxs-lookup"><span data-stu-id="e726c-108">[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e726c-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="e726c-109">Clean up deployment</span></span> 

<span data-ttu-id="e726c-110">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e726c-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e726c-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="e726c-111">Script explanation</span></span>

<span data-ttu-id="e726c-112">Esse script usa os seguintes comandos para criar um grupo de recursos, uma rede virtual, um balanceador de carga e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e726c-112">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="e726c-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="e726c-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e726c-114">Command</span><span class="sxs-lookup"><span data-stu-id="e726c-114">Command</span></span> | <span data-ttu-id="e726c-115">Observações</span><span class="sxs-lookup"><span data-stu-id="e726c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e726c-116">az group create</span><span class="sxs-lookup"><span data-stu-id="e726c-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e726c-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="e726c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e726c-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="e726c-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="e726c-119">Cria uma sub-rede e uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="e726c-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="e726c-120">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="e726c-120">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="e726c-121">Cria um endereço IP público com um endereço IP estático e um nome DNS associado.</span><span class="sxs-lookup"><span data-stu-id="e726c-121">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="e726c-122">az network lb create</span><span class="sxs-lookup"><span data-stu-id="e726c-122">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="e726c-123">Cria um Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e726c-123">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="e726c-124">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="e726c-124">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="e726c-125">Cria uma investigação do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="e726c-125">Creates a load balancer probe.</span></span> <span data-ttu-id="e726c-126">Uma investigação do balanceador de carga é usada para monitorar cada VM no conjunto de balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="e726c-126">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="e726c-127">Se qualquer VM ficar inacessível, o tráfego não é roteado para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e726c-127">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="e726c-128">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="e726c-128">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="e726c-129">Cria uma regra de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="e726c-129">Creates a load balancer rule.</span></span> <span data-ttu-id="e726c-130">Neste exemplo, uma regra é criada para a porta 80.</span><span class="sxs-lookup"><span data-stu-id="e726c-130">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="e726c-131">Conforme o tráfego HTTP chega ao balanceador de carga, ele é roteado para a porta 80, uma das VMs no conjunto de balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="e726c-131">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the load balancer set.</span></span> |
| [<span data-ttu-id="e726c-132">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="e726c-132">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="e726c-133">Crie um endereço IP de front-end para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="e726c-133">Create a frontend IP address for the Load Balancer.</span></span> |
| [<span data-ttu-id="e726c-134">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="e726c-134">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="e726c-135">Cria um pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="e726c-135">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="e726c-136">az network nic create</span><span class="sxs-lookup"><span data-stu-id="e726c-136">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="e726c-137">Cria uma placa de rede virtual e a anexa à rede virtual e à sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e726c-137">Creates a virtual network card and attaches it to the virtual network, and subnet.</span></span> |
| [<span data-ttu-id="e726c-138">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="e726c-138">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="e726c-139">Cria um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="e726c-139">Creates an availability set.</span></span> <span data-ttu-id="e726c-140">Conjuntos de disponibilidade garantem o funcionamento de aplicativos, distribuindo as máquinas virtuais em recursos físicos, de modo que, se ocorrer uma falha, todo o conjunto não é afetado.</span><span class="sxs-lookup"><span data-stu-id="e726c-140">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="e726c-141">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="e726c-141">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="e726c-142">Cria uma configuração de IP.</span><span class="sxs-lookup"><span data-stu-id="e726c-142">Creates an IP confiuration.</span></span> <span data-ttu-id="e726c-143">O recurso Microsoft.Network/AllowMultipleIpConfigurationsPerNic deve estar habilitado para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e726c-143">You must have the Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="e726c-144">Somente uma configuração pode ser designada como a configuração de IP primário por NIC, usando o sinalizador --make-primary.</span><span class="sxs-lookup"><span data-stu-id="e726c-144">Only one configuration may be designated as the primary IP configuration per NIC, using the --make-primary flag.</span></span> |
| [<span data-ttu-id="e726c-145">az vm create</span><span class="sxs-lookup"><span data-stu-id="e726c-145">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="e726c-146">Cria a máquina virtual e a conecta a placa de rede, a rede virtual, a sub-rede e o NSG.</span><span class="sxs-lookup"><span data-stu-id="e726c-146">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="e726c-147">Este comando também especifica a imagem da máquina virtual a ser usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="e726c-147">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="e726c-148">az group delete</span><span class="sxs-lookup"><span data-stu-id="e726c-148">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e726c-149">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="e726c-149">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e726c-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e726c-150">Next steps</span></span>

<span data-ttu-id="e726c-151">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e726c-151">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e726c-152">Exemplos adicionais de script de CLI de rede podem ser encontrados na [Documentação de visão geral da rede do Azure](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e726c-152">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
