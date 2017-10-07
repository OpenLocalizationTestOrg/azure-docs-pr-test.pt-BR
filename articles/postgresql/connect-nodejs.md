---
title: Conecte-se tooAzure banco de dados para PostgreSQL do Node. js | Microsoft Docs
description: "Este guia de início rápido fornece um exemplo de código Node. js, você pode usar tooconnect e consultar dados do banco de dados PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 9b269d72068ecc24bcf3fb447a2efeda512c698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a>Banco de dados do Azure para PostgreSQL: Use Node. js tooconnect e consultar dados
Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para usar PostgreSQL [Node.js](https://nodejs.org/). Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação. Olá etapas neste artigo presumem que você esteja familiarizado com o desenvolvimento usando o Node. js, e que você é novo tooworking com o banco de dados do Azure para PostgreSQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:
- [Criar Banco de dados - Portal](quickstart-create-server-database-portal.md)
- [Criar Banco de dados - CLI](quickstart-create-server-database-azure-cli.md)

Você também precisará:
- Instale o [Node.js](https://nodejs.org)

## <a name="install-pg-client"></a>Instalar o cliente pg
Instalar [pg](https://www.npmjs.com/package/pg), que é um cliente PostgreSQL para Node.js.

toodo assim, executar o Gerenciador de pacote de nó hello (npm) para JavaScript de seu cliente de pg de saudação de tooinstall de linha de comando.
```bash
npm install pg
```

Verificar a instalação de saudação listando pacotes Olá instalados.
```bash
npm list
```

## <a name="get-connection-information"></a>Obter informações de conexão
Obter Olá conexão informações necessárias tooconnect toohello banco de dados PostgreSQL. Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e procure o servidor de saudação que você acabou de criar.
3. Clique em nome do servidor de saudação.
4. Servidor de saudação selecione **visão geral** página. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
 ![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-nodejs/1-connection-string.png)
5. Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.

## <a name="running-hello-javascript-code-in-nodejs"></a>Executando o código JavaScript Olá no Node. js
Você pode iniciar o Node. js do prompt de comando Olá bash shell ou windows digitando `node`, execute o código de JavaScript de exemplo hello interativamente por cópia e colando-o no prompt de saudação. Como alternativa, você pode salvar o código JavaScript Olá em um arquivo de texto e iniciar `node filename.js` com o nome de arquivo hello como um parâmetro toorun-lo.

## <a name="connect-create-table-and-insert-data"></a>Conectar-se, criar tabela e inserir dados
A seguir use Olá tooconnect de código e carregar Olá dados usando **CREATE TABLE** e **INSERT INTO** instruções SQL.
Olá [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto é toointerface usado com o servidor do hello PostgreSQL. Olá [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) função é servidor de toohello tooestablish usado Olá conexão. Olá [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) função é a consulta SQL Olá tooexecute usado no banco de dados PostgreSQL. 

Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DROP TABLE IF EXISTS inventory;
        CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
        INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
        INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
        INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    `;

    client
        .query(query)
        .then(() => {
            console.log('Table created successfully!');
            client.end(console.log('Closed client connection'));
        })
        .catch(err => console.log(err))
        .then(() => {
            console.log('Finished execution, exiting now');
            process.exit();
        });
}
```

## <a name="read-data"></a>Ler dados
A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL. Olá [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto é toointerface usado com o servidor do hello PostgreSQL. Olá [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) função é servidor de toohello tooestablish usado Olá conexão. Olá [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) função é a consulta SQL Olá tooexecute usado no banco de dados PostgreSQL. 

Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else { queryDatabase(); }
});

function queryDatabase() {
  
    console.log(`Running query tooPostgreSQL server: ${config.host}`);

    const query = 'SELECT * FROM inventory;';

    client.query(query)
        .then(res => {
            const rows = res.rows;

            rows.map(row => {
                console.log(`Read: ${JSON.stringify(row)}`);
            });

            process.exit();
        })
        .catch(err => {
            console.log(err);
        });
}
```

## <a name="update-data"></a>Atualizar dados
A seguir use Olá código tooconnect e ler Olá dados usando um **atualização** instrução SQL. Olá [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto é toointerface usado com o servidor do hello PostgreSQL. Olá [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) função é servidor de toohello tooestablish usado Olá conexão. Olá [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) função é a consulta SQL Olá tooexecute usado no banco de dados PostgreSQL. 

Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        UPDATE inventory 
        SET quantity= 1000 WHERE name='banana';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Update completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="delete-data"></a>Excluir dados
A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL. Olá [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto é toointerface usado com o servidor do hello PostgreSQL. Olá [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) função é servidor de toohello tooestablish usado Olá conexão. Olá [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) função é a consulta SQL Olá tooexecute usado no banco de dados PostgreSQL. 

Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) {
        throw err;
    } else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DELETE FROM inventory 
        WHERE name = 'apple';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Delete completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./howto-migrate-using-export-and-import.md)
