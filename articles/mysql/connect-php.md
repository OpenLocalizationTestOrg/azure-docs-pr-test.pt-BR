---
title: "TooAzure banco de dados de conexão para MySQL do PHP | Microsoft Docs"
description: "Este guia de início rápido fornece vários exemplos de código PHP use tooconnect e consultar dados do banco de dados MySQL."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: b928748c473c1aef320ae2183f237b5b845e83f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a>Banco de dados do Azure para MySQL: Use PHP tooconnect e consultar dados
Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para MySQL usando um [PHP](http://php.net/manual/intro-whatis.php) aplicativo. Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação. Este artigo pressupõe que você esteja familiarizado com o desenvolvimento usando o PHP, mas que são novos tooworking com o banco de dados do Azure para MySQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:
- [Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a>Instalar o PHP
Instalar o PHP em seu próprio servidor ou crie um [aplicativo Web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) do Azure que inclua o PHP.

### <a name="macos"></a>MacOS
- Baixar o [PHP 7.1.4 versão](http://php.net/downloads.php)
- Instalar o PHP e consulte toohello [manual do PHP](http://php.net/manual/install.macosx.php) para a configuração adicional

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Baixar o [PHP 7.1.4 versão protegida não thread (x64)](http://php.net/downloads.php)
- Instalar o PHP e consulte toohello [manual do PHP](http://php.net/manual/install.unix.php) para a configuração adicional

### <a name="windows"></a>Windows
- Baixar o [PHP 7.1.4 versão protegida não thread (x64)](http://windows.php.net/download#php-7.1)
- Instalar o PHP e consulte toohello [manual do PHP](http://php.net/manual/install.windows.php) para a configuração adicional

## <a name="get-connection-information"></a>Obter informações de conexão
Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL. Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. No painel esquerdo do hello, clique em **todos os recursos**e em seguida, procure o servidor Olá que você criou (por exemplo, **myserver4demo**).
3. Clique em nome do servidor de saudação.
4. Servidor de saudação selecione **propriedades** página. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
 ![Nome do servidor do Banco de Dados do Azure para MySQL](./media/connect-php/1_server-properties-name-login.png)
5. Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.

## <a name="connect-and-create-a-table"></a>Conectar-se e criar uma tabela
A seguir use Olá tooconnect de código e criar uma tabela usando **CREATE TABLE** instrução SQL. 

código de saudação usa Olá **extensão MySQL aprimorado** classe (mysqli) incluído em PHP. Olá métodos de chamada do código [mysqli_init](http://php.net/manual/mysqli.init.php) e [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL. Em seguida, ele chama o método [mysqli_query](http://php.net/manual/mysqli.query.php) toorun consulta de saudação. Em seguida, ele chama o método [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose conexão de saudação.

Substitua parâmetros de host, nome de usuário, senha e db_name Olá com seus próprios valores. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

// Run hello create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a>Inserir dados
A seguir use Olá código tooconnect e inserir dados usando um **inserir** instrução SQL.

código de saudação usa Olá **extensão MySQL aprimorado** classe (mysqli) incluído em PHP. código de saudação usa o método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate um preparada Inserir instrução, em seguida, associa Olá parâmetros para cada valor de coluna inserida usando o método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). código de saudação executa a instrução de saudação usando o método [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e depois fecha Olá instrução usando o método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Substitua parâmetros de host, nome de usuário, senha e db_name Olá com seus próprios valores. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close hello connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a>Ler dados
A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL.  código de saudação usa Olá **extensão MySQL aprimorado** classe (mysqli) incluído em PHP. código de saudação usa o método [mysqli_query](http://php.net/manual/mysqli.query.php) executar consulta sql de saudação e usa [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) toofetch método hello linhas resultantes.

Substitua parâmetros de host, nome de usuário, senha e db_name Olá com seus próprios valores. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a>Atualizar dados
A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL.

código de saudação usa Olá **extensão MySQL aprimorado** classe (mysqli) incluído em PHP. código de saudação usa o método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate uma instrução update preparada, em seguida, associa parâmetros Olá para cada valor de coluna atualizada usando o método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). código de saudação executa a instrução de saudação usando o método [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e depois fecha Olá instrução usando o método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Substitua parâmetros de host, nome de usuário, senha e db_name Olá com seus próprios valores. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close hello connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a>Excluir dados
A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL. 

código de saudação usa Olá **extensão MySQL aprimorado** classe (mysqli) incluído em PHP. código de saudação usa o método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate um preparada exclusão da instrução, em seguida, associa Olá parâmetros para Olá onde cláusula na instrução hello usando o método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). código de saudação executa a instrução de saudação usando o método [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e depois fecha Olá instrução usando o método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Substitua parâmetros de host, nome de usuário, senha e db_name Olá com seus próprios valores. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Compilar um aplicativo Web PHP e MySQL no Azure](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
