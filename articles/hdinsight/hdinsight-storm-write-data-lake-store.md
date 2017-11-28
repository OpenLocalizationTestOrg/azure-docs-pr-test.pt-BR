---
title: "Gravação do Apache Storm para Armazenamento/Data Lake Store – HDInsight do Azure | Microsoft Docs"
description: "Saiba como usar o Apache Storm para gravar no armazenamento compatível com o HDFS para HDInsight. Azure Storage ou Azure Data Lake Store fornece o armazenamento de compatível com HDFS para HDInsight. Este documento e o exemplo associado demonstram como o componente de HdfsBolt pode ser usado para gravar o armazenamento padrão de um Storm no cluster HDInsight."
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
ms.openlocfilehash: 10dc8789e8f4a2b27fd3a4c6fec2ab28c674170a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="write-to-hdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="d4bf7-105">Gravar para HDFS do Apache Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4bf7-105">Write to HDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="d4bf7-106">Saiba como usar o Storm para gravar dados no armazenamento compatível com HDFS usado pelo Apache Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-106">Learn how to use Storm to write data to the HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="d4bf7-107">O HDInsight pode usar o Armazenamento do Azure e o Azure Data Lake Store como armazenamento compatível com HDFS.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="d4bf7-108">O Storm fornece um componente [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) que grava dados no HDFS.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data to HDFS.</span></span> <span data-ttu-id="d4bf7-109">Esse documento fornece informações sobre como gravar em qualquer um dos tipos de armazenamento do HdfsBolt.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-109">This document provides information on writing to either type of storage from the HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d4bf7-110">A topologia de exemplo usada neste documento depende de componentes que estão incluídos com o Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-110">The example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="d4bf7-111">Pode exigir modificações para funcionar com o Azure Data Lake Store quando usado com outros clusters do Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-111">It may require modification to work with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="d4bf7-112">Obter código</span><span class="sxs-lookup"><span data-stu-id="d4bf7-112">Get the code</span></span>

