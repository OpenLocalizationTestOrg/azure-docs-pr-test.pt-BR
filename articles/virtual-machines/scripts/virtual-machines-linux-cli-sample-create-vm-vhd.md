---
title: "aaaAzure exemplo de Script CLI - criar uma máquina virtual com um VHD | Microsoft Docs"
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
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="ba828-103">Criar uma VM com um disco rígido virtual</span><span class="sxs-lookup"><span data-stu-id="ba828-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="ba828-104">Este exemplo cria uma máquina virtual usando um VHD.</span><span class="sxs-lookup"><span data-stu-id="ba828-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="ba828-105">Cria um grupo de recursos, uma conta de armazenamento e um contêiner, e em seguida, cria uma VM, carregando o contêiner de toohello VHD Olá.</span><span class="sxs-lookup"><span data-stu-id="ba828-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading hello VHD toohello container.</span></span>
<span data-ttu-id="ba828-106">Ele substitui Olá ssh pública da chave com sua chave pública para que você tenha acesso toohello VM.</span><span class="sxs-lookup"><span data-stu-id="ba828-106">It replaces hello ssh public key with your public key so that you have access toohello VM.</span></span>

<span data-ttu-id="ba828-107">Você precisará de um VHD inicializável.</span><span class="sxs-lookup"><span data-stu-id="ba828-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="ba828-108">Você pode baixar Olá VHD que usamos de https://azclisamples.blob.core.windows.net/vhds/sample.vhd ou usar seu próprio VHD.</span><span class="sxs-lookup"><span data-stu-id="ba828-108">You can download hello VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="ba828-109">script Hello procura `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="ba828-109">hello script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ba828-110">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ba828-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ba828-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="ba828-111">Clean up deployment</span></span> 

<span data-ttu-id="ba828-112">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ba828-112">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="ba828-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="ba828-113">Script explanation</span></span>

<span data-ttu-id="ba828-114">Esse script usa Olá comandos toocreate um grupo de recursos, máquina virtual, o conjunto de disponibilidade, balanceador de carga e todos os recursos relacionados a seguir.</span><span class="sxs-lookup"><span data-stu-id="ba828-114">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="ba828-115">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="ba828-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ba828-116">Command</span><span class="sxs-lookup"><span data-stu-id="ba828-116">Command</span></span> | <span data-ttu-id="ba828-117">Observações</span><span class="sxs-lookup"><span data-stu-id="ba828-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ba828-118">az group create</span><span class="sxs-lookup"><span data-stu-id="ba828-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ba828-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="ba828-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ba828-120">az storage account list</span><span class="sxs-lookup"><span data-stu-id="ba828-120">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="ba828-121">Lista contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="ba828-121">Lists storage accounts</span></span> |
| [<span data-ttu-id="ba828-122">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="ba828-122">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="ba828-123">Verifica se um nome de conta de armazenamento é válido e se já não existe</span><span class="sxs-lookup"><span data-stu-id="ba828-123">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="ba828-124">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="ba828-124">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="ba828-125">Lista de chaves para as contas de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="ba828-125">Lists keys for hello storage accounts</span></span> |
| [<span data-ttu-id="ba828-126">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="ba828-126">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="ba828-127">Verifica se o blob Olá existe</span><span class="sxs-lookup"><span data-stu-id="ba828-127">Checks whether hello blob exists</span></span> |
| [<span data-ttu-id="ba828-128">az storage container create</span><span class="sxs-lookup"><span data-stu-id="ba828-128">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="ba828-129">Cria um contêiner em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ba828-129">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="ba828-130">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="ba828-130">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="ba828-131">Cria um blob no contêiner Olá Olá carregar VHD.</span><span class="sxs-lookup"><span data-stu-id="ba828-131">Creates a blob in hello container by uploading hello VHD.</span></span> |
| [<span data-ttu-id="ba828-132">az vm list</span><span class="sxs-lookup"><span data-stu-id="ba828-132">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="ba828-133">Usado com `--query` Verifique se o nome da VM hello está em uso.</span><span class="sxs-lookup"><span data-stu-id="ba828-133">Used with `--query` check whether hello VM name is in use.</span></span> | 
| [<span data-ttu-id="ba828-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="ba828-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="ba828-135">Cria máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba828-135">Creates hello virtual machines.</span></span> |
| [<span data-ttu-id="ba828-136">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="ba828-136">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="ba828-137">Redefine Olá SSH toogive chave Olá atual usuário acesso toohello VM.</span><span class="sxs-lookup"><span data-stu-id="ba828-137">Resets hello SSH key toogive hello current user access toohello VM.</span></span> |
| [<span data-ttu-id="ba828-138">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="ba828-138">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="ba828-139">Obtém o endereço IP Olá Olá VM que foi criado.</span><span class="sxs-lookup"><span data-stu-id="ba828-139">Gets hello IP address of hello VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ba828-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ba828-140">Next steps</span></span>

<span data-ttu-id="ba828-141">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ba828-141">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ba828-142">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba828-142">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
