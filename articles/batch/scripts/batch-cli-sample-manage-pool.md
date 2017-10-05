---
title: "Amostra de Script da CLI do Azure – Gerenciando Pools no Lote | Microsoft Docs"
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
ms.openlocfilehash: 2556b02459886390b803407c5cb828687229a44e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="a4be1-103">Gerenciando pools do Lote do Azure com CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a4be1-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="a4be1-104">Esses scripts demonstram algumas das ferramentas disponíveis na CLI do Azure para criar e gerenciar pools de nós de computação no serviço de Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4be1-104">These script demonstrates some of the tools available in the Azure CLI to create and manage pools of compute nodes in the Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="a4be1-105">Os comandos neste exemplo criam máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4be1-105">The commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="a4be1-106">VMs em execução acumularão encargos para sua conta.</span><span class="sxs-lookup"><span data-stu-id="a4be1-106">Running VMs will accrue charges to your account.</span></span> <span data-ttu-id="a4be1-107">Para minimizar esses encargos, exclua as VMs assim que terminar a execução da amostra.</span><span class="sxs-lookup"><span data-stu-id="a4be1-107">To minimize these charges, delete the VMs once you're done running the sample.</span></span> <span data-ttu-id="a4be1-108">Consulte [Limpar pools](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="a4be1-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="a4be1-109">Pools de Lote podem ser configurados de duas maneiras, com uma configuração de Serviços de Nuvem (somente Windows) ou com uma configuração de Máquina Virtual (Windows e Linux).</span><span class="sxs-lookup"><span data-stu-id="a4be1-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="a4be1-110">Os scripts de exemplo a seguir mostram como criar pools com ambas as configurações.</span><span class="sxs-lookup"><span data-stu-id="a4be1-110">The sample scripts below show how to create pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4be1-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a4be1-111">Prerequisites</span></span>

- <span data-ttu-id="a4be1-112">Instale a CLI do Azure usando as instruções fornecidas no [Guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli) se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="a4be1-112">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="a4be1-113">Crie uma conta do lote do Azure caso ainda não tenha uma.</span><span class="sxs-lookup"><span data-stu-id="a4be1-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="a4be1-114">Consulte [Criar uma conta do lote com a CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para um script de exemplo que cria uma conta.</span><span class="sxs-lookup"><span data-stu-id="a4be1-114">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="a4be1-115">Configure um aplicativo para ser executado de uma tarefa de inicialização se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="a4be1-115">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="a4be1-116">Consulte [Adicionando aplicativos ao Lote do Azure com a CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para obter um script de exemplo que cria um aplicativo e carrega um pacote de aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="a4be1-116">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="a4be1-117">Pool com o script de exemplo de configuração de serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="a4be1-117">Pool with cloud service configuration sample script</span></span>

<span data-ttu-id="a4be1-118">[!code-azurecli[principal](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Gerenciar Pools de Serviços de Nuvem")]</span><span class="sxs-lookup"><span data-stu-id="a4be1-118">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]</span></span>

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="a4be1-119">Pool com o script de exemplo de configuração de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a4be1-119">Pool with virtual machine configuration sample script</span></span>

<span data-ttu-id="a4be1-120">[!code-azurecli[principal](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Gerenciar Pools de Máquina Virtual")]</span><span class="sxs-lookup"><span data-stu-id="a4be1-120">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]</span></span>

## <a name="clean-up-pools"></a><span data-ttu-id="a4be1-121">Limpar pools</span><span class="sxs-lookup"><span data-stu-id="a4be1-121">Clean up pools</span></span>

<span data-ttu-id="a4be1-122">Depois de executar o script de exemplo acima, execute o comando a seguir para excluir os pools.</span><span class="sxs-lookup"><span data-stu-id="a4be1-122">After you run the above sample script, run the following command to delete the pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="a4be1-123">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="a4be1-123">Script explanation</span></span>

<span data-ttu-id="a4be1-124">Esse script usa os comandos a seguir para criar e manipular pools do Lote.</span><span class="sxs-lookup"><span data-stu-id="a4be1-124">This script uses the following commands to create and manipulate Batch pools.</span></span>
<span data-ttu-id="a4be1-125">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="a4be1-125">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="a4be1-126">Command</span><span class="sxs-lookup"><span data-stu-id="a4be1-126">Command</span></span> | <span data-ttu-id="a4be1-127">Observações</span><span class="sxs-lookup"><span data-stu-id="a4be1-127">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a4be1-128">az batch account login</span><span class="sxs-lookup"><span data-stu-id="a4be1-128">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="a4be1-129">Autentique em uma conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="a4be1-129">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="a4be1-130">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="a4be1-130">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="a4be1-131">Liste os aplicativos disponíveis na conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="a4be1-131">List the available applications in the Batch account.</span></span>  |
| [<span data-ttu-id="a4be1-132">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="a4be1-132">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="a4be1-133">Crie um pool de VMs.</span><span class="sxs-lookup"><span data-stu-id="a4be1-133">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="a4be1-134">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="a4be1-134">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="a4be1-135">Atualize as propriedades de um pool.</span><span class="sxs-lookup"><span data-stu-id="a4be1-135">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="a4be1-136">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="a4be1-136">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="a4be1-137">Liste as informações de imagem e SKUs do agente de nó disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a4be1-137">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="a4be1-138">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="a4be1-138">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="a4be1-139">Redimensione o número de VMs em execução no pool especificado.</span><span class="sxs-lookup"><span data-stu-id="a4be1-139">Resize the number of running VMs in the specified pool.</span></span>  |
| [<span data-ttu-id="a4be1-140">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="a4be1-140">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="a4be1-141">Exiba as propriedades de um pool.</span><span class="sxs-lookup"><span data-stu-id="a4be1-141">Display the properties of a pool.</span></span>  |
| [<span data-ttu-id="a4be1-142">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="a4be1-142">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="a4be1-143">Exclua o pool especificado.</span><span class="sxs-lookup"><span data-stu-id="a4be1-143">Delete the specified pool.</span></span>  |
| [<span data-ttu-id="a4be1-144">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="a4be1-144">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="a4be1-145">Habilite o dimensionamento automático em um pool e aplique uma fórmula.</span><span class="sxs-lookup"><span data-stu-id="a4be1-145">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="a4be1-146">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="a4be1-146">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="a4be1-147">Desabilite o dimensionamento automático em um pool.</span><span class="sxs-lookup"><span data-stu-id="a4be1-147">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="a4be1-148">az batch node list</span><span class="sxs-lookup"><span data-stu-id="a4be1-148">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="a4be1-149">Liste todos os nós de computação no pool especificado.</span><span class="sxs-lookup"><span data-stu-id="a4be1-149">List all the compute node in the specified pool.</span></span>  |
| [<span data-ttu-id="a4be1-150">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="a4be1-150">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="a4be1-151">Reinicie o nó de computação especificado.</span><span class="sxs-lookup"><span data-stu-id="a4be1-151">Reboot the specified compute node.</span></span>  |
| [<span data-ttu-id="a4be1-152">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="a4be1-152">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="a4be1-153">Exclua os nós listados do pool especificado.</span><span class="sxs-lookup"><span data-stu-id="a4be1-153">Delete the listed nodes from the specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="a4be1-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4be1-154">Next steps</span></span>

<span data-ttu-id="a4be1-155">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4be1-155">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a4be1-156">As amostras de script da CLI do Lote adicionais podem ser encontrados na [documentação do Lote do Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a4be1-156">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

