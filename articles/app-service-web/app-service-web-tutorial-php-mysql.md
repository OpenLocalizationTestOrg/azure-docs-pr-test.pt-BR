---
title: aaaBuild um aplicativo web PHP e MySQL no Azure | Microsoft Docs
description: "Saiba como tooget um aplicativo PHP trabalhando no Azure, com tooa de conexão MySQL do banco de dados no Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="8268d-103">Compilar um aplicativo Web PHP e MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="8268d-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="8268d-104">Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="8268d-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="8268d-105">Este tutorial mostra como toocreate um PHP aplicativo no Azure da web e conectá-lo tooa banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8268d-105">This tutorial shows how toocreate a PHP web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="8268d-106">Quando terminar, você terá um aplicativo [Laravel](https://laravel.com/) em execução nos Aplicativos Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="8268d-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![Aplicativo PHP em execução no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="8268d-108">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="8268d-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8268d-109">Criar um banco de dados MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="8268d-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="8268d-110">Conecte-se um tooMySQL do aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="8268d-110">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="8268d-111">Implantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="8268d-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="8268d-112">Atualizar o modelo de dados hello e reimplantar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="8268d-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="8268d-113">Transmitir logs de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="8268d-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="8268d-114">Gerenciar o aplicativo hello em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8268d-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8268d-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8268d-115">Prerequisites</span></span>

<span data-ttu-id="8268d-116">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="8268d-116">toocomplete this tutorial:</span></span>

* [<span data-ttu-id="8268d-117">Instalar o Git</span><span class="sxs-lookup"><span data-stu-id="8268d-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="8268d-118">Instalar o PHP 5.6.4 ou posterior</span><span class="sxs-lookup"><span data-stu-id="8268d-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="8268d-119">Instalar o Composer</span><span class="sxs-lookup"><span data-stu-id="8268d-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="8268d-120">Habilitar Olá extensões PHP Laravel necessidades a seguir: OpenSSL PDO MySQL, Mbstring, Tokenizer, XML</span><span class="sxs-lookup"><span data-stu-id="8268d-120">Enable hello following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="8268d-121">Instalar e iniciar o MySQL</span><span class="sxs-lookup"><span data-stu-id="8268d-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="8268d-122">Preparar o MySQL local</span><span class="sxs-lookup"><span data-stu-id="8268d-122">Prepare local MySQL</span></span>

<span data-ttu-id="8268d-123">Nesta etapa, você cria um banco de dados em seu servidor MySQL local para uso neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="8268d-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-toolocal-mysql-server"></a><span data-ttu-id="8268d-124">Conecte-se toolocal MySQL server</span><span class="sxs-lookup"><span data-stu-id="8268d-124">Connect toolocal MySQL server</span></span>

<span data-ttu-id="8268d-125">Em uma janela de terminal, conecte-se tooyour local MySQL server.</span><span class="sxs-lookup"><span data-stu-id="8268d-125">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="8268d-126">Você pode usar essa janela do terminal toorun todos os comandos de saudação neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="8268d-126">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="8268d-127">Se você for solicitado a fornecer uma senha, digite a senha de saudação para Olá `root` conta.</span><span class="sxs-lookup"><span data-stu-id="8268d-127">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="8268d-128">Se você não lembrar a senha da conta raiz, consulte [MySQL: como tooReset Olá senha raiz](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="8268d-128">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="8268d-129">Se o comando for executado com êxito, o MySQL Server estará em execução.</span><span class="sxs-lookup"><span data-stu-id="8268d-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="8268d-130">Se não, certifique-se de que o servidor MySQL local é iniciado por seguir Olá [etapas de pós-instalação do MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="8268d-130">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="8268d-131">Criar um banco de dados localmente</span><span class="sxs-lookup"><span data-stu-id="8268d-131">Create a database locally</span></span>

<span data-ttu-id="8268d-132">Em Olá `mysql` solicitar, crie um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8268d-132">At hello `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="8268d-133">Saia da conexão do servidor digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="8268d-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="8268d-134">Criar um aplicativo PHP localmente</span><span class="sxs-lookup"><span data-stu-id="8268d-134">Create a PHP app locally</span></span>
<span data-ttu-id="8268d-135">Nesta etapa, você obtém um aplicativo de exemplo Laravel, configura sua conexão de banco de dados e o executa localmente.</span><span class="sxs-lookup"><span data-stu-id="8268d-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="8268d-136">Exemplo de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="8268d-136">Clone hello sample</span></span>

<span data-ttu-id="8268d-137">Na janela do terminal hello, `cd` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8268d-137">In hello terminal window, `cd` tooa working directory.</span></span>

<span data-ttu-id="8268d-138">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="8268d-138">Run hello following command tooclone hello sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="8268d-139">`cd`diretório de tooyour clonado.</span><span class="sxs-lookup"><span data-stu-id="8268d-139">`cd` tooyour cloned directory.</span></span>
<span data-ttu-id="8268d-140">Instale pacotes de saudação necessário.</span><span class="sxs-lookup"><span data-stu-id="8268d-140">Install hello required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="8268d-141">Configurar a conexão do MySQL</span><span class="sxs-lookup"><span data-stu-id="8268d-141">Configure MySQL connection</span></span>

<span data-ttu-id="8268d-142">Na raiz do repositório hello, crie um arquivo chamado *.env*.</span><span class="sxs-lookup"><span data-stu-id="8268d-142">In hello repository root, create a file named *.env*.</span></span> <span data-ttu-id="8268d-143">Saudação de cópia variáveis a seguir em hello *.env* arquivo.</span><span class="sxs-lookup"><span data-stu-id="8268d-143">Copy hello following variables into hello *.env* file.</span></span> <span data-ttu-id="8268d-144">Substituir saudação  _&lt;root_password >_ espaço reservado com a senha do usuário do hello MySQL raiz.</span><span class="sxs-lookup"><span data-stu-id="8268d-144">Replace hello _&lt;root_password>_ placeholder with hello MySQL root user's password.</span></span>

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

<span data-ttu-id="8268d-145">Para obter informações sobre como Laravel usa Olá _.env_ de arquivos, consulte [configuração do ambiente Laravel](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="8268d-145">For information on how Laravel uses hello _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-hello-sample-locally"></a><span data-ttu-id="8268d-146">Executar o exemplo hello localmente</span><span class="sxs-lookup"><span data-stu-id="8268d-146">Run hello sample locally</span></span>

<span data-ttu-id="8268d-147">Executar [migrações de banco de dados de Laravel](https://laravel.com/docs/5.4/migrations) toocreate Olá tabelas Olá as necessidades do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8268d-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) toocreate hello tables hello application needs.</span></span> <span data-ttu-id="8268d-148">toosee quais tabelas são criadas em migrações hello, procure no hello _banco de dados/migrações_ diretório no repositório do Git hello.</span><span class="sxs-lookup"><span data-stu-id="8268d-148">toosee which tables are created in hello migrations, look in hello _database/migrations_ directory in hello Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="8268d-149">Gere uma nova chave de aplicativo do Laravel.</span><span class="sxs-lookup"><span data-stu-id="8268d-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="8268d-150">Execute o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8268d-150">Run hello application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="8268d-151">Navegue muito`http://localhost:8000` em um navegador.</span><span class="sxs-lookup"><span data-stu-id="8268d-151">Navigate too`http://localhost:8000` in a browser.</span></span> <span data-ttu-id="8268d-152">Adicione algumas tarefas na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="8268d-152">Add a few tasks in hello page.</span></span>

![PHP se conecta com êxito tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="8268d-154">Digite toostop PHP, `Ctrl + C` em Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="8268d-154">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="8268d-155">Criar o MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="8268d-155">Create MySQL in Azure</span></span>

<span data-ttu-id="8268d-156">Nesta etapa, você cria um banco de dados MySQL no [Banco de dados do Azure para MySQL (versão prévia)](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="8268d-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="8268d-157">Posteriormente, você pode configurar Olá PHP aplicativo tooconnect toothis banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8268d-157">Later, you configure hello PHP application tooconnect toothis database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="8268d-158">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8268d-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="8268d-159">Criar um servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="8268d-159">Create a MySQL server</span></span>

<span data-ttu-id="8268d-160">Criar um servidor de banco de dados do Azure para MySQL (visualização) com hello [az mysql server criar](/cli/azure/mysql/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8268d-160">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="8268d-161">Olá a seguir de comando, substitua o nome do servidor MySQL onde você pode ver Olá  _&lt;mysql_server_name >_ espaço reservado (caracteres válidos são `a-z`, `0-9`, e `-`).</span><span class="sxs-lookup"><span data-stu-id="8268d-161">In hello following command, substitute your MySQL server name where you see hello _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="8268d-162">Esse nome faz parte do nome do host do servidor de saudação MySQL (`<mysql_server_name>.database.windows.net`), ele precisa toobe globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="8268d-162">This name is part of hello MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs toobe globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="8268d-163">Quando o servidor do hello MySQL é criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8268d-163">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="8268d-164">Configurar o firewall do servidor</span><span class="sxs-lookup"><span data-stu-id="8268d-164">Configure server firewall</span></span>

<span data-ttu-id="8268d-165">Criar uma regra de firewall para o cliente do MySQL server tooallow conexões usando Olá [criar regra de firewall de servidor de mysql de az](/cli/azure/mysql/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8268d-165">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="8268d-166">Banco de dados do Azure para MySQL (visualização) atualmente não limita os serviços tooAzure somente conexões.</span><span class="sxs-lookup"><span data-stu-id="8268d-166">Azure Database for MySQL (Preview) doesn't currently limit connections only tooAzure services.</span></span> <span data-ttu-id="8268d-167">Como os endereços IP no Azure são atribuídos dinamicamente, é melhor tooenable todos os endereços IP.</span><span class="sxs-lookup"><span data-stu-id="8268d-167">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses.</span></span> <span data-ttu-id="8268d-168">serviço de saudação está em visualização.</span><span class="sxs-lookup"><span data-stu-id="8268d-168">hello service is in preview.</span></span> <span data-ttu-id="8268d-169">Estamos planejando melhores métodos para proteger o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8268d-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a><span data-ttu-id="8268d-170">Conecte-se tooproduction do MySQL server localmente</span><span class="sxs-lookup"><span data-stu-id="8268d-170">Connect tooproduction MySQL server locally</span></span>

<span data-ttu-id="8268d-171">Na janela do terminal hello, conecte-se toohello MySQL server no Azure.</span><span class="sxs-lookup"><span data-stu-id="8268d-171">In hello terminal window, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="8268d-172">Usar valor Olá especificado anteriormente para  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="8268d-172">Use hello value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="8268d-173">Quando for solicitada uma senha, use _tr0ngPa $$ w0rd!_, que você especificou quando criou o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8268d-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created hello database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="8268d-174">Criar um banco de dados de produção</span><span class="sxs-lookup"><span data-stu-id="8268d-174">Create a production database</span></span>

<span data-ttu-id="8268d-175">Em Olá `mysql` solicitar, crie um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8268d-175">At hello `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="8268d-176">Criar um usuário com permissões</span><span class="sxs-lookup"><span data-stu-id="8268d-176">Create a user with permissions</span></span>

<span data-ttu-id="8268d-177">Crie um usuário de banco de dados chamado _phpappuser_ e dê a ele todos os privilégios em Olá `sampledb` banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8268d-177">Create a database user called _phpappuser_ and give it all privileges in hello `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

<span data-ttu-id="8268d-178">Saia de conexão do servidor de saudação digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="8268d-178">Exit hello server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a><span data-ttu-id="8268d-179">Conecte-se o aplicativo tooAzure MySQL</span><span class="sxs-lookup"><span data-stu-id="8268d-179">Connect app tooAzure MySQL</span></span>

<span data-ttu-id="8268d-180">Nesta etapa, você pode se conectar Olá PHP aplicativo toohello banco de dados MySQL que é criado no banco de dados do Azure para MySQL (visualização).</span><span class="sxs-lookup"><span data-stu-id="8268d-180">In this step, you connect hello PHP application toohello MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="8268d-181">Configurar conexão do banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="8268d-181">Configure hello database connection</span></span>

<span data-ttu-id="8268d-182">Na raiz do repositório hello, crie um _. env.production_ arquivo e cópia Olá variáveis a seguir para ele.</span><span class="sxs-lookup"><span data-stu-id="8268d-182">In hello repository root, create an _.env.production_ file and copy hello following variables into it.</span></span> <span data-ttu-id="8268d-183">Substitua o espaço reservado de saudação  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="8268d-183">Replace hello placeholder _&lt;mysql_server_name>_.</span></span>

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

<span data-ttu-id="8268d-184">Salve alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="8268d-184">Save hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="8268d-185">toosecure suas informações de conexão do MySQL, esse arquivo já foi excluídas do repositório do Git de saudação (consulte _. gitignore_ na raiz do repositório de saudação).</span><span class="sxs-lookup"><span data-stu-id="8268d-185">toosecure your MySQL connection information, this file is already excluded from hello Git repository (See _.gitignore_ in hello repository root).</span></span> <span data-ttu-id="8268d-186">Posteriormente, você aprenderá como variáveis de ambiente tooconfigure no serviço de aplicativo tooconnect tooyour banco de dados no banco de dados do Azure para MySQL (visualização).</span><span class="sxs-lookup"><span data-stu-id="8268d-186">Later, you learn how tooconfigure environment variables in App Service tooconnect tooyour database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="8268d-187">Com variáveis de ambiente, você não precisa Olá *.env* arquivo no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8268d-187">With environment variables, you don't need hello *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="8268d-188">Configurar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="8268d-188">Configure SSL certificate</span></span>

<span data-ttu-id="8268d-189">Por padrão, o Banco de Dados do Azure para MySQL impõe conexões SSL de clientes.</span><span class="sxs-lookup"><span data-stu-id="8268d-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="8268d-190">tooconnect tooyour banco de dados MySQL no Azure, você deve usar um _. PEM_ certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="8268d-190">tooconnect tooyour MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="8268d-191">Abra _config/database.php_ e adicione Olá _sslmode_ e _opções_ parâmetros muito`connections.mysql`, conforme mostrado na saudação de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="8268d-191">Open _config/database.php_ and add hello _sslmode_ and _options_ parameters too`connections.mysql`, as shown in hello following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="8268d-192">toolearn como toogenerate isso _certificate.pem_, consulte [conectividade de configurar SSL em seu aplicativo toosecurely tooAzure banco de dados de conexão para MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="8268d-192">toolearn how toogenerate this _certificate.pem_, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="8268d-193">caminho de saudação _/ssl/certificate.pem_ aponta existente tooan _certificate.pem_ arquivo no repositório do Git de saudação.</span><span class="sxs-lookup"><span data-stu-id="8268d-193">hello path _/ssl/certificate.pem_ points tooan existing _certificate.pem_ file in hello Git repository.</span></span> <span data-ttu-id="8268d-194">Esse arquivo é fornecido para conveniência neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="8268d-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="8268d-195">Como melhor prática, você não deve confirmar os certificados _.pem_ no controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="8268d-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-hello-application-locally"></a><span data-ttu-id="8268d-196">Testar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="8268d-196">Test hello application locally</span></span>

<span data-ttu-id="8268d-197">Executar migrações de banco de dados Laravel com _. env.production_ como hello tabelas de saudação do ambiente arquivo toocreate no banco de dados MySQL no banco de dados do Azure para MySQL (visualização).</span><span class="sxs-lookup"><span data-stu-id="8268d-197">Run Laravel database migrations with _.env.production_ as hello environment file toocreate hello tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="8268d-198">Lembre-se de que _. env.production_ tem o banco de dados do hello conexão informações tooyour MySQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="8268d-198">Remember that _.env.production_ has hello connection information tooyour MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="8268d-199">_.env.production_ ainda não tem uma chave de aplicativo válida.</span><span class="sxs-lookup"><span data-stu-id="8268d-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="8268d-200">Gere um novo para ele no hello terminal.</span><span class="sxs-lookup"><span data-stu-id="8268d-200">Generate a new one for it in hello terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="8268d-201">Execute o aplicativo de exemplo hello com _. env.production_ como arquivo de saudação do ambiente.</span><span class="sxs-lookup"><span data-stu-id="8268d-201">Run hello sample application with _.env.production_ as hello environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="8268d-202">Navegue muito`http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="8268d-202">Navigate too`http://localhost:8000`.</span></span> <span data-ttu-id="8268d-203">Se a página de saudação carregado sem erros, Olá aplicativo PHP está se conectando toohello banco de dados MySQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="8268d-203">If hello page loads without errors, hello PHP application is connecting toohello MySQL database in Azure.</span></span>

<span data-ttu-id="8268d-204">Adicione algumas tarefas na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="8268d-204">Add a few tasks in hello page.</span></span>

![PHP se conecta com êxito tooAzure banco de dados MySQL (visualização)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="8268d-206">Digite toostop PHP, `Ctrl + C` em Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="8268d-206">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="8268d-207">Confirmar as alterações</span><span class="sxs-lookup"><span data-stu-id="8268d-207">Commit your changes</span></span>

<span data-ttu-id="8268d-208">Execute seguinte Olá Git comandos toocommit suas alterações:</span><span class="sxs-lookup"><span data-stu-id="8268d-208">Run hello following Git commands toocommit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="8268d-209">Seu aplicativo estiver pronto toobe implantado.</span><span class="sxs-lookup"><span data-stu-id="8268d-209">Your app is ready toobe deployed.</span></span>

## <a name="deploy-tooazure"></a><span data-ttu-id="8268d-210">Implantar tooAzure</span><span class="sxs-lookup"><span data-stu-id="8268d-210">Deploy tooAzure</span></span>

<span data-ttu-id="8268d-211">Nesta etapa, você deve implantar Olá conectado MySQL PHP aplicativo tooAzure do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8268d-211">In this step, you deploy hello MySQL-connected PHP application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="8268d-212">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8268d-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="8268d-213">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="8268d-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a><span data-ttu-id="8268d-214">Versão do PHP Olá conjunto</span><span class="sxs-lookup"><span data-stu-id="8268d-214">Set hello PHP version</span></span>

<span data-ttu-id="8268d-215">Versão do PHP Olá conjunto que Olá aplicativo requer usando Olá [az webapp config conjunto](/cli/azure/webapp/config#set) comando.</span><span class="sxs-lookup"><span data-stu-id="8268d-215">Set hello PHP version that hello application requires by using hello [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="8268d-216">Olá comando a seguir define Olá PHP versão too_7.0_.</span><span class="sxs-lookup"><span data-stu-id="8268d-216">hello following command sets hello PHP version too_7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="8268d-217">Definir configurações de banco de dados</span><span class="sxs-lookup"><span data-stu-id="8268d-217">Configure database settings</span></span>

<span data-ttu-id="8268d-218">Como apontado anteriormente, você pode conectar o banco de dados do Azure MySQL tooyour usando variáveis de ambiente do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8268d-218">As pointed out previously, you can connect tooyour Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="8268d-219">No serviço de aplicativo, você definir variáveis de ambiente como _configurações do aplicativo_ usando Olá [az webapp configuração appsettings conjunto](/cli/azure/webapp/config/appsettings#set) comando.</span><span class="sxs-lookup"><span data-stu-id="8268d-219">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="8268d-220">Olá, comando a seguir define as configurações de aplicativo de Olá `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, e `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="8268d-220">hello following command configures hello app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="8268d-221">Substitua os espaços reservados de saudação  _&lt;appname >_ e  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="8268d-221">Replace hello placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="8268d-222">Você pode usar o hello PHP [getenv](http://www.php.net/manual/function.getenv.php) tooaccess método hello configurações.</span><span class="sxs-lookup"><span data-stu-id="8268d-222">You can use hello PHP [getenv](http://www.php.net/manual/function.getenv.php) method tooaccess hello settings.</span></span> <span data-ttu-id="8268d-223">Olá Laravel código usa um [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper Olá PHP `getenv`.</span><span class="sxs-lookup"><span data-stu-id="8268d-223">hello Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over hello PHP `getenv`.</span></span> <span data-ttu-id="8268d-224">Por exemplo, configuração de MySQL Olá em _config/database.php_ aparência Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="8268d-224">For example, hello MySQL configuration in _config/database.php_ looks like hello following code:</span></span>

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="8268d-225">Configurar variáveis de ambiente do Laravel</span><span class="sxs-lookup"><span data-stu-id="8268d-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="8268d-226">O Laravel precisa de uma chave de aplicativo no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8268d-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="8268d-227">É possível configurá-la com as configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8268d-227">You can configure it with app settings.</span></span>

<span data-ttu-id="8268d-228">Use `php artisan` toogenerate uma nova chave de aplicativo sem salvá-la too_.env_.</span><span class="sxs-lookup"><span data-stu-id="8268d-228">Use `php artisan` toogenerate a new application key without saving it too_.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="8268d-229">Definir chave de aplicativo hello em saudação do serviço de aplicativo aplicativo web usando Olá [az webapp configuração appsettings conjunto](/cli/azure/webapp/config/appsettings#set) comando.</span><span class="sxs-lookup"><span data-stu-id="8268d-229">Set hello application key in hello App Service web app by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="8268d-230">Substitua os espaços reservados de saudação  _&lt;appname >_ e  _&lt;outputofphpartisankey: gerar >_.</span><span class="sxs-lookup"><span data-stu-id="8268d-230">Replace hello placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="8268d-231">`APP_DEBUG="true"`informa Laravel tooreturn informações de depuração quando Olá implantado o aplicativo web encontram erros.</span><span class="sxs-lookup"><span data-stu-id="8268d-231">`APP_DEBUG="true"` tells Laravel tooreturn debugging information when hello deployed web app encounters errors.</span></span> <span data-ttu-id="8268d-232">Ao executar um aplicativo de produção, defina-o muito`false`, que é mais seguro.</span><span class="sxs-lookup"><span data-stu-id="8268d-232">When running a production application, set it too`false`, which is more secure.</span></span>

### <a name="set-hello-virtual-application-path"></a><span data-ttu-id="8268d-233">Definir caminho de aplicativo virtual Olá</span><span class="sxs-lookup"><span data-stu-id="8268d-233">Set hello virtual application path</span></span>

<span data-ttu-id="8268d-234">Definir caminho de aplicativo virtual Olá para o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="8268d-234">Set hello virtual application path for hello web app.</span></span> <span data-ttu-id="8268d-235">Esta etapa é necessária porque Olá [Laravel ciclo de vida do aplicativo](https://laravel.com/docs/5.4/lifecycle) começa em Olá _pública_ diretório em vez do diretório raiz do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8268d-235">This step is required because hello [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in hello _public_ directory instead of hello application's root directory.</span></span> <span data-ttu-id="8268d-236">Outras estruturas PHP cujo ciclo de vida iniciar no diretório raiz de saudação podem trabalhar sem configuração manual do caminho de aplicativo virtual hello.</span><span class="sxs-lookup"><span data-stu-id="8268d-236">Other PHP frameworks whose lifecycle start in hello root directory can work without manual configuration of hello virtual application path.</span></span>

<span data-ttu-id="8268d-237">Definir caminho de aplicativo virtual hello usando Olá [atualização de recurso az](/cli/azure/resource#update) comando.</span><span class="sxs-lookup"><span data-stu-id="8268d-237">Set hello virtual application path by using hello [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="8268d-238">Substituir saudação  _&lt;appname >_ espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="8268d-238">Replace hello _&lt;appname>_ placeholder.</span></span>

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

<span data-ttu-id="8268d-239">Por padrão, o serviço de aplicativo do Azure pontos de caminho de aplicativo virtual raiz hello (_/_) toohello diretório de raiz de saudação implantado arquivos de aplicativo (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="8268d-239">By default, Azure App Service points hello root virtual application path (_/_) toohello root directory of hello deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="8268d-240">Configurar um usuário de implantação</span><span class="sxs-lookup"><span data-stu-id="8268d-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="8268d-241">Configurar a implantação do git local</span><span class="sxs-lookup"><span data-stu-id="8268d-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a><span data-ttu-id="8268d-242">TooAzure de envio por push do Git</span><span class="sxs-lookup"><span data-stu-id="8268d-242">Push tooAzure from Git</span></span>

<span data-ttu-id="8268d-243">Adicione um repositório Git local do Azure tooyour remoto.</span><span class="sxs-lookup"><span data-stu-id="8268d-243">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="8268d-244">Enviar por push o aplicativo de PHP de hello toohello toodeploy remoto do Azure.</span><span class="sxs-lookup"><span data-stu-id="8268d-244">Push toohello Azure remote toodeploy hello PHP application.</span></span> <span data-ttu-id="8268d-245">Você será solicitado para senha Olá fornecidas anteriormente como parte da criação de saudação do usuário de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8268d-245">You are prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="8268d-246">Durante a implantação, o Serviço de Aplicativo do Azure comunica seu andamento com o Git.</span><span class="sxs-lookup"><span data-stu-id="8268d-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> <span data-ttu-id="8268d-247">Você pode perceber que o processo de implantação de saudação instala [criador](https://getcomposer.org/) pacotes final hello.</span><span class="sxs-lookup"><span data-stu-id="8268d-247">You may notice that hello deployment process installs [Composer](https://getcomposer.org/) packages at hello end.</span></span> <span data-ttu-id="8268d-248">Serviço de aplicativo não executa esses automações durante a implantação padrão, para que este repositório de exemplo tem três adicionais arquivos no seu tooenable de diretório raiz-lo:</span><span class="sxs-lookup"><span data-stu-id="8268d-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory tooenable it:</span></span>
>
> - <span data-ttu-id="8268d-249">`.deployment`-Este arquivo informa ao serviço de aplicativo toorun `bash deploy.sh` como script de implantação personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="8268d-249">`.deployment` - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
> - <span data-ttu-id="8268d-250">`deploy.sh`-Olá script de implantação personalizada.</span><span class="sxs-lookup"><span data-stu-id="8268d-250">`deploy.sh` - hello custom deployment script.</span></span> <span data-ttu-id="8268d-251">Se você revisar o arquivo hello, você verá que ele seja executado `php composer.phar install` depois `npm install`.</span><span class="sxs-lookup"><span data-stu-id="8268d-251">If you review hello file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="8268d-252">`composer.phar`-Gerenciador de pacote de criador de saudação.</span><span class="sxs-lookup"><span data-stu-id="8268d-252">`composer.phar` - hello Composer package manager.</span></span>
>
> <span data-ttu-id="8268d-253">Você pode usar essa abordagem tooadd tooApp de implantação com base em Git de tooyour qualquer etapa serviço.</span><span class="sxs-lookup"><span data-stu-id="8268d-253">You can use this approach tooadd any step tooyour Git-based deployment tooApp Service.</span></span> <span data-ttu-id="8268d-254">Para obter mais informações, consulte [Script de implantação personalizado](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span><span class="sxs-lookup"><span data-stu-id="8268d-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="8268d-255">Procurar o aplicativo web do Azure de toohello</span><span class="sxs-lookup"><span data-stu-id="8268d-255">Browse toohello Azure web app</span></span>

<span data-ttu-id="8268d-256">Procurar muito`http://<app_name>.azurewebsites.net` e adicionar a lista de toohello algumas tarefas.</span><span class="sxs-lookup"><span data-stu-id="8268d-256">Browse too`http://<app_name>.azurewebsites.net` and add a few tasks toohello list.</span></span>

![Aplicativo PHP em execução no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="8268d-258">Parabéns! Você está executando um aplicativo PHP controlado por dados no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="8268d-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="8268d-259">Atualizar o modelo localmente e reimplantar</span><span class="sxs-lookup"><span data-stu-id="8268d-259">Update model locally and redeploy</span></span>

<span data-ttu-id="8268d-260">Nesta etapa, você fizer uma alteração simples toohello `task` dados de modelo e Olá webapp e, em seguida, publicar Olá tooAzure de atualização.</span><span class="sxs-lookup"><span data-stu-id="8268d-260">In this step, you make a simple change toohello `task` data model and hello webapp, and then publish hello update tooAzure.</span></span>

<span data-ttu-id="8268d-261">Para o cenário de tarefas hello, você deve modificar um aplicativo hello para que você possa marcar uma tarefa como concluída.</span><span class="sxs-lookup"><span data-stu-id="8268d-261">For hello tasks scenario, you modify hello application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="8268d-262">Adicionar uma coluna</span><span class="sxs-lookup"><span data-stu-id="8268d-262">Add a column</span></span>

<span data-ttu-id="8268d-263">No hello terminal, navegue toohello raiz do repositório do Git de saudação.</span><span class="sxs-lookup"><span data-stu-id="8268d-263">In hello terminal, navigate toohello root of hello Git repository.</span></span>

<span data-ttu-id="8268d-264">Gerar uma nova migração de banco de dados para Olá `tasks` tabela:</span><span class="sxs-lookup"><span data-stu-id="8268d-264">Generate a new database migration for hello `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="8268d-265">Este comando mostra Olá o nome do arquivo de migração de saudação que é gerado.</span><span class="sxs-lookup"><span data-stu-id="8268d-265">This command shows you hello name of hello migration file that's generated.</span></span> <span data-ttu-id="8268d-266">Localize esse arquivo em _database/migrations_ e abra-o.</span><span class="sxs-lookup"><span data-stu-id="8268d-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="8268d-267">Substituir saudação `up` método com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="8268d-267">Replace hello `up` method with hello following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="8268d-268">Olá código acima adiciona uma coluna booleana Olá `tasks` tabela chamada `complete`.</span><span class="sxs-lookup"><span data-stu-id="8268d-268">hello preceding code adds a boolean column in hello `tasks` table called `complete`.</span></span>

<span data-ttu-id="8268d-269">Substituir saudação `down` método com hello código para a ação de reversão Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="8268d-269">Replace hello `down` method with hello following code for hello rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="8268d-270">No Olá terminal, execute Laravel banco de dados migrações toomake Olá de alterações no banco de dados local Olá.</span><span class="sxs-lookup"><span data-stu-id="8268d-270">In hello terminal, run Laravel database migrations toomake hello change in hello local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="8268d-271">Com base em Olá [convenção de nomenclatura Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), modelo Olá `Task` (consulte _app/Task.php_) mapeia toohello `tasks` tabela por padrão.</span><span class="sxs-lookup"><span data-stu-id="8268d-271">Based on hello [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (see _app/Task.php_) maps toohello `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="8268d-272">Atualizar a lógica do aplicativo</span><span class="sxs-lookup"><span data-stu-id="8268d-272">Update application logic</span></span>

<span data-ttu-id="8268d-273">Olá abrir *routes/web.php* arquivo.</span><span class="sxs-lookup"><span data-stu-id="8268d-273">Open hello *routes/web.php* file.</span></span> <span data-ttu-id="8268d-274">aplicativo Hello define sua rotas e a lógica de negócios aqui.</span><span class="sxs-lookup"><span data-stu-id="8268d-274">hello application defines its routes and business logic here.</span></span>

<span data-ttu-id="8268d-275">No final de saudação do arquivo hello, adicione uma rota com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="8268d-275">At hello end of hello file, add a route with hello following code:</span></span>

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

<span data-ttu-id="8268d-276">Olá código anterior faz com que um modelo de dados simples atualização toohello alternando o valor de saudação do `complete`.</span><span class="sxs-lookup"><span data-stu-id="8268d-276">hello preceding code makes a simple update toohello data model by toggling hello value of `complete`.</span></span>

### <a name="update-hello-view"></a><span data-ttu-id="8268d-277">Atualizar exibição Olá</span><span class="sxs-lookup"><span data-stu-id="8268d-277">Update hello view</span></span>

<span data-ttu-id="8268d-278">Olá abrir *resources/views/tasks.blade.php* arquivo.</span><span class="sxs-lookup"><span data-stu-id="8268d-278">Open hello *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="8268d-279">Localize Olá `<tr>` marca de abertura e substituí-lo:</span><span class="sxs-lookup"><span data-stu-id="8268d-279">Find hello `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="8268d-280">Olá anterior a cor de linha do código alterações Olá dependendo se a tarefa de saudação é concluída.</span><span class="sxs-lookup"><span data-stu-id="8268d-280">hello preceding code changes hello row color depending on whether hello task is complete.</span></span>

<span data-ttu-id="8268d-281">Na próxima linha de saudação, você tem Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="8268d-281">In hello next line, you have hello following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="8268d-282">Substitua linha inteira Olá Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="8268d-282">Replace hello entire line with hello following code:</span></span>

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

<span data-ttu-id="8268d-283">Olá código acima adiciona botão de envio de saudação que faz referência a rota Olá definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8268d-283">hello preceding code adds hello submit button that references hello route that you defined earlier.</span></span>

### <a name="test-hello-changes-locally"></a><span data-ttu-id="8268d-284">Teste as mudanças de saudação localmente</span><span class="sxs-lookup"><span data-stu-id="8268d-284">Test hello changes locally</span></span>

<span data-ttu-id="8268d-285">Diretório raiz de saudação do repositório do Git hello, execute o servidor de desenvolvimento hello.</span><span class="sxs-lookup"><span data-stu-id="8268d-285">From hello root directory of hello Git repository, run hello development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="8268d-286">Olá toosee alteração de status de tarefas, navegue até muito`http://localhost:8000` e Olá selecione caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="8268d-286">toosee hello task status change, navigate too`http://localhost:8000` and select hello checkbox.</span></span>

![Caixa de seleção adicionado tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="8268d-288">Digite toostop PHP, `Ctrl + C` em Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="8268d-288">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="publish-changes-tooazure"></a><span data-ttu-id="8268d-289">Publicar alterações tooAzure</span><span class="sxs-lookup"><span data-stu-id="8268d-289">Publish changes tooAzure</span></span>

<span data-ttu-id="8268d-290">Olá terminal, execute Laravel migrações de banco de dados com Olá Olá de toomake de cadeia de caracteres de conexão de produção alterar no hello banco de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="8268d-290">In hello terminal, run Laravel database migrations with hello production connection string toomake hello change in hello Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="8268d-291">Confirmar todas as alterações de saudação no Git e, em seguida, enviar por push Olá tooAzure de alterações de código.</span><span class="sxs-lookup"><span data-stu-id="8268d-291">Commit all hello changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="8268d-292">Uma vez Olá `git push` é concluída, navegue até toohello web do Azure aplicativo e teste Olá nova funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="8268d-292">Once hello `git push` is complete, navigate toohello Azure web app and test hello new functionality.</span></span>

![Alterações de modelo e o banco de dados publicado tooAzure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="8268d-294">Se você tiver adicionado todas as tarefas, eles são mantidos no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8268d-294">If you added any tasks, they are retained in hello database.</span></span> <span data-ttu-id="8268d-295">Esquema de atualizações de dados toohello deixar os dados existentes intactas.</span><span class="sxs-lookup"><span data-stu-id="8268d-295">Updates toohello data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="8268d-296">Logs de diagnóstico de fluxo</span><span class="sxs-lookup"><span data-stu-id="8268d-296">Stream diagnostic logs</span></span>

<span data-ttu-id="8268d-297">Enquanto Olá aplicativo PHP é executado no serviço de aplicativo do Azure, você pode obter Olá console logs canalizado tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="8268d-297">While hello PHP application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="8268d-298">Dessa forma, você pode obter Olá mensagens de diagnóstico mesmo toohelp depurar erros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8268d-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="8268d-299">log toostart streaming use Olá [final de log webapp az](/cli/azure/webapp/log#tail) comando.</span><span class="sxs-lookup"><span data-stu-id="8268d-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="8268d-300">Depois de iniciado o fluxo de log, atualização de aplicativo web do Azure Olá Olá navegador tooget parte do tráfego da web.</span><span class="sxs-lookup"><span data-stu-id="8268d-300">Once log streaming has started, refresh hello Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="8268d-301">Agora você pode ver o terminal do console logs toohello indicada.</span><span class="sxs-lookup"><span data-stu-id="8268d-301">You can now see console logs piped toohello terminal.</span></span> <span data-ttu-id="8268d-302">Se você não vir os logs do console imediatamente, verifique novamente após 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="8268d-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="8268d-303">log toostop streaming a qualquer momento, tipo `Ctrl` + `C`.</span><span class="sxs-lookup"><span data-stu-id="8268d-303">toostop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="8268d-304">Um aplicativo PHP pode usar o padrão de saudação [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span><span class="sxs-lookup"><span data-stu-id="8268d-304">A PHP application can use hello standard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span></span> <span data-ttu-id="8268d-305">aplicativo de exemplo Hello usa essa abordagem em _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="8268d-305">hello sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="8268d-306">Como uma estrutura de web, [Laravel usa Monolog](https://laravel.com/docs/5.4/errors) como provedor de log hello.</span><span class="sxs-lookup"><span data-stu-id="8268d-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as hello logging provider.</span></span> <span data-ttu-id="8268d-307">toosee como tooget Monolog toooutput mensagens toohello console, consulte [PHP: como toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span><span class="sxs-lookup"><span data-stu-id="8268d-307">toosee how tooget Monolog toooutput messages toohello console, see [PHP: How toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="8268d-308">Gerenciar o aplicativo da web do Azure de saudação</span><span class="sxs-lookup"><span data-stu-id="8268d-308">Manage hello Azure web app</span></span>

<span data-ttu-id="8268d-309">Vá toohello [portal do Azure](https://portal.azure.com) toomanage Olá web aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="8268d-309">Go toohello [Azure portal](https://portal.azure.com) toomanage hello web app you created.</span></span>

<span data-ttu-id="8268d-310">No menu à esquerda do hello, clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="8268d-310">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="8268d-312">A página Visão Geral do seu aplicativo Web é exibida.</span><span class="sxs-lookup"><span data-stu-id="8268d-312">You see your web app's Overview page.</span></span> <span data-ttu-id="8268d-313">Aqui, você pode executar tarefas básicas de gerenciamento, como parar, iniciar, reiniciar, procurar e excluir.</span><span class="sxs-lookup"><span data-stu-id="8268d-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="8268d-314">menu esquerdo Olá fornece páginas de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8268d-314">hello left menu provides pages for configuring your app.</span></span>

![Página Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="8268d-316">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8268d-316">Next steps</span></span>

<span data-ttu-id="8268d-317">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="8268d-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8268d-318">Criar um banco de dados MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="8268d-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="8268d-319">Conecte-se um tooMySQL do aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="8268d-319">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="8268d-320">Implantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="8268d-320">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="8268d-321">Atualizar o modelo de dados hello e reimplantar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="8268d-321">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="8268d-322">Transmitir logs de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="8268d-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="8268d-323">Gerenciar o aplicativo hello em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8268d-323">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="8268d-324">Avançar toolearn tutorial do próximo toohello como toomap um DNS personalizado nome tooa web app.</span><span class="sxs-lookup"><span data-stu-id="8268d-324">Advance toohello next tutorial toolearn how toomap a custom DNS name tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8268d-325">Mapear um tooAzure de nome DNS de personalizada existente aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="8268d-325">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
