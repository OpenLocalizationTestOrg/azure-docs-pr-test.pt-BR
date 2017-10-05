---
title: "Executar exemplos de MapReduce do Hadoop no HDInsight – Azure | Microsoft Docs"
description: "Comece a usar os exemplos de MapReduce em arquivos jar incluídos no HDInsight. Utilize SSH para se conectar ao cluster e use o comando do Hadoop para executar trabalhos de exemplo."
keywords: jar de exemplo do hadoop, jar de exemplos do hadoop, exemplos de mapreduce do hadoop, exemplos de mapreduce
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 447c07f869ff9a2a2a00089248be98e6729d6dc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="run-the-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="2ff77-105">Executar os exemplos de MapReduce incluídos no HDInsight</span><span class="sxs-lookup"><span data-stu-id="2ff77-105">Run the MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="2ff77-106">Saiba como executar os exemplos de MapReduce incluídos com Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2ff77-106">Learn how to run the MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ff77-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2ff77-107">Prerequisites</span></span>

* <span data-ttu-id="2ff77-108">**Um cluster HDInsight**: consulte [Introdução ao uso do Hadoop com o Hive no HDInsight no Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="2ff77-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2ff77-109">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="2ff77-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2ff77-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2ff77-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="2ff77-111">**Um cliente SSH**: para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2ff77-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="the-mapreduce-examples"></a><span data-ttu-id="2ff77-112">Os exemplos do MapReduce</span><span class="sxs-lookup"><span data-stu-id="2ff77-112">The MapReduce examples</span></span>

<span data-ttu-id="2ff77-113">**Local**: os exemplos estão localizados no cluster HDInsight em `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="2ff77-113">**Location**: The samples are located on the HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="2ff77-114">**Conteúdo**: os exemplos a seguir estão contidos neste arquivo:</span><span class="sxs-lookup"><span data-stu-id="2ff77-114">**Contents**: The following samples are contained in this archive:</span></span>

* <span data-ttu-id="2ff77-115">`aggregatewordcount`: um programa de MapReduce baseado em Agregação que conta as palavras nos arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="2ff77-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="2ff77-116">`aggregatewordhist`: um programa de MapReduce baseado em Agregação que computa o histograma de palavras nos arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="2ff77-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes the histogram of the words in the input files.</span></span>
* <span data-ttu-id="2ff77-117">`bbp`: um programa de MapReduce que usa Bailey-Borwein-Plouffe para computar os dígitos exatos de Pi.</span><span class="sxs-lookup"><span data-stu-id="2ff77-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.</span></span>
* <span data-ttu-id="2ff77-118">`dbcount`: um trabalho de exemplo que conta os logs de pageview armazenados em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2ff77-118">`dbcount`: An example job that counts the pageview logs stored in a database.</span></span>
* <span data-ttu-id="2ff77-119">`distbbp`: um programa de MapReduce que usa uma fórmula do tipo BBP para computar os bits exatos de Pi.</span><span class="sxs-lookup"><span data-stu-id="2ff77-119">`distbbp`: A mapreduce program that uses a BBP-type formula to compute exact bits of Pi.</span></span>
* <span data-ttu-id="2ff77-120">`grep`: um programa de MapReduce que conta as correspondências de uma regex na entrada.</span><span class="sxs-lookup"><span data-stu-id="2ff77-120">`grep`: A mapreduce program that counts the matches of a regex in the input.</span></span>
* <span data-ttu-id="2ff77-121">`join`: um trabalho que faz a união de bancos de dados classificados, particionados igualmente.</span><span class="sxs-lookup"><span data-stu-id="2ff77-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="2ff77-122">`multifilewc`: um trabalho que conta palavras de vários arquivos.</span><span class="sxs-lookup"><span data-stu-id="2ff77-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="2ff77-123">`pentomino`: um programa de MapReduce para disposição de blocos voltado a encontrar soluções para problemas de pentomino.</span><span class="sxs-lookup"><span data-stu-id="2ff77-123">`pentomino`: A mapreduce tile laying program to find solutions to pentomino problems.</span></span>
* <span data-ttu-id="2ff77-124">`pi`: um programa de MapReduce que estima Pi usando um método semelhante ao de Monte Carlo.</span><span class="sxs-lookup"><span data-stu-id="2ff77-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="2ff77-125">`randomtextwriter`: um programa de MapReduce que grava 10 GB de dados textuais aleatórios por nó.</span><span class="sxs-lookup"><span data-stu-id="2ff77-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="2ff77-126">`randomwriter`: um programa de MapReduce que grava 10 GB de dados aleatórios por nó.</span><span class="sxs-lookup"><span data-stu-id="2ff77-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="2ff77-127">`secondarysort`: um exemplo que define uma classificação secundária para a fase de redução.</span><span class="sxs-lookup"><span data-stu-id="2ff77-127">`secondarysort`: An example defining a secondary sort to the reduce phase.</span></span>
* <span data-ttu-id="2ff77-128">`sort`: um programa de MapReduce que classifica os dados gravados pelo gravador aleatório.</span><span class="sxs-lookup"><span data-stu-id="2ff77-128">`sort`: A mapreduce program that sorts the data written by the random writer.</span></span>
* <span data-ttu-id="2ff77-129">`sudoku`: um solucionador de sudoku.</span><span class="sxs-lookup"><span data-stu-id="2ff77-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="2ff77-130">`teragen`: gera dados para o terasort.</span><span class="sxs-lookup"><span data-stu-id="2ff77-130">`teragen`: Generate data for the terasort.</span></span>
* <span data-ttu-id="2ff77-131">`terasort`: executa o terasort.</span><span class="sxs-lookup"><span data-stu-id="2ff77-131">`terasort`: Run the terasort.</span></span>
* <span data-ttu-id="2ff77-132">`teravalidate`: verifica os resultados do terasort.</span><span class="sxs-lookup"><span data-stu-id="2ff77-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="2ff77-133">`wordcount`: um programa de MapReduce que conta as palavras nos arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="2ff77-133">`wordcount`: A mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="2ff77-134">`wordmean`: um programa de MapReduce que calcula o tamanho médio das palavras nos arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="2ff77-134">`wordmean`: A mapreduce program that counts the average length of the words in the input files.</span></span>
* <span data-ttu-id="2ff77-135">`wordmedian`: um programa de MapReduce que calcula o tamanho mediano das palavras nos arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="2ff77-135">`wordmedian`: A mapreduce program that counts the median length of the words in the input files.</span></span>
* <span data-ttu-id="2ff77-136">`wordstandarddeviation`: um programa de MapReduce que calcula o desvio padrão do tamanho das palavras nos arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="2ff77-136">`wordstandarddeviation`: A mapreduce program that counts the standard deviation of the length of the words in the input files.</span></span>

<span data-ttu-id="2ff77-137">**O código-fonte**: código-fonte para esses exemplos está incluído no cluster HDInsight em `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="2ff77-137">**Source code**: Source code for these samples is included on the HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="2ff77-138">O `2.2.4.9-1` no caminho é a versão do Hortonworks Data Platform para o cluster do HDInsight e pode ser diferente para o seu cluster.</span><span class="sxs-lookup"><span data-stu-id="2ff77-138">The `2.2.4.9-1` in the path is the version of the Hortonworks Data Platform for the HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-the-wordcount-example"></a><span data-ttu-id="2ff77-139">Executar o exemplo de wordcount</span><span class="sxs-lookup"><span data-stu-id="2ff77-139">Run the wordcount example</span></span>

1. <span data-ttu-id="2ff77-140">Conecte-se ao HDInsight usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="2ff77-140">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="2ff77-141">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2ff77-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="2ff77-142">No prompt `username@#######:~$` , use o comando a seguir para listar os exemplos:</span><span class="sxs-lookup"><span data-stu-id="2ff77-142">From the `username@#######:~$` prompt, use the following command to list the samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="2ff77-143">Esse comando gera a lista de exemplos da seção anterior deste documento.</span><span class="sxs-lookup"><span data-stu-id="2ff77-143">This command generates the list of sample from the previous section of this document.</span></span>

3. <span data-ttu-id="2ff77-144">Use o comando a seguir para obter ajuda com um exemplo específico.</span><span class="sxs-lookup"><span data-stu-id="2ff77-144">Use the following command to get help on a specific sample.</span></span> <span data-ttu-id="2ff77-145">Neste caso, o exemplo é **wordcount** :</span><span class="sxs-lookup"><span data-stu-id="2ff77-145">In this case, the **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="2ff77-146">Você receberá a seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="2ff77-146">You receive the following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="2ff77-147">Essa mensagem indica que você pode fornecer vários caminhos de entrada para os documentos de origem.</span><span class="sxs-lookup"><span data-stu-id="2ff77-147">This message indicates that you can provide several input paths for the source documents.</span></span> <span data-ttu-id="2ff77-148">O caminho final é o local em que a saída (contagem de palavras em documentos de origem) está armazenada.</span><span class="sxs-lookup"><span data-stu-id="2ff77-148">The final path is where the output (count of words in the source documents) is stored.</span></span>

4. <span data-ttu-id="2ff77-149">Use o seguinte para contar todas as palavras nos blocos de anotações de Leonardo Da Vinci, que são fornecidos como dados de exemplo com o cluster:</span><span class="sxs-lookup"><span data-stu-id="2ff77-149">Use the following to count all words in the Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="2ff77-150">A entrada para esse trabalho é lida pela entrada `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="2ff77-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="2ff77-151">A saída desse exemplo é armazenada em `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="2ff77-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="2ff77-152">Ambos os caminhos estão localizados no armazenamento padrão do cluster, não no sistema de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="2ff77-152">Both paths are located on default storage for the cluster, not the local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2ff77-153">Conforme observado na ajuda do exemplo wordcount, você também pode especificar vários arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="2ff77-153">As noted in the help for the wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="2ff77-154">Por exemplo, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` contaria as palavras em davinci.txt e ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="2ff77-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="2ff77-155">Quando o trabalho for concluído, use o seguinte comando para exibir a saída:</span><span class="sxs-lookup"><span data-stu-id="2ff77-155">Once the job completes, use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="2ff77-156">Esse comando concatena todos os arquivos de saída produzidos pelo trabalho.</span><span class="sxs-lookup"><span data-stu-id="2ff77-156">This command concatenates all the output files produced by the job.</span></span> <span data-ttu-id="2ff77-157">Ele exibe a saída para o console.</span><span class="sxs-lookup"><span data-stu-id="2ff77-157">It displays the output to the console.</span></span> <span data-ttu-id="2ff77-158">A saída é semelhante ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ff77-158">The output is similar to the following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="2ff77-159">Cada linha representa uma palavra e quantas vezes ela ocorreu nos dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="2ff77-159">Each line represents a word and how many times it occurred in the input data.</span></span>

## <a name="the-sudoku-example"></a><span data-ttu-id="2ff77-160">O exemplo Sudoku</span><span class="sxs-lookup"><span data-stu-id="2ff77-160">The Sudoku example</span></span>

<span data-ttu-id="2ff77-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) é um quebra-cabeça lógico composto por nove grades de 3x3.</span><span class="sxs-lookup"><span data-stu-id="2ff77-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="2ff77-162">Algumas células da grade têm números, enquanto outros estão em branco, e a meta é encontrar os números correspondentes às células em branco.</span><span class="sxs-lookup"><span data-stu-id="2ff77-162">Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells.</span></span> <span data-ttu-id="2ff77-163">O link anterior tem mais informações sobre o quebra-cabeça, mas o propósito dessa amostra é encontrar as respostas para as células em branco.</span><span class="sxs-lookup"><span data-stu-id="2ff77-163">The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells.</span></span> <span data-ttu-id="2ff77-164">Sendo assim, nossa entrada deve ser um arquivo no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="2ff77-164">So our input should be a file that is in the following format:</span></span>

* <span data-ttu-id="2ff77-165">Nove linhas de nove colunas</span><span class="sxs-lookup"><span data-stu-id="2ff77-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="2ff77-166">Cada coluna pode conter um número ou `?` (que indica uma célula em branco)</span><span class="sxs-lookup"><span data-stu-id="2ff77-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="2ff77-167">As células são separadas por um espaço</span><span class="sxs-lookup"><span data-stu-id="2ff77-167">Cells are separated by a space</span></span>

<span data-ttu-id="2ff77-168">Há uma certa forma de construir o quebra-cabeças Sudoku que não permite repetir um número na mesma coluna ou linha.</span><span class="sxs-lookup"><span data-stu-id="2ff77-168">There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="2ff77-169">Há um exemplo no cluster do HDInsight que está construído corretamente.</span><span class="sxs-lookup"><span data-stu-id="2ff77-169">There's an example on the HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="2ff77-170">Ele está localizado em `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` e contém o seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="2ff77-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains the following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="2ff77-171">Para executar este problema de exemplo por meio do exemplo do Sudoku, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2ff77-171">To run this example problem through the Sudoku example, use the following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="2ff77-172">Os resultados são semelhantes ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ff77-172">The results appear similar to the following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="2ff77-173">Exemplo de pi (π)</span><span class="sxs-lookup"><span data-stu-id="2ff77-173">Pi (π) example</span></span>

<span data-ttu-id="2ff77-174">O exemplo do pi usa um método estatístico (quasi-Monte Carlo) para estimar o valor de pi.</span><span class="sxs-lookup"><span data-stu-id="2ff77-174">The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span></span> <span data-ttu-id="2ff77-175">Pontos são colocados aleatoriamente em um quadrado de unidade.</span><span class="sxs-lookup"><span data-stu-id="2ff77-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="2ff77-176">O quadrado também contém um círculo.</span><span class="sxs-lookup"><span data-stu-id="2ff77-176">The square also contains a circle.</span></span> <span data-ttu-id="2ff77-177">A probabilidade de que os pontos caiam dentro do círculo é igual à área do círculo, pi/4.</span><span class="sxs-lookup"><span data-stu-id="2ff77-177">The probability that the points fall within the circle are equal to the area of the circle, pi/4.</span></span> <span data-ttu-id="2ff77-178">O valor de pi pode ser estimado do valor de 4R.</span><span class="sxs-lookup"><span data-stu-id="2ff77-178">The value of pi can be estimated from the value of 4R.</span></span> <span data-ttu-id="2ff77-179">R é a proporção do número de pontos que estão dentro do círculo em relação ao número total de pontos que estão dentro do quadrado.</span><span class="sxs-lookup"><span data-stu-id="2ff77-179">R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span></span> <span data-ttu-id="2ff77-180">Quanto maior a amostra de pontos usados, melhor será a estimativa.</span><span class="sxs-lookup"><span data-stu-id="2ff77-180">The larger the sample of points used, the better the estimate is.</span></span>

<span data-ttu-id="2ff77-181">Use o seguinte comando para executar o exemplo.</span><span class="sxs-lookup"><span data-stu-id="2ff77-181">Use the following command to run this sample.</span></span> <span data-ttu-id="2ff77-182">O comando usa 16 mapas com 10.000.000 amostras cada um para estimar o valor de pi:</span><span class="sxs-lookup"><span data-stu-id="2ff77-182">This command uses 16 maps with 10,000,000 samples each to estimate the value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="2ff77-183">O valor retornado por este comando deve ser semelhante a **3,14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="2ff77-183">The value returned by this command is similar to **3.14159155000000000000**.</span></span> <span data-ttu-id="2ff77-184">Para referência, as 10 primeiras casas decimais de pi são 3,1415926535.</span><span class="sxs-lookup"><span data-stu-id="2ff77-184">For references, the first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="2ff77-185">Exemplo de GraySort de 10 GB</span><span class="sxs-lookup"><span data-stu-id="2ff77-185">10 GB Greysort example</span></span>

<span data-ttu-id="2ff77-186">GraySort é um tipo de parâmetro de comparação.</span><span class="sxs-lookup"><span data-stu-id="2ff77-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="2ff77-187">A métrica é a taxa de classificação (TB/minuto) que é obtida durante a classificação de grandes quantidades de dados, geralmente um mínimo de 100 TB.</span><span class="sxs-lookup"><span data-stu-id="2ff77-187">The metric is the sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="2ff77-188">Este exemplo usa uma quantidade modesta de 10 GB de dados para que possa ser executado de modo relativamente rápido.</span><span class="sxs-lookup"><span data-stu-id="2ff77-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="2ff77-189">Ele usa os aplicativos de MapReduce desenvolvidos por Owen O'Malley e Arun Murthy.</span><span class="sxs-lookup"><span data-stu-id="2ff77-189">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="2ff77-190">Esses aplicativos ganharam o parâmetro de comparação anual de classificação de terabytes de uso geral ("daytona") em 2009, com uma taxa de 0,578 TB/min (100 TB em 173 minutos).</span><span class="sxs-lookup"><span data-stu-id="2ff77-190">These applications won the annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="2ff77-191">Para obter mais informações sobre esse e outros benchmarks de classificação, consulte o site [Sortbenchmark](http://sortbenchmark.org/) .</span><span class="sxs-lookup"><span data-stu-id="2ff77-191">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="2ff77-192">Este exemplo usa três conjuntos de programas MapReduce:</span><span class="sxs-lookup"><span data-stu-id="2ff77-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="2ff77-193">**TeraGen**: um programa de MapReduce que gera linhas de dados para classificar</span><span class="sxs-lookup"><span data-stu-id="2ff77-193">**TeraGen**: A MapReduce program that generates rows of data to sort</span></span>

* <span data-ttu-id="2ff77-194">**TeraSort**: cria amostras dos dados de entrada e usa o MapReduce para classificar os dados em uma ordem total</span><span class="sxs-lookup"><span data-stu-id="2ff77-194">**TeraSort**: Samples the input data and uses MapReduce to sort the data into a total order</span></span>

    <span data-ttu-id="2ff77-195">A TeraSort é uma classificação de MapReduce padrão, exceto por um particionador personalizado.</span><span class="sxs-lookup"><span data-stu-id="2ff77-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="2ff77-196">O particionador usa uma lista classificada de N-1 chaves amostradas que definem o intervalo de chave para cada redução.</span><span class="sxs-lookup"><span data-stu-id="2ff77-196">The partitioner uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span></span> <span data-ttu-id="2ff77-197">Em particular, todas as chaves dessa amostra[i-1] <= chave < amostra[i] são enviadas para reduzir i.</span><span class="sxs-lookup"><span data-stu-id="2ff77-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span></span> <span data-ttu-id="2ff77-198">Esse particionador garante que as saídas da redução i sejam todas menores do que a saída da redução i+1.</span><span class="sxs-lookup"><span data-stu-id="2ff77-198">This partitioner guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span></span>

* <span data-ttu-id="2ff77-199">**TeraValidate**: um programa de MapReduce que valida que a saída é classificada globalmente</span><span class="sxs-lookup"><span data-stu-id="2ff77-199">**TeraValidate**: A MapReduce program that validates that the output is globally sorted</span></span>

    <span data-ttu-id="2ff77-200">Ele cria um mapa por arquivo no diretório de saída, e cada mapa garante que cada chave seja menor ou igual à anterior.</span><span class="sxs-lookup"><span data-stu-id="2ff77-200">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span></span> <span data-ttu-id="2ff77-201">A função map gera registros das primeiras e últimas chaves de cada arquivo.</span><span class="sxs-lookup"><span data-stu-id="2ff77-201">The map function generates records of the first and last keys of each file.</span></span> <span data-ttu-id="2ff77-202">A função de redução garante que a primeira chave do arquivo i seja maior do que a última chave do arquivo i-1.</span><span class="sxs-lookup"><span data-stu-id="2ff77-202">The reduce function ensures that the first key of file i is greater than the last key of file i-1.</span></span> <span data-ttu-id="2ff77-203">Todos os problemas são relatados como uma saída da fase de redução, com as chaves que estão fora de ordem.</span><span class="sxs-lookup"><span data-stu-id="2ff77-203">Any problems are reported as an output of the reduce phase, with the keys that are out of order.</span></span>

<span data-ttu-id="2ff77-204">Use as seguintes etapas para gerar dados, classificar e validar a saída:</span><span class="sxs-lookup"><span data-stu-id="2ff77-204">Use the following steps to generate data, sort, and then validate the output:</span></span>

1. <span data-ttu-id="2ff77-205">Gere 10 GB de dados, que são armazenados no armazenamento padrão do cluster HDInsight em `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="2ff77-205">Generate 10 GB of data, which is stored to the HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="2ff77-206">O `-Dmapred.map.tasks` informa o Hadoop quantas tarefas de mapeamento serão usadas para este trabalho.</span><span class="sxs-lookup"><span data-stu-id="2ff77-206">The `-Dmapred.map.tasks` tells Hadoop how many map tasks to use for this job.</span></span> <span data-ttu-id="2ff77-207">Os dois parâmetros finais instruem o trabalho a criar 10 GB de dados e armazená-los em `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="2ff77-207">The final two parameters instruct the job to create 10 GB of data and to store it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="2ff77-208">Use o comando a seguir para classificar os dados:</span><span class="sxs-lookup"><span data-stu-id="2ff77-208">Use the following command to sort the data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="2ff77-209">O `-Dmapred.reduce.tasks` informa o Hadoop quantas tarefas de redução serão usadas para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="2ff77-209">The `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks to use for the job.</span></span> <span data-ttu-id="2ff77-210">Os dois parâmetros finais são apenas os locais de entrada e saída dos dados.</span><span class="sxs-lookup"><span data-stu-id="2ff77-210">The final two parameters are just the input and output locations for data.</span></span>

3. <span data-ttu-id="2ff77-211">Use o seguinte para validar os dados gerados pela classificação:</span><span class="sxs-lookup"><span data-stu-id="2ff77-211">Use the following to validate the data generated by the sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="2ff77-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2ff77-212">Next steps</span></span>

<span data-ttu-id="2ff77-213">Neste artigo, você aprendeu a executar os exemplos incluídos com os clusters do HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="2ff77-213">From this article, you learned how to run the samples included with the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="2ff77-214">Para obter tutoriais sobre como usar o Pig, o Hive e o MapReduce com o HDInsight, consulte os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="2ff77-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span></span>

* <span data-ttu-id="2ff77-215">[Usar o Pig com Hadoop no HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="2ff77-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="2ff77-216">[Usar o Hive com Hadoop no HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="2ff77-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="2ff77-217">[Usar o MapReduce com Hadoop no HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="2ff77-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
