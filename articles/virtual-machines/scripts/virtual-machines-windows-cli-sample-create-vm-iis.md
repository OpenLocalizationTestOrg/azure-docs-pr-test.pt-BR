---
title: aaaAzure exemplo de Script CLI - instalar o IIS | Microsoft Docs
description: Exemplo de Script da CLI do Azure - Instalar o IIS
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 2fabc9522f424cab4c672084ba8bedfd623c87cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="74ce3-103">Criação rápida de uma máquina virtual com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="74ce3-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="74ce3-104">Esse script cria uma máquina Virtual do Azure executando o Windows Server 2016 e usa tooinstall de extensão de Script de personalizado de máquina Virtual do Azure Olá IIS.</span><span class="sxs-lookup"><span data-stu-id="74ce3-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses hello Azure Virtual Machine Custom Script Extension tooinstall IIS.</span></span> <span data-ttu-id="74ce3-105">Depois de executar o script hello, você pode acessar o site do IIS padrão Olá no endereço IP público de saudação da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="74ce3-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="74ce3-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="74ce3-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="74ce3-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="74ce3-107">Clean up deployment</span></span> 

<span data-ttu-id="74ce3-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="74ce3-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="74ce3-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="74ce3-109">Script explanation</span></span>

<span data-ttu-id="74ce3-110">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="74ce3-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="74ce3-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="74ce3-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="74ce3-112">Command</span><span class="sxs-lookup"><span data-stu-id="74ce3-112">Command</span></span> | <span data-ttu-id="74ce3-113">Observações</span><span class="sxs-lookup"><span data-stu-id="74ce3-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="74ce3-114">az group create</span><span class="sxs-lookup"><span data-stu-id="74ce3-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="74ce3-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="74ce3-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="74ce3-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="74ce3-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="74ce3-117">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="74ce3-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="74ce3-118">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="74ce3-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="74ce3-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="74ce3-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="74ce3-120">Cria um tooallow de regra de grupo de segurança de rede o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="74ce3-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="74ce3-121">Neste exemplo, a porta 80 está aberta para tráfego HTTP.</span><span class="sxs-lookup"><span data-stu-id="74ce3-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="74ce3-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="74ce3-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="74ce3-123">Adiciona e executa uma extensão de máquina virtual tooa VM.</span><span class="sxs-lookup"><span data-stu-id="74ce3-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="74ce3-124">Neste exemplo, extensão do script personalizado Olá é usado tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="74ce3-124">In this sample, hello custom script extension is used tooinstall IIS.</span></span>|
| [<span data-ttu-id="74ce3-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="74ce3-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="74ce3-126">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="74ce3-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="74ce3-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74ce3-127">Next steps</span></span>

<span data-ttu-id="74ce3-128">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="74ce3-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="74ce3-129">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="74ce3-129">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
