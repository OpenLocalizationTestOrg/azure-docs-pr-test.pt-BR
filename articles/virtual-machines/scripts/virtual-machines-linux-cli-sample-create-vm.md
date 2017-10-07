---
title: aaaAzure exemplo de Script CLI - criar uma VM do Linux | Microsoft Docs
description: "Exemplo de script da CLI do Azure - Criar uma máquina virtual Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c9855204a85cc0f6cd758a1d20121fbeea070943
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="65877-103">Criar uma máquina virtual totalmente configurada</span><span class="sxs-lookup"><span data-stu-id="65877-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="65877-104">Este script cria uma Máquina Virtual do Azure com um sistema operacional Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="65877-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="65877-105">Depois de executar o script hello, você pode acessar a máquina virtual de saudação via SSH.</span><span class="sxs-lookup"><span data-stu-id="65877-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="65877-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="65877-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="65877-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="65877-107">Clean up deployment</span></span> 

<span data-ttu-id="65877-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="65877-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="65877-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="65877-109">Script explanation</span></span>

<span data-ttu-id="65877-110">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="65877-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="65877-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="65877-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="65877-112">Command</span><span class="sxs-lookup"><span data-stu-id="65877-112">Command</span></span> | <span data-ttu-id="65877-113">Observações</span><span class="sxs-lookup"><span data-stu-id="65877-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="65877-114">az group create</span><span class="sxs-lookup"><span data-stu-id="65877-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="65877-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="65877-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="65877-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="65877-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="65877-117">Cria uma sub-rede e uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="65877-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="65877-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="65877-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="65877-119">Cria um endereço IP público com um endereço IP estático e um nome DNS associado.</span><span class="sxs-lookup"><span data-stu-id="65877-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="65877-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="65877-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="65877-121">Cria um grupo de segurança de rede (NSG), que é um limite de segurança entre a máquina de virtual de internet e Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="65877-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="65877-122">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="65877-122">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="65877-123">Cria um tooallow de regra NSG o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="65877-123">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="65877-124">Neste exemplo, a porta 22 é aberta para o tráfego SSH.</span><span class="sxs-lookup"><span data-stu-id="65877-124">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="65877-125">az network nic create</span><span class="sxs-lookup"><span data-stu-id="65877-125">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="65877-126">Cria uma placa de rede virtual e anexa-rede virtual toohello, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="65877-126">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="65877-127">az vm create</span><span class="sxs-lookup"><span data-stu-id="65877-127">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="65877-128">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="65877-128">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="65877-129">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="65877-129">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="65877-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="65877-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="65877-131">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="65877-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="65877-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65877-132">Next steps</span></span>

<span data-ttu-id="65877-133">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65877-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="65877-134">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65877-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
