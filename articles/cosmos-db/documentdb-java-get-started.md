---
title: 'Tutorial de NoSQL: API do DocumentDB para o SDK Java do Azure Cosmos DB | Microsoft Docs'
description: "Um tutorial do NoSQL que cria um banco de dados online e um aplicativo de console Java usando a API do DocumentDB para o Azure Cosmos DB. O Azure DocumentDB é um banco de dados NoSQL para JSON."
keywords: tutorial do nosql, banco de dados online, aplicativo de console java
services: cosmos-db
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/22/2017
ms.author: arramac
ms.openlocfilehash: 5c4bcda308f001572e1c34e991616fc209250a02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="86951-105">Tutorial do NoSQL: criar um aplicativo de console em Java da API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="86951-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="86951-106">.NET</span><span class="sxs-lookup"><span data-stu-id="86951-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="86951-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="86951-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="86951-108">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="86951-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="86951-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="86951-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="86951-110">Java</span><span class="sxs-lookup"><span data-stu-id="86951-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="86951-111">C++</span><span class="sxs-lookup"><span data-stu-id="86951-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="86951-112">Bem-vindo ao tutorial do NoSQL para a API do DocumentDB para o SDK Java do Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="86951-112">Welcome to the NoSQL tutorial for the DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="86951-113">Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="86951-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="86951-114">Abordamos:</span><span class="sxs-lookup"><span data-stu-id="86951-114">We cover:</span></span>

* <span data-ttu-id="86951-115">Criar e conectar-se a uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="86951-115">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="86951-116">Configurar a sua Solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86951-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="86951-117">Criando um banco de dados online</span><span class="sxs-lookup"><span data-stu-id="86951-117">Creating an online database</span></span>
* <span data-ttu-id="86951-118">Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="86951-118">Creating a collection</span></span>
* <span data-ttu-id="86951-119">Criando documentos JSON</span><span class="sxs-lookup"><span data-stu-id="86951-119">Creating JSON documents</span></span>
* <span data-ttu-id="86951-120">Consultar a coleção</span><span class="sxs-lookup"><span data-stu-id="86951-120">Querying the collection</span></span>
* <span data-ttu-id="86951-121">Criando documentos JSON</span><span class="sxs-lookup"><span data-stu-id="86951-121">Creating JSON documents</span></span>
* <span data-ttu-id="86951-122">Consultar a coleção</span><span class="sxs-lookup"><span data-stu-id="86951-122">Querying the collection</span></span>
* <span data-ttu-id="86951-123">Substituição de um documento</span><span class="sxs-lookup"><span data-stu-id="86951-123">Replacing a document</span></span>
* <span data-ttu-id="86951-124">Exclusão de um documento</span><span class="sxs-lookup"><span data-stu-id="86951-124">Deleting a document</span></span>
* <span data-ttu-id="86951-125">Excluir o banco de dados</span><span class="sxs-lookup"><span data-stu-id="86951-125">Deleting the database</span></span>

<span data-ttu-id="86951-126">Agora vamos começar!</span><span class="sxs-lookup"><span data-stu-id="86951-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86951-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="86951-127">Prerequisites</span></span>
<span data-ttu-id="86951-128">Verifique se você tem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="86951-128">Make sure you have the following:</span></span>

