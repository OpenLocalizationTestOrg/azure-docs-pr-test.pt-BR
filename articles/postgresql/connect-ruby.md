---
title: Conectar-se ao Banco de Dados do Azure para PostgreSQL usando Ruby | Microsoft Docs
description: "Este guia de início rápido fornece um exemplo de código Ruby que você pode usar para se conectar e consultar dados do Banco de Dados do Azure para PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 06/30/2017
ms.openlocfilehash: 9153a5a843dd5c18f27a3af232fea3b152240fe1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="a4d32-103">Banco de dados do Azure para PostgreSQL: usar Ruby para se conectar e consultar dados</span><span class="sxs-lookup"><span data-stu-id="a4d32-103">Azure Database for PostgreSQL: Use Ruby to connect and query data</span></span>
<span data-ttu-id="a4d32-104">Este guia de início rápido demonstra como se conectar a um banco de dados do Azure para PostgreSQL usando aplicativo [Ruby](https://www.ruby-lang.org).</span><span class="sxs-lookup"><span data-stu-id="a4d32-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="a4d32-105">Ele mostra como usar instruções SQL para consultar, inserir, atualizar e excluir dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a4d32-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="a4d32-106">Este artigo pressupõem que você está familiarizado com o desenvolvimento usando Ruby, mas que começou recentemente a trabalhar com o Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a4d32-106">This article assumes you are familiar with development using Ruby, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4d32-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a4d32-107">Prerequisites</span></span>
<span data-ttu-id="a4d32-108">Este guia de início rápido usa os recursos criados em um destes guias como ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="a4d32-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="a4d32-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="a4d32-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="a4d32-110">Criar Banco de dados - CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a4d32-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="a4d32-111">Instalar Ruby</span><span class="sxs-lookup"><span data-stu-id="a4d32-111">Install Ruby</span></span>
<span data-ttu-id="a4d32-112">Instale Ruby em seu próprio computador.</span><span class="sxs-lookup"><span data-stu-id="a4d32-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="a4d32-113">Windows</span><span class="sxs-lookup"><span data-stu-id="a4d32-113">Windows</span></span>
- <span data-ttu-id="a4d32-114">Baixe e instale a versão mais recente do [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a4d32-114">Download and Install the latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="a4d32-115">Na tela de conclusão do instalador MSI, marque a caixa que diz "Executar 'ridk install' para instalar o MSYS2 e o conjunto de ferramentas de desenvolvimento".</span><span class="sxs-lookup"><span data-stu-id="a4d32-115">On the finish screen of the MSI installer, check the box that says "Run 'ridk install' to install MSYS2 and development toolchain."</span></span> <span data-ttu-id="a4d32-116">Em seguida, clique em **Concluir** para iniciar o próximo instalador.</span><span class="sxs-lookup"><span data-stu-id="a4d32-116">Then click **Finish** to launch the next installer.</span></span>
- <span data-ttu-id="a4d32-117">O instalador RubyInstaller2 para Windows é iniciado.</span><span class="sxs-lookup"><span data-stu-id="a4d32-117">The RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="a4d32-118">Digite 2 para instalar a atualização do repositório MSYS2.</span><span class="sxs-lookup"><span data-stu-id="a4d32-118">Type 2 to install the MSYS2 repository update.</span></span> <span data-ttu-id="a4d32-119">Depois de terminar e retornar ao prompt de instalação, feche a janela de comando.</span><span class="sxs-lookup"><span data-stu-id="a4d32-119">After it finishes and returns to the installation prompt, close the command window.</span></span>
- <span data-ttu-id="a4d32-120">Inicie um novo prompt de comando (cmd) no menu Iniciar.</span><span class="sxs-lookup"><span data-stu-id="a4d32-120">Launch a new command prompt (cmd) from the Start menu.</span></span>
- <span data-ttu-id="a4d32-121">Teste a instalação do Ruby `ruby -v` para ver a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="a4d32-121">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="a4d32-122">Teste a instalação do Gem `gem -v` para ver a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="a4d32-122">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="a4d32-123">Crie o módulo PostgreSQL para Ruby usando o Gem com a execução do comando `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="a4d32-123">Build the PostgreSQL module for Ruby using Gem by running the command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="a4d32-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="a4d32-124">MacOS</span></span>
- <span data-ttu-id="a4d32-125">Instale o Ruby usando Homebrew, executando o comando `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="a4d32-125">Install Ruby using Homebrew by running the command `brew install ruby`.</span></span> <span data-ttu-id="a4d32-126">Para obter mais opções de instalação, consulte a [documentação da instalação](https://www.ruby-lang.org/en/documentation/installation/#homebrew) do Ruby</span><span class="sxs-lookup"><span data-stu-id="a4d32-126">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="a4d32-127">Teste a instalação do Ruby `ruby -v` para ver a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="a4d32-127">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="a4d32-128">Teste a instalação do Gem `gem -v` para ver a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="a4d32-128">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="a4d32-129">Crie o módulo PostgreSQL para Ruby usando o Gem com a execução do comando `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="a4d32-129">Build the PostgreSQL module for Ruby using Gem by running the command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="a4d32-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="a4d32-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="a4d32-131">Instale o Ruby executando o comando `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="a4d32-131">Install Ruby by running the command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="a4d32-132">Para obter mais opções de instalação, consulte a [documentação da instalação](https://www.ruby-lang.org/en/documentation/installation/) do Ruby</span><span class="sxs-lookup"><span data-stu-id="a4d32-132">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="a4d32-133">Teste a instalação do Ruby `ruby -v` para ver a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="a4d32-133">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="a4d32-134">Instale as atualizações mais recentes do Gem executando o comando `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="a4d32-134">Install the latest updates for Gem by running the command `sudo gem update --system`.</span></span>
- <span data-ttu-id="a4d32-135">Teste a instalação do Gem `gem -v` para ver a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="a4d32-135">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="a4d32-136">Instale gcc, make e outras ferramentas de compilação executando o comando `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="a4d32-136">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="a4d32-137">Instale as bibliotecas PostgreSQL executando o comando `sudo apt-get install libpq-dev`.</span><span class="sxs-lookup"><span data-stu-id="a4d32-137">Install the PostgreSQL libraries by running the command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="a4d32-138">Crie o módulo de pg do Ruby com Gem executando o comando `sudo gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="a4d32-138">Build the Ruby pg module using Gem by running the command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="a4d32-139">Executar código Ruby</span><span class="sxs-lookup"><span data-stu-id="a4d32-139">Run Ruby code</span></span> 
- <span data-ttu-id="a4d32-140">Salve o código em um arquivo de texto e salve o arquivo em uma pasta de projeto com extensão de arquivo .rb, como `C:\rubypostgres\read.rb` ou`/home/username/rubypostgres/read.rb`</span><span class="sxs-lookup"><span data-stu-id="a4d32-140">Save the code into a text file, and save the file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="a4d32-141">Para executar o código, inicie o prompt de comando ou o shell bash.</span><span class="sxs-lookup"><span data-stu-id="a4d32-141">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="a4d32-142">Altere o diretório para a pasta de projeto `cd rubypostgres` e digite o comando `ruby read.rb` para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a4d32-142">Change directory into your project folder `cd rubypostgres`, then type the command `ruby read.rb` to run the application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="a4d32-143">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="a4d32-143">Get connection information</span></span>
<span data-ttu-id="a4d32-144">Obtenha as informações de conexão necessárias para se conectar ao Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a4d32-144">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="a4d32-145">Você precisa das credenciais de logon e do nome do servidor totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="a4d32-145">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="a4d32-146">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a4d32-146">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a4d32-147">No menu à esquerda no Portal do Azure, clique em **Todos os recursos** e pesquise pelo servidor que você criou, como **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="a4d32-147">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="a4d32-148">Clique no nome do servidor **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="a4d32-148">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="a4d32-149">Selecione a página **Visão geral** do servidor.</span><span class="sxs-lookup"><span data-stu-id="a4d32-149">Select the server's **Overview** page.</span></span> <span data-ttu-id="a4d32-150">Anote o **Nome do servidor** e o **Nome de logon de administrador do servidor**.</span><span class="sxs-lookup"><span data-stu-id="a4d32-150">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="a4d32-151">![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="a4d32-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="a4d32-152">Se você se esquecer das informações de logon do servidor, navegue até a página **Visão Geral** para exibir o nome de logon do Administrador do servidor.</span><span class="sxs-lookup"><span data-stu-id="a4d32-152">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name.</span></span> <span data-ttu-id="a4d32-153">Se necessário, redefina a senha.</span><span class="sxs-lookup"><span data-stu-id="a4d32-153">If necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="a4d32-154">Conectar-se e criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="a4d32-154">Connect and create a table</span></span>
<span data-ttu-id="a4d32-155">Use o código a seguir para se conectar e criar uma tabela usando a instrução SQL **CREATE TABLE**, seguida por instruções SQL **INSERT INTO** para adicionar linhas à tabela.</span><span class="sxs-lookup"><span data-stu-id="a4d32-155">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="a4d32-156">O código usa um objeto [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) com construtor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) para se conectar ao Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a4d32-156">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="a4d32-157">Em seguida, ele chama o método [EXEC ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) para executar os comandos DROP, CREATE TABLE e INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="a4d32-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="a4d32-158">O código verifica erros usando a classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error).</span><span class="sxs-lookup"><span data-stu-id="a4d32-158">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="a4d32-159">Em seguida, ele chama o método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) para fechar a conexão antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="a4d32-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="a4d32-160">Substitua as cadeias de caracteres `host`, `database`, `user` e `password` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="a4d32-160">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database'

    # Drop previous table of same name if one exists
    connection.exec('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    connection.exec('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    connection.exec("INSERT INTO inventory VALUES(1, 'banana', 150)")
    connection.exec("INSERT INTO inventory VALUES(2, 'orange', 154)")
    connection.exec("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="read-data"></a><span data-ttu-id="a4d32-161">Ler dados</span><span class="sxs-lookup"><span data-stu-id="a4d32-161">Read data</span></span>
<span data-ttu-id="a4d32-162">Use o código a seguir para conectar-se e ler os dados usando uma instrução SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="a4d32-162">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="a4d32-163">O código usa um objeto [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) com construtor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) para se conectar ao Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a4d32-163">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="a4d32-164">Em seguida, ele chama o método [EXEC ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) para executar o comando SELECT, mantendo os resultados em um conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="a4d32-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the SELECT command, keeping the results in a result set.</span></span> <span data-ttu-id="a4d32-165">A coleção do conjunto de resultados é iterada usando o loop `resultSet.each do`, mantendo os valores da linha atual na variável `row`.</span><span class="sxs-lookup"><span data-stu-id="a4d32-165">The result set collection is iterated over using the `resultSet.each do` loop, keeping the current row values in the `row` variable.</span></span> <span data-ttu-id="a4d32-166">O código verifica erros usando a classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error).</span><span class="sxs-lookup"><span data-stu-id="a4d32-166">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="a4d32-167">Em seguida, ele chama o método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) para fechar a conexão antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="a4d32-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="a4d32-168">Substitua as cadeias de caracteres `host`, `database`, `user` e `password` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="a4d32-168">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :database => dbname, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    resultSet = connection.exec('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="update-data"></a><span data-ttu-id="a4d32-169">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="a4d32-169">Update data</span></span>
<span data-ttu-id="a4d32-170">Use o código a seguir para conectar-se e atualizar os dados usando uma instrução SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="a4d32-170">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="a4d32-171">O código usa um objeto [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) com construtor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) para se conectar ao Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a4d32-171">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="a4d32-172">Em seguida, ele chama o método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) para executar o comando UPDATE.</span><span class="sxs-lookup"><span data-stu-id="a4d32-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the UPDATE command.</span></span> <span data-ttu-id="a4d32-173">O código verifica erros usando a classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error).</span><span class="sxs-lookup"><span data-stu-id="a4d32-173">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="a4d32-174">Em seguida, ele chama o método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) para fechar a conexão antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="a4d32-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="a4d32-175">Substitua as cadeias de caracteres `host`, `database`, `user` e `password` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="a4d32-175">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a><span data-ttu-id="a4d32-176">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="a4d32-176">Delete data</span></span>
<span data-ttu-id="a4d32-177">Use o código a seguir para conectar-se e ler os dados usando uma instrução SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="a4d32-177">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="a4d32-178">O código usa um objeto [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) com construtor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) para se conectar ao Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="a4d32-178">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="a4d32-179">Em seguida, ele chama o método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) para executar o comando UPDATE.</span><span class="sxs-lookup"><span data-stu-id="a4d32-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the UPDATE command.</span></span> <span data-ttu-id="a4d32-180">O código verifica erros usando a classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error).</span><span class="sxs-lookup"><span data-stu-id="a4d32-180">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="a4d32-181">Em seguida, ele chama o método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) para fechar a conexão antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="a4d32-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="a4d32-182">Substitua as cadeias de caracteres `host`, `database`, `user` e `password` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="a4d32-182">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a><span data-ttu-id="a4d32-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4d32-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a4d32-184">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="a4d32-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
