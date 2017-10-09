---
title: "aplicativo de SaaS multilocatário aaaImplement com o banco de dados do SQL Azure | Microsoft Docs"
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
ms.openlocfilehash: b87b8f296e2c20a8f674b56375f43fdc92df76d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a>Implementar um aplicativos SaaS multilocatário usando o Banco de Dados SQL do Azure

Um aplicativo multilocatário é um aplicativo hospedado em um ambiente de nuvem e que fornece Olá mesmo conjunto de serviços toohundreds ou milhares de locatários que não compartilham ou ver dados uns dos outros. Um exemplo é um aplicativo SaaS que fornece serviços tootenants em um ambiente hospedado na nuvem. Esse modelo isola dados saudação para cada locatário e otimiza a distribuição de saudação do custo de recursos. 

Este tutorial demonstra como toocreate um aplicativo de SaaS multilocatário usando o banco de dados do SQL Azure.

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> * Configurar um aplicativo de SaaS multilocatário, usando o padrão de banco de dados por locatário Olá um toosupport do ambiente de banco de dados
> * Criar um catálogo de locatários
> * Provisionar um banco de dados de locatário e registrá-lo no catálogo de locatário Olá
> * Configurar um aplicativo Java de exemplo 
> * Acessar um bancos de dados de locatários simples com um aplicativo de console Java
> * Excluir um locatário

Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial, verifique se você tem:

* A versão mais recente instalada saudação do PowerShell e Olá [SDK mais recente do PowerShell do Azure](http://azure.microsoft.com/downloads/)

* A versão mais recente instalada saudação do [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). Instalar o SQL Server Management Studio também instala a versão mais recente de saudação do SQLPackage, um utilitário de linha de comando que pode ser usado tooautomate uma variedade de tarefas de desenvolvimento de banco de dados.

* Olá instalado [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) e hello [mais recente JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) instalado em seu computador. 

* Instalado o [Apache Maven](https://maven.apache.org/download.cgi). Será usado o Maven toohelp gerenciar dependências, criar, testar e executar o projeto de Java do exemplo hello

## <a name="set-up-data-environment"></a>Configurar o ambiente de dados

Você provisionará um banco de dados por locatário. modelo de banco de dados por locatário Olá fornece hello mais alto grau de isolamento entre locatários, com baixo custo de DevOps. custo de saudação toooptimize de recursos de nuvem, você será também ser Provisionando Olá locatário bancos de dados em um pool Elástico, que permite que você toooptimize Olá preço desempenho para um grupo de bancos de dados. toolearn sobre outros modelos de provisionamento do banco de dados [ver aqui](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).

Siga estas etapas toocreate do SQL server e um pool Elástico que hospedará a todos os seus bancos de dados do locatário. 

1. Crie variáveis toostore valores que serão usados no restante de saudação do tutorial de saudação. Certifique-se de que toomodify Olá IP tooinclude variável endereço seu endereço IP 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify tooinclude your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. TooAzure de logon e criar um pool de servidor e Elástico do SQL 
   
   ```PowerShell
   # Login tooAzure 
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
   
## <a name="create-tenant-catalog"></a>Criar um catálogo de locatários 

Em um aplicativo de SaaS multilocatário, é importante tooknow armazenamento de informações para um locatário. Normalmente, elas ficam armazenadas em um banco de dados de catálogo. banco de dados de catálogo Olá é toohold usado um mapeamento entre um locatário e um banco de dados no qual os dados desse locatário estão armazenados.  padrão básico Olá se aplica se uma multilocatário ou um banco de dados único locatário é usado.

Siga essas etapas toocreate um banco de dados de catálogo para o aplicativo de SaaS do exemplo hello.

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table tootrack mapping between tenants and their databases
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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a>Provisione o banco de dados para o 'locatário1' e registre no catálogo de locatários 
Use o Powershell tooprovision um banco de dados para um novo locatário 'locatário1' e registre este locatário no catálogo de saudação. 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
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

# Register 'tenant1' in hello tenant catalog 
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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a>Provisione o banco de dados para o 'locatário2' e registre no catálogo de locatários
Use o Powershell tooprovision um banco de dados para um novo locatário 'tenant2' e registre este locatário no catálogo de saudação. 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
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

# Register tenant 'tenant2' in hello tenant catalog 
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

## <a name="set-up-sample-java-application"></a>Configurar um aplicativo Java de exemplo 

1. Criar um projeto do Maven. Digite o seguinte de saudação em uma janela de prompt de comando:
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. Adicionar essa dependência, o nível de linguagem e arquivos de manifesto no arquivo de pom.xml toohello jars do toosupport opção de compilação:
   
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

3. Adicione a seguir no arquivo de App.java Olá Olá:

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
   
   System.out.println(" " + CMD_QUIT + " - quit hello application\n");
   
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
   
   // List all tenants that currently exist in hello system
   
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
   
   // Query hello data that was previously inserted into hello primary database from hello geo replicated database
   
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

4. Salve o arquivo hello.

5. Vá toocommand console e executar

   ```bash
   mvn package
   ```

6. Quando terminar, execute Olá após o aplicativo de hello toorun 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
Olá saída será assim se ele for executado com êxito:

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit hello application

* List hello tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a>Excluir primeiro locatário 
Use PowerShell toodelete Olá locatário banco de dados e o catálogo de entrada para o locatário primeiro hello.

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

Tente conectar-se muito usando 'locatário1' hello aplicativo Java. Você obterá um erro informando que locatário Olá não existe.

## <a name="next-steps"></a>Próximas etapas 

Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> * Configurar um aplicativo de SaaS multilocatário, usando o padrão de banco de dados por locatário Olá um toosupport do ambiente de banco de dados
> * Criar um catálogo de locatários
> * Provisionar um banco de dados de locatário e registrá-lo no catálogo de locatário Olá
> * Configurar um aplicativo Java de exemplo 
> * Acessar um bancos de dados de locatários simples com um aplicativo de console Java
> * Excluir um locatário

* Amostras do PowerShell para tarefas comuns, consulte [Amostras do PowerShell para o Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)

* Padrões de design para aplicativos SaaS multilocatário,confira [Padrões de design](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)

* Amostras de Java para tarefas comuns do Azure, consulte [Centro de Desenvolvimento do Java](https://azure.microsoft.com/develop/java/)



