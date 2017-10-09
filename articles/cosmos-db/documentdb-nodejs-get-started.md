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
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a>Tutorial do Node. js: Olá Use API DocumentDB no banco de dados do Azure Cosmos toocreate um aplicativo de console Node. js
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js para MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Bem-vindo toohello Node. js tutorial para hello Azure Cosmos DB Node. js SDK! Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB.

Abordaremos:

* Criar e conectar-se a conta de banco de dados do Azure Cosmos tooan
* Configurando o aplicativo
* Criando um banco de dados do nó
* Criar uma coleção
* Criando documentos JSON
* Consultando Olá coleção
* Substituição de um documento
* Exclusão de um documento
* Excluir banco de dados de nó Olá

Você não tem tempo? Não se preocupe! solução completa de saudação está disponível em [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started). Consulte [obter a solução completa de saudação](#GetSolution) para instruções rápidas.

Depois que você concluiu o tutorial do hello Node. js,. use Olá votação botões na parte superior do hello e inferior de toogive esta página nos comentários. Se você deseja toocontact você diretamente, sinta-se livre tooinclude endereço do seu email em seus comentários.

Agora vamos começar!

## <a name="prerequisites-for-hello-nodejs-tutorial"></a>Pré-requisitos para o tutorial do hello Node. js
Verifique se que você tem o seguinte hello:

* Uma conta ativa do Azure. Se não tiver uma, você poderá se inscrever em uma [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
    * Como alternativa, você pode usar o hello [emulador de banco de dados do Azure Cosmos](local-emulator.md) para este tutorial.
* [Node.js](https://nodejs.org/) versão v0.10.29 ou superior.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB
Vamos criar uma conta do Azure Cosmos DB. Se você já tiver uma conta que você deseja toouse, poderá pular muito[configurar seu aplicativo Node. js](#SetupNode). Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar seu aplicativo Node. js](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a>Etapa 2: Configurar seu aplicativo Node.js
1. Abra seu terminal favorito.
2. Localize a pasta hello ou diretório em que você deseja toosave seu aplicativo Node. js.
3. Crie dois arquivos JavaScript vazios com hello comandos a seguir:
   * Windows:
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * Linux/OS X:
     * ```touch app.js```
     * ```touch config.js```
4. Instale o módulo de documentos de saudação por meio do npm. Use Olá comando a seguir:
   * ```npm install documentdb --save```

Ótimo! Agora que você terminou a configuração, vamos começar a escrever o código.

## <a id="Config"></a>Etapa 3: definir as configurações do aplicativo
Abra ```config.js``` em seu editor de texto favorito.

Em seguida, copiar e colar trecho de código do hello abaixo e definir propriedades ```config.endpoint``` e ```config.primaryKey``` tooyour Azure Cosmos DB uri do ponto de extremidade e a chave primária. Ambas as essas configurações podem ser encontradas no hello [portal do Azure](https://portal.azure.com).

![Tutorial de Node. js - captura de tela de saudação portal do Azure, mostrando uma conta de banco de dados do Azure Cosmos, com o hub ativo Olá realçado, botão de chaves de saudação realçado em valores folha de conta do banco de dados do Azure Cosmos hello e Olá URI, chave primária e SECUNDÁRIA realçados em hello Folha de chaves - banco de dados do nó][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

Copie e cole Olá ```database id```, ```collection id```, e ```JSON documents``` tooyour ```config``` abaixo do objeto em que você definir sua ```config.endpoint``` e ```config.authKey``` propriedades. Se você já tiver dados você gostaria que toostore no banco de dados, você pode usar o Azure Cosmos DB [ferramenta de migração de dados](import-data.md) em vez de adicionar definições de saudação de documento.

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


Olá banco de dados, coleção e definições de documento atuará como seu banco de dados do Azure Cosmos ```database id```, ```collection id```e os dados dos documentos.

Finalmente, exporte seu ```config``` objeto, de modo que você poderá referenciá-lo em hello ```app.js``` arquivo.

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <a id="Connect"></a>Etapa 4: Conectar-se a conta de banco de dados do Azure Cosmos tooan
Abra seu vazio ```app.js``` arquivo no editor de texto de saudação. Copie e cole o código Olá Olá tooimport ```documentdb``` criado recentemente e módulo ```config``` módulo.

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

Copie e cole Olá Olá de toouse código salvo anteriormente ```config.endpoint``` e ```config.primaryKey``` toocreate DocumentClient um novo.

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

Agora que você tem um cliente de banco de dados do Azure Cosmos Olá código tooinitialize Olá, vamos dar uma olhada em trabalhar com recursos de banco de dados do Azure Cosmos.

## <a name="step-5-create-a-node-database"></a>Etapa 5: criar um banco de dados do Nó
Copie e cole o código de saudação abaixo tooset Olá status HTTP para não encontrado, a url de banco de dados hello e a url do conjunto de saudação. Essas urls são como cliente de banco de dados do Azure Cosmos Olá encontrará coleta e o banco de dados correto Olá.

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

Um [banco de dados](documentdb-resources.md#databases) podem ser criados usando Olá [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) função da saudação **DocumentClient** classe. Um banco de dados é um contêiner lógico de saudação do armazenamento de documentos, particionado em coleções.

Copie e cole Olá **getDatabase** função para criar o novo banco de dados no arquivo app.js Olá Olá ```id``` especificado no hello ```config``` objeto. Olá função verificará se Olá banco de dados com hello mesmo ```FamilyRegistry``` id já não existe. Se existir, vamos retornar esse banco de dados, em vez de criar um novo.

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

Copie e cole o código de saudação abaixo onde você definir Olá **getDatabase** funcionar a função de auxiliar Olá tooadd **sair** que serão impressas mensagem sair e chamada hello muito**getDatabase** função.

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

Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```

Parabéns! Você criou um banco de dados do Azure Cosmos DB com êxito.

## <a id="CreateColl"></a>Etapa 6: Criar uma coleção
> [!WARNING]
> **CreateDocumentCollectionAsync** criará uma nova coleção, que tem implicações de preços. Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

Um [coleção](documentdb-resources.md#collections) podem ser criados usando Olá [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) função da saudação **DocumentClient** classe. Uma coleção é um contêiner de documentos JSON e uma lógica de aplicativo JavaScript associada.

Copie e cole Olá **getCollection** função abaixo Olá **getDatabase** funcionar em Olá app.js arquivo toocreate sua nova coleção com hello ```id``` especificado no hello ```config```objeto. Novamente, vamos verificar toomake se uma coleção com hello mesmo ```FamilyCollection``` id já não existe. Se existir, vamos retornar essa coleção, em vez de criar uma nova.

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

Copie e cole o código de saudação abaixo chamada hello muito**getDatabase** tooexecute Olá **getCollection** função.

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```

Parabéns! Você criou uma coleção do Azure Cosmos DB com êxito.

## <a id="CreateDoc"></a>Etapa 7: Criar um documento
Um [documento](documentdb-resources.md#documents) podem ser criados usando Olá [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) função da saudação **DocumentClient** classe. Os documentos são conteúdo JSON (arbitrário) definido pelo usuário. Agora você pode inserir um documento no Azure Cosmos DB.

Copie e cole Olá **getFamilyDocument** função abaixo Olá **getCollection** função para criar documentos de saudação contendo dados JSON de saudação salvos no hello ```config``` objeto. Novamente, veremos toomake se um documento com hello mesmo id já não existe.

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

Copie e cole o código de saudação abaixo chamada hello muito**getCollection** tooexecute Olá **getFamilyDocument** função.

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```

Parabéns! Você criou um documento do Azure Cosmos DB com êxito.

![Banco de dados do nó - diagrama que ilustra uma relação hierárquica entre conta hello, banco de dados de saudação, coleção hello e documentos Olá Olá - tutorial Node. js](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a>Etapa 8: Consultar recursos do Azure Cosmos DB
O Azure Cosmos DB tem suporte para [consultas](documentdb-sql-query.md) avançadas de documentos JSON armazenados em cada coleção. Olá código exemplo a seguir mostra uma consulta que você pode executar em documentos de saudação em sua coleção.

Copie e cole Olá **queryCollection** função abaixo Olá **getFamilyDocument** função hello app.js arquivo. O Azure Cosmos DB dá suporte a consultas do tipo SQL, conforme mostrado abaixo. Para obter mais informações sobre como criar consultas complexas, confira Olá [parque de consulta](https://www.documentdb.com/sql/demo) e hello [consultar a documentação](documentdb-sql-query.md).

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


Olá diagrama a seguir ilustra como consultas de banco de dados SQL do Azure Cosmos Olá sintaxe é chamada na coleção de saudação que você criou.

![Banco de dados do nó - diagrama ilustrando escopo hello e o significado da consulta Olá - tutorial Node. js](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

Olá [FROM](documentdb-sql-query.md#FromClause) palavra-chave é opcional em consulta Olá porque as consultas de banco de dados do Azure Cosmos já estão no escopo tooa única coleção. Portanto, "FROM Families f" pode ser trocado por "FROM root r" ou qualquer outra variável de nome que você escolher. Banco de dados do Azure Cosmos deduzirá que famílias, raiz ou o nome da variável Olá você escolheu, coleção atual de saudação de referência por padrão.

Copie e cole o código de saudação abaixo chamada hello muito**getFamilyDocument** tooexecute Olá **queryCollection** função.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```

Parabéns! Você consultou com sucesso documentos do Azure Cosmos DB.

## <a id="ReplaceDocument"></a>Etapa 9: substituir um documento
O Azure Cosmos DB dá suporte à substituição de documentos JSON.

Copie e cole Olá **replaceFamilyDocument** função abaixo Olá **queryCollection** função hello app.js arquivo.

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

Copie e cole o código de saudação abaixo chamada hello muito**queryCollection** tooexecute Olá **replaceDocument** função. Além disso, adicionar Olá código toocall **queryCollection** novamente tooverify documento hello tinha alterada com êxito.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```

Parabéns! Você substituiu um documento do Azure Cosmos DB com sucesso.

## <a id="DeleteDocument"></a>Etapa 10: excluir um documento
O Azure Cosmos DB dá suporte à exclusão de documentos JSON.

Copie e cole Olá **deleteFamilyDocument** função abaixo Olá **replaceFamilyDocument** função.

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

Copie e cole o código de saudação abaixo Olá chamada toohello segundo **queryCollection** tooexecute Olá **deleteDocument** função.

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```

Parabéns! Você excluiu um documento do Azure Cosmos DB com êxito.

## <a id="DeleteDatabase"></a>Etapa 11: Excluir o banco de dados de nó de saudação
Excluindo Olá criado o banco de dados removerá o banco de dados de saudação e todos os recursos de filhos (coleções, documentos, etc.).

Copie e cole Olá **limpeza** função abaixo Olá **deleteFamilyDocument** funções de banco de dados do tooremove hello e todos os recursos de filhos de saudação.

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

Copie e cole o código de saudação abaixo chamada hello muito**deleteFamilyDocument** tooexecute Olá **limpeza** função.

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a>Etapa 12: Executar todo o aplicativo Node.js!
Completamente, sequência Olá para chamar funções deve ser assim:

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

Em seu terminal, localize seu ```app.js``` e execute o comando hello:```node app.js```

Você deve ver a saída de saudação do aplicativo iniciado get. saída de Hello deve coincidir com o texto de exemplo hello abaixo.

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

Parabéns! Você criou você concluiu o tutorial do Node. js hello e ter seu primeiro aplicativo de console de banco de dados do Azure Cosmos!

## <a id="GetSolution"></a>Obter a solução completa de tutorial de Node. js Olá
Se você não tiver tempo toocomplete Olá etapas neste tutorial, ou quiser apenas o código de saudação toodownload, você poderá obtê-lo de [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).

toorun Olá GetStarted solução que contém todos os exemplos de saudação neste artigo, você precisará seguir hello:

* [Conta do Azure Cosmos DB][create-account].
* Olá [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solução disponível no GitHub.

Instalar Olá **documentdb** módulo por meio do npm. Use Olá comando a seguir:

* ```npm install documentdb --save```

Em seguida, no hello ```config.js``` arquivo atualizar Olá config.endpoint e config.authKey valores conforme descrito em [etapa 3: definir configurações do aplicativo](#Config). 

Em seu terminal, localize seu ```app.js``` e execute o comando Olá: ```node app.js```.

Pronto, compile-o e você pode continuar! 

## <a name="next-steps"></a>Próximas etapas
* Deseja obter um exemplo mais complexo do Node.js? Confira [Compilar um aplicativo Web Node.js usando o Azure Cosmos DB](documentdb-nodejs-application.md).
* Saiba como muito[monitorar uma conta de banco de dados do Azure Cosmos](monitor-accounts.md).
* Executar consultas em nosso conjunto de dados de exemplo hello [parque de consulta](https://www.documentdb.com/sql/demo).
* Saiba mais sobre o modelo de programação de Olá Olá seção desenvolver de saudação [página de documentação do banco de dados do Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
