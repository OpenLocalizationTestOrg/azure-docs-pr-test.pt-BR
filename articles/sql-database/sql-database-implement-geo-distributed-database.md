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
# <a name="implement-a-geo-distributed-database"></a>Implementar um banco de dados distribuído geograficamente

Neste tutorial, você configurar um banco de dados do SQL Azure e o aplicativo para failover tooa remoto região e, em seguida, teste seu plano de failover. Você aprenderá como: 

> [!div class="checklist"]
> * Criar usuários de banco de dados e conceder a eles permissões
> * Configurar uma regra de firewall de nível de banco de dados
> * Criar um [grupo de failover de replicação geográfica](sql-database-geo-replication-overview.md)
> * Criar e compilar um aplicativo de Java tooquery um banco de dados do SQL Azure
> * Executar uma análise de recuperação de desastre

Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.


## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, verifique Olá se os pré-requisitos a seguir são concluídas:

- Olá instalada mais recente [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs). 
- Um Banco de Dados SQL do Azure instalado. Este tutorial usa o banco de dados do exemplo hello AdventureWorksLT com um nome de **mySampleDatabase** de um desses inícios rápidos:

   - [Criar Banco de dados - Portal](sql-database-get-started-portal.md)
   - [Criar Banco de dados - CLI](sql-database-get-started-cli.md)
   - [Criar Banco de dados - PowerShell](sql-database-get-started-powershell.md)

