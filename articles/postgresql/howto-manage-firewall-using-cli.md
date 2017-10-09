---
title: aaaCreate e gerenciar o banco de dados PostgreSQL para regras de firewall usando a CLI do Azure | Microsoft Docs
description: Este artigo descreve como toocreate e gerenciar o banco de dados PostgreSQL para regras de firewall usando a linha de comando CLI do Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="523f7-103">Criar e gerenciar regras de firewall do Banco de Dados do Azure para PostgreSQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="523f7-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="523f7-104">Regras de firewall de nível de servidor Habilitar administradores toomanage acesso tooan banco de dados do Azure para PostgreSQL Server de um endereço IP específico ou intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="523f7-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="523f7-105">Usando os comandos de CLI do Azure convenientes, você pode criar, atualizar, excluir, lista e mostrar toomanage de regras de firewall em seu servidor.</span><span class="sxs-lookup"><span data-stu-id="523f7-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="523f7-106">Para obter uma visão geral dos firewalls do Banco de Dados do Azure para PostgreSQL, confira [Regras de firewall do servidor de Banco de Dados do Azure para PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="523f7-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="523f7-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="523f7-107">Prerequisites</span></span>
<span data-ttu-id="523f7-108">toostep por este tooguide como, você precisa:</span><span class="sxs-lookup"><span data-stu-id="523f7-108">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="523f7-109">Um [Banco de Dados do Azure para servidor e banco de dados PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="523f7-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="523f7-110">Instalar [2.0 do CLI do Azure](/cli/azure/install-azure-cli) linha de comando utilitário ou use Olá Shell de nuvem do Azure no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="523f7-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="523f7-111">Configurar regras de firewall para o Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="523f7-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="523f7-112">Olá [regra de firewall de servidor de postgres de az](/cli/azure/postgres/server/firewall-rule) comandos são regras de firewall de tooconfigure usado.</span><span class="sxs-lookup"><span data-stu-id="523f7-112">hello [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used tooconfigure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="523f7-113">Listar regras de firewall</span><span class="sxs-lookup"><span data-stu-id="523f7-113">List firewall rules</span></span> 
<span data-ttu-id="523f7-114">toolist Olá existente de regras de firewall de servidor no servidor de saudação, executar Olá [lista de regra de firewall de servidor az postgres](/cli/azure/postgres/server/firewall-rule#list) comando.</span><span class="sxs-lookup"><span data-stu-id="523f7-114">toolist hello existing server firewall rules on hello server, run hello [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="523f7-115">Se houver, por padrão em JSON formatar a saída de Hello lista regras hello.</span><span class="sxs-lookup"><span data-stu-id="523f7-115">hello output lists hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="523f7-116">Você pode usar o comutador hello `--output table` para um formato mais legível da tabela como saída de hello.</span><span class="sxs-lookup"><span data-stu-id="523f7-116">You may use hello switch `--output table` for a more readable table format as hello output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="523f7-117">Criar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="523f7-117">Create firewall rule</span></span>
<span data-ttu-id="523f7-118">toocreate uma nova regra de firewall no servidor de saudação, execute Olá [criar regra de firewall de servidor de postgres de az](/cli/azure/postgres/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="523f7-118">toocreate a new firewall rule on hello server, run hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="523f7-119">Este exemplo permite que um intervalo de todos os servidores de saudação IP endereços tooaccess **mypgserver 20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="523f7-119">This example allows a range of all IP addresses tooaccess hello server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="523f7-120">fornecer tooallow um tooaccess singular de endereço IP, Olá mesmo endereço como Olá IP inicial e final de IP, como neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="523f7-120">tooallow a singular IP address tooaccess, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="523f7-121">Ao ser bem-sucedido, a saída do comando de saudação lista detalhes Olá Olá de regra de firewall criadas por padrão no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="523f7-121">Upon success, hello command output lists hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="523f7-122">Se houver uma falha, o hello saída showserror texto da mensagem.</span><span class="sxs-lookup"><span data-stu-id="523f7-122">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="523f7-123">Atualizar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="523f7-123">Update firewall rule</span></span> 
<span data-ttu-id="523f7-124">Atualizar uma regra de firewall existente no servidor usando o hello [atualização de regra de firewall de servidor az postgres](/cli/azure/postgres/server/firewall-rule#update) comando.</span><span class="sxs-lookup"><span data-stu-id="523f7-124">Update an existing firewall rule on hello server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="523f7-125">Forneça o nome de saudação da regra de firewall existente hello como entrada e a saudação inicial IP e término IP atributos tooupdate.</span><span class="sxs-lookup"><span data-stu-id="523f7-125">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="523f7-126">Ao ser bem-sucedido, a saída do comando de saudação lista detalhes Olá Olá de regra de firewall atualizado, por padrão, no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="523f7-126">Upon success, hello command output lists hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="523f7-127">Se houver uma falha, o hello saída showserror texto da mensagem.</span><span class="sxs-lookup"><span data-stu-id="523f7-127">If there is a failure, hello output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="523f7-128">Se a regra de firewall de saudação não existir, ele é criado pelo comando de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="523f7-128">If hello firewall rule does not exist, it gets created by hello update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="523f7-129">Mostrar detalhes da regra de firewall</span><span class="sxs-lookup"><span data-stu-id="523f7-129">Show firewall rule details</span></span>
<span data-ttu-id="523f7-130">Você também pode exibir detalhes da regra para um servidor de firewall existente Olá executando [Mostrar de regra de firewall de servidor az postgres](/cli/azure/postgres/server/firewall-rule#show) comando.</span><span class="sxs-lookup"><span data-stu-id="523f7-130">You can also show hello existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="523f7-131">Ao ser bem-sucedido, a saída do comando de saudação lista detalhes Olá Olá de regra de firewall especificado, por padrão, no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="523f7-131">Upon success, hello command output lists hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="523f7-132">Se houver uma falha, o hello saída showserror texto da mensagem.</span><span class="sxs-lookup"><span data-stu-id="523f7-132">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="523f7-133">Excluir regra de firewall</span><span class="sxs-lookup"><span data-stu-id="523f7-133">Delete firewall rule</span></span>
<span data-ttu-id="523f7-134">toorevoke acesso para um intervalo IP do servidor de saudação, excluir uma regra de firewall existente executando Olá [Excluir regra de firewall de servidor de postgres de az](/cli/azure/postgres/server/firewall-rule#delete) comando.</span><span class="sxs-lookup"><span data-stu-id="523f7-134">toorevoke access for an IP range from hello server, delete an existing firewall rule by executing hello [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="523f7-135">Forneça o nome de Olá Olá existente de regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="523f7-135">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="523f7-136">Após o êxito, não haverá saída.</span><span class="sxs-lookup"><span data-stu-id="523f7-136">Upon success, there is no output.</span></span> <span data-ttu-id="523f7-137">Em caso de falha, o texto de mensagem de erro de saudação é retornado.</span><span class="sxs-lookup"><span data-stu-id="523f7-137">Upon failure, hello error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="523f7-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="523f7-138">Next steps</span></span>
- <span data-ttu-id="523f7-139">Da mesma forma, você pode usar um navegador da web muito[criar e gerenciar o banco de dados PostgreSQL para regras de firewall usando Olá portal do Azure](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="523f7-139">Similarly, you can use a web browser too[Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="523f7-140">Entenda mais sobre [Regras de firewall do servidor de Banco de Dados do Azure para PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="523f7-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="523f7-141">Para obter ajuda na conexão tooan banco de dados para o servidor PostgreSQL, consulte [bibliotecas de Conexão para o banco de dados do Azure para PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="523f7-141">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
