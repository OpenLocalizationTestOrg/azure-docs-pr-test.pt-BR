---
title: "aaaApache Storm gravar tooStorage/Data Lake repositório - HDInsight do Azure | Microsoft Docs"
description: "Saiba como toouse hello o armazenamento do Apache Storm toowrite toohello compatível com o HDFS para HDInsight. Azure Storage ou repositório Azure Data Lake fornecem armazenamento de saudação comptabile HDFS para HDInsight. Esse documento e exemplo de associado hello, demonstram como o componente de HdfsBolt Olá pode ser usados toowrite toohello padrão armazenamento de uma profusão de cluster HDInsight."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="8713f-105">Gravar tooHDFS do Apache Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8713f-105">Write tooHDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="8713f-106">Saiba como toouse Storm toowrite dados toohello armazenamento compatível com o HDFS usada pelo Apache Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8713f-106">Learn how toouse Storm toowrite data toohello HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="8713f-107">O HDInsight pode usar o Armazenamento do Azure e o Azure Data Lake Store como armazenamento compatível com HDFS.</span><span class="sxs-lookup"><span data-stu-id="8713f-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="8713f-108">Tempestade fornece um [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) componente que grava dados tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="8713f-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data tooHDFS.</span></span> <span data-ttu-id="8713f-109">Este documento fornece informações sobre como escrever tooeither tipo de armazenamento de saudação HdfsBolt.</span><span class="sxs-lookup"><span data-stu-id="8713f-109">This document provides information on writing tooeither type of storage from hello HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8713f-110">exemplo Hello topologia usada neste documento depende de componentes que estão incluídos com Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8713f-110">hello example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="8713f-111">Ele pode exigir a modificação toowork com o repositório do Azure Data Lake quando usado com outros clusters Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="8713f-111">It may require modification toowork with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="8713f-112">Obter o código de saudação</span><span class="sxs-lookup"><span data-stu-id="8713f-112">Get hello code</span></span>

