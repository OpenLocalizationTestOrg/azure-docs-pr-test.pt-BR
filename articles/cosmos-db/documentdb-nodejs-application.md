---
title: Compilar um aplicativo Web do Node.js para o banco de dados do Azure Cosmos DB | Microsoft Docs
description: Este tutorial do Node.js explora como usar o Microsoft Azure Cosmos DB para armazenar e acessar dados de um aplicativo Web do Node.js Express hospedado em sites do Azure.
keywords: Desenvolvimento de aplicativos, tutorial de banco de dados, aprender node.js, tutorial do node.js
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 1a98509a98bcd2a5de593eb006f905766fe72966
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="e0601-104"><a name="_Toc395783175"></a>Compilar um aplicativo Web Node.js usando o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e0601-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0601-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e0601-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="e0601-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="e0601-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="e0601-107">Java</span><span class="sxs-lookup"><span data-stu-id="e0601-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="e0601-108">Python</span><span class="sxs-lookup"><span data-stu-id="e0601-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="e0601-109">Este tutorial do Node.js mostra como usar o Azure Cosmos DB e a API do DocumentDB para armazenar e acessar dados de um aplicativo Express do Node.js hospedado nos Sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0601-109">This Node.js tutorial shows you how to use Azure Cosmos DB and the DocumentDB API to store and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="e0601-110">Você cria um aplicativo simples de gerenciamento de tarefas baseado na Web, um aplicativo ToDo, que permite criar, recuperar e concluir tarefas.</span><span class="sxs-lookup"><span data-stu-id="e0601-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="e0601-111">As tarefas são armazenadas como documentos JSON no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e0601-111">The tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="e0601-112">Este tutorial o orienta durante a criação e a implantação do aplicativo e explica o que está acontecendo em cada trecho de código.</span><span class="sxs-lookup"><span data-stu-id="e0601-112">This tutorial walks you through the creation and deployment of the app and explains what's happening in each snippet.</span></span>

