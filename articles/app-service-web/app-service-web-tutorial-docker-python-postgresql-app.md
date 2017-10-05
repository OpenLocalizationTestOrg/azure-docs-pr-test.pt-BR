---
title: Compilar um aplicativo Web Docker Python e PostgreSQL no Azure | Microsoft Docs
description: "Saiba como fazer com que um aplicativo Docker Python funcione no Azure com conexão a um banco de dados PostgreSQL."
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e70f85a1eb4a6e1a81e0ca4fae228ca97deca6fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="55c43-103">Compilar um aplicativo Web Docker Python e PostgreSQL no Azure</span><span class="sxs-lookup"><span data-stu-id="55c43-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="55c43-104">Os aplicativos Web do Azure fornecem um serviço de hospedagem na Web altamente escalonável, com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="55c43-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="55c43-105">Este tutorial mostra como criar um aplicativo Web Docker Python básico no Azure.</span><span class="sxs-lookup"><span data-stu-id="55c43-105">This tutorial shows how to create a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="55c43-106">Você conectará esse aplicativo a um banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="55c43-106">You'll connect this app to a PostgreSQL database.</span></span> <span data-ttu-id="55c43-107">Quando terminar, você terá um aplicativo Python Flask em execução dentro de um contêiner do Docker nos [Aplicativos Web do Serviço de Aplicativo do Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55c43-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Aplicativo Docker Python Flask no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="55c43-109">Você pode seguir as etapas abaixo no macOS.</span><span class="sxs-lookup"><span data-stu-id="55c43-109">You can follow the steps below on macOS.</span></span> <span data-ttu-id="55c43-110">As instruções do Linux e do Windows são as mesmas na maioria dos casos, mas as diferenças não são detalhadas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="55c43-110">Linux and Windows instructions are the same in most cases, but the differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="55c43-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="55c43-111">Prerequisites</span></span>

<span data-ttu-id="55c43-112">Para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="55c43-112">To complete this tutorial:</span></span>

