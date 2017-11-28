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
# <a name="use-php-tooquery-an-azure-sql-database"></a><span data-ttu-id="a7cd1-103">Usar PHP tooquery um banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="a7cd1-103">Use PHP tooquery an Azure SQL database</span></span>

<span data-ttu-id="a7cd1-104">Este tutorial de início rápido demonstra como toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate tooan de tooconnect um programa SQL do Azure do banco de dados e usar dados de tooquery de instruções Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-104">This quick start tutorial demonstrates how toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7cd1-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a7cd1-105">Prerequisites</span></span>

<span data-ttu-id="a7cd1-106">toocomplete rápido nesse tutorial de início, verifique se você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="a7cd1-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="a7cd1-107">Um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-107">An Azure SQL database.</span></span> <span data-ttu-id="a7cd1-108">Esse início rápido usa recursos de saudação criados em um desses inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="a7cd1-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="a7cd1-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="a7cd1-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="a7cd1-110">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="a7cd1-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="a7cd1-111">Criar Banco de dados - PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7cd1-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="a7cd1-112">Um [regra de firewall de nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de saudação do computador Olá usar para este tutorial de início rápido.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="a7cd1-113">Você instalou o PHP e o software relacionado para seu sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="a7cd1-114">**MacOS**: instalar o Homebrew PHP, instale o driver ODBC hello e SQLCMD e, em seguida, instale Olá PHP Driver for SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-114">**MacOS**: Install Homebrew and PHP, install hello ODBC driver and SQLCMD, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="a7cd1-115">Consulte [Etapas 1.2, 1.3 e 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="a7cd1-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="a7cd1-116">**Ubuntu**: instalar o PHP e outros necessários pacotes e, em seguida, instalar Olá Driver do PHP para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-116">**Ubuntu**:  Install PHP and other required packages, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="a7cd1-117">Consulte [Etapas 1.2 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="a7cd1-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="a7cd1-118">**Windows**: instalar a versão mais recente saudação do PHP para o IIS Express, a versão mais recente Olá dos Drivers da Microsoft para SQL Server no IIS Express, Chocolatey, o driver ODBC hello e SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-118">**Windows**: Install hello newest version of PHP for IIS Express, hello newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, hello ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="a7cd1-119">Consulte [Etapas 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="a7cd1-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="a7cd1-120">Informações de conexão do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="a7cd1-120">SQL server connection information</span></span>

<span data-ttu-id="a7cd1-121">Obter Olá conexão informações necessárias tooconnect toohello SQL Azure banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="a7cd1-122">Será necessário o nome totalmente qualificado do servidor de saudação, nome do banco de dados e informações de logon em procedimentos Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="a7cd1-123">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a7cd1-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a7cd1-124">Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="a7cd1-125">Em Olá **visão geral** página do banco de dados, examine Olá nome totalmente qualificado do servidor conforme Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="a7cd1-126">Você pode focalizar Olá toobring de nome de servidor backup Olá **clique toocopy** opção.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="a7cd1-128">Se você esquecer suas informações de logon de servidor, navegar toohello banco de dados do SQL server página tooview Olá administrador nome do servidor e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="a7cd1-129">Insira o banco de dados SQL do código tooquery</span><span class="sxs-lookup"><span data-stu-id="a7cd1-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="a7cd1-130">Em seu editor de texto favorito, crie um novo arquivo, **sqltest.php**.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="a7cd1-131">Substitua o conteúdo de saudação com hello seguinte código e adicionar os valores apropriados para seu servidor, banco de dados, usuário e senha hello.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="a7cd1-132">Executar o código de saudação</span><span class="sxs-lookup"><span data-stu-id="a7cd1-132">Run hello code</span></span>

1. <span data-ttu-id="a7cd1-133">No prompt de comando hello, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a7cd1-133">At hello command prompt, run hello following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="a7cd1-134">Verifique se que 20 linhas de saudação principais são retornadas e, em seguida, feche a janela do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a7cd1-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7cd1-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a7cd1-135">Next steps</span></span>
- [<span data-ttu-id="a7cd1-136">Projetar seu primeiro banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="a7cd1-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="a7cd1-137">Drivers PHP Microsoft para SQL Server</span><span class="sxs-lookup"><span data-stu-id="a7cd1-137">Microsoft PHP Drivers for SQL Server</span></span>](https://github.com/Microsoft/msphpsql/)
- [<span data-ttu-id="a7cd1-138">Relatar problemas ou fazer perguntas</span><span class="sxs-lookup"><span data-stu-id="a7cd1-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
