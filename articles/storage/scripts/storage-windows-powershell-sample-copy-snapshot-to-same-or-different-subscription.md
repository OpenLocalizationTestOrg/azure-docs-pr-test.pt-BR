---
title: "aaaAzure exemplo de Script do PowerShell - instantâneo de cópia (mover) de um disco gerenciado toosame ou assinatura diferente | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - instantâneo de cópia (mover) de um disco gerenciado toosame ou assinatura diferente"
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
ms.openlocfilehash: 7a3565356f13cb93759dec7ef9d0357e04c3410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="4231b-103">Copiar um instantâneo de um disco gerenciado para a mesma assinatura ou outra assinatura com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4231b-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="4231b-104">Esse script cria uma cópia de um instantâneo no hello mesmo mesma assinatura ou assinatura diferente.</span><span class="sxs-lookup"><span data-stu-id="4231b-104">This script creates a copy of a snapshot in hello same same subscription or different subscription.</span></span> <span data-ttu-id="4231b-105">Use este toomove script uma assinatura de toodifferent de instantâneo para retenção de dados.</span><span class="sxs-lookup"><span data-stu-id="4231b-105">Use this script toomove a snapshot toodifferent subscription for data retention.</span></span> <span data-ttu-id="4231b-106">O armazenamento de instantâneos em outra assinatura protege contra a exclusão acidental de instantâneos em sua assinatura principal.</span><span class="sxs-lookup"><span data-stu-id="4231b-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4231b-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="4231b-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="4231b-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="4231b-108">Script explanation</span></span>

<span data-ttu-id="4231b-109">Esse script usa a seguinte comandos toocreate um instantâneo na assinatura de destino hello usando Olá Id do instantâneo de origem hello.</span><span class="sxs-lookup"><span data-stu-id="4231b-109">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="4231b-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="4231b-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4231b-111">Command</span><span class="sxs-lookup"><span data-stu-id="4231b-111">Command</span></span> | <span data-ttu-id="4231b-112">Observações</span><span class="sxs-lookup"><span data-stu-id="4231b-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4231b-113">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="4231b-113">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="4231b-114">Cria uma configuração de instantâneo que é usada para a criação do instantâneo.</span><span class="sxs-lookup"><span data-stu-id="4231b-114">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="4231b-115">Ele inclui a Id de instantâneo de pai hello e local que é o mesmo que o instantâneo do pai de saudação do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4231b-115">It includes hello resource Id of hello parent snapshot and location that is same as hello parent snapshot.</span></span>  |
| [<span data-ttu-id="4231b-116">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="4231b-116">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="4231b-117">Cria um instantâneo usando uma configuração de instantâneo, o nome do instantâneo e o nome do grupo de recursos passados como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="4231b-117">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="4231b-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4231b-118">Next steps</span></span>

[<span data-ttu-id="4231b-119">Criar uma máquina virtual com base em um instantâneo</span><span class="sxs-lookup"><span data-stu-id="4231b-119">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="4231b-120">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4231b-120">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4231b-121">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4231b-121">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
