---
title: aaaAzure exemplo de Script CLI - montar o disco do sistema operacional | Microsoft Docs
description: Exemplo de Script CLI do Azure - montar o disco do sistema operacional
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="72da1-103">Solucionar problemas de um disco de sistema operacional de VMs</span><span class="sxs-lookup"><span data-stu-id="72da1-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="72da1-104">Esse script monta o disco do sistema operacional de saudação de uma máquina virtual com falha ou problema como dados em disco tooa segunda máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="72da1-104">This script mounts hello operating system disk of a failed or problematic virtual machine as a data disk tooa second virtual machine.</span></span> <span data-ttu-id="72da1-105">Isso pode ser útil ao solucionar problemas de disco problemas ou recuperação de dados.</span><span class="sxs-lookup"><span data-stu-id="72da1-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="72da1-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="72da1-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a><span data-ttu-id="72da1-107">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="72da1-107">Script explanation</span></span>

<span data-ttu-id="72da1-108">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="72da1-108">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="72da1-109">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="72da1-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="72da1-110">Command</span><span class="sxs-lookup"><span data-stu-id="72da1-110">Command</span></span> | <span data-ttu-id="72da1-111">Observações</span><span class="sxs-lookup"><span data-stu-id="72da1-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="72da1-112">az vm show</span><span class="sxs-lookup"><span data-stu-id="72da1-112">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="72da1-113">Retorne a lista de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="72da1-113">Return a list of virtual machines.</span></span> <span data-ttu-id="72da1-114">Nesse caso, a opção de consulta de Olá é disco do sistema operacional usado tooreturn Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="72da1-114">In this case, hello query option is used tooreturn hello virtual machine operating system disk.</span></span> <span data-ttu-id="72da1-115">Esse valor é adicionado tooa nome da variável 'uri'.</span><span class="sxs-lookup"><span data-stu-id="72da1-115">This value is then added tooa variable name ‘uri’.</span></span> |
| [<span data-ttu-id="72da1-116">az vm delete</span><span class="sxs-lookup"><span data-stu-id="72da1-116">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="72da1-117">Exclui uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="72da1-117">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="72da1-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="72da1-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="72da1-119">Cria uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="72da1-119">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="72da1-120">az vm disk attach</span><span class="sxs-lookup"><span data-stu-id="72da1-120">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="72da1-121">Anexa uma máquina de virtual tooa em disco.</span><span class="sxs-lookup"><span data-stu-id="72da1-121">Attaches a disk tooa virtual machine.</span></span> |
| [<span data-ttu-id="72da1-122">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="72da1-122">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="72da1-123">Retorna Olá endereços IP de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="72da1-123">Returns hello IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="72da1-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72da1-124">Next steps</span></span>

<span data-ttu-id="72da1-125">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="72da1-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="72da1-126">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72da1-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
