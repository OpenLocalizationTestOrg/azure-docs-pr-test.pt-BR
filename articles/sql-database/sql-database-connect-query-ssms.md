---
title: 'SSMS: Conectar e consultar dados no Banco de Dados SQL do Azure | Microsoft Docs'
description: "Saiba como tooconnect tooSQL banco de dados no Azure usando o SQL Server Management Studio (SSMS). Em seguida, execute instruções Transact-SQL (T-SQL) tooquery e editar dados."
metacanonical: 
keywords: Conecte-se o banco de dados toosql, studio de gerenciamento do sql server
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 7cd2a114-c13c-4ace-9088-97bd9d68de12
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 769a3a1ecc34800bd345b64e89841f7147b144f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-sql-server-management-studio-tooconnect-and-query-data"></a>Banco de dados SQL do Azure: Dados de tooconnect e consulta Use SQL Server Management Studio

[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) é um ambiente integrado para gerenciar qualquer infraestrutura SQL, do SQL Server tooSQL banco de dados para o Microsoft Windows. Este guia rápido demonstra como o banco de dados do toouse SSMS tooconnect tooan SQL Azure e, em seguida, tooquery de instruções de uso de Transact-SQL, inserem, atualizar e excluir dados no banco de dados de saudação. 

## <a name="prerequisites"></a>Pré-requisitos

Este guia rápido usa como seus recursos de saudação ponto inicial criados em um desses inícios rápidos:

- [Criar Banco de dados - Portal](sql-database-get-started-portal.md)
- [Criar Banco de dados - CLI](sql-database-get-started-cli.md)
- [Criar Banco de dados - PowerShell](sql-database-get-started-powershell.md)

