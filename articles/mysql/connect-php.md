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
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="e8e5a-103">Banco de dados do Azure para MySQL: Use PHP tooconnect e consultar dados</span><span class="sxs-lookup"><span data-stu-id="e8e5a-103">Azure Database for MySQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="e8e5a-104">Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para MySQL usando um [PHP](http://php.net/manual/intro-whatis.php) aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="e8e5a-105">Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="e8e5a-106">Este artigo pressupõe que você esteja familiarizado com o desenvolvimento usando o PHP, mas que são novos tooworking com o banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8e5a-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e8e5a-107">Prerequisites</span></span>
<span data-ttu-id="e8e5a-108">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="e8e5a-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="e8e5a-109">Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e8e5a-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="e8e5a-110">Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e8e5a-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="e8e5a-111">Instalar o PHP</span><span class="sxs-lookup"><span data-stu-id="e8e5a-111">Install PHP</span></span>
<span data-ttu-id="e8e5a-112">Instalar o PHP em seu próprio servidor ou crie um [aplicativo Web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) do Azure que inclua o PHP.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="e8e5a-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="e8e5a-113">MacOS</span></span>
- <span data-ttu-id="e8e5a-114">Baixar o [PHP 7.1.4 versão](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="e8e5a-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="e8e5a-115">Instalar o PHP e consulte toohello [manual do PHP](http://php.net/manual/install.macosx.php) para a configuração adicional</span><span class="sxs-lookup"><span data-stu-id="e8e5a-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="e8e5a-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="e8e5a-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="e8e5a-117">Baixar o [PHP 7.1.4 versão protegida não thread (x64)](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="e8e5a-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="e8e5a-118">Instalar o PHP e consulte toohello [manual do PHP](http://php.net/manual/install.unix.php) para a configuração adicional</span><span class="sxs-lookup"><span data-stu-id="e8e5a-118">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="e8e5a-119">Windows</span><span class="sxs-lookup"><span data-stu-id="e8e5a-119">Windows</span></span>
- <span data-ttu-id="e8e5a-120">Baixar o [PHP 7.1.4 versão protegida não thread (x64)](http://windows.php.net/download#php-7.1)</span><span class="sxs-lookup"><span data-stu-id="e8e5a-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="e8e5a-121">Instalar o PHP e consulte toohello [manual do PHP](http://php.net/manual/install.windows.php) para a configuração adicional</span><span class="sxs-lookup"><span data-stu-id="e8e5a-121">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="e8e5a-122">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="e8e5a-122">Get connection information</span></span>
<span data-ttu-id="e8e5a-123">Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-123">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="e8e5a-124">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-124">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="e8e5a-125">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e8e5a-125">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e8e5a-126">No painel esquerdo do hello, clique em **todos os recursos**e em seguida, procure o servidor Olá que você criou (por exemplo, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="e8e5a-126">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="e8e5a-127">Clique em nome do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-127">Click hello server name.</span></span>
4. <span data-ttu-id="e8e5a-128">Servidor de saudação selecione **propriedades** página.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-128">Select hello server's **Properties** page.</span></span> <span data-ttu-id="e8e5a-129">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-129">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="e8e5a-130">![Nome do servidor do Banco de Dados do Azure para MySQL](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="e8e5a-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="e8e5a-131">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-131">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="e8e5a-132">Conectar-se e criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="e8e5a-132">Connect and create a table</span></span>
<span data-ttu-id="e8e5a-133">A seguir use Olá tooconnect de código e criar uma tabela usando **CREATE TABLE** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-133">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="e8e5a-134">código de saudação usa Olá **extensão MySQL aprimorado** classe (mysqli) incluído em PHP.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-134">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="e8e5a-135">Olá métodos de chamada do código [mysqli_init](http://php.net/manual/mysqli.init.php) e [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-135">hello code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span></span> <span data-ttu-id="e8e5a-136">Em seguida, ele chama o método [mysqli_query](http://php.net/manual/mysqli.query.php) toorun consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello query.</span></span> <span data-ttu-id="e8e5a-137">Em seguida, ele chama o método [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello connection.</span></span>

<span data-ttu-id="e8e5a-138">Substitua parâmetros de host, nome de usuário, senha e db_name Olá com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-138">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="insert-data"></a><span data-ttu-id="e8e5a-139">Inserir dados</span><span class="sxs-lookup"><span data-stu-id="e8e5a-139">Insert data</span></span>
<span data-ttu-id="e8e5a-140">A seguir use Olá código tooconnect e inserir dados usando um **inserir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-140">Use hello following code tooconnect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="e8e5a-141">código de saudação usa Olá **extensão MySQL aprimorado** classe (mysqli) incluído em PHP.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-141">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="e8e5a-142">código de saudação usa o método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate um preparada Inserir instrução, em seguida, associa Olá parâmetros para cada valor de coluna inserida usando o método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="e8e5a-142">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared insert statement, then binds hello parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="e8e5a-143">código de saudação executa a instrução de saudação usando o método [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e depois fecha Olá instrução usando o método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="e8e5a-143">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="e8e5a-144">Substitua parâmetros de host, nome de usuário, senha e db_name Olá com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-144">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="e8e5a-145">Ler dados</span><span class="sxs-lookup"><span data-stu-id="e8e5a-145">Read data</span></span>
<span data-ttu-id="e8e5a-146">A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-146">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="e8e5a-147">código de saudação usa Olá **extensão MySQL aprimorado** classe (mysqli) incluído em PHP.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-147">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="e8e5a-148">código de saudação usa o método [mysqli_query](http://php.net/manual/mysqli.query.php) executar consulta sql de saudação e usa [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) toofetch método hello linhas resultantes.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-148">hello code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform hello sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method toofetch hello resulting rows.</span></span>

<span data-ttu-id="e8e5a-149">Substitua parâmetros de host, nome de usuário, senha e db_name Olá com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-149">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="e8e5a-150">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="e8e5a-150">Update data</span></span>
<span data-ttu-id="e8e5a-151">A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-151">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="e8e5a-152">código de saudação usa Olá **extensão MySQL aprimorado** classe (mysqli) incluído em PHP.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-152">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="e8e5a-153">código de saudação usa o método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate uma instrução update preparada, em seguida, associa parâmetros Olá para cada valor de coluna atualizada usando o método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="e8e5a-153">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared update statement, then binds hello parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="e8e5a-154">código de saudação executa a instrução de saudação usando o método [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e depois fecha Olá instrução usando o método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="e8e5a-154">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="e8e5a-155">Substitua parâmetros de host, nome de usuário, senha e db_name Olá com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-155">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="e8e5a-156">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="e8e5a-156">Delete data</span></span>
<span data-ttu-id="e8e5a-157">A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-157">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="e8e5a-158">código de saudação usa Olá **extensão MySQL aprimorado** classe (mysqli) incluído em PHP.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-158">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="e8e5a-159">código de saudação usa o método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate um preparada exclusão da instrução, em seguida, associa Olá parâmetros para Olá onde cláusula na instrução hello usando o método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="e8e5a-159">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared delete statement, then binds hello parameters for hello where clause in hello statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="e8e5a-160">código de saudação executa a instrução de saudação usando o método [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e depois fecha Olá instrução usando o método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="e8e5a-160">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="e8e5a-161">Substitua parâmetros de host, nome de usuário, senha e db_name Olá com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e8e5a-161">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="e8e5a-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8e5a-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e8e5a-163">Compilar um aplicativo Web PHP e MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="e8e5a-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
