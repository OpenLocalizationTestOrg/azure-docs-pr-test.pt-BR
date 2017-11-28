---
title: "aaaBuild um aplicativo .NET de banco de dados do Azure Cosmos usando Olá API tabela | Microsoft Docs"
description: "Introdução à API de Tabela do BD Cosmos do Azure usando .NET"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: bdd4f8ec45407962b3d2cb26aa814a20cfc62173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a><span data-ttu-id="2acab-103">Cosmos do Azure DB: Criar um aplicativo .NET usando Olá API de tabela</span><span class="sxs-lookup"><span data-stu-id="2acab-103">Azure Cosmos DB: Build a .NET application using hello Table API</span></span>

<span data-ttu-id="2acab-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2acab-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="2acab-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="2acab-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="2acab-106">Este guia rápido demonstra como toocreate um banco de dados do Azure Cosmos conta e criar uma tabela dentro dessa conta usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2acab-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, and create a table within that account using hello Azure portal.</span></span> <span data-ttu-id="2acab-107">Você usará, em seguida, escrever código tooinsert, atualizar e excluir entidades e execute algumas consultas usando Olá novo [tabela Premium do Windows Azure Storage](https://aka.ms/premiumtablenuget) pacote (visualização) do NuGet.</span><span class="sxs-lookup"><span data-stu-id="2acab-107">You'll then write code tooinsert, update, and delete entities, and run some queries using hello new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="2acab-108">Esta biblioteca tem Olá mesmas classes e assinaturas de método como público Olá [SDK de armazenamento do Windows Azure](https://www.nuget.org/packages/WindowsAzure.Storage), mas também tem contas Olá capacidade tooconnect tooAzure Cosmos DB usando Olá [API tabela](table-introduction.md) (visualização).</span><span class="sxs-lookup"><span data-stu-id="2acab-108">This library has hello same classes and method signatures as hello public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has hello ability tooconnect tooAzure Cosmos DB accounts using hello [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2acab-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2acab-109">Prerequisites</span></span>

<span data-ttu-id="2acab-110">Se você ainda não tiver o Visual Studio de 2017 instalado, você pode baixar e usar o hello **livre** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2acab-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="2acab-111">Certifique-se de que você habilite **desenvolvimento do Azure** durante a instalação do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="2acab-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="2acab-112">Criar uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="2acab-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="2acab-113">Adicionar uma tabela</span><span class="sxs-lookup"><span data-stu-id="2acab-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="2acab-114">Adicionar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="2acab-114">Add sample data</span></span>

<span data-ttu-id="2acab-115">Agora você pode adicionar dados tooyour nova tabela usando o Gerenciador de dados (visualização).</span><span class="sxs-lookup"><span data-stu-id="2acab-115">You can now add data tooyour new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="2acab-116">No Data Explorer, expanda **sample-table**, clique em **Entidades** e clique em **Adicionar Entidade**.</span><span class="sxs-lookup"><span data-stu-id="2acab-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![Crie novas entidades no Explorador de dados no hello portal do Azure](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="2acab-118">Agora adicione caixas de valor do dados toohello PartitionKey e RowKey valor e clique em **Adicionar entidade**.</span><span class="sxs-lookup"><span data-stu-id="2acab-118">Now add data toohello PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![Definir Olá chave de partição e chave de linha para uma nova entidade](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="2acab-120">Agora você pode adicionar mais tabela tooyour de entidades, editar suas entidades ou consultar seus dados no Explorador de dados.</span><span class="sxs-lookup"><span data-stu-id="2acab-120">You can now add more entities tooyour table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="2acab-121">No Explorador de dados também é onde você pode dimensionar a taxa de transferência e adicionar procedimentos armazenados, funções definidas pelo usuário e tabela de tooyour gatilhos.</span><span class="sxs-lookup"><span data-stu-id="2acab-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers tooyour table.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="2acab-122">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="2acab-122">Clone hello sample application</span></span>

<span data-ttu-id="2acab-123">Agora vamos, clonar um aplicativo de tabela do github, defina a cadeia de caracteres de conexão hello e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="2acab-123">Now let's clone a Table app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="2acab-124">Você verá como é fácil toowork com dados programaticamente.</span><span class="sxs-lookup"><span data-stu-id="2acab-124">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="2acab-125">Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2acab-125">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="2acab-126">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="2acab-126">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="2acab-127">Em seguida, abra o arquivo de solução de saudação no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2acab-127">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="2acab-128">Examine o código de saudação</span><span class="sxs-lookup"><span data-stu-id="2acab-128">Review hello code</span></span>

<span data-ttu-id="2acab-129">Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2acab-129">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="2acab-130">Arquivo Program.cs de saudação aberto e você descobrirá que essas linhas de código criam Olá recursos de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2acab-130">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="2acab-131">Olá CloudTableClient é inicializado.</span><span class="sxs-lookup"><span data-stu-id="2acab-131">hello CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="2acab-132">A nova tabela é criada se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="2acab-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="2acab-133">Um novo contêiner de Tabela é criado.</span><span class="sxs-lookup"><span data-stu-id="2acab-133">A new Table container is created.</span></span> <span data-ttu-id="2acab-134">Você observará que essa tooregular muito semelhantes do código SDK de armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="2acab-134">You will notice this code very similar tooregular Azure Table storage SDK.</span></span> 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="2acab-135">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="2acab-135">Update your connection string</span></span>

