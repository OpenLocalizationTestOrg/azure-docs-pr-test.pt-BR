---
title: aaaPartitioning e escalonamento horizontal no banco de dados do Azure Cosmos | Microsoft Docs
description: "Saiba mais sobre como particionamento funciona no banco de dados do Azure Cosmos, como particionamento tooconfigure e chaves de partição e como toopick Olá direito chave da partição para seu aplicativo."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: cac9a8cd-b5a3-4827-8505-d40bb61b2416
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87d56db8c4ccc6b94b1650baff0fcfb3db6d1777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopartition-and-scale-in-azure-cosmos-db"></a>Como toopartition e escala no banco de dados do Azure Cosmos

[Banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) é toohelp de serviço criado um banco de dados distribuído, vários modelos global você alcançar desempenho rápido e previsível e escalabilidade perfeitamente junto com seu aplicativo à medida que cresce. Este artigo fornece uma visão geral de como o particionamento funciona para todos os dados de saudação modelos no banco de dados do Azure Cosmos e descreve como você pode configurar escala do banco de dados do Azure Cosmos contêineres tooeffectively seus aplicativos.

O particionamento e as chaves de partição também são abordados neste vídeo do Azure Friday com Scott Hanselman e o gerente de engenharia principal do BD Cosmos do Azure, Shireesh Thota.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Particionamento no BD Cosmos do Azure
No BD Cosmos do Azure, você pode armazenar e consultar dados sem esquema com tempos de resposta da ordem de milissegundos em qualquer escala. O BD Cosmos fornece contêineres para o armazenamento de dados chamados **coleções (para documentos), gráficos ou tabelas**. Contêineres são recursos lógicos e podem abranger um ou mais servidores ou partições físicas. número de saudação de partições é determinado pelo banco de dados do Cosmos com base no tamanho do armazenamento hello e taxa de transferência fornecida do contêiner Olá Olá. Cada partição no DB Cosmos tem uma quantidade fixa de armazenamento com suporte de SSD associado a ela e é replicada para alta disponibilidade. Gerenciamento de partição é totalmente gerenciado pelo banco de dados do Azure Cosmos, e você não tem código complexo toowrite ou gerenciar as partições. Os contêineres do BD Cosmos são ilimitados em termos de armazenamento e taxa de transferência. 

![horizontal](./media/introduction/azure-cosmos-db-partitioning.png) 

O particionamento é um aplicativo tooyour transparente. Dá suporte a cosmos DB rápidas leituras e gravações, consultas, lógica transacional, níveis de consistência e controle de acesso refinado por meio do recurso de contêiner único tooa métodos/APIs. identificadores de serviço Olá roteamento partição correta de toohello de solicitações de consulta e a distribuição de dados entre partições. 

Como o particionamento funciona? Cada item deve ter uma chave de partição e uma chave de linha, que o identificam exclusivamente. Sua chave de partição atua como uma partição lógica para seus dados e fornece ao BD Cosmos um limite natural para a distribuição de dados entre partições. De forma resumida, veja como o particionamento funciona no BD Cosmos do Azure:

* Você pode provisionar um contêiner do BD Cosmos com uma taxa de transferência de `T` solicitações/s
* Em segundo plano hello, partições de provisões Cosmos DB necessário tooserve `T` solicitações/s. Se `T` for maior do que a taxa de transferência máxima por partição Olá `t`, então Cosmos DB provisiona `N`  =  `T/t` partições
* Cosmos DB aloca espaço Olá da chave de partição hashes chave uniformemente em Olá `N` partições. Sendo assim, cada partição (partição física) hospeda 1-N valores de chave de partição (partições lógicas)
* Quando uma partição física `p` atingir seu limite de armazenamento, banco de dados do Cosmos perfeitamente divide `p` em duas novas partições `p1` e `p2` e distribui valores correspondentes tooroughly metade Olá chaves tooeach de saudação partições. Essa operação de divisão é aplicativo tooyour invisível.
* Da mesma forma, quando você provisionar taxa de transferência maior `t*N` taxa de transferência, Cosmos DB divide uma ou mais das sua partições toosupport Olá maior taxa de transferência

semântica de saudação para chaves de partição é semântica de saudação toomatch ligeiramente diferentes de cada API, conforme mostrado no Olá a tabela a seguir:

| API | Chave de partição | Chave de linha |
| --- | --- | --- |
| DocumentDB | caminho da chave de partição personalizada | `id` fixo | 
| MongoDB | chave de fragmentação personalizada  | `_id` fixo | 
| Gráfico | propriedade da chave de partição personalizada | `id` fixo | 
| Tabela | `PartitionKey` fixo | `RowKey` fixo | 

O BD Cosmos usa o particionamento baseado em hash. Quando você escreve um item, Cosmos DB hashes valor de chave de partição hello e use Olá hash resultado toodetermine qual partição toostore Olá item. Repositórios cosmos DB Olá todos os itens com a mesma chave de partição no hello mesma partição física. opção de Olá Olá chave de partição é uma decisão importante que você tenha toomake em tempo de design. Você deve escolher um nome de propriedade que tenha uma ampla gama de valores e tenha padrões de acesso uniformes.