<span data-ttu-id="8713f-113">projeto de saudação que contém essa topologia está disponível como um download do [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="8713f-113">hello project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="8713f-114">toocompile este projeto, você precisa Olá seguinte configuração para o seu ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="8713f-114">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="8713f-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior.</span><span class="sxs-lookup"><span data-stu-id="8713f-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="8713f-116">HDInsight 3.5 ou superior exige Java 8.</span><span class="sxs-lookup"><span data-stu-id="8713f-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="8713f-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="8713f-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="8713f-118">Olá seguintes variáveis de ambiente podem ser definidas quando você instala o Java e hello JDK em sua estação de trabalho de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="8713f-118">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="8713f-119">No entanto, você deve verificar se eles existem e que eles contêm valores de saudação corretos para seu sistema.</span><span class="sxs-lookup"><span data-stu-id="8713f-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="8713f-120">`JAVA_HOME`-deve apontar toohello diretório onde hello JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="8713f-120">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="8713f-121">`PATH`-deve conter Olá caminhos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8713f-121">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="8713f-122">`JAVA_HOME`(ou caminho equivalente Olá).</span><span class="sxs-lookup"><span data-stu-id="8713f-122">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="8713f-123">`JAVA_HOME\bin`(ou caminho equivalente Olá).</span><span class="sxs-lookup"><span data-stu-id="8713f-123">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="8713f-124">diretório de saudação onde Maven está instalado.</span><span class="sxs-lookup"><span data-stu-id="8713f-124">hello directory where Maven is installed.</span></span>

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a><span data-ttu-id="8713f-125">Como toouse Olá HdfsBolt com HDInsight</span><span class="sxs-lookup"><span data-stu-id="8713f-125">How toouse hello HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8713f-126">Antes de usar o hello HdfsBolt com Storm no HDInsight, primeiro você deve usar um arquivos jar de toocopy necessário de ação de script em Olá `extpath` para Storm.</span><span class="sxs-lookup"><span data-stu-id="8713f-126">Before using hello HdfsBolt with Storm on HDInsight, you must first use a script action toocopy required jar files into hello `extpath` for Storm.</span></span> <span data-ttu-id="8713f-127">Para obter mais informações, consulte Olá [cluster de saudação configurar](#configure) seção.</span><span class="sxs-lookup"><span data-stu-id="8713f-127">For more information, see hello [Configure hello cluster](#configure) section.</span></span>

<span data-ttu-id="8713f-128">Olá HdfsBolt usa o esquema de arquivo hello que você forneça toounderstand como toowrite tooHDFS.</span><span class="sxs-lookup"><span data-stu-id="8713f-128">hello HdfsBolt uses hello file scheme that you provide toounderstand how toowrite tooHDFS.</span></span> <span data-ttu-id="8713f-129">Com HDInsight, use um dos seguintes esquemas de saudação:</span><span class="sxs-lookup"><span data-stu-id="8713f-129">With HDInsight, use one of hello following schemes:</span></span>

* <span data-ttu-id="8713f-130">`wasb://`: usado com uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8713f-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="8713f-131">`adl://`: usado com o Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8713f-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="8713f-132">Olá tabela a seguir fornece exemplos de como usar o esquema de arquivo hello para cenários diferentes:</span><span class="sxs-lookup"><span data-stu-id="8713f-132">hello following table provides examples of using hello file scheme for different scenarios:</span></span>

| <span data-ttu-id="8713f-133">Esquema</span><span class="sxs-lookup"><span data-stu-id="8713f-133">Scheme</span></span> | <span data-ttu-id="8713f-134">Observações</span><span class="sxs-lookup"><span data-stu-id="8713f-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="8713f-135">conta de armazenamento padrão de saudação é um contêiner de blob em uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8713f-135">hello default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="8713f-136">conta de armazenamento padrão de saudação é um diretório do repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8713f-136">hello default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="8713f-137">Durante a criação do cluster, você especifica o diretório de saudação no repositório Data Lake que é a raiz de saudação do HDFS do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="8713f-137">During cluster creation, you specify hello directory in Data Lake Store that is hello root of hello cluster's HDFS.</span></span> <span data-ttu-id="8713f-138">Por exemplo, Olá `/clusters/myclustername/` directory.</span><span class="sxs-lookup"><span data-stu-id="8713f-138">For example, hello `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="8713f-139">Uma conta de armazenamento do Azure (adicionais) não padrão associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="8713f-139">A non-default (additional) Azure storage account associated with hello cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="8713f-140">raiz de saudação do hello repositório Data Lake usados pelo cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8713f-140">hello root of hello Data Lake Store used by hello cluster.</span></span> <span data-ttu-id="8713f-141">Esse esquema permite que dados tooaccess localizado fora do diretório de saudação que contém o sistema de arquivos de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="8713f-141">This scheme allows you tooaccess data that is located outside hello directory that contains hello cluster file system.</span></span> |

<span data-ttu-id="8713f-142">Para obter mais informações, consulte Olá [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) referência em Apache.org.</span><span class="sxs-lookup"><span data-stu-id="8713f-142">For more information, see hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="8713f-143">Exemplo de configuração</span><span class="sxs-lookup"><span data-stu-id="8713f-143">Example configuration</span></span>

<span data-ttu-id="8713f-144">Olá, YAML seguinte é um trecho da saudação `resources/writetohdfs.yaml` arquivo incluído no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="8713f-144">hello following YAML is an excerpt from hello `resources/writetohdfs.yaml` file included in hello example.</span></span> <span data-ttu-id="8713f-145">Esse arquivo define a topologia de profusão de saudação usando Olá [fluxo](https://storm.apache.org/releases/1.1.0/flux.html) framework para o Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="8713f-145">This file defines hello Storm topology using hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

<span data-ttu-id="8713f-146">Este YAML define Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8713f-146">This YAML defines hello following items:</span></span>

* <span data-ttu-id="8713f-147">`syncPolicy`: Define quando arquivos são sincronizados/liberado toohello sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="8713f-147">`syncPolicy`: Defines when files are synched/flushed toohello file system.</span></span> <span data-ttu-id="8713f-148">Neste exemplo, a cada 1.000 tuplas.</span><span class="sxs-lookup"><span data-stu-id="8713f-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="8713f-149">`fileNameFormat`: Define toouse de padrão de nome de arquivo e caminho de saudação ao gravar os arquivos.</span><span class="sxs-lookup"><span data-stu-id="8713f-149">`fileNameFormat`: Defines hello path and file name pattern toouse when writing files.</span></span> <span data-ttu-id="8713f-150">Neste exemplo, o caminho de saudação é fornecido em tempo de execução usando um filtro e extensão de arquivo hello é `.txt`.</span><span class="sxs-lookup"><span data-stu-id="8713f-150">In this example, hello path is provided at runtime using a filter, and hello file extension is `.txt`.</span></span>
* <span data-ttu-id="8713f-151">`recordFormat`: Define o formato interno de saudação do hello arquivos gravados.</span><span class="sxs-lookup"><span data-stu-id="8713f-151">`recordFormat`: Defines hello internal format of hello files written.</span></span> <span data-ttu-id="8713f-152">Neste exemplo, os campos são delimitados por Olá `|` caracteres.</span><span class="sxs-lookup"><span data-stu-id="8713f-152">In this example, fields are delimited by hello `|` character.</span></span>
* <span data-ttu-id="8713f-153">`rotationPolicy`: Define quando toorotate arquivos.</span><span class="sxs-lookup"><span data-stu-id="8713f-153">`rotationPolicy`: Defines when toorotate files.</span></span> <span data-ttu-id="8713f-154">Neste exemplo, nenhuma rotação é executada.</span><span class="sxs-lookup"><span data-stu-id="8713f-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="8713f-155">`hdfs-bolt`: Usa Olá componentes anteriores como parâmetros de configuração para Olá `HdfsBolt` classe.</span><span class="sxs-lookup"><span data-stu-id="8713f-155">`hdfs-bolt`: Uses hello previous components as configuration parameters for hello `HdfsBolt` class.</span></span>

<span data-ttu-id="8713f-156">Para obter mais informações sobre a estrutura do fluxo de hello, consulte [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="8713f-156">For more information on hello Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-hello-cluster"></a><span data-ttu-id="8713f-157">Configurar o cluster Olá</span><span class="sxs-lookup"><span data-stu-id="8713f-157">Configure hello cluster</span></span>

<span data-ttu-id="8713f-158">Por padrão, Storm no HDInsight não incluir componentes Olá HdfsBolt usa toocommunicate com armazenamento do Azure ou repositório Data Lake no classpath do Storm.</span><span class="sxs-lookup"><span data-stu-id="8713f-158">By default, Storm on HDInsight does not include hello components that HdfsBolt uses toocommunicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="8713f-159">Script a seguir do uso Olá ação tooadd toohello esses componentes `extlib` diretório para Storm no cluster:</span><span class="sxs-lookup"><span data-stu-id="8713f-159">Use hello following script action tooadd these components toohello `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="8713f-160">| URI de script | Nós tooapply a | Parâmetros | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | Nenhum |</span><span class="sxs-lookup"><span data-stu-id="8713f-160">| Script URI | Nodes tooapply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="8713f-161">Para obter informações sobre como usar esse script com o cluster, consulte Olá [clusters de HDInsight personalizar usando ações de script](./hdinsight-hadoop-customize-cluster-linux.md) documento.</span><span class="sxs-lookup"><span data-stu-id="8713f-161">For information on using this script with your cluster, see hello [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-hello-topology"></a><span data-ttu-id="8713f-162">Compile e empacote topologia Olá</span><span class="sxs-lookup"><span data-stu-id="8713f-162">Build and package hello topology</span></span>

1. <span data-ttu-id="8713f-163">Baixe o projeto de exemplo hello de [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="8713f-163">Download hello example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour development environment.</span></span>

2. <span data-ttu-id="8713f-164">Em um prompt de comando, terminal ou sessão do shell, alterar diretórios toohello raiz de saudação baixou o projeto.</span><span class="sxs-lookup"><span data-stu-id="8713f-164">From a command prompt, terminal, or shell session, change directories toohello root of hello downloaded project.</span></span> <span data-ttu-id="8713f-165">toobuild e pacote hello topologia, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8713f-165">toobuild and package hello topology, use hello following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="8713f-166">Após a conclusão do build hello e empacotamento, há um novo diretório chamado `target`, que contém um arquivo chamado `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="8713f-166">Once hello build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="8713f-167">Este arquivo contém a topologia de saudação compilada.</span><span class="sxs-lookup"><span data-stu-id="8713f-167">This file contains hello compiled topology.</span></span>

## <a name="deploy-and-run-hello-topology"></a><span data-ttu-id="8713f-168">Implantar e executar topologia Olá</span><span class="sxs-lookup"><span data-stu-id="8713f-168">Deploy and run hello topology</span></span>

1. <span data-ttu-id="8713f-169">Use Olá cluster HDInsight toohello de topologia do comando toocopy Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="8713f-169">Use hello following command toocopy hello topology toohello HDInsight cluster.</span></span> <span data-ttu-id="8713f-170">Substituir **usuário** com nome de usuário SSH Olá usados ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="8713f-170">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="8713f-171">Substituir **CLUSTERNAME** com o nome de saudação do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8713f-171">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="8713f-172">Quando solicitado, insira a senha Olá usada ao criar usuário SSH Olá para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8713f-172">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="8713f-173">Se você usou uma chave pública em vez de uma senha, talvez seja necessário Olá toouse `-i` parâmetro toospecify Olá caminho toohello correspondência de chave privada.</span><span class="sxs-lookup"><span data-stu-id="8713f-173">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8713f-174">Para saber mais sobre como usar o `scp` com HDInsight, confira [Usar SSH com HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8713f-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="8713f-175">Após a conclusão do carregamento de hello, use Olá tooconnect toohello HDInsight cluster usando o SSH a seguir.</span><span class="sxs-lookup"><span data-stu-id="8713f-175">Once hello upload completes, use hello following tooconnect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="8713f-176">Substituir **usuário** com nome de usuário SSH Olá usados ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="8713f-176">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="8713f-177">Substituir **CLUSTERNAME** com o nome de saudação do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8713f-177">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="8713f-178">Quando solicitado, insira a senha Olá usada ao criar usuário SSH Olá para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8713f-178">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="8713f-179">Se você usou uma chave pública em vez de uma senha, talvez seja necessário Olá toouse `-i` parâmetro toospecify Olá caminho toohello correspondência de chave privada.</span><span class="sxs-lookup"><span data-stu-id="8713f-179">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   <span data-ttu-id="8713f-180">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8713f-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="8713f-181">Uma vez conectado, use Olá comando a seguir toocreate um arquivo chamado `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="8713f-181">Once connected, use hello following command toocreate a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="8713f-182">Saudação de uso após o texto como conteúdo de saudação do hello `dev.properties` arquivo:</span><span class="sxs-lookup"><span data-stu-id="8713f-182">Use hello following text as hello contents of hello `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="8713f-183">Este exemplo presume que o cluster usa uma conta de armazenamento do Azure como armazenamento de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8713f-183">This example assumes that your cluster uses an Azure Storage account as hello default storage.</span></span> <span data-ttu-id="8713f-184">Se o cluster usar o Azure Data Lake Store, use `hdfs.url: adl:///`.</span><span class="sxs-lookup"><span data-stu-id="8713f-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="8713f-185">arquivo de saudação toosave, use __Ctrl + X__, em seguida, __Y__e, finalmente, __Enter__.</span><span class="sxs-lookup"><span data-stu-id="8713f-185">toosave hello file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="8713f-186">valores Hello neste arquivo definir URL de repositório Data Lake hello e o nome do diretório de saudação que dados são gravados.</span><span class="sxs-lookup"><span data-stu-id="8713f-186">hello values in this file set hello Data Lake store URL and hello directory name that data is written to.</span></span>

3. <span data-ttu-id="8713f-187">Use Olá topologia de saudação do toostart de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8713f-187">Use hello following command toostart hello topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="8713f-188">Esse comando inicia a topologia hello usando a estrutura de fluxo de saudação enviando-o nó de Nimbus toohello de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8713f-188">This command starts hello topology using hello Flux framework by submitting it toohello Nimbus node of hello cluster.</span></span> <span data-ttu-id="8713f-189">topologia de saudação é definida por Olá `writetohdfs.yaml` arquivo incluído no jar hello.</span><span class="sxs-lookup"><span data-stu-id="8713f-189">hello topology is defined by hello `writetohdfs.yaml` file included in hello jar.</span></span> <span data-ttu-id="8713f-190">Olá `dev.properties` arquivo é passado como um filtro e valores hello contidos no arquivo hello são lidas por topologia hello.</span><span class="sxs-lookup"><span data-stu-id="8713f-190">hello `dev.properties` file is passed as a filter, and hello values contained in hello file are read by hello topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="8713f-191">Exibir dados de saída</span><span class="sxs-lookup"><span data-stu-id="8713f-191">View output data</span></span>

<span data-ttu-id="8713f-192">dados de saudação tooview, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8713f-192">tooview hello data, use hello following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="8713f-193">Uma lista de arquivos de saudação criados por essa topologia é exibida.</span><span class="sxs-lookup"><span data-stu-id="8713f-193">A list of hello files created by this topology is displayed.</span></span>

<span data-ttu-id="8713f-194">Olá lista a seguir é um exemplo de dados Olá reajustados por comandos anteriores hello:</span><span class="sxs-lookup"><span data-stu-id="8713f-194">hello following list is an example of hello data retuned by hello previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a><span data-ttu-id="8713f-195">Parar a topologia de saudação</span><span class="sxs-lookup"><span data-stu-id="8713f-195">Stop hello topology</span></span>

<span data-ttu-id="8713f-196">Topologias Storm executar até ser interrompido ou Olá cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="8713f-196">Storm topologies run until stopped, or hello cluster is deleted.</span></span> <span data-ttu-id="8713f-197">toostop Olá topologia, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8713f-197">toostop hello topology, use hello following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="8713f-198">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="8713f-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="8713f-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8713f-199">Next steps</span></span>

<span data-ttu-id="8713f-200">Agora que você aprendeu como toouse Storm toowrite tooAzure armazenamento e repositório Azure Data Lake, descobrir outros [profusão de exemplos para HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="8713f-200">Now that you have learned how toouse Storm toowrite tooAzure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

