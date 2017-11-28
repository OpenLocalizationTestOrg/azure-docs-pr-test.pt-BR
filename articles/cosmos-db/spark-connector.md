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
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="c9a46-104">Acelerar a análise de grandes dados em tempo real com o conector do hello Spark tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c9a46-104">Accelerate real-time big-data analytics with hello Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="c9a46-105">conector de banco de dados do Cosmos Olá Spark tooAzure permite tooact de banco de dados do Azure Cosmos como uma fonte de entrada ou o coletor de saída para trabalhos do Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="c9a46-105">hello Spark tooAzure Cosmos DB connector enables Azure Cosmos DB tooact as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="c9a46-106">Conectando [Spark](http://spark.apache.org/) muito[o banco de dados do Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) acelera sua capacidade toosolve ágeis ciência de dados onde você pode usar o banco de dados do Azure Cosmos tooquickly de problemas persistirem e consultam dados.</span><span class="sxs-lookup"><span data-stu-id="c9a46-106">Connecting [Spark](http://spark.apache.org/) too[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability toosolve fast-moving data science problems where you can use Azure Cosmos DB tooquickly persist and query data.</span></span> <span data-ttu-id="c9a46-107">conector de banco de dados do Cosmos Olá Spark tooAzure utiliza com eficiência Olá nativo gerenciado do Azure Cosmos DB índices.</span><span class="sxs-lookup"><span data-stu-id="c9a46-107">hello Spark tooAzure Cosmos DB connector efficiently utilizes hello native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="c9a46-108">os índices de saudação permitem colunas atualizáveis quando você executa uma análise e predicado propague filtragem contra alteração rápida globalmente distribuídos de dados, que variam de cenários de ciência e análise de toodata Internet das coisas (IoT).</span><span class="sxs-lookup"><span data-stu-id="c9a46-108">hello indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) toodata science and analytics scenarios.</span></span>