> [!NOTE]
> É um toohave de prática recomendada uma chave de partição com muitos valores distintos (100s 1000 no mínimo).
>

Os contêineres do BD Cosmos do Azure podem ser criados como "fixos" ou "ilimitados". Contêineres de tamanho fixo têm um limite máximo de 10 GB e taxa de transferência de 10.000 RU/s. Algumas APIs permitem toobe de chave de partição Olá omitido para contêineres de tamanho fixo. toocreate um contêiner como ilimitado, você deve especificar uma taxa de transferência mínima de 2500 RU/s.

## <a name="partitioning-and-provisioned-throughput"></a>Particionamento e produtividade provisionada
O BD Cosmos foi projetado para ter um desempenho previsível. Quando cria um contêiner, você reserva a taxa de transferência em termos de **[RUs](request-units.md) (unidades de solicitação) por segundo, com um complemento potencial de RUs por minuto**. Cada solicitação é atribuída um encargo de unidade de solicitação que é proporcional toohello quantidade de recursos do sistema como CPU, memória e e/s consumida pela operação de saudação. Uma leitura de um documento de 1 KB com consistência de sessão consome uma unidade de solicitação. Uma leitura é 1 RU, independentemente do número de saudação de itens armazenados ou Olá o número de solicitações simultâneas em execução no hello simultaneamente. Itens maiores exigem mais unidades de solicitação, dependendo do tamanho de saudação. Se você souber o tamanho de saudação de suas entidades e Olá número de leituras necessárias toosupport para seu aplicativo, você pode provisionar quantidade exata de saudação de taxa de transferência necessária para seu aplicativo do Leia precisa. 

> [!NOTE]
> tooachieve Olá taxa de transferência total do contêiner hello, você deve escolher uma chave de partição que permite que você tooevenly distribui solicitações entre alguns valores de chave de partição distintos.
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-hello-azure-cosmos-db-apis"></a>Trabalhando com hello APIs de banco de dados do Azure Cosmos
Você pode usar o hello portal do Azure ou contêineres de toocreate CLI do Azure e dimensione-los a qualquer momento. Esta seção mostra como contêineres toocreate e especifique a saudação taxa de transferência e a partição de definição de chave em cada Olá suporte para APIs.

### <a name="documentdb-api"></a>API do DocumentDB
saudação de exemplo a seguir mostra como toocreate um contêiner (coleção) usando Olá API DocumentDB. Você pode encontrar mais detalhes em [Particionamento com a API do DocumentDB](partition-data.md).

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

Você pode ler um item (documento) usando Olá `GET` Olá API REST ou usando o método `ReadDocumentAsync` em uma saudação SDKs.

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>API do MongoDB
Com hello MongoDB API, você pode criar uma coleção fragmentada por meio de sua ferramenta favorita, o driver ou o SDK. Neste exemplo, usamos Olá Shell Mongo para a criação de coleção de saudação.

Em Olá Shell Mongo:

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
Resultados:

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a>API de Tabela

Com hello API de tabela, você especificar taxa de transferência Olá para tabelas na configuração de appSettings Olá para seu aplicativo:

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

Em seguida, você criar uma tabela usando o SDK de armazenamento de tabela do Azure hello. chave de partição Olá é implicitamente criado como Olá `PartitionKey` valor. 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

Você pode recuperar uma única entidade utilizando Olá trecho de código a seguir:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
Consulte [desenvolvendo com hello API tabela](tutorial-develop-table-dotnet.md) para obter mais detalhes.

### <a name="graph-api"></a>Graph API

Com hello API do Graph, você deve usar o hello portal do Azure ou contêineres de toocreate CLI. Como alternativa, como o banco de dados do Azure Cosmos vários modelo, você pode usar a uma saudação toocreate outros modelos e dimensionar seu contêiner de gráfico.

Você pode ler qualquer vértice ou usando a chave de partição hello e id no Gremlin de borda. Por exemplo, para um gráfico com a região ("EUA") como chave de partição hello e "Seattle" como chave de linha de saudação, você pode encontrar um vértice usando Olá sintaxe a seguir:

```
g.V(['USA', 'Seattle'])
```

Mesmo com as margens, você pode referenciar uma borda usando a chave de partição hello e chave de linha.

```
g.E(['USA', 'I5'])
```

Consulte [Suporte do Gremlin para o BD Cosmos](gremlin-support.md) para obter mais detalhes.


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>Design de particionamento
tooscale efetivamente com o banco de dados do Azure Cosmos, você precisa toopick uma chave de partição boa quando você criar o contêiner. Há dois aspectos principais a considerar ao escolher uma chave de partição:

