---
title: aaaCreate um banco de dados de documento de banco de dados do Azure Cosmos com Java | Microsoft Docs | Microsoft Docs
description: "Apresenta um exemplo de código de Java que você pode usar tooconnect tooand consulta Olá API DocumentDB do Azure Cosmos DB"
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
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="6f8b1-103">Banco de dados do Azure do Cosmos: Criar um banco de dados de documento usando Java e Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6f8b1-103">Azure Cosmos DB: Create a document database using Java and hello Azure portal</span></span>

<span data-ttu-id="6f8b1-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="6f8b1-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="6f8b1-106">Este guia de início rápido cria um documento de banco de dados usando Olá ferramentas portais do Azure para o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-106">This quickstart creates a document database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="6f8b1-107">Este guia de início rápido também mostra como tooquickly criar um aplicativo de console de Java usando Olá [API Java do DocumentDB](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="6f8b1-107">This quickstart also shows you how tooquickly create a Java console app using hello [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="6f8b1-108">instruções Olá este guia de início rápido podem ser seguidas em qualquer sistema operacional que é capaz de executar Java.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="6f8b1-109">Ao concluir esse início rápido será familiarizado com a criação e modificação de recursos de banco de dados de documento em Olá da interface do usuário ou através de programação, o que for sua preferência.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either hello UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f8b1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6f8b1-110">Prerequisites</span></span>

