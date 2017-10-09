---
title: aaaAzure exemplo de Script CLI - Copy (mover) gerenciado toosame discos ou assinatura diferente | Microsoft Docs
description: Exemplo de Script CLI do Azure - Copy (mover) gerenciados discos toosame ou assinatura diferente
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="3639a-103">Copiar toosame discos gerenciados ou uma assinatura diferente com CLI</span><span class="sxs-lookup"><span data-stu-id="3639a-103">Copy managed disks toosame or different subscription with CLI</span></span>

<span data-ttu-id="3639a-104">Esse script copia um disco gerenciado toosame ou uma assinatura diferente, mas em Olá mesmo região.</span><span class="sxs-lookup"><span data-stu-id="3639a-104">This script copies a managed disk toosame or different subscription but in hello same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3639a-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="3639a-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="3639a-106">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="3639a-106">Script explanation</span></span>

<span data-ttu-id="3639a-107">Esse script usa a seguinte comandos toocreate um novo disco gerenciado na assinatura usando o destino Olá Olá Id da fonte de saudação gerenciados em disco.</span><span class="sxs-lookup"><span data-stu-id="3639a-107">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="3639a-108">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="3639a-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3639a-109">Command</span><span class="sxs-lookup"><span data-stu-id="3639a-109">Command</span></span> | <span data-ttu-id="3639a-110">Observações</span><span class="sxs-lookup"><span data-stu-id="3639a-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3639a-111">az disk show</span><span class="sxs-lookup"><span data-stu-id="3639a-111">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="3639a-112">Obtém todas as propriedades de saudação de um disco gerenciado usando as propriedades do grupo de recursos e o nome do hello de disco gerenciado hello.</span><span class="sxs-lookup"><span data-stu-id="3639a-112">Gets all hello properties of a managed disk using hello name and resource group properties of hello managed disk.</span></span> <span data-ttu-id="3639a-113">Propriedade ID é usada toocopy Olá gerenciado disco toodifferent assinatura.</span><span class="sxs-lookup"><span data-stu-id="3639a-113">Id property is used toocopy hello managed disk toodifferent subscription.</span></span>  |
| [<span data-ttu-id="3639a-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="3639a-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="3639a-115">Copia um disco gerenciado ao criar um novo disco gerenciado na assinatura diferente usando Id e nome do pai Olá gerenciados em disco.</span><span class="sxs-lookup"><span data-stu-id="3639a-115">Copies a managed disk by creating a new managed disk in different subscription using Id and name hello parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="3639a-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3639a-116">Next steps</span></span>

[<span data-ttu-id="3639a-117">Criar uma máquina virtual com base em um disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="3639a-117">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="3639a-118">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3639a-118">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3639a-119">Máquinas virtuais adicionais e exemplos de script CLI de discos gerenciados podem ser encontrados no hello [documentação de VM do Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3639a-119">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
