---
title: "Cosmos do Azure DB: Criar um aplicativo web com o .NET e Olá API DocumentDB | Microsoft Docs"
description: "Apresenta um exemplo de código do .NET podem usar tooconnect tooand consulta Olá API DocumentDB do Azure Cosmos DB"
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
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="cd7e7-103">Banco de dados do Azure do Cosmos: Criar um aplicativo da web API DocumentDB com o .NET e Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cd7e7-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="cd7e7-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="cd7e7-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="cd7e7-106">Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="cd7e7-107">Você, em seguida, criar e implantar um aplicativo da web lista todo baseado Olá [API .NET do DocumentDB](documentdb-sdk-dotnet.md), conforme mostrado no hello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in hello following screenshot.</span></span> 

![Aplicativo de tarefas pendentes com os dados de exemplo](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="cd7e7-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cd7e7-109">Prerequisites</span></span>

<span data-ttu-id="cd7e7-110">Se você ainda não tiver o Visual Studio de 2017 instalado, você pode baixar e usar o hello **livre** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="cd7e7-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="cd7e7-111">Certifique-se de que você habilite **desenvolvimento do Azure** durante a instalação do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="cd7e7-112">Criar uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="cd7e7-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="cd7e7-113">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="cd7e7-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="cd7e7-114">Adicionar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="cd7e7-114">Add sample data</span></span>

<span data-ttu-id="cd7e7-115">Agora você pode adicionar dados tooyour nova coleção usando o Gerenciador de dados.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-115">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="cd7e7-116">No Explorador de dados, o novo banco de dados de saudação aparece no painel de coleções de hello.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-116">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="cd7e7-117">Expanda Olá **tarefas** de banco de dados, expanda Olá **itens** coleção, clique em **documentos**e, em seguida, clique em **novos documentos**.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-117">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Criar novos documentos no Explorador de dados no hello portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="cd7e7-119">Agora, adicione uma coleção de toohello de documento com hello estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-119">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="cd7e7-120">Depois de adicionar Olá json toohello **documentos** , clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-120">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Copiar dados json e clique em Salvar no Explorador de dados em Olá portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="cd7e7-122">Crie e salve um documento mais onde você insere um valor exclusivo para Olá `id` propriedade e alteração Olá outras propriedades como desejar.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-122">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="cd7e7-123">Os novos documentos podem ter qualquer estrutura que você deseje, pois o Azure Cosmos DB não impõe nenhum esquema para seus dados.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="cd7e7-124">Agora você pode usar consultas no Explorador de dados tooretrieve seus dados.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-124">You can now use queries in Data Explorer tooretrieve your data.</span></span> <span data-ttu-id="cd7e7-125">Por padrão, o Gerenciador de dados usa `SELECT * FROM c` tooretrieve todos os documentos na coleção hello, mas você pode alterar esse tooa diferente [consulta SQL](documentdb-sql-query.md), como `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn todos os documentos de saudação em ordem decrescente com base em o carimbo de hora.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-125">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="cd7e7-126">Você também pode usar procedimentos de toocreate armazenado no Explorador de dados, UDFs e lógica de negócios do lado do servidor de tooperform de gatilhos, bem como a taxa de transferência de escala.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-126">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="cd7e7-127">No Explorador de dados expõe todos acesso a dados através de programação interno Olá disponível no hello APIs, mas fornece acesso fácil tooyour dados em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-127">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="cd7e7-128">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="cd7e7-128">Clone hello sample application</span></span>

<span data-ttu-id="cd7e7-129">Agora vamos alternar tooworking com o código.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-129">Now let's switch tooworking with code.</span></span> <span data-ttu-id="cd7e7-130">Vamos, clonar um aplicativo de API de documentos do GitHub, defina a cadeia de caracteres de conexão hello e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-130">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="cd7e7-131">Você verá como é fácil toowork com dados programaticamente.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-131">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="cd7e7-132">Abra uma janela de terminal de git, como git bash, e `CD` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-132">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="cd7e7-133">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-133">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="cd7e7-134">Abra o arquivo de solução de todo Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-134">Then open hello todo solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="cd7e7-135">Examine o código de saudação</span><span class="sxs-lookup"><span data-stu-id="cd7e7-135">Review hello code</span></span>

<span data-ttu-id="cd7e7-136">Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-136">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="cd7e7-137">Olá abrir DocumentDBRepository.cs de arquivo e você encontrará que essas linhas de código criam Olá recursos de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-137">Open hello DocumentDBRepository.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="cd7e7-138">Olá DocumentClient é inicializada na linha 73.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-138">hello DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="cd7e7-139">Um novo banco de dados é criado na linha 88.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="cd7e7-140">Uma nova coleção é criada na linha 107.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="cd7e7-141">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="cd7e7-141">Update your connection string</span></span>

<span data-ttu-id="cd7e7-142">Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-142">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="cd7e7-143">Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-143">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="cd7e7-144">Você usará botões de cópia Olá Olá direita da saudação toocopy da tela hello URI e a chave primária no arquivo Web. config de saudação na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-144">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello web.config file in hello next step.</span></span>

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="cd7e7-146">No Visual Studio de 2017, abra o arquivo Web. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-146">In Visual Studio 2017, open hello web.config file.</span></span> 

3. <span data-ttu-id="cd7e7-147">Copie o valor URI do portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá o valor da chave do ponto de extremidade de Olá no Web. config.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-147">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="cd7e7-148">Em seguida, copie o valor de chave primária do portal de saudação e torná-lo Olá valor Olá authKey em Web. config. Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-148">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello authKey in web.config. You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a><span data-ttu-id="cd7e7-149">Executar o aplicativo da web de saudação</span><span class="sxs-lookup"><span data-stu-id="cd7e7-149">Run hello web app</span></span>
1. <span data-ttu-id="cd7e7-150">No Visual Studio, clique com botão direito no projeto Olá no **Solution Explorer** e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-150">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="cd7e7-151">Em Olá NuGet **procurar** , digite *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-151">In hello NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="cd7e7-152">Resultados de hello, instalar Olá **Microsoft.Azure.DocumentDB** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-152">From hello results, install hello **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="cd7e7-153">Isso instala o pacote de Microsoft.Azure.DocumentDB de saudação, bem como todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-153">This installs hello Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="cd7e7-154">Clique em CTRL + F5 aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-154">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="cd7e7-155">Seu aplicativo é exibido no navegador.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="cd7e7-156">Clique em **criar novo** Olá navegador e criar algumas novas tarefas em seu aplicativo de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-156">Click **Create New** in hello browser and create a few new tasks in your to-do app.</span></span>

   ![Aplicativo de tarefas pendentes com os dados de exemplo](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="cd7e7-158">Agora você pode voltar tooData Explorer e consulte a consulta, modificar e trabalhar com esses novos dados.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-158">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="cd7e7-159">Examine os SLAs em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cd7e7-159">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="cd7e7-160">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="cd7e7-160">Clean up resources</span></span>

<span data-ttu-id="cd7e7-161">Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cd7e7-161">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="cd7e7-162">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-162">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="cd7e7-163">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-163">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd7e7-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cd7e7-164">Next steps</span></span>

<span data-ttu-id="cd7e7-165">Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, crie uma coleção usando Olá Explorador de dados e executar um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-165">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a web app.</span></span> <span data-ttu-id="cd7e7-166">Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="cd7e7-166">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="cd7e7-167">Importar dados no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cd7e7-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


