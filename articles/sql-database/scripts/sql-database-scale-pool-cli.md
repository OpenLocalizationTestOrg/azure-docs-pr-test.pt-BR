---
title: "exemplo de aaaCLI dimensiona Elástico pool Azure SQL banco de dados SQL | Microsoft Docs"
description: "CLI exemplo script tooscale um pool Elástico do SQL no banco de dados SQL do Azure"
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
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="547da-103">Usar CLI tooscale um pool Elástico do SQL no banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="547da-103">Use CLI tooscale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="547da-104">Este exemplo de script da CLI do Azure cria pools elásticos do SQL, move os bancos de dados em pools e altera os níveis de desempenho do pool elástico.</span><span class="sxs-lookup"><span data-stu-id="547da-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="547da-105">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="547da-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="547da-106">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="547da-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="547da-107">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="547da-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="547da-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="547da-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="547da-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="547da-109">Clean up deployment</span></span>

<span data-ttu-id="547da-110">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="547da-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="547da-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="547da-111">Script explanation</span></span>

<span data-ttu-id="547da-112">Esse script usa Olá comandos toocreate um grupo de recursos, servidor lógico, banco de dados SQL e as regras de firewall a seguir.</span><span class="sxs-lookup"><span data-stu-id="547da-112">This script uses hello following commands toocreate a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="547da-113">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="547da-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="547da-114">Command</span><span class="sxs-lookup"><span data-stu-id="547da-114">Command</span></span> | <span data-ttu-id="547da-115">Observações</span><span class="sxs-lookup"><span data-stu-id="547da-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="547da-116">az group create</span><span class="sxs-lookup"><span data-stu-id="547da-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="547da-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="547da-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="547da-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="547da-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="547da-119">Cria um servidor lógico hosts Olá banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="547da-119">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="547da-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="547da-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="547da-121">Cria um pool Elástico de banco de dados no servidor lógico hello.</span><span class="sxs-lookup"><span data-stu-id="547da-121">Creates an elastic database pool within hello logical server.</span></span> |
| [<span data-ttu-id="547da-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="547da-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="547da-123">Cria Olá banco de dados SQL no servidor lógico hello.</span><span class="sxs-lookup"><span data-stu-id="547da-123">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="547da-124">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="547da-124">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="547da-125">Atualiza um pool Elástico de banco de dados, na saudação de alterações neste exemplo atribuído eDTU.</span><span class="sxs-lookup"><span data-stu-id="547da-125">Updates an elastic database pool, in this example changes hello assigned eDTU.</span></span> |
| [<span data-ttu-id="547da-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="547da-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="547da-127">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="547da-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="547da-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="547da-128">Next steps</span></span>

<span data-ttu-id="547da-129">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="547da-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="547da-130">Exemplos de script CLI do banco de dados SQL adicionais podem ser encontrados no hello [documentação de banco de dados do Azure SQL](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="547da-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
