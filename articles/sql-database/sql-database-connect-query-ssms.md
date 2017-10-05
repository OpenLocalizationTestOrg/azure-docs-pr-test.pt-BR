---
title: 'SSMS: Conectar e consultar dados no Banco de Dados SQL do Azure | Microsoft Docs'
description: "Saiba como se conectar a um banco de dados SQL no Azure usando o SSMS (SQL Server Management Studio). Em seguida, execute instruções T-SQL (Transact-SQL) para consultar e editar dados."
metacanonical: 
keywords: conectar-se ao banco de dados sql, sql server management studio
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
ms.openlocfilehash: 2835a72fc90d1fd39af73c6907648908e5d9fdeb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-use-sql-server-management-studio-to-connect-and-query-data"></a><span data-ttu-id="19c75-105">Banco de Dados SQL do Azure: Use o SQL Server Management Studio para conectar e consultar dados</span><span class="sxs-lookup"><span data-stu-id="19c75-105">Azure SQL Database: Use SQL Server Management Studio to connect and query data</span></span>

<span data-ttu-id="19c75-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) é um ambiente integrado para gerenciar qualquer infraestrutura do SQL, do SQL Server para o Banco de Dados SQL do Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="19c75-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) is an integrated environment for managing any SQL infrastructure, from SQL Server to SQL Database for Microsoft Windows.</span></span> <span data-ttu-id="19c75-107">Este guia rápido demonstra como usar o SSMS para conectar um banco de dados SQL do Azure, em seguida, usar instruções Transact-SQL para consultar, inserir, atualizar e excluir os dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="19c75-107">This quick start demonstrates how to use SSMS to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="19c75-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="19c75-108">Prerequisites</span></span>

