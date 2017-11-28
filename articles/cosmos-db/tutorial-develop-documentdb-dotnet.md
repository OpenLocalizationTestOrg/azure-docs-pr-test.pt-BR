---
title: 'Cosmos do Azure DB: Desenvolver com hello API DocumentDB no .NET | Microsoft Docs'
description: Saiba como toodevelop com a API de documentos do Azure Cosmos DB usando .NET
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
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a><span data-ttu-id="a54cb-103">Azure CosmosDB: Desenvolver com hello API DocumentDB no .NET</span><span class="sxs-lookup"><span data-stu-id="a54cb-103">Azure CosmosDB: Develop with hello DocumentDB API in .NET</span></span>

<span data-ttu-id="a54cb-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a54cb-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="a54cb-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="a54cb-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="a54cb-106">Este tutorial demonstra como toocreate uma conta de banco de dados do Azure Cosmos usando Olá portal do Azure e, em seguida, criar um banco de dados de documento e uma coleção com uma [chave de partição](documentdb-partition-data.md#partition-keys) usando Olá [API .NET do DocumentDB](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a54cb-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using hello [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="a54cb-107">Ao definir uma chave de partição quando você cria uma coleção, seu aplicativo preparado tooscale facilmente conforme o aumento dos dados.</span><span class="sxs-lookup"><span data-stu-id="a54cb-107">By defining a partition key when you create a collection, your application is prepared tooscale effortlessly as your data grows.</span></span> 

