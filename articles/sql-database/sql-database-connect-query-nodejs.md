---
title: aaaUse Node. js tooquery banco de dados do SQL Azure | Microsoft Docs
description: "Este tópico mostra como toouse Node. js toocreate um programa que se conecta tooan banco de dados do SQL Azure e a consulta usando instruções Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 53f70e37-5eb4-400d-972e-dd7ea0caacd4
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 3870130a486c218eafeb9cf792a4275de7fd6551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a>Use o Node. js tooquery um banco de dados do SQL Azure

Este tutorial de início rápido demonstra como toouse [Node.js](https://nodejs.org/en/) toocreate tooan de tooconnect um programa SQL do Azure do banco de dados e usar dados de tooquery de instruções Transact-SQL.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete rápido nesse tutorial de início, verifique se você tem o seguinte hello:

- Um banco de dados SQL do Azure. Esse início rápido usa recursos de saudação criados em um desses inícios rápidos: 

   - [Criar Banco de dados - Portal](sql-database-get-started-portal.md)
   - [Criar Banco de dados - CLI](sql-database-get-started-cli.md)
   - [Criar Banco de dados - PowerShell](sql-database-get-started-powershell.md)

- Um [regra de firewall de nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de saudação do computador Olá usar para este tutorial de início rápido.
- Você instalou o Node.js e o software relacionado para seu sistema operacional.
    - **MacOS**: instalar o Homebrew e Node. js e, em seguida, instalar o driver ODBC hello e SQLCMD. Veja a [Etapa 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).
    - **Ubuntu**: instalar o Node. js e, em seguida, instalar o driver ODBC hello e SQLCMD. Veja a [Etapa 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).
    - **Windows**: instalar Chocolatey e Node. js e, em seguida, instalar o driver ODBC hello e SQL CMD. Veja a [Etapa 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).

## <a name="sql-server-connection-information"></a>Informações de conexão do servidor SQL

Obter Olá conexão informações necessárias tooconnect toohello SQL Azure banco de dados. Será necessário o nome totalmente qualificado do servidor de saudação, nome do banco de dados e informações de logon em procedimentos Avançar hello.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página. 
3. Em Olá **visão geral** página do banco de dados, examine Olá nome totalmente qualificado do servidor conforme Olá a imagem a seguir. Você pode focalizar Olá toobring de nome de servidor backup Olá **clique toocopy** opção. 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se você tiver esquecido a informações de logon Olá para o servidor de banco de dados de SQL do Azure, navegue toohello banco de dados do SQL server página tooview Olá administrador nome do servidor e, se necessário, Redefinir senha hello.

> [!IMPORTANT]
> Você deve ter uma regra de firewall em vigor para o endereço IP público de saudação do computador Olá em que você executa este tutorial. Se você estiver em um computador diferente ou ter um endereço IP público diferente, crie um [regra de firewall de nível de servidor usando Olá portal do Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="create-a-nodejs-project"></a>Criar um projeto Node.js

Abra um prompt de comando e crie uma pasta chamada *sqltest*. Navegue até a pasta toohello é criado e executado Olá comando a seguir:

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a>Insira o banco de dados SQL do código tooquery

1. Em seu ambiente de desenvolvimento ou editor de texto favorito, crie um novo arquivo, **sqltest.js**.

2. Substitua o conteúdo de saudação com hello seguinte código e adicionar os valores apropriados para seu servidor, banco de dados, usuário e senha hello.

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection toodatabase
   var config = 
      {
        userName: 'someuser', // update me
        password: 'somepassword', // update me
        server: 'edmacasqlserver.database.windows.net', // update me
        options: 
           {
              database: 'somedb' //update me
              , encrypt: true
           }
      }
   var connection = new Connection(config);

   // Attempt tooconnect and execute queries if connection goes through
   connection.on('connect', function(err) 
      {
        if (err) 
          {
             console.log(err)
          }
       else
          {
              queryDatabase()
          }
      }
    );

   function queryDatabase()
      { console.log('Reading rows from hello Table...');

          // Read all rows from table
        request = new Request(
             "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid",
                function(err, rowCount, rows) 
                   {
                       console.log(rowCount + ' row(s) returned');
                       process.exit();
                   }
               );
    
        request.on('row', function(columns) {
           columns.forEach(function(column) {
               console.log("%s\t%s", column.metadata.colName, column.value);
            });
                });
        connection.execSql(request);
      }
```

## <a name="run-hello-code"></a>Executar o código de saudação

1. No prompt de comando hello, execute Olá comandos a seguir:

   ```js
   node sqltest.js
   ```

2. Verifique se que 20 linhas de saudação principais são retornadas e, em seguida, feche a janela do aplicativo hello.

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre Olá [Node.js Driver Microsoft para SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)
- Saiba como muito[se conectar e consultar um banco de dados do SQL Azure usando o .NET core](sql-database-connect-query-dotnet-core.md) no Linux/Windows/macOS.  
- Saiba mais sobre [guia de Introdução ao .NET Core no Windows/Linux/macOS usando a linha de comando Olá](/dotnet/core/tutorials/using-with-xplat-cli).
- Saiba como muito[criar seu primeiro banco de dados SQL do Azure usando o SSMS](sql-database-design-first-database.md) ou [criar seu primeiro banco de dados SQL do Azure usando o .NET](sql-database-design-first-database-csharp.md).
- Saiba como muito[conectar e consultar com SSMS](sql-database-connect-query-ssms.md)
- Saiba como muito[conectar e consultar com código do Visual Studio](sql-database-connect-query-vscode.md).


