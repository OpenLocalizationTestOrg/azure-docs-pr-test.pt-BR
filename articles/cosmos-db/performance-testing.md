---
title: Testes de escala e desempenho do Azure Cosmos DB | Microsoft Docs
description: Saiba como realizar testes de desempenho e escala com o Azure Cosmos DB
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
ms.openlocfilehash: b5a1edd08819e82437c5b22d8eb131665d7c9645
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="5125b-104">Teste de desempenho e escala com o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5125b-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="5125b-105">O teste de desempenho e escalabilidade é uma etapa importante no desenvolvimento de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5125b-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="5125b-106">Para muitos aplicativos, a camada de banco de dados tem um impacto significativo sobre o desempenho e a escalabilidade geral e, portanto, é um componente essencial do teste de desempenho.</span><span class="sxs-lookup"><span data-stu-id="5125b-106">For many applications, the database tier has a significant impact on the overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="5125b-107">O [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) foi desenvolvido para fins de escala elástica e desempenho previsível e, portanto, é uma excelente opção para aplicativos que precisam de uma camada de banco de dados de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="5125b-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="5125b-108">Este artigo é uma referência para desenvolvedores que implementam conjuntos de testes de desempenho para suas cargas de trabalho do Cosmos DB ou que avaliam o Cosmos DB para cenários de aplicativos de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="5125b-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="5125b-109">Ele se concentra principalmente nos testes de desempenho de banco de dados isolados, mas também inclui práticas recomendadas para aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="5125b-109">It focuses primarily on isolated performance testing of the database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="5125b-110">Depois de ler este artigo, você poderá responder as seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="5125b-110">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="5125b-111">Onde posso encontrar um aplicativo cliente do .NET de exemplo para testar o desempenho do Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="5125b-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="5125b-112">Como fazer para obter altos níveis de produtividade com o Azure Cosmos DB em meu aplicativo cliente?</span><span class="sxs-lookup"><span data-stu-id="5125b-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="5125b-113">Para começar a codificar, baixe o projeto na [Exemplo de teste de desempenho do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="5125b-113">To get started with code, please download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="5125b-114">A meta desse aplicativo é demonstrar as melhores práticas para extrair um melhor desempenho do Cosmos DB com um número menor de computadores cliente.</span><span class="sxs-lookup"><span data-stu-id="5125b-114">The goal of this application is to demonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="5125b-115">Ele não foi feito para demonstrar a capacidade máxima do serviço, que pode ser dimensionada sem limites.</span><span class="sxs-lookup"><span data-stu-id="5125b-115">This was not made to demonstrate the peak capacity of the service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="5125b-116">Se você estiver procurando opções de configuração do lado do cliente para melhorar o desempenho do Cosmos DB, consulte [Dicas de desempenho do Azure Cosmos DB](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="5125b-116">If you're looking for client-side configuration options to improve Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-the-performance-testing-application"></a><span data-ttu-id="5125b-117">Execute o aplicativo de teste de desempenho</span><span class="sxs-lookup"><span data-stu-id="5125b-117">Run the performance testing application</span></span>
<span data-ttu-id="5125b-118">A maneira mais rápida de começar é compilar e executar o exemplo do .NET abaixo, conforme descrito nas etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="5125b-118">The quickest way to get started is to compile and run the .NET sample below, as described in the steps below.</span></span> <span data-ttu-id="5125b-119">Você também pode examinar o código-fonte e implementar configurações semelhantes no seus aplicativos clientes.</span><span class="sxs-lookup"><span data-stu-id="5125b-119">You can also review the source code and implement similar configurations to your own client applications.</span></span>

<span data-ttu-id="5125b-120">**Etapa 1:** baixe o projeto no [Exemplo de teste de desempenho do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark) ou bifurque o repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="5125b-120">**Step 1:** Download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork the GitHub repository.</span></span>

<span data-ttu-id="5125b-121">**Etapa 2:** modifique as configurações de EndpointUrl, AuthorizationKey, CollectionThroughput e DocumentTemplate (opcional) em App.config.</span><span class="sxs-lookup"><span data-stu-id="5125b-121">**Step 2:** Modify the settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="5125b-122">Antes de provisionar as coleções com alta produtividade, confira a [Página de Preços](https://azure.microsoft.com/pricing/details/cosmos-db/) para estimar os custos por coleção.</span><span class="sxs-lookup"><span data-stu-id="5125b-122">Before provisioning collections with high throughput, please refer to the [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) to estimate the costs per collection.</span></span> <span data-ttu-id="5125b-123">O Azure Cosmos DB cobra o armazenamento e a produtividade de forma independente e por hora. Portanto, você pode economizar excluindo ou reduzindo a produtividade de suas coleções do Azure Cosmos DB após o teste.</span><span class="sxs-lookup"><span data-stu-id="5125b-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering the throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="5125b-124">**Etapa 3:** compile e execute o aplicativo de console da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="5125b-124">**Step 3:** Compile and run the console app from the command line.</span></span> <span data-ttu-id="5125b-125">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="5125b-125">You should see output like the following:</span></span>

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


<span data-ttu-id="5125b-126">**Etapa 4 (se necessário):** a produtividade relatada (RU/s) da ferramenta deverá ser igual ou maior que a produtividade provisionada da coleção.</span><span class="sxs-lookup"><span data-stu-id="5125b-126">**Step 4 (if necessary):** The throughput reported (RU/s) from the tool should be the same or higher than the provisioned throughput of the collection.</span></span> <span data-ttu-id="5125b-127">Caso contrário, o aumento do DegreeOfParallelism em pequenos incrementos pode ajudá-lo a atingir o limite.</span><span class="sxs-lookup"><span data-stu-id="5125b-127">If not, increasing the DegreeOfParallelism in small increments may help you reach the limit.</span></span> <span data-ttu-id="5125b-128">Se a taxa de transferência do seu aplicativo cliente estagnar, iniciar várias instâncias do aplicativo nas mesmas máquinas ou em máquinas diferentes ajudará você atingir o limite configurado em instâncias diferentes.</span><span class="sxs-lookup"><span data-stu-id="5125b-128">If the throughput from your client app plateaus, launching multiple instances of the app on the same or different machines will help you reach the provisioned limit across the different instances.</span></span> <span data-ttu-id="5125b-129">Se precisar de ajuda com esta etapa, escreva um email para askcosmosdb@microsoft.com ou preencha um tíquete de suporte no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5125b-129">If you need help with this step, please, write an email to askcosmosdb@microsoft.com or file a support ticket from the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="5125b-130">Uma vez que o aplicativo estiver em execução, você poderá experimentar [Políticas de indexação](indexing-policies.md) e [Níveis de consistência](consistency-levels.md) diferentes para entender seu impacto na produtividade e na latência.</span><span class="sxs-lookup"><span data-stu-id="5125b-130">Once you have the app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) to understand their impact on throughput and latency.</span></span> <span data-ttu-id="5125b-131">Você também pode examinar o código-fonte e implementar configurações semelhantes no seus pacotes de teste ou aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="5125b-131">You can also review the source code and implement similar configurations to your own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5125b-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5125b-132">Next steps</span></span>
<span data-ttu-id="5125b-133">Neste artigo, analisamos como você pode realizar testes de desempenho e escala com o Cosmos DB usando um aplicativo de console .NET.</span><span class="sxs-lookup"><span data-stu-id="5125b-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="5125b-134">Consulte os links abaixo para obter mais informações sobre como trabalhar com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5125b-134">Please refer to the links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="5125b-135">Amostra de teste de desempenho do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5125b-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="5125b-136">Opções de configuração do cliente para melhorar o desempenho do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5125b-136">Client configuration options to improve Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="5125b-137">Particionamento do lado do servidor no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5125b-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


