---
title: "script CLI aaaAzure exemplo - criar uma rede para aplicativos de várias camadas | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Criar uma rede virtual para aplicativos de várias camadas."
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
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="6d4a4-103">Criar uma rede para aplicativos de várias camadas</span><span class="sxs-lookup"><span data-stu-id="6d4a4-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="6d4a4-104">Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="6d4a4-105">Sub-rede front-end do tráfego toohello é tooHTTP limitada e SSH, enquanto o tráfego toohello sub-rede back-end é tooMySQL limitado, porta 3306.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="6d4a4-106">Após o script hello em execução, você terá duas máquinas virtuais em cada sub-rede que você pode implantar o servidor web e o software MySQL.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="6d4a4-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="6d4a4-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6d4a4-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="6d4a4-108">Clean up deployment</span></span> 

<span data-ttu-id="6d4a4-109">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="6d4a4-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="6d4a4-110">Script explanation</span></span>

<span data-ttu-id="6d4a4-111">Esse script usa Olá toocreate comandos a seguir, um grupo de recursos, a rede virtual e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="6d4a4-112">Cada comando na tabela Olá vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="6d4a4-113">Command</span><span class="sxs-lookup"><span data-stu-id="6d4a4-113">Command</span></span> | <span data-ttu-id="6d4a4-114">Observações</span><span class="sxs-lookup"><span data-stu-id="6d4a4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6d4a4-115">az group create</span><span class="sxs-lookup"><span data-stu-id="6d4a4-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="6d4a4-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6d4a4-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="6d4a4-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="6d4a4-118">Cria uma rede virtual do Azure e uma sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="6d4a4-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="6d4a4-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="6d4a4-120">Cria uma sub-rede back-end.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-120">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="6d4a4-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="6d4a4-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="6d4a4-122">Cria um tooaccess endereço IP público Olá VM de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="6d4a4-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="6d4a4-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="6d4a4-124">Cria as interfaces de rede virtual e os conecta sub-redes da rede virtual toohello de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-124">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="6d4a4-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="6d4a4-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="6d4a4-126">Cria grupos de segurança de rede (NSG) que estão associados toohello sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-126">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="6d4a4-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="6d4a4-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="6d4a4-128">Cria regras NSG que permitam ou bloqueiem as sub-redes de toospecific portas específicas.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-128">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="6d4a4-129">az vm create</span><span class="sxs-lookup"><span data-stu-id="6d4a4-129">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="6d4a4-130">Cria máquinas virtuais e anexa um tooeach NIC VM.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-130">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="6d4a4-131">Esse comando também especifica Olá toouse de imagem de máquina virtual e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-131">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="6d4a4-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="6d4a4-132">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="6d4a4-133">Exclui um grupo de recursos e todos os seus recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="6d4a4-133">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6d4a4-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d4a4-134">Next steps</span></span>

<span data-ttu-id="6d4a4-135">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6d4a4-135">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="6d4a4-136">Exemplos de script CLI rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="6d4a4-136">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
