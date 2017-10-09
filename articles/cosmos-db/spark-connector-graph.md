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
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a>BD Cosmos do Azure: executar análise de gráfico usando o Spark e o Gremlin do Apache TinkerPop

[Banco de dados do Azure Cosmos](introduction.md) é Olá globalmente distribuídos vários modelos de banco de dados de serviço da Microsoft. Você pode criar e consultar bancos de dados do gráfico, de aproveitar os recursos de distribuição global e escala horizontal Olá principais hello Azure Cosmos DB de documento e chave/valor. O BD Costmos do Azure dá suporte a cargas de trabalho gráficas OLTP (processamento de transações online) que usam o [Gremlin do Apache TinkerPop](graph-introduction.md).

[Spark](http://spark.apache.org/) é um projeto Apache Software Foundation voltado para o processamento de dados OLAP (processamento analítico online de uso geral). Spark fornece na memória/baseado em disco distribuído computação modelo híbrido que seja semelhante toohello Hadoop MapReduce modelo. Você pode implantar o Apache Spark na nuvem hello usando [HDInsight do Azure](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Combinando o BD Cosmos do Azure e o Spark, você pode executar cargas de trabalho OLTP e OLAP quando usar o Gremlin. Este artigo de início rápido demonstra como toorun Gremlin consultas no banco de dados do Azure Cosmos em um cluster Spark no HDInsight.

## <a name="prerequisites"></a>Pré-requisitos

Antes de executar este exemplo, você deve ter Olá pré-requisitos a seguir:
* Cluster Spark do Azure HDInsight 2.0
* JDK 1.8 + (execute `apt-get install default-jdk` se você não tiver o JDK)
* Maven (execute `apt-get install maven` se você não tiver o Maven)
* Uma assinatura do Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])

