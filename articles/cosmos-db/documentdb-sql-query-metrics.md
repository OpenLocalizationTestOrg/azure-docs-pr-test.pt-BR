---
title: "aaaSQL métricas de consulta para a API DocumentDB do Azure Cosmos DB | Microsoft Docs"
description: "Saiba mais sobre como tooinstrument e depuração Olá desempenho da consulta SQL de banco de dados do Azure Cosmos solicitações."
keywords: "sintaxe sql, consulta sql, consultas sql, linguagem de consulta json, conceitos de banco de dados e consultas sql, funções agregadas"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: b2fa8e8f-7291-45a3-9bd1-7284ed9077f8
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 2fee3786b7d48d254162699471943e316764b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a>Ajustando o desempenho de consulta com o Azure Cosmos DB
O Azure Cosmos DB fornece um [API do SQL para consultar dados](documentdb-sql-query.md), sem a necessidade de esquema ou índices secundários. Este artigo fornece as seguintes informações para desenvolvedores de saudação:

* Detalhes de alto nível sobre como funciona a execução da consulta SQL do Azure Cosmos DB
* Obter detalhes sobre cabeçalhos de solicitação e resposta de consulta e opções do SDK do cliente
* Algumas dicas e práticas recomendadas para desempenho de consulta
* Exemplos de como o desempenho de consulta tooutilize toodebug de estatísticas de execução de SQL

## <a name="about-sql-query-execution"></a>Sobre execução de consulta SQL

No banco de dados do Azure Cosmos, armazenar dados em contêineres, que podem aumentar tooany [throughput de solicitação ou o tamanho do armazenamento](partition-data.md). Banco de dados do Azure Cosmos perfeitamente dimensiona os dados em partições físicas em toohandle Olá abrange o crescimento de dados ou o aumento na taxa de transferência fornecida. Você pode emitir consultas tooany contêiner de dados SQL usando Olá API REST ou um de saudação suportada [SDKs do DocumentDB](documentdb-sdk-dotnet.md).

Uma visão geral de particionamento: definir uma chave de partição como "city", que determina como os dados são divididos em partições físicas. Chave de partição única dados pertencentes tooa (por exemplo, "city" = = "Seattle") é armazenado em uma partição física, mas normalmente uma única partição física tem várias chaves de partição. Quando uma partição atinge seu tamanho de armazenamento, o serviço de saudação perfeitamente partição Olá será dividida em duas novas partições e divide a chave de partição Olá uniformemente entre essas partições. Como as partições são transitórias, hello APIs usam uma abstração de uma "chave intervalo de partição", que indica os intervalos de saudação de hashes de chave de partição. 

Quando você emitir uma consulta tooAzure Cosmos DB, Olá SDK executa essas etapas lógicas:

* Analise o plano de execução Olá SQL consulta toodetermine Olá consulta. 
* Se a consulta de saudação inclui um filtro com a chave de partição hello, como `SELECT * FROM c WHERE c.city = "Seattle"`, é roteado tooa partição única. Se a consulta Olá não tem um filtro na chave de partição, em seguida, ele é executado em todas as partições e resultados são mesclados do lado do cliente.
* consulta de saudação é executada dentro de cada partição em série ou em paralelo, com base na configuração do cliente. Dentro de cada partição, consulta Olá pode tornar um ou mais viagens de ida e dependendo da complexidade da consulta hello, configurado o tamanho da página e provisionado a taxa de transferência da coleção de saudação. Cada execução retorna o número de saudação do [unidades de solicitação](request-units.md) consumido pela execução da consulta e, opcionalmente, as estatísticas de execução de consulta. 
* Olá SDK executa um resumo dos resultados de consulta de saudação entre partições. Por exemplo, se a consulta Olá envolve um ORDER BY em partições, resultados de partições individuais são classificados mesclagem tooreturn resultados em ordem classificada globalmente. Se a consulta de saudação é uma agregação como `COUNT`, Olá contagens de partições individuais são tooproduce somado Olá contagem geral.

