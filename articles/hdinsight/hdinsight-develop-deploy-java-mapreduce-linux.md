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
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a>Desenvolver programas Java MapReduce para Hadoop no HDInsight

Saiba como toouse aplicativo de MapReduce do Apache Maven toocreate um baseados em Java, em seguida, executá-lo com Hadoop no HDInsight do Azure.

> [!NOTE]
> Este exemplo foi testado mais recentemente no HDInsight 3.6.

## <a name="prerequisites"></a>Pré-requisitos

* O [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 ou posterior (ou um equivalente, como OpenJDK).
    
    > [!NOTE]
    > O HDInsight nas versões 3.4 e anteriores usam Java 7. HDInsight 3.5 e posterior usa Java 8.

* [Apache Maven](http://maven.apache.org/)

## <a name="configure-development-environment"></a>Configurar o ambiente de desenvolvimento

Olá seguintes variáveis de ambiente podem ser definidas quando você instala o Java e hello JDK. No entanto, você deve verificar se eles existem e que eles contêm valores de saudação corretos para seu sistema.

* `JAVA_HOME`-deve apontar toohello diretório onde Olá o Java runtime environment (JRE) está instalado. Por exemplo, em um sistema OS X, Unix ou Linux, ele deve ter um valor semelhante muito`/usr/lib/jvm/java-7-oracle`. No Windows, ele deve ter um valor semelhante muito`c:\Program Files (x86)\Java\jre1.7`

* `PATH`-deve conter Olá caminhos a seguir:
  
  * `JAVA_HOME`(ou caminho equivalente Olá)

  * `JAVA_HOME\bin`(ou caminho equivalente Olá)

  * diretório de saudação onde Maven está instalado

## <a name="create-a-maven-project"></a>Criar um projeto Maven

1. Uma sessão de terminal, ou a linha de comando no ambiente de desenvolvimento, altere diretórios toohello local toostore este projeto.

2. Saudação de uso `mvn` comando, que é instalado com o Maven, Olá toogenerate estrutura do projeto de saudação.

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > Se você estiver usando o PowerShell, você deverá colocar Olá `-D` parâmetros entre aspas duplas.
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Este comando cria um diretório com o nome de saudação especificado pelo Olá `artifactID` parâmetro (**wordcountjava** neste exemplo.) Este diretório contém Olá itens a seguir:

   * `pom.xml`-Olá [modelo de objeto do projeto (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) que contém informações e detalhes de configuração usados toobuild projeto de saudação.

   * `src`-diretório Olá que contém o aplicativo hello.

3. Excluir Olá `src/test/java/org/apache/hadoop/examples/apptest.java` arquivo. Ele não é usado neste exemplo.

## <a name="add-dependencies"></a>Adicionar dependências

1. Editar saudação `pom.xml` de arquivos e adicionar Olá depois do texto dentro de saudação `<dependencies>` seção:
   
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

    Isso define as bibliotecas necessárias (listadas em &lt;artifactId\>) com uma versão específica (listada em &lt;version\>). Em tempo de compilação, essas dependências são baixadas do repositório de Maven saudação padrão. Você pode usar o hello [pesquisa de Repositório Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview mais.
   
    Olá `<scope>provided</scope>` informa Maven que essas dependências não devem ser empacotadas com o aplicativo hello, conforme elas são fornecidas pelo cluster do HDInsight Olá em tempo de execução.

    > [!IMPORTANT]
    > versão Olá usada deve corresponder a versão de saudação do Hadoop presente no cluster. Para obter mais informações sobre versões, consulte Olá [o controle de versão do HDInsight componente](hdinsight-component-versioning.md) documento.

2. Adicionar Olá após toohello `pom.xml` arquivo. Esse texto deve estar dentro de saudação `<project>...</project>` no arquivo hello; por exemplo, entre as marcas `</dependencies>` e `</project>`.

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

    plug-in do primeiro Hello configura Olá [plug-in de sombra Maven](http://maven.apache.org/plugins/maven-shade-plugin/), que é usado toobuild um uberjar (às vezes chamado de um fatjar), que contém as dependências exigidas pelo aplicativo hello. Isso também impedirá a eliminação de duplicação de licenças no pacote de jar hello, que pode causar problemas em alguns sistemas.

    plug-in do segundo Olá configura a versão do Java de destino de saudação.

    > [!NOTE]
    > O HDInsight 3.4 e anteriores usam o Java 7. HDInsight 3.5 e posterior usa Java 8.

3. Salvar Olá `pom.xml` arquivo.

## <a name="create-hello-mapreduce-application"></a>Criar aplicativo de MapReduce hello

1. Vá toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` diretório e renomear Olá `App.java` arquivo muito`WordCount.java`.

2. Olá abrir `WordCount.java` do arquivo em um editor de texto e substitua o conteúdo de saudação com hello texto a seguir:
   
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
   
    Nome do pacote de saudação de aviso é `org.apache.hadoop.examples` e o nome da classe Olá é `WordCount`. Use esses nomes ao enviar o trabalho de MapReduce Olá.

3. Salve o arquivo hello.

## <a name="build-hello-application"></a>Criar um aplicativo hello

1. Alterar toohello `wordcountjava` directory, se você não ainda estiver lá.

2. Use Olá toobuild um JAR que contém aplicativos de saudação do arquivo de comando a seguir:

   ```
   mvn clean package
   ```

    Este comando limpa qualquer artefatos de compilação anterior, downloads de quaisquer dependências que ainda não tiver sido instaladas, e, em seguida, compilações e aplicativo hello de pacote.

3. Depois que o comando Olá concluído, hello `wordcountjava/target` diretório contém um arquivo chamado `wordcountjava-1.0-SNAPSHOT.jar`.
   
   > [!NOTE]
   > Olá `wordcountjava-1.0-SNAPSHOT.jar` arquivo é um uberjar, que contém o trabalho de WordCount Olá não apenas, mas também requer que as dependências de Olá trabalho em tempo de execução.

## <a id="upload"></a>Carregar jar Olá

Use Olá comando tooupload Olá jar arquivo toohello HDInsight um nó principal a seguir:

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

Este comando copia os arquivos de saudação do nó principal do toohello Olá sistema local. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="run"></a>Executar trabalho de MapReduce Olá no Hadoop

1. Conecte-se tooHDInsight usando o SSH. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Da sessão SSH hello, use Olá aplicativo MapReduce do comando toorun hello a seguir:
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    Esse comando inicia Olá aplicativo WordCount MapReduce. arquivo de entrada Hello está `/example/data/gutenberg/davinci.txt`, e o diretório de saída de hello `/example/data/wordcountout`. Arquivo de entrada hello e saída são toohello armazenado um armazenamento padrão para o cluster de saudação.

3. Após a conclusão do trabalho hello, use Olá resultados do comando tooview Olá a seguir:
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    Você deve receber uma lista de palavras e as contagens, com valores toohello semelhante texto a seguir:
   
        zeal    1
        zelus   1
        zenith  2

## <a id="nextsteps"></a>Próximas etapas

Neste documento, você aprendeu como toodevelop um trabalho de MapReduce Java. Consulte Olá documentos para toowork outras formas ao HDInsight a seguir.

* [Usar o Hive com o HDInsight][hdinsight-use-hive]
* [Usar o Pig com o HDInsight][hdinsight-use-pig]
* [Usar o MapReduce com o HDInsight](hdinsight-use-mapreduce.md)

Para obter mais informações, consulte também Olá [Central de desenvolvedores de Java](https://azure.microsoft.com/develop/java/).

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

