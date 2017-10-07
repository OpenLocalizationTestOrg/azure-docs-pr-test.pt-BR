---
title: aaaAzure exemplo de Script CLI - criar uma VM do Linux com o OMS monitoramento | Microsoft Docs
description: Exemplo de script da CLI do Azure - Criar uma VM do Linux com o monitoramento do OMS
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
ms.openlocfilehash: 7a329d4f90a20e0e11faa1f5cafd0701574dc440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="c8acc-103">Monitorar uma VM com o Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="c8acc-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="c8acc-104">Esse script cria uma máquina Virtual do Azure, instala o agente do Operations Management Suite (OMS) hello e registra o sistema Olá com um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="c8acc-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="c8acc-105">Depois que o script hello foi executado, máquina virtual de saudação ficarão visível no console do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="c8acc-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c8acc-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="c8acc-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c8acc-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="c8acc-107">Clean up deployment</span></span> 

<span data-ttu-id="c8acc-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="c8acc-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c8acc-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="c8acc-109">Script explanation</span></span>

<span data-ttu-id="c8acc-110">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="c8acc-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="c8acc-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="c8acc-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c8acc-112">Command</span><span class="sxs-lookup"><span data-stu-id="c8acc-112">Command</span></span> | <span data-ttu-id="c8acc-113">Observações</span><span class="sxs-lookup"><span data-stu-id="c8acc-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c8acc-114">az group create</span><span class="sxs-lookup"><span data-stu-id="c8acc-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c8acc-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="c8acc-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c8acc-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="c8acc-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c8acc-117">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="c8acc-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="c8acc-118">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="c8acc-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="c8acc-119">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="c8acc-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c8acc-120">Executa uma extensão de VM em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c8acc-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="c8acc-121">Nesse caso, hello extensão de agente do Operations Management Suite é o agente do OMS Olá tooinstall usado e registrar Olá VM em um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="c8acc-121">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="c8acc-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="c8acc-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c8acc-123">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="c8acc-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c8acc-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c8acc-124">Next steps</span></span>

<span data-ttu-id="c8acc-125">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c8acc-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c8acc-126">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c8acc-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
