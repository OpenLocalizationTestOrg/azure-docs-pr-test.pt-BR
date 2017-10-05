---
title: MapReduce com Hadoop no HDInsight | Microsoft Docs
description: Saiba como executar trabalhos do MapReduce no Hadoop em clusters HDInsight.
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
ms.openlocfilehash: df8ac578a56de72df667b1fa7f90f981c79d9999
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="1f787-103">Usar o MapReduce no Hadoop do HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f787-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="1f787-104">Saiba como executar trabalhos do MapReduce em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f787-104">Learn how to run MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="1f787-105">Use a tabela a seguir para descobrir várias maneiras pelas quais o MapReduce pode ser usado com o HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1f787-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="1f787-106">**Use isto**...</span><span class="sxs-lookup"><span data-stu-id="1f787-106">**Use this**...</span></span> | <span data-ttu-id="1f787-107">**...Para fazer isso**</span><span class="sxs-lookup"><span data-stu-id="1f787-107">**...to do this**</span></span> | <span data-ttu-id="1f787-108">... com esse **sistema operacional de cluster**</span><span class="sxs-lookup"><span data-stu-id="1f787-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="1f787-109">... desse **sistema operacional cliente**</span><span class="sxs-lookup"><span data-stu-id="1f787-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="1f787-110">SSH</span><span class="sxs-lookup"><span data-stu-id="1f787-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="1f787-111">Usar o comando Hadoop por meio de **SSH**</span><span class="sxs-lookup"><span data-stu-id="1f787-111">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="1f787-112">Linux</span><span class="sxs-lookup"><span data-stu-id="1f787-112">Linux</span></span> |<span data-ttu-id="1f787-113">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="1f787-114">REST</span><span class="sxs-lookup"><span data-stu-id="1f787-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="1f787-115">Enviar o trabalho remotamente usando a **REST** (os exemplos usam cURL)</span><span class="sxs-lookup"><span data-stu-id="1f787-115">Submit the job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="1f787-116">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-116">Linux or Windows</span></span> |<span data-ttu-id="1f787-117">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="1f787-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f787-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="1f787-119">Enviar o trabalho remotamente usando o **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="1f787-119">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="1f787-120">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-120">Linux or Windows</span></span> |<span data-ttu-id="1f787-121">Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-121">Windows</span></span> |
| <span data-ttu-id="1f787-122">[Área de trabalho remota](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="1f787-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="1f787-123">Usar o comando Hadoop por meio da **Área de trabalho remota**</span><span class="sxs-lookup"><span data-stu-id="1f787-123">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="1f787-124">Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-124">Windows</span></span> |<span data-ttu-id="1f787-125">Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="1f787-126">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="1f787-126">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1f787-127">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1f787-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="1f787-128"><a id="whatis"></a>O que é o MapReduce</span><span class="sxs-lookup"><span data-stu-id="1f787-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="1f787-129">O MapReduce do Hadoop é uma estrutura de software para escrever trabalhos que processam grandes quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="1f787-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="1f787-130">Os dados de entrada são divididos em partes independentes e processados em paralelo em todos os nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="1f787-130">Input data is split into independent chunks, which are then processed in parallel across the nodes in your cluster.</span></span> <span data-ttu-id="1f787-131">Um trabalho do MapReduce consiste em duas funções:</span><span class="sxs-lookup"><span data-stu-id="1f787-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="1f787-132">**Mapeador**: consome dados de entrada, analisa-os (normalmente com operações de classificação e filtro) e emite tuplas (pares chave-valor)</span><span class="sxs-lookup"><span data-stu-id="1f787-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="1f787-133">**Redutor**: consome tuplas emitidas pelo Mapeador e executa uma operação de resumo que cria um resultado menor e combinado dos dados do Mapeador</span><span class="sxs-lookup"><span data-stu-id="1f787-133">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span></span>

<span data-ttu-id="1f787-134">Um exemplo básico de trabalho de contagem de palavras do MapReduce está ilustrado no diagrama abaixo:</span><span class="sxs-lookup"><span data-stu-id="1f787-134">A basic word count MapReduce job example is illustrated in the following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="1f787-136">A saída deste trabalho é uma contagem de quantas vezes cada palavra ocorreu no texto que foi analisado.</span><span class="sxs-lookup"><span data-stu-id="1f787-136">The output of this job is a count of how many times each word occurred in the text that was analyzed.</span></span>

* <span data-ttu-id="1f787-137">O mapeador utiliza cada linha do texto de entrada como uma entrada e a divide em palavras.</span><span class="sxs-lookup"><span data-stu-id="1f787-137">The mapper takes each line from the input text as an input and breaks it into words.</span></span> <span data-ttu-id="1f787-138">Ele emite um par de chave/valor cada vez que ocorre uma palavra seguida de um 1.</span><span class="sxs-lookup"><span data-stu-id="1f787-138">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span></span> <span data-ttu-id="1f787-139">A saída será classificada antes de ser enviada ao redutor.</span><span class="sxs-lookup"><span data-stu-id="1f787-139">The output is sorted before sending it to reducer.</span></span>
* <span data-ttu-id="1f787-140">Em seguida, o redutor soma essas contagens individuais para cada palavra e emite um par de chave/valor único que contém a palavra seguido pela soma de suas ocorrências.</span><span class="sxs-lookup"><span data-stu-id="1f787-140">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span></span>

<span data-ttu-id="1f787-141">O MapReduce pode ser implementado em várias linguagens.</span><span class="sxs-lookup"><span data-stu-id="1f787-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="1f787-142">Java é a implementação mais comum e é usado para fins de demonstração neste documento.</span><span class="sxs-lookup"><span data-stu-id="1f787-142">Java is the most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="1f787-143">Linguagens de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="1f787-143">Development languages</span></span>

<span data-ttu-id="1f787-144">As linguagens ou frameworks que são baseados em Java e a Máquina Virtual Java podem ser executadas diretamente como um trabalho do MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1f787-144">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="1f787-145">O exemplo usado neste documento é um aplicativo MapReduce em Java.</span><span class="sxs-lookup"><span data-stu-id="1f787-145">The example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="1f787-146">Linguagens não Java, como C#, Python ou executáveis autônomos, devem usar o streaming do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1f787-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="1f787-147">O streaming do Hadoop se comunica com o mapeador e redutor por STDIN e STDOUT.</span><span class="sxs-lookup"><span data-stu-id="1f787-147">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="1f787-148">O mapeador e redutor leem os dados uma linha por vez do STDIN e gravam a saída em STDOUT.</span><span class="sxs-lookup"><span data-stu-id="1f787-148">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span></span> <span data-ttu-id="1f787-149">Cada linha lida ou emitida pelo mapeador e redutor deve estar no formato de um par de chave/valor, delimitado por um caractere de tabulação:</span><span class="sxs-lookup"><span data-stu-id="1f787-149">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="1f787-150">Para saber mais, confira [Streaming do Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="1f787-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="1f787-151">Para ver exemplos do uso de streaming com o HDInsight do Hadoop, consulte os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="1f787-151">For examples of using Hadoop streaming with HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="1f787-152">Desenvolver trabalhos do MapReduce em C#</span><span class="sxs-lookup"><span data-stu-id="1f787-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="1f787-153">Desenvolver trabalhos do MapReduce Python</span><span class="sxs-lookup"><span data-stu-id="1f787-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="1f787-154"><a id="data"></a>Dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="1f787-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="1f787-155">O HDInsight fornece vários conjuntos de dados de exemplo, que são armazenados no diretório `/example/data` e `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="1f787-155">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="1f787-156">Esses diretórios estão no armazenamento padrão do cluster.</span><span class="sxs-lookup"><span data-stu-id="1f787-156">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="1f787-157">Neste documento, usamos o arquivo `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="1f787-157">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="1f787-158">Esse arquivo contém o cadernos de Leonardo Da Vinci.</span><span class="sxs-lookup"><span data-stu-id="1f787-158">This file contains the notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="1f787-159"><a id="job"></a>MapReduce de exemplo</span><span class="sxs-lookup"><span data-stu-id="1f787-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="1f787-160">Um exemplo de aplicativo de contagem de palavras do MapReduce está incluído no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1f787-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="1f787-161">Este exemplo está localizado em `/example/jars/hadoop-mapreduce-examples.jar` no armazenamento padrão para o cluster.</span><span class="sxs-lookup"><span data-stu-id="1f787-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span></span>

<span data-ttu-id="1f787-162">O seguinte código Java é o código-fonte do aplicativo MapReduce contida no arquivo `hadoop-mapreduce-examples.jar`:</span><span class="sxs-lookup"><span data-stu-id="1f787-162">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="1f787-163">Para obter instruções para escrever seus próprios aplicativos MapReduce, consulte os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="1f787-163">For instructions to write your own MapReduce applications, see the following documents:</span></span>

* [<span data-ttu-id="1f787-164">Desenvolver aplicativos Java MapReduce para HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f787-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="1f787-165">Desenvolver aplicativos Python MapReduce para HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f787-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="1f787-166"><a id="run"></a>Executar o MapReduce</span><span class="sxs-lookup"><span data-stu-id="1f787-166"><a id="run"></a>Run the MapReduce</span></span>

<span data-ttu-id="1f787-167">O HDInsight pode executar trabalhos de HiveQL usando vários métodos.</span><span class="sxs-lookup"><span data-stu-id="1f787-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="1f787-168">Use a tabela a seguir para decidir qual método é o melhor para você e siga o link para obter o passo-a-passo.</span><span class="sxs-lookup"><span data-stu-id="1f787-168">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="1f787-169">**Use isto**...</span><span class="sxs-lookup"><span data-stu-id="1f787-169">**Use this**...</span></span> | <span data-ttu-id="1f787-170">**...Para fazer isso**</span><span class="sxs-lookup"><span data-stu-id="1f787-170">**...to do this**</span></span> | <span data-ttu-id="1f787-171">... com esse **sistema operacional de cluster**</span><span class="sxs-lookup"><span data-stu-id="1f787-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="1f787-172">... desse **sistema operacional cliente**</span><span class="sxs-lookup"><span data-stu-id="1f787-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="1f787-173">SSH</span><span class="sxs-lookup"><span data-stu-id="1f787-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="1f787-174">Usar o comando Hadoop por meio de **SSH**</span><span class="sxs-lookup"><span data-stu-id="1f787-174">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="1f787-175">Linux</span><span class="sxs-lookup"><span data-stu-id="1f787-175">Linux</span></span> |<span data-ttu-id="1f787-176">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="1f787-177">Curl</span><span class="sxs-lookup"><span data-stu-id="1f787-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="1f787-178">Enviar o trabalho remotamente usando a **REST**</span><span class="sxs-lookup"><span data-stu-id="1f787-178">Submit the job remotely by using **REST**</span></span> |<span data-ttu-id="1f787-179">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-179">Linux or Windows</span></span> |<span data-ttu-id="1f787-180">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="1f787-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f787-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="1f787-182">Enviar o trabalho remotamente usando o **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="1f787-182">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="1f787-183">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-183">Linux or Windows</span></span> |<span data-ttu-id="1f787-184">Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-184">Windows</span></span> |
| <span data-ttu-id="1f787-185">[Área de trabalho remota](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="1f787-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="1f787-186">Usar o comando Hadoop por meio da **Área de trabalho remota**</span><span class="sxs-lookup"><span data-stu-id="1f787-186">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="1f787-187">Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-187">Windows</span></span> |<span data-ttu-id="1f787-188">Windows</span><span class="sxs-lookup"><span data-stu-id="1f787-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="1f787-189">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="1f787-189">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1f787-190">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1f787-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="1f787-191"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f787-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="1f787-192">Para saber mais sobre como trabalhar com os dados no HDInsight, consulte os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="1f787-192">To learn more about working with data in HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="1f787-193">Desenvolver programas Java MapReduce para HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f787-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="1f787-194">Desenvolver programas MapReduce de streaming do Hadoop para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f787-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="1f787-195">Desenvolver trabalhos de MapReduce do Scalding com o Apache Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f787-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="1f787-196">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="1f787-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="1f787-197">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="1f787-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
