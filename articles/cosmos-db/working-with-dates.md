---
title: aaaWorking com datas no banco de dados do Azure Cosmos | Microsoft Docs
description: Saiba mais sobre como toowork com datas no banco de dados do Azure Cosmos.
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="70ae2-103">Trabalhando com datas no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="70ae2-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="70ae2-104">O Azure Cosmos DB fornece flexibilidade de esquema e indexação avançada por meio de um modelo de dados [JSON](http://www.json.org) nativo.</span><span class="sxs-lookup"><span data-stu-id="70ae2-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="70ae2-105">Todos os recursos do Azure Cosmos DB, incluindo bancos de dados, coleções, documentos e procedimentos armazenados são modelados e armazenados como documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="70ae2-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="70ae2-106">Como um requisito para ser portátil, o JSON (e o Azure Cosmos DB) dá suporte apenas a um conjunto pequeno de tipos básicos: Cadeia de caracteres, Número, Booliano, Matriz, Objeto e Nulo.</span><span class="sxs-lookup"><span data-stu-id="70ae2-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="70ae2-107">No entanto, o JSON é flexível e permitir que desenvolvedores e estruturas toorepresent tipos mais complexos usando esses primitivos e compor-los como objetos ou matrizes.</span><span class="sxs-lookup"><span data-stu-id="70ae2-107">However, JSON is flexible and allow developers and frameworks toorepresent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="70ae2-108">Em tipos básicos de toohello de adição, muitos aplicativos necessário Olá [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) digite toorepresent datas e os carimbos de hora.</span><span class="sxs-lookup"><span data-stu-id="70ae2-108">In addition toohello basic types, many applications need hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type toorepresent dates and timestamps.</span></span> <span data-ttu-id="70ae2-109">Este artigo descreve como os desenvolvedores podem armazenar, recuperar e consultar datas no banco de dados do Cosmos do Azure usando o SDK .NET de saudação.</span><span class="sxs-lookup"><span data-stu-id="70ae2-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using hello .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="70ae2-110">Armazenando DateTimes</span><span class="sxs-lookup"><span data-stu-id="70ae2-110">Storing DateTimes</span></span>
<span data-ttu-id="70ae2-111">Por padrão, Olá [banco de dados do SDK do Azure Cosmos](documentdb-sdk-dotnet.md) serializa os valores de data e hora como [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="70ae2-111">By default, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="70ae2-112">A maioria dos aplicativos pode usar representação de cadeia de caracteres hello padrão para DateTime para Olá motivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="70ae2-112">Most applications can use hello default string representation for DateTime for hello following reasons:</span></span>

* <span data-ttu-id="70ae2-113">Cadeias de caracteres podem ser comparadas e Olá relativo a ordenação dos valores de DateTime Olá é preservada quando eles são transformados toostrings.</span><span class="sxs-lookup"><span data-stu-id="70ae2-113">Strings can be compared, and hello relative ordering of hello DateTime values is preserved when they are transformed toostrings.</span></span> 
* <span data-ttu-id="70ae2-114">Essa abordagem não exige qualquer código personalizado ou atributos para conversão de JSON.</span><span class="sxs-lookup"><span data-stu-id="70ae2-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="70ae2-115">datas de saudação armazenado em JSON são legíveis.</span><span class="sxs-lookup"><span data-stu-id="70ae2-115">hello dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="70ae2-116">Essa abordagem pode aproveitar o índice do Azure Cosmos DB para um desempenho rápido de consulta.</span><span class="sxs-lookup"><span data-stu-id="70ae2-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="70ae2-117">Por exemplo, Olá repositórios de trecho de código a seguir um `Order` do objeto que contém duas propriedades de data e hora - `ShipDate` e `OrderDate` como um documento usando Olá .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="70ae2-117">For example, hello following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using hello .NET SDK:</span></span>

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

<span data-ttu-id="70ae2-118">Esse documento é armazenado no Azure Cosmos DB da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="70ae2-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="70ae2-119">Como alternativa, você pode armazenar DateTimes como os carimbos de hora Unix, ou seja, como um número que representa o número de saudação de segundos decorridos desde 1º de janeiro de 1970.</span><span class="sxs-lookup"><span data-stu-id="70ae2-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing hello number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="70ae2-120">A propriedade Timestamp (`_ts`) interna do Cosmos DB segue essa abordagem.</span><span class="sxs-lookup"><span data-stu-id="70ae2-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="70ae2-121">Você pode usar o hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) tooserialize DateTimes como números de classe.</span><span class="sxs-lookup"><span data-stu-id="70ae2-121">You can use hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class tooserialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="70ae2-122">Indexando DateTimes para consultas de intervalo</span><span class="sxs-lookup"><span data-stu-id="70ae2-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="70ae2-123">As consultas de intervalo são comuns com valores de DateTime.</span><span class="sxs-lookup"><span data-stu-id="70ae2-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="70ae2-124">Por exemplo, se você precisa toofind todos os pedidos criados desde ontem, ou localizar todos os pedidos enviados em Olá últimos cinco minutos, será necessário tooperform consultas de intervalo.</span><span class="sxs-lookup"><span data-stu-id="70ae2-124">For example, if you need toofind all orders created since yesterday, or find all orders shipped in hello last five minutes, you need tooperform range queries.</span></span> <span data-ttu-id="70ae2-125">tooexecute essas consultas com eficiência, você deve configurar sua coleção para indexação de intervalo em cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="70ae2-125">tooexecute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="70ae2-126">Você pode aprender mais sobre como tooconfigure indexação políticas em [políticas de indexação do banco de dados do Azure Cosmos](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="70ae2-126">You can learn more about how tooconfigure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="70ae2-127">Consultando DateTimes no LINQ</span><span class="sxs-lookup"><span data-stu-id="70ae2-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="70ae2-128">Olá SDK .NET do DocumentDB automaticamente oferece suporte a consultas de dados armazenados no banco de dados do Azure Cosmos por meio de LINQ.</span><span class="sxs-lookup"><span data-stu-id="70ae2-128">hello DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="70ae2-129">Por exemplo, hello trecho a seguir mostra uma consulta LINQ que pedidos de filtros que foram fornecidos em Olá últimos três dias.</span><span class="sxs-lookup"><span data-stu-id="70ae2-129">For example, hello following snippet shows a LINQ query that filters orders that were shipped in hello last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="70ae2-130">Você pode aprender mais sobre SQL consulta linguagem e hello provedor LINQ do Azure Cosmos banco de dados em [consultar banco de dados do Cosmos](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="70ae2-130">You can learn more about Azure Cosmos DB's SQL query language and hello LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="70ae2-131">Neste artigo, vimos como toostore, índice e consulta DateTimes no banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="70ae2-131">In this article, we looked at how toostore, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70ae2-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70ae2-132">Next Steps</span></span>
* <span data-ttu-id="70ae2-133">Baixe e execute Olá [amostras no GitHub de código](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="70ae2-133">Download and run hello [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="70ae2-134">Saiba mais sobre a [Consulta da API do DocumentDB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="70ae2-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="70ae2-135">Saiba mais sobre as [Políticas de indexação do Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="70ae2-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
