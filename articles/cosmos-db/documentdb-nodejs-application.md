---
title: aaaBuild um aplicativo da web Node. js para o banco de dados do Azure Cosmos | Microsoft Docs
description: Este tutorial Node. js explora como toouse banco de dados do Microsoft Azure Cosmos toostore e acessar dados de um aplicativo da web Express Node. js hospedado em sites do Azure.
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
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="ed5c7-104"><a name="_Toc395783175"></a>Compilar um aplicativo Web Node.js usando o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ed5c7-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed5c7-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ed5c7-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="ed5c7-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="ed5c7-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="ed5c7-107">Java</span><span class="sxs-lookup"><span data-stu-id="ed5c7-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="ed5c7-108">Python</span><span class="sxs-lookup"><span data-stu-id="ed5c7-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="ed5c7-109">Este tutorial Node. js mostra como toouse o banco de dados do Azure Cosmos e hello toostore e acessar dados de um aplicativo Node. js Express API DocumentDB hospedados nos sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-109">This Node.js tutorial shows you how toouse Azure Cosmos DB and hello DocumentDB API toostore and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="ed5c7-110">Você cria um aplicativo simples de gerenciamento de tarefas baseado na Web, um aplicativo ToDo, que permite criar, recuperar e concluir tarefas.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="ed5c7-111">tarefas de saudação são armazenadas como documentos JSON no banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-111">hello tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="ed5c7-112">Este tutorial orienta você durante a criação de saudação e implantação do aplicativo hello e explica o que está acontecendo em cada trecho de código.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-112">This tutorial walks you through hello creation and deployment of hello app and explains what's happening in each snippet.</span></span>

