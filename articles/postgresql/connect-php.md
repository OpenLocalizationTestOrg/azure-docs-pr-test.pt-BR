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
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="3f760-103">Banco de dados do Azure para PostgreSQL: Use PHP tooconnect e consultar dados</span><span class="sxs-lookup"><span data-stu-id="3f760-103">Azure Database for PostgreSQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="3f760-104">Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para PostgreSQL usando um [PHP](http://php.net/manual/intro-whatis.php) aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3f760-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="3f760-105">Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f760-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="3f760-106">Este artigo pressupõe que você esteja familiarizado com o desenvolvimento usando o PHP, mas que são novos tooworking com o banco de dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3f760-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f760-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3f760-107">Prerequisites</span></span>
<span data-ttu-id="3f760-108">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="3f760-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="3f760-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="3f760-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="3f760-110">Criar Banco de dados - CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3f760-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="3f760-111">Instalar o PHP</span><span class="sxs-lookup"><span data-stu-id="3f760-111">Install PHP</span></span>
<span data-ttu-id="3f760-112">Instalar o PHP em seu próprio servidor ou crie um [aplicativo Web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) do Azure que inclua o PHP.</span><span class="sxs-lookup"><span data-stu-id="3f760-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="3f760-113">Windows</span><span class="sxs-lookup"><span data-stu-id="3f760-113">Windows</span></span>
- <span data-ttu-id="3f760-114">Baixar o [PHP 7.1.4 versão protegida não thread (x64)](http://windows.php.net/download#php-7.1)</span><span class="sxs-lookup"><span data-stu-id="3f760-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="3f760-115">Instalar o PHP e consulte toohello [manual do PHP](http://php.net/manual/install.windows.php) para a configuração adicional</span><span class="sxs-lookup"><span data-stu-id="3f760-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="3f760-116">código de saudação usa Olá **pgsql** classe (ext/php_pgsql.dll) que está incluído na instalação do PHP da saudação.</span><span class="sxs-lookup"><span data-stu-id="3f760-116">hello code uses hello **pgsql** class (ext/php_pgsql.dll)  that is included in hello PHP installation.</span></span> 
- <span data-ttu-id="3f760-117">Olá habilitado **pgsql** extensão editando o arquivo de configuração do php.ini hello, geralmente localizado em `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="3f760-117">Enabled hello **pgsql** extension by editing hello php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="3f760-118">arquivo de configuração de saudação deve conter uma linha com o texto de saudação `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="3f760-118">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="3f760-119">Se não for exibido, adicionar texto de saudação e salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="3f760-119">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="3f760-120">Se o texto de saudação estiver presente, mas comentado com um prefixo de ponto e vírgula, descomente o texto de saudação, removendo-e-vírgula de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f760-120">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="3f760-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="3f760-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="3f760-122">Baixar o [PHP 7.1.4 versão protegida não thread (x64)](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="3f760-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="3f760-123">Instalar o PHP e consulte toohello [manual do PHP](http://php.net/manual/install.unix.php) para a configuração adicional</span><span class="sxs-lookup"><span data-stu-id="3f760-123">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="3f760-124">código de saudação usa Olá **pgsql** classe (php_pgsql.so).</span><span class="sxs-lookup"><span data-stu-id="3f760-124">hello code uses hello **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="3f760-125">Instale-a executando `sudo apt-get install php-pgsql`.</span><span class="sxs-lookup"><span data-stu-id="3f760-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="3f760-126">Olá habilitado **pgsql** extensão editando Olá `/etc/php/7.0/mods-available/pgsql.ini` arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="3f760-126">Enabled hello **pgsql** extension by editing hello `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="3f760-127">arquivo de configuração de saudação deve conter uma linha com o texto de saudação `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="3f760-127">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="3f760-128">Se não for exibido, adicionar texto de saudação e salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="3f760-128">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="3f760-129">Se o texto de saudação estiver presente, mas comentado com um prefixo de ponto e vírgula, descomente o texto de saudação, removendo-e-vírgula de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f760-129">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="3f760-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="3f760-130">MacOS</span></span>
- <span data-ttu-id="3f760-131">Baixar o [PHP 7.1.4 versão](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="3f760-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="3f760-132">Instalar o PHP e consulte toohello [manual do PHP](http://php.net/manual/install.macosx.php) para a configuração adicional</span><span class="sxs-lookup"><span data-stu-id="3f760-132">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="3f760-133">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="3f760-133">Get connection information</span></span>
<span data-ttu-id="3f760-134">Obter Olá conexão informações necessárias tooconnect toohello banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3f760-134">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="3f760-135">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="3f760-135">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="3f760-136">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3f760-136">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3f760-137">No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e pesquisa para o servidor de saudação que você criou, como **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="3f760-137">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="3f760-138">Clique em nome do servidor de saudação **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="3f760-138">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="3f760-139">Servidor de saudação selecione **visão geral** página.</span><span class="sxs-lookup"><span data-stu-id="3f760-139">Select hello server's **Overview** page.</span></span> <span data-ttu-id="3f760-140">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="3f760-140">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="3f760-141">![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="3f760-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="3f760-142">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="3f760-142">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="3f760-143">Conectar-se e criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="3f760-143">Connect and create a table</span></span>
<span data-ttu-id="3f760-144">A seguir use Olá tooconnect de código e criar uma tabela usando **CREATE TABLE** instrução SQL, seguida por **INSERT INTO** linhas de tooadd de instruções SQL em tabela hello.</span><span class="sxs-lookup"><span data-stu-id="3f760-144">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="3f760-145">Olá o método de chamada de código [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3f760-145">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="3f760-146">Em seguida, ele chama o método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun várias vezes vários comandos, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Olá detalhes se um erro de cada vez.</span><span class="sxs-lookup"><span data-stu-id="3f760-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times toorun several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred each time.</span></span> <span data-ttu-id="3f760-147">Em seguida, ele chama o método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f760-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="3f760-148">Substituir saudação `$host`, `$database`, `$user`, e `$password` parâmetros com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="3f760-148">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="3f760-149">Ler dados</span><span class="sxs-lookup"><span data-stu-id="3f760-149">Read data</span></span>
<span data-ttu-id="3f760-150">A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="3f760-150">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="3f760-151">Olá o método de chamada de código [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3f760-151">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="3f760-152">Em seguida, ele chama o método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun Olá comando SELECT, mantendo a saudação de resultados em um conjunto de resultados, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Olá detalhes se ocorreu um erro.</span><span class="sxs-lookup"><span data-stu-id="3f760-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello SELECT command, keeping hello results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span>  <span data-ttu-id="3f760-153">conjunto de resultados tooread hello, método [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) é chamado em um loop, uma vez por linha e a linha hello os dados são recuperados de uma matriz `$row`, com valor de dados por coluna em cada posição de matriz.</span><span class="sxs-lookup"><span data-stu-id="3f760-153">tooread hello result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and hello row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="3f760-154">conjunto de resultados toofree hello, método [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) é chamado.</span><span class="sxs-lookup"><span data-stu-id="3f760-154">toofree hello result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="3f760-155">Em seguida, ele chama o método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f760-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="3f760-156">Substituir saudação `$host`, `$database`, `$user`, e `$password` parâmetros com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="3f760-156">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="3f760-157">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="3f760-157">Update data</span></span>
<span data-ttu-id="3f760-158">A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="3f760-158">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="3f760-159">Olá o método de chamada de código [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3f760-159">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="3f760-160">Em seguida, ele chama o método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun um comando, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Olá detalhes se ocorreu um erro.</span><span class="sxs-lookup"><span data-stu-id="3f760-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="3f760-161">Em seguida, ele chama o método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f760-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="3f760-162">Substituir saudação `$host`, `$database`, `$user`, e `$password` parâmetros com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="3f760-162">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="3f760-163">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="3f760-163">Delete data</span></span>
<span data-ttu-id="3f760-164">A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="3f760-164">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="3f760-165">Olá o método de chamada de código [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect muito Azure banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3f760-165">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect too Azure Database for PostgreSQL.</span></span> <span data-ttu-id="3f760-166">Em seguida, ele chama o método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun um comando, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Olá detalhes se ocorreu um erro.</span><span class="sxs-lookup"><span data-stu-id="3f760-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="3f760-167">Em seguida, ele chama o método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f760-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="3f760-168">Substituir saudação `$host`, `$database`, `$user`, e `$password` parâmetros com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="3f760-168">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="3f760-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f760-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3f760-170">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="3f760-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