<span data-ttu-id="d4bf7-113">O projeto que contém essa topologia está disponível como um download em [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="d4bf7-113">The project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="d4bf7-114">Para compilar esse projeto, você precisará da seguinte configuração para seu ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-114">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="d4bf7-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="d4bf7-116">HDInsight 3.5 ou superior exige Java 8.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="d4bf7-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="d4bf7-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="d4bf7-118">As seguintes variáveis de ambiente podem ser definidas quando você instala o Java e o JDK em sua estação de trabalho de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-118">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="d4bf7-119">No entanto, você deve verificar se elas existem e se contêm os valores corretos para o seu sistema.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="d4bf7-120">`JAVA_HOME` – deve apontar para o diretório em que o JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-120">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="d4bf7-121">`PATH` – deve conter os seguintes caminhos:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-121">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="d4bf7-122">`JAVA_HOME` (ou o caminho equivalente).</span><span class="sxs-lookup"><span data-stu-id="d4bf7-122">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="d4bf7-123">`JAVA_HOME\bin` (ou o caminho equivalente).</span><span class="sxs-lookup"><span data-stu-id="d4bf7-123">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="d4bf7-124">O diretório em que o Maven está instalado.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-124">The directory where Maven is installed.</span></span>

## <a name="how-to-use-the-hdfsbolt-with-hdinsight"></a><span data-ttu-id="d4bf7-125">Como usar o HdfsBolt com HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4bf7-125">How to use the HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4bf7-126">Antes de usar o HdfsBolt com Storm no HDInsight, primeiro você deve usar uma ação de script para copiar arquivos jar necessários para o `extpath` para o Storm.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-126">Before using the HdfsBolt with Storm on HDInsight, you must first use a script action to copy required jar files into the `extpath` for Storm.</span></span> <span data-ttu-id="d4bf7-127">Para obter mais informações, consulte a seção [Configurar o cluster](#configure).</span><span class="sxs-lookup"><span data-stu-id="d4bf7-127">For more information, see the [Configure the cluster](#configure) section.</span></span>

<span data-ttu-id="d4bf7-128">O HdfsBolt usa o esquema de arquivo que você fornece para compreender como gravar no HDFS.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-128">The HdfsBolt uses the file scheme that you provide to understand how to write to HDFS.</span></span> <span data-ttu-id="d4bf7-129">Com o HDInsight, use um dos seguintes esquemas:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-129">With HDInsight, use one of the following schemes:</span></span>

* <span data-ttu-id="d4bf7-130">`wasb://`: usado com uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="d4bf7-131">`adl://`: usado com o Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="d4bf7-132">A tabela a seguir fornece exemplos de como usar o esquema de arquivos para cenários diferentes:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-132">The following table provides examples of using the file scheme for different scenarios:</span></span>

| <span data-ttu-id="d4bf7-133">Esquema</span><span class="sxs-lookup"><span data-stu-id="d4bf7-133">Scheme</span></span> | <span data-ttu-id="d4bf7-134">Observações</span><span class="sxs-lookup"><span data-stu-id="d4bf7-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="d4bf7-135">A conta de armazenamento padrão é um contêiner de blob em uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d4bf7-135">The default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="d4bf7-136">A conta de armazenamento padrão é um diretório no Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-136">The default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="d4bf7-137">Durante a criação do cluster, você pode especificar o diretório no Data Lake Store que é a raiz do HDFS do cluster.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-137">During cluster creation, you specify the directory in Data Lake Store that is the root of the cluster's HDFS.</span></span> <span data-ttu-id="d4bf7-138">Por exemplo, o diretório `/clusters/myclustername/`.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-138">For example, the `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="d4bf7-139">Uma conta de armazenamento do Azure não padrão (adicional) associada ao cluster.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-139">A non-default (additional) Azure storage account associated with the cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="d4bf7-140">A raiz do Data Lake Store usada pelo cluster.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-140">The root of the Data Lake Store used by the cluster.</span></span> <span data-ttu-id="d4bf7-141">Esse esquema permite que você acesse dados localizados fora do diretório que contém o sistema de arquivos do cluster.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-141">This scheme allows you to access data that is located outside the directory that contains the cluster file system.</span></span> |

<span data-ttu-id="d4bf7-142">Para obter mais informações, consulte a referência [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) em Apache.org.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-142">For more information, see the [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="d4bf7-143">Exemplo de configuração</span><span class="sxs-lookup"><span data-stu-id="d4bf7-143">Example configuration</span></span>

<span data-ttu-id="d4bf7-144">O YAML a seguir é um trecho do arquivo `resources/writetohdfs.yaml` incluído no exemplo.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-144">The following YAML is an excerpt from the `resources/writetohdfs.yaml` file included in the example.</span></span> <span data-ttu-id="d4bf7-145">Esse arquivo define a topologia do Storm usando a estrutura [Flux](https://storm.apache.org/releases/1.1.0/flux.html) para o Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-145">This file defines the Storm topology using the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

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

<span data-ttu-id="d4bf7-146">Esse YAML define os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-146">This YAML defines the following items:</span></span>

* <span data-ttu-id="d4bf7-147">`syncPolicy`: define quando arquivos são sincronizados/liberados para o sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-147">`syncPolicy`: Defines when files are synched/flushed to the file system.</span></span> <span data-ttu-id="d4bf7-148">Neste exemplo, a cada 1.000 tuplas.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="d4bf7-149">`fileNameFormat`: define o padrão de nome de arquivo e caminho a ser usado ao gravar os arquivos.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-149">`fileNameFormat`: Defines the path and file name pattern to use when writing files.</span></span> <span data-ttu-id="d4bf7-150">Neste exemplo, o caminho é fornecido no tempo de execução usando um filtro e a extensão de arquivo é `.txt`.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-150">In this example, the path is provided at runtime using a filter, and the file extension is `.txt`.</span></span>
* <span data-ttu-id="d4bf7-151">`recordFormat`: define o formato interno dos arquivos gravados.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-151">`recordFormat`: Defines the internal format of the files written.</span></span> <span data-ttu-id="d4bf7-152">Neste exemplo, os campos são delimitados pelo caractere `|`.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-152">In this example, fields are delimited by the `|` character.</span></span>
* <span data-ttu-id="d4bf7-153">`rotationPolicy`: define quando girar arquivos.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-153">`rotationPolicy`: Defines when to rotate files.</span></span> <span data-ttu-id="d4bf7-154">Neste exemplo, nenhuma rotação é executada.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="d4bf7-155">`hdfs-bolt`: usa os componentes anteriores como parâmetros de configuração para a classe `HdfsBolt`.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-155">`hdfs-bolt`: Uses the previous components as configuration parameters for the `HdfsBolt` class.</span></span>

<span data-ttu-id="d4bf7-156">Para saber mais sobre a estrutura Flux, confirma [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="d4bf7-156">For more information on the Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-the-cluster"></a><span data-ttu-id="d4bf7-157">Configurar o cluster</span><span class="sxs-lookup"><span data-stu-id="d4bf7-157">Configure the cluster</span></span>

<span data-ttu-id="d4bf7-158">Por padrão, o Storm no HDInsight não inclui os componentes que o HdfsBolt usa para se comunicar com o Armazenamento do Azure ou o Data Lake Store no classpath do Storm.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-158">By default, Storm on HDInsight does not include the components that HdfsBolt uses to communicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="d4bf7-159">Use a ação de script a seguir para adicionar esses componentes ao diretório `extlib` para Storm no seu cluster:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-159">Use the following script action to add these components to the `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="d4bf7-160">| URI de script | Nós aos quais aplicá-lo | Parâmetros | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | Nenhum |</span><span class="sxs-lookup"><span data-stu-id="d4bf7-160">| Script URI | Nodes to apply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="d4bf7-161">Para obter informações sobre como usar esse script com o cluster, consulte o documento [Personalizar clusters do HDInsight usando ações de script](./hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d4bf7-161">For information on using this script with your cluster, see the [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-the-topology"></a><span data-ttu-id="d4bf7-162">Compilar e criar o pacote da topologia</span><span class="sxs-lookup"><span data-stu-id="d4bf7-162">Build and package the topology</span></span>

1. <span data-ttu-id="d4bf7-163">Baixe o projeto de exemplo em [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) em seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-163">Download the example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) to your development environment.</span></span>

2. <span data-ttu-id="d4bf7-164">De um prompt de comando, terminal ou shell sessão, altere diretórios para a raiz do projeto baixado.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-164">From a command prompt, terminal, or shell session, change directories to the root of the downloaded project.</span></span> <span data-ttu-id="d4bf7-165">Para criar e empacotar a topologia, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-165">To build and package the topology, use the following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="d4bf7-166">Depois de terminar de criar e empacotar, há um novo diretório chamado `target` contendo um arquivo denominado `StormToHdfs-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-166">Once the build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="d4bf7-167">Esse arquivo contém a topologia compilada.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-167">This file contains the compiled topology.</span></span>

## <a name="deploy-and-run-the-topology"></a><span data-ttu-id="d4bf7-168">Implantar e executar a topologia</span><span class="sxs-lookup"><span data-stu-id="d4bf7-168">Deploy and run the topology</span></span>

1. <span data-ttu-id="d4bf7-169">Use o seguinte comando para copiar a topologia para o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-169">Use the following command to copy the topology to the HDInsight cluster.</span></span> <span data-ttu-id="d4bf7-170">Substitua**USER** pelo nome de usuário SSH usado ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-170">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="d4bf7-171">Substitua **CLUSTERNAME** pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-171">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="d4bf7-172">Quando solicitado, digite a senha usada ao criar o usuário SSH para o cluster.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-172">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="d4bf7-173">Se você usou uma chave pública em vez de uma senha, talvez precise usar o parâmetro `-i` para especificar o caminho para a chave privada correspondente.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-173">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d4bf7-174">Para saber mais sobre como usar o `scp` com HDInsight, confira [Usar SSH com HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d4bf7-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d4bf7-175">Quando o carregamento for concluído, use o seguinte para se conectar ao cluster HDInsight usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-175">Once the upload completes, use the following to connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="d4bf7-176">Substitua**USER** pelo nome de usuário SSH usado ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-176">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="d4bf7-177">Substitua **CLUSTERNAME** pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-177">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="d4bf7-178">Quando solicitado, digite a senha usada ao criar o usuário SSH para o cluster.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-178">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="d4bf7-179">Se você usou uma chave pública em vez de uma senha, talvez precise usar o parâmetro `-i` para especificar o caminho para a chave privada correspondente.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-179">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   <span data-ttu-id="d4bf7-180">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d4bf7-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="d4bf7-181">Depois de conectado, use o seguinte comando para criar um arquivo chamado `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-181">Once connected, use the following command to create a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="d4bf7-182">Use o seguinte texto como o conteúdo do arquivo `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-182">Use the following text as the contents of the `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="d4bf7-183">Esse exemplo presume que o cluster usa uma conta de Armazenamento do Azure como armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-183">This example assumes that your cluster uses an Azure Storage account as the default storage.</span></span> <span data-ttu-id="d4bf7-184">Se o cluster usar o Azure Data Lake Store, use `hdfs.url: adl:///`.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="d4bf7-185">Para salvar o arquivo, use __Ctrl + X__, em seguida, __Y__ e, por fim, __Enter__.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-185">To save the file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="d4bf7-186">Os valores desse arquivo definem a URL do Data Lake Store e o nome do diretório no qual os dados são gravados.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-186">The values in this file set the Data Lake store URL and the directory name that data is written to.</span></span>

3. <span data-ttu-id="d4bf7-187">Use o seguinte comando para iniciar a topologia:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-187">Use the following command to start the topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="d4bf7-188">Esse comando inicia a topologia usando a estrutura Flux, enviando-a para o nó Nimbus do cluster.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-188">This command starts the topology using the Flux framework by submitting it to the Nimbus node of the cluster.</span></span> <span data-ttu-id="d4bf7-189">A topologia é definida pelo arquivo `writetohdfs.yaml` incluído no jar.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-189">The topology is defined by the `writetohdfs.yaml` file included in the jar.</span></span> <span data-ttu-id="d4bf7-190">O arquivo `dev.properties` é passado como um filtro e os valores contidos no arquivo são lidos pela topologia.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-190">The `dev.properties` file is passed as a filter, and the values contained in the file are read by the topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="d4bf7-191">Exibir dados de saída</span><span class="sxs-lookup"><span data-stu-id="d4bf7-191">View output data</span></span>

<span data-ttu-id="d4bf7-192">Para exibir os dados, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-192">To view the data, use the following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="d4bf7-193">Uma lista dos arquivos criados por essa topologia é exibida.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-193">A list of the files created by this topology is displayed.</span></span>

<span data-ttu-id="d4bf7-194">A seguinte lista é um exemplo dos dados retornados pelos comandos anteriores:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-194">The following list is an example of the data retuned by the previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-the-topology"></a><span data-ttu-id="d4bf7-195">Parar a topologia</span><span class="sxs-lookup"><span data-stu-id="d4bf7-195">Stop the topology</span></span>

<span data-ttu-id="d4bf7-196">As topologias do Storm são executadas até serem interrompidas ou o cluster ser excluído.</span><span class="sxs-lookup"><span data-stu-id="d4bf7-196">Storm topologies run until stopped, or the cluster is deleted.</span></span> <span data-ttu-id="d4bf7-197">Para interromper a topologia, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d4bf7-197">To stop the topology, use the following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="d4bf7-198">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="d4bf7-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="d4bf7-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4bf7-199">Next steps</span></span>

<span data-ttu-id="d4bf7-200">Agora que você aprendeu a usar o Storm para gravar no Armazenamento do Azure e no Azure Data Lake Store, descubra outros [exemplos do Storm para HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d4bf7-200">Now that you have learned how to use Storm to write to Azure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

