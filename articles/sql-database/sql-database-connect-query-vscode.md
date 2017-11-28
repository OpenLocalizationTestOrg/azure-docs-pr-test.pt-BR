---
title: 'VS Code: Conectar e consultar dados no Banco de Dados SQL do Azure | Microsoft Docs'
description: "Saiba como se conectar a um Banco de Dados SQL no Azure usando o Visual Studio Code. Em seguida, execute instruções T-SQL (Transact-SQL) para consultar e editar dados."
metacanonical: 
keywords: conectar-se ao banco de dados sql
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
ms.openlocfilehash: 4076b1e7ab3a70009217a1deff72da4bff0dc871
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-use-visual-studio-code-to-connect-and-query-data"></a><span data-ttu-id="bafc6-105">Banco de Dados SQL do Azure: Use Visual Studio Code para se conectar e consultar dados</span><span class="sxs-lookup"><span data-stu-id="bafc6-105">Azure SQL Database: Use Visual Studio Code to connect and query data</span></span>

<span data-ttu-id="bafc6-106">O [Visual Studio Code](https://code.visualstudio.com/docs) é um editor de código gráfico para o Linux, macOS e Windows que oferece suporte às extensões, incluindo a [extensão mssql](https://aka.ms/mssql-marketplace) para consultar o Microsoft SQL Server, Banco de Dados SQL do Azure e SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bafc6-106">[Visual Studio Code](https://code.visualstudio.com/docs) is a graphical code editor for Linux, macOS, and Windows that supports extensions, including the [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="bafc6-107">Este início rápido demonstra como usar o Visual Studio Code para conectar um banco de dados SQL do Azure, então, usar as instruções Transact-SQL para consultar, inserir, atualizar e excluir os dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="bafc6-107">This quick start demonstrates how to use Visual Studio Code to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bafc6-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bafc6-108">Prerequisites</span></span>

<span data-ttu-id="bafc6-109">Este início rápido usa como ponto de partida os recursos criados em um destes inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="bafc6-109">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="bafc6-110">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="bafc6-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="bafc6-111">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="bafc6-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="bafc6-112">Criar Banco de dados - PowerShell</span><span class="sxs-lookup"><span data-stu-id="bafc6-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="bafc6-113">Antes de começar, verifique se você instalou a versão mais recente do [Visual Studio Code](https://code.visualstudio.com/Download) e carregou a [extensão mssql](https://aka.ms/mssql-marketplace).</span><span class="sxs-lookup"><span data-stu-id="bafc6-113">Before you start, make sure you have installed the newest version of [Visual Studio Code](https://code.visualstudio.com/Download) and loaded the [mssql extension](https://aka.ms/mssql-marketplace).</span></span> <span data-ttu-id="bafc6-114">Para obter orientações de instalação para a extensão mssql, consulte [Instalar o VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) e consulte [mssql para Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span><span class="sxs-lookup"><span data-stu-id="bafc6-114">For installation guidance for the mssql extension, see [Install VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) and see [mssql for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span></span> 

## <a name="configure-vs-code"></a><span data-ttu-id="bafc6-115">Configurar o VS Code</span><span class="sxs-lookup"><span data-stu-id="bafc6-115">Configure VS Code</span></span> 

### <a name="mac-os"></a><span data-ttu-id="bafc6-116">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="bafc6-116">**Mac OS**</span></span>
<span data-ttu-id="bafc6-117">Para o macOS, você precisa instalar o OpenSSL, que é um pré-requisito do DotNet Core a extensão mssql usa.</span><span class="sxs-lookup"><span data-stu-id="bafc6-117">For macOS, you need to install OpenSSL which is a prerequiste for DotNet Core that mssql extention uses.</span></span> <span data-ttu-id="bafc6-118">Abra seu terminal e digite os seguintes comandos para instalar o **brew** e o **OpenSSL**.</span><span class="sxs-lookup"><span data-stu-id="bafc6-118">Open your terminal and enter the following commands to install **brew** and **OpenSSL**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a><span data-ttu-id="bafc6-119">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="bafc6-119">**Linux (Ubuntu)**</span></span>

<span data-ttu-id="bafc6-120">Nenhuma configuração especial é necessária.</span><span class="sxs-lookup"><span data-stu-id="bafc6-120">No special configuration needed.</span></span>

### <a name="windows"></a><span data-ttu-id="bafc6-121">**Windows**</span><span class="sxs-lookup"><span data-stu-id="bafc6-121">**Windows**</span></span>

<span data-ttu-id="bafc6-122">Nenhuma configuração especial é necessária.</span><span class="sxs-lookup"><span data-stu-id="bafc6-122">No special configuration needed.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="bafc6-123">Informações de conexão do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="bafc6-123">SQL server connection information</span></span>

<span data-ttu-id="bafc6-124">Obtenha as informações de conexão necessárias para se conectar ao Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="bafc6-124">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="bafc6-125">Você precisará do nome totalmente qualificado do servidor, nome do banco de dados e informações de logon nos próximos procedimentos.</span><span class="sxs-lookup"><span data-stu-id="bafc6-125">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="bafc6-126">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bafc6-126">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bafc6-127">Selecione **Bancos de Dados SQL** no menu à esquerda e clique em seu banco de dados na página **Bancos de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="bafc6-127">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="bafc6-128">Na página **Visão geral** do banco de dados, examine o nome totalmente qualificado do servidor, como mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="bafc6-128">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="bafc6-129">Você pode passar o mouse sobre o nome do servidor para abrir a opção **Clique para copiar**.</span><span class="sxs-lookup"><span data-stu-id="bafc6-129">You can hover over the server name to bring up the **Click to copy** option.</span></span>

   ![informações da conexão](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="bafc6-131">Se você esqueceu as informações de logon para o servidor do Banco de Dados SQL, navegue até a página do servidor para exibir o nome de administrador do servidor e, se necessário, redefinir a senha.</span><span class="sxs-lookup"><span data-stu-id="bafc6-131">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span> 

## <a name="set-language-mode-to-sql"></a><span data-ttu-id="bafc6-132">Definir o modo de linguagem para SQL</span><span class="sxs-lookup"><span data-stu-id="bafc6-132">Set language mode to SQL</span></span>

<span data-ttu-id="bafc6-133">Defina o modo de linguagem como **SQL** no Visual Studio Code para permitir comandos mssql e T-SQL IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="bafc6-133">Set the language mode is set to **SQL** in Visual Studio Code to enable mssql commands and T-SQL IntelliSense.</span></span>

1. <span data-ttu-id="bafc6-134">Abra uma nova janela do Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bafc6-134">Open a new Visual Studio Code window.</span></span> 

2. <span data-ttu-id="bafc6-135">Clique em **Texto sem Formatação** no canto inferior direito da barra de status.</span><span class="sxs-lookup"><span data-stu-id="bafc6-135">Click **Plain Text** in the lower right-hand corner of the status bar.</span></span>
3. <span data-ttu-id="bafc6-136">No menu suspenso **Selecionar modo de linguagem** aberto, digite **SQL**e pressione **ENTER** para definir o modo de linguagem para SQL.</span><span class="sxs-lookup"><span data-stu-id="bafc6-136">In the **Select language mode** drop-down menu that opens, type **SQL**, and then press **ENTER** to set the language mode to SQL.</span></span> 

   ![Modo de linguagem SQL](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-to-your-database"></a><span data-ttu-id="bafc6-138">Conectar-se ao seu banco de dados</span><span class="sxs-lookup"><span data-stu-id="bafc6-138">Connect to your database</span></span>

<span data-ttu-id="bafc6-139">Use o Visual Studio Code para estabelecer uma conexão com seu servidor de Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="bafc6-139">Use Visual Studio Code to establish a connection to your Azure SQL Database server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bafc6-140">Antes de continuar, verifique se você tem seu servidor, banco de dados e informações de logon prontos.</span><span class="sxs-lookup"><span data-stu-id="bafc6-140">Before continuing, make sure that you have your server, database, and login information ready.</span></span> <span data-ttu-id="bafc6-141">Depois que você começar a inserir as informações de perfil da conexão, se você mudar o foco do Visual Studio Code, terá que reiniciar a criação do perfil de conexão.</span><span class="sxs-lookup"><span data-stu-id="bafc6-141">Once you begin entering the connection profile information, if you change your focus from Visual Studio Code, you have to restart creating the connection profile.</span></span>
>

1. <span data-ttu-id="bafc6-142">No VS Code, pressione **CTRL + SHIFT + P** (ou **F1**) para abrir a Paleta de Comandos.</span><span class="sxs-lookup"><span data-stu-id="bafc6-142">In VS Code, press **CTRL+SHIFT+P** (or **F1**) to open the Command Palette.</span></span>

2. <span data-ttu-id="bafc6-143">Digite **sqlcon** e pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="bafc6-143">Type **sqlcon** and press **ENTER**.</span></span>

3. <span data-ttu-id="bafc6-144">Pressione **ENTER** para selecionar **Criar Perfil de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="bafc6-144">Press **ENTER** to select **Create Connection Profile**.</span></span> <span data-ttu-id="bafc6-145">Isso cria um perfil de conexão para a instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bafc6-145">This creates a connection profile for your SQL Server instance.</span></span>

4. <span data-ttu-id="bafc6-146">Siga os prompts para especificar as propriedades de conexão para o novo perfil de conexão.</span><span class="sxs-lookup"><span data-stu-id="bafc6-146">Follow the prompts to specify the connection properties for the new connection profile.</span></span> <span data-ttu-id="bafc6-147">Depois de especificar cada valor, pressione **ENTER** para continuar.</span><span class="sxs-lookup"><span data-stu-id="bafc6-147">After specifying each value, press **ENTER** to continue.</span></span> 

   | <span data-ttu-id="bafc6-148">Configuração</span><span class="sxs-lookup"><span data-stu-id="bafc6-148">Setting</span></span>       | <span data-ttu-id="bafc6-149">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="bafc6-149">Suggested value</span></span> | <span data-ttu-id="bafc6-150">Descrição</span><span class="sxs-lookup"><span data-stu-id="bafc6-150">Description</span></span> |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="bafc6-151">**Nome do servidor</span><span class="sxs-lookup"><span data-stu-id="bafc6-151">**Server name</span></span> | <span data-ttu-id="bafc6-152">O nome do servidor totalmente qualificado</span><span class="sxs-lookup"><span data-stu-id="bafc6-152">The fully qualified server name</span></span> | <span data-ttu-id="bafc6-153">O nome deve ser semelhante como: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="bafc6-153">The name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="bafc6-154">**Nome do banco de dados**</span><span class="sxs-lookup"><span data-stu-id="bafc6-154">**Database name**</span></span> | <span data-ttu-id="bafc6-155">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="bafc6-155">mySampleDatabase</span></span> | <span data-ttu-id="bafc6-156">O nome do banco de dados ao qual conectar.</span><span class="sxs-lookup"><span data-stu-id="bafc6-156">The name of the database to which to connect.</span></span> |
   | <span data-ttu-id="bafc6-157">**Autenticação**</span><span class="sxs-lookup"><span data-stu-id="bafc6-157">**Authentication**</span></span> | <span data-ttu-id="bafc6-158">Logon do SQL</span><span class="sxs-lookup"><span data-stu-id="bafc6-158">SQL Login</span></span>| <span data-ttu-id="bafc6-159">A Autenticação do SQL é o único tipo de autenticação que configuramos neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="bafc6-159">SQL Authentication is the only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="bafc6-160">**Nome de usuário**</span><span class="sxs-lookup"><span data-stu-id="bafc6-160">**User name**</span></span> | <span data-ttu-id="bafc6-161">A conta do administrador do servidor</span><span class="sxs-lookup"><span data-stu-id="bafc6-161">The server admin account</span></span> | <span data-ttu-id="bafc6-162">Esta é a conta que você especificou quando criou o servidor.</span><span class="sxs-lookup"><span data-stu-id="bafc6-162">This is the account that you specified when you created the server.</span></span> |
   | <span data-ttu-id="bafc6-163">**Senha (Logon do SQL)**</span><span class="sxs-lookup"><span data-stu-id="bafc6-163">**Password (SQL Login)**</span></span> | <span data-ttu-id="bafc6-164">A senha para sua conta do administrador do servidor</span><span class="sxs-lookup"><span data-stu-id="bafc6-164">The password for your server admin account</span></span> | <span data-ttu-id="bafc6-165">Esta é a senha que você especificou quando criou o servidor.</span><span class="sxs-lookup"><span data-stu-id="bafc6-165">This is the password that you specified when you created the server.</span></span> |
   | <span data-ttu-id="bafc6-166">**Salvar a Senha?**</span><span class="sxs-lookup"><span data-stu-id="bafc6-166">**Save Password?**</span></span> | <span data-ttu-id="bafc6-167">Sim ou não</span><span class="sxs-lookup"><span data-stu-id="bafc6-167">Yes or No</span></span> | <span data-ttu-id="bafc6-168">Selecione Sim se não quiser inserir a senha toda vez.</span><span class="sxs-lookup"><span data-stu-id="bafc6-168">Select Yes if you do not want to enter the password each time.</span></span> |
   | <span data-ttu-id="bafc6-169">**Insira um nome para este perfil**</span><span class="sxs-lookup"><span data-stu-id="bafc6-169">**Enter a name for this profile**</span></span> | <span data-ttu-id="bafc6-170">Um nome do perfil, como **mySampleDatabase**</span><span class="sxs-lookup"><span data-stu-id="bafc6-170">A profile name, such as **mySampleDatabase**</span></span> | <span data-ttu-id="bafc6-171">Um nome do perfil salvo acelera sua conexão nos logons subsequentes.</span><span class="sxs-lookup"><span data-stu-id="bafc6-171">A saved profile name speeds your connection on subsequent logins.</span></span> | 

5. <span data-ttu-id="bafc6-172">Pressione a tecla **ESC** para fechar a mensagem de informações que informa que o perfil foi criado e está conectado.</span><span class="sxs-lookup"><span data-stu-id="bafc6-172">Press the **ESC** key to close the info message that informs you that the profile is created and connected.</span></span>

6. <span data-ttu-id="bafc6-173">Verifique se sua conexão na barra de status.</span><span class="sxs-lookup"><span data-stu-id="bafc6-173">Verify your connection in the status bar.</span></span>

   ![Status da conexão](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a><span data-ttu-id="bafc6-175">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="bafc6-175">Query data</span></span>

<span data-ttu-id="bafc6-176">Use o seguinte código para consultar os 20 principais produtos por categoria usando a instrução [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) do Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="bafc6-176">Use the following code to query for the top 20 products by category using the [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="bafc6-177">Na janela **Editor**, insira a seguinte consulta na janela de consulta vazia:</span><span class="sxs-lookup"><span data-stu-id="bafc6-177">In the **Editor** window, enter the following query in the empty query window:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. <span data-ttu-id="bafc6-178">Pressione **CTRL + SHIFT + E** para recuperar dados das tabelas Product e ProductCategory.</span><span class="sxs-lookup"><span data-stu-id="bafc6-178">Press **CTRL+SHIFT+E** to retrieve data from the Product and ProductCategory tables.</span></span>

    ![Consultar](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a><span data-ttu-id="bafc6-180">Inserir dados</span><span class="sxs-lookup"><span data-stu-id="bafc6-180">Insert data</span></span>

<span data-ttu-id="bafc6-181">Use o código a seguir para inserir um novo produto na tabela SalesLT.Product usando a instrução [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) do Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="bafc6-181">Use the following code to insert a new product into the SalesLT.Product table using the [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="bafc6-182">Na janela **Editor**, exclua a consulta anterior e insira a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="bafc6-182">In the **Editor** window, delete the previous query and enter the following query:</span></span>

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

2. <span data-ttu-id="bafc6-183">Pressione **CTRL + SHIFT + E** para inserir uma nova linha na tabela Product.</span><span class="sxs-lookup"><span data-stu-id="bafc6-183">Press **CTRL+SHIFT+E** to insert a new row in the Product table.</span></span>

## <a name="update-data"></a><span data-ttu-id="bafc6-184">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="bafc6-184">Update data</span></span>

<span data-ttu-id="bafc6-185">Use o código a seguir para atualizar o novo produto que você adicionou anteriormente usando a instrução [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) do Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="bafc6-185">Use the following code to update the new product that you previously added using the [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1.  <span data-ttu-id="bafc6-186">Na janela **Editor**, exclua a consulta anterior e insira a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="bafc6-186">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="bafc6-187">Pressione **CTRL + SHIFT + E** para atualizar a linha especificada na tabela Product.</span><span class="sxs-lookup"><span data-stu-id="bafc6-187">Press **CTRL+SHIFT+E** to update the specified row in the Product table.</span></span>

## <a name="delete-data"></a><span data-ttu-id="bafc6-188">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="bafc6-188">Delete data</span></span>

<span data-ttu-id="bafc6-189">Use o código a seguir para excluir o novo produto que você adicionou anteriormente usando a instrução [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) do Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="bafc6-189">Use the following code to delete the new product that you previously added using the [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="bafc6-190">Na janela **Editor**, exclua a consulta anterior e insira a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="bafc6-190">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="bafc6-191">Pressione **CTRL + SHIFT + E** para excluir a linha especificada na tabela Product.</span><span class="sxs-lookup"><span data-stu-id="bafc6-191">Press **CTRL+SHIFT+E** to delete the specified row in the Product table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bafc6-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bafc6-192">Next steps</span></span>

- <span data-ttu-id="bafc6-193">Para conectar e consultar usando SQL Server Management Studio, veja [Conectar e consultar com o SSMS](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="bafc6-193">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md).</span></span>
- <span data-ttu-id="bafc6-194">Para obter um artigo da MSDN magazine sobre como usar o Visual Studio Code, veja [Criar um banco de dados IDE com a postagem de blog de extensão MSSQL](https://msdn.microsoft.com/magazine/mt809115).</span><span class="sxs-lookup"><span data-stu-id="bafc6-194">For an MSDN magazine article on using Visual Studio Code, see [Create a database IDE with MSSQL extension blog post](https://msdn.microsoft.com/magazine/mt809115).</span></span>
