---
title: "exemplo de script CLI aaaAzure - o tráfego de rede VM de filtro | Microsoft Docs"
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
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="93170-103">Filtrar o tráfego de entrada e saída de rede da VM</span><span class="sxs-lookup"><span data-stu-id="93170-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="93170-104">Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="93170-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="93170-105">O tráfego de rede de entrada sub-rede front-end toohello tooHTTP limitado, HTTPS e SSH, enquanto a saída de tráfego toohello Internet de sub-rede de back-end de saudação não é permitida.</span><span class="sxs-lookup"><span data-stu-id="93170-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="93170-106">Depois de executar o script hello, você terá uma máquina virtual com dois NICs.</span><span class="sxs-lookup"><span data-stu-id="93170-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="93170-107">Cada NIC é conectado tooa outra sub-rede.</span><span class="sxs-lookup"><span data-stu-id="93170-107">Each NIC is connected tooa different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="93170-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="93170-108">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="93170-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="93170-109">Clean up deployment</span></span> 

<span data-ttu-id="93170-110">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="93170-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="93170-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="93170-111">Script explanation</span></span>

<span data-ttu-id="93170-112">Esse script usa Olá toocreate comandos a seguir, um grupo de recursos, a rede virtual e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="93170-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="93170-113">Cada comando na tabela Olá vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="93170-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="93170-114">Command</span><span class="sxs-lookup"><span data-stu-id="93170-114">Command</span></span> | <span data-ttu-id="93170-115">Observações</span><span class="sxs-lookup"><span data-stu-id="93170-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="93170-116">az group create</span><span class="sxs-lookup"><span data-stu-id="93170-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="93170-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="93170-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="93170-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="93170-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="93170-119">Cria uma rede virtual do Azure e uma sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="93170-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="93170-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="93170-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="93170-121">Cria uma sub-rede back-end.</span><span class="sxs-lookup"><span data-stu-id="93170-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="93170-122">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="93170-122">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="93170-123">Associa os NSGs toosubnets.</span><span class="sxs-lookup"><span data-stu-id="93170-123">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="93170-124">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="93170-124">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="93170-125">Cria um tooaccess endereço IP público Olá VM de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="93170-125">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="93170-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="93170-126">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="93170-127">Cria as interfaces de rede virtual e os conecta sub-redes da rede virtual toohello de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="93170-127">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="93170-128">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="93170-128">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="93170-129">Cria grupos de segurança de rede (NSG) que estão associados toohello sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="93170-129">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="93170-130">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="93170-130">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="93170-131">Cria regras NSG que permitam ou bloqueiem as sub-redes de toospecific portas específicas.</span><span class="sxs-lookup"><span data-stu-id="93170-131">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="93170-132">az vm create</span><span class="sxs-lookup"><span data-stu-id="93170-132">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="93170-133">Cria máquinas virtuais e anexa um tooeach NIC VM.</span><span class="sxs-lookup"><span data-stu-id="93170-133">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="93170-134">Esse comando também especifica Olá toouse de imagem de máquina virtual e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="93170-134">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="93170-135">az group delete</span><span class="sxs-lookup"><span data-stu-id="93170-135">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="93170-136">Exclui um grupo de recursos e todos os seus recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="93170-136">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="93170-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="93170-137">Next steps</span></span>

<span data-ttu-id="93170-138">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="93170-138">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="93170-139">Exemplos de script CLI rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="93170-139">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
