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
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="10553-103">Use Caffe no Azure HDInsight Spark para aprendizado aprofundado distribuído</span><span class="sxs-lookup"><span data-stu-id="10553-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="10553-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="10553-104">Introduction</span></span>

<span data-ttu-id="10553-105">Aprendizado está afetando tudo da saúde tootransportation toomanufacturing e muito mais.</span><span class="sxs-lookup"><span data-stu-id="10553-105">Deep learning is impacting everything from healthcare tootransportation toomanufacturing, and more.</span></span> <span data-ttu-id="10553-106">As empresas estão adotando toodeep aprendizado toosolve problemas de disco rígido, como [classificação de imagem](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [o reconhecimento de fala](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), reconhecimento do objeto e tradução de máquina.</span><span class="sxs-lookup"><span data-stu-id="10553-106">Companies are turning toodeep learning toosolve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="10553-107">Há [muitas estruturas populares](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), incluindo [MiMicrosoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano etc. Caffe é uma saudação mais famosas estruturas de não simbólicos rede neural (obrigatório) e amplamente usado em muitas áreas, incluindo a visão do computador.</span><span class="sxs-lookup"><span data-stu-id="10553-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of hello most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="10553-108">Além disso, o [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combina o Caffe ao Apache Spark. Nesse caso, o aprendizado aprofundado pode ser facilmente usado em um cluster Hadoop existente, juntamente com pipelines Spark ETL, reduzindo a complexidade do sistema e a latência de aprendizado de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="10553-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="10553-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) é hello somente a oferta de Hadoop de nuvem totalmente gerenciado que fornece otimizado clusters analíticos do código-fonte aberto para Spark, Hive, MapReduce, HBase, tempestade, Kafka e R Server sustentado por um SLA de 99,9%.</span><span class="sxs-lookup"><span data-stu-id="10553-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is hello only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="10553-110">Cada uma dessas tecnologias de Big Data e aplicativos de ISV são facilmente implantáveis como clusters gerenciados, com monitoramento e segurança de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="10553-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="10553-111">Alguns usuários estão solicitando-nos sobre como toouse profundo de aprendizado no HDInsight, que é o produto de PaaS Hadoop da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="10553-111">Some users are asking us about how toouse deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="10553-112">Temos mais tooshare no hello futura, mas hoje queremos toosummarize um blog técnico sobre como toouse Caffe no HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="10553-112">We will have more tooshare in hello future, but today we want toosummarize a technical blog on how toouse Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="10553-113">Se tiver instalado o Caffe antes, você observará que a instalação dessa estrutura pode ser um pouco desafiadora.</span><span class="sxs-lookup"><span data-stu-id="10553-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="10553-114">Este blog é primeiro ilustrará como tooinstall [Caffe no Spark](https://github.com/yahoo/CaffeOnSpark) para um cluster HDInsight, em seguida, usar Olá interna MNIST demonstração toodemostrate como toouse distribuída aprendizado usando HDInsight Spark em CPUs.</span><span class="sxs-lookup"><span data-stu-id="10553-114">In this blog, we will first illustrate how tooinstall [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use hello built-in MNIST demo toodemostrate how toouse Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="10553-115">Há quatro tooget etapas principais que ele funciona em HDInsight.</span><span class="sxs-lookup"><span data-stu-id="10553-115">There are four major steps tooget it work on HDInsight.</span></span>

1. <span data-ttu-id="10553-116">Instalar dependências de saudação necessária em todos os nós de saudação</span><span class="sxs-lookup"><span data-stu-id="10553-116">Install hello required dependencies on all hello nodes</span></span>
2. <span data-ttu-id="10553-117">Criar Caffe no Spark para HDInsight no nó de cabeçalho Olá</span><span class="sxs-lookup"><span data-stu-id="10553-117">Build Caffe on Spark for HDInsight on hello head node</span></span>
3. <span data-ttu-id="10553-118">Distribuir nós de trabalho Olá necessário bibliotecas tooall Olá</span><span class="sxs-lookup"><span data-stu-id="10553-118">Distribute hello required libraries tooall hello worker nodes</span></span>
4. <span data-ttu-id="10553-119">Compor um modelo do Caffe e executá-lo de forma distribuída</span><span class="sxs-lookup"><span data-stu-id="10553-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="10553-120">Como HDInsight é uma solução de PaaS, oferece recursos de plataforma excelente – portanto, é muito fácil tooperform algumas tarefas.</span><span class="sxs-lookup"><span data-stu-id="10553-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy tooperform some tasks.</span></span> <span data-ttu-id="10553-121">Um dos recursos de saudação que usamos muito nesta postagem de blog é chamado [ação de Script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), com a qual você pode executar o shell de comandos toocustomize nós de cluster (nó principal, nó de trabalho ou nó de borda).</span><span class="sxs-lookup"><span data-stu-id="10553-121">One of hello features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands toocustomize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a><span data-ttu-id="10553-122">Etapa 1: Instalar dependências Olá necessária em todos os nós de saudação</span><span class="sxs-lookup"><span data-stu-id="10553-122">Step 1:  Install hello required dependencies on all hello nodes</span></span>

<span data-ttu-id="10553-123">tooget iniciado, precisamos de dependências de saudação tooinstall que precisamos.</span><span class="sxs-lookup"><span data-stu-id="10553-123">tooget started, we need tooinstall hello dependencies we need.</span></span> <span data-ttu-id="10553-124">site de Caffe Hello e [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) oferece alguns wiki muito útil para instalar dependências Olá para Spark no modo YARN (que é o modo de saudação do HDInsight Spark), mas precisamos tooadd alguns mais dependências para a plataforma de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="10553-124">hello Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing hello dependencies for Spark on YARN mode (which is hello mode for HDInsight Spark), but we need tooadd a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="10553-125">Nós usar a ação de script hello como abaixo e executá-lo em todos os nós de cabeçalho hello e nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="10553-125">We will use hello script action as below and run it on all hello head nodes and worker nodes.</span></span> <span data-ttu-id="10553-126">Esta ação de script levará cerca de 20 minutos, pois essas dependências também dependem de outros pacotes.</span><span class="sxs-lookup"><span data-stu-id="10553-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="10553-127">Você deve colocá-lo em um local que seja acessível tooyour cluster HDInsight, como um local de GitHub ou a conta de armazenamento BLOB saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="10553-127">You should put it in some location that is accessible tooyour HDInsight cluster, such as a GitHub location or hello default BLOB storage account.</span></span>

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


<span data-ttu-id="10553-128">Há duas etapas na ação de script hello acima.</span><span class="sxs-lookup"><span data-stu-id="10553-128">There are two steps in hello script action above.</span></span> <span data-ttu-id="10553-129">Olá primeira etapa é tooinstall todos Olá bibliotecas necessárias.</span><span class="sxs-lookup"><span data-stu-id="10553-129">hello first step is tooinstall all hello required libraries.</span></span> <span data-ttu-id="10553-130">Essas bibliotecas incluem bibliotecas de saudação necessárias para compilar Caffe (como gflags, glog) e em execução Caffe (como numpy).</span><span class="sxs-lookup"><span data-stu-id="10553-130">Those libraries include hello necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="10553-131">Estamos usando libatlas de otimização da CPU, mas você pode seguir sempre Olá CaffeOnSpark wiki sobre a instalação de outras bibliotecas de otimização, como MKL ou CUDA (para a GPU).</span><span class="sxs-lookup"><span data-stu-id="10553-131">We are using libatlas for CPU optimization, but you can always follow hello CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="10553-132">Olá segunda etapa é toodownload, compilar e instalar protobuf 2.5.0 para Caffe durante o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="10553-132">hello second step is toodownload, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="10553-133">Protobuf 2.5.0 [é necessário](https://github.com/yahoo/CaffeOnSpark/issues/87), no entanto, essa versão não está disponível como um pacote no Ubuntu 16, por isso, precisamos toocompile do código-fonte hello.</span><span class="sxs-lookup"><span data-stu-id="10553-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need toocompile it from hello source code.</span></span> <span data-ttu-id="10553-134">Também há alguns recursos Olá Internet sobre como toocompile, como [isso](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="10553-134">There are also a few resources on hello Internet on how toocompile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="10553-135">toosimply começar, é possível executar esta ação de script em relação a seu trabalho de saudação do cluster tooall nós de nós e head (para HDInsight 3.5).</span><span class="sxs-lookup"><span data-stu-id="10553-135">toosimply get started, you can just run this script action against your cluster tooall hello worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="10553-136">Você pode executar ações de script hello para um cluster em execução, ou você também pode executar ações de script hello durante o tempo de provisionamento de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="10553-136">You can either run hello script actions for a running cluster, or you can also run hello script actions during hello cluster provision time.</span></span> <span data-ttu-id="10553-137">Para obter mais detalhes sobre as ações de script hello, consulte a documentação de saudação [aqui](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="10553-137">For more details on hello script actions, please see hello documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![Ações de script tooInstall dependências](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a><span data-ttu-id="10553-139">Etapa 2: Criar Caffe no Spark para HDInsight no nó de cabeçalho Olá</span><span class="sxs-lookup"><span data-stu-id="10553-139">Step 2: Build Caffe on Spark for HDInsight on hello head node</span></span>

<span data-ttu-id="10553-140">segunda etapa de saudação é toobuild Caffe no nó principal do hello e distribua nós de trabalho Olá compilado bibliotecas tooall hello.</span><span class="sxs-lookup"><span data-stu-id="10553-140">hello second step is toobuild Caffe on hello headnode, and then distribute hello compiled libraries tooall hello worker nodes.</span></span> <span data-ttu-id="10553-141">Nesta etapa, você precisará de muito[ssh para o nó principal](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), em seguida, basta seguir Olá [CaffeOnSpark do processo de compilação](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), e abaixo está o script hello toobuild CaffeOnSpark podem ser usados com algumas etapas adicionais.</span><span class="sxs-lookup"><span data-stu-id="10553-141">In this step, you will need too[ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow hello [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is hello script you can use toobuild CaffeOnSpark with a few additional steps.</span></span> 

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

<span data-ttu-id="10553-142">Talvez seja necessário toodo mais do que diz que documentação de saudação do CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="10553-142">You may need toodo more than what hello documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="10553-143">Olá alterações são:</span><span class="sxs-lookup"><span data-stu-id="10553-143">hello changes are:</span></span>
- <span data-ttu-id="10553-144">Alterar apenas tooCPU e usar libatlas para essa finalidade específica.</span><span class="sxs-lookup"><span data-stu-id="10553-144">Change tooCPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="10553-145">Olá conjuntos de dados toohello armazenamento de BLOB, que é um local compartilhado que é acessível tooall nós de trabalho para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="10553-145">Put hello datasets toohello BLOB storage, which is a shared location that is accessible tooall worker nodes for later use.</span></span>
- <span data-ttu-id="10553-146">Olá PUT compilados Caffe armazenamento de tooBLOB de bibliotecas, e mais tarde você copiará esses nós de saudação tooall bibliotecas usando o tempo de compilação adicionais de tooavoid de ações de script.</span><span class="sxs-lookup"><span data-stu-id="10553-146">Put hello compiled Caffe libraries tooBLOB storage, and later you will copy those libraries tooall hello nodes using script actions tooavoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="10553-147">Solução de problemas: ocorreu um Ant BuildException: exec retornou: 2</span><span class="sxs-lookup"><span data-stu-id="10553-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="10553-148">Quando você tentar primeiro toobuild CaffeOnSpark, às vezes, ele indicará que a</span><span class="sxs-lookup"><span data-stu-id="10553-148">When first trying toobuild CaffeOnSpark, sometimes it will say</span></span>

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="10553-149">Repositório de código simplesmente limpa Olá por "make limpa" e, em seguida, execute "Verifique compilação" resolverá esse problema, contanto que tenha dependências corretas hello.</span><span class="sxs-lookup"><span data-stu-id="10553-149">Simply clean hello code repository by "make clean" and then run "make build" will solve this issue, as long as you have hello correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="10553-150">Solução de problemas: tempo limite de conexão do repositório do Maven</span><span class="sxs-lookup"><span data-stu-id="10553-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="10553-151">Às vezes, maven me dá erro de tempo limite de conexão hello, toobelow semelhante:</span><span class="sxs-lookup"><span data-stu-id="10553-151">Sometimes maven gives me hello connection time out error, similar toobelow:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="10553-152">Será Okey depois de aguardar alguns minutos e tente toorebuild código de hello, portanto ele pode ser Maven alguma forma limites Olá tráfego de um endereço IP específico.</span><span class="sxs-lookup"><span data-stu-id="10553-152">It will be OK after waiting for a few minutes and then just try toorebuild hello code, so it might be Maven somehow limits hello traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="10553-153">Solução de problemas: falha de teste para Caffe</span><span class="sxs-lookup"><span data-stu-id="10553-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="10553-154">Você provavelmente verá uma falha de teste ao fazer a verificação final Olá para CaffeOnSpark, semelhante com abaixo.</span><span class="sxs-lookup"><span data-stu-id="10553-154">You probably will see a test failure when doing hello final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="10553-155">Isso é prabably relacionada com codificação UTF-8, mas não deve afetar o uso de saudação do Caffe</span><span class="sxs-lookup"><span data-stu-id="10553-155">This is prabably related with UTF-8 encoding, but should not impact hello usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a><span data-ttu-id="10553-156">Etapa 3: Distribuir nós de trabalho Olá necessário bibliotecas tooall Olá</span><span class="sxs-lookup"><span data-stu-id="10553-156">Step 3: Distribute hello required libraries tooall hello worker nodes</span></span>

<span data-ttu-id="10553-157">Olá próxima etapa é toodistribute bibliotecas de hello (Olá basicamente bibliotecas no CaffeOnSpark/caffe-público/distribuir/lib/e CaffeOnSpark/caffe-distri/distribuir/lib /) tooall nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="10553-157">hello next step is toodistribute hello libraries (basically hello libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) tooall hello nodes.</span></span> <span data-ttu-id="10553-158">Na etapa 2, colocamos essas bibliotecas no armazenamento BLOB e nesta etapa, usaremos toocopy de ações de script-tooall Olá nós principal e trabalho.</span><span class="sxs-lookup"><span data-stu-id="10553-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions toocopy it tooall hello head nodes and worker nodes.</span></span>

<span data-ttu-id="10553-159">toodo, simples de executar uma ação de script como abaixo (pode ser necessário toopoint toohello local correto específico tooyour cluster):</span><span class="sxs-lookup"><span data-stu-id="10553-159">toodo this, simple run a script action as below (you need toopoint toohello right location specific tooyour cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="10553-160">Como na etapa 2, podemos colocá-la na Olá armazenamento BLOB que é acessível tooall Olá nós, nesta etapa, simplesmente copiar-tooall Olá nós.</span><span class="sxs-lookup"><span data-stu-id="10553-160">Because in step 2, we put it on hello BLOB storage which is accessible tooall hello nodes, in this step we just simply copy it tooall hello nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="10553-161">Etapa 4: compor um modelo do Caffe e executá-lo de forma distribuída</span><span class="sxs-lookup"><span data-stu-id="10553-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="10553-162">Depois de executar Olá acima etapas, Caffe é já instalado no nó principal do hello e estamos toogo BOM.</span><span class="sxs-lookup"><span data-stu-id="10553-162">After running hello above steps, Caffe is alreay installed on hello headnode and we are good toogo.</span></span> <span data-ttu-id="10553-163">Olá próxima etapa é toowrite um modelo de Caffe.</span><span class="sxs-lookup"><span data-stu-id="10553-163">hello next step is toowrite a Caffe model.</span></span> 

<span data-ttu-id="10553-164">Caffe está usando uma "arquitetura expressiva", onde para composição de um modelo, você apenas precisa toodefine um arquivo de configuração e sem codificação (na maioria dos casos).</span><span class="sxs-lookup"><span data-stu-id="10553-164">Caffe is using an "expressive architecture", where for composing a model, you just need toodefine a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="10553-165">Vamos conferir isso.</span><span class="sxs-lookup"><span data-stu-id="10553-165">So let's take a look there.</span></span> 

<span data-ttu-id="10553-166">modelo de saudação que será treinamos atualmente é um modelo de exemplo para treinamento MNIST.</span><span class="sxs-lookup"><span data-stu-id="10553-166">hello model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="10553-167">banco de dados do Hello MNIST de dígitos manuscritos tem um conjunto de treinamento de 60.000 exemplos e um conjunto de testes de 10.000 exemplos.</span><span class="sxs-lookup"><span data-stu-id="10553-167">hello MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="10553-168">É um subconjunto de um conjunto maior disponível do NIST.</span><span class="sxs-lookup"><span data-stu-id="10553-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="10553-169">dígitos de saudação foram normalizados de tamanho e centralizado em uma imagem de tamanho fixo.</span><span class="sxs-lookup"><span data-stu-id="10553-169">hello digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="10553-170">CaffeOnSpark tem o conjunto de dados alguns scripts toodownload hello e convertê-la em formato de saudação correto.</span><span class="sxs-lookup"><span data-stu-id="10553-170">CaffeOnSpark has some scripts toodownload hello dataset and convert it into hello right format.</span></span>

<span data-ttu-id="10553-171">O CaffeOnSpark fornece alguns exemplos de topologias de rede para treinamento de MNIST.</span><span class="sxs-lookup"><span data-stu-id="10553-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="10553-172">Tem um bom design de divisão de arquitetura de rede de saudação (topologia de saudação da rede Olá) e a otimização.</span><span class="sxs-lookup"><span data-stu-id="10553-172">It has a nice design of splitting hello network architecture (hello topology of hello network) and optimization.</span></span> <span data-ttu-id="10553-173">Nesse caso, há dois arquivos necessários:</span><span class="sxs-lookup"><span data-stu-id="10553-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="10553-174">arquivo de "Solver" Hello (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) é usado para supervisionar otimização hello e geração de atualizações do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="10553-174">hello "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing hello optimization and generating parameter updates.</span></span> <span data-ttu-id="10553-175">Por exemplo, ela define se CPU ou GPU será usada, o que é dinâmica hello, serão o número de iterações, etc. Ele também define qual topologia de rede neurônio deve Olá uso de programa (que é o segundo arquivo de saudação que precisamos).</span><span class="sxs-lookup"><span data-stu-id="10553-175">For example, it defines whether CPU or GPU will be used, what's hello momentum, how many iterations will be, etc. It also defines which neuron network topology should hello program use (which is hello second file we need).</span></span> <span data-ttu-id="10553-176">Para obter mais informações sobre o Solver, consulte muito[Caffe documentação](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="10553-176">For more information about Solver, please refer too[Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="10553-177">Neste exemplo, como estamos usando CPU, em vez de GPU, podemos deve alterar a última linha hello para:</span><span class="sxs-lookup"><span data-stu-id="10553-177">For this example, since we are using CPU rather than GPU, we should change hello last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Configuração do Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="10553-179">Você pode alterar outras linhas conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="10553-179">You can change other lines as needed.</span></span>

<span data-ttu-id="10553-180">segundo arquivo de saudação (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) define como rede de neurônio Olá aparência e entrada relevante hello e arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="10553-180">hello second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how hello neuron network looks like, and hello relevant input and output file.</span></span> <span data-ttu-id="10553-181">Também precisamos tooupdate Olá tooreflect Olá treinamento dados local do arquivo de.</span><span class="sxs-lookup"><span data-stu-id="10553-181">We also need tooupdate hello file tooreflect hello training data location.</span></span> <span data-ttu-id="10553-182">Alterar Olá parte em lenet_memory_train_test.prototxt (pode ser necessário toopoint toohello local correto específico tooyour cluster) a seguir:</span><span class="sxs-lookup"><span data-stu-id="10553-182">Change hello following part in lenet_memory_train_test.prototxt (you need toopoint toohello right location specific tooyour cluster):</span></span>

- <span data-ttu-id="10553-183">Alterar file:/Users/mridul/bigml/demodl/mnist_train_lmdb"hello" muito "wasb: / / / projetos/machine_learning/image_dataset/mnist_train_lmdb"</span><span class="sxs-lookup"><span data-stu-id="10553-183">change hello "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" too"wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="10553-184">alterar "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" muito "wasb: / / / projetos/machine_learning/image_dataset/mnist_test_lmdb"</span><span class="sxs-lookup"><span data-stu-id="10553-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" too"wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Configuração do Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="10553-186">Para obter mais informações sobre como toodefine Olá rede, verifique se Olá [Caffe documentação no dataset MNIST](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="10553-186">For more information on how toodefine hello network, please check hello [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="10553-187">Para finalidade Olá este blog, usamos apenas esse exemplo MNIST simples.</span><span class="sxs-lookup"><span data-stu-id="10553-187">For hello purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="10553-188">Você deve executar o comando de saudação abaixo do nó principal hello:</span><span class="sxs-lookup"><span data-stu-id="10553-188">You should run hello command below from hello head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="10553-189">Basicamente distribui Olá necessários arquivos YARN contêiner tooeach (lenet_memory_solver.prototxt e lenet_memory_train_test.prototxt) e também definir Olá caminho relevante de cada Spark driver/executor tooLD_LIBRARY_PATH, que é definido em Olá código trecho de código e pontos de toohello local anterior que tenha CaffeOnSpark bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="10553-189">Basically it distributes hello required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) tooeach YARN container, and also set hello relevant PATH of each Spark driver/executor tooLD_LIBRARY_PATH, which is defined in hello previous code snippet and points toohello location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="10553-190">Monitoramento e solução de problemas</span><span class="sxs-lookup"><span data-stu-id="10553-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="10553-191">Como estamos usando o modo de cluster YARN, caso em que o driver do Spark de Olá estará contêiner arbitrário tooan agendada (e um nó de trabalho arbitrário) só deverá ser exibida na saída de console Olá algo como:</span><span class="sxs-lookup"><span data-stu-id="10553-191">Since we are using YARN cluster mode, in which case hello Spark driver will be scheduled tooan arbitrary container (and an arbitrary worker node) you should only see in hello console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="10553-192">Se você quiser tooknow o que aconteceu, geralmente você precisa de log do driver do Spark tooget hello, que tem mais informações.</span><span class="sxs-lookup"><span data-stu-id="10553-192">If you want tooknow what happened, you usually need tooget hello Spark driver's log, which has more information.</span></span> <span data-ttu-id="10553-193">Nesse caso, você precisa toogo toohello YARN da interface do usuário toofind Olá YARN logs relevantes.</span><span class="sxs-lookup"><span data-stu-id="10553-193">In this case, you need toogo toohello YARN UI toofind hello relevant YARN logs.</span></span> <span data-ttu-id="10553-194">Você pode obter Olá YARN da interface do usuário por esta URL:</span><span class="sxs-lookup"><span data-stu-id="10553-194">You can get hello YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![Interface do usuário do YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="10553-196">Você pode conferir a quantidade de recursos alocada para este aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="10553-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="10553-197">Você pode clicar em links de "Agendador" Olá, e, em seguida, você verá que, para este aplicativo, há 9 contêineres em execução.</span><span class="sxs-lookup"><span data-stu-id="10553-197">You can click hello "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="10553-198">Pedimos YARN tooprovide 8 executores e outro contêiner é para o processo de driver.</span><span class="sxs-lookup"><span data-stu-id="10553-198">We ask YARN tooprovide 8 executors, and another container is for driver process.</span></span> 

![Agendador do YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="10553-200">Talvez você queira toocheck Olá driver logs ou logs de contêiner se houver falhas.</span><span class="sxs-lookup"><span data-stu-id="10553-200">You may want toocheck hello  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="10553-201">Para logs de driver, você pode Olá ID do aplicativo na interface do usuário do YARN, clique botão de "Logs" hello.</span><span class="sxs-lookup"><span data-stu-id="10553-201">For driver logs, you can click hello application ID in YARN UI, then click hello "Logs" button.</span></span> <span data-ttu-id="10553-202">Olá driver logs são gravados em stderr.</span><span class="sxs-lookup"><span data-stu-id="10553-202">hello driver logs are written into stderr.</span></span>

![IU DO YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="10553-204">Por exemplo, você pode ver algumas das erro Olá abaixo dos logs de driver hello, indicando que você alocar executores de muitos.</span><span class="sxs-lookup"><span data-stu-id="10553-204">For example, you might see some of hello error below from hello driver logs, indicating you allocate too many executors.</span></span>

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

<span data-ttu-id="10553-205">Às vezes, o problema de saudação pode ocorrer em executores em vez de drivers.</span><span class="sxs-lookup"><span data-stu-id="10553-205">Sometimes, hello issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="10553-206">Nesse caso, você precisa toocheck Olá contêiner logs.</span><span class="sxs-lookup"><span data-stu-id="10553-206">In this case, you need toocheck hello container logs.</span></span> <span data-ttu-id="10553-207">Você pode sempre obter logs de contêiner de saudação e, em seguida, obter saudação do contêiner com falha.</span><span class="sxs-lookup"><span data-stu-id="10553-207">You can always get hello container logs, and then get hello failed container.</span></span> <span data-ttu-id="10553-208">Por exemplo, você pode encontrar essa falha ao executar o Caffe.</span><span class="sxs-lookup"><span data-stu-id="10553-208">For example, you might meet this failure when running Caffe.</span></span>

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

<span data-ttu-id="10553-209">Nesse caso, é necessário o ID de contêiner tooget Olá falha (em Olá acima caso, é container_1485916338528_0008_05_000005).</span><span class="sxs-lookup"><span data-stu-id="10553-209">In this case, you need tooget hello failed container ID (in hello above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="10553-210">Em seguida, você precisa toorun</span><span class="sxs-lookup"><span data-stu-id="10553-210">Then you need toorun</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="10553-211">do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="10553-211">from hello headnode.</span></span> <span data-ttu-id="10553-212">Depois de verificar a falha do contêiner, ela é causada pelo uso do modo de GPU (em que você deve usar o modo de CPU em vez disso) em lenet_memory_solver.prototxt.</span><span class="sxs-lookup"><span data-stu-id="10553-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="10553-213">Obtendo resultados</span><span class="sxs-lookup"><span data-stu-id="10553-213">Getting results</span></span>

<span data-ttu-id="10553-214">Como podemos está alocando 8 executores e topologia de rede de saudação é simple, ele deve levar somente cerca de 30 minutos toorun Olá de resultados.</span><span class="sxs-lookup"><span data-stu-id="10553-214">Since we are allocating 8 executors, and hello network topology is simple, it should only take around 30 minutes toorun hello result.</span></span> <span data-ttu-id="10553-215">Na linha de comando hello, você pode ver que colocar Olá modelo toowasb:///mnist.model e coloque Olá resultados tooa pasta denominada wasb: / / / mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="10553-215">From hello command line, you can see that we put hello model toowasb:///mnist.model, and put hello results tooa folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="10553-216">Você pode obter resultados hello, executando</span><span class="sxs-lookup"><span data-stu-id="10553-216">You can get hello results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="10553-217">e o resultado de saudação se parece com:</span><span class="sxs-lookup"><span data-stu-id="10553-217">and hello result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="10553-218">Olá SampleID representa a ID de saudação no conjunto de dados MNIST hello e rótulo Olá é número Olá Olá modelo identifica.</span><span class="sxs-lookup"><span data-stu-id="10553-218">hello SampleID represents hello ID in hello MNIST dataset, and hello label is hello number that hello model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="10553-219">Conclusão</span><span class="sxs-lookup"><span data-stu-id="10553-219">Conclusion</span></span>

<span data-ttu-id="10553-220">Nesta documentação, você tentou tooinstall CaffeOnSpark com a execução de um exemplo simples.</span><span class="sxs-lookup"><span data-stu-id="10553-220">In this documentation, you have tried tooinstall CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="10553-221">HDInsight é uma plataforma de computação distribuída nuvem gerenciado completo e é Olá melhor local para executar cargas de trabalho de análise avançada e aprendizado de máquina no conjunto de dados grande e para aprendizado distribuído, você pode usar Caffe no aprendizado tooperform HDInsight Spark tarefas.</span><span class="sxs-lookup"><span data-stu-id="10553-221">HDInsight is a full managed cloud distributed compute platform, and is hello best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark tooperform deep learning tasks.</span></span>


## <span data-ttu-id="10553-222"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="10553-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="10553-223">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="10553-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="10553-224">Cenários</span><span class="sxs-lookup"><span data-stu-id="10553-224">Scenarios</span></span>
* [<span data-ttu-id="10553-225">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="10553-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="10553-226">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="10553-226">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="10553-227">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="10553-227">Manage resources</span></span>
* [<span data-ttu-id="10553-228">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="10553-228">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

