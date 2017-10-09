---
title: "tutorial de aaaNode.js de saudação API de documentos para o banco de dados do Azure Cosmos | Microsoft Docs"
description: Um tutorial Node. js que cria um banco de dados do Cosmos com hello API DocumentDB.
keywords: "tutorial do node.js, banco de dados do nó"
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a><span data-ttu-id="69460-104">Tutorial do Node. js: Olá Use API DocumentDB no banco de dados do Azure Cosmos toocreate um aplicativo de console Node. js</span><span class="sxs-lookup"><span data-stu-id="69460-104">Node.js tutorial: Use hello DocumentDB API in Azure Cosmos DB toocreate a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="69460-105">.NET</span><span class="sxs-lookup"><span data-stu-id="69460-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="69460-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="69460-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="69460-107">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="69460-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="69460-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="69460-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="69460-109">Java</span><span class="sxs-lookup"><span data-stu-id="69460-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="69460-110">C++</span><span class="sxs-lookup"><span data-stu-id="69460-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="69460-111">Bem-vindo toohello Node. js tutorial para hello Azure Cosmos DB Node. js SDK!</span><span class="sxs-lookup"><span data-stu-id="69460-111">Welcome toohello Node.js tutorial for hello Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="69460-112">Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="69460-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="69460-113">Abordaremos:</span><span class="sxs-lookup"><span data-stu-id="69460-113">We'll cover:</span></span>

* <span data-ttu-id="69460-114">Criar e conectar-se a conta de banco de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="69460-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="69460-115">Configurando o aplicativo</span><span class="sxs-lookup"><span data-stu-id="69460-115">Setting up your application</span></span>
* <span data-ttu-id="69460-116">Criando um banco de dados do nó</span><span class="sxs-lookup"><span data-stu-id="69460-116">Creating a node database</span></span>
* <span data-ttu-id="69460-117">Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="69460-117">Creating a collection</span></span>
* <span data-ttu-id="69460-118">Criando documentos JSON</span><span class="sxs-lookup"><span data-stu-id="69460-118">Creating JSON documents</span></span>
* <span data-ttu-id="69460-119">Consultando Olá coleção</span><span class="sxs-lookup"><span data-stu-id="69460-119">Querying hello collection</span></span>
* <span data-ttu-id="69460-120">Substituição de um documento</span><span class="sxs-lookup"><span data-stu-id="69460-120">Replacing a document</span></span>
* <span data-ttu-id="69460-121">Exclusão de um documento</span><span class="sxs-lookup"><span data-stu-id="69460-121">Deleting a document</span></span>
* <span data-ttu-id="69460-122">Excluir banco de dados de nó Olá</span><span class="sxs-lookup"><span data-stu-id="69460-122">Deleting hello node database</span></span>

