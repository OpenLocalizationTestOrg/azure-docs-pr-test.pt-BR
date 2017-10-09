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
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a>Banco de dados do Azure para MySQL: Use Ruby tooconnect e consultar dados
Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para MySQL usando um [Ruby](https://www.ruby-lang.org) aplicativo e hello [mysql2](https://rubygems.org/gems/mysql2) gem de plataformas Mac, Ubuntu Linux e Windows. Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação. Este artigo pressupõe que você esteja familiarizado com o desenvolvimento usando o Ruby, mas que são novos tooworking com o banco de dados do Azure para MySQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:
- [Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a>Instalar Ruby
Instale Ruby, Gem e biblioteca de MySQL2 Olá em sua própria máquina. 

### <a name="windows"></a>Windows
1. Baixar e instalar a versão de hello 2.3 do [Ruby](http://rubyinstaller.org/downloads/).
2. Inicie um novo prompt de comando (cmd) saudação do menu de início.
3. Altere o diretório em Olá diretório Ruby para versão 2.3. `cd c:\Ruby23-x64\bin`
4. Saudação de teste Ruby instalação executando o comando Olá `ruby -v` toosee versão de hello instalada.
5. Testar a instalação de Gem Olá executando o comando Olá `gem -v` toosee versão de hello instalada.
6. Criar módulo Olá Mysql2 para Ruby usando Gem ao executar o comando Olá `gem install mysql2`.

### <a name="macos"></a>MacOS
1. Instalar Ruby usando Homebrew ao executar o comando Olá `brew install ruby`. Para obter mais opções de instalação, consulte Olá Ruby [documentação de instalação](https://www.ruby-lang.org/en/documentation/installation/#homebrew).
2. Saudação de teste Ruby instalação executando o comando Olá `ruby -v` toosee versão de hello instalada.
3. Testar a instalação de Gem Olá executando o comando Olá `gem -v` toosee versão de hello instalada.
4. Criar módulo Olá Mysql2 para Ruby usando Gem ao executar o comando Olá `gem install mysql2`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Instalar Ruby, executando o comando Olá `sudo apt-get install ruby-full`. Para obter mais opções de instalação, consulte Olá Ruby [documentação de instalação](https://www.ruby-lang.org/en/documentation/installation/).
2. Saudação de teste Ruby instalação executando o comando Olá `ruby -v` toosee versão de hello instalada.
3. Instalar as atualizações mais recentes de saudação para Gem executando o comando Olá `sudo gem update --system`.
4. Testar a instalação de Gem Olá executando o comando Olá `gem -v` toosee versão de hello instalada.
5. Instalar gcc hello, verifique e outras ferramentas de compilação, executando o comando Olá `sudo apt-get install build-essential`.
6. Instalar bibliotecas para desenvolvedores Olá MySQL cliente executando o comando Olá `sudo apt-get install libmysqlclient-dev`.
7. Criar o módulo de mysql2 de saudação para Ruby usando Gem ao executar o comando Olá `sudo gem install mysql2`.

## <a name="get-connection-information"></a>Obter informações de conexão
Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL. Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e procure o servidor de saudação você ter creased, como **myserver4demo**.
3. Clique em nome do servidor de saudação **myserver4demo**.
4. Servidor de saudação selecione **propriedades** página. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
 ![Banco de Dados do Azure para MySQL – Logon de administrador do servidor](./media/connect-ruby/1_server-properties-name-login.png)
5. Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.

## <a name="run-ruby-code"></a>Executar código Ruby 
1. Colar Olá código Ruby das seções Olá abaixo em arquivos de texto e salvar arquivos de saudação em uma pasta de projeto com RB de extensão de arquivo, como `C:\rubymysql\createtable.rb` ou `/home/username/rubymysql/createtable.rb`.
2. código de saudação toorun, inicie o prompt de comando hello ou bash shell. Altere o diretório para a pasta do seu projeto `cd rubymysql`
3. Digite comando Olá ruby seguido pelo nome de arquivo hello, tais como `ruby createtable.rb` toorun aplicativo de hello.
4. Em Olá sistema operacional Windows, se o aplicativo hello ruby não está em sua variável de ambiente path, talvez seja necessário aplicativo toouse Olá caminho completo toolaunch hello nó, como`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`

## <a name="connect-and-create-a-table"></a>Conectar-se e criar uma tabela
A seguir use Olá tooconnect de código e criar uma tabela usando **CREATE TABLE** instrução SQL, seguida por **INSERT INTO** linhas de tooadd de instruções SQL em tabela hello.

Olá código usa um [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() método tooconnect tooAzure banco de dados de classe para MySQL. Em seguida, ele chama o método [Query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) várias vezes toorun hello, CREATE TABLE, comandos DROP e INSERT INTO. Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose conexão de saudação antes de encerrar.

Substituir saudação `host`, `database`, `username`, e `password` cadeias de caracteres com seus próprios valores. 
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

## <a name="read-data"></a>Ler dados
A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL. 

Olá código usa um [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() método tooconnect tooAzure banco de dados de classe para MySQL. Em seguida, ele chama o método [Query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) comandos SELECT de saudação toorun. Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose conexão de saudação antes de encerrar.

Substituir saudação `host`, `database`, `username`, e `password` cadeias de caracteres com seus próprios valores. 

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

## <a name="update-data"></a>Atualizar dados
A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL.

Olá código usa um [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() método tooconnect tooAzure banco de dados de classe para MySQL. Em seguida, ele chama o método [Query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun comandos de atualização de saudação. Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose conexão de saudação antes de encerrar.

Substituir saudação `host`, `database`, `username`, e `password` cadeias de caracteres com seus próprios valores. 

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


## <a name="delete-data"></a>Excluir dados
A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL. 

Olá código usa um [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() método tooconnect tooAzure banco de dados de classe para MySQL. Em seguida, ele chama o método [Query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun comandos de exclusão de saudação. Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose conexão de saudação antes de encerrar.

Substituir saudação `host`, `database`, `username`, e `password` cadeias de caracteres com seus próprios valores. 

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

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./concepts-migrate-import-export.md)
