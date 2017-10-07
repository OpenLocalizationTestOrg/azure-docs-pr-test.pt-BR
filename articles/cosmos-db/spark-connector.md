---
title: aaaConnecting Apache Spark tooAzure Cosmos DB | Microsoft Docs
description: "Use este tutorial toolearn sobre o conector do Azure Cosmos DB Spark Olá que permite que as agregações do tooconnect Apache Spark tooAzure Cosmos DB tooperform distribuída e ciências de dados no sistema de banco de dados multilocatário globalmente distribuídos Olá da Microsoft que é projetado para nuvem Olá."
keywords: apache spark
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: c4f46007-2606-4273-ab16-29d0e15c0736
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: denlee
ms.openlocfilehash: 70b496fc5ca8f65675f0224e749637f5d533c346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a>Acelerar a análise de grandes dados em tempo real com o conector do hello Spark tooAzure Cosmos DB

conector de banco de dados do Cosmos Olá Spark tooAzure permite tooact de banco de dados do Azure Cosmos como uma fonte de entrada ou o coletor de saída para trabalhos do Apache Spark. Conectando [Spark](http://spark.apache.org/) muito[o banco de dados do Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) acelera sua capacidade toosolve ágeis ciência de dados onde você pode usar o banco de dados do Azure Cosmos tooquickly de problemas persistirem e consultam dados. conector de banco de dados do Cosmos Olá Spark tooAzure utiliza com eficiência Olá nativo gerenciado do Azure Cosmos DB índices. os índices de saudação permitem colunas atualizáveis quando você executa uma análise e predicado propague filtragem contra alteração rápida globalmente distribuídos de dados, que variam de cenários de ciência e análise de toodata Internet das coisas (IoT).

Para trabalhar com Spark GraphX e gráfico de Gremlin Olá APIs de DB Cosmos do Azure, consulte [executar análise de gráfico com Spark e Apache TinkerPop Gremlin](spark-connector-graph.md).

## <a name="download"></a>Baixar

tooget iniciado, baixe o conector de banco de dados do Cosmos Olá Spark tooAzure (visualização) do hello [spark do azure-cosmosdb](https://github.com/Azure/azure-cosmosdb-spark/) repositório no GitHub.

## <a name="connector-components"></a>Componentes do conector

conector de saudação utiliza Olá componentes a seguir:

* [Banco de dados do Azure Cosmos](http://documentdb.com) permite que os clientes tooprovision e escala elasticidade de taxa de transferência e armazenamento em qualquer número de regiões geográficas. Olá ofertas de serviço:
   * Ativar a chave [distribuição global](distribute-data-globally.md) e escala horizontal
   * A garantia de latências de dígito único percentil 99th Olá
   * [Vários modelos de consistência bem definidos](consistency-levels.md)
   * Garantia de alta disponibilidade com recursos de hospedagem múltipla
   * Todos os recursos são ancorados por [contratos de nível de serviço](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs) abrangentes e líderes do setor.

* O [Apache Spark](http://spark.apache.org/) é um mecanismo de processamento eficiente com código-fonte aberto criado pensando em velocidade, facilidade de uso e análise sofisticada.

* [Apache Spark no Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) para que você possa implantar o Apache Spark na nuvem Olá para implantações de missão crítica usando [HDInsight do Azure](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Versões com suporte oficial:

| Componente | Versão |
|---------|-------|
|Apache Spark|2.0+|
| Scala| 2.11|
| SDK de Java do Azure DocumentDB | 1.10.0 |

Este artigo ajuda você a executar alguns exemplos simples usando Python (via pyDocumentDB) e Olá Scala interfaces.

Há duas abordagens tooconnect Apache Spark e o banco de dados do Azure Cosmos:
- Use pyDocumentDB via Olá [SDK de Python do DocumentDB do Azure](https://github.com/Azure/azure-documentdb-python).
- Criar um conector para banco de dados do Cosmos tooAzure Spark baseados em Java, utilizando a saudação [SDK de Java do DocumentDB do Azure](https://github.com/Azure/azure-documentdb-java).

## <a name="pydocumentdb-implementation"></a>implementação de pyDocumentDB
Olá atual [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) permite tooconnect Spark tooAzure Cosmos banco de dados, conforme mostrado no diagrama a seguir de saudação:

![Spark tooAzure fluxo de dados do banco de dados do Cosmos via pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a>Fluxo de dados de implementação de pyDocumentDB Olá

Olá fluxo de dados é o seguinte:

1. nó mestre do Spark Olá conecta-se o nó de gateway de banco de dados do Azure Cosmos toohello via pyDocumentDB. Um usuário especifica apenas Olá Spark e o banco de dados do Azure Cosmos conexões. Conexões toohello respectivos mestre e gateway nós são usuário toohello transparente.
2. nó de gateway Olá torna consulta hello Azure Cosmos DB onde consulta Olá subsequentemente executa em partições da coleção Olá em nós de dados hello. resposta Olá para essas consultas é enviada de volta o nó do gateway toohello e esse conjunto de resultados é retornado nó mestre do toohello Spark.
3. Consultas subsequentes (por exemplo, em um DataFrame Spark) são enviadas a nós de trabalho toohello Spark para processamento.

Comunicação entre Spark e o banco de dados do Azure Cosmos é limitado toohello nó mestre Spark e nós de gateway de banco de dados do Azure Cosmos.  consultas de saudação vá rápido permite a camada de transporte Olá entre esses dois nós.

### <a name="install-pydocumentdb"></a>Instalar o pyDocumentDB
Você pode instalar o pyDocumentDB em seu nó de driver usando **pip**, por exemplo:

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a>Conecte-se Spark tooAzure Cosmos DB via pyDocumentDB
simplicidade de saudação do transporte de comunicação Olá faz a execução de uma consulta do Spark tooAzure Cosmos DB usando pyDocumentDB relativamente simple.

Olá seguindo o trecho de código mostra como pyDocumentDB toouse em um contexto Spark.

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring hello connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys tooconnect tooAzure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

Conforme observado no trecho de código hello:

* Olá SDK de Python de banco de dados do Azure Cosmos (`pyDocumentDB`) contém Olá Olá a todos os parâmetros de conexão necessárias. Por exemplo, Olá preferencial parâmetro locais escolhe Olá ordem de prioridade e a réplica de leitura.
*  Importar bibliotecas necessárias hello e configurar seu **masterKey** e **host** toocreate hello Azure Cosmos DB *cliente* (**pydocumentdb.document_ cliente**).


### <a name="execute-spark-queries-via-pydocumentdb"></a>Executar consultas Spark via pyDocumentDB
Olá seguintes exemplos use hello Azure Cosmos DB a instância que foi criada no trecho de código anterior hello usando Olá especificado chaves somente leitura. trecho de código a seguir Hello conecta toohello **airports.codes** coleção na conta de DoctorWho Olá especificado anteriormente e executa um aeroporto de saudação tooextract consulta cidades no estado de Washington.

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations hello Azure Cosmos DB client will use tooconnect toohello database and collection
dbLink = 'dbs/' + databaseId
collLink = dbLink + '/colls/' + collectionId

# Set query parameter
querystr = "SELECT c.City FROM c WHERE c.State='WA'"

# Query documents
query = client.QueryDocuments(collLink, querystr, options=None, partition_key=None)

# Query for partitioned collections
# query = client.QueryDocuments(collLink, query, options= { 'enableCrossPartitionQuery': True }, partition_key=None)

# Push into list `elements`
elements = list(query)
```

Depois de saudação consulta foi executada por meio de **consulta**, Olá resultado é um **query_iterable. QueryIterable** que é lista de Python tooa convertido. Uma lista de Python pode ser facilmente convertido tooa DataFrame Spark usando Olá código a seguir:

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a>Por que usar Olá pyDocumentDB tooconnect Spark tooAzure Cosmos DB?
Conectando Spark tooAzure DB Cosmos usando pyDocumentDB normalmente é para cenários em que:

* Você deseja toouse Python.
* Você estiver retornando um relativamente pequeno conjunto de resultados de banco de dados do Azure Cosmos tooSpark. Observe que Olá conjunto de dados subjacente no banco de dados do Azure Cosmos pode ser muito grande. Você está aplicando filtros, ou seja, executando filtros de predicado, em sua fonte do Azure Cosmos DB.  

## <a name="spark-tooazure-cosmos-db-connector"></a>Spark tooAzure Cosmos DB conector

conector de banco de dados do Cosmos Olá Spark tooAzure utiliza Olá [SDK de Java do DocumentDB do Azure](https://github.com/Azure/azure-documentdb-java) e move dados entre nós de trabalho Spark hello e o banco de dados do Azure Cosmos, conforme mostrado no diagrama a seguir de saudação:

![Fluxo de dados no conector do hello Spark tooAzure Cosmos DB](./media/spark-connector/spark-connector.png)

Olá fluxo de dados é o seguinte:

1. nó principal do Spark Olá conecta mapa de partição toohello Azure Cosmos DB gateway nós tooobtain hello. Um usuário especifica apenas Olá Spark e o banco de dados do Azure Cosmos conexões. Conexões toohello respectivos mestre e gateway nós são usuário toohello transparente.
2. Essas informações são fornecidas nó mestre do backup toohello Spark.  Neste ponto, você deve ser capaz de tooparse Olá consultar toodetermine Olá partições e seus locais no banco de dados do Cosmos do Azure que você precisa tooaccess.
3. Essas informações são transmitidas toohello Spark trabalho nós.
4. nós de trabalho Spark Olá conectam partições de banco de dados do Azure Cosmos toohello diretamente tooextract Olá dados e retornar Olá dados toohello partições Spark em nós de trabalho Olá Spark.

Comunicação entre Spark e o banco de dados do Azure Cosmos é significativamente mais rápido porque a movimentação de dados Olá entre nós de trabalho Spark hello e nós de dados do banco de dados do Azure Cosmos hello (partições).

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a>Criar o conector do hello Spark tooAzure Cosmos DB
Atualmente, o projeto de conector Olá usa maven. conector de saudação toobuild sem dependências, você pode executar:
```
mvn clean package
```
Você também pode baixar as versões mais recentes de saudação do hello JAR do hello *libera* pasta.

### <a name="include-hello-azure-cosmos-db-spark-jar"></a>Incluir hello Azure Cosmos DB Spark JAR
Antes de executar qualquer código, você precisa tooinclude hello Azure Cosmos DB Spark JAR.  Se você estiver usando Olá **spark shell**, em seguida, você pode incluir Olá JAR usando Olá **– jars** opção.  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

Se você quiser tooexecute Olá JAR sem dependências, use Olá código a seguir:

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

Se você estiver usando um serviço de bloco de anotações como serviço de notebook Jupyter de HDInsight do Azure, você pode usar o hello **despertar magic** comandos:

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

Olá **jars** comando permite que você tooinclude Olá dois JARs que são necessários para **spark do azure-cosmosdb** (em si e hello SDK de Java do DocumentDB do Azure) e excluir **scala-refletir** para que não interfira Olá Livy chama (anotações do Jupyter > Livy > Spark).

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a>Conecte-se Spark usando o banco de dados do Cosmos tooAzure Olá conector
Embora o transporte de comunicação de saudação é um pouco mais complicado, executando uma consulta do Spark tooAzure Cosmos banco de dados usando o conector de saudação é significativamente mais rápido.

saudação de trecho de código a seguir mostra como toouse Olá conector em um contexto Spark.

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection tooyour collection
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

Conforme observado no trecho de código hello:

- **Azure-cosmosdb-spark** contém Olá todos Olá parâmetros de conexão necessárias, que incluem os locais de saudação preferida. Por exemplo, você pode escolher a ordem de prioridade e a réplica de leitura de saudação.
- Basta importar bibliotecas necessárias hello e configurar seu cliente de banco de dados do Azure Cosmos da saudação de toocreate masterKey e host.

### <a name="execute-spark-queries-via-hello-connector"></a>Executar consultas Spark via conector Olá

Olá seguindo o exemplo usa hello Azure Cosmos DB instância foi criada no trecho de código anterior hello usando Olá especificado chaves somente leitura. Olá trecho de código a seguir conecta-se a coleção de DepartureDelays.flights_pcoll toohello (em Olá DoctorWho conta conforme especificado anteriormente) e executa uma consulta tooextract Olá atraso informações sobre voo de voos que estão partindo de Seattle.

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a>Por que usar a implementação de conector Olá Spark tooAzure Cosmos DB?

Conectando Spark tooAzure Cosmos banco de dados usando o conector de saudação é normalmente para cenários em que:

* Você deseja toouse Scala e atualizá-lo tooinclude um wrapper de Python, conforme observado na [problema 3: wrapper adicionar Python e exemplos](https://github.com/Azure/azure-cosmosdb-spark/issues/3).
* Você tem uma grande quantidade de dados tootransfer entre Apache Spark e o banco de dados do Azure Cosmos.

toogive uma ideia de diferença de desempenho de consulta hello, consulte Olá [wiki de execuções de teste de consulta](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).

## <a name="distributed-aggregation-example"></a>Exemplo de agregação distribuída
Esta seção fornece alguns exemplos de como você pode fazer agregações distribuídas e análises usando o Apache Spark e o Azure Cosmos DB juntos. Banco de dados do Azure Cosmos já oferece suporte para agregações, que é discutido Olá [agregações de escala do planeta com o banco de dados do Azure Cosmos blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/). Aqui está como você poderá levar toohello próximo nível com o Apache Spark.

Observe que essas agregações em referência toohello [bloco de anotações do Spark tooAzure Cosmos DB conector](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).

### <a name="connect-tooflights-sample-data"></a>Conecte-se a dados de exemplo tooflights
Esses exemplos de agregações acessam alguns dados de desempenho de voo armazenados em nosso banco de dados do Azure Cosmos DB **DoctorWho**. tooconnect tooit, é necessário tooutilize Olá trecho de código a seguir:

```
// Import Spark tooAzure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect tooAzure Cosmos DB Database
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US 2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

Com este trecho de código, estamos também vai toorun uma consulta básica transferências Olá conjunto filtrado de dados do banco de dados do Azure Cosmos tooSpark onde Olá este último pode executar agregações distribuídas. Nesse caso, estamos solicitando voos partindo de Seattle (SEA).

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

Olá resultados a seguir foram gerados pela execução de consultas de saudação do hello serviço de notebook Jupyter.  Observe que todos os trechos de código Olá tooany genérico e não é específico de serviço.

### <a name="running-limit-and-count-queries"></a>Execução de consultas LIMIT e COUNT
Assim como é usada a tooin SQL/Spark SQL, vamos começar com uma **limite** consulta:

![Consulta LIMIT do Spark](./media/spark-connector/spark-sql-query.png)

Olá próxima consulta é uma simples e rápido **contagem** consulta:

![Consulta COUNT do Spark](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a>Consulta GROUP BY
Neste próximo conjunto, podemos executar facilmente consultas **GROUP BY** em nosso banco de dados do Azure Cosmos DB:

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Gráfico da consulta Spark GROUP BY do Spark](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a>Consulta DISTINCT, ORDER BY
E aqui está uma consulta **DISTINCT, ORDER BY**:

![Gráfico da consulta Spark GROUP BY do Spark](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a>Continuar a análise de dados de voo Olá
Você pode usar o hello análise de toocontinue de consultas de exemplo de dados de voo Olá a seguir:

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a>Cinco principais destinos atrasados (cidades) partindo de Seattle
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Gráfico dos principais atrasos do Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a>Calcular a média de atrasos por cidades de destino partindo de Seattle
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Gráfico da média de atrasos do Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a>Próximas etapas

Se você ainda não fez isso, baixar conector de banco de dados do Cosmos Olá Spark tooAzure da saudação [spark do azure-cosmosdb](https://github.com/Azure/azure-cosmosdb-spark) repositório GitHub e explorar os recursos adicionais de saudação no repositório de saudação:

* [Exemplos de agregações distribuídas](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [Exemplos de scripts e notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

Você também poderá Olá tooreview [Apache Spark SQL, quadros de dados e conjuntos de dados guia](http://spark.apache.org/docs/latest/sql-programming-guide.html) e hello [Apache Spark no Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) artigo.
