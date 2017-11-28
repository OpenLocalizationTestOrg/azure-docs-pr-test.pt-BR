---
title: aaaDesign do Azure primeiro banco de dados para o banco de dados MySQL - CLI do Azure | Microsoft Docs
description: "Este tutorial explica como toocreate e gerenciar o banco de dados do Azure para o MySQL server e banco de dados usando o Azure CLI 2.0 na linha de comando de saudação."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="d0e30-103">Projetar seu primeiro Banco de Dados do Azure para o banco de dados MySQL</span><span class="sxs-lookup"><span data-stu-id="d0e30-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="d0e30-104">Banco de dados do Azure para MySQL é um serviço de banco de dados relacional na nuvem da Microsoft com base no mecanismo de banco de dados MySQL Community Edition de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0e30-104">Azure Database for MySQL is a relational database service in hello Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="d0e30-105">Neste tutorial, você usar Azure CLI (interface de linha de comando) e outros utilitários toolearn como para:</span><span class="sxs-lookup"><span data-stu-id="d0e30-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d0e30-106">Criar um Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="d0e30-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="d0e30-107">Configurar o firewall do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="d0e30-107">Configure hello server firewall</span></span>
> * <span data-ttu-id="d0e30-108">Use [ferramenta de linha de comando do mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate um banco de dados</span><span class="sxs-lookup"><span data-stu-id="d0e30-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="d0e30-109">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="d0e30-109">Load sample data</span></span>
> * <span data-ttu-id="d0e30-110">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="d0e30-110">Query data</span></span>
> * <span data-ttu-id="d0e30-111">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="d0e30-111">Update data</span></span>
> * <span data-ttu-id="d0e30-112">Restaurar dados</span><span class="sxs-lookup"><span data-stu-id="d0e30-112">Restore data</span></span>

<span data-ttu-id="d0e30-113">Você pode usar o hello Shell de nuvem do Azure no navegador hello, ou [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli) em seus próprios blocos de código do computador toorun Olá neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="d0e30-113">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d0e30-114">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="d0e30-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d0e30-115">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0e30-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d0e30-116">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d0e30-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="d0e30-117">Se você tiver várias assinaturas, escolha Olá a assinatura de apropriado no qual o recurso de saudação existe ou é cobrado por.</span><span class="sxs-lookup"><span data-stu-id="d0e30-117">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="d0e30-118">Selecione uma ID da assinatura específica em sua conta usando o comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="d0e30-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="d0e30-119">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d0e30-119">Create a resource group</span></span>
<span data-ttu-id="d0e30-120">Crie um [grupo de recursos do Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) com o comando [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d0e30-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="d0e30-121">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo.</span><span class="sxs-lookup"><span data-stu-id="d0e30-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="d0e30-122">Olá, exemplo a seguir cria um grupo de recursos denominado `mycliresource` em Olá `westus` local.</span><span class="sxs-lookup"><span data-stu-id="d0e30-122">hello following example creates a resource group named `mycliresource` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="d0e30-123">Criar um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="d0e30-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="d0e30-124">Crie um banco de dados do Azure para o servidor MySQL com do mysql server Olá az criar comando.</span><span class="sxs-lookup"><span data-stu-id="d0e30-124">Create an Azure Database for MySQL server with hello az mysql server create command.</span></span> <span data-ttu-id="d0e30-125">Um servidor pode gerenciar vários bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d0e30-125">A server can manage multiple databases.</span></span> <span data-ttu-id="d0e30-126">Normalmente, um banco de dados separado é usado para cada projeto ou para cada usuário.</span><span class="sxs-lookup"><span data-stu-id="d0e30-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="d0e30-127">Olá, exemplo a seguir cria um banco de dados do Azure para o MySQL server localizado em `westus` no grupo de recursos de saudação `mycliresource` com o nome `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="d0e30-127">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="d0e30-128">servidor de saudação tem um logon de administrador denominado `myadmin` e a senha `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="d0e30-128">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="d0e30-129">servidor de saudação é criado com **básica** nível de desempenho e **50** unidades compartilhadas entre todos os bancos de dados de Olá no servidor de saudação de computação.</span><span class="sxs-lookup"><span data-stu-id="d0e30-129">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="d0e30-130">Você pode escalonar a computação e armazenamento para cima ou para baixo dependendo das necessidades do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d0e30-130">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="d0e30-131">Configurar regra de firewall</span><span class="sxs-lookup"><span data-stu-id="d0e30-131">Configure firewall rule</span></span>
<span data-ttu-id="d0e30-132">Crie um banco de dados do Azure para o comando de criar a regra de firewall no nível do servidor MySQL com hello az mysql server-regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="d0e30-132">Create an Azure Database for MySQL server-level firewall rule with hello az mysql server firewall-rule create command.</span></span> <span data-ttu-id="d0e30-133">Uma regra de firewall de nível de servidor permite que um aplicativo externo, como **mysql** ferramenta de linha de comando ou o servidor de tooyour de tooconnect do MySQL Workbench através do firewall de serviço do Azure MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="d0e30-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="d0e30-134">Olá, exemplo a seguir cria uma regra de firewall para um intervalo de endereços predefinidos.</span><span class="sxs-lookup"><span data-stu-id="d0e30-134">hello following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="d0e30-135">Este exemplo mostra Olá todo possíveis intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="d0e30-135">This example shows hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a><span data-ttu-id="d0e30-136">Obter informações de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="d0e30-136">Get hello connection information</span></span>

<span data-ttu-id="d0e30-137">tooconnect tooyour server, você precisa ter credenciais de acesso e informações de host de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="d0e30-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="d0e30-138">resultado de saudação está no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="d0e30-138">hello result is in JSON format.</span></span> <span data-ttu-id="d0e30-139">Anote Olá **fullyQualifiedDomainName** e **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="d0e30-139">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="d0e30-140">Conecte-se o servidor toohello usando mysql</span><span class="sxs-lookup"><span data-stu-id="d0e30-140">Connect toohello server using mysql</span></span>
<span data-ttu-id="d0e30-141">Use [ferramenta de linha de comando do mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish tooyour uma conexão banco de dados do Azure para o MySQL server.</span><span class="sxs-lookup"><span data-stu-id="d0e30-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="d0e30-142">Neste exemplo, o comando de saudação é:</span><span class="sxs-lookup"><span data-stu-id="d0e30-142">In this example, hello command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="d0e30-143">Criar um banco de dados vazio</span><span class="sxs-lookup"><span data-stu-id="d0e30-143">Create a blank database</span></span>
<span data-ttu-id="d0e30-144">Quando estiver conectado toohello server, crie um banco de dados em branco.</span><span class="sxs-lookup"><span data-stu-id="d0e30-144">Once you’re connected toohello server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="d0e30-145">No prompt de hello, execute Olá banco de dados do comando tooswitch Olá conexão toothis recém-criado a seguir:</span><span class="sxs-lookup"><span data-stu-id="d0e30-145">At hello prompt, run hello following command tooswitch hello connection toothis newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="d0e30-146">Criar tabelas no banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="d0e30-146">Create tables in hello database</span></span>
<span data-ttu-id="d0e30-147">Agora que você sabe como tooconnect toohello banco de dados para o banco de dados MySQL, podemos ir como toocomplete algumas tarefas básicas.</span><span class="sxs-lookup"><span data-stu-id="d0e30-147">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="d0e30-148">Primeiro, criamos uma tabela e a carregamos com alguns dados.</span><span class="sxs-lookup"><span data-stu-id="d0e30-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="d0e30-149">Vamos criar uma tabela que armazena informações de inventário.</span><span class="sxs-lookup"><span data-stu-id="d0e30-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="d0e30-150">Carregar dados em tabelas de saudação</span><span class="sxs-lookup"><span data-stu-id="d0e30-150">Load data into hello tables</span></span>
<span data-ttu-id="d0e30-151">Agora que temos uma tabela, podemos inserir alguns dados nela.</span><span class="sxs-lookup"><span data-stu-id="d0e30-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="d0e30-152">Na janela de prompt de comando aberta hello, execute Olá tooinsert de consulta a seguir algumas linhas de dados.</span><span class="sxs-lookup"><span data-stu-id="d0e30-152">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="d0e30-153">Agora você tem duas linhas de dados de exemplo na tabela de saudação criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d0e30-153">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="d0e30-154">Consultar e atualizar dados Olá nas tabelas de saudação</span><span class="sxs-lookup"><span data-stu-id="d0e30-154">Query and update hello data in hello tables</span></span>
<span data-ttu-id="d0e30-155">Execute Olá consultar tooretrieve informações a seguir da tabela de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0e30-155">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="d0e30-156">Você também pode atualizar dados Olá nas tabelas de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0e30-156">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="d0e30-157">linha de saudação obtém atualizada quando você recuperar dados.</span><span class="sxs-lookup"><span data-stu-id="d0e30-157">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="d0e30-158">Restaurar um ponto anterior do banco de dados tooa no tempo</span><span class="sxs-lookup"><span data-stu-id="d0e30-158">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="d0e30-159">Imagine que você excluiu acidentalmente essa tabela.</span><span class="sxs-lookup"><span data-stu-id="d0e30-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="d0e30-160">Isso é algo que você não pode se recuperar facilmente.</span><span class="sxs-lookup"><span data-stu-id="d0e30-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="d0e30-161">Banco de dados do Azure para MySQL permite que você toogo tooany back ponto no tempo no hello última até too35 dias e esse ponto no novo servidor tooa do tempo de restauração.</span><span class="sxs-lookup"><span data-stu-id="d0e30-161">Azure Database for MySQL allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new server.</span></span> <span data-ttu-id="d0e30-162">Você pode usar esse novo toorecover de servidor os dados excluídos.</span><span class="sxs-lookup"><span data-stu-id="d0e30-162">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="d0e30-163">Olá etapas Olá exemplo server tooa ponto de restauração da seguir antes de saudação tabela foi adicionada.</span><span class="sxs-lookup"><span data-stu-id="d0e30-163">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

<span data-ttu-id="d0e30-164">Olá restauração é necessário Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="d0e30-164">For hello Restore you need hello following information:</span></span>

- <span data-ttu-id="d0e30-165">Ponto de restauração: selecione um point-in-time que ocorre antes que o servidor de saudação foi alterado.</span><span class="sxs-lookup"><span data-stu-id="d0e30-165">Restore point: Select a point-in-time that occurs before hello server was changed.</span></span> <span data-ttu-id="d0e30-166">Deve ser maior que ou igual ao valor de backup mais antigo toohello origem do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d0e30-166">Must be greater than or equal toohello source database's Oldest backup value.</span></span>
- <span data-ttu-id="d0e30-167">Servidor de destino: forneça um novo nome de servidor que você deseja toorestore para</span><span class="sxs-lookup"><span data-stu-id="d0e30-167">Target server: Provide a new server name you want toorestore to</span></span>
- <span data-ttu-id="d0e30-168">Servidor de origem: fornecer nome de saudação do servidor de saudação desejado toorestore de</span><span class="sxs-lookup"><span data-stu-id="d0e30-168">Source server: Provide hello name of hello server you want toorestore from</span></span>
- <span data-ttu-id="d0e30-169">Local: Não é possível selecionar região hello, por padrão, ele é igual ao servidor de origem Olá</span><span class="sxs-lookup"><span data-stu-id="d0e30-169">Location: You cannot select hello region, by default it is same as hello source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="d0e30-170">servidor de saudação toorestore e [restauração point-in-time tooa](./howto-restore-server-portal.md) antes Olá tabela foi excluída.</span><span class="sxs-lookup"><span data-stu-id="d0e30-170">toorestore hello server and [restore tooa point-in-time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="d0e30-171">Restaurar o servidor tooa outro ponto no tempo cria um duplicado novo servidor como servidor de saudação original como de saudação ponto no tempo especificado, desde que está dentro do período de retenção de saudação de seu [camada de serviço](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="d0e30-171">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0e30-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d0e30-172">Next Steps</span></span>
<span data-ttu-id="d0e30-173">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="d0e30-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="d0e30-174">Criar um Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="d0e30-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="d0e30-175">Configurar o firewall do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="d0e30-175">Configure hello server firewall</span></span>
> * <span data-ttu-id="d0e30-176">Use [ferramenta de linha de comando do mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate um banco de dados</span><span class="sxs-lookup"><span data-stu-id="d0e30-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="d0e30-177">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="d0e30-177">Load sample data</span></span>
> * <span data-ttu-id="d0e30-178">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="d0e30-178">Query data</span></span>
> * <span data-ttu-id="d0e30-179">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="d0e30-179">Update data</span></span>
> * <span data-ttu-id="d0e30-180">Restaurar dados</span><span class="sxs-lookup"><span data-stu-id="d0e30-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d0e30-181">Banco de Dados do Azure para MySQL - Exemplos da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d0e30-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
