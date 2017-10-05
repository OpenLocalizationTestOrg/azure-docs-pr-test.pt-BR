---
title: Compilar um aplicativo .NET do BD Cosmos do Azure usando a API de Tabela | Microsoft Docs
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
ms.openlocfilehash: 29e7eebda5177d6e852ef04ad82d9d38a8d30ed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-the-table-api"></a><span data-ttu-id="12080-103">BD Cosmos do Azure: compilar um aplicativo .NET usando a API de Tabela</span><span class="sxs-lookup"><span data-stu-id="12080-103">Azure Cosmos DB: Build a .NET application using the Table API</span></span>

<span data-ttu-id="12080-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="12080-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="12080-105">É possível criar e consultar rapidamente documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="12080-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="12080-106">Este início rápido demonstra como criar uma conta do BD Cosmos do Azure e uma tabela dentro desta conta usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="12080-106">This quick start demonstrates how to create an Azure Cosmos DB account, and create a table within that account using the Azure portal.</span></span> <span data-ttu-id="12080-107">Você vai escrever código para inserir, atualizar e excluir entidades e execute algumas consultas usando o novo pacote [tabela Premium do Microsoft Azure Storage](https://aka.ms/premiumtablenuget) (versão prévia) do NuGet.</span><span class="sxs-lookup"><span data-stu-id="12080-107">You'll then write code to insert, update, and delete entities, and run some queries using the new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="12080-108">Esta biblioteca tem as mesmas classes e assinaturas de método do [SDK do Armazenamento do Azure](https://www.nuget.org/packages/WindowsAzure.Storage) público, mas também tem a capacidade de se conectar às contas do Azure Cosmos DB usando a [API de Tabela](table-introduction.md) (versão prévia).</span><span class="sxs-lookup"><span data-stu-id="12080-108">This library has the same classes and method signatures as the public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has the ability to connect to Azure Cosmos DB accounts using the [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="12080-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="12080-109">Prerequisites</span></span>