<span data-ttu-id="2acab-136">Agora vamos atualizar informações de cadeia de caracteres de conexão de saudação para que seu aplicativo pode se comunicar tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2acab-136">Now we'll update hello connection string information so your app can talk tooAzure Cosmos DB.</span></span> 

1. <span data-ttu-id="2acab-137">No Visual Studio, abra o arquivo App. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="2acab-137">In Visual Studio, open hello app.config file.</span></span> 

2. <span data-ttu-id="2acab-138">Em Olá [portal do Azure](http://portal.azure.com/)no hello Azure Cosmos DB esquerda menu de navegação, clique em **cadeia de caracteres de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="2acab-138">In hello [Azure portal](http://portal.azure.com/), in hello Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="2acab-139">Em seguida, no painel de novo Olá botão Olá cópia para a cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2acab-139">Then in hello new pane click hello copy button for hello connection string.</span></span> 

    ![Exibir e copiar hello ponto de extremidade e chave de conta no painel de cadeia de caracteres de Conexão Olá](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="2acab-141">Cole o valor de saudação no arquivo App. config de saudação como valor de saudação do hello PremiumStorageConnectionString.</span><span class="sxs-lookup"><span data-stu-id="2acab-141">Paste hello value into hello app.config file as hello value of hello PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="2acab-142">Você pode deixar Olá StandardStorageConnectionString como está.</span><span class="sxs-lookup"><span data-stu-id="2acab-142">You can leave hello StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="2acab-143">Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2acab-143">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-web-app"></a><span data-ttu-id="2acab-144">Executar o aplicativo da web de saudação</span><span class="sxs-lookup"><span data-stu-id="2acab-144">Run hello web app</span></span>

1. <span data-ttu-id="2acab-145">No Visual Studio, clique em Olá **PremiumTableGetStarted** project no **Solution Explorer** e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2acab-145">In Visual Studio, right-click on hello **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="2acab-146">Em Olá NuGet **procurar** , digite *windowsazure PremiumTable*.</span><span class="sxs-lookup"><span data-stu-id="2acab-146">In hello NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="2acab-147">Verificar Olá **incluir pré-lançamento** caixa.</span><span class="sxs-lookup"><span data-stu-id="2acab-147">Check hello **Include prerelease** box.</span></span> 

4. <span data-ttu-id="2acab-148">Resultados de hello, instalar Olá **windowsazure PremiumTable** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="2acab-148">From hello results, install hello **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="2acab-149">Isso instala a visualização Olá pacote API de tabela de banco de dados do Azure Cosmos, bem como todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="2acab-149">This installs hello preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="2acab-150">Observe que se trata de um pacote do NuGet diferente Olá pacote do armazenamento do Windows Azure usado pelo armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="2acab-150">Note that this is a different NuGet package than hello Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="2acab-151">Clique em CTRL + F5 aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="2acab-151">Click CTRL + F5 toorun hello application.</span></span>

    <span data-ttu-id="2acab-152">janela de console Olá exibe dados de saudação sejam adicionados, recuperado, consultados, substituídos e excluídas da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="2acab-152">hello console window displays hello data being added, retrieved, queried, replaced and deleted from hello table.</span></span> <span data-ttu-id="2acab-153">Quando Olá script for concluído, pressione qualquer janela de console Olá tooclose chave.</span><span class="sxs-lookup"><span data-stu-id="2acab-153">When hello script completes, press any key tooclose hello console window.</span></span> 
    
    ![Saída do console do hello quickstart](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="2acab-155">Se você quiser toosee Olá novas entidades no Explorador de dados, basta comente linhas 188 208 em program.cs para que eles não são excluídos, execute exemplo hello novamente.</span><span class="sxs-lookup"><span data-stu-id="2acab-155">If you want toosee hello new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run hello sample again.</span></span> 

    <span data-ttu-id="2acab-156">Você pode agora voltar tooData Explorer, clique em **atualizar**, expanda Olá **pessoas** de tabela e clique em **entidades**e, em seguida, trabalhar com esses novos dados.</span><span class="sxs-lookup"><span data-stu-id="2acab-156">You can now go back tooData Explorer, click **Refresh**, expand hello **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![Novas entidades no Data Explorer](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="2acab-158">Examine os SLAs em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2acab-158">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="2acab-159">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="2acab-159">Clean up resources</span></span>

<span data-ttu-id="2acab-160">Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2acab-160">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="2acab-161">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="2acab-161">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="2acab-162">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="2acab-162">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2acab-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2acab-163">Next steps</span></span>

<span data-ttu-id="2acab-164">Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, criar uma tabela usando Olá Explorador de dados e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2acab-164">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a table using hello Data Explorer, and run an app.</span></span>  <span data-ttu-id="2acab-165">Agora você pode consultar os dados usando Olá API de tabela.</span><span class="sxs-lookup"><span data-stu-id="2acab-165">Now you can query your data using hello Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="2acab-166">Consulta usando Olá API de tabela</span><span class="sxs-lookup"><span data-stu-id="2acab-166">Query using hello Table API</span></span>](tutorial-query-table.md)

