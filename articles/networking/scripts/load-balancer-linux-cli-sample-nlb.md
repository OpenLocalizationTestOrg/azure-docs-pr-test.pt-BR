---
title: "Exemplo de Script CLI - tooVMs de tráfego de balanceamento de carga para alta disponibilidade de aaaAzure | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - tooVMs de tráfego de balanceamento de carga para alta disponibilidade"
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
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a><span data-ttu-id="56c46-103">Carregar tooVMs de tráfego de balanceamento para alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="56c46-103">Load balance traffic tooVMs for high availability</span></span>

<span data-ttu-id="56c46-104">Este exemplo de script cria todo o necessário toorun várias máquinas virtuais de Ubuntu configurado em uma alta disponibilidade e de carga balanceada configuração.</span><span class="sxs-lookup"><span data-stu-id="56c46-104">This script sample creates everything needed toorun several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="56c46-105">Após o script hello em execução, você terá três máquinas virtuais, tooan ingressado no conjunto de disponibilidade do Azure e acessível por meio de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="56c46-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="56c46-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="56c46-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="56c46-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="56c46-107">Clean up deployment</span></span> 

<span data-ttu-id="56c46-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="56c46-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="56c46-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="56c46-109">Script explanation</span></span>

<span data-ttu-id="56c46-110">Esse script usa Olá comandos toocreate um grupo de recursos, máquina virtual, o conjunto de disponibilidade, balanceador de carga e todos os recursos relacionados a seguir.</span><span class="sxs-lookup"><span data-stu-id="56c46-110">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="56c46-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="56c46-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="56c46-112">Command</span><span class="sxs-lookup"><span data-stu-id="56c46-112">Command</span></span> | <span data-ttu-id="56c46-113">Observações</span><span class="sxs-lookup"><span data-stu-id="56c46-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="56c46-114">az group create</span><span class="sxs-lookup"><span data-stu-id="56c46-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="56c46-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="56c46-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="56c46-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="56c46-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="56c46-117">Cria uma sub-rede e uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="56c46-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="56c46-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="56c46-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="56c46-119">Cria um endereço IP público com um endereço IP estático e um nome DNS associado.</span><span class="sxs-lookup"><span data-stu-id="56c46-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="56c46-120">az network lb create</span><span class="sxs-lookup"><span data-stu-id="56c46-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="56c46-121">Cria um Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="56c46-121">Creates an Azure load balancer.</span></span> |
| [<span data-ttu-id="56c46-122">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="56c46-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="56c46-123">Cria uma investigação do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="56c46-123">Creates a load balancer probe.</span></span> <span data-ttu-id="56c46-124">Uma investigação do balanceador de carga é usado toomonitor cada VM no conjunto de Balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="56c46-124">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="56c46-125">Se qualquer VM ficar inacessível, o tráfego não é roteado toohello VM.</span><span class="sxs-lookup"><span data-stu-id="56c46-125">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="56c46-126">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="56c46-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="56c46-127">Cria uma regra de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="56c46-127">Creates a load balancer rule.</span></span> <span data-ttu-id="56c46-128">Neste exemplo, uma regra é criada para a porta 80.</span><span class="sxs-lookup"><span data-stu-id="56c46-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="56c46-129">Como o tráfego HTTP chega ao balanceador de carga Olá, é roteado tooport 80 uma saudação VMs no conjunto de balanceamento de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="56c46-129">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello LB set.</span></span> |
| [<span data-ttu-id="56c46-130">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="56c46-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="56c46-131">Cria uma regra de NAT (conversão de endereços de rede) do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="56c46-131">Creates load balancer Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="56c46-132">Regras NAT mapeiam uma porta de porta tooa do balanceador de carga Olá em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56c46-132">NAT rules map a port of hello load balancer tooa port on a VM.</span></span> <span data-ttu-id="56c46-133">Neste exemplo, uma regra NAT é criada para o SSH tráfego tooeach VM no conjunto de Balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="56c46-133">In this sample, a NAT rule is created for SSH traffic tooeach VM in hello load balancer set.</span></span>  |
| [<span data-ttu-id="56c46-134">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="56c46-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="56c46-135">Cria um grupo de segurança de rede (NSG), que é um limite de segurança entre a máquina de virtual de internet e Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="56c46-135">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="56c46-136">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="56c46-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="56c46-137">Cria um tooallow de regra NSG o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="56c46-137">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="56c46-138">Neste exemplo, a porta 22 é aberta para o tráfego SSH.</span><span class="sxs-lookup"><span data-stu-id="56c46-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="56c46-139">az network nic create</span><span class="sxs-lookup"><span data-stu-id="56c46-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="56c46-140">Cria uma placa de rede virtual e anexa-rede virtual toohello, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="56c46-140">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="56c46-141">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="56c46-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="56c46-142">Cria um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="56c46-142">Creates an availability set.</span></span> <span data-ttu-id="56c46-143">Conjuntos de disponibilidade garantem o funcionamento do aplicativo distribuindo as máquinas virtuais de saudação em recursos físicos, de modo que se ocorrer falha, todo o conjunto de saudação não é afetado.</span><span class="sxs-lookup"><span data-stu-id="56c46-143">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="56c46-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="56c46-144">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="56c46-145">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="56c46-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="56c46-146">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="56c46-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="56c46-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="56c46-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="56c46-148">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="56c46-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="56c46-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="56c46-149">Next steps</span></span>

<span data-ttu-id="56c46-150">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="56c46-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="56c46-151">Exemplos de script CLI de rede do Azure adicionais podem ser encontrados no hello [documentação de rede do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="56c46-151">Additional Azure Networking CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
