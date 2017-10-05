---
title: Criar um banco de dados de documentos do Azure Cosmos DB com Java | Microsoft Docs | Microsoft Docs
description: "Apresenta um exemplo de código Java que pode ser usado para se conectar à API do DocumentDB do Azure Cosmos DB e consultá-la"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: df1a25d703a7b8082bdabb4f7d593cb005d416fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-the-azure-portal"></a><span data-ttu-id="89e5b-103">Azure Cosmos DB: Criar um banco de dados de documentos usando o Java e o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="89e5b-103">Azure Cosmos DB: Create a document database using Java and the Azure portal</span></span>

<span data-ttu-id="89e5b-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="89e5b-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="89e5b-105">É possível criar e consultar rapidamente documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e5b-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="89e5b-106">Este início rápido cria um banco de dados de documentos usando as ferramentas do portal do Azure para o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e5b-106">This quickstart creates a document database using the Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="89e5b-107">Este início rápido também mostra como criar rapidamente um aplicativo de console do Java usando a [API Java do DocumentDB](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="89e5b-107">This quickstart also shows you how to quickly create a Java console app using the [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="89e5b-108">As instruções neste guia rápido podem ser seguidas em qualquer sistema operacional capaz de executar o Java.</span><span class="sxs-lookup"><span data-stu-id="89e5b-108">The instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="89e5b-109">Ao concluir este início rápido, você estará familiarizado com a criação e a modificação dos recursos do banco de dados de documentos na IU ou programaticamente, o que for sua preferência.</span><span class="sxs-lookup"><span data-stu-id="89e5b-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either the UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89e5b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="89e5b-110">Prerequisites</span></span>

