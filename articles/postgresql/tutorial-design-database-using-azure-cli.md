---
title: Projetar seu primeiro Banco de Dados do Azure para PostgreSQL usando a CLI do Azure | Microsoft Docs
description: Este tutorial mostra como tooDesign do Azure primeiro banco de dados para PostgreSQL usando a CLI do Azure.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="06d25-103">Criar seu primeiro Banco de Dados do Azure para PostgreSQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="06d25-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="06d25-104">Neste tutorial, você usar Azure CLI (interface de linha de comando) e outros utilitários toolearn como para:</span><span class="sxs-lookup"><span data-stu-id="06d25-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="06d25-105">Criar um Banco de Dados do Azure para o PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="06d25-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="06d25-106">Configurar o firewall do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="06d25-106">Configure hello server firewall</span></span>
> * <span data-ttu-id="06d25-107">Use [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate utilitário um banco de dados</span><span class="sxs-lookup"><span data-stu-id="06d25-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="06d25-108">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="06d25-108">Load sample data</span></span>
> * <span data-ttu-id="06d25-109">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="06d25-109">Query data</span></span>
> * <span data-ttu-id="06d25-110">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="06d25-110">Update data</span></span>
> * <span data-ttu-id="06d25-111">Restaurar dados</span><span class="sxs-lookup"><span data-stu-id="06d25-111">Restore data</span></span>

<span data-ttu-id="06d25-112">Você pode usar o hello Shell de nuvem do Azure no navegador hello, ou [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli) em seus próprios blocos de código do computador toorun Olá neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="06d25-112">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="06d25-113">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="06d25-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="06d25-114">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="06d25-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="06d25-115">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="06d25-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="06d25-116">Se você tiver várias assinaturas, escolha Olá a assinatura de apropriado no qual o recurso de saudação existe ou é cobrado por.</span><span class="sxs-lookup"><span data-stu-id="06d25-116">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="06d25-117">Selecione uma ID da assinatura específica em sua conta usando o comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="06d25-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="06d25-118">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="06d25-118">Create a resource group</span></span>
<span data-ttu-id="06d25-119">Criar um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) usando Olá [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="06d25-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="06d25-120">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo.</span><span class="sxs-lookup"><span data-stu-id="06d25-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="06d25-121">Olá, exemplo a seguir cria um grupo de recursos denominado `myresourcegroup` em Olá `westus` local.</span><span class="sxs-lookup"><span data-stu-id="06d25-121">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="06d25-122">Criar um Banco de Dados do Azure para o servidor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="06d25-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="06d25-123">Criar um [banco de dados do Azure para o servidor PostgreSQL](overview.md) usando Olá [az postgres server criar](/cli/azure/postgres/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="06d25-123">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="06d25-124">Um servidor contém um grupo de bancos de dados gerenciados conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="06d25-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="06d25-125">Olá, exemplo a seguir cria um servidor chamado `mypgserver-20170401` em seu grupo de recursos `myresourcegroup` com logon de administrador de servidor `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="06d25-125">hello following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="06d25-126">Nome de um servidor mapeia o nome tooDNS e, portanto, é necessário toobe globalmente exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="06d25-126">Name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="06d25-127">Olá substituto `<server_admin_password>` com seu próprio valor.</span><span class="sxs-lookup"><span data-stu-id="06d25-127">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="06d25-128">Olá administrador logon e senha que você especificar aqui são toolog necessária no servidor de toohello e seus bancos de dados mais tarde nesse início rápido.</span><span class="sxs-lookup"><span data-stu-id="06d25-128">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="06d25-129">Lembre-se ou registre essas informações para o uso posterior.</span><span class="sxs-lookup"><span data-stu-id="06d25-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="06d25-130">Por padrão, o banco de dados **postgres** é criado em seu servidor.</span><span class="sxs-lookup"><span data-stu-id="06d25-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="06d25-131">Olá [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) banco de dados é um banco de dados padrão devem ser usados pelos usuários, utilitários e aplicativos de terceiros.</span><span class="sxs-lookup"><span data-stu-id="06d25-131">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="06d25-132">Configurar uma regra de firewall no nível de servidor</span><span class="sxs-lookup"><span data-stu-id="06d25-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="06d25-133">Criar uma regra de firewall de nível de servidor do Azure PostgreSQL com hello [criar regra de firewall de servidor de postgres de az](/cli/azure/postgres/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="06d25-133">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="06d25-134">Uma regra de firewall de nível de servidor permite que um aplicativo externo, como [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) ou [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server através do firewall de serviço do Azure PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="06d25-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="06d25-135">Você pode definir uma regra de firewall que abrange um tooconnect IP intervalo toobe capaz de sua rede.</span><span class="sxs-lookup"><span data-stu-id="06d25-135">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="06d25-136">Olá exemplo a seguir usa [criar regra de firewall de servidor de postgres de az](/cli/azure/postgres/server/firewall-rule#create) toocreate uma regra de firewall `AllowAllIps` para um endereço IP, intervalo.</span><span class="sxs-lookup"><span data-stu-id="06d25-136">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="06d25-137">tooopen todos os endereços IP, use 0.0.0.0 como Olá Iniciando endereço IP e 255.255.255.255 como Olá endereço final.</span><span class="sxs-lookup"><span data-stu-id="06d25-137">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="06d25-138">O servidor PostgreSQL do Azure se comunica pela porta 5432.</span><span class="sxs-lookup"><span data-stu-id="06d25-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="06d25-139">Ao se conectar de dentro de uma rede corporativa, o tráfego de saída pela porta 5432 talvez não seja permitido pelo firewall de sua rede.</span><span class="sxs-lookup"><span data-stu-id="06d25-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="06d25-140">Ter seu departamento de TI abrir porta 5432 tooconnect tooyour banco de dados SQL server.</span><span class="sxs-lookup"><span data-stu-id="06d25-140">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>
>

## <a name="get-hello-connection-information"></a><span data-ttu-id="06d25-141">Obter informações de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="06d25-141">Get hello connection information</span></span>

<span data-ttu-id="06d25-142">tooconnect tooyour server, você precisa ter credenciais de acesso e informações de host de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="06d25-142">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="06d25-143">resultado de saudação está no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="06d25-143">hello result is in JSON format.</span></span> <span data-ttu-id="06d25-144">Anote Olá **administratorLogin** e **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="06d25-144">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="06d25-145">Conecte-se tooAzure banco de dados para o banco de dados PostgreSQL usando psql</span><span class="sxs-lookup"><span data-stu-id="06d25-145">Connect tooAzure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="06d25-146">Se o computador cliente tem PostgreSQL instalado, você pode usar uma instância local do [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), ou Olá Console de nuvem do Azure tooconnect tooan PostgreSQL Azure server.</span><span class="sxs-lookup"><span data-stu-id="06d25-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or hello Azure Cloud Console tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="06d25-147">Agora vamos usar Olá psql utilitário de linha de comando tooconnect toohello banco de dados para o servidor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="06d25-147">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="06d25-148">Executar Olá psql comando tooconnect tooan banco de dados PostgreSQL servidor a seguir</span><span class="sxs-lookup"><span data-stu-id="06d25-148">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="06d25-149">Por exemplo, Olá comando a seguir conecta o banco de dados padrão toohello chamado **postgres** no seu servidor PostgreSQL **mypgserver 20170401.postgres.database.azure.com** usando as credenciais de acesso.</span><span class="sxs-lookup"><span data-stu-id="06d25-149">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="06d25-150">Digite hello `<server_admin_password>` você escolheu quando solicitado para a senha.</span><span class="sxs-lookup"><span data-stu-id="06d25-150">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="06d25-151">Quando estiver conectado toohello server, crie um banco de dados em branco no prompt de saudação.</span><span class="sxs-lookup"><span data-stu-id="06d25-151">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="06d25-152">No prompt de hello, execute Olá após o banco de dados do comando tooswitch conexão toohello recém-criado **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="06d25-152">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="06d25-153">Criar tabelas no banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="06d25-153">Create tables in hello database</span></span>
<span data-ttu-id="06d25-154">Agora que você sabe como tooconnect toohello banco de dados do Azure para PostgreSQL, podemos ir como toocomplete algumas tarefas básicas.</span><span class="sxs-lookup"><span data-stu-id="06d25-154">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="06d25-155">Primeiro, criamos uma tabela e a carregamos com alguns dados.</span><span class="sxs-lookup"><span data-stu-id="06d25-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="06d25-156">Vamos criar uma tabela que rastreia informações de inventário.</span><span class="sxs-lookup"><span data-stu-id="06d25-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="06d25-157">Você pode ver Olá recém-criado tabela na lista de saudação de tabelas agora digitando:</span><span class="sxs-lookup"><span data-stu-id="06d25-157">You can see hello newly created table in hello list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="06d25-158">Carregar dados em tabelas de saudação</span><span class="sxs-lookup"><span data-stu-id="06d25-158">Load data into hello tables</span></span>
<span data-ttu-id="06d25-159">Agora que temos uma tabela, podemos inserir alguns dados nela.</span><span class="sxs-lookup"><span data-stu-id="06d25-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="06d25-160">Na janela de prompt de comando aberta hello, executar Olá tooinsert de consulta a seguir algumas linhas de dados</span><span class="sxs-lookup"><span data-stu-id="06d25-160">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="06d25-161">Você tem agora duas linhas de dados de exemplo na tabela de saudação criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="06d25-161">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="06d25-162">Consultar e atualizar dados Olá nas tabelas de saudação</span><span class="sxs-lookup"><span data-stu-id="06d25-162">Query and update hello data in hello tables</span></span>
<span data-ttu-id="06d25-163">Execute Olá consultar tooretrieve informações a seguir da tabela de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="06d25-163">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="06d25-164">Você também pode atualizar dados Olá nas tabelas de saudação</span><span class="sxs-lookup"><span data-stu-id="06d25-164">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="06d25-165">linha de saudação obtém atualizada quando você recuperar dados.</span><span class="sxs-lookup"><span data-stu-id="06d25-165">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="06d25-166">Restaurar um ponto anterior do banco de dados tooa no tempo</span><span class="sxs-lookup"><span data-stu-id="06d25-166">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="06d25-167">Imagine que você excluiu acidentalmente uma tabela.</span><span class="sxs-lookup"><span data-stu-id="06d25-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="06d25-168">Isso é algo que você não pode se recuperar facilmente.</span><span class="sxs-lookup"><span data-stu-id="06d25-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="06d25-169">Banco de dados do Azure para PostgreSQL permite voltar tooany de toogo point-in-time (em Olá última too7 dias (Basic) e 35 dias (padrão)) e restaurar esse point-in-time tooa novo servidor.</span><span class="sxs-lookup"><span data-stu-id="06d25-169">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="06d25-170">Você pode usar esse novo toorecover de servidor os dados excluídos.</span><span class="sxs-lookup"><span data-stu-id="06d25-170">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="06d25-171">Olá etapas Olá exemplo server tooa ponto de restauração da seguir antes de saudação tabela foi adicionada.</span><span class="sxs-lookup"><span data-stu-id="06d25-171">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="06d25-172">Olá `az postgres server restore` comando precisa Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="06d25-172">hello `az postgres server restore` command needs hello following parameters:</span></span>
| <span data-ttu-id="06d25-173">Configuração</span><span class="sxs-lookup"><span data-stu-id="06d25-173">Setting</span></span> | <span data-ttu-id="06d25-174">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="06d25-174">Suggested value</span></span> | <span data-ttu-id="06d25-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="06d25-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="06d25-176">--resource-group</span><span class="sxs-lookup"><span data-stu-id="06d25-176">--resource-group</span></span> |  <span data-ttu-id="06d25-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06d25-177">myResourceGroup</span></span> |  <span data-ttu-id="06d25-178">O grupo de recursos no qual Olá o servidor de origem existe.</span><span class="sxs-lookup"><span data-stu-id="06d25-178">The resource group in which hello source server exists.</span></span>  |
| <span data-ttu-id="06d25-179">--nome</span><span class="sxs-lookup"><span data-stu-id="06d25-179">--name</span></span> | <span data-ttu-id="06d25-180">restaurado mypgserver</span><span class="sxs-lookup"><span data-stu-id="06d25-180">mypgserver-restored</span></span> | <span data-ttu-id="06d25-181">nome de Olá do novo servidor de saudação é criado pelo comando de restauração de saudação.</span><span class="sxs-lookup"><span data-stu-id="06d25-181">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="06d25-182">Restauração-point-in-time</span><span class="sxs-lookup"><span data-stu-id="06d25-182">restore-point-in-time</span></span> | <span data-ttu-id="06d25-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="06d25-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="06d25-184">Selecione um toorestore point-in-time para.</span><span class="sxs-lookup"><span data-stu-id="06d25-184">Select a point-in-time toorestore to.</span></span> <span data-ttu-id="06d25-185">Essa data e hora devem ser dentro do período de retenção de backup do servidor de origem hello.</span><span class="sxs-lookup"><span data-stu-id="06d25-185">This date and time must be within hello source server's backup retention period.</span></span> <span data-ttu-id="06d25-186">Use o formato ISO8601 de data e hora.</span><span class="sxs-lookup"><span data-stu-id="06d25-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="06d25-187">Por exemplo, você pode usar seu próprio fuso horário local, como `2017-04-13T05:59:00-08:00`, ou usar o formato UTC Zulu `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="06d25-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="06d25-188">--servidor de origem</span><span class="sxs-lookup"><span data-stu-id="06d25-188">--source-server</span></span> | <span data-ttu-id="06d25-189">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="06d25-189">mypgserver-20170401</span></span> | <span data-ttu-id="06d25-190">nome de saudação ou ID do hello toorestore de servidor de origem do.</span><span class="sxs-lookup"><span data-stu-id="06d25-190">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="06d25-191">Restaurar um servidor tooa point-in-time cria um novo servidor, copiando como servidor de saudação original a partir do ponto de saudação no horário especificado.</span><span class="sxs-lookup"><span data-stu-id="06d25-191">Restoring a server tooa point-in-time creates a new server, copying as hello original server as of hello point in time you specify.</span></span> <span data-ttu-id="06d25-192">local de saudação e preços valores nível para o servidor de saudação restaurada são Olá mesmo que o servidor de origem hello.</span><span class="sxs-lookup"><span data-stu-id="06d25-192">hello location and pricing tier values for hello restored server are hello same as hello source server.</span></span>

<span data-ttu-id="06d25-193">comando Olá é síncrono e retornará depois Olá servidor for restaurado.</span><span class="sxs-lookup"><span data-stu-id="06d25-193">hello command is synchronous, and will return after hello server is restored.</span></span> <span data-ttu-id="06d25-194">Quando termina de restauração hello, localize o servidor de novo Olá que foi criado.</span><span class="sxs-lookup"><span data-stu-id="06d25-194">Once hello restore finishes, locate hello new server that was created.</span></span> <span data-ttu-id="06d25-195">Verifique se Olá dados foi restaurados conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="06d25-195">Verify hello data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="06d25-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="06d25-196">Next steps</span></span>
<span data-ttu-id="06d25-197">Neste tutorial, você aprendeu como toouse Azure CLI (interface de linha de comando) e outros utilitários para:</span><span class="sxs-lookup"><span data-stu-id="06d25-197">In this tutorial, you learned how toouse Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="06d25-198">Criar um Banco de Dados do Azure para o PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="06d25-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="06d25-199">Configurar o firewall do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="06d25-199">Configure hello server firewall</span></span>
> * <span data-ttu-id="06d25-200">Use [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate utilitário um banco de dados</span><span class="sxs-lookup"><span data-stu-id="06d25-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="06d25-201">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="06d25-201">Load sample data</span></span>
> * <span data-ttu-id="06d25-202">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="06d25-202">Query data</span></span>
> * <span data-ttu-id="06d25-203">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="06d25-203">Update data</span></span>
> * <span data-ttu-id="06d25-204">Restaurar dados</span><span class="sxs-lookup"><span data-stu-id="06d25-204">Restore data</span></span>

<span data-ttu-id="06d25-205">Em seguida, Aprenda como toouse Olá tarefas semelhantes toodo portal do Azure, examine este tutorial: [criar seu primeiro banco de dados do Azure para PostgreSQL usando Olá portal do Azure](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="06d25-205">Next, learn how toouse hello Azure portal toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using hello Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
