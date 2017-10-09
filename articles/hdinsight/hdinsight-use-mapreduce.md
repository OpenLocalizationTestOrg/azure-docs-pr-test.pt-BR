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
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="f9800-103">Usar o MapReduce no Hadoop do HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9800-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="f9800-104">Saiba como toorun MapReduce trabalhos em clusters de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f9800-104">Learn how toorun MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="f9800-105">Use Olá Olá toodiscover de tabela que MapReduce pode ser usado com HDInsight de várias maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9800-105">Use hello following table toodiscover hello various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="f9800-106">**Use isto**...</span><span class="sxs-lookup"><span data-stu-id="f9800-106">**Use this**...</span></span> | <span data-ttu-id="f9800-107">**... .toodo isso**</span><span class="sxs-lookup"><span data-stu-id="f9800-107">**...toodo this**</span></span> | <span data-ttu-id="f9800-108">... com esse **sistema operacional de cluster**</span><span class="sxs-lookup"><span data-stu-id="f9800-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="f9800-109">... desse **sistema operacional cliente**</span><span class="sxs-lookup"><span data-stu-id="f9800-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="f9800-110">SSH</span><span class="sxs-lookup"><span data-stu-id="f9800-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="f9800-111">Use Olá Hadoop comando por meio de **SSH**</span><span class="sxs-lookup"><span data-stu-id="f9800-111">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="f9800-112">Linux</span><span class="sxs-lookup"><span data-stu-id="f9800-112">Linux</span></span> |<span data-ttu-id="f9800-113">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="f9800-114">REST</span><span class="sxs-lookup"><span data-stu-id="f9800-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="f9800-115">Enviar trabalho Olá remotamente usando **REST** (exemplos usam ondulação)</span><span class="sxs-lookup"><span data-stu-id="f9800-115">Submit hello job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="f9800-116">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-116">Linux or Windows</span></span> |<span data-ttu-id="f9800-117">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="f9800-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9800-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="f9800-119">Enviar trabalho Olá remotamente usando **do Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="f9800-119">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="f9800-120">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-120">Linux or Windows</span></span> |<span data-ttu-id="f9800-121">Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-121">Windows</span></span> |
| <span data-ttu-id="f9800-122">[Área de Trabalho Remota](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="f9800-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="f9800-123">Use Olá Hadoop comando por meio de **área de trabalho remota**</span><span class="sxs-lookup"><span data-stu-id="f9800-123">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="f9800-124">Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-124">Windows</span></span> |<span data-ttu-id="f9800-125">Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f9800-126">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f9800-126">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f9800-127">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f9800-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="f9800-128"><a id="whatis"></a>O que é o MapReduce</span><span class="sxs-lookup"><span data-stu-id="f9800-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="f9800-129">O MapReduce do Hadoop é uma estrutura de software para escrever trabalhos que processam grandes quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="f9800-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="f9800-130">Dados de entrada são divididos em partes independentes, que, em seguida, são processados em paralelo em nós de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="f9800-130">Input data is split into independent chunks, which are then processed in parallel across hello nodes in your cluster.</span></span> <span data-ttu-id="f9800-131">Um trabalho do MapReduce consiste em duas funções:</span><span class="sxs-lookup"><span data-stu-id="f9800-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="f9800-132">**Mapeador**: consome dados de entrada, analisa-os (normalmente com operações de classificação e filtro) e emite tuplas (pares chave-valor)</span><span class="sxs-lookup"><span data-stu-id="f9800-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="f9800-133">**Redutor**: consome tuplas emitidas pelo mapeador de saudação e executa uma operação de resumida que cria um resultado menor, combinado de saudação dados mapeador</span><span class="sxs-lookup"><span data-stu-id="f9800-133">**Reducer**: Consumes tuples emitted by hello Mapper and performs a summary operation that creates a smaller, combined result from hello Mapper data</span></span>

<span data-ttu-id="f9800-134">Olá diagrama a seguir ilustra um exemplo de trabalho MapReduce básica contagem:</span><span class="sxs-lookup"><span data-stu-id="f9800-134">A basic word count MapReduce job example is illustrated in hello following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="f9800-136">saída de Hello desse trabalho é uma contagem do número de vezes que cada palavra ocorreu em texto de saudação que foi analisado.</span><span class="sxs-lookup"><span data-stu-id="f9800-136">hello output of this job is a count of how many times each word occurred in hello text that was analyzed.</span></span>

* <span data-ttu-id="f9800-137">Mapeador de saudação entra em cada linha do texto de entrada hello como uma entrada e a divide em palavras.</span><span class="sxs-lookup"><span data-stu-id="f9800-137">hello mapper takes each line from hello input text as an input and breaks it into words.</span></span> <span data-ttu-id="f9800-138">Emite uma chave/valor par sempre que ocorre uma palavra de palavra hello é seguido por um 1.</span><span class="sxs-lookup"><span data-stu-id="f9800-138">It emits a key/value pair each time a word occurs of hello word is followed by a 1.</span></span> <span data-ttu-id="f9800-139">Olá saída é classificada antes de enviá-la tooreducer.</span><span class="sxs-lookup"><span data-stu-id="f9800-139">hello output is sorted before sending it tooreducer.</span></span>
* <span data-ttu-id="f9800-140">Redutor Olá soma essas contagens individuais para cada palavra e emite um par chave/valor único que contém a palavra hello seguida de soma de saudação de suas ocorrências.</span><span class="sxs-lookup"><span data-stu-id="f9800-140">hello reducer sums these individual counts for each word and emits a single key/value pair that contains hello word followed by hello sum of its occurrences.</span></span>

<span data-ttu-id="f9800-141">O MapReduce pode ser implementado em várias linguagens.</span><span class="sxs-lookup"><span data-stu-id="f9800-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="f9800-142">Java é a implementação mais comum de saudação e é usado para fins de demonstração neste documento.</span><span class="sxs-lookup"><span data-stu-id="f9800-142">Java is hello most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="f9800-143">Linguagens de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="f9800-143">Development languages</span></span>

<span data-ttu-id="f9800-144">Idiomas ou estruturas que são baseadas em Java e Olá a máquina Virtual Java pode ser executado diretamente como um trabalho de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="f9800-144">Languages or frameworks that are based on Java and hello Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="f9800-145">exemplo Hello usado neste documento é um aplicativo Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="f9800-145">hello example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="f9800-146">Linguagens não Java, como C#, Python ou executáveis autônomos, devem usar o streaming do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f9800-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="f9800-147">Transmissão do Hadoop se comunica com hello mapeador e Redutor em STDIN e STDOUT.</span><span class="sxs-lookup"><span data-stu-id="f9800-147">Hadoop streaming communicates with hello mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="f9800-148">Redutor mapeador Olá ler dados de uma linha em vez de STDIN e gravar Olá tooSTDOUT de saída.</span><span class="sxs-lookup"><span data-stu-id="f9800-148">hello mapper and reducer read data a line at a time from STDIN, and write hello output tooSTDOUT.</span></span> <span data-ttu-id="f9800-149">Cada linha de leitura ou emitido por Redutor e mapeador Olá deve estar no formato de saudação de um par chave/valor, delimitado por um caractere de tabulação:</span><span class="sxs-lookup"><span data-stu-id="f9800-149">Each line read or emitted by hello mapper and reducer must be in hello format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="f9800-150">Para saber mais, confira [Streaming do Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="f9800-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="f9800-151">Para obter exemplos do uso de Hadoop streaming com HDInsight, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9800-151">For examples of using Hadoop streaming with HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="f9800-152">Desenvolver trabalhos do MapReduce em C#</span><span class="sxs-lookup"><span data-stu-id="f9800-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="f9800-153">Desenvolver trabalhos do MapReduce Python</span><span class="sxs-lookup"><span data-stu-id="f9800-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="f9800-154"><a id="data"></a>Dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="f9800-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="f9800-155">HDInsight fornece vários conjuntos de dados de exemplo, que são armazenados em Olá `/example/data` e `/HdiSamples` directory.</span><span class="sxs-lookup"><span data-stu-id="f9800-155">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="f9800-156">São esses diretórios no armazenamento padrão da saudação para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="f9800-156">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="f9800-157">Neste documento, usamos Olá `/example/data/gutenberg/davinci.txt` arquivo.</span><span class="sxs-lookup"><span data-stu-id="f9800-157">In this document, we use hello `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="f9800-158">Este arquivo contém blocos de anotações de Leonardo Da Vinci hello.</span><span class="sxs-lookup"><span data-stu-id="f9800-158">This file contains hello notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="f9800-159"><a id="job"></a>MapReduce de exemplo</span><span class="sxs-lookup"><span data-stu-id="f9800-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="f9800-160">Um exemplo de aplicativo de contagem de palavras do MapReduce está incluído no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f9800-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="f9800-161">Este exemplo está localizado em `/example/jars/hadoop-mapreduce-examples.jar` no armazenamento padrão da saudação para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="f9800-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on hello default storage for your cluster.</span></span>

<span data-ttu-id="f9800-162">Olá código Java a seguir é a origem Olá Olá MapReduce aplicativos contidos no hello `hadoop-mapreduce-examples.jar` arquivo:</span><span class="sxs-lookup"><span data-stu-id="f9800-162">hello following Java code is hello source of hello MapReduce application contained in hello `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="f9800-163">Para instruções toowrite seus próprios aplicativos de MapReduce, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9800-163">For instructions toowrite your own MapReduce applications, see hello following documents:</span></span>

* [<span data-ttu-id="f9800-164">Desenvolver aplicativos Java MapReduce para HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9800-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="f9800-165">Desenvolver aplicativos Python MapReduce para HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9800-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="f9800-166"><a id="run"></a>Executar Olá MapReduce</span><span class="sxs-lookup"><span data-stu-id="f9800-166"><a id="run"></a>Run hello MapReduce</span></span>

<span data-ttu-id="f9800-167">O HDInsight pode executar trabalhos de HiveQL usando vários métodos.</span><span class="sxs-lookup"><span data-stu-id="f9800-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="f9800-168">Usar o hello toodecide tabela qual método é ideal para você a seguir, siga o link Olá para obter uma explicação.</span><span class="sxs-lookup"><span data-stu-id="f9800-168">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="f9800-169">**Use isto**...</span><span class="sxs-lookup"><span data-stu-id="f9800-169">**Use this**...</span></span> | <span data-ttu-id="f9800-170">**... .toodo isso**</span><span class="sxs-lookup"><span data-stu-id="f9800-170">**...toodo this**</span></span> | <span data-ttu-id="f9800-171">... com esse **sistema operacional de cluster**</span><span class="sxs-lookup"><span data-stu-id="f9800-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="f9800-172">... desse **sistema operacional cliente**</span><span class="sxs-lookup"><span data-stu-id="f9800-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="f9800-173">SSH</span><span class="sxs-lookup"><span data-stu-id="f9800-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="f9800-174">Use Olá Hadoop comando por meio de **SSH**</span><span class="sxs-lookup"><span data-stu-id="f9800-174">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="f9800-175">Linux</span><span class="sxs-lookup"><span data-stu-id="f9800-175">Linux</span></span> |<span data-ttu-id="f9800-176">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="f9800-177">Curl</span><span class="sxs-lookup"><span data-stu-id="f9800-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="f9800-178">Enviar trabalho Olá remotamente usando **REST**</span><span class="sxs-lookup"><span data-stu-id="f9800-178">Submit hello job remotely by using **REST**</span></span> |<span data-ttu-id="f9800-179">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-179">Linux or Windows</span></span> |<span data-ttu-id="f9800-180">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="f9800-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9800-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="f9800-182">Enviar trabalho Olá remotamente usando **do Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="f9800-182">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="f9800-183">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-183">Linux or Windows</span></span> |<span data-ttu-id="f9800-184">Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-184">Windows</span></span> |
| <span data-ttu-id="f9800-185">[Área de Trabalho Remota](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="f9800-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="f9800-186">Use Olá Hadoop comando por meio de **área de trabalho remota**</span><span class="sxs-lookup"><span data-stu-id="f9800-186">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="f9800-187">Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-187">Windows</span></span> |<span data-ttu-id="f9800-188">Windows</span><span class="sxs-lookup"><span data-stu-id="f9800-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f9800-189">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f9800-189">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f9800-190">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f9800-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="f9800-191"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f9800-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="f9800-192">toolearn mais sobre como trabalhar com dados no HDInsight, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9800-192">toolearn more about working with data in HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="f9800-193">Desenvolver programas Java MapReduce para HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9800-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="f9800-194">Desenvolver programas MapReduce de streaming do Hadoop para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9800-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="f9800-195">Desenvolver trabalhos de MapReduce do Scalding com o Apache Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9800-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="f9800-196">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="f9800-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="f9800-197">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="f9800-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
