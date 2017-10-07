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
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a><span data-ttu-id="9085d-103">Banco de dados do Azure do Cosmos: Criar um aplicativo de API de documentos com Node. js e Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9085d-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and hello Azure portal</span></span>

<span data-ttu-id="9085d-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9085d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="9085d-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="9085d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="9085d-106">Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9085d-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="9085d-107">Você, em seguida, compilar e executar um aplicativo de console criado em Olá [DocumentDB Node. js API](documentdb-sdk-node.md).</span><span class="sxs-lookup"><span data-stu-id="9085d-107">You then build and run a console app built on hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9085d-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9085d-108">Prerequisites</span></span>

* <span data-ttu-id="9085d-109">Antes de executar este exemplo, você deve ter Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9085d-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="9085d-110">[Node.js](https://nodejs.org/en/) versão v0.10.29 ou superior</span><span class="sxs-lookup"><span data-stu-id="9085d-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="9085d-111">Git</span><span class="sxs-lookup"><span data-stu-id="9085d-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="9085d-112">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="9085d-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="9085d-113">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="9085d-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="9085d-114">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="9085d-114">Clone hello sample application</span></span>

<span data-ttu-id="9085d-115">Agora vamos clone uma API de documentos de aplicativo do github, defina a cadeia de caracteres de conexão hello e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="9085d-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="9085d-116">Você verá como é fácil toowork com dados programaticamente.</span><span class="sxs-lookup"><span data-stu-id="9085d-116">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="9085d-117">Abra uma janela de terminal de git, como git bash, e `CD` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9085d-117">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="9085d-118">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="9085d-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="9085d-119">Examine o código de saudação</span><span class="sxs-lookup"><span data-stu-id="9085d-119">Review hello code</span></span>

<span data-ttu-id="9085d-120">Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9085d-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="9085d-121">Olá abrir `app.js` arquivo e descobrir que essas linhas de código criam Olá recursos de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9085d-121">Open hello `app.js` file and you find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="9085d-122">Olá `documentClient` é inicializado.</span><span class="sxs-lookup"><span data-stu-id="9085d-122">hello `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="9085d-123">Um novo banco de dados é criado.</span><span class="sxs-lookup"><span data-stu-id="9085d-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="9085d-124">Uma nova coleção é criada.</span><span class="sxs-lookup"><span data-stu-id="9085d-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="9085d-125">Alguns documentos são criados.</span><span class="sxs-lookup"><span data-stu-id="9085d-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="9085d-126">Uma consulta SQL no JSON é executada.</span><span class="sxs-lookup"><span data-stu-id="9085d-126">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="9085d-127">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="9085d-127">Update your connection string</span></span>

<span data-ttu-id="9085d-128">Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9085d-128">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="9085d-129">Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**.</span><span class="sxs-lookup"><span data-stu-id="9085d-129">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="9085d-130">Você usará botões de cópia de saudação na direita de saudação do hello toocopy da tela hello URI e a chave primária em Olá `config.js` arquivo na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="9085d-130">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `config.js` file in hello next step.</span></span>

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="9085d-132">Em aberto Olá `config.js` arquivo.</span><span class="sxs-lookup"><span data-stu-id="9085d-132">In Open hello `config.js` file.</span></span> 

3. <span data-ttu-id="9085d-133">Copie o valor URI do portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá o valor da chave do ponto de extremidade Olá no `config.js`.</span><span class="sxs-lookup"><span data-stu-id="9085d-133">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="9085d-134">Em seguida, copie o valor de chave primária do portal de saudação e torná-lo Olá valor Olá `config.primaryKey` em `config.js`.</span><span class="sxs-lookup"><span data-stu-id="9085d-134">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="9085d-135">Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9085d-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="9085d-136">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="9085d-136">Run hello app</span></span>
1. <span data-ttu-id="9085d-137">Executar `npm install` em um terminal tooinstall necessário módulos npm</span><span class="sxs-lookup"><span data-stu-id="9085d-137">Run `npm install` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="9085d-138">Executar `node app.js` em um terminal toostart seu aplicativo de nó.</span><span class="sxs-lookup"><span data-stu-id="9085d-138">Run `node app.js` in a terminal toostart your node application.</span></span>

<span data-ttu-id="9085d-139">Agora você pode voltar tooData Explorer e consulte a consulta, modificar e trabalhar com esses novos dados.</span><span class="sxs-lookup"><span data-stu-id="9085d-139">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="9085d-140">Examine os SLAs em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9085d-140">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="9085d-141">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="9085d-141">Clean up resources</span></span>

<span data-ttu-id="9085d-142">Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9085d-142">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="9085d-143">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="9085d-143">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="9085d-144">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="9085d-144">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9085d-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9085d-145">Next steps</span></span>

<span data-ttu-id="9085d-146">Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, crie uma coleção usando Olá Explorador de dados e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9085d-146">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="9085d-147">Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="9085d-147">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="9085d-148">Importar dados no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9085d-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


