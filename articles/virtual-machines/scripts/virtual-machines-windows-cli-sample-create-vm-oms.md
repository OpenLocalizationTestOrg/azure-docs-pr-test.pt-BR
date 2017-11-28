---
title: aaaAzure exemplo de Script CLI - criar uma VM do Windows Server 2016 com o OMS monitoramento | Microsoft Docs
description: Exemplo de script da CLI do Azure - Criar uma VM do Windows Server 2016 com o monitoramento do OMS
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
ms.author: rclaus
ms.openlocfilehash: 4f070430ccc5d5402ed4a80ead3b78eff25dcd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="5126e-103">Monitorar uma VM com o Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="5126e-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="5126e-104">Esse script cria uma máquina Virtual do Azure, instala o agente do Operations Management Suite (OMS) hello e registra o sistema Olá com um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="5126e-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="5126e-105">Depois que o script hello foi executado, máquina virtual de saudação ficarão visível no console do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="5126e-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5126e-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="5126e-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5126e-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="5126e-107">Clean up deployment</span></span> 

<span data-ttu-id="5126e-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="5126e-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="5126e-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="5126e-109">Script explanation</span></span>

<span data-ttu-id="5126e-110">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="5126e-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="5126e-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="5126e-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5126e-112">Command</span><span class="sxs-lookup"><span data-stu-id="5126e-112">Command</span></span> | <span data-ttu-id="5126e-113">Observações</span><span class="sxs-lookup"><span data-stu-id="5126e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5126e-114">az group create</span><span class="sxs-lookup"><span data-stu-id="5126e-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5126e-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="5126e-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5126e-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="5126e-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="5126e-117">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="5126e-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="5126e-118">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="5126e-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="5126e-119">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="5126e-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5126e-120">Executa uma extensão de VM em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5126e-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="5126e-121">Nesse caso, hello extensão de agente do Operations Management Suite é o agente do OMS Olá tooinstall usado e registrar Olá VM em um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="5126e-121">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="5126e-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="5126e-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5126e-123">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="5126e-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5126e-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5126e-124">Next steps</span></span>

<span data-ttu-id="5126e-125">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5126e-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5126e-126">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5126e-126">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