Para obter informações sobre como tooset um cluster Spark no HDInsight, consulte [clusters HDInsight provisionamento](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

## <a name="create-an-azure-cosmos-db-database-account"></a>Criar uma conta de banco de dados BD Cosmos do Azure

Primeiro, crie uma conta de banco de dados com hello API do Graph fazendo Olá seguinte:

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Adicionar uma coleção

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a>Obter o Apache TinkerPop

Obter Apache TinkerPop fazendo Olá seguinte:

1. Nó mestre de toohello remoto de cluster do HDInsight Olá `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.

2. Clonar o código-fonte TinkerPop3 Olá, compilá-lo localmente e instalá-lo tooMaven cache.

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. Instalar Olá Spark-Gremlin plug-in 

    a. instalação de saudação do plug-in de saudação é tratada pelo Uva. Preencha informações de repositórios de saudação para Uva para que possa baixar hello plug-in e suas dependências. 

      Criar arquivo de configuração de Uva de saudação se ele não está presente no `~/.groovy/grapeConfig.xml`. Saudação de usar as configurações a seguir:

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

    b. Inicie o console do Gremlin `bin/gremlin.sh`.
        
    c. Instale Olá Spark-Gremlin plug-in com a versão 3.3.0-SNAPSHOT, que você criou nas etapas anteriores hello:

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

4. Verifique se o toosee `Hadoop-Gremlin` é ativada com `:plugin list`. Desabilitar este plug-in, porque ele pode interferir na Olá Spark Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.

## <a name="prepare-tinkerpop3-dependencies"></a>Preparar dependências TinkerPop3

Quando você compilou TinkerPop3 na etapa anterior hello, o processo Olá também extraída todas as dependências de jar para Spark e Hadoop no diretório de destino de saudação. Use os jars Olá pré-instalado com HDI e recepção em dependências adicionais conforme necessário.

1. Diretório de destino do Console Gremlin toohello vá em `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`. 

2. Mover todos os jars em `ext/` muito`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.

3. Remover todos os jar bibliotecas em `lib/` que não está em Olá a seguir lista:

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

## <a name="get-hello-azure-cosmos-db-spark-connector"></a>Obter o conector do Azure Cosmos DB Spark Olá

1. Obter o conector do Azure Cosmos DB Spark Olá `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` e SDK do Java DB Cosmos `azure-documentdb-1.10.0.jar` de [conector do Azure Cosmos DB Spark no GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).

2. Como alternativa, você pode criá-lo localmente. Porque a versão mais recente de saudação do Spark Gremlin foi desenvolvido com Spark 1.6.1 e não é compatível com Spark 2.0.2, que está sendo usado no conector do Azure Cosmos DB Spark hello, você pode criar código mais recente de TinkerPop3 hello e instalar o hello jars manualmente. Olá a seguir:

    a. Clone um conector do Azure Cosmos DB Spark hello.

    b. Crie o TinkerPop3 (já feito nas etapas anteriores). Instale todos os jars TinkerPop 3.3.0-SNAPSHOT localmente.

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    c. Atualização `tinkerpop.version` `azure-documentdb-spark/pom.xml` muito`3.3.0-SNAPSHOT`.
    
    d. Compile com Maven. Olá jars necessários são colocados em `target` e `target/alternateLocation`.

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. Saudação de cópia mencionado anteriormente diretório local do jars tooa em ~ / azure-documentdb-spark:

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a>Distribuir nós de trabalho Olá dependências toohello Spark 

1. Como transformação Olá de gráficos de dados depende de TinkerPop3, você deve distribuir Olá relacionados nós de trabalho dependências tooall Spark.

2. Saudação de cópia mencionado anteriormente Gremlin dependências, Olá jar do conector CosmosDB Spark e nós de trabalho do SDK do Java CosmosDB toohello fazendo Olá seguinte:

    a. Copiar todos os jars Olá em `~/azure-documentdb-spark`.

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    b. Obter lista de saudação de todos os nós de trabalho Spark, que você pode encontrar no painel do Ambari, no hello `Spark2 Clients` lista Olá `Spark2` seção.

    c. Copie esse tooeach diretório de nós de saudação.

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a>Definir variáveis de ambiente Olá

1. Localize Olá HDP versão de cluster do Spark hello. Ele é o nome do diretório de saudação em `/usr/hdp/` (por exemplo, 2.5.4.2-7).

2. Defina hdp.version para todos os nós. No painel do Ambari, vá muito**seção YARN** > **configurações** > **avançado**e, em seguida, Olá a seguir: 
 
    a. Em `Custom yarn-site`, adicione uma nova propriedade `hdp.version` com valor de saudação da versão do HDP Olá no nó mestre hello. 
     
    b. Salve configurações de saudação. Existem avisos, mas eles podem ser ignorados. 
     
    c. Reinicie os serviços YARN e Oozie hello como ícones de notificação Olá indicam.

3. Saudação de conjunto de variáveis de ambiente a seguir no nó mestre da saudação (substituir valores de saudação conforme apropriado):

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a>Preparar a configuração de gráfico Olá

1. Criar um arquivo de configuração com hello parâmetros de conexão de banco de dados do Azure Cosmos despertar configurações e colocá-la em `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.

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

2. Saudação de atualização `spark.driver.extraClassPath` e `spark.executor.extraClassPath` tooinclude diretório de saudação do jars Olá que você tenha distribuído na etapa anterior de saudação, nesse caso `/home/sshuser/azure-documentdb-spark/*`.

3. Fornece Olá detalhes a seguir para o banco de dados do Azure Cosmos:

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a>Carregar o gráfico de TinkerPop hello e salve-o tooAzure Cosmos DB
toodemonstrate como toopersist um gráfico em Azure Cosmos DB, este exemplo usa Olá TinkerPop predefinidos gráfico moderno TinkerPop. gráfico de saudação é armazenado no formato de Kryo e ele é fornecido no repositório de TinkerPop hello.

1. Porque você está executando Gremlin no modo YARN, você deve tornar dados de gráfico de saudação disponível no sistema de arquivos Hadoop de saudação. A seguir Olá use comandos toomake um diretório e copiar arquivo de gráfico local Olá nele. 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. Atualizar temporariamente Olá `gremlin-spark.properties` arquivo toouse `GryoInputFormat` tooread gráfico de saudação. Também indicar `inputLocation` como diretório de saudação criar, como no seguinte hello:

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. Inicie o Console de Gremlin e, em seguida, criar hello computação etapas toopersist toohello configurado o banco de dados do Azure Cosmos a coleta de dados a seguir:  

    a. Criar um gráfico de saudação `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.

    b. Use SparkGraphComputer para gravar `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.

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

4. Explorador de dados, você pode verificar que Olá dos dados persistentes tooAzure Cosmos DB.

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a>Carregar o gráfico de saudação do banco de dados do Azure Cosmos e executar consultas Gremlin

1. gráfico de saudação tooload, editar `gremlin-spark.properties` tooset `graphReader` muito`DocumentDBInputRDD`:

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. Gráfico de saudação de carga, percorrer Olá dados e executar consultas de Gremlin com ele fazendo Olá seguinte:

    a. Iniciar Olá Console Gremlin `bin/gremlin.sh`.

    b. Criar o gráfico de saudação com a configuração de saudação `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.

    c. Crie uma passagem de gráfico com SparkGraphComputer`g = graph.traversal().withComputer(SparkGraphComputer)`.

    d. Olá executar consultas de gráfico Gremlin a seguir:

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
> toosee mais detalhada registro em log, definir o nível de log de saudação `conf/log4j-console.properties` tooa nível mais detalhado.
>

## <a name="next-steps"></a>Próximas etapas

Este artigo de início rápido, você aprendeu como toowork com gráficos, combinando o banco de dados do Azure Cosmos e Spark.

> [!div class="nextstepaction"]
