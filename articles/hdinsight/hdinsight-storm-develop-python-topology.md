---
title: aaaApache Storm com componentes de Python - HDInsight do Azure | Microsoft Docs
description: Saiba como toocreate uma topologia do Apache Storm que usa componentes de Python.
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
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="7b548-104">Desenvolver topologias do Apache Storm usando o Python no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b548-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="7b548-105">Saiba como toocreate uma topologia do Apache Storm que usa componentes de Python.</span><span class="sxs-lookup"><span data-stu-id="7b548-105">Learn how toocreate an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="7b548-106">Apache Storm dá suporte a vários idiomas, permitindo até que você toocombine componentes de diversos idiomas em uma topologia.</span><span class="sxs-lookup"><span data-stu-id="7b548-106">Apache Storm supports multiple languages, even allowing you toocombine components from several languages in one topology.</span></span> <span data-ttu-id="7b548-107">Olá fluxo estrutura (introduzida com Storm 0.10.0) permite que você tooeasily criar soluções que usam componentes do Python.</span><span class="sxs-lookup"><span data-stu-id="7b548-107">hello Flux framework (introduced with Storm 0.10.0) allows you tooeasily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b548-108">informações de saudação neste documento foi testadas usando o Storm no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="7b548-108">hello information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="7b548-109">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7b548-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7b548-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7b548-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="7b548-111">saudação de código para este projeto está disponível em [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="7b548-111">hello code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b548-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7b548-112">Prerequisites</span></span>

* <span data-ttu-id="7b548-113">Python 2.7 ou posterior</span><span class="sxs-lookup"><span data-stu-id="7b548-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="7b548-114">Java JDK 1.8 ou superior</span><span class="sxs-lookup"><span data-stu-id="7b548-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="7b548-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="7b548-115">Maven 3</span></span>

* <span data-ttu-id="7b548-116">(Opcional) Um ambiente de desenvolvimento local do Storm.</span><span class="sxs-lookup"><span data-stu-id="7b548-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="7b548-117">Um ambiente Storm local só é necessário se você quiser toorun topologia de saudação localmente.</span><span class="sxs-lookup"><span data-stu-id="7b548-117">A local Storm environment is only needed if you want toorun hello topology locally.</span></span> <span data-ttu-id="7b548-118">Para obter mais informações, consulte [Configurar um ambiente de desenvolvimento](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="7b548-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="7b548-119">Suporte a várias linguagens no Storm</span><span class="sxs-lookup"><span data-stu-id="7b548-119">Storm multi-language support</span></span>

