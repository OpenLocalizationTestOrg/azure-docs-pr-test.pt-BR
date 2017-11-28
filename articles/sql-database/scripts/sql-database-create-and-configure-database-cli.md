---
title: aaaCLI exemplo-criar um banco de dados SQL do Azure | Microsoft Docs
description: CLI exemplo script toocreate um banco de dados do SQL Azure
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 0d54e284e19f16387813e24d7beb7ab048a39263
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="5660a-103">Use CLI toocreate um único banco de dados do SQL Azure e configurar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="5660a-103">Use CLI toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="5660a-104">Este exemplo de script de CLI do Azure cria um banco de dados SQL do Azure e configura uma regra de firewall no nível do servidor.</span><span class="sxs-lookup"><span data-stu-id="5660a-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="5660a-105">Depois que o script hello foi executado com êxito, Olá que banco de dados SQL podem ser acessado de todos os serviços do Azure e hello endereço IP configurado.</span><span class="sxs-lookup"><span data-stu-id="5660a-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5660a-106">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5660a-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5660a-107">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5660a-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5660a-108">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5660a-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5660a-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="5660a-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5660a-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="5660a-110">Clean up deployment</span></span>

<span data-ttu-id="5660a-111">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="5660a-111">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5660a-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="5660a-112">Script explanation</span></span>

<span data-ttu-id="5660a-113">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="5660a-113">This script uses hello following commands.</span></span> <span data-ttu-id="5660a-114">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="5660a-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5660a-115">Command</span><span class="sxs-lookup"><span data-stu-id="5660a-115">Command</span></span> | <span data-ttu-id="5660a-116">Observações</span><span class="sxs-lookup"><span data-stu-id="5660a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5660a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="5660a-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="5660a-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="5660a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5660a-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="5660a-119">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="5660a-120">Cria um servidor lógico hosts Olá banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="5660a-120">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="5660a-121">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="5660a-121">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="5660a-122">Cria um firewall regra tooallow acesso tooall bancos de dados SQL no servidor de saudação do intervalo de endereços IP hello inserido.</span><span class="sxs-lookup"><span data-stu-id="5660a-122">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="5660a-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="5660a-123">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="5660a-124">Cria Olá banco de dados SQL no servidor lógico hello.</span><span class="sxs-lookup"><span data-stu-id="5660a-124">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="5660a-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="5660a-125">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="5660a-126">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="5660a-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5660a-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5660a-127">Next steps</span></span>

<span data-ttu-id="5660a-128">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5660a-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5660a-129">Exemplos de script CLI do banco de dados SQL adicionais podem ser encontrados no hello [documentação de banco de dados do Azure SQL](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5660a-129">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