* <span data-ttu-id="86951-129">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="86951-129">An active Azure account.</span></span> <span data-ttu-id="86951-130">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="86951-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="86951-131">Como alternativa, você pode usar o [Emulador do Azure Cosmos DB](local-emulator.md) neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="86951-131">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="86951-132">Git</span><span class="sxs-lookup"><span data-stu-id="86951-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="86951-133">[Java Development Kit (JDK) 7 +](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="86951-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="86951-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="86951-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="86951-135">Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="86951-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="86951-136">Vamos criar uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="86951-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="86951-137">Se você já tiver uma conta que deseja usar, poderá pular para [Clonar o projeto do GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="86951-137">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span></span> <span data-ttu-id="86951-138">Se você estiver usando o Emulador do Azure Cosmos DB, siga as etapas no [Emulador do Azure Cosmos DB](local-emulator.md) para configurar o emulador e pular para [Clonar o projeto do GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="86951-138">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="86951-139"><a id="GitClone"></a>Etapa 2: Clonar o projeto do GitHub</span><span class="sxs-lookup"><span data-stu-id="86951-139"><a id="GitClone"></a>Step 2: Clone the GitHub project</span></span>
<span data-ttu-id="86951-140">Você pode começar clonando o repositório do GitHub para a [Introdução ao Azure Cosmos DB e Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="86951-140">You can get started by cloning the GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="86951-141">Por exemplo, de um diretório local, execute o seguinte para recuperar o projeto de exemplo localmente.</span><span class="sxs-lookup"><span data-stu-id="86951-141">For example, from a local directory run the following to retrieve the sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="86951-142">O diretório contém um `pom.xml` para o projeto e uma pasta `src` que contém o código-fonte em Java incluindo `Program.java`, que mostra como executar operações simples com o Azure Cosmos DB, como criação de documentos e consulta de dados em uma coleção.</span><span class="sxs-lookup"><span data-stu-id="86951-142">The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="86951-143">O `pom.xml` inclui uma dependência no [SDK do Java do DocumentDB no Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="86951-143">The `pom.xml` includes a dependency on the [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="86951-144"><a id="Connect"></a>Etapa 3: Conectar-se a uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="86951-144"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="86951-145">Em seguida, retorne ao [Portal do Azure](https://portal.azure.com) para recuperar o ponto de extremidade e a chave mestra primária.</span><span class="sxs-lookup"><span data-stu-id="86951-145">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span></span> <span data-ttu-id="86951-146">O ponto de extremidade e a chave primária do Azure Cosmos DB são necessários para que seu aplicativo reconheça onde deve se conectar e para que o Azure Cosmos DB confie na conexão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="86951-146">The Azure Cosmos DB endpoint and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="86951-147">No Portal do Azure, navegue até sua conta do Azure Cosmos DB e clique em **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="86951-147">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="86951-148">Copie o URI do portal e cole-o em `https://FILLME.documents.azure.com` no arquivo Program.java.</span><span class="sxs-lookup"><span data-stu-id="86951-148">Copy the URI from the portal and paste it into `https://FILLME.documents.azure.com` in the Program.java file.</span></span> <span data-ttu-id="86951-149">Em seguida, copie a CHAVE PRIMÁRIA do portal e cole-a em `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="86951-149">Then copy the PRIMARY KEY from the portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Captura de tela do Portal do Azure usado pelo tutorial do NoSQL para criar um aplicativo de console em Java.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="86951-152">Etapa 4: criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="86951-152">Step 4: Create a database</span></span>
<span data-ttu-id="86951-153">Seu [banco de dados](documentdb-resources.md#databases) do Azure Cosmos DB pode ser criado usando o método [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) da classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="86951-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of the **DocumentClient** class.</span></span> <span data-ttu-id="86951-154">Um banco de dados é o contêiner lógico de armazenamento de documentos JSON particionado em coleções.</span><span class="sxs-lookup"><span data-stu-id="86951-154">A database is the logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="86951-155"><a id="CreateColl"></a>Etapa 5: Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="86951-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="86951-156">**createCollection** criará uma nova coleção com uma taxa de transferência reservada, que tem implicações de preço.</span><span class="sxs-lookup"><span data-stu-id="86951-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="86951-157">Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="86951-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="86951-158">Uma [coleção](documentdb-resources.md#collections) pode ser criada usando o método [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) da classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="86951-158">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of the **DocumentClient** class.</span></span> <span data-ttu-id="86951-159">Uma coleção é um contêiner de documentos JSON e uma lógica de aplicativo JavaScript associada.</span><span class="sxs-lookup"><span data-stu-id="86951-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="86951-160"><a id="CreateDoc"></a>Etapa 6: Criar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="86951-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="86951-161">Um [documento](documentdb-resources.md#documents) pode ser criado usando o método [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) da classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="86951-161">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of the **DocumentClient** class.</span></span> <span data-ttu-id="86951-162">Os documentos são conteúdo JSON (arbitrário) definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="86951-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="86951-163">Agora podemos inserir um ou mais documentos.</span><span class="sxs-lookup"><span data-stu-id="86951-163">We can now insert one or more documents.</span></span> <span data-ttu-id="86951-164">Se já tiver dados que deseje armazenar no banco de dados, você poderá usar a [ferramenta de migração de dados](import-data.md) do Azure Cosmos DB para importar os dados para um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="86951-164">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) to import the data into a database.</span></span>

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![Diagrama que ilustra a relação hierárquica entre a conta, o banco de dados online, a coleção e os documentos usados pelo tutorial do NoSQL para criar um aplicativo de console em Java](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="86951-166"><a id="Query"></a>Etapa 7: Consultar recursos do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="86951-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="86951-167">O Azure Cosmos DB tem suporte para [consultas](documentdb-sql-query.md) avançadas de documentos JSON armazenados em cada coleção.</span><span class="sxs-lookup"><span data-stu-id="86951-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="86951-168">O código de exemplo a seguir mostra como consultar documentos no Azure Cosmos DB usando a sintaxe SQL com o método [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments).</span><span class="sxs-lookup"><span data-stu-id="86951-168">The following sample code shows how to query documents in Azure Cosmos DB using SQL syntax with the [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="86951-169"><a id="ReplaceDocument"></a>Etapa 8: substituir o documento JSON</span><span class="sxs-lookup"><span data-stu-id="86951-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="86951-170">O Azure Cosmos DB dá suporte à atualização de documentos JSON usando o método [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument).</span><span class="sxs-lookup"><span data-stu-id="86951-170">Azure Cosmos DB supports updating JSON documents using the [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="86951-171"><a id="DeleteDocument"></a>Etapa 9: excluir o documento JSON</span><span class="sxs-lookup"><span data-stu-id="86951-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="86951-172">Da mesma forma, o Azure Cosmos DB dá suporte à exclusão de documentos JSON usando o método [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument).</span><span class="sxs-lookup"><span data-stu-id="86951-172">Similarly, Azure Cosmos DB supports deleting JSON documents using the [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="86951-173"><a id="DeleteDatabase"></a>Etapa 10: excluir o banco de dados</span><span class="sxs-lookup"><span data-stu-id="86951-173"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="86951-174">Excluir o banco de dados criado remove o banco de dados e todos os recursos filhos (coleções, documentos etc.).</span><span class="sxs-lookup"><span data-stu-id="86951-174">Deleting the created database removes the database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="86951-175"><a id="Run"></a>Etapa 11: Executar o aplicativo de console Java inteiro!</span><span class="sxs-lookup"><span data-stu-id="86951-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="86951-176">Para executar o aplicativo de console, navegue até a pasta de projeto e compile usando o Maven:</span><span class="sxs-lookup"><span data-stu-id="86951-176">To run the application from the console, navigate to the project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="86951-177">A execução de `mvn package` baixa a biblioteca mais recente do Azure Cosmos DB do Maven e produz `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="86951-177">Running `mvn package` downloads the latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="86951-178">Em seguida, execute o aplicativo por meio de:</span><span class="sxs-lookup"><span data-stu-id="86951-178">Then run the app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="86951-179">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="86951-179">Congratulations!</span></span> <span data-ttu-id="86951-180">Você concluiu este tutorial do NoSQL e tem um aplicativo de console em Java funcional!</span><span class="sxs-lookup"><span data-stu-id="86951-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="86951-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86951-181">Next steps</span></span>
* <span data-ttu-id="86951-182">Quer um tutorial do aplicativo Web Java?</span><span class="sxs-lookup"><span data-stu-id="86951-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="86951-183">Veja [Criar um aplicativo Web com Java usando o Azure Cosmos DB](documentdb-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="86951-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="86951-184">Saiba como [monitorar uma conta do Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="86951-184">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="86951-185">Executar consultas em nosso conjunto de dados de exemplo no [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="86951-185">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="86951-186">Saiba mais sobre o modelo de programação na seção Desenvolvimento da [página de documentação do Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="86951-186">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
