---
title: Compilar um aplicativo Web Java e MySQL no Azure
description: "Saiba como fazer com que um aplicativo Java que se conecta ao serviço de banco de dados MySQL do Azure funcione no serviço de aplicativo do Azure."
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
ms.openlocfilehash: eb2d59939c4e4486bb14bb143a4a18f9bc1478e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="309ef-103">Compilar um aplicativo Web Java e MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="309ef-104">Este tutorial mostra como criar um aplicativo Web Java no Azure e conectá-lo a um banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="309ef-104">This tutorial shows you how to create a Java web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="309ef-105">Quando tiver terminado, você terá um aplicativo [Spring Boot](https://projects.spring.io/spring-boot/) armazenando dados no [Banco de dados do Azure para MySQL](https://docs.microsoft.com/azure/mysql/overview) em execução em [Aplicativos Web do Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="309ef-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Aplicativo Java em execução no serviço de aplicativo do Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="309ef-107">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="309ef-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="309ef-108">Criar um banco de dados MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="309ef-109">Conectar um aplicativo de exemplo para o banco de dados</span><span class="sxs-lookup"><span data-stu-id="309ef-109">Connect a sample app to the database</span></span>
> * <span data-ttu-id="309ef-110">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-110">Deploy the app to Azure</span></span>
> * <span data-ttu-id="309ef-111">Atualizar o aplicativo e reimplantar</span><span class="sxs-lookup"><span data-stu-id="309ef-111">Update and redeploy the app</span></span>
> * <span data-ttu-id="309ef-112">Transmitir logs de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="309ef-113">Monitorar o aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-113">Monitor the app in the Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="309ef-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="309ef-114">Prerequisites</span></span>

1. [<span data-ttu-id="309ef-115">Baixe e instale o Git</span><span class="sxs-lookup"><span data-stu-id="309ef-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="309ef-116">Baixe e instale o Java JDK 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="309ef-116">Download and install the Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="309ef-117">Baixe, instale e inicie o MySQL</span><span class="sxs-lookup"><span data-stu-id="309ef-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="309ef-118">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="309ef-118">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="309ef-119">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="309ef-119">Run `az --version` to find the version.</span></span> <span data-ttu-id="309ef-120">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="309ef-120">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="309ef-121">Preparar o MySQL local</span><span class="sxs-lookup"><span data-stu-id="309ef-121">Prepare local MySQL</span></span> 

<span data-ttu-id="309ef-122">Nesta etapa, você cria um banco de dados em seu servidor MySQL local para uso ao testar o aplicativo localmente em seu computador.</span><span class="sxs-lookup"><span data-stu-id="309ef-122">In this step, you create a database in a local MySQL server for use in testing the app locally on your machine.</span></span>

### <a name="connect-to-mysql-server"></a><span data-ttu-id="309ef-123">Conectar ao servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="309ef-123">Connect to MySQL server</span></span>

<span data-ttu-id="309ef-124">Em uma janela de terminal, conecte-se ao servidor MySQL local.</span><span class="sxs-lookup"><span data-stu-id="309ef-124">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="309ef-125">Você pode usar essa janela do terminal para executar todos os comandos deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="309ef-125">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="309ef-126">Se for solicitada uma senha, insira a senha da conta `root`.</span><span class="sxs-lookup"><span data-stu-id="309ef-126">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="309ef-127">Caso não se lembre da senha de sua conta raiz, consulte [MySQL: como redefinir a senha raiz](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="309ef-127">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="309ef-128">Se o comando for executado com êxito, o servidor MySQL já estará sendo executado.</span><span class="sxs-lookup"><span data-stu-id="309ef-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="309ef-129">Caso contrário, veja se o servidor MySQL local foi iniciado seguindo as [Etapas pós-instalação do MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="309ef-129">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="309ef-130">Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="309ef-130">Create a database</span></span> 

<span data-ttu-id="309ef-131">No prompt `mysql`, crie um banco de dados e uma tabela para os itens de tarefa.</span><span class="sxs-lookup"><span data-stu-id="309ef-131">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="309ef-132">Saia da conexão do servidor digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="309ef-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-the-sample-app"></a><span data-ttu-id="309ef-133">Criar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="309ef-133">Create and run the sample app</span></span> 

<span data-ttu-id="309ef-134">Nesta etapa, você clona o aplicativo de inicialização de exemplo Primavera, configura-o para usar o banco de dados MySQL local e executa-o em seu computador.</span><span class="sxs-lookup"><span data-stu-id="309ef-134">In this step, you clone sample Spring boot app, configure it to use the local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="309ef-135">Clonar o exemplo</span><span class="sxs-lookup"><span data-stu-id="309ef-135">Clone the sample</span></span>

<span data-ttu-id="309ef-136">Na janela do terminal, navegue até um diretório de trabalho e clone o repositório de exemplo.</span><span class="sxs-lookup"><span data-stu-id="309ef-136">In the terminal window, navigate to a working directory and clone the sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-the-app-to-use-the-mysql-database"></a><span data-ttu-id="309ef-137">Configurar o aplicativo para usar o banco de dados MySQL</span><span class="sxs-lookup"><span data-stu-id="309ef-137">Configure the app to use the MySQL database</span></span>

<span data-ttu-id="309ef-138">Atualização de `spring.datasource.password` e o valor em *spring-boot-mysql-todo/src/main/resources/application.properties* com a mesma senha raiz usada para abrir o prompt do MySQL:</span><span class="sxs-lookup"><span data-stu-id="309ef-138">Update the `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with the same root password used to open the MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-the-sample"></a><span data-ttu-id="309ef-139">Criar e executar a amostra</span><span class="sxs-lookup"><span data-stu-id="309ef-139">Build and run the sample</span></span>

<span data-ttu-id="309ef-140">Compilar e executar o exemplo usando o invólucro no repositório do Maven:</span><span class="sxs-lookup"><span data-stu-id="309ef-140">Build and run the sample using the Maven wrapper included in the repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="309ef-141">Abra seu navegador para http://localhost:8080 para ver o exemplo em ação.</span><span class="sxs-lookup"><span data-stu-id="309ef-141">Open your browser to http://localhost:8080 to see in the sample in action.</span></span> <span data-ttu-id="309ef-142">Conforme você adiciona tarefas à lista, use os comandos SQL a seguir no prompt do MySQL para exibir os dados armazenados no MySQL.</span><span class="sxs-lookup"><span data-stu-id="309ef-142">As you add tasks to the list,  use the following SQL commands in the MySQL prompt to view the data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="309ef-143">Interrompa o aplicativo pressionando `Ctrl`+`C` no terminal.</span><span class="sxs-lookup"><span data-stu-id="309ef-143">Stop the application by hitting `Ctrl`+`C` in the terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="309ef-144">Criar um banco de dados MySQL do Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="309ef-145">Nesta etapa, você criará uma instância [Banco de dados para MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) usando a [CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="309ef-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="309ef-146">Configure o aplicativo de exemplo para usar este banco de dados posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="309ef-146">You configure the sample application to use this database later on in the tutorial.</span></span>

<span data-ttu-id="309ef-147">Use a CLI do Azure 2.0 em uma janela de terminal para criar os recursos necessários para hospedar seu aplicativo Java no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="309ef-147">Use the Azure CLI 2.0 in a terminal window to create the resources needed to host your Java application in Azure appservice.</span></span> <span data-ttu-id="309ef-148">Faça logon na sua assinatura do Azure com o comando [az login](/cli/azure/#login) e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="309ef-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="309ef-149">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="309ef-149">Create a resource group</span></span>

<span data-ttu-id="309ef-150">Crie um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) com o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="309ef-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="309ef-151">Um grupo de recursos do Azure é um contêiner lógico no qual recursos relacionados do Azure, como aplicativos Web, bancos de dados e contas de armazenamento são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="309ef-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="309ef-152">O exemplo a seguir cria um grupo de recursos na região da Europa Setentrional:</span><span class="sxs-lookup"><span data-stu-id="309ef-152">The following example creates a resource group in the North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="309ef-153">Para ver os possíveis valores que podem ser usados para `--location`, use o comando [az appservice list-locations](/cli/azure/appservice#list-locations).</span><span class="sxs-lookup"><span data-stu-id="309ef-153">To see the possible values you can use for `--location`, use the [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="309ef-154">Criar um servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="309ef-154">Create a MySQL server</span></span>

<span data-ttu-id="309ef-155">Crie um servidor no Banco de Dados do Azure para MySQL (versão prévia) com o comando [az mysql server create](/cli/azure/mysql/server#create).</span><span class="sxs-lookup"><span data-stu-id="309ef-155">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="309ef-156">Substitua pelo nome do servidor MySQL exclusivo onde vir o espaço reservado `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="309ef-156">Substitute your own unique MySQL server name where you see the `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="309ef-157">Esse nome é parte do nome de host do servidor MySQL, `<mysql_server_name>.mysql.database.azure.com`, portanto, ele precisa ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="309ef-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs to be globally unique.</span></span> <span data-ttu-id="309ef-158">Substitua também `<admin_user>` e `<admin_password>` por seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="309ef-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="309ef-159">Quando o servidor MySQL for criado, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="309ef-159">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="309ef-160">Configurar o firewall do servidor</span><span class="sxs-lookup"><span data-stu-id="309ef-160">Configure server firewall</span></span>

<span data-ttu-id="309ef-161">Crie uma regra de firewall para o servidor MySQL para permitir conexões de cliente usando o comando [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="309ef-161">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="309ef-162">Atualmente, o Banco de Dados do Azure para MySQL (Visualização) não habilita automaticamente conexões de serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="309ef-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="309ef-163">Como os endereços IP no Azure são atribuídos dinamicamente, é melhor habilitar todos os endereços IP por enquanto.</span><span class="sxs-lookup"><span data-stu-id="309ef-163">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses for now.</span></span> <span data-ttu-id="309ef-164">Como o serviço continua na fase de visualização, melhores métodos para proteger seu banco de dados serão habilitados.</span><span class="sxs-lookup"><span data-stu-id="309ef-164">As the service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-the-azure-mysql-database"></a><span data-ttu-id="309ef-165">Configurar o banco de dados MySQL do Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-165">Configure the Azure MySQL database</span></span>

<span data-ttu-id="309ef-166">Na janela do terminal em seu computador, conecte-se ao servidor MySQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="309ef-166">In the terminal window on your computer, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="309ef-167">Use o valor especificado anteriormente para `<admin_user>` e `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="309ef-167">Use the value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="309ef-168">Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="309ef-168">Create a database</span></span> 

<span data-ttu-id="309ef-169">No prompt `mysql`, crie um banco de dados e uma tabela para os itens de tarefa.</span><span class="sxs-lookup"><span data-stu-id="309ef-169">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="309ef-170">Criar um usuário com permissões</span><span class="sxs-lookup"><span data-stu-id="309ef-170">Create a user with permissions</span></span>

<span data-ttu-id="309ef-171">Crie um usuário do banco de dados e dê a ele todos os privilégios no banco de dados `tododb`.</span><span class="sxs-lookup"><span data-stu-id="309ef-171">Create a database user and give it all privileges in the `tododb` database.</span></span> <span data-ttu-id="309ef-172">Substitua os espaços reservados `<Javaapp_user>` e `<Javaapp_password>` por seu próprio nome exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="309ef-172">Replace the placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* TO '<Javaapp_user>';
```

<span data-ttu-id="309ef-173">Saia da conexão do servidor digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="309ef-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-the-sample-to-azure-app-service"></a><span data-ttu-id="309ef-174">Implantar o exemplo no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-174">Deploy the sample to Azure App Service</span></span>

<span data-ttu-id="309ef-175">Crie um plano do Serviço de Aplicativo do Azure com o tipo de preço **GRÁTIS** usando a CLI de comando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="309ef-175">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="309ef-176">O plano do serviço de aplicativo define os recursos físicos usados para hospedar seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="309ef-176">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="309ef-177">Todos os aplicativos atribuídos a um plano do serviço de aplicativo compartilham esses recursos, permitindo que você economize hospedando vários aplicativos.</span><span class="sxs-lookup"><span data-stu-id="309ef-177">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="309ef-178">Quando o plano estiver pronto, a CLI do Azure mostra uma saída semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="309ef-178">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="309ef-179">Criar um aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-179">Create an Azure Web app</span></span>

 <span data-ttu-id="309ef-180">Use a CLI de comando [az webapp create](/cli/azure/appservice/web#create) para criar uma definição de aplicativo Web no `myAppServicePlan` Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="309ef-180">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="309ef-181">A definição de aplicativo Web fornece uma URL para acessar seu aplicativo e define várias opções para implantar seu código no Azure.</span><span class="sxs-lookup"><span data-stu-id="309ef-181">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="309ef-182">Substitua o espaço reservado `<app_name>` por seu próprio nome exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="309ef-182">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="309ef-183">Esse nome exclusivo é parte do nome de domínio padrão para o aplicativo Web, portanto, o nome precisa ser exclusivo entre todos os aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="309ef-183">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="309ef-184">Você poderá mapear uma entrada de nome de domínio personalizada para o aplicativo Web antes de expor para seus usuários.</span><span class="sxs-lookup"><span data-stu-id="309ef-184">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="309ef-185">Quando a definição do aplicativo Web tiver pronta, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="309ef-185">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="309ef-186">Configurar o Java</span><span class="sxs-lookup"><span data-stu-id="309ef-186">Configure Java</span></span> 

<span data-ttu-id="309ef-187">Definir a configuração de tempo de execução Java que seu aplicativo precisa com o comando [az appservice web config update](/cli/azure/appservice/web/config#update).</span><span class="sxs-lookup"><span data-stu-id="309ef-187">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="309ef-188">O comando a seguir configura o aplicativo Web para ser executado em um JDK 8 Java recente e [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="309ef-188">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-the-app-to-use-the-azure-sql-database"></a><span data-ttu-id="309ef-189">Configurar o aplicativo para usar o banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-189">Configure the app to use the Azure SQL database</span></span>

<span data-ttu-id="309ef-190">Antes de executar o aplicativo de exemplo, defina as configurações do aplicativo no aplicativo Web para usar o banco de dados MySQL do Azure criado no Azure.</span><span class="sxs-lookup"><span data-stu-id="309ef-190">Before running the sample app, set application settings on the web app to use the Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="309ef-191">Essas propriedades são expostas ao aplicativo Web como variáveis de ambiente e substituem os valores definidos em application.properties dentro do aplicativo Web empacotado.</span><span class="sxs-lookup"><span data-stu-id="309ef-191">These properties are exposed to the web application as environment variables and override the values set in the application.properties inside the packaged web app.</span></span> 

<span data-ttu-id="309ef-192">Definir configurações de aplicativo usando [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) na CLI:</span><span class="sxs-lookup"><span data-stu-id="309ef-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in the CLI:</span></span>

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

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="309ef-193">Obter credenciais de implantação FTP</span><span class="sxs-lookup"><span data-stu-id="309ef-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="309ef-194">É possível implantar seu aplicativo no serviço de aplicativo do Azure de várias maneiras, incluindo FTP, Git local, GitHub, Visual Studio Team Services e BitBucket.</span><span class="sxs-lookup"><span data-stu-id="309ef-194">You can deploy your application to Azure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="309ef-195">Para este exemplo, o FTP para implantar o arquivo .WAR criado anteriormente no computador local para o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="309ef-195">For this example, FTP to deploy the .WAR file built previously on your local machine to Azure App Service.</span></span>

<span data-ttu-id="309ef-196">Para determinar as credenciais a serem passadas em um comando ftp para o aplicativo Web, use o comando [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles):</span><span class="sxs-lookup"><span data-stu-id="309ef-196">To determine what credentials to pass along in an ftp command to the Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

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

### <a name="upload-the-app-using-ftp"></a><span data-ttu-id="309ef-197">Carregar o aplicativo usando FTP</span><span class="sxs-lookup"><span data-stu-id="309ef-197">Upload the app using FTP</span></span>

<span data-ttu-id="309ef-198">Use sua ferramenta favorita de FTP para implantar o arquivo .WAR para a pasta */site/wwwroot/webapps* no endereço de servidor obtido do campo `URL` no comando anterior.</span><span class="sxs-lookup"><span data-stu-id="309ef-198">Use your favorite FTP tool to deploy the .WAR file to the */site/wwwroot/webapps* folder on the server address taken from the `URL` field in the previous command.</span></span> <span data-ttu-id="309ef-199">Remova o diretório de aplicativo padrão (RAIZ) existente e substitua o ROOT.war existente com o arquivo .WAR incorporado no tutorial anterior.</span><span class="sxs-lookup"><span data-stu-id="309ef-199">Remove the existing default (ROOT) application directory and replace the existing ROOT.war with the .WAR file built in the earlier in the tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected to waws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-the-web-app"></a><span data-ttu-id="309ef-200">Testar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="309ef-200">Test the web app</span></span>

<span data-ttu-id="309ef-201">Navegue até `http://<app_name>.azurewebsites.net/` e adicione algumas tarefas à lista.</span><span class="sxs-lookup"><span data-stu-id="309ef-201">Browse to `http://<app_name>.azurewebsites.net/` and add a few tasks to the list.</span></span> 

![Aplicativo Java em execução no serviço de aplicativo do Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="309ef-203">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="309ef-203">**Congratulations!**</span></span> <span data-ttu-id="309ef-204">Você está executando um aplicativo Java controlado por dados no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="309ef-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="309ef-205">Atualizar o aplicativo e reimplantar</span><span class="sxs-lookup"><span data-stu-id="309ef-205">Update the app and redeploy</span></span>

<span data-ttu-id="309ef-206">Atualize o aplicativo para incluir uma coluna adicional na lista de tarefas para o dia em que o item foi criado.</span><span class="sxs-lookup"><span data-stu-id="309ef-206">Update the application to include an additional column in the todo list for what day the item was created.</span></span> <span data-ttu-id="309ef-207">O Spring Boot lida com atualizações do esquema de banco de dados para você, como as alterações do modelo de dados sem alterar os registros do banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="309ef-207">Spring Boot handles updating the database schema for you as the data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="309ef-208">Em seu sistema local, abra *src/main/java/com/example/fabrikam/TodoItem.java* e adicione as importações a seguir à classe:</span><span class="sxs-lookup"><span data-stu-id="309ef-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add the following imports to the class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="309ef-209">Adicione uma propriedade `String` `timeCreated` para *src/main/java/com/example/fabrikam/TodoItem.java*, inicializando-a com um carimbo de data/hora na criação do objeto.</span><span class="sxs-lookup"><span data-stu-id="309ef-209">Add a `String` property `timeCreated` to *src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="309ef-210">Adicione getters/setters para a nova propriedade `timeCreated` enquanto você estiver editando este arquivo.</span><span class="sxs-lookup"><span data-stu-id="309ef-210">Add getters/setters for the new `timeCreated` property while you are editing this file.</span></span>

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

3. <span data-ttu-id="309ef-211">Atualize *src/main/java/com/example/fabrikam/TodoDemoController.java* em uma linha no método `updateTodo` para definir o carimbo de data/hora:</span><span class="sxs-lookup"><span data-stu-id="309ef-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in the `updateTodo` method to set the timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="309ef-212">Adicione suporte para o novo campo no modelo Thymeleaf.</span><span class="sxs-lookup"><span data-stu-id="309ef-212">Add support for the new field in the Thymeleaf template.</span></span> <span data-ttu-id="309ef-213">Atualize *src/main/resources/templates/index.html* com um novo cabeçalho de tabela para o carimbo de data/hora e um novo campo para exibir o valor do carimbo de data/hora em cada linha de dados de tabela.</span><span class="sxs-lookup"><span data-stu-id="309ef-213">Update *src/main/resources/templates/index.html* with a new table header for the timestamp, and a new field to display the value of the timestamp in each table data row.</span></span>

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

5. <span data-ttu-id="309ef-214">Recompile o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="309ef-214">Rebuild the application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="309ef-215">Realize o FTP no .WAR atualizado como antes, removendo o diretório existente *site/wwwroot/webapps/ROOT* e *ROOT.war*, em seguida, carregando o arquivo .WAR atualizado como ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="309ef-215">FTP the updated .WAR as before, removing the existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading the updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="309ef-216">Quando você atualiza o aplicativo, uma coluna **Hora da Criação** fica visível.</span><span class="sxs-lookup"><span data-stu-id="309ef-216">When you refresh the app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="309ef-217">Quando você adiciona uma nova tarefa, o aplicativo preenche automaticamente o carimbo de data/hora.</span><span class="sxs-lookup"><span data-stu-id="309ef-217">When you add a new task, the app will populate the timestamp automatically.</span></span> <span data-ttu-id="309ef-218">As tarefas existentes permanecem inalteradas e trabalham com o aplicativo, embora o modelo de dados subjacente tenha sido alterado.</span><span class="sxs-lookup"><span data-stu-id="309ef-218">Your existing tasks remain unchanged and work with the app even though the underlying data model has changed.</span></span> 

![Aplicativo Java atualizado com uma nova coluna](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="309ef-220">Logs de diagnóstico de fluxo</span><span class="sxs-lookup"><span data-stu-id="309ef-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="309ef-221">Enquanto o aplicativo Java é executado no Serviço de Aplicativo do Azure, é possível fazer com que os logs do console sejam encaminhados diretamente para seu terminal.</span><span class="sxs-lookup"><span data-stu-id="309ef-221">While your Java application runs in Azure App Service, you can get the console logs piped directly to your terminal.</span></span> <span data-ttu-id="309ef-222">Dessa forma, é possível obter as mesmas mensagens de diagnóstico para ajudá-lo a depurar erros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="309ef-222">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="309ef-223">Para iniciar o streaming de log, use o comando [az webapp log tail](/cli/azure/appservice/web/log#tail).</span><span class="sxs-lookup"><span data-stu-id="309ef-223">To start log streaming, use the [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="309ef-224">Gerenciar seu aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-224">Manage your Azure web app</span></span>

<span data-ttu-id="309ef-225">Vá para o portal do Azure para ver o aplicativo Web que você criou.</span><span class="sxs-lookup"><span data-stu-id="309ef-225">Go to the Azure portal to see the web app you created.</span></span>

<span data-ttu-id="309ef-226">Para fazer isso, entre em [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="309ef-226">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="309ef-227">No menu à esquerda, clique em **Serviço de Aplicativo**, em seguida, clique no nome do seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="309ef-227">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Navegação do portal para o aplicativo Web do Azure](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="309ef-229">Por padrão, a folha de seu aplicativo Web mostra a página **Visão Geral**.</span><span class="sxs-lookup"><span data-stu-id="309ef-229">By default, your web app's blade shows the **Overview** page.</span></span> <span data-ttu-id="309ef-230">Esta página fornece uma visão de como está seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="309ef-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="309ef-231">Aqui, você também pode executar tarefas de gerenciamento como parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="309ef-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="309ef-232">As guias no lado esquerdo da folha mostram as páginas de configuração diferentes que você pode abrir.</span><span class="sxs-lookup"><span data-stu-id="309ef-232">The tabs on the left side of the blade show the different configuration pages you can open.</span></span>

![Folha Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="309ef-234">Essas guias na folha mostram muitos recursos excelentes que você pode adicionar ao seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="309ef-234">These tabs in the blade show the many great features you can add to your web app.</span></span> <span data-ttu-id="309ef-235">A lista a seguir fornece algumas possibilidades:</span><span class="sxs-lookup"><span data-stu-id="309ef-235">The following list gives you just a few of the possibilities:</span></span>
* <span data-ttu-id="309ef-236">mapear um nome DNS personalizado</span><span class="sxs-lookup"><span data-stu-id="309ef-236">Map a custom DNS name</span></span>
* <span data-ttu-id="309ef-237">associar um certificado SSL personalizado</span><span class="sxs-lookup"><span data-stu-id="309ef-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="309ef-238">configurar uma implantação contínua</span><span class="sxs-lookup"><span data-stu-id="309ef-238">Configure continuous deployment</span></span>
* <span data-ttu-id="309ef-239">Escalar vertical e horizontalmente</span><span class="sxs-lookup"><span data-stu-id="309ef-239">Scale up and out</span></span>
* <span data-ttu-id="309ef-240">adicionar a autenticação do usuário</span><span class="sxs-lookup"><span data-stu-id="309ef-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="309ef-241">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="309ef-241">Clean up resources</span></span>

<span data-ttu-id="309ef-242">Se não precisar desses recursos para outro tutorial (consulte [Próximas etapas](#next)), você poderá excluí-los executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="309ef-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running the following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="309ef-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="309ef-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="309ef-244">Criar um banco de dados MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="309ef-245">Conectar um aplicativo Java de exemplo para o MySQL</span><span class="sxs-lookup"><span data-stu-id="309ef-245">Connect a sample Java app to the MySQL</span></span>
> * <span data-ttu-id="309ef-246">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-246">Deploy the app to Azure</span></span>
> * <span data-ttu-id="309ef-247">Atualizar o aplicativo e reimplantar</span><span class="sxs-lookup"><span data-stu-id="309ef-247">Update and redeploy the app</span></span>
> * <span data-ttu-id="309ef-248">Transmitir logs de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="309ef-249">Gerenciar o aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-249">Manage the app in the Azure portal</span></span>

<span data-ttu-id="309ef-250">Vá para o próximo tutorial para aprender a mapear um nome DNS personalizado para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="309ef-250">Advance to the next tutorial to learn how to map a custom DNS name to the app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="309ef-251">Mapear um nome DNS personalizado existente para aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="309ef-251">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)