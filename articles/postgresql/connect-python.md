---
title: Conectar-se ao Banco de Dados do Azure para PostgreSQL do Python | Microsoft Docs
description: "Este guia de início rápido fornece um exemplo de código Python que você pode usar para se conectar e consultar dados do Banco de Dados do Azure para PostgreSQL."
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
ms.openlocfilehash: d682d94143fb9fd5e2c2a578c3cb0dcfa101462c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-python-to-connect-and-query-data"></a><span data-ttu-id="f9096-103">Banco de dados do Azure para PostgreSQL: usar Python para se conectar e consultar dados</span><span class="sxs-lookup"><span data-stu-id="f9096-103">Azure Database for PostgreSQL: Use Python to connect and query data</span></span>
<span data-ttu-id="f9096-104">Este guia de início rápido demonstra como usar [Python](https://python.org) para se conectar a um Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f9096-104">This quickstart demonstrates how to use [Python](https://python.org) to connect to an Azure Database for PostgreSQL.</span></span> <span data-ttu-id="f9096-105">Ele também demonstra como usar instruções SQL para consultar, inserir, atualizar e excluir dados no banco de dados das plataformas macOS, Windows, Ubuntu e Linux.</span><span class="sxs-lookup"><span data-stu-id="f9096-105">It also demonstrates how to use SQL statements to query, insert, update, and delete data in the database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="f9096-106">As etapas neste artigo pressupõem que você está familiarizado com o desenvolvimento usando Python e que começou recentemente a trabalhar com o Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f9096-106">The steps in this article assume that you are familiar with developing using Python and are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9096-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f9096-107">Prerequisites</span></span>
<span data-ttu-id="f9096-108">Este guia de início rápido usa os recursos criados em um destes guias como ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="f9096-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="f9096-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="f9096-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="f9096-110">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="f9096-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="f9096-111">Você também precisará de:</span><span class="sxs-lookup"><span data-stu-id="f9096-111">You also need:</span></span>
- <span data-ttu-id="f9096-112">[Python](https://www.python.org/downloads/) instalado</span><span class="sxs-lookup"><span data-stu-id="f9096-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="f9096-113">Pacote [pip](https://pip.pypa.io/en/stable/installing/) instalado (o pip já está instalado se você está trabalhando com binários Python 2 > = 2.7.9 ou Python 3 > = 3,4 baixados de [python.org](https://python.org).</span><span class="sxs-lookup"><span data-stu-id="f9096-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-the-python-connection-libraries-for-postgresql"></a><span data-ttu-id="f9096-114">Instalar as bibliotecas de conexão do Python para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f9096-114">Install the Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="f9096-115">Instale o pacote [psycopg2](http://initd.org/psycopg/docs/install.html), que permite a conexão e a consulta ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f9096-115">Install the [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you to connect and query the database.</span></span> <span data-ttu-id="f9096-116">psycopg2 está [disponível em PyPI](https://pypi.python.org/pypi/psycopg2/) na forma de pacotes de [roda](http://pythonwheels.com/) para as plataformas mais comuns (Linux, OSX, Windows).</span><span class="sxs-lookup"><span data-stu-id="f9096-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in the form of [wheel](http://pythonwheels.com/) packages for the most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="f9096-117">Use a instalação de pip para obter a versão binária do módulo, incluindo todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="f9096-117">Use pip install to get the binary version of the module including all the dependencies.</span></span>

1. <span data-ttu-id="f9096-118">Em seu próprio computador, inicie uma interface de linha de comando:</span><span class="sxs-lookup"><span data-stu-id="f9096-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="f9096-119">No Linux, abra o shell do Bash.</span><span class="sxs-lookup"><span data-stu-id="f9096-119">On Linux, launch the Bash shell.</span></span>
    - <span data-ttu-id="f9096-120">No macOS, abra o Terminal.</span><span class="sxs-lookup"><span data-stu-id="f9096-120">On macOS, launch the Terminal.</span></span>
    - <span data-ttu-id="f9096-121">No Windows, inicie o prompt de comando no menu Iniciar.</span><span class="sxs-lookup"><span data-stu-id="f9096-121">On Windows, launch the Command Prompt from the Start Menu.</span></span>
2. <span data-ttu-id="f9096-122">Não deixe de usar a versão mais recente de pip executando um comando como:</span><span class="sxs-lookup"><span data-stu-id="f9096-122">Ensure that you are using the most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="f9096-123">Execute o seguinte comando para instalar o pacote psycopg2:</span><span class="sxs-lookup"><span data-stu-id="f9096-123">Run the following command to install the psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="f9096-124">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="f9096-124">Get connection information</span></span>
<span data-ttu-id="f9096-125">Obtenha as informações de conexão necessárias para se conectar ao Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f9096-125">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="f9096-126">Você precisa das credenciais de logon e do nome do servidor totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="f9096-126">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="f9096-127">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f9096-127">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f9096-128">No menu à esquerda no Portal do Azure, clique em **Todos os recursos** e pesquise **mypgserver-20170401** (o servidor que você acabou de criar).</span><span class="sxs-lookup"><span data-stu-id="f9096-128">From the left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (the server you just created).</span></span>
3. <span data-ttu-id="f9096-129">Clique no nome do servidor **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="f9096-129">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="f9096-130">Selecione a página **Visão Geral** do servidor e anote o **Nome do servidor** e **Nome de logon do administrador do servidor**.</span><span class="sxs-lookup"><span data-stu-id="f9096-130">Select the server's **Overview** page, and then make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="f9096-131">![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="f9096-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="f9096-132">Se você se esquecer das informações de logon do servidor, navegue até a página **Visão Geral** para exibir o nome de logon do Administrador do servidor e, se necessário, redefinir a senha.</span><span class="sxs-lookup"><span data-stu-id="f9096-132">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="how-to-run-python-code"></a><span data-ttu-id="f9096-133">Como executar o código Python</span><span class="sxs-lookup"><span data-stu-id="f9096-133">How to run Python code</span></span>
<span data-ttu-id="f9096-134">Este tópico contém um total de quatro exemplos de código, cada uma executando uma função específica.</span><span class="sxs-lookup"><span data-stu-id="f9096-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="f9096-135">As instruções a seguir indicam como criar um arquivo de texto, inserir um bloco de código e salvar o arquivo para que possa ser executado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="f9096-135">The following instructions indicate how to create a text file, insert a code block, and then save the file so that you can run it later.</span></span> <span data-ttu-id="f9096-136">Crie quatro arquivos separados, um para cada bloco de código.</span><span class="sxs-lookup"><span data-stu-id="f9096-136">Be sure to create four separate files, one for each code block.</span></span>

- <span data-ttu-id="f9096-137">Crie um novo arquivo usando seu editor de texto favorito.</span><span class="sxs-lookup"><span data-stu-id="f9096-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="f9096-138">Copie e cole um dos exemplos de código das seções a seguir no arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="f9096-138">Copy and paste one of the code samples in the following sections into the text file.</span></span> <span data-ttu-id="f9096-139">Substitua os parâmetros **host**, **dbname**, **user** e **password** pelos valores que você especificou ao criar o servidor e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f9096-139">Replace the **host**, **dbname**, **user**, and **password** parameters with the values that you specified when you created the server and database.</span></span>
- <span data-ttu-id="f9096-140">Salve o arquivo com a extensão .py (por exemplo, postgres.py) em sua pasta de projeto.</span><span class="sxs-lookup"><span data-stu-id="f9096-140">Save the file with the .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="f9096-141">Se você está executando o sistema operacional Windows, selecione a codificação UTF-8 ao salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="f9096-141">If you are running the Windows OS, be sure to select UTF-8 encoding when saving the file.</span></span> 
- <span data-ttu-id="f9096-142">Inicie o prompt de comando ou shell do Bash e altere o diretório para a pasta do projeto, por exemplo, `cd postgres`.</span><span class="sxs-lookup"><span data-stu-id="f9096-142">Launch the Command Prompt or Bash shell and then change the directory to your project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="f9096-143">Para executar o código, digite o comando python seguido pelo nome do arquivo, por exemplo, `Python postgres.py`.</span><span class="sxs-lookup"><span data-stu-id="f9096-143">To run the code, type the Python command followed by the file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="f9096-144">A partir da versão 3 do Python, você poderá ver o erro `SyntaxError: Missing parentheses in call to 'print'` ao executar os blocos de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="f9096-144">Starting in Python version 3, you may see the error `SyntaxError: Missing parentheses in call to 'print'` when running the following code blocks.</span></span> <span data-ttu-id="f9096-145">Se isso acontecer, substitua cada chamada ao comando `print "string"` por uma chamada de função usando parênteses, como `print("string")`.</span><span class="sxs-lookup"><span data-stu-id="f9096-145">If that happens, replace each call to the command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="f9096-146">Conectar-se, criar tabela e inserir dados</span><span class="sxs-lookup"><span data-stu-id="f9096-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="f9096-147">Use o código a seguir para se conectar e carregar os dados usando a função [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) com a instrução SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="f9096-147">Use the following code to connect and load the data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="f9096-148">A função [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) é usada para executar a consulta SQL no banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f9096-148">The [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used to execute the SQL query against PostgreSQL database.</span></span> <span data-ttu-id="f9096-149">Substitua os parâmetros host, dbname, user e password pelos valores que você especificou ao criar o servidor e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f9096-149">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
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

<span data-ttu-id="f9096-150">Depois que o código é executado com êxito, a saída é exibida da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f9096-150">After the code runs successfully, the output appears as follows:</span></span>

![Saída da linha de comando](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="f9096-152">Ler dados</span><span class="sxs-lookup"><span data-stu-id="f9096-152">Read data</span></span>
<span data-ttu-id="f9096-153">Use o código a seguir para ler os dados inseridos usando a função [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) a instrução SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="f9096-153">Use the following code to read the data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="f9096-154">Essa função aceita uma consulta e retorna um conjunto de resultados que pode ser iterado com o uso de [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span><span class="sxs-lookup"><span data-stu-id="f9096-154">This function accepts a query and returns a result set that can be iterated over with the use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="f9096-155">Substitua os parâmetros host, dbname, user e password pelos valores que você especificou ao criar o servidor e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f9096-155">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
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

## <a name="update-data"></a><span data-ttu-id="f9096-156">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="f9096-156">Update data</span></span>
<span data-ttu-id="f9096-157">Use o código a seguir para atualizar a linha de inventário que você inseriu anteriormente usando a função [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) com a instrução SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="f9096-157">Use the following code to update the inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="f9096-158">Substitua os parâmetros host, dbname, user e password pelos valores que você especificou ao criar o servidor e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f9096-158">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
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

# Update a data row in the table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a><span data-ttu-id="f9096-159">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="f9096-159">Delete data</span></span>
<span data-ttu-id="f9096-160">Use o código a seguir para excluir o item de inventário que você inseriu anteriormente usando a função [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) com a instrução SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="f9096-160">Use the following code to delete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="f9096-161">Substitua os parâmetros host, dbname, user e password pelos valores que você especificou ao criar o servidor e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f9096-161">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
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

## <a name="next-steps"></a><span data-ttu-id="f9096-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f9096-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f9096-163">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="f9096-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