<span data-ttu-id="19c75-109">Este início rápido usa como ponto de partida os recursos criados em um destes inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="19c75-109">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="19c75-110">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="19c75-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="19c75-111">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="19c75-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="19c75-112">Criar Banco de dados - PowerShell</span><span class="sxs-lookup"><span data-stu-id="19c75-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="19c75-113">Antes de começar, verifique se você instalou a versão mais recente do [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c75-113">Before you start, make sure you have installed the newest version of [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="19c75-114">Informações de conexão do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="19c75-114">SQL server connection information</span></span>

<span data-ttu-id="19c75-115">Obtenha as informações de conexão necessárias para se conectar ao Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="19c75-115">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="19c75-116">Você precisará do nome totalmente qualificado do servidor, nome do banco de dados e informações de logon nos próximos procedimentos.</span><span class="sxs-lookup"><span data-stu-id="19c75-116">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="19c75-117">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="19c75-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="19c75-118">Selecione **Bancos de Dados SQL** no menu à esquerda e clique em seu banco de dados na página **Bancos de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="19c75-118">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="19c75-119">Na página **Visão geral** do banco de dados, analise o nome totalmente qualificado do servidor, como mostrado na imagem abaixo.</span><span class="sxs-lookup"><span data-stu-id="19c75-119">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span></span> <span data-ttu-id="19c75-120">Você pode passar o mouse sobre o nome do servidor para abrir a opção **Clique para copiar**.</span><span class="sxs-lookup"><span data-stu-id="19c75-120">You can hover over the server name to bring up the **Click to copy** option.</span></span>

   ![informações da conexão](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="19c75-122">Se você esqueceu as informações de logon para o servidor do Banco de Dados SQL do Azure, navegue até a página do servidor do Banco de Dados SQL para exibir o nome de administrador do servidor e, se necessário, redefinir a senha.</span><span class="sxs-lookup"><span data-stu-id="19c75-122">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span> 

## <a name="connect-to-your-database"></a><span data-ttu-id="19c75-123">Conectar-se ao seu banco de dados</span><span class="sxs-lookup"><span data-stu-id="19c75-123">Connect to your database</span></span>

<span data-ttu-id="19c75-124">Use o SQL Server Management Studio para estabelecer uma conexão com seu servidor de Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="19c75-124">Use SQL Server Management Studio to establish a connection to your Azure SQL Database server.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="19c75-125">Um servidor lógico do Banco de Dados SQL do Azure escuta na porta 1433.</span><span class="sxs-lookup"><span data-stu-id="19c75-125">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="19c75-126">Se você estiver tentando conectar um servidor lógico do Banco de Dados SQL do Azure de dentro de um firewall corporativo, essa porta deverá estar aberta no firewall corporativo para que você possa conectar-se com êxito.</span><span class="sxs-lookup"><span data-stu-id="19c75-126">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

1. <span data-ttu-id="19c75-127">Abra o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="19c75-127">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="19c75-128">Na caixa de diálogo **Conectar ao Servidor**, insira as informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="19c75-128">In the **Connect to Server** dialog box, enter the following information:</span></span>

   | <span data-ttu-id="19c75-129">Configuração</span><span class="sxs-lookup"><span data-stu-id="19c75-129">Setting</span></span>       | <span data-ttu-id="19c75-130">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="19c75-130">Suggested value</span></span> | <span data-ttu-id="19c75-131">Descrição</span><span class="sxs-lookup"><span data-stu-id="19c75-131">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="19c75-132">**Tipo de servidor**</span><span class="sxs-lookup"><span data-stu-id="19c75-132">**Server type**</span></span> | <span data-ttu-id="19c75-133">Mecanismo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="19c75-133">Database engine</span></span> | <span data-ttu-id="19c75-134">Esse valor é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="19c75-134">This value is required.</span></span> |
   | <span data-ttu-id="19c75-135">**Nome do servidor**</span><span class="sxs-lookup"><span data-stu-id="19c75-135">**Server name**</span></span> | <span data-ttu-id="19c75-136">O nome do servidor totalmente qualificado</span><span class="sxs-lookup"><span data-stu-id="19c75-136">The fully qualified server name</span></span> | <span data-ttu-id="19c75-137">O nome deve ser semelhante como: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="19c75-137">The name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="19c75-138">**Autenticação**</span><span class="sxs-lookup"><span data-stu-id="19c75-138">**Authentication**</span></span> | <span data-ttu-id="19c75-139">Autenticação do SQL Server</span><span class="sxs-lookup"><span data-stu-id="19c75-139">SQL Server Authentication</span></span> | <span data-ttu-id="19c75-140">A Autenticação do SQL é o único tipo de autenticação que configuramos neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="19c75-140">SQL Authentication is the only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="19c75-141">**Logon**</span><span class="sxs-lookup"><span data-stu-id="19c75-141">**Login**</span></span> | <span data-ttu-id="19c75-142">A conta do administrador do servidor</span><span class="sxs-lookup"><span data-stu-id="19c75-142">The server admin account</span></span> | <span data-ttu-id="19c75-143">Esta é a conta que você especificou quando criou o servidor.</span><span class="sxs-lookup"><span data-stu-id="19c75-143">This is the account that you specified when you created the server.</span></span> |
   | <span data-ttu-id="19c75-144">**Senha**</span><span class="sxs-lookup"><span data-stu-id="19c75-144">**Password**</span></span> | <span data-ttu-id="19c75-145">A senha para sua conta do administrador do servidor</span><span class="sxs-lookup"><span data-stu-id="19c75-145">The password for your server admin account</span></span> | <span data-ttu-id="19c75-146">Esta é a senha que você especificou quando criou o servidor.</span><span class="sxs-lookup"><span data-stu-id="19c75-146">This is the password that you specified when you created the server.</span></span> |

   ![conectar-se ao servidor](./media/sql-database-connect-query-ssms/connect.png)  

3. <span data-ttu-id="19c75-148">Clique em **Opções** na caixa de diálogo **Conectar servidor**.</span><span class="sxs-lookup"><span data-stu-id="19c75-148">Click **Options** in the **Connect to server** dialog box.</span></span> <span data-ttu-id="19c75-149">Na seção **Conectar ao banco de dados**, digite **mySampleDatabase** para conectar-se a este banco de dados.</span><span class="sxs-lookup"><span data-stu-id="19c75-149">In the **Connect to database** section, enter **mySampleDatabase** to connect to this database.</span></span>

   ![conectar o banco de dados no servidor](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="19c75-151">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="19c75-151">Click **Connect**.</span></span> <span data-ttu-id="19c75-152">A janela Pesquisador de Objetos abre no SSMS.</span><span class="sxs-lookup"><span data-stu-id="19c75-152">The Object Explorer window opens in SSMS.</span></span> 

   ![conectado ao servidor](./media/sql-database-connect-query-ssms/connected.png)  

5. <span data-ttu-id="19c75-154">No Pesquisador de Objetos, expanda **Bancos de Dados** e expanda **mySampleDatabase** para exibir os objetos no banco de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="19c75-154">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.</span></span>

## <a name="query-data"></a><span data-ttu-id="19c75-155">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="19c75-155">Query data</span></span>

<span data-ttu-id="19c75-156">Use o seguinte código para consultar os 20 principais produtos por categoria usando a instrução [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) do Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="19c75-156">Use the following code to query for the top 20 products by category using the [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="19c75-157">No Pesquisador de Objetos, clique com o botão direito em **mySampleDatabase** e clique em **Nova Consulta**.</span><span class="sxs-lookup"><span data-stu-id="19c75-157">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="19c75-158">Uma janela de consulta em branco conectada ao seu banco de dados é aberta.</span><span class="sxs-lookup"><span data-stu-id="19c75-158">A blank query window opens that is connected to your database.</span></span>
2. <span data-ttu-id="19c75-159">Na janela de consulta, insira a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="19c75-159">In the query window, enter the following query:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. <span data-ttu-id="19c75-160">Na barra de ferramentas, clique em **Executar** para recuperar dados das tabelas Product e ProductCategory.</span><span class="sxs-lookup"><span data-stu-id="19c75-160">On the toolbar, click **Execute** to retrieve data from the Product and ProductCategory tables.</span></span>

    ![query](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a><span data-ttu-id="19c75-162">Inserir dados</span><span class="sxs-lookup"><span data-stu-id="19c75-162">Insert data</span></span>

<span data-ttu-id="19c75-163">Use o código a seguir para inserir um novo produto na tabela SalesLT.Product usando a instrução [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) do Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="19c75-163">Use the following code to insert a new product into the SalesLT.Product table using the [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="19c75-164">Na janela de consulta, substitua a consulta anterior pela seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="19c75-164">In the query window, replace the previous query with the following query:</span></span>

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

2. <span data-ttu-id="19c75-165">Na barra de ferramentas, clique em **Executar** para inserir uma nova linha na tabela Product.</span><span class="sxs-lookup"><span data-stu-id="19c75-165">On the toolbar, click **Execute**  to insert a new row in the Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a><span data-ttu-id="19c75-166">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="19c75-166">Update data</span></span>

<span data-ttu-id="19c75-167">Use o código a seguir para atualizar o novo produto que você adicionou anteriormente usando a instrução [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) do Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="19c75-167">Use the following code to update the new product that you previously added using the [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="19c75-168">Na janela de consulta, substitua a consulta anterior pela seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="19c75-168">In the query window, replace the previous query with the following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="19c75-169">Na barra de ferramentas, clique em **Executar** para atualizar a linha especificada na tabela Product.</span><span class="sxs-lookup"><span data-stu-id="19c75-169">On the toolbar, click **Execute** to update the specified row in the Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a><span data-ttu-id="19c75-170">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="19c75-170">Delete data</span></span>

<span data-ttu-id="19c75-171">Use o código a seguir para excluir o novo produto que você adicionou anteriormente usando a instrução [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) do Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="19c75-171">Use the following code to delete the new product that you previously added using the [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="19c75-172">Na janela de consulta, substitua a consulta anterior pela seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="19c75-172">In the query window, replace the previous query with the following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="19c75-173">Na barra de ferramentas, clique em **Executar** para excluir a linha especificada na tabela Product.</span><span class="sxs-lookup"><span data-stu-id="19c75-173">On the toolbar, click **Execute** to delete the specified row in the Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a><span data-ttu-id="19c75-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="19c75-174">Next steps</span></span>

- <span data-ttu-id="19c75-175">Para saber mais sobre como criar e gerenciar servidores e bancos de dados com o Transact-SQL, confira [Saiba mais sobre servidores de bancos de dados e banco de dados SQL do Azure](sql-database-servers-databases.md).</span><span class="sxs-lookup"><span data-stu-id="19c75-175">To learn about creating and managing servers and databases with Transact-SQL, see [Learn about Azure SQL Database servers and databases](sql-database-servers-databases.md).</span></span>
- <span data-ttu-id="19c75-176">Para saber mais sobre o SSMS, consulte [Usar o SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c75-176">For information about SSMS, see [Use SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>
- <span data-ttu-id="19c75-177">Para conectar e consultar usando o Visual Studio Code, veja [Conectar e consultar com o Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="19c75-177">To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="19c75-178">Para conectar e consultar usando o .NET, veja [Conectar e consultar com o .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="19c75-178">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="19c75-179">Para conectar e consultar usando o PHP, veja [Conectar e consultar com o PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="19c75-179">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="19c75-180">Para conectar e consultar usando o Node.js, veja [Conectar e consultar com o Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="19c75-180">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="19c75-181">Para conectar e consultar usando o Java, veja [Conectar e consultar com o Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="19c75-181">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="19c75-182">Para conectar e consultar usando o Python, veja [Conectar e consultar com o Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="19c75-182">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="19c75-183">Para conectar e consultar usando o Ruby, veja [Conectar e consultar com o Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="19c75-183">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>