![Captura de tela de saudação aplicativo minha lista de tarefas criada neste tutorial Node. js](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="ed5c7-114">Não ter tempo toocomplete Olá tutorial e deseja apenas solução completa de saudação tooget?</span><span class="sxs-lookup"><span data-stu-id="ed5c7-114">Don't have time toocomplete hello tutorial and just want tooget hello complete solution?</span></span> <span data-ttu-id="ed5c7-115">Não é um problema, você pode obter a solução de exemplo completo de saudação do [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="ed5c7-115">Not a problem, you can get hello complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="ed5c7-116">Apenas ler Olá [Leiame](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) arquivo para obter instruções sobre como toorun Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-116">Just read hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how toorun hello app.</span></span>

## <span data-ttu-id="ed5c7-117"><a name="_Toc395783176"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ed5c7-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="ed5c7-118">Este tutorial do Node.js presume que você tenha alguma experiência anterior com o Node.js e sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="ed5c7-119">Antes de seguir as instruções neste artigo hello, você deve garantir que você tenha a seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="ed5c7-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="ed5c7-120">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-120">An active Azure account.</span></span> <span data-ttu-id="ed5c7-121">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ed5c7-122">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ed5c7-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="ed5c7-123">OU</span><span class="sxs-lookup"><span data-stu-id="ed5c7-123">OR</span></span>

   <span data-ttu-id="ed5c7-124">Uma instalação local do hello [emulador de banco de dados do Azure Cosmos](local-emulator.md) (somente Windows).</span><span class="sxs-lookup"><span data-stu-id="ed5c7-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="ed5c7-125">[Node.js][Node.js] versão v0.10.29 ou superior.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="ed5c7-126">[Gerador expresso](http://www.expressjs.com/starter/generator.html) (você pode instalá-lo por meio de `npm install express-generator -g`)</span><span class="sxs-lookup"><span data-stu-id="ed5c7-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="ed5c7-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="ed5c7-127">[Git][Git].</span></span>

## <span data-ttu-id="ed5c7-128"><a name="_Toc395637761"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ed5c7-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="ed5c7-129">Vamos começar criando uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="ed5c7-130">Se você já tiver uma conta ou se você estiver usando hello Azure Cosmos DB emulador para este tutorial, você poderá ignorar muito[etapa 2: criar um novo aplicativo Node. js](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="ed5c7-130">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="ed5c7-131"><a name="_Toc395783178"></a>Etapa 2: criar um novo aplicativo do Node.js</span><span class="sxs-lookup"><span data-stu-id="ed5c7-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="ed5c7-132">Agora vamos aprender toocreate um projeto de Hello World Node básico usando Olá [Express](http://expressjs.com/) framework.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-132">Now let's learn toocreate a basic Hello World Node.js project using hello [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="ed5c7-133">Abra seu terminal favorito, como o prompt de comando do hello Node. js.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-133">Open your favorite terminal, such as hello Node.js command prompt.</span></span>
2. <span data-ttu-id="ed5c7-134">Navegue toohello diretório em que você gostaria que o novo aplicativo de saudação toostore.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-134">Navigate toohello directory in which you'd like toostore hello new application.</span></span>
3. <span data-ttu-id="ed5c7-135">Use Olá gerador express toogenerate um novo aplicativo chamado **todo**.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-135">Use hello express generator toogenerate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="ed5c7-136">Abra o novo diretório **tarefas** e instale as dependências.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="ed5c7-137">Execute seu novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="ed5c7-138">Você pode exibir o novo aplicativo navegando seu navegador muito[http://localhost:3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="ed5c7-138">You can view your new application by navigating your browser too[http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Saiba Node. js - captura de tela da saudação aplicativo Hello World em uma janela do navegador](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="ed5c7-140">Em seguida, toostop Olá aplicativo, pressione CTRL + C na janela do terminal hello e, em seguida, clique em **y** tooterminate trabalho de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-140">Then, toostop hello application, press CTRL+C in hello terminal window and then click **y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="ed5c7-141"><a name="_Toc395783179"></a>Etapa 3: Instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="ed5c7-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="ed5c7-142">Olá **Package. JSON** arquivo é um dos arquivos de saudação criados na raiz de saudação do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-142">hello **package.json** file is one of hello files created in hello root of hello project.</span></span> <span data-ttu-id="ed5c7-143">Esse arquivo contém uma lista dos módulos adicionais que são necessários para seu aplicativo do Node.js.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="ed5c7-144">Posteriormente, quando você implanta esse tooAzure aplicativo sites, esse arquivo é usado toodetermine quais toobe da necessidade de módulos instalados no Azure toosupport seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-144">Later, when you deploy this application tooAzure Websites, this file is used toodetermine which modules need toobe installed on Azure toosupport your application.</span></span> <span data-ttu-id="ed5c7-145">Ainda precisamos tooinstall dois pacotes de mais para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-145">We still need tooinstall two more packages for this tutorial.</span></span>

1. <span data-ttu-id="ed5c7-146">Em Olá terminal, instale Olá **async** módulo por meio do npm.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-146">Back in hello terminal, install hello **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="ed5c7-147">Instalar Olá **documentdb** módulo por meio do npm.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-147">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="ed5c7-148">Este é o módulo de saudação onde acontece toda mágica do Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-148">This is hello module where all hello Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="ed5c7-149">Uma verificação rápida da saudação **Package. JSON** arquivo de aplicativo hello deve mostrar Olá módulos adicionais.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-149">A quick check of hello **package.json** file of hello application should show hello additional modules.</span></span> <span data-ttu-id="ed5c7-150">Esse arquivo será informar o Azure toodownload quais pacotes e instalar quando executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-150">This file will tell Azure which packages toodownload and install when running your application.</span></span> <span data-ttu-id="ed5c7-151">Ele deve se parecer com o exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-151">It should resemble hello example below.</span></span>
   
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
   
    <span data-ttu-id="ed5c7-152">Isso informa ao Nó (e ao Azure mais tarde) que seu aplicativo depende desses módulos adicionais.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="ed5c7-153"><a name="_Toc395783180"></a>Etapa 4: Usando o serviço de banco de dados do Azure Cosmos Olá em um aplicativo de nó</span><span class="sxs-lookup"><span data-stu-id="ed5c7-153"><a name="_Toc395783180"></a>Step 4: Using hello Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="ed5c7-154">Que cuida de todos os a configuração inicial hello e configuração, agora vamos get para baixo toowhy estamos aqui e que é parte de código usando o banco de dados do Azure Cosmos de toowrite.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-154">That takes care of all hello initial setup and configuration, now let’s get down toowhy we’re here, and that’s toowrite some code using Azure Cosmos DB.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="ed5c7-155">Criar modelo Olá</span><span class="sxs-lookup"><span data-stu-id="ed5c7-155">Create hello model</span></span>
1. <span data-ttu-id="ed5c7-156">No diretório do projeto hello, criar um novo diretório chamado **modelos** em Olá mesmo diretório que o arquivo Package. JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-156">In hello project directory, create a new directory named **models** in hello same directory as hello package.json file.</span></span>
2. <span data-ttu-id="ed5c7-157">Em Olá **modelos** diretório, crie um novo arquivo chamado **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-157">In hello **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="ed5c7-158">Esse arquivo irá conter modelo Olá Olá tarefas criados pelo nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-158">This file will contain hello model for hello tasks created by our application.</span></span>
3. <span data-ttu-id="ed5c7-159">Em Olá mesmo **modelos** diretório, crie um novo arquivo denominado **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-159">In hello same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="ed5c7-160">Esse arquivo conterá algum código útil e reutilizável, que será usado em todo o nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="ed5c7-161">Código a seguir de saudação de cópia em muito**docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="ed5c7-161">Copy hello following code in too**docdbUtils.js**</span></span>
   
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
   
5. <span data-ttu-id="ed5c7-162">Salve e feche o hello **docdbUtils.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-162">Save and close hello **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="ed5c7-163">Início de saudação do hello **taskDao.js** de arquivo, adicione Olá Olá de tooreference de código a seguir **DocumentDBClient** e hello **docdbUtils.js** criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="ed5c7-163">At hello beginning of hello **taskDao.js** file, add hello following code tooreference hello **DocumentDBClient** and hello **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="ed5c7-164">Em seguida, você adicionará código toodefine e exportar o objeto de tarefa hello.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-164">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="ed5c7-165">Isso é responsável por inicializar nosso objeto de tarefa e a configuração Olá banco de dados e o conjunto de documentos, vamos usar.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-165">This is responsible for initializing our Task object and setting up hello Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="ed5c7-166">Em seguida, adicione Olá métodos adicionais de toodefine de código a seguir em objeto de tarefa hello, que permitem que as interações com os dados armazenados no banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-166">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
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
9. <span data-ttu-id="ed5c7-167">Salve e feche o hello **taskDao.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-167">Save and close hello **taskDao.js** file.</span></span> 

### <a name="create-hello-controller"></a><span data-ttu-id="ed5c7-168">Criar hello controlador</span><span class="sxs-lookup"><span data-stu-id="ed5c7-168">Create hello controller</span></span>
1. <span data-ttu-id="ed5c7-169">Em Olá **rotas** diretório do projeto, criar um novo arquivo denominado **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-169">In hello **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="ed5c7-170">Adicionar Olá código a seguir muito**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-170">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="ed5c7-171">Isso carrega Olá DocumentDBClient e async módulos, que são usados por **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-171">This loads hello DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="ed5c7-172">Isso também definido Olá **TaskList** função, que é passada a uma instância do hello **tarefa** objeto definimos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="ed5c7-172">This also defined hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="ed5c7-173">Continue adicionando toohello **tasklist.js** arquivo adicionando métodos de saudação usados muito**showTasks, addTask**, e **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="ed5c7-173">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks, addTask**, and **completeTasks**:</span></span>
   
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
4. <span data-ttu-id="ed5c7-174">Salve e feche o hello **tasklist.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-174">Save and close hello **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="ed5c7-175">Adicionar config.js</span><span class="sxs-lookup"><span data-stu-id="ed5c7-175">Add config.js</span></span>
1. <span data-ttu-id="ed5c7-176">No diretório do projeto, crie um novo arquivo chamado **config.js**.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="ed5c7-177">Adicionar Olá seguir muito**config.js**.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-177">Add hello following too**config.js**.</span></span> <span data-ttu-id="ed5c7-178">Isso define as configurações e valores necessários para nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="ed5c7-179">Em Olá **config.js** arquivo atualizar valores de saudação do HOST e AUTH_KEY usando valores hello encontrados na folha de chaves de saudação da sua conta de banco de dados do Azure Cosmos Olá [portal do Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ed5c7-179">In hello **config.js** file, update hello values of HOST and AUTH_KEY using hello values found in hello Keys blade of your Azure Cosmos DB account on hello [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="ed5c7-180">Salve e feche o hello **config.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-180">Save and close hello **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="ed5c7-181">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="ed5c7-181">Modify app.js</span></span>
1. <span data-ttu-id="ed5c7-182">No diretório do projeto hello, abra Olá **app.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-182">In hello project directory, open hello **app.js** file.</span></span> <span data-ttu-id="ed5c7-183">Este arquivo foi criado anteriormente ao aplicativo de web Express hello foi criado.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-183">This file was created earlier when hello Express web application was created.</span></span>
2. <span data-ttu-id="ed5c7-184">Adicionar Olá seguir superior de toohello código de **app.js**</span><span class="sxs-lookup"><span data-stu-id="ed5c7-184">Add hello following code toohello top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="ed5c7-185">Esse código define Olá toobe de arquivo de configuração usado e continua tooread valores desse arquivo para algumas variáveis que usaremos em breve.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-185">This code defines hello config file toobe used, and proceeds tooread values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="ed5c7-186">Substituir saudação duas linhas a seguir **app.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="ed5c7-186">Replace hello following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="ed5c7-187">com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed5c7-187">with hello following snippet:</span></span>
   
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
5. <span data-ttu-id="ed5c7-188">Essas linhas definem uma nova instância da nossa **TaskDao** objeto, com um novo tooAzure de conexão Cosmos DB (usando valores hello leia Olá **config.js**), inicializar o objeto de tarefa hello e, em seguida, associar ações do formulário toomethods em nosso **TaskList** controlador.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-188">These lines define a new instance of our **TaskDao** object, with a new connection tooAzure Cosmos DB (using hello values read from hello **config.js**), initialize hello task object and then bind form actions toomethods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="ed5c7-189">Por fim, salve e feche o hello **app.js** arquivo, quase pronto.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-189">Finally, save and close hello **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="ed5c7-190"><a name="_Toc395783181"></a>Etapa 5: Criar uma interface do usuário</span><span class="sxs-lookup"><span data-stu-id="ed5c7-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="ed5c7-191">Agora vamos examinar nossa interface do usuário atenção toobuilding Olá para um usuário, na verdade, pode interagir com o nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-191">Now let’s turn our attention toobuilding hello user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="ed5c7-192">Olá aplicativo Express criamos usa **Jade** como mecanismo de exibição de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-192">hello Express application we created uses **Jade** as hello view engine.</span></span> <span data-ttu-id="ed5c7-193">Para obter mais informações sobre Jade consulte muito[http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="ed5c7-193">For more information on Jade please refer too[http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="ed5c7-194">Olá **layout.jade** arquivo hello **exibições** diretório é usado como um modelo global para outros **.jade** arquivos.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-194">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="ed5c7-195">Nesta etapa você modificá-la toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), que é um kit de ferramentas que torna mais fácil toodesign um site de aparência adequado.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-195">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span> 
2. <span data-ttu-id="ed5c7-196">Olá abrir **layout.jade** arquivo encontrado em Olá **exibições** pasta e substitua conteúdo Olá com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="ed5c7-196">Open hello **layout.jade** file found in hello **views** folder and replace hello contents with hello following:</span></span>

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

    <span data-ttu-id="ed5c7-197">Isso indica efetivamente Olá **Jade** mecanismo toorender alguns HTML para nosso aplicativo e cria um **bloco** chamado **conteúdo** onde é possível fornecer o layout de saudação para nosso conteúdo páginas.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-197">This effectively tells hello **Jade** engine toorender some HTML for our application and creates a **block** called **content** where we can supply hello layout for our content pages.</span></span>

    <span data-ttu-id="ed5c7-198">Salve e feche o arquivo **layout.jade** .</span><span class="sxs-lookup"><span data-stu-id="ed5c7-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="ed5c7-199">Agora, abra Olá **Jade** arquivo, a exibição Olá que será usada pelo nosso aplicativo e substitua o conteúdo de saudação do arquivo hello pela seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="ed5c7-199">Now open hello **index.jade** file, hello view that will be used by our application, and replace hello content of hello file with hello following:</span></span>
   
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
   

<span data-ttu-id="ed5c7-200">Isso estende o layout e fornece o conteúdo Olá **conteúdo** espaço reservado que vimos em Olá **layout.jade** arquivo anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-200">This extends layout, and provides content for hello **content** placeholder we saw in hello **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="ed5c7-201">Nesse layout criamos dois formulários HTML.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="ed5c7-202">formulário primeiro Olá contém uma tabela para nossos dados e um botão que nos permite tooupdate itens postando muito**/completetask** método do nosso controlador.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-202">hello first form contains a table for our data and a button that allows us tooupdate items by posting too**/completetask** method of our controller.</span></span>
    
<span data-ttu-id="ed5c7-203">segunda forma de saudação contém dois campos de entrada e um botão que nos permite toocreate um novo item postando muito**/addtask** método do nosso controlador.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-203">hello second form contains two input fields and a button that allows us toocreate a new item by posting too**/addtask** method of our controller.</span></span>

<span data-ttu-id="ed5c7-204">Isso deve ser tudo o que precisamos para nossa toowork de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-204">This should be all that we need for our application toowork.</span></span>

## <span data-ttu-id="ed5c7-205"><a name="_Toc395783181"></a>Etapa 6: Execute o seu aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="ed5c7-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="ed5c7-206">aplicativo de hello tootest em seu computador local, execute `npm start` em Olá terminal toostart seu aplicativo e atualize seu [http://localhost:3000](http://localhost:3000) página do navegador.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-206">tootest hello application on your local machine, run `npm start` in hello terminal toostart your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="ed5c7-207">página Olá deve agora ser semelhante Olá imagem abaixo:</span><span class="sxs-lookup"><span data-stu-id="ed5c7-207">hello page should now look like hello image below:</span></span>
   
    ![Captura de tela da saudação aplicativo MyTodo lista em uma janela do navegador](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="ed5c7-209">Se você receber um erro sobre Olá recuo no arquivo de layout.jade hello ou Olá Jade, certifique-se de que duas primeiras linhas Olá em ambos os arquivos é justificado à esquerda, sem espaços.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-209">If you receive an error about hello indent in hello layout.jade file or hello index.jade file, ensure that hello first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="ed5c7-210">Se houver espaços antes duas primeiras linhas de saudação, removê-los, salve os dois arquivos e atualizar a janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-210">If there are spaces before hello first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="ed5c7-211">Use Olá campos de Item, o nome do Item e categoria tooenter uma nova tarefa e, em seguida, clique em **Adicionar Item**.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-211">Use hello Item, Item Name and Category fields tooenter a new task and then click **Add Item**.</span></span> <span data-ttu-id="ed5c7-212">Isso cria um documento no Azure Cosmos DB com essas propriedades.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="ed5c7-213">página Olá deve atualizar Olá toodisplay recém-criado item na lista de tarefas de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-213">hello page should update toodisplay hello newly created item in hello ToDo list.</span></span>
   
    ![Captura de tela do aplicativo hello com um novo item na lista de tarefas de saudação](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="ed5c7-215">toocomplete uma tarefa, basta marcar Olá a caixa de seleção na coluna completa hello e, em seguida, clique em **atualizar tarefas**.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-215">toocomplete a task, simply check hello checkbox in hello Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="ed5c7-216">Isso atualiza o documento de saudação já criado.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-216">This updates hello document you already created.</span></span>

5. <span data-ttu-id="ed5c7-217">aplicativo de hello toostop, pressione CTRL + C na janela do terminal hello e, em seguida, clique em **Y** tooterminate trabalho de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-217">toostop hello application, press CTRL+C in hello terminal window and then click **Y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="ed5c7-218"><a name="_Toc395783182"></a>Etapa 7: Implantar o tooAzure de projeto de desenvolvimento de aplicativo sites</span><span class="sxs-lookup"><span data-stu-id="ed5c7-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project tooAzure Websites</span></span>
1. <span data-ttu-id="ed5c7-219">Se ainda não o fez, habilite um repositório git do seu site do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="ed5c7-220">Você pode encontrar instruções sobre como toodo isso em Olá [tooAzure de implantação Local do Git do serviço de aplicativo](../app-service-web/app-service-deploy-local-git.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-220">You can find instructions on how toodo this in hello [Local Git Deployment tooAzure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="ed5c7-221">Adicione seu site do Azure como um git remoto.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="ed5c7-222">Implante por push toohello remoto.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-222">Deploy by pushing toohello remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="ed5c7-223">Em poucos segundos, o git terminará de publicar seu aplicativo Web e iniciará um navegador onde você poderá ver seu trabalho sendo executado no Azure!</span><span class="sxs-lookup"><span data-stu-id="ed5c7-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="ed5c7-224">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="ed5c7-224">Congratulations!</span></span> <span data-ttu-id="ed5c7-225">Você acabou de criado seu primeiro Node. js Express aplicativo Web usando o banco de dados do Azure Cosmos e publicá-la tooAzure sites.</span><span class="sxs-lookup"><span data-stu-id="ed5c7-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it tooAzure Websites.</span></span>

    <span data-ttu-id="ed5c7-226">Se você quiser toodownload ou consulte aplicativos de referência completa de toohello para este tutorial, ele pode ser baixado de [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="ed5c7-226">If you want toodownload or refer toohello complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="ed5c7-227"><a name="_Toc395637775"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ed5c7-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="ed5c7-228">Deseja tooperform escala e testes de desempenho com o banco de dados do Azure Cosmos?</span><span class="sxs-lookup"><span data-stu-id="ed5c7-228">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="ed5c7-229">Confira [teste de desempenho e escalabilidade com o Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="ed5c7-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="ed5c7-230">Saiba como muito[monitorar uma conta de banco de dados do Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="ed5c7-230">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="ed5c7-231">Executar consultas em nosso conjunto de dados de exemplo hello [parque de consulta](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="ed5c7-231">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="ed5c7-232">Explorar Olá [documentação de banco de dados do Azure Cosmos](https://docs.microsoft.com/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="ed5c7-232">Explore hello [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

