---
title: 'Cosmos do Azure DB: Desenvolver com hello API DocumentDB no .NET | Microsoft Docs'
description: Saiba como toodevelop com a API de documentos do Azure Cosmos DB usando .NET
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a>Azure CosmosDB: Desenvolver com hello API DocumentDB no .NET

O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente. 

Este tutorial demonstra como toocreate uma conta de banco de dados do Azure Cosmos usando Olá portal do Azure e, em seguida, criar um banco de dados de documento e uma coleção com uma [chave de partição](documentdb-partition-data.md#partition-keys) usando Olá [API .NET do DocumentDB](documentdb-introduction.md). Ao definir uma chave de partição quando você cria uma coleção, seu aplicativo preparado tooscale facilmente conforme o aumento dos dados. 

Seguir Olá tutorial abrange tarefas usando Olá [API .NET do DocumentDB](documentdb-sdk-dotnet.md):

> [!div class="checklist"]
> * Criar uma conta do Azure Cosmos DB
> * Criar um banco de dados e uma coleção com uma chave de partição
> * Criar documentos JSON
> * Atualizar um documento
> * Consultar coleções particionadas
> * Executar procedimentos armazenados
> * Excluir um documento
> * Excluir um banco de dados

## <a name="prerequisites"></a>Pré-requisitos
Verifique se que você tem o seguinte hello:

* Uma conta ativa do Azure. Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/). 
    * Como alternativa, você pode usar o hello [emulador de banco de dados do Azure Cosmos](local-emulator.md) para este tutorial se você gostaria que toouse um ambiente local que emula os serviços do Azure DocumentDB Olá para fins de desenvolvimento.
