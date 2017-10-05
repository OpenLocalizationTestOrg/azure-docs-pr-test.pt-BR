---
title: "Exemplo de script da CLI do Azure - Criar uma máquina virtual Linux com NGINX | Microsoft Docs"
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
ms.openlocfilehash: 416624d9e378d09f4fb0593119dbc30adeb09f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="2286c-103">Criar uma máquina virtual com o NGINX</span><span class="sxs-lookup"><span data-stu-id="2286c-103">Create a VM with NGINX</span></span>

<span data-ttu-id="2286c-104">Esse script cria uma Máquina Virtual do Azure e usa a Extensão de Script Personalizado da Máquina Virtual do Azure para instalar o NGINX.</span><span class="sxs-lookup"><span data-stu-id="2286c-104">This script creates an Azure Virtual Machine and uses the Azure Virtual Machine Custom Script Extension to install NGINX.</span></span> <span data-ttu-id="2286c-105">Após a execução do script, é possível acessar um site de demonstração no endereço IP público da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2286c-105">After running the script, you can access a demo website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2286c-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="2286c-106">Sample script</span></span>

<span data-ttu-id="2286c-107">[!code-azurecli-interactive[principal](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Criação rápida de VM")]</span><span class="sxs-lookup"><span data-stu-id="2286c-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]</span></span>

## <a name="custom-script-extension"></a><span data-ttu-id="2286c-108">Extensão de script personalizado</span><span class="sxs-lookup"><span data-stu-id="2286c-108">Custom Script Extension</span></span>

<span data-ttu-id="2286c-109">A extensão de script personalizado copia esse script na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2286c-109">The custom script extension copies this script onto the virtual machine.</span></span> <span data-ttu-id="2286c-110">O script é executado, em seguida, para instalar e configurar um servidor de web NGINX.</span><span class="sxs-lookup"><span data-stu-id="2286c-110">The script is then run to install and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="2286c-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="2286c-111">Clean up deployment</span></span> 

<span data-ttu-id="2286c-112">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="2286c-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2286c-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="2286c-113">Script explanation</span></span>

<span data-ttu-id="2286c-114">Este script usa os comandos a seguir para criar um grupo de recursos, uma máquina virtual e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="2286c-114">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="2286c-115">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="2286c-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2286c-116">Command</span><span class="sxs-lookup"><span data-stu-id="2286c-116">Command</span></span> | <span data-ttu-id="2286c-117">Observações</span><span class="sxs-lookup"><span data-stu-id="2286c-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2286c-118">az group create</span><span class="sxs-lookup"><span data-stu-id="2286c-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2286c-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="2286c-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2286c-120">az vm create</span><span class="sxs-lookup"><span data-stu-id="2286c-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2286c-121">Cria as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="2286c-121">Creates the virtual machine.</span></span> <span data-ttu-id="2286c-122">Este comando também especifica a imagem de máquina virtual a ser usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="2286c-122">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="2286c-123">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="2286c-123">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="2286c-124">Cria uma regra de grupo de segurança de rede para permitir o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="2286c-124">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="2286c-125">Neste exemplo, a porta 80 está aberta para tráfego HTTP.</span><span class="sxs-lookup"><span data-stu-id="2286c-125">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="2286c-126">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="2286c-126">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2286c-127">Adiciona e executa uma extensão da máquina virtual a uma VM.</span><span class="sxs-lookup"><span data-stu-id="2286c-127">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="2286c-128">Neste exemplo, a extensão de script personalizado é usada para instalar o NGINX.</span><span class="sxs-lookup"><span data-stu-id="2286c-128">In this sample, the custom script extension is used to install NGINX.</span></span>|
| [<span data-ttu-id="2286c-129">az group delete</span><span class="sxs-lookup"><span data-stu-id="2286c-129">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2286c-130">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="2286c-130">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2286c-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2286c-131">Next steps</span></span>

<span data-ttu-id="2286c-132">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2286c-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2286c-133">Os exemplos de script da CLI de máquina virtual adicionais podem ser encontrados na [documentação da VM Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2286c-133">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
