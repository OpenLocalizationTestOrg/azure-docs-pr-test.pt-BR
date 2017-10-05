---
title: "Script da CLI do Azure - Criar uma conta, banco de dados e coleção da API do MongoDB de Banco de Dados Cosmo do Azure | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Criar uma conta, banco de dados e coleção da API de MongoDB de Banco de Dados Cosmo do Azure"
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
ms.openlocfilehash: b0bf637db90cfcb987ad43ed34cb8065d28b0fcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-an-mongodb-api-account-using-the-azure-cli"></a><span data-ttu-id="be55a-103">Banco de Dados Cosmos do Azure: Criar uma conta da API do MongoDB usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="be55a-103">Azure Cosmos DB: Create an MongoDB API account using the Azure CLI</span></span>

<span data-ttu-id="be55a-104">Este exemplo de script da CLI cria uma conta, banco de dados e coleção da API de MongoDB de Banco de Dados Cosmo do Azure.</span><span class="sxs-lookup"><span data-stu-id="be55a-104">This sample CLI script creates an Azure Cosmos DB MongoDB API account, database, and collection.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="be55a-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="be55a-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="be55a-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="be55a-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="be55a-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="be55a-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="be55a-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="be55a-108">Sample script</span></span>

<span data-ttu-id="be55a-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-mongodb-account/create-cosmosdb-mongodb-account.sh?highlight=15-35 "Criar uma conta, banco de dados e coleção da API de MongoDB de Banco de Dados Cosmo do Azure")]</span><span class="sxs-lookup"><span data-stu-id="be55a-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-mongodb-account/create-cosmosdb-mongodb-account.sh?highlight=15-35 "Create an Azure Cosmos DB MongoDB API account, database, and collection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="be55a-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="be55a-110">Clean up deployment</span></span>

<span data-ttu-id="be55a-111">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="be55a-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="be55a-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="be55a-112">Script explanation</span></span>

<span data-ttu-id="be55a-113">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="be55a-113">This script uses the following commands.</span></span> <span data-ttu-id="be55a-114">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="be55a-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="be55a-115">Command</span><span class="sxs-lookup"><span data-stu-id="be55a-115">Command</span></span> | <span data-ttu-id="be55a-116">Observações</span><span class="sxs-lookup"><span data-stu-id="be55a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="be55a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="be55a-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="be55a-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="be55a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="be55a-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="be55a-119">az cosmosdb create</span></span>](/cli/azure/cosmosdb#create) | <span data-ttu-id="be55a-120">Cria uma conta do Banco de Dados Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="be55a-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="be55a-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="be55a-121">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="be55a-122">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="be55a-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="be55a-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be55a-123">Next steps</span></span>

<span data-ttu-id="be55a-124">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="be55a-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="be55a-125">Exemplos adicionais de scripts da CLI do Banco de Dados Cosmos do Azure podem ser encontrados na [Documentação da CLI do Banco de Dados Cosmos do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="be55a-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
