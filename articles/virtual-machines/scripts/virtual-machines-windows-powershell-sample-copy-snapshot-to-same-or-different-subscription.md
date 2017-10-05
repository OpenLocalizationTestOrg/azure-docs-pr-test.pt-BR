---
title: "Amostra de script do Azure PowerShell – Copiar (mover) um instantâneo de um disco gerenciado para a mesma assinatura ou outra assinatura | Microsoft Docs"
description: "Amostra de script do Azure PowerShell – Copiar (mover) um instantâneo de um disco gerenciado para a mesma assinatura ou outra assinatura"
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
ms.openlocfilehash: f7b4869669a2c5e840f9bd384dcd6d6096ba58e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="5dc07-103">Copiar um instantâneo de um disco gerenciado para a mesma assinatura ou outra assinatura com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5dc07-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="5dc07-104">Esse script cria uma cópia de um instantâneo na mesma assinatura ou em outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="5dc07-104">This script creates a copy of a snapshot in the same same subscription or different subscription.</span></span> <span data-ttu-id="5dc07-105">Use esse script para mover um instantâneo para outra assinatura para a retenção de dados.</span><span class="sxs-lookup"><span data-stu-id="5dc07-105">Use this script to move a snapshot to different subscription for data retention.</span></span> <span data-ttu-id="5dc07-106">O armazenamento de instantâneos em outra assinatura protege contra a exclusão acidental de instantâneos em sua assinatura principal.</span><span class="sxs-lookup"><span data-stu-id="5dc07-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5dc07-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="5dc07-107">Sample script</span></span>

<span data-ttu-id="5dc07-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copiar instantâneo")]</span><span class="sxs-lookup"><span data-stu-id="5dc07-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="5dc07-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="5dc07-109">Script explanation</span></span>

<span data-ttu-id="5dc07-110">Esse script usa os comandos a seguir para criar um instantâneo na assinatura de destino usando a ID do instantâneo de origem.</span><span class="sxs-lookup"><span data-stu-id="5dc07-110">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="5dc07-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="5dc07-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5dc07-112">Command</span><span class="sxs-lookup"><span data-stu-id="5dc07-112">Command</span></span> | <span data-ttu-id="5dc07-113">Observações</span><span class="sxs-lookup"><span data-stu-id="5dc07-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5dc07-114">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="5dc07-114">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="5dc07-115">Cria uma configuração de instantâneo que é usada para a criação do instantâneo.</span><span class="sxs-lookup"><span data-stu-id="5dc07-115">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="5dc07-116">Inclui a ID do recurso do instantâneo pai e o local que é o mesmo local do instantâneo pai.</span><span class="sxs-lookup"><span data-stu-id="5dc07-116">It includes the resource Id of the parent snapshot and location that is same as the parent snapshot.</span></span>  |
| [<span data-ttu-id="5dc07-117">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="5dc07-117">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="5dc07-118">Cria um instantâneo usando uma configuração de instantâneo, o nome do instantâneo e o nome do grupo de recursos passados como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="5dc07-118">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="5dc07-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5dc07-119">Next steps</span></span>

[<span data-ttu-id="5dc07-120">Criar uma máquina virtual com base em um instantâneo</span><span class="sxs-lookup"><span data-stu-id="5dc07-120">Create a virtual machine from a snapshot</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="5dc07-121">Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5dc07-121">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5dc07-122">Amostras de script do PowerShell da máquina virtual adicionais podem ser encontrados na [documentação da VM Windows do Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5dc07-122">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>