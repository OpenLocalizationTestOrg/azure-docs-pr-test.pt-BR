---
title: aaaConnect tooAzure banco de dados PostgreSQL usando Ruby | Microsoft Docs
description: "Este guia de início rápido fornece um exemplo de código Ruby, você pode usar tooconnect e consultar dados do banco de dados PostgreSQL."
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
ms.openlocfilehash: 7a0c8c92023452b40ca19d76fa659744f3e9a236
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="cdda7-103">Banco de dados do Azure para PostgreSQL: Use Ruby tooconnect e consultar dados</span><span class="sxs-lookup"><span data-stu-id="cdda7-103">Azure Database for PostgreSQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="cdda7-104">Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para PostgreSQL usando um [Ruby](https://www.ruby-lang.org) aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cdda7-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="cdda7-105">Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdda7-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="cdda7-106">Este artigo pressupõe que você esteja familiarizado com o desenvolvimento usando o Ruby, mas que são novos tooworking com o banco de dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="cdda7-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdda7-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cdda7-107">Prerequisites</span></span>
<span data-ttu-id="cdda7-108">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="cdda7-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="cdda7-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="cdda7-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="cdda7-110">Criar Banco de dados - CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cdda7-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="cdda7-111">Instalar Ruby</span><span class="sxs-lookup"><span data-stu-id="cdda7-111">Install Ruby</span></span>
<span data-ttu-id="cdda7-112">Instale Ruby em seu próprio computador.</span><span class="sxs-lookup"><span data-stu-id="cdda7-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="cdda7-113">Windows</span><span class="sxs-lookup"><span data-stu-id="cdda7-113">Windows</span></span>
- <span data-ttu-id="cdda7-114">Download e instalação Olá última versão do [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="cdda7-114">Download and Install hello latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="cdda7-115">Em Olá concluir a tela do instalador MSI de hello, marque caixa de saudação que diz "Run 'ridk instalar' tooinstall MSYS2 e ferramentas de desenvolvimento."</span><span class="sxs-lookup"><span data-stu-id="cdda7-115">On hello finish screen of hello MSI installer, check hello box that says "Run 'ridk install' tooinstall MSYS2 and development toolchain."</span></span> <span data-ttu-id="cdda7-116">Em seguida, clique em **concluir** instalador próximo do toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="cdda7-116">Then click **Finish** toolaunch hello next installer.</span></span>
- <span data-ttu-id="cdda7-117">Olá RubyInstaller2 para o Windows installer é iniciado.</span><span class="sxs-lookup"><span data-stu-id="cdda7-117">hello RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="cdda7-118">Tipo de atualização do repositório de saudação MSYS2 tooinstall 2.</span><span class="sxs-lookup"><span data-stu-id="cdda7-118">Type 2 tooinstall hello MSYS2 repository update.</span></span> <span data-ttu-id="cdda7-119">Depois de terminar e retorna o prompt de instalação do toohello, feche a janela de comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdda7-119">After it finishes and returns toohello installation prompt, close hello command window.</span></span>
- <span data-ttu-id="cdda7-120">Inicie um novo prompt de comando (cmd) saudação do menu de início.</span><span class="sxs-lookup"><span data-stu-id="cdda7-120">Launch a new command prompt (cmd) from hello Start menu.</span></span>
- <span data-ttu-id="cdda7-121">Saudação de teste instalação Ruby `ruby -v` toosee versão de hello instalada.</span><span class="sxs-lookup"><span data-stu-id="cdda7-121">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="cdda7-122">Testar a instalação do Gem Olá `gem -v` toosee versão de hello instalada.</span><span class="sxs-lookup"><span data-stu-id="cdda7-122">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="cdda7-123">Criar módulo de PostgreSQL Olá para Ruby usando Gem ao executar o comando Olá `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="cdda7-123">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="cdda7-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="cdda7-124">MacOS</span></span>
- <span data-ttu-id="cdda7-125">Instalar Ruby usando Homebrew ao executar o comando Olá `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="cdda7-125">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="cdda7-126">Para obter mais opções de instalação, consulte Olá Ruby [documentação da instalação](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span><span class="sxs-lookup"><span data-stu-id="cdda7-126">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="cdda7-127">Saudação de teste instalação Ruby `ruby -v` toosee versão de hello instalada.</span><span class="sxs-lookup"><span data-stu-id="cdda7-127">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="cdda7-128">Testar a instalação do Gem Olá `gem -v` toosee versão de hello instalada.</span><span class="sxs-lookup"><span data-stu-id="cdda7-128">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="cdda7-129">Criar módulo de PostgreSQL Olá para Ruby usando Gem ao executar o comando Olá `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="cdda7-129">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="cdda7-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="cdda7-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="cdda7-131">Instalar Ruby, executando o comando Olá `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="cdda7-131">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="cdda7-132">Para obter mais opções de instalação, consulte Olá Ruby [documentação de instalação](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="cdda7-132">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="cdda7-133">Saudação de teste instalação Ruby `ruby -v` toosee versão de hello instalada.</span><span class="sxs-lookup"><span data-stu-id="cdda7-133">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="cdda7-134">Instalar as atualizações mais recentes de saudação para Gem executando o comando Olá `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="cdda7-134">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
- <span data-ttu-id="cdda7-135">Testar a instalação do Gem Olá `gem -v` toosee versão de hello instalada.</span><span class="sxs-lookup"><span data-stu-id="cdda7-135">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="cdda7-136">Instalar gcc hello, verifique e outras ferramentas de compilação, executando o comando Olá `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="cdda7-136">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="cdda7-137">Instalar bibliotecas de PostgreSQL de saudação executando o comando Olá `sudo apt-get install libpq-dev`.</span><span class="sxs-lookup"><span data-stu-id="cdda7-137">Install hello PostgreSQL libraries by running hello command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="cdda7-138">Criar hello pg Ruby módulo usando Gem ao executar o comando Olá `sudo gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="cdda7-138">Build hello Ruby pg module using Gem by running hello command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="cdda7-139">Executar código Ruby</span><span class="sxs-lookup"><span data-stu-id="cdda7-139">Run Ruby code</span></span> 
- <span data-ttu-id="cdda7-140">Salve o código de saudação em um arquivo de texto e salve o arquivo de saudação em uma pasta de projeto com RB de extensão de arquivo, como `C:\rubypostgres\read.rb` ou`/home/username/rubypostgres/read.rb`</span><span class="sxs-lookup"><span data-stu-id="cdda7-140">Save hello code into a text file, and save hello file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="cdda7-141">código de saudação toorun, inicie o prompt de comando hello ou bash shell.</span><span class="sxs-lookup"><span data-stu-id="cdda7-141">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="cdda7-142">Altere o diretório para a pasta de projeto `cd rubypostgres`, em seguida, digite o comando Olá `ruby read.rb` aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="cdda7-142">Change directory into your project folder `cd rubypostgres`, then type hello command `ruby read.rb` toorun hello application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="cdda7-143">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="cdda7-143">Get connection information</span></span>
<span data-ttu-id="cdda7-144">Obter Olá conexão informações necessárias tooconnect toohello banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="cdda7-144">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="cdda7-145">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="cdda7-145">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="cdda7-146">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cdda7-146">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cdda7-147">No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e pesquisa para o servidor de saudação que você criou, como **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="cdda7-147">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="cdda7-148">Clique em nome do servidor de saudação **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="cdda7-148">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="cdda7-149">Servidor de saudação selecione **visão geral** página.</span><span class="sxs-lookup"><span data-stu-id="cdda7-149">Select hello server's **Overview** page.</span></span> <span data-ttu-id="cdda7-150">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="cdda7-150">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="cdda7-151">![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="cdda7-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="cdda7-152">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** nome de logon do administrador de servidor do página tooview hello.</span><span class="sxs-lookup"><span data-stu-id="cdda7-152">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name.</span></span> <span data-ttu-id="cdda7-153">Se necessário, Olá redefinição da senha.</span><span class="sxs-lookup"><span data-stu-id="cdda7-153">If necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="cdda7-154">Conectar-se e criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="cdda7-154">Connect and create a table</span></span>
<span data-ttu-id="cdda7-155">A seguir use Olá tooconnect de código e criar uma tabela usando **CREATE TABLE** instrução SQL, seguida por **INSERT INTO** linhas de tooadd de instruções SQL em tabela hello.</span><span class="sxs-lookup"><span data-stu-id="cdda7-155">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="cdda7-156">Olá código usa um [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto com construtor [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="cdda7-156">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="cdda7-157">Em seguida, ele chama o método [EXEC ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello, CREATE TABLE, comandos DROP e INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="cdda7-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="cdda7-158">Olá código verifica erros usando Olá [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe.</span><span class="sxs-lookup"><span data-stu-id="cdda7-158">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="cdda7-159">Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose conexão de saudação antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="cdda7-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="cdda7-160">Substituir saudação `host`, `database`, `user`, e `password` cadeias de caracteres com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="cdda7-160">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
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
    puts 'Successfully created connection toodatabase'

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

## <a name="read-data"></a><span data-ttu-id="cdda7-161">Ler dados</span><span class="sxs-lookup"><span data-stu-id="cdda7-161">Read data</span></span>
<span data-ttu-id="cdda7-162">A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="cdda7-162">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="cdda7-163">Olá código usa um [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto com construtor [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="cdda7-163">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="cdda7-164">Em seguida, ele chama o método [EXEC ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Olá comando SELECT, mantendo a saudação de resultados em um conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="cdda7-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello SELECT command, keeping hello results in a result set.</span></span> <span data-ttu-id="cdda7-165">Olá coleção do conjunto de resultados é iterada usando Olá `resultSet.each do` loop, manter os valores de linha atual Olá Olá `row` variável.</span><span class="sxs-lookup"><span data-stu-id="cdda7-165">hello result set collection is iterated over using hello `resultSet.each do` loop, keeping hello current row values in hello `row` variable.</span></span> <span data-ttu-id="cdda7-166">Olá código verifica erros usando Olá [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe.</span><span class="sxs-lookup"><span data-stu-id="cdda7-166">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="cdda7-167">Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose conexão de saudação antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="cdda7-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="cdda7-168">Substituir saudação `host`, `database`, `user`, e `password` cadeias de caracteres com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="cdda7-168">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

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

## <a name="update-data"></a><span data-ttu-id="cdda7-169">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="cdda7-169">Update data</span></span>
<span data-ttu-id="cdda7-170">A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="cdda7-170">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="cdda7-171">Olá código usa um [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto com construtor [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="cdda7-171">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="cdda7-172">Em seguida, ele chama o método [EXEC ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Olá comando UPDATE.</span><span class="sxs-lookup"><span data-stu-id="cdda7-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="cdda7-173">Olá código verifica erros usando Olá [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe.</span><span class="sxs-lookup"><span data-stu-id="cdda7-173">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="cdda7-174">Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose conexão de saudação antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="cdda7-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="cdda7-175">Substituir saudação `host`, `database`, `user`, e `password` cadeias de caracteres com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="cdda7-175">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a><span data-ttu-id="cdda7-176">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="cdda7-176">Delete data</span></span>
<span data-ttu-id="cdda7-177">A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="cdda7-177">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="cdda7-178">Olá código usa um [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto com construtor [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="cdda7-178">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="cdda7-179">Em seguida, ele chama o método [EXEC ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Olá comando UPDATE.</span><span class="sxs-lookup"><span data-stu-id="cdda7-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="cdda7-180">Olá código verifica erros usando Olá [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe.</span><span class="sxs-lookup"><span data-stu-id="cdda7-180">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="cdda7-181">Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose conexão de saudação antes de encerrar.</span><span class="sxs-lookup"><span data-stu-id="cdda7-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="cdda7-182">Substituir saudação `host`, `database`, `user`, e `password` cadeias de caracteres com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="cdda7-182">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a><span data-ttu-id="cdda7-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cdda7-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="cdda7-184">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="cdda7-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
