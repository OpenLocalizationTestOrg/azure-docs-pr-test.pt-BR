---
title: aaaBuild um aplicativo web Python Docker e PostgreSQL no Azure | Microsoft Docs
description: "Saiba como tooget um aplicativo de Docker Python trabalhando no Azure, com conexão tooa PostgreSQL de banco de dados."
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
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="a23f6-103">Compilar um aplicativo Web Docker Python e PostgreSQL no Azure</span><span class="sxs-lookup"><span data-stu-id="a23f6-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="a23f6-104">Os aplicativos Web do Azure fornecem um serviço de hospedagem na Web altamente escalonável, com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="a23f6-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="a23f6-105">Este tutorial mostra como toocreate um Python Docker básica web aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="a23f6-105">This tutorial shows how toocreate a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="a23f6-106">Você vai se conectar a esse banco de dados do aplicativo tooa PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a23f6-106">You'll connect this app tooa PostgreSQL database.</span></span> <span data-ttu-id="a23f6-107">Quando terminar, você terá um aplicativo Python Flask em execução dentro de um contêiner do Docker nos [Aplicativos Web do Serviço de Aplicativo do Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a23f6-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Aplicativo Docker Python Flask no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="a23f6-109">Você pode seguir as etapas de saudação abaixo em macOS.</span><span class="sxs-lookup"><span data-stu-id="a23f6-109">You can follow hello steps below on macOS.</span></span> <span data-ttu-id="a23f6-110">Instruções do Linux e Windows são Olá mesmo na maioria dos casos, mas as diferenças de saudação não são detalhadas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a23f6-110">Linux and Windows instructions are hello same in most cases, but hello differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="a23f6-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a23f6-111">Prerequisites</span></span>