<span data-ttu-id="12080-110">Se você ainda não tem o Visual 2017 Studio instalado, poderá baixar e usar o **Visual Studio 2017 Community Edition** [gratuito](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="12080-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="12080-111">Verifique se você habilitou o **desenvolvimento do Azure** durante a instalação do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12080-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="12080-112">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="12080-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="12080-113">Adicionar uma tabela</span><span class="sxs-lookup"><span data-stu-id="12080-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="12080-114">Adicionar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="12080-114">Add sample data</span></span>

<span data-ttu-id="12080-115">Agora é possível adicionar dados à sua nova tabela usando o Data Explorer (versão prévia).</span><span class="sxs-lookup"><span data-stu-id="12080-115">You can now add data to your new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="12080-116">No Data Explorer, expanda **sample-table**, clique em **Entidades** e clique em **Adicionar Entidade**.</span><span class="sxs-lookup"><span data-stu-id="12080-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![Criar novas entidades no Data Explorer no portal do Azure](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="12080-118">Agora, adicione dados às caixas de valor PartitionKey e RowKey e clique em **Adicionar Entidade**.</span><span class="sxs-lookup"><span data-stu-id="12080-118">Now add data to the PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![Definir a chave de partição e a chave de linha para uma nova entidade](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="12080-120">Agora, é possível adicionar mais entidades à tabela, editar as entidades ou consultar os dados no Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="12080-120">You can now add more entities to your table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="12080-121">Por meio do Data Explorer, também é possível dimensionar a taxa de transferência e adicionar procedimentos armazenados, funções definidas pelo usuário e gatilhos à tabela.</span><span class="sxs-lookup"><span data-stu-id="12080-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers to your table.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="12080-122">Clonar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="12080-122">Clone the sample application</span></span>

<span data-ttu-id="12080-123">Agora, clonaremos um aplicativo de Tabela do github, definiremos a cadeia de conexão e o executaremos.</span><span class="sxs-lookup"><span data-stu-id="12080-123">Now let's clone a Table app from github, set the connection string, and run it.</span></span> <span data-ttu-id="12080-124">Você verá como é fácil trabalhar usando dados de forma programática.</span><span class="sxs-lookup"><span data-stu-id="12080-124">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="12080-125">Abra uma janela de terminal do Git, como git bash, e `cd` para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="12080-125">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="12080-126">Execute o comando a seguir para clonar o repositório de exemplo.</span><span class="sxs-lookup"><span data-stu-id="12080-126">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="12080-127">Em seguida, abra o arquivo da solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12080-127">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="12080-128">Examine o código</span><span class="sxs-lookup"><span data-stu-id="12080-128">Review the code</span></span>

<span data-ttu-id="12080-129">Façamos uma rápida análise do que está acontecendo no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="12080-129">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="12080-130">Abra o arquivo Program.cs e você verá que essas linhas de código criam os recursos do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="12080-130">Open the Program.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="12080-131">O CloudTableClient é inicializado.</span><span class="sxs-lookup"><span data-stu-id="12080-131">The CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="12080-132">A nova tabela é criada se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="12080-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="12080-133">Um novo contêiner de Tabela é criado.</span><span class="sxs-lookup"><span data-stu-id="12080-133">A new Table container is created.</span></span> <span data-ttu-id="12080-134">Você observará que esse código é muito semelhante a um SDK normal de Armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="12080-134">You will notice this code very similar to regular Azure Table storage SDK.</span></span> 

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

## <a name="update-your-connection-string"></a><span data-ttu-id="12080-135">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="12080-135">Update your connection string</span></span>

<span data-ttu-id="12080-136">Agora vamos atualizar as informações de cadeia de conexão para que o seu aplicativo possa se comunicar com o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="12080-136">Now we'll update the connection string information so your app can talk to Azure Cosmos DB.</span></span> 

1. <span data-ttu-id="12080-137">No Visual Studio, abra o arquivo app.config.</span><span class="sxs-lookup"><span data-stu-id="12080-137">In Visual Studio, open the app.config file.</span></span> 

2. <span data-ttu-id="12080-138">No [portal do Azure](http://portal.azure.com/), no menu de navegação à esquerda do BD Cosmos do Azure, clique em **Cadeia de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="12080-138">In the [Azure portal](http://portal.azure.com/), in the Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="12080-139">Em seguida, no novo painel, clique no botão Copiar da cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="12080-139">Then in the new pane click the copy button for the connection string.</span></span> 

    ![Exibir e copiar o ponto de extremidade e a chave de conta no painel Cadeia de Conexão](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="12080-141">Cole o valor no arquivo PP.config como o valor de PremiumStorageConnectionString.</span><span class="sxs-lookup"><span data-stu-id="12080-141">Paste the value into the app.config file as the value of the PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="12080-142">Você pode deixar o StandardStorageConnectionString como está.</span><span class="sxs-lookup"><span data-stu-id="12080-142">You can leave the StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="12080-143">Agora, você atualizou o aplicativo com todas as informações necessárias para se comunicar com o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="12080-143">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="run-the-web-app"></a><span data-ttu-id="12080-144">Executar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="12080-144">Run the web app</span></span>

1. <span data-ttu-id="12080-145">No Visual Studio, clique com o botão direito do mouse no projeto **PremiumTableGetStarted** no **Gerenciador de Soluções** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="12080-145">In Visual Studio, right-click on the **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="12080-146">Na caixa **procurar** do NuGet, digite *WindowsAzure.Storage-PremiumTable*.</span><span class="sxs-lookup"><span data-stu-id="12080-146">In the NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="12080-147">Marque a caixa de seleção **Incluir pré-lançamento**.</span><span class="sxs-lookup"><span data-stu-id="12080-147">Check the **Include prerelease** box.</span></span> 

4. <span data-ttu-id="12080-148">Nos resultados, instale a biblioteca **WindowsAzure.Storage-PremiumTable**.</span><span class="sxs-lookup"><span data-stu-id="12080-148">From the results, install the **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="12080-149">Isso instala o pacote da API de Tabela do BD Cosmos do Azure de versão prévia, bem como todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="12080-149">This installs the preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="12080-150">Observe que se trata de um pacote NuGet diferente do pacote do Armazenamento do Microsoft Azure usado pelo armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="12080-150">Note that this is a different NuGet package than the Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="12080-151">Clique em CTRL + F5 para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="12080-151">Click CTRL + F5 to run the application.</span></span>

    <span data-ttu-id="12080-152">A janela do console exibe os dados que estão sendo adicionados, recuperados, consultados, substituídos e excluídos da tabela.</span><span class="sxs-lookup"><span data-stu-id="12080-152">The console window displays the data being added, retrieved, queried, replaced and deleted from the table.</span></span> <span data-ttu-id="12080-153">Quando o script for concluído, pressione qualquer tecla duas vezes para fechar a janela do console.</span><span class="sxs-lookup"><span data-stu-id="12080-153">When the script completes, press any key to close the console window.</span></span> 
    
    ![Saída de console do início rápido](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="12080-155">Se você deseja ver as novas entidades no Data Explorer, basta comentar as linhas 188 208 em program.cs para que elas não sejam excluídas e execute o exemplo novamente.</span><span class="sxs-lookup"><span data-stu-id="12080-155">If you want to see the new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run the sample again.</span></span> 

    <span data-ttu-id="12080-156">Agora, você pode ir para o Data Explorer, clicar em **Atualizar**, expandir a tabela **Pessoas** e clicar em **Entidades** para trabalhar com esses novos dados.</span><span class="sxs-lookup"><span data-stu-id="12080-156">You can now go back to Data Explorer, click **Refresh**, expand the **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![Novas entidades no Data Explorer](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="12080-158">Examinar SLAs no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="12080-158">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="12080-159">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="12080-159">Clean up resources</span></span>

<span data-ttu-id="12080-160">Se você não continuar usando este aplicativo, exclua todos os recursos criados por esse início rápido no portal do Azure com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="12080-160">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="12080-161">No menu à esquerda no Portal do Azure, clique em **Grupos de recursos** e depois clique no nome do recurso criado.</span><span class="sxs-lookup"><span data-stu-id="12080-161">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="12080-162">Em sua página de grupo de recursos, clique em **Excluir**, digite o nome do recurso para excluir na caixa de texto e depois clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="12080-162">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12080-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12080-163">Next steps</span></span>

<span data-ttu-id="12080-164">Neste início rápido, você aprendeu como criar uma conta do BD Cosmos do Azure, como criar uma tabela usando o Data Explorer e como executar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="12080-164">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span></span>  <span data-ttu-id="12080-165">Agora, você pode consultar os dados usando a API de Tabela.</span><span class="sxs-lookup"><span data-stu-id="12080-165">Now you can query your data using the Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="12080-166">Consultar usando a API de Tabela</span><span class="sxs-lookup"><span data-stu-id="12080-166">Query using the Table API</span></span>](tutorial-query-table.md)