Antes de começar, verifique se você instalou a versão mais recente de saudação do [SSMS](https://msdn.microsoft.com/library/mt238290.aspx). 

## <a name="sql-server-connection-information"></a>Informações de conexão do servidor SQL

Obter Olá conexão informações necessárias tooconnect toohello SQL Azure banco de dados. Será necessário o nome totalmente qualificado do servidor de saudação, nome do banco de dados e informações de logon em procedimentos Avançar hello.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página. 
3. Em Olá **visão geral** para seu banco de dados, examine o nome totalmente qualificado do servidor de saudação conforme mostrado na imagem de saudação abaixo. Você pode focalizar Olá toobring de nome de servidor backup Olá **clique toocopy** opção.

   ![informações da conexão](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se você tiver esquecido a informações de logon Olá para o servidor de banco de dados de SQL do Azure, navegue toohello banco de dados do SQL server página tooview Olá administrador nome do servidor e, se necessário, Redefinir senha hello. 

## <a name="connect-tooyour-database"></a>Conecte-se o banco de dados tooyour

Use o SQL Server Management Studio tooestablish um servidor de banco de dados SQL do tooyour de conexão. 

> [!IMPORTANT]
> Um servidor lógico do Banco de Dados SQL do Azure escuta na porta 1433. Se você estiver tentando tooconnect tooan banco de dados do Azure SQL servidor lógico de dentro de um firewall corporativo, essa porta deve estar aberta no firewall corporativo Olá para toosuccessfully você se conectar.
>

1. Abra o SQL Server Management Studio.

2. Em Olá **conectar tooServer** caixa de diálogo, digite Olá informações a seguir:

   | Configuração       | Valor sugerido | Descrição | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Mecanismo de banco de dados | Esse valor é obrigatório. |
   | **Nome do servidor** | nome totalmente qualificado do servidor de saudação | Olá nome deve ser semelhante a esta: **mynewserver20170313.database.windows.net**. |
   | **Autenticação** | Autenticação do SQL Server | Autenticação do SQL é o tipo de autenticação somente de saudação que configuramos neste tutorial. |
   | **Logon** | conta de administrador do servidor de saudação | Essa é a conta de saudação que você especificou quando criou o servidor de saudação. |
   | **Senha** | senha de saudação para sua conta de administrador do servidor | Essa é a senha de saudação que você especificou quando criou o servidor de saudação. |

   ![Conecte-se tooserver](./media/sql-database-connect-query-ssms/connect.png)  

3. Clique em **opções** em Olá **conectar tooserver** caixa de diálogo. Em Olá **conectar toodatabase** seção, digite **mySampleDatabase** tooconnect toothis database.

   ![Conecte-se toodb no servidor](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. Clique em **Conectar**. janela do Pesquisador de objetos de saudação é aberta no SSMS. 

   ![tooserver conectado](./media/sql-database-connect-query-ssms/connected.png)  

5. No Pesquisador de objetos, expanda **bancos de dados** e, em seguida, expanda **mySampleDatabase** tooview objetos de saudação no banco de dados de exemplo hello.

## <a name="query-data"></a>Consultar dados

Tooquery para Olá primeiros 20 produtos de código a seguir do uso Olá por categoria usando Olá [selecione](https://msdn.microsoft.com/library/ms189499.aspx) instrução Transact-SQL.

1. No Pesquisador de Objetos, clique com o botão direito em **mySampleDatabase** e clique em **Nova Consulta**. Uma janela de consulta em branco é aberto que é conectado tooyour banco de dados.
2. Na janela de consulta hello, digite Olá consulta a seguir:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. Na barra de ferramentas hello, clique em **Execute** tooretrieve dados de tabelas Product e ProductCategory de saudação.

    ![query](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a>Inserir dados

Use Olá de código a seguir tooinsert um novo produto na tabela de SalesLT.Product hello usando Olá [inserir](https://msdn.microsoft.com/library/ms174335.aspx) instrução Transact-SQL.

1. Na janela de consulta hello, substitua consulta anterior Olá Olá consulta a seguir:

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. Na barra de ferramentas hello, clique em **Execute** tooinsert uma nova linha na tabela de produto hello.

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a>Atualizar dados

Tooupdate Olá novo produto que você adicionou anteriormente usando Olá de código a seguir de saudação de uso [atualização](https://msdn.microsoft.com/library/ms177523.aspx) instrução Transact-SQL.

1. Na janela de consulta hello, substitua consulta anterior Olá Olá consulta a seguir:

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. Na barra de ferramentas hello, clique em **Execute** tooupdate Olá especificado linha hello produto tabela.

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a>Excluir dados

Toodelete Olá novo produto que você adicionou anteriormente usando Olá de código a seguir de saudação de uso [excluir](https://msdn.microsoft.com/library/ms189835.aspx) instrução Transact-SQL.

1. Na janela de consulta hello, substitua consulta anterior Olá Olá consulta a seguir:

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. Na barra de ferramentas hello, clique em **Execute** toodelete Olá especificado linha hello produto tabela.

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a>Próximas etapas

- toolearn sobre como criar e gerenciar servidores e bancos de dados com o Transact-SQL, consulte [Saiba mais sobre bancos de dados e servidores de banco de dados do Azure SQL](sql-database-servers-databases.md).
- Para saber mais sobre o SSMS, consulte [Usar o SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).
- tooconnect e consulta usando código do Visual Studio, consulte [conectar e consultar com código do Visual Studio](sql-database-connect-query-vscode.md).
- tooconnect e consulta usando .NET, consulte [conectar e consultar com .NET](sql-database-connect-query-dotnet.md).
- tooconnect e consulta usando o PHP, consulte [conectar e consultar com PHP](sql-database-connect-query-php.md).
- tooconnect e consulta usando Node. js, consulte [conectar e consultar com Node. js](sql-database-connect-query-nodejs.md).
- tooconnect e consulta usando o Java, consulte [conectar e consultar com Java](sql-database-connect-query-java.md).
- tooconnect e consulta usando Python, consulte [conectar e consultar com Python](sql-database-connect-query-python.md).
- tooconnect e consulta usando o Ruby, consulte [conectar e consultar com Ruby](sql-database-connect-query-ruby.md).
