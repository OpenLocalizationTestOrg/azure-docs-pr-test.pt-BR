---
title: Exemplo da CLI para criar um banco de dados SQL do Azure | Microsoft Docs
description: Script de exemplo da CLI do Azure para criar um banco de dados SQL
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
ms.openlocfilehash: 908898ca691d2b53b9f54afa60c41e091163bd50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="c6d96-103">Use a CLI para criar um banco de dados SQL do Azure individual e configurar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="c6d96-103">Use CLI to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="c6d96-104">Este exemplo de script de CLI do Azure cria um banco de dados SQL do Azure e configura uma regra de firewall no nível do servidor.</span><span class="sxs-lookup"><span data-stu-id="c6d96-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="c6d96-105">Depois que o script tiver sido executado com êxito, o Banco de Dados SQL poderá ser acessado de todos os serviços do Azure e o endereço IP configurado.</span><span class="sxs-lookup"><span data-stu-id="c6d96-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c6d96-106">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c6d96-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c6d96-107">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="c6d96-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="c6d96-108">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c6d96-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c6d96-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="c6d96-109">Sample script</span></span>

<span data-ttu-id="c6d96-110">[!code-azurecli-interactive[principal](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Criar Banco de Dados SQL")]</span><span class="sxs-lookup"><span data-stu-id="c6d96-110">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c6d96-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="c6d96-111">Clean up deployment</span></span>

<span data-ttu-id="c6d96-112">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="c6d96-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c6d96-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="c6d96-113">Script explanation</span></span>

<span data-ttu-id="c6d96-114">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="c6d96-114">This script uses the following commands.</span></span> <span data-ttu-id="c6d96-115">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="c6d96-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c6d96-116">Command</span><span class="sxs-lookup"><span data-stu-id="c6d96-116">Command</span></span> | <span data-ttu-id="c6d96-117">Observações</span><span class="sxs-lookup"><span data-stu-id="c6d96-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c6d96-118">az group create</span><span class="sxs-lookup"><span data-stu-id="c6d96-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="c6d96-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="c6d96-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c6d96-120">az sql server create</span><span class="sxs-lookup"><span data-stu-id="c6d96-120">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="c6d96-121">Cria um servidor lógico que hospeda o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="c6d96-121">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="c6d96-122">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="c6d96-122">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="c6d96-123">Cria uma regra de firewall para permitir o acesso a todos os bancos de dados SQL no servidor do intervalo de endereços IP inserido.</span><span class="sxs-lookup"><span data-stu-id="c6d96-123">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="c6d96-124">az sql db create</span><span class="sxs-lookup"><span data-stu-id="c6d96-124">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="c6d96-125">Cria o Banco de Dados SQL no servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="c6d96-125">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="c6d96-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="c6d96-126">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="c6d96-127">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="c6d96-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c6d96-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6d96-128">Next steps</span></span>

<span data-ttu-id="c6d96-129">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c6d96-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c6d96-130">Os exemplos de script da CLI do Banco de Dados SQL adicionais podem ser encontrados na [documentação do Banco de Dados SQL do Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c6d96-130">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