Olá SDKs fornecem várias opções para a execução da consulta. Por exemplo, essas opções estão disponíveis em Olá no .NET `FeedOptions` classe. Olá tabela a seguir descreve essas opções e como elas afetam o tempo de execução de consulta. 

| Opção | Descrição |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | Deve ser definido tootrue para qualquer consulta que requer toobe executado em mais de uma partição. Este é um sinalizador explícita tooenable você compensações de desempenho consciente toomake durante o tempo de desenvolvimento. |
| `EnableScanInQuery` | Deve ser definido tootrue se você rejeitou a indexação, mas desejar consulta de saudação toorun por meio de uma verificação mesmo assim. Só aplicável se a indexação para Olá solicitado caminho de filtro está desabilitado. | 
| `MaxItemCount` | número máximo de saudação de itens tooreturn por servidor de toohello de ida e volta. Definindo muito-1, você pode deixar o servidor de saudação gerenciar Olá número de itens. Ou, você pode diminuir esse valor tooretrieve somente um pequeno número de itens por viagem de ida e. 
| `MaxBufferedItemCount` | Isso é uma opção do lado do cliente e usado o consumo de memória Olá toolimit ao executar entre partições ORDER BY. Um valor mais alto ajuda a reduzir a latência de saudação de classificação entre partições. |
| `MaxDegreeOfParallelism` | Obtém ou define o número de saudação de operações simultâneas executados do lado do cliente durante a execução de consulta paralelos em Olá serviço de banco de dados do DocumentDB do Azure. Um valor de propriedade positivo limita o número de saudação do valor de conjunto de toohello operações simultâneas. Se estiver definido como tooless que 0, o sistema de saudação decide automaticamente número de saudação de toorun operações simultâneas. |
| `PopulateQueryMetrics` | Habilita o log detalhado de estatísticas de tempo gasto em várias fases de execução da consulta como tempo de compilação, o tempo de loop de índice e o documento de tempo de carregamento. Você pode compartilhar a saída de estatísticas de consulta com problemas de desempenho de consulta de toodiagnose de suporte do Azure. |
| `RequestContinuation` | Você pode retomar a execução de consulta, passando no token de continuação opaco Olá retornado por qualquer consulta. o token de continuação Olá encapsula todos os estados necessários para a execução de consulta. |
| `ResponseContinuationTokenLimitInKb` | Você pode limitar o tamanho máximo de saudação do token de continuação Olá retornado pelo servidor de saudação. Talvez seja necessário tooset isso se seu host de aplicativo tem limites de tamanho do cabeçalho de resposta. Essa configuração pode aumentar Olá RUs consumidos para consulta hello e duração geral.  |

Por exemplo, vamos usar uma consulta de exemplo na chave de partição solicitada em uma coleção com `/city` como partição Olá chave e provisionada com 100.000 RU/s de taxa de transferência. Solicitar esta consulta usando `CreateDocumentQuery<T>` no .NET como Olá a seguir:

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
        MaxItemCount = -1, 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();
```

Olá trecho SDK mostrado acima, corresponde toohello solicitação de API de REST a seguir:

```
POST https://arramacquerymetrics-westus.documents.azure.com/dbs/db/colls/sample/docs HTTP/1.1
x-ms-continuation: 
x-ms-documentdb-isquery: True
x-ms-max-item-count: -1
x-ms-documentdb-query-enablecrosspartition: True
x-ms-documentdb-query-parallelizecrosspartitionquery: True
x-ms-documentdb-query-iscontinuationexpected: True
x-ms-documentdb-populatequerymetrics: True
x-ms-date: Tue, 27 Jun 2017 21:52:18 GMT
authorization: type%3dmaster%26ver%3d1.0%26sig%3drp1Hi83Y8aVV5V6LzZ6xhtQVXRAMz0WNMnUuvriUv%2b4%3d
x-ms-session-token: 7:8,6:2008,5:8,4:2008,3:8,2:2008,1:8,0:8,9:8,8:4008
Cache-Control: no-cache
x-ms-consistency-level: Session
User-Agent: documentdb-dotnet-sdk/1.14.1 Host/32-bit MicrosoftWindowsNT/6.2.9200.0
x-ms-version: 2017-02-22
Accept: application/json
Content-Type: application/query+json
Host: arramacquerymetrics-westus.documents.azure.com
Content-Length: 52
Expect: 100-continue

