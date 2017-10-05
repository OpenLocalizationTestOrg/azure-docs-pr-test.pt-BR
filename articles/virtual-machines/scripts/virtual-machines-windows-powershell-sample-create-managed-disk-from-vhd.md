---
title: "Amostra de script do Azure PowerShell – Criar um disco gerenciado com base em um arquivo VHD em uma conta de armazenamento na mesma assinatura ou em outra assinatura | Microsoft Docs"
description: "Amostra de script do Azure PowerShell – Criar um disco gerenciado com base em um arquivo VHD em uma conta de armazenamento na mesma assinatura ou em outra assinatura"
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
ms.openlocfilehash: 728def40a3eb132537decbd099fa71f4544c6b87
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="5c2d9-103">Criar um disco gerenciado com base em um arquivo VHD em uma conta de armazenamento na mesma assinatura ou em outra assinatura com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c2d9-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="5c2d9-104">Esse script cria um disco gerenciado com base em um arquivo VHD em uma conta de armazenamento na mesma assinatura ou em outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="5c2d9-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="5c2d9-105">Use esse script para importar um VHD especializado (não generalizado/do Sysprep) para um disco do sistema operacional gerenciado para criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5c2d9-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="5c2d9-106">Além disso, use-o para importar um VHD de dados para um disco de dados gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5c2d9-106">Also, use it to import a data VHD to managed data disk.</span></span> 

<span data-ttu-id="5c2d9-107">Não crie vários discos gerenciados idênticos com base em um arquivo VHD em um curto período.</span><span class="sxs-lookup"><span data-stu-id="5c2d9-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="5c2d9-108">Para criar discos gerenciados com base em um arquivo VHD, o instantâneo de blob do arquivo VHD é criado e, em seguida, é usado para criar discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5c2d9-108">To create managed disks from a vhd file, blob snapshot of the vhd file is created and then it is used to create managed disks.</span></span> <span data-ttu-id="5c2d9-109">Apenas um único instantâneo de blob pode ser criado em um minuto, o que causa falhas na criação do disco devido à limitação.</span><span class="sxs-lookup"><span data-stu-id="5c2d9-109">Only one blob snapshot can be created in a minute that causes disk creation failures due to throttling.</span></span> <span data-ttu-id="5c2d9-110">Para evitar essa limitação, crie um [instantâneo gerenciado com base no arquivo VHD](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) e, em seguida, use o instantâneo gerenciado para criar vários discos gerenciados em um curto período.</span><span class="sxs-lookup"><span data-stu-id="5c2d9-110">To avoid this throttling, create a [managed snapshot from the vhd file](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use the managed snapshot to create multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5c2d9-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="5c2d9-111">Sample script</span></span>

<span data-ttu-id="5c2d9-112">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Criar um disco gerenciado com base em um VHD")]</span><span class="sxs-lookup"><span data-stu-id="5c2d9-112">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="5c2d9-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="5c2d9-113">Script explanation</span></span>

<span data-ttu-id="5c2d9-114">Esse script usa os comandos a seguir para criar um disco gerenciado com base em um VHD em outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="5c2d9-114">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="5c2d9-115">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="5c2d9-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5c2d9-116">Command</span><span class="sxs-lookup"><span data-stu-id="5c2d9-116">Command</span></span> | <span data-ttu-id="5c2d9-117">Observações</span><span class="sxs-lookup"><span data-stu-id="5c2d9-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5c2d9-118">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="5c2d9-118">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="5c2d9-119">Cria uma configuração de disco que é usada para a criação do disco.</span><span class="sxs-lookup"><span data-stu-id="5c2d9-119">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="5c2d9-120">Ele inclui o tipo de armazenamento, o local, a ID do recurso da conta de armazenamento em que o VHD pai está armazenado e o URI VHD do VHD pai.</span><span class="sxs-lookup"><span data-stu-id="5c2d9-120">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="5c2d9-121">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="5c2d9-121">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="5c2d9-122">Cria um disco utilizando a configuração do disco, o nome do disco e o nome do grupo de recursos passados como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="5c2d9-122">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5c2d9-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c2d9-123">Next steps</span></span>

[<span data-ttu-id="5c2d9-124">Criar uma máquina virtual anexando um disco gerenciado como um disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="5c2d9-124">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="5c2d9-125">Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5c2d9-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5c2d9-126">Amostras de script do PowerShell da máquina virtual adicionais podem ser encontrados na [documentação da VM Windows do Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c2d9-126">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>