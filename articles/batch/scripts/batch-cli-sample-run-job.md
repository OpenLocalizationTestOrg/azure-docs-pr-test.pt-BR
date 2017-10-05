---
title: "Amostra de Script da CLI do Azure – Executar um trabalho com o Lote | Microsoft Docs"
description: "Amostra de Script da CLI do Azure – Executar um trabalho com o Lote"
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
ms.openlocfilehash: 5fe1e3595d9459e60b2fd54d6f17f6822731f453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="c625b-103">Executar trabalhos no Lote do Azure com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c625b-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="c625b-104">Esse script cria um trabalho no Lote e adiciona uma série de tarefas ao trabalho.</span><span class="sxs-lookup"><span data-stu-id="c625b-104">This script creates a Batch job and adds a series of tasks to the job.</span></span> <span data-ttu-id="c625b-105">Ele também demonstra como monitorar um trabalho e suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="c625b-105">It also demonstrates how to monitor a job and its tasks.</span></span> <span data-ttu-id="c625b-106">Por fim, ele mostra como consultar o serviço de lote com eficiência para obter informações sobre tarefas do trabalho.</span><span class="sxs-lookup"><span data-stu-id="c625b-106">Finally, it shows how to query the Batch service efficiently for information about the job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c625b-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c625b-107">Prerequisites</span></span>

- <span data-ttu-id="c625b-108">Instale a CLI do Azure usando as instruções fornecidas no [Guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli) se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="c625b-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="c625b-109">Crie uma conta do lote do Azure caso ainda não tenha uma.</span><span class="sxs-lookup"><span data-stu-id="c625b-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="c625b-110">Consulte [Criar uma conta do lote com a CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para um script de exemplo que cria uma conta.</span><span class="sxs-lookup"><span data-stu-id="c625b-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="c625b-111">Configure um aplicativo para ser executado de uma tarefa de inicialização se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="c625b-111">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="c625b-112">Consulte [Adicionando aplicativos ao Lote do Azure com a CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para obter um script de exemplo que cria um aplicativo e carrega um pacote de aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="c625b-112">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>
- <span data-ttu-id="c625b-113">Configure um pool no qual o trabalho será executado.</span><span class="sxs-lookup"><span data-stu-id="c625b-113">Configure a pool on which the job will run.</span></span> <span data-ttu-id="c625b-114">Consulte [Gerenciando pools de Lote do Azure com a CLI do Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) para obter um script de exemplo que cria um pool com uma Configuração de serviço de nuvem ou uma Configuração de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c625b-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="c625b-115">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="c625b-115">Sample script</span></span>

<span data-ttu-id="c625b-116">[!code-azurecli[principal](../../../cli_scripts/batch/run-job/run-job.sh "Executar trabalhos")]</span><span class="sxs-lookup"><span data-stu-id="c625b-116">[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]</span></span>

## <a name="clean-up-job"></a><span data-ttu-id="c625b-117">Trabalho de limpeza</span><span class="sxs-lookup"><span data-stu-id="c625b-117">Clean up job</span></span>

<span data-ttu-id="c625b-118">Depois de executar o exemplo de script acima, execute o comando a seguir para remover o trabalho e todas as suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="c625b-118">After you run the above sample script, run the following command to remove the job and all of its tasks.</span></span> <span data-ttu-id="c625b-119">Observe que o pool precisará ser excluído separadamente.</span><span class="sxs-lookup"><span data-stu-id="c625b-119">Note that the pool will need to be deleted separately.</span></span> <span data-ttu-id="c625b-120">Consulte [Gerenciando pools de Lote do Azure com a CLI do Azure](./batch-cli-sample-manage-pool.md) para obter mais informações sobre como criar e excluir grupos.</span><span class="sxs-lookup"><span data-stu-id="c625b-120">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="c625b-121">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="c625b-121">Script explanation</span></span>

<span data-ttu-id="c625b-122">Esse script usa os seguintes comandos para criar um trabalho do Lote e suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="c625b-122">This script uses the following commands to create a Batch job and tasks.</span></span> <span data-ttu-id="c625b-123">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="c625b-123">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="c625b-124">Command</span><span class="sxs-lookup"><span data-stu-id="c625b-124">Command</span></span> | <span data-ttu-id="c625b-125">Observações</span><span class="sxs-lookup"><span data-stu-id="c625b-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c625b-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="c625b-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="c625b-127">Autentica em uma conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="c625b-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="c625b-128">az batch job create</span><span class="sxs-lookup"><span data-stu-id="c625b-128">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="c625b-129">Cria um trabalho do Lote.</span><span class="sxs-lookup"><span data-stu-id="c625b-129">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="c625b-130">az batch job set</span><span class="sxs-lookup"><span data-stu-id="c625b-130">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="c625b-131">Atualiza as propriedades de um trabalho do Lote.</span><span class="sxs-lookup"><span data-stu-id="c625b-131">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="c625b-132">az batch job show</span><span class="sxs-lookup"><span data-stu-id="c625b-132">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="c625b-133">Recupera detalhes de um trabalho especificado do Lote.</span><span class="sxs-lookup"><span data-stu-id="c625b-133">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="c625b-134">az batch task create</span><span class="sxs-lookup"><span data-stu-id="c625b-134">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="c625b-135">Adiciona uma tarefa ao trabalho do Lote especificado.</span><span class="sxs-lookup"><span data-stu-id="c625b-135">Adds a task to the specified Batch job.</span></span>  |
| [<span data-ttu-id="c625b-136">az batch task show</span><span class="sxs-lookup"><span data-stu-id="c625b-136">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="c625b-137">Recupera os detalhes de uma tarefa do trabalho do Lote especificado.</span><span class="sxs-lookup"><span data-stu-id="c625b-137">Retrieves the details of a task from the specified Batch job.</span></span>  |
| [<span data-ttu-id="c625b-138">az batch task list</span><span class="sxs-lookup"><span data-stu-id="c625b-138">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="c625b-139">Lista as tarefas associadas ao trabalho especificado.</span><span class="sxs-lookup"><span data-stu-id="c625b-139">Lists the tasks associated with the specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="c625b-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c625b-140">Next steps</span></span>

<span data-ttu-id="c625b-141">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c625b-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c625b-142">As amostras de script da CLI do Lote adicionais podem ser encontrados na [documentação do Lote do Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c625b-142">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
