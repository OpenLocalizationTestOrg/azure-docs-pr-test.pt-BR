---
title: "Cosmos do Azure DB: Criar um aplicativo com Node. js e Olá API DocumentDB | Microsoft Docs"
description: "Apresenta um exemplo de código de Node. js que você pode usar tooconnect tooand consulta Olá API DocumentDB do Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a>Banco de dados do Azure do Cosmos: Criar um aplicativo de API de documentos com Node. js e Olá portal do Azure

O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente. 

Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá portal do Azure. Você, em seguida, compilar e executar um aplicativo de console criado em Olá [DocumentDB Node. js API](documentdb-sdk-node.md).

## <a name="prerequisites"></a>Pré-requisitos

* Antes de executar este exemplo, você deve ter Olá pré-requisitos a seguir:
    * [Node.js](https://nodejs.org/en/) versão v0.10.29 ou superior
    * [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Crie uma conta de banco de dados

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Adicionar uma coleção

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello

Agora vamos clone uma API de documentos de aplicativo do github, defina a cadeia de caracteres de conexão hello e executá-lo. Você verá como é fácil toowork com dados programaticamente. 

1. Abra uma janela de terminal de git, como git bash, e `CD` tooa diretório de trabalho.  

2. Execute Olá repositório de exemplo do comando tooclone Olá a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a>Examine o código de saudação

Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello. Olá abrir `app.js` arquivo e descobrir que essas linhas de código criam Olá recursos de banco de dados do Azure Cosmos. 

* Olá `documentClient` é inicializado.

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* Um novo banco de dados é criado.

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Uma nova coleção é criada.

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Alguns documentos são criados.

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Uma consulta SQL no JSON é executada.

    ```nodejs
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
    ```    

## <a name="update-your-connection-string"></a>Atualizar sua cadeia de conexão

Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.

1. Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**. Você usará botões de cópia de saudação na direita de saudação do hello toocopy da tela hello URI e a chave primária em Olá `config.js` arquivo na próxima etapa do hello.

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-documentdb-dotnet/keys.png)

2. Em aberto Olá `config.js` arquivo. 

3. Copie o valor URI do portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá o valor da chave do ponto de extremidade Olá no `config.js`. 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. Em seguida, copie o valor de chave primária do portal de saudação e torná-lo Olá valor Olá `config.primaryKey` em `config.js`. Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos. 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a>Executar o aplicativo hello
1. Executar `npm install` em um terminal tooinstall necessário módulos npm

2. Executar `node app.js` em um terminal toostart seu aplicativo de nó.

Agora você pode voltar tooData Explorer e consulte a consulta, modificar e trabalhar com esses novos dados. 

## <a name="review-slas-in-hello-azure-portal"></a>Examine os SLAs em Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:

1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você. 
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, crie uma coleção usando Olá Explorador de dados e executar o aplicativo. Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais. 

> [!div class="nextstepaction"]
> [Importar dados no Azure Cosmos DB](import-data.md)


