---
title: aaaPartitioning e escala no banco de dados do Azure Cosmos | Microsoft Docs
description: "Saiba mais sobre como particionamento funciona no banco de dados do Azure Cosmos, como particionamento tooconfigure e chaves de partição e como toopick Olá direito chave da partição para seu aplicativo."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30621d2ba0b89efb72005680d5f3a73998347514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a>Particionamento no banco de dados do Cosmos do Azure usando Olá API DocumentDB

[Banco de dados do Microsoft Azure Cosmos](../cosmos-db/introduction.md) é toohelp de serviço criado um banco de dados distribuído, vários modelos global você alcançar desempenho rápido e previsível e escalabilidade perfeitamente junto com seu aplicativo à medida que cresce. 

Este artigo fornece uma visão geral de como toowork com o particionamento de banco de dados do Cosmos contêineres com hello API DocumentDB. Consulte [particionamento e escala horizontal](../cosmos-db/partition-data.md) para obter uma visão geral dos conceitos e das melhores práticas de particionamento com uma API do Azure Cosmos DB. 

tooget iniciada com o código, baixe o projeto de saudação do [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir:   

* Como funciona o particionamento no Azure Cosmos DB?
* Como fazer para configurar o particionamento no Azure Cosmos DB?
* Quais são as chaves de partição, e como escolher a chave de partição correta de saudação para meu aplicativo?

tooget iniciada com o código, baixe o projeto de saudação do [exemplo de Driver de teste do Azure Cosmos DB desempenho](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a>Chaves de partição

Olá API DocumentDB, você especifica a definição de chave de partição Olá na forma de saudação de um caminho JSON. Olá tabela a seguir mostra exemplos de definições de chave de partição e valores hello correspondente tooeach. chave de partição Olá é especificado como um caminho, por exemplo, `/department` representa Olá departamento de propriedade. 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Chave de partição</strong></p></td>
            <td valign="top"><p><strong>Descrição</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>/department</p></td>
            <td valign="top"><p>Corresponde o valor toohello doc.department onde o documento é o item de saudação.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/properties/name</p></td>
            <td valign="top"><p>Corresponde o valor de toohello de doc.properties.name onde o documento é o item de saudação (propriedade aninhada).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/id</p></td>
            <td valign="top"><p>Corresponde o valor de toohello de doc.id (chave de id e a partição são Olá mesmo propriedade).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/"nome do departamento"</p></td>
            <td valign="top"><p>Corresponde o valor toohello doc ["nome do departamento"] onde o documento é o item de saudação.</p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> sintaxe Olá para chave de partição é especificação de caminho toohello semelhante para caminhos de política de indexação com diferença chave Olá Olá caminho corresponde a propriedade toohello em vez do valor de hello, ou seja, não há nenhum caractere curinga no final da saudação. Por exemplo, você especificaria /department/? Olá tooindex valores em departamento, mas Especifica /department como definição de chave de partição de saudação. chave de partição Olá implicitamente é indexada e não pode ser excluído da indexação usando substituições de política de indexação.
> 
> 

Vamos examinar como opção de saudação de chave de partição afeta o desempenho de saudação do seu aplicativo.

## <a name="working-with-hello-azure-cosmos-db-sdks"></a>Trabalhando com hello SDKs do banco de dados do Azure Cosmos
O Azure Cosmos DB adicionou suporte ao particionamento automático na [API REST versão 2015-12-16](/rest/api/documentdb/). Em contêineres de toocreate particionado de ordem, você deve baixar versões do SDK 1.6.0 ou suporte mais recente, em uma saudação plataformas SDK (.NET, Node.js, Java, Python, MongoDB). 

### <a name="creating-containers"></a>Criando contêineres
Olá exemplo a seguir mostra um toocreate de trecho de código .NET dados de telemetria de dispositivo um contêiner toostore 20.000 de unidades de solicitação por segundo de taxa de transferência. Olá SDK define o valor de OfferThroughput de saudação (que por sua vez define Olá `x-ms-offer-throughput` cabeçalho de solicitação na Olá REST API). Aqui vamos definir Olá `/deviceId` como chave de partição hello. opção de saudação de chave de partição é salvo junto com o restante Olá Olá metadados do contêiner como o nome e a política de indexação.

Para este exemplo, escolhemos `deviceId` como sabemos que (a) uma vez que há um grande número de dispositivos, gravações podem ser distribuídas uniformemente em partições e possibilitando tooscale Olá banco de dados tooingest grandes volumes de dados e (b) muitas solicitações hello como busca de leitura mais recente Olá para um dispositivo são deviceId único tooa no escopo e podem ser recuperados de uma única partição.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here hello property deviceId will be used as hello partition key too
// spread across partitions. Configured for 10K RU/s throughput and an indexing policy that supports 
// sorting against any number or string property.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

Este método faz uma API REST chamar tooCosmos banco de dados e serviço Olá provisionará um número de partições com base na taxa de transferência solicitada hello. Você pode alterar a taxa de transferência de saudação de um contêiner como o desempenho precisa evoluir. 

### <a name="reading-and-writing-items"></a>Lendo e gravando itens
Agora, vamos inserir dados no Cosmos DB. Aqui está um exemplo de classe que contém uma leitura do dispositivo e tooinsert de tooCreateDocumentAsync uma chamada de um novo dispositivo de leitura de um contêiner. Este é um exemplo utilizando Olá API DocumentDB:

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

// Create a document. Here hello partition key is extracted as "XMS-0001" based on hello collection definition
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

Vamos ler Olá item por sua chave de partição e a id, atualizá-lo e como uma etapa final, exclua-o por id e a chave de partição. Observe que as leituras de saudação incluem um valor de PartitionKey (correspondente toohello `x-ms-documentdb-partitionkey` cabeçalho de solicitação na Olá API REST).

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);

// Delete document. Needs partition key
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="querying-partitioned-containers"></a>Consultando contêineres particionados
Quando você consulta dados em contêineres particionados, o banco de dados do Cosmos automaticamente rotas Olá partições toohello de consulta correspondente valores de chave de partição do toohello especificados no filtro de saudação (se houver). Por exemplo, esta consulta é roteado toojust Olá partição contendo Olá chave de partição "XMS-0001".

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
Olá consulta a seguir não tem um filtro na chave de partição da saudação (DeviceId) e é leque exibindo tooall partições onde ela é executada no índice da partição Olá. Observe que você tem Olá toospecify EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` em Olá API REST) toohave Olá SDK tooexecute uma consulta em partições.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

O Cosmos DB dá suporte a [funções de agregação](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` e `AVG` em contêineres particionados usando SQL, a partir dos SDKs 1.12.0 e posterior. Consultas devem incluir um único operador de agregação e devem incluir um valor único na projeção de saudação.

### <a name="parallel-query-execution"></a>Execução de consulta paralela
Olá Cosmos DB SDKs 1.9.0 e acima do opções de execução de consulta paralela, que permitem que você tooperform baixa latência as consultas em coleções particionadas, mesmo quando eles precisarem de tootouch um grande número de partições. Por exemplo, Olá consulta a seguir é toorun configurado em paralelo entre partições.

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Você pode gerenciar a execução de consulta paralela ajustando Olá parâmetros a seguir:

* Definindo `MaxDegreeOfParallelism`, você pode controlar o grau de paralelismo, ou seja, Olá de número máximo de partições do contêiner de rede simultâneas conexões toohello hello. Se você definir muito-1, o grau de paralelismo Olá é gerenciado pelo Olá SDK. Se hello `MaxDegreeOfParallelism` não for especificado ou definido too0, que é o valor padrão de saudação, haverá partições de uma única rede conexão toohello contêiner.
* Definindo `MaxBufferedItemCount`, você pode compensar a latência da consulta e a utilização da memória no lado do cliente. Se você omite esse parâmetro ou defina muito-1, número de saudação de itens em buffer durante a execução de consulta paralela é gerenciado pelo Olá SDK.

Considerando Olá mesmo estado da coleção hello, uma consulta paralela retornará resultados Olá mesma ordem como em execução em série. Ao executar uma consulta entre partições que inclui a classificação (ORDER BY e/ou superior), problemas de banco de dados do SDK do Azure Cosmos Olá Olá consulta em paralelo em partições e mesclagens resultados parcialmente classificados no hello cliente lado tooproduce resultados ordenados globalmente.

### <a name="executing-stored-procedures"></a>Executando procedimentos armazenados
Você também pode executar transações atômicas em relação a documentos com hello a mesma ID de dispositivo, por exemplo, se você estiver mantendo agregações ou Olá estado mais recente de um dispositivo em um único item. 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
Na próxima seção, Olá, vamos examinar como você pode mover toopartitioned contêineres de contêineres de partição única.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, fornecemos uma visão geral de como toowork com o particionamento do banco de dados do Azure Cosmos contêineres com hello API DocumentDB. Consulte também [particionamento e escala horizontal](../cosmos-db/partition-data.md) para obter uma visão geral dos conceitos e das melhores práticas de particionamento com uma API do Azure Cosmos DB. 

* Executar testes de desempenho e escala com o BD Cosmos do Azure. Consulte [Teste de desempenho e escala com o BD Cosmos do Azure](performance-testing.md) para obter um exemplo.
* Introdução a codificação com hello [SDKs](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/)
* Saiba mais sobre a [produtividade provisionada no DB Cosmos do Azure](request-units.md)

