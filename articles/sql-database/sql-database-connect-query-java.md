---
title: aaaUse Java tooquery banco de dados do SQL Azure | Microsoft Docs
description: "Este tópico mostra como toouse Java toocreate um programa que se conecta tooan banco de dados do SQL Azure e a consulta usando instruções Transact-SQL."
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: andrela
ms.openlocfilehash: f014edbe38ca0e7b6e43f4eb4d2e53d3561bf3e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-java-tooquery-an-azure-sql-database"></a>Usar Java tooquery um banco de dados do SQL Azure

Este guia rápido demonstra como toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan SQL do Azure do banco de dados e, em seguida, usar dados de tooquery de instruções Transact-SQL.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete rápida nesse tutorial de início, certifique-se de ter Olá pré-requisitos a seguir:

- Um banco de dados SQL do Azure. Esse início rápido usa recursos de saudação criados em um desses inícios rápidos: 

   - [Criar Banco de dados - Portal](sql-database-get-started-portal.md)
   - [Criar Banco de dados - CLI](sql-database-get-started-cli.md)
   - [Criar Banco de dados - PowerShell](sql-database-get-started-powershell.md)

- Um [regra de firewall de nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de saudação do computador Olá usar para este tutorial de início rápido.

- Você instalou o Java e o software relacionado para seu sistema operacional.

    - **MacOS**: instale o Homebrew e o Java e, em seguida, instale o Maven. Veja a [Etapa 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).
    - **Ubuntu**: instalar Olá Java Development Kit e Maven. Confira as [etapas 1.2, 1.3 e 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).
    - **Windows**: instalar Olá Java Development Kit e Maven. Veja a [Etapa 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).    

## <a name="sql-server-connection-information"></a>Informações de conexão do servidor SQL

Obter Olá conexão informações necessárias tooconnect toohello SQL Azure banco de dados. Será necessário o nome totalmente qualificado do servidor de saudação, nome do banco de dados e informações de logon em procedimentos Avançar hello.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página. 
3. Em Olá **visão geral** para seu banco de dados, examine o nome totalmente qualificado do servidor de saudação conforme Olá a imagem a seguir: você pode focalizar Olá toobring de nome de servidor backup Olá **clique toocopy** opção.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se você esquecer suas informações de logon de servidor, navegue toohello banco de dados do SQL server página tooview Olá administrador nome do servidor.  Se necessário, Olá redefinição da senha.     

## <a name="create-maven-project-and-dependencies"></a>**Como criar dependências e projeto Maven**
1. De Olá terminal, crie um novo projeto de Maven chamado **sqltest**. 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. Digite **Y** quando solicitado.
3. Altere o diretório muito**sqltest** e abra ***pom.xml*** com seu editor de texto favorito.  Adicionar Olá **Microsoft JDBC Driver para SQL Server** Olá dependências do projeto tooyour usando o seguinte código:

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. Também na ***pom.xml***, adicionar Olá projeto tooyour de propriedades a seguir.  Se você não tiver uma seção de propriedades, você pode adicioná-lo depois de dependências de saudação.

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. Salve e feche o ***pom.xml***.

## <a name="insert-code-tooquery-sql-database"></a>Insira o banco de dados SQL do código tooquery

1. Você já deve ter um arquivo chamado ***App.java*** no seu projeto Maven localizado em:  ..\sqltest\src\main\java\com\sqlsamples\App.java

2. Abra o arquivo hello e substituir seu conteúdo com os seguintes Olá código e adicione os valores apropriados para seu servidor, banco de dados, usuário e senha hello.

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect toodatabase
           String hostName = "your_server.database.windows.net";
           String dbName = "your_database";
           String user = "your_username";
           String password = "your_password";
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
           Connection connection = null;

           try {
                   connection = DriverManager.getConnection(url);
                   String schema = connection.getSchema();
                   System.out.println("Successful connection - Schema: " + schema);

                   System.out.println("Query data example:");
                   System.out.println("=========================================");

                   // Create and execute a SELECT SQL statement.
                   String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                       + "FROM [SalesLT].[ProductCategory] pc "  
                       + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                   try (Statement statement = connection.createStatement();
                       ResultSet resultSet = statement.executeQuery(selectSql)) {

                           // Print results from select statement
                           System.out.println("Top 20 categories:");
                           while (resultSet.next())
                           {
                               System.out.println(resultSet.getString(1) + " "
                                   + resultSet.getString(2));
                           }
                    connection.close();
                   }                   
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-hello-code"></a>Executar o código de saudação

1. No prompt de comando hello, execute Olá comandos a seguir:

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. Verifique se que 20 linhas de saudação principais são retornadas e, em seguida, feche a janela do aplicativo hello.


## <a name="next-steps"></a>Próximas etapas
- [Projetar seu primeiro banco de dados SQL do Azure](sql-database-design-first-database.md)
- [Microsoft JDBC Driver para SQL Server](https://github.com/microsoft/mssql-jdbc)
- [Relatar problemas/fazer perguntas](https://github.com/microsoft/mssql-jdbc/issues)