1. [<span data-ttu-id="55c43-113">Instalar o Git</span><span class="sxs-lookup"><span data-stu-id="55c43-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="55c43-114">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="55c43-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="55c43-115">Instale e execute o PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="55c43-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="55c43-116">Instale o Docker Community Edition</span><span class="sxs-lookup"><span data-stu-id="55c43-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="55c43-117">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="55c43-117">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="55c43-118">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="55c43-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="55c43-119">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="55c43-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="55c43-120">Testar a instalação do PostgreSQL local e criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="55c43-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="55c43-121">Abra a janela do terminal e execute `psql postgres` para se conectar ao servidor PostgreSQL local.</span><span class="sxs-lookup"><span data-stu-id="55c43-121">Open the terminal window and run `psql postgres` to connect to your local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="55c43-122">Se sua conexão tiver êxito, o banco de dados PostgreSQL já estará em execução.</span><span class="sxs-lookup"><span data-stu-id="55c43-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="55c43-123">Caso contrário, certifique-se de que o banco de dados PostgresQL local seja iniciado seguindo as etapas em [Baixe - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="55c43-123">If not, make sure that your local PostgresQL database is started by following the steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="55c43-124">Crie um banco de dados chamado *eventregistration* e configure um usuário de banco de dados separado chamado *manager* com a senha *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="55c43-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```
<span data-ttu-id="55c43-125">Digite *\q* para sair do cliente do PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="55c43-125">Type *\q* to exit the PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="55c43-126">Criar um aplicativo Python Flask local</span><span class="sxs-lookup"><span data-stu-id="55c43-126">Create local Python Flask application</span></span>

<span data-ttu-id="55c43-127">Nesta etapa, você configura o projeto Python Flask local.</span><span class="sxs-lookup"><span data-stu-id="55c43-127">In this step, you set up the local Python Flask project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="55c43-128">Clonar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="55c43-128">Clone the sample application</span></span>

<span data-ttu-id="55c43-129">Abra a janela do terminal e `CD` para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="55c43-129">Open the terminal window, and `CD` to a working directory.</span></span>  

<span data-ttu-id="55c43-130">Execute os comandos a seguir para clonar o repositório de exemplo e vá até a versão *0.1-initialapp*.</span><span class="sxs-lookup"><span data-stu-id="55c43-130">Run the following commands to clone the sample repository and go to the *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="55c43-131">Esse repositório de exemplo contém um aplicativo [Flask](http://flask.pocoo.org/).</span><span class="sxs-lookup"><span data-stu-id="55c43-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-the-application"></a><span data-ttu-id="55c43-132">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="55c43-132">Run the application</span></span>

> [!NOTE] 
> <span data-ttu-id="55c43-133">Em uma etapa posterior, simplificaremos esse processo criando um contêiner do Docker para ser usado com o nosso banco de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="55c43-133">In a later step you simplify this process by building a Docker container to use with the production database.</span></span>

<span data-ttu-id="55c43-134">Instale os pacotes necessários e inicie o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55c43-134">Install the required packages and start the application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="55c43-135">Quando o aplicativo estiver totalmente carregado, você verá algo semelhante à seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="55c43-135">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="55c43-136">Navegue até http://127.0.0.1:5000 em um navegador.</span><span class="sxs-lookup"><span data-stu-id="55c43-136">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="55c43-137">Clique em **Registrar!**</span><span class="sxs-lookup"><span data-stu-id="55c43-137">Click **Register!**</span></span> <span data-ttu-id="55c43-138">e crie um usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="55c43-138">and create a test user.</span></span>

![Aplicativo Python Flask em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="55c43-140">O aplicativo de exemplo Flask armazena dados do usuário no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="55c43-140">The Flask sample application stores user data in the database.</span></span> <span data-ttu-id="55c43-141">Se você tiver êxito ao registrar um usuário, seu aplicativo está gravando os dados no banco de dados PostgreSQL local.</span><span class="sxs-lookup"><span data-stu-id="55c43-141">If you are successful at registering a user, your app is writing data to the local PostgreSQL database.</span></span>

<span data-ttu-id="55c43-142">Para parar o servidor Flask a qualquer momento, digite Ctrl+C no terminal.</span><span class="sxs-lookup"><span data-stu-id="55c43-142">To stop the Flask server at anytime, type Ctrl+C in the terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="55c43-143">Criar um banco de dados PostgreSQL de produção</span><span class="sxs-lookup"><span data-stu-id="55c43-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="55c43-144">Nesta etapa, você cria um banco de dados PostgreSQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="55c43-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="55c43-145">Quando seu aplicativo for implantado no Azure, ele usará esse banco de dados na nuvem.</span><span class="sxs-lookup"><span data-stu-id="55c43-145">When your app is deployed to Azure, it will use this cloud database.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="55c43-146">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="55c43-146">Log in to Azure</span></span>

<span data-ttu-id="55c43-147">Agora, você usará a CLI do Azure 2.0 para criar os recursos necessários para hospedar o aplicativo Python no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="55c43-147">You are now going to use the Azure CLI 2.0 to create the resources needed to host your Python application in Azure App Service.</span></span>  <span data-ttu-id="55c43-148">Faça logon na sua assinatura do Azure com o comando [az login](/cli/azure/#login) e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="55c43-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="55c43-149">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="55c43-149">Create a resource group</span></span>

<span data-ttu-id="55c43-150">Crie um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) com o [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="55c43-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="55c43-151">O exemplo a seguir cria um grupo de recursos na região Oeste dos EUA:</span><span class="sxs-lookup"><span data-stu-id="55c43-151">The following example creates a resource group in the West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="55c43-152">Use o comando CLI do Azure [az appservice list-locations](/cli/azure/appservice#list-locations) para listar os locais disponíveis.</span><span class="sxs-lookup"><span data-stu-id="55c43-152">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="55c43-153">Criar um Banco de Dados do Azure para o servidor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="55c43-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="55c43-154">Crie um servidor PostgreSQL com o comando [az postgres server create](/cli/azure/documentdb#create).</span><span class="sxs-lookup"><span data-stu-id="55c43-154">Create a PostgreSQL server with the [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="55c43-155">No comando a seguir, substitua um nome do servidor exclusivo para o espaço reservado  *\<postgresql_name >* e um nome de usuário para o espaço reservado  *\<admin_username >*.</span><span class="sxs-lookup"><span data-stu-id="55c43-155">In the following command, substitute a unique server name for the *\<postgresql_name>* placeholder and a user name for the *\<admin_username>* placeholder.</span></span> <span data-ttu-id="55c43-156">Esse nome do servidor é usado como parte de seu ponto de extremidade do PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), portanto, ele precisa ser exclusivo entre todos os servidores no Azure.</span><span class="sxs-lookup"><span data-stu-id="55c43-156">The server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so the name needs to be unique across all servers in Azure.</span></span> <span data-ttu-id="55c43-157">O nome de usuário é necessário para a conta do usuário administrador de banco de dados inicial.</span><span class="sxs-lookup"><span data-stu-id="55c43-157">The user name is for the initial database admin user account.</span></span> <span data-ttu-id="55c43-158">É solicitado que você escolha uma senha para esse usuário.</span><span class="sxs-lookup"><span data-stu-id="55c43-158">You are prompted to pick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="55c43-159">Quando o servidor PostgreSQL do Banco de Dados do Azure for criado, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="55c43-159">When the Azure Database for PostgreSQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-the-azure-database-for-postgresql-server"></a><span data-ttu-id="55c43-160">Criando uma regra de firewall para o Banco de Dados do Azure para o servidor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="55c43-160">Create a firewall rule for the Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="55c43-161">Execute o seguinte comando da CLI do Azure para permitir o acesso ao banco de dados a partir de todos os endereços IP.</span><span class="sxs-lookup"><span data-stu-id="55c43-161">Run the following Azure CLI command to allow access to the database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="55c43-162">A CLI do Azure confirma a criação da regra de firewall com saída semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="55c43-162">The Azure CLI confirms the firewall rule creation with output similar to the following example:</span></span>

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-to-the-database"></a><span data-ttu-id="55c43-163">Conectar o aplicativo Python Flask ao banco de dados</span><span class="sxs-lookup"><span data-stu-id="55c43-163">Connect your Python Flask application to the database</span></span>

<span data-ttu-id="55c43-164">Nesta etapa, você conecta seu aplicativo de exemplo Python Flask ao Banco de Dados do Azure para o servidor PostgreSQL criado.</span><span class="sxs-lookup"><span data-stu-id="55c43-164">In this step, you connect your Python Flask sample application to the Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="55c43-165">Criando um banco de dados vazio e configurando um novo usuário do aplicativo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="55c43-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="55c43-166">Crie um usuário de banco de dados com acesso somente a um banco de dados individual.</span><span class="sxs-lookup"><span data-stu-id="55c43-166">Create a database user with access to a single database only.</span></span> <span data-ttu-id="55c43-167">Você usará essas credenciais para evitar fornecer acesso completo ao aplicativo para o servidor.</span><span class="sxs-lookup"><span data-stu-id="55c43-167">You'll use these credentials to avoid giving the application full access to the server.</span></span>

<span data-ttu-id="55c43-168">Conecte-se ao banco de dados (sua senha de administrador será solicitada).</span><span class="sxs-lookup"><span data-stu-id="55c43-168">Connect to the database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="55c43-169">Crie o banco de dados e o usuário usando a CLI do PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="55c43-169">Create the database and user from the PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```

<span data-ttu-id="55c43-170">Digite *\q* para sair do cliente do PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="55c43-170">Type *\q* to exit the PostgreSQL client.</span></span>

### <a name="test-the-application-locally-against-the-azure-postgresql-database"></a><span data-ttu-id="55c43-171">Teste o aplicativo localmente no banco de dados PostgreSQL do Azure</span><span class="sxs-lookup"><span data-stu-id="55c43-171">Test the application locally against the Azure PostgreSQL database</span></span> 

<span data-ttu-id="55c43-172">Voltando para a pasta *aplicativo* do repositório do Github clonado, podemos executar o aplicativo Python Flask atualizando as variáveis de ambiente do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="55c43-172">Going back now to the *app* folder of the cloned Github repository, you can run the Python Flask application by updating the database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="55c43-173">Quando o aplicativo estiver totalmente carregado, você verá algo semelhante à seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="55c43-173">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="55c43-174">Navegue até http://127.0.0.1:5000 em um navegador.</span><span class="sxs-lookup"><span data-stu-id="55c43-174">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="55c43-175">Clique em **Registrar!**</span><span class="sxs-lookup"><span data-stu-id="55c43-175">Click **Register!**</span></span> <span data-ttu-id="55c43-176">e crie um registro de teste.</span><span class="sxs-lookup"><span data-stu-id="55c43-176">and create a test registration.</span></span> <span data-ttu-id="55c43-177">Agora, você está gravando dados no banco de dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="55c43-177">You are now writing data to the database in Azure.</span></span>

![Aplicativo Python Flask em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-the-application-from-a-docker-container"></a><span data-ttu-id="55c43-179">Executando o aplicativo de um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="55c43-179">Running the application from a Docker Container</span></span>

<span data-ttu-id="55c43-180">Criar a imagem de contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="55c43-180">Build the Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="55c43-181">O Docker exibe uma confirmação de que criou o contêiner com êxito.</span><span class="sxs-lookup"><span data-stu-id="55c43-181">Docker displays a confirmation that it successfully created the container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="55c43-182">Adicione variáveis de ambiente do banco de dados a um arquivo de variável de ambiente *db.env*.</span><span class="sxs-lookup"><span data-stu-id="55c43-182">Add database environment variables to an environment variable file *db.env*.</span></span> <span data-ttu-id="55c43-183">O aplicativo se conectará ao banco de dados de produção PostgreSQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="55c43-183">The app will connect to the PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="55c43-184">Execute o aplicativo de dentro do contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="55c43-184">Run the app from within the Docker container.</span></span> <span data-ttu-id="55c43-185">O seguinte comando especifica o arquivo de variável de ambiente e mapeia a porta 5000 padrão do Flask para nossa porta 5000 local.</span><span class="sxs-lookup"><span data-stu-id="55c43-185">The following command specifies the environment variable file and maps the default Flask port 5000 to local port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="55c43-186">A saída é semelhante ao que você viu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="55c43-186">The output is similar to what you saw earlier.</span></span> <span data-ttu-id="55c43-187">No entanto, a migração de banco de dados inicial não precisa mais ser executada e, portanto, é ignorada.</span><span class="sxs-lookup"><span data-stu-id="55c43-187">However, the initial database migration no longer needs to be performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="55c43-188">O banco de dados já contém o registro que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="55c43-188">The database already contains the registration you created previously.</span></span>

![Aplicativo Python Flask baseado em contêiner do Docker em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-the-docker-container-to-a-container-registry"></a><span data-ttu-id="55c43-190">Carregar o contêiner do Docker em um registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="55c43-190">Upload the Docker container to a container registry</span></span>

<span data-ttu-id="55c43-191">Nesta etapa, faça upload do contêiner do Docker em um registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="55c43-191">In this step, you upload the Docker container to a container registry.</span></span> <span data-ttu-id="55c43-192">Você utilizará o Registro de Contêiner do Azure, mas também pode usar outros registros populares, como o Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="55c43-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="55c43-193">Criar um Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="55c43-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="55c43-194">No seguinte comando para criar um registro de contêiner, substitua *\<registry_name>* por um nome de registro de contêiner do Azure exclusivo de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="55c43-194">In the following command to create a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="55c43-195">Saída</span><span class="sxs-lookup"><span data-stu-id="55c43-195">Output</span></span>
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-the-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="55c43-196">Recuperar as credenciais de registro para enviar e receber imagens do Docker</span><span class="sxs-lookup"><span data-stu-id="55c43-196">Retrieve the registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="55c43-197">Para mostrar as credenciais de registro, habilite o modo de administração pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="55c43-197">To show registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="55c43-198">Você verá duas senhas.</span><span class="sxs-lookup"><span data-stu-id="55c43-198">You see two passwords.</span></span> <span data-ttu-id="55c43-199">Tome nota do nome de usuário e da primeira senha.</span><span class="sxs-lookup"><span data-stu-id="55c43-199">Make note of the user name and the first password.</span></span>

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-to-azure-container-registry"></a><span data-ttu-id="55c43-200">Carregue o contêiner do Docker no Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="55c43-200">Upload your Docker container to Azure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-the-docker-python-flask-application-to-azure"></a><span data-ttu-id="55c43-201">Implantar o aplicativo Docker Python Flask no Azure</span><span class="sxs-lookup"><span data-stu-id="55c43-201">Deploy the Docker Python Flask application to Azure</span></span>

<span data-ttu-id="55c43-202">Nesta etapa, você implanta seu aplicativo Python Flask baseado em contêiner do Docker no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="55c43-202">In this step, you deploy your Docker container-based Python Flask application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="55c43-203">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="55c43-203">Create an App Service plan</span></span>

<span data-ttu-id="55c43-204">Criar um plano do Serviço de Aplicativo com o comando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="55c43-204">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="55c43-205">O exemplo a seguir cria um plano do Serviço de Aplicativo baseado em Linux chamado *myAppServicePlan* usando o tipo de preço S1:</span><span class="sxs-lookup"><span data-stu-id="55c43-205">The following example creates a Linux-based App Service plan named *myAppServicePlan* using the S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="55c43-206">Quando o Plano do Serviço de Aplicativo é criado, a CLI do Azure mostra informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="55c43-206">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a><span data-ttu-id="55c43-207">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="55c43-207">Create a web app</span></span>

<span data-ttu-id="55c43-208">Crie um aplicativo Web no plano do Serviço de Aplicativo do *myAppServicePlan* com o comando [az webapp create](/cli/azure/webapp#create).</span><span class="sxs-lookup"><span data-stu-id="55c43-208">Create a web app in the *myAppServicePlan* App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="55c43-209">O aplicativo Web fornece um espaço de hospedagem para implantar seu código e fornecer uma URL para exibir o aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="55c43-209">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="55c43-210">Use para criar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="55c43-210">Use  to create the web app.</span></span> 

<span data-ttu-id="55c43-211">No seguinte comando, substitua o espaço reservado *\<app_name>* por um nome de aplicativo exclusivo.</span><span class="sxs-lookup"><span data-stu-id="55c43-211">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="55c43-212">Esse nome é parte da URL padrão para o aplicativo Web, portanto, o nome precisa ser exclusivo em todos os aplicativos no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="55c43-212">This name is part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="55c43-213">Quando o aplicativo Web tiver sido criado, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="55c43-213">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-the-database-environment-variables"></a><span data-ttu-id="55c43-214">Configurar as variáveis de ambiente do banco de dados</span><span class="sxs-lookup"><span data-stu-id="55c43-214">Configure the database environment variables</span></span>

<span data-ttu-id="55c43-215">No início do tutorial, você definiu as variáveis de ambiente para se conectar a seu banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="55c43-215">Earlier in the tutorial, you defined environment variables to connect to your PostgreSQL database.</span></span>

<span data-ttu-id="55c43-216">No Serviço de Aplicativo, defina as variáveis de ambiente como _configurações do aplicativo_ usando o comando [az webapp config appsettings set](/cli/azure/webapp/config#set).</span><span class="sxs-lookup"><span data-stu-id="55c43-216">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="55c43-217">O seguinte exemplo especifica os detalhes da conexão de banco de dados como configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55c43-217">The following example specifies the database connection details as app settings.</span></span> <span data-ttu-id="55c43-218">Ele também usa a variável *PORT* ao mapa PORT 5000 do seu Contêiner do Docker para receber o tráfego HTTP na PORT 80.</span><span class="sxs-lookup"><span data-stu-id="55c43-218">It also uses the *PORT* variable to map PORT 5000 from your Docker Container to receive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="55c43-219">Configurar a implantação do contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="55c43-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="55c43-220">O Serviço de Aplicativo pode baixar e executar automaticamente um contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="55c43-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="55c43-221">Sempre que você atualizar o contêiner do Docker ou alterar as configurações, reinicie o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55c43-221">Whenever you update the Docker container or change the settings, restart the app.</span></span> <span data-ttu-id="55c43-222">Reiniciar garante que todas as configurações serão aplicadas e o último contêiner será extraído do registro.</span><span class="sxs-lookup"><span data-stu-id="55c43-222">Restarting ensures that all settings are applied and the latest container is pulled from the registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="55c43-223">Navegar até o aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="55c43-223">Browse to the Azure web app</span></span> 

<span data-ttu-id="55c43-224">Navegue até o aplicativo Web implantado usando o navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="55c43-224">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="55c43-225">O aplicativo Web leva mais tempo para carregar porque o contêiner deve ser baixado e iniciado depois que a configuração do contêiner for alterada.</span><span class="sxs-lookup"><span data-stu-id="55c43-225">The web app takes longer to load because the container has to be downloaded and started after the container configuration is changed.</span></span>

<span data-ttu-id="55c43-226">Você verá convidados registrados anteriormente que foram salvos no banco de dados de produção do Azure na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="55c43-226">You see previously registered guests that were saved to the Azure production database in the previous step.</span></span>

![Aplicativo Python Flask baseado em contêiner do Docker em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="55c43-228">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="55c43-228">**Congratulations!**</span></span> <span data-ttu-id="55c43-229">Você está executando um aplicativo Python Flask baseado em um contêiner do Docker no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="55c43-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="55c43-230">Atualizar o modelo de dados e reimplantar</span><span class="sxs-lookup"><span data-stu-id="55c43-230">Update data model and redeploy</span></span>

<span data-ttu-id="55c43-231">Nesta etapa, você adiciona o número de participantes a cada registro de evento atualizando o modelo de Convidado.</span><span class="sxs-lookup"><span data-stu-id="55c43-231">In this step, you add the number of attendees to each event registration by updating the Guest model.</span></span>

<span data-ttu-id="55c43-232">Veja a versão *0.2-migration* com o seguinte comando Git:</span><span class="sxs-lookup"><span data-stu-id="55c43-232">Check out the *0.2-migration* release with the following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="55c43-233">Essa versão já fez as alterações necessárias nos modos de exibição, controladores e modelo.</span><span class="sxs-lookup"><span data-stu-id="55c43-233">This release already made the necessary changes to views, controllers, and model.</span></span> <span data-ttu-id="55c43-234">Ela também inclui uma migração de banco de dados gerada por meio de *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="55c43-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="55c43-235">É possível ver todas as alterações feitas por meio do seguinte comando Git:</span><span class="sxs-lookup"><span data-stu-id="55c43-235">You can see all changes made via the following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="55c43-236">Testar suas alterações localmente</span><span class="sxs-lookup"><span data-stu-id="55c43-236">Test your changes locally</span></span>

<span data-ttu-id="55c43-237">Execute os comandos a seguir para testar as alterações localmente executando o servidor Flask.</span><span class="sxs-lookup"><span data-stu-id="55c43-237">Run the following commands to test your changes locally by running the flask server.</span></span>

<span data-ttu-id="55c43-238">Mac / Linux:</span><span class="sxs-lookup"><span data-stu-id="55c43-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="55c43-239">Navegue até http://127.0.0.1:5000 no navegador para exibir as alterações.</span><span class="sxs-lookup"><span data-stu-id="55c43-239">Navigate to http://127.0.0.1:5000 in your browser to view the changes.</span></span> <span data-ttu-id="55c43-240">Crie um registro de teste.</span><span class="sxs-lookup"><span data-stu-id="55c43-240">Create a test registration.</span></span>

![Aplicativo Python Flask baseado em contêiner do Docker em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-to-azure"></a><span data-ttu-id="55c43-242">Publicar alterações no Azure</span><span class="sxs-lookup"><span data-stu-id="55c43-242">Publish changes to Azure</span></span>

<span data-ttu-id="55c43-243">Crie a nova imagem do Docker, envie-a para o registro de contêiner e reinicie o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55c43-243">Build the new docker image, push it to the container registry, and restart the app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="55c43-244">Navegue até seu aplicativo Web do Azure e teste a nova funcionalidade novamente.</span><span class="sxs-lookup"><span data-stu-id="55c43-244">Navigate to your Azure web app and try out the new functionality again.</span></span> <span data-ttu-id="55c43-245">Crie outro registro de evento.</span><span class="sxs-lookup"><span data-stu-id="55c43-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Aplicativo Docker Python Flask no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="55c43-247">Gerenciar seu aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="55c43-247">Manage your Azure web app</span></span>

<span data-ttu-id="55c43-248">Vá para o [portal do Azure](https://portal.azure.com) para ver o aplicativo Web que você criou.</span><span class="sxs-lookup"><span data-stu-id="55c43-248">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="55c43-249">No menu à esquerda, clique em **Serviço de Aplicativos** e, em seguida, clique no nome do seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="55c43-249">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Navegação do portal para o aplicativo Web do Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="55c43-251">Por padrão, o portal mostra a página **Visão geral** do seu aplicativo Web .</span><span class="sxs-lookup"><span data-stu-id="55c43-251">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="55c43-252">Esta página fornece uma visão de como está seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55c43-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="55c43-253">Aqui, você também pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="55c43-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="55c43-254">As guias no lado esquerdo da página mostram as páginas de configuração diferentes que você pode abrir.</span><span class="sxs-lookup"><span data-stu-id="55c43-254">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Página Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="55c43-256">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="55c43-256">Next steps</span></span>

<span data-ttu-id="55c43-257">Vá para o próximo tutorial para saber como mapear um nome DNS personalizado para o seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="55c43-257">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="55c43-258">Mapear um nome DNS personalizado existente para aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="55c43-258">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
