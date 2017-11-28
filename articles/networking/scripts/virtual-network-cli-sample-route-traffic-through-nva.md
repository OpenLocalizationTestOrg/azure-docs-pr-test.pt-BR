---
title: "exemplo de script CLI aaaAzure - rotear o tráfego por meio de um dispositivo de rede virtual | Microsoft Docs"
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="a51ba-103">Rotear o tráfego por meio de uma solução de virtualização de rede</span><span class="sxs-lookup"><span data-stu-id="a51ba-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="a51ba-104">Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="a51ba-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="a51ba-105">Ele também cria uma VM com tráfego tooroute habilitado entre duas sub-redes de saudação de encaminhamento IP.</span><span class="sxs-lookup"><span data-stu-id="a51ba-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="a51ba-106">Depois de executar o script hello, você pode implantar o software de rede, como um aplicativo de firewall, toohello VM.</span><span class="sxs-lookup"><span data-stu-id="a51ba-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="a51ba-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="a51ba-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a51ba-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="a51ba-108">Clean up deployment</span></span> 

<span data-ttu-id="a51ba-109">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a51ba-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="a51ba-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="a51ba-110">Script explanation</span></span>

<span data-ttu-id="a51ba-111">Esse script usa Olá toocreate comandos a seguir, um grupo de recursos, a rede virtual e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="a51ba-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="a51ba-112">Cada comando na tabela Olá vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="a51ba-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="a51ba-113">Command</span><span class="sxs-lookup"><span data-stu-id="a51ba-113">Command</span></span> | <span data-ttu-id="a51ba-114">Observações</span><span class="sxs-lookup"><span data-stu-id="a51ba-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a51ba-115">az group create</span><span class="sxs-lookup"><span data-stu-id="a51ba-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="a51ba-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="a51ba-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a51ba-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="a51ba-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="a51ba-118">Cria uma rede virtual do Azure e uma sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="a51ba-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="a51ba-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="a51ba-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="a51ba-120">Cria as sub-redes back-end e DMZ.</span><span class="sxs-lookup"><span data-stu-id="a51ba-120">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="a51ba-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="a51ba-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="a51ba-122">Cria um tooaccess endereço IP público Olá VM de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="a51ba-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="a51ba-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="a51ba-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="a51ba-124">Cria uma interface de rede virtual e habilita o encaminhamento IP nela.</span><span class="sxs-lookup"><span data-stu-id="a51ba-124">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="a51ba-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="a51ba-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="a51ba-126">Cria um grupo de segurança de rede (NSG).</span><span class="sxs-lookup"><span data-stu-id="a51ba-126">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="a51ba-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="a51ba-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="a51ba-128">Cria regras NSG que permitem que as portas HTTP e HTTPS de entrada toohello VM.</span><span class="sxs-lookup"><span data-stu-id="a51ba-128">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="a51ba-129">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="a51ba-129">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="a51ba-130">Associa Olá NSGs e toosubnets de tabelas de rota.</span><span class="sxs-lookup"><span data-stu-id="a51ba-130">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="a51ba-131">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="a51ba-131">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="a51ba-132">Cria uma tabela de rotas com todas as rotas.</span><span class="sxs-lookup"><span data-stu-id="a51ba-132">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="a51ba-133">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="a51ba-133">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="a51ba-134">Cria rotas tooroute tráfego entre as sub-redes e saudação da Internet por meio de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="a51ba-134">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="a51ba-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="a51ba-135">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="a51ba-136">Cria uma máquina virtual e anexa Olá NIC tooit.</span><span class="sxs-lookup"><span data-stu-id="a51ba-136">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="a51ba-137">Esse comando também especifica Olá toouse de imagem de máquina virtual e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="a51ba-137">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="a51ba-138">az group delete</span><span class="sxs-lookup"><span data-stu-id="a51ba-138">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="a51ba-139">Exclui um grupo de recursos e todos os seus recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="a51ba-139">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a51ba-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a51ba-140">Next steps</span></span>

<span data-ttu-id="a51ba-141">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a51ba-141">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="a51ba-142">Exemplos de script CLI rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="a51ba-142">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
