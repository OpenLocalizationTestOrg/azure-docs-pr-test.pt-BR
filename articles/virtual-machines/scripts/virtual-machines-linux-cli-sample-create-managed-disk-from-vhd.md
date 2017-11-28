---
title: aaaAzure exemplo de Script CLI - criar um disco gerenciado de um arquivo VHD em uma conta de armazenamento no hello mesma assinatura | Microsoft Docs
description: Script CLI do Azure de exemplo - criar um disco gerenciado de um arquivo VHD em uma conta de armazenamento no hello mesma assinatura
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
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a><span data-ttu-id="23e2a-103">Criar um disco gerenciado de um arquivo VHD em uma conta de armazenamento no hello mesma assinatura com a CLI</span><span class="sxs-lookup"><span data-stu-id="23e2a-103">Create a managed disk from a VHD file in a storage account in hello same subscription with CLI</span></span>

<span data-ttu-id="23e2a-104">Esse script cria um disco gerenciado de um arquivo VHD em uma conta de armazenamento no hello mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="23e2a-104">This script creates a managed disk from a VHD file in a storage account in hello same subscription.</span></span> <span data-ttu-id="23e2a-105">Use este script tooimport um especializado toocreate de disco do toomanaged SO de VHD (não generalizado/com Sysprep) uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="23e2a-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="23e2a-106">Ou então, usá-lo tooimport um disco de dados toomanaged dados VHD.</span><span class="sxs-lookup"><span data-stu-id="23e2a-106">Or, use it tooimport a data VHD toomanaged data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="23e2a-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="23e2a-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="23e2a-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="23e2a-108">Script explanation</span></span>

<span data-ttu-id="23e2a-109">Esse script usará os seguintes comandos toocreate um disco gerenciado em um VHD.</span><span class="sxs-lookup"><span data-stu-id="23e2a-109">This script uses following commands toocreate a managed disk from a VHD.</span></span> <span data-ttu-id="23e2a-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="23e2a-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="23e2a-111">Command</span><span class="sxs-lookup"><span data-stu-id="23e2a-111">Command</span></span> | <span data-ttu-id="23e2a-112">Observações</span><span class="sxs-lookup"><span data-stu-id="23e2a-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="23e2a-113">az disk create</span><span class="sxs-lookup"><span data-stu-id="23e2a-113">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="23e2a-114">Cria um disco gerenciado usando o URI de um VHD em uma conta de armazenamento no hello mesma assinatura</span><span class="sxs-lookup"><span data-stu-id="23e2a-114">Creates a managed disk using URI of a VHD in a storage account in hello same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="23e2a-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="23e2a-115">Next steps</span></span>

[<span data-ttu-id="23e2a-116">Criar uma máquina virtual anexando um disco gerenciado como disco do SO</span><span class="sxs-lookup"><span data-stu-id="23e2a-116">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="23e2a-117">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="23e2a-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="23e2a-118">Máquinas virtuais adicionais e exemplos de script CLI de discos gerenciados podem ser encontrados no hello [documentação de VM do Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="23e2a-118">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
