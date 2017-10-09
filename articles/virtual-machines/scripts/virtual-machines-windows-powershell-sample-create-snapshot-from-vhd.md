---
title: "aaaAzure exemplo de Script do PowerShell - criar um instantâneo de um VHD toocreate vários discos gerenciados idênticos em pouco tempo | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - criar um instantâneo de um VHD toocreate vários discos gerenciados idênticos em pouco tempo"
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
ms.openlocfilehash: 5f11793b3669df099b6c31dfdbe906c96ba51786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="a8b71-103">Criar um instantâneo de um VHD toocreate vários discos gerenciados idênticos em pouco tempo com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8b71-103">Create a snapshot from a VHD toocreate multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="a8b71-104">Esse script cria um instantâneo de um arquivo VHD em uma conta de armazenamento na mesma assinatura ou em uma diferente.</span><span class="sxs-lookup"><span data-stu-id="a8b71-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="a8b71-105">Use este script tooimport um instantâneo de tooa especializado (não generalizado/com Sysprep) VHD e use Olá instantâneo toocreate vários discos gerenciados idênticos em pouco tempo.</span><span class="sxs-lookup"><span data-stu-id="a8b71-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD tooa snapshot and then use hello snapshot toocreate multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="a8b71-106">Além disso, use tooimport um instantâneo dos dados VHD tooa e use Olá instantâneo toocreate vários discos gerenciados em pouco tempo.</span><span class="sxs-lookup"><span data-stu-id="a8b71-106">Also, use it tooimport a data VHD tooa snapshot and then use hello snapshot toocreate multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a8b71-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="a8b71-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="a8b71-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="a8b71-108">Script explanation</span></span>

<span data-ttu-id="a8b71-109">Esse script usará os seguintes comandos toocreate um disco gerenciado em um VHD em assinatura diferente.</span><span class="sxs-lookup"><span data-stu-id="a8b71-109">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="a8b71-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="a8b71-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a8b71-111">Command</span><span class="sxs-lookup"><span data-stu-id="a8b71-111">Command</span></span> | <span data-ttu-id="a8b71-112">Observações</span><span class="sxs-lookup"><span data-stu-id="a8b71-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a8b71-113">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="a8b71-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="a8b71-114">Cria a configuração do disco que é usada para criação do disco.</span><span class="sxs-lookup"><span data-stu-id="a8b71-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="a8b71-115">Inclui o tipo de armazenamento, local, Id Olá da conta de armazenamento onde está armazenado o VHD pai de saudação do recurso e URI do VHD do pai Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="a8b71-115">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, and VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="a8b71-116">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="a8b71-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="a8b71-117">Cria um disco utilizando a configuração do disco, o nome do disco e o nome do grupo de recursos passados como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="a8b71-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a8b71-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8b71-118">Next steps</span></span>

[<span data-ttu-id="a8b71-119">Criar um disco gerenciado a partir do instantâneo</span><span class="sxs-lookup"><span data-stu-id="a8b71-119">Create a managed disk from snapshot</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="a8b71-120">Criar uma máquina virtual anexando um disco gerenciado como disco do SO</span><span class="sxs-lookup"><span data-stu-id="a8b71-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="a8b71-121">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a8b71-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a8b71-122">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a8b71-122">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