<span data-ttu-id="7b548-120">Apache Storm foi projetado toowork com componentes escritos usando qualquer linguagem de programação.</span><span class="sxs-lookup"><span data-stu-id="7b548-120">Apache Storm was designed toowork with components written using any programming language.</span></span> <span data-ttu-id="7b548-121">componentes de saudação devem entender como toowork com hello [definição Thrift Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="7b548-121">hello components must understand how toowork with hello [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="7b548-122">Para Python, um módulo é fornecido como parte do projeto do Apache Storm Olá que permite que você tooeasily interface com Storm.</span><span class="sxs-lookup"><span data-stu-id="7b548-122">For Python, a module is provided as part of hello Apache Storm project that allows you tooeasily interface with Storm.</span></span> <span data-ttu-id="7b548-123">Você pode encontrar esse módulo em [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="7b548-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="7b548-124">Tempestade é um processo de Java que é executado em Olá Máquina Virtual Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="7b548-124">Storm is a Java process that runs on hello Java Virtual Machine (JVM).</span></span> <span data-ttu-id="7b548-125">Componentes escritos em outras linguagens são executados como subprocessos.</span><span class="sxs-lookup"><span data-stu-id="7b548-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="7b548-126">Olá Storm se comunica com esses subprocessos usando JSON mensagens enviadas pela stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="7b548-126">hello Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="7b548-127">Mais detalhes sobre a comunicação entre os componentes podem ser encontrados no hello [Multi-lang protocolo](https://storm.apache.org/documentation/Multilang-protocol.html) documentação.</span><span class="sxs-lookup"><span data-stu-id="7b548-127">More details on communication between components can be found in hello [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-hello-flux-framework"></a><span data-ttu-id="7b548-128">Python com estrutura de fluxo de saudação</span><span class="sxs-lookup"><span data-stu-id="7b548-128">Python with hello Flux framework</span></span>

<span data-ttu-id="7b548-129">estrutura de fluxo de saudação permite que você toodefine topologias de Storm separadamente de componentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b548-129">hello Flux framework allows you toodefine Storm topologies separately from hello components.</span></span> <span data-ttu-id="7b548-130">estrutura do fluxo de Olá usa topologia de Storm YAML toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="7b548-130">hello Flux framework uses YAML toodefine hello Storm topology.</span></span> <span data-ttu-id="7b548-131">Olá, texto a seguir é um exemplo de como tooreference um componente de Python no documento YAML hello:</span><span class="sxs-lookup"><span data-stu-id="7b548-131">hello following text is an example of how tooreference a Python component in hello YAML document:</span></span>

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

<span data-ttu-id="7b548-132">Olá classe `FluxShellSpout` é usado toostart hello `sentencespout.py` script que implementa spout hello.</span><span class="sxs-lookup"><span data-stu-id="7b548-132">hello class `FluxShellSpout` is used toostart hello `sentencespout.py` script that implements hello spout.</span></span>

<span data-ttu-id="7b548-133">Fluxo espera Olá Python scripts toobe no hello `/resources` diretório dentro do arquivo jar Olá que contém a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b548-133">Flux expects hello Python scripts toobe in hello `/resources` directory inside hello jar file that contains hello topology.</span></span> <span data-ttu-id="7b548-134">Para este exemplo armazena scripts de Python Olá em Olá `/multilang/resources` directory.</span><span class="sxs-lookup"><span data-stu-id="7b548-134">So this example stores hello Python scripts in hello `/multilang/resources` directory.</span></span> <span data-ttu-id="7b548-135">Olá `pom.xml` inclui esse arquivo usando Olá XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b548-135">hello `pom.xml` includes this file using hello following XML:</span></span>

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="7b548-136">Como mencionado anteriormente, há um `storm.py` arquivo que implementa a definição de Thrift Olá para Storm.</span><span class="sxs-lookup"><span data-stu-id="7b548-136">As mentioned earlier, there is a `storm.py` file that implements hello Thrift definition for Storm.</span></span> <span data-ttu-id="7b548-137">Olá fluxo framework inclui `storm.py` automaticamente quando Olá projeto é compilado, para que você não tenha tooworry sobre incluí-lo.</span><span class="sxs-lookup"><span data-stu-id="7b548-137">hello Flux framework includes `storm.py` automatically when hello project is built, so you don't have tooworry about including it.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="7b548-138">Compilar o projeto de saudação</span><span class="sxs-lookup"><span data-stu-id="7b548-138">Build hello project</span></span>

<span data-ttu-id="7b548-139">De raiz de saudação do projeto hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b548-139">From hello root of hello project, use hello following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="7b548-140">Este comando cria um `target/WordCount-1.0-SNAPSHOT.jar` arquivo que contém a saudação compilado topologia.</span><span class="sxs-lookup"><span data-stu-id="7b548-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains hello compiled topology.</span></span>

## <a name="run-hello-topology-locally"></a><span data-ttu-id="7b548-141">Executar topologia Olá localmente</span><span class="sxs-lookup"><span data-stu-id="7b548-141">Run hello topology locally</span></span>

<span data-ttu-id="7b548-142">topologia de saudação do toorun localmente, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b548-142">toorun hello topology locally, use hello following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="7b548-143">Esse comando requer um ambiente de desenvolvimento local do Storm.</span><span class="sxs-lookup"><span data-stu-id="7b548-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="7b548-144">Para obter mais informações, consulte [Configurar um ambiente de desenvolvimento](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span><span class="sxs-lookup"><span data-stu-id="7b548-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="7b548-145">Uma vez Olá topologia inicia, ele emite informações toohello console local semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b548-145">Once hello topology starts, it emits information toohello local console similar toohello following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="7b548-146">topologia de saudação toostop, use __Ctrl + C__.</span><span class="sxs-lookup"><span data-stu-id="7b548-146">toostop hello topology, use __Ctrl + C__.</span></span>

## <a name="run-hello-storm-topology-on-hdinsight"></a><span data-ttu-id="7b548-147">Execute a topologia de profusão de saudação no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b548-147">Run hello Storm topology on HDInsight</span></span>

1. <span data-ttu-id="7b548-148">Olá toocopy do comando de uso a seguir de saudação `WordCount-1.0-SNAPSHOT.jar` tooyour Storm no cluster HDInsight do arquivo:</span><span class="sxs-lookup"><span data-stu-id="7b548-148">Use hello following command toocopy hello `WordCount-1.0-SNAPSHOT.jar` file tooyour Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="7b548-149">Substituir `sshuser` com usuário SSH Olá para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="7b548-149">Replace `sshuser` with hello SSH user for your cluster.</span></span> <span data-ttu-id="7b548-150">Substituir `mycluster` com o nome do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7b548-150">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="7b548-151">Você pode ser solicitados tooenter senha Olá usuário SSH de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b548-151">You may be prompted tooenter hello password for hello SSH user.</span></span>

    <span data-ttu-id="7b548-152">Para obter mais informações sobre como usar o SSH e o SCP, confira [Usar o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7b548-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="7b548-153">Depois que o arquivo hello foi carregado, conecte-se toohello cluster usando o SSH:</span><span class="sxs-lookup"><span data-stu-id="7b548-153">Once hello file has been uploaded, connect toohello cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="7b548-154">Da sessão SSH hello, use Olá topologia de saudação do comando toostart a seguir no cluster hello:</span><span class="sxs-lookup"><span data-stu-id="7b548-154">From hello SSH session, use hello following command toostart hello topology on hello cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="7b548-155">Você pode usar a topologia de Olá Olá Storm da interface do usuário tooview em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7b548-155">You can use hello Storm UI tooview hello topology on hello cluster.</span></span> <span data-ttu-id="7b548-156">Olá profusão de interface do usuário está localizado em https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="7b548-156">hello Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="7b548-157">Substitua `mycluster` pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="7b548-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="7b548-158">Após ser iniciada, uma topologia do Storm é executada até ser interrompida.</span><span class="sxs-lookup"><span data-stu-id="7b548-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="7b548-159">toostop Olá topologia, use um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="7b548-159">toostop hello topology, use one of hello following methods:</span></span>
>
> * <span data-ttu-id="7b548-160">Olá `storm kill TOPOLOGYNAME` comando da linha de comando Olá</span><span class="sxs-lookup"><span data-stu-id="7b548-160">hello `storm kill TOPOLOGYNAME` command from hello command line</span></span>
> * <span data-ttu-id="7b548-161">Olá **Kill** botão Olá profusão de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="7b548-161">hello **Kill** button in hello Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7b548-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b548-162">Next steps</span></span>

<span data-ttu-id="7b548-163">Consulte Olá documentos para outra maneiras de toouse Python com HDInsight a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b548-163">See hello following documents for other ways toouse Python with HDInsight:</span></span>

* [<span data-ttu-id="7b548-164">Como toouse Python para streaming trabalhos MapReduce</span><span class="sxs-lookup"><span data-stu-id="7b548-164">How toouse Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="7b548-165">Como toouse Python definida pelo usuário funções (UDF) na Pig e Hive</span><span class="sxs-lookup"><span data-stu-id="7b548-165">How toouse Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