* **Limite de consulta e transações**: sua opção de chave de partição deve equilibrar suas entidades de uso de saudação do hello necessidade tooenable de transações em Olá requisito toodistribute em vários tooensure de chaves de partição uma solução escalonável. De um lado, você pode definir Olá mesma chave de partição para todos os itens, mas isso pode limitar a escalabilidade de saudação de sua solução. Em Olá outro lado, você pode atribuir uma chave de partição exclusivo para cada item, o que seria altamente escalonável, mas poderia impedir o uso de transações entre documentos por meio de procedimentos armazenados e gatilhos. Uma chave de partição ideal é um que permite consultas eficientes toouse e que tem cardinalidade suficiente tooensure sua solução é escalável. 
* **Afunilamentos de desempenho e armazenamento**: é importante toopick uma propriedade que permite grava toobe distribuído entre vários valores distintos. Solicitações toohello a mesma chave de partição não pode exceder a taxa de transferência de saudação de uma única partição e são limitados. Portanto, é importante toopick uma chave de partição não resulta em "pontos de acesso" dentro de seu aplicativo. Desde que todos os dados de saudação para uma chave de partição única deve ser armazenada em uma partição, também é recomendável tooavoid chaves de partição com grandes volumes de dados para Olá mesmo valor. 

Vejamos alguns cenários do mundo real e boas chaves de partição para cada um deles:
* Se você estiver implementando um perfil de usuário back-end, ID de usuário de saudação é uma boa escolha para chave de partição.
* Se você estiver armazenando dados de IoT, por exemplo, o estado do dispositivo, uma ID do dispositivo será uma boa opção para a chave de partição.
* Se você estiver usando o banco de dados do Azure Cosmos para registrar em log dados de série temporal, Olá, em seguida, o nome do host ou o ID do processo é uma boa escolha para chave de partição.
* Se você tiver uma arquitetura de multilocatária, ID de locatário Olá é uma boa escolha para chave de partição.

Em alguns casos como IoT de uso e perfis de usuário, chave de partição Olá pode ser Olá mesmo como o id (chave de documento). Em outros, como dados de série temporal hello, você pode ter uma chave de partição que é diferente da id de saudação.

### <a name="partitioning-and-loggingtime-series-data"></a>Dados de particionamento e registro em log/da série temporal
Um dos casos de uso comuns saudação do banco de dados do Cosmos é para registro em log e telemetria. É importante toopick uma chave de partição boa desde que talvez seja necessário tooread/gravação grandes volumes de dados. Escolha de saudação depende de sua leitura e gravação taxas e tipos de consultas que você espera que toorun. Aqui estão algumas dicas sobre como toochoose uma chave de partição válida.

* Se o caso de uso envolve uma pequena taxa de gravações acumular por um longo período de tempo e tooquery necessidade por intervalos de carimbos e outros filtros, e em seguida, usando um pacote cumulativo de saudação carimbo de hora, por exemplo, data como uma chave de partição é uma boa abordagem. Isso permite que você tooquery em todos os dados de saudação de uma data de uma única partição. 
* Se sua carga de trabalho for intensa em termos de gravação, o que é mais comum, você deverá usar uma chave de partição que não esteja baseada em carimbo de data/hora para que o BD Cosmos possa distribuir as gravações uniformemente entre várias partições. Aqui, um nome do host, ID do processo, ID da atividade ou outra propriedade com alta cardinalidade é uma boa opção. 
* Uma terceira abordagem é um híbrido um onde você tem vários contêineres, uma para cada dia/mês e chave de partição Olá é uma propriedade granular como nome do host. Isso tem o benefício de saudação que você pode definir a taxa de transferência diferente com base na janela de tempo de saudação, por exemplo, recipiente Olá Olá mês atual está provisionado com maior taxa de transferência desde que ele serve leituras e gravações, enquanto os meses anteriores com reduzir a taxa de transferência desde eles servem apenas leituras.

### <a name="partitioning-and-multi-tenancy"></a>Particionamento e multilocação
Se você estiver implementando um aplicativo multilocatário usando o BD Cosmos, haverá dois padrões populares – uma chave de uma partição por locatário e um contêiner por locatário. Aqui estão os profissionais de saudação e desvantagens de cada um:

* Uma chave de partição por locatário: nesse modelo, os locatários são colocados em um único contêiner. No entanto, consultas e inserções de itens em um único locatário podem ser executadas em relação a uma única partição. Você também pode implementar a lógica transacional em todos os itens dentro de um locatário. Como vários locatários compartilham um contêiner, você pode economizar custos de armazenamento e taxa de transferência realizando o pooling de recursos para locatários em um único contêiner em vez de provisionar capacidade extra para cada locatário. desvantagem de saudação é que você não tem o isolamento de desempenho por locatário. Aumentos de desempenho, throughput aplicam toohello contêiner inteiro vs destinadas aumenta para locatários.
* Um contêiner por locatário: cada locatário tem seu próprio contêiner. Nesse modelo, você pode reservar o desempenho por locatário. Com o novo modelo de preços de provisionamento do BD Cosmos, esse modelo é mais econômico para aplicativos multilocatário com um número pequeno de locatários.

Você também pode usar uma abordagem em camadas combinação/collocates locatários pequenos e migra maior contêiner próprio tootheir de locatários.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, fornecemos uma visão geral dos conceitos e práticas recomendadas para o particionamento com qualquer API do BD Cosmos do Azure. 

* Saiba mais sobre a [taxa de transferência provisionada no BD Cosmos do Azure](request-units.md)
* Saiba mais sobre [distribuição global no BD Cosmos do Azure](distribute-data-globally.md)



