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
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a>Banco de dados do Azure para PostgreSQL: uso Python tooconnect e consultar dados
Este guia de início rápido demonstra como toouse [Python](https://python.org) tooconnect tooan banco de dados do Azure para PostgreSQL. Ele também demonstra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação do macOS, Ubuntu Linux e plataformas do Windows. etapas de Olá neste artigo presumem que você esteja familiarizado com o desenvolvimento usando Python e é tooworking novo com o banco de dados do Azure para PostgreSQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:
- [Criar Banco de dados - Portal](quickstart-create-server-database-portal.md)
- [Criar Banco de dados - CLI](quickstart-create-server-database-azure-cli.md)

Você também precisará de:
- [Python](https://www.python.org/downloads/) instalado
- Pacote [pip](https://pip.pypa.io/en/stable/installing/) instalado (o pip já está instalado se você está trabalhando com binários Python 2 > = 2.7.9 ou Python 3 > = 3,4 baixados de [python.org](https://python.org).

## <a name="install-hello-python-connection-libraries-for-postgresql"></a>Instalar bibliotecas de conexão de Python Olá para PostgreSQL
Instalar Olá [psycopg2](http://initd.org/psycopg/docs/install.html) pacote, que permite que você tooconnect e consulta de banco de dados de saudação. é psycopg2 [disponível em PyPI](https://pypi.python.org/pypi/psycopg2/) na forma de saudação de [roda](http://pythonwheels.com/) pacotes para plataformas mais comuns de saudação (Linux e OSX, Windows). Use pip instalar versão binária do tooget saudação do módulo de hello, incluindo todas as dependências de saudação.

1. Em seu próprio computador, inicie uma interface de linha de comando:
    - No Linux, inicie o shell Bash hello.
    - Em macOS, inicie Olá Terminal.
    - No Windows, inicie a saudação de Prompt de comando do Menu Iniciar do hello.
2. Certifique-se de que estão usando a versão mais atual Olá de pip executando um comando como:
    ```cmd
    pip install -U pip
    ```

3. Execute Olá pacote do comando tooinstall Olá psycopg2 a seguir:
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a>Obter informações de conexão
Obter Olá conexão informações necessárias tooconnect toohello banco de dados PostgreSQL. Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e procure **mypgserver 20170401** (servidor de saudação você acabou de criar).
3. Clique em nome do servidor de saudação **mypgserver 20170401**.
4. Servidor de saudação selecione **visão geral** página e anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
 ![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-python/1-connection-string.png)
5. Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.

## <a name="how-toorun-python-code"></a>Como toorun código Python
Este tópico contém um total de quatro exemplos de código, cada uma executando uma função específica. Olá instruções a seguir indicam como toocreate um arquivo de texto, inserir um bloco de código e, em seguida, salve o arquivo de saudação para que possa ser executado posteriormente. Ser se toocreate quatro arquivos separados, um para cada bloco de código.

- Crie um novo arquivo usando seu editor de texto favorito.
- Copie e cole um dos exemplos de código Olá Olá seções a seguir no arquivo de texto de saudação. Substituir saudação **host**, **dbname**, **usuário**, e **senha** parâmetros com valores hello que você especificou quando criou Olá servidor e banco de dados.
- Salve o arquivo de saudação com extensão de py hello (por exemplo, postgres.py) em sua pasta de projeto. Se você estiver executando Olá sistema operacional Windows, ser se tooselect codificação UTF-8 ao salvar arquivo hello. 
- Inicie o shell do Prompt de comando ou Bash hello e altere a pasta de projeto tooyour do diretório hello, por exemplo `cd postgres`.
-  código toorun Olá Olá tipo comando Python seguido pelo nome de arquivo hello, por exemplo `Python postgres.py`.

> [!NOTE]
> A partir do Python versão 3, você pode ver o erro de saudação `SyntaxError: Missing parentheses in call too'print'` ao executar Olá blocos de código a seguir. Se isso acontecer, substitua cada comando de toohello chamada `print "string"` com uma chamada de função usando parênteses, como `print("string")`.

## <a name="connect-create-table-and-insert-data"></a>Conectar-se, criar tabela e inserir dados
A seguir use Olá tooconnect de código e carregar Olá dados usando [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) funcionar com **inserir** instrução SQL. Olá [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) função é a consulta SQL Olá tooexecute usado no banco de dados PostgreSQL. Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.

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

Depois de saudação código é executado com êxito, saída de hello aparece da seguinte maneira:

![Saída da linha de comando](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a>Ler dados
Dados de saudação tooread inseridos usando de código a seguir de saudação de uso [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funcionar com **selecione** instrução SQL. Essa função aceita uma consulta e retorna um conjunto de resultados que pode ser iteradas com o uso de saudação do [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall). Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.

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

## <a name="update-data"></a>Atualizar dados
Linha de inventário de saudação tooupdate inserido anteriormente usando de código a seguir de saudação de uso [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funcionar com **atualização** instrução SQL. Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.

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

## <a name="delete-data"></a>Excluir dados
Toodelete um item de estoque que você inseriu anteriormente usando o código a seguir de Olá de uso [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funcionar com **excluir** instrução SQL. Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.

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

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./howto-migrate-using-export-and-import.md)
