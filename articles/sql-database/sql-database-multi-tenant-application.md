---
title: "Implementar o aplicativos SaaS multilocatário com o Banco de Dados SQL do Azure | Microsoft Docs"
description: "Implementar o aplicativos SaaS multilocatário com o Banco de Dados SQL do Azure."
services: sql-database
documentationcenter: 
author: AyoOlubeko
manager: jhubbard
editor: monicar
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/08/2017
ms.author: AyoOlubek
ms.openlocfilehash: 0aea69d86a51c38c99a72f46737de1eea27bef83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="b3b77-103">Implementar um aplicativos SaaS multilocatário usando o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="b3b77-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="b3b77-104">Um aplicativo multilocatário é um aplicativo hospedado em um ambiente de nuvem e fornece o mesmo conjunto de serviços para centenas ou milhares de locatários que não compartilham ou veem os dados uns dos outros.</span><span class="sxs-lookup"><span data-stu-id="b3b77-104">A multi-tenant application is an application hosted in a cloud environment and that provides the same set of services to hundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="b3b77-105">Um exemplo é um aplicativo SaaS que fornece serviços para locatários em um ambiente hospedado em nuvem.</span><span class="sxs-lookup"><span data-stu-id="b3b77-105">An example is an SaaS application that provides services to tenants in a cloud-hosted environment.</span></span> <span data-ttu-id="b3b77-106">Esse modelo isola os dados de cada locatário e otimiza a distribuição dos recursos, reduzindo os custos.</span><span class="sxs-lookup"><span data-stu-id="b3b77-106">This model isolates the data for each tenant and optimizes the distribution of resources for cost.</span></span> 

<span data-ttu-id="b3b77-107">Este tutorial demonstra como criar um aplicativo SaaS multilocatário usando o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3b77-107">This tutorial demonstrates how to create a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="b3b77-108">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="b3b77-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b3b77-109">Configurar um ambiente de banco de dados para dar suporte a um aplicativo SaaS multilocatário, usando o padrão de banco de dados por locatário</span><span class="sxs-lookup"><span data-stu-id="b3b77-109">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="b3b77-110">Criar um catálogo de locatários</span><span class="sxs-lookup"><span data-stu-id="b3b77-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="b3b77-111">Provisionar um banco de dados de locatário e registrá-lo no catálogo de locatários</span><span class="sxs-lookup"><span data-stu-id="b3b77-111">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="b3b77-112">Configurar um aplicativo Java de exemplo</span><span class="sxs-lookup"><span data-stu-id="b3b77-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="b3b77-113">Acessar um bancos de dados de locatários simples com um aplicativo de console Java</span><span class="sxs-lookup"><span data-stu-id="b3b77-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="b3b77-114">Excluir um locatário</span><span class="sxs-lookup"><span data-stu-id="b3b77-114">Delete a tenant</span></span>

<span data-ttu-id="b3b77-115">Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="b3b77-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3b77-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b3b77-116">Prerequisites</span></span>

