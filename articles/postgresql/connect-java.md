---
title: Conectar-se ao Banco de Dados do Azure para PostgreSQL usando Java | Microsoft Docs
description: "Este guia de início rápido fornece um exemplo de código Java que você pode usar para se conectar e consultar dados do Banco de Dados do Azure para PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 730a3f464b4437c260d09abc026a186a0e26293c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-java-to-connect-and-query-data"></a><span data-ttu-id="3f3d6-103">Banco de dados do Azure para PostgreSQL: usar Java para se conectar e consultar dados</span><span class="sxs-lookup"><span data-stu-id="3f3d6-103">Azure Database for PostgreSQL: Use Java to connect and query data</span></span>
<span data-ttu-id="3f3d6-104">Este guia de início rápido demonstra como se conectar a um banco de dados do Azure para PostgreSQL usando aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="3f3d6-105">Ele mostra como usar instruções SQL para consultar, inserir, atualizar e excluir dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="3f3d6-106">As etapas neste artigo pressupõem que você está familiarizado com o desenvolvimento usando o Java e que começou recentemente a trabalhar com o Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-106">The steps in this article assume that you are familiar with developing using Java, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f3d6-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3f3d6-107">Prerequisites</span></span>
<span data-ttu-id="3f3d6-108">Este guia de início rápido usa os recursos criados em um destes guias como ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="3f3d6-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="3f3d6-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="3f3d6-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="3f3d6-110">Criar Banco de dados - CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3f3d6-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="3f3d6-111">Você também precisará:</span><span class="sxs-lookup"><span data-stu-id="3f3d6-111">You also need to:</span></span>
- <span data-ttu-id="3f3d6-112">Baixar o [Driver JDBC PostgreSQL](https://jdbc.postgresql.org/download.html) correspondente à versão do Java e o Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-112">Download the [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and the Java Development Kit.</span></span>
- <span data-ttu-id="3f3d6-113">Incluir o arquivo jar do JDBC PostgreSQL (por exemplo, postgresql-42.1.1.jar) no classpath do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-113">Include the PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="3f3d6-114">Para saber mais, confira [detalhes de classpath](https://jdbc.postgresql.org/documentation/head/classpath.html).</span><span class="sxs-lookup"><span data-stu-id="3f3d6-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="3f3d6-115">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="3f3d6-115">Get connection information</span></span>
<span data-ttu-id="3f3d6-116">Obtenha as informações de conexão necessárias para se conectar ao Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-116">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="3f3d6-117">Você precisa das credenciais de logon e do nome do servidor totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-117">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="3f3d6-118">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3f3d6-118">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3f3d6-119">No menu à esquerda no Portal do Azure, clique em **Todos os recursos** e pesquise pelo servidor que você criou, como **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-119">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="3f3d6-120">Clique no nome do servidor **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-120">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="3f3d6-121">Selecione a página **Visão geral** do servidor.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-121">Select the server's **Overview** page.</span></span> <span data-ttu-id="3f3d6-122">Anote o **Nome do servidor** e o **Nome de logon de administrador do servidor**.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-122">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="3f3d6-123">![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="3f3d6-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="3f3d6-124">Se você se esquecer das informações de logon do servidor, navegue até a página **Visão Geral** para exibir o nome de logon do Administrador do servidor e, se necessário, redefinir a senha.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-124">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="3f3d6-125">Conectar-se, criar tabela e inserir dados</span><span class="sxs-lookup"><span data-stu-id="3f3d6-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="3f3d6-126">Use o código a seguir para se conectar e carregar os dados usando a função com uma instrução SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-126">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="3f3d6-127">Os métodos [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html) e [executeQuery ()](https://jdbc.postgresql.org/documentation/head/query.html) são usados para se conectar, descartar e criar a tabela.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-127">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, drop, and create the table.</span></span> <span data-ttu-id="3f3d6-128">O objeto [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) é usado para criar os comandos insert, com setString() e setInt() para associar os valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-128">The [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="3f3d6-129">O método [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) executa o comando para cada conjunto de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs the command for each set of parameters.</span></span> 

<span data-ttu-id="3f3d6-130">Substitua os parâmetros host, database, user e password pelos valores que você especificou quando criou seu próprio servidor e banco de dados.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-130">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
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
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="read-data"></a><span data-ttu-id="3f3d6-131">Ler dados</span><span class="sxs-lookup"><span data-stu-id="3f3d6-131">Read data</span></span>
<span data-ttu-id="3f3d6-132">Use o código a seguir para ler os dados com uma instrução SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-132">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="3f3d6-133">Os métodos [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement](https://jdbc.postgresql.org/documentation/head/query.html) e [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) são usados para se conectar, criar e executar a instrução select.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-133">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, create, and run the select statement.</span></span> <span data-ttu-id="3f3d6-134">Os resultados são processados usando um objeto [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html).</span><span class="sxs-lookup"><span data-stu-id="3f3d6-134">The results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="3f3d6-135">Substitua os parâmetros host, database, user e password pelos valores que você especificou quando criou seu próprio servidor e banco de dados.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-135">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
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
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="3f3d6-136">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="3f3d6-136">Update data</span></span>
<span data-ttu-id="3f3d6-137">Use o código a seguir para alterar os dados com uma instrução SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-137">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="3f3d6-138">Os métodos [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html) e [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) são usados para se conectar, preparar e executar a instrução select.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-138">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the update statement.</span></span> 

<span data-ttu-id="3f3d6-139">Substitua os parâmetros host, database, user e password pelos valores que você especificou quando criou seu próprio servidor e banco de dados.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-139">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```
## <a name="delete-data"></a><span data-ttu-id="3f3d6-140">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="3f3d6-140">Delete data</span></span>
<span data-ttu-id="3f3d6-141">Use o código a seguir para remover dados com uma instrução SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-141">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="3f3d6-142">Os métodos [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html) e [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) são usados para se conectar, preparar e executar a instrução select.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-142">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the delete statement.</span></span> 

<span data-ttu-id="3f3d6-143">Substitua os parâmetros host, database, user e password pelos valores que você especificou quando criou seu próprio servidor e banco de dados.</span><span class="sxs-lookup"><span data-stu-id="3f3d6-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="3f3d6-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f3d6-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3f3d6-145">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="3f3d6-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
