---
title: "Exemplo de Script CLI - instantâneo de exportação/copiar como conta de armazenamento tooa VHD em uma região diferente de aaaAzure | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - instantâneo de exportação/copiar como conta de armazenamento do VHD tooa na assinatura igual ou diferente"
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
ms.openlocfilehash: 945f83d2ed715642156ca7b252af08559c652b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a><span data-ttu-id="41d39-103">Exportação/copiar gerenciado instantâneos como conta de armazenamento tooa VHD em uma região diferente com CLI</span><span class="sxs-lookup"><span data-stu-id="41d39-103">Export/Copy managed snapshots as VHD tooa storage account in different region with CLI</span></span>

<span data-ttu-id="41d39-104">Esse script exporta uma conta de armazenamento gerenciado instantâneo tooa em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="41d39-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="41d39-105">Ele gera primeiro Olá SAS URI do instantâneo hello e, em seguida, usa-toocopy-tooa conta de armazenamento em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="41d39-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="41d39-106">Use esse backup de toomaintain script discos gerenciados em uma região diferente para recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="41d39-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="41d39-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="41d39-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="41d39-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="41d39-108">Script explanation</span></span>

<span data-ttu-id="41d39-109">Esse script usa a seguinte comandos toogenerate URI SAS para uma saudação de instantâneos e cópias gerenciada instantâneo tooa conta de armazenamento usando o URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="41d39-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="41d39-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="41d39-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="41d39-111">Command</span><span class="sxs-lookup"><span data-stu-id="41d39-111">Command</span></span> | <span data-ttu-id="41d39-112">Observações</span><span class="sxs-lookup"><span data-stu-id="41d39-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="41d39-113">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="41d39-113">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="41d39-114">Gera SAS somente leitura que é usado toocopy conta de armazenamento de tooa de arquivo VHD de base ou baixá-lo tooon local</span><span class="sxs-lookup"><span data-stu-id="41d39-114">Generates read-only SAS that is used toocopy underlying VHD file tooa storage account or download it tooon-premises</span></span>  |
| [<span data-ttu-id="41d39-115">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="41d39-115">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="41d39-116">Copia um blob de forma assíncrona de um tooanother de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="41d39-116">Copies a blob asynchronously from one storage account tooanother</span></span> |

## <a name="next-steps"></a><span data-ttu-id="41d39-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41d39-117">Next steps</span></span>

[<span data-ttu-id="41d39-118">Criar um disco gerenciado com base em um VHD</span><span class="sxs-lookup"><span data-stu-id="41d39-118">Create a managed disk from a VHD</span></span>](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="41d39-119">Criar uma máquina virtual com base em um disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="41d39-119">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="41d39-120">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="41d39-120">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="41d39-121">Máquinas virtuais adicionais e exemplos de script CLI de discos gerenciados podem ser encontrados no hello [documentação de VM do Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="41d39-121">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
