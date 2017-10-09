---
title: "aaaUse Caffe no Azure HDInsight Spark para aprendizado distribuído | Microsoft Docs"
description: "Use Caffe no Azure HDInsight Spark para aprendizado aprofundado distribuído"
services: hdinsight
documentationcenter: 
author: xiaoyongzhu
manager: asadk
editor: cgronlun
tags: azure-portal
ms.assetid: 71dcd1ad-4cad-47ad-8a9d-dcb7fa3c2ff9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: xiaoyzhu
ms.openlocfilehash: d6476a7ed3a0df38538e845d7d5404067b01113c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a>Use Caffe no Azure HDInsight Spark para aprendizado aprofundado distribuído


## <a name="introduction"></a>Introdução

Aprendizado está afetando tudo da saúde tootransportation toomanufacturing e muito mais. As empresas estão adotando toodeep aprendizado toosolve problemas de disco rígido, como [classificação de imagem](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [o reconhecimento de fala](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), reconhecimento do objeto e tradução de máquina. 

Há [muitas estruturas populares](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), incluindo [MiMicrosoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano etc. Caffe é uma saudação mais famosas estruturas de não simbólicos rede neural (obrigatório) e amplamente usado em muitas áreas, incluindo a visão do computador. Além disso, o [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combina o Caffe ao Apache Spark. Nesse caso, o aprendizado aprofundado pode ser facilmente usado em um cluster Hadoop existente, juntamente com pipelines Spark ETL, reduzindo a complexidade do sistema e a latência de aprendizado de ponta a ponta.

[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) é hello somente a oferta de Hadoop de nuvem totalmente gerenciado que fornece otimizado clusters analíticos do código-fonte aberto para Spark, Hive, MapReduce, HBase, tempestade, Kafka e R Server sustentado por um SLA de 99,9%. Cada uma dessas tecnologias de Big Data e aplicativos de ISV são facilmente implantáveis como clusters gerenciados, com monitoramento e segurança de nível empresarial.

Alguns usuários estão solicitando-nos sobre como toouse profundo de aprendizado no HDInsight, que é o produto de PaaS Hadoop da Microsoft. Temos mais tooshare no hello futura, mas hoje queremos toosummarize um blog técnico sobre como toouse Caffe no HDInsight Spark.

Se tiver instalado o Caffe antes, você observará que a instalação dessa estrutura pode ser um pouco desafiadora. Este blog é primeiro ilustrará como tooinstall [Caffe no Spark](https://github.com/yahoo/CaffeOnSpark) para um cluster HDInsight, em seguida, usar Olá interna MNIST demonstração toodemostrate como toouse distribuída aprendizado usando HDInsight Spark em CPUs.

Há quatro tooget etapas principais que ele funciona em HDInsight.

1. Instalar dependências de saudação necessária em todos os nós de saudação
2. Criar Caffe no Spark para HDInsight no nó de cabeçalho Olá
3. Distribuir nós de trabalho Olá necessário bibliotecas tooall Olá
4. Compor um modelo do Caffe e executá-lo de forma distribuída

Como HDInsight é uma solução de PaaS, oferece recursos de plataforma excelente – portanto, é muito fácil tooperform algumas tarefas. Um dos recursos de saudação que usamos muito nesta postagem de blog é chamado [ação de Script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), com a qual você pode executar o shell de comandos toocustomize nós de cluster (nó principal, nó de trabalho ou nó de borda).

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a>Etapa 1: Instalar dependências Olá necessária em todos os nós de saudação

tooget iniciado, precisamos de dependências de saudação tooinstall que precisamos. site de Caffe Hello e [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) oferece alguns wiki muito útil para instalar dependências Olá para Spark no modo YARN (que é o modo de saudação do HDInsight Spark), mas precisamos tooadd alguns mais dependências para a plataforma de HDInsight. Nós usar a ação de script hello como abaixo e executá-lo em todos os nós de cabeçalho hello e nós de trabalho. Esta ação de script levará cerca de 20 minutos, pois essas dependências também dependem de outros pacotes. Você deve colocá-lo em um local que seja acessível tooyour cluster HDInsight, como um local de GitHub ou a conta de armazenamento BLOB saudação padrão.

    #!/bin/bash
    #Please be aware that installing hello below will add additional 20 mins toocluster creation because of hello dependencies
    #installing all dependencies, including hello ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all hello nodes

    sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler maven libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev build-essential  libboost-all-dev python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

    #install protobuf
    wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
    sudo tar xzvf protobuf-2.5.0.tar.gz -C /tmp/
    cd /tmp/protobuf-2.5.0/
    sudo ./configure
    sudo make
    sudo make check
    sudo make install
    sudo ldconfig
    echo "protobuf installation done"


Há duas etapas na ação de script hello acima. Olá primeira etapa é tooinstall todos Olá bibliotecas necessárias. Essas bibliotecas incluem bibliotecas de saudação necessárias para compilar Caffe (como gflags, glog) e em execução Caffe (como numpy). Estamos usando libatlas de otimização da CPU, mas você pode seguir sempre Olá CaffeOnSpark wiki sobre a instalação de outras bibliotecas de otimização, como MKL ou CUDA (para a GPU).

Olá segunda etapa é toodownload, compilar e instalar protobuf 2.5.0 para Caffe durante o tempo de execução. Protobuf 2.5.0 [é necessário](https://github.com/yahoo/CaffeOnSpark/issues/87), no entanto, essa versão não está disponível como um pacote no Ubuntu 16, por isso, precisamos toocompile do código-fonte hello. Também há alguns recursos Olá Internet sobre como toocompile, como [isso](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)

toosimply começar, é possível executar esta ação de script em relação a seu trabalho de saudação do cluster tooall nós de nós e head (para HDInsight 3.5). Você pode executar ações de script hello para um cluster em execução, ou você também pode executar ações de script hello durante o tempo de provisionamento de cluster hello. Para obter mais detalhes sobre as ações de script hello, consulte a documentação de saudação [aqui](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)

![Ações de script tooInstall dependências](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a>Etapa 2: Criar Caffe no Spark para HDInsight no nó de cabeçalho Olá

segunda etapa de saudação é toobuild Caffe no nó principal do hello e distribua nós de trabalho Olá compilado bibliotecas tooall hello. Nesta etapa, você precisará de muito[ssh para o nó principal](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), em seguida, basta seguir Olá [CaffeOnSpark do processo de compilação](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), e abaixo está o script hello toobuild CaffeOnSpark podem ser usados com algumas etapas adicionais. 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need toobe updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want tooupdate those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up hello environment before building (especially when rebuiding), or there will be errors such as "failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #hello build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put hello already compiled CaffeOnSpark libraries toowasb storage, then read back tooeach node using script actions. This is because CaffeOnSpark requires all hello nodes have hello libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

Talvez seja necessário toodo mais do que diz que documentação de saudação do CaffeOnSpark. Olá alterações são:
- Alterar apenas tooCPU e usar libatlas para essa finalidade específica.
- Olá conjuntos de dados toohello armazenamento de BLOB, que é um local compartilhado que é acessível tooall nós de trabalho para uso posterior.
- Olá PUT compilados Caffe armazenamento de tooBLOB de bibliotecas, e mais tarde você copiará esses nós de saudação tooall bibliotecas usando o tempo de compilação adicionais de tooavoid de ações de script.


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a>Solução de problemas: ocorreu um Ant BuildException: exec retornou: 2

Quando você tentar primeiro toobuild CaffeOnSpark, às vezes, ele indicará que a

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

Repositório de código simplesmente limpa Olá por "make limpa" e, em seguida, execute "Verifique compilação" resolverá esse problema, contanto que tenha dependências corretas hello.

### <a name="troubleshooting-maven-repository-connection-time-out"></a>Solução de problemas: tempo limite de conexão do repositório do Maven

Às vezes, maven me dá erro de tempo limite de conexão hello, toobelow semelhante:

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

Será Okey depois de aguardar alguns minutos e tente toorebuild código de hello, portanto ele pode ser Maven alguma forma limites Olá tráfego de um endereço IP específico.


### <a name="troubleshooting-test-failure-for-caffe"></a>Solução de problemas: falha de teste para Caffe

Você provavelmente verá uma falha de teste ao fazer a verificação final Olá para CaffeOnSpark, semelhante com abaixo. Isso é prabably relacionada com codificação UTF-8, mas não deve afetar o uso de saudação do Caffe

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a>Etapa 3: Distribuir nós de trabalho Olá necessário bibliotecas tooall Olá

Olá próxima etapa é toodistribute bibliotecas de hello (Olá basicamente bibliotecas no CaffeOnSpark/caffe-público/distribuir/lib/e CaffeOnSpark/caffe-distri/distribuir/lib /) tooall nós de saudação. Na etapa 2, colocamos essas bibliotecas no armazenamento BLOB e nesta etapa, usaremos toocopy de ações de script-tooall Olá nós principal e trabalho.

toodo, simples de executar uma ação de script como abaixo (pode ser necessário toopoint toohello local correto específico tooyour cluster):

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

Como na etapa 2, podemos colocá-la na Olá armazenamento BLOB que é acessível tooall Olá nós, nesta etapa, simplesmente copiar-tooall Olá nós.

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a>Etapa 4: compor um modelo do Caffe e executá-lo de forma distribuída

Depois de executar Olá acima etapas, Caffe é já instalado no nó principal do hello e estamos toogo BOM. Olá próxima etapa é toowrite um modelo de Caffe. 

Caffe está usando uma "arquitetura expressiva", onde para composição de um modelo, você apenas precisa toodefine um arquivo de configuração e sem codificação (na maioria dos casos). Vamos conferir isso. 

modelo de saudação que será treinamos atualmente é um modelo de exemplo para treinamento MNIST. banco de dados do Hello MNIST de dígitos manuscritos tem um conjunto de treinamento de 60.000 exemplos e um conjunto de testes de 10.000 exemplos. É um subconjunto de um conjunto maior disponível do NIST. dígitos de saudação foram normalizados de tamanho e centralizado em uma imagem de tamanho fixo. CaffeOnSpark tem o conjunto de dados alguns scripts toodownload hello e convertê-la em formato de saudação correto.

O CaffeOnSpark fornece alguns exemplos de topologias de rede para treinamento de MNIST. Tem um bom design de divisão de arquitetura de rede de saudação (topologia de saudação da rede Olá) e a otimização. Nesse caso, há dois arquivos necessários: 

arquivo de "Solver" Hello (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) é usado para supervisionar otimização hello e geração de atualizações do parâmetro. Por exemplo, ela define se CPU ou GPU será usada, o que é dinâmica hello, serão o número de iterações, etc. Ele também define qual topologia de rede neurônio deve Olá uso de programa (que é o segundo arquivo de saudação que precisamos). Para obter mais informações sobre o Solver, consulte muito[Caffe documentação](http://caffe.berkeleyvision.org/tutorial/solver.html).

Neste exemplo, como estamos usando CPU, em vez de GPU, podemos deve alterar a última linha hello para:

    # solver mode: CPU or GPU
    solver_mode: CPU

![Configuração do Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

Você pode alterar outras linhas conforme necessário.

segundo arquivo de saudação (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) define como rede de neurônio Olá aparência e entrada relevante hello e arquivo de saída. Também precisamos tooupdate Olá tooreflect Olá treinamento dados local do arquivo de. Alterar Olá parte em lenet_memory_train_test.prototxt (pode ser necessário toopoint toohello local correto específico tooyour cluster) a seguir:

- Alterar file:/Users/mridul/bigml/demodl/mnist_train_lmdb"hello" muito "wasb: / / / projetos/machine_learning/image_dataset/mnist_train_lmdb"
- alterar "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" muito "wasb: / / / projetos/machine_learning/image_dataset/mnist_test_lmdb"

![Configuração do Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

Para obter mais informações sobre como toodefine Olá rede, verifique se Olá [Caffe documentação no dataset MNIST](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)

Para finalidade Olá este blog, usamos apenas esse exemplo MNIST simples. Você deve executar o comando de saudação abaixo do nó principal hello:

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

Basicamente distribui Olá necessários arquivos YARN contêiner tooeach (lenet_memory_solver.prototxt e lenet_memory_train_test.prototxt) e também definir Olá caminho relevante de cada Spark driver/executor tooLD_LIBRARY_PATH, que é definido em Olá código trecho de código e pontos de toohello local anterior que tenha CaffeOnSpark bibliotecas. 

## <a name="monitoring-and-troubleshooting"></a>Monitoramento e solução de problemas

Como estamos usando o modo de cluster YARN, caso em que o driver do Spark de Olá estará contêiner arbitrário tooan agendada (e um nó de trabalho arbitrário) só deverá ser exibida na saída de console Olá algo como:

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

Se você quiser tooknow o que aconteceu, geralmente você precisa de log do driver do Spark tooget hello, que tem mais informações. Nesse caso, você precisa toogo toohello YARN da interface do usuário toofind Olá YARN logs relevantes. Você pode obter Olá YARN da interface do usuário por esta URL: 

    https://yourclustername.azurehdinsight.net/yarnui
   
![Interface do usuário do YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

Você pode conferir a quantidade de recursos alocada para este aplicativo específico. Você pode clicar em links de "Agendador" Olá, e, em seguida, você verá que, para este aplicativo, há 9 contêineres em execução. Pedimos YARN tooprovide 8 executores e outro contêiner é para o processo de driver. 

![Agendador do YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

Talvez você queira toocheck Olá driver logs ou logs de contêiner se houver falhas. Para logs de driver, você pode Olá ID do aplicativo na interface do usuário do YARN, clique botão de "Logs" hello. Olá driver logs são gravados em stderr.

![IU DO YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

Por exemplo, você pode ver algumas das erro Olá abaixo dos logs de driver hello, indicando que você alocar executores de muitos.

    17/02/01 07:26:06 ERROR ApplicationMaster: User class threw exception: java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
    java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
        at com.yahoo.ml.caffe.CaffeOnSpark.trainWithValidation(CaffeOnSpark.scala:261)
        at com.yahoo.ml.caffe.CaffeOnSpark$.main(CaffeOnSpark.scala:42)
        at com.yahoo.ml.caffe.CaffeOnSpark.main(CaffeOnSpark.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.spark.deploy.yarn.ApplicationMaster$$anon$2.run(ApplicationMaster.scala:627)

Às vezes, o problema de saudação pode ocorrer em executores em vez de drivers. Nesse caso, você precisa toocheck Olá contêiner logs. Você pode sempre obter logs de contêiner de saudação e, em seguida, obter saudação do contêiner com falha. Por exemplo, você pode encontrar essa falha ao executar o Caffe.

    17/02/01 07:12:05 WARN YarnAllocator: Container marked as failed: container_1485916338528_0008_05_000005 on host: 10.0.0.14. Exit status: 134. Diagnostics: Exception from container-launch.
    Container id: container_1485916338528_0008_05_000005
    Exit code: 134
    Exception message: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

    Stack trace: ExitCodeException exitCode=134: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

        at org.apache.hadoop.util.Shell.runCommand(Shell.java:933)
        at org.apache.hadoop.util.Shell.run(Shell.java:844)
        at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:1123)
        at org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor.launchContainer(DefaultContainerExecutor.java:225)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:317)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:83)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
        at java.lang.Thread.run(Thread.java:745)


    Container exited with a non-zero exit code 134

Nesse caso, é necessário o ID de contêiner tooget Olá falha (em Olá acima caso, é container_1485916338528_0008_05_000005). Em seguida, você precisa toorun 

    yarn logs -containerId container_1485916338528_0008_03_000005

do nó principal hello. Depois de verificar a falha do contêiner, ela é causada pelo uso do modo de GPU (em que você deve usar o modo de CPU em vez disso) em lenet_memory_solver.prototxt.

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a>Obtendo resultados

Como podemos está alocando 8 executores e topologia de rede de saudação é simple, ele deve levar somente cerca de 30 minutos toorun Olá de resultados. Na linha de comando hello, você pode ver que colocar Olá modelo toowasb:///mnist.model e coloque Olá resultados tooa pasta denominada wasb: / / / mnist_features_result.

Você pode obter resultados hello, executando

    hadoop fs -cat hdfs:///mnist_features_result/*

e o resultado de saudação se parece com:

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

Olá SampleID representa a ID de saudação no conjunto de dados MNIST hello e rótulo Olá é número Olá Olá modelo identifica.


## <a name="conclusion"></a>Conclusão

Nesta documentação, você tentou tooinstall CaffeOnSpark com a execução de um exemplo simples. HDInsight é uma plataforma de computação distribuída nuvem gerenciado completo e é Olá melhor local para executar cargas de trabalho de análise avançada e aprendizado de máquina no conjunto de dados grande e para aprendizado distribuído, você pode usar Caffe no aprendizado tooperform HDInsight Spark tarefas.


## <a name="seealso"></a>Consulte também
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Cenários
* [Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a>Gerenciar recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)

