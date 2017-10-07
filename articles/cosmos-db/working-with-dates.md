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
# <a name="working-with-dates-in-azure-cosmos-db"></a>Trabalhando com datas no Azure Cosmos DB
O Azure Cosmos DB fornece flexibilidade de esquema e indexação avançada por meio de um modelo de dados [JSON](http://www.json.org) nativo. Todos os recursos do Azure Cosmos DB, incluindo bancos de dados, coleções, documentos e procedimentos armazenados são modelados e armazenados como documentos JSON. Como um requisito para ser portátil, o JSON (e o Azure Cosmos DB) dá suporte apenas a um conjunto pequeno de tipos básicos: Cadeia de caracteres, Número, Booliano, Matriz, Objeto e Nulo. No entanto, o JSON é flexível e permitir que desenvolvedores e estruturas toorepresent tipos mais complexos usando esses primitivos e compor-los como objetos ou matrizes. 

Em tipos básicos de toohello de adição, muitos aplicativos necessário Olá [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) digite toorepresent datas e os carimbos de hora. Este artigo descreve como os desenvolvedores podem armazenar, recuperar e consultar datas no banco de dados do Cosmos do Azure usando o SDK .NET de saudação.

## <a name="storing-datetimes"></a>Armazenando DateTimes
Por padrão, Olá [banco de dados do SDK do Azure Cosmos](documentdb-sdk-dotnet.md) serializa os valores de data e hora como [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) cadeias de caracteres. A maioria dos aplicativos pode usar representação de cadeia de caracteres hello padrão para DateTime para Olá motivos a seguir:

* Cadeias de caracteres podem ser comparadas e Olá relativo a ordenação dos valores de DateTime Olá é preservada quando eles são transformados toostrings. 
* Essa abordagem não exige qualquer código personalizado ou atributos para conversão de JSON.
* datas de saudação armazenado em JSON são legíveis.
* Essa abordagem pode aproveitar o índice do Azure Cosmos DB para um desempenho rápido de consulta.

Por exemplo, Olá repositórios de trecho de código a seguir um `Order` do objeto que contém duas propriedades de data e hora - `ShipDate` e `OrderDate` como um documento usando Olá .NET SDK:

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

Esse documento é armazenado no Azure Cosmos DB da seguinte maneira:

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

Como alternativa, você pode armazenar DateTimes como os carimbos de hora Unix, ou seja, como um número que representa o número de saudação de segundos decorridos desde 1º de janeiro de 1970. A propriedade Timestamp (`_ts`) interna do Cosmos DB segue essa abordagem. Você pode usar o hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) tooserialize DateTimes como números de classe. 

## <a name="indexing-datetimes-for-range-queries"></a>Indexando DateTimes para consultas de intervalo
As consultas de intervalo são comuns com valores de DateTime. Por exemplo, se você precisa toofind todos os pedidos criados desde ontem, ou localizar todos os pedidos enviados em Olá últimos cinco minutos, será necessário tooperform consultas de intervalo. tooexecute essas consultas com eficiência, você deve configurar sua coleção para indexação de intervalo em cadeias de caracteres.

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

Você pode aprender mais sobre como tooconfigure indexação políticas em [políticas de indexação do banco de dados do Azure Cosmos](indexing-policies.md).

## <a name="querying-datetimes-in-linq"></a>Consultando DateTimes no LINQ
Olá SDK .NET do DocumentDB automaticamente oferece suporte a consultas de dados armazenados no banco de dados do Azure Cosmos por meio de LINQ. Por exemplo, hello trecho a seguir mostra uma consulta LINQ que pedidos de filtros que foram fornecidos em Olá últimos três dias.

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

Você pode aprender mais sobre SQL consulta linguagem e hello provedor LINQ do Azure Cosmos banco de dados em [consultar banco de dados do Cosmos](documentdb-sql-query.md).

Neste artigo, vimos como toostore, índice e consulta DateTimes no banco de dados do Azure Cosmos.

## <a name="next-steps"></a>Próximas etapas
* Baixe e execute Olá [amostras no GitHub de código](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)
* Saiba mais sobre a [Consulta da API do DocumentDB](documentdb-sql-query.md)
* Saiba mais sobre as [Políticas de indexação do Azure Cosmos DB](indexing-policies.md)
