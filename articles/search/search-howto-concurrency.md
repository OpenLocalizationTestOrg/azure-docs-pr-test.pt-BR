---
title: "Como gerenciar gravações simultâneas aos recursos no Azure Search"
description: "Use a simultaneidade otimista para evitar colisões de ar intermediário em atualizações ou exclusões para os índices do Azure Search, indexadores e fontes de dados."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: 
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: heidist
ms.openlocfilehash: aee1b7376d4829e3e2f5a232525e3c3cb4df9d8e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-manage-concurrency-in-azure-search"></a><span data-ttu-id="ef7fb-103">Como gerenciar a simultaneidade no Azure Search</span><span class="sxs-lookup"><span data-stu-id="ef7fb-103">How to manage concurrency in Azure Search</span></span>

<span data-ttu-id="ef7fb-104">Ao gerenciar recursos do Azure Search, como índices e fontes de dados, é importante atualizar recursos com segurança, especialmente se os recursos são acessados simultaneamente por diferentes componentes do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-104">When managing Azure Search resources such as indexes and data sources, it's important to update resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="ef7fb-105">Quando dois clientes atualizam simultaneamente um recurso sem coordenação, condições de corrida são possíveis.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="ef7fb-106">Para evitar isso, o Azure Search oferece uma *modelo de simultaneidade otimista*.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-106">To prevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="ef7fb-107">Não há nenhum bloqueio em um recurso.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-107">There are no locks on a resource.</span></span> <span data-ttu-id="ef7fb-108">Em vez disso, há uma ETag para todos os recursos que identifica a versão do recurso para que você possa criar solicitações que evitam substituições acidentais.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-108">Instead, there is an ETag for every resource that identifies the resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="ef7fb-109">Código conceitual em uma [solução C# de exemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explica como funciona o controle de simultaneidade no Azure Search.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="ef7fb-110">O código cria condições que invocam o controle de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-110">The code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="ef7fb-111">Ler o [fragmento de código a seguir](#samplecode) é provavelmente suficiente para a maioria dos desenvolvedores, mas se você deseja executar, edite appsettings.json para adicionar o nome do serviço e uma chave de api de administração.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-111">Reading the [code fragment below](#samplecode) is probably sufficient for most developers, but if you want to run it, edit appsettings.json to add the service name and an admin api-key.</span></span> <span data-ttu-id="ef7fb-112">Dado um URL de serviço de `http://myservice.search.windows.net`, o nome do serviço é `myservice`.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-112">Given a service URL of `http://myservice.search.windows.net`, the service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="ef7fb-113">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="ef7fb-113">How it works</span></span>

<span data-ttu-id="ef7fb-114">A simultaneidade otimista é implementada por meio de verificações de condição de acesso nas chamadas à API gravando índices, indexadores, fontes de dados e recursos synonymMap.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-114">Optimistic concurrency is implemented through access condition checks in API calls writing to indexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="ef7fb-115">Todos os recursos tiverem uma [ *marca da entidade (ETag)* ](https://en.wikipedia.org/wiki/HTTP_ETag) que fornece informações de versão do objeto.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="ef7fb-116">Verificando o ETag pela primeira vez, você pode evitar atualizações simultâneas em um fluxo de trabalho típico (obter, modificar localmente e atualizar), garantindo que a ETag do recurso coincida com sua cópia local.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-116">By checking the ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring the resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="ef7fb-117">A API REST usa um [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) no cabeçalho da solicitação.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-117">The REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on the request header.</span></span>
+ <span data-ttu-id="ef7fb-118">O SDK .NET define o ETag por meio de um objeto accessCondition, definindo o [Cabeçalho If-Match | If-Match-None](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) no recurso.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-118">The .NET SDK sets the ETag through an accessCondition object, setting the [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on the resource.</span></span> <span data-ttu-id="ef7fb-119">Qualquer objeto que herda de [IResourceWithETag (SDK do .NET)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) possui um objeto accessCondition.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="ef7fb-120">Sempre que você atualizar um recurso, a ETag é alterada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="ef7fb-121">Quando você implementa o gerenciamento de simultaneidade, tudo o que você está fazendo é colocar uma pré-condição na solicitação de atualização que exige o recurso remoto com o mesmo ETag como a cópia do recurso que você modificou no cliente.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-121">When you implement concurrency management, all you're doing is putting a precondition on the update request that requires the remote resource to have the same ETag as the copy of the resource that you modified on the client.</span></span> <span data-ttu-id="ef7fb-122">Se um processo simultâneo já alterou o recurso remoto, a ETag não corresponderá com a pré-condição e a solicitação falhará com HTTP 412.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-122">If a concurrent process has changed the remote resource already, the ETag will not match the precondition and the request will fail with HTTP 412.</span></span> <span data-ttu-id="ef7fb-123">Se você estiver usando o SDK do .NET, isso se manifesta como uma `CloudException` onde o método de extensão `IsAccessConditionFailed()` retorna true.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-123">If you're using the .NET SDK, this manifests as a `CloudException` where the `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="ef7fb-124">Há apenas um mecanismo para simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="ef7fb-125">Ele sempre é usado, independentemente de qual API é usada para atualizações de recursos.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="ef7fb-126">Casos de uso e código de exemplo</span><span class="sxs-lookup"><span data-stu-id="ef7fb-126">Use cases and sample code</span></span>

<span data-ttu-id="ef7fb-127">O código a seguir demonstra verificações accessCondition para operações de atualização da chave:</span><span class="sxs-lookup"><span data-stu-id="ef7fb-127">The following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="ef7fb-128">Falha de uma atualização se o recurso não existe mais</span><span class="sxs-lookup"><span data-stu-id="ef7fb-128">Fail an update if the resource no longer exists</span></span>
+ <span data-ttu-id="ef7fb-129">Falha de uma atualização se a versão do recurso muda</span><span class="sxs-lookup"><span data-stu-id="ef7fb-129">Fail an update if the resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="ef7fb-130">Código de exemplo do [programa DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="ef7fb-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

```
    class Program
    {
        // This sample shows how ETags work by performing conditional updates and deletes
        // on an Azure Search index.
        static void Main(string[] args)
        {
            IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
            IConfigurationRoot configuration = builder.Build();

            SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

            Console.WriteLine("Deleting index...\n");
            DeleteTestIndexIfExists(serviceClient);

            // Every top-level resource in Azure Search has an associated ETag that keeps track of which version
            // of the resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once the resource exists in Azure Search, its ETag will be populated. Make sure to use the object
            // returned by the SearchServiceClient! Otherwise, you will still have the old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that the update will only
            // succeed if the index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates to the same resource. If another
            // client tries to update the resource, it will fail as long as all clients are using the right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. To start, both clients see the same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates the index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries to update the index, but fails, thanks to the ETag check.
            try
            {
                indexForClient2.Fields.Add(new Field("b", DataType.Boolean));
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient2, 
                    accessCondition: AccessCondition.IfNotChanged(indexForClient2));

                Console.WriteLine("Whoops; This shouldn't happen");
                Environment.Exit(1);
            }
            catch (CloudException e) when (e.IsAccessConditionFailed())
            {
                Console.WriteLine("Client 2 failed to update the index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of the DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using the Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // the resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key to end application...\n");
            Console.ReadKey();
        }

        private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
        {
            string searchServiceName = configuration["SearchServiceName"];
            string adminApiKey = configuration["SearchServiceAdminApiKey"];

            SearchServiceClient serviceClient =
                new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
            return serviceClient;
        }

        private static void DeleteTestIndexIfExists(SearchServiceClient serviceClient)
        {
            if (serviceClient.Indexes.Exists("test"))
            {
                serviceClient.Indexes.Delete("test");
            }
        }

        private static Index DefineTestIndex() =>
            new Index()
            {
                Name = "test",
                Fields = new[] { new Field("id", DataType.String) { IsKey = true } }
            };
    }
}
```

## <a name="design-pattern"></a><span data-ttu-id="ef7fb-131">Padrão de design</span><span class="sxs-lookup"><span data-stu-id="ef7fb-131">Design pattern</span></span>

<span data-ttu-id="ef7fb-132">Um padrão de design para implementar simultaneidade otimista deve incluir um loop que repete a verificação da condição de acesso, um teste para a condição de acesso e, opcionalmente, recupera um recurso atualizado antes de tentar aplicar novamente as alterações.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-132">A design pattern for implementing optimistic concurrency should include a loop that retries the access condition check, a test for the access condition, and optionally retrieves an updated resource before attempting to re-apply the changes.</span></span> 

<span data-ttu-id="ef7fb-133">Este trecho de código mostra a adição de um synonymMap para um índice que já existe.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-133">This code snippet illustrates the addition of a synonymMap to an index that already exists.</span></span> <span data-ttu-id="ef7fb-134">Este código é do [Tutorial C# de sinônimos (visualização) do Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="ef7fb-134">This code is from the [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="ef7fb-135">O trecho de código obtém o índice "hotéis", verifica a versão do objeto em uma operação de atualização, gera uma exceção se a condição falha e, em seguida, repete a operação (até três vezes), iniciando com a recuperação de índice do servidor para obter a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-135">The snippet gets the "hotels" index, checks the object version on an update operation, throws an exception if the condition fails, and then retries the operation (up to three times), starting with index retrieval from the server to get the latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // The IfNotChanged condition ensures that the index is updated only if the ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated the index successfully.\n");
                    break;
                }
                catch (CloudException e) when (e.IsAccessConditionFailed())
                {
                    Console.WriteLine($"Index update failed : {e.Message}. Attempt({i}/{MaxNumTries}).\n");
                }
            }
        }
        
        private static Index AddSynonymMapsToFields(Index index)
        {
            index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
            index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };
            return index;
        }


## <a name="next-steps"></a><span data-ttu-id="ef7fb-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ef7fb-136">Next steps</span></span>

<span data-ttu-id="ef7fb-137">Examine o [exemplo sinônimos c#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) para obter mais contexto sobre como atualizar um índice existente, com segurança.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-137">Review the [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how to safely update an existing index.</span></span>

<span data-ttu-id="ef7fb-138">Tente modificar qualquer um dos exemplos a seguir para incluir objetos ETags ou AccessCondition.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-138">Try modifying either of the following samples to include ETags or AccessCondition objects.</span></span>

+ [<span data-ttu-id="ef7fb-139">exemplo de REST API no GitHub</span><span class="sxs-lookup"><span data-stu-id="ef7fb-139">REST API sample on Github</span></span>](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ <span data-ttu-id="ef7fb-140">[exemplo do SDK do .NET no GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ef7fb-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="ef7fb-141">Essa solução inclui o projeto "DotNetEtagsExplainer" que contém o código apresentado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ef7fb-141">This solution includes the "DotNetEtagsExplainer" project containing the code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="ef7fb-142">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ef7fb-142">See also</span></span>

  <span data-ttu-id="ef7fb-143">[Cabeçalhos de resposta e solicitação HTTP comuns](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span><span class="sxs-lookup"><span data-stu-id="ef7fb-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="ef7fb-144">[Códigos de status HTTP](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [operações de índice (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span><span class="sxs-lookup"><span data-stu-id="ef7fb-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>