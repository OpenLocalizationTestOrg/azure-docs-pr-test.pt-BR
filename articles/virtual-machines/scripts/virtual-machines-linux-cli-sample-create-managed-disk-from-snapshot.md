---
title: "aaaAzure exemplo de Script CLI - criar um disco gerenciado de um instantâneo | Microsoft Docs"
description: "Amostra de script da CLI do Azure – Criar um disco gerenciado com base em um instantâneo"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 549692f5027b3f50b0dd89fe701ebbf0f51d6031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="524ed-103">Criar um disco gerenciado com base em um instantâneo com a CLI</span><span class="sxs-lookup"><span data-stu-id="524ed-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="524ed-104">Esse script cria um disco gerenciado com base em um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="524ed-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="524ed-105">Use-toorestore uma máquina virtual de instantâneos do sistema operacional e discos de dados.</span><span class="sxs-lookup"><span data-stu-id="524ed-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="524ed-106">Crie discos gerenciados do sistema operacional e de dados com base nos respectivos instantâneos e, em seguida, crie uma nova máquina virtual anexando os discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="524ed-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="524ed-107">Restaure também discos de dados de uma VM existente anexando os discos de dados criados com base em instantâneos.</span><span class="sxs-lookup"><span data-stu-id="524ed-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="524ed-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="524ed-108">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="524ed-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="524ed-109">Script explanation</span></span>

<span data-ttu-id="524ed-110">Esse script usará os seguintes comandos toocreate um disco gerenciado de um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="524ed-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="524ed-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="524ed-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="524ed-112">Command</span><span class="sxs-lookup"><span data-stu-id="524ed-112">Command</span></span> | <span data-ttu-id="524ed-113">Observações</span><span class="sxs-lookup"><span data-stu-id="524ed-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="524ed-114">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="524ed-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="524ed-115">Obtém todas as propriedades de saudação de um instantâneo usando o nome hello e propriedades de grupo de recursos de instantâneo de saudação.</span><span class="sxs-lookup"><span data-stu-id="524ed-115">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="524ed-116">Propriedade ID é um disco gerenciado toocreate usado.</span><span class="sxs-lookup"><span data-stu-id="524ed-116">Id property is used toocreate managed disk.</span></span>  |
| [<span data-ttu-id="524ed-117">az disk create</span><span class="sxs-lookup"><span data-stu-id="524ed-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="524ed-118">Cria um disco gerenciado usando a Id de instantâneo de um instantâneo gerenciado</span><span class="sxs-lookup"><span data-stu-id="524ed-118">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="524ed-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="524ed-119">Next steps</span></span>

[<span data-ttu-id="524ed-120">Criar uma máquina virtual anexando um disco gerenciado como disco do SO</span><span class="sxs-lookup"><span data-stu-id="524ed-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="524ed-121">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="524ed-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="524ed-122">Máquinas virtuais adicionais e exemplos de script CLI de discos gerenciados podem ser encontrados no hello [documentação de VM do Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="524ed-122">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
