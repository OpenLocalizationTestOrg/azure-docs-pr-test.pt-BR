---
title: "aaaAzure exemplo de Script do PowerShell - criar um disco gerenciado de um instantâneo | Microsoft Docs"
description: "Amostra de script do Azure PowerShell – Criar um disco gerenciado com base em um instantâneo"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 4fa34a8d6c67171083fba9a9ad73ecca5e0f0229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="cf547-103">Criar um disco gerenciado com base em um instantâneo com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf547-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="cf547-104">Esse script cria um disco gerenciado com base em um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="cf547-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="cf547-105">Use-toorestore uma máquina virtual de instantâneos do sistema operacional e discos de dados.</span><span class="sxs-lookup"><span data-stu-id="cf547-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="cf547-106">Crie discos gerenciados do sistema operacional e de dados com base nos respectivos instantâneos e, em seguida, crie uma nova máquina virtual anexando os discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cf547-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="cf547-107">Restaure também discos de dados de uma VM existente anexando os discos de dados criados com base em instantâneos.</span><span class="sxs-lookup"><span data-stu-id="cf547-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="cf547-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="cf547-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="cf547-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="cf547-109">Script explanation</span></span>

<span data-ttu-id="cf547-110">Esse script usará os seguintes comandos toocreate um disco gerenciado de um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="cf547-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="cf547-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="cf547-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="cf547-112">Command</span><span class="sxs-lookup"><span data-stu-id="cf547-112">Command</span></span> | <span data-ttu-id="cf547-113">Observações</span><span class="sxs-lookup"><span data-stu-id="cf547-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cf547-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="cf547-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="cf547-115">Obtém as propriedades do instantâneo.</span><span class="sxs-lookup"><span data-stu-id="cf547-115">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="cf547-116">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="cf547-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="cf547-117">Cria a configuração do disco que é usada para criação do disco.</span><span class="sxs-lookup"><span data-stu-id="cf547-117">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="cf547-118">Ele inclui recursos Olá Id do instantâneo Olá pai local que é o mesmo local de saudação do tipo de armazenamento de instantâneo e hello pai.</span><span class="sxs-lookup"><span data-stu-id="cf547-118">It includes hello resource Id of hello parent snapshot, location that is same as hello location of parent snapshot and hello storage type.</span></span>  |
| [<span data-ttu-id="cf547-119">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="cf547-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="cf547-120">Cria um disco utilizando a configuração do disco, o nome do disco e o nome do grupo de recursos passados como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="cf547-120">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="cf547-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cf547-121">Next steps</span></span>

[<span data-ttu-id="cf547-122">Criar uma máquina virtual com base em um disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="cf547-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="cf547-123">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cf547-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="cf547-124">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cf547-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
