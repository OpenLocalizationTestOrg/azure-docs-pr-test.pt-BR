---
title: Criar e gerenciar regras de firewall do Banco de Dados do Azure para PostgreSQL usando a CLI do Azure | Microsoft Docs
description: Este artigo descreve como criar e gerenciar regras de firewall do banco de dados do Azure para PostgreSQL usando a linha de comando CLI do Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 6f081416dd7d78f0153b3fda21a340a8c1a70c5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="9697f-103">Criar e gerenciar regras de firewall do Banco de Dados do Azure para PostgreSQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9697f-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="9697f-104">As regras de firewall no nível de servidor permitem que os administradores gerenciem o acesso a um Banco de Dados SQL do Azure para servidor PostgreSQL de um endereço IP específico ou intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="9697f-104">Server-level firewall rules enable administrators to manage access to an Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="9697f-105">Usando comandos convenientes da CLI do Azure, você pode criar, atualizar, excluir, listar e mostrar as regras de firewall para gerenciar o servidor.</span><span class="sxs-lookup"><span data-stu-id="9697f-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="9697f-106">Para obter uma visão geral dos firewalls do Banco de Dados do Azure para PostgreSQL, confira [Regras de firewall do servidor de Banco de Dados do Azure para PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="9697f-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9697f-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9697f-107">Prerequisites</span></span>
<span data-ttu-id="9697f-108">Para seguir este guia de instruções, você precisa:</span><span class="sxs-lookup"><span data-stu-id="9697f-108">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="9697f-109">Um [Banco de Dados do Azure para servidor e banco de dados PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="9697f-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="9697f-110">Instalar o utilitário de linha de comando [CLI do Azure 2.0](/cli/azure/install-azure-cli) ou usar o Azure Cloud Shell no navegador.</span><span class="sxs-lookup"><span data-stu-id="9697f-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="9697f-111">Configurar regras de firewall para o Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9697f-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="9697f-112">Os comandos de [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) são usados para configurar regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="9697f-112">The [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used to configure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="9697f-113">Listar regras de firewall</span><span class="sxs-lookup"><span data-stu-id="9697f-113">List firewall rules</span></span> 
<span data-ttu-id="9697f-114">Para listar as regras de firewall de servidor existente no servidor, execute o comando [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list).</span><span class="sxs-lookup"><span data-stu-id="9697f-114">To list the existing server firewall rules on the server, run the [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="9697f-115">A saída listará as regras, se houver, por padrão, no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="9697f-115">The output lists the rules if any, by default in JSON format.</span></span> <span data-ttu-id="9697f-116">Você pode usar a opção `--output table` para obter um formato de tabela mais legível como saída.</span><span class="sxs-lookup"><span data-stu-id="9697f-116">You may use the switch `--output table` for a more readable table format as the output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="9697f-117">Criar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="9697f-117">Create firewall rule</span></span>
<span data-ttu-id="9697f-118">Crie uma regra de firewall no nível de servidor do PostgreSQL do Azure com o comando [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="9697f-118">To create a new firewall rule on the server, run the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="9697f-119">Este exemplo permite um intervalo de todos os endereços IP para acessar o servidor **mypgserver-20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="9697f-119">This example allows a range of all IP addresses to access the server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="9697f-120">Para permitir o acesso de um endereço IP único, forneça o mesmo endereço como o IP Inicial e IP Final, como neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="9697f-120">To allow a singular IP address to access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="9697f-121">Após o êxito, a saída do comando listará os detalhes da regra do firewall que você criou, em formato JSON por padrão.</span><span class="sxs-lookup"><span data-stu-id="9697f-121">Upon success, the command output lists the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="9697f-122">Se houver uma falha, a saída mostrará o texto da mensagem de erro em vez disso.</span><span class="sxs-lookup"><span data-stu-id="9697f-122">If there is a failure, the output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="9697f-123">Atualizar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="9697f-123">Update firewall rule</span></span> 
<span data-ttu-id="9697f-124">Atualize uma regra de firewall existente no servidor usando o comando [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update).</span><span class="sxs-lookup"><span data-stu-id="9697f-124">Update an existing firewall rule on the server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="9697f-125">Forneça o nome da regra de firewall existente como entrada, e os atributos IP inicial e IP final para atualizar.</span><span class="sxs-lookup"><span data-stu-id="9697f-125">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="9697f-126">Após o êxito, a saída do comando listará os detalhes da regra do firewall que você atualizou, em formato JSON por padrão.</span><span class="sxs-lookup"><span data-stu-id="9697f-126">Upon success, the command output lists the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="9697f-127">Se houver uma falha, a saída mostrará o texto da mensagem de erro em vez disso.</span><span class="sxs-lookup"><span data-stu-id="9697f-127">If there is a failure, the output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="9697f-128">Se a regra de firewall não existir, ela será criada pelo comando de atualização.</span><span class="sxs-lookup"><span data-stu-id="9697f-128">If the firewall rule does not exist, it gets created by the update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="9697f-129">Mostrar detalhes da regra de firewall</span><span class="sxs-lookup"><span data-stu-id="9697f-129">Show firewall rule details</span></span>
<span data-ttu-id="9697f-130">Você também pode exibir detalhes da regra para um servidor de firewall existente executando o comando [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show).</span><span class="sxs-lookup"><span data-stu-id="9697f-130">You can also show the existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="9697f-131">Após o êxito, a saída do comando listará os detalhes da regra do firewall que você especificou, em formato JSON por padrão.</span><span class="sxs-lookup"><span data-stu-id="9697f-131">Upon success, the command output lists the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="9697f-132">Se houver uma falha, a saída mostrará o texto da mensagem de erro em vez disso.</span><span class="sxs-lookup"><span data-stu-id="9697f-132">If there is a failure, the output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="9697f-133">Excluir regra de firewall</span><span class="sxs-lookup"><span data-stu-id="9697f-133">Delete firewall rule</span></span>
<span data-ttu-id="9697f-134">Para revogar o acesso para um intervalo IP do servidor, exclua uma regra de firewall existente executando o comando [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete).</span><span class="sxs-lookup"><span data-stu-id="9697f-134">To revoke access for an IP range from the server, delete an existing firewall rule by executing the [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="9697f-135">Forneça o nome da regra de firewall existente.</span><span class="sxs-lookup"><span data-stu-id="9697f-135">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="9697f-136">Após o êxito, não haverá saída.</span><span class="sxs-lookup"><span data-stu-id="9697f-136">Upon success, there is no output.</span></span> <span data-ttu-id="9697f-137">Em caso de falha, o texto da mensagem de erro retornará.</span><span class="sxs-lookup"><span data-stu-id="9697f-137">Upon failure, the error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9697f-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9697f-138">Next steps</span></span>
- <span data-ttu-id="9697f-139">Da mesma forma, você pode usar um navegador da Web para [Criar e gerenciar as regras de firewall do Banco de Dados do Azure para PostgreSQL usando o Portal do Azure](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9697f-139">Similarly, you can use a web browser to [Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="9697f-140">Entenda mais sobre [Regras de firewall do servidor de Banco de Dados do Azure para PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="9697f-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="9697f-141">Para obter ajuda com a conexão com um Banco de Dados para servidor PostgreSQL, veja [Bibliotecas de conexão para o Banco de Dados do Azure para PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="9697f-141">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
