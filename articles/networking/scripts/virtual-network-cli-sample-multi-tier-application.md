---
title: "Exemplo de script da CLI do Azure - Criar uma rede para aplicativos de várias camadas | Microsoft Docs"
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
ms.openlocfilehash: de65d820f2d9eea49b58185c81d815675fd76740
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="5dfe9-103">Criar uma rede para aplicativos de várias camadas</span><span class="sxs-lookup"><span data-stu-id="5dfe9-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="5dfe9-104">Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="5dfe9-105">O tráfego para a sub-rede de front-end é limitado a HTTP e SSH, enquanto o tráfego para a sub-rede de back-end é limitado a MySQL, porta 3306.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="5dfe9-106">Depois de executar o script, você terá duas máquinas virtuais, um em cada sub-rede, nas quais você pode implantar o servidor Web e o software MySQL.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="5dfe9-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="5dfe9-107">Sample script</span></span>


<span data-ttu-id="5dfe9-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Rede virtual para aplicativos de várias camadas")]</span><span class="sxs-lookup"><span data-stu-id="5dfe9-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5dfe9-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="5dfe9-109">Clean up deployment</span></span> 

<span data-ttu-id="5dfe9-110">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="5dfe9-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="5dfe9-111">Script explanation</span></span>

<span data-ttu-id="5dfe9-112">Este script usa os comandos a seguir para criar um grupo de recursos, uma rede virtual e grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="5dfe9-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="5dfe9-114">Command</span><span class="sxs-lookup"><span data-stu-id="5dfe9-114">Command</span></span> | <span data-ttu-id="5dfe9-115">Observações</span><span class="sxs-lookup"><span data-stu-id="5dfe9-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5dfe9-116">az group create</span><span class="sxs-lookup"><span data-stu-id="5dfe9-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="5dfe9-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5dfe9-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="5dfe9-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="5dfe9-119">Cria uma rede virtual do Azure e uma sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="5dfe9-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="5dfe9-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="5dfe9-121">Cria uma sub-rede back-end.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="5dfe9-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="5dfe9-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="5dfe9-123">Cria um endereço IP público para acessar a VM da Internet.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="5dfe9-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="5dfe9-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="5dfe9-125">Cria as interfaces de rede virtual e as anexa às sub-redes de front-end e back-end da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-125">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="5dfe9-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="5dfe9-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="5dfe9-127">Cria NSG (grupos de segurança de rede) associados às sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-127">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="5dfe9-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="5dfe9-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="5dfe9-129">Cria regras NSG que permitem ou bloqueiam portas específicas para sub-redes específicas.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-129">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="5dfe9-130">az vm create</span><span class="sxs-lookup"><span data-stu-id="5dfe9-130">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="5dfe9-131">Cria máquinas virtuais e anexa um NIC a cada VM.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-131">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="5dfe9-132">Este comando também especifica a imagem de máquina virtual a ser usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-132">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="5dfe9-133">az group delete</span><span class="sxs-lookup"><span data-stu-id="5dfe9-133">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="5dfe9-134">Exclui um grupo de recursos e todos os seus recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="5dfe9-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5dfe9-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5dfe9-135">Next steps</span></span>

<span data-ttu-id="5dfe9-136">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5dfe9-136">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="5dfe9-137">Exemplos adicionais de script de CLI de rede podem ser encontrados na [Documentação de visão geral da rede do Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="5dfe9-137">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>