---
title: aaaAzure exemplo de Script CLI - adicionar um aplicativo em lote | Microsoft Docs
description: "Amostra de Script da CLI do Azure – Adicionar um aplicativo no Lote"
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
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a><span data-ttu-id="29ddd-103">Adicionar aplicativos tooAzure lote com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="29ddd-103">Adding applications tooAzure Batch with Azure CLI</span></span>

<span data-ttu-id="29ddd-104">Este script demonstra como tooset um aplicativo para uso com um pool de lote do Azure ou uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="29ddd-104">This script demonstrates how tooset up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="29ddd-105">tooset um aplicativo, o executável, juntamente com quaisquer dependências, em um arquivo. zip do pacote.</span><span class="sxs-lookup"><span data-stu-id="29ddd-105">tooset up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="29ddd-106">Neste zip executável do exemplo hello arquivo é denominado ' Meu-aplicativo-exe.zip'.</span><span class="sxs-lookup"><span data-stu-id="29ddd-106">In this example hello executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29ddd-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="29ddd-107">Prerequisites</span></span>

- <span data-ttu-id="29ddd-108">Instalar Olá CLI do Azure com instruções Olá no hello [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se você ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="29ddd-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="29ddd-109">Crie uma conta do lote do Azure caso ainda não tenha uma.</span><span class="sxs-lookup"><span data-stu-id="29ddd-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="29ddd-110">Consulte [criar uma conta de lote com hello CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para um script de exemplo que cria uma conta.</span><span class="sxs-lookup"><span data-stu-id="29ddd-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="29ddd-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="29ddd-111">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a><span data-ttu-id="29ddd-112">Limpar aplicativo</span><span class="sxs-lookup"><span data-stu-id="29ddd-112">Clean up application</span></span>

<span data-ttu-id="29ddd-113">Depois de executar Olá acima script de exemplo, execute Olá tooremove comandos a seguir o aplicativo e todos os seus pacotes de aplicativo carregado.</span><span class="sxs-lookup"><span data-stu-id="29ddd-113">After you run hello above sample script, run hello following commands tooremove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="29ddd-114">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="29ddd-114">Script explanation</span></span>

<span data-ttu-id="29ddd-115">Esse script usa Olá toocreate comandos a seguir, um aplicativo e carregar um pacote de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29ddd-115">This script uses hello following commands toocreate an application and upload an application package.</span></span>
<span data-ttu-id="29ddd-116">Cada comando na tabela Olá vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="29ddd-116">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="29ddd-117">Command</span><span class="sxs-lookup"><span data-stu-id="29ddd-117">Command</span></span> | <span data-ttu-id="29ddd-118">Observações</span><span class="sxs-lookup"><span data-stu-id="29ddd-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="29ddd-119">az batch application create</span><span class="sxs-lookup"><span data-stu-id="29ddd-119">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="29ddd-120">Criar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29ddd-120">Creates an application.</span></span>  |
| [<span data-ttu-id="29ddd-121">az batch application set</span><span class="sxs-lookup"><span data-stu-id="29ddd-121">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="29ddd-122">Atualiza as propriedades de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29ddd-122">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="29ddd-123">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="29ddd-123">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="29ddd-124">Adiciona um toohello do pacote de aplicativo especificado aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29ddd-124">Adds an application package toohello specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="29ddd-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="29ddd-125">Next steps</span></span>

<span data-ttu-id="29ddd-126">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="29ddd-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="29ddd-127">Exemplos de script em lotes CLI adicionais podem ser encontrados no hello [documentação CLI de lote do Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="29ddd-127">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
