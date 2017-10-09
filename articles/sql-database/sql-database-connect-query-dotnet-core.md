---
title: aaaUse .NET Core tooquery banco de dados do SQL Azure | Microsoft Docs
description: "Este tópico mostra como toouse .NET Core toocreate um programa que se conecta tooan banco de dados do SQL Azure e consultá-los usando instruções Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 2d10c407f44f43b6baa3bf337cdd1173d9c9c35f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-c-tooquery-an-azure-sql-database"></a>Use o .NET Core (c#) tooquery um banco de dados do SQL Azure

Este tutorial de início rápido demonstra como toouse [.NET Core](https://www.microsoft.com/net/) em Linux/Windows/macOS toocreate c# programa tooconnect tooan SQL Azure banco de dados e usar dados de tooquery de instruções Transact-SQL.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete rápido nesse tutorial de início, verifique se você tem o seguinte hello:

- Um banco de dados SQL do Azure. Esse início rápido usa recursos de saudação criados em um desses inícios rápidos: 

   - [Criar Banco de dados - Portal](sql-database-get-started-portal.md)
   - [Criar Banco de dados - CLI](sql-database-get-started-cli.md)
   - [Criar Banco de dados - PowerShell](sql-database-get-started-powershell.md)

- Um [regra de firewall de nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de saudação do computador Olá usar para este tutorial de início rápido.
- Você instalou [.NET Core para o sistema operacional](https://www.microsoft.com/net/core). 

## <a name="sql-server-connection-information"></a>Informações de conexão do servidor SQL

Obter Olá conexão informações necessárias tooconnect toohello SQL Azure banco de dados. Será necessário o nome totalmente qualificado do servidor de saudação, nome do banco de dados e informações de logon em procedimentos Avançar hello.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página. 
3. Em Olá **visão geral** página do banco de dados, examine Olá nome totalmente qualificado do servidor conforme Olá a imagem a seguir. Você pode focalizar Olá toobring de nome de servidor backup Olá **clique toocopy** opção. 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se você esquecer suas informações de logon do banco de dados SQL server, navegue toohello banco de dados do SQL server página tooview Olá administrador nome do servidor. Você pode redefinir a senha de saudação se necessário.

5. Clique em **Mostrar cadeias de conexão de banco de dados**.

6. Saudação de revisão completa **ADO.NET** cadeia de caracteres de conexão.

    ![Cadeia de conexão do ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> Você deve ter uma regra de firewall em vigor para o endereço IP público de saudação do computador Olá em que você executa este tutorial. Se você estiver em um computador diferente ou ter um endereço IP público diferente, crie um [regra de firewall de nível de servidor usando Olá portal do Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 
>
  
## <a name="create-a-new-net-project"></a>Criar um novo projeto .NET

1. Abra um prompt de comando e crie uma pasta chamada *sqltest*. Navegue até a pasta toohello é criado e executado Olá comando a seguir:

    ```
    dotnet new console
    ```

2. Abra ***sqltest.csproj*** com seu editor de texto favorito e adicione SqlClient como uma dependência usando Olá código a seguir:

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-tooquery-sql-database"></a>Insira o banco de dados SQL do código tooquery

1. Em seu ambiente de desenvolvimento ou editor de texto favorito, abra **Program.cs**

2. Substitua o conteúdo de saudação com hello seguinte código e adicionar os valores apropriados para seu servidor, banco de dados, usuário e senha hello.

```csharp
using System;
using System.Data.SqlClient;
using System.Text;

namespace sqltest
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.ReadLine();
        }
    }
}
```

## <a name="run-hello-code"></a>Executar o código de saudação

1. No prompt de comando hello, execute Olá comandos a seguir:

   ```csharp
   dotnet restore
   dotnet run
   ```

2. Verifique se que 20 linhas de saudação principais são retornadas e, em seguida, feche a janela do aplicativo hello.


## <a name="next-steps"></a>Próximas etapas

- [Introdução ao .NET Core no Windows/Linux/macOS usando a linha de comando Olá](/dotnet/core/tutorials/using-with-xplat-cli).
- Saiba como muito[se conectar e consultar um banco de dados do SQL Azure usando Olá .NET framework e Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).  
- Saiba como muito[criar seu primeiro banco de dados SQL do Azure usando o SSMS](sql-database-design-first-database.md) ou [criar seu primeiro banco de dados SQL do Azure usando o .NET](sql-database-design-first-database-csharp.md).
- Para saber mais sobre o .NET, veja a [documentação do .NET](https://docs.microsoft.com/dotnet/).
