---
title: aaaAzure exemplo de Script CLI - criar uma VM do Linux com WordPress | Microsoft Docs
description: "Exemplo de script da CLI do Azure - Criar uma máquina virtual Linux com WordPress"
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
ms.openlocfilehash: 2c5c03d08b6d5d27eb8c505b1dbd817eda5f2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="6d22f-103">Criar uma máquina virtual com WordPress</span><span class="sxs-lookup"><span data-stu-id="6d22f-103">Create a VM with WordPress</span></span>

<span data-ttu-id="6d22f-104">Esse script cria uma máquina virtual e, em seguida, usa Olá Máquina Virtual do Azure script personalizado extensão tooinstall WordPress.</span><span class="sxs-lookup"><span data-stu-id="6d22f-104">This script creates a virtual machine, and then uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="6d22f-105">Após script hello em execução, você pode acessar o site de configuração do WordPress Olá em `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="6d22f-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6d22f-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="6d22f-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6d22f-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="6d22f-107">Clean up deployment</span></span> 

<span data-ttu-id="6d22f-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="6d22f-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6d22f-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="6d22f-109">Script explanation</span></span>

<span data-ttu-id="6d22f-110">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6d22f-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="6d22f-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="6d22f-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6d22f-112">Command</span><span class="sxs-lookup"><span data-stu-id="6d22f-112">Command</span></span> | <span data-ttu-id="6d22f-113">Observações</span><span class="sxs-lookup"><span data-stu-id="6d22f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6d22f-114">az group create</span><span class="sxs-lookup"><span data-stu-id="6d22f-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6d22f-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="6d22f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6d22f-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="6d22f-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6d22f-117">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="6d22f-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="6d22f-118">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="6d22f-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="6d22f-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="6d22f-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="6d22f-120">Cria um tooallow de regra de grupo de segurança de rede o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="6d22f-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="6d22f-121">Neste exemplo, a porta 80 está aberta para tráfego HTTP.</span><span class="sxs-lookup"><span data-stu-id="6d22f-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="6d22f-122">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="6d22f-122">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6d22f-123">Adicione a máquina virtual do hello extensão de Script personalizado toohello, que chama um script tooinstall WordPress.</span><span class="sxs-lookup"><span data-stu-id="6d22f-123">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
| [<span data-ttu-id="6d22f-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="6d22f-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6d22f-125">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="6d22f-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6d22f-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d22f-126">Next steps</span></span>

<span data-ttu-id="6d22f-127">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6d22f-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6d22f-128">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d22f-128">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
