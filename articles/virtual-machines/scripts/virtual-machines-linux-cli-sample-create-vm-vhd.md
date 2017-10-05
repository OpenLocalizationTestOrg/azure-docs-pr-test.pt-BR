---
title: "Exemplo de script da CLI do Azure – Criar uma VM com um VHD | Microsoft Docs"
description: "Amostra de script da CLI do Azure – criar uma VM usando um disco rígido virtual."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: fab65296a552c1839522c5254a868a3dc96227f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="adf60-103">Criar uma VM com um disco rígido virtual</span><span class="sxs-lookup"><span data-stu-id="adf60-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="adf60-104">Este exemplo cria uma máquina virtual usando um VHD.</span><span class="sxs-lookup"><span data-stu-id="adf60-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="adf60-105">Ele cria um grupo de recursos, uma conta de armazenamento e um contêiner, então cria uma VM carregando o VHD no contêiner.</span><span class="sxs-lookup"><span data-stu-id="adf60-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading the VHD to the container.</span></span>
<span data-ttu-id="adf60-106">Ele substitui a chave pública de SSH pela sua chave pública, de modo que você tem acesso à VM.</span><span class="sxs-lookup"><span data-stu-id="adf60-106">It replaces the ssh public key with your public key so that you have access to the VM.</span></span>

<span data-ttu-id="adf60-107">Você precisará de um VHD inicializável.</span><span class="sxs-lookup"><span data-stu-id="adf60-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="adf60-108">Você pode baixar o VHD que usamos de https://azclisamples.blob.core.windows.net/vhds/sample.vhd ou usar seu próprio VHD.</span><span class="sxs-lookup"><span data-stu-id="adf60-108">You can download the VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="adf60-109">O script procura `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="adf60-109">The script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="adf60-110">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="adf60-110">Sample script</span></span>

<span data-ttu-id="adf60-111">[!code-azurecli-interactive[principal](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Criar VM usando um VHD")]</span><span class="sxs-lookup"><span data-stu-id="adf60-111">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="adf60-112">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="adf60-112">Clean up deployment</span></span> 

<span data-ttu-id="adf60-113">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="adf60-113">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="adf60-114">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="adf60-114">Script explanation</span></span>

<span data-ttu-id="adf60-115">Esse script usa os seguintes comandos para criar um grupo de recursos, uma máquina virtual, um conjunto de disponibilidade, um balanceador de carga e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="adf60-115">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="adf60-116">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="adf60-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="adf60-117">Command</span><span class="sxs-lookup"><span data-stu-id="adf60-117">Command</span></span> | <span data-ttu-id="adf60-118">Observações</span><span class="sxs-lookup"><span data-stu-id="adf60-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="adf60-119">az group create</span><span class="sxs-lookup"><span data-stu-id="adf60-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="adf60-120">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="adf60-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="adf60-121">az storage account list</span><span class="sxs-lookup"><span data-stu-id="adf60-121">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="adf60-122">Lista contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="adf60-122">Lists storage accounts</span></span> |
| [<span data-ttu-id="adf60-123">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="adf60-123">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="adf60-124">Verifica se um nome de conta de armazenamento é válido e se já não existe</span><span class="sxs-lookup"><span data-stu-id="adf60-124">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="adf60-125">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="adf60-125">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="adf60-126">Lista as chaves das contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="adf60-126">Lists keys for the storage accounts</span></span> |
| [<span data-ttu-id="adf60-127">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="adf60-127">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="adf60-128">Verifica se o blob existe</span><span class="sxs-lookup"><span data-stu-id="adf60-128">Checks whether the blob exists</span></span> |
| [<span data-ttu-id="adf60-129">az storage container create</span><span class="sxs-lookup"><span data-stu-id="adf60-129">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="adf60-130">Cria um contêiner em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="adf60-130">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="adf60-131">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="adf60-131">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="adf60-132">Cria um blob no contêiner carregando o VHD.</span><span class="sxs-lookup"><span data-stu-id="adf60-132">Creates a blob in the container by uploading the VHD.</span></span> |
| [<span data-ttu-id="adf60-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="adf60-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="adf60-134">Usado com `--query`, verifica se o nome da VM está em uso.</span><span class="sxs-lookup"><span data-stu-id="adf60-134">Used with `--query` check whether the VM name is in use.</span></span> | 
| [<span data-ttu-id="adf60-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="adf60-135">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="adf60-136">Cria as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="adf60-136">Creates the virtual machines.</span></span> |
| [<span data-ttu-id="adf60-137">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="adf60-137">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="adf60-138">Redefine a chave SSH para fornecer o acesso do usuário atual para a VM.</span><span class="sxs-lookup"><span data-stu-id="adf60-138">Resets the SSH key to give the current user access to the VM.</span></span> |
| [<span data-ttu-id="adf60-139">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="adf60-139">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="adf60-140">Obtém o endereço IP da VM que foi criada.</span><span class="sxs-lookup"><span data-stu-id="adf60-140">Gets the IP address of the VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="adf60-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="adf60-141">Next steps</span></span>

<span data-ttu-id="adf60-142">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="adf60-142">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="adf60-143">Os exemplos de script da CLI de máquina virtual adicionais podem ser encontrados na [documentação da VM Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="adf60-143">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
