---
title: "Amostra de script do Azure PowerShell – Exportar/copiar um instantâneo como VHD para uma conta de armazenamento em outra região | Microsoft Docs"
description: "Amostra de script do Azure PowerShell – Exportar/copiar um instantâneo como VHD para uma conta de armazenamento em outra região"
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
ms.openlocfilehash: 80f83f4b66165ddd2bdd0edca2be5d026cb11a9b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="ada75-103">Exportar/copiar instantâneos gerenciados como VHD para uma conta de armazenamento em outa região com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ada75-103">Export/Copy managed snapshots as VHD to a storage account in different region with PowerShell</span></span>

<span data-ttu-id="ada75-104">Esse script exporta um instantâneo gerenciado para uma conta de armazenamento em outra região.</span><span class="sxs-lookup"><span data-stu-id="ada75-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="ada75-105">Primeiro, ele gera o URI de SAS do instantâneo e, em seguida, usa-o para copiá-lo para uma conta de armazenamento em outra região.</span><span class="sxs-lookup"><span data-stu-id="ada75-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="ada75-106">Use esse script para manter o backup dos discos gerenciados em outra região para a recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="ada75-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ada75-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ada75-107">Sample script</span></span>

<span data-ttu-id="ada75-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copiar instantâneo")]</span><span class="sxs-lookup"><span data-stu-id="ada75-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="ada75-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="ada75-109">Script explanation</span></span>

<span data-ttu-id="ada75-110">Esse script usa os comandos a seguir para gerar o URI de SAS para um instantâneo gerenciado e copia o instantâneo para uma conta de armazenamento usando o URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="ada75-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="ada75-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="ada75-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ada75-112">Command</span><span class="sxs-lookup"><span data-stu-id="ada75-112">Command</span></span> | <span data-ttu-id="ada75-113">Observações</span><span class="sxs-lookup"><span data-stu-id="ada75-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ada75-114">Grant-AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="ada75-114">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="ada75-115">Gera o URI de SAS para um instantâneo que é usado para copiá-lo para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ada75-115">Generates SAS URI for a snapshot that is used to copy it to a storage account.</span></span> |
| [<span data-ttu-id="ada75-116">New-AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="ada75-116">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="ada75-117">Cria um contexto de conta de armazenamento usando o nome da conta e a chave.</span><span class="sxs-lookup"><span data-stu-id="ada75-117">Creates a storage account context using the account name and key.</span></span> <span data-ttu-id="ada75-118">Esse contexto pode ser usado para executar operações de leitura/gravação na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ada75-118">This context can be used to perform read/write operations on the storage account.</span></span> |
| [<span data-ttu-id="ada75-119">Start-AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="ada75-119">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="ada75-120">Copia o VHD subjacente de um instantâneo para uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="ada75-120">Copies the underlying VHD of a snapshot to a storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ada75-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ada75-121">Next steps</span></span>

[<span data-ttu-id="ada75-122">Criar um disco gerenciado com base em um VHD</span><span class="sxs-lookup"><span data-stu-id="ada75-122">Create a managed disk from a VHD</span></span>](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="ada75-123">Criar uma máquina virtual com base em um disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="ada75-123">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="ada75-124">Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ada75-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ada75-125">Amostras de script do PowerShell da máquina virtual adicionais podem ser encontrados na [documentação da VM Windows do Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ada75-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>