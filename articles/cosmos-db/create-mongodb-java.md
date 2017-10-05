---
title: 'BD Cosmos do Azure: compilar um aplicativo de console com Java e a API do MongoDB | Microsoft Docs'
description: "Apresenta um exemplo de código Java que pode ser usado para se conectar à API do MongoDB do BD Cosmos do Azure e consultá-la"
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
ms.openlocfilehash: f84294d7d324f094d173f7a2ec89759266a74210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-the-azure-portal"></a><span data-ttu-id="284c1-103">BD Cosmos do Azure: compilar um aplicativo de console da API do MongoDB com Java e o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="284c1-103">Azure Cosmos DB: Build a MongoDB API console app with Java and the Azure portal</span></span>

<span data-ttu-id="284c1-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="284c1-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="284c1-105">É possível criar e consultar rapidamente documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="284c1-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="284c1-106">Este início rápido demonstra como criar uma conta do BD Cosmos do Azure, um banco de dados de documento e uma coleção usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="284c1-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="284c1-107">Você compilará e implantará um aplicativo de console compilado no [driver MongoDB Java](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="284c1-107">You'll then build and deploy a console app built on the [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="284c1-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="284c1-108">Prerequisites</span></span>

* <span data-ttu-id="284c1-109">Antes que possa executar esta amostra, você deverá ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="284c1-109">Before you can run this sample, you must have the following prerequisites:</span></span>
   * <span data-ttu-id="284c1-110">JDK 1.7 + (execute `apt-get install default-jdk` se você não tiver o JDK)</span><span class="sxs-lookup"><span data-stu-id="284c1-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="284c1-111">Maven (execute `apt-get install maven` se você não tiver o Maven)</span><span class="sxs-lookup"><span data-stu-id="284c1-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="284c1-112">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="284c1-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="284c1-113">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="284c1-113">Add a collection</span></span>

<span data-ttu-id="284c1-114">Nomeie o novo banco de dados, **db** e sua nova coleção, **coll**.</span><span class="sxs-lookup"><span data-stu-id="284c1-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="284c1-115">Clonar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="284c1-115">Clone the sample application</span></span>

<span data-ttu-id="284c1-116">Agora, clonaremos um aplicativo de API do MongoDB do GitHub, definiremos a cadeia de conexão e o executaremos.</span><span class="sxs-lookup"><span data-stu-id="284c1-116">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="284c1-117">Você verá como é fácil trabalhar usando dados de forma programática.</span><span class="sxs-lookup"><span data-stu-id="284c1-117">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="284c1-118">Abra uma janela de terminal do Git, como git bash, e `cd` para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="284c1-118">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="284c1-119">Execute o comando a seguir para clonar o repositório de exemplo.</span><span class="sxs-lookup"><span data-stu-id="284c1-119">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="284c1-120">Em seguida, abra o arquivo da solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="284c1-120">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="284c1-121">Examine o código</span><span class="sxs-lookup"><span data-stu-id="284c1-121">Review the code</span></span>

<span data-ttu-id="284c1-122">Façamos uma rápida análise do que está acontecendo no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="284c1-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="284c1-123">Abra o arquivo `Program.cs` e você verá que essas linhas de código criam os recursos do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="284c1-123">Open the `Program.cs` file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="284c1-124">O DocumentClient é inicializado.</span><span class="sxs-lookup"><span data-stu-id="284c1-124">The DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="284c1-125">Um novo banco de dados e uma nova coleção são criados.</span><span class="sxs-lookup"><span data-stu-id="284c1-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="284c1-126">Alguns documentos são inseridos usando `MongoCollection.insertOne`</span><span class="sxs-lookup"><span data-stu-id="284c1-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="284c1-127">Algumas consultas são executadas usando `MongoCollection.find`</span><span class="sxs-lookup"><span data-stu-id="284c1-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="284c1-128">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="284c1-128">Update your connection string</span></span>

<span data-ttu-id="284c1-129">Agora, volte ao Portal do Azure para obter informações sobre a cadeia de conexão e copiá-las para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="284c1-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="284c1-130">Da conta, selecione **Início Rápido**, selecione Java e copie a cadeia de conexão para a área de transferência</span><span class="sxs-lookup"><span data-stu-id="284c1-130">From the Account, select **Quick Start**, select Java, then copy the connection string to your clipboard</span></span>

2. <span data-ttu-id="284c1-131">Abra o arquivo `Program.java`, substitua o argumento para o construtor MongoClientURI pela cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="284c1-131">Open the `Program.java` file, replace the argument to the MongoClientURI constructor with the connection string.</span></span> <span data-ttu-id="284c1-132">Agora, você atualizou o aplicativo com todas as informações necessárias para se comunicar com o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="284c1-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-console-app"></a><span data-ttu-id="284c1-133">Execute o aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="284c1-133">Run the console app</span></span>

1. <span data-ttu-id="284c1-134">Executar `mvn package` em um terminal para instalar os módulos npm necessários</span><span class="sxs-lookup"><span data-stu-id="284c1-134">Run `mvn package` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="284c1-135">Execute `mvn exec:java -D exec.mainClass=GetStarted.Program` em um terminal para iniciar o aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="284c1-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal to start your Java application.</span></span>

<span data-ttu-id="284c1-136">Agora você pode usar [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) para consultar, modificar e trabalhar com esses novos dados.</span><span class="sxs-lookup"><span data-stu-id="284c1-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) to query, modify, and work with this new data.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="284c1-137">Examinar SLAs no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="284c1-137">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="284c1-138">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="284c1-138">Clean up resources</span></span>

<span data-ttu-id="284c1-139">Se você não continuar usando este aplicativo, exclua todos os recursos criados por esse início rápido no portal do Azure com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="284c1-139">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="284c1-140">No menu à esquerda no Portal do Azure, clique em **Grupos de recursos** e depois clique no nome do recurso criado.</span><span class="sxs-lookup"><span data-stu-id="284c1-140">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="284c1-141">Em sua página de grupo de recursos, clique em **Excluir**, digite o nome do recurso para excluir na caixa de texto e depois clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="284c1-141">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="284c1-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="284c1-142">Next steps</span></span>

<span data-ttu-id="284c1-143">Neste início rápido, você aprendeu como criar uma conta do BD Cosmos do Azure, como criar uma coleção usando o Data Explorer e como executar um aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="284c1-143">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a console app.</span></span> <span data-ttu-id="284c1-144">Agora, é possível importar outros dados para sua conta do BD Cosmos.</span><span class="sxs-lookup"><span data-stu-id="284c1-144">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="284c1-145">Importar dados do MongoDB no BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="284c1-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