* [Visual Studio](http://www.visualstudio.com/).

## <a name="create-an-azure-cosmos-db-account"></a>Criar uma conta do Azure Cosmos DB

Vamos começar criando uma conta de banco de dados do Azure Cosmos em Olá portal do Azure.

> [!TIP]
> * Já tem uma conta do Azure Cosmos DB? Nesse caso, pular muito[configurar sua solução do Visual Studio](#SetupVS)
> * Você tinha uma conta do Azure DocumentDB? Se assim, sua conta agora é uma conta de banco de dados do Azure Cosmos e poderá pular muito[configurar sua solução do Visual Studio](#SetupVS).  
> * Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar sua solução do Visual Studio](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Configurar sua solução do Visual Studio
1. Abra o **Visual Studio** no seu computador.
2. Em Olá **arquivo** menu, selecione **novo**e, em seguida, escolha **projeto**.
3. Em Olá **novo projeto** caixa de diálogo, selecione **modelos** / **Visual C#** / **aplicativo de Console (.NET Framework)**, nomeie o projeto e, em seguida, clique em **Okey**.
   ![Captura de tela da janela do novo projeto de saudação](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)

4. Em Olá **Solution Explorer**, clique com o botão direito no seu novo aplicativo de console, que está em sua solução do Visual Studio, e, em seguida, clique em **gerenciar pacotes NuGet...**
    
    ![Captura de tela de saudação à direita Menu clicado para Olá projeto](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. Em Olá **NuGet** , clique em **procurar**e o tipo **documentdb** na caixa de pesquisa de saudação.
<!---stopped here--->
6. Nos resultados de saudação localizar **Microsoft.Azure.DocumentDB** e clique em **instalar**.
   ID do pacote Olá Olá biblioteca de cliente de banco de dados do Azure Cosmos é [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).
   ![Captura de tela de saudação Menu do NuGet para localizar o SDK de cliente de banco de dados do Azure Cosmos](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)

    Se você receber uma mensagem sobre Analisando alterações toohello solução, clique em **Okey**. Se receber uma mensagem sobre a aceitação da licença, clique em **Aceito**.

## <a id="Connect"></a>Adicionar referências tooyour projeto
Olá restantes etapas para este tutorial forneça Olá API DocumentDB código trechos de código toocreate e atualização Azure Cosmos DB recursos necessários em seu projeto.

Primeiro, adicione o aplicativo de tooyour essas referências.
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <a id="add-references"></a>Conecte seu aplicativo

Em seguida, adicione essas duas constantes e sua variável de *cliente* no seu aplicativo.

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

Em seguida, head fazer toohello [portal do Azure](https://portal.azure.com) tooretrieve sua URL de ponto de extremidade e a chave primária. URL de ponto de extremidade de saudação e a chave primária são necessárias para seu aplicativo toounderstand onde tooconnect e para o banco de dados do Azure Cosmos tootrust conexão do seu aplicativo.

Olá portal do Azure, navegue conta de banco de dados do Azure Cosmos tooyour em, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**.

Copiar Olá URI do portal de saudação e cole-o sobre `<your endpoint URL>` no arquivo program.cs de saudação. Cópia Olá chave primária do portal hello e cole-o sobre `<your primary key>`. Ser Olá-se de tooremove `<` e `>` de seus valores.

![Captura de tela de saudação portal do Azure usado pelo Olá NoSQL tutorial toocreate um aplicativo de console c#. Mostra uma conta de banco de dados do Azure Cosmos, com hello chaves realçadas na folha de conta do banco de dados do Azure Cosmos Olá, Olá URI e valores de chave primária realçados na folha de chaves Olá](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <a id="instantiate"></a>Criar uma instância de saudação DocumentClient

Agora, crie uma nova instância da saudação **DocumentClient**.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <a id="create-database"></a>Criar um banco de dados

Em seguida, crie um banco de dados do Azure Cosmos [banco de dados](documentdb-resources.md#databases) usando Olá [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método ou [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método hello ** DocumentClient** classe da saudação [SDK .NET do DocumentDB](documentdb-sdk-dotnet.md). Um banco de dados é um contêiner lógico de saudação do armazenamento de documentos JSON particionado em coleções.

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a>Escolha uma chave de partição 

Coleções são contêineres para armazenamento de documentos. Elas são recursos lógicos e podem [abranger uma ou mais partições físicas](partition-data.md). Um [chave de partição](documentdb-partition-data.md) é uma propriedade (ou caminho) em documentos que é usado toodistribute seus dados entre os servidores de saudação ou partições. Todos os documentos com hello a mesma chave de partição são armazenados em Olá mesma partição. 

Determinação de uma chave de partição é uma decisão importante toomake antes de criar uma coleção. Chaves de partição são uma propriedade (ou caminho) em documentos que podem ser usado pelo banco de dados do Azure Cosmos toodistribute seus dados entre vários servidores ou partições. Cosmos DB hashes de valor de chave de partição hello e usa partição de Olá Olá hash resultados toodetermine na qual documento de saudação toostore. Olá a todos os documentos com hello a mesma chave de partição são armazenados na mesma partição e chaves de partição não podem ser alteradas depois que uma coleção é criada. 

Para este tutorial, vamos chave de partição Olá tooset muito`/deviceId` assim que Olá todos os dados de saudação para um único dispositivo é armazenado em uma única partição. Você deseja toochoose uma chave de partição que tem um grande número de valores, cada um dos quais são usados no sobre Olá mesma frequência tooensure Cosmos DB pode balancear a carga que seus dados crescem e alcançar a taxa de transferência total de coleção Olá Olá. 

Para obter mais informações sobre particionamento, consulte [como toopartition e escala no banco de dados do Azure Cosmos?](partition-data.md) 

## <a id="CreateColl"></a>Criar uma coleção 

Agora que sabemos que nossa chave da partição, `/deviceId`, permite criar um [coleção](documentdb-resources.md#collections) usando Olá [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método ou [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método hello **DocumentClient** classe. Uma coleção é um contêiner de documentos JSON e qualquer lógica de aplicativo JavaScript associada. 

> [!WARNING]
> Criando uma coleção tem preços implicações, como reservar a taxa de transferência para Olá toocommunicate de aplicativo com o banco de dados do Azure Cosmos. Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

Esse método torna a uma API REST chame tooAzure Cosmos DB e Olá provisões de serviço um número de partições com base na taxa de transferência solicitada hello. Você pode alterar a taxa de transferência de saudação de uma coleção como o desempenho precisa evoluir usando Olá SDK ou hello [portal do Azure](set-throughput.md).

## <a id="CreateDoc"></a>Criar documentos JSON
Vamos inserir alguns documentos JSON no Azure Cosmos DB. Um [documento](documentdb-resources.md#documents) podem ser criados usando Olá [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método hello **DocumentClient** classe. Os documentos são conteúdo JSON (arbitrário) definido pelo usuário. Essa classe de exemplo contém uma leitura do dispositivo e tooinsert de tooCreateDocumentAsync uma chamada de um novo dispositivo de leitura em uma coleção.

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

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
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
## <a name="read-data"></a>Ler dados

Vamos ler o documento de saudação por sua chave de partição e Id usando o método de ReadDocumentAsync hello. Observe que as leituras de saudação incluem um valor de PartitionKey (correspondente toohello `x-ms-documentdb-partitionkey` cabeçalho de solicitação na Olá API REST).

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a>Atualizar dados

Agora vamos atualizar alguns dados usando o método de ReplaceDocumentAsync hello.

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a>Excluir dados

Agora permite excluir um documento com chave de partição e id usando o método de DeleteDocumentAsync hello.

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a>Consultar coleções particionadas

Quando você consulta dados em coleções particionadas, o banco de dados do Azure Cosmos automaticamente rotas Olá partições toohello de consulta correspondente valores de chave de partição do toohello especificados no filtro de saudação (se houver). Por exemplo, esta consulta é roteado toojust Olá partição contendo Olá chave de partição "XMS-0001".

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

## <a name="parallel-query-execution"></a>Execução de consulta paralela
Olá SDKs do DocumentDB do Azure Cosmos DB 1.9.0 e acima do opções de execução de consulta paralela, que permitem que você tooperform baixa latência as consultas em coleções particionadas, mesmo quando eles precisarem de tootouch um grande número de partições. Por exemplo, Olá consulta a seguir é toorun configurado em paralelo entre partições.

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Você pode gerenciar a execução de consulta paralela ajustando Olá parâmetros a seguir:

* Definindo `MaxDegreeOfParallelism`, você pode controlar o grau de paralelismo, ou seja, Olá de número máximo de partições da coleção de rede simultâneas conexões toohello Olá. Se você definir muito-1, o grau de paralelismo Olá é gerenciado pelo Olá SDK. Se hello `MaxDegreeOfParallelism` não for especificado ou definido too0, que é o valor padrão de saudação, haverá partições de uma única rede conexão toohello coleção.
* Definindo `MaxBufferedItemCount`, você pode compensar a latência da consulta e a utilização da memória no lado do cliente. Se você omite esse parâmetro ou defina muito-1, número de saudação de itens em buffer durante a execução de consulta paralela é gerenciado pelo Olá SDK.

Considerando Olá mesmo estado da coleção hello, uma consulta paralela retornará resultados Olá mesma ordem como em execução em série. Ao executar uma consulta entre partições que inclui a classificação (ORDER BY e/ou superior), Olá SDK do DocumentDB emite a consulta de saudação em paralelo em partições e mescla resultados parcialmente classificados no hello cliente lado tooproduce resultados ordenados globalmente.

## <a name="execute-stored-procedures"></a>Executar procedimentos armazenados
Por fim, você pode executar transações atômicas em relação a documentos com hello a mesma ID de dispositivo, por exemplo, se você estiver mantendo agregações ou Olá estado mais recente de um dispositivo em um único documento adicionando Olá projeto tooyour de código a seguir.

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

E isso é tudo! Esses são os principais componentes de saudação de um aplicativo de banco de dados do Azure Cosmos que usa uma distribuição de dados de escala de tooefficiently chave de partição em partições.  

## <a name="clean-up-resources"></a>Limpar recursos

Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este tutorial Olá portal do Azure com hello etapas a seguir:

1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e, em seguida, clique em nome exclusivo de saudação do recurso Olá criado. 
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello: 

> [!div class="checklist"]
> * Criou uma conta do Azure Cosmos DB
> * Criou um banco de dados e uma coleção com uma chave de partição
> * Criou documentos JSON
> * Atualizou um documento
> * Consultou coleções particionadas
> * Executou um procedimento armazenado
> * Excluiu um documento
> * Excluiu um banco de dados

Você pode continuar toohello tutorial de Avançar e importar a conta de banco de dados do Cosmos tooyour dados adicionais. 

> [!div class="nextstepaction"]
> [Importar dados no Azure Cosmos DB](import-data.md)