<span data-ttu-id="b3b77-117">Para concluir este tutorial, verifique se você tem:</span><span class="sxs-lookup"><span data-stu-id="b3b77-117">To complete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="b3b77-118">Instalada a versão mais recente do PowerShell e o [SDK mais recente do Azure PowerShell](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="b3b77-118">Installed the newest version of PowerShell and the [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="b3b77-119">Instalada a versão mais recente do [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="b3b77-119">Installed the latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="b3b77-120">Instalar o SQL Server Management Studio também instala a versão mais recente do SQLPackage, um utilitário de linha de comando que pode ser usado para automatizar diversas tarefas de desenvolvimento de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b3b77-120">Installing SQL Server Management Studio also installs the latest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span></span>

* <span data-ttu-id="b3b77-121">[JRE 8 (Java Runtime Environment)](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) e o [JDK (JAVA Development Kit) mais recente](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) foram instalados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="b3b77-121">Installed the [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and the [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="b3b77-122">Instalado o [Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="b3b77-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="b3b77-123">O Maven será usado para ajudar a gerenciar as dependências, compilar, testar e executar seu projeto Java de exemplo</span><span class="sxs-lookup"><span data-stu-id="b3b77-123">Maven will be used to help manage dependencies, build, test and run the sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="b3b77-124">Configurar o ambiente de dados</span><span class="sxs-lookup"><span data-stu-id="b3b77-124">Set up data environment</span></span>

<span data-ttu-id="b3b77-125">Você provisionará um banco de dados por locatário.</span><span class="sxs-lookup"><span data-stu-id="b3b77-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="b3b77-126">O modelo de banco de dados por locatário proporciona o mais alto grau de isolamento entre locatários, pouco custo de DevOps.</span><span class="sxs-lookup"><span data-stu-id="b3b77-126">The database-per-tenant model provides the highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="b3b77-127">Para otimizar o custo dos recursos de nuvem, você também provisionará os bancos de dados do locatário em um pool elástico, que permite a otimização do desempenho de preço de um grupo de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="b3b77-127">To optimize the cost of cloud resources, you will also be provisioning the tenant databases into an elastic pool which allows you to optimize the price performance for a group of databases.</span></span> <span data-ttu-id="b3b77-128">Para saber mais sobre outro modelos de provisionamento de banco de dados [clique aqui](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="b3b77-128">To learn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="b3b77-129">Execute estas etapas para criar um SQL Server e um pool elástico que hospedará todos os seus bancos de dados de locatário.</span><span class="sxs-lookup"><span data-stu-id="b3b77-129">Follow these steps to create a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="b3b77-130">Crie variáveis para armazenar valores que serão usados no restante do tutorial.</span><span class="sxs-lookup"><span data-stu-id="b3b77-130">Create variables to store values that will be used in the rest of the tutorial.</span></span> <span data-ttu-id="b3b77-131">Modifique a variável de endereço IP para incluir seu endereço IP</span><span class="sxs-lookup"><span data-stu-id="b3b77-131">Make sure to modify the IP address variable to include your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify to include your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="b3b77-132">Fazer logon no Azure e criar um SQL Server e pool elástico</span><span class="sxs-lookup"><span data-stu-id="b3b77-132">Login to Azure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login to Azure 
   Login-AzureRmAccount
   
   # Create resource group 
   New-AzureRmResourceGroup -Name "myResourceGroup" -Location "northcentralus"
   
   # Create logical SQL Server with firewall rules 
   New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
       -ServerName $servername `
       -Location "northcentralus" `
       -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   
   New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
       -ServerName $servername `
       -FirewallRuleName "singleAddress" -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
   
   # Create elastic pool 
   New-AzureRmSqlElasticPool -ResourceGroupName "myResourceGroup"
       -ServerName $servername `
       -ElasticPoolName "myElasticPool" `
       -Edition "Standard" `
       -Dtu 50 `
       -DatabaseDtuMin 10 `
       -DatabaseDtuMax 20
   ```
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="b3b77-133">Criar um catálogo de locatários</span><span class="sxs-lookup"><span data-stu-id="b3b77-133">Create tenant catalog</span></span> 

<span data-ttu-id="b3b77-134">Em um aplicativo SaaS multilocatário, é importante saber onde estão armazenadas as informações de um locatário.</span><span class="sxs-lookup"><span data-stu-id="b3b77-134">In a multi-tenant SaaS application, it’s important to know where information for a tenant is stored.</span></span> <span data-ttu-id="b3b77-135">Normalmente, elas ficam armazenadas em um banco de dados de catálogo.</span><span class="sxs-lookup"><span data-stu-id="b3b77-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="b3b77-136">O banco de dados de catálogo é usado como um mapeamento entre um locatário e um banco de dados no qual os dados do locatário estão armazenados.</span><span class="sxs-lookup"><span data-stu-id="b3b77-136">The catalog database is used to hold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="b3b77-137">O padrão básico se aplica se um banco de dados multilocatário ou um banco de dados de locatário único for usado.</span><span class="sxs-lookup"><span data-stu-id="b3b77-137">The basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="b3b77-138">Execute estas etapas para criar um banco de dados de catálogo para o aplicativo SaaS de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b3b77-138">Follow these steps to create a catalog database for the sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table to track mapping between tenants and their databases
$commandText = "
CREATE TABLE Tenants
(
   TenantId         INT IDENTITY PRIMARY KEY,
   TenantName       NVARCHAR(128) NOT NULL,
   TenantDatabase   NVARCHAR(128) NOT NULL
);

CREATE INDEX IX_TenantName ON Tenants (TenantName);"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="b3b77-139">Provisione o banco de dados para o 'locatário1' e registre no catálogo de locatários</span><span class="sxs-lookup"><span data-stu-id="b3b77-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="b3b77-140">Use o Powershell para provisionar um banco de dados para um novo locatário, 'locatário1', e registre esse locatário no catálogo.</span><span class="sxs-lookup"><span data-stu-id="b3b77-140">Use Powershell to provision a database for a new tenant 'tenant1' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant1');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant1 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register 'tenant1' in the tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant1', '$tenant1');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="b3b77-141">Provisione o banco de dados para o 'locatário2' e registre no catálogo de locatários</span><span class="sxs-lookup"><span data-stu-id="b3b77-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="b3b77-142">Use o Powershell para provisionar um banco de dados para um novo locatário, 'locatário2', e registre esse locatário no catálogo.</span><span class="sxs-lookup"><span data-stu-id="b3b77-142">Use Powershell to provision a database for a new tenant 'tenant2' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant2');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant2 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register tenant 'tenant2' in the tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant2', '$tenant2');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="set-up-sample-java-application"></a><span data-ttu-id="b3b77-143">Configurar um aplicativo Java de exemplo</span><span class="sxs-lookup"><span data-stu-id="b3b77-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="b3b77-144">Criar um projeto do Maven.</span><span class="sxs-lookup"><span data-stu-id="b3b77-144">Create a maven project.</span></span> <span data-ttu-id="b3b77-145">Digite o seguinte em uma janela de prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="b3b77-145">Type the following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="b3b77-146">Adicione esta dependência, o nível da linguagem e a opção de compilação para oferecer suporte a arquivos de manifesto em jars para o arquivo pom.xml:</span><span class="sxs-lookup"><span data-stu-id="b3b77-146">Add this dependency, language level, and build option to support manifest files in jars to the pom.xml file:</span></span>
   
   ```XML
   <dependency>
         <groupId>com.microsoft.sqlserver</groupId>
         <artifactId>mssql-jdbc</artifactId>
         <version>6.1.0.jre8</version>
   </dependency>
   
   <properties>
         <maven.compiler.source>1.8</maven.compiler.source>
         <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   
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

3. <span data-ttu-id="b3b77-147">Adicione o seguinte ao arquivo App.java:</span><span class="sxs-lookup"><span data-stu-id="b3b77-147">Add the following into the App.java file:</span></span>

   ```java 
   package com.sqldbsamples;
   
   import java.util.Map;
   
   import java.util.HashMap;
   
   import java.io.BufferedReader;
   
   import java.io.InputStreamReader;
   
   import java.sql.Connection;
   
   import java.sql.Statement;
   
   import java.sql.PreparedStatement;
   
   import java.sql.ResultSet;
   
   import java.sql.DriverManager;
   
   public class App {
   
   private static final String SERVER_NAME = "your-server-name";
   
   private static final String CATALOG_DB_NAME = "tenantCatalog";
   
   private static final String USER = "ServerAdmin";
   
   private static final String PASSWORD = "ChangeYourAdminPassword1";
   
   private static final String CATALOG_DB_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, CATALOG_DB_NAME, USER, PASSWORD);
   
   private static final String CMD_LIST = "LIST";

   private static final String CMD_QUERY = "QUERY";

   private static final String CMD_QUIT = "QUIT";
   
   public static void main(String[] args) {
   
   System.out.println("\n############################");
   
   System.out.println("## SAAS DATABASE TUTORIAL ##");
   
   System.out.println("############################\n");
   
   System.out.println("OPTIONS");
   
   System.out.println(" " + CMD_LIST + " - list tenants");
   
   System.out.println(" " + CMD_QUERY + " <NAME> - connect and tenant query tenant <NAME>");
   
   System.out.println(" " + CMD_QUIT + " - quit the application\n");
   
   try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
   
   while(true) {
   
   String[] input = br.readLine().split("\\s");
   
   if (null != input && input.length > 0) {
   
   if (input[0].equalsIgnoreCase(CMD_LIST)) {
   
   listTenants();
   
   } else if (input[0].toLowerCase().startsWith(CMD_QUERY.toLowerCase()) && input.length == 2) {
   
   queryTenant(input[1].trim());
   
   } else if (input[0].equalsIgnoreCase(CMD_QUIT)) {
   
   break;
   
   } else {
   
   System.out.println(" -> Command not supported");
   
   }
   
   }
   
   System.out.println("");
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void listTenants() {
   
   // List all tenants that currently exist in the system
   
   String sql = "SELECT TenantName FROM Tenants";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   Statement stmt = connection.createStatement();
   
   ResultSet resultSet = stmt.executeQuery(sql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void queryTenant(String name) {
   
   // Query the data that was previously inserted into the primary database from the geo replicated database
   
   String url = null;
   
   String sql = "SELECT TenantDatabase FROM Tenants WHERE TenantName = ?";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   PreparedStatement pstmt = connection.prepareStatement(sql)) {
   
   pstmt.setString(1, name);
   
   try (ResultSet resultSet = pstmt.executeQuery()) {
   
   if (resultSet.next()) {
   
   url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, resultSet.getString(1), USER, PASSWORD);
   
   }
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   if (null != url) {
   
   String tenantSql = "SELECT TenantName FROM WhoAmI";
   
   try (Connection connection = DriverManager.getConnection(url);
   
   Statement stmt = connection.createStatement();

   ResultSet resultSet = stmt.executeQuery(tenantSql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> Entry in table WhoAmI in tenant " + name + " is: " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   } else {
   
   System.out.println(" -> Tenant " + name + " not found");
   
   }
   
   }
   
   }
   ```

4. <span data-ttu-id="b3b77-148">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="b3b77-148">Save the file.</span></span>

5. <span data-ttu-id="b3b77-149">Acesse o console de comando e execute</span><span class="sxs-lookup"><span data-stu-id="b3b77-149">Go to command console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="b3b77-150">Quando terminar, execute o seguinte para executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="b3b77-150">When finished, execute the following to run the application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="b3b77-151">A saída será parecida com esta, se for executado com êxito:</span><span class="sxs-lookup"><span data-stu-id="b3b77-151">The output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit the application

* List the tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="b3b77-152">Excluir primeiro locatário</span><span class="sxs-lookup"><span data-stu-id="b3b77-152">Delete first tenant</span></span> 
<span data-ttu-id="b3b77-153">Use o PowerShell para excluir a entrada no banco de dados e no catálogo de locatários do primeiro locatário.</span><span class="sxs-lookup"><span data-stu-id="b3b77-153">Use PowerShell to delete the tenant database and catalog entry for the first tenant.</span></span>

```PowerShell
# Remove 'tenant1' from catalog 
$commandText = "DELETE FROM Tenants WHERE TenantName = '$tenant1';"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Delete database 
Remove-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1
```

<span data-ttu-id="b3b77-154">Tente se conectar a 'locatário1' usando o aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="b3b77-154">Try connecting to 'tenant1' using the Java application.</span></span> <span data-ttu-id="b3b77-155">Você receberá um erro informando que o locatário não existe.</span><span class="sxs-lookup"><span data-stu-id="b3b77-155">You will get an error stating that the tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3b77-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b3b77-156">Next steps</span></span> 

<span data-ttu-id="b3b77-157">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="b3b77-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b3b77-158">Configurar um ambiente de banco de dados para dar suporte a um aplicativo SaaS multilocatário, usando o padrão de banco de dados por locatário</span><span class="sxs-lookup"><span data-stu-id="b3b77-158">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="b3b77-159">Criar um catálogo de locatários</span><span class="sxs-lookup"><span data-stu-id="b3b77-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="b3b77-160">Provisionar um banco de dados de locatário e registrá-lo no catálogo de locatários</span><span class="sxs-lookup"><span data-stu-id="b3b77-160">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="b3b77-161">Configurar um aplicativo Java de exemplo</span><span class="sxs-lookup"><span data-stu-id="b3b77-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="b3b77-162">Acessar um bancos de dados de locatários simples com um aplicativo de console Java</span><span class="sxs-lookup"><span data-stu-id="b3b77-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="b3b77-163">Excluir um locatário</span><span class="sxs-lookup"><span data-stu-id="b3b77-163">Delete a tenant</span></span>

* <span data-ttu-id="b3b77-164">Amostras do PowerShell para tarefas comuns, consulte [Amostras do PowerShell para o Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="b3b77-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="b3b77-165">Padrões de design para aplicativos SaaS multilocatário,confira [Padrões de design](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="b3b77-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="b3b77-166">Amostras de Java para tarefas comuns do Azure, consulte [Centro de Desenvolvimento do Java](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="b3b77-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



