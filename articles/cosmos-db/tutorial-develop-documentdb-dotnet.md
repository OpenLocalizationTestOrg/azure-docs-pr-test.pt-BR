---
title: 'Azure Cosmos DB: Desenvolver com a API DocumentDB no .NET | Microsoft Docs'
description: Aprenda a desenvolver com a API DocumentDB do Azure Cosmos DB usando o .NET
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 2eed74ae9bd173b0944ec190dfe5d9a4bdc54c37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmosdb-develop-with-the-documentdb-api-in-net"></a><span data-ttu-id="363e1-103">Azure Cosmos DB: Desenvolver com a API DocumentDB no .NET</span><span class="sxs-lookup"><span data-stu-id="363e1-103">Azure CosmosDB: Develop with the DocumentDB API in .NET</span></span>

<span data-ttu-id="363e1-104">O Azure Cosmos DB é o serviço de banco de dados multimodelo distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="363e1-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="363e1-105">É possível criar e consultar rapidamente documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="363e1-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="363e1-106">Este tutorial mostra como criar uma conta do Azure Cosmos DB usando o portal do Azure e, em seguida, criar um banco de dados de documentos e uma coleção com uma [chave de partição](documentdb-partition-data.md#partition-keys) usando a [API .NET do DocumentDB](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="363e1-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using the [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="363e1-107">Ao definindo uma chave de partição quando você cria uma coleção, seu aplicativo está preparado para dimensionar com facilidade à medida que seus dados crescem.</span><span class="sxs-lookup"><span data-stu-id="363e1-107">By defining a partition key when you create a collection, your application is prepared to scale effortlessly as your data grows.</span></span> 

<span data-ttu-id="363e1-108">Este tutorial cobre as seguintes tarefas usando [API .NET do DocumentDB](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="363e1-108">This tutorial covers the following tasks by using the [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="363e1-109">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="363e1-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="363e1-110">Criar um banco de dados e uma coleção com uma chave de partição</span><span class="sxs-lookup"><span data-stu-id="363e1-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="363e1-111">Criar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="363e1-111">Create JSON documents</span></span>
> * <span data-ttu-id="363e1-112">Atualizar um documento</span><span class="sxs-lookup"><span data-stu-id="363e1-112">Update a document</span></span>
> * <span data-ttu-id="363e1-113">Consultar coleções particionadas</span><span class="sxs-lookup"><span data-stu-id="363e1-113">Query partitioned collections</span></span>
> * <span data-ttu-id="363e1-114">Executar procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="363e1-114">Run stored procedures</span></span>
> * <span data-ttu-id="363e1-115">Excluir um documento</span><span class="sxs-lookup"><span data-stu-id="363e1-115">Delete a document</span></span>
> * <span data-ttu-id="363e1-116">Excluir um banco de dados</span><span class="sxs-lookup"><span data-stu-id="363e1-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="363e1-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="363e1-117">Prerequisites</span></span>
<span data-ttu-id="363e1-118">Certifique-se que você tem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="363e1-118">Please make sure you have the following:</span></span>

* <span data-ttu-id="363e1-119">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="363e1-119">An active Azure account.</span></span> <span data-ttu-id="363e1-120">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="363e1-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="363e1-121">Como alternativa, você pode usar o [emulador do Azure Cosmos DB](local-emulator.md) para este tutorial se você deseja usar um ambiente local que emula o serviço do Azure DocumentDB para fins de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="363e1-121">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like to use a local environment that emulates the Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="363e1-122">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="363e1-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="363e1-123">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="363e1-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="363e1-124">Vamos começar criando uma conta do Azure Cosmos DB no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="363e1-124">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="363e1-125">Já tem uma conta do Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="363e1-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="363e1-126">Nesse caso, pule para [Configurar sua solução do Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="363e1-126">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="363e1-127">Você tinha uma conta do Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="363e1-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="363e1-128">Se sua conta agora é uma conta do Azure Cosmos DB, você pode pular para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="363e1-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="363e1-129">Se estiver usando o Emulador do Azure Cosmos DB, execute as etapas em [Emulador do Azure Cosmos DB](local-emulator.md) para configurar o emulador e pule para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="363e1-129">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="363e1-130"><a id="SetupVS"></a>Configurar sua solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="363e1-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="363e1-131">Abra o **Visual Studio** no seu computador.</span><span class="sxs-lookup"><span data-stu-id="363e1-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="363e1-132">No menu **Arquivo**, selecione **Novo** e depois **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="363e1-132">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="363e1-133">Na caixa de diálogo **Novo Projeto**, selecione **Modelos** / **Visual C#** / **Aplicativo de Console (.NET Framework)**, nomeie o projeto e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="363e1-133">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="363e1-134">![Captura de tela da janela Novo Projeto](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="363e1-134">![Screen shot of the New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="363e1-135">No **Gerenciador de Soluções**, clique com o botão direito do mouse no seu novo aplicativo de console, que está em sua solução do Visual Studio e clique em **gerenciar pacotes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="363e1-135">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Captura de tela do menu exibido pelo clique com o botão direito do mouse para o projeto](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="363e1-137">Na guia **NuGet**, clique em **Procurar** e digite **documentdb** na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="363e1-137">In the **NuGet** tab, click **Browse**, and type **documentdb** in the search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="363e1-138">Nos resultados, encontre **Microsoft.Azure.DocumentDB** e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="363e1-138">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="363e1-139">A ID do pacote para a Biblioteca de Clientes do Azure Cosmos DB é [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="363e1-139">The package ID for the Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="363e1-140">![Captura de tela do menu NuGet para localizar documentos do SDK do cliente do Azure Cosmos DB](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="363e1-140">![Screen shot of the NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="363e1-141">Se receber uma mensagem sobre a análise das alterações para a solução, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="363e1-141">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="363e1-142">Se receber uma mensagem sobre a aceitação da licença, clique em **Aceito**.</span><span class="sxs-lookup"><span data-stu-id="363e1-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="363e1-143"><a id="Connect"></a>Adicionar referências ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="363e1-143"><a id="Connect"></a>Add references to your project</span></span>
<span data-ttu-id="363e1-144">As etapas restantes neste tutorial fornecem os trechos de código da API do DocumentDB necessárias para criar e atualizar os recursos do Azure Cosmos DB em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="363e1-144">The remaining steps in this tutorial provide the DocumentDB API code snippets required to create and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="363e1-145">Primeiro, adicione essas referências ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="363e1-145">First, add these references to your application.</span></span>
<!---These aren't added by default when you install the pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="363e1-146"><a id="add-references"></a>Conecte seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="363e1-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="363e1-147">Em seguida, adicione essas duas constantes e sua variável de *cliente* no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="363e1-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="363e1-148">Em seguida, volte ao [portal do Azure](https://portal.azure.com) para recuperar a URL do ponto de extremidade e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="363e1-148">Then, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="363e1-149">A URL do ponto de extremidade e a chave primária são necessárias para que seu aplicativo reconheça onde deve se conectar e para que o Azure Cosmos DB confie na conexão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="363e1-149">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="363e1-150">No portal do Azure, navegue até a sua conta do Azure Cosmos DB, clique em **Chaves** e, em seguida, clique em **Chaves de leitura/gravação**.</span><span class="sxs-lookup"><span data-stu-id="363e1-150">In the Azure portal, navigate to your Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="363e1-151">Copie o URI do portal e cole-o em `<your endpoint URL>` no arquivo program.cs.</span><span class="sxs-lookup"><span data-stu-id="363e1-151">Copy the URI from the portal and paste it over `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="363e1-152">Em seguida, copie a CHAVE PRIMÁRIA do portal e cole-a em `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="363e1-152">Then copy the PRIMARY KEY from the portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="363e1-153">Certifique-se de remover o `<` e `>` de seus valores.</span><span class="sxs-lookup"><span data-stu-id="363e1-153">Be sure to remove the `<` and `>` from your values.</span></span>

![Captura de tela do portal do Azure usado pelo tutorial do NoSQL para criar um aplicativo de console em C#.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="363e1-156"><a id="instantiate"></a>Criar uma instância do DocumentClient</span><span class="sxs-lookup"><span data-stu-id="363e1-156"><a id="instantiate"></a>Instantiate the DocumentClient</span></span>

<span data-ttu-id="363e1-157">Agora, crie uma nova instância do **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="363e1-157">Now, create a new instance of the **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="363e1-158"><a id="create-database"></a>Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="363e1-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="363e1-159">Em seguida, crie um [banco de dados](documentdb-resources.md#databases) do Azure Cosmos DB usando o método [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) ou o método [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) da classe **DocumentClient** a partir do [SDK .NET do DocumentDB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="363e1-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class from the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="363e1-160">Um banco de dados é o contêiner lógico de armazenamento de documentos JSON particionado em coleções.</span><span class="sxs-lookup"><span data-stu-id="363e1-160">A database is the logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="363e1-161">Escolha uma chave de partição</span><span class="sxs-lookup"><span data-stu-id="363e1-161">Decide on a partition key</span></span> 

<span data-ttu-id="363e1-162">Coleções são contêineres para armazenamento de documentos.</span><span class="sxs-lookup"><span data-stu-id="363e1-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="363e1-163">Elas são recursos lógicos e podem [abranger uma ou mais partições físicas](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="363e1-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="363e1-164">Uma [chave de partição](documentdb-partition-data.md) é uma propriedade (ou caminho) nos documentos que é ser usada para distribuir dados entre vários servidores ou partições.</span><span class="sxs-lookup"><span data-stu-id="363e1-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used to distribute your data among the servers or partitions.</span></span> <span data-ttu-id="363e1-165">Todos os documentos com a mesma chave de partição são armazenados na mesma partição.</span><span class="sxs-lookup"><span data-stu-id="363e1-165">All documents with the same partition key are stored in the same partition.</span></span> 

<span data-ttu-id="363e1-166">Determinar uma chave de partição é uma decisão importante que deve ser tomada antes de você criar uma coleção.</span><span class="sxs-lookup"><span data-stu-id="363e1-166">Determining a partition key is an important decision to make before you create a collection.</span></span> <span data-ttu-id="363e1-167">As chaves de partição são uma propriedade (ou caminho) nos documentos que podem ser usadas pelo Azure Cosmos DB para distribuir dados entre vários servidores ou partições.</span><span class="sxs-lookup"><span data-stu-id="363e1-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB to distribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="363e1-168">O Cosmos DB faz o hash do valor da chave de partição e usa o resultado com hash para determinar em qual partição deve armazenar o item.</span><span class="sxs-lookup"><span data-stu-id="363e1-168">Cosmos DB hashes the partition key value and uses the hashed result to determine the partition in which to store the document.</span></span> <span data-ttu-id="363e1-169">Todos os documentos com a mesma chave de partição são armazenados na mesma partição e as chaves de partição não podem ser alteradas depois que uma coleção é criada.</span><span class="sxs-lookup"><span data-stu-id="363e1-169">All documents with the same partition key are stored in the same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="363e1-170">Para este tutorial, vamos definir a chave de partição para `/deviceId` para que todos os dados para um único dispositivo sejam armazenados em uma única partição.</span><span class="sxs-lookup"><span data-stu-id="363e1-170">For this tutorial, we're going to set the partition key to `/deviceId` so that the all the data for a single device is stored in a single partition.</span></span> <span data-ttu-id="363e1-171">Você deseja escolher uma chave de partição que tem um grande número de valores, cada um dos quais são usados com quase a mesma frequência para garantir que o Cosmos DB pode balancear a carga conforme os dados aumentam e atingem a taxa de transferência total da coleção.</span><span class="sxs-lookup"><span data-stu-id="363e1-171">You want to choose a partition key that has a large number of values, each of which are used at about the same frequency to ensure Cosmos DB can load balance as your data grows and achieve the full throughput of the collection.</span></span> 

<span data-ttu-id="363e1-172">Para obter mais informações sobre particionamento, consulte [Como particionar e dimensionar no Azure Cosmos DB?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="363e1-172">For more information about partitioning, see [How to partition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="363e1-173"><a id="CreateColl"></a>Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="363e1-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="363e1-174">Agora que conhecemos a nossa chave de partição, `/deviceId`, permite criar uma [coleção](documentdb-resources.md#collections) usando o método [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) ou o método [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) da classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="363e1-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="363e1-175">Uma coleção é um contêiner de documentos JSON e qualquer lógica de aplicativo JavaScript associada.</span><span class="sxs-lookup"><span data-stu-id="363e1-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="363e1-176">Criar uma coleção tem implicações de preços, pois você está reservando a taxa de transferência para o aplicativo se comunicar com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="363e1-176">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="363e1-177">Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="363e1-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here the JSON property deviceId is used  
// as the partition key to spread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

<span data-ttu-id="363e1-178">Esse método faz uma chamada da API REST ao Azure Cosmos DB e o serviço provisiona várias partições com base na produtividade solicitada.</span><span class="sxs-lookup"><span data-stu-id="363e1-178">This method makes a REST API call to Azure Cosmos DB, and the service provisions a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="363e1-179">Você pode alterar a taxa de transferência de uma coleção conforme suas necessidades de desempenho aumentarem usando o SDK ou o [portal do Azure](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="363e1-179">You can change the throughput of a collection as your performance needs evolve using the SDK or the [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="363e1-180"><a id="CreateDoc"></a>Criar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="363e1-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="363e1-181">Vamos inserir alguns documentos JSON no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="363e1-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="363e1-182">Um [documento](documentdb-resources.md#documents) pode ser criado usando o método [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) da classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="363e1-182">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="363e1-183">Os documentos são conteúdo JSON (arbitrário) definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="363e1-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="363e1-184">Essa classe de exemplo contém uma leitura de dispositivo e uma chamada para CreateDocumentAsync para inserir uma nova leitura de dispositivo em uma coleção.</span><span class="sxs-lookup"><span data-stu-id="363e1-184">This sample class contains a device reading, and a call to CreateDocumentAsync to insert a new device reading into a collection.</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here the partition key is extracted 
// as "XMS-0001" based on the collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a><span data-ttu-id="363e1-185">Ler dados</span><span class="sxs-lookup"><span data-stu-id="363e1-185">Read data</span></span>

<span data-ttu-id="363e1-186">Vamos ler o documento pela sua chave de partição e Id usando o método ReadDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="363e1-186">Let's read the document by its partition key and Id using the ReadDocumentAsync method.</span></span> <span data-ttu-id="363e1-187">Observe que as leituras incluem um valor de PartitionKey (correspondente ao cabeçalho de solicitação `x-ms-documentdb-partitionkey` na API REST).</span><span class="sxs-lookup"><span data-stu-id="363e1-187">Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the Id to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="363e1-188">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="363e1-188">Update data</span></span>

<span data-ttu-id="363e1-189">Agora, vamos atualizar alguns dados usando o método ReplaceDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="363e1-189">Now let's update some data using the ReplaceDocumentAsync method.</span></span>

```csharp
// Update the document. Partition key is not required, again extracted from the document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="363e1-190">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="363e1-190">Delete data</span></span>

<span data-ttu-id="363e1-191">Agora vamos excluir um documento pela sua chave de partição e id usando o método DeleteDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="363e1-191">Now lets delete a document by partition key and id by using the DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. The partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="363e1-192">Consultar coleções particionadas</span><span class="sxs-lookup"><span data-stu-id="363e1-192">Query partitioned collections</span></span>

<span data-ttu-id="363e1-193">Quando você consulta dados em coleções particionadas, o Azure Cosmos DB roteia automaticamente a consulta para as partições que correspondem aos valores de chave de partição especificados no filtro (caso haja algum).</span><span class="sxs-lookup"><span data-stu-id="363e1-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="363e1-194">Por exemplo, esta consulta é roteada para apenas a partição que contém a chave de partição "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="363e1-194">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="363e1-195">A consulta a seguir não tem um filtro na chave de partição (DeviceId) e é distribuída para todas as partições em que ela é executada no índice da partição.</span><span class="sxs-lookup"><span data-stu-id="363e1-195">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="363e1-196">Observe que você precisa especificar o EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` na API REST) para fazer com que o SDK execute uma consulta em partições.</span><span class="sxs-lookup"><span data-stu-id="363e1-196">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="363e1-197">Execução de consulta paralela</span><span class="sxs-lookup"><span data-stu-id="363e1-197">Parallel query execution</span></span>
<span data-ttu-id="363e1-198">Os SDKs de DocumentDB do Azure Cosmos DB 1.9.0 e superiores são compatíveis com execução de consulta paralela, que permite realizar consultas de baixa latência em coleções particionadas, mesmo quando elas precisam tocar um grande número de partições.</span><span class="sxs-lookup"><span data-stu-id="363e1-198">The Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="363e1-199">Por exemplo, a consulta a seguir é configurada para ser executada paralelamente entre partições.</span><span class="sxs-lookup"><span data-stu-id="363e1-199">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="363e1-200">Você pode gerenciar a execução de consulta paralela ajustando os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="363e1-200">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="363e1-201">Ao definir `MaxDegreeOfParallelism`, é possível controlar o grau de paralelismo, isto é, o número máximo de conexões de rede simultâneas com as partições da coleção.</span><span class="sxs-lookup"><span data-stu-id="363e1-201">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the collection's partitions.</span></span> <span data-ttu-id="363e1-202">Se você definir esse valor como -1, o grau de paralelismo será gerenciado pelo SDK.</span><span class="sxs-lookup"><span data-stu-id="363e1-202">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="363e1-203">Se o `MaxDegreeOfParallelism` não for especificado nem definido para 0, que é o valor padrão, haverá uma única conexão de rede para as partições da coleção.</span><span class="sxs-lookup"><span data-stu-id="363e1-203">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the collection's partitions.</span></span>
* <span data-ttu-id="363e1-204">Definindo `MaxBufferedItemCount`, você pode compensar a latência da consulta e a utilização da memória no lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="363e1-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="363e1-205">Se você omitir esse parâmetro ou defini-lo como -1, o número de itens armazenados em buffer durante a execução da consulta paralela será gerenciado pelo SDK.</span><span class="sxs-lookup"><span data-stu-id="363e1-205">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="363e1-206">Dado o mesmo estado da coleção, uma consulta paralela retornará resultados na mesma ordem da execução serial.</span><span class="sxs-lookup"><span data-stu-id="363e1-206">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="363e1-207">Ao executar uma consulta entre partições que inclui classificação (ORDER BY e/ou TOP), o SDK do DocumentDB emite a consulta paralelamente entre partições e mescla os resultados parcialmente classificados no lado do cliente para produzir resultados ordenados globalmente.</span><span class="sxs-lookup"><span data-stu-id="363e1-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the DocumentDB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="363e1-208">Executar procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="363e1-208">Execute stored procedures</span></span>
<span data-ttu-id="363e1-209">Por último, você poderá executar transações atômicas em documentos com a mesma ID de dispositivo, por exemplo, se você estiver mantendo agregações ou o estado mais recente de um dispositivo em um único documento adicionado o código a seguir ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="363e1-209">Lastly, you can execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single document by adding the following code to your project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="363e1-210">E isso é tudo!</span><span class="sxs-lookup"><span data-stu-id="363e1-210">And that's it!</span></span> <span data-ttu-id="363e1-211">Esses são os principais componentes de um aplicativo do Azure Cosmos DB que usa uma chave de partição para dimensionar com eficiência a distribuição de dados em partições.</span><span class="sxs-lookup"><span data-stu-id="363e1-211">those are the main components of an Azure Cosmos DB application that uses a partition key to efficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="363e1-212">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="363e1-212">Clean up resources</span></span>

<span data-ttu-id="363e1-213">Se você não continuar usando este aplicativo, exclua todos os recursos criados por esse tutorial no portal do Azure com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="363e1-213">If you're not going to continue to use this app, delete all resources created by this tutorial in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="363e1-214">No menu à esquerda no portal do Azure, clique em **Grupos de recursos** e depois clique no nome exclusivo do recurso criado.</span><span class="sxs-lookup"><span data-stu-id="363e1-214">From the left-hand menu in the Azure portal, click **Resource groups** and then click the unique name of the resource you created.</span></span> 
2. <span data-ttu-id="363e1-215">Em sua página de grupo de recursos, clique em **Excluir**, digite o nome do recurso para excluir na caixa de texto e depois clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="363e1-215">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="363e1-216">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="363e1-216">Next steps</span></span>

<span data-ttu-id="363e1-217">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="363e1-217">In this tutorial, you've done the following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="363e1-218">Criou uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="363e1-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="363e1-219">Criou um banco de dados e uma coleção com uma chave de partição</span><span class="sxs-lookup"><span data-stu-id="363e1-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="363e1-220">Criou documentos JSON</span><span class="sxs-lookup"><span data-stu-id="363e1-220">Created JSON documents</span></span>
> * <span data-ttu-id="363e1-221">Atualizou um documento</span><span class="sxs-lookup"><span data-stu-id="363e1-221">Updated a document</span></span>
> * <span data-ttu-id="363e1-222">Consultou coleções particionadas</span><span class="sxs-lookup"><span data-stu-id="363e1-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="363e1-223">Executou um procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="363e1-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="363e1-224">Excluiu um documento</span><span class="sxs-lookup"><span data-stu-id="363e1-224">Deleted a document</span></span>
> * <span data-ttu-id="363e1-225">Excluiu um banco de dados</span><span class="sxs-lookup"><span data-stu-id="363e1-225">Deleted a database</span></span>

<span data-ttu-id="363e1-226">Agora você pode prosseguir para o próximo tutorial e importar dados adicionais para a sua conta do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="363e1-226">You can now proceed to the next tutorial and import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="363e1-227">Importar dados para o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="363e1-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
