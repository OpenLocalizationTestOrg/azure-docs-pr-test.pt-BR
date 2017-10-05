---
title: 'Azure Cosmos DB: Desenvolver com a API no .NET | Microsoft Docs'
description: Aprenda a desenvolver com a API DocumentDB do Azure Cosmos DB usando o .NET
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: eeaa0c4f84a408815371742334d2ba7ce600b72f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-develop-with-the-graph-api-in-net"></a><span data-ttu-id="3ba67-103">Azure Cosmos DB: Desenvolver com a API do Graph no .NET</span><span class="sxs-lookup"><span data-stu-id="3ba67-103">Azure Cosmos DB: Develop with the Graph API in .NET</span></span>
<span data-ttu-id="3ba67-104">O Azure Cosmos DB é o serviço de banco de dados multimodelo distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3ba67-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="3ba67-105">É possível criar e consultar rapidamente documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3ba67-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="3ba67-106">Este tutorial demonstra como criar uma conta do Azure Cosmos DB usando o portal do Azure e como criar um banco de dados do gráfico e o contêiner.</span><span class="sxs-lookup"><span data-stu-id="3ba67-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal and how to create a graph database and container.</span></span> <span data-ttu-id="3ba67-107">O aplicativo, em seguida, cria uma rede social simple com quatro pessoas que usam a [API do Graph](graph-sdk-dotnet.md) (visualização), em seguida, percorre e consulta o gráfico usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3ba67-107">The application then creates a simple social network with four people using the [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries the graph using Gremlin.</span></span>

<span data-ttu-id="3ba67-108">Este tutorial cobre as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="3ba67-108">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3ba67-109">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3ba67-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="3ba67-110">Criar um banco de dados do gráfico e um contêiner</span><span class="sxs-lookup"><span data-stu-id="3ba67-110">Create a graph database and container</span></span>
> * <span data-ttu-id="3ba67-111">Serializar os vértices e bordas aos objetos .NET</span><span class="sxs-lookup"><span data-stu-id="3ba67-111">Serialize vertices and edges to .NET objects</span></span>
> * <span data-ttu-id="3ba67-112">Adicionar vértices e bordas</span><span class="sxs-lookup"><span data-stu-id="3ba67-112">Add vertices and edges</span></span>
> * <span data-ttu-id="3ba67-113">Consultar o gráfico usando Gremlin</span><span class="sxs-lookup"><span data-stu-id="3ba67-113">Query the graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="3ba67-114">Gráficos no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3ba67-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="3ba67-115">Você pode usar o Azure Cosmos DB para criar, atualizar e consultar gráficos usando a biblioteca [Microsoft.Azure.Graphs](graph-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3ba67-115">You can use Azure Cosmos DB to create, update, and query graphs using the [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="3ba67-116">A biblioteca Microsoft.Azure.Graph fornece um método de extensão único `CreateGremlinQuery<T>` sobre a classe `DocumentClient` para executar consultas de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3ba67-116">The Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of the `DocumentClient` class to execute Gremlin queries.</span></span>

<span data-ttu-id="3ba67-117">Gremlin é uma linguagem de programação funcional que oferece suporte a operações de gravação (DML) e operações de consulta e passagem.</span><span class="sxs-lookup"><span data-stu-id="3ba67-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="3ba67-118">Abordamos alguns exemplos neste artigo para introdução ao uso do Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3ba67-118">We cover a few examples in this article to get your started with Gremlin.</span></span> <span data-ttu-id="3ba67-119">Veja [consultas Gremlin](gremlin-support.md) para obter uma explicação detalhada dos recursos Gremlin disponíveis no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3ba67-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3ba67-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3ba67-120">Prerequisites</span></span>
<span data-ttu-id="3ba67-121">Certifique-se que você tem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3ba67-121">Please make sure you have the following:</span></span>

* <span data-ttu-id="3ba67-122">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba67-122">An active Azure account.</span></span> <span data-ttu-id="3ba67-123">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="3ba67-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="3ba67-124">Como alternativa, você pode usar o [Emulador do DocumentDB do Azure](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3ba67-124">Alternatively, you can use the [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="3ba67-125">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="3ba67-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="3ba67-126">Criar uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="3ba67-126">Create database account</span></span>

<span data-ttu-id="3ba67-127">Vamos começar criando uma conta do Azure Cosmos DB no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba67-127">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="3ba67-128">Já tem uma conta do Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="3ba67-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="3ba67-129">Nesse caso, pule para [Configurar sua solução do Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="3ba67-129">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="3ba67-130">Você tinha uma conta do Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="3ba67-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="3ba67-131">Se sua conta agora é uma conta do Azure Cosmos DB, você pode pular para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="3ba67-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="3ba67-132">Se estiver usando o Emulador do Azure Cosmos DB, execute as etapas em [Emulador do Azure Cosmos DB](local-emulator.md) para configurar o emulador e pule para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="3ba67-132">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="3ba67-133"><a id="SetupVS"></a>Configurar sua solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3ba67-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="3ba67-134">Abra o **Visual Studio** no seu computador.</span><span class="sxs-lookup"><span data-stu-id="3ba67-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="3ba67-135">No menu **Arquivo**, selecione **Novo** e depois **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="3ba67-135">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="3ba67-136">Na caixa de diálogo **Novo Projeto**, selecione **Modelos** / **Visual C#** / **Aplicativo de Console (.NET Framework)**, nomeie o projeto e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ba67-136">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="3ba67-137">No **Gerenciador de Soluções**, clique com o botão direito do mouse no seu novo aplicativo de console, que está em sua solução do Visual Studio e clique em **gerenciar pacotes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="3ba67-137">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="3ba67-138">Na guia **NuGet**, clique em **Procurar**e digite **Microsoft.Azure.Graphs** na caixa de pesquisa e marque **Incluir versões de pré-lançamento**.</span><span class="sxs-lookup"><span data-stu-id="3ba67-138">In the **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in the search box, and check the **Include prerelease versions**.</span></span>
6. <span data-ttu-id="3ba67-139">Nos resultados, encontre **Microsoft.Azure.Graphs** e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="3ba67-139">Within the results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="3ba67-140">Se receber uma mensagem sobre a análise das alterações para a solução, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ba67-140">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="3ba67-141">Se receber uma mensagem sobre a aceitação da licença, clique em **Aceito**.</span><span class="sxs-lookup"><span data-stu-id="3ba67-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="3ba67-142">A biblioteca `Microsoft.Azure.Graphs` fornece um método de extensão único `CreateGremlinQuery<T>` para executar operações de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3ba67-142">The `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="3ba67-143">Gremlin é uma linguagem de programação funcional que oferece suporte a operações de gravação (DML) e operações de consulta e passagem.</span><span class="sxs-lookup"><span data-stu-id="3ba67-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="3ba67-144">Abordamos alguns exemplos neste artigo para introdução ao uso do Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3ba67-144">We cover a few examples in this article to get your started with Gremlin.</span></span> <span data-ttu-id="3ba67-145">[Consultas Gremlin](gremlin-support.md) possui uma explicação detalhada dos recursos Gremlin no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3ba67-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="3ba67-146"><a id="add-references"></a>Conecte seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="3ba67-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="3ba67-147">Adicionar essas duas constantes e sua variável de *cliente* no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ba67-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="3ba67-148">Em seguida, volte ao [portal do Azure](https://portal.azure.com) para recuperar a URL do ponto de extremidade e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="3ba67-148">Next, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="3ba67-149">A URL do ponto de extremidade e a chave primária são necessárias para que seu aplicativo reconheça onde deve se conectar e para que o Azure Cosmos DB confie na conexão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ba67-149">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span> 

<span data-ttu-id="3ba67-150">No portal do Azure, navegue até a sua conta do Azure Cosmos DB, clique em **Chaves** e, em seguida, clique em **Chaves de leitura/gravação**.</span><span class="sxs-lookup"><span data-stu-id="3ba67-150">In the Azure portal, navigate to your Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="3ba67-151">Copie o URI do portal e cole-o sobre `Endpoint` na propriedade do ponto de extremidade acima.</span><span class="sxs-lookup"><span data-stu-id="3ba67-151">Copy the URI from the portal and paste it over `Endpoint` in the endpoint property above.</span></span> <span data-ttu-id="3ba67-152">Em seguida, copie a CHAVE PRIMÁRIA do portal e cole-a na propriedade `AuthKey` acima.</span><span class="sxs-lookup"><span data-stu-id="3ba67-152">Then copy the PRIMARY KEY from the portal and paste it into the `AuthKey` property above.</span></span> 

<span data-ttu-id="3ba67-153">![Captura de tela do portal do Azure usada pelo tutorial para criar um aplicativo C#.</span><span class="sxs-lookup"><span data-stu-id="3ba67-153">![Screen shot of the Azure portal used by the tutorial to create a C# application.</span></span> <span data-ttu-id="3ba67-154">Mostra para uma conta do Azure Cosmos DB o botão CHAVES realçado na barra de navegação do Azure Cosmos DB e os valores de URI e CHAVE PRIMÁRIA realçados na folha Chaves][chaves]</span><span class="sxs-lookup"><span data-stu-id="3ba67-154">Shows an Azure Cosmos DB account the KEYS button highlighted on the Azure Cosmos DB navigation , and the URI and PRIMARY KEY values highlighted on the Keys blade][keys]</span></span> 
 
## <span data-ttu-id="3ba67-155"><a id="instantiate"></a>Criar uma instância do DocumentClient</span><span class="sxs-lookup"><span data-stu-id="3ba67-155"><a id="instantiate"></a>Instantiate the DocumentClient</span></span> 
<span data-ttu-id="3ba67-156">Em seguida, crie uma nova instância do **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="3ba67-156">Next, create a new instance of the **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="3ba67-157"><a id="create-database"></a>Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="3ba67-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="3ba67-158">Agora, crie um [banco de dados](documentdb-resources.md#databases) do Azure Cosmos DB usando o método [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) ou o método [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) da classe **DocumentClient** a partir do [SDK .NET do DocumentDB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3ba67-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class from the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="3ba67-159">Criar um gráfico</span><span class="sxs-lookup"><span data-stu-id="3ba67-159">Create a graph</span></span> 

<span data-ttu-id="3ba67-160">Em seguida, crie um contêiner de gráfico usando o usando o método [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) ou o método [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) da classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="3ba67-160">Next, create a graph container by using the using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="3ba67-161">Uma coleção é um contêiner de entidades de gráfico.</span><span class="sxs-lookup"><span data-stu-id="3ba67-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="3ba67-162"><a id="serializing"></a>Serializar os vértices e bordas aos objetos .NET</span><span class="sxs-lookup"><span data-stu-id="3ba67-162"><a id="serializing"></a>Serialize vertices and edges to .NET objects</span></span>
<span data-ttu-id="3ba67-163">O Azure Cosmos DB usa o [formato de arame GraphSON](gremlin-support.md), que define um esquema JSON de vértices, bordas e propriedades.</span><span class="sxs-lookup"><span data-stu-id="3ba67-163">Azure Cosmos DB uses the [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="3ba67-164">O SDK do .NET do Azure DB Cosmos inclui JSON.NET como uma dependência, e isso nos permite serializar/desserializar GraphSON em objetos .NET com os quais podemos trabalhar no código.</span><span class="sxs-lookup"><span data-stu-id="3ba67-164">The Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us to serialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="3ba67-165">Por exemplo, vamos trabalhar com uma rede social simples com quatro pessoas.</span><span class="sxs-lookup"><span data-stu-id="3ba67-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="3ba67-166">Veremos como criar vértices `Person`, adicionar relacionamentos `Knows` entre eles, em seguida, consultar e percorrer o gráfico para localizar relacionamentos "amigo de amigo".</span><span class="sxs-lookup"><span data-stu-id="3ba67-166">We look at how to create `Person` vertices, add `Knows` relationships between them, then query and traverse the graph to find "friend of friend" relationships.</span></span> 

<span data-ttu-id="3ba67-167">O namespace `Microsoft.Azure.Graphs.Elements` fornece as classes `Vertex`, `Edge`, `Property` e `VertexProperty` para desserializar respostas GraphSON para objetos do .NET bem definidos.</span><span class="sxs-lookup"><span data-stu-id="3ba67-167">The `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses to well-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="3ba67-168">Executar Gremlin usando CreateGremlinQuery</span><span class="sxs-lookup"><span data-stu-id="3ba67-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="3ba67-169">Gremlin, assim como o SQL, oferece suporte a operações de consulta, gravação e leitura.</span><span class="sxs-lookup"><span data-stu-id="3ba67-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="3ba67-170">Por exemplo, o trecho a seguir mostra como criar vértices, bordas, executar algumas consultas de exemplo usando `CreateGremlinQuery<T>` e iterar assincronamente esses resultados usando `ExecuteNextAsync` e \`HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="3ba67-170">For example, the following snippet shows how to create vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // The CreateGremlinQuery method extensions allow you to execute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a><span data-ttu-id="3ba67-171">Adicionar vértices e bordas</span><span class="sxs-lookup"><span data-stu-id="3ba67-171">Add vertices and edges</span></span>

<span data-ttu-id="3ba67-172">Vamos examinar as instruções Gremlin mostradas na seção anterior em mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="3ba67-172">Let's look at the Gremlin statements shown in the preceding section more detail.</span></span> <span data-ttu-id="3ba67-173">Primeiro, temos alguns vértices usando o método `addV` do Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3ba67-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="3ba67-174">Por exemplo, o trecho a seguir cria um vértice "Thomas Andersen" do tipo "Pessoa", com propriedades de nome, sobrenome e idade.</span><span class="sxs-lookup"><span data-stu-id="3ba67-174">For example, the following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

<span data-ttu-id="3ba67-175">Em seguida, podemos criar algumas arestas entre esses vértices usando o método `addE` do Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3ba67-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

<span data-ttu-id="3ba67-176">Podemos atualizar um vértice existente usando a etapa `properties` no Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3ba67-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="3ba67-177">Podemos ignorar a chamada para executar a consulta por meio de `HasMoreResults` e `ExecuteNextAsync` para o restante dos exemplos.</span><span class="sxs-lookup"><span data-stu-id="3ba67-177">We skip the call to execute the query via `HasMoreResults` and `ExecuteNextAsync` for the rest of the examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="3ba67-178">Você pode remover bordas e vértices usando a etapa `drop` do Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3ba67-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="3ba67-179">Aqui está um trecho que mostra como excluir um vértice e uma borda.</span><span class="sxs-lookup"><span data-stu-id="3ba67-179">Here's a snippet that shows how to delete a vertex and an edge.</span></span> <span data-ttu-id="3ba67-180">Observe que descartar um vértice executa uma exclusão em cascata das bordas associadas.</span><span class="sxs-lookup"><span data-stu-id="3ba67-180">Note that dropping a vertex performs a cascading delete of the associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-the-graph"></a><span data-ttu-id="3ba67-181">Consultar o gráfico</span><span class="sxs-lookup"><span data-stu-id="3ba67-181">Query the graph</span></span>

<span data-ttu-id="3ba67-182">Você também pode executar consultas e passagens usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3ba67-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="3ba67-183">Por exemplo, o trecho a seguir mostra como contar o número de vértices no gráfico:</span><span class="sxs-lookup"><span data-stu-id="3ba67-183">For example, the following snippet shows how to count the number of vertices in the graph:</span></span>

```cs
// Run a query to count vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="3ba67-184">Execute filtros usando as etapas `has` e `hasLabel` do Gremlin e combine-as usando `and`, `or` e `not` para compilar filtros mais complexos:</span><span class="sxs-lookup"><span data-stu-id="3ba67-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="3ba67-185">Você pode projetar certas propriedades nos resultados da consulta usando a etapa `values`:</span><span class="sxs-lookup"><span data-stu-id="3ba67-185">You can project certain properties in the query results using the `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="3ba67-186">Até agora, só vimos operadores de consulta que funcionam em qualquer banco de dados.</span><span class="sxs-lookup"><span data-stu-id="3ba67-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="3ba67-187">Os gráficos são rápidos e eficientes para operações de passagem quando você precisa navegar até os vértices e bordas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="3ba67-187">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="3ba67-188">Vamos encontrar todos os amigos de Thomas.</span><span class="sxs-lookup"><span data-stu-id="3ba67-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="3ba67-189">Fazemos isso usando a etapa `outE` do Gremlin para localizar todos as bordas externas de Thomas, depois passamos para os vértices internos dessas bordas usando a etapa `inV` do Gremlin:</span><span class="sxs-lookup"><span data-stu-id="3ba67-189">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="3ba67-190">A próxima consulta executa dois saltos para localizar todos os "amigos dos amigos" de Thomas, chamando `outE` e `inV` duas vezes.</span><span class="sxs-lookup"><span data-stu-id="3ba67-190">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="3ba67-191">Você pode criar consultas mais complexas e implementar uma lógica avançada de passagem de gráfico usando o Gremlin, incluindo a combinação de expressões de filtro, executando o loop usando a etapa `loop` e implementando a navegação condicional usando a etapa `choose`.</span><span class="sxs-lookup"><span data-stu-id="3ba67-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="3ba67-192">Saiba mais sobre o que você pode fazer com o [Suporte do Gremlin](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="3ba67-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="3ba67-193">Isso é tudo, este tutorial do Azure Cosmos DB está concluído!</span><span class="sxs-lookup"><span data-stu-id="3ba67-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="3ba67-194">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="3ba67-194">Clean up resources</span></span>

<span data-ttu-id="3ba67-195">Se você não continuar usando este aplicativo, siga as seguintes etapas para excluir todos os recursos criados neste tutorial no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba67-195">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>  

1. <span data-ttu-id="3ba67-196">No menu à esquerda no portal do Azure, clique em **Grupos de recursos** e depois clique no nome do recurso criado.</span><span class="sxs-lookup"><span data-stu-id="3ba67-196">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="3ba67-197">Em sua página de grupo de recursos, clique em **Excluir**, digite o nome do recurso para excluir na caixa de texto e depois clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="3ba67-197">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ba67-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3ba67-198">Next Steps</span></span>

<span data-ttu-id="3ba67-199">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3ba67-199">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3ba67-200">Criou uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3ba67-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="3ba67-201">Criou um banco de dados do gráfico e um contêiner</span><span class="sxs-lookup"><span data-stu-id="3ba67-201">Created a graph database and container</span></span>
> * <span data-ttu-id="3ba67-202">Serializou vértices e bordas para os objetos .NET</span><span class="sxs-lookup"><span data-stu-id="3ba67-202">Serialized vertices and edges to .NET objects</span></span>
> * <span data-ttu-id="3ba67-203">Adicionou vértices e bordas</span><span class="sxs-lookup"><span data-stu-id="3ba67-203">Added vertices and edges</span></span>
> * <span data-ttu-id="3ba67-204">Consultou o gráfico usando Gremlin</span><span class="sxs-lookup"><span data-stu-id="3ba67-204">Queried the graph using Gremlin</span></span>

<span data-ttu-id="3ba67-205">Agora, você pode criar consultas mais complexas e implementar uma lógica de passagem de gráfico avançada usando o Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3ba67-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ba67-206">Consultar usando o Gremlin</span><span class="sxs-lookup"><span data-stu-id="3ba67-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
