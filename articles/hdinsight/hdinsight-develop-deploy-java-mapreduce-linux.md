---
title: "Criar MapReduce em Java para Hadoop – Azure HDInsight | Microsoft Docs"
description: Saiba como usar o Apache Maven para criar um aplicativo de MapReduce baseado em Java e, em seguida, execute-o com o Hadoop no Azure HDInsight.
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
ms.assetid: 9ee6384c-cb61-4087-8273-fb53fa27c1c3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 11d63f22204eb2acb530378f53ac72f16a35a4f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="d7ff7-103">Desenvolver programas Java MapReduce para Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7ff7-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="d7ff7-104">Saiba como usar o Apache Maven para criar um aplicativo de MapReduce baseado em Java e, em seguida, execute-o com o Hadoop no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-104">Learn how to use Apache Maven to create a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="d7ff7-105">Este exemplo foi testado mais recentemente no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="d7ff7-106"><a name="prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d7ff7-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="d7ff7-107">O [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 ou posterior (ou um equivalente, como OpenJDK).</span><span class="sxs-lookup"><span data-stu-id="d7ff7-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="d7ff7-108">O HDInsight nas versões 3.4 e anteriores usam Java 7.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="d7ff7-109">HDInsight 3.5 e posterior usa Java 8.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="d7ff7-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="d7ff7-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="d7ff7-111">Configurar o ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="d7ff7-111">Configure development environment</span></span>

<span data-ttu-id="d7ff7-112">As seguintes variáveis de ambiente podem ser definidas quando você instala o Java e o JDK.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-112">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="d7ff7-113">No entanto, você deve verificar se elas existem e se contêm os valores corretos para o seu sistema.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-113">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="d7ff7-114">`JAVA_HOME` – deve apontar para o diretório no qual o JRE (Java Runtime Environment) está instalado.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-114">`JAVA_HOME` - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="d7ff7-115">Por exemplo, em um sistema OS X, Unix ou Linux, ele deve ter um valor semelhante a `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-115">For example, on an OS X, Unix or Linux system, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="d7ff7-116">No Windows, ele teria um valor semelhante a `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="d7ff7-116">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="d7ff7-117">`PATH` – deve conter os seguintes caminhos:</span><span class="sxs-lookup"><span data-stu-id="d7ff7-117">`PATH` - should contain the following paths:</span></span>
  
  * <span data-ttu-id="d7ff7-118">`JAVA_HOME` (ou o caminho equivalente)</span><span class="sxs-lookup"><span data-stu-id="d7ff7-118">`JAVA_HOME` (or the equivalent path)</span></span>

  * <span data-ttu-id="d7ff7-119">`JAVA_HOME\bin` (ou o caminho equivalente)</span><span class="sxs-lookup"><span data-stu-id="d7ff7-119">`JAVA_HOME\bin` (or the equivalent path)</span></span>

  * <span data-ttu-id="d7ff7-120">O diretório onde o Maven está instalado</span><span class="sxs-lookup"><span data-stu-id="d7ff7-120">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="d7ff7-121">Criar um projeto Maven</span><span class="sxs-lookup"><span data-stu-id="d7ff7-121">Create a Maven project</span></span>

1. <span data-ttu-id="d7ff7-122">Em uma sessão do terminal ou linha de comando em seu ambiente de desenvolvimento, mude os diretórios para o local em que você deseja armazenar o projeto.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-122">From a terminal session, or command line in your development environment, change directories to the location you want to store this project.</span></span>

2. <span data-ttu-id="d7ff7-123">Use o comando `mvn`, que é instalado com o Maven, para gerar o scaffolding para o projeto.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-123">Use the `mvn` command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="d7ff7-124">Se você estiver usando o PowerShell, coloque os parâmetros `-D` entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-124">If you are using PowerShell, you must enclose the `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="d7ff7-125">Esse comando cria um diretório com o nome especificado pelo parâmetro `artifactID` (**wordcountjava** neste exemplo). Esse diretório contém os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d7ff7-125">This command creates a directory with the name specified by the `artifactID` parameter (**wordcountjava** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="d7ff7-126">`pom.xml` – o [POM (Modelo de Objeto de Projeto)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) que contém informações e detalhes de configuração usados para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-126">`pom.xml` - The [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used to build the project.</span></span>

   * <span data-ttu-id="d7ff7-127">`src` – o diretório que contém o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-127">`src` - The directory that contains the application.</span></span>

3. <span data-ttu-id="d7ff7-128">Exclua arquivo o `src/test/java/org/apache/hadoop/examples/apptest.java`.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-128">Delete the `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="d7ff7-129">Ele não é usado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="d7ff7-130">Adicionar dependências</span><span class="sxs-lookup"><span data-stu-id="d7ff7-130">Add dependencies</span></span>

1. <span data-ttu-id="d7ff7-131">Edite o arquivo `pom.xml` e adicione o seguinte texto dentro da seção `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="d7ff7-131">Edit the `pom.xml` file and add the following text inside the `<dependencies>` section:</span></span>
   
   ```xml
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-examples</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-client-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
   ```

    <span data-ttu-id="d7ff7-132">Isso define as bibliotecas necessárias (listadas em &lt;artifactId\>) com uma versão específica (listada em &lt;version\>).</span><span class="sxs-lookup"><span data-stu-id="d7ff7-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="d7ff7-133">Em tempo de compilação, essa dependência será baixada do repositório padrão do Maven.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-133">At compile time, these dependencies are downloaded from the default Maven repository.</span></span> <span data-ttu-id="d7ff7-134">Você pode usar a [pesquisa de repositório do Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) para exibir mais informações.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-134">You can use the [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) to view more.</span></span>
   
    <span data-ttu-id="d7ff7-135">O `<scope>provided</scope>` informa o Maven que essas dependências não devem ser empacotadas com o aplicativo, pois são fornecidas pelo cluster do HDInsight em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-135">The `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with the application, as they are provided by the HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d7ff7-136">A versão usada deve corresponder à versão do Hadoop no cluster.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-136">The version used should match the version of Hadoop present on your cluster.</span></span> <span data-ttu-id="d7ff7-137">Para obter mais informações sobre versões, consulte o documento [Versão do componente HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="d7ff7-137">For more information on versions, see the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="d7ff7-138">Adicione o seguinte ao arquivo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-138">Add the following to the `pom.xml` file.</span></span> <span data-ttu-id="d7ff7-139">Esse texto deve estar dentro das marcas `<project>...</project>` no arquivo, por exemplo, entre `</dependencies>` e `</project>`.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-139">This text must be inside the `<project>...</project>` tags in the file; for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
            </configuration>
            <executions>
            <execution>
                <phase>package</phase>
                    <goals>
                    <goal>shade</goal>
                    </goals>
            </execution>
            </executions>
            </plugin>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.1</version>
            <configuration>
            <source>1.8</source>
            <target>1.8</target>
            </configuration>
        </plugin>
        </plugins>
    </build>
   ```

    <span data-ttu-id="d7ff7-140">O primeiro plug-in configura o [Plug-in Maven Shade](http://maven.apache.org/plugins/maven-shade-plugin/), que é usado para criar um uberjar (às vezes chamado de fatjar), que contém as dependências exigidas pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-140">The first plugin configures the [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used to build an uberjar (sometimes called a fatjar), which contains dependencies required by the application.</span></span> <span data-ttu-id="d7ff7-141">Ele também evita a duplicação de licenças no pacote jar, que pode causar problemas em alguns sistemas.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-141">It also prevents duplication of licenses within the jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="d7ff7-142">O segundo plug-in configura a versão de Java de destino.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-142">The second plugin configures the target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d7ff7-143">O HDInsight 3.4 e anteriores usam o Java 7.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="d7ff7-144">HDInsight 3.5 e posterior usa Java 8.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="d7ff7-145">Salve o arquivo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-145">Save the `pom.xml` file.</span></span>

## <a name="create-the-mapreduce-application"></a><span data-ttu-id="d7ff7-146">Criar o aplicativo MapReduce</span><span class="sxs-lookup"><span data-stu-id="d7ff7-146">Create the MapReduce application</span></span>

1. <span data-ttu-id="d7ff7-147">Vá para o diretório `wordcountjava/src/main/java/org/apache/hadoop/examples` e renomeie o arquivo `App.java` para `WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-147">Go to the `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename the `App.java` file to `WordCount.java`.</span></span>

2. <span data-ttu-id="d7ff7-148">Abra o arquivo `WordCount.java` em um editor de texto e substitua o conteúdo pelo seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="d7ff7-148">Open the `WordCount.java` file in a text editor and replace the contents with the following text:</span></span>
   
    ```java
    package org.apache.hadoop.examples;

    import java.io.IOException;
    import java.util.StringTokenizer;
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.fs.Path;
    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Job;
    import org.apache.hadoop.mapreduce.Mapper;
    import org.apache.hadoop.mapreduce.Reducer;
    import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
    import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class WordCount {

        public static class TokenizerMapper
            extends Mapper<Object, Text, Text, IntWritable>{

        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context
                        ) throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
            word.set(itr.nextToken());
            context.write(word, one);
            }
        }
    }

    public static class IntSumReducer
            extends Reducer<Text,IntWritable,Text,IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values,
                            Context context
                            ) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
            sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
        if (otherArgs.length != 2) {
            System.err.println("Usage: wordcount <in> <out>");
            System.exit(2);
        }
        Job job = new Job(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
        FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
        }
    }
    ```
   
    <span data-ttu-id="d7ff7-149">Observe que o nome do pacote é `org.apache.hadoop.examples` e o nome de classe é `WordCount`.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-149">Notice the package name is `org.apache.hadoop.examples` and the class name is `WordCount`.</span></span> <span data-ttu-id="d7ff7-150">Você usará esses nomes quando enviar o trabalho MapReduce.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-150">You use these names when you submit the MapReduce job.</span></span>

3. <span data-ttu-id="d7ff7-151">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-151">Save the file.</span></span>

## <a name="build-the-application"></a><span data-ttu-id="d7ff7-152">Compilar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="d7ff7-152">Build the application</span></span>

1. <span data-ttu-id="d7ff7-153">Altere para o diretório `wordcountjava` se ainda não estiver lá.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-153">Change to the `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="d7ff7-154">Use o comando a seguir para compilar um arquivo JAR contendo o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="d7ff7-154">Use the following command to build a JAR file containing the application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="d7ff7-155">Esse comando limpa quaisquer artefatos de criação anteriores, baixa quaisquer dependências que ainda não foram instaladas e, então, compila o aplicativo e cria seu pacote.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package the application.</span></span>

3. <span data-ttu-id="d7ff7-156">Quando o comando é concluído, o diretório `wordcountjava/target` contém um arquivo chamado `wordcountjava-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-156">Once the command finishes, the `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d7ff7-157">O arquivo `wordcountjava-1.0-SNAPSHOT.jar` é um uberjar, que contém não apenas o trabalho WordCount, mas também as dependências necessárias para o trabalho em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-157">The `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only the WordCount job, but also dependencies that the job requires at runtime.</span></span>

## <span data-ttu-id="d7ff7-158"><a id="upload"></a>Carregar o jar</span><span class="sxs-lookup"><span data-stu-id="d7ff7-158"><a id="upload"></a>Upload the jar</span></span>

<span data-ttu-id="d7ff7-159">Use o comando a seguir para carregar o arquivo jar para o nó do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d7ff7-159">Use the following command to upload the jar file to the HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for the cluster. Replace __CLUSTERNAME__ with the HDInsight cluster name.

<span data-ttu-id="d7ff7-160">Esse comando copia os arquivos do sistema local para o nó principal.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-160">This command copies the files from the local system to the head node.</span></span> <span data-ttu-id="d7ff7-161">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d7ff7-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="d7ff7-162"><a name="run"></a>Para executar o trabalho MapReduce no Hadoop</span><span class="sxs-lookup"><span data-stu-id="d7ff7-162"><a name="run"></a>Run the MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="d7ff7-163">Conecte-se ao HDInsight usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-163">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="d7ff7-164">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d7ff7-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d7ff7-165">Na sessão do SSH, use o seguinte comando para executar o aplicativo MapReduce:</span><span class="sxs-lookup"><span data-stu-id="d7ff7-165">From the SSH session, use the following command to run the MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="d7ff7-166">Esse comando inicia o aplicativo WordCount MapReduce.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-166">This command starts the WordCount MapReduce application.</span></span> <span data-ttu-id="d7ff7-167">O arquivo de entrada é `/example/data/gutenberg/davinci.txt`, e o diretório de saída é `/example/data/wordcountout`.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-167">The input file is `/example/data/gutenberg/davinci.txt`, and the output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="d7ff7-168">Os arquivos de entrada e saída são armazenados no armazenamento padrão do cluster.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-168">Both the input file and output are stored to the default storage for the cluster.</span></span>

3. <span data-ttu-id="d7ff7-169">Quando o trabalho for concluído, use o seguinte comando para exibir os resultados:</span><span class="sxs-lookup"><span data-stu-id="d7ff7-169">Once the job completes, use the following command to view the results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="d7ff7-170">Você deverá receber uma lista de palavras e contagens, com valores semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="d7ff7-170">You should receive a list of words and counts, with values similar to the following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="d7ff7-171"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d7ff7-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="d7ff7-172">Neste documento, você aprendeu a desenvolver um trabalho MapReduce em Java.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-172">In this document, you have learned how to develop a Java MapReduce job.</span></span> <span data-ttu-id="d7ff7-173">Consulte os seguintes documentos para ver outras maneiras de trabalhar com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d7ff7-173">See the following documents for other ways to work with HDInsight.</span></span>

* <span data-ttu-id="d7ff7-174">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="d7ff7-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="d7ff7-175">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="d7ff7-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="d7ff7-176">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7ff7-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="d7ff7-177">Para obter mais informações, consulte também o [Centro de desenvolvedores do Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="d7ff7-177">For more information, see also the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[powershell-PSCredential]: http://social.technet.microsoft.com/wiki/contents/articles/4546.working-with-passwords-secure-strings-and-credentials-in-windows-powershell.aspx

