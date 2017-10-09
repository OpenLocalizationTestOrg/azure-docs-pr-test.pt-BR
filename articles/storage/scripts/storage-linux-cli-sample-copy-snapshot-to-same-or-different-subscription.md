---
title: "Exemplo de Script CLI - instantâneo de cópia (mover) de um disco gerenciado toosame ou assinatura diferente com CLI de aaaAzure | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - instantâneo de cópia (mover) de um disco gerenciado toosame ou assinatura diferente com CLI"
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
ms.openlocfilehash: 4a21fd2435181a033b563100888aba0c5834496d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="90fc8-103">Copiar um instantâneo de um disco gerenciado toosame ou uma assinatura diferente com CLI</span><span class="sxs-lookup"><span data-stu-id="90fc8-103">Copy snapshot of a managed disk toosame or different subscription with CLI</span></span>

<span data-ttu-id="90fc8-104">Esse script copia um instantâneo de um disco gerenciado toosame ou uma assinatura diferente.</span><span class="sxs-lookup"><span data-stu-id="90fc8-104">This script copies a snapshot of a managed disk toosame or different subscription.</span></span> <span data-ttu-id="90fc8-105">Use toomove este script uma assinatura do instantâneo toodifferent Olá mesma região que o instantâneo do hello pai.</span><span class="sxs-lookup"><span data-stu-id="90fc8-105">Use this script toomove a snapshot toodifferent subscription in hello same region as hello parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="90fc8-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="90fc8-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="90fc8-107">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="90fc8-107">Script explanation</span></span>

<span data-ttu-id="90fc8-108">Esse script usa a seguinte comandos toocreate um instantâneo na assinatura de destino hello usando Olá Id do instantâneo de origem hello.</span><span class="sxs-lookup"><span data-stu-id="90fc8-108">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="90fc8-109">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="90fc8-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="90fc8-110">Command</span><span class="sxs-lookup"><span data-stu-id="90fc8-110">Command</span></span> | <span data-ttu-id="90fc8-111">Observações</span><span class="sxs-lookup"><span data-stu-id="90fc8-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="90fc8-112">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="90fc8-112">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="90fc8-113">Obtém todas as propriedades de saudação de um instantâneo usando o nome hello e propriedades de grupo de recursos de instantâneo de saudação.</span><span class="sxs-lookup"><span data-stu-id="90fc8-113">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="90fc8-114">Propriedade ID é usada toocopy Olá instantâneo toodifferent assinatura.</span><span class="sxs-lookup"><span data-stu-id="90fc8-114">Id property is used toocopy hello snapshot toodifferent subscription.</span></span>  |
| [<span data-ttu-id="90fc8-115">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="90fc8-115">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="90fc8-116">Copia um instantâneo ao criar um instantâneo na assinatura diferente usando Olá Id e nome do hello instantâneo pai.</span><span class="sxs-lookup"><span data-stu-id="90fc8-116">Copies a snapshot by creating a snapshot in different subscription using hello Id and name of hello parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="90fc8-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="90fc8-117">Next steps</span></span>

[<span data-ttu-id="90fc8-118">Criar uma máquina virtual com base em um instantâneo</span><span class="sxs-lookup"><span data-stu-id="90fc8-118">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="90fc8-119">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="90fc8-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="90fc8-120">Máquinas virtuais adicionais e exemplos de script CLI de discos gerenciados podem ser encontrados no hello [documentação de VM do Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="90fc8-120">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