* [<span data-ttu-id="89e5b-111">Java Development Kit (JDK) 1.7 +</span><span class="sxs-lookup"><span data-stu-id="89e5b-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="89e5b-112">No Ubuntu, execute `apt-get install default-jdk` para instalar o JDK.</span><span class="sxs-lookup"><span data-stu-id="89e5b-112">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="89e5b-113">Defina a variável de ambiente JAVA_HOME para apontar para a pasta onde o JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="89e5b-113">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="89e5b-114">[Baixar](http://maven.apache.org/download.cgi) e [instalar](http://maven.apache.org/install.html) um armazenamento binário [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="89e5b-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="89e5b-115">No Ubuntu, você pode executar `apt-get install maven` para instalar o Maven.</span><span class="sxs-lookup"><span data-stu-id="89e5b-115">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="89e5b-116">Git</span><span class="sxs-lookup"><span data-stu-id="89e5b-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="89e5b-117">No Ubuntu, você pode executar `sudo apt-get install git` para instalar o Git.</span><span class="sxs-lookup"><span data-stu-id="89e5b-117">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="89e5b-118">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="89e5b-118">Create a database account</span></span>

<span data-ttu-id="89e5b-119">Antes de criar um banco de dados de documentos, você precisa criar uma conta do banco de dados SQL (DocumentDB) com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e5b-119">Before you can create a document database, you need to create a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="89e5b-120">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="89e5b-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="89e5b-121">Adicionar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="89e5b-121">Add sample data</span></span>

<span data-ttu-id="89e5b-122">Agora você pode adicionar dados à sua nova coleção usando o Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="89e5b-122">You can now add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="89e5b-123">No Data Explorer, o novo banco de dados aparece no painel Coleções.</span><span class="sxs-lookup"><span data-stu-id="89e5b-123">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="89e5b-124">Expanda o banco de dados **Tarefas**, expanda a coleção **Itens**, clique em **Documentos** e clique em **Novos Documentos**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-124">Expand the **Tasks** database, expand the **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Criar novos documentos no Data Explorer no portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="89e5b-126">Agora, adicione um documento à coleção com a seguinte estrutura.</span><span class="sxs-lookup"><span data-stu-id="89e5b-126">Now add a document to the collection with the following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="89e5b-127">Depois de ter adicionado o json à guia **Documentos**, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-127">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![Copie nos dados json e clique em Salvar no Data Explorer no portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="89e5b-129">Crie e salve mais um documento onde você insere um valor exclusivo para a propriedade `id` e altere as outras propriedades quando achar adequado.</span><span class="sxs-lookup"><span data-stu-id="89e5b-129">Create and save one more document where you insert a unique value for the `id` property, and change the other properties as you see fit.</span></span> <span data-ttu-id="89e5b-130">Os novos documentos podem ter qualquer estrutura que você deseje, pois o Azure Cosmos DB não impõe nenhum esquema para seus dados.</span><span class="sxs-lookup"><span data-stu-id="89e5b-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="89e5b-131">Agora, você pode usar as consultas no Data Explorer para recuperar os dados clicando nos botões **Editar Filtro** e **Aplicar Filtro**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-131">You can now use queries in Data Explorer to retrieve your data by clicking the **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="89e5b-132">Por padrão, o Data Explorer usa `SELECT * FROM c` para recuperar todos os documentos na coleção, mas você pode alterar isso para uma [consulta SQL ](documentdb-sql-query.md) diferente, como `SELECT * FROM c ORDER BY c._ts DESC`, para retornar todos os documentos em ordem descendente com base no carimbo de data/hora.</span><span class="sxs-lookup"><span data-stu-id="89e5b-132">By default, Data Explorer uses `SELECT * FROM c` to retrieve all documents in the collection, but you can change that to a different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, to return all the documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="89e5b-133">Você também pode usar o Data Explorer para criar procedimentos armazenados, UDFs e gatilhos para executar a lógica de negócios do servidor, além de dimensionar a taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="89e5b-133">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="89e5b-134">O Data Explorer expõe todo o acesso a dados interno via programação disponível nas APIs, mas oferece acesso fácil aos dados no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="89e5b-134">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="89e5b-135">Clonar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="89e5b-135">Clone the sample application</span></span>

<span data-ttu-id="89e5b-136">Agora, vamos trabalhar com o código.</span><span class="sxs-lookup"><span data-stu-id="89e5b-136">Now let's switch to working with code.</span></span> <span data-ttu-id="89e5b-137">Vamos clonar um aplicativo de API do DocumentDB do GitHub, definir a cadeia de conexão e executá-la.</span><span class="sxs-lookup"><span data-stu-id="89e5b-137">Let's clone a DocumentDB API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="89e5b-138">Você verá como é fácil trabalhar usando dados de forma programática.</span><span class="sxs-lookup"><span data-stu-id="89e5b-138">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="89e5b-139">Abra uma janela de terminal do Git, como git bash, e `CD` para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="89e5b-139">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="89e5b-140">Execute o comando a seguir para clonar o repositório de exemplo.</span><span class="sxs-lookup"><span data-stu-id="89e5b-140">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="89e5b-141">Examine o código</span><span class="sxs-lookup"><span data-stu-id="89e5b-141">Review the code</span></span>

<span data-ttu-id="89e5b-142">Façamos uma rápida revisão do que está acontecendo no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89e5b-142">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="89e5b-143">Abra o arquivo `Program.java` na pasta \src\GetStarted e encontre estas linhas de código que criam os recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e5b-143">Open the `Program.java` file from the \src\GetStarted folder, and find these lines of code that create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="89e5b-144">O `DocumentClient` é inicializado.</span><span class="sxs-lookup"><span data-stu-id="89e5b-144">The `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="89e5b-145">Um novo banco de dados é criado.</span><span class="sxs-lookup"><span data-stu-id="89e5b-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="89e5b-146">Uma nova coleção é criada.</span><span class="sxs-lookup"><span data-stu-id="89e5b-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="89e5b-147">Alguns documentos são criados.</span><span class="sxs-lookup"><span data-stu-id="89e5b-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written to Azure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="89e5b-148">Uma consulta SQL no JSON é executada.</span><span class="sxs-lookup"><span data-stu-id="89e5b-148">A SQL query over JSON is performed.</span></span>

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="89e5b-149">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="89e5b-149">Update your connection string</span></span>

<span data-ttu-id="89e5b-150">Agora, volte ao portal do Azure para obter informações sobre a cadeia de conexão e copiá-las para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89e5b-150">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="89e5b-151">Isso permitirá que seu aplicativo comunique-se com o banco de dados hospedado.</span><span class="sxs-lookup"><span data-stu-id="89e5b-151">This will enable your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="89e5b-152">No [Portal do Azure](http://portal.azure.com/), na sua conta do Azure Cosmos DB, no painel de navegação esquerdo, clique em **Chaves** e, em seguida, clique em **Chaves de leitura/gravação**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-152">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="89e5b-153">Você usará os botões de cópia no lado direito da tela para copiar o URI e a CHAVE PRIMÁRIA para o arquivo `Program.java` na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="89e5b-153">You'll use the copy buttons on the right side of the screen to copy the URI and PRIMARY KEY into the `Program.java` file in the next step.</span></span>

    ![Exibir e copiar uma chave de acesso no Portal do Azure, folha Chaves](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="89e5b-155">No arquivo `Program.java`aberto, copie o valor do URI no portal (usando o botão de cópia) e transforme-o no valor do ponto de extremidade para o construtor DocumentClient em `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="89e5b-155">In the open `Program.java` file, copy your URI value from the portal (using the copy button) and make it the value of the endpoint to the DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="89e5b-156">Em seguida, copie o valor da CHAVE PRIMÁRIA no portal e cole-o em "FILLME", tornando-o o segundo parâmetro no construtor DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="89e5b-156">Then copy your PRIMARY KEY value from the portal and paste it over “FILLME”, making it the second parameter in the DocumentClient constructor.</span></span> <span data-ttu-id="89e5b-157">Agora, você atualizou o aplicativo com todas as informações necessárias para se comunicar com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e5b-157">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-app"></a><span data-ttu-id="89e5b-158">Execute o aplicativo</span><span class="sxs-lookup"><span data-stu-id="89e5b-158">Run the app</span></span>

1. <span data-ttu-id="89e5b-159">Na janela do terminal git, `cd` para a pasta azure-cosmos-db-documentdb-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="89e5b-159">In the git terminal window, `cd` to the azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="89e5b-160">Na janela do terminal git, digite `mvn package` para instalar os pacotes necessários do Java.</span><span class="sxs-lookup"><span data-stu-id="89e5b-160">In the git terminal window, type `mvn package` to install the required Java packages.</span></span>

3. <span data-ttu-id="89e5b-161">Na janela do terminal de git, execute `mvn exec:java -D exec.mainClass=GetStarted.Program` na janela de terminal para iniciar o aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="89e5b-161">In the git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in the terminal window to start your Java application.</span></span>

    <span data-ttu-id="89e5b-162">Na janela de terminal, você receberá uma notificação de que o banco de dados FamilyDB foi criado e deve pressionar uma tecla para continuar.</span><span class="sxs-lookup"><span data-stu-id="89e5b-162">In the terminal window, you'll receive notification that the FamilyDB database was created, and to press a key to continue.</span></span> <span data-ttu-id="89e5b-163">Pressione uma tecla para criar o banco de dados, em seguida, alterne para o Data Explorer e verá que agora ele contém um banco de dados FamilyDB.</span><span class="sxs-lookup"><span data-stu-id="89e5b-163">Press a key to create the database, then switch to the Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="89e5b-164">Continue a pressionar teclas para criar a coleção e os documentos, em seguida, faça uma consulta.</span><span class="sxs-lookup"><span data-stu-id="89e5b-164">Continue to press keys to create the collection and the documents and then perform a query.</span></span> <span data-ttu-id="89e5b-165">Quando o projeto concluir, os recursos serão excluídos de sua conta.</span><span class="sxs-lookup"><span data-stu-id="89e5b-165">When the project completes, the resources are deleted from your account.</span></span> 

    ![Exibir e copiar uma chave de acesso no Portal do Azure, folha Chaves](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="89e5b-167">Examinar SLAs no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="89e5b-167">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="89e5b-168">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="89e5b-168">Clean up resources</span></span>

<span data-ttu-id="89e5b-169">Se você não continuar usando este aplicativo, exclua todos os recursos criados por esse início rápido no portal do Azure com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="89e5b-169">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="89e5b-170">No menu à esquerda no Portal do Azure, clique em **Grupos de recursos** e depois clique no nome do recurso criado.</span><span class="sxs-lookup"><span data-stu-id="89e5b-170">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="89e5b-171">Em sua página de grupo de recursos, clique em **Excluir**, digite o nome do recurso para excluir na caixa de texto e depois clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-171">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89e5b-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="89e5b-172">Next steps</span></span>

<span data-ttu-id="89e5b-173">Neste início rápido, você aprendeu como criar uma conta do Azure Cosmos DB, uma coleção usando o Data Explorer e executar um aplicativo para fazer a mesma coisa programaticamente.</span><span class="sxs-lookup"><span data-stu-id="89e5b-173">In this quickstart, you've learned how to create an Azure Cosmos DB account, document database, and collection using the Data Explorer, and run an app to do the same thing programmatically.</span></span> <span data-ttu-id="89e5b-174">Agora, é possível importar outros dados para sua conta do BD Cosmos.</span><span class="sxs-lookup"><span data-stu-id="89e5b-174">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="89e5b-175">Importar dados no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="89e5b-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