<span data-ttu-id="a23f6-112">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="a23f6-112">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="a23f6-113">Instalar o Git</span><span class="sxs-lookup"><span data-stu-id="a23f6-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="a23f6-114">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="a23f6-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="a23f6-115">Instale e execute o PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="a23f6-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="a23f6-116">Instale o Docker Community Edition</span><span class="sxs-lookup"><span data-stu-id="a23f6-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a23f6-117">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a23f6-117">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a23f6-118">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a23f6-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a23f6-119">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a23f6-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="a23f6-120">Testar a instalação do PostgreSQL local e criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="a23f6-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="a23f6-121">Abra a janela do terminal hello e execute `psql postgres` tooconnect tooyour local PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="a23f6-121">Open hello terminal window and run `psql postgres` tooconnect tooyour local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="a23f6-122">Se sua conexão tiver êxito, o banco de dados PostgreSQL já estará em execução.</span><span class="sxs-lookup"><span data-stu-id="a23f6-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="a23f6-123">Se não, certifique-se de que o banco de dados PostgresQL local é iniciado, seguindo as etapas de saudação em [Downloads - PostgreSQL Core distribuição](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="a23f6-123">If not, make sure that your local PostgresQL database is started by following hello steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="a23f6-124">Crie um banco de dados chamado *eventregistration* e configure um usuário de banco de dados separado chamado *manager* com a senha *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="a23f6-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
<span data-ttu-id="a23f6-125">Tipo *\q* cliente do tooexit Olá PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a23f6-125">Type *\q* tooexit hello PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="a23f6-126">Criar um aplicativo Python Flask local</span><span class="sxs-lookup"><span data-stu-id="a23f6-126">Create local Python Flask application</span></span>

<span data-ttu-id="a23f6-127">Nesta etapa, você configura Olá local Python bulbo projeto.</span><span class="sxs-lookup"><span data-stu-id="a23f6-127">In this step, you set up hello local Python Flask project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="a23f6-128">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="a23f6-128">Clone hello sample application</span></span>

<span data-ttu-id="a23f6-129">Janela do terminal Olá aberta, e `CD` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a23f6-129">Open hello terminal window, and `CD` tooa working directory.</span></span>  

<span data-ttu-id="a23f6-130">Seguinte Olá executar comandos tooclone Olá exemplo repositório e ir toohello *initialapp 0.1* de versão.</span><span class="sxs-lookup"><span data-stu-id="a23f6-130">Run hello following commands tooclone hello sample repository and go toohello *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="a23f6-131">Esse repositório de exemplo contém um aplicativo [Flask](http://flask.pocoo.org/).</span><span class="sxs-lookup"><span data-stu-id="a23f6-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-hello-application"></a><span data-ttu-id="a23f6-132">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="a23f6-132">Run hello application</span></span>

> [!NOTE] 
> <span data-ttu-id="a23f6-133">Em uma etapa posterior, você simplificar esse processo criando um toouse de contêiner do Docker com o banco de dados de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="a23f6-133">In a later step you simplify this process by building a Docker container toouse with hello production database.</span></span>

<span data-ttu-id="a23f6-134">Instalar pacotes de saudação necessários e iniciar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a23f6-134">Install hello required packages and start hello application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="a23f6-135">Quando o aplicativo hello está totalmente carregado, você verá algo semelhante toohello seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="a23f6-135">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="a23f6-136">Navegue toohttp://127.0.0.1:5000 em um navegador.</span><span class="sxs-lookup"><span data-stu-id="a23f6-136">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="a23f6-137">Clique em **Registrar!**</span><span class="sxs-lookup"><span data-stu-id="a23f6-137">Click **Register!**</span></span> <span data-ttu-id="a23f6-138">e crie um usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="a23f6-138">and create a test user.</span></span>

![Aplicativo Python Flask em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="a23f6-140">Olá aplicativo de exemplo do bulbo armazena dados de usuário no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="a23f6-140">hello Flask sample application stores user data in hello database.</span></span> <span data-ttu-id="a23f6-141">Se você estiver com êxito no registro de um usuário, seu aplicativo está gravando dados toohello PostgreSQL banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="a23f6-141">If you are successful at registering a user, your app is writing data toohello local PostgreSQL database.</span></span>

<span data-ttu-id="a23f6-142">toostop Olá bulbo servidor a qualquer momento, digite Ctrl + C Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="a23f6-142">toostop hello Flask server at anytime, type Ctrl+C in hello terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="a23f6-143">Criar um banco de dados PostgreSQL de produção</span><span class="sxs-lookup"><span data-stu-id="a23f6-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="a23f6-144">Nesta etapa, você cria um banco de dados PostgreSQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="a23f6-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="a23f6-145">Quando seu aplicativo é implantado tooAzure, ele usará esse banco de dados de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a23f6-145">When your app is deployed tooAzure, it will use this cloud database.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="a23f6-146">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="a23f6-146">Log in tooAzure</span></span>

<span data-ttu-id="a23f6-147">Você está agora necessários de recursos de saudação do contínuo toouse hello Azure CLI 2.0 toocreate toohost seu aplicativo Python no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a23f6-147">You are now going toouse hello Azure CLI 2.0 toocreate hello resources needed toohost your Python application in Azure App Service.</span></span>  <span data-ttu-id="a23f6-148">Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="a23f6-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="a23f6-149">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a23f6-149">Create a resource group</span></span>

<span data-ttu-id="a23f6-150">Criar um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) com hello [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a23f6-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="a23f6-151">Olá exemplo a seguir cria um grupo de recursos na região Oeste dos EUA de saudação:</span><span class="sxs-lookup"><span data-stu-id="a23f6-151">hello following example creates a resource group in hello West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="a23f6-152">Saudação de uso [locais de lista do serviço de aplicativo az](/cli/azure/appservice#list-locations) locais disponíveis toolist de comando CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a23f6-152">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="a23f6-153">Criar um Banco de Dados do Azure para o servidor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="a23f6-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="a23f6-154">Criar um servidor PostgreSQL com hello [az postgres server criar](/cli/azure/documentdb#create) comando.</span><span class="sxs-lookup"><span data-stu-id="a23f6-154">Create a PostgreSQL server with hello [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="a23f6-155">Olá a seguir de comando, substitua um nome de servidor exclusivo para Olá  *\<postgresql_name >* espaço reservado e um nome de usuário para Olá  *\<admin_username >* espaço reservado .</span><span class="sxs-lookup"><span data-stu-id="a23f6-155">In hello following command, substitute a unique server name for hello *\<postgresql_name>* placeholder and a user name for hello *\<admin_username>* placeholder.</span></span> <span data-ttu-id="a23f6-156">nome do servidor de saudação for usado como parte de seu ponto de extremidade PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), portanto, o nome do hello deve toobe exclusivo em todos os servidores no Azure.</span><span class="sxs-lookup"><span data-stu-id="a23f6-156">hello server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so hello name needs toobe unique across all servers in Azure.</span></span> <span data-ttu-id="a23f6-157">nome de usuário Olá destina-se a conta de usuário do administrador de banco de dados inicial de saudação.</span><span class="sxs-lookup"><span data-stu-id="a23f6-157">hello user name is for hello initial database admin user account.</span></span> <span data-ttu-id="a23f6-158">Você está toopick solicitada uma senha para este usuário.</span><span class="sxs-lookup"><span data-stu-id="a23f6-158">You are prompted toopick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="a23f6-159">Quando Olá banco de dados PostgreSQL servidor é criada, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a23f6-159">When hello Azure Database for PostgreSQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a><span data-ttu-id="a23f6-160">Criar uma regra de firewall para hello banco de dados do Azure para servidor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="a23f6-160">Create a firewall rule for hello Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="a23f6-161">Execute Olá seguir CLI do Azure comando tooallow toohello banco de dados de todos os endereços IP.</span><span class="sxs-lookup"><span data-stu-id="a23f6-161">Run hello following Azure CLI command tooallow access toohello database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="a23f6-162">Olá CLI do Azure confirma a criação de regra de firewall de saudação com saída toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a23f6-162">hello Azure CLI confirms hello firewall rule creation with output similar toohello following example:</span></span>

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

## <a name="connect-your-python-flask-application-toohello-database"></a><span data-ttu-id="a23f6-163">Conecte-se o seu banco de dados do Python bulbo aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="a23f6-163">Connect your Python Flask application toohello database</span></span>

<span data-ttu-id="a23f6-164">Nesta etapa, você se conectar a servidor PostgreSQL que você criou seu bulbo Python exemplo aplicativo toohello banco de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="a23f6-164">In this step, you connect your Python Flask sample application toohello Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="a23f6-165">Criando um banco de dados vazio e configurando um novo usuário do aplicativo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="a23f6-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="a23f6-166">Crie um usuário de banco de dados com tooa único banco de dados somente.</span><span class="sxs-lookup"><span data-stu-id="a23f6-166">Create a database user with access tooa single database only.</span></span> <span data-ttu-id="a23f6-167">Você usará esses tooavoid credenciais entregar Olá aplicativo acesso completo toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="a23f6-167">You'll use these credentials tooavoid giving hello application full access toohello server.</span></span>

<span data-ttu-id="a23f6-168">Conecte o banco de dados de toohello (você for solicitado a fornecer sua senha de administrador).</span><span class="sxs-lookup"><span data-stu-id="a23f6-168">Connect toohello database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="a23f6-169">Crie banco de dados de saudação e usuário de saudação PostgreSQL CLI.</span><span class="sxs-lookup"><span data-stu-id="a23f6-169">Create hello database and user from hello PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

<span data-ttu-id="a23f6-170">Tipo *\q* cliente do tooexit Olá PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a23f6-170">Type *\q* tooexit hello PostgreSQL client.</span></span>

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a><span data-ttu-id="a23f6-171">Testar o aplicativo hello localmente no banco de dados PostgreSQL do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="a23f6-171">Test hello application locally against hello Azure PostgreSQL database</span></span> 

<span data-ttu-id="a23f6-172">Voltando agora toohello *aplicativo* pasta da saudação clonado repositório Github, você pode executar o aplicativo de Python bulbo hello atualizando variáveis de ambiente de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="a23f6-172">Going back now toohello *app* folder of hello cloned Github repository, you can run hello Python Flask application by updating hello database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="a23f6-173">Quando o aplicativo hello está totalmente carregado, você verá algo semelhante toohello seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="a23f6-173">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="a23f6-174">Navegue toohttp://127.0.0.1:5000 em um navegador.</span><span class="sxs-lookup"><span data-stu-id="a23f6-174">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="a23f6-175">Clique em **Registrar!**</span><span class="sxs-lookup"><span data-stu-id="a23f6-175">Click **Register!**</span></span> <span data-ttu-id="a23f6-176">e crie um registro de teste.</span><span class="sxs-lookup"><span data-stu-id="a23f6-176">and create a test registration.</span></span> <span data-ttu-id="a23f6-177">Agora você está criando o banco de dados de toohello de dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="a23f6-177">You are now writing data toohello database in Azure.</span></span>

![Aplicativo Python Flask em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a><span data-ttu-id="a23f6-179">Executando o aplicativo hello de um contêiner de Docker</span><span class="sxs-lookup"><span data-stu-id="a23f6-179">Running hello application from a Docker Container</span></span>

<span data-ttu-id="a23f6-180">Crie imagem de contêiner do Docker hello.</span><span class="sxs-lookup"><span data-stu-id="a23f6-180">Build hello Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="a23f6-181">Docker exibirá uma confirmação contêiner Olá criou com êxito.</span><span class="sxs-lookup"><span data-stu-id="a23f6-181">Docker displays a confirmation that it successfully created hello container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="a23f6-182">Adicionar arquivo da variável de ambiente banco de dados ambiente variáveis tooan *db.env*.</span><span class="sxs-lookup"><span data-stu-id="a23f6-182">Add database environment variables tooan environment variable file *db.env*.</span></span> <span data-ttu-id="a23f6-183">aplicativo Hello conectará o banco de dados de produção PostgreSQL de toohello no Azure.</span><span class="sxs-lookup"><span data-stu-id="a23f6-183">hello app will connect toohello PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="a23f6-184">Execute o aplicativo de saudação de dentro do contêiner do Docker hello.</span><span class="sxs-lookup"><span data-stu-id="a23f6-184">Run hello app from within hello Docker container.</span></span> <span data-ttu-id="a23f6-185">Olá comando a seguir especifica o arquivo de variável de ambiente hello e mapeia saudação padrão bulbo 5000 toolocal porta 5000.</span><span class="sxs-lookup"><span data-stu-id="a23f6-185">hello following command specifies hello environment variable file and maps hello default Flask port 5000 toolocal port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="a23f6-186">saída de Hello é toowhat semelhante que vimos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a23f6-186">hello output is similar toowhat you saw earlier.</span></span> <span data-ttu-id="a23f6-187">No entanto, a migração do banco de dados inicial de saudação não precisa mais toobe executada e, portanto, é ignorada.</span><span class="sxs-lookup"><span data-stu-id="a23f6-187">However, hello initial database migration no longer needs toobe performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="a23f6-188">banco de dados de saudação já contém o registro Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a23f6-188">hello database already contains hello registration you created previously.</span></span>

![Aplicativo Python Flask baseado em contêiner do Docker em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a><span data-ttu-id="a23f6-190">Carregar o registro de contêiner tooa do contêiner de Docker Olá</span><span class="sxs-lookup"><span data-stu-id="a23f6-190">Upload hello Docker container tooa container registry</span></span>

<span data-ttu-id="a23f6-191">Nesta etapa, você deve carregar o registro de contêiner do hello Docker contêiner tooa.</span><span class="sxs-lookup"><span data-stu-id="a23f6-191">In this step, you upload hello Docker container tooa container registry.</span></span> <span data-ttu-id="a23f6-192">Você utilizará o Registro de Contêiner do Azure, mas também pode usar outros registros populares, como o Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="a23f6-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="a23f6-193">Criar um Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="a23f6-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="a23f6-194">Olá após o comando toocreate um registro de contêiner substitua  *\<registry_name >* com um nome de registro do contêiner do Azure exclusivo de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="a23f6-194">In hello following command toocreate a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="a23f6-195">Saída</span><span class="sxs-lookup"><span data-stu-id="a23f6-195">Output</span></span>
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

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="a23f6-196">Recuperar as credenciais de registro hello para enviar por push e pull imagens do Docker</span><span class="sxs-lookup"><span data-stu-id="a23f6-196">Retrieve hello registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="a23f6-197">credenciais de registro tooshow, habilite o modo de administração pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="a23f6-197">tooshow registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="a23f6-198">Você verá duas senhas.</span><span class="sxs-lookup"><span data-stu-id="a23f6-198">You see two passwords.</span></span> <span data-ttu-id="a23f6-199">Anote o nome de usuário hello e senha primeiro hello.</span><span class="sxs-lookup"><span data-stu-id="a23f6-199">Make note of hello user name and hello first password.</span></span>

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

### <a name="upload-your-docker-container-tooazure-container-registry"></a><span data-ttu-id="a23f6-200">Carregue seu contêiner de Docker tooAzure registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="a23f6-200">Upload your Docker container tooAzure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a><span data-ttu-id="a23f6-201">Implantar Olá Docker Python bulbo aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="a23f6-201">Deploy hello Docker Python Flask application tooAzure</span></span>

<span data-ttu-id="a23f6-202">Nesta etapa, você deve implantar o tooAzure de aplicativo de Python bulbo de baseado no contêiner de Docker do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a23f6-202">In this step, you deploy your Docker container-based Python Flask application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="a23f6-203">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a23f6-203">Create an App Service plan</span></span>

<span data-ttu-id="a23f6-204">Criar um plano de serviço de aplicativo com hello [criar plano de serviço de aplicativo az](/cli/azure/appservice/plan#create) comando.</span><span class="sxs-lookup"><span data-stu-id="a23f6-204">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="a23f6-205">Olá, exemplo a seguir cria um plano de serviço de aplicativo baseado em Linux chamado *myAppServicePlan* usando Olá S1 preço:</span><span class="sxs-lookup"><span data-stu-id="a23f6-205">hello following example creates a Linux-based App Service plan named *myAppServicePlan* using hello S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="a23f6-206">Quando Olá plano de serviço de aplicativo é criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a23f6-206">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="a23f6-207">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="a23f6-207">Create a web app</span></span>

<span data-ttu-id="a23f6-208">Criar um aplicativo web no hello *myAppServicePlan* plano de serviço de aplicativo com hello [az webapp criar](/cli/azure/webapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="a23f6-208">Create a web app in hello *myAppServicePlan* App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="a23f6-209">Fornece de aplicativo de web Hello você hospedagem espaço toodeploy seu código e fornece uma URL para você Olá tooview aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="a23f6-209">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="a23f6-210">Use toocreate Olá web app.</span><span class="sxs-lookup"><span data-stu-id="a23f6-210">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="a23f6-211">Olá a seguir de comando, substitua Olá  *\<app_name >* espaço reservado com um nome exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a23f6-211">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="a23f6-212">Esse nome faz parte da URL de padrão de saudação do aplicativo da web de Olá, para que o nome do hello deve toobe exclusivo entre todos os aplicativos no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a23f6-212">This name is part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="a23f6-213">Quando o aplicativo da web de saudação tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a23f6-213">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-hello-database-environment-variables"></a><span data-ttu-id="a23f6-214">Configurar variáveis de ambiente de banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="a23f6-214">Configure hello database environment variables</span></span>

<span data-ttu-id="a23f6-215">Anteriormente no tutorial hello, definido pelo banco de dados do ambiente variáveis tooconnect tooyour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a23f6-215">Earlier in hello tutorial, you defined environment variables tooconnect tooyour PostgreSQL database.</span></span>

<span data-ttu-id="a23f6-216">No serviço de aplicativo, você definir variáveis de ambiente como _configurações do aplicativo_ usando Olá [az webapp configuração appsettings conjunto](/cli/azure/webapp/config#set) comando.</span><span class="sxs-lookup"><span data-stu-id="a23f6-216">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="a23f6-217">Olá exemplo a seguir especifica detalhes de conexão de banco de dados de saudação como configurações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a23f6-217">hello following example specifies hello database connection details as app settings.</span></span> <span data-ttu-id="a23f6-218">Ele também usa Olá *porta* variável toomap PORT 5000 seu tráfego de tooreceive HTTP do contêiner do Docker na porta 80.</span><span class="sxs-lookup"><span data-stu-id="a23f6-218">It also uses hello *PORT* variable toomap PORT 5000 from your Docker Container tooreceive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="a23f6-219">Configurar a implantação do contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="a23f6-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="a23f6-220">O Serviço de Aplicativo pode baixar e executar automaticamente um contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="a23f6-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="a23f6-221">Sempre que você atualiza o contêiner de Docker hello, ou alterar configurações de hello, reinicie o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a23f6-221">Whenever you update hello Docker container or change hello settings, restart hello app.</span></span> <span data-ttu-id="a23f6-222">Reiniciar garante que todas as configurações são aplicadas e contêiner mais recente Olá retirado do registro hello.</span><span class="sxs-lookup"><span data-stu-id="a23f6-222">Restarting ensures that all settings are applied and hello latest container is pulled from hello registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="a23f6-223">Procurar o aplicativo web do Azure de toohello</span><span class="sxs-lookup"><span data-stu-id="a23f6-223">Browse toohello Azure web app</span></span> 

<span data-ttu-id="a23f6-224">Procurar toohello implantado um aplicativo da web usando um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="a23f6-224">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="a23f6-225">Olá web app leva mais tooload como contêiner de saudação tem toobe baixados e iniciados após a alteração de configuração do contêiner hello.</span><span class="sxs-lookup"><span data-stu-id="a23f6-225">hello web app takes longer tooload because hello container has toobe downloaded and started after hello container configuration is changed.</span></span>

<span data-ttu-id="a23f6-226">Você verá convidados registrados anteriormente que foram salvos o banco de dados de produção do Azure toohello na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="a23f6-226">You see previously registered guests that were saved toohello Azure production database in hello previous step.</span></span>

![Aplicativo Python Flask baseado em contêiner do Docker em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="a23f6-228">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="a23f6-228">**Congratulations!**</span></span> <span data-ttu-id="a23f6-229">Você está executando um aplicativo Python Flask baseado em um contêiner do Docker no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a23f6-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="a23f6-230">Atualizar o modelo de dados e reimplantar</span><span class="sxs-lookup"><span data-stu-id="a23f6-230">Update data model and redeploy</span></span>

<span data-ttu-id="a23f6-231">Nesta etapa, você pode adicionar número Olá participantes tooeach de registro de eventos atualizando o modelo de convidado hello.</span><span class="sxs-lookup"><span data-stu-id="a23f6-231">In this step, you add hello number of attendees tooeach event registration by updating hello Guest model.</span></span>

<span data-ttu-id="a23f6-232">Check-out Olá *0,2 migração* versão com hello git comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a23f6-232">Check out hello *0.2-migration* release with hello following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="a23f6-233">Esta versão já feitas Olá modelo, controladores e tooviews as alterações necessárias.</span><span class="sxs-lookup"><span data-stu-id="a23f6-233">This release already made hello necessary changes tooviews, controllers, and model.</span></span> <span data-ttu-id="a23f6-234">Ela também inclui uma migração de banco de dados gerada por meio de *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="a23f6-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="a23f6-235">Você pode ver todas as alterações feitas por meio da saudação git comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a23f6-235">You can see all changes made via hello following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="a23f6-236">Testar suas alterações localmente</span><span class="sxs-lookup"><span data-stu-id="a23f6-236">Test your changes locally</span></span>

<span data-ttu-id="a23f6-237">Execute Olá tootest comandos a seguir as alterações localmente pelo servidor de bulbo Olá em execução.</span><span class="sxs-lookup"><span data-stu-id="a23f6-237">Run hello following commands tootest your changes locally by running hello flask server.</span></span>

<span data-ttu-id="a23f6-238">Mac / Linux:</span><span class="sxs-lookup"><span data-stu-id="a23f6-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="a23f6-239">Navegue toohttp://127.0.0.1:5000 suas alterações de saudação do navegador tooview.</span><span class="sxs-lookup"><span data-stu-id="a23f6-239">Navigate toohttp://127.0.0.1:5000 in your browser tooview hello changes.</span></span> <span data-ttu-id="a23f6-240">Crie um registro de teste.</span><span class="sxs-lookup"><span data-stu-id="a23f6-240">Create a test registration.</span></span>

![Aplicativo Python Flask baseado em contêiner do Docker em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a><span data-ttu-id="a23f6-242">Publicar alterações tooAzure</span><span class="sxs-lookup"><span data-stu-id="a23f6-242">Publish changes tooAzure</span></span>

<span data-ttu-id="a23f6-243">Criar nova imagem do docker hello, por push do registro de contêiner toohello e reiniciar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a23f6-243">Build hello new docker image, push it toohello container registry, and restart hello app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="a23f6-244">Navegue tooyour aplicativo de web do Azure e experimente a nova funcionalidade de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="a23f6-244">Navigate tooyour Azure web app and try out hello new functionality again.</span></span> <span data-ttu-id="a23f6-245">Crie outro registro de evento.</span><span class="sxs-lookup"><span data-stu-id="a23f6-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Aplicativo Docker Python Flask no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="a23f6-247">Gerenciar seu aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="a23f6-247">Manage your Azure web app</span></span>

<span data-ttu-id="a23f6-248">Vá toohello [portal do Azure](https://portal.azure.com) toosee Olá web aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="a23f6-248">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="a23f6-249">No menu à esquerda do hello, clique em **serviços de aplicativos**, clique em nome de saudação do seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a23f6-249">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="a23f6-251">Por padrão, o portal de saudação mostra seu aplicativo de web **visão geral** página.</span><span class="sxs-lookup"><span data-stu-id="a23f6-251">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="a23f6-252">Esta página fornece uma visão de como está seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a23f6-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="a23f6-253">Aqui, você também pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="a23f6-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="a23f6-254">guias de Olá no lado esquerdo de saudação da página de saudação mostram páginas de configuração diferentes de hello, que você pode abrir.</span><span class="sxs-lookup"><span data-stu-id="a23f6-254">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Página Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="a23f6-256">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a23f6-256">Next steps</span></span>

<span data-ttu-id="a23f6-257">Avançar toolearn tutorial do próximo toohello como toomap um DNS personalizado nome tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="a23f6-257">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="a23f6-258">Mapear um tooAzure de nome DNS de personalizada existente aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="a23f6-258">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
