---
title: "aaaAzure exemplo de Script CLI - criar uma máquina virtual, anexando um disco gerenciado como disco do sistema operacional | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – Criar uma VM, anexando um disco gerenciado como disco do sistema operacional"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="d3d67-103">Criar uma máquina virtual usando um disco de sistema operacional gerenciado existente com a CLI</span><span class="sxs-lookup"><span data-stu-id="d3d67-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="d3d67-104">Esse script cria uma máquina virtual anexando um disco gerenciado existente como disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="d3d67-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="d3d67-105">Use esse script em cenários anteriores:</span><span class="sxs-lookup"><span data-stu-id="d3d67-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="d3d67-106">Criar uma VM de um disco de sistema operacional gerenciado existente que foi copiado de um disco gerenciado em uma assinatura diferente</span><span class="sxs-lookup"><span data-stu-id="d3d67-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="d3d67-107">Criar uma VM de um disco gerenciado existente que foi criado de um arquivo VHD especializado</span><span class="sxs-lookup"><span data-stu-id="d3d67-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="d3d67-108">Criar uma VM de um disco do sistema operacional gerenciado existente que foi criado de um instantâneo</span><span class="sxs-lookup"><span data-stu-id="d3d67-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d3d67-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="d3d67-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d3d67-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="d3d67-110">Clean up deployment</span></span> 

<span data-ttu-id="d3d67-111">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="d3d67-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d3d67-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="d3d67-112">Script explanation</span></span>

<span data-ttu-id="d3d67-113">Esse script usa Olá comandos tooget gerenciado disco propriedades a seguir, anexar um disco gerenciado tooa nova VM e criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d3d67-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="d3d67-114">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="d3d67-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d3d67-115">Command</span><span class="sxs-lookup"><span data-stu-id="d3d67-115">Command</span></span> | <span data-ttu-id="d3d67-116">Observações</span><span class="sxs-lookup"><span data-stu-id="d3d67-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d3d67-117">az disk show</span><span class="sxs-lookup"><span data-stu-id="d3d67-117">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="d3d67-118">Obtém propriedades de disco gerenciado usando o nome do disco e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d3d67-118">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="d3d67-119">Propriedade ID é usada tooattach tooa um disco gerenciado nova VM</span><span class="sxs-lookup"><span data-stu-id="d3d67-119">Id property is used tooattach a managed disk tooa new VM</span></span> |
| [<span data-ttu-id="d3d67-120">az vm create</span><span class="sxs-lookup"><span data-stu-id="d3d67-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d3d67-121">Cria uma VM usando um disco do sistema operacional gerenciado</span><span class="sxs-lookup"><span data-stu-id="d3d67-121">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="d3d67-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d3d67-122">Next steps</span></span>

<span data-ttu-id="d3d67-123">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d3d67-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d3d67-124">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3d67-124">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
