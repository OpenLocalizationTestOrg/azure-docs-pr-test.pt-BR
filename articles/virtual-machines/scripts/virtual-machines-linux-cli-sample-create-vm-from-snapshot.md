---
title: "Exemplo de script da CLI do Azure – Criar uma VM de um instantâneo | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – Criar uma VM de um instantâneo"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 6e47c3baebd5b68ec29d55c43dc00ae7665c81f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="fbbcc-103">Criar uma máquina virtual de um instantâneo com a CLI</span><span class="sxs-lookup"><span data-stu-id="fbbcc-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="fbbcc-104">Esse script cria uma máquina virtual de um instantâneo de um disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="fbbcc-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fbbcc-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="fbbcc-105">Sample script</span></span>

<span data-ttu-id="fbbcc-106">[!code-azurecli-interactive[principal](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Criar VM por meio do instantâneo")]</span><span class="sxs-lookup"><span data-stu-id="fbbcc-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="fbbcc-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="fbbcc-107">Clean up deployment</span></span> 

<span data-ttu-id="fbbcc-108">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="fbbcc-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fbbcc-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="fbbcc-109">Script explanation</span></span>

<span data-ttu-id="fbbcc-110">Este script usa os comandos a seguir para criar um disco gerenciado, uma máquina virtual e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="fbbcc-110">This script uses the following commands to create a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="fbbcc-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="fbbcc-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fbbcc-112">Command</span><span class="sxs-lookup"><span data-stu-id="fbbcc-112">Command</span></span> | <span data-ttu-id="fbbcc-113">Observações</span><span class="sxs-lookup"><span data-stu-id="fbbcc-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fbbcc-114">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="fbbcc-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="fbbcc-115">Obtém o instantâneo usando o nome do instantâneo e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fbbcc-115">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="fbbcc-116">A propriedade de ID do objeto retornado é usada para criar um disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="fbbcc-116">Id property of the returned object is used to create a managed disk.</span></span>  |
| [<span data-ttu-id="fbbcc-117">az disk create</span><span class="sxs-lookup"><span data-stu-id="fbbcc-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="fbbcc-118">Cria discos gerenciados de um instantâneo usando ID de instantâneo, nome do disco, tipo de armazenamento e tamanho</span><span class="sxs-lookup"><span data-stu-id="fbbcc-118">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="fbbcc-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="fbbcc-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="fbbcc-120">Cria uma VM usando um disco do sistema operacional gerenciado</span><span class="sxs-lookup"><span data-stu-id="fbbcc-120">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fbbcc-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fbbcc-121">Next steps</span></span>

<span data-ttu-id="fbbcc-122">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fbbcc-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fbbcc-123">Os exemplos de script da CLI de máquina virtual adicionais podem ser encontrados na [documentação da VM Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fbbcc-123">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