{"query":"SELECT * FROM c WHERE c.city = 'Seattle'"}
```

Cada página de execução de consulta corresponde tooa API REST `POST` com hello `Accept: application/query+json` cabeçalho e consulta SQL Olá no corpo de saudação. Cada consulta faz com que um ou mais arredondar o servidor de toohello viagens com hello `x-ms-continuation` token ecoada entre a execução de tooresume de cliente e servidor de saudação. Opções de configuração de saudação do FeedOptions são passadas toohello servidor na forma de saudação de cabeçalhos de solicitação. Por exemplo, `MaxItemCount` corresponde muito`x-ms-max-item-count`. 

Olá, solicitação retorna seguinte hello (truncados para legibilidade) resposta:

```
HTTP/1.1 200 Ok
Cache-Control: no-store, no-cache
Pragma: no-cache
Transfer-Encoding: chunked
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Strict-Transport-Security: max-age=31536000
x-ms-last-state-change-utc: Tue, 27 Jun 2017 21:01:57.561 GMT
x-ms-resource-quota: documentSize=10240;documentsSize=10485760;documentsCount=-1;collectionSize=10485760;
x-ms-resource-usage: documentSize=1;documentsSize=884;documentsCount=2000;collectionSize=1408;
x-ms-item-count: 2000
x-ms-schemaversion: 1.3
x-ms-alt-content-path: dbs/db/colls/sample
x-ms-content-path: +9kEANVq0wA=
x-ms-xp-role: 1
x-ms-documentdb-query-metrics: totalExecutionTimeInMs=33.67;queryCompileTimeInMs=0.06;queryLogicalPlanBuildTimeInMs=0.02;queryPhysicalPlanBuildTimeInMs=0.10;queryOptimizationTimeInMs=0.00;VMExecutionTimeInMs=32.56;indexLookupTimeInMs=0.36;documentLoadTimeInMs=9.58;systemFunctionExecuteTimeInMs=0.00;userFunctionExecuteTimeInMs=0.00;retrievedDocumentCount=2000;retrievedDocumentSize=1125600;outputDocumentCount=2000;writeOutputTimeInMs=18.10;indexUtilizationRatio=1.00
x-ms-request-charge: 604.42
x-ms-serviceversion: version=1.14.34.4
x-ms-activity-id: 0df8b5f6-83b9-4493-abda-cce6d0f91486
x-ms-session-token: 2:2008
x-ms-gatewayversion: version=1.14.33.2
Date: Tue, 27 Jun 2017 21:59:49 GMT
```

cabeçalhos de resposta de chave Olá retornados da consulta Olá incluem o seguinte hello:

| Opção | Descrição |
| ------ | ----------- |
| `x-ms-item-count` | número de saudação de itens retornados na resposta de saudação. Isso é dependente de saudação fornecida `x-ms-max-item-count`, Olá o número de itens que podem se ajustar no tamanho da carga Olá máximo de resposta, taxa de transferência fornecida hello e tempo de execução de consulta. |  
| `x-ms-continuation:` | Olá continuação token tooresume a execução de consulta hello, se houver mais resultados disponíveis. | 
| `x-ms-documentdb-query-metrics` | estatísticas de consulta Olá para execução de saudação. Isso é uma cadeia de caracteres delimitada que contém as estatísticas de tempo gasto em Olá várias fases de execução da consulta. Retornado se `x-ms-documentdb-populatequerymetrics` está definido muito`True`. | 
| `x-ms-request-charge` | Olá inúmeros [unidades de solicitação](request-units.md) consumidos pela consulta hello. | 

Para obter detalhes sobre cabeçalhos de solicitação de API REST do hello e opções, consulte [consultar recursos usando Olá API REST do DocumentDB](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api).

## <a name="best-practices-for-query-performance"></a>Práticas recomendadas para desempenho de consulta
Olá seguem fatores mais comuns de saudação que afetam o desempenho de consulta de banco de dados do Azure Cosmos. Podemos obter detalhes de cada um desses tópicos neste artigo.

| Fator | Dica | 
| ------ | -----| 
| Taxa de transferência provisionada | Medir RU por consulta e verifique se você tem Olá provisionado taxa de transferência necessária para que suas consultas. | 
| Particionamento e chaves de partição | Favorecer consultas com valor de chave de partição Olá na cláusula de filtro de saudação de baixa latência. |
| Opções de consulta e de SDK | Siga as práticas recomendadas do SDK com conectividade direta e ajuste as opções de execução de consulta do lado do cliente. |
| Latência da rede | Conta para a rede sobrecarga em medidas e usar tooread APIs de hospedagem múltipla de saudação mais próximo de região. |
| Política de indexação | Certifique-se de que você tenha Olá necessário caminhos/política de indexação para consulta hello. |
| Métricas de execução da consulta | Analise Olá consulta execução métricas tooidentify potencial regravações de formas de consulta e dados.  |

### <a name="provisioned-throughput"></a>Taxa de transferência provisionada
No Cosmos DB, você cria contêineres de dados, cada um com a taxa de transferência reservada expressa em RUs (unidades de solicitação) por segundo. Uma leitura de um documento de 1 KB é 1 RU e cada operação (incluindo consultas) é normalizado tooa número fixo de RUs com base em sua complexidade. Por exemplo, se você tiver 1000 RU/s provisionado para o contêiner, e você tiver uma consulta como `SELECT * FROM c WHERE c.city = 'Seattle'` que consome 5 RUs, em seguida, você pode executar (1000 RU/s) / (RU/consulta 5) = 200 consulta/s tais consultas por segundo. 

Se você enviar consultas/s mais de 200, o serviço de Olá inicia a limitação de taxa de solicitações de entrada acima 200/s. Olá SDKs automaticamente lidar com isso, executando uma repetição/retirada, portanto, você poderá notar uma latência mais alta para essas consultas. Aumentar Olá provisionado taxa de transferência toohello necessário valor aumenta a latência da consulta e a taxa de transferência. 

toolearn mais informações sobre unidades de solicitação, consulte [unidades de solicitação](request-units.md).

### <a name="partitioning-and-partition-keys"></a>Particionamento e chaves de partição
Com o banco de dados do Azure Cosmos, normalmente consultas executam na ordem do mais rápido mais eficiente tooslower/menos eficiente de saudação. 

* OBTER em uma chave de partição única e a chave de item
* Consulta com uma cláusula de filtro em uma chave de partição única
* Consulta sem uma cláusula de filtro de igualdade ou um intervalo em qualquer propriedade
* Consulta sem filtros

Consultas que tooconsult necessidade todas as partições necessidade maior latência e pode consumir RUs superior. Como cada partição tem indexação automática em relação a todas as propriedades, consulta Olá pode ser atendida com eficiência do índice Olá nesse caso. Você pode fazer consultas que abrangem mais rápido de partições usando opções de paralelismo hello.

toolearn mais informações sobre particionamento e chaves de partição, consulte [particionamento no banco de dados do Azure Cosmos](partition-data.md).

### <a name="sdk-and-query-options"></a>Opções de consulta e de SDK
Consulte [dicas de desempenho](performance-tips.md) e [testes de desempenho](performance-testing.md) para como tooget Olá melhor desempenho no cliente do banco de dados do Azure Cosmos. Isso inclui usar Olá SDKs mais recentes, configurando as configurações de específico de plataforma como o número padrão de conexões, a frequência da coleta de lixo e usando as opções de conectividade leve como Direct/TCP. 


#### <a name="max-item-count"></a>Contagem máxima de itens
Para consultas, Olá valor `MaxItemCount` pode ter um impacto significativo no tempo de consulta de ponta a ponta. Cada viagem de ida e retornará não mais do que o número de saudação de itens no servidor toohello `MaxItemCount` (padrão de 100 itens). Definir esse valor mais alto tooa (-1 é recomendado e máximo) melhorará a duração de consulta geral limitando Olá número de idas e voltas entre servidor e cliente, especialmente para consultas com grandes conjuntos de resultados.

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a>Grau máximo de paralelismo
Para consultas, ajustar Olá `MaxDegreeOfParallelism` tooidentify Olá melhores configurações para seu aplicativo, especialmente se você executar consultas entre partições (sem um filtro no valor de chave de partição Olá). `MaxDegreeOfParallelism`Controla o número máximo de saudação de tarefas em paralelo, ou seja, no máximo Olá toobe partições visitado em paralelo. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();
```

