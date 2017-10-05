---
title: "Amostra de script do Azure PowerShell – Criar um disco gerenciado com base em um instantâneo | Microsoft Docs"
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
ms.openlocfilehash: 9105d9dc06eea33b3a4e1eeea7fd793919166c9b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="1d58e-103">Criar um disco gerenciado com base em um instantâneo com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d58e-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="1d58e-104">Esse script cria um disco gerenciado com base em um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="1d58e-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="1d58e-105">Use-o para restaurar uma máquina virtual de instantâneos do sistema operacional e de discos de dados.</span><span class="sxs-lookup"><span data-stu-id="1d58e-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="1d58e-106">Crie discos gerenciados do sistema operacional e de dados com base nos respectivos instantâneos e, em seguida, crie uma nova máquina virtual anexando os discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1d58e-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="1d58e-107">Restaure também discos de dados de uma VM existente anexando os discos de dados criados com base em instantâneos.</span><span class="sxs-lookup"><span data-stu-id="1d58e-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1d58e-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="1d58e-108">Sample script</span></span>

<span data-ttu-id="1d58e-109">[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Criar um disco gerenciado com base em um instantâneo")]</span><span class="sxs-lookup"><span data-stu-id="1d58e-109">[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="1d58e-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="1d58e-110">Script explanation</span></span>

<span data-ttu-id="1d58e-111">Esse script usa os comandos a seguir para criar um disco gerenciado com base em um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="1d58e-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="1d58e-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="1d58e-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1d58e-113">Command</span><span class="sxs-lookup"><span data-stu-id="1d58e-113">Command</span></span> | <span data-ttu-id="1d58e-114">Observações</span><span class="sxs-lookup"><span data-stu-id="1d58e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1d58e-115">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="1d58e-115">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="1d58e-116">Obtém as propriedades do instantâneo.</span><span class="sxs-lookup"><span data-stu-id="1d58e-116">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="1d58e-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="1d58e-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="1d58e-118">Cria uma configuração de disco que é usada para a criação do disco.</span><span class="sxs-lookup"><span data-stu-id="1d58e-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="1d58e-119">Inclui a ID do recurso do instantâneo pai, o local que é o mesmo local do instantâneo pai e o tipo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1d58e-119">It includes the resource Id of the parent snapshot, location that is same as the location of parent snapshot and the storage type.</span></span>  |
| [<span data-ttu-id="1d58e-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="1d58e-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="1d58e-121">Cria um disco utilizando a configuração do disco, o nome do disco e o nome do grupo de recursos passados como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="1d58e-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="1d58e-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1d58e-122">Next steps</span></span>

[<span data-ttu-id="1d58e-123">Criar uma máquina virtual com base em um disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="1d58e-123">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="1d58e-124">Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1d58e-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1d58e-125">Amostras de script do PowerShell da máquina virtual adicionais podem ser encontrados na [documentação da VM Windows do Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d58e-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>