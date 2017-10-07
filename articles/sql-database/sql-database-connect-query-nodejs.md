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
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a><span data-ttu-id="3b617-103">Use o Node. js tooquery um banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="3b617-103">Use Node.js tooquery an Azure SQL database</span></span>

<span data-ttu-id="3b617-104">Este tutorial de início rápido demonstra como toouse [Node.js](https://nodejs.org/en/) toocreate tooan de tooconnect um programa SQL do Azure do banco de dados e usar dados de tooquery de instruções Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="3b617-104">This quick start tutorial demonstrates how toouse [Node.js](https://nodejs.org/en/) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b617-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3b617-105">Prerequisites</span></span>

<span data-ttu-id="3b617-106">toocomplete rápido nesse tutorial de início, verifique se você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="3b617-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="3b617-107">Um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b617-107">An Azure SQL database.</span></span> <span data-ttu-id="3b617-108">Esse início rápido usa recursos de saudação criados em um desses inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="3b617-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="3b617-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="3b617-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="3b617-110">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="3b617-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="3b617-111">Criar Banco de dados - PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b617-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="3b617-112">Um [regra de firewall de nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de saudação do computador Olá usar para este tutorial de início rápido.</span><span class="sxs-lookup"><span data-stu-id="3b617-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="3b617-113">Você instalou o Node.js e o software relacionado para seu sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="3b617-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="3b617-114">**MacOS**: instalar o Homebrew e Node. js e, em seguida, instalar o driver ODBC hello e SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="3b617-114">**MacOS**: Install Homebrew and Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="3b617-115">Veja a [Etapa 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span><span class="sxs-lookup"><span data-stu-id="3b617-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="3b617-116">**Ubuntu**: instalar o Node. js e, em seguida, instalar o driver ODBC hello e SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="3b617-116">**Ubuntu**: Install Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="3b617-117">Veja a [Etapa 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="3b617-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="3b617-118">**Windows**: instalar Chocolatey e Node. js e, em seguida, instalar o driver ODBC hello e SQL CMD.</span><span class="sxs-lookup"><span data-stu-id="3b617-118">**Windows**: Install Chocolatey and Node.js, and then install hello ODBC driver and SQL CMD.</span></span> <span data-ttu-id="3b617-119">Veja a [Etapa 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span><span class="sxs-lookup"><span data-stu-id="3b617-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="3b617-120">Informações de conexão do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="3b617-120">SQL server connection information</span></span>

<span data-ttu-id="3b617-121">Obter Olá conexão informações necessárias tooconnect toohello SQL Azure banco de dados.</span><span class="sxs-lookup"><span data-stu-id="3b617-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="3b617-122">Será necessário o nome totalmente qualificado do servidor de saudação, nome do banco de dados e informações de logon em procedimentos Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="3b617-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="3b617-123">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3b617-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3b617-124">Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="3b617-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="3b617-125">Em Olá **visão geral** página do banco de dados, examine Olá nome totalmente qualificado do servidor conforme Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="3b617-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="3b617-126">Você pode focalizar Olá toobring de nome de servidor backup Olá **clique toocopy** opção.</span><span class="sxs-lookup"><span data-stu-id="3b617-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="3b617-128">Se você tiver esquecido a informações de logon Olá para o servidor de banco de dados de SQL do Azure, navegue toohello banco de dados do SQL server página tooview Olá administrador nome do servidor e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="3b617-128">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b617-129">Você deve ter uma regra de firewall em vigor para o endereço IP público de saudação do computador Olá em que você executa este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3b617-129">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="3b617-130">Se você estiver em um computador diferente ou ter um endereço IP público diferente, crie um [regra de firewall de nível de servidor usando Olá portal do Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="3b617-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="3b617-131">Criar um projeto Node.js</span><span class="sxs-lookup"><span data-stu-id="3b617-131">Create a Node.js project</span></span>

<span data-ttu-id="3b617-132">Abra um prompt de comando e crie uma pasta chamada *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="3b617-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="3b617-133">Navegue até a pasta toohello é criado e executado Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3b617-133">Navigate toohello folder you created and run hello following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="3b617-134">Insira o banco de dados SQL do código tooquery</span><span class="sxs-lookup"><span data-stu-id="3b617-134">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="3b617-135">Em seu ambiente de desenvolvimento ou editor de texto favorito, crie um novo arquivo, **sqltest.js**.</span><span class="sxs-lookup"><span data-stu-id="3b617-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="3b617-136">Substitua o conteúdo de saudação com hello seguinte código e adicionar os valores apropriados para seu servidor, banco de dados, usuário e senha hello.</span><span class="sxs-lookup"><span data-stu-id="3b617-136">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="3b617-137">Executar o código de saudação</span><span class="sxs-lookup"><span data-stu-id="3b617-137">Run hello code</span></span>

1. <span data-ttu-id="3b617-138">No prompt de comando hello, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3b617-138">At hello command prompt, run hello following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="3b617-139">Verifique se que 20 linhas de saudação principais são retornadas e, em seguida, feche a janela do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3b617-139">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b617-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b617-140">Next steps</span></span>

- <span data-ttu-id="3b617-141">Saiba mais sobre Olá [Node.js Driver Microsoft para SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="3b617-141">Learn about hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="3b617-142">Saiba como muito[se conectar e consultar um banco de dados do SQL Azure usando o .NET core](sql-database-connect-query-dotnet-core.md) no Linux/Windows/macOS.</span><span class="sxs-lookup"><span data-stu-id="3b617-142">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="3b617-143">Saiba mais sobre [guia de Introdução ao .NET Core no Windows/Linux/macOS usando a linha de comando Olá](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="3b617-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="3b617-144">Saiba como muito[criar seu primeiro banco de dados SQL do Azure usando o SSMS](sql-database-design-first-database.md) ou [criar seu primeiro banco de dados SQL do Azure usando o .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="3b617-144">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="3b617-145">Saiba como muito[conectar e consultar com SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="3b617-145">Learn how too[Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="3b617-146">Saiba como muito[conectar e consultar com código do Visual Studio](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="3b617-146">Learn how too[Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