<span data-ttu-id="a54cb-108">Seguir Olá tutorial abrange tarefas usando Olá [API .NET do DocumentDB](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="a54cb-108">This tutorial covers hello following tasks by using hello [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a54cb-109">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a54cb-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="a54cb-110">Criar um banco de dados e uma coleção com uma chave de partição</span><span class="sxs-lookup"><span data-stu-id="a54cb-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="a54cb-111">Criar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="a54cb-111">Create JSON documents</span></span>
> * <span data-ttu-id="a54cb-112">Atualizar um documento</span><span class="sxs-lookup"><span data-stu-id="a54cb-112">Update a document</span></span>
> * <span data-ttu-id="a54cb-113">Consultar coleções particionadas</span><span class="sxs-lookup"><span data-stu-id="a54cb-113">Query partitioned collections</span></span>
> * <span data-ttu-id="a54cb-114">Executar procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="a54cb-114">Run stored procedures</span></span>
> * <span data-ttu-id="a54cb-115">Excluir um documento</span><span class="sxs-lookup"><span data-stu-id="a54cb-115">Delete a document</span></span>
> * <span data-ttu-id="a54cb-116">Excluir um banco de dados</span><span class="sxs-lookup"><span data-stu-id="a54cb-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a54cb-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a54cb-117">Prerequisites</span></span>
<span data-ttu-id="a54cb-118">Verifique se que você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="a54cb-118">Please make sure you have hello following:</span></span>

* <span data-ttu-id="a54cb-119">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a54cb-119">An active Azure account.</span></span> <span data-ttu-id="a54cb-120">Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a54cb-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="a54cb-121">Como alternativa, você pode usar o hello [emulador de banco de dados do Azure Cosmos](local-emulator.md) para este tutorial se você gostaria que toouse um ambiente local que emula os serviços do Azure DocumentDB Olá para fins de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="a54cb-121">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like toouse a local environment that emulates hello Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="a54cb-122">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="a54cb-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="a54cb-123">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a54cb-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="a54cb-124">Vamos começar criando uma conta de banco de dados do Azure Cosmos em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a54cb-124">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="a54cb-125">Já tem uma conta do Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="a54cb-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="a54cb-126">Nesse caso, pular muito[configurar sua solução do Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="a54cb-126">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="a54cb-127">Você tinha uma conta do Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="a54cb-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="a54cb-128">Se assim, sua conta agora é uma conta de banco de dados do Azure Cosmos e poderá pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="a54cb-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="a54cb-129">Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="a54cb-129">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="a54cb-130"><a id="SetupVS"></a>Configurar sua solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a54cb-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="a54cb-131">Abra o **Visual Studio** no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a54cb-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="a54cb-132">Em Olá **arquivo** menu, selecione **novo**e, em seguida, escolha **projeto**.</span><span class="sxs-lookup"><span data-stu-id="a54cb-132">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="a54cb-133">Em Olá **novo projeto** caixa de diálogo, selecione **modelos** / **Visual C#** / **aplicativo de Console (.NET Framework)**, nomeie o projeto e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="a54cb-133">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="a54cb-134">![Captura de tela da janela do novo projeto de saudação](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="a54cb-134">![Screen shot of hello New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="a54cb-135">Em Olá **Solution Explorer**, clique com o botão direito no seu novo aplicativo de console, que está em sua solução do Visual Studio, e, em seguida, clique em **gerenciar pacotes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="a54cb-135">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Captura de tela de saudação à direita Menu clicado para Olá projeto](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="a54cb-137">Em Olá **NuGet** , clique em **procurar**e o tipo **documentdb** na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="a54cb-137">In hello **NuGet** tab, click **Browse**, and type **documentdb** in hello search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="a54cb-138">Nos resultados de saudação localizar **Microsoft.Azure.DocumentDB** e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="a54cb-138">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="a54cb-139">ID do pacote Olá Olá biblioteca de cliente de banco de dados do Azure Cosmos é [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="a54cb-139">hello package ID for hello Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="a54cb-140">![Captura de tela de saudação Menu do NuGet para localizar o SDK de cliente de banco de dados do Azure Cosmos](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="a54cb-140">![Screen shot of hello NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="a54cb-141">Se você receber uma mensagem sobre Analisando alterações toohello solução, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="a54cb-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="a54cb-142">Se receber uma mensagem sobre a aceitação da licença, clique em **Aceito**.</span><span class="sxs-lookup"><span data-stu-id="a54cb-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="a54cb-143"><a id="Connect"></a>Adicionar referências tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="a54cb-143"><a id="Connect"></a>Add references tooyour project</span></span>
<span data-ttu-id="a54cb-144">Olá restantes etapas para este tutorial forneça Olá API DocumentDB código trechos de código toocreate e atualização Azure Cosmos DB recursos necessários em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="a54cb-144">hello remaining steps in this tutorial provide hello DocumentDB API code snippets required toocreate and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="a54cb-145">Primeiro, adicione o aplicativo de tooyour essas referências.</span><span class="sxs-lookup"><span data-stu-id="a54cb-145">First, add these references tooyour application.</span></span>
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="a54cb-146"><a id="add-references"></a>Conecte seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="a54cb-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="a54cb-147">Em seguida, adicione essas duas constantes e sua variável de *cliente* no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a54cb-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="a54cb-148">Em seguida, head fazer toohello [portal do Azure](https://portal.azure.com) tooretrieve sua URL de ponto de extremidade e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="a54cb-148">Then, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="a54cb-149">URL de ponto de extremidade de saudação e a chave primária são necessárias para seu aplicativo toounderstand onde tooconnect e para o banco de dados do Azure Cosmos tootrust conexão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a54cb-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="a54cb-150">Olá portal do Azure, navegue conta de banco de dados do Azure Cosmos tooyour em, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**.</span><span class="sxs-lookup"><span data-stu-id="a54cb-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="a54cb-151">Copiar Olá URI do portal de saudação e cole-o sobre `<your endpoint URL>` no arquivo program.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="a54cb-151">Copy hello URI from hello portal and paste it over `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="a54cb-152">Cópia Olá chave primária do portal hello e cole-o sobre `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="a54cb-152">Then copy hello PRIMARY KEY from hello portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="a54cb-153">Ser Olá-se de tooremove `<` e `>` de seus valores.</span><span class="sxs-lookup"><span data-stu-id="a54cb-153">Be sure tooremove hello `<` and `>` from your values.</span></span>

![Captura de tela de saudação portal do Azure usado pelo Olá NoSQL tutorial toocreate um aplicativo de console c#.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="a54cb-156"><a id="instantiate"></a>Criar uma instância de saudação DocumentClient</span><span class="sxs-lookup"><span data-stu-id="a54cb-156"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span>

<span data-ttu-id="a54cb-157">Agora, crie uma nova instância da saudação **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="a54cb-157">Now, create a new instance of hello **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="a54cb-158"><a id="create-database"></a>Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="a54cb-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="a54cb-159">Em seguida, crie um banco de dados do Azure Cosmos [banco de dados](documentdb-resources.md#databases) usando Olá [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método ou [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método hello ** DocumentClient** classe da saudação [SDK .NET do DocumentDB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a54cb-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="a54cb-160">Um banco de dados é um contêiner lógico de saudação do armazenamento de documentos JSON particionado em coleções.</span><span class="sxs-lookup"><span data-stu-id="a54cb-160">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="a54cb-161">Escolha uma chave de partição</span><span class="sxs-lookup"><span data-stu-id="a54cb-161">Decide on a partition key</span></span> 

<span data-ttu-id="a54cb-162">Coleções são contêineres para armazenamento de documentos.</span><span class="sxs-lookup"><span data-stu-id="a54cb-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="a54cb-163">Elas são recursos lógicos e podem [abranger uma ou mais partições físicas](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="a54cb-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="a54cb-164">Um [chave de partição](documentdb-partition-data.md) é uma propriedade (ou caminho) em documentos que é usado toodistribute seus dados entre os servidores de saudação ou partições.</span><span class="sxs-lookup"><span data-stu-id="a54cb-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used toodistribute your data among hello servers or partitions.</span></span> <span data-ttu-id="a54cb-165">Todos os documentos com hello a mesma chave de partição são armazenados em Olá mesma partição.</span><span class="sxs-lookup"><span data-stu-id="a54cb-165">All documents with hello same partition key are stored in hello same partition.</span></span> 

<span data-ttu-id="a54cb-166">Determinação de uma chave de partição é uma decisão importante toomake antes de criar uma coleção.</span><span class="sxs-lookup"><span data-stu-id="a54cb-166">Determining a partition key is an important decision toomake before you create a collection.</span></span> <span data-ttu-id="a54cb-167">Chaves de partição são uma propriedade (ou caminho) em documentos que podem ser usado pelo banco de dados do Azure Cosmos toodistribute seus dados entre vários servidores ou partições.</span><span class="sxs-lookup"><span data-stu-id="a54cb-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB toodistribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="a54cb-168">Cosmos DB hashes de valor de chave de partição hello e usa partição de Olá Olá hash resultados toodetermine na qual documento de saudação toostore.</span><span class="sxs-lookup"><span data-stu-id="a54cb-168">Cosmos DB hashes hello partition key value and uses hello hashed result toodetermine hello partition in which toostore hello document.</span></span> <span data-ttu-id="a54cb-169">Olá a todos os documentos com hello a mesma chave de partição são armazenados na mesma partição e chaves de partição não podem ser alteradas depois que uma coleção é criada.</span><span class="sxs-lookup"><span data-stu-id="a54cb-169">All documents with hello same partition key are stored in hello same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="a54cb-170">Para este tutorial, vamos chave de partição Olá tooset muito`/deviceId` assim que Olá todos os dados de saudação para um único dispositivo é armazenado em uma única partição.</span><span class="sxs-lookup"><span data-stu-id="a54cb-170">For this tutorial, we're going tooset hello partition key too`/deviceId` so that hello all hello data for a single device is stored in a single partition.</span></span> <span data-ttu-id="a54cb-171">Você deseja toochoose uma chave de partição que tem um grande número de valores, cada um dos quais são usados no sobre Olá mesma frequência tooensure Cosmos DB pode balancear a carga que seus dados crescem e alcançar a taxa de transferência total de coleção Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="a54cb-171">You want toochoose a partition key that has a large number of values, each of which are used at about hello same frequency tooensure Cosmos DB can load balance as your data grows and achieve hello full throughput of hello collection.</span></span> 

<span data-ttu-id="a54cb-172">Para obter mais informações sobre particionamento, consulte [como toopartition e escala no banco de dados do Azure Cosmos?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="a54cb-172">For more information about partitioning, see [How toopartition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="a54cb-173"><a id="CreateColl"></a>Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="a54cb-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="a54cb-174">Agora que sabemos que nossa chave da partição, `/deviceId`, permite criar um [coleção](documentdb-resources.md#collections) usando Olá [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método ou [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="a54cb-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="a54cb-175">Uma coleção é um contêiner de documentos JSON e qualquer lógica de aplicativo JavaScript associada.</span><span class="sxs-lookup"><span data-stu-id="a54cb-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="a54cb-176">Criando uma coleção tem preços implicações, como reservar a taxa de transferência para Olá toocommunicate de aplicativo com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a54cb-176">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="a54cb-177">Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="a54cb-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
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

<span data-ttu-id="a54cb-178">Esse método torna a uma API REST chame tooAzure Cosmos DB e Olá provisões de serviço um número de partições com base na taxa de transferência solicitada hello.</span><span class="sxs-lookup"><span data-stu-id="a54cb-178">This method makes a REST API call tooAzure Cosmos DB, and hello service provisions a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="a54cb-179">Você pode alterar a taxa de transferência de saudação de uma coleção como o desempenho precisa evoluir usando Olá SDK ou hello [portal do Azure](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="a54cb-179">You can change hello throughput of a collection as your performance needs evolve using hello SDK or hello [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="a54cb-180"><a id="CreateDoc"></a>Criar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="a54cb-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="a54cb-181">Vamos inserir alguns documentos JSON no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a54cb-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="a54cb-182">Um [documento](documentdb-resources.md#documents) podem ser criados usando Olá [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="a54cb-182">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="a54cb-183">Os documentos são conteúdo JSON (arbitrário) definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="a54cb-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="a54cb-184">Essa classe de exemplo contém uma leitura do dispositivo e tooinsert de tooCreateDocumentAsync uma chamada de um novo dispositivo de leitura em uma coleção.</span><span class="sxs-lookup"><span data-stu-id="a54cb-184">This sample class contains a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a collection.</span></span>

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

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
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
## <a name="read-data"></a><span data-ttu-id="a54cb-185">Ler dados</span><span class="sxs-lookup"><span data-stu-id="a54cb-185">Read data</span></span>

<span data-ttu-id="a54cb-186">Vamos ler o documento de saudação por sua chave de partição e Id usando o método de ReadDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="a54cb-186">Let's read hello document by its partition key and Id using hello ReadDocumentAsync method.</span></span> <span data-ttu-id="a54cb-187">Observe que as leituras de saudação incluem um valor de PartitionKey (correspondente toohello `x-ms-documentdb-partitionkey` cabeçalho de solicitação na Olá API REST).</span><span class="sxs-lookup"><span data-stu-id="a54cb-187">Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="a54cb-188">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="a54cb-188">Update data</span></span>

<span data-ttu-id="a54cb-189">Agora vamos atualizar alguns dados usando o método de ReplaceDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="a54cb-189">Now let's update some data using hello ReplaceDocumentAsync method.</span></span>

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="a54cb-190">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="a54cb-190">Delete data</span></span>

<span data-ttu-id="a54cb-191">Agora permite excluir um documento com chave de partição e id usando o método de DeleteDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="a54cb-191">Now lets delete a document by partition key and id by using hello DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="a54cb-192">Consultar coleções particionadas</span><span class="sxs-lookup"><span data-stu-id="a54cb-192">Query partitioned collections</span></span>

<span data-ttu-id="a54cb-193">Quando você consulta dados em coleções particionadas, o banco de dados do Azure Cosmos automaticamente rotas Olá partições toohello de consulta correspondente valores de chave de partição do toohello especificados no filtro de saudação (se houver).</span><span class="sxs-lookup"><span data-stu-id="a54cb-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="a54cb-194">Por exemplo, esta consulta é roteado toojust Olá partição contendo Olá chave de partição "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="a54cb-194">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="a54cb-195">Olá consulta a seguir não tem um filtro na chave de partição da saudação (DeviceId) e é leque exibindo tooall partições onde ela é executada no índice da partição Olá.</span><span class="sxs-lookup"><span data-stu-id="a54cb-195">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="a54cb-196">Observe que você tem Olá toospecify EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` em Olá API REST) toohave Olá SDK tooexecute uma consulta em partições.</span><span class="sxs-lookup"><span data-stu-id="a54cb-196">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="a54cb-197">Execução de consulta paralela</span><span class="sxs-lookup"><span data-stu-id="a54cb-197">Parallel query execution</span></span>
<span data-ttu-id="a54cb-198">Olá SDKs do DocumentDB do Azure Cosmos DB 1.9.0 e acima do opções de execução de consulta paralela, que permitem que você tooperform baixa latência as consultas em coleções particionadas, mesmo quando eles precisarem de tootouch um grande número de partições.</span><span class="sxs-lookup"><span data-stu-id="a54cb-198">hello Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="a54cb-199">Por exemplo, Olá consulta a seguir é toorun configurado em paralelo entre partições.</span><span class="sxs-lookup"><span data-stu-id="a54cb-199">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="a54cb-200">Você pode gerenciar a execução de consulta paralela ajustando Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="a54cb-200">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="a54cb-201">Definindo `MaxDegreeOfParallelism`, você pode controlar o grau de paralelismo, ou seja, Olá de número máximo de partições da coleção de rede simultâneas conexões toohello Olá.</span><span class="sxs-lookup"><span data-stu-id="a54cb-201">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello collection's partitions.</span></span> <span data-ttu-id="a54cb-202">Se você definir muito-1, o grau de paralelismo Olá é gerenciado pelo Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="a54cb-202">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="a54cb-203">Se hello `MaxDegreeOfParallelism` não for especificado ou definido too0, que é o valor padrão de saudação, haverá partições de uma única rede conexão toohello coleção.</span><span class="sxs-lookup"><span data-stu-id="a54cb-203">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello collection's partitions.</span></span>
* <span data-ttu-id="a54cb-204">Definindo `MaxBufferedItemCount`, você pode compensar a latência da consulta e a utilização da memória no lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="a54cb-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="a54cb-205">Se você omite esse parâmetro ou defina muito-1, número de saudação de itens em buffer durante a execução de consulta paralela é gerenciado pelo Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="a54cb-205">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="a54cb-206">Considerando Olá mesmo estado da coleção hello, uma consulta paralela retornará resultados Olá mesma ordem como em execução em série.</span><span class="sxs-lookup"><span data-stu-id="a54cb-206">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="a54cb-207">Ao executar uma consulta entre partições que inclui a classificação (ORDER BY e/ou superior), Olá SDK do DocumentDB emite a consulta de saudação em paralelo em partições e mescla resultados parcialmente classificados no hello cliente lado tooproduce resultados ordenados globalmente.</span><span class="sxs-lookup"><span data-stu-id="a54cb-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello DocumentDB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="a54cb-208">Executar procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="a54cb-208">Execute stored procedures</span></span>
<span data-ttu-id="a54cb-209">Por fim, você pode executar transações atômicas em relação a documentos com hello a mesma ID de dispositivo, por exemplo, se você estiver mantendo agregações ou Olá estado mais recente de um dispositivo em um único documento adicionando Olá projeto tooyour de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="a54cb-209">Lastly, you can execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single document by adding hello following code tooyour project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="a54cb-210">E isso é tudo!</span><span class="sxs-lookup"><span data-stu-id="a54cb-210">And that's it!</span></span> <span data-ttu-id="a54cb-211">Esses são os principais componentes de saudação de um aplicativo de banco de dados do Azure Cosmos que usa uma distribuição de dados de escala de tooefficiently chave de partição em partições.</span><span class="sxs-lookup"><span data-stu-id="a54cb-211">those are hello main components of an Azure Cosmos DB application that uses a partition key tooefficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="a54cb-212">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="a54cb-212">Clean up resources</span></span>

<span data-ttu-id="a54cb-213">Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este tutorial Olá portal do Azure com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a54cb-213">If you're not going toocontinue toouse this app, delete all resources created by this tutorial in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="a54cb-214">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e, em seguida, clique em nome exclusivo de saudação do recurso Olá criado.</span><span class="sxs-lookup"><span data-stu-id="a54cb-214">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello unique name of hello resource you created.</span></span> 
2. <span data-ttu-id="a54cb-215">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="a54cb-215">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a54cb-216">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a54cb-216">Next steps</span></span>

<span data-ttu-id="a54cb-217">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="a54cb-217">In this tutorial, you've done hello following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="a54cb-218">Criou uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a54cb-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="a54cb-219">Criou um banco de dados e uma coleção com uma chave de partição</span><span class="sxs-lookup"><span data-stu-id="a54cb-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="a54cb-220">Criou documentos JSON</span><span class="sxs-lookup"><span data-stu-id="a54cb-220">Created JSON documents</span></span>
> * <span data-ttu-id="a54cb-221">Atualizou um documento</span><span class="sxs-lookup"><span data-stu-id="a54cb-221">Updated a document</span></span>
> * <span data-ttu-id="a54cb-222">Consultou coleções particionadas</span><span class="sxs-lookup"><span data-stu-id="a54cb-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="a54cb-223">Executou um procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="a54cb-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="a54cb-224">Excluiu um documento</span><span class="sxs-lookup"><span data-stu-id="a54cb-224">Deleted a document</span></span>
> * <span data-ttu-id="a54cb-225">Excluiu um banco de dados</span><span class="sxs-lookup"><span data-stu-id="a54cb-225">Deleted a database</span></span>

<span data-ttu-id="a54cb-226">Você pode continuar toohello tutorial de Avançar e importar a conta de banco de dados do Cosmos tooyour dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="a54cb-226">You can now proceed toohello next tutorial and import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="a54cb-227">Importar dados no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a54cb-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
