---
title: aaaUse tooquery Ruby banco de dados do SQL Azure | Microsoft Docs
description: "Este tópico mostra como toouse toocreate Ruby um programa que se conecta tooan banco de dados do SQL Azure e a consulta usando instruções Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a>Use tooquery Ruby um banco de dados do SQL Azure

Este tutorial de início rápido demonstra como toouse [Ruby](https://www.ruby-lang.org) toocreate tooan de tooconnect um programa SQL do Azure do banco de dados e usar dados de tooquery de instruções Transact-SQL.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete rápida nesse tutorial de início, certifique-se de ter Olá pré-requisitos a seguir:

- Um banco de dados SQL do Azure. Esse início rápido usa recursos de saudação criados em um desses inícios rápidos: 

   - [Criar Banco de dados - Portal](sql-database-get-started-portal.md)
   - [Criar Banco de dados - CLI](sql-database-get-started-cli.md)
   - [Criar Banco de dados - PowerShell](sql-database-get-started-powershell.md)

- Um [regra de firewall de nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de saudação do computador Olá usar para este tutorial de início rápido.
- Você instalou o Ruby e o software relacionado para seu sistema operacional.
    - **MacOS**: instale o Homebrew, instale o rbenv e ruby-build, instale o Ruby e, em seguida, instale o FreeTDS. Confira a [Etapa 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).
    - **Ubuntu**: instale os pré-requisitos do Ruby, instale o rbenv e ruby-build, instale o Ruby e, em seguida, instale o FreeTDS. Confira a [Etapa 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).

## <a name="sql-server-connection-information"></a>Informações de conexão do servidor SQL

Obter Olá conexão informações necessárias tooconnect toohello SQL Azure banco de dados. Será necessário o nome totalmente qualificado do servidor de saudação, nome do banco de dados e informações de logon em procedimentos Avançar hello.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página. 
3. Em Olá **visão geral** para seu banco de dados, examine o nome totalmente qualificado do servidor de saudação. Você pode focalizar Olá toobring de nome de servidor backup Olá **clique toocopy** opção, conforme mostrado no Olá a imagem a seguir:

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se você tiver esquecido a informações de logon Olá para o servidor de banco de dados de SQL do Azure, navegue toohello banco de dados do SQL server página tooview Olá administrador nome do servidor e, se necessário, Redefinir senha hello.

> [!IMPORTANT]
> Você deve ter uma regra de firewall em vigor para o endereço IP público de saudação do computador Olá em que você executa este tutorial. Se você estiver em um computador diferente ou ter um endereço IP público diferente, crie um [regra de firewall de nível de servidor usando Olá portal do Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="insert-code-tooquery-sql-database"></a>Insira o banco de dados SQL do código tooquery

1. Em seu editor de texto favorito, crie um novo arquivo, **sqltest.rb**

2. Substitua o conteúdo de saudação com hello seguinte código e adicionar os valores apropriados para seu servidor, banco de dados, usuário e senha hello.

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-hello-code"></a>Executar o código de saudação

1. No prompt de comando hello, execute Olá comandos a seguir:

   ```bash
   ruby sqltest.rb
   ```

2. Verifique se que 20 linhas de saudação principais são retornadas e, em seguida, feche a janela do aplicativo hello.


## <a name="next-steps"></a>Próximas etapas
- [Projetar seu primeiro banco de dados SQL do Azure](sql-database-design-first-database.md)
- [Repositório GitHub do TinyTDS](https://github.com/rails-sqlserver/tiny_tds)
- [Relatar problemas ou fazer perguntas sobre o TinyTDS](https://github.com/rails-sqlserver/tiny_tds/issues)
- [Drivers Ruby para SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
