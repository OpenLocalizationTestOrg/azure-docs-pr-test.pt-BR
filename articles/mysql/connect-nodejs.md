---
title: "TooAzure banco de dados de conexão para MySQL a partir do Node. js | Microsoft Docs"
description: "Este guia de início rápido fornece vários exemplos de código do Node. js use tooconnect e consultar dados do banco de dados MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/17/2017
ms.openlocfilehash: ed9a39b5ab003e8216cef1c0f6a95a75c3db8458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a>Banco de dados do Azure para MySQL: Use Node. js tooconnect e consultar dados
Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para usar o MySQL [Node.js](https://nodejs.org/) de plataformas Mac, Ubuntu Linux e Windows. Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação. Olá etapas neste artigo presumem que você esteja familiarizado com o desenvolvimento usando o Node. js, e que você é novo tooworking com o banco de dados do Azure para MySQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:
- [Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

Você também precisará:
- Instalar Olá [Node.js](https://nodejs.org) tempo de execução.
- Instalar [mysql2](https://www.npmjs.com/package/mysql2) tooMySQL tooconnect de saudação aplicativo Node. js do pacote. 

## <a name="install-nodejs-and-hello-mysql-connector"></a>Instalar o Node. js e Olá conector MySQL
Dependendo de sua plataforma, siga Olá instruções apropriadas tooinstall Node. js. Use npm tooinstall Olá mysql2 pacote e suas dependências em sua pasta de projeto.

### <a name="windows"></a>**Windows**
1. Visite Olá [página de downloads do Node. js](https://nodejs.org/en/download/) e selecione a opção de instalador desejada do Windows.
2. Crie uma pasta de projeto local, como `nodejsmysql`. 
3. Inicie o prompt de comando hello e cd na pasta de projeto Olá, como`cd c:\nodejsmysql\`
4. Execute biblioteca do hello NPM ferramenta tooinstall Olá mysql2 na pasta de projeto hello.

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. Verificar a instalação de saudação verificando Olá `npm list` de saída de texto para `mysql2@1.3.5`.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
1. A seguir Olá execução comandos tooinstall **Node.js** e **npm** Gerenciador de pacotes de saudação para Node. js.

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. Executar Olá toomake comandos a seguir em uma pasta de projeto `mysqlnodejs` e instale o pacote de mysql2 de saudação para essa pasta.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. Verificar a instalação de saudação marcando texto de saída da lista npm `mysql2@1.3.5`.

### <a name="mac-os"></a>**Mac OS**
1. Digite hello tooinstall comandos a seguir **brew**, um Gerenciador de pacotes de fácil de usar para Mac OS X e **Node.js**.

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. Executar Olá toomake comandos a seguir em uma pasta de projeto `mysqlnodejs` e instale o pacote de mysql2 de saudação para essa pasta.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. Verificar a instalação de saudação verificando Olá `npm list` de saída de texto para `mysql2@1.3.6`. número de versão Hello pode variar conforme novos patches são liberados.

## <a name="get-connection-information"></a>Obter informações de conexão
Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL. Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. No painel esquerdo do hello, clique em **todos os recursos**e em seguida, procure o servidor Olá que você criou (por exemplo, **myserver4demo**).
3. Clique em nome do servidor de saudação **myserver4demo**.
4. Servidor de saudação selecione **propriedades** página. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
 ![Banco de Dados do Azure para MySQL – Logon de administrador do servidor](./media/connect-nodejs/1_server-properties-name-login.png)
5. Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.

## <a name="running-hello-javascript-code-in-nodejs"></a>Executando o código JavaScript Olá no Node. js
1. Cole o código JavaScript Olá para arquivos de texto e salve em uma pasta de projeto com. js da extensão de arquivo, como C:\nodejsmysql\createtable.js ou /home/username/nodejsmysql/createtable.js
2. Inicie o prompt de comando hello ou bash shell. Altere o diretório para a pasta do projeto `cd nodejsmysql`.
3. aplicativo de hello toorun, digite Olá nó comando seguido pelo nome de arquivo hello, como `node createtable.js`.
4. No Windows, se o aplicativo de nó hello não está em seu caminho de variável de ambiente, talvez seja necessário aplicativo toouse hello caminho completo toolaunch Olá nó, como`"C:\Program Files\nodejs\node.exe" createtable.js`

## <a name="connect-create-table-and-insert-data"></a>Conectar-se, criar tabela e inserir dados
A seguir use Olá tooconnect de código e carregar Olá dados usando **CREATE TABLE** e **INSERT INTO** instruções SQL.

Olá [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método é toointerface usado com o servidor MySQL de saudação. Olá [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) função é servidor de toohello tooestablish usado Olá conexão. Olá [Query ()](https://github.com/mysqljs/mysql#performing-queries) função é a consulta SQL Olá tooexecute usado no banco de dados MySQL. 

Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
    if (err) { 
        console.log("!!! Cannot connect !!! Error:");
        throw err;
    }
    else
    {
       console.log("Connection established.");
           queryDatabase();
    }   
});

function queryDatabase(){
       conn.query('DROP TABLE IF EXISTS inventory;', function (err, results, fields) { 
            if (err) throw err; 
            console.log('Dropped inventory table if existed.');
        })
       conn.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);', 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Created inventory table.');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['banana', 150], 
            function (err, results, fields) {
                if (err) throw err;
            else console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['orange', 154], 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['apple', 100], 
        function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.end(function (err) { 
        if (err) throw err;
        else  console.log('Done.') 
        });
};
```

## <a name="read-data"></a>Ler dados
A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL. 

Olá [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método é toointerface usado com o servidor MySQL de saudação. Olá [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) método é servidor de toohello tooestablish usado Olá conexão. Olá [Query ()](https://github.com/mysqljs/mysql#performing-queries) método é a consulta SQL Olá tooexecute usado no banco de dados MySQL. matriz de resultados de saudação é toohold usado Olá resultados de consulta de saudação.

Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            readData();
        }   
    });

function readData(){
        conn.query('SELECT * FROM inventory', 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Selected ' + results.length + ' row(s).');
                for (i = 0; i < results.length; i++) {
                    console.log('Row: ' + JSON.stringify(results[i]));
                }
                console.log('Done.');
            })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Closing connection.') 
        });
};
```

## <a name="update-data"></a>Atualizar dados
A seguir use Olá código tooconnect e ler Olá dados usando um **atualização** instrução SQL. 

Olá [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método é toointerface usado com o servidor MySQL de saudação. Olá [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) método é servidor de toohello tooestablish usado Olá conexão. Olá [Query ()](https://github.com/mysqljs/mysql#performing-queries) método é a consulta SQL Olá tooexecute usado no banco de dados MySQL. 

Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            updateData();
        }   
    });

function updateData(){
       conn.query('UPDATE inventory SET quantity = ? WHERE name = ?', [200, 'banana'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Updated ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="delete-data"></a>Excluir dados
A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL. 

Olá [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método é toointerface usado com o servidor MySQL de saudação. Olá [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) método é servidor de toohello tooestablish usado Olá conexão. Olá [Query ()](https://github.com/mysqljs/mysql#performing-queries) método é a consulta SQL Olá tooexecute usado no banco de dados MySQL. 

Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            deleteData();
        }   
    });

function deleteData(){
       conn.query('DELETE FROM inventory WHERE name = ?', ['orange'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Deleted ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./concepts-migrate-import-export.md)
