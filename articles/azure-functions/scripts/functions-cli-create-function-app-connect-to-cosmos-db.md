---
title: "aaaCreate uma função do Azure que se conecta tooan banco de dados do Azure Cosmos | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar uma função do Azure que se conecta tooan Azure Cosmos DB"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a><span data-ttu-id="d11cd-103">Criar uma função do Azure que se conecta tooan Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d11cd-103">Create an Azure Function that connects tooan Azure Cosmos DB</span></span>

<span data-ttu-id="d11cd-104">Esse script de exemplo cria um aplicativo de função do Azure e conecta-se o banco de dados de banco de dados do Azure Cosmos tooan.</span><span class="sxs-lookup"><span data-stu-id="d11cd-104">This sample script creates an Azure Function App and connects tooan Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d11cd-105">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="d11cd-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d11cd-106">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d11cd-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d11cd-107">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d11cd-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d11cd-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="d11cd-108">Sample script</span></span>

<span data-ttu-id="d11cd-109">Este exemplo cria um aplicativo de função do Azure e adiciona uma configuração de chave tooapp Cosmos DB ponto de extremidade e acesso.</span><span class="sxs-lookup"><span data-stu-id="d11cd-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key tooapp settings.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d11cd-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="d11cd-110">Clean up deployment</span></span>

<span data-ttu-id="d11cd-111">Após a execução do exemplo de script hello, Olá acompanhamento pode ser usado tooremove grupo de recursos de saudação e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="d11cd-111">After hello script sample has been run, hello follow command can be used tooremove hello resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d11cd-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="d11cd-112">Script explanation</span></span>

<span data-ttu-id="d11cd-113">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="d11cd-113">This script uses hello following commands.</span></span> <span data-ttu-id="d11cd-114">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="d11cd-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d11cd-115">Command</span><span class="sxs-lookup"><span data-stu-id="d11cd-115">Command</span></span> | <span data-ttu-id="d11cd-116">Observações</span><span class="sxs-lookup"><span data-stu-id="d11cd-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d11cd-117">az login</span><span class="sxs-lookup"><span data-stu-id="d11cd-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="d11cd-118">TooAzure de logon.</span><span class="sxs-lookup"><span data-stu-id="d11cd-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="d11cd-119">az group create</span><span class="sxs-lookup"><span data-stu-id="d11cd-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d11cd-120">Criar um grupo de recursos com local</span><span class="sxs-lookup"><span data-stu-id="d11cd-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="d11cd-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="d11cd-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="d11cd-122">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="d11cd-122">Create a storage account</span></span> |
| [<span data-ttu-id="d11cd-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="d11cd-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="d11cd-124">Criar um novo aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="d11cd-124">Create a new function app</span></span> |
| [<span data-ttu-id="d11cd-125">az documentdb create</span><span class="sxs-lookup"><span data-stu-id="d11cd-125">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="d11cd-126">Criar banco de dados do documentdb</span><span class="sxs-lookup"><span data-stu-id="d11cd-126">Create documentdb database</span></span> |
| [<span data-ttu-id="d11cd-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="d11cd-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="d11cd-128">Limpar</span><span class="sxs-lookup"><span data-stu-id="d11cd-128">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d11cd-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d11cd-129">Next steps</span></span>

<span data-ttu-id="d11cd-130">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d11cd-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d11cd-131">Exemplos de script CLI do Azure funções adicionais podem ser encontrados no hello [documentação de funções do Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d11cd-131">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>




