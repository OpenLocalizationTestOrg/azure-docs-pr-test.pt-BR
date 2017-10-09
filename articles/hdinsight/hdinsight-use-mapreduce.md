---
title: aaaMapReduce com Hadoop no HDInsight | Microsoft Docs
description: Saiba como toorun MapReduce trabalhos no Hadoop em clusters de HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f321501-d62c-4ffc-b5d6-102ecba6dd76
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0cf7ad0e6769e678be64f9e4ec8ed7a214ab7af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a>Usar o MapReduce no Hadoop do HDInsight

Saiba como toorun MapReduce trabalhos em clusters de HDInsight. Use Olá Olá toodiscover de tabela que MapReduce pode ser usado com HDInsight de várias maneiras a seguir:

| **Use isto**... | **... .toodo isso** | ... com esse **sistema operacional de cluster** | ... desse **sistema operacional cliente** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Use Olá Hadoop comando por meio de **SSH** |Linux |Linux, Unix, Mac OS X ou Windows |
| [REST](hdinsight-hadoop-use-mapreduce-curl.md) |Enviar trabalho Olá remotamente usando **REST** (exemplos usam ondulação) |Linux ou Windows |Linux, Unix, Mac OS X ou Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Enviar trabalho Olá remotamente usando **do Windows PowerShell** |Linux ou Windows |Windows |
| [Área de Trabalho Remota](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 e 3.3) |Use Olá Hadoop comando por meio de **área de trabalho remota** |Windows |Windows |

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="whatis"></a>O que é o MapReduce

O MapReduce do Hadoop é uma estrutura de software para escrever trabalhos que processam grandes quantidades de dados. Dados de entrada são divididos em partes independentes, que, em seguida, são processados em paralelo em nós de saudação do cluster. Um trabalho do MapReduce consiste em duas funções:

* **Mapeador**: consome dados de entrada, analisa-os (normalmente com operações de classificação e filtro) e emite tuplas (pares chave-valor)

* **Redutor**: consome tuplas emitidas pelo mapeador de saudação e executa uma operação de resumida que cria um resultado menor, combinado de saudação dados mapeador

Olá diagrama a seguir ilustra um exemplo de trabalho MapReduce básica contagem:

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

saída de Hello desse trabalho é uma contagem do número de vezes que cada palavra ocorreu em texto de saudação que foi analisado.

* Mapeador de saudação entra em cada linha do texto de entrada hello como uma entrada e a divide em palavras. Emite uma chave/valor par sempre que ocorre uma palavra de palavra hello é seguido por um 1. Olá saída é classificada antes de enviá-la tooreducer.
* Redutor Olá soma essas contagens individuais para cada palavra e emite um par chave/valor único que contém a palavra hello seguida de soma de saudação de suas ocorrências.

O MapReduce pode ser implementado em várias linguagens. Java é a implementação mais comum de saudação e é usado para fins de demonstração neste documento.

## <a name="development-languages"></a>Linguagens de desenvolvimento

Idiomas ou estruturas que são baseadas em Java e Olá a máquina Virtual Java pode ser executado diretamente como um trabalho de MapReduce. exemplo Hello usado neste documento é um aplicativo Java MapReduce. Linguagens não Java, como C#, Python ou executáveis autônomos, devem usar o streaming do Hadoop.

Transmissão do Hadoop se comunica com hello mapeador e Redutor em STDIN e STDOUT. Redutor mapeador Olá ler dados de uma linha em vez de STDIN e gravar Olá tooSTDOUT de saída. Cada linha de leitura ou emitido por Redutor e mapeador Olá deve estar no formato de saudação de um par chave/valor, delimitado por um caractere de tabulação:

    [key]/t[value]

Para saber mais, confira [Streaming do Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).

Para obter exemplos do uso de Hadoop streaming com HDInsight, consulte Olá documentos a seguir:

* [Desenvolver trabalhos do MapReduce em C#](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Desenvolver trabalhos do MapReduce Python](hdinsight-hadoop-streaming-python.md)

## <a id="data"></a>Dados de exemplo

HDInsight fornece vários conjuntos de dados de exemplo, que são armazenados em Olá `/example/data` e `/HdiSamples` directory. São esses diretórios no armazenamento padrão da saudação para seu cluster. Neste documento, usamos Olá `/example/data/gutenberg/davinci.txt` arquivo. Este arquivo contém blocos de anotações de Leonardo Da Vinci hello.

## <a id="job"></a>MapReduce de exemplo

Um exemplo de aplicativo de contagem de palavras do MapReduce está incluído no seu cluster HDInsight. Este exemplo está localizado em `/example/jars/hadoop-mapreduce-examples.jar` no armazenamento padrão da saudação para seu cluster.

Olá código Java a seguir é a origem Olá Olá MapReduce aplicativos contidos no hello `hadoop-mapreduce-examples.jar` arquivo:

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

Para instruções toowrite seus próprios aplicativos de MapReduce, consulte Olá documentos a seguir:

* [Desenvolver aplicativos Java MapReduce para HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Desenvolver aplicativos Python MapReduce para HDInsight](hdinsight-hadoop-streaming-python.md)

## <a id="run"></a>Executar Olá MapReduce

O HDInsight pode executar trabalhos de HiveQL usando vários métodos. Usar o hello toodecide tabela qual método é ideal para você a seguir, siga o link Olá para obter uma explicação.

| **Use isto**... | **... .toodo isso** | ... com esse **sistema operacional de cluster** | ... desse **sistema operacional cliente** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Use Olá Hadoop comando por meio de **SSH** |Linux |Linux, Unix, Mac OS X ou Windows |
| [Curl](hdinsight-hadoop-use-mapreduce-curl.md) |Enviar trabalho Olá remotamente usando **REST** |Linux ou Windows |Linux, Unix, Mac OS X ou Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Enviar trabalho Olá remotamente usando **do Windows PowerShell** |Linux ou Windows |Windows |
| [Área de Trabalho Remota](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 e 3.3) |Use Olá Hadoop comando por meio de **área de trabalho remota** |Windows |Windows |

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="nextsteps"></a>Próximas etapas

toolearn mais sobre como trabalhar com dados no HDInsight, consulte Olá documentos a seguir:

* [Desenvolver programas Java MapReduce para HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Desenvolver programas MapReduce de streaming do Hadoop para o HDInsight](hdinsight-hadoop-streaming-python.md)

* [Desenvolver trabalhos de MapReduce do Scalding com o Apache Hadoop no HDInsight](hdinsight-hadoop-mapreduce-scalding.md)

* [Usar o Hive com o HDInsight][hdinsight-use-hive]

* [Usar o Pig com o HDInsight][hdinsight-use-pig]


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
