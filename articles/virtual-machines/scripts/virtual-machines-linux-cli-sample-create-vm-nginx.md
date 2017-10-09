---
title: aaaAzure exemplo de Script CLI - criar uma VM do Linux com NGINX | Microsoft Docs
description: "Exemplo de script da CLI do Azure - Criar uma máquina virtual Linux com NGINX"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="607de-103">Criar uma máquina virtual com o NGINX</span><span class="sxs-lookup"><span data-stu-id="607de-103">Create a VM with NGINX</span></span>

<span data-ttu-id="607de-104">Esse script cria uma máquina Virtual do Azure e usa Olá extensão de Script de personalizado de máquina Virtual do Azure tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="607de-104">This script creates an Azure Virtual Machine and uses hello Azure Virtual Machine Custom Script Extension tooinstall NGINX.</span></span> <span data-ttu-id="607de-105">Depois de executar o script hello, você pode acessar um site de demonstração no endereço IP público de saudação da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="607de-105">After running hello script, you can access a demo website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="607de-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="607de-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a><span data-ttu-id="607de-107">Extensão de script personalizado</span><span class="sxs-lookup"><span data-stu-id="607de-107">Custom Script Extension</span></span>

<span data-ttu-id="607de-108">extensão do script personalizado Olá copia o script na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="607de-108">hello custom script extension copies this script onto hello virtual machine.</span></span> <span data-ttu-id="607de-109">script Hello é execute tooinstall e configurar um servidor web NGINX.</span><span class="sxs-lookup"><span data-stu-id="607de-109">hello script is then run tooinstall and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="607de-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="607de-110">Clean up deployment</span></span> 

<span data-ttu-id="607de-111">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="607de-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="607de-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="607de-112">Script explanation</span></span>

<span data-ttu-id="607de-113">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="607de-113">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="607de-114">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="607de-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="607de-115">Command</span><span class="sxs-lookup"><span data-stu-id="607de-115">Command</span></span> | <span data-ttu-id="607de-116">Observações</span><span class="sxs-lookup"><span data-stu-id="607de-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="607de-117">az group create</span><span class="sxs-lookup"><span data-stu-id="607de-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="607de-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="607de-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="607de-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="607de-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="607de-120">Cria a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="607de-120">Creates hello virtual machine.</span></span> <span data-ttu-id="607de-121">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="607de-121">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="607de-122">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="607de-122">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="607de-123">Cria um tooallow de regra de grupo de segurança de rede o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="607de-123">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="607de-124">Neste exemplo, a porta 80 está aberta para tráfego HTTP.</span><span class="sxs-lookup"><span data-stu-id="607de-124">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="607de-125">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="607de-125">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="607de-126">Adiciona e executa uma extensão de máquina virtual tooa VM.</span><span class="sxs-lookup"><span data-stu-id="607de-126">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="607de-127">Neste exemplo, a extensão de script personalizado de saudação é usado tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="607de-127">In this sample, hello custom script extension is used tooinstall NGINX.</span></span>|
| [<span data-ttu-id="607de-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="607de-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="607de-129">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="607de-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="607de-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="607de-130">Next steps</span></span>

<span data-ttu-id="607de-131">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="607de-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="607de-132">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="607de-132">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
