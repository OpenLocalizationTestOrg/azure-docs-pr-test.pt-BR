---
title: aaaCreate MapReduce Java para Hadoop - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse aplicativo de MapReduce do Apache Maven toocreate um baseados em Java, em seguida, executá-lo com Hadoop no HDInsight do Azure."
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
ms.openlocfilehash: 903a57a482395f7da79002188399a4d6288ff0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="d9061-103">Desenvolver programas Java MapReduce para Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9061-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="d9061-104">Saiba como toouse aplicativo de MapReduce do Apache Maven toocreate um baseados em Java, em seguida, executá-lo com Hadoop no HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9061-104">Learn how toouse Apache Maven toocreate a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="d9061-105">Este exemplo foi testado mais recentemente no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="d9061-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="d9061-106"><a name="prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d9061-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="d9061-107">O [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 ou posterior (ou um equivalente, como OpenJDK).</span><span class="sxs-lookup"><span data-stu-id="d9061-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="d9061-108">O HDInsight nas versões 3.4 e anteriores usam Java 7.</span><span class="sxs-lookup"><span data-stu-id="d9061-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="d9061-109">HDInsight 3.5 e posterior usa Java 8.</span><span class="sxs-lookup"><span data-stu-id="d9061-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="d9061-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="d9061-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="d9061-111">Configurar o ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="d9061-111">Configure development environment</span></span>

<span data-ttu-id="d9061-112">Olá seguintes variáveis de ambiente podem ser definidas quando você instala o Java e hello JDK.</span><span class="sxs-lookup"><span data-stu-id="d9061-112">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="d9061-113">No entanto, você deve verificar se eles existem e que eles contêm valores de saudação corretos para seu sistema.</span><span class="sxs-lookup"><span data-stu-id="d9061-113">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="d9061-114">`JAVA_HOME`-deve apontar toohello diretório onde Olá o Java runtime environment (JRE) está instalado.</span><span class="sxs-lookup"><span data-stu-id="d9061-114">`JAVA_HOME` - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="d9061-115">Por exemplo, em um sistema OS X, Unix ou Linux, ele deve ter um valor semelhante muito`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="d9061-115">For example, on an OS X, Unix or Linux system, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="d9061-116">No Windows, ele deve ter um valor semelhante muito`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="d9061-116">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="d9061-117">`PATH`-deve conter Olá caminhos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9061-117">`PATH` - should contain hello following paths:</span></span>
  
  * <span data-ttu-id="d9061-118">`JAVA_HOME`(ou caminho equivalente Olá)</span><span class="sxs-lookup"><span data-stu-id="d9061-118">`JAVA_HOME` (or hello equivalent path)</span></span>

  * <span data-ttu-id="d9061-119">`JAVA_HOME\bin`(ou caminho equivalente Olá)</span><span class="sxs-lookup"><span data-stu-id="d9061-119">`JAVA_HOME\bin` (or hello equivalent path)</span></span>

  * <span data-ttu-id="d9061-120">diretório de saudação onde Maven está instalado</span><span class="sxs-lookup"><span data-stu-id="d9061-120">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="d9061-121">Criar um projeto Maven</span><span class="sxs-lookup"><span data-stu-id="d9061-121">Create a Maven project</span></span>

1. <span data-ttu-id="d9061-122">Uma sessão de terminal, ou a linha de comando no ambiente de desenvolvimento, altere diretórios toohello local toostore este projeto.</span><span class="sxs-lookup"><span data-stu-id="d9061-122">From a terminal session, or command line in your development environment, change directories toohello location you want toostore this project.</span></span>

