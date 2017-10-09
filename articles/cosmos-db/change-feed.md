---
title: "aaaWorking com alteração Olá feed suporte no banco de dados do Azure Cosmos | Microsoft Docs"
description: "Banco de dados do uso do Azure Cosmos alterar suporte feed tootrack alterações nos documentos e executar o processamento baseado em evento, como gatilhos e mantendo os sistemas de caches e análise atualizada."
keywords: "feed de alteração"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a>Trabalhando com suporte de feed Olá alteração no banco de dados do Azure Cosmos
O [Azure Cosmos DB](../cosmos-db/introduction.md) é um serviço de banco de dados rápido, flexível e replicado globalmente, usado para armazenar grandes volumes de dados transacionais e operacionais com latência previsível de milissegundos de dígito único para leituras e gravações. Isso o torna adequado para IoT, jogos, varejo e aplicativos de log operacional. Um padrão de design comum nesses aplicativos é tootrack alterações feitas a dados do banco de dados do Cosmos tooAzure e atualizar a exibições materializadas, executam a análise em tempo real, toocold de dados de arquivamento e acionar notificações em determinados eventos de acordo com essas alterações. Olá **alteração feed suporte** no banco de dados do Azure Cosmos permite soluções de toobuild eficiente e escalonável para cada um desses padrões.

Com suporte de feed de alteração, o banco de dados do Azure Cosmos fornece uma lista ordenada de documentos em uma coleção de banco de dados do Azure Cosmos na ordem de saudação na qual elas foram modificadas. Este feed pode ser usado toolisten para toodata modificações na coleção de saudação e executar ações como:

* Disparar tooan uma chamada de API, quando um documento é inserido ou modificado
* Executar o processamento em tempo real (fluxo) em atualizações
* Sincronizar dados com um cache, o mecanismo de pesquisa ou o data warehouse

As alterações no Azure Cosmos DB são persistentes e podem ser processadas de forma assíncrona e distribuídas entre um ou mais consumidores para processamento paralelo. Vamos examinar Olá APIs de feed de alteração e como você pode usá-los toobuild aplicativos escalonáveis de em tempo real. Este artigo mostra como toowork com o banco de dados do Azure Cosmos alterar feed e hello API DocumentDB. 

