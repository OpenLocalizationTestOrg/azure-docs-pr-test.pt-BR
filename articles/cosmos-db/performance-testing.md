---
title: aaaAzure Cosmos DB escala e o teste de desempenho | Microsoft Docs
description: Saiba como tooperform dimensionar e teste de desempenho com o banco de dados do Azure Cosmos
keywords: testes de desempenho
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="97f64-104">Teste de desempenho e escala com o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="97f64-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="97f64-105">O teste de desempenho e escalabilidade é uma etapa importante no desenvolvimento de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="97f64-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="97f64-106">Para muitos aplicativos, a camada de banco de dados de saudação tem um impacto significativo hello desempenho e escalabilidade, e é, portanto, um componente crítico de desempenho de teste.</span><span class="sxs-lookup"><span data-stu-id="97f64-106">For many applications, hello database tier has a significant impact on hello overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="97f64-107">O [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) foi desenvolvido para fins de escala elástica e desempenho previsível e, portanto, é uma excelente opção para aplicativos que precisam de uma camada de banco de dados de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="97f64-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="97f64-108">Este artigo é uma referência para desenvolvedores que implementam conjuntos de testes de desempenho para suas cargas de trabalho do Cosmos DB ou que avaliam o Cosmos DB para cenários de aplicativos de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="97f64-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="97f64-109">Ele se concentra principalmente nos testes de desempenho isolado do banco de dados hello, mas também inclui as práticas recomendadas para aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="97f64-109">It focuses primarily on isolated performance testing of hello database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="97f64-110">Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="97f64-110">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="97f64-111">Onde posso encontrar um aplicativo cliente do .NET de exemplo para testar o desempenho do Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="97f64-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="97f64-112">Como fazer para obter altos níveis de produtividade com o Azure Cosmos DB em meu aplicativo cliente?</span><span class="sxs-lookup"><span data-stu-id="97f64-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="97f64-113">tooget iniciada com o código, baixe o projeto de saudação do [exemplo de teste de desempenho do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="97f64-113">tooget started with code, please download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="97f64-114">meta de saudação do aplicativo é toodemonstrate práticas recomendadas para a extração de melhor desempenho do banco de dados do Cosmos com um pequeno número de computadores cliente.</span><span class="sxs-lookup"><span data-stu-id="97f64-114">hello goal of this application is toodemonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="97f64-115">Isso não foi feito toodemonstrate capacidade de pico de saudação do serviço de saudação, que pode ser dimensionado limitlessly.</span><span class="sxs-lookup"><span data-stu-id="97f64-115">This was not made toodemonstrate hello peak capacity of hello service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="97f64-116">Se você estiver procurando por opções de configuração do cliente tooimprove Cosmos banco de dados de desempenho, consulte [dicas de desempenho do banco de dados do Azure Cosmos](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="97f64-116">If you're looking for client-side configuration options tooimprove Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-hello-performance-testing-application"></a><span data-ttu-id="97f64-117">Execute o aplicativo de teste de desempenho de saudação</span><span class="sxs-lookup"><span data-stu-id="97f64-117">Run hello performance testing application</span></span>
<span data-ttu-id="97f64-118">Olá tooget de maneira mais rápida iniciado é toocompile e Olá execução de .NET de exemplo abaixo, conforme descrito nas etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="97f64-118">hello quickest way tooget started is toocompile and run hello .NET sample below, as described in hello steps below.</span></span> <span data-ttu-id="97f64-119">Você pode também examinar código-fonte hello e implementar aplicativos de cliente próprio de tooyour configurações semelhantes.</span><span class="sxs-lookup"><span data-stu-id="97f64-119">You can also review hello source code and implement similar configurations tooyour own client applications.</span></span>

<span data-ttu-id="97f64-120">**Etapa 1:** Download Olá Proje [exemplo de teste de desempenho do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), ou o repositório do GitHub Olá bifurcação.</span><span class="sxs-lookup"><span data-stu-id="97f64-120">**Step 1:** Download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork hello GitHub repository.</span></span>

<span data-ttu-id="97f64-121">**Etapa 2:** modificar as configurações de saudação para EndpointUrl, AuthorizationKey, CollectionThroughput e DocumentTemplate (opcional) no App. config.</span><span class="sxs-lookup"><span data-stu-id="97f64-121">**Step 2:** Modify hello settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="97f64-122">Antes de provisionar coleções com alta taxa de transferência, consulte toohello [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/) custos de saudação tooestimate por coleção.</span><span class="sxs-lookup"><span data-stu-id="97f64-122">Before provisioning collections with high throughput, please refer toohello [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello costs per collection.</span></span> <span data-ttu-id="97f64-123">Banco de dados do Azure Cosmos cobra armazenamento e a taxa de transferência de forma independente em uma base por hora, então você pode salvar os custos excluindo ou diminuir a taxa de transferência de saudação de suas coleções de banco de dados do Azure Cosmos após o teste.</span><span class="sxs-lookup"><span data-stu-id="97f64-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering hello throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="97f64-124">**Etapa 3:** compilar e executar o aplicativo de console Olá da linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="97f64-124">**Step 3:** Compile and run hello console app from hello command line.</span></span> <span data-ttu-id="97f64-125">Você deve ver a saída como Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="97f64-125">You should see output like hello following:</span></span>

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


<span data-ttu-id="97f64-126">**Etapa 4 (se necessário):** Olá taxa de transferência relatada (RU/s) da ferramenta Olá deve ser Olá mesmo ou maior que a taxa de transferência fornecida da coleção Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="97f64-126">**Step 4 (if necessary):** hello throughput reported (RU/s) from hello tool should be hello same or higher than hello provisioned throughput of hello collection.</span></span> <span data-ttu-id="97f64-127">Caso contrário, aumentando Olá DegreeOfParallelism em pequenos incrementos pode ajudá-lo a atingir o limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="97f64-127">If not, increasing hello DegreeOfParallelism in small increments may help you reach hello limit.</span></span> <span data-ttu-id="97f64-128">Se plateaus a taxa de transferência de saudação do seu aplicativo cliente, iniciar várias instâncias do aplicativo hello em Olá mesmo ou computadores diferentes, ajudará você a atingir o limite de saudação provisionada em Olá instâncias diferentes.</span><span class="sxs-lookup"><span data-stu-id="97f64-128">If hello throughput from your client app plateaus, launching multiple instances of hello app on hello same or different machines will help you reach hello provisioned limit across hello different instances.</span></span> <span data-ttu-id="97f64-129">Se você precisar de ajuda com essa etapa, escreva um email tooaskcosmosdb@microsoft.com ou emitir um ticket de suporte de saudação [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="97f64-129">If you need help with this step, please, write an email tooaskcosmosdb@microsoft.com or file a support ticket from hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="97f64-130">Uma vez que o aplicativo hello em execução, você pode tentar diferentes [políticas de indexação](indexing-policies.md) e [níveis de consistência](consistency-levels.md) toounderstand seu impacto na taxa de transferência e latência.</span><span class="sxs-lookup"><span data-stu-id="97f64-130">Once you have hello app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) toounderstand their impact on throughput and latency.</span></span> <span data-ttu-id="97f64-131">Também pode examinar o código-fonte hello e implementar aplicativos de produção ou de conjuntos de testes próprio de tooyour de configurações semelhantes.</span><span class="sxs-lookup"><span data-stu-id="97f64-131">You can also review hello source code and implement similar configurations tooyour own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97f64-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97f64-132">Next steps</span></span>
<span data-ttu-id="97f64-133">Neste artigo, analisamos como você pode realizar testes de desempenho e escala com o Cosmos DB usando um aplicativo de console .NET.</span><span class="sxs-lookup"><span data-stu-id="97f64-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="97f64-134">Consulte toohello links abaixo para obter informações adicionais sobre como trabalhar com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="97f64-134">Please refer toohello links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="97f64-135">Amostra de teste de desempenho do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="97f64-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="97f64-136">Tooimprove de opções de configuração do cliente desempenho de banco de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="97f64-136">Client configuration options tooimprove Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="97f64-137">Particionamento do lado do servidor no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="97f64-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


