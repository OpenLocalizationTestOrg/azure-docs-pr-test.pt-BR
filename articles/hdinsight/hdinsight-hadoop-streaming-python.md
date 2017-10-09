---
title: trabalhos de Python streaming MapReduce aaaDevelop com HDInsight - Azure | Microsoft Docs
description: Saiba como toouse Python no fluxo de trabalhos de MapReduce. O Hadoop fornece uma API de streaming para MapReduce para escrever em linguagens diferentes do Java.
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a6ae3ba650b665ecc5839a4ddf5282f8ccfb6bd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="7ab56-104">Desenvolver programas MapReduce de streaming do Python para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ab56-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="7ab56-105">Saiba como toouse Python em MapReduce operações de fluxo contínuo.</span><span class="sxs-lookup"><span data-stu-id="7ab56-105">Learn how toouse Python in streaming MapReduce operations.</span></span> <span data-ttu-id="7ab56-106">Hadoop fornece uma API de streaming para MapReduce que permite que você toowrite mapa e reduzir as funções em idiomas diferentes do Java.</span><span class="sxs-lookup"><span data-stu-id="7ab56-106">Hadoop provides a streaming API for MapReduce that enables you toowrite map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="7ab56-107">Olá etapas deste documento implementam Olá mapa e reduzem componentes em Python.</span><span class="sxs-lookup"><span data-stu-id="7ab56-107">hello steps in this document implement hello Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ab56-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7ab56-108">Prerequisites</span></span>

* <span data-ttu-id="7ab56-109">Um Hadoop baseado em Linux no cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ab56-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7ab56-110">etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux.</span><span class="sxs-lookup"><span data-stu-id="7ab56-110">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="7ab56-111">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7ab56-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7ab56-112">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7ab56-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7ab56-113">Um editor de texto</span><span class="sxs-lookup"><span data-stu-id="7ab56-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7ab56-114">editor de texto de saudação deve usar LF terminação de linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="7ab56-114">hello text editor must use LF as hello line ending.</span></span> <span data-ttu-id="7ab56-115">Usar uma terminação de linha de CRLF causa erros durante a execução do trabalho MapReduce Olá em clusters HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="7ab56-115">Using a line ending of CRLF causes errors when running hello MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="7ab56-116">Olá `ssh` e `scp` comandos, ou [PowerShell do Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="7ab56-116">hello `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="7ab56-117">Contagem de palavras</span><span class="sxs-lookup"><span data-stu-id="7ab56-117">Word count</span></span>

<span data-ttu-id="7ab56-118">Este exemplo é uma contagem básica de palavras implementada em um Python usando um mapeador e um redutor.</span><span class="sxs-lookup"><span data-stu-id="7ab56-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="7ab56-119">Mapeador de saudação quebras de frase em palavras individuais e Redutor Olá agrega palavras hello e contagens de saída de hello tooproduce.</span><span class="sxs-lookup"><span data-stu-id="7ab56-119">hello mapper breaks sentences into individual words, and hello reducer aggregates hello words and counts tooproduce hello output.</span></span>

<span data-ttu-id="7ab56-120">Olá fluxograma a seguir ilustra o que acontece durante saudação e reduzir as fases.</span><span class="sxs-lookup"><span data-stu-id="7ab56-120">hello following flowchart illustrates what happens during hello map and reduce phases.</span></span>

