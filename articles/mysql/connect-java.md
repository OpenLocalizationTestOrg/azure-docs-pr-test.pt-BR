---
title: "TooAzure banco de dados de conexão para MySQL usando Java | Microsoft Docs"
description: "Este guia de início rápido fornece um exemplo de código Java, você pode usar tooconnect e consultar dados de um banco de dados do Azure para o banco de dados MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.devlang: java
ms.date: 06/20/2017
ms.openlocfilehash: d584b5491d29700b36fae26800c59d93ceb3e265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="0f1ae-103">Banco de dados do Azure para MySQL: usar Java tooconnect e consultar dados</span><span class="sxs-lookup"><span data-stu-id="0f1ae-103">Azure Database for MySQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="0f1ae-104">Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para MySQL usando um aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="0f1ae-105">Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="0f1ae-106">Olá etapas neste artigo presumem que você esteja familiarizado com o desenvolvimento usando o Java, e que você é novo tooworking com o banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f1ae-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0f1ae-107">Prerequisites</span></span>
<span data-ttu-id="0f1ae-108">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="0f1ae-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="0f1ae-109">Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0f1ae-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="0f1ae-110">Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0f1ae-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="0f1ae-111">Você também precisará:</span><span class="sxs-lookup"><span data-stu-id="0f1ae-111">You also need to:</span></span>
- <span data-ttu-id="0f1ae-112">Baixar o driver JDBC Olá [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span><span class="sxs-lookup"><span data-stu-id="0f1ae-112">Download hello JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="0f1ae-113">Inclua arquivo jar do JDBC hello (por exemplo mysql-conector-java-5.1.42-bin.jar) para o classpath do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-113">Include hello JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="0f1ae-114">Se você tiver problemas com isso, confira as especificações de caminho de classe, como [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) ou [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html) na documentação do seu ambiente</span><span class="sxs-lookup"><span data-stu-id="0f1ae-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="0f1ae-115">Certifique-se de que seu banco de dados do Azure para segurança de conexão MySQL é configurado com firewall Olá aberto e as configurações de SSL ajustada para tooconnect seu aplicativo com êxito.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-115">Ensure your Azure Database for MySQL connection security is configured with hello firewall opened and SSL settings adjusted for your application tooconnect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="0f1ae-116">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="0f1ae-116">Get connection information</span></span>
<span data-ttu-id="0f1ae-117">Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="0f1ae-118">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="0f1ae-119">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0f1ae-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0f1ae-120">No painel esquerdo do hello, clique em **todos os recursos**e em seguida, procure o servidor Olá que você criou (por exemplo, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="0f1ae-120">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="0f1ae-121">Clique em nome do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-121">Click hello server name.</span></span>
4. <span data-ttu-id="0f1ae-122">Servidor de saudação selecione **propriedades** página.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="0f1ae-123">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="0f1ae-124">![Nome do servidor do Banco de Dados do Azure para MySQL](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="0f1ae-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="0f1ae-125">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="0f1ae-126">Conectar-se, criar tabela e inserir dados</span><span class="sxs-lookup"><span data-stu-id="0f1ae-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="0f1ae-127">Saudação de uso seguintes código tooconnect e carga Olá dados usando a função hello com um **inserir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-127">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="0f1ae-128">Olá [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) método é usado tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-128">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="0f1ae-129">Métodos [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) e execute () são usado toodrop e criar tabela hello.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used toodrop and create hello table.</span></span> <span data-ttu-id="0f1ae-130">o objeto de prepareStatement de saudação é usado toobuild Olá os comandos insert, com valores de parâmetro de saudação toobind setString() e setInt().</span><span class="sxs-lookup"><span data-stu-id="0f1ae-130">hello prepareStatement object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="0f1ae-131">Método executeUpdate() executa o comando de saudação para cada conjunto de valores dos parâmetros tooinsert hello.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-131">Method executeUpdate() runs hello command for each set of parameters tooinsert hello values.</span></span> 

<span data-ttu-id="0f1ae-132">Substitua os valores hello que você especificou quando criou seu próprio servidor e banco de dados host hello, banco de dados, usuário e parâmetros de senha.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-132">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Drop previous table of same name if one exists.
                Statement statement = connection.createStatement();
                statement.execute("DROP TABLE IF EXISTS inventory;");
                System.out.println("Finished dropping table (if existed).");
    
                // Create table.
                statement.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
                System.out.println("Created table.");
                
                // Insert some data into table.
                int nRowsInserted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO inventory (name, quantity) VALUES (?, ?);");
                preparedStatement.setString(1, "banana");
                preparedStatement.setInt(2, 150);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "orange");
                preparedStatement.setInt(2, 154);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "apple");
                preparedStatement.setInt(2, 100);
                nRowsInserted += preparedStatement.executeUpdate();
                System.out.println(String.format("Inserted %d row(s) of data.", nRowsInserted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="read-data"></a><span data-ttu-id="0f1ae-133">Ler dados</span><span class="sxs-lookup"><span data-stu-id="0f1ae-133">Read data</span></span>
<span data-ttu-id="0f1ae-134">Dados de saudação tooread com código a seguir de saudação Use um **selecione** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-134">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="0f1ae-135">Olá [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) método é usado tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-135">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="0f1ae-136">Olá métodos [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) e ExecuteQuery () são usado tooconnect e execute a instrução select hello.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-136">hello methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used tooconnect and run hello select statement.</span></span> <span data-ttu-id="0f1ae-137">resultados de saudação são processados usando um [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) objeto.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-137">hello results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="0f1ae-138">Substitua os valores hello que você especificou quando criou seu próprio servidor e banco de dados host hello, banco de dados, usuário e parâmetros de senha.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-138">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
    
                Statement statement = connection.createStatement();
                ResultSet results = statement.executeQuery("SELECT * from inventory;");
                while (results.next())
                {
                    String outputString = 
                        String.format(
                            "Data row = (%s, %s, %s)",
                            results.getString(1),
                            results.getString(2),
                            results.getString(3));
                    System.out.println(outputString);
                }
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="0f1ae-139">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="0f1ae-139">Update data</span></span>
<span data-ttu-id="0f1ae-140">Dados de saudação toochange com código a seguir de saudação Use um **atualização** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-140">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="0f1ae-141">Olá [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) método é usado tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-141">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="0f1ae-142">Olá métodos [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) e executeUpdate() são usada tooprepare e execute a instrução de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-142">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="0f1ae-143">Substitua os valores hello que você especificou quando criou seu próprio servidor e banco de dados host hello, banco de dados, usuário e parâmetros de senha.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }
        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="delete-data"></a><span data-ttu-id="0f1ae-144">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="0f1ae-144">Delete data</span></span>
<span data-ttu-id="0f1ae-145">Código a seguir de saudação de uso tooremove dados com um **excluir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-145">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="0f1ae-146">Olá [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) método é usado tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-146">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span>  <span data-ttu-id="0f1ae-147">Olá métodos [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) e executeUpdate() são usada tooprepare e execute a instrução de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-147">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="0f1ae-148">Substitua os valores hello que você especificou quando criou seu próprio servidor e banco de dados host hello, banco de dados, usuário e parâmetros de senha.</span><span class="sxs-lookup"><span data-stu-id="0f1ae-148">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";
        
        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="0f1ae-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0f1ae-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0f1ae-150">Migrar seu banco de dados de MySQL tooAzure banco de dados para MySQL usando dump e restore</span><span class="sxs-lookup"><span data-stu-id="0f1ae-150">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
