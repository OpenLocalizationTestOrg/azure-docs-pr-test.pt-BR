---
title: "Exemplo de script da CLI do Azure - Filtrar o tráfego de rede da VM | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Filtrar o tráfego de entrada e saída de rede da VM."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 68ee013cff4e0be15af30239e0314f779f50177a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="b6130-103">Filtrar o tráfego de entrada e saída de rede da VM</span><span class="sxs-lookup"><span data-stu-id="b6130-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="b6130-104">Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="b6130-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="b6130-105">O tráfego de rede de entrada para a sub-rede de front-end é limitado a HTTP, HTTPS e SSH, enquanto o tráfego de rede de saída para a Internet da sub-rede de back-end não é permitido.</span><span class="sxs-lookup"><span data-stu-id="b6130-105">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="b6130-106">Depois de executar o script, você terá uma máquina virtual com dois NICs.</span><span class="sxs-lookup"><span data-stu-id="b6130-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="b6130-107">Cada NIC pode estar conectado a uma sub-rede diferente.</span><span class="sxs-lookup"><span data-stu-id="b6130-107">Each NIC is connected to a different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b6130-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b6130-108">Sample script</span></span>


<span data-ttu-id="b6130-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filtrar tráfego de rede da VM")]</span><span class="sxs-lookup"><span data-stu-id="b6130-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b6130-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="b6130-110">Clean up deployment</span></span> 

<span data-ttu-id="b6130-111">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="b6130-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="b6130-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="b6130-112">Script explanation</span></span>

<span data-ttu-id="b6130-113">Este script usa os comandos a seguir para criar um grupo de recursos, uma rede virtual e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="b6130-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="b6130-114">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="b6130-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="b6130-115">Command</span><span class="sxs-lookup"><span data-stu-id="b6130-115">Command</span></span> | <span data-ttu-id="b6130-116">Observações</span><span class="sxs-lookup"><span data-stu-id="b6130-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b6130-117">az group create</span><span class="sxs-lookup"><span data-stu-id="b6130-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="b6130-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="b6130-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b6130-119">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="b6130-119">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="b6130-120">Cria uma rede virtual do Azure e uma sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="b6130-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="b6130-121">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="b6130-121">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="b6130-122">Cria uma sub-rede back-end.</span><span class="sxs-lookup"><span data-stu-id="b6130-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="b6130-123">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="b6130-123">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="b6130-124">Associa os NSGs às sub-redes.</span><span class="sxs-lookup"><span data-stu-id="b6130-124">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="b6130-125">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="b6130-125">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="b6130-126">Cria um endereço IP público para acessar a VM da Internet.</span><span class="sxs-lookup"><span data-stu-id="b6130-126">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="b6130-127">az network nic create</span><span class="sxs-lookup"><span data-stu-id="b6130-127">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="b6130-128">Cria as interfaces de rede virtual e as anexa às sub-redes de front-end e back-end da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b6130-128">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="b6130-129">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="b6130-129">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="b6130-130">Cria NSG (grupos de segurança de rede) associados às sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="b6130-130">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="b6130-131">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="b6130-131">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="b6130-132">Cria regras NSG que permitem ou bloqueiam portas específicas para sub-redes específicas.</span><span class="sxs-lookup"><span data-stu-id="b6130-132">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="b6130-133">az vm create</span><span class="sxs-lookup"><span data-stu-id="b6130-133">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="b6130-134">Cria máquinas virtuais e anexa um NIC a cada VM.</span><span class="sxs-lookup"><span data-stu-id="b6130-134">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="b6130-135">Este comando também especifica a imagem de máquina virtual a ser usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="b6130-135">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="b6130-136">az group delete</span><span class="sxs-lookup"><span data-stu-id="b6130-136">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="b6130-137">Exclui um grupo de recursos e todos os seus recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="b6130-137">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b6130-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b6130-138">Next steps</span></span>

<span data-ttu-id="b6130-139">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b6130-139">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="b6130-140">Exemplos adicionais de script de CLI de rede podem ser encontrados na [Documentação de visão geral da rede do Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="b6130-140">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>