![ilustração do processo de mapreduce Olá](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="7ab56-122">Transmissão do MapReduce</span><span class="sxs-lookup"><span data-stu-id="7ab56-122">Streaming MapReduce</span></span>

<span data-ttu-id="7ab56-123">Hadoop permite que você toospecify um arquivo que contém o mapa de saudação e reduzir a lógica que é usada por um trabalho.</span><span class="sxs-lookup"><span data-stu-id="7ab56-123">Hadoop allows you toospecify a file that contains hello map and reduce logic that is used by a job.</span></span> <span data-ttu-id="7ab56-124">requisitos específicos Olá Olá mapear e reduzir lógica são:</span><span class="sxs-lookup"><span data-stu-id="7ab56-124">hello specific requirements for hello map and reduce logic are:</span></span>

* <span data-ttu-id="7ab56-125">**Entrada**: Olá mapa e reduzir componentes devem ler dados de entrada de STDIN.</span><span class="sxs-lookup"><span data-stu-id="7ab56-125">**Input**: hello map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="7ab56-126">**Saída**: Olá mapa e reduzir componentes devem gravar tooSTDOUT de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="7ab56-126">**Output**: hello map and reduce components must write output data tooSTDOUT.</span></span>
* <span data-ttu-id="7ab56-127">**Formato de dados**: dados Olá consumido e produzido devem ser um par chave/valor, separado por um caractere de tabulação.</span><span class="sxs-lookup"><span data-stu-id="7ab56-127">**Data format**: hello data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="7ab56-128">Python facilmente possa lidar com esses requisitos usando Olá `sys` tooread do módulo de STDIN e usar `print` tooprint tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="7ab56-128">Python can easily handle these requirements by using hello `sys` module tooread from STDIN and using `print` tooprint tooSTDOUT.</span></span> <span data-ttu-id="7ab56-129">Olá tarefas restantes é simplesmente formatar Olá dados com uma guia (`\t`) caractere entre Olá chave e valor.</span><span class="sxs-lookup"><span data-stu-id="7ab56-129">hello remaining task is simply formatting hello data with a tab (`\t`) character between hello key and value.</span></span>

## <a name="create-hello-mapper-and-reducer"></a><span data-ttu-id="7ab56-130">Criar Redutor e mapeador Olá</span><span class="sxs-lookup"><span data-stu-id="7ab56-130">Create hello mapper and reducer</span></span>

1. <span data-ttu-id="7ab56-131">Crie um arquivo chamado `mapper.py` e use Olá seguindo o código como o conteúdo de saudação:</span><span class="sxs-lookup"><span data-stu-id="7ab56-131">Create a file named `mapper.py` and use hello following code as hello content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use hello sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read hello data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write tooSTDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="7ab56-132">Crie um arquivo chamado **reducer.py** e use Olá seguindo o código como o conteúdo de saudação:</span><span class="sxs-lookup"><span data-stu-id="7ab56-132">Create a file named **reducer.py** and use hello following code as hello content:</span></span>

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out hello separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read hello data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using hello word as hello key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull hello count(s) for hello word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write toostdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="7ab56-133">Executar usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ab56-133">Run using PowerShell</span></span>

<span data-ttu-id="7ab56-134">tooensure os arquivos tenham terminações de linha à direita do hello, Olá usar script do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ab56-134">tooensure that your files have hello right line endings, use hello following PowerShell script:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

<span data-ttu-id="7ab56-135">Usar Olá arquivos de saudação de tooupload de script do PowerShell a seguir, executar trabalho hello e exibir saída de hello:</span><span class="sxs-lookup"><span data-stu-id="7ab56-135">Use hello following PowerShell script tooupload hello files, run hello job, and view hello output:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="7ab56-136">Executar de uma sessão SSH</span><span class="sxs-lookup"><span data-stu-id="7ab56-136">Run from an SSH session</span></span>

1. <span data-ttu-id="7ab56-137">De seu ambiente de desenvolvimento em Olá mesmo diretório como `mapper.py` e `reducer.py` arquivos, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ab56-137">From your development environment, in hello same directory as `mapper.py` and `reducer.py` files, use hello following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="7ab56-138">Substituir `username` com nome de usuário SSH Olá para o cluster, e `clustername` com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="7ab56-138">Replace `username` with hello SSH user name for your cluster, and `clustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="7ab56-139">Este comando copia os arquivos de saudação do nó principal do toohello Olá sistema local.</span><span class="sxs-lookup"><span data-stu-id="7ab56-139">This command copies hello files from hello local system toohello head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7ab56-140">Se você usou uma senha toosecure sua conta SSH, você será solicitado a senha hello.</span><span class="sxs-lookup"><span data-stu-id="7ab56-140">If you used a password toosecure your SSH account, you are prompted for hello password.</span></span> <span data-ttu-id="7ab56-141">Se você usou uma chave SSH, você pode ter Olá toouse `-i` chave privada do toohello de caminho do parâmetro e hello.</span><span class="sxs-lookup"><span data-stu-id="7ab56-141">If you used an SSH key, you may have toouse hello `-i` parameter and hello path toohello private key.</span></span> <span data-ttu-id="7ab56-142">Por exemplo: `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="7ab56-142">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="7ab56-143">Conecte o cluster toohello usando SSH:</span><span class="sxs-lookup"><span data-stu-id="7ab56-143">Connect toohello cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="7ab56-144">Para obter mais informações a respeito, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7ab56-144">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="7ab56-145">reducer.py e tooensure Olá mapper.py têm Olá corrigir terminações de linha, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ab56-145">tooensure hello mapper.py and reducer.py have hello correct line endings, use hello following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="7ab56-146">Use Olá trabalho MapReduce do comando toostart Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="7ab56-146">Use hello following command toostart hello MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="7ab56-147">Esse comando tem Olá partes a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ab56-147">This command has hello following parts:</span></span>

   * <span data-ttu-id="7ab56-148">**hadoop-streaming.jar**: usado ao executar operações de transmissão do MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7ab56-148">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="7ab56-149">Ele interfaces Hadoop com código de MapReduce externo Olá que você fornecer.</span><span class="sxs-lookup"><span data-stu-id="7ab56-149">It interfaces Hadoop with hello external MapReduce code you provide.</span></span>

   * <span data-ttu-id="7ab56-150">**-arquivos**: adiciona Olá especificado do trabalho MapReduce arquivos toohello.</span><span class="sxs-lookup"><span data-stu-id="7ab56-150">**-files**: Adds hello specified files toohello MapReduce job.</span></span>

   * <span data-ttu-id="7ab56-151">**-Mapeador**: Hadoop informa quais arquivos toouse como Olá mapeador.</span><span class="sxs-lookup"><span data-stu-id="7ab56-151">**-mapper**: Tells Hadoop which file toouse as hello mapper.</span></span>

   * <span data-ttu-id="7ab56-152">**-Redutor**: Hadoop informa quais arquivos toouse como Olá Redutor.</span><span class="sxs-lookup"><span data-stu-id="7ab56-152">**-reducer**: Tells Hadoop which file toouse as hello reducer.</span></span>

   * <span data-ttu-id="7ab56-153">**-entrada**: arquivo de entrada hello que podemos deve contar palavras do.</span><span class="sxs-lookup"><span data-stu-id="7ab56-153">**-input**: hello input file that we should count words from.</span></span>

   * <span data-ttu-id="7ab56-154">**-saída**: diretório Olá Olá saída é gravado.</span><span class="sxs-lookup"><span data-stu-id="7ab56-154">**-output**: hello directory that hello output is written to.</span></span>

    <span data-ttu-id="7ab56-155">Como funciona o trabalho de MapReduce Olá, o processo de saudação é exibido como porcentagens.</span><span class="sxs-lookup"><span data-stu-id="7ab56-155">As hello MapReduce job works, hello process is displayed as percentages.</span></span>

        <span data-ttu-id="7ab56-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="7ab56-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="7ab56-157">Olá tooview de saída, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ab56-157">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="7ab56-158">Este comando exibe uma lista de palavras e quantas vezes o word Olá ocorreu.</span><span class="sxs-lookup"><span data-stu-id="7ab56-158">This command displays a list of words and how many times hello word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ab56-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7ab56-159">Next steps</span></span>

<span data-ttu-id="7ab56-160">Agora que você aprendeu como toouse streaming MapRedcue trabalhos com HDInsight, use Olá tooexplore links a seguir toowork outras maneiras com HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab56-160">Now that you have learned how toouse streaming MapRedcue jobs with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="7ab56-161">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ab56-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7ab56-162">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ab56-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7ab56-163">Usar trabalhos do MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ab56-163">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
