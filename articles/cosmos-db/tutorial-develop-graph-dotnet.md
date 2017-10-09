---
title: 'Cosmos do Azure DB: Desenvolver com hello API do Graph em .NET | Microsoft Docs'
description: Saiba como toodevelop com a API de documentos do Azure Cosmos DB usando .NET
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
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a><span data-ttu-id="603ec-103">Cosmos do Azure DB: Desenvolver com hello API do Graph em .NET</span><span class="sxs-lookup"><span data-stu-id="603ec-103">Azure Cosmos DB: Develop with hello Graph API in .NET</span></span>
<span data-ttu-id="603ec-104">O Azure Cosmos DB é o serviço de banco de dados multimodelo distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="603ec-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="603ec-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="603ec-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="603ec-106">Este tutorial demonstra como toocreate uma conta de banco de dados do Azure Cosmos usando Olá portal do Azure e toocreate um banco de dados do gráfico e o contêiner.</span><span class="sxs-lookup"><span data-stu-id="603ec-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal and how toocreate a graph database and container.</span></span> <span data-ttu-id="603ec-107">aplicativo Hello cria uma rede social simple com quatro pessoas usando Olá [API do Graph](graph-sdk-dotnet.md) (visualização), então atravessa e consultas gráfico hello usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="603ec-107">hello application then creates a simple social network with four people using hello [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries hello graph using Gremlin.</span></span>

<span data-ttu-id="603ec-108">Este tutorial aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="603ec-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="603ec-109">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="603ec-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="603ec-110">Criar um banco de dados do gráfico e um contêiner</span><span class="sxs-lookup"><span data-stu-id="603ec-110">Create a graph database and container</span></span>
> * <span data-ttu-id="603ec-111">Serializar objetos too.NET de vértices e bordas</span><span class="sxs-lookup"><span data-stu-id="603ec-111">Serialize vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="603ec-112">Adicionar vértices e bordas</span><span class="sxs-lookup"><span data-stu-id="603ec-112">Add vertices and edges</span></span>
> * <span data-ttu-id="603ec-113">Gráfico de saudação de consulta usando Gremlin</span><span class="sxs-lookup"><span data-stu-id="603ec-113">Query hello graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="603ec-114">Gráficos no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="603ec-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="603ec-115">Você pode usar o banco de dados do Azure Cosmos toocreate, atualizar e gráficos de consulta usando Olá [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="603ec-115">You can use Azure Cosmos DB toocreate, update, and query graphs using hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="603ec-116">biblioteca de Microsoft.Azure.Graph Olá fornece um método de extensão único `CreateGremlinQuery<T>` sobre Olá `DocumentClient` consultas de Gremlin tooexecute de classe.</span><span class="sxs-lookup"><span data-stu-id="603ec-116">hello Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of hello `DocumentClient` class tooexecute Gremlin queries.</span></span>

<span data-ttu-id="603ec-117">Gremlin é uma linguagem de programação funcional que oferece suporte a operações de gravação (DML) e operações de consulta e passagem.</span><span class="sxs-lookup"><span data-stu-id="603ec-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="603ec-118">Abordaremos alguns exemplos neste artigo tooget seu iniciada com Gremlin.</span><span class="sxs-lookup"><span data-stu-id="603ec-118">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="603ec-119">Veja [consultas Gremlin](gremlin-support.md) para obter uma explicação detalhada dos recursos Gremlin disponíveis no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="603ec-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="603ec-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="603ec-120">Prerequisites</span></span>
<span data-ttu-id="603ec-121">Verifique se que você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="603ec-121">Please make sure you have hello following:</span></span>

* <span data-ttu-id="603ec-122">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="603ec-122">An active Azure account.</span></span> <span data-ttu-id="603ec-123">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="603ec-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="603ec-124">Como alternativa, você pode usar o hello [emulador do Azure DocumentDB](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="603ec-124">Alternatively, you can use hello [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="603ec-125">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="603ec-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="603ec-126">Criar uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="603ec-126">Create database account</span></span>

<span data-ttu-id="603ec-127">Vamos começar criando uma conta de banco de dados do Azure Cosmos em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="603ec-127">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="603ec-128">Já tem uma conta do Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="603ec-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="603ec-129">Nesse caso, pular muito[configurar sua solução do Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="603ec-129">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="603ec-130">Você tinha uma conta do Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="603ec-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="603ec-131">Se assim, sua conta agora é uma conta de banco de dados do Azure Cosmos e poderá pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="603ec-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="603ec-132">Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="603ec-132">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="603ec-133"><a id="SetupVS"></a>Configurar sua solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="603ec-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="603ec-134">Abra o **Visual Studio** no seu computador.</span><span class="sxs-lookup"><span data-stu-id="603ec-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="603ec-135">Em Olá **arquivo** menu, selecione **novo**e, em seguida, escolha **projeto**.</span><span class="sxs-lookup"><span data-stu-id="603ec-135">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="603ec-136">Em Olá **novo projeto** caixa de diálogo, selecione **modelos** / **Visual C#** / **aplicativo de Console (.NET Framework)**, nomeie o projeto e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="603ec-136">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="603ec-137">Em Olá **Solution Explorer**, clique com o botão direito no seu novo aplicativo de console, que está em sua solução do Visual Studio, e, em seguida, clique em **gerenciar pacotes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="603ec-137">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="603ec-138">Em Olá **NuGet** , clique em **procurar**e o tipo **Microsoft.Azure.Graphs** na caixa de pesquisa hello e seleção Olá **incluem as versões de pré-lançamento**.</span><span class="sxs-lookup"><span data-stu-id="603ec-138">In hello **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in hello search box, and check hello **Include prerelease versions**.</span></span>
6. <span data-ttu-id="603ec-139">Nos resultados de saudação localizar **Microsoft.Azure.Graphs** e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="603ec-139">Within hello results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="603ec-140">Se você receber uma mensagem sobre Analisando alterações toohello solução, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="603ec-140">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="603ec-141">Se receber uma mensagem sobre a aceitação da licença, clique em **Aceito**.</span><span class="sxs-lookup"><span data-stu-id="603ec-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="603ec-142">Olá `Microsoft.Azure.Graphs` biblioteca fornece um método de extensão único `CreateGremlinQuery<T>` para executar as operações de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="603ec-142">hello `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="603ec-143">Gremlin é uma linguagem de programação funcional que oferece suporte a operações de gravação (DML) e operações de consulta e passagem.</span><span class="sxs-lookup"><span data-stu-id="603ec-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="603ec-144">Abordaremos alguns exemplos neste artigo tooget seu iniciada com Gremlin.</span><span class="sxs-lookup"><span data-stu-id="603ec-144">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="603ec-145">[Consultas Gremlin](gremlin-support.md) possui uma explicação detalhada dos recursos Gremlin no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="603ec-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="603ec-146"><a id="add-references"></a>Conecte seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="603ec-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="603ec-147">Adicionar essas duas constantes e sua variável de *cliente* no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="603ec-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="603ec-148">Em seguida, head fazer toohello [portal do Azure](https://portal.azure.com) tooretrieve sua URL de ponto de extremidade e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="603ec-148">Next, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="603ec-149">URL de ponto de extremidade de saudação e a chave primária são necessárias para seu aplicativo toounderstand onde tooconnect e para o banco de dados do Azure Cosmos tootrust conexão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="603ec-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span> 

<span data-ttu-id="603ec-150">Olá portal do Azure, navegue conta de banco de dados do Azure Cosmos tooyour em, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**.</span><span class="sxs-lookup"><span data-stu-id="603ec-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="603ec-151">Copiar Olá URI do portal de saudação e cole-o sobre `Endpoint` na propriedade do ponto de extremidade de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="603ec-151">Copy hello URI from hello portal and paste it over `Endpoint` in hello endpoint property above.</span></span> <span data-ttu-id="603ec-152">Em seguida, copie Olá chave primária do portal hello e cole-a saudação `AuthKey` propriedade acima.</span><span class="sxs-lookup"><span data-stu-id="603ec-152">Then copy hello PRIMARY KEY from hello portal and paste it into hello `AuthKey` property above.</span></span> 

<span data-ttu-id="603ec-153">! [Captura de tela de saudação portal do Azure usado pelo toocreate tutorial Olá um aplicativo c#.</span><span class="sxs-lookup"><span data-stu-id="603ec-153">![Screen shot of hello Azure portal used by hello tutorial toocreate a C# application.</span></span> <span data-ttu-id="603ec-154">Mostra uma saudação de conta do banco de dados do Azure Cosmos botão chaves realçado em hello Azure Cosmos DB navegação e os valores de chave primária e URI Olá realçados em Olá folha de chaves] [chaves]</span><span class="sxs-lookup"><span data-stu-id="603ec-154">Shows an Azure Cosmos DB account hello KEYS button highlighted on hello Azure Cosmos DB navigation , and hello URI and PRIMARY KEY values highlighted on hello Keys blade][keys]</span></span> 
 
## <span data-ttu-id="603ec-155"><a id="instantiate"></a>Criar uma instância de saudação DocumentClient</span><span class="sxs-lookup"><span data-stu-id="603ec-155"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span> 
<span data-ttu-id="603ec-156">Em seguida, crie uma nova instância da saudação **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="603ec-156">Next, create a new instance of hello **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="603ec-157"><a id="create-database"></a>Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="603ec-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="603ec-158">Agora, crie um banco de dados do Azure Cosmos [banco de dados](documentdb-resources.md#databases) usando Olá [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método ou [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método hello  **DocumentClient** classe da saudação [SDK .NET do DocumentDB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="603ec-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="603ec-159">Criar um gráfico</span><span class="sxs-lookup"><span data-stu-id="603ec-159">Create a graph</span></span> 

<span data-ttu-id="603ec-160">Em seguida, crie um contêiner de gráfico usando hello usando Olá [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método ou [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método hello **DocumentClient**  classe.</span><span class="sxs-lookup"><span data-stu-id="603ec-160">Next, create a graph container by using hello using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="603ec-161">Uma coleção é um contêiner de entidades de gráfico.</span><span class="sxs-lookup"><span data-stu-id="603ec-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="603ec-162"><a id="serializing"></a>Serializar objetos too.NET de vértices e bordas</span><span class="sxs-lookup"><span data-stu-id="603ec-162"><a id="serializing"></a>Serialize vertices and edges too.NET objects</span></span>
<span data-ttu-id="603ec-163">Banco de dados do Azure Cosmos usa Olá [formato com fio GraphSON](gremlin-support.md), que define um esquema JSON para vértices, bordas e propriedades.</span><span class="sxs-lookup"><span data-stu-id="603ec-163">Azure Cosmos DB uses hello [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="603ec-164">Hello Azure Cosmos DB .NET SDK inclui JSON.NET como uma dependência, e isso nos permite tooserialize/desserializar GraphSON em objetos .NET que possamos trabalhar com código.</span><span class="sxs-lookup"><span data-stu-id="603ec-164">hello Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us tooserialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="603ec-165">Por exemplo, vamos trabalhar com uma rede social simples com quatro pessoas.</span><span class="sxs-lookup"><span data-stu-id="603ec-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="603ec-166">Vamos examinar como toocreate `Person` vértices, adicionar `Knows` relações entre elas, em seguida, consultar e percorrer as relações de "friend de amigo" hello gráfico toofind.</span><span class="sxs-lookup"><span data-stu-id="603ec-166">We look at how toocreate `Person` vertices, add `Knows` relationships between them, then query and traverse hello graph toofind "friend of friend" relationships.</span></span> 

<span data-ttu-id="603ec-167">Olá `Microsoft.Azure.Graphs.Elements` namespace fornece `Vertex`, `Edge`, `Property` e `VertexProperty` classes para desserializar objetos do GraphSON respostas toowell definidos pelo .NET.</span><span class="sxs-lookup"><span data-stu-id="603ec-167">hello `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses toowell-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="603ec-168">Executar Gremlin usando CreateGremlinQuery</span><span class="sxs-lookup"><span data-stu-id="603ec-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="603ec-169">Gremlin, assim como o SQL, oferece suporte a operações de consulta, gravação e leitura.</span><span class="sxs-lookup"><span data-stu-id="603ec-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="603ec-170">Por exemplo, hello trecho a seguir mostra como toocreate vértices, bordas, executam alguns exemplos de consultas usando `CreateGremlinQuery<T>`e iterar assincronamente esses resultados usando `ExecuteNextAsync` e ' HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="603ec-170">For example, hello following snippet shows how toocreate vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

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

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
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

## <a name="add-vertices-and-edges"></a><span data-ttu-id="603ec-171">Adicionar vértices e bordas</span><span class="sxs-lookup"><span data-stu-id="603ec-171">Add vertices and edges</span></span>

<span data-ttu-id="603ec-172">Vamos dar uma olhada em instruções de Gremlin Olá mostradas na saudação anterior seção mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="603ec-172">Let's look at hello Gremlin statements shown in hello preceding section more detail.</span></span> <span data-ttu-id="603ec-173">Primeiro, temos alguns vértices usando o método `addV` do Gremlin.</span><span class="sxs-lookup"><span data-stu-id="603ec-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="603ec-174">Por exemplo, hello trecho a seguir cria um vértice "Thomas Andersen" do tipo "Pessoa", com propriedades de nome, sobrenome e idade.</span><span class="sxs-lookup"><span data-stu-id="603ec-174">For example, hello following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

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

<span data-ttu-id="603ec-175">Em seguida, podemos criar algumas arestas entre esses vértices usando o método `addE` do Gremlin.</span><span class="sxs-lookup"><span data-stu-id="603ec-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

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

<span data-ttu-id="603ec-176">Podemos atualizar um vértice existente usando a etapa `properties` no Gremlin.</span><span class="sxs-lookup"><span data-stu-id="603ec-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="603ec-177">Podemos ignorar Olá chamada tooexecute Olá consulta `HasMoreResults` e `ExecuteNextAsync` para rest Olá dos exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="603ec-177">We skip hello call tooexecute hello query via `HasMoreResults` and `ExecuteNextAsync` for hello rest of hello examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="603ec-178">Você pode remover bordas e vértices usando a etapa `drop` do Gremlin.</span><span class="sxs-lookup"><span data-stu-id="603ec-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="603ec-179">Aqui está um trecho de código que mostra como toodelete um vértice e uma borda.</span><span class="sxs-lookup"><span data-stu-id="603ec-179">Here's a snippet that shows how toodelete a vertex and an edge.</span></span> <span data-ttu-id="603ec-180">Observe que o descarte de um vértice realiza uma exclusão em cascata de saudação associados bordas.</span><span class="sxs-lookup"><span data-stu-id="603ec-180">Note that dropping a vertex performs a cascading delete of hello associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a><span data-ttu-id="603ec-181">Gráfico de saudação de consulta</span><span class="sxs-lookup"><span data-stu-id="603ec-181">Query hello graph</span></span>

<span data-ttu-id="603ec-182">Você também pode executar consultas e passagens usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="603ec-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="603ec-183">Por exemplo, a saudação trecho de código a seguir mostra como toocount Olá número de vértices no gráfico de saudação:</span><span class="sxs-lookup"><span data-stu-id="603ec-183">For example, hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="603ec-184">Você pode executar filtros usando do Gremlin `has` e `hasLabel` etapas e combiná-los usando `and`, `or`, e `not` toobuild mais complexo filtros:</span><span class="sxs-lookup"><span data-stu-id="603ec-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="603ec-185">Você pode projetar determinadas propriedades em resultados da consulta hello usando Olá `values` etapa:</span><span class="sxs-lookup"><span data-stu-id="603ec-185">You can project certain properties in hello query results using hello `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="603ec-186">Até agora, só vimos operadores de consulta que funcionam em qualquer banco de dados.</span><span class="sxs-lookup"><span data-stu-id="603ec-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="603ec-187">Gráficos são rápidos e eficientes para operações de passagem quando você precisa toonavigate toorelated bordas e vértices.</span><span class="sxs-lookup"><span data-stu-id="603ec-187">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="603ec-188">Vamos encontrar todos os amigos de Thomas.</span><span class="sxs-lookup"><span data-stu-id="603ec-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="603ec-189">Podemos fazer isso por meio do Gremlin `outE` etapa toofind Olá todas as out-bordas de Thomas, em seguida, passar toohello nos vértices das bordas usando do Gremlin `inV` etapa:</span><span class="sxs-lookup"><span data-stu-id="603ec-189">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="603ec-190">executa a consulta seguinte Olá toofind de dois saltos todos "amigos Thomas intitulado dos amigos", chamando `outE` e `inV` duas vezes.</span><span class="sxs-lookup"><span data-stu-id="603ec-190">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="603ec-191">Você pode criar consultas mais complexas e implementar a lógica de passagem de gráfico avançado usando Gremlin, incluindo filtro combinação expressões, executar um loop usando Olá `loop` etapa e implementação navegação condicional usando Olá `choose` etapa.</span><span class="sxs-lookup"><span data-stu-id="603ec-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="603ec-192">Saiba mais sobre o que você pode fazer com o [Suporte do Gremlin](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="603ec-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="603ec-193">Isso é tudo, este tutorial do Azure Cosmos DB está concluído!</span><span class="sxs-lookup"><span data-stu-id="603ec-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="603ec-194">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="603ec-194">Clean up resources</span></span>

<span data-ttu-id="603ec-195">Se você não vai toocontinue toouse esse aplicativo, use Olá seguindo as etapas toodelete todos os recursos criados por esse tutorial Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="603ec-195">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>  

1. <span data-ttu-id="603ec-196">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="603ec-196">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="603ec-197">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="603ec-197">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="603ec-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="603ec-198">Next Steps</span></span>

<span data-ttu-id="603ec-199">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="603ec-199">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="603ec-200">Criou uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="603ec-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="603ec-201">Criou um banco de dados do gráfico e um contêiner</span><span class="sxs-lookup"><span data-stu-id="603ec-201">Created a graph database and container</span></span>
> * <span data-ttu-id="603ec-202">Objetos serializados de too.NET de vértices e bordas</span><span class="sxs-lookup"><span data-stu-id="603ec-202">Serialized vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="603ec-203">Adicionou vértices e bordas</span><span class="sxs-lookup"><span data-stu-id="603ec-203">Added vertices and edges</span></span>
> * <span data-ttu-id="603ec-204">Gráfico de saudação consultados usando Gremlin</span><span class="sxs-lookup"><span data-stu-id="603ec-204">Queried hello graph using Gremlin</span></span>

<span data-ttu-id="603ec-205">Agora, você pode criar consultas mais complexas e implementar uma lógica de passagem de gráfico avançada usando o Gremlin.</span><span class="sxs-lookup"><span data-stu-id="603ec-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="603ec-206">Consultar usando o Gremlin</span><span class="sxs-lookup"><span data-stu-id="603ec-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
