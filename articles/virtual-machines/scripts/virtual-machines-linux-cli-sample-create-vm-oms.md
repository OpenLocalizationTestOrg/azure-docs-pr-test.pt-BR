---
title: Exemplo de script da CLI do Azure - Criar uma VM do Linux com o monitoramento do OMS | Microsoft Docs
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
ms.openlocfilehash: 31bfcc532a7d1ea418fb9a15ec882963d1913756
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="1b601-103">Monitorar uma VM com o Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="1b601-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="1b601-104">Esse script cria uma Máquina Virtual do Azure, instala o agente do OMS (Operations Management Suite) e registra o sistema com um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="1b601-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="1b601-105">Depois que o script tiver sido executado, a máquina virtual ficará visível no console do OMS.</span><span class="sxs-lookup"><span data-stu-id="1b601-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1b601-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="1b601-106">Sample script</span></span>

<span data-ttu-id="1b601-107">[!code-azurecli-interactive[principal](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Criação rápida de VM")]</span><span class="sxs-lookup"><span data-stu-id="1b601-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1b601-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="1b601-108">Clean up deployment</span></span> 

<span data-ttu-id="1b601-109">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="1b601-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1b601-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="1b601-110">Script explanation</span></span>

<span data-ttu-id="1b601-111">Este script usa os comandos a seguir para criar um grupo de recursos, uma máquina virtual e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="1b601-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="1b601-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="1b601-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1b601-113">Command</span><span class="sxs-lookup"><span data-stu-id="1b601-113">Command</span></span> | <span data-ttu-id="1b601-114">Observações</span><span class="sxs-lookup"><span data-stu-id="1b601-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1b601-115">az group create</span><span class="sxs-lookup"><span data-stu-id="1b601-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1b601-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="1b601-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1b601-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="1b601-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="1b601-118">Cria a máquina virtual e a conecta a placa de rede, a rede virtual, a sub-rede e o NSG.</span><span class="sxs-lookup"><span data-stu-id="1b601-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="1b601-119">Este comando também especifica a imagem de máquina virtual a ser usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="1b601-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="1b601-120">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="1b601-120">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="1b601-121">Executa uma extensão de VM em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1b601-121">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="1b601-122">Nesse caso, a extensão do agente Operations Management Suite é usada para instalar o agente do OMS e para registrar a VM em um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="1b601-122">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="1b601-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="1b601-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="1b601-124">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="1b601-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1b601-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b601-125">Next steps</span></span>

<span data-ttu-id="1b601-126">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1b601-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1b601-127">Os exemplos de script da CLI de máquina virtual adicionais podem ser encontrados na [documentação da VM Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b601-127">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
