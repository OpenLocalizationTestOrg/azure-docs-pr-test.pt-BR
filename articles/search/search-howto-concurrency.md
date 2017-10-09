---
title: "aaaHow toomanage simultâneo grava tooresources na pesquisa do Azure"
description: "Use colisões de ar intermediário de tooavoid de simultaneidade otimista em índices de pesquisa tooAzure atualizações ou exclusões, indexadores e fontes de dados."
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
ms.openlocfilehash: c061d2b5c4d2dbd0fd5633405b01ab2912fbc754
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-concurrency-in-azure-search"></a><span data-ttu-id="e3131-103">Como a simultaneidade toomanage na pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="e3131-103">How toomanage concurrency in Azure Search</span></span>

<span data-ttu-id="e3131-104">Ao gerenciar recursos de pesquisa do Azure, como índices e fontes de dados, é importante tooupdate recursos com segurança, especialmente se os recursos são acessados simultaneamente por diferentes componentes do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3131-104">When managing Azure Search resources such as indexes and data sources, it's important tooupdate resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="e3131-105">Quando dois clientes atualizam simultaneamente um recurso sem coordenação, condições de corrida são possíveis.</span><span class="sxs-lookup"><span data-stu-id="e3131-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="e3131-106">tooprevent isso, oferece uma pesquisa do Azure uma *modelo de simultaneidade otimista*.</span><span class="sxs-lookup"><span data-stu-id="e3131-106">tooprevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="e3131-107">Não há nenhum bloqueio em um recurso.</span><span class="sxs-lookup"><span data-stu-id="e3131-107">There are no locks on a resource.</span></span> <span data-ttu-id="e3131-108">Em vez disso, há uma ETag para todos os recursos que identifica a versão do recurso Olá para que você pode criar solicitações evitar acidental substitui.</span><span class="sxs-lookup"><span data-stu-id="e3131-108">Instead, there is an ETag for every resource that identifies hello resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="e3131-109">Código conceitual em uma [solução C# de exemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explica como funciona o controle de simultaneidade no Azure Search.</span><span class="sxs-lookup"><span data-stu-id="e3131-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="e3131-110">código de saudação cria condições que invocar o controle de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="e3131-110">hello code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="e3131-111">Saudação de leitura [fragmento de código a seguir](#samplecode) provavelmente será suficiente para a maioria dos desenvolvedores, mas se você quiser toorun, editar o nome do serviço de saudação appSettings. JSON tooadd e uma chave de api de administração.</span><span class="sxs-lookup"><span data-stu-id="e3131-111">Reading hello [code fragment below](#samplecode) is probably sufficient for most developers, but if you want toorun it, edit appsettings.json tooadd hello service name and an admin api-key.</span></span> <span data-ttu-id="e3131-112">Dado um URL de serviço de `http://myservice.search.windows.net`, nome do serviço Olá é `myservice`.</span><span class="sxs-lookup"><span data-stu-id="e3131-112">Given a service URL of `http://myservice.search.windows.net`, hello service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="e3131-113">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="e3131-113">How it works</span></span>

<span data-ttu-id="e3131-114">Otimista de simultaneidade é implementada por meio do acesso condição verifica nas chamadas à API escrever tooindexes, indexadores, fontes de dados e recursos de synonymMap.</span><span class="sxs-lookup"><span data-stu-id="e3131-114">Optimistic concurrency is implemented through access condition checks in API calls writing tooindexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="e3131-115">Todos os recursos tiverem uma [ *marca da entidade (ETag)* ](https://en.wikipedia.org/wiki/HTTP_ETag) que fornece informações de versão do objeto.</span><span class="sxs-lookup"><span data-stu-id="e3131-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="e3131-116">Verificando Olá ETag pela primeira vez, você pode evitar atualizações simultâneas em um fluxo de trabalho típico (get, modificar localmente e atualizar), garantindo correspondências de ETag do recurso Olá sua cópia local.</span><span class="sxs-lookup"><span data-stu-id="e3131-116">By checking hello ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring hello resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="e3131-117">Olá REST API usa uma [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) no cabeçalho da solicitação hello.</span><span class="sxs-lookup"><span data-stu-id="e3131-117">hello REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello request header.</span></span>
+ <span data-ttu-id="e3131-118">Olá SDK .NET define Olá ETag por meio de um objeto accessCondition, definindo Olá [If-Match | Cabeçalho If-Match-nenhum](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) no recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3131-118">hello .NET SDK sets hello ETag through an accessCondition object, setting hello [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello resource.</span></span> <span data-ttu-id="e3131-119">Qualquer objeto que herda de [IResourceWithETag (SDK do .NET)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) possui um objeto accessCondition.</span><span class="sxs-lookup"><span data-stu-id="e3131-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="e3131-120">Sempre que você atualizar um recurso, a ETag é alterada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e3131-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="e3131-121">Quando você implementa o gerenciamento de simultaneidade, tudo o que você está fazendo é colocar uma pré-condição na solicitação de atualização de saudação que requer o recurso remoto Olá toohave Olá ETag mesmo como cópia de saudação do recurso Olá modificado no cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3131-121">When you implement concurrency management, all you're doing is putting a precondition on hello update request that requires hello remote resource toohave hello same ETag as hello copy of hello resource that you modified on hello client.</span></span> <span data-ttu-id="e3131-122">Se um processo simultâneo foi alterado recurso remoto Olá já, Olá ETag não corresponderá a pré-condição hello e Olá solicitação falha com HTTP 412.</span><span class="sxs-lookup"><span data-stu-id="e3131-122">If a concurrent process has changed hello remote resource already, hello ETag will not match hello precondition and hello request will fail with HTTP 412.</span></span> <span data-ttu-id="e3131-123">Se você estiver usando o SDK .NET de hello, isso se manifesta como uma `CloudException` onde Olá `IsAccessConditionFailed()` método de extensão retorna true.</span><span class="sxs-lookup"><span data-stu-id="e3131-123">If you're using hello .NET SDK, this manifests as a `CloudException` where hello `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="e3131-124">Há apenas um mecanismo para simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="e3131-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="e3131-125">Ele sempre é usado, independentemente de qual API é usada para atualizações de recursos.</span><span class="sxs-lookup"><span data-stu-id="e3131-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="e3131-126">Casos de uso e código de exemplo</span><span class="sxs-lookup"><span data-stu-id="e3131-126">Use cases and sample code</span></span>

<span data-ttu-id="e3131-127">saudação de código a seguir demonstra accessCondition verifica para operações de atualização da chave:</span><span class="sxs-lookup"><span data-stu-id="e3131-127">hello following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="e3131-128">Falha de uma atualização se Olá recurso não existe mais</span><span class="sxs-lookup"><span data-stu-id="e3131-128">Fail an update if hello resource no longer exists</span></span>
+ <span data-ttu-id="e3131-129">Falha de uma atualização se altera de versão do recurso de saudação</span><span class="sxs-lookup"><span data-stu-id="e3131-129">Fail an update if hello resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="e3131-130">Código de exemplo do [programa DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="e3131-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

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
            // of hello resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once hello resource exists in Azure Search, its ETag will be populated. Make sure toouse hello object
            // returned by hello SearchServiceClient! Otherwise, you will still have hello old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that hello update will only
            // succeed if hello index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates toohello same resource. If another
            // client tries tooupdate hello resource, it will fail as long as all clients are using hello right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. toostart, both clients see hello same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates hello index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries tooupdate hello index, but fails, thanks toohello ETag check.
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
                Console.WriteLine("Client 2 failed tooupdate hello index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of hello DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using hello Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // hello resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key tooend application...\n");
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

## <a name="design-pattern"></a><span data-ttu-id="e3131-131">Padrão de design</span><span class="sxs-lookup"><span data-stu-id="e3131-131">Design pattern</span></span>

<span data-ttu-id="e3131-132">Um padrão de design para implementar a simultaneidade otimista deve incluir um loop que repete a verificação de condição de acesso hello, um teste para a condição de acesso Olá e, opcionalmente, recupera um recurso atualizado antes de tentar toore-aplicar alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3131-132">A design pattern for implementing optimistic concurrency should include a loop that retries hello access condition check, a test for hello access condition, and optionally retrieves an updated resource before attempting toore-apply hello changes.</span></span> 

<span data-ttu-id="e3131-133">Este trecho de código ilustra a adição de saudação de um índice de tooan synonymMap que já existe.</span><span class="sxs-lookup"><span data-stu-id="e3131-133">This code snippet illustrates hello addition of a synonymMap tooan index that already exists.</span></span> <span data-ttu-id="e3131-134">Esse código é do hello [tutorial c# sinônimo (visualização) para pesquisa do Azure](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="e3131-134">This code is from hello [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="e3131-135">trecho de saudação obtém hotéis"hello" índice, verifica a versão do objeto Olá em uma operação de atualização, lança uma exceção se a condição Olá falhar e, em seguida, repetições Olá operação (backup toothree vezes), iniciando com a recuperação de índice de saudação do hello servidor tooget mais recente Versão.</span><span class="sxs-lookup"><span data-stu-id="e3131-135">hello snippet gets hello "hotels" index, checks hello object version on an update operation, throws an exception if hello condition fails, and then retries hello operation (up toothree times), starting with index retrieval from hello server tooget hello latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // hello IfNotChanged condition ensures that hello index is updated only if hello ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated hello index successfully.\n");
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


## <a name="next-steps"></a><span data-ttu-id="e3131-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3131-136">Next steps</span></span>

<span data-ttu-id="e3131-137">Saudação de revisão [exemplo sinônimos c#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) para obter mais contexto sobre como atualizar um índice existente, toosafely.</span><span class="sxs-lookup"><span data-stu-id="e3131-137">Review hello [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how toosafely update an existing index.</span></span>

<span data-ttu-id="e3131-138">Tente modificar qualquer uma das seguintes Olá exemplos tooinclude ETags ou AccessCondition objetos.</span><span class="sxs-lookup"><span data-stu-id="e3131-138">Try modifying either of hello following samples tooinclude ETags or AccessCondition objects.</span></span>

+ [<span data-ttu-id="e3131-139">exemplo de REST API no GitHub</span><span class="sxs-lookup"><span data-stu-id="e3131-139">REST API sample on Github</span></span>](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ <span data-ttu-id="e3131-140">[exemplo do SDK do .NET no GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="e3131-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="e3131-141">Essa solução inclui o projeto de "DotNetEtagsExplainer" hello contendo código Olá apresentado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="e3131-141">This solution includes hello "DotNetEtagsExplainer" project containing hello code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="e3131-142">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e3131-142">See also</span></span>

  <span data-ttu-id="e3131-143">[Cabeçalhos de resposta e solicitação HTTP comuns](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span><span class="sxs-lookup"><span data-stu-id="e3131-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="e3131-144">[Códigos de status HTTP](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [operações de índice (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span><span class="sxs-lookup"><span data-stu-id="e3131-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>