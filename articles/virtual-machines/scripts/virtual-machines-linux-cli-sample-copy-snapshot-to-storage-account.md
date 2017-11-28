---
title: "Amostra de script da CLI do Azure – Exportar/copiar um instantâneo como VHD para uma conta de armazenamento em outra região | Microsoft Docs"
description: "Amostra de script da CLI do Azure – Exportar/copiar um instantâneo como VHD para uma conta de armazenamento na mesma ou em outra assinatura"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: a6ea65aba91641ece415db4df6ae9c17b42a0954
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-cli"></a><span data-ttu-id="81a2c-103">Exportar/copiar instantâneos gerenciados como VHD para uma conta de armazenamento em outa região com a CLI</span><span class="sxs-lookup"><span data-stu-id="81a2c-103">Export/Copy managed snapshots as VHD to a storage account in different region with CLI</span></span>

<span data-ttu-id="81a2c-104">Esse script exporta um instantâneo gerenciado para uma conta de armazenamento em outra região.</span><span class="sxs-lookup"><span data-stu-id="81a2c-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="81a2c-105">Primeiro, ele gera o URI de SAS do instantâneo e, em seguida, usa-o para copiá-lo para uma conta de armazenamento em outra região.</span><span class="sxs-lookup"><span data-stu-id="81a2c-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="81a2c-106">Use esse script para manter o backup dos discos gerenciados em outra região para a recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="81a2c-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="81a2c-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="81a2c-107">Sample script</span></span>

<span data-ttu-id="81a2c-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copiar instantâneo")]</span><span class="sxs-lookup"><span data-stu-id="81a2c-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="81a2c-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="81a2c-109">Script explanation</span></span>

<span data-ttu-id="81a2c-110">Esse script usa os comandos a seguir para gerar o URI de SAS para um instantâneo gerenciado e copia o instantâneo para uma conta de armazenamento usando o URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="81a2c-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="81a2c-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="81a2c-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="81a2c-112">Command</span><span class="sxs-lookup"><span data-stu-id="81a2c-112">Command</span></span> | <span data-ttu-id="81a2c-113">Observações</span><span class="sxs-lookup"><span data-stu-id="81a2c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="81a2c-114">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="81a2c-114">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="81a2c-115">Gera o SAS somente leitura usado para copiar o arquivo VHD subjacente para uma conta de armazenamento ou o baixa no local</span><span class="sxs-lookup"><span data-stu-id="81a2c-115">Generates read-only SAS that is used to copy underlying VHD file to a storage account or download it to on-premises</span></span>  |
| [<span data-ttu-id="81a2c-116">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="81a2c-116">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="81a2c-117">Copia um blob de forma assíncrona de uma conta de armazenamento para outra</span><span class="sxs-lookup"><span data-stu-id="81a2c-117">Copies a blob asynchronously from one storage account to another</span></span> |

## <a name="next-steps"></a><span data-ttu-id="81a2c-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="81a2c-118">Next steps</span></span>

[<span data-ttu-id="81a2c-119">Criar um disco gerenciado com base em um VHD</span><span class="sxs-lookup"><span data-stu-id="81a2c-119">Create a managed disk from a VHD</span></span>](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="81a2c-120">Criar uma máquina virtual com base em um disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="81a2c-120">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="81a2c-121">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="81a2c-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="81a2c-122">Os exemplos adicionais de script da CLI de máquina virtual e discos gerenciados podem ser encontrados na [documentação da VM Linux do Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="81a2c-122">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
