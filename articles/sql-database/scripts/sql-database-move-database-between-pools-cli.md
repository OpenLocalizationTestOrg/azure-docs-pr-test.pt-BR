---
title: "pool Elástico do banco de dados SQL aaaCLI exemplo move SQL do Azure | Microsoft Docs"
description: "CLI exemplo script toomove um banco de dados SQL em um pool Elástico do SQL Azure"
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
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="216cb-103">Usar CLI toomove um banco de dados do SQL Azure em um pool Elástico do SQL</span><span class="sxs-lookup"><span data-stu-id="216cb-103">Use CLI toomove an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="216cb-104">Este exemplo de script CLI do Azure cria dois pools Elásticos move um banco de dados do SQL Azure de um pool Elástico do SQL em outro pool Elástico do SQL e, em seguida, move o banco de dados de saudação fora do nível de desempenho do pool Elástico tooa único banco de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="216cb-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves hello database out of elastic pool tooa single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="216cb-105">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="216cb-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="216cb-106">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="216cb-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="216cb-107">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="216cb-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="216cb-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="216cb-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="216cb-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="216cb-109">Clean up deployment</span></span>

<span data-ttu-id="216cb-110">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="216cb-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="216cb-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="216cb-111">Script explanation</span></span>

<span data-ttu-id="216cb-112">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="216cb-112">This script uses hello following commands.</span></span> <span data-ttu-id="216cb-113">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="216cb-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="216cb-114">Command</span><span class="sxs-lookup"><span data-stu-id="216cb-114">Command</span></span> | <span data-ttu-id="216cb-115">Observações</span><span class="sxs-lookup"><span data-stu-id="216cb-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="216cb-116">az group create</span><span class="sxs-lookup"><span data-stu-id="216cb-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="216cb-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="216cb-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="216cb-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="216cb-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="216cb-119">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="216cb-119">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="216cb-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="216cb-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="216cb-121">Cria um pool Elástico no servidor lógico hello.</span><span class="sxs-lookup"><span data-stu-id="216cb-121">Creates an elastic pool within hello logical server.</span></span> |
| [<span data-ttu-id="216cb-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="216cb-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="216cb-123">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="216cb-123">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="216cb-124">az sql db update</span><span class="sxs-lookup"><span data-stu-id="216cb-124">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="216cb-125">Atualiza as propriedades do banco de dados ou move um banco de dados para dentro, para fora entre pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="216cb-125">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="216cb-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="216cb-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="216cb-127">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="216cb-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="216cb-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="216cb-128">Next steps</span></span>

<span data-ttu-id="216cb-129">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="216cb-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="216cb-130">Exemplos de script CLI do banco de dados SQL adicionais podem ser encontrados no hello [documentação de banco de dados do Azure SQL](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="216cb-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


