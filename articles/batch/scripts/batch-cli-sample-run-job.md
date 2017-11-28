---
title: aaaAzure exemplo de Script CLI - com um trabalho em lotes | Microsoft Docs
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="32426-103">Executar trabalhos no Lote do Azure com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="32426-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="32426-104">Esse script cria um trabalho em lotes e adiciona uma série de trabalho de toohello de tarefas.</span><span class="sxs-lookup"><span data-stu-id="32426-104">This script creates a Batch job and adds a series of tasks toohello job.</span></span> <span data-ttu-id="32426-105">Ele também demonstra como toomonitor um trabalho e suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="32426-105">It also demonstrates how toomonitor a job and its tasks.</span></span> <span data-ttu-id="32426-106">Finalmente, ele mostra como tooquery Olá serviço de lote com eficiência para obter informações sobre tarefas de saudação do trabalho.</span><span class="sxs-lookup"><span data-stu-id="32426-106">Finally, it shows how tooquery hello Batch service efficiently for information about hello job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32426-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="32426-107">Prerequisites</span></span>

- <span data-ttu-id="32426-108">Instalar Olá CLI do Azure com instruções Olá no hello [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se você ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="32426-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="32426-109">Crie uma conta do lote do Azure caso ainda não tenha uma.</span><span class="sxs-lookup"><span data-stu-id="32426-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="32426-110">Consulte [criar uma conta de lote com hello CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para um script de exemplo que cria uma conta.</span><span class="sxs-lookup"><span data-stu-id="32426-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="32426-111">Se você ainda não tiver feito isso, configure toorun um aplicativo de uma tarefa de início.</span><span class="sxs-lookup"><span data-stu-id="32426-111">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="32426-112">Consulte [adicionar aplicativos tooAzure lote com a CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para um script de exemplo que cria um aplicativo e os carrega um tooAzure do pacote de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32426-112">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>
- <span data-ttu-id="32426-113">Configure um pool no qual Olá trabalho será executado.</span><span class="sxs-lookup"><span data-stu-id="32426-113">Configure a pool on which hello job will run.</span></span> <span data-ttu-id="32426-114">Consulte [Gerenciando pools de Lote do Azure com a CLI do Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) para obter um script de exemplo que cria um pool com uma Configuração de serviço de nuvem ou uma Configuração de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="32426-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="32426-115">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="32426-115">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a><span data-ttu-id="32426-116">Trabalho de limpeza</span><span class="sxs-lookup"><span data-stu-id="32426-116">Clean up job</span></span>

<span data-ttu-id="32426-117">Depois de executar Olá acima script de exemplo, execute Olá tooremove de comando a seguir, o trabalho e todas as suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="32426-117">After you run hello above sample script, run hello following command tooremove the job and all of its tasks.</span></span> <span data-ttu-id="32426-118">Observe que o pool de saudação precisará toobe excluído separadamente.</span><span class="sxs-lookup"><span data-stu-id="32426-118">Note that hello pool will need toobe deleted separately.</span></span> <span data-ttu-id="32426-119">Consulte [Gerenciando pools de Lote do Azure com a CLI do Azure](./batch-cli-sample-manage-pool.md) para obter mais informações sobre como criar e excluir grupos.</span><span class="sxs-lookup"><span data-stu-id="32426-119">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="32426-120">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="32426-120">Script explanation</span></span>

<span data-ttu-id="32426-121">Esse script usa Olá toocreate comandos a seguir, um trabalho em lotes e tarefas.</span><span class="sxs-lookup"><span data-stu-id="32426-121">This script uses hello following commands toocreate a Batch job and tasks.</span></span> <span data-ttu-id="32426-122">Cada comando na tabela Olá vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="32426-122">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="32426-123">Command</span><span class="sxs-lookup"><span data-stu-id="32426-123">Command</span></span> | <span data-ttu-id="32426-124">Observações</span><span class="sxs-lookup"><span data-stu-id="32426-124">Notes</span></span> |
|---|---|
| [<span data-ttu-id="32426-125">az batch account login</span><span class="sxs-lookup"><span data-stu-id="32426-125">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="32426-126">Autentica em uma conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="32426-126">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="32426-127">az batch job create</span><span class="sxs-lookup"><span data-stu-id="32426-127">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="32426-128">Cria um trabalho do Lote.</span><span class="sxs-lookup"><span data-stu-id="32426-128">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="32426-129">az batch job set</span><span class="sxs-lookup"><span data-stu-id="32426-129">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="32426-130">Atualiza as propriedades de um trabalho do Lote.</span><span class="sxs-lookup"><span data-stu-id="32426-130">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="32426-131">az batch job show</span><span class="sxs-lookup"><span data-stu-id="32426-131">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="32426-132">Recupera detalhes de um trabalho especificado do Lote.</span><span class="sxs-lookup"><span data-stu-id="32426-132">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="32426-133">az batch task create</span><span class="sxs-lookup"><span data-stu-id="32426-133">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="32426-134">Adiciona que uma tarefa toohello especificado trabalho em lotes.</span><span class="sxs-lookup"><span data-stu-id="32426-134">Adds a task toohello specified Batch job.</span></span>  |
| [<span data-ttu-id="32426-135">az batch task show</span><span class="sxs-lookup"><span data-stu-id="32426-135">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="32426-136">Recupera Olá detalhes de uma tarefa de saudação especificado trabalho em lotes.</span><span class="sxs-lookup"><span data-stu-id="32426-136">Retrieves hello details of a task from hello specified Batch job.</span></span>  |
| [<span data-ttu-id="32426-137">az batch task list</span><span class="sxs-lookup"><span data-stu-id="32426-137">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="32426-138">Lista as tarefas de saudação associadas ao trabalho especificado hello.</span><span class="sxs-lookup"><span data-stu-id="32426-138">Lists hello tasks associated with hello specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="32426-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="32426-139">Next steps</span></span>

<span data-ttu-id="32426-140">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="32426-140">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="32426-141">Exemplos de script em lotes CLI adicionais podem ser encontrados no hello [documentação CLI de lote do Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="32426-141">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
