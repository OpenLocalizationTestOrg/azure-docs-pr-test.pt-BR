---
title: chave de conta de banco de dados do CLI gere novamente o Script do Azure Cosmos aaaAzure | Microsoft Docs
description: "Exemplo de script da CLI do Azure – regenerar uma chave de conta do BD Cosmos do Azure"
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
ms.openlocfilehash: ca77e05039775c90d7541899eeffc45a76d60657
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="regenerate-an-azure-cosmos-db-account-key-using-hello-azure-cli"></a><span data-ttu-id="40153-103">Regenerar uma chave de conta do banco de dados do Azure Cosmos usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="40153-103">Regenerate an Azure Cosmos DB account key using hello Azure CLI</span></span>

<span data-ttu-id="40153-104">Este exemplo gera novamente a qualquer tipo de chave de conta de banco de dados do Azure Cosmos usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="40153-104">This sample regenerates any kind of Azure Cosmos DB account key using hello Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="40153-105">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="40153-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="40153-106">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="40153-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="40153-107">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="40153-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="40153-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="40153-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-regenerate-keys/secure-cosmosdb-regenerate-keys.sh?highlight=27-31 "Regenerate Azure Cosmos DB account keys")]

## <a name="clean-up-deployment"></a><span data-ttu-id="40153-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="40153-109">Clean up deployment</span></span>

<span data-ttu-id="40153-110">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="40153-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="40153-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="40153-111">Script explanation</span></span>

<span data-ttu-id="40153-112">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="40153-112">This script uses hello following commands.</span></span> <span data-ttu-id="40153-113">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="40153-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="40153-114">Command</span><span class="sxs-lookup"><span data-stu-id="40153-114">Command</span></span> | <span data-ttu-id="40153-115">Observações</span><span class="sxs-lookup"><span data-stu-id="40153-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="40153-116">az group create</span><span class="sxs-lookup"><span data-stu-id="40153-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="40153-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="40153-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="40153-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="40153-118">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#create) | <span data-ttu-id="40153-119">Atualiza uma conta do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="40153-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="40153-120">az cosmosdb regenerate-key</span><span class="sxs-lookup"><span data-stu-id="40153-120">az cosmosdb regenerate-key</span></span>](/cli/azure/cosmosdb/regenerate-key) | <span data-ttu-id="40153-121">Regenera chaves de conta do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="40153-121">Regeneratates Azure Cosmos DB account keys.</span></span> |
| [<span data-ttu-id="40153-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="40153-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="40153-123">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="40153-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="40153-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="40153-124">Next steps</span></span>

<span data-ttu-id="40153-125">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="40153-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="40153-126">Exemplos de script CLI do Azure Cosmos DB adicionais podem ser encontrados no hello [documentação CLI de banco de dados do Azure Cosmos](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="40153-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
