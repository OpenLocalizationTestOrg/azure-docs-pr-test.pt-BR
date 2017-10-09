---
title: Conectar-se tooAzure banco de dados para PostgreSQL do Python | Microsoft Docs
description: "Este guia de início rápido fornece um exemplo de código do Python que você pode usar tooconnect e consultar dados do banco de dados PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 08/15/2017
ms.openlocfilehash: 7d6d9f5424fb39ad8837999d4788b4363c818887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="10c6c-103">Banco de dados do Azure para PostgreSQL: uso Python tooconnect e consultar dados</span><span class="sxs-lookup"><span data-stu-id="10c6c-103">Azure Database for PostgreSQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="10c6c-104">Este guia de início rápido demonstra como toouse [Python](https://python.org) tooconnect tooan banco de dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="10c6c-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for PostgreSQL.</span></span> <span data-ttu-id="10c6c-105">Ele também demonstra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação do macOS, Ubuntu Linux e plataformas do Windows.</span><span class="sxs-lookup"><span data-stu-id="10c6c-105">It also demonstrates how toouse SQL statements tooquery, insert, update, and delete data in hello database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="10c6c-106">etapas de Olá neste artigo presumem que você esteja familiarizado com o desenvolvimento usando Python e é tooworking novo com o banco de dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="10c6c-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10c6c-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="10c6c-107">Prerequisites</span></span>
<span data-ttu-id="10c6c-108">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="10c6c-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="10c6c-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="10c6c-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="10c6c-110">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="10c6c-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="10c6c-111">Você também precisará de:</span><span class="sxs-lookup"><span data-stu-id="10c6c-111">You also need:</span></span>
- <span data-ttu-id="10c6c-112">[Python](https://www.python.org/downloads/) instalado</span><span class="sxs-lookup"><span data-stu-id="10c6c-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="10c6c-113">Pacote [pip](https://pip.pypa.io/en/stable/installing/) instalado (o pip já está instalado se você está trabalhando com binários Python 2 > = 2.7.9 ou Python 3 > = 3,4 baixados de [python.org](https://python.org).</span><span class="sxs-lookup"><span data-stu-id="10c6c-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-hello-python-connection-libraries-for-postgresql"></a><span data-ttu-id="10c6c-114">Instalar bibliotecas de conexão de Python Olá para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="10c6c-114">Install hello Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="10c6c-115">Instalar Olá [psycopg2](http://initd.org/psycopg/docs/install.html) pacote, que permite que você tooconnect e consulta de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="10c6c-115">Install hello [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you tooconnect and query hello database.</span></span> <span data-ttu-id="10c6c-116">é psycopg2 [disponível em PyPI](https://pypi.python.org/pypi/psycopg2/) na forma de saudação de [roda](http://pythonwheels.com/) pacotes para plataformas mais comuns de saudação (Linux e OSX, Windows).</span><span class="sxs-lookup"><span data-stu-id="10c6c-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in hello form of [wheel](http://pythonwheels.com/) packages for hello most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="10c6c-117">Use pip instalar versão binária do tooget saudação do módulo de hello, incluindo todas as dependências de saudação.</span><span class="sxs-lookup"><span data-stu-id="10c6c-117">Use pip install tooget hello binary version of hello module including all hello dependencies.</span></span>

1. <span data-ttu-id="10c6c-118">Em seu próprio computador, inicie uma interface de linha de comando:</span><span class="sxs-lookup"><span data-stu-id="10c6c-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="10c6c-119">No Linux, inicie o shell Bash hello.</span><span class="sxs-lookup"><span data-stu-id="10c6c-119">On Linux, launch hello Bash shell.</span></span>
    - <span data-ttu-id="10c6c-120">Em macOS, inicie Olá Terminal.</span><span class="sxs-lookup"><span data-stu-id="10c6c-120">On macOS, launch hello Terminal.</span></span>
    - <span data-ttu-id="10c6c-121">No Windows, inicie a saudação de Prompt de comando do Menu Iniciar do hello.</span><span class="sxs-lookup"><span data-stu-id="10c6c-121">On Windows, launch hello Command Prompt from hello Start Menu.</span></span>
2. <span data-ttu-id="10c6c-122">Certifique-se de que estão usando a versão mais atual Olá de pip executando um comando como:</span><span class="sxs-lookup"><span data-stu-id="10c6c-122">Ensure that you are using hello most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="10c6c-123">Execute Olá pacote do comando tooinstall Olá psycopg2 a seguir:</span><span class="sxs-lookup"><span data-stu-id="10c6c-123">Run hello following command tooinstall hello psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="10c6c-124">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="10c6c-124">Get connection information</span></span>
<span data-ttu-id="10c6c-125">Obter Olá conexão informações necessárias tooconnect toohello banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="10c6c-125">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="10c6c-126">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="10c6c-126">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="10c6c-127">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="10c6c-127">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="10c6c-128">No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e procure **mypgserver 20170401** (servidor de saudação você acabou de criar).</span><span class="sxs-lookup"><span data-stu-id="10c6c-128">From hello left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (hello server you just created).</span></span>
3. <span data-ttu-id="10c6c-129">Clique em nome do servidor de saudação **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="10c6c-129">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="10c6c-130">Servidor de saudação selecione **visão geral** página e anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="10c6c-130">Select hello server's **Overview** page, and then make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="10c6c-131">![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="10c6c-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="10c6c-132">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="10c6c-132">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="how-toorun-python-code"></a><span data-ttu-id="10c6c-133">Como toorun código Python</span><span class="sxs-lookup"><span data-stu-id="10c6c-133">How toorun Python code</span></span>
<span data-ttu-id="10c6c-134">Este tópico contém um total de quatro exemplos de código, cada uma executando uma função específica.</span><span class="sxs-lookup"><span data-stu-id="10c6c-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="10c6c-135">Olá instruções a seguir indicam como toocreate um arquivo de texto, inserir um bloco de código e, em seguida, salve o arquivo de saudação para que possa ser executado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="10c6c-135">hello following instructions indicate how toocreate a text file, insert a code block, and then save hello file so that you can run it later.</span></span> <span data-ttu-id="10c6c-136">Ser se toocreate quatro arquivos separados, um para cada bloco de código.</span><span class="sxs-lookup"><span data-stu-id="10c6c-136">Be sure toocreate four separate files, one for each code block.</span></span>

- <span data-ttu-id="10c6c-137">Crie um novo arquivo usando seu editor de texto favorito.</span><span class="sxs-lookup"><span data-stu-id="10c6c-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="10c6c-138">Copie e cole um dos exemplos de código Olá Olá seções a seguir no arquivo de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="10c6c-138">Copy and paste one of hello code samples in hello following sections into hello text file.</span></span> <span data-ttu-id="10c6c-139">Substituir saudação **host**, **dbname**, **usuário**, e **senha** parâmetros com valores hello que você especificou quando criou Olá servidor e banco de dados.</span><span class="sxs-lookup"><span data-stu-id="10c6c-139">Replace hello **host**, **dbname**, **user**, and **password** parameters with hello values that you specified when you created hello server and database.</span></span>
- <span data-ttu-id="10c6c-140">Salve o arquivo de saudação com extensão de py hello (por exemplo, postgres.py) em sua pasta de projeto.</span><span class="sxs-lookup"><span data-stu-id="10c6c-140">Save hello file with hello .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="10c6c-141">Se você estiver executando Olá sistema operacional Windows, ser se tooselect codificação UTF-8 ao salvar arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="10c6c-141">If you are running hello Windows OS, be sure tooselect UTF-8 encoding when saving hello file.</span></span> 
- <span data-ttu-id="10c6c-142">Inicie o shell do Prompt de comando ou Bash hello e altere a pasta de projeto tooyour do diretório hello, por exemplo `cd postgres`.</span><span class="sxs-lookup"><span data-stu-id="10c6c-142">Launch hello Command Prompt or Bash shell and then change hello directory tooyour project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="10c6c-143">código toorun Olá Olá tipo comando Python seguido pelo nome de arquivo hello, por exemplo `Python postgres.py`.</span><span class="sxs-lookup"><span data-stu-id="10c6c-143">toorun hello code, type hello Python command followed by hello file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="10c6c-144">A partir do Python versão 3, você pode ver o erro de saudação `SyntaxError: Missing parentheses in call too'print'` ao executar Olá blocos de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="10c6c-144">Starting in Python version 3, you may see hello error `SyntaxError: Missing parentheses in call too'print'` when running hello following code blocks.</span></span> <span data-ttu-id="10c6c-145">Se isso acontecer, substitua cada comando de toohello chamada `print "string"` com uma chamada de função usando parênteses, como `print("string")`.</span><span class="sxs-lookup"><span data-stu-id="10c6c-145">If that happens, replace each call toohello command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="10c6c-146">Conectar-se, criar tabela e inserir dados</span><span class="sxs-lookup"><span data-stu-id="10c6c-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="10c6c-147">A seguir use Olá tooconnect de código e carregar Olá dados usando [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) funcionar com **inserir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="10c6c-147">Use hello following code tooconnect and load hello data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="10c6c-148">Olá [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) função é a consulta SQL Olá tooexecute usado no banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="10c6c-148">hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> <span data-ttu-id="10c6c-149">Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.</span><span class="sxs-lookup"><span data-stu-id="10c6c-149">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Drop previous table of same name if one exists
cursor.execute("DROP TABLE IF EXISTS inventory;")
print "Finished dropping table (if existed)"

# Create table
cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
print "Finished creating table"

# Insert some data into table
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
print "Inserted 3 rows of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

<span data-ttu-id="10c6c-150">Depois de saudação código é executado com êxito, saída de hello aparece da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="10c6c-150">After hello code runs successfully, hello output appears as follows:</span></span>

![Saída da linha de comando](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="10c6c-152">Ler dados</span><span class="sxs-lookup"><span data-stu-id="10c6c-152">Read data</span></span>
<span data-ttu-id="10c6c-153">Dados de saudação tooread inseridos usando de código a seguir de saudação de uso [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funcionar com **selecione** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="10c6c-153">Use hello following code tooread hello data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="10c6c-154">Essa função aceita uma consulta e retorna um conjunto de resultados que pode ser iteradas com o uso de saudação do [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span><span class="sxs-lookup"><span data-stu-id="10c6c-154">This function accepts a query and returns a result set that can be iterated over with hello use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="10c6c-155">Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.</span><span class="sxs-lookup"><span data-stu-id="10c6c-155">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Fetch all rows from table
cursor.execute("SELECT * FROM inventory;")
rows = cursor.fetchall()

# Print all rows
for row in rows:
    print "Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2]))

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="update-data"></a><span data-ttu-id="10c6c-156">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="10c6c-156">Update data</span></span>
<span data-ttu-id="10c6c-157">Linha de inventário de saudação tooupdate inserido anteriormente usando de código a seguir de saudação de uso [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funcionar com **atualização** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="10c6c-157">Use hello following code tooupdate hello inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="10c6c-158">Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.</span><span class="sxs-lookup"><span data-stu-id="10c6c-158">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Update a data row in hello table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a><span data-ttu-id="10c6c-159">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="10c6c-159">Delete data</span></span>
<span data-ttu-id="10c6c-160">Toodelete um item de estoque que você inseriu anteriormente usando o código a seguir de Olá de uso [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funcionar com **excluir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="10c6c-160">Use hello following code toodelete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="10c6c-161">Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.</span><span class="sxs-lookup"><span data-stu-id="10c6c-161">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Delete data row from table
cursor.execute("DELETE FROM inventory WHERE name = %s;", ("orange",))
print "Deleted 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="10c6c-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="10c6c-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="10c6c-163">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="10c6c-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