2. <span data-ttu-id="d9061-123">Saudação de uso `mvn` comando, que é instalado com o Maven, Olá toogenerate estrutura do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9061-123">Use hello `mvn` command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="d9061-124">Se você estiver usando o PowerShell, você deverá colocar Olá `-D` parâmetros entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="d9061-124">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="d9061-125">Este comando cria um diretório com o nome de saudação especificado pelo Olá `artifactID` parâmetro (**wordcountjava** neste exemplo.) Este diretório contém Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9061-125">This command creates a directory with hello name specified by hello `artifactID` parameter (**wordcountjava** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="d9061-126">`pom.xml`-Olá [modelo de objeto do projeto (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) que contém informações e detalhes de configuração usados toobuild projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9061-126">`pom.xml` - hello [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used toobuild hello project.</span></span>

   * <span data-ttu-id="d9061-127">`src`-diretório Olá que contém o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d9061-127">`src` - hello directory that contains hello application.</span></span>

3. <span data-ttu-id="d9061-128">Excluir Olá `src/test/java/org/apache/hadoop/examples/apptest.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="d9061-128">Delete hello `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="d9061-129">Ele não é usado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="d9061-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="d9061-130">Adicionar dependências</span><span class="sxs-lookup"><span data-stu-id="d9061-130">Add dependencies</span></span>

1. <span data-ttu-id="d9061-131">Editar saudação `pom.xml` de arquivos e adicionar Olá depois do texto dentro de saudação `<dependencies>` seção:</span><span class="sxs-lookup"><span data-stu-id="d9061-131">Edit hello `pom.xml` file and add hello following text inside hello `<dependencies>` section:</span></span>
   
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

    <span data-ttu-id="d9061-132">Isso define as bibliotecas necessárias (listadas em &lt;artifactId\>) com uma versão específica (listada em &lt;version\>).</span><span class="sxs-lookup"><span data-stu-id="d9061-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="d9061-133">Em tempo de compilação, essas dependências são baixadas do repositório de Maven saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="d9061-133">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="d9061-134">Você pode usar o hello [pesquisa de Repositório Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview mais.</span><span class="sxs-lookup"><span data-stu-id="d9061-134">You can use hello [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview more.</span></span>
   
    <span data-ttu-id="d9061-135">Olá `<scope>provided</scope>` informa Maven que essas dependências não devem ser empacotadas com o aplicativo hello, conforme elas são fornecidas pelo cluster do HDInsight Olá em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="d9061-135">hello `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with hello application, as they are provided by hello HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d9061-136">versão Olá usada deve corresponder a versão de saudação do Hadoop presente no cluster.</span><span class="sxs-lookup"><span data-stu-id="d9061-136">hello version used should match hello version of Hadoop present on your cluster.</span></span> <span data-ttu-id="d9061-137">Para obter mais informações sobre versões, consulte Olá [o controle de versão do HDInsight componente](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="d9061-137">For more information on versions, see hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="d9061-138">Adicionar Olá após toohello `pom.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="d9061-138">Add hello following toohello `pom.xml` file.</span></span> <span data-ttu-id="d9061-139">Esse texto deve estar dentro de saudação `<project>...</project>` no arquivo hello; por exemplo, entre as marcas `</dependencies>` e `</project>`.</span><span class="sxs-lookup"><span data-stu-id="d9061-139">This text must be inside hello `<project>...</project>` tags in hello file; for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="d9061-140">plug-in do primeiro Hello configura Olá [plug-in de sombra Maven](http://maven.apache.org/plugins/maven-shade-plugin/), que é usado toobuild um uberjar (às vezes chamado de um fatjar), que contém as dependências exigidas pelo aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d9061-140">hello first plugin configures hello [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used toobuild an uberjar (sometimes called a fatjar), which contains dependencies required by hello application.</span></span> <span data-ttu-id="d9061-141">Isso também impedirá a eliminação de duplicação de licenças no pacote de jar hello, que pode causar problemas em alguns sistemas.</span><span class="sxs-lookup"><span data-stu-id="d9061-141">It also prevents duplication of licenses within hello jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="d9061-142">plug-in do segundo Olá configura a versão do Java de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9061-142">hello second plugin configures hello target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9061-143">O HDInsight 3.4 e anteriores usam o Java 7.</span><span class="sxs-lookup"><span data-stu-id="d9061-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="d9061-144">HDInsight 3.5 e posterior usa Java 8.</span><span class="sxs-lookup"><span data-stu-id="d9061-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="d9061-145">Salvar Olá `pom.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="d9061-145">Save hello `pom.xml` file.</span></span>

## <a name="create-hello-mapreduce-application"></a><span data-ttu-id="d9061-146">Criar aplicativo de MapReduce hello</span><span class="sxs-lookup"><span data-stu-id="d9061-146">Create hello MapReduce application</span></span>

1. <span data-ttu-id="d9061-147">Vá toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` diretório e renomear Olá `App.java` arquivo muito`WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="d9061-147">Go toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename hello `App.java` file too`WordCount.java`.</span></span>

2. <span data-ttu-id="d9061-148">Olá abrir `WordCount.java` do arquivo em um editor de texto e substitua o conteúdo de saudação com hello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9061-148">Open hello `WordCount.java` file in a text editor and replace hello contents with hello following text:</span></span>
   
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
   
    <span data-ttu-id="d9061-149">Nome do pacote de saudação de aviso é `org.apache.hadoop.examples` e o nome da classe Olá é `WordCount`.</span><span class="sxs-lookup"><span data-stu-id="d9061-149">Notice hello package name is `org.apache.hadoop.examples` and hello class name is `WordCount`.</span></span> <span data-ttu-id="d9061-150">Use esses nomes ao enviar o trabalho de MapReduce Olá.</span><span class="sxs-lookup"><span data-stu-id="d9061-150">You use these names when you submit hello MapReduce job.</span></span>

3. <span data-ttu-id="d9061-151">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="d9061-151">Save hello file.</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="d9061-152">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d9061-152">Build hello application</span></span>

1. <span data-ttu-id="d9061-153">Alterar toohello `wordcountjava` directory, se você não ainda estiver lá.</span><span class="sxs-lookup"><span data-stu-id="d9061-153">Change toohello `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="d9061-154">Use Olá toobuild um JAR que contém aplicativos de saudação do arquivo de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9061-154">Use hello following command toobuild a JAR file containing hello application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="d9061-155">Este comando limpa qualquer artefatos de compilação anterior, downloads de quaisquer dependências que ainda não tiver sido instaladas, e, em seguida, compilações e aplicativo hello de pacote.</span><span class="sxs-lookup"><span data-stu-id="d9061-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package hello application.</span></span>

3. <span data-ttu-id="d9061-156">Depois que o comando Olá concluído, hello `wordcountjava/target` diretório contém um arquivo chamado `wordcountjava-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="d9061-156">Once hello command finishes, hello `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d9061-157">Olá `wordcountjava-1.0-SNAPSHOT.jar` arquivo é um uberjar, que contém o trabalho de WordCount Olá não apenas, mas também requer que as dependências de Olá trabalho em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="d9061-157">hello `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only hello WordCount job, but also dependencies that hello job requires at runtime.</span></span>

## <span data-ttu-id="d9061-158"><a id="upload"></a>Carregar jar Olá</span><span class="sxs-lookup"><span data-stu-id="d9061-158"><a id="upload"></a>Upload hello jar</span></span>

<span data-ttu-id="d9061-159">Use Olá comando tooupload Olá jar arquivo toohello HDInsight um nó principal a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9061-159">Use hello following command tooupload hello jar file toohello HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

<span data-ttu-id="d9061-160">Este comando copia os arquivos de saudação do nó principal do toohello Olá sistema local.</span><span class="sxs-lookup"><span data-stu-id="d9061-160">This command copies hello files from hello local system toohello head node.</span></span> <span data-ttu-id="d9061-161">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d9061-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="d9061-162"><a name="run"></a>Executar trabalho de MapReduce Olá no Hadoop</span><span class="sxs-lookup"><span data-stu-id="d9061-162"><a name="run"></a>Run hello MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="d9061-163">Conecte-se tooHDInsight usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="d9061-163">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="d9061-164">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d9061-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d9061-165">Da sessão SSH hello, use Olá aplicativo MapReduce do comando toorun hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9061-165">From hello SSH session, use hello following command toorun hello MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="d9061-166">Esse comando inicia Olá aplicativo WordCount MapReduce.</span><span class="sxs-lookup"><span data-stu-id="d9061-166">This command starts hello WordCount MapReduce application.</span></span> <span data-ttu-id="d9061-167">arquivo de entrada Hello está `/example/data/gutenberg/davinci.txt`, e o diretório de saída de hello `/example/data/wordcountout`.</span><span class="sxs-lookup"><span data-stu-id="d9061-167">hello input file is `/example/data/gutenberg/davinci.txt`, and hello output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="d9061-168">Arquivo de entrada hello e saída são toohello armazenado um armazenamento padrão para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9061-168">Both hello input file and output are stored toohello default storage for hello cluster.</span></span>

3. <span data-ttu-id="d9061-169">Após a conclusão do trabalho hello, use Olá resultados do comando tooview Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9061-169">Once hello job completes, use hello following command tooview hello results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="d9061-170">Você deve receber uma lista de palavras e as contagens, com valores toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9061-170">You should receive a list of words and counts, with values similar toohello following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="d9061-171"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9061-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="d9061-172">Neste documento, você aprendeu como toodevelop um trabalho de MapReduce Java.</span><span class="sxs-lookup"><span data-stu-id="d9061-172">In this document, you have learned how toodevelop a Java MapReduce job.</span></span> <span data-ttu-id="d9061-173">Consulte Olá documentos para toowork outras formas ao HDInsight a seguir.</span><span class="sxs-lookup"><span data-stu-id="d9061-173">See hello following documents for other ways toowork with HDInsight.</span></span>

* <span data-ttu-id="d9061-174">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="d9061-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="d9061-175">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="d9061-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="d9061-176">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9061-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="d9061-177">Para obter mais informações, consulte também Olá [Central de desenvolvedores de Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="d9061-177">For more information, see also hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

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

