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
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="25bc4-103">Banco de dados do Azure para MySQL: Use Node. js tooconnect e consultar dados</span><span class="sxs-lookup"><span data-stu-id="25bc4-103">Azure Database for MySQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="25bc4-104">Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para usar o MySQL [Node.js](https://nodejs.org/) de plataformas Mac, Ubuntu Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="25bc4-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="25bc4-105">Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="25bc4-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="25bc4-106">Olá etapas neste artigo presumem que você esteja familiarizado com o desenvolvimento usando o Node. js, e que você é novo tooworking com o banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="25bc4-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25bc4-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="25bc4-107">Prerequisites</span></span>
<span data-ttu-id="25bc4-108">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="25bc4-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="25bc4-109">Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="25bc4-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="25bc4-110">Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="25bc4-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="25bc4-111">Você também precisará:</span><span class="sxs-lookup"><span data-stu-id="25bc4-111">You also need to:</span></span>
- <span data-ttu-id="25bc4-112">Instalar Olá [Node.js](https://nodejs.org) tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="25bc4-112">Install hello [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="25bc4-113">Instalar [mysql2](https://www.npmjs.com/package/mysql2) tooMySQL tooconnect de saudação aplicativo Node. js do pacote.</span><span class="sxs-lookup"><span data-stu-id="25bc4-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package tooconnect tooMySQL from hello Node.js application.</span></span> 

## <a name="install-nodejs-and-hello-mysql-connector"></a><span data-ttu-id="25bc4-114">Instalar o Node. js e Olá conector MySQL</span><span class="sxs-lookup"><span data-stu-id="25bc4-114">Install Node.js and hello MySQL connector</span></span>
<span data-ttu-id="25bc4-115">Dependendo de sua plataforma, siga Olá instruções apropriadas tooinstall Node. js.</span><span class="sxs-lookup"><span data-stu-id="25bc4-115">Depending on your platform, follow hello appropriate instructions tooinstall Node.js.</span></span> <span data-ttu-id="25bc4-116">Use npm tooinstall Olá mysql2 pacote e suas dependências em sua pasta de projeto.</span><span class="sxs-lookup"><span data-stu-id="25bc4-116">Use npm tooinstall hello mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="25bc4-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="25bc4-117">**Windows**</span></span>
1. <span data-ttu-id="25bc4-118">Visite Olá [página de downloads do Node. js](https://nodejs.org/en/download/) e selecione a opção de instalador desejada do Windows.</span><span class="sxs-lookup"><span data-stu-id="25bc4-118">Visit hello [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="25bc4-119">Crie uma pasta de projeto local, como `nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="25bc4-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="25bc4-120">Inicie o prompt de comando hello e cd na pasta de projeto Olá, como`cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="25bc4-120">Launch hello command prompt and cd into hello project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="25bc4-121">Execute biblioteca do hello NPM ferramenta tooinstall Olá mysql2 na pasta de projeto hello.</span><span class="sxs-lookup"><span data-stu-id="25bc4-121">Run hello NPM tool tooinstall hello mysql2 library into hello project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="25bc4-122">Verificar a instalação de saudação verificando Olá `npm list` de saída de texto para `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="25bc4-122">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="25bc4-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="25bc4-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="25bc4-124">A seguir Olá execução comandos tooinstall **Node.js** e **npm** Gerenciador de pacotes de saudação para Node. js.</span><span class="sxs-lookup"><span data-stu-id="25bc4-124">Run hello following commands tooinstall **Node.js** and **npm** hello package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="25bc4-125">Executar Olá toomake comandos a seguir em uma pasta de projeto `mysqlnodejs` e instale o pacote de mysql2 de saudação para essa pasta.</span><span class="sxs-lookup"><span data-stu-id="25bc4-125">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="25bc4-126">Verificar a instalação de saudação marcando texto de saída da lista npm `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="25bc4-126">Verify hello installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="25bc4-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="25bc4-127">**Mac OS**</span></span>
1. <span data-ttu-id="25bc4-128">Digite hello tooinstall comandos a seguir **brew**, um Gerenciador de pacotes de fácil de usar para Mac OS X e **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="25bc4-128">Enter hello following commands tooinstall **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="25bc4-129">Executar Olá toomake comandos a seguir em uma pasta de projeto `mysqlnodejs` e instale o pacote de mysql2 de saudação para essa pasta.</span><span class="sxs-lookup"><span data-stu-id="25bc4-129">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="25bc4-130">Verificar a instalação de saudação verificando Olá `npm list` de saída de texto para `mysql2@1.3.6`.</span><span class="sxs-lookup"><span data-stu-id="25bc4-130">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="25bc4-131">número de versão Hello pode variar conforme novos patches são liberados.</span><span class="sxs-lookup"><span data-stu-id="25bc4-131">hello version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="25bc4-132">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="25bc4-132">Get connection information</span></span>
<span data-ttu-id="25bc4-133">Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="25bc4-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="25bc4-134">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="25bc4-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="25bc4-135">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="25bc4-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="25bc4-136">No painel esquerdo do hello, clique em **todos os recursos**e em seguida, procure o servidor Olá que você criou (por exemplo, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="25bc4-136">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="25bc4-137">Clique em nome do servidor de saudação **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="25bc4-137">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="25bc4-138">Servidor de saudação selecione **propriedades** página.</span><span class="sxs-lookup"><span data-stu-id="25bc4-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="25bc4-139">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="25bc4-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="25bc4-140">![Banco de Dados do Azure para MySQL – Logon de administrador do servidor](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="25bc4-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="25bc4-141">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="25bc4-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="25bc4-142">Executando o código JavaScript Olá no Node. js</span><span class="sxs-lookup"><span data-stu-id="25bc4-142">Running hello JavaScript code in Node.js</span></span>
1. <span data-ttu-id="25bc4-143">Cole o código JavaScript Olá para arquivos de texto e salve em uma pasta de projeto com. js da extensão de arquivo, como C:\nodejsmysql\createtable.js ou /home/username/nodejsmysql/createtable.js</span><span class="sxs-lookup"><span data-stu-id="25bc4-143">Paste hello JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="25bc4-144">Inicie o prompt de comando hello ou bash shell.</span><span class="sxs-lookup"><span data-stu-id="25bc4-144">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="25bc4-145">Altere o diretório para a pasta do projeto `cd nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="25bc4-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="25bc4-146">aplicativo de hello toorun, digite Olá nó comando seguido pelo nome de arquivo hello, como `node createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="25bc4-146">toorun hello application, type hello node command followed by hello file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="25bc4-147">No Windows, se o aplicativo de nó hello não está em seu caminho de variável de ambiente, talvez seja necessário aplicativo toouse hello caminho completo toolaunch Olá nó, como`"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="25bc4-147">On Windows, if hello node application is not in your environment variable path, you may need toouse hello full path toolaunch hello node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="25bc4-148">Conectar-se, criar tabela e inserir dados</span><span class="sxs-lookup"><span data-stu-id="25bc4-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="25bc4-149">A seguir use Olá tooconnect de código e carregar Olá dados usando **CREATE TABLE** e **INSERT INTO** instruções SQL.</span><span class="sxs-lookup"><span data-stu-id="25bc4-149">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="25bc4-150">Olá [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método é toointerface usado com o servidor MySQL de saudação.</span><span class="sxs-lookup"><span data-stu-id="25bc4-150">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="25bc4-151">Olá [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) função é servidor de toohello tooestablish usado Olá conexão.</span><span class="sxs-lookup"><span data-stu-id="25bc4-151">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="25bc4-152">Olá [Query ()](https://github.com/mysqljs/mysql#performing-queries) função é a consulta SQL Olá tooexecute usado no banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="25bc4-152">hello [query()](https://github.com/mysqljs/mysql#performing-queries) function is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="25bc4-153">Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="25bc4-153">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="25bc4-154">Ler dados</span><span class="sxs-lookup"><span data-stu-id="25bc4-154">Read data</span></span>
<span data-ttu-id="25bc4-155">A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="25bc4-155">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="25bc4-156">Olá [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método é toointerface usado com o servidor MySQL de saudação.</span><span class="sxs-lookup"><span data-stu-id="25bc4-156">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="25bc4-157">Olá [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) método é servidor de toohello tooestablish usado Olá conexão.</span><span class="sxs-lookup"><span data-stu-id="25bc4-157">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="25bc4-158">Olá [Query ()](https://github.com/mysqljs/mysql#performing-queries) método é a consulta SQL Olá tooexecute usado no banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="25bc4-158">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> <span data-ttu-id="25bc4-159">matriz de resultados de saudação é toohold usado Olá resultados de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="25bc4-159">hello results array is used toohold hello results of hello query.</span></span>

<span data-ttu-id="25bc4-160">Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="25bc4-160">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="25bc4-161">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="25bc4-161">Update data</span></span>
<span data-ttu-id="25bc4-162">A seguir use Olá código tooconnect e ler Olá dados usando um **atualização** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="25bc4-162">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="25bc4-163">Olá [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método é toointerface usado com o servidor MySQL de saudação.</span><span class="sxs-lookup"><span data-stu-id="25bc4-163">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="25bc4-164">Olá [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) método é servidor de toohello tooestablish usado Olá conexão.</span><span class="sxs-lookup"><span data-stu-id="25bc4-164">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="25bc4-165">Olá [Query ()](https://github.com/mysqljs/mysql#performing-queries) método é a consulta SQL Olá tooexecute usado no banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="25bc4-165">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="25bc4-166">Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="25bc4-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="25bc4-167">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="25bc4-167">Delete data</span></span>
<span data-ttu-id="25bc4-168">A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="25bc4-168">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="25bc4-169">Olá [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método é toointerface usado com o servidor MySQL de saudação.</span><span class="sxs-lookup"><span data-stu-id="25bc4-169">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="25bc4-170">Olá [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) método é servidor de toohello tooestablish usado Olá conexão.</span><span class="sxs-lookup"><span data-stu-id="25bc4-170">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="25bc4-171">Olá [Query ()](https://github.com/mysqljs/mysql#performing-queries) método é a consulta SQL Olá tooexecute usado no banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="25bc4-171">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="25bc4-172">Substituir saudação `host`, `user`, `password`, e `database` parâmetros com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="25bc4-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="25bc4-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="25bc4-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="25bc4-174">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="25bc4-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
