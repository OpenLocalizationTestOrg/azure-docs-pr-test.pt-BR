---
title: 'Azure Cosmos DB: compilar um aplicativo Web com o .NET e com a API do DocumentDB | Microsoft Docs'
description: "Apresenta um exemplo de código .NET que pode ser usado para se conectar à API do DocumentDB do Azure Cosmos DB e consultá-la"
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
ms.openlocfilehash: 9bb863261da64c97f99757d4a0cb3474a7755591
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="e468d-103">Azure Cosmos DB: compilar um aplicativo Web da API do DocumentDB com o .NET e com o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e468d-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="e468d-104">O Azure Cosmos DB é um serviço de banco de dados multimodelo, globalmente distribuído da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e468d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="e468d-105">É possível criar e consultar rapidamente documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e468d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="e468d-106">Este início rápido demonstra como criar uma conta do Azure Cosmos DB, um banco de dados de documento e uma coleção usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e468d-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="e468d-107">Você, em seguida, compilará e implantará um aplicativo Web de lista de tarefas pendentes compilado na [API do .NET do DocumentDB](documentdb-sdk-dotnet.md), conforme mostrado na captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="e468d-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in the following screenshot.</span></span> 

![Aplicativo de tarefas pendentes com os dados de exemplo](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="e468d-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e468d-109">Prerequisites</span></span>

<span data-ttu-id="e468d-110">Se você ainda não tem o Visual 2017 Studio instalado, poderá baixar e usar o **Visual Studio 2017 Community Edition** [gratuito](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e468d-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="e468d-111">Verifique se você habilitou o **desenvolvimento do Azure** durante a instalação do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e468d-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="e468d-112">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="e468d-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="e468d-113">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="e468d-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="e468d-114">Adicionar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="e468d-114">Add sample data</span></span>

<span data-ttu-id="e468d-115">Agora você pode adicionar dados à sua nova coleção usando o Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="e468d-115">You can now add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="e468d-116">No Data Explorer, o novo banco de dados aparece no painel Coleções.</span><span class="sxs-lookup"><span data-stu-id="e468d-116">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="e468d-117">Expanda o banco de dados **Tarefas**, expanda a coleção **Itens**, clique em **Documentos** e clique em **Novos Documentos**.</span><span class="sxs-lookup"><span data-stu-id="e468d-117">Expand the **Tasks** database, expand the **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Criar novos documentos no Data Explorer no portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="e468d-119">Agora, adicione um documento à coleção com a seguinte estrutura.</span><span class="sxs-lookup"><span data-stu-id="e468d-119">Now add a document to the collection with the following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="e468d-120">Depois de ter adicionado o json à guia **Documentos**, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e468d-120">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![Copie nos dados json e clique em Salvar no Data Explorer no portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="e468d-122">Crie e salve mais um documento onde você insere um valor exclusivo para a propriedade `id` e altere as outras propriedades quando achar adequado.</span><span class="sxs-lookup"><span data-stu-id="e468d-122">Create and save one more document where you insert a unique value for the `id` property, and change the other properties as you see fit.</span></span> <span data-ttu-id="e468d-123">Os novos documentos podem ter qualquer estrutura que você deseje, pois o Azure Cosmos DB não impõe nenhum esquema para seus dados.</span><span class="sxs-lookup"><span data-stu-id="e468d-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="e468d-124">Agora você pode usar consultas no Data Explorer para recuperar os dados.</span><span class="sxs-lookup"><span data-stu-id="e468d-124">You can now use queries in Data Explorer to retrieve your data.</span></span> <span data-ttu-id="e468d-125">Por padrão, o Data Explorer usa `SELECT * FROM c` para recuperar todos os documentos na coleção, mas você pode alterar isso para uma [consulta SQL ](documentdb-sql-query.md) diferente, como `SELECT * FROM c ORDER BY c._ts DESC`, para retornar todos os documentos em ordem descendente com base no carimbo de data/hora.</span><span class="sxs-lookup"><span data-stu-id="e468d-125">By default, Data Explorer uses `SELECT * FROM c` to retrieve all documents in the collection, but you can change that to a different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, to return all the documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="e468d-126">Você também pode usar o Data Explorer para criar procedimentos armazenados, UDFs e gatilhos para executar a lógica de negócios do servidor, além de dimensionar a taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="e468d-126">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="e468d-127">O Data Explorer expõe todo o acesso a dados interno via programação disponível nas APIs, mas oferece acesso fácil aos dados no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e468d-127">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="e468d-128">Clonar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="e468d-128">Clone the sample application</span></span>

<span data-ttu-id="e468d-129">Agora, vamos trabalhar com o código.</span><span class="sxs-lookup"><span data-stu-id="e468d-129">Now let's switch to working with code.</span></span> <span data-ttu-id="e468d-130">Vamos clonar um aplicativo de API do DocumentDB do GitHub, definir a cadeia de conexão e executá-la.</span><span class="sxs-lookup"><span data-stu-id="e468d-130">Let's clone a DocumentDB API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="e468d-131">Você verá como é fácil trabalhar usando dados de forma programática.</span><span class="sxs-lookup"><span data-stu-id="e468d-131">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="e468d-132">Abra uma janela de terminal do Git, como git bash, e `CD` para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e468d-132">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="e468d-133">Execute o comando a seguir para clonar o repositório de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e468d-133">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="e468d-134">Em seguida, abra o arquivo da solução todo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e468d-134">Then open the todo solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="e468d-135">Examine o código</span><span class="sxs-lookup"><span data-stu-id="e468d-135">Review the code</span></span>

<span data-ttu-id="e468d-136">Façamos uma rápida análise do que está acontecendo no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e468d-136">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="e468d-137">Abra o arquivo DocumentDBRepository.cs e você verá que essas linhas de código criam os recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e468d-137">Open the DocumentDBRepository.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="e468d-138">O DocumentClient é inicializado na linha 73.</span><span class="sxs-lookup"><span data-stu-id="e468d-138">The DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="e468d-139">Um novo banco de dados é criado na linha 88.</span><span class="sxs-lookup"><span data-stu-id="e468d-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="e468d-140">Uma nova coleção é criada na linha 107.</span><span class="sxs-lookup"><span data-stu-id="e468d-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="e468d-141">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="e468d-141">Update your connection string</span></span>

<span data-ttu-id="e468d-142">Agora, volte ao portal do Azure para obter informações sobre a cadeia de conexão e copiá-las para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e468d-142">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="e468d-143">No[Portal do Azure](http://portal.azure.com/), na sua conta do Azure Cosmos DB, no painel de navegação esquerdo, clique em **Chaves** e, em seguida, clique em **Chaves de leitura/gravação**.</span><span class="sxs-lookup"><span data-stu-id="e468d-143">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="e468d-144">Você usará os botões de cópia no lado direito da tela para copiar o URI e a Chave Primária para o arquivo web.config na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="e468d-144">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the web.config file in the next step.</span></span>

    ![Exibir e copiar uma chave de acesso no Portal do Azure, folha Chaves](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="e468d-146">No Visual Studio 2017, abra o arquivo web.config.</span><span class="sxs-lookup"><span data-stu-id="e468d-146">In Visual Studio 2017, open the web.config file.</span></span> 

3. <span data-ttu-id="e468d-147">Copie o valor do URI do portal (usando o botão de cópia) e transforme-o no valor da chave do ponto de extremidade em web.config.</span><span class="sxs-lookup"><span data-stu-id="e468d-147">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="e468d-148">Em seguida, copie o valor da CHAVE PRIMÁRIA do portal e transforme-o no valor de authKey em web.config. Agora, você atualizou o aplicativo com todas as informações necessárias para se comunicar com o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e468d-148">Then copy your PRIMARY KEY value from the portal and make it the value of the authKey in web.config. You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-the-web-app"></a><span data-ttu-id="e468d-149">Executar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="e468d-149">Run the web app</span></span>
1. <span data-ttu-id="e468d-150">No Visual Studio, clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e468d-150">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="e468d-151">Na caixa **Procurar** do NuGet, digite *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="e468d-151">In the NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="e468d-152">Com base nos resultados, instale a biblioteca **Microsoft.Azure.DocumentDB**.</span><span class="sxs-lookup"><span data-stu-id="e468d-152">From the results, install the **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="e468d-153">Isso instala o pacote Microsoft.Azure.DocumentDB, bem como todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="e468d-153">This installs the Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="e468d-154">Clique em CTRL + F5 para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e468d-154">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="e468d-155">Seu aplicativo é exibido no navegador.</span><span class="sxs-lookup"><span data-stu-id="e468d-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="e468d-156">Clique em **Criar Novo** no navegador e crie algumas novas tarefas em seu aplicativo de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="e468d-156">Click **Create New** in the browser and create a few new tasks in your to-do app.</span></span>

   ![Aplicativo de tarefas pendentes com os dados de exemplo](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="e468d-158">Agora, é possível voltar ao Data Explorer e ver a consulta, modificar e trabalhar com esses novos dados.</span><span class="sxs-lookup"><span data-stu-id="e468d-158">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="e468d-159">Examinar SLAs no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e468d-159">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="e468d-160">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="e468d-160">Clean up resources</span></span>

<span data-ttu-id="e468d-161">Se você não continuar usando este aplicativo, exclua todos os recursos criados por esse início rápido no portal do Azure com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e468d-161">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="e468d-162">No menu à esquerda no Portal do Azure, clique em **Grupos de recursos** e depois clique no nome do recurso criado.</span><span class="sxs-lookup"><span data-stu-id="e468d-162">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="e468d-163">Em sua página de grupo de recursos, clique em **Excluir**, digite o nome do recurso para excluir na caixa de texto e depois clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="e468d-163">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e468d-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e468d-164">Next steps</span></span>

<span data-ttu-id="e468d-165">Neste início rápido, você aprendeu como criar uma conta do Azure Cosmos DB, como criar uma coleção usando o Data Explorer e como executar um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e468d-165">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a web app.</span></span> <span data-ttu-id="e468d-166">Agora, é possível importar outros dados para sua conta do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e468d-166">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e468d-167">Importar dados no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e468d-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


