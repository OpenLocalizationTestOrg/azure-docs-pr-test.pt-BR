---
title: "Exemplo de script da CLI do Azure - Rotear o tráfego por meio de uma solução de virtualização de rede | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Rotear o tráfego por meio de uma solução de virtualização de rede de firewall.solução de virtualização."
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
ms.openlocfilehash: 78091b515c00591a4af8d807945475b6be50188a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="b8526-103">Rotear o tráfego por meio de uma solução de virtualização de rede</span><span class="sxs-lookup"><span data-stu-id="b8526-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="b8526-104">Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="b8526-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="b8526-105">Ele também cria uma VM com o encaminhamento de IP habilitado para rotear o tráfego entre as duas sub-redes.</span><span class="sxs-lookup"><span data-stu-id="b8526-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="b8526-106">Depois de executar o script, você pode implantar o software de rede, como um aplicativo de firewall, à VM.</span><span class="sxs-lookup"><span data-stu-id="b8526-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="b8526-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b8526-107">Sample script</span></span>


<span data-ttu-id="b8526-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Rotear o tráfego por meio de uma solução de virtualização de rede")]</span><span class="sxs-lookup"><span data-stu-id="b8526-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b8526-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="b8526-109">Clean up deployment</span></span> 

<span data-ttu-id="b8526-110">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="b8526-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="b8526-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="b8526-111">Script explanation</span></span>

<span data-ttu-id="b8526-112">Este script usa os comandos a seguir para criar um grupo de recursos, uma rede virtual e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="b8526-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="b8526-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="b8526-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="b8526-114">Command</span><span class="sxs-lookup"><span data-stu-id="b8526-114">Command</span></span> | <span data-ttu-id="b8526-115">Observações</span><span class="sxs-lookup"><span data-stu-id="b8526-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b8526-116">az group create</span><span class="sxs-lookup"><span data-stu-id="b8526-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="b8526-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="b8526-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b8526-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="b8526-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="b8526-119">Cria uma rede virtual do Azure e uma sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="b8526-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="b8526-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="b8526-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="b8526-121">Cria as sub-redes back-end e DMZ.</span><span class="sxs-lookup"><span data-stu-id="b8526-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="b8526-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="b8526-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="b8526-123">Cria um endereço IP público para acessar a VM da Internet.</span><span class="sxs-lookup"><span data-stu-id="b8526-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="b8526-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="b8526-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="b8526-125">Cria uma interface de rede virtual e habilita o encaminhamento IP nela.</span><span class="sxs-lookup"><span data-stu-id="b8526-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="b8526-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="b8526-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="b8526-127">Cria um grupo de segurança de rede (NSG).</span><span class="sxs-lookup"><span data-stu-id="b8526-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="b8526-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="b8526-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="b8526-129">Cria regras de NSG que permitem as portas HTTP e HTTPS de entrada para a VM.</span><span class="sxs-lookup"><span data-stu-id="b8526-129">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="b8526-130">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="b8526-130">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="b8526-131">Associa os NSGs e tabelas de rotas às sub-redes.</span><span class="sxs-lookup"><span data-stu-id="b8526-131">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="b8526-132">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="b8526-132">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="b8526-133">Cria uma tabela de rotas com todas as rotas.</span><span class="sxs-lookup"><span data-stu-id="b8526-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="b8526-134">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="b8526-134">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="b8526-135">Cria as rotas para rotear o tráfego entre sub-redes e a Internet por meio da VM.</span><span class="sxs-lookup"><span data-stu-id="b8526-135">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="b8526-136">az vm create</span><span class="sxs-lookup"><span data-stu-id="b8526-136">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="b8526-137">Cria uma máquina virtual e anexa o NIC a ela.</span><span class="sxs-lookup"><span data-stu-id="b8526-137">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="b8526-138">Este comando também especifica a imagem de máquina virtual a ser usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="b8526-138">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="b8526-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="b8526-139">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="b8526-140">Exclui um grupo de recursos e todos os seus recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="b8526-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b8526-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8526-141">Next steps</span></span>

<span data-ttu-id="b8526-142">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b8526-142">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="b8526-143">Exemplos adicionais de script de CLI de rede podem ser encontrados na [Documentação de visão geral da rede do Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="b8526-143">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>