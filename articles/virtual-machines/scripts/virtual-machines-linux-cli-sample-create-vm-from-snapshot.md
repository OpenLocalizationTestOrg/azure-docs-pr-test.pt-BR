---
title: "aaaAzure exemplo de Script CLI - criar uma máquina virtual de um instantâneo | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – Criar uma VM de um instantâneo"
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
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="ae850-103">Criar uma máquina virtual de um instantâneo com a CLI</span><span class="sxs-lookup"><span data-stu-id="ae850-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="ae850-104">Esse script cria uma máquina virtual de um instantâneo de um disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="ae850-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ae850-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ae850-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ae850-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="ae850-106">Clean up deployment</span></span> 

<span data-ttu-id="ae850-107">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ae850-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ae850-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="ae850-108">Script explanation</span></span>

<span data-ttu-id="ae850-109">Esse script usa Olá seguir comandos toocreate um disco gerenciado, máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="ae850-109">This script uses hello following commands toocreate a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="ae850-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="ae850-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ae850-111">Command</span><span class="sxs-lookup"><span data-stu-id="ae850-111">Command</span></span> | <span data-ttu-id="ae850-112">Observações</span><span class="sxs-lookup"><span data-stu-id="ae850-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ae850-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="ae850-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="ae850-114">Obtém o instantâneo usando o nome do instantâneo e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ae850-114">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="ae850-115">Propriedade de ID de objeto retornado de hello é usado toocreate um disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="ae850-115">Id property of hello returned object is used toocreate a managed disk.</span></span>  |
| [<span data-ttu-id="ae850-116">az disk create</span><span class="sxs-lookup"><span data-stu-id="ae850-116">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="ae850-117">Cria discos gerenciados de um instantâneo usando ID de instantâneo, nome do disco, tipo de armazenamento e tamanho</span><span class="sxs-lookup"><span data-stu-id="ae850-117">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="ae850-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="ae850-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ae850-119">Cria uma VM usando um disco do sistema operacional gerenciado</span><span class="sxs-lookup"><span data-stu-id="ae850-119">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ae850-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ae850-120">Next steps</span></span>

<span data-ttu-id="ae850-121">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ae850-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ae850-122">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ae850-122">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
