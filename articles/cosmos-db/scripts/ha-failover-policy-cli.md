---
title: "Script da CLI do Azure – criar uma política de failover para alta disponibilidade | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – criar uma política de failover para alta disponibilidade"
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
ms.openlocfilehash: 96083d66cc1a2ef179f9313c1b3ed04162c1c048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-failover-policy-for-high-availability-using-the-azure-cli"></a><span data-ttu-id="48ef5-103">Crie uma política de failover para alta disponibilidade usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="48ef5-103">Create a failover policy for high availability using the Azure CLI</span></span>

<span data-ttu-id="48ef5-104">Este exemplo de script da CLI cria uma conta do BD Cosmos do Azure e, em seguida, a configura para alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="48ef5-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="48ef5-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="48ef5-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="48ef5-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="48ef5-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="48ef5-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="48ef5-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="48ef5-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="48ef5-108">Sample script</span></span>

<span data-ttu-id="48ef5-109">[!code-azurecli-interactive[principal](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Criar uma política de failover do BD Cosmos do Azure")]</span><span class="sxs-lookup"><span data-stu-id="48ef5-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Create an Azure Cosmos DB failover policy")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="48ef5-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="48ef5-110">Clean up deployment</span></span>

<span data-ttu-id="48ef5-111">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="48ef5-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="48ef5-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="48ef5-112">Script explanation</span></span>

<span data-ttu-id="48ef5-113">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="48ef5-113">This script uses the following commands.</span></span> <span data-ttu-id="48ef5-114">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="48ef5-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="48ef5-115">Command</span><span class="sxs-lookup"><span data-stu-id="48ef5-115">Command</span></span> | <span data-ttu-id="48ef5-116">Observações</span><span class="sxs-lookup"><span data-stu-id="48ef5-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="48ef5-117">az group create</span><span class="sxs-lookup"><span data-stu-id="48ef5-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="48ef5-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="48ef5-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="48ef5-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="48ef5-119">az cosmosdb create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="48ef5-120">Cria uma conta do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="48ef5-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="48ef5-121">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="48ef5-121">az cosmosdb update</span></span>](/cli/azure/cosmosdb#update) | <span data-ttu-id="48ef5-122">Atualiza uma conta do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="48ef5-122">Updates Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="48ef5-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="48ef5-123">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="48ef5-124">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="48ef5-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="48ef5-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48ef5-125">Next steps</span></span>

<span data-ttu-id="48ef5-126">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="48ef5-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="48ef5-127">Exemplos adicionais de scripts da CLI do Banco de Dados Cosmos do Azure podem ser encontrados na [Documentação da CLI do Banco de Dados Cosmos do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="48ef5-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
