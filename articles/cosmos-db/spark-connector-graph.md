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
ms.openlocfilehash: 0be5c9b12cdba4a428c809d00e1e68785a9ec1ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="58634-103">BD Cosmos do Azure: executar análise de gráfico usando o Spark e o Gremlin do Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="58634-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="58634-104">[Banco de dados do Azure Cosmos](introduction.md) é Olá globalmente distribuídos vários modelos de banco de dados de serviço da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="58634-104">[Azure Cosmos DB](introduction.md) is hello globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="58634-105">Você pode criar e consultar bancos de dados do gráfico, de aproveitar os recursos de distribuição global e escala horizontal Olá principais hello Azure Cosmos DB de documento e chave/valor.</span><span class="sxs-lookup"><span data-stu-id="58634-105">You can create and query document, key/value, and graph databases, all of which benefit from hello global-distribution and horizontal-scale capabilities at hello core of Azure Cosmos DB.</span></span> <span data-ttu-id="58634-106">O BD Costmos do Azure dá suporte a cargas de trabalho gráficas OLTP (processamento de transações online) que usam o [Gremlin do Apache TinkerPop](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="58634-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="58634-107">[Spark](http://spark.apache.org/) é um projeto Apache Software Foundation voltado para o processamento de dados OLAP (processamento analítico online de uso geral).</span><span class="sxs-lookup"><span data-stu-id="58634-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="58634-108">Spark fornece na memória/baseado em disco distribuído computação modelo híbrido que seja semelhante toohello Hadoop MapReduce modelo.</span><span class="sxs-lookup"><span data-stu-id="58634-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar toohello Hadoop MapReduce model.</span></span> <span data-ttu-id="58634-109">Você pode implantar o Apache Spark na nuvem hello usando [HDInsight do Azure](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="58634-109">You can deploy Apache Spark in hello cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="58634-110">Combinando o BD Cosmos do Azure e o Spark, você pode executar cargas de trabalho OLTP e OLAP quando usar o Gremlin.</span><span class="sxs-lookup"><span data-stu-id="58634-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="58634-111">Este artigo de início rápido demonstra como toorun Gremlin consultas no banco de dados do Azure Cosmos em um cluster Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58634-111">This quick-start article demonstrates how toorun Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58634-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="58634-112">Prerequisites</span></span>

<span data-ttu-id="58634-113">Antes de executar este exemplo, você deve ter Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="58634-113">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="58634-114">Cluster Spark do Azure HDInsight 2.0</span><span class="sxs-lookup"><span data-stu-id="58634-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="58634-115">JDK 1.8 + (execute `apt-get install default-jdk` se você não tiver o JDK)</span><span class="sxs-lookup"><span data-stu-id="58634-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="58634-116">Maven (execute `apt-get install maven` se você não tiver o Maven)</span><span class="sxs-lookup"><span data-stu-id="58634-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="58634-117">Uma assinatura do Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="58634-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="58634-118">Para obter informações sobre como tooset um cluster Spark no HDInsight, consulte [clusters HDInsight provisionamento](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="58634-118">For information about how tooset up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="58634-119">Criar uma conta de banco de dados BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="58634-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="58634-120">Primeiro, crie uma conta de banco de dados com hello API do Graph fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="58634-120">First, create a database account with hello Graph API by doing hello following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="58634-121">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="58634-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="58634-122">Obter o Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="58634-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="58634-123">Obter Apache TinkerPop fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="58634-123">Get Apache TinkerPop by doing hello following:</span></span>

1. <span data-ttu-id="58634-124">Nó mestre de toohello remoto de cluster do HDInsight Olá `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="58634-124">Remote toohello master node of hello HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="58634-125">Clonar o código-fonte TinkerPop3 Olá, compilá-lo localmente e instalá-lo tooMaven cache.</span><span class="sxs-lookup"><span data-stu-id="58634-125">Clone hello TinkerPop3 source code, build it locally, and install it tooMaven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="58634-126">Instalar Olá Spark-Gremlin plug-in</span><span class="sxs-lookup"><span data-stu-id="58634-126">Install hello Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="58634-127">a.</span><span class="sxs-lookup"><span data-stu-id="58634-127">a.</span></span> <span data-ttu-id="58634-128">instalação de saudação do plug-in de saudação é tratada pelo Uva.</span><span class="sxs-lookup"><span data-stu-id="58634-128">hello installation of hello plug-in is handled by Grape.</span></span> <span data-ttu-id="58634-129">Preencha informações de repositórios de saudação para Uva para que possa baixar hello plug-in e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="58634-129">Populate hello repositories information for Grape so it can download hello plug-in and its dependencies.</span></span> 

      <span data-ttu-id="58634-130">Criar arquivo de configuração de Uva de saudação se ele não está presente no `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="58634-130">Create hello grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="58634-131">Saudação de usar as configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="58634-131">Use hello following settings:</span></span>

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

    <span data-ttu-id="58634-132">b.</span><span class="sxs-lookup"><span data-stu-id="58634-132">b.</span></span> <span data-ttu-id="58634-133">Inicie o console do Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="58634-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="58634-134">c.</span><span class="sxs-lookup"><span data-stu-id="58634-134">c.</span></span> <span data-ttu-id="58634-135">Instale Olá Spark-Gremlin plug-in com a versão 3.3.0-SNAPSHOT, que você criou nas etapas anteriores hello:</span><span class="sxs-lookup"><span data-stu-id="58634-135">Install hello Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in hello previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart hello console toouse [tinkerpop.spark]
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

4. <span data-ttu-id="58634-136">Verifique se o toosee `Hadoop-Gremlin` é ativada com `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="58634-136">Check toosee whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="58634-137">Desabilitar este plug-in, porque ele pode interferir na Olá Spark Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="58634-137">Disable this plug-in, because it could interfere with hello Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="58634-138">Preparar dependências TinkerPop3</span><span class="sxs-lookup"><span data-stu-id="58634-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="58634-139">Quando você compilou TinkerPop3 na etapa anterior hello, o processo Olá também extraída todas as dependências de jar para Spark e Hadoop no diretório de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="58634-139">When you built TinkerPop3 in hello previous step, hello process also pulled all jar dependencies for Spark and Hadoop in hello target directory.</span></span> <span data-ttu-id="58634-140">Use os jars Olá pré-instalado com HDI e recepção em dependências adicionais conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="58634-140">Use hello jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="58634-141">Diretório de destino do Console Gremlin toohello vá em `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="58634-141">Go toohello Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="58634-142">Mover todos os jars em `ext/` muito`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="58634-142">Move all jars under `ext/` too`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="58634-143">Remover todos os jar bibliotecas em `lib/` que não está em Olá a seguir lista:</span><span class="sxs-lookup"><span data-stu-id="58634-143">Remove all jar libraries under `lib/` that are not in hello following list:</span></span>

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

## <a name="get-hello-azure-cosmos-db-spark-connector"></a><span data-ttu-id="58634-144">Obter o conector do Azure Cosmos DB Spark Olá</span><span class="sxs-lookup"><span data-stu-id="58634-144">Get hello Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="58634-145">Obter o conector do Azure Cosmos DB Spark Olá `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` e SDK do Java DB Cosmos `azure-documentdb-1.10.0.jar` de [conector do Azure Cosmos DB Spark no GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="58634-145">Get hello Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="58634-146">Como alternativa, você pode criá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="58634-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="58634-147">Porque a versão mais recente de saudação do Spark Gremlin foi desenvolvido com Spark 1.6.1 e não é compatível com Spark 2.0.2, que está sendo usado no conector do Azure Cosmos DB Spark hello, você pode criar código mais recente de TinkerPop3 hello e instalar o hello jars manualmente.</span><span class="sxs-lookup"><span data-stu-id="58634-147">Because hello latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in hello Azure Cosmos DB Spark connector, you can build hello latest TinkerPop3 code and install hello jars manually.</span></span> <span data-ttu-id="58634-148">Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="58634-148">Do hello following:</span></span>

    <span data-ttu-id="58634-149">a.</span><span class="sxs-lookup"><span data-stu-id="58634-149">a.</span></span> <span data-ttu-id="58634-150">Clone um conector do Azure Cosmos DB Spark hello.</span><span class="sxs-lookup"><span data-stu-id="58634-150">Clone hello Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="58634-151">b.</span><span class="sxs-lookup"><span data-stu-id="58634-151">b.</span></span> <span data-ttu-id="58634-152">Crie o TinkerPop3 (já feito nas etapas anteriores).</span><span class="sxs-lookup"><span data-stu-id="58634-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="58634-153">Instale todos os jars TinkerPop 3.3.0-SNAPSHOT localmente.</span><span class="sxs-lookup"><span data-stu-id="58634-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="58634-154">c.</span><span class="sxs-lookup"><span data-stu-id="58634-154">c.</span></span> <span data-ttu-id="58634-155">Atualização `tinkerpop.version` `azure-documentdb-spark/pom.xml` muito`3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="58634-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` too`3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="58634-156">d.</span><span class="sxs-lookup"><span data-stu-id="58634-156">d.</span></span> <span data-ttu-id="58634-157">Compile com Maven.</span><span class="sxs-lookup"><span data-stu-id="58634-157">Build with Maven.</span></span> <span data-ttu-id="58634-158">Olá jars necessários são colocados em `target` e `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="58634-158">hello needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="58634-159">Saudação de cópia mencionado anteriormente diretório local do jars tooa em ~ / azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="58634-159">Copy hello previously mentioned jars tooa local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a><span data-ttu-id="58634-160">Distribuir nós de trabalho Olá dependências toohello Spark</span><span class="sxs-lookup"><span data-stu-id="58634-160">Distribute hello dependencies toohello Spark worker nodes</span></span> 

1. <span data-ttu-id="58634-161">Como transformação Olá de gráficos de dados depende de TinkerPop3, você deve distribuir Olá relacionados nós de trabalho dependências tooall Spark.</span><span class="sxs-lookup"><span data-stu-id="58634-161">Because hello transformation of graph data depends on TinkerPop3, you must distribute hello related dependencies tooall Spark worker nodes.</span></span>

2. <span data-ttu-id="58634-162">Saudação de cópia mencionado anteriormente Gremlin dependências, Olá jar do conector CosmosDB Spark e nós de trabalho do SDK do Java CosmosDB toohello fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="58634-162">Copy hello previously mentioned Gremlin dependencies, hello CosmosDB Spark connector jar, and CosmosDB Java SDK toohello worker nodes by doing hello following:</span></span>

    <span data-ttu-id="58634-163">a.</span><span class="sxs-lookup"><span data-stu-id="58634-163">a.</span></span> <span data-ttu-id="58634-164">Copiar todos os jars Olá em `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="58634-164">Copy all hello jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="58634-165">b.</span><span class="sxs-lookup"><span data-stu-id="58634-165">b.</span></span> <span data-ttu-id="58634-166">Obter lista de saudação de todos os nós de trabalho Spark, que você pode encontrar no painel do Ambari, no hello `Spark2 Clients` lista Olá `Spark2` seção.</span><span class="sxs-lookup"><span data-stu-id="58634-166">Get hello list of all Spark worker nodes, which you can find on Ambari Dashboard, in hello `Spark2 Clients` list in hello `Spark2` section.</span></span>

    <span data-ttu-id="58634-167">c.</span><span class="sxs-lookup"><span data-stu-id="58634-167">c.</span></span> <span data-ttu-id="58634-168">Copie esse tooeach diretório de nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="58634-168">Copy that directory tooeach of hello nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a><span data-ttu-id="58634-169">Definir variáveis de ambiente Olá</span><span class="sxs-lookup"><span data-stu-id="58634-169">Set up hello environment variables</span></span>

1. <span data-ttu-id="58634-170">Localize Olá HDP versão de cluster do Spark hello.</span><span class="sxs-lookup"><span data-stu-id="58634-170">Find hello HDP version of hello Spark cluster.</span></span> <span data-ttu-id="58634-171">Ele é o nome do diretório de saudação em `/usr/hdp/` (por exemplo, 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="58634-171">It is hello directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="58634-172">Defina hdp.version para todos os nós.</span><span class="sxs-lookup"><span data-stu-id="58634-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="58634-173">No painel do Ambari, vá muito**seção YARN** > **configurações** > **avançado**e, em seguida, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="58634-173">In Ambari Dashboard, go too**YARN section** > **Configs** > **Advanced**, and then do hello following:</span></span> 
 
    <span data-ttu-id="58634-174">a.</span><span class="sxs-lookup"><span data-stu-id="58634-174">a.</span></span> <span data-ttu-id="58634-175">Em `Custom yarn-site`, adicione uma nova propriedade `hdp.version` com valor de saudação da versão do HDP Olá no nó mestre hello.</span><span class="sxs-lookup"><span data-stu-id="58634-175">In `Custom yarn-site`, add a new property `hdp.version` with hello value of hello HDP version on hello master node.</span></span> 
     
    <span data-ttu-id="58634-176">b.</span><span class="sxs-lookup"><span data-stu-id="58634-176">b.</span></span> <span data-ttu-id="58634-177">Salve configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="58634-177">Save hello configurations.</span></span> <span data-ttu-id="58634-178">Existem avisos, mas eles podem ser ignorados.</span><span class="sxs-lookup"><span data-stu-id="58634-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="58634-179">c.</span><span class="sxs-lookup"><span data-stu-id="58634-179">c.</span></span> <span data-ttu-id="58634-180">Reinicie os serviços YARN e Oozie hello como ícones de notificação Olá indicam.</span><span class="sxs-lookup"><span data-stu-id="58634-180">Restart hello YARN and Oozie services as hello notification icons indicate.</span></span>

3. <span data-ttu-id="58634-181">Saudação de conjunto de variáveis de ambiente a seguir no nó mestre da saudação (substituir valores de saudação conforme apropriado):</span><span class="sxs-lookup"><span data-stu-id="58634-181">Set hello following environment variables on hello master node (replace hello values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a><span data-ttu-id="58634-182">Preparar a configuração de gráfico Olá</span><span class="sxs-lookup"><span data-stu-id="58634-182">Prepare hello graph configuration</span></span>

1. <span data-ttu-id="58634-183">Criar um arquivo de configuração com hello parâmetros de conexão de banco de dados do Azure Cosmos despertar configurações e colocá-la em `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="58634-183">Create a configuration file with hello Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

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

    # Classpath for hello driver and executors
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

2. <span data-ttu-id="58634-184">Saudação de atualização `spark.driver.extraClassPath` e `spark.executor.extraClassPath` tooinclude diretório de saudação do jars Olá que você tenha distribuído na etapa anterior de saudação, nesse caso `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="58634-184">Update hello `spark.driver.extraClassPath` and `spark.executor.extraClassPath` tooinclude hello directory of hello jars that you distributed in hello previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="58634-185">Fornece Olá detalhes a seguir para o banco de dados do Azure Cosmos:</span><span class="sxs-lookup"><span data-stu-id="58634-185">Provide hello following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a><span data-ttu-id="58634-186">Carregar o gráfico de TinkerPop hello e salve-o tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="58634-186">Load hello TinkerPop graph, and save it tooAzure Cosmos DB</span></span>
<span data-ttu-id="58634-187">toodemonstrate como toopersist um gráfico em Azure Cosmos DB, este exemplo usa Olá TinkerPop predefinidos gráfico moderno TinkerPop.</span><span class="sxs-lookup"><span data-stu-id="58634-187">toodemonstrate how toopersist a graph into Azure Cosmos DB, this example uses hello TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="58634-188">gráfico de saudação é armazenado no formato de Kryo e ele é fornecido no repositório de TinkerPop hello.</span><span class="sxs-lookup"><span data-stu-id="58634-188">hello graph is stored in Kryo format, and it's provided in hello TinkerPop repository.</span></span>

1. <span data-ttu-id="58634-189">Porque você está executando Gremlin no modo YARN, você deve tornar dados de gráfico de saudação disponível no sistema de arquivos Hadoop de saudação.</span><span class="sxs-lookup"><span data-stu-id="58634-189">Because you are running Gremlin in YARN mode, you must make hello graph data available in hello Hadoop file system.</span></span> <span data-ttu-id="58634-190">A seguir Olá use comandos toomake um diretório e copiar arquivo de gráfico local Olá nele.</span><span class="sxs-lookup"><span data-stu-id="58634-190">Use hello following commands toomake a directory and copy hello local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="58634-191">Atualizar temporariamente Olá `gremlin-spark.properties` arquivo toouse `GryoInputFormat` tooread gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="58634-191">Temporarily update hello `gremlin-spark.properties` file toouse `GryoInputFormat` tooread hello graph.</span></span> <span data-ttu-id="58634-192">Também indicar `inputLocation` como diretório de saudação criar, como no seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="58634-192">Also indicate `inputLocation` as hello directory you create, as in hello following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="58634-193">Inicie o Console de Gremlin e, em seguida, criar hello computação etapas toopersist toohello configurado o banco de dados do Azure Cosmos a coleta de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="58634-193">Start Gremlin Console, and then create hello following computation steps toopersist data toohello configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="58634-194">a.</span><span class="sxs-lookup"><span data-stu-id="58634-194">a.</span></span> <span data-ttu-id="58634-195">Criar um gráfico de saudação `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="58634-195">Create hello graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="58634-196">b.</span><span class="sxs-lookup"><span data-stu-id="58634-196">b.</span></span> <span data-ttu-id="58634-197">Use SparkGraphComputer para gravar `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="58634-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

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

4. <span data-ttu-id="58634-198">Explorador de dados, você pode verificar que Olá dos dados persistentes tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="58634-198">From Data Explorer, you can verify that hello data has been persisted tooAzure Cosmos DB.</span></span>

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="58634-199">Carregar o gráfico de saudação do banco de dados do Azure Cosmos e executar consultas Gremlin</span><span class="sxs-lookup"><span data-stu-id="58634-199">Load hello graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="58634-200">gráfico de saudação tooload, editar `gremlin-spark.properties` tooset `graphReader` muito`DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="58634-200">tooload hello graph, edit `gremlin-spark.properties` tooset `graphReader` too`DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="58634-201">Gráfico de saudação de carga, percorrer Olá dados e executar consultas de Gremlin com ele fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="58634-201">Load hello graph, traverse hello data, and run Gremlin queries with it by doing hello following:</span></span>

    <span data-ttu-id="58634-202">a.</span><span class="sxs-lookup"><span data-stu-id="58634-202">a.</span></span> <span data-ttu-id="58634-203">Iniciar Olá Console Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="58634-203">Start hello Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="58634-204">b.</span><span class="sxs-lookup"><span data-stu-id="58634-204">b.</span></span> <span data-ttu-id="58634-205">Criar o gráfico de saudação com a configuração de saudação `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="58634-205">Create hello graph with hello configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="58634-206">c.</span><span class="sxs-lookup"><span data-stu-id="58634-206">c.</span></span> <span data-ttu-id="58634-207">Crie uma passagem de gráfico com SparkGraphComputer`g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="58634-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="58634-208">d.</span><span class="sxs-lookup"><span data-stu-id="58634-208">d.</span></span> <span data-ttu-id="58634-209">Olá executar consultas de gráfico Gremlin a seguir:</span><span class="sxs-lookup"><span data-stu-id="58634-209">Run hello following Gremlin graph queries:</span></span>

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
> <span data-ttu-id="58634-210">toosee mais detalhada registro em log, definir o nível de log de saudação `conf/log4j-console.properties` tooa nível mais detalhado.</span><span class="sxs-lookup"><span data-stu-id="58634-210">toosee more detailed logging, set hello log level in `conf/log4j-console.properties` tooa more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="58634-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="58634-211">Next steps</span></span>

<span data-ttu-id="58634-212">Este artigo de início rápido, você aprendeu como toowork com gráficos, combinando o banco de dados do Azure Cosmos e Spark.</span><span class="sxs-lookup"><span data-stu-id="58634-212">In this quick-start article, you've learned how toowork with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
