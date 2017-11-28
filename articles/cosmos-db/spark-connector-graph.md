---
title: "BD Cosmos do Azure: executar análise de gráfico usando o Spark e o Gremlin do Apache TinkerPops | Microsoft Docs"
description: "Este artigo apresenta instruções para configurar e executar computação paralela e análise de gráfico no BD Cosmos do Azure com Spark e TinkerPop SparkGraphComputer."
services: cosmosdb
documentationcenter: 
author: khdang
manager: shireest
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: gremlin
ms.topic: article
ms.date: 06/05/2017
ms.author: khdang
ms.openlocfilehash: 27c4d945e418b130c68cfde845571eb93658101e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="06274-103">BD Cosmos do Azure: executar análise de gráfico usando o Spark e o Gremlin do Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="06274-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="06274-104">[Azure Cosmos DB](introduction.md) é o serviço de banco de dados multimodelo distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06274-104">[Azure Cosmos DB](introduction.md) is the globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="06274-105">É possível criar e consultar documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="06274-105">You can create and query document, key/value, and graph databases, all of which benefit from the global-distribution and horizontal-scale capabilities at the core of Azure Cosmos DB.</span></span> <span data-ttu-id="06274-106">O BD Costmos do Azure dá suporte a cargas de trabalho gráficas OLTP (processamento de transações online) que usam o [Gremlin do Apache TinkerPop](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="06274-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="06274-107">[Spark](http://spark.apache.org/) é um projeto Apache Software Foundation voltado para o processamento de dados OLAP (processamento analítico online de uso geral).</span><span class="sxs-lookup"><span data-stu-id="06274-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="06274-108">O Spark fornece um modelo de computação distribuída híbrido em memória/baseado em disco que é semelhante ao modelo MapReduce do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="06274-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar to the Hadoop MapReduce model.</span></span> <span data-ttu-id="06274-109">Você pode implantar o Apache Spark na nuvem usando o [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="06274-109">You can deploy Apache Spark in the cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="06274-110">Combinando o BD Cosmos do Azure e o Spark, você pode executar cargas de trabalho OLTP e OLAP quando usar o Gremlin.</span><span class="sxs-lookup"><span data-stu-id="06274-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="06274-111">Este artigo rápido demonstra como executar consultas do Gremlin no Banco de Dados Cosmos do Azure em um cluster Spark do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="06274-111">This quick-start article demonstrates how to run Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06274-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="06274-112">Prerequisites</span></span>

<span data-ttu-id="06274-113">Antes que possa executar esta amostra, você deverá ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="06274-113">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="06274-114">Cluster Spark do Azure HDInsight 2.0</span><span class="sxs-lookup"><span data-stu-id="06274-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="06274-115">JDK 1.8 + (execute `apt-get install default-jdk` se você não tiver o JDK)</span><span class="sxs-lookup"><span data-stu-id="06274-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="06274-116">Maven (execute `apt-get install maven` se você não tiver o Maven)</span><span class="sxs-lookup"><span data-stu-id="06274-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="06274-117">Uma assinatura do Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="06274-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="06274-118">Para obter informações sobre como configurar um cluster Spark no HDInsight, consulte [Provisionando clusters HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="06274-118">For information about how to set up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="06274-119">Criar uma conta de banco de dados BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="06274-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="06274-120">Primeiro, crie uma conta de banco de dados com a API do Graph fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="06274-120">First, create a database account with the Graph API by doing the following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="06274-121">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="06274-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="06274-122">Obter o Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="06274-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="06274-123">Obtenha o Apache TinkerPop fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="06274-123">Get Apache TinkerPop by doing the following:</span></span>

1. <span data-ttu-id="06274-124">Vá remotamente para o nó principal do cluster HDInsight`ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="06274-124">Remote to the master node of the HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="06274-125">Clonar o código-fonte do TinkerPop3, compilá-lo localmente e instalar no cache do Maven.</span><span class="sxs-lookup"><span data-stu-id="06274-125">Clone the TinkerPop3 source code, build it locally, and install it to Maven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="06274-126">Instalar o plug-in Spark-Gremlin</span><span class="sxs-lookup"><span data-stu-id="06274-126">Install the Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="06274-127">a.</span><span class="sxs-lookup"><span data-stu-id="06274-127">a.</span></span> <span data-ttu-id="06274-128">A instalação do plug-in é tratada pelo Grape.</span><span class="sxs-lookup"><span data-stu-id="06274-128">The installation of the plug-in is handled by Grape.</span></span> <span data-ttu-id="06274-129">Preencha as informações de repositórios do Grape para que possa baixar o plug-in e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="06274-129">Populate the repositories information for Grape so it can download the plug-in and its dependencies.</span></span> 

      <span data-ttu-id="06274-130">Crie o arquivo de configuração do Grape se não estiver presente no `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="06274-130">Create the grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="06274-131">Use as configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="06274-131">Use the following settings:</span></span>

    ```xml
    <ivysettings>
    <settings defaultResolver="downloadGrapes"/>
    <resolvers>
        <chain name="downloadGrapes">
        <filesystem name="cachedGrapes">
            <ivy pattern="${user.home}/.groovy/grapes/[organisation]/[module]/ivy-[revision].xml"/>
            <artifact pattern="${user.home}/.groovy/grapes/[organisation]/[module]/[type]s/[artifact]-[revision].[ext]"/>
        </filesystem>
        <ibiblio name="codehaus" root="http://repository.codehaus.org/" m2compatible="true"/>
        <ibiblio name="central" root="http://central.maven.org/maven2/" m2compatible="true"/>
        <ibiblio name="jitpack" root="https://jitpack.io" m2compatible="true"/>
        <ibiblio name="java.net2" root="http://download.java.net/maven/2/" m2compatible="true"/>
        <ibiblio name="apache-snapshots" root="http://repository.apache.org/snapshots/" m2compatible="true"/>
        <ibiblio name="local" root="file:${user.home}/.m2/repository/" m2compatible="true"/>
        </chain>
    </resolvers>
    </ivysettings>
    ``` 

    <span data-ttu-id="06274-132">b.</span><span class="sxs-lookup"><span data-stu-id="06274-132">b.</span></span> <span data-ttu-id="06274-133">Inicie o console do Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="06274-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="06274-134">c.</span><span class="sxs-lookup"><span data-stu-id="06274-134">c.</span></span> <span data-ttu-id="06274-135">Instale o plug-in Spark-Gremlin com a versão 3.3.0-SNAPSHOT que você criou nas etapas anteriores:</span><span class="sxs-lookup"><span data-stu-id="06274-135">Install the Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in the previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart the console to use [tinkerpop.spark]
    gremlin> :q
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :plugin use tinkerpop.spark
    ==>tinkerpop.spark activated
    ```

4. <span data-ttu-id="06274-136">Verifique se `Hadoop-Gremlin` é ativado com `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="06274-136">Check to see whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="06274-137">Desabilite esse plug-in, pois ele pode interferir no plug-in Spark-Gremlin `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="06274-137">Disable this plug-in, because it could interfere with the Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="06274-138">Preparar dependências TinkerPop3</span><span class="sxs-lookup"><span data-stu-id="06274-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="06274-139">Quando você criou o TinkerPop3 na etapa anterior, o processo também puxou todas as dependências jar para o Spark e o Hadoop no diretório de destino.</span><span class="sxs-lookup"><span data-stu-id="06274-139">When you built TinkerPop3 in the previous step, the process also pulled all jar dependencies for Spark and Hadoop in the target directory.</span></span> <span data-ttu-id="06274-140">Use os jars pré-instalado com HDI e só use dependências adicionais se necessário.</span><span class="sxs-lookup"><span data-stu-id="06274-140">Use the jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="06274-141">Vá para o diretório de destino do Console do Gremlin em `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="06274-141">Go to the Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="06274-142">Mova todos os jars em `ext/` para `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="06274-142">Move all jars under `ext/` to `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="06274-143">Remova todas as bibliotecas jar em `lib/` que não estiverem na seguinte lista:</span><span class="sxs-lookup"><span data-stu-id="06274-143">Remove all jar libraries under `lib/` that are not in the following list:</span></span>

    ```bash
    # TinkerPop3
    gremlin-console-3.3.0-SNAPSHOT.jar
    gremlin-core-3.3.0-SNAPSHOT.jar       
    gremlin-groovy-3.3.0-SNAPSHOT.jar     
    gremlin-shaded-3.3.0-SNAPSHOT.jar     
    hadoop-gremlin-3.3.0-SNAPSHOT.jar     
    spark-gremlin-3.3.0-SNAPSHOT.jar      
    tinkergraph-gremlin-3.3.0-SNAPSHOT.jar

    # Gremlin depedencies
    asm-3.2.jar                                
    avro-1.7.4.jar                             
    caffeine-2.3.1.jar                         
    cglib-2.2.1-v20090111.jar                  
    gbench-0.4.3-groovy-2.4.jar                
    gprof-0.3.1-groovy-2.4.jar                 
    groovy-2.4.9-indy.jar                      
    groovy-2.4.9.jar                           
    groovy-console-2.4.9.jar                   
    groovy-groovysh-2.4.9-indy.jar             
    groovy-json-2.4.9-indy.jar                 
    groovy-jsr223-2.4.9-indy.jar               
    groovy-sql-2.4.9-indy.jar                  
    groovy-swing-2.4.9.jar                     
    groovy-templates-2.4.9.jar                 
    groovy-xml-2.4.9.jar                       
    hadoop-yarn-server-nodemanager-2.7.2.jar   
    hppc-0.7.1.jar                             
    javatuples-1.2.jar                         
    jaxb-impl-2.2.3-1.jar                      
    jbcrypt-0.4.jar                            
    jcabi-log-0.14.jar                         
    jcabi-manifests-1.1.jar                    
    jersey-core-1.9.jar                        
    jersey-guice-1.9.jar                       
    jersey-json-1.9.jar                        
    jettison-1.1.jar                           
    scalatest_2.11-2.2.6.jar                   
    servlet-api-2.5.jar                        
    snakeyaml-1.15.jar                         
    unused-1.0.0.jar                           
    xml-apis-1.3.04.jar                        
    ```

## <a name="get-the-azure-cosmos-db-spark-connector"></a><span data-ttu-id="06274-144">Obter o conector Spark do BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="06274-144">Get the Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="06274-145">Obter o Conector Spark do BD Cosmos do Azure `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` e o SDK Java do BD Cosmos `azure-documentdb-1.10.0.jar` no [Conector Spark para BD Cosmos do Azure no GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="06274-145">Get the Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="06274-146">Como alternativa, você pode criá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="06274-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="06274-147">Como a versão mais recente do Spark-Gremlin foi criada com o Spark 1.6.1 e não é compatível com o Spark 2.0.2, que é usado atualmente no Conector Spark do BD Cosmos do Azure, você pode compilar o código TinkerPop3 mais recente e instalar os jars manualmente.</span><span class="sxs-lookup"><span data-stu-id="06274-147">Because the latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in the Azure Cosmos DB Spark connector, you can build the latest TinkerPop3 code and install the jars manually.</span></span> <span data-ttu-id="06274-148">Faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="06274-148">Do the following:</span></span>

    <span data-ttu-id="06274-149">a.</span><span class="sxs-lookup"><span data-stu-id="06274-149">a.</span></span> <span data-ttu-id="06274-150">Clone o conector Spark do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="06274-150">Clone the Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="06274-151">b.</span><span class="sxs-lookup"><span data-stu-id="06274-151">b.</span></span> <span data-ttu-id="06274-152">Crie o TinkerPop3 (já feito nas etapas anteriores).</span><span class="sxs-lookup"><span data-stu-id="06274-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="06274-153">Instale todos os jars TinkerPop 3.3.0-SNAPSHOT localmente.</span><span class="sxs-lookup"><span data-stu-id="06274-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="06274-154">c.</span><span class="sxs-lookup"><span data-stu-id="06274-154">c.</span></span> <span data-ttu-id="06274-155">Atualize `tinkerpop.version` `azure-documentdb-spark/pom.xml` para `3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="06274-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` to `3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="06274-156">d.</span><span class="sxs-lookup"><span data-stu-id="06274-156">d.</span></span> <span data-ttu-id="06274-157">Compile com Maven.</span><span class="sxs-lookup"><span data-stu-id="06274-157">Build with Maven.</span></span> <span data-ttu-id="06274-158">Os jars necessários são colocados em `target` e `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="06274-158">The needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="06274-159">Copie os jars mencionados anteriormente para um diretório local em ~/azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="06274-159">Copy the previously mentioned jars to a local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-the-dependencies-to-the-spark-worker-nodes"></a><span data-ttu-id="06274-160">Distribuir as dependências nos nós de trabalho Spark</span><span class="sxs-lookup"><span data-stu-id="06274-160">Distribute the dependencies to the Spark worker nodes</span></span> 

1. <span data-ttu-id="06274-161">Como a transformação de dados do gráfico depende do TinkerPop3, você precisa distribuir as dependências relacionadas para todos os nós de trabalho Spark.</span><span class="sxs-lookup"><span data-stu-id="06274-161">Because the transformation of graph data depends on TinkerPop3, you must distribute the related dependencies to all Spark worker nodes.</span></span>

2. <span data-ttu-id="06274-162">Copie as dependências do Gremlin mencionadas anteriormente, além do jar conector Spark do CosmosDB e do SDK Java do CosmosDB para os nós de trabalho fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="06274-162">Copy the previously mentioned Gremlin dependencies, the CosmosDB Spark connector jar, and CosmosDB Java SDK to the worker nodes by doing the following:</span></span>

    <span data-ttu-id="06274-163">a.</span><span class="sxs-lookup"><span data-stu-id="06274-163">a.</span></span> <span data-ttu-id="06274-164">Copie todos os jars em `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="06274-164">Copy all the jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="06274-165">b.</span><span class="sxs-lookup"><span data-stu-id="06274-165">b.</span></span> <span data-ttu-id="06274-166">Obtenha a lista de todos os nós de trabalho Spark encontrados no painel do Ambari, na lista `Spark2 Clients` da seção `Spark2`.</span><span class="sxs-lookup"><span data-stu-id="06274-166">Get the list of all Spark worker nodes, which you can find on Ambari Dashboard, in the `Spark2 Clients` list in the `Spark2` section.</span></span>

    <span data-ttu-id="06274-167">c.</span><span class="sxs-lookup"><span data-stu-id="06274-167">c.</span></span> <span data-ttu-id="06274-168">Copiar o diretório para cada um dos nós.</span><span class="sxs-lookup"><span data-stu-id="06274-168">Copy that directory to each of the nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-the-environment-variables"></a><span data-ttu-id="06274-169">Configurar as variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="06274-169">Set up the environment variables</span></span>

1. <span data-ttu-id="06274-170">Localize a versão HDP do cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="06274-170">Find the HDP version of the Spark cluster.</span></span> <span data-ttu-id="06274-171">É o nome do diretório em `/usr/hdp/` (por exemplo, 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="06274-171">It is the directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="06274-172">Defina hdp.version para todos os nós.</span><span class="sxs-lookup"><span data-stu-id="06274-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="06274-173">No painel do Ambari, vá para a **seção YARN** > **Configurações** > **Avançado** e faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="06274-173">In Ambari Dashboard, go to **YARN section** > **Configs** > **Advanced**, and then do the following:</span></span> 
 
    <span data-ttu-id="06274-174">a.</span><span class="sxs-lookup"><span data-stu-id="06274-174">a.</span></span> <span data-ttu-id="06274-175">Em `Custom yarn-site`, adicione uma nova propriedade `hdp.version` com o valor da versão do HDP no nó principal.</span><span class="sxs-lookup"><span data-stu-id="06274-175">In `Custom yarn-site`, add a new property `hdp.version` with the value of the HDP version on the master node.</span></span> 
     
    <span data-ttu-id="06274-176">b.</span><span class="sxs-lookup"><span data-stu-id="06274-176">b.</span></span> <span data-ttu-id="06274-177">Salve as configurações.</span><span class="sxs-lookup"><span data-stu-id="06274-177">Save the configurations.</span></span> <span data-ttu-id="06274-178">Existem avisos, mas eles podem ser ignorados.</span><span class="sxs-lookup"><span data-stu-id="06274-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="06274-179">c.</span><span class="sxs-lookup"><span data-stu-id="06274-179">c.</span></span> <span data-ttu-id="06274-180">Reinicie os serviços YARN e Oozie conforme indicado pelos ícones de notificação.</span><span class="sxs-lookup"><span data-stu-id="06274-180">Restart the YARN and Oozie services as the notification icons indicate.</span></span>

3. <span data-ttu-id="06274-181">Defina as seguintes variáveis de ambiente no nó principal (substitua os valores conforme apropriado):</span><span class="sxs-lookup"><span data-stu-id="06274-181">Set the following environment variables on the master node (replace the values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-the-graph-configuration"></a><span data-ttu-id="06274-182">Preparar a configuração do gráfico</span><span class="sxs-lookup"><span data-stu-id="06274-182">Prepare the graph configuration</span></span>

1. <span data-ttu-id="06274-183">Crie um arquivo de configuração com os parâmetros de conexão do BD Cosmos do Azure e as configurações do Spark e coloque-o em`tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="06274-183">Create a configuration file with the Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

    ```
    gremlin.graph=org.apache.tinkerpop.gremlin.hadoop.structure.HadoopGraph
    gremlin.hadoop.jarsInDistributedCache=true
    gremlin.hadoop.defaultGraphComputer=org.apache.tinkerpop.gremlin.spark.process.computer.SparkGraphComputer

    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    gremlin.hadoop.graphWriter=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBOutputRDD

    ####################################
    # SparkGraphComputer Configuration #
    ####################################
    spark.master=yarn
    spark.executor.memory=3g
    spark.executor.instances=6
    spark.serializer=org.apache.spark.serializer.KryoSerializer
    spark.kryo.registrator=org.apache.tinkerpop.gremlin.spark.structure.io.gryo.GryoRegistrator
    gremlin.spark.persistContext=true

    # Classpath for the driver and executors
    spark.driver.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    spark.executor.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    
    ######################################
    # DocumentDB Spark connector         #
    ######################################
    spark.documentdb.connectionMode=Gateway
    spark.documentdb.schema_samplingratio=1.0
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    spark.documentdb.preferredRegions=FILLIN
    ```

2. <span data-ttu-id="06274-184">Atualize `spark.driver.extraClassPath` e `spark.executor.extraClassPath` para incluir o diretório dos jars distribuído na etapa anterior, neste caso, `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="06274-184">Update the `spark.driver.extraClassPath` and `spark.executor.extraClassPath` to include the directory of the jars that you distributed in the previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="06274-185">Forneça os seguintes detalhes para o BD Cosmos do Azure:</span><span class="sxs-lookup"><span data-stu-id="06274-185">Provide the following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-the-tinkerpop-graph-and-save-it-to-azure-cosmos-db"></a><span data-ttu-id="06274-186">Carregar o gráfico do TinkerPop e salve-o no BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="06274-186">Load the TinkerPop graph, and save it to Azure Cosmos DB</span></span>
<span data-ttu-id="06274-187">Para demonstrar como persistir um gráfico no BD Cosmos do Azure, este exemplo usa o gráfico moderno TinkerPop predefinido.</span><span class="sxs-lookup"><span data-stu-id="06274-187">To demonstrate how to persist a graph into Azure Cosmos DB, this example uses the TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="06274-188">O gráfico é armazenado no formato Kryo e fornecido no repositório TinkerPop.</span><span class="sxs-lookup"><span data-stu-id="06274-188">The graph is stored in Kryo format, and it's provided in the TinkerPop repository.</span></span>

1. <span data-ttu-id="06274-189">Como você está executando o Gremlin no modo YARN, deve disponibilizar os dados do gráfico no sistema de arquivos Hadoop.</span><span class="sxs-lookup"><span data-stu-id="06274-189">Because you are running Gremlin in YARN mode, you must make the graph data available in the Hadoop file system.</span></span> <span data-ttu-id="06274-190">Use os comandos a seguir para criar um diretório e copiam o arquivo do gráfico local nele.</span><span class="sxs-lookup"><span data-stu-id="06274-190">Use the following commands to make a directory and copy the local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="06274-191">Atualize temporariamente o arquivo `gremlin-spark.properties` para usar `GryoInputFormat` e ler o gráfico.</span><span class="sxs-lookup"><span data-stu-id="06274-191">Temporarily update the `gremlin-spark.properties` file to use `GryoInputFormat` to read the graph.</span></span> <span data-ttu-id="06274-192">Indique também `inputLocation` como o diretório criado, como no exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="06274-192">Also indicate `inputLocation` as the directory you create, as in the following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="06274-193">Inicie o Console do Gremlin e crie as seguintes etapas de computação para persistir dados para a coleção do BD Cosmos do Azure configurada:</span><span class="sxs-lookup"><span data-stu-id="06274-193">Start Gremlin Console, and then create the following computation steps to persist data to the configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="06274-194">a.</span><span class="sxs-lookup"><span data-stu-id="06274-194">a.</span></span> <span data-ttu-id="06274-195">Crie o gráfico `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="06274-195">Create the graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="06274-196">b.</span><span class="sxs-lookup"><span data-stu-id="06274-196">b.</span></span> <span data-ttu-id="06274-197">Use SparkGraphComputer para gravar `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="06274-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[gryoinputformat->documentdboutputrdd]
    gremlin> hg = graph.
                compute(SparkGraphComputer.class).
                result(GraphComputer.ResultGraph.NEW).
                persist(GraphComputer.Persist.EDGES).
                program(TraversalVertexProgram.build().
                    traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)), "gremlin-groovy", "g.V()").
                    create(graph)).
                submit().
                get() 
    ==>result[hadoopgraph[documentdbinputrdd->documentdboutputrdd],memory[size:1]]
    ```

4. <span data-ttu-id="06274-198">No Data Explorer, você pode verificar se os dados foram persistidos para o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="06274-198">From Data Explorer, you can verify that the data has been persisted to Azure Cosmos DB.</span></span>

## <a name="load-the-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="06274-199">Carregue o gráfico do BD Cosmos do Azure e execute consultas do Gremlin</span><span class="sxs-lookup"><span data-stu-id="06274-199">Load the graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="06274-200">Para carregar o gráfico, edite `gremlin-spark.properties` para definir `graphReader` como `DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="06274-200">To load the graph, edit `gremlin-spark.properties` to set `graphReader` to `DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="06274-201">Carregue o gráfico, percorra os dados e execute consultas do Gremlin com ele fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="06274-201">Load the graph, traverse the data, and run Gremlin queries with it by doing the following:</span></span>

    <span data-ttu-id="06274-202">a.</span><span class="sxs-lookup"><span data-stu-id="06274-202">a.</span></span> <span data-ttu-id="06274-203">Inicie o Console do Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="06274-203">Start the Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="06274-204">b.</span><span class="sxs-lookup"><span data-stu-id="06274-204">b.</span></span> <span data-ttu-id="06274-205">Crie um gráfico com as configurações`graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="06274-205">Create the graph with the configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="06274-206">c.</span><span class="sxs-lookup"><span data-stu-id="06274-206">c.</span></span> <span data-ttu-id="06274-207">Crie uma passagem de gráfico com SparkGraphComputer`g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="06274-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="06274-208">d.</span><span class="sxs-lookup"><span data-stu-id="06274-208">d.</span></span> <span data-ttu-id="06274-209">Execute as seguintes consultas de gráfico do Gremlin:</span><span class="sxs-lookup"><span data-stu-id="06274-209">Run the following Gremlin graph queries:</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[documentdbinputrdd->documentdboutputrdd]
    gremlin> g = graph.traversal().withComputer(SparkGraphComputer)
    ==>graphtraversalsource[hadoopgraph[documentdbinputrdd->documentdboutputrdd], sparkgraphcomputer]
    gremlin> g.V().count()
    ==>6
    gremlin> g.E().count()
    ==>6
    gremlin> g.V(1).out().values('name')
    ==>josh
    ==>vadas
    ==>lop
    gremlin> g.V().hasLabel('person').coalesce(values('nickname'), values('name'))
    ==>josh
    ==>peter
    ==>vadas
    ==>marko
    gremlin> g.V().hasLabel('person').
            choose(values('name')).
                option('marko', values('age')).
                option('josh', values('name')).
                option('vadas', valueMap()).
                option('peter', label())
    ==>josh
    ==>person
    ==>[name:[vadas],age:[27]]
    ==>29
    ```

> [!NOTE]
> <span data-ttu-id="06274-210">Para ver o log mais detalhado, defina o log de nível em `conf/log4j-console.properties` como um nível mais detalhado.</span><span class="sxs-lookup"><span data-stu-id="06274-210">To see more detailed logging, set the log level in `conf/log4j-console.properties` to a more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="06274-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="06274-211">Next steps</span></span>

<span data-ttu-id="06274-212">Este artigo de início rápido, você aprendeu como trabalhar com gráficos, combinando o banco de dados do Azure Cosmos e Spark.</span><span class="sxs-lookup"><span data-stu-id="06274-212">In this quick-start article, you've learned how to work with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