<span data-ttu-id="69460-123">Você não tem tempo?</span><span class="sxs-lookup"><span data-stu-id="69460-123">Don't have time?</span></span> <span data-ttu-id="69460-124">Não se preocupe!</span><span class="sxs-lookup"><span data-stu-id="69460-124">Don't worry!</span></span> <span data-ttu-id="69460-125">solução completa de saudação está disponível em [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="69460-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="69460-126">Consulte [obter a solução completa de saudação](#GetSolution) para instruções rápidas.</span><span class="sxs-lookup"><span data-stu-id="69460-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="69460-127">Depois que você concluiu o tutorial do hello Node. js,. use Olá votação botões na parte superior do hello e inferior de toogive esta página nos comentários.</span><span class="sxs-lookup"><span data-stu-id="69460-127">After you've completed hello Node.js tutorial, please use hello voting buttons at hello top and bottom of this page toogive us feedback.</span></span> <span data-ttu-id="69460-128">Se você deseja toocontact você diretamente, sinta-se livre tooinclude endereço do seu email em seus comentários.</span><span class="sxs-lookup"><span data-stu-id="69460-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="69460-129">Agora vamos começar!</span><span class="sxs-lookup"><span data-stu-id="69460-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-nodejs-tutorial"></a><span data-ttu-id="69460-130">Pré-requisitos para o tutorial do hello Node. js</span><span class="sxs-lookup"><span data-stu-id="69460-130">Prerequisites for hello Node.js tutorial</span></span>
<span data-ttu-id="69460-131">Verifique se que você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="69460-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="69460-132">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="69460-132">An active Azure account.</span></span> <span data-ttu-id="69460-133">Se não tiver uma, você poderá se inscrever em uma [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="69460-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="69460-134">Como alternativa, você pode usar o hello [emulador de banco de dados do Azure Cosmos](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="69460-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="69460-135">[Node.js](https://nodejs.org/) versão v0.10.29 ou superior.</span><span class="sxs-lookup"><span data-stu-id="69460-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="69460-136">Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="69460-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="69460-137">Vamos criar uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="69460-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="69460-138">Se você já tiver uma conta que você deseja toouse, poderá pular muito[configurar seu aplicativo Node. js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="69460-138">If you already have an account you want toouse, you can skip ahead too[Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="69460-139">Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar seu aplicativo Node. js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="69460-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="69460-140"><a id="SetupNode"></a>Etapa 2: Configurar seu aplicativo Node.js</span><span class="sxs-lookup"><span data-stu-id="69460-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="69460-141">Abra seu terminal favorito.</span><span class="sxs-lookup"><span data-stu-id="69460-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="69460-142">Localize a pasta hello ou diretório em que você deseja toosave seu aplicativo Node. js.</span><span class="sxs-lookup"><span data-stu-id="69460-142">Locate hello folder or directory where you'd like toosave your Node.js application.</span></span>
3. <span data-ttu-id="69460-143">Crie dois arquivos JavaScript vazios com hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="69460-143">Create two empty JavaScript files with hello following commands:</span></span>
   * <span data-ttu-id="69460-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="69460-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="69460-145">Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="69460-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="69460-146">Instale o módulo de documentos de saudação por meio do npm.</span><span class="sxs-lookup"><span data-stu-id="69460-146">Install hello documentdb module via npm.</span></span> <span data-ttu-id="69460-147">Use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="69460-147">Use hello following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="69460-148">Ótimo!</span><span class="sxs-lookup"><span data-stu-id="69460-148">Great!</span></span> <span data-ttu-id="69460-149">Agora que você terminou a configuração, vamos começar a escrever o código.</span><span class="sxs-lookup"><span data-stu-id="69460-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="69460-150"><a id="Config"></a>Etapa 3: definir as configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="69460-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="69460-151">Abra ```config.js``` em seu editor de texto favorito.</span><span class="sxs-lookup"><span data-stu-id="69460-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="69460-152">Em seguida, copiar e colar trecho de código do hello abaixo e definir propriedades ```config.endpoint``` e ```config.primaryKey``` tooyour Azure Cosmos DB uri do ponto de extremidade e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="69460-152">Then, copy and paste hello code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` tooyour Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="69460-153">Ambas as essas configurações podem ser encontradas no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="69460-153">Both these configurations can be found in hello [Azure portal](https://portal.azure.com).</span></span>

![Tutorial de Node. js - captura de tela de saudação portal do Azure, mostrando uma conta de banco de dados do Azure Cosmos, com o hub ativo Olá realçado, botão de chaves de saudação realçado em valores folha de conta do banco de dados do Azure Cosmos hello e Olá URI, chave primária e SECUNDÁRIA realçados em hello Folha de chaves - banco de dados do nó][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="69460-155">Copie e cole Olá ```database id```, ```collection id```, e ```JSON documents``` tooyour ```config``` abaixo do objeto em que você definir sua ```config.endpoint``` e ```config.authKey``` propriedades.</span><span class="sxs-lookup"><span data-stu-id="69460-155">Copy and paste hello ```database id```, ```collection id```, and ```JSON documents``` tooyour ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="69460-156">Se você já tiver dados você gostaria que toostore no banco de dados, você pode usar o Azure Cosmos DB [ferramenta de migração de dados](import-data.md) em vez de adicionar definições de saudação de documento.</span><span class="sxs-lookup"><span data-stu-id="69460-156">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding hello document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


<span data-ttu-id="69460-157">Olá banco de dados, coleção e definições de documento atuará como seu banco de dados do Azure Cosmos ```database id```, ```collection id```e os dados dos documentos.</span><span class="sxs-lookup"><span data-stu-id="69460-157">hello database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="69460-158">Finalmente, exporte seu ```config``` objeto, de modo que você poderá referenciá-lo em hello ```app.js``` arquivo.</span><span class="sxs-lookup"><span data-stu-id="69460-158">Finally, export your ```config``` object, so that you can reference it within hello ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <span data-ttu-id="69460-159"><a id="Connect"></a>Etapa 4: Conectar-se a conta de banco de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="69460-159"><a id="Connect"></a> Step 4: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="69460-160">Abra seu vazio ```app.js``` arquivo no editor de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="69460-160">Open your empty ```app.js``` file in hello text editor.</span></span> <span data-ttu-id="69460-161">Copie e cole o código Olá Olá tooimport ```documentdb``` criado recentemente e módulo ```config``` módulo.</span><span class="sxs-lookup"><span data-stu-id="69460-161">Copy and paste hello code below tooimport hello ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="69460-162">Copie e cole Olá Olá de toouse código salvo anteriormente ```config.endpoint``` e ```config.primaryKey``` toocreate DocumentClient um novo.</span><span class="sxs-lookup"><span data-stu-id="69460-162">Copy and paste hello code toouse hello previously saved ```config.endpoint``` and ```config.primaryKey``` toocreate a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="69460-163">Agora que você tem um cliente de banco de dados do Azure Cosmos Olá código tooinitialize Olá, vamos dar uma olhada em trabalhar com recursos de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="69460-163">Now that you have hello code tooinitialize hello Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="69460-164">Etapa 5: criar um banco de dados do Nó</span><span class="sxs-lookup"><span data-stu-id="69460-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="69460-165">Copie e cole o código de saudação abaixo tooset Olá status HTTP para não encontrado, a url de banco de dados hello e a url do conjunto de saudação.</span><span class="sxs-lookup"><span data-stu-id="69460-165">Copy and paste hello code below tooset hello HTTP status for Not Found, hello database url, and hello collection url.</span></span> <span data-ttu-id="69460-166">Essas urls são como cliente de banco de dados do Azure Cosmos Olá encontrará coleta e o banco de dados correto Olá.</span><span class="sxs-lookup"><span data-stu-id="69460-166">These urls are how hello Azure Cosmos DB client will find hello right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="69460-167">Um [banco de dados](documentdb-resources.md#databases) podem ser criados usando Olá [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) função da saudação **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="69460-167">A [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="69460-168">Um banco de dados é um contêiner lógico de saudação do armazenamento de documentos, particionado em coleções.</span><span class="sxs-lookup"><span data-stu-id="69460-168">A database is hello logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="69460-169">Copie e cole Olá **getDatabase** função para criar o novo banco de dados no arquivo app.js Olá Olá ```id``` especificado no hello ```config``` objeto.</span><span class="sxs-lookup"><span data-stu-id="69460-169">Copy and paste hello **getDatabase** function for creating your new database in hello app.js file with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="69460-170">Olá função verificará se Olá banco de dados com hello mesmo ```FamilyRegistry``` id já não existe.</span><span class="sxs-lookup"><span data-stu-id="69460-170">hello function will check if hello database with hello same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="69460-171">Se existir, vamos retornar esse banco de dados, em vez de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="69460-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

<span data-ttu-id="69460-172">Copie e cole o código de saudação abaixo onde você definir Olá **getDatabase** funcionar a função de auxiliar Olá tooadd **sair** que serão impressas mensagem sair e chamada hello muito**getDatabase** função.</span><span class="sxs-lookup"><span data-stu-id="69460-172">Copy and paste hello code below where you set hello **getDatabase** function tooadd hello helper function **exit** that will print hello exit message and hello call too**getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="69460-173">Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="69460-173">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="69460-174">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="69460-174">Congratulations!</span></span> <span data-ttu-id="69460-175">Você criou um banco de dados do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="69460-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="69460-176"><a id="CreateColl"></a>Etapa 6: Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="69460-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="69460-177">**CreateDocumentCollectionAsync** criará uma nova coleção, que tem implicações de preços.</span><span class="sxs-lookup"><span data-stu-id="69460-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="69460-178">Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="69460-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="69460-179">Um [coleção](documentdb-resources.md#collections) podem ser criados usando Olá [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) função da saudação **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="69460-179">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="69460-180">Uma coleção é um contêiner de documentos JSON e uma lógica de aplicativo JavaScript associada.</span><span class="sxs-lookup"><span data-stu-id="69460-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="69460-181">Copie e cole Olá **getCollection** função abaixo Olá **getDatabase** funcionar em Olá app.js arquivo toocreate sua nova coleção com hello ```id``` especificado no hello ```config```objeto.</span><span class="sxs-lookup"><span data-stu-id="69460-181">Copy and paste hello **getCollection** function underneath hello **getDatabase** function in hello app.js file toocreate your new collection with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="69460-182">Novamente, vamos verificar toomake se uma coleção com hello mesmo ```FamilyCollection``` id já não existe.</span><span class="sxs-lookup"><span data-stu-id="69460-182">Again, we'll check toomake sure a collection with hello same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="69460-183">Se existir, vamos retornar essa coleção, em vez de criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="69460-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

<span data-ttu-id="69460-184">Copie e cole o código de saudação abaixo chamada hello muito**getDatabase** tooexecute Olá **getCollection** função.</span><span class="sxs-lookup"><span data-stu-id="69460-184">Copy and paste hello code below hello call too**getDatabase** tooexecute hello **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="69460-185">Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="69460-185">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="69460-186">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="69460-186">Congratulations!</span></span> <span data-ttu-id="69460-187">Você criou uma coleção do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="69460-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="69460-188"><a id="CreateDoc"></a>Etapa 7: Criar um documento</span><span class="sxs-lookup"><span data-stu-id="69460-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="69460-189">Um [documento](documentdb-resources.md#documents) podem ser criados usando Olá [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) função da saudação **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="69460-189">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="69460-190">Os documentos são conteúdo JSON (arbitrário) definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="69460-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="69460-191">Agora você pode inserir um documento no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="69460-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="69460-192">Copie e cole Olá **getFamilyDocument** função abaixo Olá **getCollection** função para criar documentos de saudação contendo dados JSON de saudação salvos no hello ```config``` objeto.</span><span class="sxs-lookup"><span data-stu-id="69460-192">Copy and paste hello **getFamilyDocument** function underneath hello **getCollection** function for creating hello documents containing hello JSON data saved in hello ```config``` object.</span></span> <span data-ttu-id="69460-193">Novamente, veremos toomake se um documento com hello mesmo id já não existe.</span><span class="sxs-lookup"><span data-stu-id="69460-193">Again, we'll check toomake sure a document with hello same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="69460-194">Copie e cole o código de saudação abaixo chamada hello muito**getCollection** tooexecute Olá **getFamilyDocument** função.</span><span class="sxs-lookup"><span data-stu-id="69460-194">Copy and paste hello code below hello call too**getCollection** tooexecute hello **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="69460-195">Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="69460-195">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="69460-196">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="69460-196">Congratulations!</span></span> <span data-ttu-id="69460-197">Você criou um documento do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="69460-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Banco de dados do nó - diagrama que ilustra uma relação hierárquica entre conta hello, banco de dados de saudação, coleção hello e documentos Olá Olá - tutorial Node. js](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="69460-199"><a id="Query"></a>Etapa 8: Consultar recursos do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="69460-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="69460-200">O Azure Cosmos DB tem suporte para [consultas](documentdb-sql-query.md) avançadas de documentos JSON armazenados em cada coleção.</span><span class="sxs-lookup"><span data-stu-id="69460-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="69460-201">Olá código exemplo a seguir mostra uma consulta que você pode executar em documentos de saudação em sua coleção.</span><span class="sxs-lookup"><span data-stu-id="69460-201">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

<span data-ttu-id="69460-202">Copie e cole Olá **queryCollection** função abaixo Olá **getFamilyDocument** função hello app.js arquivo.</span><span class="sxs-lookup"><span data-stu-id="69460-202">Copy and paste hello **queryCollection** function underneath hello **getFamilyDocument** function in hello app.js file.</span></span> <span data-ttu-id="69460-203">O Azure Cosmos DB dá suporte a consultas do tipo SQL, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="69460-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="69460-204">Para obter mais informações sobre como criar consultas complexas, confira Olá [parque de consulta](https://www.documentdb.com/sql/demo) e hello [consultar a documentação](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="69460-204">For more information on building complex queries, check out hello [Query Playground](https://www.documentdb.com/sql/demo) and hello [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


<span data-ttu-id="69460-205">Olá diagrama a seguir ilustra como consultas de banco de dados SQL do Azure Cosmos Olá sintaxe é chamada na coleção de saudação que você criou.</span><span class="sxs-lookup"><span data-stu-id="69460-205">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created.</span></span>

![Banco de dados do nó - diagrama ilustrando escopo hello e o significado da consulta Olá - tutorial Node. js](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="69460-207">Olá [FROM](documentdb-sql-query.md#FromClause) palavra-chave é opcional em consulta Olá porque as consultas de banco de dados do Azure Cosmos já estão no escopo tooa única coleção.</span><span class="sxs-lookup"><span data-stu-id="69460-207">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="69460-208">Portanto, "FROM Families f" pode ser trocado por "FROM root r" ou qualquer outra variável de nome que você escolher.</span><span class="sxs-lookup"><span data-stu-id="69460-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="69460-209">Banco de dados do Azure Cosmos deduzirá que famílias, raiz ou o nome da variável Olá você escolheu, coleção atual de saudação de referência por padrão.</span><span class="sxs-lookup"><span data-stu-id="69460-209">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

<span data-ttu-id="69460-210">Copie e cole o código de saudação abaixo chamada hello muito**getFamilyDocument** tooexecute Olá **queryCollection** função.</span><span class="sxs-lookup"><span data-stu-id="69460-210">Copy and paste hello code below hello call too**getFamilyDocument** tooexecute hello **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="69460-211">Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="69460-211">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="69460-212">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="69460-212">Congratulations!</span></span> <span data-ttu-id="69460-213">Você consultou com sucesso documentos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="69460-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="69460-214"><a id="ReplaceDocument"></a>Etapa 9: substituir um documento</span><span class="sxs-lookup"><span data-stu-id="69460-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="69460-215">O Azure Cosmos DB dá suporte à substituição de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="69460-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="69460-216">Copie e cole Olá **replaceFamilyDocument** função abaixo Olá **queryCollection** função hello app.js arquivo.</span><span class="sxs-lookup"><span data-stu-id="69460-216">Copy and paste hello **replaceFamilyDocument** function underneath hello **queryCollection** function in hello app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="69460-217">Copie e cole o código de saudação abaixo chamada hello muito**queryCollection** tooexecute Olá **replaceDocument** função.</span><span class="sxs-lookup"><span data-stu-id="69460-217">Copy and paste hello code below hello call too**queryCollection** tooexecute hello **replaceDocument** function.</span></span> <span data-ttu-id="69460-218">Além disso, adicionar Olá código toocall **queryCollection** novamente tooverify documento hello tinha alterada com êxito.</span><span class="sxs-lookup"><span data-stu-id="69460-218">Also, add hello code toocall **queryCollection** again tooverify that hello document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="69460-219">Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="69460-219">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="69460-220">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="69460-220">Congratulations!</span></span> <span data-ttu-id="69460-221">Você substituiu um documento do Azure Cosmos DB com sucesso.</span><span class="sxs-lookup"><span data-stu-id="69460-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="69460-222"><a id="DeleteDocument"></a>Etapa 10: excluir um documento</span><span class="sxs-lookup"><span data-stu-id="69460-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="69460-223">O Azure Cosmos DB dá suporte à exclusão de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="69460-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="69460-224">Copie e cole Olá **deleteFamilyDocument** função abaixo Olá **replaceFamilyDocument** função.</span><span class="sxs-lookup"><span data-stu-id="69460-224">Copy and paste hello **deleteFamilyDocument** function underneath hello **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="69460-225">Copie e cole o código de saudação abaixo Olá chamada toohello segundo **queryCollection** tooexecute Olá **deleteDocument** função.</span><span class="sxs-lookup"><span data-stu-id="69460-225">Copy and paste hello code below hello call toohello second **queryCollection** tooexecute hello **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="69460-226">Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="69460-226">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="69460-227">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="69460-227">Congratulations!</span></span> <span data-ttu-id="69460-228">Você excluiu um documento do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="69460-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="69460-229"><a id="DeleteDatabase"></a>Etapa 11: Excluir o banco de dados de nó de saudação</span><span class="sxs-lookup"><span data-stu-id="69460-229"><a id="DeleteDatabase"></a>Step 11: Delete hello Node database</span></span>
<span data-ttu-id="69460-230">Excluindo Olá criado o banco de dados removerá o banco de dados de saudação e todos os recursos de filhos (coleções, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="69460-230">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="69460-231">Copie e cole Olá **limpeza** função abaixo Olá **deleteFamilyDocument** funções de banco de dados do tooremove hello e todos os recursos de filhos de saudação.</span><span class="sxs-lookup"><span data-stu-id="69460-231">Copy and paste hello **cleanup** function underneath hello **deleteFamilyDocument** function tooremove hello database and all hello children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="69460-232">Copie e cole o código de saudação abaixo chamada hello muito**deleteFamilyDocument** tooexecute Olá **limpeza** função.</span><span class="sxs-lookup"><span data-stu-id="69460-232">Copy and paste hello code below hello call too**deleteFamilyDocument** tooexecute hello **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="69460-233"><a id="Run"></a>Etapa 12: Executar todo o aplicativo Node.js!</span><span class="sxs-lookup"><span data-stu-id="69460-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="69460-234">Completamente, sequência Olá para chamar funções deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="69460-234">Altogether, hello sequence for calling your functions should look like this:</span></span>

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="69460-235">Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="69460-235">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="69460-236">Você deve ver a saída de saudação do aplicativo iniciado get.</span><span class="sxs-lookup"><span data-stu-id="69460-236">You should see hello output of your get started app.</span></span> <span data-ttu-id="69460-237">saída de Hello deve coincidir com o texto de exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="69460-237">hello output should match hello example text below.</span></span>

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

<span data-ttu-id="69460-238">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="69460-238">Congratulations!</span></span> <span data-ttu-id="69460-239">Você criou você concluiu o tutorial do Node. js hello e ter seu primeiro aplicativo de console de banco de dados do Azure Cosmos!</span><span class="sxs-lookup"><span data-stu-id="69460-239">You've created you've completed hello Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="69460-240"><a id="GetSolution"></a>Obter a solução completa de tutorial de Node. js Olá</span><span class="sxs-lookup"><span data-stu-id="69460-240"><a id="GetSolution"></a>Get hello complete Node.js tutorial solution</span></span>
<span data-ttu-id="69460-241">Se você não tiver tempo toocomplete Olá etapas neste tutorial, ou quiser apenas o código de saudação toodownload, você poderá obtê-lo de [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="69460-241">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="69460-242">toorun Olá GetStarted solução que contém todos os exemplos de saudação neste artigo, você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="69460-242">toorun hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="69460-243">[Conta do Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="69460-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="69460-244">Olá [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solução disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="69460-244">hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="69460-245">Instalar Olá **documentdb** módulo por meio do npm.</span><span class="sxs-lookup"><span data-stu-id="69460-245">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="69460-246">Use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="69460-246">Use hello following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="69460-247">Em seguida, no hello ```config.js``` arquivo atualizar Olá config.endpoint e config.authKey valores conforme descrito em [etapa 3: definir configurações do aplicativo](#Config).</span><span class="sxs-lookup"><span data-stu-id="69460-247">Next, in hello ```config.js``` file, update hello config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="69460-248">Em seu terminal, localize seu ```app.js``` e execute o comando Olá: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="69460-248">Then in your terminal, locate your ```app.js``` file and run hello command: ```node app.js```.</span></span>

<span data-ttu-id="69460-249">Pronto, compile-o e você pode continuar!</span><span class="sxs-lookup"><span data-stu-id="69460-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="69460-250">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="69460-250">Next steps</span></span>
* <span data-ttu-id="69460-251">Deseja obter um exemplo mais complexo do Node.js?</span><span class="sxs-lookup"><span data-stu-id="69460-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="69460-252">Confira [Compilar um aplicativo Web Node.js usando o Azure Cosmos DB](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="69460-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="69460-253">Saiba como muito[monitorar uma conta de banco de dados do Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="69460-253">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="69460-254">Executar consultas em nosso conjunto de dados de exemplo hello [parque de consulta](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="69460-254">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="69460-255">Saiba mais sobre o modelo de programação de Olá Olá seção desenvolver de saudação [página de documentação do banco de dados do Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="69460-255">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
