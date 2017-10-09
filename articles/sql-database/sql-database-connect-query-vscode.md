---
title: 'VS Code: Conectar e consultar dados no Banco de Dados SQL do Azure | Microsoft Docs'
description: "Saiba como tooconnect tooSQL banco de dados no Azure usando o código do Visual Studio. Em seguida, execute instruções Transact-SQL (T-SQL) tooquery e editar dados."
metacanonical: 
keywords: Conecte-se o banco de dados toosql
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/20/2017
ms.author: carlrab
ms.openlocfilehash: ed8bdbfc3271b463a21cde5ff6b5f05fd0ff51d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-visual-studio-code-tooconnect-and-query-data"></a>Banco de dados SQL do Azure: O código do Visual Studio para usar tooconnect e consultar dados

[Código do Visual Studio](https://code.visualstudio.com/docs) é um editor de código gráfica para Linux, macOS, e que oferece suporte a extensões, incluindo Windows hello [mssql extensão](https://aka.ms/mssql-marketplace) para consultar o Microsoft SQL Server, o banco de dados do SQL Azure e SQL Data Warehouse. Este guia rápido demonstra como banco de dados do toouse código do Visual Studio tooconnect tooan SQL Azure e, em seguida, use Transact-SQL instruções tooquery, inserir, atualizar e excluir dados no banco de dados de saudação.

## <a name="prerequisites"></a>Pré-requisitos

Este guia rápido usa como seus recursos de saudação ponto inicial criados em um desses inícios rápidos:

- [Criar Banco de dados - Portal](sql-database-get-started-portal.md)
- [Criar Banco de dados - CLI](sql-database-get-started-cli.md)
- [Criar Banco de dados - PowerShell](sql-database-get-started-powershell.md)

Antes de começar, verifique se você instalou a versão mais recente de saudação do [código do Visual Studio](https://code.visualstudio.com/Download) e carregados hello [mssql extensão](https://aka.ms/mssql-marketplace). Para instruções de instalação para a extensão do mssql hello, consulte [instalar VS código](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) e consulte [mssql para o código do Visual Studio](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

## <a name="configure-vs-code"></a>Configurar o VS Code 

### <a name="mac-os"></a>**Mac OS**
Para macOS, você precisa tooinstall OpenSSL que é um pré-requisito para DotNet Core essa extensão mssql usa. Abra seu terminal e insira Olá tooinstall comandos a seguir **brew** e **OpenSSL**. 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**

Nenhuma configuração especial é necessária.

### <a name="windows"></a>**Windows**

Nenhuma configuração especial é necessária.

## <a name="sql-server-connection-information"></a>Informações de conexão do servidor SQL

Obter Olá conexão informações necessárias tooconnect toohello SQL Azure banco de dados. Será necessário o nome totalmente qualificado do servidor de saudação, nome do banco de dados e informações de logon em procedimentos Avançar hello.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página. 
3. Em Olá **visão geral** página do banco de dados, examine Olá nome totalmente qualificado do servidor conforme Olá a imagem a seguir. Você pode focalizar Olá toobring de nome de servidor backup Olá **clique toocopy** opção.

   ![informações da conexão](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se você tiver esquecido a informações de logon Olá para o servidor de banco de dados de SQL do Azure, navegue toohello banco de dados do SQL server página tooview Olá administrador nome do servidor e, se necessário, Redefinir senha hello. 

## <a name="set-language-mode-toosql"></a>Set language modo tooSQL

Modo de linguagem de saudação do conjunto é definido muito**SQL** em comandos do Visual Studio Code tooenable mssql e T-SQL IntelliSense.

1. Abra uma nova janela do Visual Studio Code. 

2. Clique em **texto sem formatação** no canto inferior direito de Olá Olá da barra de status.
3. Em Olá **modo Selecionar idioma** menu suspenso que se abre, digite **SQL**e, em seguida, pressione **ENTER** tooset Olá idioma modo tooSQL. 

   ![Modo de linguagem SQL](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-tooyour-database"></a>Conecte-se o banco de dados tooyour

Use o código do Visual Studio tooestablish um servidor de banco de dados SQL do tooyour de conexão.

> [!IMPORTANT]
> Antes de continuar, verifique se você tem seu servidor, banco de dados e informações de logon prontos. Quando você começar a inserir informações de perfil de conexão hello, se você alterar o foco de código do Visual Studio, você tem toorestart criação de perfil de conexão de saudação.
>

1. No código VS, pressione **CTRL + SHIFT + P** (ou **F1**) tooopen Olá paleta de comando.

2. Digite **sqlcon** e pressione **ENTER**.

3. Pressione **ENTER** tooselect **criar perfil de Conexão**. Isso cria um perfil de conexão para a instância do SQL Server.

4. Siga Olá prompts toospecify Olá conexão propriedades para o novo perfil de conexão hello. Depois de especificar cada valor, pressione **ENTER** toocontinue. 

   | Configuração       | Valor sugerido | Descrição |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor | nome totalmente qualificado do servidor de saudação | Olá nome deve ser semelhante a esta: **mynewserver20170313.database.windows.net**. |
   | **Nome do banco de dados** | mySampleDatabase | nome de saudação do hello tooconnect de toowhich de banco de dados. |
   | **Autenticação** | Logon do SQL| Autenticação do SQL é o tipo de autenticação somente de saudação que configuramos neste tutorial. |
   | **Nome de usuário** | conta de administrador do servidor de saudação | Essa é a conta de saudação que você especificou quando criou o servidor de saudação. |
   | **Senha (Logon do SQL)** | senha de saudação para sua conta de administrador do servidor | Essa é a senha de saudação que você especificou quando criou o servidor de saudação. |
   | **Salvar a Senha?** | Sim ou não | Selecione Sim se você não quiser senha de saudação tooenter cada vez. |
   | **Insira um nome para este perfil** | Um nome do perfil, como **mySampleDatabase** | Um nome do perfil salvo acelera sua conexão nos logons subsequentes. | 

5. Olá pressione **ESC** tooclose chave mensagem de informações de saudação que informa que o perfil de saudação é criado e conectado.

6. Verifique se sua conexão na barra de status de saudação.

   ![Status da conexão](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a>Consultar dados

Tooquery para Olá primeiros 20 produtos de código a seguir do uso Olá por categoria usando Olá [selecione](https://msdn.microsoft.com/library/ms189499.aspx) instrução Transact-SQL.

1. Em Olá **Editor** janela, digite Olá consulta na janela de consulta vazia Olá a seguir:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. Pressione **CTRL + SHIFT + E** tooretrieve dados de tabelas Product e ProductCategory de saudação.

    ![Consultar](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a>Inserir dados

Use Olá de código a seguir tooinsert um novo produto na tabela de SalesLT.Product hello usando Olá [inserir](https://msdn.microsoft.com/library/ms174335.aspx) instrução Transact-SQL.

1. Em Olá **Editor** janela, excluir a consulta anterior hello e digite Olá consulta a seguir:

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

2. Pressione **CTRL + SHIFT + E** tooinsert uma nova linha na tabela de produto hello.

## <a name="update-data"></a>Atualizar dados

Tooupdate Olá novo produto que você adicionou anteriormente usando Olá de código a seguir de saudação de uso [atualização](https://msdn.microsoft.com/library/ms177523.aspx) instrução Transact-SQL.

1.  Em Olá **Editor** janela, excluir a consulta anterior hello e digite Olá consulta a seguir:

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. Pressione **CTRL + SHIFT + E** tooupdate Olá especificado linha hello produto tabela.

## <a name="delete-data"></a>Excluir dados

Toodelete Olá novo produto que você adicionou anteriormente usando Olá de código a seguir de saudação de uso [excluir](https://msdn.microsoft.com/library/ms189835.aspx) instrução Transact-SQL.

1. Em Olá **Editor** janela, excluir a consulta anterior hello e digite Olá consulta a seguir:

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. Pressione **CTRL + SHIFT + E** toodelete Olá especificado linha hello produto tabela.

## <a name="next-steps"></a>Próximas etapas

- tooconnect e consulta usando o SQL Server Management Studio, consulte [conectar e consultar com SSMS](sql-database-connect-query-ssms.md).
- Para obter um artigo da MSDN magazine sobre como usar o Visual Studio Code, veja [Criar um banco de dados IDE com a postagem de blog de extensão MSSQL](https://msdn.microsoft.com/magazine/mt809115).
