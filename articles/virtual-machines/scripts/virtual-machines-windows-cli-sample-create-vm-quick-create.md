---
title: "Exemplo de Script da CLI do Azure - Criação rápida de uma VM do Windows Server 2016 | Microsoft Docs"
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
ms.openlocfilehash: 084518bf7bc1d01c4a146efe3e0b7fe08149ce35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="quick-create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="91944-103">Criação rápida de uma máquina virtual com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="91944-103">Quick Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="91944-104">Esse script cria uma Máquina Virtual do Azure que executa o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="91944-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="91944-105">Após a execução do script, é possível acessar a máquina virtual por meio de uma conexão de Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="91944-105">After running the script, you can access the virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="91944-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="91944-106">Sample script</span></span>

<span data-ttu-id="91944-107">[!code-azurecli-interactive[principal](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Criação rápida de VM")]</span><span class="sxs-lookup"><span data-stu-id="91944-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="91944-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="91944-108">Clean up deployment</span></span> 

<span data-ttu-id="91944-109">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="91944-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="91944-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="91944-110">Script explanation</span></span>

<span data-ttu-id="91944-111">Este script usa os comandos a seguir para criar um grupo de recursos, uma máquina virtual e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="91944-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="91944-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="91944-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="91944-113">Command</span><span class="sxs-lookup"><span data-stu-id="91944-113">Command</span></span> | <span data-ttu-id="91944-114">Observações</span><span class="sxs-lookup"><span data-stu-id="91944-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="91944-115">az group create</span><span class="sxs-lookup"><span data-stu-id="91944-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="91944-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="91944-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="91944-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="91944-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="91944-118">Cria a máquina virtual e a conecta à placa de rede, a rede virtual, à sub-rede e ao grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="91944-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="91944-119">Este comando também especifica a imagem da máquina virtual a ser usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="91944-119">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="91944-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="91944-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="91944-121">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="91944-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="91944-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="91944-122">Next steps</span></span>

<span data-ttu-id="91944-123">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91944-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="91944-124">Exemplos de script CLI máquinas virtuais adicionais podem ser encontrados na [documentação da VM do Windows do Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="91944-124">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
