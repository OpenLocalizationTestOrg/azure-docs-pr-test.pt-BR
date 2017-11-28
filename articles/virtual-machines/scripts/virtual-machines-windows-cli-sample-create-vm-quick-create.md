---
title: "aaaAzure exemplo de Script CLI - rápido criar uma VM do Windows Server 2016 | Microsoft Docs"
description: "Exemplo de Script da CLI do Azure - Criação rápida de uma VM do Windows Server 2016"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rickstercdn
ms.openlocfilehash: 4c736ce9e2ecc9ee75b34f903cad52c9c0ee0707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="6c99b-103">Criação rápida de uma máquina virtual com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6c99b-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="6c99b-104">Esse script cria uma Máquina Virtual do Azure que executa o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="6c99b-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="6c99b-105">Depois de executar o script hello, você pode acessar a máquina virtual de saudação por meio de uma conexão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="6c99b-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6c99b-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="6c99b-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6c99b-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="6c99b-107">Clean up deployment</span></span> 

<span data-ttu-id="6c99b-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="6c99b-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="6c99b-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="6c99b-109">Script explanation</span></span>

<span data-ttu-id="6c99b-110">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6c99b-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="6c99b-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="6c99b-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6c99b-112">Command</span><span class="sxs-lookup"><span data-stu-id="6c99b-112">Command</span></span> | <span data-ttu-id="6c99b-113">Observações</span><span class="sxs-lookup"><span data-stu-id="6c99b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6c99b-114">az group create</span><span class="sxs-lookup"><span data-stu-id="6c99b-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6c99b-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="6c99b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6c99b-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="6c99b-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6c99b-117">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="6c99b-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="6c99b-118">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="6c99b-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="6c99b-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="6c99b-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6c99b-120">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="6c99b-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c99b-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c99b-121">Next steps</span></span>

<span data-ttu-id="6c99b-122">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6c99b-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6c99b-123">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c99b-123">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
