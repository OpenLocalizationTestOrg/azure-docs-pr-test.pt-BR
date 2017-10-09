---
title: aaaAzure exemplo de Script CLI - VMs reiniciar | Microsoft Docs
description: "Amostra de script da CLI do Azure – Reinicializar VMs por marcação e ID"
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
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a><span data-ttu-id="cb275-103">Reiniciar VMs</span><span class="sxs-lookup"><span data-stu-id="cb275-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="cb275-104">Este exemplo mostra duas maneiras tooget algumas VMs e reiniciá-los.</span><span class="sxs-lookup"><span data-stu-id="cb275-104">This sample shows a couple of ways tooget some VMs and restart them.</span></span>

<span data-ttu-id="cb275-105">Olá primeiro reinicia todas as VMs Olá no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb275-105">hello first restarts all hello VMs in hello resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="cb275-106">saudação de segundo obtém Hello marcados VMs usando `az resouce list` filtra toohello recursos que são as VMs e reinicia nessas VMs.</span><span class="sxs-lookup"><span data-stu-id="cb275-106">hello second gets hello tagged VMs using `az resouce list` and filters toohello resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="cb275-107">Este exemplo funciona em um shell Bash.</span><span class="sxs-lookup"><span data-stu-id="cb275-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="cb275-108">Para obter opções sobre a execução de scripts de CLI do Azure no cliente do Windows, consulte [em execução Olá CLI do Azure no Windows](../windows/cli-options.md).</span><span class="sxs-lookup"><span data-stu-id="cb275-108">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="cb275-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="cb275-109">Sample script</span></span>

<span data-ttu-id="cb275-110">exemplo Hello tem três scripts.</span><span class="sxs-lookup"><span data-stu-id="cb275-110">hello sample has three scripts.</span></span>
<span data-ttu-id="cb275-111">Olá um primeiro provisionar Olá máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="cb275-111">hello first one provisions hello virtual machines.</span></span>
<span data-ttu-id="cb275-112">Ele usa a opção de não-espera Olá comando Olá retorna sem esperar em cada toobe VM provisionado.</span><span class="sxs-lookup"><span data-stu-id="cb275-112">It uses hello no-wait option so hello command returns without waiting on each VM toobe provisioned.</span></span>
<span data-ttu-id="cb275-113">Olá segundo aguarda Olá VMs toobe totalmente provisionado.</span><span class="sxs-lookup"><span data-stu-id="cb275-113">hello second waits for hello VMs toobe fully provisioned.</span></span>
<span data-ttu-id="cb275-114">script de terceiro Olá reinicia todas as VMs de saudação que foram provisionadas e, em seguida, basta Olá marcados VMs.</span><span class="sxs-lookup"><span data-stu-id="cb275-114">hello third script restarts all hello VMs that were provisioned, and then just hello tagged VMs.</span></span>

### <a name="provision-hello-vms"></a><span data-ttu-id="cb275-115">Saudação de provisionar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="cb275-115">Provision hello VMs</span></span>

<span data-ttu-id="cb275-116">Esse script cria um grupo de recursos e, em seguida, ele cria três toorestart de VMs.</span><span class="sxs-lookup"><span data-stu-id="cb275-116">This script creates a resource group and then it creates three VMs toorestart.</span></span>
<span data-ttu-id="cb275-117">Duas delas são marcadas.</span><span class="sxs-lookup"><span data-stu-id="cb275-117">Two of them are tagged.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a><span data-ttu-id="cb275-118">Aguarde</span><span class="sxs-lookup"><span data-stu-id="cb275-118">Wait</span></span>

<span data-ttu-id="cb275-119">Esse script verifica no hello cada 20 segundos até que todas as três VMs são provisionadas ou um deles falha tooprovision do status de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="cb275-119">This script checks on hello provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails tooprovision.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a><span data-ttu-id="cb275-120">Reiniciar Olá VMs</span><span class="sxs-lookup"><span data-stu-id="cb275-120">Restart hello VMs</span></span>

<span data-ttu-id="cb275-121">Esse script reinicia todas as VMs Olá no grupo de recursos de saudação e reinicia apenas Olá marcado VMs.</span><span class="sxs-lookup"><span data-stu-id="cb275-121">This script restarts all hello VMs in hello resource group, and then it restarts just hello tagged VMs.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a><span data-ttu-id="cb275-122">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="cb275-122">Clean up deployment</span></span> 

<span data-ttu-id="cb275-123">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove Olá os grupos de recursos, VMs e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="cb275-123">After hello script sample has been run, hello following command can be used tooremove hello resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="cb275-124">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="cb275-124">Script explanation</span></span>

<span data-ttu-id="cb275-125">Esse script usa Olá comandos toocreate um grupo de recursos, máquina virtual, o conjunto de disponibilidade, balanceador de carga e todos os recursos relacionados a seguir.</span><span class="sxs-lookup"><span data-stu-id="cb275-125">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="cb275-126">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="cb275-126">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="cb275-127">Command</span><span class="sxs-lookup"><span data-stu-id="cb275-127">Command</span></span> | <span data-ttu-id="cb275-128">Observações</span><span class="sxs-lookup"><span data-stu-id="cb275-128">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cb275-129">az group create</span><span class="sxs-lookup"><span data-stu-id="cb275-129">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="cb275-130">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="cb275-130">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cb275-131">az vm create</span><span class="sxs-lookup"><span data-stu-id="cb275-131">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="cb275-132">Cria máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb275-132">Creates hello virtual machines.</span></span>  |
| [<span data-ttu-id="cb275-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="cb275-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="cb275-134">Usado com `--query` tooensure Olá VMs são provisionados antes de reiniciá-los e, em seguida, tooget Olá IDs de saudação VMs toorestart-los.</span><span class="sxs-lookup"><span data-stu-id="cb275-134">Used with `--query` tooensure hello VMs are provisioned before restarting them, and then tooget hello IDs of hello VMs toorestart them.</span></span> |
| [<span data-ttu-id="cb275-135">az resource list</span><span class="sxs-lookup"><span data-stu-id="cb275-135">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="cb275-136">Usado com `--query` tooget Olá IDs de VMs hello usando Olá marca.</span><span class="sxs-lookup"><span data-stu-id="cb275-136">Used with `--query` tooget hello IDs of hello VMs using hello tag.</span></span> |
| [<span data-ttu-id="cb275-137">az vm restart</span><span class="sxs-lookup"><span data-stu-id="cb275-137">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="cb275-138">Reinicia Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="cb275-138">Restarts hello VMs.</span></span> |
| [<span data-ttu-id="cb275-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="cb275-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="cb275-140">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="cb275-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cb275-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb275-141">Next steps</span></span>

<span data-ttu-id="cb275-142">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cb275-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cb275-143">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cb275-143">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
