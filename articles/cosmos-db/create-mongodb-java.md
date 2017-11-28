---
title: "Cosmos do Azure DB: Criar um aplicativo de console com o Java e Olá MongoDB API | Microsoft Docs"
description: "Apresenta um exemplo de código de Java que você pode usar tooconnect tooand consulta hello Azure Cosmos DB MongoDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a><span data-ttu-id="7859b-103">Banco de dados do Azure do Cosmos: Criar um aplicativo de console do MongoDB API com Java e Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7859b-103">Azure Cosmos DB: Build a MongoDB API console app with Java and hello Azure portal</span></span>

<span data-ttu-id="7859b-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7859b-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="7859b-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="7859b-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="7859b-106">Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7859b-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="7859b-107">Você, em seguida, criar e implantar um aplicativo de console criado em Olá [driver MongoDB Java](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="7859b-107">You'll then build and deploy a console app built on hello [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7859b-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7859b-108">Prerequisites</span></span>

* <span data-ttu-id="7859b-109">Antes de executar este exemplo, você deve ter Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7859b-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
   * <span data-ttu-id="7859b-110">JDK 1.7 + (execute `apt-get install default-jdk` se você não tiver o JDK)</span><span class="sxs-lookup"><span data-stu-id="7859b-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="7859b-111">Maven (execute `apt-get install maven` se você não tiver o Maven)</span><span class="sxs-lookup"><span data-stu-id="7859b-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="7859b-112">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="7859b-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="7859b-113">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="7859b-113">Add a collection</span></span>

<span data-ttu-id="7859b-114">Nomeie o novo banco de dados, **db** e sua nova coleção, **coll**.</span><span class="sxs-lookup"><span data-stu-id="7859b-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="7859b-115">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="7859b-115">Clone hello sample application</span></span>

<span data-ttu-id="7859b-116">Agora vamos clone uma API do MongoDB aplicativo do github, defina a cadeia de caracteres de conexão hello e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="7859b-116">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="7859b-117">Você verá como é fácil toowork com dados programaticamente.</span><span class="sxs-lookup"><span data-stu-id="7859b-117">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="7859b-118">Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7859b-118">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="7859b-119">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="7859b-119">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="7859b-120">Em seguida, abra o arquivo de solução de saudação no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7859b-120">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="7859b-121">Examine o código de saudação</span><span class="sxs-lookup"><span data-stu-id="7859b-121">Review hello code</span></span>

<span data-ttu-id="7859b-122">Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7859b-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="7859b-123">Olá abrir `Program.cs` de arquivo e você descobrirá que essas linhas de código criam Olá recursos de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7859b-123">Open hello `Program.cs` file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="7859b-124">Olá DocumentClient é inicializado.</span><span class="sxs-lookup"><span data-stu-id="7859b-124">hello DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="7859b-125">Um novo banco de dados e uma nova coleção são criados.</span><span class="sxs-lookup"><span data-stu-id="7859b-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="7859b-126">Alguns documentos são inseridos usando `MongoCollection.insertOne`</span><span class="sxs-lookup"><span data-stu-id="7859b-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="7859b-127">Algumas consultas são executadas usando `MongoCollection.find`</span><span class="sxs-lookup"><span data-stu-id="7859b-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="7859b-128">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="7859b-128">Update your connection string</span></span>

<span data-ttu-id="7859b-129">Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7859b-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="7859b-130">Olá conta, selecione **início rápido**, selecione o Java e copie a área de transferência tooyour cadeia de caracteres de conexão de saudação</span><span class="sxs-lookup"><span data-stu-id="7859b-130">From hello Account, select **Quick Start**, select Java, then copy hello connection string tooyour clipboard</span></span>

2. <span data-ttu-id="7859b-131">Olá abrir `Program.java` de arquivo, substitua o construtor do hello argumento toohello MongoClientURI com a cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="7859b-131">Open hello `Program.java` file, replace hello argument toohello MongoClientURI constructor with hello connection string.</span></span> <span data-ttu-id="7859b-132">Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7859b-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-console-app"></a><span data-ttu-id="7859b-133">Execute o aplicativo de console Olá</span><span class="sxs-lookup"><span data-stu-id="7859b-133">Run hello console app</span></span>

1. <span data-ttu-id="7859b-134">Executar `mvn package` em um terminal tooinstall necessário módulos npm</span><span class="sxs-lookup"><span data-stu-id="7859b-134">Run `mvn package` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="7859b-135">Executar `mvn exec:java -D exec.mainClass=GetStarted.Program` em um terminal toostart seu aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="7859b-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal toostart your Java application.</span></span>

<span data-ttu-id="7859b-136">Agora você pode usar [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modificar e trabalhar com esses novos dados.</span><span class="sxs-lookup"><span data-stu-id="7859b-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modify, and work with this new data.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="7859b-137">Examine os SLAs em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7859b-137">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="7859b-138">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="7859b-138">Clean up resources</span></span>

<span data-ttu-id="7859b-139">Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7859b-139">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="7859b-140">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="7859b-140">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="7859b-141">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="7859b-141">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7859b-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7859b-142">Next steps</span></span>

<span data-ttu-id="7859b-143">Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, criar uma coleção usando Olá Explorador de dados e executar um aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="7859b-143">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a console app.</span></span> <span data-ttu-id="7859b-144">Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="7859b-144">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7859b-145">Importar dados do MongoDB no BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="7859b-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


