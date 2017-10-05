---
title: Como usar o Azure Search de um aplicativo .NET | Microsoft Docs
description: Como usar a Pesquisa do Azure de um aplicativo .NET
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 552a7ab193e12d2e72da494166d774e974c85d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-search-from-a-net-application"></a><span data-ttu-id="7379e-103">Como usar a Pesquisa do Azure de um aplicativo .NET</span><span class="sxs-lookup"><span data-stu-id="7379e-103">How to use Azure Search from a .NET Application</span></span>
<span data-ttu-id="7379e-104">Este artigo é um passo a passo para ajudar você a usar o [SDK do .NET da Pesquisa do Azure](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="7379e-104">This article is a walkthrough to get you up and running with the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="7379e-105">Você pode usar o SDK do .NET para implementar uma experiência de pesquisa avançada em seu aplicativo usando a Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="7379e-105">You can use the .NET SDK to implement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-the-azure-search-sdk"></a><span data-ttu-id="7379e-106">Novidades no SDK da Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="7379e-106">What's in the Azure Search SDK</span></span>
<span data-ttu-id="7379e-107">O SDK é composto por um uma biblioteca de cliente, `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="7379e-107">The SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="7379e-108">Ele permite que você gerencie seus índices, fontes de dados e indexadores, carregue e gerencie documentos e execute consultas, sem a necessidade de lidar com os detalhes de HTTP e JSON.</span><span class="sxs-lookup"><span data-stu-id="7379e-108">It enables you to manage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having to deal with the details of HTTP and JSON.</span></span>

<span data-ttu-id="7379e-109">A biblioteca de cliente define classes como `Index`, `Field` e `Document`, e operações como `Indexes.Create` e `Documents.Search` nas classes `SearchServiceClient` e `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="7379e-109">The client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on the `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="7379e-110">Essas classes são organizadas nos namespaces a seguir:</span><span class="sxs-lookup"><span data-stu-id="7379e-110">These classes are organized into the following namespaces:</span></span>

* [<span data-ttu-id="7379e-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="7379e-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="7379e-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="7379e-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="7379e-113">A versão atual do SDK .Net da Pesquisa do Azure está disponível para o público geral.</span><span class="sxs-lookup"><span data-stu-id="7379e-113">The current version of the Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="7379e-114">Se você quer fornecer comentários para que possamos incorporar na próxima versão, visite nossa [página de comentários](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="7379e-114">If you would like to provide feedback for us to incorporate in the next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="7379e-115">O SDK do .NET dá suporte à versão `2016-09-01` da [API REST da Azure Search](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="7379e-115">The .NET SDK supports version `2016-09-01` of the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="7379e-116">Agora, essa versão inclui suporte para analisadores personalizados e suporte para indexador de Tabela do Azure e Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="7379e-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="7379e-117">Os recursos de visualização que *não* fazem parte dessa versão, como o suporte para indexação de arquivos JSON e CSV, estão em [visualização](search-api-2015-02-28-preview.md) e disponíveis por meio da antiga [versão 2.0 preview do SDK do .NET](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="7379e-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via the older [2.0-preview version of the .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="7379e-118">Esse SDK não oferece suporte a [Operações de Gerenciamento](https://docs.microsoft.com/rest/api/searchmanagement/), como criar e dimensionar os serviços de Pesquisa e gerenciar chaves de API.</span><span class="sxs-lookup"><span data-stu-id="7379e-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="7379e-119">Se você precisar gerenciar seus recursos de Pesquisa a partir de um aplicativo .NET, é possível usar o [SDK de Gerenciamento do .NET da Azure Search](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="7379e-119">If you need to manage your Search resources from a .NET application, you can use the [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-to-the-latest-version-of-the-sdk"></a><span data-ttu-id="7379e-120">Atualizando para a última versão do SDK</span><span class="sxs-lookup"><span data-stu-id="7379e-120">Upgrading to the latest version of the SDK</span></span>
<span data-ttu-id="7379e-121">Se você já estiver usando uma versão mais antiga do SDK do .NET da Pesquisa do Azure e quiser atualizar para a versão disponível para o público geral, [este artigo](search-dotnet-sdk-migration.md) explicará como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="7379e-121">If you're already using an older version of the Azure Search .NET SDK and you'd like to upgrade to the new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-the-sdk"></a><span data-ttu-id="7379e-122">Requisitos para o SDK</span><span class="sxs-lookup"><span data-stu-id="7379e-122">Requirements for the SDK</span></span>
1. <span data-ttu-id="7379e-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7379e-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="7379e-124">Seu próprio serviço de Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="7379e-124">Your own Azure Search service.</span></span> <span data-ttu-id="7379e-125">Para usar o SDK, você precisará do nome do serviço e de uma ou mais chaves de API.</span><span class="sxs-lookup"><span data-stu-id="7379e-125">In order to use the SDK, you will need the name of your service and one or more API keys.</span></span> <span data-ttu-id="7379e-126">[Criar um serviço no portal](search-create-service-portal.md) ajudará você com estas etapas.</span><span class="sxs-lookup"><span data-stu-id="7379e-126">[Create a service in the portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="7379e-127">Baixe o [pacote NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) do SDK do .NET da Pesquisa do Azure usando "Gerenciar pacotes NuGet" no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7379e-127">Download the Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="7379e-128">Basta procurar o nome do pacote `Microsoft.Azure.Search` em NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="7379e-128">Just search for the package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="7379e-129">O SDK do .NET do Azure Search oferece suporte a aplicativos voltados para o .NET Framework 4.6 e o .NET Core.</span><span class="sxs-lookup"><span data-stu-id="7379e-129">The Azure Search .NET SDK supports applications targeting the .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="7379e-130">Principais cenários</span><span class="sxs-lookup"><span data-stu-id="7379e-130">Core scenarios</span></span>
<span data-ttu-id="7379e-131">Há várias coisas que você precisará fazer em seu aplicativo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="7379e-131">There are several things you'll need to do in your search application.</span></span> <span data-ttu-id="7379e-132">Neste tutorial, abordaremos os principais cenários:</span><span class="sxs-lookup"><span data-stu-id="7379e-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="7379e-133">Criando um índice</span><span class="sxs-lookup"><span data-stu-id="7379e-133">Creating an index</span></span>
* <span data-ttu-id="7379e-134">Preenchimento do índice com documentos</span><span class="sxs-lookup"><span data-stu-id="7379e-134">Populating the index with documents</span></span>
* <span data-ttu-id="7379e-135">Procura por documentos usando filtros e pesquisa de texto completo</span><span class="sxs-lookup"><span data-stu-id="7379e-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="7379e-136">O código de exemplo a seguir ilustra cada um deles.</span><span class="sxs-lookup"><span data-stu-id="7379e-136">The sample code that follows illustrates each of these.</span></span> <span data-ttu-id="7379e-137">Fique à vontade para usar os trechos de código em seu próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7379e-137">Feel free to use the code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="7379e-138">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7379e-138">Overview</span></span>
<span data-ttu-id="7379e-139">O exemplo de aplicativo que vamos explorar cria um novo índice chamado "hotéis", preenche-o com alguns documentos e, em seguida, executa algumas consultas de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="7379e-139">The sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="7379e-140">Este é o programa principal, mostrando o fluxo geral:</span><span class="sxs-lookup"><span data-stu-id="7379e-140">Here is the main program, showing the overall flow:</span></span>

```csharp
// This sample shows how to delete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="7379e-141">Você pode encontrar o código-fonte completo do aplicativo de exemplo usado neste passo a passo no [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="7379e-141">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="7379e-142">Vamos examinar isso passo a passo.</span><span class="sxs-lookup"><span data-stu-id="7379e-142">We'll walk through this step by step.</span></span> <span data-ttu-id="7379e-143">Primeiro, é necessário criar um novo `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="7379e-143">First we need to create a new `SearchServiceClient`.</span></span> <span data-ttu-id="7379e-144">Esse objeto permite o gerenciamento de índices.</span><span class="sxs-lookup"><span data-stu-id="7379e-144">This object allows you to manage indexes.</span></span> <span data-ttu-id="7379e-145">Para construir um, você precisa fornecer o nome do serviço da Pesquisa do Azure, bem como uma chave de API de administração.</span><span class="sxs-lookup"><span data-stu-id="7379e-145">In order to construct one, you need to provide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="7379e-146">Você pode inserir essas informações no arquivo `appsettings.json` do [aplicativo de exemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="7379e-146">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> <span data-ttu-id="7379e-147">Se você fornecer uma chave incorreta (por exemplo, uma chave de consulta quando era necessário fornecer uma chave de administrador), o `SearchServiceClient` lançará uma `CloudException` com a mensagem de erro "Forbidden" na primeira vez que você chamar um método de operação, como `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="7379e-147">If you provide an incorrect key (for example, a query key where an admin key was required), the `SearchServiceClient` will throw a `CloudException` with the error message "Forbidden" the first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="7379e-148">Se isso ocorrer, verifique novamente a chave da API.</span><span class="sxs-lookup"><span data-stu-id="7379e-148">If this happens to you, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="7379e-149">As próximas linhas chamam métodos para criação de um índice chamado "hotéis," excluindo-o primeiro caso ele já exista.</span><span class="sxs-lookup"><span data-stu-id="7379e-149">The next few lines call methods to create an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="7379e-150">Abordaremos esses métodos um pouco mais tarde.</span><span class="sxs-lookup"><span data-stu-id="7379e-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="7379e-151">Em seguida, o índice precisa ser preenchido.</span><span class="sxs-lookup"><span data-stu-id="7379e-151">Next, the index needs to be populated.</span></span> <span data-ttu-id="7379e-152">Para fazer isso, precisaremos de um `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="7379e-152">To do this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="7379e-153">Há duas maneiras de obter um: construindo ou chamando `Indexes.GetClient` no `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="7379e-153">There are two ways to obtain one: by constructing it, or by calling `Indexes.GetClient` on the `SearchServiceClient`.</span></span> <span data-ttu-id="7379e-154">Usaremos o último por conveniência.</span><span class="sxs-lookup"><span data-stu-id="7379e-154">We use the latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="7379e-155">Em um aplicativo típico de pesquisa, o gerenciamento e o preenchimento do índice é tratado por um componente separado das consultas de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="7379e-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="7379e-156">`Indexes.GetClient` é conveniente para preencher um índice porque poupa o trabalho de fornecer outras `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="7379e-156">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="7379e-157">Ele faz isso passando a chave de administrador que você usou para criar o `SearchServiceClient` ao novo `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="7379e-157">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="7379e-158">No entanto, na parte do aplicativo que executa consultas, é melhor criar o `SearchIndexClient` diretamente para que você possa passar uma chave de consulta em vez de uma chave de administrador.</span><span class="sxs-lookup"><span data-stu-id="7379e-158">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="7379e-159">Isso está de acordo com o princípio de privilégios mínimos e ajuda a tornar seu aplicativo mais seguro.</span><span class="sxs-lookup"><span data-stu-id="7379e-159">This is consistent with the principle of least privilege and will help to make your application more secure.</span></span> <span data-ttu-id="7379e-160">Você pode saber mais sobre chaves de administração e chaves de consulta [aqui](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="7379e-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="7379e-161">Agora que temos um `SearchIndexClient`, podemos preencher o índice.</span><span class="sxs-lookup"><span data-stu-id="7379e-161">Now that we have a `SearchIndexClient`, we can populate the index.</span></span> <span data-ttu-id="7379e-162">Isso é feito por outro método que descreveremos mais tarde detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="7379e-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="7379e-163">Por fim, executamos algumas consultas de pesquisa e exibimos os resultados.</span><span class="sxs-lookup"><span data-stu-id="7379e-163">Finally, we execute a few search queries and display the results.</span></span> <span data-ttu-id="7379e-164">Dessa vez, usamos outro `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="7379e-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="7379e-165">Posteriormente, faremos uma análise mais detalhada do método `RunQueries`.</span><span class="sxs-lookup"><span data-stu-id="7379e-165">We will take a closer look at the `RunQueries` method later.</span></span> <span data-ttu-id="7379e-166">Este é o código para criar o novo `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="7379e-166">Here is the code to create the new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="7379e-167">Dessa vez, usaremos uma chave de consulta, já que não precisamos de acesso de gravação para o índice.</span><span class="sxs-lookup"><span data-stu-id="7379e-167">This time we use a query key since we do not need write access to the index.</span></span> <span data-ttu-id="7379e-168">Você pode inserir essas informações no arquivo `appsettings.json` do [aplicativo de exemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="7379e-168">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="7379e-169">Se você executar esse aplicativo com um nome de serviço válido e chaves API, o resultado deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="7379e-169">If you run this application with a valid service name and API keys, the output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents to be indexed...
    
    Search the entire index for the term 'budget' and return only the hotelName field:
    
    Name: Roach Motel
    
    Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river
    
    Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search the entire index for the term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key to end application...

<span data-ttu-id="7379e-170">O código-fonte completo do aplicativo é fornecido ao final deste artigo.</span><span class="sxs-lookup"><span data-stu-id="7379e-170">The full source code of the application is provided at the end of this article.</span></span>

<span data-ttu-id="7379e-171">Em seguida, analisaremos com mais detalhes cada um dos métodos chamados pelo `Main`.</span><span class="sxs-lookup"><span data-stu-id="7379e-171">Next, we will take a closer look at each of the methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="7379e-172">Criando um índice</span><span class="sxs-lookup"><span data-stu-id="7379e-172">Creating an index</span></span>
<span data-ttu-id="7379e-173">Depois de criar um `SearchServiceClient`, a próxima coisa que o `Main` faz é excluir o índice "hotéis", caso ele já exista.</span><span class="sxs-lookup"><span data-stu-id="7379e-173">After creating a `SearchServiceClient`, the next thing `Main` does is delete the "hotels" index if it already exists.</span></span> <span data-ttu-id="7379e-174">Isso é feito pelo método a seguir:</span><span class="sxs-lookup"><span data-stu-id="7379e-174">That is done by the following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="7379e-175">Esse método usa o `SearchServiceClient` fornecido para verificar se o índice existe e, nesse caso, excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="7379e-175">This method uses the given `SearchServiceClient` to check if the index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="7379e-176">O exemplo código deste artigo usa os métodos síncronos do SDK do .NET da Pesquisa do Azure para manter a simplicidade.</span><span class="sxs-lookup"><span data-stu-id="7379e-176">The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="7379e-177">Recomendamos que você use os métodos assíncronos em seus próprios aplicativos para mantê-los escalonáveis e responsivos.</span><span class="sxs-lookup"><span data-stu-id="7379e-177">We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive.</span></span> <span data-ttu-id="7379e-178">Por exemplo, no método acima você pode usar `ExistsAsync` e `DeleteAsync` em vez de `Exists` e `Delete`.</span><span class="sxs-lookup"><span data-stu-id="7379e-178">For example, in the method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="7379e-179">Em seguida, `Main` cria um novo índice "hotéis" chamando este método:</span><span class="sxs-lookup"><span data-stu-id="7379e-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

<span data-ttu-id="7379e-180">Esse método cria um novo objeto `Index` com uma lista de objetos `Field` que definem o esquema do novo índice.</span><span class="sxs-lookup"><span data-stu-id="7379e-180">This method creates a new `Index` object with a list of `Field` objects that defines the schema of the new index.</span></span> <span data-ttu-id="7379e-181">Cada campo tem um nome, tipo de dados e vários atributos que definem seu comportamento de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="7379e-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="7379e-182">A classe `FieldBuilder` usa a reflexão para criar uma lista de objetos `Field` para o índice, examinando os atributos e propriedades públicas da classe do modelo `Hotel` determinada.</span><span class="sxs-lookup"><span data-stu-id="7379e-182">The `FieldBuilder` class uses reflection to create a list of `Field` objects for the index by examining the public properties and attributes of the given `Hotel` model class.</span></span> <span data-ttu-id="7379e-183">Posteriormente, faremos uma análise mais detalhada da classe `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="7379e-183">We'll take a closer look at the `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="7379e-184">Você pode criar quando desejar a lista de objetos `Field` diretamente, em vez de usar o `FieldBuilder` se necessário.</span><span class="sxs-lookup"><span data-stu-id="7379e-184">You can always create the list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="7379e-185">Por exemplo, você pode não querer usar uma classe de modelo ou pode precisar usar uma classe de modelo existente que não deseja modificar adicionando atributos.</span><span class="sxs-lookup"><span data-stu-id="7379e-185">For example, you may not want to use a model class or you may need to use an existing model class that you don't want to modify by adding attributes.</span></span>
>
> 

<span data-ttu-id="7379e-186">Além dos campos, você também pode adicionar perfis de pontuação, sugestões ou opções de CORS para o índice (eles foram omitidos do exemplo por questão de brevidade).</span><span class="sxs-lookup"><span data-stu-id="7379e-186">In addition to fields, you can also add scoring profiles, suggesters, or CORS options to the Index (these are omitted from the sample for brevity).</span></span> <span data-ttu-id="7379e-187">Você pode saber mais sobre o objeto Index e suas partes na [referência do SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), bem como na [Referência da API REST do Azure Search](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="7379e-187">You can find more information about the Index object and its constituent parts in the [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-the-index"></a><span data-ttu-id="7379e-188">Preenchendo o índice</span><span class="sxs-lookup"><span data-stu-id="7379e-188">Populating the index</span></span>
<span data-ttu-id="7379e-189">A próxima etapa no `Main` é popular o índice recém-criado.</span><span class="sxs-lookup"><span data-stu-id="7379e-189">The next step in `Main` is to populate the newly-created index.</span></span> <span data-ttu-id="7379e-190">Isso é feito com o método a seguir:</span><span class="sxs-lookup"><span data-stu-id="7379e-190">This is done in the following method:</span></span>

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
        new Hotel()
        { 
            HotelId = "1", 
            BaseRate = 199.0, 
            Description = "Best hotel in town",
            DescriptionFr = "Meilleur hôtel en ville",
            HotelName = "Fancy Stay",
            Category = "Luxury", 
            Tags = new[] { "pool", "view", "wifi", "concierge" },
            ParkingIncluded = false, 
            SmokingAllowed = false,
            LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero), 
            Rating = 5, 
            Location = GeographyPoint.Create(47.678581, -122.131577)
        },
        new Hotel()
        { 
            HotelId = "2", 
            BaseRate = 79.99,
            Description = "Cheapest hotel in town",
            DescriptionFr = "Hôtel le moins cher en ville",
            HotelName = "Roach Motel",
            Category = "Budget",
            Tags = new[] { "motel", "budget" },
            ParkingIncluded = true,
            SmokingAllowed = true,
            LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
            Rating = 1,
            Location = GeographyPoint.Create(49.678581, -122.131577)
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close to town hall and the river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of the documents in
        // the batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log the failed document keys and continue.
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents to be indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="7379e-191">Este método tem quatro partes.</span><span class="sxs-lookup"><span data-stu-id="7379e-191">This method has four parts.</span></span> <span data-ttu-id="7379e-192">O primeiro cria uma matriz de objetos `Hotel` que servirá como nossos dados de entrada para carregamento do índice.</span><span class="sxs-lookup"><span data-stu-id="7379e-192">The first creates an array of `Hotel` objects that will serve as our input data to upload to the index.</span></span> <span data-ttu-id="7379e-193">Esses dados são codificados para manter a simplicidade.</span><span class="sxs-lookup"><span data-stu-id="7379e-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="7379e-194">Em seu próprio aplicativo, provavelmente seus dados virão de uma fonte de dados externa, como um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="7379e-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="7379e-195">A segunda parte cria um `IndexBatch` com os documentos.</span><span class="sxs-lookup"><span data-stu-id="7379e-195">The second part creates an `IndexBatch` containing the documents.</span></span> <span data-ttu-id="7379e-196">Especifique a operação que você quer aplicar ao lote no momento da criação dele, nesse caso, chamando `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="7379e-196">You specify the operation you want to apply to the batch at the time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="7379e-197">O lote é então carregado para o índice da Pesquisa do Azure pelo método `Documents.Index` .</span><span class="sxs-lookup"><span data-stu-id="7379e-197">The batch is then uploaded to the Azure Search index by the `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="7379e-198">Neste exemplo, estamos carregando apenas documentos.</span><span class="sxs-lookup"><span data-stu-id="7379e-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="7379e-199">Se você quiser mesclar alterações em documentos existentes ou excluir documentos, poderá criar lotes chamando `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` ou `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="7379e-199">If you wanted to merge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="7379e-200">Também é possível combinar diferentes operações em um único lote chamando `IndexBatch.New`, que usa uma coleção de objetos `IndexAction`, com cada um deles informando à Pesquisa do Azure para executar uma operação específica em um documento.</span><span class="sxs-lookup"><span data-stu-id="7379e-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search to perform a particular operation on a document.</span></span> <span data-ttu-id="7379e-201">Você pode criar cada `IndexAction` com sua própria operação chamando o método correspondente como `IndexAction.Merge`, `IndexAction.Upload` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="7379e-201">You can create each `IndexAction` with its own operation by calling the corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="7379e-202">A terceira parte desse método é um bloco catch que trata um caso de erro importante para indexação.</span><span class="sxs-lookup"><span data-stu-id="7379e-202">The third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="7379e-203">Se o serviço de Pesquisa do Azure não indexar alguns documentos no lote, uma `IndexBatchException` será lançada por `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="7379e-203">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="7379e-204">Isso pode acontecer se você estiver indexando documentos enquanto o serviço estiver sob carga pesada.</span><span class="sxs-lookup"><span data-stu-id="7379e-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="7379e-205">**É altamente recomendável a manipulação explícita desse caso em seu código.**</span><span class="sxs-lookup"><span data-stu-id="7379e-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="7379e-206">Você pode atrasar e repetir a indexação de documentos que falharam, ou você pode registrar em log e continuar, como faz o exemplo, ou pode alguma outra coisa, dependendo dos requisitos de consistência de dados do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7379e-206">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="7379e-207">Você pode usar o método `FindFailedActionsToRetry` para criar um novo lote contendo somente as ações que falharam em uma chamada anterior para `Index`.</span><span class="sxs-lookup"><span data-stu-id="7379e-207">You can use the `FindFailedActionsToRetry` method to construct a new batch containing only the actions that failed in a previous call to `Index`.</span></span> <span data-ttu-id="7379e-208">O método é documentado [aqui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) e há uma discussão sobre como usá-lo corretamente [em StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="7379e-208">The method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how to properly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="7379e-209">Por fim, o método `UploadDocuments` atrasa por dois segundos.</span><span class="sxs-lookup"><span data-stu-id="7379e-209">Finally, the `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="7379e-210">A indexação ocorre de maneira assíncrona em seu serviço de Pesquisa do Azure, portanto, o exemplo de aplicativo precisa aguardar alguns instantes para garantir que os documentos estejam disponíveis para pesquisa.</span><span class="sxs-lookup"><span data-stu-id="7379e-210">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="7379e-211">Normalmente, atrasos como esses só são necessários em demonstrações, testes e exemplos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="7379e-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="7379e-212">Como o SDK do .NET lida com documentos</span><span class="sxs-lookup"><span data-stu-id="7379e-212">How the .NET SDK handles documents</span></span>
<span data-ttu-id="7379e-213">Você pode estar se perguntando como o SDK do .NET da Pesquisa do Azure é capaz de carregar instâncias de uma classe definida pelo usuário, como `Hotel` , no índice.</span><span class="sxs-lookup"><span data-stu-id="7379e-213">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="7379e-214">Para ajudar a responder a essa pergunta, vamos examinar a classe `Hotel` :</span><span class="sxs-lookup"><span data-stu-id="7379e-214">To help answer that question, let's look at the `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// The SerializePropertyNamesAsCamelCase attribute is defined in the Azure Search .NET SDK.
// It ensures that Pascal-case property names in the model class are mapped to camel-case
// field names in the index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }
}
```

<span data-ttu-id="7379e-215">A primeira coisa a observar é que cada propriedade pública de `Hotel` corresponde a um campo na definição do índice, mas com uma diferença fundamental: o nome de cada campo começa com uma letra minúscula ("minúsculas concatenadas"), enquanto o nome de cada propriedade pública de `Hotel` começa com uma letra maiúscula ("maiúsculas concatenadas").</span><span class="sxs-lookup"><span data-stu-id="7379e-215">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="7379e-216">Esse é um cenário comum em aplicativos .NET que executam associação de dados quando o esquema de destino está fora do controle do desenvolvedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7379e-216">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="7379e-217">Em vez de violar as diretrizes de nomenclatura do .NET, usando minúscula para os nomes de propriedade, você pode informar ao SDK para mapear automaticamente os nomes de propriedade como minúscula com o atributo `[SerializePropertyNamesAsCamelCase]` .</span><span class="sxs-lookup"><span data-stu-id="7379e-217">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="7379e-218">O SDK do .NET de Pesquisa do Azure usa a biblioteca [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) para serializar e desserializar os objetos de modelo personalizados para e a partir do JSON.</span><span class="sxs-lookup"><span data-stu-id="7379e-218">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="7379e-219">Se necessário, você pode personalizar essa serialização.</span><span class="sxs-lookup"><span data-stu-id="7379e-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="7379e-220">Para obter mais detalhes, consulte [Serialização personalizada com JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="7379e-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="7379e-221">A segunda coisa a observar são os atributos como `IsFilterable`, `IsSearchable`, `Key` e `Analyzer` que decoram cada propriedade pública.</span><span class="sxs-lookup"><span data-stu-id="7379e-221">The second thing to notice are the attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="7379e-222">Esses atributos são mapeados diretamente para os [atributos correspondentes do índice da Azure Search](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="7379e-222">These attributes map directly to the [corresponding attributes of the Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="7379e-223">A classe `FieldBuilder` os utiliza para criar definições de campo para o índice.</span><span class="sxs-lookup"><span data-stu-id="7379e-223">The `FieldBuilder` class uses these to construct field definitions for the index.</span></span>

<span data-ttu-id="7379e-224">O terceiro fator importante sobre a classe `Hotel` são os tipos de dados das propriedades públicas.</span><span class="sxs-lookup"><span data-stu-id="7379e-224">The third important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="7379e-225">Os tipos .NET dessas propriedades estão mapeados para seus tipos de campo equivalentes na definição do índice.</span><span class="sxs-lookup"><span data-stu-id="7379e-225">The .NET types of  these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="7379e-226">Por exemplo, a propriedade de cadeia de caracteres `Category` mapeia para o campo `category`, que é do tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="7379e-226">For example, the `Category` string property maps to the `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="7379e-227">Há mapeamentos de tipo semelhantes entre `bool?` e `Edm.Boolean`, `DateTimeOffset?` e `Edm.DateTimeOffset` etc. As regras específicas para o mapeamento de tipos estão documentadas com o método `Documents.Get` na [referência do SDK do .NET do Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="7379e-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="7379e-228">A classe `FieldBuilder` cuida desse mapeamento para você, mas ainda pode ser útil para entender caso você precise solucionar problemas de serialização.</span><span class="sxs-lookup"><span data-stu-id="7379e-228">The `FieldBuilder` class takes care of this mapping for you, but it can still be helpful to understand in case you need to troubleshoot any serialization issues.</span></span>

<span data-ttu-id="7379e-229">Essa capacidade de usar suas próprias classes como documentos funciona em ambas as direções; Você também pode recuperar os resultados da pesquisa e fazer com que o SDK os desserialize automaticamente para um tipo de sua escolha, como veremos na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="7379e-229">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as we will see in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="7379e-230">O SDK do .NET da Pesquisa do Azure também oferece suporte a documentos do tipo dinâmico usando a classe `Document`, que é um mapeamento de chave/valor de nomes de campo para valores de campo.</span><span class="sxs-lookup"><span data-stu-id="7379e-230">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="7379e-231">Isso é útil em cenários nos quais você não conhece o esquema de índice no momento do design, ou nos quais seria inconveniente associar a classes de modelo específico.</span><span class="sxs-lookup"><span data-stu-id="7379e-231">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="7379e-232">Todos os métodos no SDK que lidam com documentos têm sobrecargas que funcionam com a classe `Document` , bem como sobrecargas fortemente tipadas que utilizam um parâmetro de tipo genérico.</span><span class="sxs-lookup"><span data-stu-id="7379e-232">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="7379e-233">Somente as últimas são usadas no exemplo de código deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="7379e-233">Only the latter are used in the sample code in this tutorial.</span></span> <span data-ttu-id="7379e-234">A classe `Document` herda de `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="7379e-234">The `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="7379e-235">Encontre outros detalhes [aqui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="7379e-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="7379e-236">**Por que você deve usar tipos de dados anuláveis**</span><span class="sxs-lookup"><span data-stu-id="7379e-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="7379e-237">Ao criar suas próprias classes de modelo para mapear para um índice de Pesquisa do Azure, sugerimos declarar as propriedades dos tipos de valor como `bool` e `int` para serem anuláveis (por exemplo, `bool?` em vez de `bool`).</span><span class="sxs-lookup"><span data-stu-id="7379e-237">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="7379e-238">Se você usar uma propriedade não anulável, será preciso **assegurar** que nenhum documento no índice contenha um valor nulo para o campo correspondente.</span><span class="sxs-lookup"><span data-stu-id="7379e-238">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="7379e-239">Nem o SDK, nem o serviço Pesquisa do Azure ajudarão você a impor isso.</span><span class="sxs-lookup"><span data-stu-id="7379e-239">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="7379e-240">Isso não é apenas uma preocupação hipotética: imagine um cenário em que você adiciona um novo campo a um índice existente do tipo `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="7379e-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="7379e-241">Depois de atualizar a definição de índice, todos os documentos terão um valor nulo para esse novo campo (já que todos os tipos são anuláveis na Pesquisa do Azure).</span><span class="sxs-lookup"><span data-stu-id="7379e-241">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="7379e-242">Ao usar uma classe de modelo com uma propriedade não anulável `int` para esse campo, você obterá uma `JsonSerializationException` como esta ao tentar recuperar os documentos:</span><span class="sxs-lookup"><span data-stu-id="7379e-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="7379e-243">Por esse motivo, sugerimos que você use tipos anuláveis nas suas classes de modelo como uma prática recomendada.</span><span class="sxs-lookup"><span data-stu-id="7379e-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="7379e-244">Serialização personalizada com JSON.NET</span><span class="sxs-lookup"><span data-stu-id="7379e-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="7379e-245">O SDK usa JSON.NET para serializar e desserializar documentos.</span><span class="sxs-lookup"><span data-stu-id="7379e-245">The SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="7379e-246">Você pode personalizar a serialização e desserialização, se necessário, definindo seu próprio `JsonConverter` ou `IContractResolver` (consulte a [documentação do JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) para obter mais detalhes).</span><span class="sxs-lookup"><span data-stu-id="7379e-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see the [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="7379e-247">Isso pode ser útil quando você quer adaptar uma classe de modelo existente de seu aplicativo para usar com a Pesquisa do Azure e outros cenários mais avançados.</span><span class="sxs-lookup"><span data-stu-id="7379e-247">This can be useful when you want to adapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="7379e-248">Por exemplo, com a serialização personalizada, você pode:</span><span class="sxs-lookup"><span data-stu-id="7379e-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="7379e-249">Incluir ou excluir determinadas propriedades da sua classe de modelo para serem armazenadas como campos de documento.</span><span class="sxs-lookup"><span data-stu-id="7379e-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="7379e-250">Mapear os nomes de propriedade no código aos nomes de campo no índice.</span><span class="sxs-lookup"><span data-stu-id="7379e-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="7379e-251">Crie atributos personalizados que podem ser usados para mapear propriedades para campos do documento.</span><span class="sxs-lookup"><span data-stu-id="7379e-251">Create custom attributes that can be used for mapping properties to document fields.</span></span>

<span data-ttu-id="7379e-252">Você pode encontrar exemplos de implementação de serialização personalizada nos testes de unidade para o SDK .NET da Pesquisa do Azure no GitHub.</span><span class="sxs-lookup"><span data-stu-id="7379e-252">You can find examples of implementing custom serialization in the unit tests for the Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="7379e-253">Um bom ponto de partida é [esta pasta](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span><span class="sxs-lookup"><span data-stu-id="7379e-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="7379e-254">Ela contém classes que são usadas pelos testes de serialização personalizada.</span><span class="sxs-lookup"><span data-stu-id="7379e-254">It contains classes that are used by the custom serialization tests.</span></span>

### <a name="searching-for-documents-in-the-index"></a><span data-ttu-id="7379e-255">Pesquisando documentos no índice</span><span class="sxs-lookup"><span data-stu-id="7379e-255">Searching for documents in the index</span></span>
<span data-ttu-id="7379e-256">A última etapa no exemplo de aplicativo é procurar por documentos no índice.</span><span class="sxs-lookup"><span data-stu-id="7379e-256">The last step in the sample application is to search for some documents in the index.</span></span> <span data-ttu-id="7379e-257">O método a seguir faz isso:</span><span class="sxs-lookup"><span data-stu-id="7379e-257">The following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
    Console.WriteLine("and return the hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take the top two results, and show only hotelName and ");
    Console.WriteLine("lastRenovationDate:\n");

    parameters =
        new SearchParameters()
        {
            OrderBy = new[] { "lastRenovationDate desc" },
            Select = new[] { "hotelName", "lastRenovationDate" },
            Top = 2
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.WriteLine("Search the entire index for the term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="7379e-258">Cada vez que ele executa uma consulta, esse método cria, primeiro, um novo objeto `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="7379e-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="7379e-259">Isso é usado para especificar opções adicionais para a consulta, como classificação, filtragem, paginação e organização.</span><span class="sxs-lookup"><span data-stu-id="7379e-259">This is used to specify additional options for the query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="7379e-260">Nesse método, estamos definindo as propriedades de `Filter`, `Select`, `OrderBy` e `Top` para consultas diferentes.</span><span class="sxs-lookup"><span data-stu-id="7379e-260">In this method, we're setting the `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="7379e-261">Todas as propriedades de `SearchParameters` são documentadas [aqui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="7379e-261">All the `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="7379e-262">A próxima etapa é executar a consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="7379e-262">The next step is to actually execute the search query.</span></span> <span data-ttu-id="7379e-263">Isso é feito usando o método `Documents.Search` .</span><span class="sxs-lookup"><span data-stu-id="7379e-263">This is done using the `Documents.Search` method.</span></span> <span data-ttu-id="7379e-264">Para cada consulta, passamos o texto de pesquisa a ser usado como uma cadeia de caracteres (ou `"*"` se não houver um texto de pesquisa) e também os parâmetros de pesquisa criados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7379e-264">For each query, we pass the search text to use as a string (or `"*"` if there is no search text), plus the search parameters created earlier.</span></span> <span data-ttu-id="7379e-265">Também podemos especificar `Hotel` como o parâmetro de tipo para `Documents.Search`, que informa ao SDK para desserializar documentos nos resultados da pesquisa em objetos do tipo `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="7379e-265">We also specify `Hotel` as the type parameter for `Documents.Search`, which tells the SDK to deserialize documents in the search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="7379e-266">Você pode saber mais sobre a sintaxe de expressão da consulta de pesquisa [aqui](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="7379e-266">You can find more information about the search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="7379e-267">Por fim, depois de cada consulta, esse método percorre todas as correspondências nos resultados da pesquisa, imprimindo cada documento no console:</span><span class="sxs-lookup"><span data-stu-id="7379e-267">Finally, after each query this method iterates through all the matches in the search results, printing each document to the console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="7379e-268">Vejamos cada uma das consultas com mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="7379e-268">Let's take a closer look at each of the queries in turn.</span></span> <span data-ttu-id="7379e-269">Este é o código para executar a primeira consulta:</span><span class="sxs-lookup"><span data-stu-id="7379e-269">Here is the code to execute the first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="7379e-270">Neste caso, estamos pesquisando hotéis que correspondam à palavra "budget" e queremos nos resultados apenas os nomes dos hotéis, conforme especificado pelo parâmetro `Select`.</span><span class="sxs-lookup"><span data-stu-id="7379e-270">In this case, we're searching for hotels that match the word "budget", and we want to get back only the hotel names, as specified by the `Select` parameter.</span></span> <span data-ttu-id="7379e-271">Estes são os resultados:</span><span class="sxs-lookup"><span data-stu-id="7379e-271">Here are the results:</span></span>

    Name: Roach Motel

<span data-ttu-id="7379e-272">Em seguida, queremos encontrar hotéis com uma diária inferior a US$ 150 e obter resultados somente com a ID e descrição dos hotéis:</span><span class="sxs-lookup"><span data-stu-id="7379e-272">Next, we want to find the hotels with a nightly rate of less than $150, and return only the hotel ID and description:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="7379e-273">Esta consulta usa uma expressão `$filter` do OData, `baseRate lt 150`, para filtrar os documentos no índice.</span><span class="sxs-lookup"><span data-stu-id="7379e-273">This query uses an OData `$filter` expression, `baseRate lt 150`, to filter the documents in the index.</span></span> <span data-ttu-id="7379e-274">Você pode saber mais sobre a sintaxe do OData com suporte da Pesquisa do Azure [aqui](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="7379e-274">You can find out more about the OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="7379e-275">Estes são alguns dos resultados da consulta:</span><span class="sxs-lookup"><span data-stu-id="7379e-275">Here are the results of the query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river

<span data-ttu-id="7379e-276">Em seguida, queremos localizar os dois principais hotéis reformados mais recentemente e mostrar o nome dos hotéis e a data da última reforma.</span><span class="sxs-lookup"><span data-stu-id="7379e-276">Next, we want to find the top two hotels that have been most recently renovated, and show the hotel name and last renovation date.</span></span> <span data-ttu-id="7379e-277">Eis o código:</span><span class="sxs-lookup"><span data-stu-id="7379e-277">Here is the code:</span></span> 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="7379e-278">Neste caso, usaremos novamente a sintaxe do OData para especificar o parâmetro `OrderBy` como `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="7379e-278">In this case, we again use OData syntax to specify the `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="7379e-279">Também vamos definir `Top` como 2 para garantir que só iremos receber os dois principais documentos.</span><span class="sxs-lookup"><span data-stu-id="7379e-279">We also set `Top` to 2 to ensure we only get the top two documents.</span></span> <span data-ttu-id="7379e-280">Como antes, definimos `Select` para especificar quais campos devem ser retornados.</span><span class="sxs-lookup"><span data-stu-id="7379e-280">As before, we set `Select` to specify which fields should be returned.</span></span>

<span data-ttu-id="7379e-281">Estes são os resultados:</span><span class="sxs-lookup"><span data-stu-id="7379e-281">Here are the results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="7379e-282">Por fim, queremos encontrar todos os hotéis que correspondam à palavra "motel":</span><span class="sxs-lookup"><span data-stu-id="7379e-282">Finally, we want to find all hotels that match the word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="7379e-283">Estes são os resultados, que incluem todos os campos uma vez que não especificamos a propriedade `Select`:</span><span class="sxs-lookup"><span data-stu-id="7379e-283">And here are the results, which include all fields since we did not specify the `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="7379e-284">Essa etapa conclui o tutorial, mas não pare aqui.</span><span class="sxs-lookup"><span data-stu-id="7379e-284">This step completes the tutorial, but don't stop here.</span></span> <span data-ttu-id="7379e-285">**Próximas etapas** fornece os recursos adicionais para aprender mais sobre a Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="7379e-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7379e-286">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7379e-286">Next steps</span></span>
* <span data-ttu-id="7379e-287">Procure as referências para o [SDK do .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) e a [API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="7379e-287">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="7379e-288">Aprofunde seus conhecimentos por meio de [vídeos e outros exemplos e tutoriais](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="7379e-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="7379e-289">Revise as [convenções de nomenclatura](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) para saber as regras de nomeação de vários objetos.</span><span class="sxs-lookup"><span data-stu-id="7379e-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) to learn the rules for naming various objects.</span></span>
* <span data-ttu-id="7379e-290">Examine os [tipos de dados com suporte](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) na Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="7379e-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
