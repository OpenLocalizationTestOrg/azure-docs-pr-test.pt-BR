---
title: aaaHow toouse pesquisa do Azure de um aplicativo .NET | Microsoft Docs
description: Como o Azure toouse de pesquisa de um aplicativo .NET
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
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a><span data-ttu-id="d1313-103">Como o Azure toouse de pesquisa de um aplicativo .NET</span><span class="sxs-lookup"><span data-stu-id="d1313-103">How toouse Azure Search from a .NET Application</span></span>
<span data-ttu-id="d1313-104">Este artigo é um passo a passo tooget você em funcionamento com hello [SDK .NET da pesquisa do Azure](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="d1313-104">This article is a walkthrough tooget you up and running with hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="d1313-105">Você pode usar Olá .NET SDK tooimplement uma rica experiência de pesquisa em seu aplicativo usando a pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1313-105">You can use hello .NET SDK tooimplement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-hello-azure-search-sdk"></a><span data-ttu-id="d1313-106">O que é Olá a pesquisa do Azure SDK</span><span class="sxs-lookup"><span data-stu-id="d1313-106">What's in hello Azure Search SDK</span></span>
<span data-ttu-id="d1313-107">Olá SDK consiste em uma biblioteca de cliente, `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="d1313-107">hello SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="d1313-108">Ele permite que você toomanage seus índices, fontes de dados e indexadores, bem como carregar e gerenciar documentos e executar consultas, sem a necessidade de toodeal com detalhes de saudação do HTTP e JSON.</span><span class="sxs-lookup"><span data-stu-id="d1313-108">It enables you toomanage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having toodeal with hello details of HTTP and JSON.</span></span>

<span data-ttu-id="d1313-109">biblioteca de cliente Olá define classes como `Index`, `Field`, e `Document`, bem como operações como `Indexes.Create` e `Documents.Search` em Olá `SearchServiceClient` e `SearchIndexClient` classes.</span><span class="sxs-lookup"><span data-stu-id="d1313-109">hello client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on hello `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="d1313-110">Essas classes são organizadas em Olá namespaces a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1313-110">These classes are organized into hello following namespaces:</span></span>

* [<span data-ttu-id="d1313-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="d1313-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="d1313-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="d1313-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="d1313-113">versão atual de saudação do hello SDK .NET da pesquisa do Azure agora está disponível.</span><span class="sxs-lookup"><span data-stu-id="d1313-113">hello current version of hello Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="d1313-114">Se você quiser tooprovide comentários para que possamos tooincorporate na próxima versão de hello, visite nosso [página de comentários](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="d1313-114">If you would like tooprovide feedback for us tooincorporate in hello next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="d1313-115">Olá SDK .NET oferece suporte à versão `2016-09-01` de saudação [API de REST de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="d1313-115">hello .NET SDK supports version `2016-09-01` of hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="d1313-116">Agora, essa versão inclui suporte para analisadores personalizados e suporte para indexador de Tabela do Azure e Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1313-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="d1313-117">Recursos que são de visualização *não* parte desta versão, como o suporte para indexação de arquivos CSV e JSON, estão em [visualização](search-api-2015-02-28-preview.md) e disponível por meio de saudação anterior [versão 2.0-visualização do SDK .NET de saudação ](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="d1313-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via hello older [2.0-preview version of hello .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="d1313-118">Esse SDK não oferece suporte a [Operações de Gerenciamento](https://docs.microsoft.com/rest/api/searchmanagement/), como criar e dimensionar os serviços de Pesquisa e gerenciar chaves de API.</span><span class="sxs-lookup"><span data-stu-id="d1313-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="d1313-119">Se você precisar toomanage seus recursos de pesquisa de um aplicativo .NET, você pode usar o hello [Azure SDK de gerenciamento de .NET da pesquisa](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="d1313-119">If you need toomanage your Search resources from a .NET application, you can use hello [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a><span data-ttu-id="d1313-120">Atualizando a versão mais recente toohello de saudação SDK</span><span class="sxs-lookup"><span data-stu-id="d1313-120">Upgrading toohello latest version of hello SDK</span></span>
<span data-ttu-id="d1313-121">Se você já estiver usando uma versão mais antiga do hello SDK .NET da pesquisa do Azure e você desejar tooupgrade toohello nova disponível versão, [neste artigo](search-dotnet-sdk-migration.md) explica como.</span><span class="sxs-lookup"><span data-stu-id="d1313-121">If you're already using an older version of hello Azure Search .NET SDK and you'd like tooupgrade toohello new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-hello-sdk"></a><span data-ttu-id="d1313-122">Requisitos para Olá SDK</span><span class="sxs-lookup"><span data-stu-id="d1313-122">Requirements for hello SDK</span></span>
1. <span data-ttu-id="d1313-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d1313-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="d1313-124">Seu próprio serviço de Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1313-124">Your own Azure Search service.</span></span> <span data-ttu-id="d1313-125">Saudação de toouse ordem SDK, você precisará nome de saudação do serviço e uma ou mais chaves de API.</span><span class="sxs-lookup"><span data-stu-id="d1313-125">In order toouse hello SDK, you will need hello name of your service and one or more API keys.</span></span> <span data-ttu-id="d1313-126">[Criar um serviço no portal de saudação](search-create-service-portal.md) ajudá-lo através dessas etapas.</span><span class="sxs-lookup"><span data-stu-id="d1313-126">[Create a service in hello portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="d1313-127">Baixar o SDK .NET da pesquisa do Azure de saudação [pacote NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) usando "Gerenciar pacotes NuGet" no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1313-127">Download hello Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="d1313-128">Procurar nome de pacote hello `Microsoft.Azure.Search` em NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="d1313-128">Just search for hello package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="d1313-129">Olá SDK .NET da pesquisa do Azure oferece suporte a aplicativos destinados a saudação do .NET Framework 4.6 e o .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d1313-129">hello Azure Search .NET SDK supports applications targeting hello .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="d1313-130">Principais cenários</span><span class="sxs-lookup"><span data-stu-id="d1313-130">Core scenarios</span></span>
<span data-ttu-id="d1313-131">Há várias coisas que você precisará toodo no seu aplicativo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d1313-131">There are several things you'll need toodo in your search application.</span></span> <span data-ttu-id="d1313-132">Neste tutorial, abordaremos os principais cenários:</span><span class="sxs-lookup"><span data-stu-id="d1313-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="d1313-133">Criando um índice</span><span class="sxs-lookup"><span data-stu-id="d1313-133">Creating an index</span></span>
* <span data-ttu-id="d1313-134">Popular o índice de saudação com documentos</span><span class="sxs-lookup"><span data-stu-id="d1313-134">Populating hello index with documents</span></span>
* <span data-ttu-id="d1313-135">Procura por documentos usando filtros e pesquisa de texto completo</span><span class="sxs-lookup"><span data-stu-id="d1313-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="d1313-136">código de exemplo Hello a seguir ilustra cada um deles.</span><span class="sxs-lookup"><span data-stu-id="d1313-136">hello sample code that follows illustrates each of these.</span></span> <span data-ttu-id="d1313-137">Sinta-se livre toouse Olá trechos de código em seu próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1313-137">Feel free toouse hello code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="d1313-138">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d1313-138">Overview</span></span>
<span data-ttu-id="d1313-139">Olá vamos explorar do aplicativo de exemplo cria um novo índice chamado "hotéis", preenche-o com alguns documentos, em seguida, executa algumas consultas de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d1313-139">hello sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="d1313-140">Aqui está o programa principal hello, mostrando Olá fluxo geral:</span><span class="sxs-lookup"><span data-stu-id="d1313-140">Here is hello main program, showing hello overall flow:</span></span>

```csharp
// This sample shows how toodelete, create, upload documents and query an index
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

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="d1313-141">Você pode encontrar o código-fonte completo Olá Olá do aplicativo de exemplo usado no passo a passo no [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="d1313-141">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="d1313-142">Vamos examinar isso passo a passo.</span><span class="sxs-lookup"><span data-stu-id="d1313-142">We'll walk through this step by step.</span></span> <span data-ttu-id="d1313-143">Primeiro, precisamos toocreate um novo `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="d1313-143">First we need toocreate a new `SearchServiceClient`.</span></span> <span data-ttu-id="d1313-144">Esse objeto permite toomanage índices.</span><span class="sxs-lookup"><span data-stu-id="d1313-144">This object allows you toomanage indexes.</span></span> <span data-ttu-id="d1313-145">Ordem tooconstruct um, é necessário tooprovide o nome do serviço de pesquisa do Azure, bem como uma chave de API de administração.</span><span class="sxs-lookup"><span data-stu-id="d1313-145">In order tooconstruct one, you need tooprovide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="d1313-146">Você pode inserir essas informações em Olá `appsettings.json` arquivo hello [aplicativo de exemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="d1313-146">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

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
> <span data-ttu-id="d1313-147">Se você fornecer uma chave incorreta (por exemplo, uma chave de consulta em que foi necessária uma chave de administração), Olá `SearchServiceClient` lançará um `CloudException` com hello "Proibido" de mensagem do hello erro primeira vez que você chamar um método de operação, como `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="d1313-147">If you provide an incorrect key (for example, a query key where an admin key was required), hello `SearchServiceClient` will throw a `CloudException` with hello error message "Forbidden" hello first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="d1313-148">Se isso acontecer tooyou, verifique novamente a chave de API.</span><span class="sxs-lookup"><span data-stu-id="d1313-148">If this happens tooyou, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="d1313-149">Olá próximas linhas chamar métodos toocreate um índice nomeado "hotéis", excluí-lo pela primeira vez, se ele já existe.</span><span class="sxs-lookup"><span data-stu-id="d1313-149">hello next few lines call methods toocreate an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="d1313-150">Abordaremos esses métodos um pouco mais tarde.</span><span class="sxs-lookup"><span data-stu-id="d1313-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="d1313-151">Em seguida, o índice Olá precisa toobe preenchido.</span><span class="sxs-lookup"><span data-stu-id="d1313-151">Next, hello index needs toobe populated.</span></span> <span data-ttu-id="d1313-152">toodo isso, será necessário um `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="d1313-152">toodo this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="d1313-153">Há dois tooobtain maneiras um: Criando-lo, ou chamando `Indexes.GetClient` em Olá `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="d1313-153">There are two ways tooobtain one: by constructing it, or by calling `Indexes.GetClient` on hello `SearchServiceClient`.</span></span> <span data-ttu-id="d1313-154">Usamos Olá último para sua conveniência.</span><span class="sxs-lookup"><span data-stu-id="d1313-154">We use hello latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="d1313-155">Em um aplicativo típico de pesquisa, o gerenciamento e o preenchimento do índice é tratado por um componente separado das consultas de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d1313-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="d1313-156">`Indexes.GetClient`é conveniente para preencher um índice porque poupa Olá problemas de fornecer outra `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="d1313-156">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="d1313-157">Ele faz isso passando a chave de administração Olá Olá de toocreate usadas que você `SearchServiceClient` toohello novo `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="d1313-157">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="d1313-158">No entanto, em parte de saudação do aplicativo que executa consultas, é melhor Olá de toocreate `SearchIndexClient` diretamente para que você pode passar de uma chave de consulta em vez de uma chave de administração.</span><span class="sxs-lookup"><span data-stu-id="d1313-158">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="d1313-159">Isso é consistente com o princípio de saudação de menos privilégios e ajudará toomake seu aplicativo mais seguro.</span><span class="sxs-lookup"><span data-stu-id="d1313-159">This is consistent with hello principle of least privilege and will help toomake your application more secure.</span></span> <span data-ttu-id="d1313-160">Você pode saber mais sobre chaves de administração e chaves de consulta [aqui](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="d1313-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="d1313-161">Agora que temos um `SearchIndexClient`, é possível preencher o índice de hello.</span><span class="sxs-lookup"><span data-stu-id="d1313-161">Now that we have a `SearchIndexClient`, we can populate hello index.</span></span> <span data-ttu-id="d1313-162">Isso é feito por outro método que descreveremos mais tarde detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="d1313-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="d1313-163">Por fim, podemos executar algumas consultas de pesquisa e exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1313-163">Finally, we execute a few search queries and display hello results.</span></span> <span data-ttu-id="d1313-164">Dessa vez, usamos outro `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="d1313-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="d1313-165">Nós o conduziremos detalhadamente Olá `RunQueries` método posteriormente.</span><span class="sxs-lookup"><span data-stu-id="d1313-165">We will take a closer look at hello `RunQueries` method later.</span></span> <span data-ttu-id="d1313-166">Aqui está o Olá Olá de toocreate código novo `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="d1313-166">Here is hello code toocreate hello new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="d1313-167">Dessa vez usamos uma chave de consulta porque não precisamos do índice de toohello de acesso de gravação.</span><span class="sxs-lookup"><span data-stu-id="d1313-167">This time we use a query key since we do not need write access toohello index.</span></span> <span data-ttu-id="d1313-168">Você pode inserir essas informações em Olá `appsettings.json` arquivo hello [aplicativo de exemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="d1313-168">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="d1313-169">Se você executar este aplicativo com um nome de serviço válido e chaves de API, saída de hello deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="d1313-169">If you run this application with a valid service name and API keys, hello output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
    Search hello entire index for hello term 'budget' and return only hello hotelName field:
    
    Name: Roach Motel
    
    Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river
    
    Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search hello entire index for hello term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key tooend application...

<span data-ttu-id="d1313-170">código-fonte completo do aplicativo hello Olá é fornecido no final deste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="d1313-170">hello full source code of hello application is provided at hello end of this article.</span></span>

<span data-ttu-id="d1313-171">Em seguida, nós o conduziremos examinar mais detalhadamente cada um dos métodos Olá chamados pelo `Main`.</span><span class="sxs-lookup"><span data-stu-id="d1313-171">Next, we will take a closer look at each of hello methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="d1313-172">Criando um índice</span><span class="sxs-lookup"><span data-stu-id="d1313-172">Creating an index</span></span>
<span data-ttu-id="d1313-173">Depois de criar um `SearchServiceClient`, coisa Avançar Olá `Main` does é o índice de exclusão hello "hotéis" se ele já existe.</span><span class="sxs-lookup"><span data-stu-id="d1313-173">After creating a `SearchServiceClient`, hello next thing `Main` does is delete hello "hotels" index if it already exists.</span></span> <span data-ttu-id="d1313-174">Isso é feito por Olá método a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1313-174">That is done by hello following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="d1313-175">Esse método usa Olá dado `SearchServiceClient` toocheck se houver Olá índice e nesse caso, exclua-o.</span><span class="sxs-lookup"><span data-stu-id="d1313-175">This method uses hello given `SearchServiceClient` toocheck if hello index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="d1313-176">código de exemplo Hello este artigo usa métodos síncronos de saudação do hello SDK .NET da pesquisa do Azure para manter a simplicidade.</span><span class="sxs-lookup"><span data-stu-id="d1313-176">hello example code in this article uses hello synchronous methods of hello Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="d1313-177">É recomendável que você use os métodos assíncronos Olá em seu próprios aplicativos tookeep-los, escalonáveis e responsivos.</span><span class="sxs-lookup"><span data-stu-id="d1313-177">We recommend that you use hello asynchronous methods in your own applications tookeep them scalable and responsive.</span></span> <span data-ttu-id="d1313-178">Por exemplo, no hello método anteriormente, você pode usar `ExistsAsync` e `DeleteAsync` em vez de `Exists` e `Delete`.</span><span class="sxs-lookup"><span data-stu-id="d1313-178">For example, in hello method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="d1313-179">Em seguida, `Main` cria um novo índice "hotéis" chamando este método:</span><span class="sxs-lookup"><span data-stu-id="d1313-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

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

<span data-ttu-id="d1313-180">Esse método cria um novo `Index` objeto com uma lista de `Field` objetos que define o esquema de saudação do novo índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1313-180">This method creates a new `Index` object with a list of `Field` objects that defines hello schema of hello new index.</span></span> <span data-ttu-id="d1313-181">Cada campo tem um nome, tipo de dados e vários atributos que definem seu comportamento de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d1313-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="d1313-182">Olá `FieldBuilder` classe usa reflexão toocreate uma lista de `Field` objetos para o índice de saudação examinando Olá propriedades públicas e os atributos de saudação dado `Hotel` classe de modelo.</span><span class="sxs-lookup"><span data-stu-id="d1313-182">hello `FieldBuilder` class uses reflection toocreate a list of `Field` objects for hello index by examining hello public properties and attributes of hello given `Hotel` model class.</span></span> <span data-ttu-id="d1313-183">Vamos dar uma análise detalhada Olá `Hotel` classe posteriormente.</span><span class="sxs-lookup"><span data-stu-id="d1313-183">We'll take a closer look at hello `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="d1313-184">Você sempre pode criar lista de saudação do `Field` objetos diretamente em vez de usar `FieldBuilder` se necessário.</span><span class="sxs-lookup"><span data-stu-id="d1313-184">You can always create hello list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="d1313-185">Por exemplo, talvez você não queira toouse uma classe de modelo ou talvez seja necessário toouse uma classe de modelo existente que você não deseja toomodify adicionando atributos.</span><span class="sxs-lookup"><span data-stu-id="d1313-185">For example, you may not want toouse a model class or you may need toouse an existing model class that you don't want toomodify by adding attributes.</span></span>
>
> 

<span data-ttu-id="d1313-186">Além disso toofields, você pode também adicionar perfis de pontuação, sugestões ou opções de CORS toohello índice (elas são omitidas do exemplo hello para fins de brevidade).</span><span class="sxs-lookup"><span data-stu-id="d1313-186">In addition toofields, you can also add scoring profiles, suggesters, or CORS options toohello Index (these are omitted from hello sample for brevity).</span></span> <span data-ttu-id="d1313-187">Você pode encontrar mais informações sobre o objeto de índice hello e suas partes constituintes em Olá [referência de SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), bem como no hello [referência da API de REST de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="d1313-187">You can find more information about hello Index object and its constituent parts in hello [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-hello-index"></a><span data-ttu-id="d1313-188">Popular o índice de saudação</span><span class="sxs-lookup"><span data-stu-id="d1313-188">Populating hello index</span></span>
<span data-ttu-id="d1313-189">a próxima etapa Olá no `Main` toopopulate Olá recém-criado índice.</span><span class="sxs-lookup"><span data-stu-id="d1313-189">hello next step in `Main` is toopopulate hello newly-created index.</span></span> <span data-ttu-id="d1313-190">Isso é feito no hello método a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1313-190">This is done in hello following method:</span></span>

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
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
        // hello batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log hello failed document keys and continue.
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents toobe indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="d1313-191">Este método tem quatro partes.</span><span class="sxs-lookup"><span data-stu-id="d1313-191">This method has four parts.</span></span> <span data-ttu-id="d1313-192">Olá primeiro cria uma matriz de `Hotel` objetos que servirão como o índice de toohello de tooupload nossos dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="d1313-192">hello first creates an array of `Hotel` objects that will serve as our input data tooupload toohello index.</span></span> <span data-ttu-id="d1313-193">Esses dados são codificados para manter a simplicidade.</span><span class="sxs-lookup"><span data-stu-id="d1313-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="d1313-194">Em seu próprio aplicativo, provavelmente seus dados virão de uma fonte de dados externa, como um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="d1313-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="d1313-195">Olá segunda parte cria um `IndexBatch` que contêm documentos hello.</span><span class="sxs-lookup"><span data-stu-id="d1313-195">hello second part creates an `IndexBatch` containing hello documents.</span></span> <span data-ttu-id="d1313-196">Especifique Olá operação desejada tooapply toohello lote no tempo de saudação criá-lo, nesse caso, chamando `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="d1313-196">You specify hello operation you want tooapply toohello batch at hello time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="d1313-197">Olá lote for carregado toohello pesquisa do Azure de índice por Olá `Documents.Index` método.</span><span class="sxs-lookup"><span data-stu-id="d1313-197">hello batch is then uploaded toohello Azure Search index by hello `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="d1313-198">Neste exemplo, estamos carregando apenas documentos.</span><span class="sxs-lookup"><span data-stu-id="d1313-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="d1313-199">Se você quisesse toomerge alterações nos documentos existentes ou excluir documentos, você pode criar lotes chamando `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, ou `IndexBatch.Delete` em vez disso.</span><span class="sxs-lookup"><span data-stu-id="d1313-199">If you wanted toomerge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="d1313-200">Também é possível misturar operações diferentes em um único lote chamando `IndexBatch.New`, que usa uma coleção de `IndexAction` objetos, cada um deles informa tooperform de pesquisa do Azure, uma operação específica em um documento.</span><span class="sxs-lookup"><span data-stu-id="d1313-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search tooperform a particular operation on a document.</span></span> <span data-ttu-id="d1313-201">Você pode criar cada `IndexAction` com sua própria operação chamando o método correspondente hello como `IndexAction.Merge`, `IndexAction.Upload`e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="d1313-201">You can create each `IndexAction` with its own operation by calling hello corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="d1313-202">Olá terceira parte desse método é um bloco catch que manipula um caso de erro importante para indexação.</span><span class="sxs-lookup"><span data-stu-id="d1313-202">hello third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="d1313-203">Se o serviço de pesquisa do Azure falhar tooindex alguns Olá documentos em lote hello, um `IndexBatchException` é gerada pelo `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="d1313-203">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="d1313-204">Isso pode acontecer se você estiver indexando documentos enquanto o serviço estiver sob carga pesada.</span><span class="sxs-lookup"><span data-stu-id="d1313-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="d1313-205">**É altamente recomendável a manipulação explícita desse caso em seu código.**</span><span class="sxs-lookup"><span data-stu-id="d1313-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="d1313-206">Você pode atrasar e repita indexação documentos Olá que falhou, ou faça e continuar como não do exemplo hello, ou você pode fazer algo diferente, dependendo dos requisitos de consistência de dados do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1313-206">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="d1313-207">Você pode usar o hello `FindFailedActionsToRetry` método tooconstruct um novo lote que contém somente Olá ações falha em uma chamada anterior muito`Index`.</span><span class="sxs-lookup"><span data-stu-id="d1313-207">You can use hello `FindFailedActionsToRetry` method tooconstruct a new batch containing only hello actions that failed in a previous call too`Index`.</span></span> <span data-ttu-id="d1313-208">método Hello está documentado [aqui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) e há uma discussão de como tooproperly usar [em StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="d1313-208">hello method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how tooproperly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="d1313-209">Por fim, Olá `UploadDocuments` atrasos de método de dois segundos.</span><span class="sxs-lookup"><span data-stu-id="d1313-209">Finally, hello `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="d1313-210">A indexação ocorre assincronamente no serviço de pesquisa do Azure, para que o aplicativo de exemplo hello precisa toowait um tooensure curto período de tempo que os documentos de saudação estão disponíveis para pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d1313-210">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="d1313-211">Normalmente, atrasos como esses só são necessários em demonstrações, testes e exemplos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d1313-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="d1313-212">Olá como documentos de identificadores do SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="d1313-212">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="d1313-213">Você deve estar se perguntando como Olá SDK .NET da pesquisa do Azure é instâncias tooupload capaz de uma classe definida pelo usuário como `Hotel` toohello índice.</span><span class="sxs-lookup"><span data-stu-id="d1313-213">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="d1313-214">toohelp responder essa pergunta, vamos examinar a saudação `Hotel` classe:</span><span class="sxs-lookup"><span data-stu-id="d1313-214">toohelp answer that question, let's look at hello `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
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

<span data-ttu-id="d1313-215">Olá primeiro toonotice é que cada propriedade pública de `Hotel` corresponde tooa campo na definição de índice hello, mas com uma diferença fundamental: nome de saudação de cada campo começa com uma letra minúscula ("concatenação com maiusculas"), ao nome de saudação de cada público propriedade de `Hotel` começa com uma letra maiuscula ("Pascal case").</span><span class="sxs-lookup"><span data-stu-id="d1313-215">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="d1313-216">Este é um cenário comum em aplicativos .NET que executem a associação de dados em que o esquema de destino Olá é controle Olá fora do desenvolvedor do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d1313-216">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="d1313-217">Em vez de tooviolate Olá .NET diretrizes de nomenclatura, tornando o caso de ter de nomes de propriedade, você pode informar Olá SDK toomap Olá propriedade nomes toocamel caso automaticamente com hello `[SerializePropertyNamesAsCamelCase]` atributo.</span><span class="sxs-lookup"><span data-stu-id="d1313-217">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="d1313-218">Olá SDK .NET da pesquisa do Azure usa Olá [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize de biblioteca e desserializar o tooand de objetos de modelo personalizado do JSON.</span><span class="sxs-lookup"><span data-stu-id="d1313-218">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="d1313-219">Se necessário, você pode personalizar essa serialização.</span><span class="sxs-lookup"><span data-stu-id="d1313-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="d1313-220">Para obter mais detalhes, consulte [Serialização personalizada com JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="d1313-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="d1313-221">Olá toonotice do segundo item são Olá atributos como `IsFilterable`, `IsSearchable`, `Key`, e `Analyzer` que decorar cada propriedade pública.</span><span class="sxs-lookup"><span data-stu-id="d1313-221">hello second thing toonotice are hello attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="d1313-222">Esses atributos são mapeados diretamente toohello [atributos correspondentes do índice de pesquisa do Azure Olá](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="d1313-222">These attributes map directly toohello [corresponding attributes of hello Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="d1313-223">Olá `FieldBuilder` classe usa essas definições de campo tooconstruct para índice hello.</span><span class="sxs-lookup"><span data-stu-id="d1313-223">hello `FieldBuilder` class uses these tooconstruct field definitions for hello index.</span></span>

<span data-ttu-id="d1313-224">Olá terceiro importante sobre Olá `Hotel` classe são tipos de dados de saudação de propriedades públicas de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1313-224">hello third important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="d1313-225">tipos de .NET Olá dessas propriedades mapeiam tipos de campo equivalente de tootheir na definição de índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1313-225">hello .NET types of  these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="d1313-226">Por exemplo, Olá `Category` mapas de propriedade de cadeia de caracteres toohello `category` campo, que é do tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="d1313-226">For example, hello `Category` string property maps toohello `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="d1313-227">Não há mapeamentos de tipo semelhante entre `bool?` e `Edm.Boolean`, `DateTimeOffset?` e `Edm.DateTimeOffset`, as regras específicas de saudação etc. para mapeamento de tipo hello documentadas com hello `Documents.Get` método hello [SDK .NET da pesquisa do Azure referência](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="d1313-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="d1313-228">Olá `FieldBuilder` classe cuida desse mapeamento para você, mas ainda pode ser útil toounderstand caso você precise tootroubleshoot quaisquer problemas de serialização.</span><span class="sxs-lookup"><span data-stu-id="d1313-228">hello `FieldBuilder` class takes care of this mapping for you, but it can still be helpful toounderstand in case you need tootroubleshoot any serialization issues.</span></span>

<span data-ttu-id="d1313-229">Essa capacidade toouse suas próprias classes como documentos funciona em ambas as direções; Você também pode recuperar os resultados da pesquisa e ter Olá SDK automaticamente desserializá-los tooa tipo de sua escolha, como veremos na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="d1313-229">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as we will see in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="d1313-230">Olá SDK .NET da pesquisa do Azure também oferece suporte a documentos digitadas dinamicamente usando Olá `Document` classe, que é um mapeamento de chave/valor nomes toofield de valores de campo.</span><span class="sxs-lookup"><span data-stu-id="d1313-230">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="d1313-231">Isso é útil em cenários onde você não souber o esquema de índice Olá em tempo de design, ou onde seria classes de modelo de toospecific toobind inconveniente.</span><span class="sxs-lookup"><span data-stu-id="d1313-231">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="d1313-232">Todos os métodos Olá Olá SDK que lidam com documentos têm sobrecargas que funcionam com hello `Document` classe, bem como sobrecargas fortemente tipados que usam um parâmetro de tipo genérico.</span><span class="sxs-lookup"><span data-stu-id="d1313-232">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="d1313-233">Olá somente última são usados no código de exemplo hello neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="d1313-233">Only hello latter are used in hello sample code in this tutorial.</span></span> <span data-ttu-id="d1313-234">Olá `Document` classe herda de `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="d1313-234">hello `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="d1313-235">Encontre outros detalhes [aqui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="d1313-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="d1313-236">**Por que você deve usar tipos de dados anuláveis**</span><span class="sxs-lookup"><span data-stu-id="d1313-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="d1313-237">Durante a criação de índice de pesquisa do Azure seu próprio modelo classes toomap tooan, é recomendável declarando propriedades de tipos de valor como `bool` e `int` toobe anulável (por exemplo, `bool?` em vez de `bool`).</span><span class="sxs-lookup"><span data-stu-id="d1313-237">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="d1313-238">Se você usar uma propriedade não anulável, você tem muito**garante** sem documentos no índice contêm um valor nulo para o campo correspondente do hello.</span><span class="sxs-lookup"><span data-stu-id="d1313-238">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="d1313-239">Olá SDK, nem Olá serviço Azure Search ajudará você tooenforce isso.</span><span class="sxs-lookup"><span data-stu-id="d1313-239">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="d1313-240">Isso não é apenas uma preocupação hipotética: Imagine um cenário em que você adicionar um novo campo tooan índice existente que é do tipo `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="d1313-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="d1313-241">Depois de atualizar a definição de índice hello, todos os documentos terá um valor nulo para esse novo campo (desde que todos os tipos são anuláveis na pesquisa do Azure).</span><span class="sxs-lookup"><span data-stu-id="d1313-241">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="d1313-242">Se você usar uma classe de modelo com um não anulável `int` propriedade para esse campo, você receberá um `JsonSerializationException` assim ao tentar tooretrieve documentos:</span><span class="sxs-lookup"><span data-stu-id="d1313-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="d1313-243">Por esse motivo, sugerimos que você use tipos anuláveis nas suas classes de modelo como uma prática recomendada.</span><span class="sxs-lookup"><span data-stu-id="d1313-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="d1313-244">Serialização personalizada com JSON.NET</span><span class="sxs-lookup"><span data-stu-id="d1313-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="d1313-245">Olá SDK utiliza JSON.NET para serialização e desserialização de documentos.</span><span class="sxs-lookup"><span data-stu-id="d1313-245">hello SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="d1313-246">Você pode personalizar a serialização e desserialização se necessário, definindo suas próprias `JsonConverter` ou `IContractResolver` (consulte Olá [JSON.NET documentação](http://www.newtonsoft.com/json/help/html/Introduction.htm) para obter mais detalhes).</span><span class="sxs-lookup"><span data-stu-id="d1313-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see hello [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="d1313-247">Isso pode ser útil quando você quiser tooadapt uma classe de modelo existente do seu aplicativo para uso com a pesquisa do Azure e outros cenários mais avançados.</span><span class="sxs-lookup"><span data-stu-id="d1313-247">This can be useful when you want tooadapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="d1313-248">Por exemplo, com a serialização personalizada, você pode:</span><span class="sxs-lookup"><span data-stu-id="d1313-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="d1313-249">Incluir ou excluir determinadas propriedades da sua classe de modelo para serem armazenadas como campos de documento.</span><span class="sxs-lookup"><span data-stu-id="d1313-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="d1313-250">Mapear os nomes de propriedade no código aos nomes de campo no índice.</span><span class="sxs-lookup"><span data-stu-id="d1313-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="d1313-251">Crie atributos personalizados que podem ser usados para mapear os campos de toodocument propriedades.</span><span class="sxs-lookup"><span data-stu-id="d1313-251">Create custom attributes that can be used for mapping properties toodocument fields.</span></span>

<span data-ttu-id="d1313-252">Você pode encontrar exemplos de implementação de serialização personalizada em testes de unidade Olá para Olá SDK .NET da pesquisa do Azure no GitHub.</span><span class="sxs-lookup"><span data-stu-id="d1313-252">You can find examples of implementing custom serialization in hello unit tests for hello Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="d1313-253">Um bom ponto de partida é [esta pasta](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span><span class="sxs-lookup"><span data-stu-id="d1313-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="d1313-254">Contém classes que são usadas pelos testes de serialização personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="d1313-254">It contains classes that are used by hello custom serialization tests.</span></span>

### <a name="searching-for-documents-in-hello-index"></a><span data-ttu-id="d1313-255">Procurando documentos no índice Olá</span><span class="sxs-lookup"><span data-stu-id="d1313-255">Searching for documents in hello index</span></span>
<span data-ttu-id="d1313-256">Olá última etapa no aplicativo de exemplo hello é toosearch para alguns documentos no índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1313-256">hello last step in hello sample application is toosearch for some documents in hello index.</span></span> <span data-ttu-id="d1313-257">Olá método a seguir faz isso:</span><span class="sxs-lookup"><span data-stu-id="d1313-257">hello following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
    Console.WriteLine("and return hello hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take hello top two results, and show only hotelName and ");
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

    Console.WriteLine("Search hello entire index for hello term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="d1313-258">Cada vez que ele executa uma consulta, esse método cria, primeiro, um novo objeto `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="d1313-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="d1313-259">Isso é opções adicionais de toospecify usado para consulta hello como classificação, filtragem, paginação e facetas.</span><span class="sxs-lookup"><span data-stu-id="d1313-259">This is used toospecify additional options for hello query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="d1313-260">Nesse método, estamos configurando Olá `Filter`, `Select`, `OrderBy`, e `Top` propriedade para consultas diferentes.</span><span class="sxs-lookup"><span data-stu-id="d1313-260">In this method, we're setting hello `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="d1313-261">Saudação de todos os `SearchParameters` propriedades são documentadas [aqui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="d1313-261">All hello `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="d1313-262">Olá próxima etapa é tooactually executar a consulta de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1313-262">hello next step is tooactually execute hello search query.</span></span> <span data-ttu-id="d1313-263">Isso é feito usando Olá `Documents.Search` método.</span><span class="sxs-lookup"><span data-stu-id="d1313-263">This is done using hello `Documents.Search` method.</span></span> <span data-ttu-id="d1313-264">Para cada consulta, passamos Olá toouse de texto de pesquisa como uma cadeia de caracteres (ou `"*"` se não houver nenhum texto de pesquisa), além de saudação pesquisar parâmetros criados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d1313-264">For each query, we pass hello search text toouse as a string (or `"*"` if there is no search text), plus hello search parameters created earlier.</span></span> <span data-ttu-id="d1313-265">Especificar `Hotel` como parâmetro de tipo Olá para `Documents.Search`, que informa documentos de toodeserialize SDK Olá nos resultados da pesquisa Olá em objetos do tipo `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="d1313-265">We also specify `Hotel` as hello type parameter for `Documents.Search`, which tells hello SDK toodeserialize documents in hello search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="d1313-266">Você pode encontrar mais informações sobre sintaxe de expressão de consulta de pesquisa Olá [aqui](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="d1313-266">You can find more information about hello search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="d1313-267">Finalmente, depois de cada consulta este método itera todas as correspondências de saudação nos resultados da pesquisa hello, imprimindo cada console toohello de documento:</span><span class="sxs-lookup"><span data-stu-id="d1313-267">Finally, after each query this method iterates through all hello matches in hello search results, printing each document toohello console:</span></span>

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

<span data-ttu-id="d1313-268">Por sua vez, vamos examinar mais detalhadamente cada uma das consultas de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1313-268">Let's take a closer look at each of hello queries in turn.</span></span> <span data-ttu-id="d1313-269">Aqui está a saudação código tooexecute Olá primeira consulta:</span><span class="sxs-lookup"><span data-stu-id="d1313-269">Here is hello code tooexecute hello first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="d1313-270">Nesse caso, estamos pesquisando hotéis que coincidir palavra hello "budget", e queremos tooget volta apenas Olá hotel nomes, conforme especificado pelas Olá `Select` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d1313-270">In this case, we're searching for hotels that match hello word "budget", and we want tooget back only hello hotel names, as specified by hello `Select` parameter.</span></span> <span data-ttu-id="d1313-271">Estes são os resultados de saudação:</span><span class="sxs-lookup"><span data-stu-id="d1313-271">Here are hello results:</span></span>

    Name: Roach Motel

<span data-ttu-id="d1313-272">Em seguida, podemos deseja hotéis de saudação toofind com uma taxa noturna de menor que US $150 e retornar somente Olá hotel ID e a descrição:</span><span class="sxs-lookup"><span data-stu-id="d1313-272">Next, we want toofind hello hotels with a nightly rate of less than $150, and return only hello hotel ID and description:</span></span>

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

<span data-ttu-id="d1313-273">Essa consulta usa um OData `$filter` expressão, `baseRate lt 150`, documentos de saudação toofilter no índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1313-273">This query uses an OData `$filter` expression, `baseRate lt 150`, toofilter hello documents in hello index.</span></span> <span data-ttu-id="d1313-274">Você pode encontrar mais informações sobre Olá sintaxe do OData que oferece suporte à pesquisa do Azure [aqui](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="d1313-274">You can find out more about hello OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="d1313-275">Estes são os resultados de saudação da consulta hello:</span><span class="sxs-lookup"><span data-stu-id="d1313-275">Here are hello results of hello query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

<span data-ttu-id="d1313-276">Em seguida, queremos toofind Olá superior dois hotéis foram renovados mais recentemente e mostram o nome do hotel hello e a última data de renovação.</span><span class="sxs-lookup"><span data-stu-id="d1313-276">Next, we want toofind hello top two hotels that have been most recently renovated, and show hello hotel name and last renovation date.</span></span> <span data-ttu-id="d1313-277">Aqui está o código de saudação:</span><span class="sxs-lookup"><span data-stu-id="d1313-277">Here is hello code:</span></span> 

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

<span data-ttu-id="d1313-278">Nesse caso, usamos novamente saudação do OData sintaxe toospecify `OrderBy` parâmetro como `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="d1313-278">In this case, we again use OData syntax toospecify hello `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="d1313-279">Podemos também definir `Top` too2 tooensure somente obtemos documentos de duas primeiras hello.</span><span class="sxs-lookup"><span data-stu-id="d1313-279">We also set `Top` too2 tooensure we only get hello top two documents.</span></span> <span data-ttu-id="d1313-280">Como antes, definimos `Select` toospecify quais campos devem ser retornados.</span><span class="sxs-lookup"><span data-stu-id="d1313-280">As before, we set `Select` toospecify which fields should be returned.</span></span>

<span data-ttu-id="d1313-281">Estes são os resultados de saudação:</span><span class="sxs-lookup"><span data-stu-id="d1313-281">Here are hello results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="d1313-282">Por fim, queremos toofind todos os hotéis que coincidir palavra hello "motel":</span><span class="sxs-lookup"><span data-stu-id="d1313-282">Finally, we want toofind all hotels that match hello word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="d1313-283">Aqui estão os resultados de hello, que incluem todos os campos porque não especificamos Olá `Select` propriedade:</span><span class="sxs-lookup"><span data-stu-id="d1313-283">And here are hello results, which include all fields since we did not specify hello `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="d1313-284">Essa etapa conclui o tutorial hello, mas não interrompe aqui.</span><span class="sxs-lookup"><span data-stu-id="d1313-284">This step completes hello tutorial, but don't stop here.</span></span> <span data-ttu-id="d1313-285">**Próximas etapas** fornece os recursos adicionais para aprender mais sobre a Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1313-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1313-286">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1313-286">Next steps</span></span>
* <span data-ttu-id="d1313-287">Procurar referências Olá Olá [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) e [API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="d1313-287">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="d1313-288">Aprofunde seus conhecimentos por meio de [vídeos e outros exemplos e tutoriais](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="d1313-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="d1313-289">Revisão [convenções de nomenclatura](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn regras de saudação de nomeação de vários objetos.</span><span class="sxs-lookup"><span data-stu-id="d1313-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello rules for naming various objects.</span></span>
* <span data-ttu-id="d1313-290">Examine os [tipos de dados com suporte](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) na Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1313-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
