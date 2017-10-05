---
title: "Script da CLI do Azure – criar um Banco de Dados do Azure para PostgreSQL | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – cria um Banco de Dados do Azure para servidor PostgreSQL e configura uma regra de firewall no nível do servidor."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: e545b568cd57fdcf28ab33a5ebfa34a495111c7f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="12b04-103">Crie um Banco de Dados do Azure para servidor PostgreSQL e configure uma regra de firewall usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="12b04-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="12b04-104">Este exemplo de script da CLI cria um Banco de Dados do Azure para servidor PostgreSQL e configura uma regra de firewall no nível do servidor.</span><span class="sxs-lookup"><span data-stu-id="12b04-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="12b04-105">Depois que o script tiver sido executado com êxito, o servidor PostgreSQL poderá ser acessado de todos os serviços do Azure e o endereço IP configurado.</span><span class="sxs-lookup"><span data-stu-id="12b04-105">Once the script has been successfully run, the PostgreSQL server can be accessed from all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="12b04-106">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="12b04-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="12b04-107">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="12b04-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="12b04-108">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="12b04-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="12b04-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="12b04-109">Sample script</span></span>
<span data-ttu-id="12b04-110">Neste script de exemplo, edite as linhas destacadas para personalizar o nome de usuário administrador e a senha.</span><span class="sxs-lookup"><span data-stu-id="12b04-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="12b04-111">[!code-azurecli-interactive[principal](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Criar um banco de dados do Azure para PostgreSQL e a regra de firewall de nível de servidor.")]</span><span class="sxs-lookup"><span data-stu-id="12b04-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="12b04-112">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="12b04-112">Clean up deployment</span></span>
<span data-ttu-id="12b04-113">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="12b04-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="12b04-114">[!code-azurecli-interactive[principal](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Excluir o grupo de recursos.")]</span><span class="sxs-lookup"><span data-stu-id="12b04-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="12b04-115">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="12b04-115">Script explanation</span></span>
<span data-ttu-id="12b04-116">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="12b04-116">This script uses the following commands.</span></span> <span data-ttu-id="12b04-117">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="12b04-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="12b04-118">**Comando**</span><span class="sxs-lookup"><span data-stu-id="12b04-118">**Command**</span></span> | <span data-ttu-id="12b04-119">**Observações**</span><span class="sxs-lookup"><span data-stu-id="12b04-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="12b04-120">az group create</span><span class="sxs-lookup"><span data-stu-id="12b04-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="12b04-121">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="12b04-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="12b04-122">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="12b04-122">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="12b04-123">Cria um servidor PostgreSQL que hospeda os bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="12b04-123">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="12b04-124">az postgres server firewall create</span><span class="sxs-lookup"><span data-stu-id="12b04-124">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="12b04-125">Cria uma regra de firewall para permitir o acesso ao servidor e aos bancos de dados contidos nele no intervalo de endereços IP inserido.</span><span class="sxs-lookup"><span data-stu-id="12b04-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="12b04-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="12b04-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="12b04-127">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="12b04-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="12b04-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12b04-128">Next steps</span></span>
- <span data-ttu-id="12b04-129">Leia mais sobre a CLI do Azure: [Documentação da CLI do Azure](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="12b04-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="12b04-130">Experimente scripts adicionais: [exemplos da CLI do Azure para o Banco de Dados do Azure para PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="12b04-130">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
