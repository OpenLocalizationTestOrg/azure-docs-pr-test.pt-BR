---
title: aaaAzure exemplo de Script CLI - criar uma VM do Windows Server 2016 com o IIS usando a DSC | Microsoft Docs
description: Exemplo de script da CLI do Azure - Criar uma VM do Windows Server 2016 com o IIS usando a DSC
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 9883b5925dddca3dd53d083679a0e76d0fb982e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="758f6-103">Criar uma máquina virtual com o IIS usando a DSC</span><span class="sxs-lookup"><span data-stu-id="758f6-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="758f6-104">Esse script cria uma máquina virtual e usa Olá tooinstall de extensão de script personalizado de DSC de máquina Virtual do Azure e configurar o IIS.</span><span class="sxs-lookup"><span data-stu-id="758f6-104">This script creates a virtual machine, and uses hello Azure Virtual Machine DSC custom script extension tooinstall and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="758f6-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="758f6-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="758f6-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="758f6-106">Clean up deployment</span></span> 

<span data-ttu-id="758f6-107">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="758f6-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="758f6-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="758f6-108">Script explanation</span></span>

<span data-ttu-id="758f6-109">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="758f6-109">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="758f6-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="758f6-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="758f6-111">Command</span><span class="sxs-lookup"><span data-stu-id="758f6-111">Command</span></span> | <span data-ttu-id="758f6-112">Observações</span><span class="sxs-lookup"><span data-stu-id="758f6-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="758f6-113">az group create</span><span class="sxs-lookup"><span data-stu-id="758f6-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="758f6-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="758f6-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="758f6-115">az vm create</span><span class="sxs-lookup"><span data-stu-id="758f6-115">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="758f6-116">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="758f6-116">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="758f6-117">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="758f6-117">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="758f6-118">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="758f6-118">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="758f6-119">Adicione a máquina virtual de toohello de extensão de Script personalizado de saudação que chama um script tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="758f6-119">Add hello Custom Script Extension toohello virtual machine which invokes a script tooinstall IIS.</span></span> |
| [<span data-ttu-id="758f6-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="758f6-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="758f6-121">Cria um tooallow de regra de grupo de segurança de rede o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="758f6-121">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="758f6-122">Neste exemplo, a porta 80 está aberta para tráfego HTTP.</span><span class="sxs-lookup"><span data-stu-id="758f6-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="758f6-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="758f6-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="758f6-124">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="758f6-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="758f6-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="758f6-125">Next steps</span></span>

<span data-ttu-id="758f6-126">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="758f6-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="758f6-127">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="758f6-127">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
