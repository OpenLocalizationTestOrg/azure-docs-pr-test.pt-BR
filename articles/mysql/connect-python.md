---
title: "TooAzure banco de dados de conexão para MySQL da Python | Microsoft Docs"
description: "Este guia de início rápido fornece o que Python várias amostras, você pode usar tooconnect e consultar dados do banco de dados do Azure para MySQL de código."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: python
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 9df5211adcab886a502fd138347aed8fb587cd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="e9c63-103">Banco de dados do Azure para MySQL: uso Python tooconnect e consultar dados</span><span class="sxs-lookup"><span data-stu-id="e9c63-103">Azure Database for MySQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="e9c63-104">Este guia de início rápido demonstra como toouse [Python](https://python.org) tooconnect tooan banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="e9c63-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for MySQL.</span></span> <span data-ttu-id="e9c63-105">Ele usa instruções tooquery, insert, update e delete dados do SQL no banco de dados de saudação de plataformas Windows, Ubuntu Linux e Mac OS.</span><span class="sxs-lookup"><span data-stu-id="e9c63-105">It uses SQL statements tooquery, insert, update, and delete data in hello database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="e9c63-106">Olá etapas neste artigo presumem que você esteja familiarizado com o desenvolvimento com Python e é tooworking novo com o banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="e9c63-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9c63-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e9c63-107">Prerequisites</span></span>
<span data-ttu-id="e9c63-108">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="e9c63-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="e9c63-109">Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e9c63-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="e9c63-110">Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e9c63-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a><span data-ttu-id="e9c63-111">Instalar o Python e Olá conector MySQL</span><span class="sxs-lookup"><span data-stu-id="e9c63-111">Install Python and hello MySQL connector</span></span>
<span data-ttu-id="e9c63-112">Instalar [Python](https://www.python.org/downloads/) e hello [conector MySQL da Python](https://dev.mysql.com/downloads/connector/python/) em seu próprio computador.</span><span class="sxs-lookup"><span data-stu-id="e9c63-112">Install [Python](https://www.python.org/downloads/) and hello [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="e9c63-113">Dependendo de sua plataforma, siga as etapas de saudação:</span><span class="sxs-lookup"><span data-stu-id="e9c63-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="e9c63-114">Windows</span><span class="sxs-lookup"><span data-stu-id="e9c63-114">Windows</span></span>
1. <span data-ttu-id="e9c63-115">Baixe e instale o Python 2.7 em [python.org](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="e9c63-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="e9c63-116">Verifique a instalação de Python de saudação iniciando Olá prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="e9c63-116">Check hello Python installation by launching hello command prompt.</span></span> <span data-ttu-id="e9c63-117">Execute o comando Olá `C:\python27\python.exe -V` usando Olá maiusculas V switch toosee Olá número de versão.</span><span class="sxs-lookup"><span data-stu-id="e9c63-117">Run hello command `C:\python27\python.exe -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="e9c63-118">Instalar o conector do Python Olá para MySQL a partir do [mysql.com](https://dev.mysql.com/downloads/connector/python/) versão tooyour correspondente de Python.</span><span class="sxs-lookup"><span data-stu-id="e9c63-118">Install hello Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding tooyour version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="e9c63-119">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="e9c63-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="e9c63-120">No Linux (Ubuntu), o Python normalmente é instalado como parte da instalação padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9c63-120">In Linux (Ubuntu), Python is typically installed as part of hello default installation.</span></span>
2. <span data-ttu-id="e9c63-121">Verifique a instalação de Python de saudação iniciando o shell bash hello.</span><span class="sxs-lookup"><span data-stu-id="e9c63-121">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="e9c63-122">Execute o comando Olá `python -V` usando Olá maiusculas V switch toosee Olá número de versão.</span><span class="sxs-lookup"><span data-stu-id="e9c63-122">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="e9c63-123">Verificar instalação de PIP Olá executando Olá `pip show pip -V` toosee número de versão de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="e9c63-123">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span> 
4. <span data-ttu-id="e9c63-124">PIP pode ser incluído em algumas versões do Python.</span><span class="sxs-lookup"><span data-stu-id="e9c63-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="e9c63-125">Se o PIP não estiver instalado, você pode instalar Olá [PIP] (https://pip.pypa.io/en/stable/installing/) o pacote, executando o comando `sudo apt-get install python-pip`.</span><span class="sxs-lookup"><span data-stu-id="e9c63-125">If PIP is not installed, you may install hello [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="e9c63-126">Atualização PIP toohello versão mais recente, executando Olá `pip install -U pip` comando.</span><span class="sxs-lookup"><span data-stu-id="e9c63-126">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="e9c63-127">Instale o conector de MySQL de saudação Python e suas dependências usando o comando PIP hello:</span><span class="sxs-lookup"><span data-stu-id="e9c63-127">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="e9c63-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="e9c63-128">MacOS</span></span>
1. <span data-ttu-id="e9c63-129">No Mac OS, Python normalmente é instalado como parte da instalação do sistema operacional padrão hello.</span><span class="sxs-lookup"><span data-stu-id="e9c63-129">In Mac OS, Python is typically installed as part of hello default OS installation.</span></span>
2. <span data-ttu-id="e9c63-130">Verifique a instalação de Python de saudação iniciando o shell bash hello.</span><span class="sxs-lookup"><span data-stu-id="e9c63-130">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="e9c63-131">Execute o comando Olá `python -V` usando Olá maiusculas V switch toosee Olá número de versão.</span><span class="sxs-lookup"><span data-stu-id="e9c63-131">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="e9c63-132">Verificar instalação de PIP Olá executando Olá `pip show pip -V` toosee número de versão de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="e9c63-132">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span>
4. <span data-ttu-id="e9c63-133">PIP pode ser incluído em algumas versões do Python.</span><span class="sxs-lookup"><span data-stu-id="e9c63-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="e9c63-134">Se o PIP não estiver instalado, você pode instalar Olá [PIP](https://pip.pypa.io/en/stable/installing/) pacote.</span><span class="sxs-lookup"><span data-stu-id="e9c63-134">If PIP is not installed, you may install hello [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="e9c63-135">Atualização PIP toohello versão mais recente, executando Olá `pip install -U pip` comando.</span><span class="sxs-lookup"><span data-stu-id="e9c63-135">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="e9c63-136">Instale o conector de MySQL de saudação Python e suas dependências usando o comando PIP hello:</span><span class="sxs-lookup"><span data-stu-id="e9c63-136">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="e9c63-137">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="e9c63-137">Get connection information</span></span>
<span data-ttu-id="e9c63-138">Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="e9c63-138">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="e9c63-139">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="e9c63-139">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="e9c63-140">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e9c63-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e9c63-141">No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e procure o servidor de saudação você ter creased, como **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="e9c63-141">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="e9c63-142">Clique em nome do servidor de saudação **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="e9c63-142">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="e9c63-143">Servidor de saudação selecione **propriedades** página.</span><span class="sxs-lookup"><span data-stu-id="e9c63-143">Select hello server's **Properties** page.</span></span> <span data-ttu-id="e9c63-144">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="e9c63-144">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="e9c63-145">![Banco de Dados do Azure para MySQL – Logon de administrador do servidor](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="e9c63-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="e9c63-146">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="e9c63-146">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="e9c63-147">Executar Código Python</span><span class="sxs-lookup"><span data-stu-id="e9c63-147">Run Python Code</span></span>
- <span data-ttu-id="e9c63-148">Cole o código Olá em um arquivo de texto e salve o arquivo de saudação em uma pasta de projeto com py de extensão de arquivo, como C:\pythonmysql\createtable.py ou /home/username/pythonmysql/createtable.py</span><span class="sxs-lookup"><span data-stu-id="e9c63-148">Paste hello code into a text file, and save hello file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="e9c63-149">código de saudação toorun, inicie o prompt de comando hello ou bash shell.</span><span class="sxs-lookup"><span data-stu-id="e9c63-149">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="e9c63-150">Altere o diretório para a pasta do projeto `cd pythonmysql`.</span><span class="sxs-lookup"><span data-stu-id="e9c63-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="e9c63-151">Em seguida, digite o comando a python Olá seguido pelo nome de arquivo hello `python createtable.py` aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="e9c63-151">Then type hello python command followed by hello file name `python createtable.py` toorun hello application.</span></span> <span data-ttu-id="e9c63-152">No Olá sistema operacional Windows, se python.exe não for encontrado, você pode fornecer Olá caminho completo toohello executável ou adicione o caminho do Python Olá na variável de ambiente path hello.</span><span class="sxs-lookup"><span data-stu-id="e9c63-152">On hello Windows OS, if python.exe is not found, you may provide hello full path toohello executable, or add hello Python path into hello path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="e9c63-153">Conectar-se, criar tabela e inserir dados</span><span class="sxs-lookup"><span data-stu-id="e9c63-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="e9c63-154">A seguir use Olá código tooconnect toohello servidor, criar uma tabela e carregar Olá dados usando um **inserir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e9c63-154">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="e9c63-155">No código hello, biblioteca de mysql.connector Olá é importada.</span><span class="sxs-lookup"><span data-stu-id="e9c63-155">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="e9c63-156">Olá [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) função é usada tooconnect tooAzure banco de dados MySQL usando Olá [argumentos de conexão](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) na coleção de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9c63-156">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="e9c63-157">código de saudação usa um cursor em conexão Olá, e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método executa a consulta SQL de saudação no banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="e9c63-157">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="e9c63-158">Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9c63-158">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Drop previous table of same name if one exists
  cursor.execute("DROP TABLE IF EXISTS inventory;")
  print("Finished dropping table (if existed).")

  # Create table
  cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
  print("Finished creating table.")

  # Insert some data into table
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
  print("Inserted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="read-data"></a><span data-ttu-id="e9c63-159">Ler dados</span><span class="sxs-lookup"><span data-stu-id="e9c63-159">Read data</span></span>
<span data-ttu-id="e9c63-160">A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e9c63-160">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="e9c63-161">No código hello, biblioteca de mysql.connector Olá é importada.</span><span class="sxs-lookup"><span data-stu-id="e9c63-161">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="e9c63-162">Olá [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) função é usada tooconnect tooAzure banco de dados MySQL usando Olá [argumentos de conexão](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) na coleção de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9c63-162">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="e9c63-163">código de saudação usa um cursor em conexão Olá, e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método executa a instrução de SQL de saudação no banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="e9c63-163">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> <span data-ttu-id="e9c63-164">linhas de dados de saudação são lidos usando Olá [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) método.</span><span class="sxs-lookup"><span data-stu-id="e9c63-164">hello data rows are read using hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="e9c63-165">Olá conjunto de resultados é mantido em uma linha da coleção e um para o iterador é tooloop usado em linhas de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9c63-165">hello result set is kept in a collection row and a for iterator is used tooloop over hello rows.</span></span>

<span data-ttu-id="e9c63-166">Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9c63-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Read data
  cursor.execute("SELECT * FROM inventory;")
  rows = cursor.fetchall()
  print("Read",cursor.rowcount,"row(s) of data.")

  # Print all rows
  for row in rows:
    print("Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2])))

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="update-data"></a><span data-ttu-id="e9c63-167">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="e9c63-167">Update data</span></span>
<span data-ttu-id="e9c63-168">A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e9c63-168">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="e9c63-169">No código hello, biblioteca de mysql.connector Olá é importada.</span><span class="sxs-lookup"><span data-stu-id="e9c63-169">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="e9c63-170">Olá [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) função é usada tooconnect tooAzure banco de dados MySQL usando Olá [argumentos de conexão](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) na coleção de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9c63-170">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="e9c63-171">código de saudação usa um cursor em conexão Olá, e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método executa a instrução de SQL de saudação no banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="e9c63-171">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> 

<span data-ttu-id="e9c63-172">Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9c63-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in hello table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a><span data-ttu-id="e9c63-173">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="e9c63-173">Delete data</span></span>
<span data-ttu-id="e9c63-174">A seguir use Olá código tooconnect e remover dados usando um **excluir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e9c63-174">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="e9c63-175">No código hello, biblioteca de mysql.connector Olá é importada.</span><span class="sxs-lookup"><span data-stu-id="e9c63-175">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="e9c63-176">Olá [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) função é usada tooconnect tooAzure banco de dados MySQL usando Olá [argumentos de conexão](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) na coleção de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9c63-176">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="e9c63-177">código de saudação usa um cursor em conexão Olá, e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método executa a consulta SQL de saudação no banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="e9c63-177">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="e9c63-178">Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9c63-178">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established.")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in hello table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a><span data-ttu-id="e9c63-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e9c63-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e9c63-180">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="e9c63-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
