---
title: "Exemplo de Script do PowerShell - instantâneo de exportação/copiar como conta de armazenamento tooa VHD em uma região diferente de aaaAzure | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - instantâneo de exportação/copiar como conta de armazenamento do VHD tooa na mesma região diferente"
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
ms.openlocfilehash: 3b3e38c6b06bfa1e117f4e913dfc09443a795196
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="35299-103">Exportação/copiar gerenciado instantâneos como conta de armazenamento tooa VHD em uma região diferente com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="35299-103">Export/Copy managed snapshots as VHD tooa storage account in different region with PowerShell</span></span>

<span data-ttu-id="35299-104">Esse script exporta uma conta de armazenamento gerenciado instantâneo tooa em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="35299-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="35299-105">Ele gera primeiro Olá SAS URI do instantâneo hello e, em seguida, usa-toocopy-tooa conta de armazenamento em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="35299-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="35299-106">Use esse backup de toomaintain script discos gerenciados em uma região diferente para recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="35299-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="35299-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="35299-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="35299-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="35299-108">Script explanation</span></span>

<span data-ttu-id="35299-109">Esse script usa a seguinte comandos toogenerate URI SAS para uma saudação de instantâneos e cópias gerenciada instantâneo tooa conta de armazenamento usando o URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="35299-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="35299-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="35299-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="35299-111">Command</span><span class="sxs-lookup"><span data-stu-id="35299-111">Command</span></span> | <span data-ttu-id="35299-112">Observações</span><span class="sxs-lookup"><span data-stu-id="35299-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="35299-113">Grant-AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="35299-113">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="35299-114">Gera o URI de SAS para um instantâneo que seja usada toocopy-tooa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="35299-114">Generates SAS URI for a snapshot that is used toocopy it tooa storage account.</span></span> |
| [<span data-ttu-id="35299-115">New-AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="35299-115">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="35299-116">Cria um contexto de conta de armazenamento usando a chave e o nome da conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="35299-116">Creates a storage account context using hello account name and key.</span></span> <span data-ttu-id="35299-117">Esse contexto pode ser usado tooperform operações de leitura/gravação na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="35299-117">This context can be used tooperform read/write operations on hello storage account.</span></span> |
| [<span data-ttu-id="35299-118">Start-AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="35299-118">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="35299-119">Cópias Olá VHD subjacente de uma conta de armazenamento instantâneo tooa</span><span class="sxs-lookup"><span data-stu-id="35299-119">Copies hello underlying VHD of a snapshot tooa storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="35299-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="35299-120">Next steps</span></span>

[<span data-ttu-id="35299-121">Criar um disco gerenciado com base em um VHD</span><span class="sxs-lookup"><span data-stu-id="35299-121">Create a managed disk from a VHD</span></span>](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="35299-122">Criar uma máquina virtual com base em um disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="35299-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="35299-123">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="35299-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="35299-124">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="35299-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
