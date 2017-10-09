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
# <a name="use-ruby-tooquery-an-azure-sql-database"></a><span data-ttu-id="bf1bf-103">Use tooquery Ruby um banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bf1bf-103">Use Ruby tooquery an Azure SQL database</span></span>

<span data-ttu-id="bf1bf-104">Este tutorial de início rápido demonstra como toouse [Ruby](https://www.ruby-lang.org) toocreate tooan de tooconnect um programa SQL do Azure do banco de dados e usar dados de tooquery de instruções Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-104">This quick start tutorial demonstrates how toouse [Ruby](https://www.ruby-lang.org) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf1bf-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bf1bf-105">Prerequisites</span></span>

<span data-ttu-id="bf1bf-106">toocomplete rápida nesse tutorial de início, certifique-se de ter Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf1bf-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="bf1bf-107">Um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-107">An Azure SQL database.</span></span> <span data-ttu-id="bf1bf-108">Esse início rápido usa recursos de saudação criados em um desses inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="bf1bf-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="bf1bf-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="bf1bf-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="bf1bf-110">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="bf1bf-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="bf1bf-111">Criar Banco de dados - PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf1bf-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="bf1bf-112">Um [regra de firewall de nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de saudação do computador Olá usar para este tutorial de início rápido.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="bf1bf-113">Você instalou o Ruby e o software relacionado para seu sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="bf1bf-114">**MacOS**: instale o Homebrew, instale o rbenv e ruby-build, instale o Ruby e, em seguida, instale o FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="bf1bf-115">Confira a [Etapa 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="bf1bf-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="bf1bf-116">**Ubuntu**: instale os pré-requisitos do Ruby, instale o rbenv e ruby-build, instale o Ruby e, em seguida, instale o FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="bf1bf-117">Confira a [Etapa 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="bf1bf-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="bf1bf-118">Informações de conexão do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="bf1bf-118">SQL server connection information</span></span>

<span data-ttu-id="bf1bf-119">Obter Olá conexão informações necessárias tooconnect toohello SQL Azure banco de dados.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-119">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="bf1bf-120">Será necessário o nome totalmente qualificado do servidor de saudação, nome do banco de dados e informações de logon em procedimentos Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-120">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="bf1bf-121">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bf1bf-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bf1bf-122">Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-122">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="bf1bf-123">Em Olá **visão geral** para seu banco de dados, examine o nome totalmente qualificado do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-123">On hello **Overview** page for your database, review hello fully qualified server name.</span></span> <span data-ttu-id="bf1bf-124">Você pode focalizar Olá toobring de nome de servidor backup Olá **clique toocopy** opção, conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf1bf-124">You can hover over hello server name toobring up hello **Click toocopy** option, as shown in hello following image:</span></span>

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="bf1bf-126">Se você tiver esquecido a informações de logon Olá para o servidor de banco de dados de SQL do Azure, navegue toohello banco de dados do SQL server página tooview Olá administrador nome do servidor e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-126">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf1bf-127">Você deve ter uma regra de firewall em vigor para o endereço IP público de saudação do computador Olá em que você executa este tutorial.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="bf1bf-128">Se você estiver em um computador diferente ou ter um endereço IP público diferente, crie um [regra de firewall de nível de servidor usando Olá portal do Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="bf1bf-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="bf1bf-129">Insira o banco de dados SQL do código tooquery</span><span class="sxs-lookup"><span data-stu-id="bf1bf-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="bf1bf-130">Em seu editor de texto favorito, crie um novo arquivo, **sqltest.rb**</span><span class="sxs-lookup"><span data-stu-id="bf1bf-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="bf1bf-131">Substitua o conteúdo de saudação com hello seguinte código e adicionar os valores apropriados para seu servidor, banco de dados, usuário e senha hello.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="bf1bf-132">Executar o código de saudação</span><span class="sxs-lookup"><span data-stu-id="bf1bf-132">Run hello code</span></span>

1. <span data-ttu-id="bf1bf-133">No prompt de comando hello, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf1bf-133">At hello command prompt, run hello following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="bf1bf-134">Verifique se que 20 linhas de saudação principais são retornadas e, em seguida, feche a janela do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bf1bf-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bf1bf-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf1bf-135">Next Steps</span></span>
- [<span data-ttu-id="bf1bf-136">Projetar seu primeiro banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="bf1bf-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="bf1bf-137">Repositório GitHub do TinyTDS</span><span class="sxs-lookup"><span data-stu-id="bf1bf-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="bf1bf-138">Relatar problemas ou fazer perguntas sobre o TinyTDS</span><span class="sxs-lookup"><span data-stu-id="bf1bf-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="bf1bf-139">Drivers Ruby para SQL Server</span><span class="sxs-lookup"><span data-stu-id="bf1bf-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
