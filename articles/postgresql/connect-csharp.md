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
# <a name="azure-database-for-postgresql-use-net-c-tooconnect-and-query-data"></a>Banco de dados do Azure para PostgreSQL: dados de consulta e tooconnect Use .NET (c#)
Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para PostgreSQL usando um aplicativo c#. Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação. Olá etapas neste artigo presumem que você esteja familiarizado com o desenvolvimento usando c#, e que você é novo tooworking com o banco de dados do Azure para PostgreSQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:
- [Criar Banco de dados - Portal](quickstart-create-server-database-portal.md)
- [Criar Banco de dados - CLI](quickstart-create-server-database-azure-cli.md)

Você também precisará:
- Instalar o [.NET Framework](https://www.microsoft.com/net/download). Siga as etapas de Olá Olá vinculado artigo tooinstall .NET especificamente para a plataforma (Windows, Ubuntu Linux ou macOS). 
- Instalar [Visual Studio](https://www.visualstudio.com/downloads/) ou código tootype e edição de código do Visual Studio.
- Instalar a biblioteca [Npgsql](http://www.npgsql.org/doc/index.html) conforme descrito abaixo.

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a>Instalar referências Npgsql referências em sua solução do Visual Studio
tooconnect de saudação c# tooPostgreSQL de aplicativo, use a biblioteca ADO.NET de código-fonte aberto de Olá chamada Npgsql. NuGet ajuda a baixar e gerenciar referências Olá facilmente.

1. Crie uma nova solução C# ou abra uma existente: 
   - No Visual Studio, crie uma solução clicando no menu Arquivo **Novo** > **Projeto**.
   - Na caixa de diálogo Novo projeto de hello, expanda **modelos** > **Visual C#**. 
   - Escolha um modelo apropriado, como **Aplicativo de Console (.NET Core)**.

2. Use Olá Npgsql tooinstall Nuget Package Manager:
   - Clique em Olá **ferramentas** menu > **NuGet Package Manager** > **Package Manager Console**.
   - Em Olá **Package Manager Console**, tipo`Install-Package Npgsql`
   - Olá instalar comando downloads Olá Npgsql.dll e os assemblies relacionados e adiciona-las como dependências em solução de saudação.

## <a name="get-connection-information"></a>Obter informações de conexão
Obter Olá conexão informações necessárias tooconnect toohello banco de dados PostgreSQL. Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e pesquisa para o servidor de saudação que você criou, como **mypgserver 20170401**.
3. Clique em nome do servidor de saudação **mypgserver 20170401**.
4. Servidor de saudação selecione **visão geral** página. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
 ![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-csharp/1-connection-string.png)
5. Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.

## <a name="connect-create-table-and-insert-data"></a>Conectar-se, criar tabela e inserir dados
A seguir use Olá tooconnect de código e carregar Olá dados usando **CREATE TABLE** e **INSERT INTO** instruções SQL. código de Olá usa a classe NpgsqlCommand com o método [Open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL uma conexão. Em seguida, código de saudação usa o método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), define a propriedade CommandText de saudação e chama o método [ExecuteNonQuery ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun comandos de banco de dados de saudação. 

Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação. 

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

## <a name="read-data"></a>Ler dados
A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL. código de Olá usa a classe NpgsqlCommand com o método [Open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL uma conexão. Código de saudação usará o método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) e método [ExecuteReader ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun comandos de banco de dados de saudação. Olá próximo código Use [Read](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello registros nos resultados da saudação. Em seguida, usa o código de saudação [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) e [getString ()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse valores hello registro hello.

Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação. 

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


## <a name="update-data"></a>Atualizar dados
A seguir use Olá código tooconnect e ler Olá dados usando um **atualização** instrução SQL. código de Olá usa a classe NpgsqlCommand com o método [Open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL uma conexão. Em seguida, código de saudação usa o método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), define a propriedade CommandText de saudação e chama o método [ExecuteNonQuery ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun comandos de banco de dados de saudação.

Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação. 

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


## <a name="delete-data"></a>Excluir dados
A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL. 

 código de Olá usa a classe NpgsqlCommand com o método [Open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL uma conexão. Em seguida, código de saudação usa o método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), define a propriedade CommandText de saudação e chama o método [ExecuteNonQuery ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun comandos de banco de dados de saudação.

Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação. 

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

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./howto-migrate-using-export-and-import.md)