* [<span data-ttu-id="6f8b1-111">Java Development Kit (JDK) 1.7 +</span><span class="sxs-lookup"><span data-stu-id="6f8b1-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="6f8b1-112">No Ubuntu, execute `apt-get install default-jdk` tooinstall Olá JDK.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="6f8b1-113">Ser toohello tooset se Olá JAVA_HOME ambiente variável toopoint pasta onde Olá JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="6f8b1-114">[Baixar](http://maven.apache.org/download.cgi) e [instalar](http://maven.apache.org/install.html) um armazenamento binário [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="6f8b1-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="6f8b1-115">No Ubuntu, você pode executar `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="6f8b1-116">Git</span><span class="sxs-lookup"><span data-stu-id="6f8b1-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="6f8b1-117">No Ubuntu, você pode executar `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="6f8b1-118">Criar uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="6f8b1-118">Create a database account</span></span>

<span data-ttu-id="6f8b1-119">Antes de criar um banco de dados de documento, você precisa toocreate uma conta de banco de dados SQL (documentos) com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-119">Before you can create a document database, you need toocreate a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="6f8b1-120">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="6f8b1-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="6f8b1-121">Adicionar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="6f8b1-121">Add sample data</span></span>

<span data-ttu-id="6f8b1-122">Agora você pode adicionar dados tooyour nova coleção usando o Gerenciador de dados.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-122">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="6f8b1-123">No Explorador de dados, o novo banco de dados de saudação aparece no painel de coleções de hello.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-123">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="6f8b1-124">Expanda Olá **tarefas** de banco de dados, expanda Olá **itens** coleção, clique em **documentos**e, em seguida, clique em **novos documentos**.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-124">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Criar novos documentos no Explorador de dados no hello portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="6f8b1-126">Agora, adicione uma coleção de toohello de documento com hello estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-126">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="6f8b1-127">Depois de adicionar Olá json toohello **documentos** , clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-127">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Copiar dados json e clique em Salvar no Explorador de dados em Olá portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="6f8b1-129">Crie e salve um documento mais onde você insere um valor exclusivo para Olá `id` propriedade e alteração Olá outras propriedades como desejar.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-129">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="6f8b1-130">Os novos documentos podem ter qualquer estrutura que você deseje, pois o Azure Cosmos DB não impõe nenhum esquema para seus dados.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="6f8b1-131">Você pode agora usar consultas no Explorador de dados tooretrieve seus dados clicando Olá **Editar filtro** e **Aplicar filtro** botões.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-131">You can now use queries in Data Explorer tooretrieve your data by clicking hello **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="6f8b1-132">Por padrão, o Gerenciador de dados usa `SELECT * FROM c` tooretrieve todos os documentos na coleção hello, mas você pode alterar esse tooa diferente [consulta SQL](documentdb-sql-query.md), como `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn todos os documentos de saudação em ordem decrescente com base em o carimbo de hora.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-132">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="6f8b1-133">Você também pode usar procedimentos de toocreate armazenado no Explorador de dados, UDFs e lógica de negócios do lado do servidor de tooperform de gatilhos, bem como a taxa de transferência de escala.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-133">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="6f8b1-134">No Explorador de dados expõe todos acesso a dados através de programação interno Olá disponível no hello APIs, mas fornece acesso fácil tooyour dados em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-134">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="6f8b1-135">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="6f8b1-135">Clone hello sample application</span></span>

<span data-ttu-id="6f8b1-136">Agora vamos alternar tooworking com o código.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-136">Now let's switch tooworking with code.</span></span> <span data-ttu-id="6f8b1-137">Vamos, clonar um aplicativo de API de documentos do GitHub, defina a cadeia de caracteres de conexão hello e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-137">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="6f8b1-138">Você verá como é fácil toowork com dados programaticamente.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-138">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="6f8b1-139">Abra uma janela de terminal de git, como git bash, e `CD` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-139">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="6f8b1-140">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-140">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="6f8b1-141">Examine o código de saudação</span><span class="sxs-lookup"><span data-stu-id="6f8b1-141">Review hello code</span></span>

<span data-ttu-id="6f8b1-142">Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-142">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="6f8b1-143">Olá abrir `Program.java` arquivo da pasta de \src\GetStarted hello e encontrar essas linhas de código que cria Olá recursos de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-143">Open hello `Program.java` file from hello \src\GetStarted folder, and find these lines of code that create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="6f8b1-144">Olá `DocumentClient` é inicializado.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-144">hello `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="6f8b1-145">Um novo banco de dados é criado.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="6f8b1-146">Uma nova coleção é criada.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="6f8b1-147">Alguns documentos são criados.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="6f8b1-148">Uma consulta SQL no JSON é executada.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-148">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="6f8b1-149">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="6f8b1-149">Update your connection string</span></span>

<span data-ttu-id="6f8b1-150">Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-150">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span> <span data-ttu-id="6f8b1-151">Isso permitirá toocommunicate seu aplicativo com o banco de dados hospedado.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-151">This will enable your app toocommunicate with your hosted database.</span></span>

1. <span data-ttu-id="6f8b1-152">Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-152">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="6f8b1-153">Você usará botões de cópia de saudação na direita de saudação do hello toocopy da tela hello URI e a chave primária em Olá `Program.java` arquivo na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-153">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and PRIMARY KEY into hello `Program.java` file in hello next step.</span></span>

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="6f8b1-155">Em Olá abrir `Program.java` de arquivo, copie o valor URI do portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá valor Olá ponto de extremidade toohello DocumentClient construtor `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-155">In hello open `Program.java` file, copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint toohello DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="6f8b1-156">Em seguida, copie o valor de chave primária do portal hello e cole-o em "FILLME", tornando-Olá segundo parâmetro no construtor de DocumentClient hello.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-156">Then copy your PRIMARY KEY value from hello portal and paste it over “FILLME”, making it hello second parameter in hello DocumentClient constructor.</span></span> <span data-ttu-id="6f8b1-157">Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-157">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-app"></a><span data-ttu-id="6f8b1-158">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="6f8b1-158">Run hello app</span></span>

1. <span data-ttu-id="6f8b1-159">Na janela do terminal Olá git, `cd` pasta azure-cosmos-db-documentdb-java-getting-started toohello.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-159">In hello git terminal window, `cd` toohello azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="6f8b1-160">Na janela do terminal Olá git, digite `mvn package` tooinstall Olá necessário pacotes Java.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-160">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="6f8b1-161">Na janela do terminal Olá git, execute `mvn exec:java -D exec.mainClass=GetStarted.Program` no hello janela do terminal toostart seu aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-161">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

    <span data-ttu-id="6f8b1-162">Na janela do terminal hello, você recebe notificação que Olá FamilyDB banco de dados foi criado e toopress toocontinue uma chave.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-162">In hello terminal window, you'll receive notification that hello FamilyDB database was created, and toopress a key toocontinue.</span></span> <span data-ttu-id="6f8b1-163">Pressione um banco de dados de saudação toocreate chave, alterne toohello Explorador de dados e você verá que agora ele contém um banco de dados FamilyDB.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-163">Press a key toocreate hello database, then switch toohello Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="6f8b1-164">Continuar toopress chaves toocreate Olá coleta e hello documentos e, em seguida, executar uma consulta.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-164">Continue toopress keys toocreate hello collection and hello documents and then perform a query.</span></span> <span data-ttu-id="6f8b1-165">Quando o projeto de saudação for concluído, recursos de saudação são excluídos de sua conta.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-165">When hello project completes, hello resources are deleted from your account.</span></span> 

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="6f8b1-167">Examine os SLAs em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6f8b1-167">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="6f8b1-168">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="6f8b1-168">Clean up resources</span></span>

<span data-ttu-id="6f8b1-169">Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6f8b1-169">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="6f8b1-170">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-170">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="6f8b1-171">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-171">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f8b1-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6f8b1-172">Next steps</span></span>

<span data-ttu-id="6f8b1-173">Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá Explorador de dados e executar um aplicativo toodo Olá mesmo programaticamente.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-173">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, document database, and collection using hello Data Explorer, and run an app toodo hello same thing programmatically.</span></span> <span data-ttu-id="6f8b1-174">Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="6f8b1-174">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="6f8b1-175">Importar dados no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6f8b1-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


