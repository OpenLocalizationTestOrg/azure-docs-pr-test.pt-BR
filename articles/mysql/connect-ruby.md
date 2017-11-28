---
title: "Conexão com o banco de dados do Azure para MySQL usando Ruby | Microsoft Docs"
description: "Este guia de início rápido fornece vários exemplos de código Ruby que podem ser usados para conectar e consultar dados do banco de dados do Azure para MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/13/2017
ms.openlocfilehash: e54f1dccbae060c52f48bfeb277c045b99a91715
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="ff95d-103">Banco de dados do Azure para MySQL: como usar Ruby para conectar e consultar dados</span><span class="sxs-lookup"><span data-stu-id="ff95d-103">Azure Database for MySQL: Use Ruby to connect and query data</span></span>
<span data-ttu-id="ff95d-104">Este guia de início rápido mostra como se conectar a um banco de dados do Azure para MySQL usando um aplicativo [Ruby](https://www.ruby-lang.org) e o [mysql2](https://rubygems.org/gems/mysql2) gem de plataformas Mac, Ubuntu Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="ff95d-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and the [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="ff95d-105">Ele mostra como usar instruções SQL para consultar, inserir, atualizar e excluir dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ff95d-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="ff95d-106">Este artigo pressupõe que você está familiarizado com o desenvolvimento usando Ruby, mas que começou a trabalhar recentemente com o banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff95d-106">This article assumes you are familiar with development using Ruby, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff95d-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ff95d-107">Prerequisites</span></span>
<span data-ttu-id="ff95d-108">Este guia de início rápido usa os recursos criados em um destes guias como ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="ff95d-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="ff95d-109">Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ff95d-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="ff95d-110">Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ff95d-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="ff95d-111">Instalar Ruby</span><span class="sxs-lookup"><span data-stu-id="ff95d-111">Install Ruby</span></span>
<span data-ttu-id="ff95d-112">Instale o Ruby, o Gem e a biblioteca MySQL2 no seu computador.</span><span class="sxs-lookup"><span data-stu-id="ff95d-112">Install Ruby, Gem, and the MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="ff95d-113">Windows</span><span class="sxs-lookup"><span data-stu-id="ff95d-113">Windows</span></span>
1. <span data-ttu-id="ff95d-114">Baixe e instale a versão 2.3 do [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ff95d-114">Download and Install the 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="ff95d-115">Inicie um novo prompt de comando (cmd) no menu Iniciar.</span><span class="sxs-lookup"><span data-stu-id="ff95d-115">Launch a new command prompt (cmd) from the Start menu.</span></span>
3. <span data-ttu-id="ff95d-116">Altere o diretório para a versão 2.3 do diretório Ruby.</span><span class="sxs-lookup"><span data-stu-id="ff95d-116">Change directory into the Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="ff95d-117">Teste a instalação do Ruby executando o comando `ruby -v` para ver a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="ff95d-117">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
5. <span data-ttu-id="ff95d-118">Teste a instalação do Gem executando o comando `gem -v` para ver a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="ff95d-118">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
6. <span data-ttu-id="ff95d-119">Compile o módulo Mysql2 para Ruby usando o Gem com a execução do comando `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="ff95d-119">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="ff95d-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="ff95d-120">MacOS</span></span>
1. <span data-ttu-id="ff95d-121">Instale o Ruby usando Homebrew, executando o comando `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="ff95d-121">Install Ruby using Homebrew by running the command `brew install ruby`.</span></span> <span data-ttu-id="ff95d-122">Para obter mais opções de instalação, consulte a [documentação da instalação](https://www.ruby-lang.org/en/documentation/installation/#homebrew) do Ruby</span><span class="sxs-lookup"><span data-stu-id="ff95d-122">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="ff95d-123">Teste a instalação do Ruby executando o comando `ruby -v` para ver a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="ff95d-123">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="ff95d-124">Teste a instalação do Gem executando o comando `gem -v` para ver a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="ff95d-124">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
4. <span data-ttu-id="ff95d-125">Compile o módulo Mysql2 para Ruby usando o Gem com a execução do comando `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="ff95d-125">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="ff95d-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="ff95d-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="ff95d-127">Instale o Ruby executando o comando `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="ff95d-127">Install Ruby by running the command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="ff95d-128">Para obter mais opções de instalação, consulte a [documentação da instalação](https://www.ruby-lang.org/en/documentation/installation/) do Ruby</span><span class="sxs-lookup"><span data-stu-id="ff95d-128">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="ff95d-129">Teste a instalação do Ruby executando o comando `ruby -v` para ver a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="ff95d-129">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="ff95d-130">Instale as atualizações mais recentes do Gem executando o comando `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="ff95d-130">Install the latest updates for Gem by running the command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="ff95d-131">Teste a instalação do Gem executando o comando `gem -v` para ver a versão instalada.</span><span class="sxs-lookup"><span data-stu-id="ff95d-131">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
5. <span data-ttu-id="ff95d-132">Instale gcc, make e outras ferramentas de compilação executando o comando `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="ff95d-132">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="ff95d-133">Instale as bibliotecas de desenvolvedor de cliente do MySQL, executando o comando `sudo apt-get install libmysqlclient-dev`.</span><span class="sxs-lookup"><span data-stu-id="ff95d-133">Install the MySQL client developer libraries by running the command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="ff95d-134">Compile o módulo mysql2 para Ruby usando o Gem com a execução do comando `sudo gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="ff95d-134">Build the mysql2 module for Ruby using Gem by running the command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="ff95d-135">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="ff95d-135">Get connection information</span></span>
<span data-ttu-id="ff95d-136">Obtenha as informações de conexão necessárias para se conectar ao Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff95d-136">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="ff95d-137">Você precisa das credenciais de logon e do nome do servidor totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="ff95d-137">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="ff95d-138">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ff95d-138">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ff95d-139">No menu à esquerda no Portal do Azure, clique em **Todos os recursos** e pesquise pelo servidor que você criou, como **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="ff95d-139">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="ff95d-140">Clique no nome do servidor **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="ff95d-140">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="ff95d-141">Selecione a página **Propriedades** do servidor.</span><span class="sxs-lookup"><span data-stu-id="ff95d-141">Select the server's **Properties** page.</span></span> <span data-ttu-id="ff95d-142">Anote o **Nome do servidor** e o **Nome de logon de administrador do servidor**.</span><span class="sxs-lookup"><span data-stu-id="ff95d-142">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="ff95d-143">![Banco de Dados do Azure para MySQL – Logon de administrador do servidor](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="ff95d-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="ff95d-144">Se você se esquecer das informações de logon do servidor, navegue até a página **Visão Geral** para exibir o nome de logon do Administrador do servidor e, se necessário, redefinir a senha.</span><span class="sxs-lookup"><span data-stu-id="ff95d-144">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="ff95d-145">Executar código Ruby</span><span class="sxs-lookup"><span data-stu-id="ff95d-145">Run Ruby code</span></span> 
1. <span data-ttu-id="ff95d-146">Cole o código Ruby das seções abaixo em arquivos de texto e os salve em uma pasta de projeto com a extensão de arquivo .rb, como `C:\rubymysql\createtable.rb` ou `/home/username/rubymysql/createtable.rb`.</span><span class="sxs-lookup"><span data-stu-id="ff95d-146">Paste the Ruby code from the sections below into text files, and save the files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="ff95d-147">Para executar o código, inicie o prompt de comando ou o shell bash.</span><span class="sxs-lookup"><span data-stu-id="ff95d-147">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="ff95d-148">Altere o diretório para a pasta do seu projeto `cd rubymysql`</span><span class="sxs-lookup"><span data-stu-id="ff95d-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="ff95d-149">Digite o comando ruby seguido pelo nome do arquivo, como `ruby createtable.rb`, para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ff95d-149">Then type the ruby command followed by the file name, such as `ruby createtable.rb` to run the application.</span></span>
4. <span data-ttu-id="ff95d-150">No sistema operacional Windows, se o aplicativo ruby não estiver no seu caminho de variável de ambiente, você precisará usar o caminho completo para iniciar o aplicativo de nó, como `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="ff95d-150">On the Windows OS, if the ruby application is not in your path environment variable, you may need to use the full path to launch the node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="ff95d-151">Conectar-se e criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="ff95d-151">Connect and create a table</span></span>
<span data-ttu-id="ff95d-152">Use o código a seguir para se conectar e criar uma tabela usando a instrução SQL **CREATE TABLE**, seguida por instruções SQL **INSERT INTO** para adicionar linhas à tabela.</span><span class="sxs-lookup"><span data-stu-id="ff95d-152">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="ff95d-153">O código usa um método .new() de classe [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) para se conectar ao banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff95d-153">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="ff95d-154">Em seguida, ele chama o método [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) várias vezes para executar os comandos DROP, CREATE TABLE e INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="ff95d-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times to run the DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="ff95d-155">Em seguida, ele chama o método [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) para fechar a conexão antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="ff95d-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="ff95d-156">Substitua as cadeias de caracteres `host`, `database`, `username` e `password` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="ff95d-156">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection to database.'

    # Drop previous table of same name if one exists
    client.query('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    client.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    client.query("INSERT INTO inventory VALUES(1, 'banana', 150)")
    client.query("INSERT INTO inventory VALUES(2, 'orange', 154)")
    client.query("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="read-data"></a><span data-ttu-id="ff95d-157">Ler dados</span><span class="sxs-lookup"><span data-stu-id="ff95d-157">Read data</span></span>
<span data-ttu-id="ff95d-158">Use o código a seguir para conectar-se e ler os dados usando uma instrução SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="ff95d-158">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="ff95d-159">O código usa um método .new() de classe [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) para se conectar ao banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff95d-159">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="ff95d-160">Em seguida, ele chama o método [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) para executar os comandos SELECT.</span><span class="sxs-lookup"><span data-stu-id="ff95d-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the SELECT commands.</span></span> <span data-ttu-id="ff95d-161">Em seguida, ele chama o método [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) para fechar a conexão antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="ff95d-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="ff95d-162">Substitua as cadeias de caracteres `host`, `database`, `username` e `password` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="ff95d-162">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection to database.'

    # Read data
    resultSet = client.query('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end
    puts 'Read ' + resultSet.count.to_s + ' row(s).'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="update-data"></a><span data-ttu-id="ff95d-163">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="ff95d-163">Update data</span></span>
<span data-ttu-id="ff95d-164">Use o código a seguir para conectar-se e atualizar os dados usando uma instrução SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="ff95d-164">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="ff95d-165">O código usa um método .new() de classe [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) para se conectar ao banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff95d-165">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="ff95d-166">Em seguida, ele chama o método [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) para executar os comandos UPDATE.</span><span class="sxs-lookup"><span data-stu-id="ff95d-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the UPDATE commands.</span></span> <span data-ttu-id="ff95d-167">Em seguida, ele chama o método [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) para fechar a conexão antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="ff95d-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="ff95d-168">Substitua as cadeias de caracteres `host`, `database`, `username` e `password` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="ff95d-168">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection to database.'

    # Update data
   client.query('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
   puts 'Updated 1 row of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```


## <a name="delete-data"></a><span data-ttu-id="ff95d-169">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="ff95d-169">Delete data</span></span>
<span data-ttu-id="ff95d-170">Use o código a seguir para conectar-se e ler os dados usando uma instrução SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="ff95d-170">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="ff95d-171">O código usa um método .new() de classe [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) para se conectar ao banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff95d-171">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="ff95d-172">Em seguida, ele chama o método [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) para executar os comandos DELETE.</span><span class="sxs-lookup"><span data-stu-id="ff95d-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the DELETE commands.</span></span> <span data-ttu-id="ff95d-173">Em seguida, ele chama o método [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) para fechar a conexão antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="ff95d-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="ff95d-174">Substitua as cadeias de caracteres `host`, `database`, `username` e `password` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="ff95d-174">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection to database.'

    # Delete data
    resultSet = client.query('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="next-steps"></a><span data-ttu-id="ff95d-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ff95d-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ff95d-176">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="ff95d-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
