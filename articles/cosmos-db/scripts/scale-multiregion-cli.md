---
title: "Script da CLI do Azure – replicação em várias regiões para o BD Cosmos do Azure | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – replicação em várias regiões para o BD Cosmos do Azure"
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
ms.openlocfilehash: ab716c28b88412438d0cea80377f9f0f40dc8bd6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-the-azure-cli"></a><span data-ttu-id="1db26-103">Replique uma conta do BD Cosmos do Azure em várias regiões e configure as prioridades de failover usando o a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1db26-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using the Azure CLI</span></span>

<span data-ttu-id="1db26-104">Este exemplo replica qualquer tipo de conta do BD Cosmos do Azure em várias regiões e configura as prioridades de failover usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1db26-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using the Azure CLI.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1db26-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1db26-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1db26-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="1db26-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="1db26-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1db26-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1db26-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="1db26-108">Sample script</span></span>

<span data-ttu-id="1db26-109">[!code-azurecli-interactive[principal](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Dimensionar o BD Cosmos do Azure em várias regiões")]</span><span class="sxs-lookup"><span data-stu-id="1db26-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Scale Azure Cosmos DB into multiple regions")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1db26-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="1db26-110">Clean up deployment</span></span>

<span data-ttu-id="1db26-111">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="1db26-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1db26-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="1db26-112">Script explanation</span></span>

<span data-ttu-id="1db26-113">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="1db26-113">This script uses the following commands.</span></span> <span data-ttu-id="1db26-114">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="1db26-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1db26-115">Command</span><span class="sxs-lookup"><span data-stu-id="1db26-115">Command</span></span> | <span data-ttu-id="1db26-116">Observações</span><span class="sxs-lookup"><span data-stu-id="1db26-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1db26-117">az group create</span><span class="sxs-lookup"><span data-stu-id="1db26-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="1db26-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="1db26-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1db26-119">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="1db26-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="1db26-120">Atualiza uma conta do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1db26-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="1db26-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="1db26-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="1db26-122">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="1db26-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1db26-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1db26-123">Next steps</span></span>

<span data-ttu-id="1db26-124">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1db26-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1db26-125">Exemplos adicionais de scripts da CLI do Banco de Dados Cosmos do Azure podem ser encontrados na [Documentação da CLI do Banco de Dados Cosmos do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1db26-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
