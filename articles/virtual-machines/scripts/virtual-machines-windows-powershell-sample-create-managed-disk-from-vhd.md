---
title: aaaAzure exemplo de Script do PowerShell - criar um disco gerenciado de um arquivo VHD em uma conta de armazenamento na assinatura iguais ou diferente | Microsoft Docs
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
ms.openlocfilehash: 47acff274cdf79d6fc3cd685cda01cad3d14ca8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="8feb6-103">Criar um disco gerenciado com base em um arquivo VHD em uma conta de armazenamento na mesma assinatura ou em outra assinatura com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8feb6-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="8feb6-104">Esse script cria um disco gerenciado com base em um arquivo VHD em uma conta de armazenamento na mesma assinatura ou em outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="8feb6-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="8feb6-105">Use este script tooimport um especializado toocreate de disco do toomanaged SO de VHD (não generalizado/com Sysprep) uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8feb6-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="8feb6-106">Além disso, use tooimport um disco de dados toomanaged dados VHD.</span><span class="sxs-lookup"><span data-stu-id="8feb6-106">Also, use it tooimport a data VHD toomanaged data disk.</span></span> 

<span data-ttu-id="8feb6-107">Não crie vários discos gerenciados idênticos com base em um arquivo VHD em um curto período.</span><span class="sxs-lookup"><span data-stu-id="8feb6-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="8feb6-108">toocreate discos gerenciado de um arquivo vhd, instantâneo de blob do arquivo de vhd Olá é criado e, em seguida, é usado toocreate gerenciado discos.</span><span class="sxs-lookup"><span data-stu-id="8feb6-108">toocreate managed disks from a vhd file, blob snapshot of hello vhd file is created and then it is used toocreate managed disks.</span></span> <span data-ttu-id="8feb6-109">Instantâneo de blob apenas uma pode ser criado em um minuto que causa falhas na criação do disco toothrottling vencimento.</span><span class="sxs-lookup"><span data-stu-id="8feb6-109">Only one blob snapshot can be created in a minute that causes disk creation failures due toothrottling.</span></span> <span data-ttu-id="8feb6-110">tooavoid essa limitação, criar um [gerenciado instantâneo de arquivo de vhd Olá](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) e, em seguida, use Olá gerenciados instantâneo toocreate vários discos gerenciados em curto período de tempo.</span><span class="sxs-lookup"><span data-stu-id="8feb6-110">tooavoid this throttling, create a [managed snapshot from hello vhd file](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use hello managed snapshot toocreate multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8feb6-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="8feb6-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="8feb6-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="8feb6-112">Script explanation</span></span>

<span data-ttu-id="8feb6-113">Esse script usará os seguintes comandos toocreate um disco gerenciado em um VHD em assinatura diferente.</span><span class="sxs-lookup"><span data-stu-id="8feb6-113">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="8feb6-114">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="8feb6-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8feb6-115">Command</span><span class="sxs-lookup"><span data-stu-id="8feb6-115">Command</span></span> | <span data-ttu-id="8feb6-116">Observações</span><span class="sxs-lookup"><span data-stu-id="8feb6-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8feb6-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="8feb6-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="8feb6-118">Cria a configuração do disco que é usada para criação do disco.</span><span class="sxs-lookup"><span data-stu-id="8feb6-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="8feb6-119">Ele inclui o tipo de armazenamento, local, Id Olá da conta de armazenamento onde o VHD pai de saudação está armazenada, URI do VHD de VHD pai de saudação do recurso.</span><span class="sxs-lookup"><span data-stu-id="8feb6-119">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="8feb6-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="8feb6-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="8feb6-121">Cria um disco utilizando a configuração do disco, o nome do disco e o nome do grupo de recursos passados como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="8feb6-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8feb6-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8feb6-122">Next steps</span></span>

[<span data-ttu-id="8feb6-123">Criar uma máquina virtual anexando um disco gerenciado como disco do SO</span><span class="sxs-lookup"><span data-stu-id="8feb6-123">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="8feb6-124">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8feb6-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8feb6-125">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8feb6-125">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
