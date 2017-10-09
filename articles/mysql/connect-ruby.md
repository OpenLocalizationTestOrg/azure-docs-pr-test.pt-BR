---
title: "TooAzure banco de dados de conexão para MySQL usando o Ruby | Microsoft Docs"
description: "Este guia de início rápido fornece vários exemplos de código Ruby, você pode usar tooconnect e consultar dados do banco de dados MySQL."
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
ms.openlocfilehash: ff0880dcc24e96f467c9092bc663ce3dc4c2637a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="e6119-103">Banco de dados do Azure para MySQL: Use Ruby tooconnect e consultar dados</span><span class="sxs-lookup"><span data-stu-id="e6119-103">Azure Database for MySQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="e6119-104">Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para MySQL usando um [Ruby](https://www.ruby-lang.org) aplicativo e hello [mysql2](https://rubygems.org/gems/mysql2) gem de plataformas Mac, Ubuntu Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="e6119-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and hello [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="e6119-105">Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6119-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="e6119-106">Este artigo pressupõe que você esteja familiarizado com o desenvolvimento usando o Ruby, mas que são novos tooworking com o banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="e6119-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6119-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e6119-107">Prerequisites</span></span>
<span data-ttu-id="e6119-108">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="e6119-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="e6119-109">Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e6119-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="e6119-110">Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e6119-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="e6119-111">Instalar Ruby</span><span class="sxs-lookup"><span data-stu-id="e6119-111">Install Ruby</span></span>
<span data-ttu-id="e6119-112">Instale Ruby, Gem e biblioteca de MySQL2 Olá em sua própria máquina.</span><span class="sxs-lookup"><span data-stu-id="e6119-112">Install Ruby, Gem, and hello MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="e6119-113">Windows</span><span class="sxs-lookup"><span data-stu-id="e6119-113">Windows</span></span>
1. <span data-ttu-id="e6119-114">Baixar e instalar a versão de hello 2.3 do [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e6119-114">Download and Install hello 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="e6119-115">Inicie um novo prompt de comando (cmd) saudação do menu de início.</span><span class="sxs-lookup"><span data-stu-id="e6119-115">Launch a new command prompt (cmd) from hello Start menu.</span></span>
3. <span data-ttu-id="e6119-116">Altere o diretório em Olá diretório Ruby para versão 2.3.</span><span class="sxs-lookup"><span data-stu-id="e6119-116">Change directory into hello Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="e6119-117">Saudação de teste Ruby instalação executando o comando Olá `ruby -v` toosee versão de hello instalada.</span><span class="sxs-lookup"><span data-stu-id="e6119-117">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="e6119-118">Testar a instalação de Gem Olá executando o comando Olá `gem -v` toosee versão de hello instalada.</span><span class="sxs-lookup"><span data-stu-id="e6119-118">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
6. <span data-ttu-id="e6119-119">Criar módulo Olá Mysql2 para Ruby usando Gem ao executar o comando Olá `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="e6119-119">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="e6119-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="e6119-120">MacOS</span></span>
1. <span data-ttu-id="e6119-121">Instalar Ruby usando Homebrew ao executar o comando Olá `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="e6119-121">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="e6119-122">Para obter mais opções de instalação, consulte Olá Ruby [documentação de instalação](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span><span class="sxs-lookup"><span data-stu-id="e6119-122">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="e6119-123">Saudação de teste Ruby instalação executando o comando Olá `ruby -v` toosee versão de hello instalada.</span><span class="sxs-lookup"><span data-stu-id="e6119-123">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="e6119-124">Testar a instalação de Gem Olá executando o comando Olá `gem -v` toosee versão de hello instalada.</span><span class="sxs-lookup"><span data-stu-id="e6119-124">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
4. <span data-ttu-id="e6119-125">Criar módulo Olá Mysql2 para Ruby usando Gem ao executar o comando Olá `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="e6119-125">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="e6119-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="e6119-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="e6119-127">Instalar Ruby, executando o comando Olá `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="e6119-127">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="e6119-128">Para obter mais opções de instalação, consulte Olá Ruby [documentação de instalação](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="e6119-128">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="e6119-129">Saudação de teste Ruby instalação executando o comando Olá `ruby -v` toosee versão de hello instalada.</span><span class="sxs-lookup"><span data-stu-id="e6119-129">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="e6119-130">Instalar as atualizações mais recentes de saudação para Gem executando o comando Olá `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="e6119-130">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="e6119-131">Testar a instalação de Gem Olá executando o comando Olá `gem -v` toosee versão de hello instalada.</span><span class="sxs-lookup"><span data-stu-id="e6119-131">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="e6119-132">Instalar gcc hello, verifique e outras ferramentas de compilação, executando o comando Olá `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="e6119-132">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="e6119-133">Instalar bibliotecas para desenvolvedores Olá MySQL cliente executando o comando Olá `sudo apt-get install libmysqlclient-dev`.</span><span class="sxs-lookup"><span data-stu-id="e6119-133">Install hello MySQL client developer libraries by running hello command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="e6119-134">Criar o módulo de mysql2 de saudação para Ruby usando Gem ao executar o comando Olá `sudo gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="e6119-134">Build hello mysql2 module for Ruby using Gem by running hello command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="e6119-135">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="e6119-135">Get connection information</span></span>
<span data-ttu-id="e6119-136">Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="e6119-136">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="e6119-137">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="e6119-137">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="e6119-138">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e6119-138">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e6119-139">No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e procure o servidor de saudação você ter creased, como **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="e6119-139">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="e6119-140">Clique em nome do servidor de saudação **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="e6119-140">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="e6119-141">Servidor de saudação selecione **propriedades** página.</span><span class="sxs-lookup"><span data-stu-id="e6119-141">Select hello server's **Properties** page.</span></span> <span data-ttu-id="e6119-142">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="e6119-142">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="e6119-143">![Banco de Dados do Azure para MySQL – Logon de administrador do servidor](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="e6119-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="e6119-144">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="e6119-144">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="e6119-145">Executar código Ruby</span><span class="sxs-lookup"><span data-stu-id="e6119-145">Run Ruby code</span></span> 
1. <span data-ttu-id="e6119-146">Colar Olá código Ruby das seções Olá abaixo em arquivos de texto e salvar arquivos de saudação em uma pasta de projeto com RB de extensão de arquivo, como `C:\rubymysql\createtable.rb` ou `/home/username/rubymysql/createtable.rb`.</span><span class="sxs-lookup"><span data-stu-id="e6119-146">Paste hello Ruby code from hello sections below into text files, and save hello files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="e6119-147">código de saudação toorun, inicie o prompt de comando hello ou bash shell.</span><span class="sxs-lookup"><span data-stu-id="e6119-147">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="e6119-148">Altere o diretório para a pasta do seu projeto `cd rubymysql`</span><span class="sxs-lookup"><span data-stu-id="e6119-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="e6119-149">Digite comando Olá ruby seguido pelo nome de arquivo hello, tais como `ruby createtable.rb` toorun aplicativo de hello.</span><span class="sxs-lookup"><span data-stu-id="e6119-149">Then type hello ruby command followed by hello file name, such as `ruby createtable.rb` toorun hello application.</span></span>
4. <span data-ttu-id="e6119-150">Em Olá sistema operacional Windows, se o aplicativo hello ruby não está em sua variável de ambiente path, talvez seja necessário aplicativo toouse Olá caminho completo toolaunch hello nó, como`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="e6119-150">On hello Windows OS, if hello ruby application is not in your path environment variable, you may need toouse hello full path toolaunch hello node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="e6119-151">Conectar-se e criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="e6119-151">Connect and create a table</span></span>
<span data-ttu-id="e6119-152">A seguir use Olá tooconnect de código e criar uma tabela usando **CREATE TABLE** instrução SQL, seguida por **INSERT INTO** linhas de tooadd de instruções SQL em tabela hello.</span><span class="sxs-lookup"><span data-stu-id="e6119-152">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="e6119-153">Olá código usa um [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() método tooconnect tooAzure banco de dados de classe para MySQL.</span><span class="sxs-lookup"><span data-stu-id="e6119-153">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="e6119-154">Em seguida, ele chama o método [Query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) várias vezes toorun hello, CREATE TABLE, comandos DROP e INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="e6119-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="e6119-155">Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose conexão de saudação antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="e6119-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="e6119-156">Substituir saudação `host`, `database`, `username`, e `password` cadeias de caracteres com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e6119-156">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
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
    puts 'Successfully created connection toodatabase.'

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

## <a name="read-data"></a><span data-ttu-id="e6119-157">Ler dados</span><span class="sxs-lookup"><span data-stu-id="e6119-157">Read data</span></span>
<span data-ttu-id="e6119-158">A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e6119-158">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="e6119-159">Olá código usa um [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() método tooconnect tooAzure banco de dados de classe para MySQL.</span><span class="sxs-lookup"><span data-stu-id="e6119-159">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="e6119-160">Em seguida, ele chama o método [Query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) comandos SELECT de saudação toorun.</span><span class="sxs-lookup"><span data-stu-id="e6119-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello SELECT commands.</span></span> <span data-ttu-id="e6119-161">Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose conexão de saudação antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="e6119-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="e6119-162">Substituir saudação `host`, `database`, `username`, e `password` cadeias de caracteres com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e6119-162">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

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

## <a name="update-data"></a><span data-ttu-id="e6119-163">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="e6119-163">Update data</span></span>
<span data-ttu-id="e6119-164">A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e6119-164">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="e6119-165">Olá código usa um [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() método tooconnect tooAzure banco de dados de classe para MySQL.</span><span class="sxs-lookup"><span data-stu-id="e6119-165">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="e6119-166">Em seguida, ele chama o método [Query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun comandos de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6119-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello UPDATE commands.</span></span> <span data-ttu-id="e6119-167">Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose conexão de saudação antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="e6119-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="e6119-168">Substituir saudação `host`, `database`, `username`, e `password` cadeias de caracteres com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e6119-168">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

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


## <a name="delete-data"></a><span data-ttu-id="e6119-169">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="e6119-169">Delete data</span></span>
<span data-ttu-id="e6119-170">A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e6119-170">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="e6119-171">Olá código usa um [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() método tooconnect tooAzure banco de dados de classe para MySQL.</span><span class="sxs-lookup"><span data-stu-id="e6119-171">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="e6119-172">Em seguida, ele chama o método [Query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun comandos de exclusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6119-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE commands.</span></span> <span data-ttu-id="e6119-173">Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose conexão de saudação antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="e6119-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="e6119-174">Substituir saudação `host`, `database`, `username`, e `password` cadeias de caracteres com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e6119-174">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

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

## <a name="next-steps"></a><span data-ttu-id="e6119-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e6119-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e6119-176">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="e6119-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
