---
title: "TooAzure banco de dados de conexão para PostgreSQL do c# | Microsoft Docs"
description: "Este guia de início rápido fornece um c# (.NET) exemplo de código você pode usar tooconnect e consultar dados do banco de dados PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: csharp
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 5ba7426f8ad263193cdb208b3531da0ceff181dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="1bf23-103">Banco de dados do Azure para PostgreSQL: dados de consulta e tooconnect Use .NET (c#)</span><span class="sxs-lookup"><span data-stu-id="1bf23-103">Azure Database for PostgreSQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="1bf23-104">Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para PostgreSQL usando um aplicativo c#.</span><span class="sxs-lookup"><span data-stu-id="1bf23-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="1bf23-105">Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bf23-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="1bf23-106">Olá etapas neste artigo presumem que você esteja familiarizado com o desenvolvimento usando c#, e que você é novo tooworking com o banco de dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1bf23-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bf23-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1bf23-107">Prerequisites</span></span>
<span data-ttu-id="1bf23-108">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="1bf23-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="1bf23-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="1bf23-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="1bf23-110">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="1bf23-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="1bf23-111">Você também precisará:</span><span class="sxs-lookup"><span data-stu-id="1bf23-111">You also need to:</span></span>
- <span data-ttu-id="1bf23-112">Instalar o [.NET Framework](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="1bf23-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="1bf23-113">Siga as etapas de Olá Olá vinculado artigo tooinstall .NET especificamente para a plataforma (Windows, Ubuntu Linux ou macOS).</span><span class="sxs-lookup"><span data-stu-id="1bf23-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="1bf23-114">Instalar [Visual Studio](https://www.visualstudio.com/downloads/) ou código tootype e edição de código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1bf23-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code tootype and edit code.</span></span>
- <span data-ttu-id="1bf23-115">Instalar a biblioteca [Npgsql](http://www.npgsql.org/doc/index.html) conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="1bf23-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="1bf23-116">Instalar referências Npgsql referências em sua solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1bf23-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="1bf23-117">tooconnect de saudação c# tooPostgreSQL de aplicativo, use a biblioteca ADO.NET de código-fonte aberto de Olá chamada Npgsql.</span><span class="sxs-lookup"><span data-stu-id="1bf23-117">tooconnect from hello C# application tooPostgreSQL, use hello open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="1bf23-118">NuGet ajuda a baixar e gerenciar referências Olá facilmente.</span><span class="sxs-lookup"><span data-stu-id="1bf23-118">NuGet helps download and manage hello references easily.</span></span>

1. <span data-ttu-id="1bf23-119">Crie uma nova solução C# ou abra uma existente:</span><span class="sxs-lookup"><span data-stu-id="1bf23-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="1bf23-120">No Visual Studio, crie uma solução clicando no menu Arquivo **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="1bf23-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="1bf23-121">Na caixa de diálogo Novo projeto de hello, expanda **modelos** > **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="1bf23-121">In hello New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="1bf23-122">Escolha um modelo apropriado, como **Aplicativo de Console (.NET Core)**.</span><span class="sxs-lookup"><span data-stu-id="1bf23-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="1bf23-123">Use Olá Npgsql tooinstall Nuget Package Manager:</span><span class="sxs-lookup"><span data-stu-id="1bf23-123">Use hello Nuget Package Manager tooinstall Npgsql:</span></span>
   - <span data-ttu-id="1bf23-124">Clique em Olá **ferramentas** menu > **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="1bf23-124">Click hello **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="1bf23-125">Em Olá **Package Manager Console**, tipo`Install-Package Npgsql`</span><span class="sxs-lookup"><span data-stu-id="1bf23-125">In hello **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="1bf23-126">Olá instalar comando downloads Olá Npgsql.dll e os assemblies relacionados e adiciona-las como dependências em solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bf23-126">hello install command downloads hello Npgsql.dll and related assemblies and adds them as dependencies in hello solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="1bf23-127">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="1bf23-127">Get connection information</span></span>
<span data-ttu-id="1bf23-128">Obter Olá conexão informações necessárias tooconnect toohello banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1bf23-128">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="1bf23-129">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="1bf23-129">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="1bf23-130">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1bf23-130">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1bf23-131">No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e pesquisa para o servidor de saudação que você criou, como **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="1bf23-131">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="1bf23-132">Clique em nome do servidor de saudação **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="1bf23-132">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="1bf23-133">Servidor de saudação selecione **visão geral** página.</span><span class="sxs-lookup"><span data-stu-id="1bf23-133">Select hello server's **Overview** page.</span></span> <span data-ttu-id="1bf23-134">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="1bf23-134">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="1bf23-135">![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="1bf23-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="1bf23-136">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="1bf23-136">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="1bf23-137">Conectar-se, criar tabela e inserir dados</span><span class="sxs-lookup"><span data-stu-id="1bf23-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="1bf23-138">A seguir use Olá tooconnect de código e carregar Olá dados usando **CREATE TABLE** e **INSERT INTO** instruções SQL.</span><span class="sxs-lookup"><span data-stu-id="1bf23-138">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="1bf23-139">código de Olá usa a classe NpgsqlCommand com o método [Open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL uma conexão.</span><span class="sxs-lookup"><span data-stu-id="1bf23-139">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="1bf23-140">Em seguida, código de saudação usa o método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), define a propriedade CommandText de saudação e chama o método [ExecuteNonQuery ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun comandos de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bf23-140">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span> 

<span data-ttu-id="1bf23-141">Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bf23-141">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresCreate
    {
        // Obtain connection string information from hello portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4}; SSL Mode=Prefer; Trust Server Certificate=true",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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
                    @"
                                INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                                INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                                INSERT INTO inventory (name, quantity) VALUES ({4}, {5});
                            ",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="read-data"></a><span data-ttu-id="1bf23-142">Ler dados</span><span class="sxs-lookup"><span data-stu-id="1bf23-142">Read data</span></span>
<span data-ttu-id="1bf23-143">A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="1bf23-143">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="1bf23-144">código de Olá usa a classe NpgsqlCommand com o método [Open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL uma conexão.</span><span class="sxs-lookup"><span data-stu-id="1bf23-144">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="1bf23-145">Código de saudação usará o método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) e método [ExecuteReader ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun comandos de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bf23-145">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun hello database commands.</span></span> <span data-ttu-id="1bf23-146">Olá próximo código Use [Read](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello registros nos resultados da saudação.</span><span class="sxs-lookup"><span data-stu-id="1bf23-146">Next hello code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="1bf23-147">Em seguida, usa o código de saudação [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) e [getString ()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse valores hello registro hello.</span><span class="sxs-lookup"><span data-stu-id="1bf23-147">Then hello code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse hello values in hello record.</span></span>

<span data-ttu-id="1bf23-148">Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bf23-148">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresRead
    {
        // Obtain connection string information from hello portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="update-data"></a><span data-ttu-id="1bf23-149">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="1bf23-149">Update data</span></span>
<span data-ttu-id="1bf23-150">A seguir use Olá código tooconnect e ler Olá dados usando um **atualização** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="1bf23-150">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="1bf23-151">código de Olá usa a classe NpgsqlCommand com o método [Open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL uma conexão.</span><span class="sxs-lookup"><span data-stu-id="1bf23-151">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="1bf23-152">Em seguida, código de saudação usa o método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), define a propriedade CommandText de saudação e chama o método [ExecuteNonQuery ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun comandos de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bf23-152">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="1bf23-153">Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bf23-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresUpdate
    {
        // Obtain connection string information from hello portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="delete-data"></a><span data-ttu-id="1bf23-154">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="1bf23-154">Delete data</span></span>
<span data-ttu-id="1bf23-155">A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="1bf23-155">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="1bf23-156">código de Olá usa a classe NpgsqlCommand com o método [Open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL uma conexão.</span><span class="sxs-lookup"><span data-stu-id="1bf23-156">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="1bf23-157">Em seguida, código de saudação usa o método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), define a propriedade CommandText de saudação e chama o método [ExecuteNonQuery ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun comandos de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bf23-157">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="1bf23-158">Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bf23-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresDelete
    {
        // Obtain connection string information from hello portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="1bf23-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1bf23-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1bf23-160">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="1bf23-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
