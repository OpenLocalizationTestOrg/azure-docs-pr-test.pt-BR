---
title: Conectar-se ao Banco de Dados do Azure para MySQL do C# | Microsoft Docs
description: "Este guia de início rápido fornece um exemplo de código em C# (.NET) que você pode usar para se conectar e consultar dados do Banco de Dados do Azure para MySQL."
services: MySQL
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: MySQL-database
ms.custom: mvc
ms.devlang: csharp
ms.topic: hero-article
ms.date: 07/10/2017
ms.openlocfilehash: f1488f6b4a240165c71c95f759af73d6b9fd7bfe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-database-for-mysql-use-net-c-to-connect-and-query-data"></a><span data-ttu-id="a49d9-103">Banco de Dados do Azure para MySQL: usar .NET (C#) para se conectar e consultar dados</span><span class="sxs-lookup"><span data-stu-id="a49d9-103">Azure Database for MySQL: Use .NET (C#) to connect and query data</span></span>
<span data-ttu-id="a49d9-104">Este guia de início rápido demonstra como se conectar a um Banco de Dados do Azure para MySQL usando um aplicativo C#.</span><span class="sxs-lookup"><span data-stu-id="a49d9-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a C# application.</span></span> <span data-ttu-id="a49d9-105">Ele mostra como usar instruções SQL para consultar, inserir, atualizar e excluir dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a49d9-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="a49d9-106">As etapas neste artigo pressupõem que você esteja familiarizado com o desenvolvimento usando C# e começou recentemente a trabalhar com o Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="a49d9-106">The steps in this article assume that you are familiar with developing using C#, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a49d9-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a49d9-107">Prerequisites</span></span>
<span data-ttu-id="a49d9-108">Este guia de início rápido usa os recursos criados em um destes guias como ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="a49d9-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="a49d9-109">Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a49d9-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="a49d9-110">Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a49d9-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="a49d9-111">Você também precisará:</span><span class="sxs-lookup"><span data-stu-id="a49d9-111">You also need to:</span></span>
- <span data-ttu-id="a49d9-112">Instalar o [.NET](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="a49d9-112">Install [.NET](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="a49d9-113">Executar as etapas no artigo vinculado para instalar o .NET especificamente para sua plataforma (Windows, Ubuntu Linux ou macOS).</span><span class="sxs-lookup"><span data-stu-id="a49d9-113">Follow the steps in the linked article to install .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="a49d9-114">Instalar o [Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a49d9-114">Install [Visual Studio](https://www.visualstudio.com/downloads/).</span></span>
- <span data-ttu-id="a49d9-115">Instalar o [Driver ODBC para MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span><span class="sxs-lookup"><span data-stu-id="a49d9-115">Install [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="a49d9-116">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="a49d9-116">Get connection information</span></span>
<span data-ttu-id="a49d9-117">Obtenha as informações de conexão necessárias para se conectar ao Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="a49d9-117">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="a49d9-118">Você precisa das credenciais de logon e do nome do servidor totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="a49d9-118">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="a49d9-119">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a49d9-119">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a49d9-120">No menu à esquerda no Portal do Azure, clique em **Todos os recursos** e pesquise pelo servidor que você criou, como **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="a49d9-120">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="a49d9-121">Clique no nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="a49d9-121">Click the server name.</span></span>
4. <span data-ttu-id="a49d9-122">Selecione a página **Propriedades** do servidor.</span><span class="sxs-lookup"><span data-stu-id="a49d9-122">Select the server's **Properties** page.</span></span> <span data-ttu-id="a49d9-123">Anote o **Nome do servidor** e o **Nome de logon de administrador do servidor**.</span><span class="sxs-lookup"><span data-stu-id="a49d9-123">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="a49d9-124">![Nome do servidor do Banco de Dados do Azure para MySQL](./media/connect-csharp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="a49d9-124">![Azure Database for MySQL server name](./media/connect-csharp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="a49d9-125">Se você se esquecer das informações de logon do servidor, navegue até a página **Visão Geral** para exibir o nome de logon do Administrador do servidor e, se necessário, redefinir a senha.</span><span class="sxs-lookup"><span data-stu-id="a49d9-125">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="a49d9-126">Conectar-se, criar tabela e inserir dados</span><span class="sxs-lookup"><span data-stu-id="a49d9-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="a49d9-127">Use o código a seguir para se conectar e carregar os dados usando instruções SQL **CREATE TABLE** e **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="a49d9-127">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="a49d9-128">O código usa a classe ODBC com o método [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) para estabelecer uma conexão com o MySQL.</span><span class="sxs-lookup"><span data-stu-id="a49d9-128">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="a49d9-129">Em seguida, o código usa o método [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), define a propriedade CommandText e chama o método [ExecuteNonQuery ()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) para executar os comandos do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a49d9-129">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets the CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) to run the database commands.</span></span> 

<span data-ttu-id="a49d9-130">Substitua os parâmetros Host, DBName, User e Password pelos valores que você especificou quando criou o servidor e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a49d9-130">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;

namespace driver
{
    class MySQLCreate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "DROP TABLE IF EXISTS inventory;";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished dropping table (if existed)");

            command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished creating table");

            command.CommandText =
                String.Format(
                    @"INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                    INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                    INSERT INTO inventory (name, quantity) VALUES ({4}, {5});",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }

    }
}

```

## <a name="read-data"></a><span data-ttu-id="a49d9-131">Ler dados</span><span class="sxs-lookup"><span data-stu-id="a49d9-131">Read data</span></span>

<span data-ttu-id="a49d9-132">Use o código a seguir para conectar-se e ler os dados usando uma instrução SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="a49d9-132">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="a49d9-133">O código usa a classe ODBC com o método [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) para estabelecer uma conexão com o MySQL.</span><span class="sxs-lookup"><span data-stu-id="a49d9-133">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="a49d9-134">Em seguida, o código usa o método [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) e o método [ExecuteReader ()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) para executar os comandos de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a49d9-134">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) and method [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) to run the database commands.</span></span> <span data-ttu-id="a49d9-135">Em seguida, o código usa [Read](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) para acessar os registros nos resultados.</span><span class="sxs-lookup"><span data-stu-id="a49d9-135">Next the code uses [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) to advance to the records in the results.</span></span> <span data-ttu-id="a49d9-136">Em seguida, o código usa GetInt32 e GetString para analisar os valores do registro.</span><span class="sxs-lookup"><span data-stu-id="a49d9-136">Then the code uses GetInt32 and GetString to parse the values in the record.</span></span>

<span data-ttu-id="a49d9-137">Substitua os parâmetros Host, DBName, User e Password pelos valores que você especificou quando criou o servidor e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a49d9-137">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;


namespace driver
{
    class MySQLRead
    {

        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "SELECT * FROM inventory;";

            var reader = command.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(
                    string.Format(
                        "Reading from table=({0}, {1}, {2})",
                        reader.GetInt32(0).ToString(),
                        reader.GetString(1),
                        reader.GetInt32(2).ToString()
                        )
                    );
            }

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}


```

## <a name="update-data"></a><span data-ttu-id="a49d9-138">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="a49d9-138">Update data</span></span>
<span data-ttu-id="a49d9-139">Use o código a seguir para conectar-se e ler os dados usando uma instrução SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="a49d9-139">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="a49d9-140">O código usa a classe ODBC com o método [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) para estabelecer uma conexão com o MySQL.</span><span class="sxs-lookup"><span data-stu-id="a49d9-140">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="a49d9-141">Em seguida, o código usa o método [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), define a propriedade CommandText e chama o método [ExecuteNonQuery ()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) para executar os comandos do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a49d9-141">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets the CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) to run the database commands.</span></span>

<span data-ttu-id="a49d9-142">Substitua os parâmetros Host, DBName, User e Password pelos valores que você especificou quando criou o servidor e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a49d9-142">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLUpdate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("UPDATE inventory SET quantity = {0} WHERE name = {1};",
                200,
                "\'banana\'"
                );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows updated={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}



```


## <a name="delete-data"></a><span data-ttu-id="a49d9-143">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="a49d9-143">Delete data</span></span>
<span data-ttu-id="a49d9-144">Use o código a seguir para conectar-se e excluir os dados usando uma instrução SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="a49d9-144">Use the following code to connect and delete the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="a49d9-145">O código usa a classe ODBC com o método [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) para estabelecer uma conexão com o MySQL.</span><span class="sxs-lookup"><span data-stu-id="a49d9-145">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="a49d9-146">Em seguida, o código usa o método [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), define a propriedade CommandText e chama o método [ExecuteNonQuery ()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) para executar os comandos do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a49d9-146">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets the CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) to run the database commands.</span></span>

<span data-ttu-id="a49d9-147">Substitua os parâmetros Host, DBName, User e Password pelos valores que você especificou quando criou o servidor e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a49d9-147">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLDelete
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
                String.Format("DELETE FROM inventory WHERE name = {0};",
                    "\'orange\'");
            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows deleted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="a49d9-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a49d9-148">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a49d9-149">Migrar seu banco de dados MySQL para o Banco de Dados do Azure para MySQL usando despejo e restauração</span><span class="sxs-lookup"><span data-stu-id="a49d9-149">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
