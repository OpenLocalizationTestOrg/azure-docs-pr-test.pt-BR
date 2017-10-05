---
title: "Exemplo de CLI para mover um pool elástico do banco de dados SQL do Azure | Microsoft Docs"
description: "Script de exemplo da CLI do Azure para mover um banco de dados SQL em um pool elástico do SQL"
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
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 1dc31a0b20f36e28a58896ed63a5e0395ae1d3af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-move-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="5a92b-103">Usar a CLI para mover um banco de dados SQL do Azure em um pool elástico do SQL</span><span class="sxs-lookup"><span data-stu-id="5a92b-103">Use CLI to move an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="5a92b-104">Este exemplo de script da CLI do Azure cria dois pools elásticos e move um banco de dados SQL do Azure de um pool elástico do SQL para outro pool elástico do SQL, depois move um banco de dados de um pool elástico para um nível de desempenho de banco de dados individual.</span><span class="sxs-lookup"><span data-stu-id="5a92b-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves the database out of elastic pool to a single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5a92b-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5a92b-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5a92b-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="5a92b-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="5a92b-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5a92b-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5a92b-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="5a92b-108">Sample script</span></span>

<span data-ttu-id="5a92b-109">[!code-azurecli-interactive[principal](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Mover banco de dados entre pools")]</span><span class="sxs-lookup"><span data-stu-id="5a92b-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5a92b-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="5a92b-110">Clean up deployment</span></span>

<span data-ttu-id="5a92b-111">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="5a92b-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5a92b-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="5a92b-112">Script explanation</span></span>

<span data-ttu-id="5a92b-113">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="5a92b-113">This script uses the following commands.</span></span> <span data-ttu-id="5a92b-114">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="5a92b-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5a92b-115">Command</span><span class="sxs-lookup"><span data-stu-id="5a92b-115">Command</span></span> | <span data-ttu-id="5a92b-116">Observações</span><span class="sxs-lookup"><span data-stu-id="5a92b-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5a92b-117">az group create</span><span class="sxs-lookup"><span data-stu-id="5a92b-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5a92b-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="5a92b-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5a92b-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="5a92b-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="5a92b-120">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="5a92b-120">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="5a92b-121">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="5a92b-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="5a92b-122">Cria um pool elástico dentro do servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="5a92b-122">Creates an elastic pool within the logical server.</span></span> |
| [<span data-ttu-id="5a92b-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="5a92b-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="5a92b-124">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="5a92b-124">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="5a92b-125">az sql db update</span><span class="sxs-lookup"><span data-stu-id="5a92b-125">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="5a92b-126">Atualiza as propriedades do banco de dados ou move um banco de dados para dentro, para fora entre pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="5a92b-126">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="5a92b-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="5a92b-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5a92b-128">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="5a92b-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5a92b-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a92b-129">Next steps</span></span>

<span data-ttu-id="5a92b-130">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5a92b-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5a92b-131">Os exemplos de script da CLI do Banco de Dados SQL adicionais podem ser encontrados na [documentação do Banco de Dados SQL do Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5a92b-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


