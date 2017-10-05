---
title: "Script da CLI do Azure – taxa de transferência do contêiner do BD Cosmos do Azure | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – taxa de transferência do contêiner do BD Cosmos do Azure"
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
ms.openlocfilehash: f08733cd4074c7144b20a0592522423e729e6f1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-the-azure-cli"></a><span data-ttu-id="da1b5-103">Dimensione a taxa de transferência do contêiner do BD Cosmos do Azure usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="da1b5-103">Scale Azure Cosmos DB container throughput using the Azure CLI</span></span>

<span data-ttu-id="da1b5-104">Este exemplo dimensiona a taxa de transferência do contêiner para qualquer tipo de contêiner do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="da1b5-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="da1b5-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="da1b5-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="da1b5-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="da1b5-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="da1b5-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="da1b5-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="da1b5-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="da1b5-108">Sample script</span></span>

<span data-ttu-id="da1b5-109">[!code-azurecli-interactive[principal](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Taxa de transferência do BD Cosmos do Azure")]</span><span class="sxs-lookup"><span data-stu-id="da1b5-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="da1b5-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="da1b5-110">Clean up deployment</span></span>

<span data-ttu-id="da1b5-111">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="da1b5-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="da1b5-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="da1b5-112">Script explanation</span></span>

<span data-ttu-id="da1b5-113">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="da1b5-113">This script uses the following commands.</span></span> <span data-ttu-id="da1b5-114">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="da1b5-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="da1b5-115">Command</span><span class="sxs-lookup"><span data-stu-id="da1b5-115">Command</span></span> | <span data-ttu-id="da1b5-116">Observações</span><span class="sxs-lookup"><span data-stu-id="da1b5-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="da1b5-117">az group create</span><span class="sxs-lookup"><span data-stu-id="da1b5-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="da1b5-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="da1b5-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="da1b5-119">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="da1b5-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="da1b5-120">Atualiza uma conta do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="da1b5-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="da1b5-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="da1b5-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="da1b5-122">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="da1b5-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="da1b5-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="da1b5-123">Next steps</span></span>

<span data-ttu-id="da1b5-124">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="da1b5-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="da1b5-125">Exemplos adicionais de scripts da CLI do Banco de Dados Cosmos do Azure podem ser encontrados na [Documentação da CLI do Banco de Dados Cosmos do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="da1b5-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