Vamos supor que
* D = padrão máximo número de tarefas paralelas (= número total de processador na máquina do cliente Olá)
* P = número máximo especificado pelo usuário de tarefas paralelas
* N = número de partições que precisa toobe visitado para responder a uma consulta

A seguir é as implicações de como consultas paralelas Olá se comportem de valores diferentes de P.
* (P == 0) => Modo serial
* (P == 1) => Máximo de uma tarefa
* (P > 1) => Mín. (P, N) de tarefas paralelas 
* (P < 1) => Mín. (N, D) de tarefas paralelas

Notas de versão do SDK e detalhes sobre classes e métodos implementados, consulte [SDKs do DocumentDB](documentdb-sdk-dotnet.md)

### <a name="network-latency"></a>Latência da rede
Consulte [distribuição global do banco de dados do Azure Cosmos](tutorial-global-distribution-documentdb.md) como tooset até distribuição global e conectar-se a região mais próxima toohello. Latência de rede tem um impacto significativo no desempenho da consulta quando precisar toomake várias viagens ou recuperar um grande conjunto de resultados de consulta de saudação. 

Olá seção em métricas de execução de consulta explica como tooretrieve Olá servidor de tempo de execução de consultas ( `totalExecutionTimeInMs`), de modo que você pode diferenciar entre o tempo gasto na execução da consulta e o tempo gasto em trânsito de rede.

