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
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a>Banco de dados do Azure para PostgreSQL: Use Ruby tooconnect e consultar dados
Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para PostgreSQL usando um [Ruby](https://www.ruby-lang.org) aplicativo. Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação. Este artigo pressupõe que você esteja familiarizado com o desenvolvimento usando o Ruby, mas que são novos tooworking com o banco de dados do Azure para PostgreSQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:
- [Criar Banco de dados - Portal](quickstart-create-server-database-portal.md)
- [Criar Banco de dados - CLI do Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a>Instalar Ruby
Instale Ruby em seu próprio computador. 

### <a name="windows"></a>Windows
- Download e instalação Olá última versão do [Ruby](http://rubyinstaller.org/downloads/).
- Em Olá concluir a tela do instalador MSI de hello, marque caixa de saudação que diz "Run 'ridk instalar' tooinstall MSYS2 e ferramentas de desenvolvimento." Em seguida, clique em **concluir** instalador próximo do toolaunch hello.
- Olá RubyInstaller2 para o Windows installer é iniciado. Tipo de atualização do repositório de saudação MSYS2 tooinstall 2. Depois de terminar e retorna o prompt de instalação do toohello, feche a janela de comando de saudação.
- Inicie um novo prompt de comando (cmd) saudação do menu de início.
- Saudação de teste instalação Ruby `ruby -v` toosee versão de hello instalada.
- Testar a instalação do Gem Olá `gem -v` toosee versão de hello instalada.
- Criar módulo de PostgreSQL Olá para Ruby usando Gem ao executar o comando Olá `gem install pg`.

### <a name="macos"></a>MacOS
- Instalar Ruby usando Homebrew ao executar o comando Olá `brew install ruby`. Para obter mais opções de instalação, consulte Olá Ruby [documentação da instalação](https://www.ruby-lang.org/en/documentation/installation/#homebrew)
- Saudação de teste instalação Ruby `ruby -v` toosee versão de hello instalada.
- Testar a instalação do Gem Olá `gem -v` toosee versão de hello instalada.
- Criar módulo de PostgreSQL Olá para Ruby usando Gem ao executar o comando Olá `gem install pg`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Instalar Ruby, executando o comando Olá `sudo apt-get install ruby-full`. Para obter mais opções de instalação, consulte Olá Ruby [documentação de instalação](https://www.ruby-lang.org/en/documentation/installation/).
- Saudação de teste instalação Ruby `ruby -v` toosee versão de hello instalada.
- Instalar as atualizações mais recentes de saudação para Gem executando o comando Olá `sudo gem update --system`.
- Testar a instalação do Gem Olá `gem -v` toosee versão de hello instalada.
- Instalar gcc hello, verifique e outras ferramentas de compilação, executando o comando Olá `sudo apt-get install build-essential`.
- Instalar bibliotecas de PostgreSQL de saudação executando o comando Olá `sudo apt-get install libpq-dev`.
- Criar hello pg Ruby módulo usando Gem ao executar o comando Olá `sudo gem install pg`.

## <a name="run-ruby-code"></a>Executar código Ruby 
- Salve o código de saudação em um arquivo de texto e salve o arquivo de saudação em uma pasta de projeto com RB de extensão de arquivo, como `C:\rubypostgres\read.rb` ou`/home/username/rubypostgres/read.rb`
- código de saudação toorun, inicie o prompt de comando hello ou bash shell. Altere o diretório para a pasta de projeto `cd rubypostgres`, em seguida, digite o comando Olá `ruby read.rb` aplicativo hello de toorun.

## <a name="get-connection-information"></a>Obter informações de conexão
Obter Olá conexão informações necessárias tooconnect toohello banco de dados PostgreSQL. Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e pesquisa para o servidor de saudação que você criou, como **mypgserver 20170401**.
3. Clique em nome do servidor de saudação **mypgserver 20170401**.
4. Servidor de saudação selecione **visão geral** página. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
 ![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-ruby/1-connection-string.png)
5. Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** nome de logon do administrador de servidor do página tooview hello. Se necessário, Olá redefinição da senha.

## <a name="connect-and-create-a-table"></a>Conectar-se e criar uma tabela
A seguir use Olá tooconnect de código e criar uma tabela usando **CREATE TABLE** instrução SQL, seguida por **INSERT INTO** linhas de tooadd de instruções SQL em tabela hello.

Olá código usa um [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto com construtor [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure banco de dados PostgreSQL. Em seguida, ele chama o método [EXEC ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello, CREATE TABLE, comandos DROP e INSERT INTO. Olá código verifica erros usando Olá [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe. Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose conexão de saudação antes de encerrar.

Substituir saudação `host`, `database`, `user`, e `password` cadeias de caracteres com seus próprios valores. 
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

## <a name="read-data"></a>Ler dados
A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL. 

Olá código usa um [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto com construtor [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure banco de dados PostgreSQL. Em seguida, ele chama o método [EXEC ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Olá comando SELECT, mantendo a saudação de resultados em um conjunto de resultados. Olá coleção do conjunto de resultados é iterada usando Olá `resultSet.each do` loop, manter os valores de linha atual Olá Olá `row` variável. Olá código verifica erros usando Olá [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe. Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose conexão de saudação antes de encerrar.

Substituir saudação `host`, `database`, `user`, e `password` cadeias de caracteres com seus próprios valores. 

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

## <a name="update-data"></a>Atualizar dados
A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL.

Olá código usa um [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto com construtor [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure banco de dados PostgreSQL. Em seguida, ele chama o método [EXEC ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Olá comando UPDATE. Olá código verifica erros usando Olá [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe. Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose conexão de saudação antes de encerrar.

Substituir saudação `host`, `database`, `user`, e `password` cadeias de caracteres com seus próprios valores. 

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


## <a name="delete-data"></a>Excluir dados
A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL. 

Olá código usa um [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto com construtor [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure banco de dados PostgreSQL. Em seguida, ele chama o método [EXEC ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Olá comando UPDATE. Olá código verifica erros usando Olá [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe. Em seguida, ele chama o método [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose conexão de saudação antes de encerrar.

Substituir saudação `host`, `database`, `user`, e `password` cadeias de caracteres com seus próprios valores. 

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

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./howto-migrate-using-export-and-import.md)
