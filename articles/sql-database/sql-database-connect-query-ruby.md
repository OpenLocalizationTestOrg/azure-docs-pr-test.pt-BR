---
title: Como usar o Ruby para consultar o Banco de Dados SQL do Azure| Microsoft Docs
description: "Este tópico mostra como usar o Ruby para criar um programa que se conecta a um Banco de Dados SQL do Azure e consultá-los usando instruções do Transact-SQL."
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
ms.openlocfilehash: 25ff9a9cfaa5494dbb006c84e235099fe51e6545
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-ruby-to-query-an-azure-sql-database"></a><span data-ttu-id="0fb01-103">Como usar o Ruby para consultar um banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="0fb01-103">Use Ruby to query an Azure SQL database</span></span>

<span data-ttu-id="0fb01-104">Este tutorial de início rápido demonstra como usar o [Ruby](https://www.ruby-lang.org) para criar um programa para se conectar a um banco de dados SQL do Azure e usar instruções Transact-SQL para consultar dados.</span><span class="sxs-lookup"><span data-stu-id="0fb01-104">This quick start tutorial demonstrates how to use [Ruby](https://www.ruby-lang.org) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fb01-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0fb01-105">Prerequisites</span></span>

<span data-ttu-id="0fb01-106">Para concluir este tutorial de início rápido, certifique-se de que tenha os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="0fb01-106">To complete this quick start tutorial, make sure you have the following prerequisites:</span></span>

- <span data-ttu-id="0fb01-107">Um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fb01-107">An Azure SQL database.</span></span> <span data-ttu-id="0fb01-108">Este início rápido usa os recursos criados em um destes inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="0fb01-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="0fb01-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="0fb01-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="0fb01-110">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="0fb01-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="0fb01-111">Criar Banco de dados - PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fb01-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="0fb01-112">Uma [regra de firewall no nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público do computador usado neste tutorial de início rápido.</span><span class="sxs-lookup"><span data-stu-id="0fb01-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="0fb01-113">Você instalou o Ruby e o software relacionado para seu sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="0fb01-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="0fb01-114">**MacOS**: instale o Homebrew, instale o rbenv e ruby-build, instale o Ruby e, em seguida, instale o FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="0fb01-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="0fb01-115">Confira a [Etapa 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="0fb01-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="0fb01-116">**Ubuntu**: instale os pré-requisitos do Ruby, instale o rbenv e ruby-build, instale o Ruby e, em seguida, instale o FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="0fb01-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="0fb01-117">Confira a [Etapa 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="0fb01-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="0fb01-118">Informações de conexão do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="0fb01-118">SQL server connection information</span></span>

<span data-ttu-id="0fb01-119">Obtenha as informações de conexão necessárias para se conectar ao Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fb01-119">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="0fb01-120">Você precisará do nome totalmente qualificado do servidor, nome do banco de dados e informações de logon nos próximos procedimentos.</span><span class="sxs-lookup"><span data-stu-id="0fb01-120">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="0fb01-121">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0fb01-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0fb01-122">Selecione **Bancos de Dados SQL** no menu à esquerda e clique em seu banco de dados na página **Bancos de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="0fb01-122">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="0fb01-123">Na página **Visão geral** de seu banco de dados, examine o nome do servidor totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="0fb01-123">On the **Overview** page for your database, review the fully qualified server name.</span></span> <span data-ttu-id="0fb01-124">Você pode passar o mouse sobre o nome do servidor para abrir a opção **Clique para copiar**, conforme exibido na imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="0fb01-124">You can hover over the server name to bring up the **Click to copy** option, as shown in the following image:</span></span>

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="0fb01-126">Se você esqueceu as informações de logon para o servidor do Banco de Dados SQL do Azure, navegue até a página do servidor do Banco de Dados SQL para exibir o nome de administrador do servidor e, se necessário, redefinir a senha.</span><span class="sxs-lookup"><span data-stu-id="0fb01-126">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0fb01-127">Você deve ter uma regra de firewall em vigor para o endereço IP público do computador em que você executa este tutorial.</span><span class="sxs-lookup"><span data-stu-id="0fb01-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="0fb01-128">Se você estiver em um computador diferente ou se tiver um endereço IP público diferente, crie uma [regra de firewall no nível de servidor usando o portal do Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="0fb01-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="0fb01-129">Inserir código para consultar o banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="0fb01-129">Insert code to query SQL database</span></span>

1. <span data-ttu-id="0fb01-130">Em seu editor de texto favorito, crie um novo arquivo, **sqltest.rb**</span><span class="sxs-lookup"><span data-stu-id="0fb01-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="0fb01-131">Substitua o conteúdo pelo código a seguir e adicione os valores apropriados para seu servidor, banco de dados, usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="0fb01-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="0fb01-132">Executar o código</span><span class="sxs-lookup"><span data-stu-id="0fb01-132">Run the code</span></span>

1. <span data-ttu-id="0fb01-133">No prompt de comando, execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="0fb01-133">At the command prompt, run the following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="0fb01-134">Verifique se as 20 linhas superiores são retornadas e, em seguida, feche a janela do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0fb01-134">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0fb01-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0fb01-135">Next Steps</span></span>
- [<span data-ttu-id="0fb01-136">Projetar seu primeiro banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="0fb01-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="0fb01-137">Repositório GitHub do TinyTDS</span><span class="sxs-lookup"><span data-stu-id="0fb01-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="0fb01-138">Relatar problemas ou fazer perguntas sobre o TinyTDS</span><span class="sxs-lookup"><span data-stu-id="0fb01-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="0fb01-139">Drivers Ruby para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0fb01-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
