---
title: aaaConnect tooAzure banco de dados PostgreSQL usando PHP | Microsoft Docs
description: "Este guia de início rápido fornece um exemplo de código PHP, você pode usar tooconnect e consultar dados do banco de dados PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: php
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: 008505e837e37cb8c7fea3fc164b3446c3580e46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a>Banco de dados do Azure para PostgreSQL: Use PHP tooconnect e consultar dados
Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para PostgreSQL usando um [PHP](http://php.net/manual/intro-whatis.php) aplicativo. Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação. Este artigo pressupõe que você esteja familiarizado com o desenvolvimento usando o PHP, mas que são novos tooworking com o banco de dados do Azure para PostgreSQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:
- [Criar Banco de dados - Portal](quickstart-create-server-database-portal.md)
- [Criar Banco de dados - CLI do Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a>Instalar o PHP
Instalar o PHP em seu próprio servidor ou crie um [aplicativo Web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) do Azure que inclua o PHP.

### <a name="windows"></a>Windows
- Baixar o [PHP 7.1.4 versão protegida não thread (x64)](http://windows.php.net/download#php-7.1)
- Instalar o PHP e consulte toohello [manual do PHP](http://php.net/manual/install.windows.php) para a configuração adicional
- código de saudação usa Olá **pgsql** classe (ext/php_pgsql.dll) que está incluído na instalação do PHP da saudação. 
- Olá habilitado **pgsql** extensão editando o arquivo de configuração do php.ini hello, geralmente localizado em `C:\Program Files\PHP\v7.1\php.ini`. arquivo de configuração de saudação deve conter uma linha com o texto de saudação `extension=php_pgsql.so`. Se não for exibido, adicionar texto de saudação e salve o arquivo hello. Se o texto de saudação estiver presente, mas comentado com um prefixo de ponto e vírgula, descomente o texto de saudação, removendo-e-vírgula de saudação.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Baixar o [PHP 7.1.4 versão protegida não thread (x64)](http://php.net/downloads.php) 
- Instalar o PHP e consulte toohello [manual do PHP](http://php.net/manual/install.unix.php) para a configuração adicional
- código de saudação usa Olá **pgsql** classe (php_pgsql.so). Instale-a executando `sudo apt-get install php-pgsql`.
- Olá habilitado **pgsql** extensão editando Olá `/etc/php/7.0/mods-available/pgsql.ini` arquivo de configuração. arquivo de configuração de saudação deve conter uma linha com o texto de saudação `extension=php_pgsql.so`. Se não for exibido, adicionar texto de saudação e salve o arquivo hello. Se o texto de saudação estiver presente, mas comentado com um prefixo de ponto e vírgula, descomente o texto de saudação, removendo-e-vírgula de saudação.

### <a name="macos"></a>MacOS
- Baixar o [PHP 7.1.4 versão](http://php.net/downloads.php)
- Instalar o PHP e consulte toohello [manual do PHP](http://php.net/manual/install.macosx.php) para a configuração adicional

## <a name="get-connection-information"></a>Obter informações de conexão
Obter Olá conexão informações necessárias tooconnect toohello banco de dados PostgreSQL. Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e pesquisa para o servidor de saudação que você criou, como **mypgserver 20170401**.
3. Clique em nome do servidor de saudação **mypgserver 20170401**.
4. Servidor de saudação selecione **visão geral** página. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
 ![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-php/1-connection-string.png)
5. Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.

## <a name="connect-and-create-a-table"></a>Conectar-se e criar uma tabela
A seguir use Olá tooconnect de código e criar uma tabela usando **CREATE TABLE** instrução SQL, seguida por **INSERT INTO** linhas de tooadd de instruções SQL em tabela hello.

Olá o método de chamada de código [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure banco de dados PostgreSQL. Em seguida, ele chama o método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun várias vezes vários comandos, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Olá detalhes se um erro de cada vez. Em seguida, ele chama o método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexão de saudação.

Substituir saudação `$host`, `$database`, `$user`, e `$password` parâmetros com seus próprios valores. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");
    print "Successfully created connection toodatabase.<br/>";

    // Drop previous table of same name if one exists.
    $query = "DROP TABLE IF EXISTS inventory;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished dropping table (if existed).<br/>";

    // Create table.
    $query = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished creating table.<br/>";

    // Insert some data into table.
    $name = '\'banana\'';
    $quantity = 150;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($1, $2);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'orange\'';
    $quantity = 154;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'apple\'';
    $quantity = 100;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error()). "<br/>";

    print "Inserted 3 rows of data.<br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="read-data"></a>Ler dados
A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL. 

 Olá o método de chamada de código [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure banco de dados PostgreSQL. Em seguida, ele chama o método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun Olá comando SELECT, mantendo a saudação de resultados em um conjunto de resultados, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Olá detalhes se ocorreu um erro.  conjunto de resultados tooread hello, método [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) é chamado em um loop, uma vez por linha e a linha hello os dados são recuperados de uma matriz `$row`, com valor de dados por coluna em cada posição de matriz.  conjunto de resultados toofree hello, método [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) é chamado. Em seguida, ele chama o método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexão de saudação.

Substituir saudação `$host`, `$database`, `$user`, e `$password` parâmetros com seus próprios valores. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Perform some SQL queries over hello connection.
    $query = "SELECT * from inventory";
    $result_set = pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    while ($row = pg_fetch_row($result_set))
    {
        print "Data row = ($row[0], $row[1], $row[2]). <br/>";
    }

    // Free result_set
    pg_free_result($result_set);

    // Closing connection
    pg_close($connection);
?>
```

## <a name="update-data"></a>Atualizar dados
A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL.

Olá o método de chamada de código [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure banco de dados PostgreSQL. Em seguida, ele chama o método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun um comando, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Olá detalhes se ocorreu um erro. Em seguida, ele chama o método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexão de saudação.

Substituir saudação `$host`, `$database`, `$user`, e `$password` parâmetros com seus próprios valores. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). ".<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Modify some data in table.
    $new_quantity = 200;
    $name = '\'banana\'';
    $query = "UPDATE inventory SET quantity = $new_quantity WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ".<br/>");
    print "Updated 1 row of data. </br>";

    // Closing connection
    pg_close($connection);
?>
```


## <a name="delete-data"></a>Excluir dados
A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL. 

 Olá o método de chamada de código [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect muito Azure banco de dados PostgreSQL. Em seguida, ele chama o método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun um comando, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Olá detalhes se ocorreu um erro. Em seguida, ele chama o método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexão de saudação.

Substituir saudação `$host`, `$database`, `$user`, e `$password` parâmetros com seus próprios valores. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed toocreate connection toodatabase: ". pg_last_error(). ". </br>");

    print "Successfully created connection toodatabase. <br/>";

    // Delete some data from table.
    $name = '\'orange\'';
    $query = "DELETE FROM inventory WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ". <br/>");
    print "Deleted 1 row of data. <br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./howto-migrate-using-export-and-import.md)
