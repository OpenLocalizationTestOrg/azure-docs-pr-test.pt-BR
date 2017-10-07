---
title: 'Tutorial de NoSQL: API do DocumentDB para o SDK Java do Azure Cosmos DB | Microsoft Docs'
description: "Um tutorial NoSQL que cria um banco de dados online e o aplicativo de console de Java usando Olá API DocumentDB para o banco de dados do Azure Cosmos. O Azure DocumentDB é um banco de dados NoSQL para JSON."
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
ms.openlocfilehash: 1a298a15ab911d140b9df30ad52cfe0fa07c55b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="221ab-105">Tutorial do NoSQL: criar um aplicativo de console em Java da API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="221ab-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="221ab-106">.NET</span><span class="sxs-lookup"><span data-stu-id="221ab-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="221ab-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="221ab-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="221ab-108">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="221ab-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="221ab-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="221ab-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="221ab-110">Java</span><span class="sxs-lookup"><span data-stu-id="221ab-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="221ab-111">C++</span><span class="sxs-lookup"><span data-stu-id="221ab-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="221ab-112">Bem-vindo toohello NoSQL tutorial para Olá DocumentDB API do SDK de Java do Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="221ab-112">Welcome toohello NoSQL tutorial for hello DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="221ab-113">Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="221ab-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="221ab-114">Abordamos:</span><span class="sxs-lookup"><span data-stu-id="221ab-114">We cover:</span></span>

* <span data-ttu-id="221ab-115">Criar e conectar-se a conta de banco de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="221ab-115">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="221ab-116">Configurar a sua Solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="221ab-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="221ab-117">Criando um banco de dados online</span><span class="sxs-lookup"><span data-stu-id="221ab-117">Creating an online database</span></span>
* <span data-ttu-id="221ab-118">Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="221ab-118">Creating a collection</span></span>
* <span data-ttu-id="221ab-119">Criando documentos JSON</span><span class="sxs-lookup"><span data-stu-id="221ab-119">Creating JSON documents</span></span>
* <span data-ttu-id="221ab-120">Consultando Olá coleção</span><span class="sxs-lookup"><span data-stu-id="221ab-120">Querying hello collection</span></span>
* <span data-ttu-id="221ab-121">Criando documentos JSON</span><span class="sxs-lookup"><span data-stu-id="221ab-121">Creating JSON documents</span></span>
* <span data-ttu-id="221ab-122">Consultando Olá coleção</span><span class="sxs-lookup"><span data-stu-id="221ab-122">Querying hello collection</span></span>
* <span data-ttu-id="221ab-123">Substituição de um documento</span><span class="sxs-lookup"><span data-stu-id="221ab-123">Replacing a document</span></span>
* <span data-ttu-id="221ab-124">Exclusão de um documento</span><span class="sxs-lookup"><span data-stu-id="221ab-124">Deleting a document</span></span>
* <span data-ttu-id="221ab-125">Excluir banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="221ab-125">Deleting hello database</span></span>

<span data-ttu-id="221ab-126">Agora vamos começar!</span><span class="sxs-lookup"><span data-stu-id="221ab-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="221ab-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="221ab-127">Prerequisites</span></span>
<span data-ttu-id="221ab-128">Verifique se que você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="221ab-128">Make sure you have hello following:</span></span>

