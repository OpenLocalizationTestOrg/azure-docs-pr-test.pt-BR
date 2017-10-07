---
title: exemplos de Hadoop MapReduce aaaRun no HDInsight - Azure | Microsoft Docs
description: "Comece a usar os exemplos de MapReduce em arquivos jar incluídos no HDInsight. Usar SSH tooconnect toohello cluster e, em seguida, usar trabalhos de exemplo hello Hadoop comando toorun."
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
ms.openlocfilehash: 7a16bbd51eb17570fcaa3b1e0f5990fa889c106a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="bdab5-105">Executar Olá MapReduce exemplos incluídos no HDInsight</span><span class="sxs-lookup"><span data-stu-id="bdab5-105">Run hello MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="bdab5-106">Saiba como exemplos de MapReduce Olá toorun incluídos com Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bdab5-106">Learn how toorun hello MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdab5-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bdab5-107">Prerequisites</span></span>

* <span data-ttu-id="bdab5-108">**Um cluster HDInsight**: consulte [Introdução ao uso do Hadoop com o Hive no HDInsight no Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="bdab5-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bdab5-109">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bdab5-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bdab5-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bdab5-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="bdab5-111">**Um cliente SSH**: para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bdab5-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="hello-mapreduce-examples"></a><span data-ttu-id="bdab5-112">exemplos de MapReduce Olá</span><span class="sxs-lookup"><span data-stu-id="bdab5-112">hello MapReduce examples</span></span>

<span data-ttu-id="bdab5-113">**Local**: Olá exemplos estão localizados em Olá cluster HDInsight no `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="bdab5-113">**Location**: hello samples are located on hello HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="bdab5-114">**Conteúdo**: Olá exemplos a seguir está contido neste arquivo:</span><span class="sxs-lookup"><span data-stu-id="bdab5-114">**Contents**: hello following samples are contained in this archive:</span></span>

* <span data-ttu-id="bdab5-115">`aggregatewordcount`: Uma agregação com base em programa mapreduce que conta Olá palavras nos arquivos de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="bdab5-116">`aggregatewordhist`: Uma agregação com base em programa mapreduce que calcula o histograma Olá palavras Olá nos arquivos de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes hello histogram of hello words in hello input files.</span></span>
* <span data-ttu-id="bdab5-117">`bbp`: Um programa mapreduce que usa Bailey-Borwein-Plouffe toocompute exatos dígitos de Pi.</span><span class="sxs-lookup"><span data-stu-id="bdab5-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe toocompute exact digits of Pi.</span></span>
* <span data-ttu-id="bdab5-118">`dbcount`: Um trabalho de exemplo que conta logs de página Olá armazenados em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="bdab5-118">`dbcount`: An example job that counts hello pageview logs stored in a database.</span></span>
* <span data-ttu-id="bdab5-119">`distbbp`: Um programa mapreduce que usa uma fórmula toocompute de BBP tipo exato bits de Pi.</span><span class="sxs-lookup"><span data-stu-id="bdab5-119">`distbbp`: A mapreduce program that uses a BBP-type formula toocompute exact bits of Pi.</span></span>
* <span data-ttu-id="bdab5-120">`grep`: Um programa mapreduce que conta Olá faz a correspondência de um regex na entrada hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-120">`grep`: A mapreduce program that counts hello matches of a regex in hello input.</span></span>
* <span data-ttu-id="bdab5-121">`join`: um trabalho que faz a união de bancos de dados classificados, particionados igualmente.</span><span class="sxs-lookup"><span data-stu-id="bdab5-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="bdab5-122">`multifilewc`: um trabalho que conta palavras de vários arquivos.</span><span class="sxs-lookup"><span data-stu-id="bdab5-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="bdab5-123">`pentomino`: Um bloco de mapreduce layout soluções do programa toofind toopentomino problemas.</span><span class="sxs-lookup"><span data-stu-id="bdab5-123">`pentomino`: A mapreduce tile laying program toofind solutions toopentomino problems.</span></span>
* <span data-ttu-id="bdab5-124">`pi`: um programa de MapReduce que estima Pi usando um método semelhante ao de Monte Carlo.</span><span class="sxs-lookup"><span data-stu-id="bdab5-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="bdab5-125">`randomtextwriter`: um programa de MapReduce que grava 10 GB de dados textuais aleatórios por nó.</span><span class="sxs-lookup"><span data-stu-id="bdab5-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="bdab5-126">`randomwriter`: um programa de MapReduce que grava 10 GB de dados aleatórios por nó.</span><span class="sxs-lookup"><span data-stu-id="bdab5-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="bdab5-127">`secondarysort`: Um exemplo definindo uma classificação secundária toohello reduzir fase.</span><span class="sxs-lookup"><span data-stu-id="bdab5-127">`secondarysort`: An example defining a secondary sort toohello reduce phase.</span></span>
* <span data-ttu-id="bdab5-128">`sort`: Um programa mapreduce que classifica dados Olá gravados pelo gravador aleatório hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-128">`sort`: A mapreduce program that sorts hello data written by hello random writer.</span></span>
* <span data-ttu-id="bdab5-129">`sudoku`: um solucionador de sudoku.</span><span class="sxs-lookup"><span data-stu-id="bdab5-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="bdab5-130">`teragen`: Gere dados para terasort hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-130">`teragen`: Generate data for hello terasort.</span></span>
* <span data-ttu-id="bdab5-131">`terasort`: Execute terasort hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-131">`terasort`: Run hello terasort.</span></span>
* <span data-ttu-id="bdab5-132">`teravalidate`: verifica os resultados do terasort.</span><span class="sxs-lookup"><span data-stu-id="bdab5-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="bdab5-133">`wordcount`: Um programa mapreduce que conta Olá palavras nos arquivos de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-133">`wordcount`: A mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="bdab5-134">`wordmean`: Um programa mapreduce que conta o comprimento médio de saudação de palavras Olá nos arquivos de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-134">`wordmean`: A mapreduce program that counts hello average length of hello words in hello input files.</span></span>
* <span data-ttu-id="bdab5-135">`wordmedian`: Arquivos de entrada um programa mapreduce que conta o comprimento médio de saudação de palavras Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="bdab5-135">`wordmedian`: A mapreduce program that counts hello median length of hello words in hello input files.</span></span>
* <span data-ttu-id="bdab5-136">`wordstandarddeviation`: Arquivos de entrada um programa mapreduce que conta o desvio padrão de saudação de comprimento de saudação do palavras Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="bdab5-136">`wordstandarddeviation`: A mapreduce program that counts hello standard deviation of hello length of hello words in hello input files.</span></span>

<span data-ttu-id="bdab5-137">**Código-fonte**: código-fonte para esses exemplos está incluído na Olá cluster HDInsight no `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="bdab5-137">**Source code**: Source code for these samples is included on hello HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="bdab5-138">Olá `2.2.4.9-1` no hello caminho é versão de saudação do hello Hortonworks Data Platform para o cluster do HDInsight hello e pode ser diferente para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="bdab5-138">hello `2.2.4.9-1` in hello path is hello version of hello Hortonworks Data Platform for hello HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-hello-wordcount-example"></a><span data-ttu-id="bdab5-139">Executar o exemplo de wordcount hello</span><span class="sxs-lookup"><span data-stu-id="bdab5-139">Run hello wordcount example</span></span>

1. <span data-ttu-id="bdab5-140">Conecte-se tooHDInsight usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="bdab5-140">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="bdab5-141">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bdab5-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="bdab5-142">De saudação `username@#######:~$` prompt, use Olá exemplos do comando toolist Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdab5-142">From hello `username@#######:~$` prompt, use hello following command toolist hello samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="bdab5-143">Este comando gera a lista de saudação do exemplo da seção anterior Olá deste documento.</span><span class="sxs-lookup"><span data-stu-id="bdab5-143">This command generates hello list of sample from hello previous section of this document.</span></span>

3. <span data-ttu-id="bdab5-144">Saudação de uso após o comando tooget ajuda sobre um exemplo específico.</span><span class="sxs-lookup"><span data-stu-id="bdab5-144">Use hello following command tooget help on a specific sample.</span></span> <span data-ttu-id="bdab5-145">Nesse caso, Olá **wordcount** exemplo:</span><span class="sxs-lookup"><span data-stu-id="bdab5-145">In this case, hello **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="bdab5-146">Você receberá a seguinte mensagem de saudação:</span><span class="sxs-lookup"><span data-stu-id="bdab5-146">You receive hello following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="bdab5-147">Esta mensagem indica que você pode fornecer vários caminhos de entrada para documentos de origem hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-147">This message indicates that you can provide several input paths for hello source documents.</span></span> <span data-ttu-id="bdab5-148">caminho de final de saudação é onde a saída de hello (contagem de palavras em documentos de origem Olá) é armazenada.</span><span class="sxs-lookup"><span data-stu-id="bdab5-148">hello final path is where hello output (count of words in hello source documents) is stored.</span></span>

4. <span data-ttu-id="bdab5-149">Use Olá toocount a seguir todas as palavras Olá blocos de anotações de Leonardo Da Vinci, que são fornecidos como dados de exemplo com o cluster:</span><span class="sxs-lookup"><span data-stu-id="bdab5-149">Use hello following toocount all words in hello Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="bdab5-150">A entrada para esse trabalho é lida pela entrada `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="bdab5-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="bdab5-151">A saída desse exemplo é armazenada em `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="bdab5-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="bdab5-152">Ambos os caminhos estão localizados no armazenamento padrão para o cluster hello, sistema de arquivos local do hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-152">Both paths are located on default storage for hello cluster, not hello local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bdab5-153">Conforme observado na Ajuda da saudação para exemplo de wordcount hello, você também pode especificar vários arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="bdab5-153">As noted in hello help for hello wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="bdab5-154">Por exemplo, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` contaria as palavras em davinci.txt e ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="bdab5-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="bdab5-155">Após a conclusão do trabalho hello, use Olá saída do comando tooview Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdab5-155">Once hello job completes, use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="bdab5-156">Este comando concatena todos os arquivos de saída de hello produzidos pelo trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="bdab5-156">This command concatenates all hello output files produced by hello job.</span></span> <span data-ttu-id="bdab5-157">Ele exibe o console do hello saída toohello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-157">It displays hello output toohello console.</span></span> <span data-ttu-id="bdab5-158">saudação de saída é similar toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdab5-158">hello output is similar toohello following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="bdab5-159">Cada linha representa uma palavra e dados de entrada de número de vezes que ocorreu no hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-159">Each line represents a word and how many times it occurred in hello input data.</span></span>

## <a name="hello-sudoku-example"></a><span data-ttu-id="bdab5-160">exemplo de Sudoku Hello</span><span class="sxs-lookup"><span data-stu-id="bdab5-160">hello Sudoku example</span></span>

<span data-ttu-id="bdab5-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) é um quebra-cabeça lógico composto por nove grades de 3x3.</span><span class="sxs-lookup"><span data-stu-id="bdab5-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="bdab5-162">Algumas células na grade de saudação têm números, enquanto outros são em branco, e a meta de saudação é toosolve para células em branco hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-162">Some cells in hello grid have numbers, while others are blank, and hello goal is toosolve for hello blank cells.</span></span> <span data-ttu-id="bdab5-163">link anterior Olá tem mais informações sobre quebra-cabeça de hello, mas finalidade deste exemplo hello é toosolve para células em branco hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-163">hello previous link has more information on hello puzzle, but hello purpose of this sample is toosolve for hello blank cells.</span></span> <span data-ttu-id="bdab5-164">Portanto, nossa entrada deve ser um arquivo que está no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdab5-164">So our input should be a file that is in hello following format:</span></span>

* <span data-ttu-id="bdab5-165">Nove linhas de nove colunas</span><span class="sxs-lookup"><span data-stu-id="bdab5-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="bdab5-166">Cada coluna pode conter um número ou `?` (que indica uma célula em branco)</span><span class="sxs-lookup"><span data-stu-id="bdab5-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="bdab5-167">As células são separadas por um espaço</span><span class="sxs-lookup"><span data-stu-id="bdab5-167">Cells are separated by a space</span></span>

<span data-ttu-id="bdab5-168">Há um determinado tooconstruct de maneira quebra-cabeças Sudoku; Você não pode repetir um número em uma coluna ou linha.</span><span class="sxs-lookup"><span data-stu-id="bdab5-168">There is a certain way tooconstruct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="bdab5-169">Há um exemplo no cluster HDInsight Olá que é construído corretamente.</span><span class="sxs-lookup"><span data-stu-id="bdab5-169">There's an example on hello HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="bdab5-170">Ele está localizado em `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` e contém Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdab5-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains hello following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="bdab5-171">toorun esse problema de exemplo por meio de saudação Sudoku exemplo, use Olá seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="bdab5-171">toorun this example problem through hello Sudoku example, use hello following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="bdab5-172">resultados de saudação aparecem semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdab5-172">hello results appear similar toohello following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="bdab5-173">Exemplo de pi (π)</span><span class="sxs-lookup"><span data-stu-id="bdab5-173">Pi (π) example</span></span>

<span data-ttu-id="bdab5-174">exemplo de pi Hello usa uma estatística (quase Monte Carlo) valor de saudação do método tooestimate de pi.</span><span class="sxs-lookup"><span data-stu-id="bdab5-174">hello pi sample uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="bdab5-175">Pontos são colocados aleatoriamente em um quadrado de unidade.</span><span class="sxs-lookup"><span data-stu-id="bdab5-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="bdab5-176">Quadrado Olá também contém um círculo.</span><span class="sxs-lookup"><span data-stu-id="bdab5-176">hello square also contains a circle.</span></span> <span data-ttu-id="bdab5-177">probabilidade de que os pontos de saudação se enquadra círculo Olá Olá são área toohello igual de saudação círculo, pi/4.</span><span class="sxs-lookup"><span data-stu-id="bdab5-177">hello probability that hello points fall within hello circle are equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="bdab5-178">valor de saudação de pi pode ser estimada do valor de saudação do 4R.</span><span class="sxs-lookup"><span data-stu-id="bdab5-178">hello value of pi can be estimated from hello value of 4R.</span></span> <span data-ttu-id="bdab5-179">R é a taxa de saudação do número de saudação de pontos que estão dentro de saudação círculo toohello número total de pontos que estão dentro do quadrado hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-179">R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="bdab5-180">Olá exemplo a saudação maior de pontos usados, melhor estimativa de Olá Olá é.</span><span class="sxs-lookup"><span data-stu-id="bdab5-180">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="bdab5-181">Use este exemplo de hello toorun de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="bdab5-181">Use hello following command toorun this sample.</span></span> <span data-ttu-id="bdab5-182">Esse comando usa 16 mapas com valor de saudação tooestimate 10.000.000 exemplos de pi:</span><span class="sxs-lookup"><span data-stu-id="bdab5-182">This command uses 16 maps with 10,000,000 samples each tooestimate hello value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="bdab5-183">Olá valor retornado por este comando é semelhante muito**3.14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="bdab5-183">hello value returned by this command is similar too**3.14159155000000000000**.</span></span> <span data-ttu-id="bdab5-184">Para obter referências, hello 10 primeiros casas decimais de pi são 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="bdab5-184">For references, hello first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="bdab5-185">Exemplo de GraySort de 10 GB</span><span class="sxs-lookup"><span data-stu-id="bdab5-185">10 GB Greysort example</span></span>

<span data-ttu-id="bdab5-186">GraySort é um tipo de parâmetro de comparação.</span><span class="sxs-lookup"><span data-stu-id="bdab5-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="bdab5-187">métrica de saudação é a taxa de classificação de hello (TB por minuto) que é obtida durante a classificação de grandes quantidades de dados, geralmente um 100 TB mínimo.</span><span class="sxs-lookup"><span data-stu-id="bdab5-187">hello metric is hello sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="bdab5-188">Este exemplo usa uma quantidade modesta de 10 GB de dados para que possa ser executado de modo relativamente rápido.</span><span class="sxs-lookup"><span data-stu-id="bdab5-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="bdab5-189">Ele usa os aplicativos de MapReduce Olá desenvolvidos por Owen O'Malley e Arun Murthy.</span><span class="sxs-lookup"><span data-stu-id="bdab5-189">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="bdab5-190">Esses aplicativos ganhou o parâmetro de comparação do hello anual para fins gerais ("daytona") terabyte classificação em 2009, com uma taxa de 0.578 TB/min (100 TB em 173 minutos).</span><span class="sxs-lookup"><span data-stu-id="bdab5-190">These applications won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="bdab5-191">Para obter mais informações sobre este e outros parâmetros de comparação de classificação, consulte Olá [Sortbenchmark](http://sortbenchmark.org/) site.</span><span class="sxs-lookup"><span data-stu-id="bdab5-191">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="bdab5-192">Este exemplo usa três conjuntos de programas MapReduce:</span><span class="sxs-lookup"><span data-stu-id="bdab5-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="bdab5-193">**TeraGen**: MapReduce um programa que gera linhas de dados toosort</span><span class="sxs-lookup"><span data-stu-id="bdab5-193">**TeraGen**: A MapReduce program that generates rows of data toosort</span></span>

* <span data-ttu-id="bdab5-194">**TeraSort**: exemplos de dados de entrada hello e usa dados de saudação do MapReduce toosort em uma ordem de total</span><span class="sxs-lookup"><span data-stu-id="bdab5-194">**TeraSort**: Samples hello input data and uses MapReduce toosort hello data into a total order</span></span>

    <span data-ttu-id="bdab5-195">A TeraSort é uma classificação de MapReduce padrão, exceto por um particionador personalizado.</span><span class="sxs-lookup"><span data-stu-id="bdab5-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="bdab5-196">o particionador Olá usa uma lista classificada de chaves de n-1 de amostra que definem o intervalo de chave Olá para cada reduza.</span><span class="sxs-lookup"><span data-stu-id="bdab5-196">hello partitioner uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="bdab5-197">Em particular, todas as chaves de tal que exemplo [i-1] < = chave < exemplo [i] são enviadas tooreduce i.</span><span class="sxs-lookup"><span data-stu-id="bdab5-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="bdab5-198">Este particionador garantias de saídas de saudação do reduzem i são todos com menos de reduzir a saída de saudação do i + 1.</span><span class="sxs-lookup"><span data-stu-id="bdab5-198">This partitioner guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>

* <span data-ttu-id="bdab5-199">**TeraValidate**: programa MapReduce A valida essa saída Olá global é classificado</span><span class="sxs-lookup"><span data-stu-id="bdab5-199">**TeraValidate**: A MapReduce program that validates that hello output is globally sorted</span></span>

    <span data-ttu-id="bdab5-200">Ele cria um mapa por arquivo no diretório de saída de hello e cada mapa garante que cada chave é menor ou igual a toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="bdab5-200">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="bdab5-201">função de mapa Hello gera registros de saudação primeiro e último chaves de cada arquivo.</span><span class="sxs-lookup"><span data-stu-id="bdab5-201">hello map function generates records of hello first and last keys of each file.</span></span> <span data-ttu-id="bdab5-202">Olá reduzir função garante que Olá primeira chave de arquivo i é maior que a chave do último Olá de i-1 de arquivo.</span><span class="sxs-lookup"><span data-stu-id="bdab5-202">hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="bdab5-203">Todos os problemas são relatados como uma saída de hello reduzir fase, com as chaves de saudação que estão fora de ordem.</span><span class="sxs-lookup"><span data-stu-id="bdab5-203">Any problems are reported as an output of hello reduce phase, with hello keys that are out of order.</span></span>

<span data-ttu-id="bdab5-204">Toogenerate dados, as etapas a seguir do uso Olá classificar e, em seguida, validar a saída de hello:</span><span class="sxs-lookup"><span data-stu-id="bdab5-204">Use hello following steps toogenerate data, sort, and then validate hello output:</span></span>

1. <span data-ttu-id="bdab5-205">Gerar 10 GB de dados, que é o armazenamento padrão do cluster do HDInsight toohello armazenado em `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="bdab5-205">Generate 10 GB of data, which is stored toohello HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="bdab5-206">Olá `-Dmapred.map.tasks` informa quantos toouse tarefas de mapa para este trabalho de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="bdab5-206">hello `-Dmapred.map.tasks` tells Hadoop how many map tasks toouse for this job.</span></span> <span data-ttu-id="bdab5-207">Olá final dois parâmetros instruem o hello trabalho toocreate 10 GB de dados e toostore-lo em `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="bdab5-207">hello final two parameters instruct hello job toocreate 10 GB of data and toostore it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="bdab5-208">Saudação de usar dados de saudação do toosort de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdab5-208">Use hello following command toosort hello data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="bdab5-209">Olá `-Dmapred.reduce.tasks` informa Hadoop reduzem quantas tarefas toouse para trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="bdab5-209">hello `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks toouse for hello job.</span></span> <span data-ttu-id="bdab5-210">parâmetros de saudação final dois são Olá apenas de entrada e locais para dados de saída.</span><span class="sxs-lookup"><span data-stu-id="bdab5-210">hello final two parameters are just hello input and output locations for data.</span></span>

3. <span data-ttu-id="bdab5-211">Use Olá seguintes toovalidate Olá dados gerados por classificação hello:</span><span class="sxs-lookup"><span data-stu-id="bdab5-211">Use hello following toovalidate hello data generated by hello sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="bdab5-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bdab5-212">Next steps</span></span>

<span data-ttu-id="bdab5-213">Neste artigo, você aprendeu como exemplos de saudação toorun incluídos com hello clusters HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="bdab5-213">From this article, you learned how toorun hello samples included with hello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="bdab5-214">Para tutoriais sobre como usar o Pig, Hive e MapReduce com HDInsight, consulte Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="bdab5-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="bdab5-215">[Usar o Pig com Hadoop no HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="bdab5-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="bdab5-216">[Usar o Hive com Hadoop no HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="bdab5-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="bdab5-217">[Usar o MapReduce com Hadoop no HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="bdab5-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
