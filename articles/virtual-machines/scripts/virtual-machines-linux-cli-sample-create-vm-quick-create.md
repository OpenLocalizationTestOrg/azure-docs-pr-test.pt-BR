---
title: "aaaAzure exemplo de Script CLI - rápido criar uma VM do Linux | Microsoft Docs"
description: "Exemplo de Script da CLI do Azure - Criação rápida de uma máquina virtual Linux"
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
ms.openlocfilehash: edecf274f4e401af3603e5be37a989e2e0eb22c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="2445b-103">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2445b-103">Create a virtual machine</span></span>

<span data-ttu-id="2445b-104">Esse script cria uma máquina Virtual Azure com sistema operacional Ubuntu e recursos de rede relacionados.</span><span class="sxs-lookup"><span data-stu-id="2445b-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="2445b-105">Depois de executar o script hello, você pode acessar a máquina virtual de saudação via SSH.</span><span class="sxs-lookup"><span data-stu-id="2445b-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2445b-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="2445b-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2445b-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="2445b-107">Clean up deployment</span></span> 

<span data-ttu-id="2445b-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="2445b-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2445b-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="2445b-109">Script explanation</span></span>

<span data-ttu-id="2445b-110">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="2445b-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="2445b-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="2445b-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2445b-112">Command</span><span class="sxs-lookup"><span data-stu-id="2445b-112">Command</span></span> | <span data-ttu-id="2445b-113">Observações</span><span class="sxs-lookup"><span data-stu-id="2445b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2445b-114">az group create</span><span class="sxs-lookup"><span data-stu-id="2445b-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2445b-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="2445b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2445b-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="2445b-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2445b-117">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="2445b-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="2445b-118">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="2445b-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="2445b-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="2445b-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2445b-120">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="2445b-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2445b-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2445b-121">Next steps</span></span>

<span data-ttu-id="2445b-122">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2445b-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2445b-123">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2445b-123">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
