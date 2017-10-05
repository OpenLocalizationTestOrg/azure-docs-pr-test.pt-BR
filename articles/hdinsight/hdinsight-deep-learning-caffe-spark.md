---
title: "Usar Caffe no Azure HDInsight Spark para aprendizado aprofundado distribuído | Microsoft Docs"
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
ms.openlocfilehash: 14b7808c9534bce3049422d6bce1e8914b2c2fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="0ca23-103">Use Caffe no Azure HDInsight Spark para aprendizado aprofundado distribuído</span><span class="sxs-lookup"><span data-stu-id="0ca23-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="0ca23-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="0ca23-104">Introduction</span></span>

<span data-ttu-id="0ca23-105">O aprendizado aprofundado está afetando tudo, desde os serviços de saúde até os transportes e a fabricação e muito mais.</span><span class="sxs-lookup"><span data-stu-id="0ca23-105">Deep learning is impacting everything from healthcare to transportation to manufacturing, and more.</span></span> <span data-ttu-id="0ca23-106">As empresas estão recorrendo ao aprendizado aprofundado para resolver problemas de disco rígidos, como [classificação da imagem](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [reconhecimento de fala](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), reconhecimento de objeto e tradução automática.</span><span class="sxs-lookup"><span data-stu-id="0ca23-106">Companies are turning to deep learning to solve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="0ca23-107">Há [muitas estruturas populares](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), incluindo [MiMicrosoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano etc. O Caffe é uma das estruturas não simbólicas de rede neural mais famosas (obrigatória) e é amplamente usado em muitas áreas, incluindo a visão do computador.</span><span class="sxs-lookup"><span data-stu-id="0ca23-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of the most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="0ca23-108">Além disso, o [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combina o Caffe ao Apache Spark. Nesse caso, o aprendizado aprofundado pode ser facilmente usado em um cluster Hadoop existente, juntamente com pipelines Spark ETL, reduzindo a complexidade do sistema e a latência de aprendizado de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="0ca23-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="0ca23-109">O [HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) é a única oferta de Hadoop de nuvem totalmente gerenciada, que oferece clusters de análise de software livre otimizados para Spark, Hive, MapReduce, HBase, Storm, Kafka e R Server com suporte de SLA de 99,9%.</span><span class="sxs-lookup"><span data-stu-id="0ca23-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is the only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="0ca23-110">Cada uma dessas tecnologias de Big Data e aplicativos de ISV são facilmente implantáveis como clusters gerenciados, com monitoramento e segurança de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="0ca23-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="0ca23-111">Alguns usuários perguntam como usar o aprendizado aprofundado no HDInsight, que é o produto Hadoop PaaS da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0ca23-111">Some users are asking us about how to use deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="0ca23-112">Teremos mais para abordar no futuro, mas hoje queremos para resumir uma postagem de blog técnica sobre como usar o Caffe no HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="0ca23-112">We will have more to share in the future, but today we want to summarize a technical blog on how to use Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="0ca23-113">Se tiver instalado o Caffe antes, você observará que a instalação dessa estrutura pode ser um pouco desafiadora.</span><span class="sxs-lookup"><span data-stu-id="0ca23-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="0ca23-114">Nesse blog, primeiro ilustramos como instalar o [Caffe no Spark](https://github.com/yahoo/CaffeOnSpark) para um cluster HDInsight e usar a demonstração do MNIST interno para demonstrar como usar o Aprendizado Distribuído Aprofundado usando o HDInsight Spark nas CPUs.</span><span class="sxs-lookup"><span data-stu-id="0ca23-114">In this blog, we will first illustrate how to install [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use the built-in MNIST demo to demostrate how to use Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="0ca23-115">Há quatro etapas principais para fazer com que ele funcione no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ca23-115">There are four major steps to get it work on HDInsight.</span></span>

1. <span data-ttu-id="0ca23-116">Instalar as dependências necessárias em todos os nós</span><span class="sxs-lookup"><span data-stu-id="0ca23-116">Install the required dependencies on all the nodes</span></span>
2. <span data-ttu-id="0ca23-117">Compilar Caffe no Spark para HDInsight no nó principal</span><span class="sxs-lookup"><span data-stu-id="0ca23-117">Build Caffe on Spark for HDInsight on the head node</span></span>
3. <span data-ttu-id="0ca23-118">Distribuir as bibliotecas necessárias para todos os nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="0ca23-118">Distribute the required libraries to all the worker nodes</span></span>
4. <span data-ttu-id="0ca23-119">Compor um modelo do Caffe e executá-lo de forma distribuída</span><span class="sxs-lookup"><span data-stu-id="0ca23-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="0ca23-120">Como HDInsight é uma solução de PaaS, ele oferece excelentes recursos de plataforma. Portanto, é muito fácil executar algumas tarefas.</span><span class="sxs-lookup"><span data-stu-id="0ca23-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy to perform some tasks.</span></span> <span data-ttu-id="0ca23-121">Um dos recursos que usamos intensamente nesta postagem de blog é chamado [Ação de Script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux). Com ele, você pode executar comandos do shell para personalizar nós de cluster (nó principal, nó de trabalho ou nó de borda).</span><span class="sxs-lookup"><span data-stu-id="0ca23-121">One of the features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands to customize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-the-required-dependencies-on-all-the-nodes"></a><span data-ttu-id="0ca23-122">Etapa 1: instalar as dependências necessárias em todos os nós</span><span class="sxs-lookup"><span data-stu-id="0ca23-122">Step 1:  Install the required dependencies on all the nodes</span></span>

<span data-ttu-id="0ca23-123">Para começar, precisamos instalar as dependências necessárias.</span><span class="sxs-lookup"><span data-stu-id="0ca23-123">To get started, we need to install the dependencies we need.</span></span> <span data-ttu-id="0ca23-124">O site do Caffe e o [site do CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) oferecem um wiki muito útil para instalar as dependências para Spark no modo YARN (que é o modo para HDInsight Spark), mas precisamos adicionar algumas outras dependências para a plataforma HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ca23-124">The Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing the dependencies for Spark on YARN mode (which is the mode for HDInsight Spark), but we need to add a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="0ca23-125">Vamos usar a ação de script abaixo e executá-la em todos os nós principais e nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0ca23-125">We will use the script action as below and run it on all the head nodes and worker nodes.</span></span> <span data-ttu-id="0ca23-126">Esta ação de script levará cerca de 20 minutos, pois essas dependências também dependem de outros pacotes.</span><span class="sxs-lookup"><span data-stu-id="0ca23-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="0ca23-127">Você deve colocá-lo em um local acessível ao cluster HDInsight, como um local do GitHub ou a conta de armazenamento de BLOBs padrão.</span><span class="sxs-lookup"><span data-stu-id="0ca23-127">You should put it in some location that is accessible to your HDInsight cluster, such as a GitHub location or the default BLOB storage account.</span></span>

    #!/bin/bash
    #Please be aware that installing the below will add additional 20 mins to cluster creation because of the dependencies
    #installing all dependencies, including the ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all the nodes

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


<span data-ttu-id="0ca23-128">Há duas etapas na ação de script acima.</span><span class="sxs-lookup"><span data-stu-id="0ca23-128">There are two steps in the script action above.</span></span> <span data-ttu-id="0ca23-129">A primeira etapa é instalar todas as bibliotecas necessárias.</span><span class="sxs-lookup"><span data-stu-id="0ca23-129">The first step is to install all the required libraries.</span></span> <span data-ttu-id="0ca23-130">Essas bibliotecas incluem as bibliotecas necessárias para compilar o Caffe (como gflags, glog) e executá-lo (como numpy).</span><span class="sxs-lookup"><span data-stu-id="0ca23-130">Those libraries include the necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="0ca23-131">Estamos usando libatlas para otimização de CPU, mas você sempre pode seguir o wiki CaffeOnSpark sobre a instalação de outras bibliotecas de otimização, como MKL ou CUDA (para GPU).</span><span class="sxs-lookup"><span data-stu-id="0ca23-131">We are using libatlas for CPU optimization, but you can always follow the CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="0ca23-132">A segunda etapa é baixar, compilar e instalar protobuf 2.5.0 para Caffe durante a execução.</span><span class="sxs-lookup"><span data-stu-id="0ca23-132">The second step is to download, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="0ca23-133">O Protobuf 2.5.0 [é necessário](https://github.com/yahoo/CaffeOnSpark/issues/87). No entanto, essa versão não está disponível como um pacote no Ubuntu 16. Portanto, precisamos compilá-la por meio do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="0ca23-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need to compile it from the source code.</span></span> <span data-ttu-id="0ca23-134">Também há alguns recursos na Internet sobre como compilá-lo, como [este](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="0ca23-134">There are also a few resources on the Internet on how to compile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="0ca23-135">Para simplesmente começar, você pode executar esta ação de script em relação ao cluster para todos os nós de trabalho e nós principais (para HDInsight 3.5).</span><span class="sxs-lookup"><span data-stu-id="0ca23-135">To simply get started, you can just run this script action against your cluster to all the worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="0ca23-136">Você pode executar as ações de script para um cluster em execução ou também pode executar as ações de script durante o tempo de provisionamento do cluster.</span><span class="sxs-lookup"><span data-stu-id="0ca23-136">You can either run the script actions for a running cluster, or you can also run the script actions during the cluster provision time.</span></span> <span data-ttu-id="0ca23-137">Para obter mais detalhes sobre as ações de script, confira a documentação [aqui](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="0ca23-137">For more details on the script actions, please see the documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![Ações de script para instalar dependências](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-the-head-node"></a><span data-ttu-id="0ca23-139">Etapa 2: compilar o Caffe no Spark para HDInsight no nó principal</span><span class="sxs-lookup"><span data-stu-id="0ca23-139">Step 2: Build Caffe on Spark for HDInsight on the head node</span></span>

<span data-ttu-id="0ca23-140">A segunda etapa é compilar o Caffe no nó principal e distribuir as bibliotecas compiladas para todos os nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0ca23-140">The second step is to build Caffe on the headnode, and then distribute the compiled libraries to all the worker nodes.</span></span> <span data-ttu-id="0ca23-141">Nesta etapa, você precisará executar [ssh no nó principal](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e, depois, seguir o [processo de compilação do CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn). A seguir está o script que você pode usar para compilar o CaffeOnSpark com algumas etapas adicionais.</span><span class="sxs-lookup"><span data-stu-id="0ca23-141">In this step, you will need to [ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow the [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is the script you can use to build CaffeOnSpark with a few additional steps.</span></span> 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need to be updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want to update those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up the environment before building (especially when rebuiding), or there will be errors such as "failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #the build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put the already compiled CaffeOnSpark libraries to wasb storage, then read back to each node using script actions. This is because CaffeOnSpark requires all the nodes have the libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

<span data-ttu-id="0ca23-142">Talvez seja necessário fazer mais do que diz a documentação do CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="0ca23-142">You may need to do more than what the documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="0ca23-143">As alterações são:</span><span class="sxs-lookup"><span data-stu-id="0ca23-143">The changes are:</span></span>
- <span data-ttu-id="0ca23-144">Altere para CPU apenas e use libatlas para essa finalidade específica.</span><span class="sxs-lookup"><span data-stu-id="0ca23-144">Change to CPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="0ca23-145">Coloque os conjuntos de dados no armazenamento de BLOBs, que é um local compartilhado acessível a todos os nós de trabalho para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="0ca23-145">Put the datasets to the BLOB storage, which is a shared location that is accessible to all worker nodes for later use.</span></span>
- <span data-ttu-id="0ca23-146">Coloque as bibliotecas do Caffe compiladas no armazenamento de BLOBs. Posteriormente, você copiará essas bibliotecas para todos os nós usando ações de script para evitar tempo de compilação adicional.</span><span class="sxs-lookup"><span data-stu-id="0ca23-146">Put the compiled Caffe libraries to BLOB storage, and later you will copy those libraries to all the nodes using script actions to avoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="0ca23-147">Solução de problemas: ocorreu um Ant BuildException: exec retornou: 2</span><span class="sxs-lookup"><span data-stu-id="0ca23-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="0ca23-148">Ao tentar criar pela primeira vez o CaffeOnSpark, às vezes, ele indicará que</span><span class="sxs-lookup"><span data-stu-id="0ca23-148">When first trying to build CaffeOnSpark, sometimes it will say</span></span>

    failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="0ca23-149">Basta limpar o repositório de código com "make clean" e executar "make build" para resolver o problema, contanto que você tenha as dependências corretas.</span><span class="sxs-lookup"><span data-stu-id="0ca23-149">Simply clean the code repository by "make clean" and then run "make build" will solve this issue, as long as you have the correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="0ca23-150">Solução de problemas: tempo limite de conexão do repositório do Maven</span><span class="sxs-lookup"><span data-stu-id="0ca23-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="0ca23-151">Às vezes, o maven gera o erro de tempo limite de conexão, semelhante ao item abaixo:</span><span class="sxs-lookup"><span data-stu-id="0ca23-151">Sometimes maven gives me the connection time out error, similar to below:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request to {s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="0ca23-152">Tudo estará correto após aguardar alguns minutos e tentar apenas recompilar o código. Pode ser que Maven limite de alguma forma o tráfego de determinado endereço IP.</span><span class="sxs-lookup"><span data-stu-id="0ca23-152">It will be OK after waiting for a few minutes and then just try to rebuild the code, so it might be Maven somehow limits the traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="0ca23-153">Solução de problemas: falha de teste para Caffe</span><span class="sxs-lookup"><span data-stu-id="0ca23-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="0ca23-154">Você provavelmente receberá uma falha de teste ao fazer a verificação final para o CaffeOnSpark, semelhante ao item abaixo.</span><span class="sxs-lookup"><span data-stu-id="0ca23-154">You probably will see a test failure when doing the final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="0ca23-155">Isso provavelmente está relacionado à codificação UTF-8, mas não deve afetar o uso do Caffe</span><span class="sxs-lookup"><span data-stu-id="0ca23-155">This is prabably related with UTF-8 encoding, but should not impact the usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-the-required-libraries-to-all-the-worker-nodes"></a><span data-ttu-id="0ca23-156">Etapa 3: distribuir as bibliotecas necessárias para todos os nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="0ca23-156">Step 3: Distribute the required libraries to all the worker nodes</span></span>

<span data-ttu-id="0ca23-157">A próxima etapa é distribuir as bibliotecas (basicamente, as bibliotecas em CaffeOnSpark/caffe-público/distribuir/lib/e CaffeOnSpark/caffe-distri/distribute/lib/) para todos os nós.</span><span class="sxs-lookup"><span data-stu-id="0ca23-157">The next step is to distribute the libraries (basically the libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) to all the nodes.</span></span> <span data-ttu-id="0ca23-158">Na Etapa 2, colocamos essas bibliotecas no armazenamento de BLOBs. Nesta etapa, usaremos as ações de script para copiá-las para todos os nós principais e nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0ca23-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions to copy it to all the head nodes and worker nodes.</span></span>

<span data-ttu-id="0ca23-159">Para fazer isso, basta executar uma ação de script conforme mostrado a seguir (você precisa apontar para o local certo específico para o cluster):</span><span class="sxs-lookup"><span data-stu-id="0ca23-159">To do this, simple run a script action as below (you need to point to the right location specific to your cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="0ca23-160">Como na etapa 2, ele é colocado no armazenamento de BLOBS que é acessível a todos os nós; nesta etapa, simplesmente o copiamos para todos os nós.</span><span class="sxs-lookup"><span data-stu-id="0ca23-160">Because in step 2, we put it on the BLOB storage which is accessible to all the nodes, in this step we just simply copy it to all the nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="0ca23-161">Etapa 4: compor um modelo do Caffe e executá-lo de forma distribuída</span><span class="sxs-lookup"><span data-stu-id="0ca23-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="0ca23-162">Depois de executar as etapas acima, Caffe já está instalado no nó principal e estamos prontos.</span><span class="sxs-lookup"><span data-stu-id="0ca23-162">After running the above steps, Caffe is alreay installed on the headnode and we are good to go.</span></span> <span data-ttu-id="0ca23-163">A próxima etapa é escrever um modelo do Caffe.</span><span class="sxs-lookup"><span data-stu-id="0ca23-163">The next step is to write a Caffe model.</span></span> 

<span data-ttu-id="0ca23-164">O Caffe está usando uma "arquitetura expressiva," em que, para compor um modelo, basta definir um arquivo de configuração, sem codificação (na maioria dos casos).</span><span class="sxs-lookup"><span data-stu-id="0ca23-164">Caffe is using an "expressive architecture", where for composing a model, you just need to define a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="0ca23-165">Vamos conferir isso.</span><span class="sxs-lookup"><span data-stu-id="0ca23-165">So let's take a look there.</span></span> 

<span data-ttu-id="0ca23-166">O modelo que treinaremos hoje é um modelo de exemplo para treinamento de MNIST.</span><span class="sxs-lookup"><span data-stu-id="0ca23-166">The model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="0ca23-167">O banco de dados MNIST de dígitos manuscritos tem um conjunto de treinamento de 60.000 exemplos e um conjunto de teste de 10.000 exemplos.</span><span class="sxs-lookup"><span data-stu-id="0ca23-167">The MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="0ca23-168">É um subconjunto de um conjunto maior disponível do NIST.</span><span class="sxs-lookup"><span data-stu-id="0ca23-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="0ca23-169">Os dígitos foram normalizados em termos de tamanho e centralizados em uma imagem de tamanho fixo.</span><span class="sxs-lookup"><span data-stu-id="0ca23-169">The digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="0ca23-170">O CaffeOnSpark tem alguns scripts para baixar o conjunto de dados e convertê-lo em um formato correto.</span><span class="sxs-lookup"><span data-stu-id="0ca23-170">CaffeOnSpark has some scripts to download the dataset and convert it into the right format.</span></span>

<span data-ttu-id="0ca23-171">O CaffeOnSpark fornece alguns exemplos de topologias de rede para treinamento de MNIST.</span><span class="sxs-lookup"><span data-stu-id="0ca23-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="0ca23-172">Ele tem um bom design que divide a arquitetura de rede (a topologia da rede) e a otimização.</span><span class="sxs-lookup"><span data-stu-id="0ca23-172">It has a nice design of splitting the network architecture (the topology of the network) and optimization.</span></span> <span data-ttu-id="0ca23-173">Nesse caso, há dois arquivos necessários:</span><span class="sxs-lookup"><span data-stu-id="0ca23-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="0ca23-174">o arquivo "Solver" (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) é usado para supervisionar a otimização e gerar atualizações de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="0ca23-174">the "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing the optimization and generating parameter updates.</span></span> <span data-ttu-id="0ca23-175">Por exemplo, ele define se a CPU ou GPU será usada, qual é a dinâmica, quantas iterações haverá etc. Ela também define qual topologia de rede de neurônios o programa deve usar (que é o segundo arquivo de que precisamos).</span><span class="sxs-lookup"><span data-stu-id="0ca23-175">For example, it defines whether CPU or GPU will be used, what's the momentum, how many iterations will be, etc. It also defines which neuron network topology should the program use (which is the second file we need).</span></span> <span data-ttu-id="0ca23-176">Para obter mais informações sobre o recurso Solver, confira a [documentação do Caffe](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="0ca23-176">For more information about Solver, please refer to [Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="0ca23-177">Para este exemplo, como estamos usando a CPU em vez de GPU, devemos alterar a última linha:</span><span class="sxs-lookup"><span data-stu-id="0ca23-177">For this example, since we are using CPU rather than GPU, we should change the last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Configuração do Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="0ca23-179">Você pode alterar outras linhas conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="0ca23-179">You can change other lines as needed.</span></span>

<span data-ttu-id="0ca23-180">O segundo arquivo (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) define a aparência da rede de neurônios e o arquivo de entrada e saída relevante.</span><span class="sxs-lookup"><span data-stu-id="0ca23-180">The second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how the neuron network looks like, and the relevant input and output file.</span></span> <span data-ttu-id="0ca23-181">Também precisamos atualizar o arquivo para refletir o local de dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="0ca23-181">We also need to update the file to reflect the training data location.</span></span> <span data-ttu-id="0ca23-182">Altere a seguinte parte em lenet_memory_train_test.prototxt (você precisa apontar para o local certo específico para seu cluster):</span><span class="sxs-lookup"><span data-stu-id="0ca23-182">Change the following part in lenet_memory_train_test.prototxt (you need to point to the right location specific to your cluster):</span></span>

- <span data-ttu-id="0ca23-183">altere "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" para "wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span><span class="sxs-lookup"><span data-stu-id="0ca23-183">change the "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" to "wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="0ca23-184">altere "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" para "wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span><span class="sxs-lookup"><span data-stu-id="0ca23-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" to "wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Configuração do Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="0ca23-186">Para obter mais informações sobre como definir a rede, confira a [documentação do Caffe no conjunto de dados MNIST](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="0ca23-186">For more information on how to define the network, please check the [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="0ca23-187">Para os objetivos deste blog, usamos apenas este exemplo MNIST simples.</span><span class="sxs-lookup"><span data-stu-id="0ca23-187">For the purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="0ca23-188">Você deve executar o comando abaixo no nó principal:</span><span class="sxs-lookup"><span data-stu-id="0ca23-188">You should run the command below from the head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="0ca23-189">Basicamente, distribui os arquivos necessários (lenet_memory_solver.prototxt e lenet_memory_train_test.prototxt) para cada contêiner YARN e também define o caminho relevante de cada driver/executor Spark para LD_LIBRARY_PATH, que é definido no trecho de código anterior e aponta para o local que tem bibliotecas CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="0ca23-189">Basically it distributes the required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) to each YARN container, and also set the relevant PATH of each Spark driver/executor to LD_LIBRARY_PATH, which is defined in the previous code snippet and points to the location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="0ca23-190">Monitoramento e solução de problemas</span><span class="sxs-lookup"><span data-stu-id="0ca23-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="0ca23-191">Como estamos usando o modo de cluster YARN, em que o driver Spark será agendado para um contêiner arbitrário (e um nó de trabalho arbitrário), você só verá no console uma saída semelhante a:</span><span class="sxs-lookup"><span data-stu-id="0ca23-191">Since we are using YARN cluster mode, in which case the Spark driver will be scheduled to an arbitrary container (and an arbitrary worker node) you should only see in the console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="0ca23-192">Se quiser saber o que aconteceu, geralmente você precisará obter o log do driver do Spark, que tem mais informações.</span><span class="sxs-lookup"><span data-stu-id="0ca23-192">If you want to know what happened, you usually need to get the Spark driver's log, which has more information.</span></span> <span data-ttu-id="0ca23-193">Nesse caso, você precisa acessar a interface do usuário YARN para encontrar os logs YARN relevantes.</span><span class="sxs-lookup"><span data-stu-id="0ca23-193">In this case, you need to go to the YARN UI to find the relevant YARN logs.</span></span> <span data-ttu-id="0ca23-194">Você pode obter a interface do usuário do YARN por meio desta URL:</span><span class="sxs-lookup"><span data-stu-id="0ca23-194">You can get the YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![Interface do usuário do YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="0ca23-196">Você pode conferir a quantidade de recursos alocada para este aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="0ca23-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="0ca23-197">Você pode clicar no link "Agendador" e verá que, para esse aplicativo, existem nove contêineres em execução.</span><span class="sxs-lookup"><span data-stu-id="0ca23-197">You can click the "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="0ca23-198">Solicitamos que YARN forneça oito executores, e outro contêiner é para o processo de driver.</span><span class="sxs-lookup"><span data-stu-id="0ca23-198">We ask YARN to provide 8 executors, and another container is for driver process.</span></span> 

![Agendador do YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="0ca23-200">Convém verificar os logs de driver ou logs de contêiner, se houver falhas.</span><span class="sxs-lookup"><span data-stu-id="0ca23-200">You may want to check the  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="0ca23-201">Para logs de driver, você pode clicar na ID do aplicativo na interface do usuário do YARN e clicar no botão "Logs".</span><span class="sxs-lookup"><span data-stu-id="0ca23-201">For driver logs, you can click the application ID in YARN UI, then click the "Logs" button.</span></span> <span data-ttu-id="0ca23-202">Os logs de driver são gravados em stderr.</span><span class="sxs-lookup"><span data-stu-id="0ca23-202">The driver logs are written into stderr.</span></span>

![IU DO YARN 2](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="0ca23-204">Por exemplo, você pode ver alguns do erro abaixo dos logs do driver, indicando que você aloca um número excessivo de executores.</span><span class="sxs-lookup"><span data-stu-id="0ca23-204">For example, you might see some of the error below from the driver logs, indicating you allocate too many executors.</span></span>

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

<span data-ttu-id="0ca23-205">Às vezes, o problema pode ocorrer em executores em vez de drivers.</span><span class="sxs-lookup"><span data-stu-id="0ca23-205">Sometimes, the issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="0ca23-206">Nesse caso, você precisa verificar os logs de contêiner.</span><span class="sxs-lookup"><span data-stu-id="0ca23-206">In this case, you need to check the container logs.</span></span> <span data-ttu-id="0ca23-207">Você sempre pode obter os logs do contêiner e depois obter o contêiner com falha.</span><span class="sxs-lookup"><span data-stu-id="0ca23-207">You can always get the container logs, and then get the failed container.</span></span> <span data-ttu-id="0ca23-208">Por exemplo, você pode encontrar essa falha ao executar o Caffe.</span><span class="sxs-lookup"><span data-stu-id="0ca23-208">For example, you might meet this failure when running Caffe.</span></span>

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

<span data-ttu-id="0ca23-209">Nesse caso, você precisa obter a ID de contêiner com falha (no caso acima, é container_1485916338528_0008_05_000005).</span><span class="sxs-lookup"><span data-stu-id="0ca23-209">In this case, you need to get the failed container ID (in the above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="0ca23-210">Em seguida, você precisa executar</span><span class="sxs-lookup"><span data-stu-id="0ca23-210">Then you need to run</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="0ca23-211">no nó principal.</span><span class="sxs-lookup"><span data-stu-id="0ca23-211">from the headnode.</span></span> <span data-ttu-id="0ca23-212">Depois de verificar a falha do contêiner, ela é causada pelo uso do modo de GPU (em que você deve usar o modo de CPU em vez disso) em lenet_memory_solver.prototxt.</span><span class="sxs-lookup"><span data-stu-id="0ca23-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written to STDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="0ca23-213">Obtendo resultados</span><span class="sxs-lookup"><span data-stu-id="0ca23-213">Getting results</span></span>

<span data-ttu-id="0ca23-214">Como estamos alocando oito executores, e a topologia de rede é simples, só levará cerca de 30 minutos para executar o resultado.</span><span class="sxs-lookup"><span data-stu-id="0ca23-214">Since we are allocating 8 executors, and the network topology is simple, it should only take around 30 minutes to run the result.</span></span> <span data-ttu-id="0ca23-215">Na linha de comando, você pode ver que colocamos o modelo wasb:///mnist.model e colocamos os resultados em uma pasta chamada wasb:///mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="0ca23-215">From the command line, you can see that we put the model to wasb:///mnist.model, and put the results to a folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="0ca23-216">Você pode obter os resultados executando</span><span class="sxs-lookup"><span data-stu-id="0ca23-216">You can get the results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="0ca23-217">e o resultado é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="0ca23-217">and the result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="0ca23-218">O SampleID representa a ID do conjunto de dados MNIST e o rótulo é o número que identifica o modelo.</span><span class="sxs-lookup"><span data-stu-id="0ca23-218">The SampleID represents the ID in the MNIST dataset, and the label is the number that the model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="0ca23-219">Conclusão</span><span class="sxs-lookup"><span data-stu-id="0ca23-219">Conclusion</span></span>

<span data-ttu-id="0ca23-220">Nesta documentação, você tentou instalar o CaffeOnSpark com a execução de um exemplo simples.</span><span class="sxs-lookup"><span data-stu-id="0ca23-220">In this documentation, you have tried to install CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="0ca23-221">O HDInsight é uma plataforma de computação distribuída de nuvem gerenciada completa e é o melhor lugar para executar cargas de trabalho de análise avançada e aprendizado de máquina em um conjunto de dados grande. Para o aprendizado distribuído, você pode usar o Caffe no HDInsight Spark para executar tarefas de aprendizado aprofundado.</span><span class="sxs-lookup"><span data-stu-id="0ca23-221">HDInsight is a full managed cloud distributed compute platform, and is the best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark to perform deep learning tasks.</span></span>


## <span data-ttu-id="0ca23-222"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="0ca23-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="0ca23-223">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ca23-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="0ca23-224">Cenários</span><span class="sxs-lookup"><span data-stu-id="0ca23-224">Scenarios</span></span>
* <span data-ttu-id="0ca23-225">
            [Spark com Machine Learning: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="0ca23-225">[Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data](hdinsight-apache-spark-ipython-notebook-machine-learning.md)</span></span>
* <span data-ttu-id="0ca23-226">
            [Spark com Machine Learning: usar o Spark no HDInsight para prever resultados da inspeção de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)</span><span class="sxs-lookup"><span data-stu-id="0ca23-226">[Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results](hdinsight-apache-spark-machine-learning-mllib-ipython.md)</span></span>

### <a name="manage-resources"></a><span data-ttu-id="0ca23-227">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="0ca23-227">Manage resources</span></span>
* [<span data-ttu-id="0ca23-228">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ca23-228">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

