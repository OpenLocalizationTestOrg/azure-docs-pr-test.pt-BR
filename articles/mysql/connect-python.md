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
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a>Banco de dados do Azure para MySQL: uso Python tooconnect e consultar dados
Este guia de início rápido demonstra como toouse [Python](https://python.org) tooconnect tooan banco de dados do Azure para MySQL. Ele usa instruções tooquery, insert, update e delete dados do SQL no banco de dados de saudação de plataformas Windows, Ubuntu Linux e Mac OS. Olá etapas neste artigo presumem que você esteja familiarizado com o desenvolvimento com Python e é tooworking novo com o banco de dados do Azure para MySQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:
- [Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a>Instalar o Python e Olá conector MySQL
Instalar [Python](https://www.python.org/downloads/) e hello [conector MySQL da Python](https://dev.mysql.com/downloads/connector/python/) em seu próprio computador. Dependendo de sua plataforma, siga as etapas de saudação:

### <a name="windows"></a>Windows
1. Baixe e instale o Python 2.7 em [python.org](https://www.python.org/downloads/windows/). 
2. Verifique a instalação de Python de saudação iniciando Olá prompt de comando. Execute o comando Olá `C:\python27\python.exe -V` usando Olá maiusculas V switch toosee Olá número de versão.
3. Instalar o conector do Python Olá para MySQL a partir do [mysql.com](https://dev.mysql.com/downloads/connector/python/) versão tooyour correspondente de Python.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. No Linux (Ubuntu), o Python normalmente é instalado como parte da instalação padrão de saudação.
2. Verifique a instalação de Python de saudação iniciando o shell bash hello. Execute o comando Olá `python -V` usando Olá maiusculas V switch toosee Olá número de versão.
3. Verificar instalação de PIP Olá executando Olá `pip show pip -V` toosee número de versão de saudação do comando. 
4. PIP pode ser incluído em algumas versões do Python. Se o PIP não estiver instalado, você pode instalar Olá [PIP] (https://pip.pypa.io/en/stable/installing/) o pacote, executando o comando `sudo apt-get install python-pip`.
5. Atualização PIP toohello versão mais recente, executando Olá `pip install -U pip` comando.
6. Instale o conector de MySQL de saudação Python e suas dependências usando o comando PIP hello:

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a>MacOS
1. No Mac OS, Python normalmente é instalado como parte da instalação do sistema operacional padrão hello.
2. Verifique a instalação de Python de saudação iniciando o shell bash hello. Execute o comando Olá `python -V` usando Olá maiusculas V switch toosee Olá número de versão.
3. Verificar instalação de PIP Olá executando Olá `pip show pip -V` toosee número de versão de saudação do comando.
4. PIP pode ser incluído em algumas versões do Python. Se o PIP não estiver instalado, você pode instalar Olá [PIP](https://pip.pypa.io/en/stable/installing/) pacote.
5. Atualização PIP toohello versão mais recente, executando Olá `pip install -U pip` comando.
6. Instale o conector de MySQL de saudação Python e suas dependências usando o comando PIP hello:

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a>Obter informações de conexão
Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL. Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e procure o servidor de saudação você ter creased, como **myserver4demo**.
3. Clique em nome do servidor de saudação **myserver4demo**.
4. Servidor de saudação selecione **propriedades** página. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
 ![Banco de Dados do Azure para MySQL – Logon de administrador do servidor](./media/connect-python/1_server-properties-name-login.png)
5. Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.
   

## <a name="run-python-code"></a>Executar Código Python
- Cole o código Olá em um arquivo de texto e salve o arquivo de saudação em uma pasta de projeto com py de extensão de arquivo, como C:\pythonmysql\createtable.py ou /home/username/pythonmysql/createtable.py
- código de saudação toorun, inicie o prompt de comando hello ou bash shell. Altere o diretório para a pasta do projeto `cd pythonmysql`. Em seguida, digite o comando a python Olá seguido pelo nome de arquivo hello `python createtable.py` aplicativo hello de toorun. No Olá sistema operacional Windows, se python.exe não for encontrado, você pode fornecer Olá caminho completo toohello executável ou adicione o caminho do Python Olá na variável de ambiente path hello. `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a>Conectar-se, criar tabela e inserir dados
A seguir use Olá código tooconnect toohello servidor, criar uma tabela e carregar Olá dados usando um **inserir** instrução SQL. 

No código hello, biblioteca de mysql.connector Olá é importada. Olá [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) função é usada tooconnect tooAzure banco de dados MySQL usando Olá [argumentos de conexão](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) na coleção de configuração de saudação. código de saudação usa um cursor em conexão Olá, e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método executa a consulta SQL de saudação no banco de dados MySQL. 

Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.

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

## <a name="read-data"></a>Ler dados
A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL. 

No código hello, biblioteca de mysql.connector Olá é importada. Olá [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) função é usada tooconnect tooAzure banco de dados MySQL usando Olá [argumentos de conexão](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) na coleção de configuração de saudação. código de saudação usa um cursor em conexão Olá, e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método executa a instrução de SQL de saudação no banco de dados MySQL. linhas de dados de saudação são lidos usando Olá [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) método. Olá conjunto de resultados é mantido em uma linha da coleção e um para o iterador é tooloop usado em linhas de saudação.

Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.

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

## <a name="update-data"></a>Atualizar dados
A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL. 

No código hello, biblioteca de mysql.connector Olá é importada.  Olá [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) função é usada tooconnect tooAzure banco de dados MySQL usando Olá [argumentos de conexão](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) na coleção de configuração de saudação. código de saudação usa um cursor em conexão Olá, e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método executa a instrução de SQL de saudação no banco de dados MySQL. 

Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.

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

## <a name="delete-data"></a>Excluir dados
A seguir use Olá código tooconnect e remover dados usando um **excluir** instrução SQL. 

No código hello, biblioteca de mysql.connector Olá é importada.  Olá [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) função é usada tooconnect tooAzure banco de dados MySQL usando Olá [argumentos de conexão](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) na coleção de configuração de saudação. código de saudação usa um cursor em conexão Olá, e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método executa a consulta SQL de saudação no banco de dados MySQL. 

Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.

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

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./concepts-migrate-import-export.md)
