---
title: Exemplo de script da CLI do Azure - Como criar uma VM do Windows Server 2016 com NLB | Microsoft Docs
description: Exemplo de script da CLI do Azure - Como criar uma VM do Windows Server 2016 com NLB
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: 916204d2b94868057b824feee7b7d032c66382f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="228e1-103">Como balancear a carga de tráfego entre máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="228e1-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="228e1-104">Este exemplo de script cria todos os componentes necessários para executar várias máquinas virtuais do Ubuntu configuradas em uma alta disponibilidade e configuração de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="228e1-104">This script sample creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="228e1-105">Após a execução do script, você terá três máquinas virtuais, associadas a um Conjunto de Disponibilidade do Azure, e acessíveis por meio de um Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="228e1-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="228e1-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="228e1-106">Sample script</span></span>

<span data-ttu-id="228e1-107">[!code-azurecli-interactive[principal](../../../cli_scripts/virtual-machine/create-vm-nlb/create-windows-vm-nlb.sh "Criação rápida de VM")]</span><span class="sxs-lookup"><span data-stu-id="228e1-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-windows-vm-nlb.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="228e1-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="228e1-108">Clean up deployment</span></span> 

<span data-ttu-id="228e1-109">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="228e1-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="228e1-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="228e1-110">Script explanation</span></span>

<span data-ttu-id="228e1-111">Esse script usa os seguintes comandos para criar um grupo de recursos, uma máquina virtual, um conjunto de disponibilidade, um balanceador de carga e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="228e1-111">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="228e1-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="228e1-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="228e1-113">Command</span><span class="sxs-lookup"><span data-stu-id="228e1-113">Command</span></span> | <span data-ttu-id="228e1-114">Observações</span><span class="sxs-lookup"><span data-stu-id="228e1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="228e1-115">az group create</span><span class="sxs-lookup"><span data-stu-id="228e1-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="228e1-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="228e1-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="228e1-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="228e1-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="228e1-118">Cria uma sub-rede e uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="228e1-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="228e1-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="228e1-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="228e1-120">Cria um endereço IP público com um endereço IP estático e um nome DNS associado.</span><span class="sxs-lookup"><span data-stu-id="228e1-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="228e1-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="228e1-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="228e1-122">Cria um balanceador de carga de rede (NLB) do Azure.</span><span class="sxs-lookup"><span data-stu-id="228e1-122">Creates an Azure Network Load Balancer (NLB).</span></span> |
| [<span data-ttu-id="228e1-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="228e1-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="228e1-124">Cria uma investigação NLB.</span><span class="sxs-lookup"><span data-stu-id="228e1-124">Creates an NLB probe.</span></span> <span data-ttu-id="228e1-125">Uma investigação NLB é usada para monitorar cada VM no conjunto do NLB.</span><span class="sxs-lookup"><span data-stu-id="228e1-125">An NLB probe is used to monitor each VM in the NLB set.</span></span> <span data-ttu-id="228e1-126">Se qualquer VM ficar inacessível, o tráfego não é roteado para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="228e1-126">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="228e1-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="228e1-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="228e1-128">Cria uma regra NLB.</span><span class="sxs-lookup"><span data-stu-id="228e1-128">Creates an NLB rule.</span></span> <span data-ttu-id="228e1-129">Neste exemplo, uma regra é criada para a porta 80.</span><span class="sxs-lookup"><span data-stu-id="228e1-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="228e1-130">Conforme o tráfego HTTP chega ao NLB, ele é roteado para a porta 80, uma das VMs no conjunto do NLB.</span><span class="sxs-lookup"><span data-stu-id="228e1-130">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span></span> |
| [<span data-ttu-id="228e1-131">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="228e1-131">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="228e1-132">Cria uma regra de conversão de endereços de rede (NAT) do NLB.</span><span class="sxs-lookup"><span data-stu-id="228e1-132">Creates an NLB Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="228e1-133">Regras de NAT mapeiam uma porta do NLB para uma porta em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="228e1-133">NAT rules map a port of the NLB to a port on a VM.</span></span> <span data-ttu-id="228e1-134">Neste exemplo, é criada uma regra de NAT para o tráfego SSH para cada VM no conjunto do NLB.</span><span class="sxs-lookup"><span data-stu-id="228e1-134">In this sample, a NAT rule is created for SSH traffic to each VM in the NLB set.</span></span>  |
| [<span data-ttu-id="228e1-135">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="228e1-135">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="228e1-136">Cria um grupo de segurança de rede (NSG), que é um limite de segurança entre a Internet e a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="228e1-136">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="228e1-137">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="228e1-137">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="228e1-138">Cria uma regra NSG para permitir o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="228e1-138">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="228e1-139">Neste exemplo, a porta 22 é aberta para o tráfego SSH.</span><span class="sxs-lookup"><span data-stu-id="228e1-139">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="228e1-140">az network nic create</span><span class="sxs-lookup"><span data-stu-id="228e1-140">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="228e1-141">Cria uma placa de rede virtual e a anexa à rede virtual, à sub-rede e ao NSG.</span><span class="sxs-lookup"><span data-stu-id="228e1-141">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="228e1-142">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="228e1-142">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="228e1-143">Cria um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="228e1-143">Creates an availability set.</span></span> <span data-ttu-id="228e1-144">Conjuntos de disponibilidade garantem o funcionamento de aplicativos, distribuindo as máquinas virtuais em recursos físicos, de modo que, se ocorrer uma falha, todo o conjunto não é afetado.</span><span class="sxs-lookup"><span data-stu-id="228e1-144">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="228e1-145">az vm create</span><span class="sxs-lookup"><span data-stu-id="228e1-145">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="228e1-146">Cria a máquina virtual e a conecta a placa de rede, a rede virtual, a sub-rede e o NSG.</span><span class="sxs-lookup"><span data-stu-id="228e1-146">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="228e1-147">Este comando também especifica a imagem da máquina virtual a ser usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="228e1-147">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="228e1-148">az group delete</span><span class="sxs-lookup"><span data-stu-id="228e1-148">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="228e1-149">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="228e1-149">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="228e1-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="228e1-150">Next steps</span></span>

<span data-ttu-id="228e1-151">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="228e1-151">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="228e1-152">Exemplos de script CLI máquinas virtuais adicionais podem ser encontrados na [documentação da VM do Windows do Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="228e1-152">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