- Identificar um método tooexecute SQL scripts no banco de dados, você pode usar uma saudação ferramentas de consulta a seguir:
   - editor de consultas de saudação do hello [portal do Azure](https://portal.azure.com). Para obter mais informações sobre como usar o editor de consultas Olá Olá portal do Azure, consulte [conectar e consultar usando o Editor de consulta](sql-database-get-started-portal.md#query-the-sql-database).
   - versão mais recente de saudação do [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), que é um ambiente integrado para gerenciar qualquer infraestrutura SQL, do SQL Server tooSQL banco de dados para o Microsoft Windows.
   - versão mais recente de saudação do [código do Visual Studio](https://code.visualstudio.com/docs), que é um editor de código gráfica para macOS, Linux e Windows que oferece suporte a extensões, incluindo Olá [mssql extensão](https://aka.ms/mssql-marketplace) para consultar o Microsoft SQL Server , Banco de dados SQL do azure e SQL Data Warehouse. Para obter mais informações sobre como usar essa ferramenta com o Banco de Dados SQL do Azure, consulte [Conectar e consultar com código VS](sql-database-connect-query-vscode.md). 

## <a name="create-database-users-and-grant-permissions"></a>Criar usuários de banco de dados e conceder permissões

Conecte-se o banco de dados tooyour e criar contas de usuário usando uma saudação ferramentas de consulta a seguir:

- editor de consultas de saudação do hello portal do Azure
- SQL Server Management Studio
- Visual Studio Code

Essas contas de usuário automaticamente replicam servidor secundário tooyour (e ser mantidas em sincronia). toouse SQL Server Management Studio ou o código do Visual Studio, talvez seja necessário tooconfigure uma regra de firewall, se você estiver se conectando de um cliente em um endereço IP para o qual você ainda não tiver configurado um firewall. Para encontrar as etapas detalhadas, consulte [Criar uma regra de firewall no nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).

- Em uma janela de consulta, execute Olá consulta toocreate duas contas de usuário no banco de dados a seguir. Esse script concede **db_owner** permissões toohello **app_admin** conta e concede **selecione** e **atualização** toohello de permissões **app_user** conta. 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a>Criar firewall no nível de banco de dados

Crie uma [regra de firewall de nível de banco de dados](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) para seu Banco de Dados SQL. Essa regra de firewall de nível de banco de dados automaticamente replica toohello servidor secundário que você cria neste tutorial. Para manter a simplicidade (neste tutorial), use Olá endereço IP público do computador Olá no qual você está executando Olá as etapas neste tutorial. endereço IP de saudação toodetermine usado para a regra de firewall de nível de servidor de saudação do computador atual, consulte [criar um firewall de nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).  

- Na janela de consulta aberta, substitua consulta anterior Olá Olá consulta a seguir, substituindo os endereços IP hello com endereços IP adequados Olá para o seu ambiente.  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a>Criar um grupo de failover automático de replicação geográfica ativa 

Usando o PowerShell do Azure, crie um [grupo de replicação geográfica de failover automático](sql-database-geo-replication-overview.md) entre o servidor SQL do Azure existente e o hello novo vazio do servidor do SQL Azure em uma região do Azure e, em seguida, adicione o grupo de failover de toohello de banco de dados de exemplo.

> [!IMPORTANT]
> Esses cmdlets requerem o Azure PowerShell 4.0. [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. Popular variáveis para seus scripts do PowerShell usando valores de saudação para seu servidor existente e o banco de dados de exemplo e fornecer um valor exclusivo para o nome do grupo de failover.

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

2. Criar um servidor de backup vazio na sua região de failover.

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. Crie um grupo de failover entre dois servidores de saudação.

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

4. Adicione o grupo de failover do banco de dados toohello.

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

## <a name="install-java-software"></a>Instalar o software Java

Olá etapas nesta seção pressupõem que você esteja familiarizado com o desenvolvimento usando Java e é tooworking novo com o banco de dados do SQL Azure. 

### <a name="mac-os"></a>**Mac OS**
Abra seu terminal e navegue tooa diretório onde você planeja criar seu projeto Java. Instalar **brew** e **Maven** inserindo Olá comandos a seguir: 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

Para obter orientações detalhadas sobre como instalar e configurar o ambiente Java e Maven, vá Olá [compilar um aplicativo usando o SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), selecione **Java**, selecione **MacOS**e, em seguida, execute Olá instruções detalhadas para configurar o Java e Maven na etapa 1.2 e 1.3.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
Abra seu terminal e navegue tooa diretório onde você planeja criar seu projeto Java. Instalar **Maven** inserindo Olá comandos a seguir:

```bash
sudo apt-get install maven
```

Para obter orientações detalhadas sobre como instalar e configurar o ambiente Java e Maven, vá Olá [compilar um aplicativo usando o SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), selecione **Java**, selecione **Ubuntu**e, em seguida, execute Olá instruções detalhadas para configurar o Java e Maven na etapa 1.2, 1.3 e 1.4.

### <a name="windows"></a>**Windows**
Instalar [Maven](https://maven.apache.org/download.cgi) usando o instalador oficial hello. Use Maven toohelp gerenciar dependências, compilar, testar e executar seu projeto Java. Para obter orientações detalhadas sobre como instalar e configurar o ambiente Java e Maven, vá Olá [compilar um aplicativo usando o SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), selecione **Java**, selecione Windows e, em seguida, execute Olá instruções detalhadas para Configurando o Java e Maven na etapa 1.2 e 1.3.

## <a name="create-sqldbsample-project"></a>Criar projeto SqlDbSample

1. No console de comando de saudação (como Bash), crie um projeto Maven. 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. Digite **Y** e clique em **Enter**.
3. Altere os diretórios para seu projeto recém-criado.

   ```bash
   cd SqlDbSamples
   ```

4. Usando seu editor favorito, abra o arquivo de pom.xml de saudação na pasta do projeto. 

5. Adicione hello Microsoft JDBC Driver para o projeto do SQL Server dependência tooyour Maven abrindo o editor de texto favorito e copiando e colando Olá linhas seguintes no arquivo pom.xml. Não substitua valores existentes de saudação preenchida preenchidos no arquivo hello. Olá dependência JDBC deve ser colado em Olá maior (seção "dependências").   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. Especifica versão de saudação do projeto de saudação do Java toocompile contra adicionando Olá após a seção "propriedades" no arquivo de pom.xml Olá após a seção de "dependências" Olá. 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. Adicione a seguinte hello "criar" seção em Olá pom.xml arquivo após hello "propriedades" seção toosupport arquivos de manifesto no jars.       

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
8. Salve e feche o arquivo de pom.xml hello.
9. Abrir o arquivo de App.java hello (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) e substitua o conteúdo de saudação com hello conteúdo a seguir. Substitua o nome do grupo de failover Olá pelo nome de Olá para o grupo de failover. Se você tiver alterado os valores hello por nome de banco de dados hello, usuário ou senha, altere esses valores também.

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
6. Salve e feche o arquivo de App.java hello.

## <a name="compile-and-run-hello-sqldbsample-project"></a>Compilar e executar Olá SqlDbSample projeto

1. No console de comando hello, execute o comando de toofollowing.

   ```bash
   mvn package
   ```
2. Quando terminar, execute Olá aplicativo de hello toorun de comando (ele é executado por aproximadamente 1 hora, a menos que você pare manualmente) a seguir:

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a>Executar o treinamento de recuperação de desastre

1. Chame o failover manual do grupo de failover. 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. Observe Olá resultados de aplicativo durante o failover. Algumas inserções falharem enquanto atualiza Olá cache DNS.     

3. Descubra qual função seu servidor de recuperação de desastre executando.

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. Failback.

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. Observe Olá resultados de aplicativo durante o failback. Algumas inserções falharem enquanto atualiza Olá cache DNS.     

6. Descubra qual função seu servidor de recuperação de desastre executando.

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a>Próximas etapas 

Para saber mais, confira [Grupos de failover e replicação geográfica ativa](sql-database-geo-replication-overview.md).