### <a name="indexing-policy"></a>Política de indexação
Consulte [Configurando a política de indexação](indexing-policies.md) para indexação de caminhos, tipos e os modos e como elas afetam a execução da consulta. Por padrão, Olá política de indexação usa a indexação de Hash para cadeias de caracteres, que é eficiente para consultas de igualdade, mas não para consultas de intervalo/ordem através de consultas. Se você precisar de consultas de intervalo para cadeias de caracteres, é recomendável especificar Olá tipo de índice de intervalo para todas as cadeias de caracteres. 

## <a name="query-execution-metrics"></a>Métricas de execução da consulta
Você pode obter métricas detalhadas na execução da consulta, passando Olá opcional `x-ms-documentdb-populatequerymetrics` cabeçalho (`FeedOptions.PopulateQueryMetrics` no hello .NET SDK). Olá valor retornado em `x-ms-documentdb-query-metrics` tem Olá destinadas para solução de problemas de execução de consulta avançada de pares de chave-valor a seguir. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;

```

| Métrica | Unidade | Descrição | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | milissegundos | Tempo de execução da consulta | 
| `queryCompileTimeInMs` | milissegundos | Tempo de compilação de consulta  | 
| `queryLogicalPlanBuildTimeInMs` | milissegundos | Plano de consulta lógica tempo toobuild | 
| `queryPhysicalPlanBuildTimeInMs` | milissegundos | Plano de consulta físico toobuild tempo | 
| `queryOptimizationTimeInMs` | milissegundos | Tempo gasto na otimização de consulta | 
| `VMExecutionTimeInMs` | milissegundos | Tempo gasto em tempo de execução de consulta | 
| `indexLookupTimeInMs` | milissegundos | Tempo gasto na camada física de índice | 
| `documentLoadTimeInMs` | milissegundos | Tempo gasto no carregamento de documentos  | 
| `systemFunctionExecuteTimeInMs` | milissegundos | Tempo total gasto executando funções de sistema (interno) em milissegundos  | 
| `userFunctionExecuteTimeInMs` | milissegundos | Tempo total gasto executando funções definidas pelo usuário (interno) em milissegundos | 
| `retrievedDocumentCount` | milissegundos | Número total de documentos recuperados  | 
| `retrievedDocumentSize` | bytes | Tamanho total dos documentos recuperados em bytes  | 
| `outputDocumentCount` | count | Número de documentos de saída | 
| `writeOutputTimeInMs` | milissegundos | Tempo de execução da consulta em milissegundos | 
| `indexUtilizationRatio` | taxa de (< = 1) | Taxa do número de documentos correspondida Olá filtro toohello quantos documentos carregados  | 

Olá cliente SDKs podem internamente fazer várias operações tooserve Olá consulta dentro de cada partição. cliente Olá torna mais de uma chamada por partição se resultados totais Olá excederem `x-ms-max-item-count`, se consulta Olá excede a taxa de transferência fornecida para partição de Olá Olá se hello carga de consulta atinge o tamanho máximo de saudação por página ou se hello consulta atinge Olá sistema alocados tempo limite. Cada execução da consulta parcial retorna um `x-ms-documentdb-query-metrics` para a página. 

Aqui estão alguns exemplos de consultas e como toointerpret algumas das métricas de saudação retornadas da execução da consulta: 

| Consultar | Métrica de exemplo | Descrição | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | Olá número de documentos recuperados é 100 + 1 cláusula TOP Olá de toomatch. Tempo de consulta é gasto principalmente `WriteOutputTime` e `DocumentLoadTime` porque é uma verificação. | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | RetrievedDocumentCount agora é mais alto (500 + 1 toomatch Olá cláusula TOP). | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | Cerca de 0,9 ms é gasto na IndexLookupTime para uma pesquisa de chave, porque ele é um índice de pesquisa `/N/?`. | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | Um pouco mais de tempo (ms 1.7) é gasto em IndexLookupTime por um exame de intervalo, porque ele é um índice de pesquisa `/N/?`. | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | Mesmo tempo gasto em `DocumentLoadTime` como consultas anteriores, mas inferior `WriteOutputTime` porque estamos projetando apenas uma propriedade. | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | Sobre 213 ms é gasto na `UserDefinedFunctionExecutionTime` executar Olá UDF em cada valor de `c.N`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | Cerca de 0,6 ms é gasto na `IndexLookupTime` em `/Name/?`. A maioria das Olá consulta tempo de execução (ms ~ 7) em `SystemFunctionExecutionTime`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | A consulta é executada como uma verificação, pois ela usa `LOWER`, e 500 de 2491 documentos recuperados são retornados. |


## <a name="next-steps"></a>Próximas etapas
* toolearn sobre operadores de consulta SQL Olá com suporte e palavras-chave, consulte [consulta SQL](documentdb-sql-query.md). 
* toolearn sobre unidades de solicitação, consulte [unidades de solicitação](request-units.md).
* toolearn sobre a política de indexação, consulte [política de indexação](indexing-policies.md) 