* <span data-ttu-id="221ab-129">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="221ab-129">An active Azure account.</span></span> <span data-ttu-id="221ab-130">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="221ab-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="221ab-131">Como alternativa, você pode usar o hello [emulador de banco de dados do Azure Cosmos](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="221ab-131">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="221ab-132">Git</span><span class="sxs-lookup"><span data-stu-id="221ab-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="221ab-133">[Java Development Kit (JDK) 7 +](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="221ab-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="221ab-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="221ab-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="221ab-135">Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="221ab-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="221ab-136">Vamos criar uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="221ab-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="221ab-137">Se você já tiver uma conta que você deseja toouse, poderá pular muito[projeto do Clone Olá GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="221ab-137">If you already have an account you want toouse, you can skip ahead too[Clone hello GitHub project](#GitClone).</span></span> <span data-ttu-id="221ab-138">Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) tooset backup emulador hello e pular muito[projeto do Clone Olá GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="221ab-138">If you are using hello Azure Cosmos DB Emulator, follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) tooset up hello emulator and skip ahead too[Clone hello GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="221ab-139"><a id="GitClone"></a>Etapa 2: Clonar o projeto do GitHub Olá</span><span class="sxs-lookup"><span data-stu-id="221ab-139"><a id="GitClone"></a>Step 2: Clone hello GitHub project</span></span>
<span data-ttu-id="221ab-140">Você pode começar pela clonagem de repositório do GitHub Olá para [começar a usar o banco de dados do Azure Cosmos e Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="221ab-140">You can get started by cloning hello GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="221ab-141">Por exemplo, um diretório local execute Olá seguindo o projeto de exemplo de hello tooretrieve localmente.</span><span class="sxs-lookup"><span data-stu-id="221ab-141">For example, from a local directory run hello following tooretrieve hello sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="221ab-142">Olá diretório contém um `pom.xml` para projeto hello e um `src` pasta que contém o código de origem de Java incluindo `Program.java` que mostra como executar operações simples com o banco de dados do Azure Cosmos como criação de documentos e consultar dados dentro de um coleção.</span><span class="sxs-lookup"><span data-stu-id="221ab-142">hello directory contains a `pom.xml` for hello project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="221ab-143">Olá `pom.xml` inclui uma dependência no hello [SDK de Java do DocumentDB em Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="221ab-143">hello `pom.xml` includes a dependency on hello [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="221ab-144"><a id="Connect"></a>Etapa 3: Conectar-se a conta de banco de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="221ab-144"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="221ab-145">Em seguida, head fazer toohello [Portal do Azure](https://portal.azure.com) tooretrieve seu ponto de extremidade e a chave primária do mestre.</span><span class="sxs-lookup"><span data-stu-id="221ab-145">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint and primary master key.</span></span> <span data-ttu-id="221ab-146">Hello Azure Cosmos DB de ponto de extremidade e a chave primária são necessárias para seu aplicativo toounderstand onde tooconnect e para o banco de dados do Azure Cosmos tootrust conexão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="221ab-146">hello Azure Cosmos DB endpoint and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="221ab-147">Olá Portal do Azure, navegue conta de banco de dados do Azure Cosmos tooyour e, em seguida, clique no **chaves**.</span><span class="sxs-lookup"><span data-stu-id="221ab-147">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="221ab-148">Copie Olá URI do portal hello e cole-o na `https://FILLME.documents.azure.com` no arquivo de Program.java hello.</span><span class="sxs-lookup"><span data-stu-id="221ab-148">Copy hello URI from hello portal and paste it into `https://FILLME.documents.azure.com` in hello Program.java file.</span></span> <span data-ttu-id="221ab-149">Cópia Olá chave primária do portal hello e cole-o na `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="221ab-149">Then copy hello PRIMARY KEY from hello portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Captura de tela de saudação Portal do Azure usado pelo Olá NoSQL tutorial toocreate um aplicativo de console de Java.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="221ab-152">Etapa 4: criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="221ab-152">Step 4: Create a database</span></span>
<span data-ttu-id="221ab-153">O banco de dados do Azure Cosmos [banco de dados](documentdb-resources.md#databases) podem ser criados usando Olá [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) método hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="221ab-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="221ab-154">Um banco de dados é um contêiner lógico de saudação do armazenamento de documentos JSON particionado em coleções.</span><span class="sxs-lookup"><span data-stu-id="221ab-154">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="221ab-155"><a id="CreateColl"></a>Etapa 5: Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="221ab-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="221ab-156">**createCollection** criará uma nova coleção com uma taxa de transferência reservada, que tem implicações de preço.</span><span class="sxs-lookup"><span data-stu-id="221ab-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="221ab-157">Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="221ab-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="221ab-158">Um [coleção](documentdb-resources.md#collections) podem ser criados usando Olá [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) método hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="221ab-158">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="221ab-159">Uma coleção é um contêiner de documentos JSON e uma lógica de aplicativo JavaScript associada.</span><span class="sxs-lookup"><span data-stu-id="221ab-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="221ab-160"><a id="CreateDoc"></a>Etapa 6: Criar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="221ab-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="221ab-161">Um [documento](documentdb-resources.md#documents) podem ser criados usando Olá [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) método hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="221ab-161">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="221ab-162">Os documentos são conteúdo JSON (arbitrário) definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="221ab-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="221ab-163">Agora podemos inserir um ou mais documentos.</span><span class="sxs-lookup"><span data-stu-id="221ab-163">We can now insert one or more documents.</span></span> <span data-ttu-id="221ab-164">Se você já tiver dados você gostaria que toostore no banco de dados, você pode usar o Azure Cosmos DB [ferramenta de migração de dados](import-data.md) tooimport dados de saudação em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="221ab-164">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

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

![Diagrama ilustrando uma relação hierárquica Olá entre conta Olá, banco de dados online Olá, coleção hello e documentos Olá usados pelo Olá NoSQL tutorial toocreate um aplicativo de console do Java](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="221ab-166"><a id="Query"></a>Etapa 7: Consultar recursos do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="221ab-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="221ab-167">O Azure Cosmos DB tem suporte para [consultas](documentdb-sql-query.md) avançadas de documentos JSON armazenados em cada coleção.</span><span class="sxs-lookup"><span data-stu-id="221ab-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="221ab-168">Olá, código de exemplo a seguir mostra como tooquery documentos no banco de dados do Azure Cosmos usando a sintaxe SQL com hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) método.</span><span class="sxs-lookup"><span data-stu-id="221ab-168">hello following sample code shows how tooquery documents in Azure Cosmos DB using SQL syntax with hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="221ab-169"><a id="ReplaceDocument"></a>Etapa 8: substituir o documento JSON</span><span class="sxs-lookup"><span data-stu-id="221ab-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="221ab-170">Banco de dados do Azure Cosmos dá suporte à atualização documentos JSON usando Olá [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) método.</span><span class="sxs-lookup"><span data-stu-id="221ab-170">Azure Cosmos DB supports updating JSON documents using hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="221ab-171"><a id="DeleteDocument"></a>Etapa 9: excluir o documento JSON</span><span class="sxs-lookup"><span data-stu-id="221ab-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="221ab-172">Da mesma forma, o banco de dados do Azure Cosmos dá suporte a excluir documentos JSON usando Olá [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) método.</span><span class="sxs-lookup"><span data-stu-id="221ab-172">Similarly, Azure Cosmos DB supports deleting JSON documents using hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="221ab-173"><a id="DeleteDatabase"></a>Etapa 10: Excluir o banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="221ab-173"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="221ab-174">Banco de dados excluindo Olá criado remove o banco de dados de saudação e todos os recursos de filhos (coleções, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="221ab-174">Deleting hello created database removes hello database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="221ab-175"><a id="Run"></a>Etapa 11: Executar o aplicativo de console Java inteiro!</span><span class="sxs-lookup"><span data-stu-id="221ab-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="221ab-176">aplicativo de hello toorun Olá no console do, navegue toohello a pasta do projeto e compilar usando Maven:</span><span class="sxs-lookup"><span data-stu-id="221ab-176">toorun hello application from hello console, navigate toohello project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="221ab-177">Executando `mvn package` baixa a biblioteca de banco de dados do Azure Cosmos mais recente de saudação do Maven e produz `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="221ab-177">Running `mvn package` downloads hello latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="221ab-178">Em seguida, execute o aplicativo hello executando:</span><span class="sxs-lookup"><span data-stu-id="221ab-178">Then run hello app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="221ab-179">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="221ab-179">Congratulations!</span></span> <span data-ttu-id="221ab-180">Você concluiu este tutorial do NoSQL e tem um aplicativo de console em Java funcional!</span><span class="sxs-lookup"><span data-stu-id="221ab-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="221ab-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="221ab-181">Next steps</span></span>
* <span data-ttu-id="221ab-182">Quer um tutorial do aplicativo Web Java?</span><span class="sxs-lookup"><span data-stu-id="221ab-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="221ab-183">Veja [Criar um aplicativo Web com Java usando o Azure Cosmos DB](documentdb-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="221ab-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="221ab-184">Saiba como muito[monitorar uma conta de banco de dados do Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="221ab-184">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="221ab-185">Executar consultas em nosso conjunto de dados de exemplo hello [parque de consulta](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="221ab-185">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="221ab-186">Saiba mais sobre o modelo de programação de Olá Olá seção desenvolver de saudação [página de documentação do banco de dados do Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="221ab-186">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
