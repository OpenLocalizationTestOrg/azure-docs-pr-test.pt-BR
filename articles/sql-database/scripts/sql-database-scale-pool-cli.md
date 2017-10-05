---
title: "O exemplo de CLI dimensiona um pool elástico do banco de dados SQL do Azure | Microsoft Docs"
description: "Script de exemplo da CLI do Azure para dimensionar um pool elástico do SQL no Banco de Dados SQL do Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 888d2b7b7c118fede82d39881570a3b3d7b09961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-cli-to-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="1e100-103">Use a CLI para dimensionar um pool elástico no Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="1e100-103">Use CLI to scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="1e100-104">Este exemplo de script da CLI do Azure cria pools elásticos do SQL, move os bancos de dados em pools e altera os níveis de desempenho do pool elástico.</span><span class="sxs-lookup"><span data-stu-id="1e100-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1e100-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1e100-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1e100-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="1e100-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="1e100-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1e100-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1e100-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="1e100-108">Sample script</span></span>

<span data-ttu-id="1e100-109">[!code-azurecli-interactive[principal](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Mover banco de dados entre pools")]</span><span class="sxs-lookup"><span data-stu-id="1e100-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1e100-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="1e100-110">Clean up deployment</span></span>

<span data-ttu-id="1e100-111">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="1e100-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1e100-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="1e100-112">Script explanation</span></span>

<span data-ttu-id="1e100-113">Este script usa os comandos a seguir para criar um grupo de recursos, um servidor lógico, um Banco de Dados SQL e as regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="1e100-113">This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="1e100-114">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="1e100-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1e100-115">Command</span><span class="sxs-lookup"><span data-stu-id="1e100-115">Command</span></span> | <span data-ttu-id="1e100-116">Observações</span><span class="sxs-lookup"><span data-stu-id="1e100-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1e100-117">az group create</span><span class="sxs-lookup"><span data-stu-id="1e100-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1e100-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="1e100-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1e100-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="1e100-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="1e100-120">Cria um servidor lógico que hospeda o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="1e100-120">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="1e100-121">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="1e100-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="1e100-122">Cria um pool de banco de dados elástico dentro do servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="1e100-122">Creates an elastic database pool within the logical server.</span></span> |
| [<span data-ttu-id="1e100-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="1e100-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="1e100-124">Cria o Banco de Dados SQL no servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="1e100-124">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="1e100-125">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="1e100-125">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="1e100-126">Atualiza um pool de banco de dados elástico, neste exemplo altera o eDTU atribuído.</span><span class="sxs-lookup"><span data-stu-id="1e100-126">Updates an elastic database pool, in this example changes the assigned eDTU.</span></span> |
| [<span data-ttu-id="1e100-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="1e100-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="1e100-128">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="1e100-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1e100-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1e100-129">Next steps</span></span>

<span data-ttu-id="1e100-130">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1e100-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1e100-131">Os exemplos de script da CLI do Banco de Dados SQL adicionais podem ser encontrados na [documentação do Banco de Dados SQL do Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1e100-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
