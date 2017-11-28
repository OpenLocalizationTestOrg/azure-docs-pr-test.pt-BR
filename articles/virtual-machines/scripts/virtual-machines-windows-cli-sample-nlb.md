---
title: aaaAzure exemplo de Script CLI - criar uma VM do Windows Server 2016 com o NLB | Microsoft Docs
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
ms.openlocfilehash: aaaac0c2cc32ce0cac21417926399d848bd6fa09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="7fcaf-103">Como balancear a carga de tráfego entre máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="7fcaf-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="7fcaf-104">Este exemplo de script cria todo o necessário toorun várias máquinas virtuais de Ubuntu configurado em uma alta disponibilidade e de carga balanceada configuração.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-104">This script sample creates everything needed toorun several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="7fcaf-105">Após o script hello em execução, você terá três máquinas virtuais, tooan ingressado no conjunto de disponibilidade do Azure e acessível por meio de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7fcaf-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="7fcaf-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-windows-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7fcaf-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="7fcaf-107">Clean up deployment</span></span> 

<span data-ttu-id="7fcaf-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="7fcaf-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="7fcaf-109">Script explanation</span></span>

<span data-ttu-id="7fcaf-110">Esse script usa Olá comandos toocreate um grupo de recursos, máquina virtual, o conjunto de disponibilidade, balanceador de carga e todos os recursos relacionados a seguir.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-110">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="7fcaf-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7fcaf-112">Command</span><span class="sxs-lookup"><span data-stu-id="7fcaf-112">Command</span></span> | <span data-ttu-id="7fcaf-113">Observações</span><span class="sxs-lookup"><span data-stu-id="7fcaf-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7fcaf-114">az group create</span><span class="sxs-lookup"><span data-stu-id="7fcaf-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7fcaf-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7fcaf-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="7fcaf-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="7fcaf-117">Cria uma sub-rede e uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="7fcaf-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="7fcaf-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="7fcaf-119">Cria um endereço IP público com um endereço IP estático e um nome DNS associado.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="7fcaf-120">az network lb create</span><span class="sxs-lookup"><span data-stu-id="7fcaf-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="7fcaf-121">Cria um balanceador de carga de rede (NLB) do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-121">Creates an Azure Network Load Balancer (NLB).</span></span> |
| [<span data-ttu-id="7fcaf-122">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="7fcaf-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="7fcaf-123">Cria uma investigação NLB.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-123">Creates an NLB probe.</span></span> <span data-ttu-id="7fcaf-124">Uma investigação NLB é usado toomonitor cada VM no conjunto NLB hello.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-124">An NLB probe is used toomonitor each VM in hello NLB set.</span></span> <span data-ttu-id="7fcaf-125">Se qualquer VM ficar inacessível, o tráfego não é roteado toohello VM.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-125">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="7fcaf-126">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="7fcaf-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="7fcaf-127">Cria uma regra NLB.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-127">Creates an NLB rule.</span></span> <span data-ttu-id="7fcaf-128">Neste exemplo, uma regra é criada para a porta 80.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="7fcaf-129">Como o tráfego HTTP chega ao Olá NLB, é roteado tooport 80 uma das VMs Olá Olá NLB conjunto.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-129">As HTTP traffic arrives at hello NLB, it is routed tooport 80 one of hello VMs in hello NLB set.</span></span> |
| [<span data-ttu-id="7fcaf-130">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="7fcaf-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="7fcaf-131">Cria uma regra de conversão de endereços de rede (NAT) do NLB.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-131">Creates an NLB Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="7fcaf-132">Regras NAT mapeiam uma porta de saudação porta tooa NLB em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-132">NAT rules map a port of hello NLB tooa port on a VM.</span></span> <span data-ttu-id="7fcaf-133">Neste exemplo, uma regra NAT é criada para o SSH tráfego tooeach VM no conjunto NLB hello.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-133">In this sample, a NAT rule is created for SSH traffic tooeach VM in hello NLB set.</span></span>  |
| [<span data-ttu-id="7fcaf-134">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="7fcaf-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="7fcaf-135">Cria um grupo de segurança de rede (NSG), que é um limite de segurança entre a máquina de virtual de internet e Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-135">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="7fcaf-136">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="7fcaf-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="7fcaf-137">Cria um tooallow de regra NSG o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-137">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="7fcaf-138">Neste exemplo, a porta 22 é aberta para o tráfego SSH.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="7fcaf-139">az network nic create</span><span class="sxs-lookup"><span data-stu-id="7fcaf-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="7fcaf-140">Cria uma placa de rede virtual e anexa-rede virtual toohello, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-140">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="7fcaf-141">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="7fcaf-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="7fcaf-142">Cria um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-142">Creates an availability set.</span></span> <span data-ttu-id="7fcaf-143">Conjuntos de disponibilidade garantem o funcionamento do aplicativo distribuindo as máquinas virtuais de saudação em recursos físicos, de modo que se ocorrer falha, todo o conjunto de saudação não é afetado.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-143">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="7fcaf-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="7fcaf-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="7fcaf-145">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="7fcaf-146">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="7fcaf-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="7fcaf-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="7fcaf-148">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="7fcaf-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7fcaf-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7fcaf-149">Next steps</span></span>

<span data-ttu-id="7fcaf-150">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7fcaf-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7fcaf-151">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7fcaf-151">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
