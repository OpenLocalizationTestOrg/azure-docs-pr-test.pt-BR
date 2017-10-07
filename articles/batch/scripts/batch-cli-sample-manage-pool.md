---
title: aaaAzure exemplo de Script CLI - Gerenciando Pools em lote | Microsoft Docs
description: "Amostra de Script da CLI do Azure – Gerenciando Pools no Lote"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="912bf-103">Gerenciando pools do Lote do Azure com CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="912bf-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="912bf-104">Esses scripts demonstra algumas das ferramentas de saudação disponíveis no hello CLI do Azure toocreate e gerenciar pools de nós de computação no serviço de lote do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="912bf-104">These script demonstrates some of hello tools available in hello Azure CLI toocreate and manage pools of compute nodes in hello Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="912bf-105">comandos de saudação neste exemplo criam máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="912bf-105">hello commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="912bf-106">VMs em execução se acumulam cobra tooyour conta.</span><span class="sxs-lookup"><span data-stu-id="912bf-106">Running VMs will accrue charges tooyour account.</span></span> <span data-ttu-id="912bf-107">toominimize esses encargos, excluir VMs hello quando você terminar de exemplo de hello em execução.</span><span class="sxs-lookup"><span data-stu-id="912bf-107">toominimize these charges, delete hello VMs once you're done running hello sample.</span></span> <span data-ttu-id="912bf-108">Consulte [Limpar pools](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="912bf-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="912bf-109">Pools de Lote podem ser configurados de duas maneiras, com uma configuração de Serviços de Nuvem (somente Windows) ou com uma configuração de Máquina Virtual (Windows e Linux).</span><span class="sxs-lookup"><span data-stu-id="912bf-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="912bf-110">scripts de exemplo Hello abaixo mostram como pools de toocreate com ambas as configurações.</span><span class="sxs-lookup"><span data-stu-id="912bf-110">hello sample scripts below show how toocreate pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="912bf-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="912bf-111">Prerequisites</span></span>

- <span data-ttu-id="912bf-112">Instalar Olá CLI do Azure com instruções Olá no hello [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se você ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="912bf-112">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="912bf-113">Crie uma conta do lote do Azure caso ainda não tenha uma.</span><span class="sxs-lookup"><span data-stu-id="912bf-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="912bf-114">Consulte [criar uma conta de lote com hello CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para um script de exemplo que cria uma conta.</span><span class="sxs-lookup"><span data-stu-id="912bf-114">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="912bf-115">Se você ainda não tiver feito isso, configure toorun um aplicativo de uma tarefa de início.</span><span class="sxs-lookup"><span data-stu-id="912bf-115">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="912bf-116">Consulte [adicionar aplicativos tooAzure lote com a CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para um script de exemplo que cria um aplicativo e os carrega um tooAzure do pacote de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="912bf-116">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="912bf-117">Pool com o script de exemplo de configuração de serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="912bf-117">Pool with cloud service configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="912bf-118">Pool com o script de exemplo de configuração de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="912bf-118">Pool with virtual machine configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a><span data-ttu-id="912bf-119">Limpar pools</span><span class="sxs-lookup"><span data-stu-id="912bf-119">Clean up pools</span></span>

<span data-ttu-id="912bf-120">Depois de executar Olá acima script de exemplo, execute Olá seguintes pools de saudação do comando toodelete.</span><span class="sxs-lookup"><span data-stu-id="912bf-120">After you run hello above sample script, run hello following command toodelete hello pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="912bf-121">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="912bf-121">Script explanation</span></span>

<span data-ttu-id="912bf-122">Esse script usa Olá toocreate comandos a seguir e manipular os pools de lote.</span><span class="sxs-lookup"><span data-stu-id="912bf-122">This script uses hello following commands toocreate and manipulate Batch pools.</span></span>
<span data-ttu-id="912bf-123">Cada comando na tabela Olá vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="912bf-123">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="912bf-124">Command</span><span class="sxs-lookup"><span data-stu-id="912bf-124">Command</span></span> | <span data-ttu-id="912bf-125">Observações</span><span class="sxs-lookup"><span data-stu-id="912bf-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="912bf-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="912bf-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="912bf-127">Autentique em uma conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="912bf-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="912bf-128">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="912bf-128">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="912bf-129">Lista os aplicativos disponíveis na conta do lote de saudação hello.</span><span class="sxs-lookup"><span data-stu-id="912bf-129">List hello available applications in hello Batch account.</span></span>  |
| [<span data-ttu-id="912bf-130">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="912bf-130">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="912bf-131">Crie um pool de VMs.</span><span class="sxs-lookup"><span data-stu-id="912bf-131">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="912bf-132">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="912bf-132">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="912bf-133">Atualize as propriedades de um pool.</span><span class="sxs-lookup"><span data-stu-id="912bf-133">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="912bf-134">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="912bf-134">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="912bf-135">Liste as informações de imagem e SKUs do agente de nó disponíveis.</span><span class="sxs-lookup"><span data-stu-id="912bf-135">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="912bf-136">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="912bf-136">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="912bf-137">Redimensionamento Olá número de VMs em execução Olá especificado pool.</span><span class="sxs-lookup"><span data-stu-id="912bf-137">Resize hello number of running VMs in hello specified pool.</span></span>  |
| [<span data-ttu-id="912bf-138">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="912bf-138">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="912bf-139">Exibir as propriedades de saudação de um pool.</span><span class="sxs-lookup"><span data-stu-id="912bf-139">Display hello properties of a pool.</span></span>  |
| [<span data-ttu-id="912bf-140">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="912bf-140">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="912bf-141">Excluir Olá especificado pool.</span><span class="sxs-lookup"><span data-stu-id="912bf-141">Delete hello specified pool.</span></span>  |
| [<span data-ttu-id="912bf-142">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="912bf-142">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="912bf-143">Habilite o dimensionamento automático em um pool e aplique uma fórmula.</span><span class="sxs-lookup"><span data-stu-id="912bf-143">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="912bf-144">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="912bf-144">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="912bf-145">Desabilite o dimensionamento automático em um pool.</span><span class="sxs-lookup"><span data-stu-id="912bf-145">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="912bf-146">az batch node list</span><span class="sxs-lookup"><span data-stu-id="912bf-146">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="912bf-147">Lista todos os nó de computação Olá Olá especificado pool.</span><span class="sxs-lookup"><span data-stu-id="912bf-147">List all hello compute node in hello specified pool.</span></span>  |
| [<span data-ttu-id="912bf-148">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="912bf-148">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="912bf-149">Reinicialize o nó de computação especificado hello.</span><span class="sxs-lookup"><span data-stu-id="912bf-149">Reboot hello specified compute node.</span></span>  |
| [<span data-ttu-id="912bf-150">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="912bf-150">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="912bf-151">Excluir Olá listado nós de saudação especificado pool.</span><span class="sxs-lookup"><span data-stu-id="912bf-151">Delete hello listed nodes from hello specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="912bf-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="912bf-152">Next steps</span></span>

<span data-ttu-id="912bf-153">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="912bf-153">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="912bf-154">Exemplos de script em lotes CLI adicionais podem ser encontrados no hello [documentação CLI de lote do Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="912bf-154">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

