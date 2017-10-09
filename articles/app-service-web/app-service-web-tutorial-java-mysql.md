---
title: aaaBuild um aplicativo web Java e MySQL no Azure
description: "Saiba como tooget um aplicativo Java que se conecta serviço de banco de dados MySQL Azure toohello trabalhando no serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="a79b5-103">Compilar um aplicativo Web Java e MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="a79b5-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="a79b5-104">Este tutorial mostra como toocreate um Java aplicativo no Azure da web e conectá-lo tooa banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="a79b5-104">This tutorial shows you how toocreate a Java web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="a79b5-105">Quando tiver terminado, você terá um aplicativo [Spring Boot](https://projects.spring.io/spring-boot/) armazenando dados no [Banco de dados do Azure para MySQL](https://docs.microsoft.com/azure/mysql/overview) em execução em [Aplicativos Web do Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="a79b5-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Aplicativo Java em execução no serviço de aplicativo do Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="a79b5-107">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="a79b5-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a79b5-108">Criar um banco de dados MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="a79b5-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="a79b5-109">Conectar a um banco de dados de toohello de aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="a79b5-109">Connect a sample app toohello database</span></span>
> * <span data-ttu-id="a79b5-110">Implantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="a79b5-110">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="a79b5-111">Atualize e reimplante o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="a79b5-111">Update and redeploy hello app</span></span>
> * <span data-ttu-id="a79b5-112">Transmitir logs de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="a79b5-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="a79b5-113">Monitorar o aplicativo hello Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a79b5-113">Monitor hello app in hello Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a79b5-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a79b5-114">Prerequisites</span></span>

1. [<span data-ttu-id="a79b5-115">Baixe e instale o Git</span><span class="sxs-lookup"><span data-stu-id="a79b5-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="a79b5-116">Baixe e instale Olá Java JDK de 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="a79b5-116">Download and install hello Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="a79b5-117">Baixe, instale e inicie o MySQL</span><span class="sxs-lookup"><span data-stu-id="a79b5-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a79b5-118">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a79b5-118">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a79b5-119">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a79b5-119">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a79b5-120">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a79b5-120">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="a79b5-121">Preparar o MySQL local</span><span class="sxs-lookup"><span data-stu-id="a79b5-121">Prepare local MySQL</span></span> 

<span data-ttu-id="a79b5-122">Nesta etapa, você criará um banco de dados em um servidor local do MySQL para uso no aplicativo de teste Olá localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a79b5-122">In this step, you create a database in a local MySQL server for use in testing hello app locally on your machine.</span></span>

### <a name="connect-toomysql-server"></a><span data-ttu-id="a79b5-123">Conecte-se o servidor tooMySQL</span><span class="sxs-lookup"><span data-stu-id="a79b5-123">Connect tooMySQL server</span></span>

<span data-ttu-id="a79b5-124">Em uma janela de terminal, conecte-se tooyour local MySQL server.</span><span class="sxs-lookup"><span data-stu-id="a79b5-124">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="a79b5-125">Você pode usar essa janela do terminal toorun todos os comandos de saudação neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a79b5-125">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="a79b5-126">Se você for solicitado a fornecer uma senha, digite a senha de saudação para Olá `root` conta.</span><span class="sxs-lookup"><span data-stu-id="a79b5-126">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="a79b5-127">Se você não lembrar a senha da conta raiz, consulte [MySQL: como tooReset Olá senha raiz](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="a79b5-127">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="a79b5-128">Se o comando for executado com êxito, o servidor MySQL já estará sendo executado.</span><span class="sxs-lookup"><span data-stu-id="a79b5-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="a79b5-129">Se não, certifique-se de que o servidor MySQL local é iniciado por seguir Olá [etapas de pós-instalação do MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="a79b5-129">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="a79b5-130">Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="a79b5-130">Create a database</span></span> 

<span data-ttu-id="a79b5-131">Em Olá `mysql` solicitar, crie um banco de dados e uma tabela para Olá itens pendentes.</span><span class="sxs-lookup"><span data-stu-id="a79b5-131">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="a79b5-132">Saia da conexão do servidor digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="a79b5-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a><span data-ttu-id="a79b5-133">Criar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="a79b5-133">Create and run hello sample app</span></span> 

<span data-ttu-id="a79b5-134">Nesta etapa, você clonar amostra de aplicativo de inicialização de Spring, configurá-lo toouse Olá MySQL banco de dados local e executá-lo em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a79b5-134">In this step, you clone sample Spring boot app, configure it toouse hello local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="a79b5-135">Exemplo de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="a79b5-135">Clone hello sample</span></span>

<span data-ttu-id="a79b5-136">Na janela do terminal hello, navegue tooa trabalhando repositório de exemplo hello diretório e clone.</span><span class="sxs-lookup"><span data-stu-id="a79b5-136">In hello terminal window, navigate tooa working directory and clone hello sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a><span data-ttu-id="a79b5-137">Configurar o banco de dados do hello aplicativo toouse Olá MySQL</span><span class="sxs-lookup"><span data-stu-id="a79b5-137">Configure hello app toouse hello MySQL database</span></span>

<span data-ttu-id="a79b5-138">Saudação de atualização `spring.datasource.password` e o valor no *spring-boot-mysql-todo/src/main/resources/application.properties* com hello a mesma senha de raiz usada prompt do tooopen Olá MySQL:</span><span class="sxs-lookup"><span data-stu-id="a79b5-138">Update hello `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with hello same root password used tooopen hello MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a><span data-ttu-id="a79b5-139">Compilar e executar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="a79b5-139">Build and run hello sample</span></span>

<span data-ttu-id="a79b5-140">Compilar e executar o exemplo hello usando Olá Maven wrapper incluído no repositório de saudação:</span><span class="sxs-lookup"><span data-stu-id="a79b5-140">Build and run hello sample using hello Maven wrapper included in hello repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="a79b5-141">Abra seu toosee toohttp://localhost:8080 de navegador no exemplo hello em ação.</span><span class="sxs-lookup"><span data-stu-id="a79b5-141">Open your browser toohttp://localhost:8080 toosee in hello sample in action.</span></span> <span data-ttu-id="a79b5-142">Como adicionar tarefas toohello lista, use Olá comandos do SQL a seguir no hello MySQL dados de saudação do prompt tooview armazenados no MySQL.</span><span class="sxs-lookup"><span data-stu-id="a79b5-142">As you add tasks toohello list,  use hello following SQL commands in hello MySQL prompt tooview hello data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="a79b5-143">Parar o aplicativo hello atingindo `Ctrl` + `C` em Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="a79b5-143">Stop hello application by hitting `Ctrl`+`C` in hello terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="a79b5-144">Criar um banco de dados MySQL do Azure</span><span class="sxs-lookup"><span data-stu-id="a79b5-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="a79b5-145">Nesta etapa, você criará uma [banco de dados do Azure para MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instância usando Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a79b5-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="a79b5-146">Configure toouse de aplicativo de exemplo hello esse banco de dados posteriormente no tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="a79b5-146">You configure hello sample application toouse this database later on in hello tutorial.</span></span>

<span data-ttu-id="a79b5-147">Olá use 2.0 do CLI do Azure em um terminal toocreate Olá recursos necessários toohost seu aplicativo Java no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a79b5-147">Use hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost your Java application in Azure appservice.</span></span> <span data-ttu-id="a79b5-148">Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="a79b5-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="a79b5-149">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a79b5-149">Create a resource group</span></span>

<span data-ttu-id="a79b5-150">Criar um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="a79b5-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="a79b5-151">Um grupo de recursos do Azure é um contêiner lógico no qual recursos relacionados do Azure, como aplicativos Web, bancos de dados e contas de armazenamento são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a79b5-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="a79b5-152">Olá exemplo a seguir cria um grupo de recursos na região do Norte da Europa hello:</span><span class="sxs-lookup"><span data-stu-id="a79b5-152">hello following example creates a resource group in hello North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="a79b5-153">valores possíveis do hello toosee você pode usar para `--location`, use Olá [locais de lista do serviço de aplicativo az](/cli/azure/appservice#list-locations) comando.</span><span class="sxs-lookup"><span data-stu-id="a79b5-153">toosee hello possible values you can use for `--location`, use hello [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="a79b5-154">Criar um servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="a79b5-154">Create a MySQL server</span></span>

<span data-ttu-id="a79b5-155">Criar um servidor de banco de dados do Azure para MySQL (visualização) com hello [az mysql server criar](/cli/azure/mysql/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="a79b5-155">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="a79b5-156">Substituir seu próprio nome do servidor MySQL exclusivo onde você pode ver Olá `<mysql_server_name>` espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="a79b5-156">Substitute your own unique MySQL server name where you see hello `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="a79b5-157">Esse nome faz parte do nome de host do servidor MySQL, `<mysql_server_name>.mysql.database.azure.com`, portanto, ele precisa toobe globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="a79b5-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs toobe globally unique.</span></span> <span data-ttu-id="a79b5-158">Substitua também `<admin_user>` e `<admin_password>` por seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="a79b5-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="a79b5-159">Quando o servidor do hello MySQL é criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a79b5-159">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="a79b5-160">Configurar o firewall do servidor</span><span class="sxs-lookup"><span data-stu-id="a79b5-160">Configure server firewall</span></span>

<span data-ttu-id="a79b5-161">Criar uma regra de firewall para o cliente do MySQL server tooallow conexões usando Olá [criar regra de firewall de servidor de mysql de az](/cli/azure/mysql/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="a79b5-161">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="a79b5-162">Atualmente, o Banco de Dados do Azure para MySQL (Visualização) não habilita automaticamente conexões de serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="a79b5-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="a79b5-163">Como os endereços IP no Azure são atribuídos dinamicamente, é melhor tooenable todos os endereços IP agora.</span><span class="sxs-lookup"><span data-stu-id="a79b5-163">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses for now.</span></span> <span data-ttu-id="a79b5-164">Como o serviço de saudação continua sua visualização, melhores métodos para proteger seu banco de dados serão habilitados.</span><span class="sxs-lookup"><span data-stu-id="a79b5-164">As hello service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-hello-azure-mysql-database"></a><span data-ttu-id="a79b5-165">Configurar o banco de dados do hello Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="a79b5-165">Configure hello Azure MySQL database</span></span>

<span data-ttu-id="a79b5-166">Na janela do terminal Olá em seu computador, conecte-se toohello MySQL server no Azure.</span><span class="sxs-lookup"><span data-stu-id="a79b5-166">In hello terminal window on your computer, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="a79b5-167">Usar valor Olá especificado anteriormente para `<admin_user>` e `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="a79b5-167">Use hello value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="a79b5-168">Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="a79b5-168">Create a database</span></span> 

<span data-ttu-id="a79b5-169">Em Olá `mysql` solicitar, crie um banco de dados e uma tabela para Olá itens pendentes.</span><span class="sxs-lookup"><span data-stu-id="a79b5-169">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="a79b5-170">Criar um usuário com permissões</span><span class="sxs-lookup"><span data-stu-id="a79b5-170">Create a user with permissions</span></span>

<span data-ttu-id="a79b5-171">Criar um usuário de banco de dados e dê a ele todos os privilégios em Olá `tododb` banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a79b5-171">Create a database user and give it all privileges in hello `tododb` database.</span></span> <span data-ttu-id="a79b5-172">Substitua os espaços reservados de saudação `<Javaapp_user>` e `<Javaapp_password>` com seu próprio nome exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a79b5-172">Replace hello placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

<span data-ttu-id="a79b5-173">Saia da conexão do servidor digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="a79b5-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a><span data-ttu-id="a79b5-174">Implantar Olá exemplo tooAzure do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="a79b5-174">Deploy hello sample tooAzure App Service</span></span>

<span data-ttu-id="a79b5-175">Criar um plano de serviço de aplicativo do Azure com hello **livre** preço usando Olá [criar plano de serviço de aplicativo az](/cli/azure/appservice/plan#create) comando CLI.</span><span class="sxs-lookup"><span data-stu-id="a79b5-175">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="a79b5-176">plano de serviço de aplicativo Hello define Olá recursos físicos usados toohost seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a79b5-176">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="a79b5-177">Todos os aplicativos atribuídos plano de serviço de aplicativo tooan compartilham esses recursos, permitindo que você toosave custo ao hospedar vários aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a79b5-177">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="a79b5-178">Quando o plano de saudação estiver pronto, Olá que CLI do Azure mostra semelhante saída toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a79b5-178">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="a79b5-179">Criar um aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="a79b5-179">Create an Azure Web app</span></span>

 <span data-ttu-id="a79b5-180">Saudação de uso [az webapp criar](/cli/azure/appservice/web#create) toocreate de comando CLI uma definição de aplicativo da web em Olá `myAppServicePlan` plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a79b5-180">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="a79b5-181">definição de aplicativo da web Hello fornece um URL tooaccess seu aplicativo com e configura toodeploy de várias opções tooAzure seu código.</span><span class="sxs-lookup"><span data-stu-id="a79b5-181">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="a79b5-182">Olá substituto `<app_name>` espaço reservado com seu próprio nome exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a79b5-182">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="a79b5-183">Esse nome exclusivo faz parte saudação padrão do nome de domínio de aplicativo da web hello, para que o nome do hello deve toobe exclusivo entre todos os aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="a79b5-183">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="a79b5-184">Você pode mapear um aplicativo web do domínio personalizado nome entrada toohello antes de você expor tooyour usuários.</span><span class="sxs-lookup"><span data-stu-id="a79b5-184">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="a79b5-185">Quando a definição de aplicativo da web hello estiver pronta, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a79b5-185">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="a79b5-186">Configurar o Java</span><span class="sxs-lookup"><span data-stu-id="a79b5-186">Configure Java</span></span> 

<span data-ttu-id="a79b5-187">Definir a configuração de tempo de execução do Java Olá precisa de seu aplicativo com hello [atualização da configuração az serviço de aplicativo web](/cli/azure/appservice/web/config#update) comando.</span><span class="sxs-lookup"><span data-stu-id="a79b5-187">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="a79b5-188">Olá comando a seguir configura Olá web aplicativo toorun em um recente Java 8 JDK e [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="a79b5-188">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a><span data-ttu-id="a79b5-189">Configurar banco de dados do hello aplicativo toouse Olá SQL Azure</span><span class="sxs-lookup"><span data-stu-id="a79b5-189">Configure hello app toouse hello Azure SQL database</span></span>

<span data-ttu-id="a79b5-190">Antes de executar o aplicativo de exemplo hello, defina configurações de aplicativo no Olá web aplicativo toouse hello Azure banco de dados MySQL criado no Azure.</span><span class="sxs-lookup"><span data-stu-id="a79b5-190">Before running hello sample app, set application settings on hello web app toouse hello Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="a79b5-191">Essas propriedades são expostos toohello aplicativo de web como variáveis de ambiente e substituem os valores hello definidos em application.properties hello dentro Olá web empacotado aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a79b5-191">These properties are exposed toohello web application as environment variables and override hello values set in hello application.properties inside hello packaged web app.</span></span> 

<span data-ttu-id="a79b5-192">Definir configurações de aplicativo usando [az webapp configuração appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) em Olá CLI:</span><span class="sxs-lookup"><span data-stu-id="a79b5-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in hello CLI:</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="a79b5-193">Obter credenciais de implantação FTP</span><span class="sxs-lookup"><span data-stu-id="a79b5-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="a79b5-194">Você pode implantar o serviço de aplicativo de tooAzure aplicativo de várias maneiras, incluindo o FTP, local Git, GitHub, Visual Studio Team Services e BitBucket.</span><span class="sxs-lookup"><span data-stu-id="a79b5-194">You can deploy your application tooAzure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="a79b5-195">Por exemplo, Olá de toodeploy FTP. Arquivo WAR criado anteriormente na tooAzure sua máquina local do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a79b5-195">For this example, FTP toodeploy hello .WAR file built previously on your local machine tooAzure App Service.</span></span>

<span data-ttu-id="a79b5-196">toodetermine quais credenciais toopass ao longo de um toohello comando ftp aplicativo Web, Use [az serviço de aplicativo web implantação lista publicação perfis-](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) comando:</span><span class="sxs-lookup"><span data-stu-id="a79b5-196">toodetermine what credentials toopass along in an ftp command toohello Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a><span data-ttu-id="a79b5-197">Carregar o aplicativo hello usando FTP</span><span class="sxs-lookup"><span data-stu-id="a79b5-197">Upload hello app using FTP</span></span>

<span data-ttu-id="a79b5-198">Use a saudação de toodeploy de ferramenta FTP favorita. Toohello de arquivo WAR */site/wwwroot/webapps* pasta no endereço do servidor de saudação obtido Olá `URL` campo no comando anterior hello.</span><span class="sxs-lookup"><span data-stu-id="a79b5-198">Use your favorite FTP tool toodeploy hello .WAR file toohello */site/wwwroot/webapps* folder on hello server address taken from hello `URL` field in hello previous command.</span></span> <span data-ttu-id="a79b5-199">Remover o diretório de aplicativo padrão (raiz) existente hello e substitua Olá existente ROOT.war com hello. Arquivo WAR incorporado Olá anteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="a79b5-199">Remove hello existing default (ROOT) application directory and replace hello existing ROOT.war with hello .WAR file built in hello earlier in hello tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a><span data-ttu-id="a79b5-200">Aplicativo de web de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="a79b5-200">Test hello web app</span></span>

<span data-ttu-id="a79b5-201">Procurar muito`http://<app_name>.azurewebsites.net/` e adicionar a lista de toohello algumas tarefas.</span><span class="sxs-lookup"><span data-stu-id="a79b5-201">Browse too`http://<app_name>.azurewebsites.net/` and add a few tasks toohello list.</span></span> 

![Aplicativo Java em execução no serviço de aplicativo do Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="a79b5-203">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="a79b5-203">**Congratulations!**</span></span> <span data-ttu-id="a79b5-204">Você está executando um aplicativo Java controlado por dados no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a79b5-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="a79b5-205">Aplicativo de saudação de atualização e reimplantação</span><span class="sxs-lookup"><span data-stu-id="a79b5-205">Update hello app and redeploy</span></span>

<span data-ttu-id="a79b5-206">Atualize Olá aplicativo tooinclude uma coluna adicional na lista de tarefas Olá para o item de saudação dia foi criado.</span><span class="sxs-lookup"><span data-stu-id="a79b5-206">Update hello application tooinclude an additional column in hello todo list for what day hello item was created.</span></span> <span data-ttu-id="a79b5-207">Inicialização de Spring trata atualizar esquema de banco de dados de saudação para você como Olá alterações do modelo de dados sem alterar os registros do banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="a79b5-207">Spring Boot handles updating hello database schema for you as hello data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="a79b5-208">Em seu sistema local, abra o *src/main/java/com/example/fabrikam/TodoItem.java* e adicione a seguinte Olá importa toohello classe:</span><span class="sxs-lookup"><span data-stu-id="a79b5-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add hello following imports toohello class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="a79b5-209">Adicionar um `String` propriedade `timeCreated` muito*src/main/java/com/example/fabrikam/TodoItem.java*, inicializá-la com um carimbo de hora na criação do objeto.</span><span class="sxs-lookup"><span data-stu-id="a79b5-209">Add a `String` property `timeCreated` too*src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="a79b5-210">Adicionar getters/setters Olá novo `timeCreated` propriedade enquanto você estiver editando o arquivo.</span><span class="sxs-lookup"><span data-stu-id="a79b5-210">Add getters/setters for hello new `timeCreated` property while you are editing this file.</span></span>

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. <span data-ttu-id="a79b5-211">Atualização *src/main/java/com/example/fabrikam/TodoDemoController.java* com uma linha no hello `updateTodo` método tooset Olá timestamp:</span><span class="sxs-lookup"><span data-stu-id="a79b5-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in hello `updateTodo` method tooset hello timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="a79b5-212">Adicione suporte para o novo campo de saudação no modelo de Thymeleaf hello.</span><span class="sxs-lookup"><span data-stu-id="a79b5-212">Add support for hello new field in hello Thymeleaf template.</span></span> <span data-ttu-id="a79b5-213">Atualização *src/main/resources/templates/index.html* com um novo cabeçalho de tabela para Olá timestamp e um novo valor de saudação toodisplay do campo de carimbo de hora de saudação em cada linha de dados de tabela.</span><span class="sxs-lookup"><span data-stu-id="a79b5-213">Update *src/main/resources/templates/index.html* with a new table header for hello timestamp, and a new field toodisplay hello value of hello timestamp in each table data row.</span></span>

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. <span data-ttu-id="a79b5-214">Recompile o aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="a79b5-214">Rebuild hello application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="a79b5-215">Saudação FTP atualizada. WAR como antes, removendo Olá existente *site/wwwroot/webapps/ROOT* diretório e *ROOT.war*, e em seguida, carregar Olá atualizado. Arquivo WAR como ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="a79b5-215">FTP hello updated .WAR as before, removing hello existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading hello updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="a79b5-216">Quando você atualiza o aplicativo hello, um **tempo criado** coluna agora está visível.</span><span class="sxs-lookup"><span data-stu-id="a79b5-216">When you refresh hello app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="a79b5-217">Quando você adiciona uma nova tarefa, o aplicativo hello preencherá automaticamente Olá timestamp.</span><span class="sxs-lookup"><span data-stu-id="a79b5-217">When you add a new task, hello app will populate hello timestamp automatically.</span></span> <span data-ttu-id="a79b5-218">As tarefas existentes permanecem inalterada e trabalhar com o aplicativo hello, mesmo que Olá subjacente do modelo de dados foi alterado.</span><span class="sxs-lookup"><span data-stu-id="a79b5-218">Your existing tasks remain unchanged and work with hello app even though hello underlying data model has changed.</span></span> 

![Aplicativo Java atualizado com uma nova coluna](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="a79b5-220">Logs de diagnóstico de fluxo</span><span class="sxs-lookup"><span data-stu-id="a79b5-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="a79b5-221">Enquanto seu aplicativo Java é executado no serviço de aplicativo do Azure, você pode obter console Olá logs diretamente conectados tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="a79b5-221">While your Java application runs in Azure App Service, you can get hello console logs piped directly tooyour terminal.</span></span> <span data-ttu-id="a79b5-222">Dessa forma, você pode obter Olá mensagens de diagnóstico mesmo toohelp depurar erros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a79b5-222">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="a79b5-223">log toostart streaming use Olá [final de log webapp az](/cli/azure/appservice/web/log#tail) comando.</span><span class="sxs-lookup"><span data-stu-id="a79b5-223">toostart log streaming, use hello [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="a79b5-224">Gerenciar seu aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="a79b5-224">Manage your Azure web app</span></span>

<span data-ttu-id="a79b5-225">Vá toohello toosee portal do Azure Olá web aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="a79b5-225">Go toohello Azure portal toosee hello web app you created.</span></span>

<span data-ttu-id="a79b5-226">toodo isso, entrar muito[https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a79b5-226">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="a79b5-227">No menu à esquerda do hello, clique em **do serviço de aplicativo**, clique em nome de saudação do seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a79b5-227">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="a79b5-229">Por padrão, a folha do seu aplicativo web mostra Olá **visão geral** página.</span><span class="sxs-lookup"><span data-stu-id="a79b5-229">By default, your web app's blade shows hello **Overview** page.</span></span> <span data-ttu-id="a79b5-230">Esta página fornece uma visão de como está seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a79b5-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="a79b5-231">Aqui, você também pode executar tarefas de gerenciamento como parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="a79b5-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="a79b5-232">guias de Olá no lado esquerdo de saudação da folha de saudação mostram páginas de configuração diferentes de hello, que você pode abrir.</span><span class="sxs-lookup"><span data-stu-id="a79b5-232">hello tabs on hello left side of hello blade show hello different configuration pages you can open.</span></span>

![Folha Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="a79b5-234">Essas guias na folha de saudação mostram Olá vários recursos excelentes, você pode adicionar o aplicativo da web de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a79b5-234">These tabs in hello blade show hello many great features you can add tooyour web app.</span></span> <span data-ttu-id="a79b5-235">Olá lista a seguir fornece apenas algumas possibilidades de saudação:</span><span class="sxs-lookup"><span data-stu-id="a79b5-235">hello following list gives you just a few of hello possibilities:</span></span>
* <span data-ttu-id="a79b5-236">mapear um nome DNS personalizado</span><span class="sxs-lookup"><span data-stu-id="a79b5-236">Map a custom DNS name</span></span>
* <span data-ttu-id="a79b5-237">associar um certificado SSL personalizado</span><span class="sxs-lookup"><span data-stu-id="a79b5-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="a79b5-238">configurar uma implantação contínua</span><span class="sxs-lookup"><span data-stu-id="a79b5-238">Configure continuous deployment</span></span>
* <span data-ttu-id="a79b5-239">Escalar vertical e horizontalmente</span><span class="sxs-lookup"><span data-stu-id="a79b5-239">Scale up and out</span></span>
* <span data-ttu-id="a79b5-240">adicionar a autenticação do usuário</span><span class="sxs-lookup"><span data-stu-id="a79b5-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="a79b5-241">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="a79b5-241">Clean up resources</span></span>

<span data-ttu-id="a79b5-242">Se você não precisa desses recursos para outro tutorial (consulte [próximas etapas](#next)), você pode excluí-los executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a79b5-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running hello following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="a79b5-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a79b5-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a79b5-244">Criar um banco de dados MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="a79b5-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="a79b5-245">Conecte-se um toohello de aplicativo de Java de exemplo MySQL</span><span class="sxs-lookup"><span data-stu-id="a79b5-245">Connect a sample Java app toohello MySQL</span></span>
> * <span data-ttu-id="a79b5-246">Implantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="a79b5-246">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="a79b5-247">Atualize e reimplante o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="a79b5-247">Update and redeploy hello app</span></span>
> * <span data-ttu-id="a79b5-248">Transmitir logs de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="a79b5-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="a79b5-249">Gerenciar o aplicativo hello em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a79b5-249">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="a79b5-250">Avançar toolearn tutorial do próximo toohello como toomap um DNS personalizado nome toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a79b5-250">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="a79b5-251">Mapear um tooAzure de nome DNS de personalizada existente aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="a79b5-251">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
