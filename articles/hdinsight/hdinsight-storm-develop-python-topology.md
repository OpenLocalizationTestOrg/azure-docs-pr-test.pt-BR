---
title: "Apache Storm com componentes Python – Azure HDInsight | Microsoft Docs"
description: Saiba como criar uma topologia Apache Storm que usa componentes de Python.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: apache storm python
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 305c4060ad81458b254e66a4bad6dfd7bf69b28d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="93099-104">Desenvolver topologias do Apache Storm usando o Python no HDInsight</span><span class="sxs-lookup"><span data-stu-id="93099-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="93099-105">Saiba como criar uma topologia Apache Storm que usa componentes de Python.</span><span class="sxs-lookup"><span data-stu-id="93099-105">Learn how to create an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="93099-106">O Apache Storm dá suporte a várias linguagens, permitindo até a combinação de componentes de várias linguagens em uma topologia.</span><span class="sxs-lookup"><span data-stu-id="93099-106">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span></span> <span data-ttu-id="93099-107">A estrutura de fluxo (introduzida com o Storm 0.10.0) permite que você crie facilmente soluções que usam componentes do Python.</span><span class="sxs-lookup"><span data-stu-id="93099-107">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93099-108">As informações neste documento foram testadas usando o Storm no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="93099-108">The information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="93099-109">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="93099-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="93099-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="93099-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="93099-111">O código para esse projeto está disponível em [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="93099-111">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93099-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="93099-112">Prerequisites</span></span>

* <span data-ttu-id="93099-113">Python 2.7 ou posterior</span><span class="sxs-lookup"><span data-stu-id="93099-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="93099-114">Java JDK 1.8 ou superior</span><span class="sxs-lookup"><span data-stu-id="93099-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="93099-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="93099-115">Maven 3</span></span>

* <span data-ttu-id="93099-116">(Opcional) Um ambiente de desenvolvimento local do Storm.</span><span class="sxs-lookup"><span data-stu-id="93099-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="93099-117">Um ambiente local do Storm só será necessário se você quiser executar a topologia localmente.</span><span class="sxs-lookup"><span data-stu-id="93099-117">A local Storm environment is only needed if you want to run the topology locally.</span></span> <span data-ttu-id="93099-118">Para obter mais informações, consulte [Configurar um ambiente de desenvolvimento](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="93099-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="93099-119">Suporte a várias linguagens no Storm</span><span class="sxs-lookup"><span data-stu-id="93099-119">Storm multi-language support</span></span>

