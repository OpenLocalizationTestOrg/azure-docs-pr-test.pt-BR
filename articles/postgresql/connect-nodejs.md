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
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="6cebe-103">Banco de dados do Azure para PostgreSQL: Use Node. js tooconnect e consultar dados</span><span class="sxs-lookup"><span data-stu-id="6cebe-103">Azure Database for PostgreSQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="6cebe-104">Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para usar PostgreSQL [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="6cebe-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="6cebe-105">Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6cebe-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="6cebe-106">Olá etapas neste artigo presumem que você esteja familiarizado com o desenvolvimento usando o Node. js, e que você é novo tooworking com o banco de dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cebe-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6cebe-107">Prerequisites</span></span>
<span data-ttu-id="6cebe-108">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="6cebe-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="6cebe-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="6cebe-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="6cebe-110">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="6cebe-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="6cebe-111">Você também precisará:</span><span class="sxs-lookup"><span data-stu-id="6cebe-111">You also need to:</span></span>
- <span data-ttu-id="6cebe-112">Instale o [Node.js](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="6cebe-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="6cebe-113">Instalar o cliente pg</span><span class="sxs-lookup"><span data-stu-id="6cebe-113">Install pg client</span></span>
<span data-ttu-id="6cebe-114">Instalar [pg](https://www.npmjs.com/package/pg), que é um cliente PostgreSQL para Node.js.</span><span class="sxs-lookup"><span data-stu-id="6cebe-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="6cebe-115">toodo assim, executar o Gerenciador de pacote de nó hello (npm) para JavaScript de seu cliente de pg de saudação de tooinstall de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="6cebe-115">toodo so, run hello node package manager (npm) for JavaScript from your command line tooinstall hello pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="6cebe-116">Verificar a instalação de saudação listando pacotes Olá instalados.</span><span class="sxs-lookup"><span data-stu-id="6cebe-116">Verify hello installation by listing hello packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="6cebe-117">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="6cebe-117">Get connection information</span></span>
<span data-ttu-id="6cebe-118">Obter Olá conexão informações necessárias tooconnect toohello banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-118">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="6cebe-119">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="6cebe-119">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="6cebe-120">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6cebe-120">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6cebe-121">No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e procure o servidor de saudação que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="6cebe-121">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created.</span></span>
3. <span data-ttu-id="6cebe-122">Clique em nome do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="6cebe-122">Click hello server name.</span></span>
4. <span data-ttu-id="6cebe-123">Servidor de saudação selecione **visão geral** página.</span><span class="sxs-lookup"><span data-stu-id="6cebe-123">Select hello server's **Overview** page.</span></span> <span data-ttu-id="6cebe-124">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="6cebe-124">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="6cebe-125">![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="6cebe-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="6cebe-126">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="6cebe-126">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="6cebe-127">Executando o código JavaScript Olá no Node. js</span><span class="sxs-lookup"><span data-stu-id="6cebe-127">Running hello JavaScript code in Node.js</span></span>
<span data-ttu-id="6cebe-128">Você pode iniciar o Node. js do prompt de comando Olá bash shell ou windows digitando `node`, execute o código de JavaScript de exemplo hello interativamente por cópia e colando-o no prompt de saudação.</span><span class="sxs-lookup"><span data-stu-id="6cebe-128">You may launch Node.js from hello bash shell or windows command prompt by typing `node`, then run hello example JavaScript code interactively by copy and pasting it onto hello prompt.</span></span> <span data-ttu-id="6cebe-129">Como alternativa, você pode salvar o código JavaScript Olá em um arquivo de texto e iniciar `node filename.js` com o nome de arquivo hello como um parâmetro toorun-lo.</span><span class="sxs-lookup"><span data-stu-id="6cebe-129">Alternatively, you may save hello JavaScript code into a text file and launch `node filename.js` with hello file name as a parameter toorun it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="6cebe-130">Conectar-se, criar tabela e inserir dados</span><span class="sxs-lookup"><span data-stu-id="6cebe-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="6cebe-131">A seguir use Olá tooconnect de código e carregar Olá dados usando **CREATE TABLE** e **INSERT INTO** instruções SQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-131">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="6cebe-132">Olá [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto é toointerface usado com o servidor do hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-132">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="6cebe-133">Olá [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) função é servidor de toohello tooestablish usado Olá conexão.</span><span class="sxs-lookup"><span data-stu-id="6cebe-133">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="6cebe-134">Olá [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) função é a consulta SQL Olá tooexecute usado no banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-134">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="6cebe-135">Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.</span><span class="sxs-lookup"><span data-stu-id="6cebe-135">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="6cebe-136">Ler dados</span><span class="sxs-lookup"><span data-stu-id="6cebe-136">Read data</span></span>
<span data-ttu-id="6cebe-137">A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-137">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="6cebe-138">Olá [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto é toointerface usado com o servidor do hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-138">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="6cebe-139">Olá [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) função é servidor de toohello tooestablish usado Olá conexão.</span><span class="sxs-lookup"><span data-stu-id="6cebe-139">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="6cebe-140">Olá [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) função é a consulta SQL Olá tooexecute usado no banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-140">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="6cebe-141">Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.</span><span class="sxs-lookup"><span data-stu-id="6cebe-141">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="6cebe-142">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="6cebe-142">Update data</span></span>
<span data-ttu-id="6cebe-143">A seguir use Olá código tooconnect e ler Olá dados usando um **atualização** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-143">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="6cebe-144">Olá [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto é toointerface usado com o servidor do hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-144">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="6cebe-145">Olá [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) função é servidor de toohello tooestablish usado Olá conexão.</span><span class="sxs-lookup"><span data-stu-id="6cebe-145">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="6cebe-146">Olá [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) função é a consulta SQL Olá tooexecute usado no banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-146">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="6cebe-147">Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.</span><span class="sxs-lookup"><span data-stu-id="6cebe-147">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="delete-data"></a><span data-ttu-id="6cebe-148">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="6cebe-148">Delete data</span></span>
<span data-ttu-id="6cebe-149">A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-149">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="6cebe-150">Olá [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto é toointerface usado com o servidor do hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-150">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="6cebe-151">Olá [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) função é servidor de toohello tooestablish usado Olá conexão.</span><span class="sxs-lookup"><span data-stu-id="6cebe-151">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="6cebe-152">Olá [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) função é a consulta SQL Olá tooexecute usado no banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="6cebe-152">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="6cebe-153">Substitua os valores hello que você especificou quando criou o banco de dados e servidor de saudação host hello, dbname, usuário e parâmetros de senha.</span><span class="sxs-lookup"><span data-stu-id="6cebe-153">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="6cebe-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6cebe-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6cebe-155">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="6cebe-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