![Captura de tela do aplicativo Minha lista de tarefas pendentes criado neste tutorial](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="e0601-114">Não há tempo para concluir o tutorial e deseja apenas a solução completa?</span><span class="sxs-lookup"><span data-stu-id="e0601-114">Don't have time to complete the tutorial and just want to get the complete solution?</span></span> <span data-ttu-id="e0601-115">Não é um problema, você pode obter a solução de exemplo completo da [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="e0601-115">Not a problem, you can get the complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="e0601-116">Leia o arquivo [Leiame](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) para obter instruções sobre como executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0601-116">Just read the [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how to run the app.</span></span>

## <span data-ttu-id="e0601-117"><a name="_Toc395783176"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e0601-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="e0601-118">Este tutorial do Node.js presume que você tenha alguma experiência anterior com o Node.js e sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0601-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="e0601-119">Antes de seguir as instruções deste artigo, verifique se você possui o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e0601-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="e0601-120">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0601-120">An active Azure account.</span></span> <span data-ttu-id="e0601-121">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="e0601-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e0601-122">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e0601-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="e0601-123">OU</span><span class="sxs-lookup"><span data-stu-id="e0601-123">OR</span></span>

   <span data-ttu-id="e0601-124">Uma instalação local do [Emulador do Azure Cosmos DB](local-emulator.md) (Somente no Windows).</span><span class="sxs-lookup"><span data-stu-id="e0601-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="e0601-125">[Node.js][Node.js] versão v0.10.29 ou superior.</span><span class="sxs-lookup"><span data-stu-id="e0601-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="e0601-126">[Gerador expresso](http://www.expressjs.com/starter/generator.html) (você pode instalá-lo por meio de `npm install express-generator -g`)</span><span class="sxs-lookup"><span data-stu-id="e0601-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="e0601-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="e0601-127">[Git][Git].</span></span>

## <span data-ttu-id="e0601-128"><a name="_Toc395637761"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e0601-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="e0601-129">Vamos começar criando uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e0601-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="e0601-130">Se você já tiver uma conta ou se estiver usando o Emulador do Azure Cosmos DB para este tutorial, pule para a [Etapa 2: criar um novo aplicativo do Node.js](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="e0601-130">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="e0601-131"><a name="_Toc395783178"></a>Etapa 2: criar um novo aplicativo do Node.js</span><span class="sxs-lookup"><span data-stu-id="e0601-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="e0601-132">Agora vamos aprender a criar um projeto Hello World Node.js básico usando a estrutura [Express](http://expressjs.com/) .</span><span class="sxs-lookup"><span data-stu-id="e0601-132">Now let's learn to create a basic Hello World Node.js project using the [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="e0601-133">Abra seu terminal favorito, como o prompt de comando do Node.js.</span><span class="sxs-lookup"><span data-stu-id="e0601-133">Open your favorite terminal, such as the Node.js command prompt.</span></span>
2. <span data-ttu-id="e0601-134">Navegue até o diretório no qual você deseja armazenar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0601-134">Navigate to the directory in which you'd like to store the new application.</span></span>
3. <span data-ttu-id="e0601-135">Use o gerador expresso para gerar um novo aplicativo chamado **tarefas**.</span><span class="sxs-lookup"><span data-stu-id="e0601-135">Use the express generator to generate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="e0601-136">Abra o novo diretório **tarefas** e instale as dependências.</span><span class="sxs-lookup"><span data-stu-id="e0601-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="e0601-137">Execute seu novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0601-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="e0601-138">Veja seu novo aplicativo navegando em seu navegador até [http://localhost:3000/](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="e0601-138">You can view your new application by navigating your browser to [http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Saiba mais sobre o Node.js — captura de tela do aplicativo Hello World em uma janela do navegador](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="e0601-140">Em seguida, para interromper o aplicativo, pressione CTRL+C na janela do terminal e clique em **y** para finalizar o trabalho em lotes.</span><span class="sxs-lookup"><span data-stu-id="e0601-140">Then, to stop the application, press CTRL+C in the terminal window and then click **y** to terminate the batch job.</span></span>

## <span data-ttu-id="e0601-141"><a name="_Toc395783179"></a>Etapa 3: Instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="e0601-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="e0601-142">O arquivo **package.json** é um dos arquivos criados na raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="e0601-142">The **package.json** file is one of the files created in the root of the project.</span></span> <span data-ttu-id="e0601-143">Esse arquivo contém uma lista dos módulos adicionais que são necessários para seu aplicativo do Node.js.</span><span class="sxs-lookup"><span data-stu-id="e0601-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="e0601-144">Posteriormente, ao implantar esse aplicativo em sites do Azure, esse arquivo será usado para determinar quais módulos precisam ser instalados no Azure para dar suporte ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0601-144">Later, when you deploy this application to Azure Websites, this file is used to determine which modules need to be installed on Azure to support your application.</span></span> <span data-ttu-id="e0601-145">Ainda precisamos instalar mais dois pacotes para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e0601-145">We still need to install two more packages for this tutorial.</span></span>

1. <span data-ttu-id="e0601-146">De volta ao terminal, instale o módulo **async** via npm.</span><span class="sxs-lookup"><span data-stu-id="e0601-146">Back in the terminal, install the **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="e0601-147">Instale o módulo **documentdb** via npm.</span><span class="sxs-lookup"><span data-stu-id="e0601-147">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="e0601-148">Este é o módulo em que toda a mágica do Azure Cosmos DB acontece.</span><span class="sxs-lookup"><span data-stu-id="e0601-148">This is the module where all the Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="e0601-149">Uma verificação rápida do arquivo **package.json** do aplicativo deve mostrar os módulos adicionais.</span><span class="sxs-lookup"><span data-stu-id="e0601-149">A quick check of the **package.json** file of the application should show the additional modules.</span></span> <span data-ttu-id="e0601-150">Esse arquivo informará ao Azure quais pacotes para baixar e instalar ao executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0601-150">This file will tell Azure which packages to download and install when running your application.</span></span> <span data-ttu-id="e0601-151">Ele deve se parecer com o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="e0601-151">It should resemble the example below.</span></span>
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    <span data-ttu-id="e0601-152">Isso informa ao Nó (e ao Azure mais tarde) que seu aplicativo depende desses módulos adicionais.</span><span class="sxs-lookup"><span data-stu-id="e0601-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="e0601-153"><a name="_Toc395783180"></a>Etapa 4: Usar o serviço do Azure Cosmos DB em um aplicativo de nó</span><span class="sxs-lookup"><span data-stu-id="e0601-153"><a name="_Toc395783180"></a>Step 4: Using the Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="e0601-154">Isso cuida de toda a instalação e configuração inicial. Agora vamos ao motivo de estarmos aqui, ou seja, para gravar algum código usando o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e0601-154">That takes care of all the initial setup and configuration, now let’s get down to why we’re here, and that’s to write some code using Azure Cosmos DB.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="e0601-155">Criar o modelo</span><span class="sxs-lookup"><span data-stu-id="e0601-155">Create the model</span></span>
1. <span data-ttu-id="e0601-156">No diretório do projeto, crie um novo diretório chamado **modelos** no mesmo diretório que o arquivo package.json.</span><span class="sxs-lookup"><span data-stu-id="e0601-156">In the project directory, create a new directory named **models** in the same directory as the package.json file.</span></span>
2. <span data-ttu-id="e0601-157">No diretório **models**, criar um novo arquivo chamado **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="e0601-157">In the **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="e0601-158">Esse arquivo conterá o modelo para as tarefas criadas pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0601-158">This file will contain the model for the tasks created by our application.</span></span>
3. <span data-ttu-id="e0601-159">No mesmo diretório **models**, crie um novo arquivo chamado **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="e0601-159">In the same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="e0601-160">Esse arquivo conterá algum código útil e reutilizável, que será usado em todo o nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0601-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="e0601-161">Copie o seguinte código para **docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="e0601-161">Copy the following code in to **docdbUtils.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. <span data-ttu-id="e0601-162">Salve e feche o arquivo **docdbUtils.js** .</span><span class="sxs-lookup"><span data-stu-id="e0601-162">Save and close the **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="e0601-163">No início do arquivo **taskDao.js**, adicione o seguinte código para fazer referência a **DocumentDBClient** e **docdbUtils.js** criados anteriormente:</span><span class="sxs-lookup"><span data-stu-id="e0601-163">At the beginning of the **taskDao.js** file, add the following code to reference the **DocumentDBClient** and the **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="e0601-164">Em seguida, você adicionará o código para definir e exportar o objeto da tarefa.</span><span class="sxs-lookup"><span data-stu-id="e0601-164">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="e0601-165">Ele é responsável pela inicialização do nosso objeto de Tarefa e por configurar o Banco de Dados e o Conjunto de Documentos que usaremos.</span><span class="sxs-lookup"><span data-stu-id="e0601-165">This is responsible for initializing our Task object and setting up the Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="e0601-166">Em seguida, adicione o seguinte código para definir métodos adicionais no objeto da Tarefa, que permitem interações com os dados armazenados no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e0601-166">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. <span data-ttu-id="e0601-167">Salve e feche o arquivo **taskDao.js** .</span><span class="sxs-lookup"><span data-stu-id="e0601-167">Save and close the **taskDao.js** file.</span></span> 

### <a name="create-the-controller"></a><span data-ttu-id="e0601-168">Criar o controlador</span><span class="sxs-lookup"><span data-stu-id="e0601-168">Create the controller</span></span>
1. <span data-ttu-id="e0601-169">No diretório **rotas** do projeto, crie um novo arquivo chamado **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="e0601-169">In the **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="e0601-170">Adicione os seguintes códigos ao **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="e0601-170">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="e0601-171">Ele carrega os módulos DocumentDBClient e assíncrono, que são usados pelo **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="e0601-171">This loads the DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="e0601-172">Isso também definiu a função de **TaskList**, que é transmitida a uma instância do objeto **Task** definido anteriormente:</span><span class="sxs-lookup"><span data-stu-id="e0601-172">This also defined the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="e0601-173">Continue adicionando ao arquivo **tasklist.js**, adicionando os métodos usados para **showTasks, addTask** e **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="e0601-173">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks, addTask**, and **completeTasks**:</span></span>
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. <span data-ttu-id="e0601-174">Salve e feche o arquivo **tasklist.js** .</span><span class="sxs-lookup"><span data-stu-id="e0601-174">Save and close the **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="e0601-175">Adicionar config.js</span><span class="sxs-lookup"><span data-stu-id="e0601-175">Add config.js</span></span>
1. <span data-ttu-id="e0601-176">No diretório do projeto, crie um novo arquivo chamado **config.js**.</span><span class="sxs-lookup"><span data-stu-id="e0601-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="e0601-177">Adicione o seguinte ao **config.js**.</span><span class="sxs-lookup"><span data-stu-id="e0601-177">Add the following to **config.js**.</span></span> <span data-ttu-id="e0601-178">Isso define as configurações e valores necessários para nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0601-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[the URI value from the Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[the PRIMARY KEY value from the Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="e0601-179">No arquivo **config.js**, atualize os valores de HOST e de AUTH_KEY usando os valores encontrados na folha Chaves de sua conta do Azure Cosmos DB no [Portal do Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e0601-179">In the **config.js** file, update the values of HOST and AUTH_KEY using the values found in the Keys blade of your Azure Cosmos DB account on the [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="e0601-180">Salve e feche o arquivo **config.js** .</span><span class="sxs-lookup"><span data-stu-id="e0601-180">Save and close the **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="e0601-181">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="e0601-181">Modify app.js</span></span>
1. <span data-ttu-id="e0601-182">No diretório do projeto, abra o arquivo **app.js** .</span><span class="sxs-lookup"><span data-stu-id="e0601-182">In the project directory, open the **app.js** file.</span></span> <span data-ttu-id="e0601-183">Esse arquivo foi criado anteriormente, quando o aplicativo Web Express foi criado.</span><span class="sxs-lookup"><span data-stu-id="e0601-183">This file was created earlier when the Express web application was created.</span></span>
2. <span data-ttu-id="e0601-184">Adicione o seguinte código à parte superior do **app.js**</span><span class="sxs-lookup"><span data-stu-id="e0601-184">Add the following code to the top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="e0601-185">Esse código define o arquivo de configuração a ser usado e continua a ler valores desse arquivo em algumas variáveis que usaremos em breve.</span><span class="sxs-lookup"><span data-stu-id="e0601-185">This code defines the config file to be used, and proceeds to read values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="e0601-186">Substitua as duas linhas seguintes no arquivo **app.js** :</span><span class="sxs-lookup"><span data-stu-id="e0601-186">Replace the following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="e0601-187">pelo trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0601-187">with the following snippet:</span></span>
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. <span data-ttu-id="e0601-188">Essas linhas definem uma nova instância do nosso objeto **TaskDao**, com uma nova conexão ao Azure Cosmos DB (usando os valores lidos a partir de **config.js**), inicialize o objeto de tarefa e associe ações do formulário aos métodos no nosso controlador **TaskList**.</span><span class="sxs-lookup"><span data-stu-id="e0601-188">These lines define a new instance of our **TaskDao** object, with a new connection to Azure Cosmos DB (using the values read from the **config.js**), initialize the task object and then bind form actions to methods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="e0601-189">Por fim, salve e feche o arquivo **app.js** ; está praticamente pronto.</span><span class="sxs-lookup"><span data-stu-id="e0601-189">Finally, save and close the **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="e0601-190"><a name="_Toc395783181"></a>Etapa 5: Criar uma interface do usuário</span><span class="sxs-lookup"><span data-stu-id="e0601-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="e0601-191">Agora vamos voltar a atenção para criar a interface do usuário, desse modo, um usuário pode realmente interagir com nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0601-191">Now let’s turn our attention to building the user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="e0601-192">O aplicativo Express que criamos usa **Jade** como mecanismo de exibição.</span><span class="sxs-lookup"><span data-stu-id="e0601-192">The Express application we created uses **Jade** as the view engine.</span></span> <span data-ttu-id="e0601-193">Para obter mais informações sobre o Jade, consulte [http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="e0601-193">For more information on Jade please refer to [http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="e0601-194">O arquivo **layout.jade** no diretório **views** é usado como um modelo global para outros arquivos **.jade**.</span><span class="sxs-lookup"><span data-stu-id="e0601-194">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="e0601-195">Nesta etapa, você o modificará para usar a [Twitter Bootstrap](https://github.com/twbs/bootstrap), que é um kit de ferramentas que facilita a criação de um site com uma aparência interessante.</span><span class="sxs-lookup"><span data-stu-id="e0601-195">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span> 
2. <span data-ttu-id="e0601-196">Abra o arquivo **layout.jade** encontrado na pasta **views** e substitua o conteúdo pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="e0601-196">Open the **layout.jade** file found in the **views** folder and replace the contents with the following:</span></span>

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    <span data-ttu-id="e0601-197">Isso instrui o mecanismo **Jade** a renderizar um HTML para nosso aplicativo e cria um **bloco** chamado **content**, em que podemos fornecer o layout para nossas páginas de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="e0601-197">This effectively tells the **Jade** engine to render some HTML for our application and creates a **block** called **content** where we can supply the layout for our content pages.</span></span>

    <span data-ttu-id="e0601-198">Salve e feche o arquivo **layout.jade** .</span><span class="sxs-lookup"><span data-stu-id="e0601-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="e0601-199">Agora, abra o arquivo **index.jade** , o modo de exibição que será usado pelo nosso aplicativo, e substitua o conteúdo do arquivo pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="e0601-199">Now open the **index.jade** file, the view that will be used by our application, and replace the content of the file with the following:</span></span>
   
        extends layout
        block content
           h1 #{title}
           br
        
           form(action="/completetask", method="post")
             table.table.table-striped.table-bordered
               tr
                 td Name
                 td Category
                 td Date
                 td Complete
               if (typeof tasks === "undefined")
                 tr
                   td
               else
                 each task in tasks
                   tr
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

<span data-ttu-id="e0601-200">Isso estende o layout e fornece conteúdo para o espaço reservado **content** que vimos no arquivo **layout.jade** anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e0601-200">This extends layout, and provides content for the **content** placeholder we saw in the **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="e0601-201">Nesse layout criamos dois formulários HTML.</span><span class="sxs-lookup"><span data-stu-id="e0601-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="e0601-202">O primeiro formulário contém uma tabela para nossos dados e um botão que permite atualizar itens pelo lançamento do método **/completetask** de nosso controlador.</span><span class="sxs-lookup"><span data-stu-id="e0601-202">The first form contains a table for our data and a button that allows us to update items by posting to **/completetask** method of our controller.</span></span>
    
<span data-ttu-id="e0601-203">O segundo formulário contém dois campos de entrada e um botão que nos permite criar um novo item ao ser lançado o método **/addtask** do nosso controlador.</span><span class="sxs-lookup"><span data-stu-id="e0601-203">The second form contains two input fields and a button that allows us to create a new item by posting to **/addtask** method of our controller.</span></span>

<span data-ttu-id="e0601-204">Isso deve ser tudo o que precisamos para que nosso aplicativo funcione.</span><span class="sxs-lookup"><span data-stu-id="e0601-204">This should be all that we need for our application to work.</span></span>

## <span data-ttu-id="e0601-205"><a name="_Toc395783181"></a>Etapa 6: Execute o seu aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="e0601-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="e0601-206">Para testar o aplicativo no computador local, execute `npm start` no terminal para iniciar o aplicativo e atualize a página do navegador [http://localhost:3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="e0601-206">To test the application on your local machine, run `npm start` in the terminal to start your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="e0601-207">Agora a página deve ser semelhante à seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="e0601-207">The page should now look like the image below:</span></span>
   
    ![Captura de tela do aplicativo MyTodo List em uma janela do navegador](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="e0601-209">Se receber um erro sobre o recuo no arquivo layout.jade ou o arquivo index.jade, verifique se as duas primeiras linhas em ambos os arquivos estão justificadas à esquerda, sem espaços.</span><span class="sxs-lookup"><span data-stu-id="e0601-209">If you receive an error about the indent in the layout.jade file or the index.jade file, ensure that the first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="e0601-210">Se houver espaços antes das duas primeiras linhas, remova-os, salve os dois arquivos e atualize a janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="e0601-210">If there are spaces before the first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="e0601-211">Use os campos Item, Nome do Item e Categoria para inserir uma nova tarefa e clique em **Adicionar Item**.</span><span class="sxs-lookup"><span data-stu-id="e0601-211">Use the Item, Item Name and Category fields to enter a new task and then click **Add Item**.</span></span> <span data-ttu-id="e0601-212">Isso cria um documento no Azure Cosmos DB com essas propriedades.</span><span class="sxs-lookup"><span data-stu-id="e0601-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="e0601-213">A página deverá ser atualizada para exibir o item recém-criado na lista de Tarefas Pendentes.</span><span class="sxs-lookup"><span data-stu-id="e0601-213">The page should update to display the newly created item in the ToDo list.</span></span>
   
    ![Captura de tela do aplicativo com um novo item na lista de Tarefas pendentes](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="e0601-215">Para concluir uma tarefa, basta marcar a caixa de seleção na coluna Concluir e clicar em **Atualizar tarefas**.</span><span class="sxs-lookup"><span data-stu-id="e0601-215">To complete a task, simply check the checkbox in the Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="e0601-216">Isso atualiza o documento que você já criou.</span><span class="sxs-lookup"><span data-stu-id="e0601-216">This updates the document you already created.</span></span>

5. <span data-ttu-id="e0601-217">Para interromper o aplicativo, pressione CTRL+C na janela do terminal e clique em **Y** para finalizar o trabalho em lotes.</span><span class="sxs-lookup"><span data-stu-id="e0601-217">To stop the application, press CTRL+C in the terminal window and then click **Y** to terminate the batch job.</span></span>

## <span data-ttu-id="e0601-218"><a name="_Toc395783182"></a>Etapa 7: implantar seu projeto de desenvolvimento de aplicativo nos sites do Azure</span><span class="sxs-lookup"><span data-stu-id="e0601-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project to Azure Websites</span></span>
1. <span data-ttu-id="e0601-219">Se ainda não o fez, habilite um repositório git do seu site do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0601-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="e0601-220">Encontre instruções sobre como fazer isso no tópico [Implantação GIT Local no Serviço de Aplicativo do Azure](../app-service-web/app-service-deploy-local-git.md) .</span><span class="sxs-lookup"><span data-stu-id="e0601-220">You can find instructions on how to do this in the [Local Git Deployment to Azure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="e0601-221">Adicione seu site do Azure como um git remoto.</span><span class="sxs-lookup"><span data-stu-id="e0601-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="e0601-222">Implante o envio por push para o computador remoto.</span><span class="sxs-lookup"><span data-stu-id="e0601-222">Deploy by pushing to the remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="e0601-223">Em poucos segundos, o git terminará de publicar seu aplicativo Web e iniciará um navegador onde você poderá ver seu trabalho sendo executado no Azure!</span><span class="sxs-lookup"><span data-stu-id="e0601-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="e0601-224">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="e0601-224">Congratulations!</span></span> <span data-ttu-id="e0601-225">Você acabou de criar seu primeiro Aplicativo Web Express do Node.js usando o Azure Cosmos DB e o publicou nos sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0601-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it to Azure Websites.</span></span>

    <span data-ttu-id="e0601-226">Se você quiser baixar ou consultar o aplicativo de referência completa para este tutorial, ele pode ser baixado do [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="e0601-226">If you want to download or refer to the complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="e0601-227"><a name="_Toc395637775"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0601-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="e0601-228">Quer executar testes de desempenho e escala com o Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="e0601-228">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="e0601-229">Confira [teste de desempenho e escalabilidade com o Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="e0601-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="e0601-230">Saiba como [monitorar uma conta do Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="e0601-230">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="e0601-231">Executar consultas em nosso conjunto de dados de exemplo no [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="e0601-231">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="e0601-232">Explore a [Documentação do Azure Cosmos DB](https://docs.microsoft.com/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="e0601-232">Explore the [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

