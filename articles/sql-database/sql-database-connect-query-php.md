---
title: aaaUse PHP tooquery banco de dados do SQL Azure | Microsoft Docs
description: "Este tópico mostra como toouse PHP toocreate um programa que se conecta tooan banco de dados do SQL Azure e a consulta usando instruções Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 4e71db4a-a 22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 5fc49dcc42ab07cc1bec554be39bdf08dbd6f75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-php-tooquery-an-azure-sql-database"></a>Usar PHP tooquery um banco de dados do SQL Azure

Este tutorial de início rápido demonstra como toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate tooan de tooconnect um programa SQL do Azure do banco de dados e usar dados de tooquery de instruções Transact-SQL.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete rápido nesse tutorial de início, verifique se você tem o seguinte hello:

- Um banco de dados SQL do Azure. Esse início rápido usa recursos de saudação criados em um desses inícios rápidos: 

   - [Criar Banco de dados - Portal](sql-database-get-started-portal.md)
   - [Criar Banco de dados - CLI](sql-database-get-started-cli.md)
   - [Criar Banco de dados - PowerShell](sql-database-get-started-powershell.md)

- Um [regra de firewall de nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de saudação do computador Olá usar para este tutorial de início rápido.

- Você instalou o PHP e o software relacionado para seu sistema operacional.

    - **MacOS**: instalar o Homebrew PHP, instale o driver ODBC hello e SQLCMD e, em seguida, instale Olá PHP Driver for SQL Server. Consulte [Etapas 1.2, 1.3 e 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).
    - **Ubuntu**: instalar o PHP e outros necessários pacotes e, em seguida, instalar Olá Driver do PHP para SQL Server. Consulte [Etapas 1.2 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).
    - **Windows**: instalar a versão mais recente saudação do PHP para o IIS Express, a versão mais recente Olá dos Drivers da Microsoft para SQL Server no IIS Express, Chocolatey, o driver ODBC hello e SQLCMD. Consulte [Etapas 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).    

## <a name="sql-server-connection-information"></a>Informações de conexão do servidor SQL

Obter Olá conexão informações necessárias tooconnect toohello SQL Azure banco de dados. Será necessário o nome totalmente qualificado do servidor de saudação, nome do banco de dados e informações de logon em procedimentos Avançar hello.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página. 
3. Em Olá **visão geral** página do banco de dados, examine Olá nome totalmente qualificado do servidor conforme Olá a imagem a seguir. Você pode focalizar Olá toobring de nome de servidor backup Olá **clique toocopy** opção.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se você esquecer suas informações de logon de servidor, navegar toohello banco de dados do SQL server página tooview Olá administrador nome do servidor e, se necessário, Redefinir senha hello.     
    
## <a name="insert-code-tooquery-sql-database"></a>Insira o banco de dados SQL do código tooquery

1. Em seu editor de texto favorito, crie um novo arquivo, **sqltest.php**.  

2. Substitua o conteúdo de saudação com hello seguinte código e adicionar os valores apropriados para seu servidor, banco de dados, usuário e senha hello.

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes hello connection
   $conn = sqlsrv_connect($serverName, $connectionOptions);
   $tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
           FROM [SalesLT].[ProductCategory] pc
           JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid";
   $getResults= sqlsrv_query($conn, $tsql);
   echo ("Reading data from table" . PHP_EOL);
   if ($getResults == FALSE)
       echo (sqlsrv_errors());
   while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
   }
   sqlsrv_free_stmt($getResults);
   ?>
   ```

## <a name="run-hello-code"></a>Executar o código de saudação

1. No prompt de comando hello, execute Olá comandos a seguir:

   ```php
   php sqltest.php
   ```

2. Verifique se que 20 linhas de saudação principais são retornadas e, em seguida, feche a janela do aplicativo hello.

## <a name="next-steps"></a>Próximas etapas
- [Projetar seu primeiro banco de dados SQL do Azure](sql-database-design-first-database.md)
- [Drivers PHP Microsoft para SQL Server](https://github.com/Microsoft/msphpsql/)
- [Relatar problemas ou fazer perguntas](https://github.com/Microsoft/msphpsql/issues)
