---
title: Conectando o Apache Spark ao Azure Cosmos DB | Microsoft Docs
description: "Use este tutorial para saber mais sobre o conector do Spark ao Azure Cosmos DB que permite a conexão do Apache Spark ao Azure Cosmos DB para realizar agregações distribuídas e ciências de dados no banco de dados multilocatário distribuído globalmente da Microsoft projetado para a nuvem."
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
ms.openlocfilehash: 8ecbb478c81cde25bbd0d1c9ee07ae02b07f8cc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-the-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="25665-104">Acelerar a análise de Big Data em tempo real com o conector do Spark ao Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="25665-104">Accelerate real-time big-data analytics with the Spark to Azure Cosmos DB connector</span></span>

<span data-ttu-id="25665-105">O conector do Spark ao Azure Cosmos DB permite que o Azure Cosmos DB atue como uma fonte de entrada ou um coletor de saída para trabalhos do Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="25665-105">The Spark to Azure Cosmos DB connector enables Azure Cosmos DB to act as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="25665-106">Conectar o [Spark](http://spark.apache.org/) ao [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) acelera sua capacidade de solucionar problemas de ciência de dados ágeis na qual você pode usar o Azure Cosmos DB para manter e consultar dados rapidamente.</span><span class="sxs-lookup"><span data-stu-id="25665-106">Connecting [Spark](http://spark.apache.org/) to [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability to solve fast-moving data science problems where you can use Azure Cosmos DB to quickly persist and query data.</span></span> <span data-ttu-id="25665-107">O conector do Spark ao Azure Cosmos DB utiliza com eficiência os índices gerenciados nativos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="25665-107">The Spark to Azure Cosmos DB connector efficiently utilizes the native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="25665-108">Os índices habilitam colunas atualizáveis quando você executa uma análise e filtragem predicada em dados de alteração rápida distribuídos globalmente, que variam de Internet das coisas (IoT) para ciência de dados e cenários de análise.</span><span class="sxs-lookup"><span data-stu-id="25665-108">The indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) to data science and analytics scenarios.</span></span>

<span data-ttu-id="25665-109">Para trabalhar com Spark GraphX e o Gremlin graph APIs do Azure Cosmos DB, consulte [Executar análise de gráfico com Spark e Apache TinkerPop Gremlin](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="25665-109">For working with Spark GraphX and the Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="25665-110">Baixar</span><span class="sxs-lookup"><span data-stu-id="25665-110">Download</span></span>

<span data-ttu-id="25665-111">Para começar, baixo o conector do Spark ao Azure Cosmos DB (versão prévia) no repositório [azure-documentdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) do GitHub.</span><span class="sxs-lookup"><span data-stu-id="25665-111">To get started, download the Spark to Azure Cosmos DB connector (preview) from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="25665-112">Componentes do conector</span><span class="sxs-lookup"><span data-stu-id="25665-112">Connector components</span></span>

<span data-ttu-id="25665-113">O conector usa os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="25665-113">The connector utilizes the following components:</span></span>

* <span data-ttu-id="25665-114">O [Azure Cosmos DB](http://documentdb.com) permite que os clientes provisionem e dimensionem de forma elástica a produtividade e o armazenamento em qualquer quantidade de regiões geográficas.</span><span class="sxs-lookup"><span data-stu-id="25665-114">[Azure Cosmos DB](http://documentdb.com) enables customers to provision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="25665-115">O serviço oferece:</span><span class="sxs-lookup"><span data-stu-id="25665-115">The service offers:</span></span>
   * <span data-ttu-id="25665-116">Ativar a chave [distribuição global](distribute-data-globally.md) e escala horizontal</span><span class="sxs-lookup"><span data-stu-id="25665-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="25665-117">A garantia de latências de dígito único no percentil 99</span><span class="sxs-lookup"><span data-stu-id="25665-117">Guaranteed single digit latencies at the 99th percentile</span></span>
   * [<span data-ttu-id="25665-118">Vários modelos de consistência bem definidos</span><span class="sxs-lookup"><span data-stu-id="25665-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="25665-119">Garantia de alta disponibilidade com recursos de hospedagem múltipla</span><span class="sxs-lookup"><span data-stu-id="25665-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="25665-120">Todos os recursos são ancorados por [contratos de nível de serviço](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs) abrangentes e líderes do setor.</span><span class="sxs-lookup"><span data-stu-id="25665-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="25665-121">O [Apache Spark](http://spark.apache.org/) é um mecanismo de processamento eficiente com código-fonte aberto criado pensando em velocidade, facilidade de uso e análise sofisticada.</span><span class="sxs-lookup"><span data-stu-id="25665-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="25665-122">[Apache Spark em Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) para que você possa implantar o Apache Spark na nuvem para implantações críticas usando o [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="25665-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in the cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="25665-123">Versões com suporte oficial:</span><span class="sxs-lookup"><span data-stu-id="25665-123">Officially supported versions:</span></span>

| <span data-ttu-id="25665-124">Componente</span><span class="sxs-lookup"><span data-stu-id="25665-124">Component</span></span> | <span data-ttu-id="25665-125">Versão</span><span class="sxs-lookup"><span data-stu-id="25665-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="25665-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="25665-126">Apache Spark</span></span>|<span data-ttu-id="25665-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="25665-127">2.0+</span></span>|
| <span data-ttu-id="25665-128">Scala</span><span class="sxs-lookup"><span data-stu-id="25665-128">Scala</span></span>| <span data-ttu-id="25665-129">2.11</span><span class="sxs-lookup"><span data-stu-id="25665-129">2.11</span></span>|
| <span data-ttu-id="25665-130">SDK de Java do Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="25665-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="25665-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="25665-131">1.10.0</span></span> |

<span data-ttu-id="25665-132">Este artigo ajuda você a executar alguns exemplos simples com Python (via pyDocumentDB) e a interface Scala.</span><span class="sxs-lookup"><span data-stu-id="25665-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and the Scala interfaces.</span></span>

<span data-ttu-id="25665-133">Há duas abordagens para conectar o Apache Spark e o Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="25665-133">There are two approaches to connect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="25665-134">Usar pyDocumentDB por meio do [SDK de Python do Azure DocumentDB](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="25665-134">Use pyDocumentDB via the [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="25665-135">Criar um conector do Spark ao Azure Cosmos DB baseado em Java utilizando o [SDK de Java do Azure DocumentDB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="25665-135">Create a Java-based Spark to Azure Cosmos DB connector by utilizing the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="25665-136">implementação de pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="25665-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="25665-137">O [SDK do pyDocumentDB](https://github.com/Azure/azure-documentdb-python) atual possibilita a conexão do Spark ao Azure Cosmos DB, conforme mostra o seguinte diagrama:</span><span class="sxs-lookup"><span data-stu-id="25665-137">The current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you to connect Spark to Azure Cosmos DB as shown in the following diagram:</span></span>

![Fluxo de dados do Spark ao Azure Cosmos DB por meio do banco de dados do pyDocumentDB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-the-pydocumentdb-implementation"></a><span data-ttu-id="25665-139">Fluxo de dados da implementação do pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="25665-139">Data flow of the pyDocumentDB implementation</span></span>

<span data-ttu-id="25665-140">O fluxo de dados é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="25665-140">The data flow is as follows:</span></span>

1. <span data-ttu-id="25665-141">O nó mestre do Spark conecta-se ao nó de gateway do Azure Cosmos DB via pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="25665-141">The Spark master node connects to the Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="25665-142">Um usuário especifica apenas as conexões do Spark e do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="25665-142">A user specifies only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="25665-143">Conexões com os respectivos nós mestre e gateway são transparentes para o usuário.</span><span class="sxs-lookup"><span data-stu-id="25665-143">Connections to the respective master and gateway nodes are transparent to the user.</span></span>
2. <span data-ttu-id="25665-144">O nó de gateway executa a consulta no Azure Cosmos DB, no qual a consulta é executada posteriormente em partições da coleção nos nós de dados.</span><span class="sxs-lookup"><span data-stu-id="25665-144">The gateway node makes the query against Azure Cosmos DB where the query subsequently runs against the collection's partitions in the data nodes.</span></span> <span data-ttu-id="25665-145">A resposta para essas consultas é enviada de volta ao nó de gateway e esse conjunto de resultados retorna ao nó mestre do Spark.</span><span class="sxs-lookup"><span data-stu-id="25665-145">The response for those queries is sent back to the gateway node, and that result set is returned to the Spark master node.</span></span>
3. <span data-ttu-id="25665-146">Consultas subsequentes (por exemplo, em um DataFrame do Spark) são enviadas aos nós de trabalho do Spark para processamento.</span><span class="sxs-lookup"><span data-stu-id="25665-146">Subsequent queries (for example, against a Spark DataFrame) are sent to the Spark worker nodes for processing.</span></span>

<span data-ttu-id="25665-147">A comunicação entre o Spark e o Azure Cosmos DB é limitada ao nó mestre do Spark e aos nós de gateway do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="25665-147">Communication between Spark and Azure Cosmos DB is limited to the Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="25665-148">As consultas avança tão depressa como a camada de transporte entre esses dois nós permite.</span><span class="sxs-lookup"><span data-stu-id="25665-148">The queries go as fast as the transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="25665-149">Instalar o pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="25665-149">Install pyDocumentDB</span></span>
<span data-ttu-id="25665-150">Você pode instalar o pyDocumentDB em seu nó de driver usando **pip**, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="25665-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-to-azure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="25665-151">Conectar o Spark ao Azure Cosmos DB por meio do pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="25665-151">Connect Spark to Azure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="25665-152">A simplicidade do transporte da comunicação torna a execução de uma consulta do Spark ao Azure Cosmos DB usando o pyDocumentDB relativamente simples.</span><span class="sxs-lookup"><span data-stu-id="25665-152">The simplicity of the communication transport makes execution of a query from Spark to Azure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="25665-153">O trecho de código a seguir mostra como usar o pyDocumentDB dentro de um contexto do Spark.</span><span class="sxs-lookup"><span data-stu-id="25665-153">The following code snippet shows how to use pyDocumentDB in a Spark context.</span></span>

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring the connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys to connect to Azure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

<span data-ttu-id="25665-154">Conforme observado no trecho de código:</span><span class="sxs-lookup"><span data-stu-id="25665-154">As noted in the code snippet:</span></span>

* <span data-ttu-id="25665-155">O SDK de Python do Azure Cosmos DB (`pyDocumentDB`) contém todos os parâmetros de conexão necessárias.</span><span class="sxs-lookup"><span data-stu-id="25665-155">The Azure Cosmos DB Python SDK (`pyDocumentDB`) contains the all the necessary connection parameters.</span></span> <span data-ttu-id="25665-156">Por exemplo, o parâmetro de locais preferencial escolhe a ordem de prioridade e a réplica de leitura.</span><span class="sxs-lookup"><span data-stu-id="25665-156">For example, the preferred locations parameter chooses the read replica and priority order.</span></span>
*  <span data-ttu-id="25665-157">Importe as bibliotecas necessárias e configure a **masterKey** e o **host** para criar o *client* do Azure Cosmos DB (**pydocumentdb.document_client**).</span><span class="sxs-lookup"><span data-stu-id="25665-157">Import the necessary libraries and configure your **masterKey** and **host** to create the Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="25665-158">Executar consultas Spark via pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="25665-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="25665-159">Os exemplos a seguir usam a instância do Azure Cosmos DB criada no trecho anterior usando as chaves somente leitura especificadas.</span><span class="sxs-lookup"><span data-stu-id="25665-159">The following examples use the Azure Cosmos DB instance that was created in the previous snippet by using the specified read-only keys.</span></span> <span data-ttu-id="25665-160">O trecho de código a seguir se conecta à coleção **airports.codes** na conta DoctorWho, conforme especificado anteriormente executando uma consulta para extrair as cidades com aeroporto no estado de Washington.</span><span class="sxs-lookup"><span data-stu-id="25665-160">The following code snippet connects to the **airports.codes** collection in the DoctorWho account as specified earlier and runs a query to extract the airport cities in Washington state.</span></span>

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations the Azure Cosmos DB client will use to connect to the database and collection
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

<span data-ttu-id="25665-161">Após a execução da consulta por meio de **consulta**, o resultado será um **query_iterable.QueryIterable** que é convertido em uma lista de Python.</span><span class="sxs-lookup"><span data-stu-id="25665-161">After the query has been executed via **query**, the result is a **query_iterable.QueryIterable** that is converted to a Python list.</span></span> <span data-ttu-id="25665-162">Uma lista de Python pode ser facilmente convertida em um DataFrame do Spark usando o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="25665-162">A Python list can be easily converted to a Spark DataFrame by using the following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-the-pydocumentdb-to-connect-spark-to-azure-cosmos-db"></a><span data-ttu-id="25665-163">Por que usar o pyDocumentDB para conectar o Spark ao Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="25665-163">Why use the pyDocumentDB to connect Spark to Azure Cosmos DB?</span></span>
<span data-ttu-id="25665-164">A conexão do Spark ao Azure Cosmos DB usando pyDocumentDB normalmente ocorre para cenários nos quais:</span><span class="sxs-lookup"><span data-stu-id="25665-164">Connecting Spark to Azure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="25665-165">Você deseja usar Python.</span><span class="sxs-lookup"><span data-stu-id="25665-165">You want to use Python.</span></span>
* <span data-ttu-id="25665-166">Você está retornando um conjunto de resultados relativamente pequeno do Azure Cosmos DB para o Spark.</span><span class="sxs-lookup"><span data-stu-id="25665-166">You are returning a relatively small result set from Azure Cosmos DB to Spark.</span></span> <span data-ttu-id="25665-167">Observe que o conjunto de dados subjacente dentro do Azure Cosmos DB pode ser muito grande.</span><span class="sxs-lookup"><span data-stu-id="25665-167">Note that the underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="25665-168">Você está aplicando filtros, ou seja, executando filtros de predicado, em sua fonte do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="25665-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="25665-169">Conector do Spark ao Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="25665-169">Spark to Azure Cosmos DB connector</span></span>

<span data-ttu-id="25665-170">O conector do Spark ao Azure Cosmos DB utiliza o [SDK do Java do Azure DocumentDB](https://github.com/Azure/azure-documentdb-java) e move dados entre os nós de trabalho do Spark e do Azure Cosmos DB, conforme mostrado no diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="25665-170">The Spark to Azure Cosmos DB connector utilizes the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between the Spark worker nodes and Azure Cosmos DB as shown in the following diagram:</span></span>

![Fluxo de dados no conector do Spark ao Azure Cosmos DB](./media/spark-connector/spark-connector.png)

<span data-ttu-id="25665-172">O fluxo de dados é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="25665-172">The data flow is as follows:</span></span>

1. <span data-ttu-id="25665-173">O nó mestre do Spark conecta com o nó de gateway do Azure Cosmos DB para obter o mapa de partições.</span><span class="sxs-lookup"><span data-stu-id="25665-173">The Spark master node connects to the Azure Cosmos DB gateway node to obtain the partition map.</span></span> <span data-ttu-id="25665-174">Um usuário especifica apenas as conexões do Spark e do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="25665-174">A user specifies only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="25665-175">Conexões com os respectivos nós mestre e gateway são transparentes para o usuário.</span><span class="sxs-lookup"><span data-stu-id="25665-175">Connections to the respective master and gateway nodes are transparent to the user.</span></span>
2. <span data-ttu-id="25665-176">Essas informações são fornecidas de volta ao nó mestre do Spark.</span><span class="sxs-lookup"><span data-stu-id="25665-176">This information is provided back to the Spark master node.</span></span>  <span data-ttu-id="25665-177">Neste ponto, você deve conseguir analisar a consulta para determinar as partições e suas localizações no Azure Cosmos DB que você precisa acessar.</span><span class="sxs-lookup"><span data-stu-id="25665-177">At this point, you should be able to parse the query to determine the partitions and their locations in Azure Cosmos DB that you need to access.</span></span>
3. <span data-ttu-id="25665-178">Essas informações são transmitidas para os nós de trabalho do Spark.</span><span class="sxs-lookup"><span data-stu-id="25665-178">This information is transmitted to the Spark worker nodes.</span></span>
4. <span data-ttu-id="25665-179">Os nós de trabalho do Spark se conectam diretamente às partições do Azure Cosmos DB para extrair os dados e retornar os dados para as partições do Spark nos nós de trabalho do Spark.</span><span class="sxs-lookup"><span data-stu-id="25665-179">The Spark worker nodes connect to the Azure Cosmos DB partitions directly to extract the data and return the data to the Spark partitions in the Spark worker nodes.</span></span>

<span data-ttu-id="25665-180">A comunicação entre o Spark e o Azure Cosmos DB é consideravelmente mais rápida, pois a movimentação de dados ocorre entre os nós de trabalho do Spark e os nós de dados do Azure Cosmos DB (partições).</span><span class="sxs-lookup"><span data-stu-id="25665-180">Communication between Spark and Azure Cosmos DB is significantly faster because the data movement is between the Spark worker nodes and the Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-the-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="25665-181">Criar o conector do Spark ao Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="25665-181">Build the Spark to Azure Cosmos DB connector</span></span>
<span data-ttu-id="25665-182">Atualmente, o projeto do conector usa maven.</span><span class="sxs-lookup"><span data-stu-id="25665-182">Currently, the connector project uses maven.</span></span> <span data-ttu-id="25665-183">Para compilar o conector sem dependências, execute:</span><span class="sxs-lookup"><span data-stu-id="25665-183">To build the connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="25665-184">Você também pode baixar as versões mais recentes dos arquivos JAR da pasta *releases*.</span><span class="sxs-lookup"><span data-stu-id="25665-184">You can also download the latest versions of the JAR from the *releases* folder.</span></span>

### <a name="include-the-azure-cosmos-db-spark-jar"></a><span data-ttu-id="25665-185">Incluir o Azure Cosmos DB Spark JAR</span><span class="sxs-lookup"><span data-stu-id="25665-185">Include the Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="25665-186">Antes de executar qualquer código, você precisa incluir o Azure Cosmos DB Spark JAR.</span><span class="sxs-lookup"><span data-stu-id="25665-186">Before you execute any code, you need to include the Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="25665-187">Se você estiver usando o **spark-shell**, você poderá incluir o JAR usando a opção **--jars**.</span><span class="sxs-lookup"><span data-stu-id="25665-187">If you are using the **spark-shell**, then you can include the JAR by using the **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="25665-188">se você quiser executar o JAR sem dependências, use o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="25665-188">If you want to execute the JAR without dependencies, use the following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="25665-189">Se você estiver usando um serviço de notebook, como Jupyter do Azure HDInsight, use os comandos **spark magic**:</span><span class="sxs-lookup"><span data-stu-id="25665-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use the **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="25665-190">O comando **jars** permite que você inclua os dois JARs necessários para **azure-cosmosdb-spark** (o próprio e o SDK de Java do Azure DocumentDB) e exclui **scala-reflect** para que ele não interfira nas chamadas do Livy (notebook Jupyter > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="25665-190">The **jars** command enables you to include the two JARs that are needed for **azure-cosmosdb-spark** (itself and the Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with the Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-to-azure-cosmos-db-using-the-connector"></a><span data-ttu-id="25665-191">Conecte o Spark ao Azure Cosmos DB usando o conector</span><span class="sxs-lookup"><span data-stu-id="25665-191">Connect Spark to Azure Cosmos DB using the connector</span></span>
<span data-ttu-id="25665-192">Embora o transporte de comunicação seja um pouco mais complicado, a execução de uma consulta do Spark ao Azure Cosmos DB usando o conector é consideravelmente mais rápida.</span><span class="sxs-lookup"><span data-stu-id="25665-192">Although the communication transport is a little more complicated, executing a query from Spark to Azure Cosmos DB by using the connector is significantly faster.</span></span>

<span data-ttu-id="25665-193">O trecho de código a seguir mostra como usar o conector em um contexto do Spark.</span><span class="sxs-lookup"><span data-stu-id="25665-193">The following code snippet shows how to use the connector in a Spark context.</span></span>

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection to your collection
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

<span data-ttu-id="25665-194">Conforme observado no trecho de código:</span><span class="sxs-lookup"><span data-stu-id="25665-194">As noted in the code snippet:</span></span>

- <span data-ttu-id="25665-195">**azure-cosmosdb-spark** contém todos os parâmetros de conexão necessários, que incluem os locais preferenciais.</span><span class="sxs-lookup"><span data-stu-id="25665-195">**azure-cosmosdb-spark** contains the all the necessary connection parameters, which include the preferred locations.</span></span> <span data-ttu-id="25665-196">Por exemplo, você pode escolher a ordem de prioridade e a réplica de leitura.</span><span class="sxs-lookup"><span data-stu-id="25665-196">For example, you can choose the read replica and priority order.</span></span>
- <span data-ttu-id="25665-197">Basta importar as bibliotecas necessárias e configurar a masterKey e o host para criar o cliente do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="25665-197">Just import the necessary libraries and configure your masterKey and host to create the Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-the-connector"></a><span data-ttu-id="25665-198">Executar consultas Spark por meio do conector</span><span class="sxs-lookup"><span data-stu-id="25665-198">Execute Spark queries via the connector</span></span>

<span data-ttu-id="25665-199">O exemplo a seguir usa a instância do Azure Cosmos DB criada no trecho anterior usando as chaves somente leitura especificadas.</span><span class="sxs-lookup"><span data-stu-id="25665-199">The following example uses the Azure Cosmos DB instance that was created in the previous snippet by using the specified read-only keys.</span></span> <span data-ttu-id="25665-200">O trecho de código a seguir conecta-se à coleção DepartureDelays.flights_pcoll (na conta DoctorWho, conforme especificado anteriormente) e executa uma consulta para extrair as informações de atraso de voo que estão partindo de Seattle.</span><span class="sxs-lookup"><span data-stu-id="25665-200">The following code snippet connects to the DepartureDelays.flights_pcoll collection (in the DoctorWho account as specified earlier) and runs a query to extract the flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-the-spark-to-azure-cosmos-db-connector-implementation"></a><span data-ttu-id="25665-201">Por que usar a implementação do conector do Spark ao Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="25665-201">Why use the Spark to Azure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="25665-202">A conexão do Spark ao Azure Cosmos DB usando o conector é normalmente usada em cenários em que:</span><span class="sxs-lookup"><span data-stu-id="25665-202">Connecting Spark to Azure Cosmos DB by using the connector is typically for scenarios where:</span></span>

* <span data-ttu-id="25665-203">Você deseja usar Scala e atualizá-lo para incluir um wrapper de Python, conforme observado em [Problema 3: Adicionar wrapper de Python e exemplos](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span><span class="sxs-lookup"><span data-stu-id="25665-203">You want to use Scala and update it to include a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="25665-204">Você tem uma grande quantidade de dados para transferir entre o Apache Spark e o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="25665-204">You have a large amount of data to transfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="25665-205">Para dar uma ideia da diferença de desempenho da consulta, confira o [wiki de Execuções de teste de consulta](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="25665-205">To give you an idea of the query performance difference, see the [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="25665-206">Exemplo de agregação distribuída</span><span class="sxs-lookup"><span data-stu-id="25665-206">Distributed aggregation example</span></span>
<span data-ttu-id="25665-207">Esta seção fornece alguns exemplos de como você pode fazer agregações distribuídas e análises usando o Apache Spark e o Azure Cosmos DB juntos.</span><span class="sxs-lookup"><span data-stu-id="25665-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="25665-208">O Azure Cosmos DB já oferece suporte para agregações, que é discutido em [agregações de escala do planeta com o blog do Azure Cosmos DB](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span><span class="sxs-lookup"><span data-stu-id="25665-208">Azure Cosmos DB already supports aggregations, which is discussed in the [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="25665-209">Aqui está como ele pode ser usado para o próximo nível com o Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="25665-209">Here is how you can take it to the next level with Apache Spark.</span></span>

<span data-ttu-id="25665-210">Observe que essas agregações fazem referência ao [notebook do Conector do Spark ao Azure Cosmos DB](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="25665-210">Note that these aggregations are in reference to the [Spark to Azure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-to-flights-sample-data"></a><span data-ttu-id="25665-211">Conecte-se aos dados de exemplo de voos</span><span class="sxs-lookup"><span data-stu-id="25665-211">Connect to flights sample data</span></span>
<span data-ttu-id="25665-212">Esses exemplos de agregações acessam alguns dados de desempenho de voo armazenados em nosso banco de dados do Azure Cosmos DB **DoctorWho**.</span><span class="sxs-lookup"><span data-stu-id="25665-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="25665-213">Para se conectar a ele, você precisa utilizar o trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="25665-213">To connect to it, you need to utilize the following code snippet:</span></span>

```
// Import Spark to Azure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect to Azure Cosmos DB Database
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

<span data-ttu-id="25665-214">Com este trecho de código, também vamos executar uma consulta base que transfere o conjunto de dados filtrado do Azure Cosmos DB para o Spark em que o último pode executar agregações distribuídas.</span><span class="sxs-lookup"><span data-stu-id="25665-214">With this snippet, we are also going to run a base query that transfers the filtered set of data from Azure Cosmos DB to Spark where the latter can perform distributed aggregates.</span></span> <span data-ttu-id="25665-215">Nesse caso, estamos solicitando voos partindo de Seattle (SEA).</span><span class="sxs-lookup"><span data-stu-id="25665-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="25665-216">Os resultados a seguir foram gerados pela execução das consultas do serviço de notebook do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="25665-216">The following results were generated by running the queries from the Jupyter notebook service.</span></span>  <span data-ttu-id="25665-217">Observe que todos os trechos de código são genéricos e não são específicos a qualquer serviço.</span><span class="sxs-lookup"><span data-stu-id="25665-217">Note that all the code snippets are generic and not specific to any service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="25665-218">Execução de consultas LIMIT e COUNT</span><span class="sxs-lookup"><span data-stu-id="25665-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="25665-219">Assim como você estava acostumado no SQL/Spark SQL, vamos começar com uma consulta **LIMIT**:</span><span class="sxs-lookup"><span data-stu-id="25665-219">Just like you're used to in SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Consulta LIMIT do Spark](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="25665-221">A próxima consulta é uma consulta **COUNT** simples e rápida:</span><span class="sxs-lookup"><span data-stu-id="25665-221">The next query is a simple and fast **COUNT** query:</span></span>

![Consulta COUNT do Spark](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="25665-223">Consulta GROUP BY</span><span class="sxs-lookup"><span data-stu-id="25665-223">GROUP BY query</span></span>
<span data-ttu-id="25665-224">Neste próximo conjunto, podemos executar facilmente consultas **GROUP BY** em nosso banco de dados do Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="25665-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Gráfico da consulta Spark GROUP BY do Spark](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="25665-226">Consulta DISTINCT, ORDER BY</span><span class="sxs-lookup"><span data-stu-id="25665-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="25665-227">E aqui está uma consulta **DISTINCT, ORDER BY**:</span><span class="sxs-lookup"><span data-stu-id="25665-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Gráfico da consulta Spark GROUP BY do Spark](./media/spark-connector/order-by-query.png)

### <a name="continue-the-flight-data-analysis"></a><span data-ttu-id="25665-229">Continuar a análise de dados de voo</span><span class="sxs-lookup"><span data-stu-id="25665-229">Continue the flight data analysis</span></span>
<span data-ttu-id="25665-230">Você pode usar os seguintes exemplos de consultas para continuar a análise dos dados de voo:</span><span class="sxs-lookup"><span data-stu-id="25665-230">You can use the following example queries to continue analysis of the flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="25665-231">Cinco principais destinos atrasados (cidades) partindo de Seattle</span><span class="sxs-lookup"><span data-stu-id="25665-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Gráfico dos principais atrasos do Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="25665-233">Calcular a média de atrasos por cidades de destino partindo de Seattle</span><span class="sxs-lookup"><span data-stu-id="25665-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Gráfico da média de atrasos do Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="25665-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="25665-235">Next steps</span></span>

<span data-ttu-id="25665-236">Se você ainda não baixou, baixe o conector do Spark ao Azure Cosmos DB no repositório GitHub [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) e explore os recursos adicionais no repositório:</span><span class="sxs-lookup"><span data-stu-id="25665-236">If you haven't already, download the Spark to Azure Cosmos DB connector from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore the additional resources in the repo:</span></span>

* [<span data-ttu-id="25665-237">Exemplos de agregações distribuídas</span><span class="sxs-lookup"><span data-stu-id="25665-237">Distributed Aggregations Examples</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [<span data-ttu-id="25665-238">Exemplos de scripts e notebooks</span><span class="sxs-lookup"><span data-stu-id="25665-238">Sample Scripts and Notebooks</span></span>](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

<span data-ttu-id="25665-239">Convém examinar o [Guia do Apache Spark SQL, quadros de dados e conjuntos de dados](http://spark.apache.org/docs/latest/sql-programming-guide.html) e o artigo [Apache Spark no Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="25665-239">You might also want to review the [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and the [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
