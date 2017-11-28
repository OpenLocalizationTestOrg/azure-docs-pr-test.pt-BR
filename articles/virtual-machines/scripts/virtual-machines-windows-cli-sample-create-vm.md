---
title: aaaAzure exemplo de Script CLI - criar uma VM do Windows Server | Microsoft Docs
description: "Exemplo de script da CLI do Azure - Criar uma máquina virtual do Windows Server"
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
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f4cb431a68c911f877f5af87c393849bd8d2676a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="1b812-103">Criar uma máquina virtual com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1b812-103">Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="1b812-104">Esse script cria uma Máquina Virtual do Azure que executa o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="1b812-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="1b812-105">Depois de executar o script hello, você pode acessar a máquina virtual de saudação por meio de uma conexão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="1b812-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1b812-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="1b812-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1b812-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="1b812-107">Clean up deployment</span></span> 

<span data-ttu-id="1b812-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="1b812-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="1b812-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="1b812-109">Script explanation</span></span>

<span data-ttu-id="1b812-110">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="1b812-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="1b812-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="1b812-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1b812-112">Command</span><span class="sxs-lookup"><span data-stu-id="1b812-112">Command</span></span> | <span data-ttu-id="1b812-113">Observações</span><span class="sxs-lookup"><span data-stu-id="1b812-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1b812-114">az group create</span><span class="sxs-lookup"><span data-stu-id="1b812-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1b812-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="1b812-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1b812-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="1b812-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="1b812-117">Cria uma sub-rede e uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b812-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="1b812-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="1b812-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="1b812-119">Cria um endereço IP público com um endereço IP estático e um nome DNS associado.</span><span class="sxs-lookup"><span data-stu-id="1b812-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="1b812-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="1b812-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="1b812-121">Cria um grupo de segurança de rede (NSG), que é um limite de segurança entre a máquina de virtual de internet e Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="1b812-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="1b812-122">az network nic create</span><span class="sxs-lookup"><span data-stu-id="1b812-122">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="1b812-123">Cria uma placa de rede virtual e anexa-rede virtual toohello, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="1b812-123">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="1b812-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="1b812-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="1b812-125">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="1b812-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="1b812-126">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="1b812-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="1b812-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="1b812-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="1b812-128">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="1b812-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1b812-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b812-129">Next steps</span></span>

<span data-ttu-id="1b812-130">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1b812-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1b812-131">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b812-131">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
