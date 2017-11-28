---
title: "Amostra de script da CLI do Azure – Copiar (mover) um instantâneo de um disco gerenciado para a mesma ou outra assinatura com CLI | Microsoft Docs"
description: "Amostra de script da CLI do Azure – Copiar (mover) um instantâneo de um disco gerenciado para a mesma ou outra assinatura com CLI"
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
ms.openlocfilehash: 0127e342bd0c3afbe9de775399f5510814bff499
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="3d358-103">Copiar um instantâneo de um disco gerenciado para a mesma assinatura ou outra assinatura com a CLI</span><span class="sxs-lookup"><span data-stu-id="3d358-103">Copy snapshot of a managed disk to same or different subscription with CLI</span></span>

<span data-ttu-id="3d358-104">Esse script copia um instantâneo de um disco gerenciado para a mesma assinatura ou outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="3d358-104">This script copies a snapshot of a managed disk to same or different subscription.</span></span> <span data-ttu-id="3d358-105">Use este script para mover um instantâneo para outra assinatura na mesma região do instantâneo pai.</span><span class="sxs-lookup"><span data-stu-id="3d358-105">Use this script to move a snapshot to different subscription in the same region as the parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3d358-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="3d358-106">Sample script</span></span>

<span data-ttu-id="3d358-107">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copiar instantâneo")]</span><span class="sxs-lookup"><span data-stu-id="3d358-107">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="3d358-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="3d358-108">Script explanation</span></span>

<span data-ttu-id="3d358-109">Esse script usa os comandos a seguir para criar um instantâneo na assinatura de destino usando a ID do instantâneo de origem.</span><span class="sxs-lookup"><span data-stu-id="3d358-109">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="3d358-110">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="3d358-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3d358-111">Command</span><span class="sxs-lookup"><span data-stu-id="3d358-111">Command</span></span> | <span data-ttu-id="3d358-112">Observações</span><span class="sxs-lookup"><span data-stu-id="3d358-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3d358-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="3d358-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="3d358-114">Obtém todas as propriedades de um instantâneo usando o nome e as propriedades do grupo de recursos do instantâneo.</span><span class="sxs-lookup"><span data-stu-id="3d358-114">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="3d358-115">A propriedade de ID é usada para copiar o instantâneo para uma assinatura diferente.</span><span class="sxs-lookup"><span data-stu-id="3d358-115">Id property is used to copy the snapshot to different subscription.</span></span>  |
| [<span data-ttu-id="3d358-116">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="3d358-116">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="3d358-117">Copia um instantâneo criando um instantâneo na assinatura diferente usando a Id e o nome do instantâneo pai.</span><span class="sxs-lookup"><span data-stu-id="3d358-117">Copies a snapshot by creating a snapshot in different subscription using the Id and name of the parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="3d358-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d358-118">Next steps</span></span>

[<span data-ttu-id="3d358-119">Criar uma máquina virtual com base em um instantâneo</span><span class="sxs-lookup"><span data-stu-id="3d358-119">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="3d358-120">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3d358-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3d358-121">Os exemplos adicionais de script da CLI de máquina virtual e discos gerenciados podem ser encontrados na [documentação da VM Linux do Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d358-121">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
