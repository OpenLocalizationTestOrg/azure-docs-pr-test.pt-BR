---
title: aaaAzure exemplo de Script CLI - criar duas VMs com um NSG interno e externo | Microsoft Docs
description: Exemplo de script da CLI do Azure - Criar duas VMs com um NSG interno e um externo
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f04e62d09575bee34ac4aeee949736b34000c337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="4bfa7-103">Proteger o tráfego de rede entre máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="4bfa7-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="4bfa7-104">Esse script cria duas máquinas virtuais e protege tooboth de tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-104">This script creates two virtual machines and secures incoming traffic tooboth.</span></span> <span data-ttu-id="4bfa7-105">Uma máquina virtual é acessível em Olá internet e um grupo de segurança de rede (NSG) configurado tooallow tráfego na porta 3389 e na porta 80.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-105">One virtual machine is accessible on hello internet and has a network security group (NSG) configured tooallow traffic on port 3389 and port 80.</span></span> <span data-ttu-id="4bfa7-106">Olá segunda máquina de virtual não está acessível no hello internet e tem um NSG configurado tooonly permitir o tráfego da máquina virtual da primeira hello.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-106">hello second virtual machine is not accessible on hello internet, and has an NSG configured tooonly allow traffic from hello first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4bfa7-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="4bfa7-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4bfa7-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="4bfa7-108">Clean up deployment</span></span> 

<span data-ttu-id="4bfa7-109">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="4bfa7-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="4bfa7-110">Script explanation</span></span>

<span data-ttu-id="4bfa7-111">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="4bfa7-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4bfa7-113">Command</span><span class="sxs-lookup"><span data-stu-id="4bfa7-113">Command</span></span> | <span data-ttu-id="4bfa7-114">Observações</span><span class="sxs-lookup"><span data-stu-id="4bfa7-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4bfa7-115">az group create</span><span class="sxs-lookup"><span data-stu-id="4bfa7-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4bfa7-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4bfa7-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="4bfa7-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="4bfa7-118">Cria uma sub-rede e uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="4bfa7-119">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="4bfa7-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="4bfa7-120">Cria uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="4bfa7-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="4bfa7-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="4bfa7-122">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-122">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="4bfa7-123">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-123">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="4bfa7-124">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="4bfa7-124">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="4bfa7-125">Atualiza uma regra NSG.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-125">Updates an NSG rule.</span></span> <span data-ttu-id="4bfa7-126">Neste exemplo, a regra de back-end de Olá é atualizada toopass tráfego somente da sub-rede front-end hello.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-126">In this sample, hello back-end rule is updated toopass through traffic only from hello front-end subnet.</span></span> |
| [<span data-ttu-id="4bfa7-127">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="4bfa7-127">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="4bfa7-128">Retorna informações sobre uma regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-128">Returns information about a network security group rule.</span></span> <span data-ttu-id="4bfa7-129">Neste exemplo, o nome da regra Olá é armazenado em uma variável para uso posteriormente no script hello.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-129">In this sample, hello rule name is stored in a variable for use later in hello script.</span></span> |
| [<span data-ttu-id="4bfa7-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="4bfa7-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="4bfa7-131">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="4bfa7-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4bfa7-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4bfa7-132">Next steps</span></span>

<span data-ttu-id="4bfa7-133">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4bfa7-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4bfa7-134">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4bfa7-134">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