<span data-ttu-id="93099-120">O Apache Storm foi projetado para trabalhar com componentes escritos usando qualquer linguagem de programação.</span><span class="sxs-lookup"><span data-stu-id="93099-120">Apache Storm was designed to work with components written using any programming language.</span></span> <span data-ttu-id="93099-121">Os componentes devem entender como trabalhar com a [definição do Thrift para Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="93099-121">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="93099-122">Para o Python, é fornecido um módulo como parte do projeto do Apache Storm que permite interagir facilmente com o Storm.</span><span class="sxs-lookup"><span data-stu-id="93099-122">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span></span> <span data-ttu-id="93099-123">Você pode encontrar esse módulo em [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="93099-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="93099-124">O Storm é um processo Java que é executado na máquina virtual Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="93099-124">Storm is a Java process that runs on the Java Virtual Machine (JVM).</span></span> <span data-ttu-id="93099-125">Componentes escritos em outras linguagens são executados como subprocessos.</span><span class="sxs-lookup"><span data-stu-id="93099-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="93099-126">O Storm comunica-se com esses subprocessos usando mensagens JSON enviadas por stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="93099-126">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="93099-127">Mais detalhes sobre a comunicação entre os componentes podem ser encontrados na documentação sobre [Protocolo de várias linguagens](https://storm.apache.org/documentation/Multilang-protocol.html) .</span><span class="sxs-lookup"><span data-stu-id="93099-127">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-the-flux-framework"></a><span data-ttu-id="93099-128">Python com a estrutura do Flux</span><span class="sxs-lookup"><span data-stu-id="93099-128">Python with the Flux framework</span></span>

<span data-ttu-id="93099-129">A estrutura do Flux permite que você defina topologias Storm separadamente dos componentes.</span><span class="sxs-lookup"><span data-stu-id="93099-129">The Flux framework allows you to define Storm topologies separately from the components.</span></span> <span data-ttu-id="93099-130">A estrutura do Flux usa YAML para definir a topologia Storm.</span><span class="sxs-lookup"><span data-stu-id="93099-130">The Flux framework uses YAML to define the Storm topology.</span></span> <span data-ttu-id="93099-131">O texto a seguir é um exemplo de um componente do Python é referenciado no documento YAML:</span><span class="sxs-lookup"><span data-stu-id="93099-131">The following text is an example of how to reference a Python component in the YAML document:</span></span>

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

<span data-ttu-id="93099-132">A classe `FluxShellSpout` é usada para iniciar o script `sentencespout.py` que implementa o spout.</span><span class="sxs-lookup"><span data-stu-id="93099-132">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span></span>

<span data-ttu-id="93099-133">O Flux espera que os scripts de Python estejam no diretório `/resources`, dentro do arquivo jar que contém a topologia.</span><span class="sxs-lookup"><span data-stu-id="93099-133">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span></span> <span data-ttu-id="93099-134">Assim, este exemplo armazena os scripts do Python no diretório `/multilang/resources`.</span><span class="sxs-lookup"><span data-stu-id="93099-134">So this example stores the Python scripts in the `/multilang/resources` directory.</span></span> <span data-ttu-id="93099-135">O `pom.xml` inclui esse arquivo usando o XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="93099-135">The `pom.xml` includes this file using the following XML:</span></span>

```xml
<!-- include the Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="93099-136">Conforme mencionado anteriormente, há um arquivo `storm.py` que implementa a definição do Thrift para o Storm.</span><span class="sxs-lookup"><span data-stu-id="93099-136">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span></span> <span data-ttu-id="93099-137">A estrutura do Flux inclui o `storm.py` automaticamente quando o projeto é compilado, portanto, você não precisa se preocupar em incluí-lo.</span><span class="sxs-lookup"><span data-stu-id="93099-137">The Flux framework includes `storm.py` automatically when the project is built, so you don't have to worry about including it.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="93099-138">Compilar o projeto</span><span class="sxs-lookup"><span data-stu-id="93099-138">Build the project</span></span>

<span data-ttu-id="93099-139">Da raiz do projeto, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="93099-139">From the root of the project, use the following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="93099-140">Esse comando cria um arquivo `target/WordCount-1.0-SNAPSHOT.jar` que contém a topologia compilada.</span><span class="sxs-lookup"><span data-stu-id="93099-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span></span>

## <a name="run-the-topology-locally"></a><span data-ttu-id="93099-141">Executar a topologia localmente</span><span class="sxs-lookup"><span data-stu-id="93099-141">Run the topology locally</span></span>

<span data-ttu-id="93099-142">Para executar a topologia localmente, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="93099-142">To run the topology locally, use the following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="93099-143">Esse comando requer um ambiente de desenvolvimento local do Storm.</span><span class="sxs-lookup"><span data-stu-id="93099-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="93099-144">Para obter mais informações, consulte [Configurar um ambiente de desenvolvimento](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span><span class="sxs-lookup"><span data-stu-id="93099-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="93099-145">Uma vez que a topologia é iniciada, ela emite informações para o console local semelhantes ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="93099-145">Once the topology starts, it emits information to the local console similar to the following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="93099-146">Para interromper a topologia, use __Ctrl+C__.</span><span class="sxs-lookup"><span data-stu-id="93099-146">To stop the topology, use __Ctrl + C__.</span></span>

## <a name="run-the-storm-topology-on-hdinsight"></a><span data-ttu-id="93099-147">Executar a topologia Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="93099-147">Run the Storm topology on HDInsight</span></span>

1. <span data-ttu-id="93099-148">Use o comando a seguir para copiar o arquivo `WordCount-1.0-SNAPSHOT.jar` para o Storm no cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="93099-148">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="93099-149">Substitua `sshuser` pelo usuário SSH para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="93099-149">Replace `sshuser` with the SSH user for your cluster.</span></span> <span data-ttu-id="93099-150">Substitua `mycluster` pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="93099-150">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="93099-151">Pode ser solicitado que você insira a senha do usuário SSH.</span><span class="sxs-lookup"><span data-stu-id="93099-151">You may be prompted to enter the password for the SSH user.</span></span>

    <span data-ttu-id="93099-152">Para obter mais informações sobre como usar o SSH e o SCP, confira [Usar o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="93099-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="93099-153">Depois que o arquivo for carregado, conecte-se ao cluster usando SSH:</span><span class="sxs-lookup"><span data-stu-id="93099-153">Once the file has been uploaded, connect to the cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="93099-154">Na sessão de SSH, use o seguinte comando para iniciar a topologia no cluster:</span><span class="sxs-lookup"><span data-stu-id="93099-154">From the SSH session, use the following command to start the topology on the cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="93099-155">Você pode usar a interface do usuário do Storm para exibir a topologia no cluster.</span><span class="sxs-lookup"><span data-stu-id="93099-155">You can use the Storm UI to view the topology on the cluster.</span></span> <span data-ttu-id="93099-156">Essa interface do usuário do Storm está localizada em https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="93099-156">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="93099-157">Substitua `mycluster` pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="93099-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="93099-158">Após ser iniciada, uma topologia do Storm é executada até ser interrompida.</span><span class="sxs-lookup"><span data-stu-id="93099-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="93099-159">Para interromper a topologia, é possível usar um dos métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="93099-159">To stop the topology, use one of the following methods:</span></span>
>
> * <span data-ttu-id="93099-160">O comando `storm kill TOPOLOGYNAME` da linha de comando</span><span class="sxs-lookup"><span data-stu-id="93099-160">The `storm kill TOPOLOGYNAME` command from the command line</span></span>
> * <span data-ttu-id="93099-161">O botão **Encerrar** na interface do usuário Storm.</span><span class="sxs-lookup"><span data-stu-id="93099-161">The **Kill** button in the Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="93099-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="93099-162">Next steps</span></span>

<span data-ttu-id="93099-163">Consulte os seguintes documentos para conhecer outras maneiras de usar o Python com o HDInsight:</span><span class="sxs-lookup"><span data-stu-id="93099-163">See the following documents for other ways to use Python with HDInsight:</span></span>

* [<span data-ttu-id="93099-164">Como usar o Python para trabalhos de MapReduce de streaming</span><span class="sxs-lookup"><span data-stu-id="93099-164">How to use Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="93099-165">Como usar UDF (Funções Definidas pelo Usuário) do Python no Pig e Hive</span><span class="sxs-lookup"><span data-stu-id="93099-165">How to use Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
