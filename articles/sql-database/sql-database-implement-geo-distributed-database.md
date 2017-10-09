---
title: "aaaImplement uma solução de banco de dados do Azure SQL distribuído geograficamente | Microsoft Docs"
description: Saiba tooconfigure o banco de dados do SQL Azure e o aplicativo para failover tooa replicada do banco de dados e failover de teste.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 9295d33c669405108a1a64ef1e7cb77f582773a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="70128-103">Implementar um banco de dados distribuído geograficamente</span><span class="sxs-lookup"><span data-stu-id="70128-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="70128-104">Neste tutorial, você configurar um banco de dados do SQL Azure e o aplicativo para failover tooa remoto região e, em seguida, teste seu plano de failover.</span><span class="sxs-lookup"><span data-stu-id="70128-104">In this tutorial, you configure an Azure SQL database and application for failover tooa remote region, and then test your failover plan.</span></span> <span data-ttu-id="70128-105">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="70128-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="70128-106">Criar usuários de banco de dados e conceder a eles permissões</span><span class="sxs-lookup"><span data-stu-id="70128-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="70128-107">Configurar uma regra de firewall de nível de banco de dados</span><span class="sxs-lookup"><span data-stu-id="70128-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="70128-108">Criar um [grupo de failover de replicação geográfica](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="70128-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="70128-109">Criar e compilar um aplicativo de Java tooquery um banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="70128-109">Create and compile a Java application tooquery an Azure SQL database</span></span>
> * <span data-ttu-id="70128-110">Executar uma análise de recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="70128-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="70128-111">Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="70128-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="70128-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="70128-112">Prerequisites</span></span>

<span data-ttu-id="70128-113">toocomplete neste tutorial, verifique Olá se os pré-requisitos a seguir são concluídas:</span><span class="sxs-lookup"><span data-stu-id="70128-113">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

- <span data-ttu-id="70128-114">Olá instalada mais recente [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="70128-114">Installed hello latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="70128-115">Um Banco de Dados SQL do Azure instalado.</span><span class="sxs-lookup"><span data-stu-id="70128-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="70128-116">Este tutorial usa o banco de dados do exemplo hello AdventureWorksLT com um nome de **mySampleDatabase** de um desses inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="70128-116">This tutorial uses hello AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="70128-117">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="70128-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="70128-118">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="70128-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="70128-119">Criar Banco de dados - PowerShell</span><span class="sxs-lookup"><span data-stu-id="70128-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="70128-120">Identificar um método tooexecute SQL scripts no banco de dados, você pode usar uma saudação ferramentas de consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="70128-120">Have identified a method tooexecute SQL scripts against your database, you can use one of hello following query tools:</span></span>
   - <span data-ttu-id="70128-121">editor de consultas de saudação do hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70128-121">hello query editor in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="70128-122">Para obter mais informações sobre como usar o editor de consultas Olá Olá portal do Azure, consulte [conectar e consultar usando o Editor de consulta](sql-database-get-started-portal.md#query-the-sql-database).</span><span class="sxs-lookup"><span data-stu-id="70128-122">For more information on using hello query editor in hello Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="70128-123">versão mais recente de saudação do [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), que é um ambiente integrado para gerenciar qualquer infraestrutura SQL, do SQL Server tooSQL banco de dados para o Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="70128-123">hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="70128-124">versão mais recente de saudação do [código do Visual Studio](https://code.visualstudio.com/docs), que é um editor de código gráfica para macOS, Linux e Windows que oferece suporte a extensões, incluindo Olá [mssql extensão](https://aka.ms/mssql-marketplace) para consultar o Microsoft SQL Server , Banco de dados SQL do azure e SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="70128-124">hello newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="70128-125">Para obter mais informações sobre como usar essa ferramenta com o Banco de Dados SQL do Azure, consulte [Conectar e consultar com código VS](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="70128-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="70128-126">Criar usuários de banco de dados e conceder permissões</span><span class="sxs-lookup"><span data-stu-id="70128-126">Create database users and grant permissions</span></span>

<span data-ttu-id="70128-127">Conecte-se o banco de dados tooyour e criar contas de usuário usando uma saudação ferramentas de consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="70128-127">Connect tooyour database and create user accounts using one of hello following query tools:</span></span>

- <span data-ttu-id="70128-128">editor de consultas de saudação do hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="70128-128">hello Query editor in hello Azure portal</span></span>
- <span data-ttu-id="70128-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="70128-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="70128-130">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="70128-130">Visual Studio Code</span></span>

<span data-ttu-id="70128-131">Essas contas de usuário automaticamente replicam servidor secundário tooyour (e ser mantidas em sincronia).</span><span class="sxs-lookup"><span data-stu-id="70128-131">These user accounts replicate automatically tooyour secondary server (and be kept in sync).</span></span> <span data-ttu-id="70128-132">toouse SQL Server Management Studio ou o código do Visual Studio, talvez seja necessário tooconfigure uma regra de firewall, se você estiver se conectando de um cliente em um endereço IP para o qual você ainda não tiver configurado um firewall.</span><span class="sxs-lookup"><span data-stu-id="70128-132">toouse SQL Server Management Studio or Visual Studio Code, you may need tooconfigure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="70128-133">Para encontrar as etapas detalhadas, consulte [Criar uma regra de firewall no nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="70128-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="70128-134">Em uma janela de consulta, execute Olá consulta toocreate duas contas de usuário no banco de dados a seguir.</span><span class="sxs-lookup"><span data-stu-id="70128-134">In a query window, execute hello following query toocreate two user accounts in your database.</span></span> <span data-ttu-id="70128-135">Esse script concede **db_owner** permissões toohello **app_admin** conta e concede **selecione** e **atualização** toohello de permissões **app_user** conta.</span><span class="sxs-lookup"><span data-stu-id="70128-135">This script grants **db_owner** permissions toohello **app_admin** account and grants **SELECT** and **UPDATE** permissions toohello **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="70128-136">Criar firewall no nível de banco de dados</span><span class="sxs-lookup"><span data-stu-id="70128-136">Create database-level firewall</span></span>

<span data-ttu-id="70128-137">Crie uma [regra de firewall de nível de banco de dados](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) para seu Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="70128-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="70128-138">Essa regra de firewall de nível de banco de dados automaticamente replica toohello servidor secundário que você cria neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="70128-138">This database-level firewall rule replicates automatically toohello secondary server that you create in this tutorial.</span></span> <span data-ttu-id="70128-139">Para manter a simplicidade (neste tutorial), use Olá endereço IP público do computador Olá no qual você está executando Olá as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="70128-139">For simplicity (in this tutorial), use hello public IP address of hello computer on which you are performing hello steps in this tutorial.</span></span> <span data-ttu-id="70128-140">endereço IP de saudação toodetermine usado para a regra de firewall de nível de servidor de saudação do computador atual, consulte [criar um firewall de nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="70128-140">toodetermine hello IP address used for hello server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="70128-141">Na janela de consulta aberta, substitua consulta anterior Olá Olá consulta a seguir, substituindo os endereços IP hello com endereços IP adequados Olá para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="70128-141">In your open query window, replace hello previous query with hello following query, replacing hello IP addresses with hello appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="70128-142">Criar um grupo de failover automático de replicação geográfica ativa</span><span class="sxs-lookup"><span data-stu-id="70128-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="70128-143">Usando o PowerShell do Azure, crie um [grupo de replicação geográfica de failover automático](sql-database-geo-replication-overview.md) entre o servidor SQL do Azure existente e o hello novo vazio do servidor do SQL Azure em uma região do Azure e, em seguida, adicione o grupo de failover de toohello de banco de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="70128-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and hello new empty Azure SQL server in an Azure region, and then add your sample database toohello failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70128-144">Esses cmdlets requerem o Azure PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="70128-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="70128-145">Popular variáveis para seus scripts do PowerShell usando valores de saudação para seu servidor existente e o banco de dados de exemplo e fornecer um valor exclusivo para o nome do grupo de failover.</span><span class="sxs-lookup"><span data-stu-id="70128-145">Populate variables for your PowerShell scripts using hello values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

   ```powershell
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   $myresourcegroupname = "<your resource group name>"
   $mylocation = "<your resource group location>"
   $myservername = "<your existing server name>"
   $mydatabasename = "mySampleDatabase"
   $mydrlocation = "<your disaster recovery location>"
   $mydrservername = "<your disaster recovery server name>"
   $myfailovergroupname = "<your unique failover group name>"
   ```

2. <span data-ttu-id="70128-146">Criar um servidor de backup vazio na sua região de failover.</span><span class="sxs-lookup"><span data-stu-id="70128-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="70128-147">Crie um grupo de failover entre dois servidores de saudação.</span><span class="sxs-lookup"><span data-stu-id="70128-147">Create a failover group between hello two servers.</span></span>

   ```powershell
   $myfailovergroup = New-AzureRMSqlDatabaseFailoverGroup `
      –ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -PartnerServerName $mydrservername  `
      –FailoverGroupName $myfailovergroupname `
      –FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   $myfailovergroup   
   ```

4. <span data-ttu-id="70128-148">Adicione o grupo de failover do banco de dados toohello.</span><span class="sxs-lookup"><span data-stu-id="70128-148">Add your database toohello failover group.</span></span>

   ```powershell
   $myfailovergroup = Get-AzureRmSqlDatabase `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -DatabaseName $mydatabasename | `
    Add-AzureRmSqlDatabaseToFailoverGroup `
      -ResourceGroupName $myresourcegroupname ` `
      -ServerName $myservername `
      -FailoverGroupName $myfailovergroupname
   $myfailovergroup   
   ```

## <a name="install-java-software"></a><span data-ttu-id="70128-149">Instalar o software Java</span><span class="sxs-lookup"><span data-stu-id="70128-149">Install Java software</span></span>

<span data-ttu-id="70128-150">Olá etapas nesta seção pressupõem que você esteja familiarizado com o desenvolvimento usando Java e é tooworking novo com o banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="70128-150">hello steps in this section assume that you are familiar with developing using Java and are new tooworking with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="70128-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="70128-151">**Mac OS**</span></span>
<span data-ttu-id="70128-152">Abra seu terminal e navegue tooa diretório onde você planeja criar seu projeto Java.</span><span class="sxs-lookup"><span data-stu-id="70128-152">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="70128-153">Instalar **brew** e **Maven** inserindo Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="70128-153">Install **brew** and **Maven** by entering hello following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="70128-154">Para obter orientações detalhadas sobre como instalar e configurar o ambiente Java e Maven, vá Olá [compilar um aplicativo usando o SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), selecione **Java**, selecione **MacOS**e, em seguida, execute Olá instruções detalhadas para configurar o Java e Maven na etapa 1.2 e 1.3.</span><span class="sxs-lookup"><span data-stu-id="70128-154">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="70128-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="70128-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="70128-156">Abra seu terminal e navegue tooa diretório onde você planeja criar seu projeto Java.</span><span class="sxs-lookup"><span data-stu-id="70128-156">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="70128-157">Instalar **Maven** inserindo Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="70128-157">Install **Maven** by entering hello following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="70128-158">Para obter orientações detalhadas sobre como instalar e configurar o ambiente Java e Maven, vá Olá [compilar um aplicativo usando o SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), selecione **Java**, selecione **Ubuntu**e, em seguida, execute Olá instruções detalhadas para configurar o Java e Maven na etapa 1.2, 1.3 e 1.4.</span><span class="sxs-lookup"><span data-stu-id="70128-158">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="70128-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="70128-159">**Windows**</span></span>
<span data-ttu-id="70128-160">Instalar [Maven](https://maven.apache.org/download.cgi) usando o instalador oficial hello.</span><span class="sxs-lookup"><span data-stu-id="70128-160">Install [Maven](https://maven.apache.org/download.cgi) using hello official installer.</span></span> <span data-ttu-id="70128-161">Use Maven toohelp gerenciar dependências, compilar, testar e executar seu projeto Java.</span><span class="sxs-lookup"><span data-stu-id="70128-161">Use Maven toohelp manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="70128-162">Para obter orientações detalhadas sobre como instalar e configurar o ambiente Java e Maven, vá Olá [compilar um aplicativo usando o SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), selecione **Java**, selecione Windows e, em seguida, execute Olá instruções detalhadas para Configurando o Java e Maven na etapa 1.2 e 1.3.</span><span class="sxs-lookup"><span data-stu-id="70128-162">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="70128-163">Criar projeto SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="70128-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="70128-164">No console de comando de saudação (como Bash), crie um projeto Maven.</span><span class="sxs-lookup"><span data-stu-id="70128-164">In hello command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="70128-165">Digite **Y** e clique em **Enter**.</span><span class="sxs-lookup"><span data-stu-id="70128-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="70128-166">Altere os diretórios para seu projeto recém-criado.</span><span class="sxs-lookup"><span data-stu-id="70128-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="70128-167">Usando seu editor favorito, abra o arquivo de pom.xml de saudação na pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="70128-167">Using your favorite editor, open hello pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="70128-168">Adicione hello Microsoft JDBC Driver para o projeto do SQL Server dependência tooyour Maven abrindo o editor de texto favorito e copiando e colando Olá linhas seguintes no arquivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="70128-168">Add hello Microsoft JDBC Driver for SQL Server dependency tooyour Maven project by opening your favorite text editor and copying and pasting hello following lines into your pom.xml file.</span></span> <span data-ttu-id="70128-169">Não substitua valores existentes de saudação preenchida preenchidos no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="70128-169">Do not overwrite hello existing values prepopulated in hello file.</span></span> <span data-ttu-id="70128-170">Olá dependência JDBC deve ser colado em Olá maior (seção "dependências").</span><span class="sxs-lookup"><span data-stu-id="70128-170">hello JDBC dependency must be pasted within hello larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="70128-171">Especifica versão de saudação do projeto de saudação do Java toocompile contra adicionando Olá após a seção "propriedades" no arquivo de pom.xml Olá após a seção de "dependências" Olá.</span><span class="sxs-lookup"><span data-stu-id="70128-171">Specify hello version of Java toocompile hello project against by adding hello following “properties” section into hello pom.xml file after hello "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="70128-172">Adicione a seguinte hello "criar" seção em Olá pom.xml arquivo após hello "propriedades" seção toosupport arquivos de manifesto no jars.</span><span class="sxs-lookup"><span data-stu-id="70128-172">Add hello following "build" section into hello pom.xml file after hello "properties" section toosupport manifest files in jars.</span></span>       

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.apache.maven.plugins</groupId>
         <artifactId>maven-jar-plugin</artifactId>
         <version>3.0.0</version>
         <configuration>
           <archive>
             <manifest>
               <mainClass>com.sqldbsamples.App</mainClass>
             </manifest>
           </archive>
        </configuration>
       </plugin>
     </plugins>
   </build>
   ```
8. <span data-ttu-id="70128-173">Salve e feche o arquivo de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="70128-173">Save and close hello pom.xml file.</span></span>
9. <span data-ttu-id="70128-174">Abrir o arquivo de App.java hello (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) e substitua o conteúdo de saudação com hello conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="70128-174">Open hello App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace hello contents with hello following contents.</span></span> <span data-ttu-id="70128-175">Substitua o nome do grupo de failover Olá pelo nome de Olá para o grupo de failover.</span><span class="sxs-lookup"><span data-stu-id="70128-175">Replace hello failover group name with hello name for your failover group.</span></span> <span data-ttu-id="70128-176">Se você tiver alterado os valores hello por nome de banco de dados hello, usuário ou senha, altere esses valores também.</span><span class="sxs-lookup"><span data-stu-id="70128-176">If you have changed hello values for hello database name, user, or password, change those values as well.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.Timestamp;
   import java.sql.DriverManager;
   import java.util.Date;
   import java.util.concurrent.TimeUnit;

   public class App {

      private static final String FAILOVER_GROUP_NAME = "myfailovergroupname";
  
      private static final String DB_NAME = "mySampleDatabase";
      private static final String USER = "app_user";
      private static final String PASSWORD = "ChangeYourPassword1";

      private static final String READ_WRITE_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);
      private static final String READ_ONLY_URL = String.format("jdbc:sqlserver://%s.secondary.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);

      public static void main(String[] args) {
         System.out.println("#######################################");
         System.out.println("## GEO DISTRIBUTED DATABASE TUTORIAL ##");
         System.out.println("#######################################");
         System.out.println(""); 

         int highWaterMark = getHighWaterMarkId();

         try {
            for(int i = 1; i < 1000; i++) {
                //  loop will run for about 1 hour
                System.out.print(i + ": insert on primary " + (insertData((highWaterMark + i))?"successful":"failed"));
                TimeUnit.SECONDS.sleep(1);
                System.out.print(", read from secondary " + (selectData((highWaterMark + i))?"successful":"failed") + "\n");
                TimeUnit.SECONDS.sleep(3);
            }
         } catch(Exception e) {
            e.printStackTrace();
      }
   }

   private static boolean insertData(int id) {
      // Insert data into hello product table with a unique product name that we can use toofind hello product again later
      String sql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         pstmt.setInt(2, 200989 + id + 10000);
         pstmt.setString(3, "Blue");
         pstmt.setDouble(4, 75.00);
         pstmt.setDouble(5, 89.99);
         pstmt.setTimestamp(6, new Timestamp(new Date().getTime()));
         return (1 == pstmt.executeUpdate());
      } catch (Exception e) {
         return false;
      }
   }

   private static boolean selectData(int id) {
      // Query hello data that was previously inserted into hello primary database from hello geo replicated database
      String sql = "SELECT Name, Color, ListPrice FROM SalesLT.Product WHERE Name = ?";

      try (Connection connection = DriverManager.getConnection(READ_ONLY_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         try (ResultSet resultSet = pstmt.executeQuery()) {
            return resultSet.next();
         }
      } catch (Exception e) {
         return false;
      }
   }

   private static int getHighWaterMarkId() {
      // Query hello high water mark id that is stored in hello table toobe able toomake unique inserts 
      String sql = "SELECT MAX(ProductId) FROM SalesLT.Product";
      int result = 1;
        
      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              Statement stmt = connection.createStatement();
              ResultSet resultSet = stmt.executeQuery(sql)) {
         if (resultSet.next()) {
             result =  resultSet.getInt(1);
            }
         } catch (Exception e) {
          e.printStackTrace();
         }
         return result;
      }
   }
   ```
6. <span data-ttu-id="70128-177">Salve e feche o arquivo de App.java hello.</span><span class="sxs-lookup"><span data-stu-id="70128-177">Save and close hello App.java file.</span></span>

## <a name="compile-and-run-hello-sqldbsample-project"></a><span data-ttu-id="70128-178">Compilar e executar Olá SqlDbSample projeto</span><span class="sxs-lookup"><span data-stu-id="70128-178">Compile and run hello SqlDbSample project</span></span>

1. <span data-ttu-id="70128-179">No console de comando hello, execute o comando de toofollowing.</span><span class="sxs-lookup"><span data-stu-id="70128-179">In hello command console, execute toofollowing command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="70128-180">Quando terminar, execute Olá aplicativo de hello toorun de comando (ele é executado por aproximadamente 1 hora, a menos que você pare manualmente) a seguir:</span><span class="sxs-lookup"><span data-stu-id="70128-180">When finished, execute hello following command toorun hello application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="70128-181">Executar o treinamento de recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="70128-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="70128-182">Chame o failover manual do grupo de failover.</span><span class="sxs-lookup"><span data-stu-id="70128-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="70128-183">Observe Olá resultados de aplicativo durante o failover.</span><span class="sxs-lookup"><span data-stu-id="70128-183">Observe hello application results during failover.</span></span> <span data-ttu-id="70128-184">Algumas inserções falharem enquanto atualiza Olá cache DNS.</span><span class="sxs-lookup"><span data-stu-id="70128-184">Some inserts fail while hello DNS cache refreshes.</span></span>     

3. <span data-ttu-id="70128-185">Descubra qual função seu servidor de recuperação de desastre executando.</span><span class="sxs-lookup"><span data-stu-id="70128-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="70128-186">Failback.</span><span class="sxs-lookup"><span data-stu-id="70128-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="70128-187">Observe Olá resultados de aplicativo durante o failback.</span><span class="sxs-lookup"><span data-stu-id="70128-187">Observe hello application results during failback.</span></span> <span data-ttu-id="70128-188">Algumas inserções falharem enquanto atualiza Olá cache DNS.</span><span class="sxs-lookup"><span data-stu-id="70128-188">Some inserts fail while hello DNS cache refreshes.</span></span>     

6. <span data-ttu-id="70128-189">Descubra qual função seu servidor de recuperação de desastre executando.</span><span class="sxs-lookup"><span data-stu-id="70128-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="70128-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70128-190">Next steps</span></span> 

<span data-ttu-id="70128-191">Para saber mais, confira [Grupos de failover e replicação geográfica ativa](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70128-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