<span data-ttu-id="c9a46-109">Para trabalhar com Spark GraphX e gráfico de Gremlin Olá APIs de DB Cosmos do Azure, consulte [executar análise de gráfico com Spark e Apache TinkerPop Gremlin](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="c9a46-109">For working with Spark GraphX and hello Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="c9a46-110">Baixar</span><span class="sxs-lookup"><span data-stu-id="c9a46-110">Download</span></span>

<span data-ttu-id="c9a46-111">tooget iniciado, baixe o conector de banco de dados do Cosmos Olá Spark tooAzure (visualização) do hello [spark do azure-cosmosdb](https://github.com/Azure/azure-cosmosdb-spark/) repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="c9a46-111">tooget started, download hello Spark tooAzure Cosmos DB connector (preview) from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="c9a46-112">Componentes do conector</span><span class="sxs-lookup"><span data-stu-id="c9a46-112">Connector components</span></span>

<span data-ttu-id="c9a46-113">conector de saudação utiliza Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9a46-113">hello connector utilizes hello following components:</span></span>

* <span data-ttu-id="c9a46-114">[Banco de dados do Azure Cosmos](http://documentdb.com) permite que os clientes tooprovision e escala elasticidade de taxa de transferência e armazenamento em qualquer número de regiões geográficas.</span><span class="sxs-lookup"><span data-stu-id="c9a46-114">[Azure Cosmos DB](http://documentdb.com) enables customers tooprovision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="c9a46-115">Olá ofertas de serviço:</span><span class="sxs-lookup"><span data-stu-id="c9a46-115">hello service offers:</span></span>
   * <span data-ttu-id="c9a46-116">Ativar a chave [distribuição global](distribute-data-globally.md) e escala horizontal</span><span class="sxs-lookup"><span data-stu-id="c9a46-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="c9a46-117">A garantia de latências de dígito único percentil 99th Olá</span><span class="sxs-lookup"><span data-stu-id="c9a46-117">Guaranteed single digit latencies at hello 99th percentile</span></span>
   * [<span data-ttu-id="c9a46-118">Vários modelos de consistência bem definidos</span><span class="sxs-lookup"><span data-stu-id="c9a46-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="c9a46-119">Garantia de alta disponibilidade com recursos de hospedagem múltipla</span><span class="sxs-lookup"><span data-stu-id="c9a46-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="c9a46-120">Todos os recursos são ancorados por [contratos de nível de serviço](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs) abrangentes e líderes do setor.</span><span class="sxs-lookup"><span data-stu-id="c9a46-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="c9a46-121">O [Apache Spark](http://spark.apache.org/) é um mecanismo de processamento eficiente com código-fonte aberto criado pensando em velocidade, facilidade de uso e análise sofisticada.</span><span class="sxs-lookup"><span data-stu-id="c9a46-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="c9a46-122">[Apache Spark no Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) para que você possa implantar o Apache Spark na nuvem Olá para implantações de missão crítica usando [HDInsight do Azure](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="c9a46-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in hello cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="c9a46-123">Versões com suporte oficial:</span><span class="sxs-lookup"><span data-stu-id="c9a46-123">Officially supported versions:</span></span>

| <span data-ttu-id="c9a46-124">Componente</span><span class="sxs-lookup"><span data-stu-id="c9a46-124">Component</span></span> | <span data-ttu-id="c9a46-125">Versão</span><span class="sxs-lookup"><span data-stu-id="c9a46-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="c9a46-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="c9a46-126">Apache Spark</span></span>|<span data-ttu-id="c9a46-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="c9a46-127">2.0+</span></span>|
| <span data-ttu-id="c9a46-128">Scala</span><span class="sxs-lookup"><span data-stu-id="c9a46-128">Scala</span></span>| <span data-ttu-id="c9a46-129">2.11</span><span class="sxs-lookup"><span data-stu-id="c9a46-129">2.11</span></span>|
| <span data-ttu-id="c9a46-130">SDK de Java do Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c9a46-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="c9a46-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="c9a46-131">1.10.0</span></span> |

<span data-ttu-id="c9a46-132">Este artigo ajuda você a executar alguns exemplos simples usando Python (via pyDocumentDB) e Olá Scala interfaces.</span><span class="sxs-lookup"><span data-stu-id="c9a46-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and hello Scala interfaces.</span></span>

<span data-ttu-id="c9a46-133">Há duas abordagens tooconnect Apache Spark e o banco de dados do Azure Cosmos:</span><span class="sxs-lookup"><span data-stu-id="c9a46-133">There are two approaches tooconnect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="c9a46-134">Use pyDocumentDB via Olá [SDK de Python do DocumentDB do Azure](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="c9a46-134">Use pyDocumentDB via hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="c9a46-135">Criar um conector para banco de dados do Cosmos tooAzure Spark baseados em Java, utilizando a saudação [SDK de Java do DocumentDB do Azure](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="c9a46-135">Create a Java-based Spark tooAzure Cosmos DB connector by utilizing hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="c9a46-136">implementação de pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="c9a46-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="c9a46-137">Olá atual [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) permite tooconnect Spark tooAzure Cosmos banco de dados, conforme mostrado no diagrama a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="c9a46-137">hello current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you tooconnect Spark tooAzure Cosmos DB as shown in hello following diagram:</span></span>

![Spark tooAzure fluxo de dados do banco de dados do Cosmos via pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a><span data-ttu-id="c9a46-139">Fluxo de dados de implementação de pyDocumentDB Olá</span><span class="sxs-lookup"><span data-stu-id="c9a46-139">Data flow of hello pyDocumentDB implementation</span></span>

<span data-ttu-id="c9a46-140">Olá fluxo de dados é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c9a46-140">hello data flow is as follows:</span></span>

1. <span data-ttu-id="c9a46-141">nó mestre do Spark Olá conecta-se o nó de gateway de banco de dados do Azure Cosmos toohello via pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="c9a46-141">hello Spark master node connects toohello Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="c9a46-142">Um usuário especifica apenas Olá Spark e o banco de dados do Azure Cosmos conexões.</span><span class="sxs-lookup"><span data-stu-id="c9a46-142">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="c9a46-143">Conexões toohello respectivos mestre e gateway nós são usuário toohello transparente.</span><span class="sxs-lookup"><span data-stu-id="c9a46-143">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="c9a46-144">nó de gateway Olá torna consulta hello Azure Cosmos DB onde consulta Olá subsequentemente executa em partições da coleção Olá em nós de dados hello.</span><span class="sxs-lookup"><span data-stu-id="c9a46-144">hello gateway node makes hello query against Azure Cosmos DB where hello query subsequently runs against hello collection's partitions in hello data nodes.</span></span> <span data-ttu-id="c9a46-145">resposta Olá para essas consultas é enviada de volta o nó do gateway toohello e esse conjunto de resultados é retornado nó mestre do toohello Spark.</span><span class="sxs-lookup"><span data-stu-id="c9a46-145">hello response for those queries is sent back toohello gateway node, and that result set is returned toohello Spark master node.</span></span>
3. <span data-ttu-id="c9a46-146">Consultas subsequentes (por exemplo, em um DataFrame Spark) são enviadas a nós de trabalho toohello Spark para processamento.</span><span class="sxs-lookup"><span data-stu-id="c9a46-146">Subsequent queries (for example, against a Spark DataFrame) are sent toohello Spark worker nodes for processing.</span></span>

<span data-ttu-id="c9a46-147">Comunicação entre Spark e o banco de dados do Azure Cosmos é limitado toohello nó mestre Spark e nós de gateway de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c9a46-147">Communication between Spark and Azure Cosmos DB is limited toohello Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="c9a46-148">consultas de saudação vá rápido permite a camada de transporte Olá entre esses dois nós.</span><span class="sxs-lookup"><span data-stu-id="c9a46-148">hello queries go as fast as hello transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="c9a46-149">Instalar o pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="c9a46-149">Install pyDocumentDB</span></span>
<span data-ttu-id="c9a46-150">Você pode instalar o pyDocumentDB em seu nó de driver usando **pip**, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c9a46-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="c9a46-151">Conecte-se Spark tooAzure Cosmos DB via pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="c9a46-151">Connect Spark tooAzure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="c9a46-152">simplicidade de saudação do transporte de comunicação Olá faz a execução de uma consulta do Spark tooAzure Cosmos DB usando pyDocumentDB relativamente simple.</span><span class="sxs-lookup"><span data-stu-id="c9a46-152">hello simplicity of hello communication transport makes execution of a query from Spark tooAzure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="c9a46-153">Olá seguindo o trecho de código mostra como pyDocumentDB toouse em um contexto Spark.</span><span class="sxs-lookup"><span data-stu-id="c9a46-153">hello following code snippet shows how toouse pyDocumentDB in a Spark context.</span></span>

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

<span data-ttu-id="c9a46-154">Conforme observado no trecho de código hello:</span><span class="sxs-lookup"><span data-stu-id="c9a46-154">As noted in hello code snippet:</span></span>

* <span data-ttu-id="c9a46-155">Olá SDK de Python de banco de dados do Azure Cosmos (`pyDocumentDB`) contém Olá Olá a todos os parâmetros de conexão necessárias.</span><span class="sxs-lookup"><span data-stu-id="c9a46-155">hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contains hello all hello necessary connection parameters.</span></span> <span data-ttu-id="c9a46-156">Por exemplo, Olá preferencial parâmetro locais escolhe Olá ordem de prioridade e a réplica de leitura.</span><span class="sxs-lookup"><span data-stu-id="c9a46-156">For example, hello preferred locations parameter chooses hello read replica and priority order.</span></span>
*  <span data-ttu-id="c9a46-157">Importar bibliotecas necessárias hello e configurar seu **masterKey** e **host** toocreate hello Azure Cosmos DB *cliente* (**pydocumentdb.document_ cliente**).</span><span class="sxs-lookup"><span data-stu-id="c9a46-157">Import hello necessary libraries and configure your **masterKey** and **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="c9a46-158">Executar consultas Spark via pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="c9a46-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="c9a46-159">Olá seguintes exemplos use hello Azure Cosmos DB a instância que foi criada no trecho de código anterior hello usando Olá especificado chaves somente leitura.</span><span class="sxs-lookup"><span data-stu-id="c9a46-159">hello following examples use hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="c9a46-160">trecho de código a seguir Hello conecta toohello **airports.codes** coleção na conta de DoctorWho Olá especificado anteriormente e executa um aeroporto de saudação tooextract consulta cidades no estado de Washington.</span><span class="sxs-lookup"><span data-stu-id="c9a46-160">hello following code snippet connects toohello **airports.codes** collection in hello DoctorWho account as specified earlier and runs a query tooextract hello airport cities in Washington state.</span></span>

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

<span data-ttu-id="c9a46-161">Depois de saudação consulta foi executada por meio de **consulta**, Olá resultado é um **query_iterable. QueryIterable** que é lista de Python tooa convertido.</span><span class="sxs-lookup"><span data-stu-id="c9a46-161">After hello query has been executed via **query**, hello result is a **query_iterable.QueryIterable** that is converted tooa Python list.</span></span> <span data-ttu-id="c9a46-162">Uma lista de Python pode ser facilmente convertido tooa DataFrame Spark usando Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9a46-162">A Python list can be easily converted tooa Spark DataFrame by using hello following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a><span data-ttu-id="c9a46-163">Por que usar Olá pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="c9a46-163">Why use hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span></span>
<span data-ttu-id="c9a46-164">Conectando Spark tooAzure DB Cosmos usando pyDocumentDB normalmente é para cenários em que:</span><span class="sxs-lookup"><span data-stu-id="c9a46-164">Connecting Spark tooAzure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="c9a46-165">Você deseja toouse Python.</span><span class="sxs-lookup"><span data-stu-id="c9a46-165">You want toouse Python.</span></span>
* <span data-ttu-id="c9a46-166">Você estiver retornando um relativamente pequeno conjunto de resultados de banco de dados do Azure Cosmos tooSpark.</span><span class="sxs-lookup"><span data-stu-id="c9a46-166">You are returning a relatively small result set from Azure Cosmos DB tooSpark.</span></span> <span data-ttu-id="c9a46-167">Observe que Olá conjunto de dados subjacente no banco de dados do Azure Cosmos pode ser muito grande.</span><span class="sxs-lookup"><span data-stu-id="c9a46-167">Note that hello underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="c9a46-168">Você está aplicando filtros, ou seja, executando filtros de predicado, em sua fonte do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c9a46-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="c9a46-169">Spark tooAzure Cosmos DB conector</span><span class="sxs-lookup"><span data-stu-id="c9a46-169">Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="c9a46-170">conector de banco de dados do Cosmos Olá Spark tooAzure utiliza Olá [SDK de Java do DocumentDB do Azure](https://github.com/Azure/azure-documentdb-java) e move dados entre nós de trabalho Spark hello e o banco de dados do Azure Cosmos, conforme mostrado no diagrama a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="c9a46-170">hello Spark tooAzure Cosmos DB connector utilizes hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between hello Spark worker nodes and Azure Cosmos DB as shown in hello following diagram:</span></span>

![Fluxo de dados no conector do hello Spark tooAzure Cosmos DB](./media/spark-connector/spark-connector.png)

<span data-ttu-id="c9a46-172">Olá fluxo de dados é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c9a46-172">hello data flow is as follows:</span></span>

1. <span data-ttu-id="c9a46-173">nó principal do Spark Olá conecta mapa de partição toohello Azure Cosmos DB gateway nós tooobtain hello.</span><span class="sxs-lookup"><span data-stu-id="c9a46-173">hello Spark master node connects toohello Azure Cosmos DB gateway node tooobtain hello partition map.</span></span> <span data-ttu-id="c9a46-174">Um usuário especifica apenas Olá Spark e o banco de dados do Azure Cosmos conexões.</span><span class="sxs-lookup"><span data-stu-id="c9a46-174">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="c9a46-175">Conexões toohello respectivos mestre e gateway nós são usuário toohello transparente.</span><span class="sxs-lookup"><span data-stu-id="c9a46-175">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="c9a46-176">Essas informações são fornecidas nó mestre do backup toohello Spark.</span><span class="sxs-lookup"><span data-stu-id="c9a46-176">This information is provided back toohello Spark master node.</span></span>  <span data-ttu-id="c9a46-177">Neste ponto, você deve ser capaz de tooparse Olá consultar toodetermine Olá partições e seus locais no banco de dados do Cosmos do Azure que você precisa tooaccess.</span><span class="sxs-lookup"><span data-stu-id="c9a46-177">At this point, you should be able tooparse hello query toodetermine hello partitions and their locations in Azure Cosmos DB that you need tooaccess.</span></span>
3. <span data-ttu-id="c9a46-178">Essas informações são transmitidas toohello Spark trabalho nós.</span><span class="sxs-lookup"><span data-stu-id="c9a46-178">This information is transmitted toohello Spark worker nodes.</span></span>
4. <span data-ttu-id="c9a46-179">nós de trabalho Spark Olá conectam partições de banco de dados do Azure Cosmos toohello diretamente tooextract Olá dados e retornar Olá dados toohello partições Spark em nós de trabalho Olá Spark.</span><span class="sxs-lookup"><span data-stu-id="c9a46-179">hello Spark worker nodes connect toohello Azure Cosmos DB partitions directly tooextract hello data and return hello data toohello Spark partitions in hello Spark worker nodes.</span></span>

<span data-ttu-id="c9a46-180">Comunicação entre Spark e o banco de dados do Azure Cosmos é significativamente mais rápido porque a movimentação de dados Olá entre nós de trabalho Spark hello e nós de dados do banco de dados do Azure Cosmos hello (partições).</span><span class="sxs-lookup"><span data-stu-id="c9a46-180">Communication between Spark and Azure Cosmos DB is significantly faster because hello data movement is between hello Spark worker nodes and hello Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="c9a46-181">Criar o conector do hello Spark tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c9a46-181">Build hello Spark tooAzure Cosmos DB connector</span></span>
<span data-ttu-id="c9a46-182">Atualmente, o projeto de conector Olá usa maven.</span><span class="sxs-lookup"><span data-stu-id="c9a46-182">Currently, hello connector project uses maven.</span></span> <span data-ttu-id="c9a46-183">conector de saudação toobuild sem dependências, você pode executar:</span><span class="sxs-lookup"><span data-stu-id="c9a46-183">toobuild hello connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="c9a46-184">Você também pode baixar as versões mais recentes de saudação do hello JAR do hello *libera* pasta.</span><span class="sxs-lookup"><span data-stu-id="c9a46-184">You can also download hello latest versions of hello JAR from hello *releases* folder.</span></span>

### <a name="include-hello-azure-cosmos-db-spark-jar"></a><span data-ttu-id="c9a46-185">Incluir hello Azure Cosmos DB Spark JAR</span><span class="sxs-lookup"><span data-stu-id="c9a46-185">Include hello Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="c9a46-186">Antes de executar qualquer código, você precisa tooinclude hello Azure Cosmos DB Spark JAR.</span><span class="sxs-lookup"><span data-stu-id="c9a46-186">Before you execute any code, you need tooinclude hello Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="c9a46-187">Se você estiver usando Olá **spark shell**, em seguida, você pode incluir Olá JAR usando Olá **– jars** opção.</span><span class="sxs-lookup"><span data-stu-id="c9a46-187">If you are using hello **spark-shell**, then you can include hello JAR by using hello **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="c9a46-188">Se você quiser tooexecute Olá JAR sem dependências, use Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9a46-188">If you want tooexecute hello JAR without dependencies, use hello following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="c9a46-189">Se você estiver usando um serviço de bloco de anotações como serviço de notebook Jupyter de HDInsight do Azure, você pode usar o hello **despertar magic** comandos:</span><span class="sxs-lookup"><span data-stu-id="c9a46-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use hello **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="c9a46-190">Olá **jars** comando permite que você tooinclude Olá dois JARs que são necessários para **spark do azure-cosmosdb** (em si e hello SDK de Java do DocumentDB do Azure) e excluir **scala-refletir** para que não interfira Olá Livy chama (anotações do Jupyter > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="c9a46-190">hello **jars** command enables you tooinclude hello two JARs that are needed for **azure-cosmosdb-spark** (itself and hello Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with hello Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a><span data-ttu-id="c9a46-191">Conecte-se Spark usando o banco de dados do Cosmos tooAzure Olá conector</span><span class="sxs-lookup"><span data-stu-id="c9a46-191">Connect Spark tooAzure Cosmos DB using hello connector</span></span>
<span data-ttu-id="c9a46-192">Embora o transporte de comunicação de saudação é um pouco mais complicado, executando uma consulta do Spark tooAzure Cosmos banco de dados usando o conector de saudação é significativamente mais rápido.</span><span class="sxs-lookup"><span data-stu-id="c9a46-192">Although hello communication transport is a little more complicated, executing a query from Spark tooAzure Cosmos DB by using hello connector is significantly faster.</span></span>

<span data-ttu-id="c9a46-193">saudação de trecho de código a seguir mostra como toouse Olá conector em um contexto Spark.</span><span class="sxs-lookup"><span data-stu-id="c9a46-193">hello following code snippet shows how toouse hello connector in a Spark context.</span></span>

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

<span data-ttu-id="c9a46-194">Conforme observado no trecho de código hello:</span><span class="sxs-lookup"><span data-stu-id="c9a46-194">As noted in hello code snippet:</span></span>

- <span data-ttu-id="c9a46-195">**Azure-cosmosdb-spark** contém Olá todos Olá parâmetros de conexão necessárias, que incluem os locais de saudação preferida.</span><span class="sxs-lookup"><span data-stu-id="c9a46-195">**azure-cosmosdb-spark** contains hello all hello necessary connection parameters, which include hello preferred locations.</span></span> <span data-ttu-id="c9a46-196">Por exemplo, você pode escolher a ordem de prioridade e a réplica de leitura de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9a46-196">For example, you can choose hello read replica and priority order.</span></span>
- <span data-ttu-id="c9a46-197">Basta importar bibliotecas necessárias hello e configurar seu cliente de banco de dados do Azure Cosmos da saudação de toocreate masterKey e host.</span><span class="sxs-lookup"><span data-stu-id="c9a46-197">Just import hello necessary libraries and configure your masterKey and host toocreate hello Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-hello-connector"></a><span data-ttu-id="c9a46-198">Executar consultas Spark via conector Olá</span><span class="sxs-lookup"><span data-stu-id="c9a46-198">Execute Spark queries via hello connector</span></span>

<span data-ttu-id="c9a46-199">Olá seguindo o exemplo usa hello Azure Cosmos DB instância foi criada no trecho de código anterior hello usando Olá especificado chaves somente leitura.</span><span class="sxs-lookup"><span data-stu-id="c9a46-199">hello following example uses hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="c9a46-200">Olá trecho de código a seguir conecta-se a coleção de DepartureDelays.flights_pcoll toohello (em Olá DoctorWho conta conforme especificado anteriormente) e executa uma consulta tooextract Olá atraso informações sobre voo de voos que estão partindo de Seattle.</span><span class="sxs-lookup"><span data-stu-id="c9a46-200">hello following code snippet connects toohello DepartureDelays.flights_pcoll collection (in hello DoctorWho account as specified earlier) and runs a query tooextract hello flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a><span data-ttu-id="c9a46-201">Por que usar a implementação de conector Olá Spark tooAzure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="c9a46-201">Why use hello Spark tooAzure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="c9a46-202">Conectando Spark tooAzure Cosmos banco de dados usando o conector de saudação é normalmente para cenários em que:</span><span class="sxs-lookup"><span data-stu-id="c9a46-202">Connecting Spark tooAzure Cosmos DB by using hello connector is typically for scenarios where:</span></span>

* <span data-ttu-id="c9a46-203">Você deseja toouse Scala e atualizá-lo tooinclude um wrapper de Python, conforme observado na [problema 3: wrapper adicionar Python e exemplos](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span><span class="sxs-lookup"><span data-stu-id="c9a46-203">You want toouse Scala and update it tooinclude a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="c9a46-204">Você tem uma grande quantidade de dados tootransfer entre Apache Spark e o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c9a46-204">You have a large amount of data tootransfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="c9a46-205">toogive uma ideia de diferença de desempenho de consulta hello, consulte Olá [wiki de execuções de teste de consulta](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="c9a46-205">toogive you an idea of hello query performance difference, see hello [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="c9a46-206">Exemplo de agregação distribuída</span><span class="sxs-lookup"><span data-stu-id="c9a46-206">Distributed aggregation example</span></span>
<span data-ttu-id="c9a46-207">Esta seção fornece alguns exemplos de como você pode fazer agregações distribuídas e análises usando o Apache Spark e o Azure Cosmos DB juntos.</span><span class="sxs-lookup"><span data-stu-id="c9a46-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="c9a46-208">Banco de dados do Azure Cosmos já oferece suporte para agregações, que é discutido Olá [agregações de escala do planeta com o banco de dados do Azure Cosmos blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span><span class="sxs-lookup"><span data-stu-id="c9a46-208">Azure Cosmos DB already supports aggregations, which is discussed in hello [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="c9a46-209">Aqui está como você poderá levar toohello próximo nível com o Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="c9a46-209">Here is how you can take it toohello next level with Apache Spark.</span></span>

<span data-ttu-id="c9a46-210">Observe que essas agregações em referência toohello [bloco de anotações do Spark tooAzure Cosmos DB conector](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="c9a46-210">Note that these aggregations are in reference toohello [Spark tooAzure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-tooflights-sample-data"></a><span data-ttu-id="c9a46-211">Conecte-se a dados de exemplo tooflights</span><span class="sxs-lookup"><span data-stu-id="c9a46-211">Connect tooflights sample data</span></span>
<span data-ttu-id="c9a46-212">Esses exemplos de agregações acessam alguns dados de desempenho de voo armazenados em nosso banco de dados do Azure Cosmos DB **DoctorWho**.</span><span class="sxs-lookup"><span data-stu-id="c9a46-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="c9a46-213">tooconnect tooit, é necessário tooutilize Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9a46-213">tooconnect tooit, you need tooutilize hello following code snippet:</span></span>

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

<span data-ttu-id="c9a46-214">Com este trecho de código, estamos também vai toorun uma consulta básica transferências Olá conjunto filtrado de dados do banco de dados do Azure Cosmos tooSpark onde Olá este último pode executar agregações distribuídas.</span><span class="sxs-lookup"><span data-stu-id="c9a46-214">With this snippet, we are also going toorun a base query that transfers hello filtered set of data from Azure Cosmos DB tooSpark where hello latter can perform distributed aggregates.</span></span> <span data-ttu-id="c9a46-215">Nesse caso, estamos solicitando voos partindo de Seattle (SEA).</span><span class="sxs-lookup"><span data-stu-id="c9a46-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="c9a46-216">Olá resultados a seguir foram gerados pela execução de consultas de saudação do hello serviço de notebook Jupyter.</span><span class="sxs-lookup"><span data-stu-id="c9a46-216">hello following results were generated by running hello queries from hello Jupyter notebook service.</span></span>  <span data-ttu-id="c9a46-217">Observe que todos os trechos de código Olá tooany genérico e não é específico de serviço.</span><span class="sxs-lookup"><span data-stu-id="c9a46-217">Note that all hello code snippets are generic and not specific tooany service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="c9a46-218">Execução de consultas LIMIT e COUNT</span><span class="sxs-lookup"><span data-stu-id="c9a46-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="c9a46-219">Assim como é usada a tooin SQL/Spark SQL, vamos começar com uma **limite** consulta:</span><span class="sxs-lookup"><span data-stu-id="c9a46-219">Just like you're used tooin SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Consulta LIMIT do Spark](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="c9a46-221">Olá próxima consulta é uma simples e rápido **contagem** consulta:</span><span class="sxs-lookup"><span data-stu-id="c9a46-221">hello next query is a simple and fast **COUNT** query:</span></span>

![Consulta COUNT do Spark](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="c9a46-223">Consulta GROUP BY</span><span class="sxs-lookup"><span data-stu-id="c9a46-223">GROUP BY query</span></span>
<span data-ttu-id="c9a46-224">Neste próximo conjunto, podemos executar facilmente consultas **GROUP BY** em nosso banco de dados do Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="c9a46-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Gráfico da consulta Spark GROUP BY do Spark](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="c9a46-226">Consulta DISTINCT, ORDER BY</span><span class="sxs-lookup"><span data-stu-id="c9a46-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="c9a46-227">E aqui está uma consulta **DISTINCT, ORDER BY**:</span><span class="sxs-lookup"><span data-stu-id="c9a46-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Gráfico da consulta Spark GROUP BY do Spark](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a><span data-ttu-id="c9a46-229">Continuar a análise de dados de voo Olá</span><span class="sxs-lookup"><span data-stu-id="c9a46-229">Continue hello flight data analysis</span></span>
<span data-ttu-id="c9a46-230">Você pode usar o hello análise de toocontinue de consultas de exemplo de dados de voo Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9a46-230">You can use hello following example queries toocontinue analysis of hello flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="c9a46-231">Cinco principais destinos atrasados (cidades) partindo de Seattle</span><span class="sxs-lookup"><span data-stu-id="c9a46-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Gráfico dos principais atrasos do Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="c9a46-233">Calcular a média de atrasos por cidades de destino partindo de Seattle</span><span class="sxs-lookup"><span data-stu-id="c9a46-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Gráfico da média de atrasos do Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="c9a46-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9a46-235">Next steps</span></span>

<span data-ttu-id="c9a46-236">Se você ainda não fez isso, baixar conector de banco de dados do Cosmos Olá Spark tooAzure da saudação [spark do azure-cosmosdb](https://github.com/Azure/azure-cosmosdb-spark) repositório GitHub e explorar os recursos adicionais de saudação no repositório de saudação:</span><span class="sxs-lookup"><span data-stu-id="c9a46-236">If you haven't already, download hello Spark tooAzure Cosmos DB connector from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore hello additional resources in hello repo:</span></span>

* [<span data-ttu-id="c9a46-237">Exemplos de agregações distribuídas</span><span class="sxs-lookup"><span data-stu-id="c9a46-237">Distributed Aggregations Examples</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [<span data-ttu-id="c9a46-238">Exemplos de scripts e notebooks</span><span class="sxs-lookup"><span data-stu-id="c9a46-238">Sample Scripts and Notebooks</span></span>](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

<span data-ttu-id="c9a46-239">Você também poderá Olá tooreview [Apache Spark SQL, quadros de dados e conjuntos de dados guia](http://spark.apache.org/docs/latest/sql-programming-guide.html) e hello [Apache Spark no Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="c9a46-239">You might also want tooreview hello [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and hello [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
