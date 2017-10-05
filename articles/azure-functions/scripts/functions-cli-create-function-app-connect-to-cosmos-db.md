---
title: "Criar uma Função do Azure que se conecta a um Azure Cosmos DB | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – Criar uma Função do Azure que se conecta a um BD do Azure Cosmos"
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
ms.openlocfilehash: ba7e934f71824493f29b001cea6dd1c567ef3414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-that-connects-to-an-azure-cosmos-db"></a><span data-ttu-id="24ce7-103">Criar um Azure Function que se conecta a um Banco de Dados Cosmo do Azure</span><span class="sxs-lookup"><span data-stu-id="24ce7-103">Create an Azure Function that connects to an Azure Cosmos DB</span></span>

<span data-ttu-id="24ce7-104">Este exemplo de script cria um Aplicativo de funções do Azure e se conecta a um banco de dados do Banco de Dados Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="24ce7-104">This sample script creates an Azure Function App and connects to an Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="24ce7-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="24ce7-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="24ce7-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="24ce7-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="24ce7-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="24ce7-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="24ce7-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="24ce7-108">Sample script</span></span>

<span data-ttu-id="24ce7-109">Este exemplo cria um Aplicativo de funções do Azure e adiciona uma chave de acesso e um ponto de extremidade de BD do Cosmos para configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="24ce7-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key to app settings.</span></span>

<span data-ttu-id="24ce7-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Criar um Azure Function que se conecta a um Banco de Dados Cosmo do Azure")]</span><span class="sxs-lookup"><span data-stu-id="24ce7-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects to an Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="24ce7-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="24ce7-111">Clean up deployment</span></span>

<span data-ttu-id="24ce7-112">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="24ce7-112">After the script sample has been run, the follow command can be used to remove the resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="24ce7-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="24ce7-113">Script explanation</span></span>

<span data-ttu-id="24ce7-114">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="24ce7-114">This script uses the following commands.</span></span> <span data-ttu-id="24ce7-115">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="24ce7-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="24ce7-116">Command</span><span class="sxs-lookup"><span data-stu-id="24ce7-116">Command</span></span> | <span data-ttu-id="24ce7-117">Observações</span><span class="sxs-lookup"><span data-stu-id="24ce7-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="24ce7-118">az login</span><span class="sxs-lookup"><span data-stu-id="24ce7-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="24ce7-119">Logon no Azure.</span><span class="sxs-lookup"><span data-stu-id="24ce7-119">Login to Azure.</span></span> |
| [<span data-ttu-id="24ce7-120">az group create</span><span class="sxs-lookup"><span data-stu-id="24ce7-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="24ce7-121">Criar um grupo de recursos com local</span><span class="sxs-lookup"><span data-stu-id="24ce7-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="24ce7-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="24ce7-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="24ce7-123">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="24ce7-123">Create a storage account</span></span> |
| [<span data-ttu-id="24ce7-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="24ce7-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="24ce7-125">Criar um novo aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="24ce7-125">Create a new function app</span></span> |
| [<span data-ttu-id="24ce7-126">az documentdb create</span><span class="sxs-lookup"><span data-stu-id="24ce7-126">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="24ce7-127">Criar banco de dados do documentdb</span><span class="sxs-lookup"><span data-stu-id="24ce7-127">Create documentdb database</span></span> |
| [<span data-ttu-id="24ce7-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="24ce7-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="24ce7-129">Limpar</span><span class="sxs-lookup"><span data-stu-id="24ce7-129">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="24ce7-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="24ce7-130">Next steps</span></span>

<span data-ttu-id="24ce7-131">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="24ce7-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="24ce7-132">Exemplos adicionais de scripts da CLI do Azure Functions podem ser encontrados na [Documentação do Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="24ce7-132">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>




