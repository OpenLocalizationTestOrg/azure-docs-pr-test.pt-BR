---
title: "Amostra de Script da CLI do Azure – Adicionar um aplicativo no Lote | Microsoft Docs"
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
ms.openlocfilehash: 5d057eaf32867aedc95d58c5185e2be1f9385ec0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-applications-to-azure-batch-with-azure-cli"></a><span data-ttu-id="0d9f9-103">Adicionar aplicativos ao Lote do Azure com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0d9f9-103">Adding applications to Azure Batch with Azure CLI</span></span>

<span data-ttu-id="0d9f9-104">Este script demonstra como configurar um aplicativo para uso com um pool ou tarefa do Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d9f9-104">This script demonstrates how to set up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="0d9f9-105">Para configurar um aplicativo, coloque seu executável, junto com quaisquer dependências, em um arquivo .zip.</span><span class="sxs-lookup"><span data-stu-id="0d9f9-105">To set up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="0d9f9-106">Neste exemplo, o arquivo executável zip é chamado 'my-application-exe.zip'.</span><span class="sxs-lookup"><span data-stu-id="0d9f9-106">In this example the executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d9f9-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0d9f9-107">Prerequisites</span></span>

- <span data-ttu-id="0d9f9-108">Instale a CLI do Azure usando as instruções fornecidas no [Guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli) se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="0d9f9-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="0d9f9-109">Crie uma conta do lote do Azure caso ainda não tenha uma.</span><span class="sxs-lookup"><span data-stu-id="0d9f9-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="0d9f9-110">Consulte [Criar uma conta do lote com a CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para um script de exemplo que cria uma conta.</span><span class="sxs-lookup"><span data-stu-id="0d9f9-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="0d9f9-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="0d9f9-111">Sample script</span></span>

<span data-ttu-id="0d9f9-112">[!code-azurecli[principal](../../../cli_scripts/batch/add-application/add-application.sh "Adicionar aplicativo")]</span><span class="sxs-lookup"><span data-stu-id="0d9f9-112">[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]</span></span>

## <a name="clean-up-application"></a><span data-ttu-id="0d9f9-113">Limpar aplicativo</span><span class="sxs-lookup"><span data-stu-id="0d9f9-113">Clean up application</span></span>

<span data-ttu-id="0d9f9-114">Depois de executar o script de exemplo acima, execute os comandos a seguir para remover o aplicativo e todos os seus pacotes de aplicativo carregados.</span><span class="sxs-lookup"><span data-stu-id="0d9f9-114">After you run the above sample script, run the following commands to remove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="0d9f9-115">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="0d9f9-115">Script explanation</span></span>

<span data-ttu-id="0d9f9-116">Esse script usa os seguintes comandos para criar um aplicativo e carregar um pacote de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d9f9-116">This script uses the following commands to create an application and upload an application package.</span></span>
<span data-ttu-id="0d9f9-117">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="0d9f9-117">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="0d9f9-118">Command</span><span class="sxs-lookup"><span data-stu-id="0d9f9-118">Command</span></span> | <span data-ttu-id="0d9f9-119">Observações</span><span class="sxs-lookup"><span data-stu-id="0d9f9-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0d9f9-120">az batch application create</span><span class="sxs-lookup"><span data-stu-id="0d9f9-120">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="0d9f9-121">Criar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d9f9-121">Creates an application.</span></span>  |
| [<span data-ttu-id="0d9f9-122">az batch application set</span><span class="sxs-lookup"><span data-stu-id="0d9f9-122">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="0d9f9-123">Atualiza as propriedades de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d9f9-123">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="0d9f9-124">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="0d9f9-124">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="0d9f9-125">Adiciona um pacote de aplicativos ao aplicativo especificado.</span><span class="sxs-lookup"><span data-stu-id="0d9f9-125">Adds an application package to the specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="0d9f9-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d9f9-126">Next steps</span></span>

<span data-ttu-id="0d9f9-127">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0d9f9-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0d9f9-128">As amostras de script da CLI do Lote adicionais podem ser encontrados na [documentação do Lote do Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0d9f9-128">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
