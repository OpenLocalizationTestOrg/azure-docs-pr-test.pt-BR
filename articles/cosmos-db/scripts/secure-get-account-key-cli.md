---
title: chaves de aaaAzure conta Get de Script CLI para o banco de dados do Azure Cosmos | Microsoft Docs
description: "Exemplo de script da CLI do Azure – obter chaves da conta para o BD Cosmos do Azure"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: d6462b3eebc8bc6935a6fa07dcae37a33e5f382e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-hello-azure-cli"></a><span data-ttu-id="11af9-103">Obtenham chaves da conta de banco de dados do Azure Cosmos usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="11af9-103">Get account keys for Azure Cosmos DB using hello Azure CLI</span></span>

<span data-ttu-id="11af9-104">Este exemplo obtém chaves de conta para qualquer tipo de conta do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="11af9-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="11af9-105">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="11af9-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="11af9-106">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="11af9-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="11af9-107">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="11af9-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="11af9-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="11af9-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-get-account-key/secure-cosmosdb-get-account-key.sh?highlight=22-25 "Get Azure Cosmos DB account keys")]

## <a name="clean-up-deployment"></a><span data-ttu-id="11af9-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="11af9-109">Clean up deployment</span></span>

<span data-ttu-id="11af9-110">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="11af9-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="11af9-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="11af9-111">Script explanation</span></span>

<span data-ttu-id="11af9-112">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="11af9-112">This script uses hello following commands.</span></span> <span data-ttu-id="11af9-113">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="11af9-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="11af9-114">Command</span><span class="sxs-lookup"><span data-stu-id="11af9-114">Command</span></span> | <span data-ttu-id="11af9-115">Observações</span><span class="sxs-lookup"><span data-stu-id="11af9-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="11af9-116">az group create</span><span class="sxs-lookup"><span data-stu-id="11af9-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="11af9-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="11af9-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="11af9-118">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="11af9-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="11af9-119">Atualiza uma conta do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="11af9-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="11af9-120">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="11af9-120">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="11af9-121">Cria um servidor lógico hosts Olá banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="11af9-121">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="11af9-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="11af9-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="11af9-123">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="11af9-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="11af9-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11af9-124">Next steps</span></span>

<span data-ttu-id="11af9-125">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="11af9-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="11af9-126">Exemplos de script CLI do Azure Cosmos DB adicionais podem ser encontrados no hello [documentação CLI de banco de dados do Azure Cosmos](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="11af9-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