![Usar o banco de dados do Azure Cosmos alteração feed análise em tempo real toopower e cenários de computação controlada por evento](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> Alteração de feed de suporte é fornecida somente para Olá API DocumentDB neste momento. Olá Graph API e a API de tabela não têm suporte no momento.

## <a name="use-cases-and-scenarios"></a>Cenários e casos de uso
Feed de alteração permite processamento eficiente de grandes conjuntos de dados com um alto volume de gravações e oferece uma tooidentify de conjuntos de dados inteiro tooquerying alternativo que foi alterado. Por exemplo, você pode executar Olá seguintes tarefas com eficiência:

* Atualize um cache, índice de pesquisa ou data warehouse com os dados armazenados no Azure Cosmos DB.
* Implementar dados de nível de aplicativo em camadas e de arquivamento, ou seja, armazenar "dados ativos" no banco de dados do Azure Cosmos e perder a validade "dados frios" muito[armazenamento de BLOBs do Azure](../storage/common/storage-introduction.md) ou [repositório Azure Data Lake](../data-lake-store/data-lake-store-overview.md).
* Implementar a análise em lote nos dados usando o [Apache Hadoop](run-hadoop-with-hdinsight.md).
* Implementar [pipelines lambda no Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) com o Azure Cosmos DB. O Azure Cosmos DB fornece uma solução de banco de dados escalonável que pode manipular a ingestão e a consulta, além de implementar arquiteturas lambda com baixo TCO. 
* Execute tooanother zero tempo de inatividade migrações conta de banco de dados do Azure Cosmos com um esquema de particionamento diferente.

**Pipelines lambda com o Azure Cosmos DB para ingestão e consulta:**

![Pipeline lambda baseado no Azure Cosmos DB para ingestão e consulta](./media/change-feed/lambda.png)

Você pode usar o banco de dados do Azure Cosmos tooreceive e armazenar dados de evento de dispositivos, sensores, infraestrutura e aplicativos e processar esses eventos em tempo real com [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), ou [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

Dentro de seu [sem servidor](http://azure.com/serverless) aplicativos web e móveis, você pode monitorar eventos como tootrigger de perfil, preferências ou local do cliente de tooyour alterações determinadas ações como dispositivo de envio por push notificações tootheir usando [As funções do azure](../azure-functions/functions-bindings-documentdb.md) ou [serviços de aplicativos](https://azure.microsoft.com/services/app-service/). Se você estiver usando o banco de dados do Azure Cosmos toobuild um jogo, você pode, por exemplo, usar tabelas em tempo real do feed tooimplement alterações com base em classificações de jogos concluídas.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>Como funciona o feed de alterações no Azure Cosmos DB
Banco de dados do Azure Cosmos fornece Olá capacidade tooincrementally ler as atualizações feitas tooan coleção do banco de dados do Azure Cosmos. Este feed alteração tem Olá propriedades a seguir:

* As alterações são persistentes no Azure Cosmos DB e podem ser processadas de forma assíncrona.
* Alterações toodocuments dentro de uma coleção estão disponíveis imediatamente no feed de alteração de saudação.
* Cada documento de tooa alteração aparece exatamente uma vez no feed de alteração de saudação e clientes gerenciem sua lógica de ponto de verificação. biblioteca de feed do processador de alteração Olá fornece verificação automática e "pelo menos uma vez" semântica.
* A mudança mais recente Olá somente para um determinado documento está incluída no log de alterações de saudação. As alterações intermediárias podem não estar disponíveis.
* Olá alteração feed é classificado por ordem de modificação em cada valor de chave de partição. Não há nenhuma garantia de ordem entre os valores de chave de partição.
* As alterações podem ser sincronizadas de qualquer ponto no tempo, ou seja, não há nenhum período de retenção de dados fixo para o qual haja alterações disponíveis.
* As alterações estão disponíveis em blocos de intervalos de chaves de partição. Esse recurso permite que as alterações de coleções grandes toobe processados em paralelo por vários consumidores/servidores.
* Os aplicativos podem solicitar para alterar vários feeds simultaneamente em Olá mesmo coleção.

O feed de alterações do Azure Cosmos DB é habilitado por padrão para todas as contas. Você pode usar o [taxa de transferência fornecida](request-units.md) em sua região de gravação ou em qualquer [ler região](distribute-data-globally.md) tooread de saudação alterar feed, assim como qualquer outra operação do banco de dados do Azure Cosmos. feed de alteração de saudação inclui inserções e operações de atualização feitas toodocuments na coleção de saudação. Você pode capturar exclusões ao definir um sinalizador de "exclusão reversível" em seus documentos em vez de exclusões. Como alternativa, você pode definir um período de validade finito para seus documentos por meio de saudação [recurso TTL](time-to-live.md), por exemplo, 24 horas e use Olá valor dessa propriedade toocapture exclui. Com essa solução, você tem alterações tooprocess dentro de um intervalo de tempo menor que o período de validade de TTL hello. Olá alteração feed está disponível para cada intervalo de chave de partição na coleção de saudação do documento e, portanto, pode ser distribuído em um ou mais consumidores para processamento paralelo. 

![Processamento distribuído do feed de alterações do Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

Você tem algumas opções para implementar um feed de alterações em seu código de cliente. Olá seções que imediatamente a seguir descrevem como tooimplement Olá feed de alteração usando hello Azure Cosmos DB REST API e Olá SDKs do DocumentDB. No entanto, para aplicativos .NET, recomendamos usar Olá novo [processador biblioteca de feed de alteração](#change-feed-processor) para eventos de processamento de saudação alterar feed como ele simplifica a alterações de leitura em partições e permite que vários threads trabalhando em paralelo. 

## <a id="rest-apis"></a>Trabalhando com hello API REST e SDKs do DocumentDB
O Azure Cosmos DB fornece contêineres elásticos de armazenamento e produtividade chamados **coleções**. Os dados em coleções são logicamente agrupados usando [chaves de partição](partition-data.md) para obtenção de escalabilidade e desempenho. O Azure Cosmos DB fornece várias APIs para acessar esses dados, incluindo pesquisa por ID (Read/Get), consulta e feeds de leitura (verificações). Olá feed de alteração pode ser obtida preenchendo dois nova solicitação cabeçalhos toohello documentos `ReadDocumentFeed` API e podem ser processadas em paralelo em intervalos de chaves de partição.

### <a name="readdocumentfeed-api"></a>API do ReadDocumentFeed
Vamos examinar o funcionamento do ReadDocumentFeed. Ler um feed de documentos em uma coleção por meio de saudação dá suporte a banco de dados do Azure Cosmos `ReadDocumentFeed` API. Por exemplo, hello solicitação a seguir retorna uma página de documentos dentro Olá `serverlogs` coleção. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Resultados podem ser limitados usando Olá `x-ms-max-item-count` cabeçalho e leituras podem ser retomado reenviando a solicitação de saudação com um `x-ms-continuation` cabeçalho é retornado na resposta anterior hello. Quando executado de um único cliente, `ReadDocumentFeed` itera resultados entre partições em série. 

**Leitura serial de feed de documento**

Você também pode recuperar o feed de saudação de documentos usando uma saudação suportada [SDKs do banco de dados do Azure Cosmos](documentdb-sdk-dotnet.md). Por exemplo, Olá trecho a seguir mostra como Olá toouse [ReadDocumentFeedAsync método](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) no .NET.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>Execução distribuída do ReadDocumentFeed
Para coleções que contêm terabytes de dados ou mais, ou um grande volume de atualizações de ingestão, a execução serial de feed de leitura de um único computador cliente pode não ser prática. Em ordem toosupport esses cenários de dados grande, Cosmos do Azure DB fornece APIs toodistribute `ReadDocumentFeed` chamadas de modo transparente entre vários leitores/consumidores de cliente. 

**Feed de Documento de Leitura Distribuída**

processamento escalonável de tooprovide de alterações incrementais, o banco de dados do Cosmos do Azure oferece suporte a um modelo de expansão para alteração de saudação feed API com base em intervalos de chaves de partição.

* Você pode obter uma lista de intervalos de chaves de partição para uma coleção que esteja executando uma chamada `ReadPartitionKeyRanges`. 
* Para cada intervalo de chave de partição, você pode realizar uma `ReadDocumentFeed` tooread documentos com chaves de partição dentro desse intervalo.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Recuperação de intervalos de chaves de partição para uma coleção
Você pode recuperar intervalos de chave de partição Olá Olá solicitante `pkranges` recursos dentro de uma coleção. Por exemplo hello solicitação a seguir recupera Olá lista de intervalos de chaves de partição para Olá `serverlogs` coleção:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

Essa solicitação retorna Olá resposta que contém metadados sobre intervalos de chave de partição Olá a seguir:

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


**Propriedades do intervalo de chave de partição**: cada intervalo de chave de partição inclui propriedades de metadados de saudação de saudação a tabela a seguir:

<table>
    <tr>
        <th>Nome do cabeçalho</th>
        <th>Descrição</th>
    </tr>
    <tr>
        <td>ID</td>
        <td>
            <p>Olá ID para o intervalo de chave de partição hello. É uma ID estável e exclusiva dentro de cada coleção.</p>
            <p>Deve ser usado em Olá as seguintes alterações de tooread chamada pelo intervalo de chave de partição.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>valor de hash da chave da partição máximo de Olá para o intervalo de chave de partição hello. Para uso interno.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>valor de hash da chave de partição mínima Olá para intervalo de chave de partição de saudação. Para uso interno.</td>
    </tr>       
</table>

Você pode fazer isso usando uma saudação suportada [SDKs do banco de dados do Azure Cosmos](documentdb-sdk-dotnet.md). Por exemplo, hello trecho a seguir mostra como os intervalos de chave de partição tooretrieve no .NET usando Olá [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) método.

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

Banco de dados do Azure Cosmos oferece suporte à recuperação de documentos por intervalo de chave de partição por configuração Olá opcional `x-ms-documentdb-partitionkeyrangeid` cabeçalho. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Execução de um ReadDocumentFeed incremental
ReadDocumentFeed dá suporte a saudação cenários/tarefas para processamento incremental de alterações no banco de dados do Azure Cosmos coleções a seguir:

* Ler todas as alterações toodocuments desde o início de Olá, ou seja, desde a criação de coleção.
* Ler todas as alterações toofuture atualizações toodocuments da hora atual, ou as alterações desde um tempo especificado pelo usuário.
* Ler toodocuments de todas as alterações de uma versão lógica da coleção de saudação (ETag). Você pode seus consumidores com base em Olá retornado ETag de solicitações de leitura de feed incrementais de ponto de verificação.

alterações de saudação incluem toodocuments inserções e atualizações. Exclui toocapture, você deve usar uma propriedade "exclusão reversível" em seus documentos, ou Olá [propriedade TTL interna](time-to-live.md) toosignal uma exclusão pendente no hello alterar feed.

Olá a seguinte tabela lista Olá [solicitação](/rest/api/documentdb/common-documentdb-rest-request-headers.md) e [cabeçalhos de resposta](/rest/api/documentdb/common-documentdb-rest-response-headers.md) para operações de ReadDocumentFeed.

**Cabeçalhos de solicitação para ReadDocumentFeed incremental**:

<table>
    <tr>
        <th>Nome do cabeçalho</th>
        <th>Descrição</th>
    </tr>
    <tr>
        <td>A-IM</td>
        <td>Deve ser definido de muito "feed Incremental", ou não especificado de outra forma</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>Nenhum cabeçalho: retorna todas as alterações de saudação começando (criação de coleção)</p>
            <p>"*": retorna todos os novos toodata alterações na coleção de saudação</p>         
            <p>&lt;ETag&gt;: se definir tooa coleção ETag, retorna todas as alterações feitas desde que timestamp lógico</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>Formato de hora RFC 1123; ignorado se If-None-Match for especificado</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>ID de intervalo de chave da partição de saudação de leitura de dados.</td>
    </tr>
</table>

**Cabeçalhos de resposta para ReadDocumentFeed incremental**:

<table> <tr>
        <th>Nome do cabeçalho</th>
        <th>Descrição</th>
    </tr>
    <tr>
        <td>etag</td>
        <td>
            <p>número de sequência lógica de Hello (LSN) do último documento retornado na resposta de saudação.</p>
            <p>O ReadDocumentFeed incremental pode ser retomado por meio do reenvio desse valor em If-None-Match.</p>
        </td>
    </tr>
</table>

Aqui está um tooreturn de solicitação de exemplo todas as alterações incrementais na coleção de versão/ETag Olá lógica `28535` e intervalo de chave de partição = `16`:

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

As alterações são ordenadas por vez em cada valor de chave de partição dentro do intervalo de chave de partição hello. Não há nenhuma garantia de ordem entre os valores de chave de partição. Se houver mais resultados que pode caber em uma única página, você pode ler a próxima página Olá de resultados reenviando a solicitação Olá com hello `If-None-Match` cabeçalho com toohello igual valor `etag` da resposta anterior hello. Se vários documentos foram inseridos ou atualizados transacionalmente dentro de um procedimento armazenado ou gatilho, eles serão todos os retornados em Olá mesmo página de resposta.

> [!NOTE]
> Com o feed de alteração, você pode obter mais itens retornados em uma página que o especificado na `x-ms-max-item-count` no caso de saudação de vários documentos inseridos ou atualizados dentro de procedimentos armazenados ou disparadores. 

Ao usar o hello .NET SDK (1.17.0), defina o campo Olá `StartTime` na `ChangeFeedOptions` documentos toodirectly retorno alterado desde `StartTime` ao chamar `CreateDocumentChangeFeedQuery`. Especificando `If-Modified-Since` usando Olá API REST, sua solicitação retorna não Olá documentos si, mas em vez disso, o token de continuação hello ou `etag` no cabeçalho de resposta de saudação. documentos de Olá tooreturn Olá modificado especificado tempo, o token de continuação Olá `etag` deve ser usado na próxima solicitação Olá com `If-None-Match` tooreturn Olá documentos reais. 

Olá .NET SDK fornece Olá [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) e [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) tooaccess alterações tooa coleção de classes auxiliares. Olá trecho a seguir mostra como tooretrieve todas as alterações desde o início do hello usando Olá SDK .NET de um único cliente.

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
E hello trecho a seguir mostra como tooprocess é alterado em tempo real com o banco de dados do Azure Cosmos usando Olá alterações de feed de suporte e Olá anterior de função. Olá primeira chamada retorna todos os documentos de saudação na coleção de saudação e Olá segundo só retorna Olá dois documentos criados que foram criados desde o último ponto de verificação de saudação.

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

Você também pode filtrar Olá alteração feed usando eventos do processo do cliente no lado do lógica tooselectively. Por exemplo, aqui está um trecho de código que usa o cliente lado LINQ tooprocess apenas eventos de alteração de temperatura de sensores de dispositivo.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>Biblioteca do processador do feed de alterações
Outra opção é Olá toouse [biblioteca Azure Cosmos DB alterar Feed processador](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), que podem ajudá-lo a facilmente distribuir o processamento de uma alteração de feed em vários consumidores de eventos. biblioteca de saudação é excelente para a criação de leitores de feed na plataforma .NET de saudação de alteração. Alguns fluxos de trabalho que seriam simplificados usando biblioteca de processador de Feed de alteração Olá sobre métodos de saudação incluídos no hello outros SDKs do banco de dados Cosmos incluem: 

* Efetuar pull de atualizações de feed de alterações quando os dados são armazenados em várias partições
* Movendo ou replicando dados de uma coleção tooanother
* Execução paralela de ações disparadas por toodata atualizações e alterações de feed 

Enquanto usar Olá APIs em Olá Cosmos SDKs fornece acesso preciso toochange feed atualizações em cada partição, usando biblioteca de processador de Feed de alteração de saudação simplifica as alterações de leitura em partições e vários threads de trabalho em paralelo. Em vez de ler manualmente as alterações de cada contêiner e salvar um token de continuação para cada partição, Olá alterar Feed do processador gerencia automaticamente as alterações de leitura em partições usando um mecanismo de concessão.

biblioteca de saudação está disponível como um pacote do NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) e de código-fonte como Github [exemplo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor). 

### <a name="understanding-change-feed-processor-library"></a>Noções básicas sobre a biblioteca do processador do feed de alterações 

Existem quatro componentes principais da implementação Olá alterar Feed do processador: Olá monitorado coleção, coleção de concessão hello, host de processador hello e consumidores de saudação. 

**Coleta monitorada:** coleção Olá monitorado é dados de saudação do qual Olá alteração feed é gerado. Qualquer coleção toohello monitorado inserções e as alterações são refletidas no feed de alteração de saudação da coleção de saudação. 

**Coleção de concessão:** Olá coordenadas de coleção de concessão alteração Olá feed entre vários trabalhadores de processamento. Uma coleção separada é toostore usado concessões de saudação com uma concessão por partição. É vantajoso toostore esta coleção de concessão em uma conta diferente com hello gravar Olá toowhere próximo região processador de Feed de alteração está em execução. Um objeto de concessão contém Olá seguintes atributos: 
* Proprietário: Especifica o host de saudação que possui a concessão de saudação
* Continuação: Especifica a posição de saudação (token de continuação) na alteração Olá feed para uma determinada partição
* Timestamp: Hora da última concessão foi atualizada; Olá timestamp pode ser usado toocheck se a concessão de saudação é considerado expirado 

**Host de processador:** cada host determina quantos tooprocess de partições com base em quantos outras instâncias de hosts têm concessões ativas. 
1.  Quando um host é iniciado, ele adquire cargas de trabalho concessões toobalance Olá em todos os hosts. Um host renova concessões periodicamente para que as concessões permaneçam ativas. 
2.  Uma host pontos de verificação Olá última continuação tooits token concessão para cada leitura. tooensure simultaneidade, um host de verificações de segurança hello ETag para cada atualização de concessão. Também há suporte para outras estratégias de ponto de verificação.  
3.  Durante o desligamento, um host libera todas as concessões mas mantém Olá informações de continuação, para que ele possa retomar a leitura do ponto de verificação armazenado hello mais tarde. 

No momento o número de saudação de hosts não pode ser maior que o número de saudação de partições (concessões).

**Os consumidores:** workers, ou os consumidores são os threads que executam alteração Olá feed processamento iniciado por cada host. Cada host de processador pode ter vários consumidores. Cada consumidor lê o feed de alteração de saudação do hello partição é atribuída tooand notifica o host de alterações e expirado concessões.

toofurther compreender como esses quatro elementos do processador de Feed de alteração de trabalham juntos, vamos examinar um exemplo hello diagrama a seguir. Olá monitorado coleção armazena documentos e usa city"hello" como chave de partição hello. Podemos ver que partição Olá azul contém documentos com campo de "city" hello de "E um" e assim por diante. Há dois hosts, cada um com dois consumidores lendo de partições Olá quatro em paralelo. Olá setas mostram a consumidores Olá lendo de um ponto específico no hello alterar feed. Na primeira partição do hello, azul mais escuro Olá representa alterações não lidas enquanto azul-claro Olá representa Olá já ler alterações no feed de alteração de saudação. hosts de saudação usam Olá concessão coleção toostore uma faixa de tookeep "continuação" valor de saudação atual de leitura de posição de cada consumidor. 

![Usando a alteração do banco de dados do Azure Cosmos Olá alimentação de host de processador](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>Usando a Biblioteca do processador do feed de alterações 
Olá seção a seguir explica como toouse Olá biblioteca de processador de Feed de alteração no contexto de saudação de replicar as alterações de uma coleção de destino de tooa de coleção de origem. Aqui, a coleção de origem Olá é coleção Olá monitorado no processador de Feed de alteração. 

**Instalar e incluir o pacote de NuGet de processador de Feed de alteração de saudação** 

Antes de instalar o Pacote NuGet do Processador do feed de alterações, instale: 
* Microsoft.Azure.DocumentDB, versão 1.13.1 ou superior 
* Newtonsoft.Json, versão 9.0.1 ou superior. Instale `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` e o inclua como uma referência.

**Criar uma coleção monitorada, uma coleção de destino e uma coleção de concessão** 

Saudação de toouse ordem biblioteca de processador de Feed de alteração, coleção de concessão Olá precisa toobe criado antes de executar o (s) processador de saudação. Novamente, é recomendável armazenar uma coleção de concessão em uma conta diferente com uma saudação de toowhere gravação região mais próxima que alteração de Feed de processador está sendo executado. Neste exemplo de movimentação de dados, precisamos de coleção de destino Olá toocreate antes de executar o host de processador de Feed de alteração de saudação. No código de exemplo hello, podemos chamar uma saudação de toocreate método auxiliar monitorada, concedida e as coleções de destino se eles ainda não existir. 

> [!WARNING]
> Criando uma coleção tem preços implicações, como reservar a taxa de transferência para Olá toocommunicate de aplicativo com o banco de dados do Azure Cosmos. Para obter mais detalhes, visite Olá [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*Criando um host de processador*

Olá `ChangeFeedProcessorHost` classe fornece um ambiente de tempo de execução do thread-safe, vários processos, seguro para implementações de processador de evento que também fornece gerenciamento de concessão de ponto de verificação e partição. Olá toouse `ChangeFeedProcessorHost` classe, você pode implementar `IChangeFeedObserver`. Essa interface contém três métodos:

* `OpenAsync`: essa função é chamada quando o observador do feed de alterações é aberto. Pode ser modificado tooperform uma ação específica ao consumidor/observador é aberto.  
* `CloseAsync`: essa função é chamada quando o observador do feed de alterações é terminado. Pode ser modificado tooperform uma ação específica ao consumidor/observador está fechado.  
* `ProcessChangesAsync`: essa função é chamada quando novas alterações de documento estão disponíveis no feed de alterações. Ele pode ser modificado tooperform uma ação específica após cada atualização de alteração de feed.  

Em nosso exemplo, implementamos interface Olá `IChangeFeedObserver` por meio de saudação `DocumentFeedObserver` classe. Aqui, Olá `ProcessChangesAsync` upserts (atualizações) um documento de alteração de feed na coleção de destino de saudação de função. Este exemplo é útil para mover dados de uma coleção tooanother na chave de partição de saudação de toochange de ordem de um conjunto de dados. 

*Executando Olá Host de processador*

Antes de começar o processamento de eventos, as opções do feed de alterações e as opções de host do feed de alterações podem ser personalizadas. 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
campos específicos de saudação que podem ser personalizados são resumidos na Olá tabelas a seguir. 

**Opções do feed de alterações**:
<table>
    <tr>
        <th>Nome da Propriedade</th>
        <th>Descrição</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Obtém ou define o número máximo de saudação do toobe de itens retornado na operação de enumeração Olá no serviço de banco de dados do banco de dados do Azure Cosmos de saudação.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Obtém ou define a id de intervalo de chave da partição para a solicitação atual Olá Olá no serviço de banco de dados do banco de dados do Azure Cosmos hello.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Obtém ou define o token de continuação Olá solicitação no serviço de banco de dados do banco de dados do Azure Cosmos hello.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>Obtém ou define o token de sessão Olá para uso com a coerência de sessão no serviço de banco de dados do banco de dados do Azure Cosmos de saudação.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Obtém ou define se a alteração de feed no serviço de banco de dados do banco de dados do Azure Cosmos Olá deve começar de Olá começando (true) ou do atual (false). Por padrão, ele inicia do local atual (false).</td>
    </tr>
</table>

**Opções do host do feed de alterações**:
<table>
    <tr>
        <th>Nome da Propriedade</th>
        <th>Tipo</th>
        <th>Descrição</th>
    </tr>
    <tr>
        <td>LeaseRenewInterval</td>
        <td>TimeSpan</td>
        <td>intervalo de saudação para todas as concessões para partições mantidos atualmente pela instância de ChangeFeedEventHost hello.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>TimeSpan</td>
        <td>Olá intervalo tookick off toocompute uma tarefa se partições são distribuídas uniformemente entre as instâncias do host conhecido.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>TimeSpan</td>
        <td>intervalo de saudação para qual Olá concessão é obtida em uma concessão que representa uma partição. Se a concessão de saudação não for renovada dentro deste intervalo, expirou e propriedade de partição Olá move tooanother ChangeFeedEventHost instância.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>TimeSpan</td>
        <td>atraso de saudação entre a sondagem de uma partição para as novas alterações no hello feed depois que todas as alterações atuais serão descarregadas.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>Olá concessões de toocheckpoint de frequência.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>int</td>
        <td>Contagem de partição mínima Olá para o host de saudação.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>int</td>
        <td>número máximo de saudação do host de saudação de partições pode atender.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>Bool</td>
        <td>Se na saudação de início do host de saudação todas as concessões existentes deve ser excluído e host Olá deve começar do zero.</td>
    </tr>
</table>


toostart processamento de eventos, instanciar `ChangeFeedProcessorHost`, fornecendo os parâmetros adequados Olá para sua coleção de banco de dados do Azure Cosmos. Em seguida, chame `RegisterObserverAsync` tooregister sua `IChangeFeedObserver` implementação (DocumentFeedObserver neste exemplo) com o tempo de execução de saudação. Neste ponto, o host Olá tentativas tooacquire uma concessão em cada intervalo de chave de partição na coleção de banco de dados do Azure Cosmos hello usando um algoritmo de "greedy". Essas concessões duram por determinado período e, em seguida, devem ser renovadas. Como novos nós, instâncias de trabalho, nesse caso, ficam online, eles usam reservas de concessão e ao longo do tempo carga Olá alterna entre os nós como cada host tenta tooacquire mais concessões. 

No código de exemplo hello, usamos um toocreate (DocumentFeedObserverFactory.cs) de classe de fábrica um observador e hello `RegistObserverFactoryAsync` tooregister observador de saudação. 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
Ao longo do tempo, é estabelecido um equilíbrio. Esse recurso dinâmico permite que a CPU com base em tooconsumers toobe aplicado o dimensionamento automático, para ampliar e reduzir. Se as alterações estão disponíveis no banco de dados do Azure Cosmos a uma taxa mais rápida que os consumidores possam processar, Olá aumento de CPU nos consumidores pode ser usado toocause um dimensionamento automático na contagem de instâncias de trabalho.

## <a name="next-steps"></a>Próximas etapas
* Tente Olá [alteração de banco de dados do Azure Cosmos feed exemplos de código no GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Introdução a codificação com hello [SDKs do banco de dados do Azure Cosmos](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/).
