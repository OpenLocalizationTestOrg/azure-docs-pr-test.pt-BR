---
title: aaaAzure exemplo de Script do PowerShell - Copy (mover) gerenciado toosame discos ou assinatura diferente | Microsoft Docs
description: Exemplo de Script do PowerShell do Azure - Copy (mover) gerenciados discos toosame ou assinatura diferente
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 5a92118e10a14615e5b1713f1b90188b37b05305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="1a918-103">Discos de cópia gerenciada no hello mesmo assinatura ou uma assinatura diferente com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a918-103">Copy managed disks in hello same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="1a918-104">Esse script cria uma cópia de um disco gerenciado existente no hello mesma assinatura ou assinatura diferente.</span><span class="sxs-lookup"><span data-stu-id="1a918-104">This script creates a copy of an existing managed disk in hello same subscription or different subscription.</span></span> <span data-ttu-id="1a918-105">Olá novo disco é criado no hello mesmo região pai Olá gerenciados em disco.</span><span class="sxs-lookup"><span data-stu-id="1a918-105">hello new disk is created in hello same region as hello parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1a918-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="1a918-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="1a918-107">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="1a918-107">Script explanation</span></span>

<span data-ttu-id="1a918-108">Esse script usa a seguinte comandos toocreate um novo disco gerenciado na assinatura usando o destino Olá Olá Id da fonte de saudação gerenciados em disco.</span><span class="sxs-lookup"><span data-stu-id="1a918-108">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="1a918-109">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="1a918-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1a918-110">Command</span><span class="sxs-lookup"><span data-stu-id="1a918-110">Command</span></span> | <span data-ttu-id="1a918-111">Observações</span><span class="sxs-lookup"><span data-stu-id="1a918-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1a918-112">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="1a918-112">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="1a918-113">Cria a configuração do disco que é usada para criação do disco.</span><span class="sxs-lookup"><span data-stu-id="1a918-113">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="1a918-114">Ele inclui recursos de saudação Id do disco pai de saudação e local que é o mesmo local de saudação do disco pai.</span><span class="sxs-lookup"><span data-stu-id="1a918-114">It includes hello resource Id of hello parent disk and location that is same as hello location of parent disk.</span></span>  |
| [<span data-ttu-id="1a918-115">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="1a918-115">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="1a918-116">Cria um disco utilizando a configuração do disco, o nome do disco e o nome do grupo de recursos passados como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="1a918-116">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="1a918-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1a918-117">Next steps</span></span>

[<span data-ttu-id="1a918-118">Criar uma máquina virtual com base em um disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="1a918-118">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="1a918-119">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a918-119">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1a918-120">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1a918-120">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
