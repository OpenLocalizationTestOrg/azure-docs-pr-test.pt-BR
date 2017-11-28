---
title: "Desenvolver trabalhos MapReduce de streaming do Python com o HDInsight – Azure | Microsoft Docs"
description: Saiba como usar o Python no streaming para trabalhos de MapReduce. O Hadoop fornece uma API de streaming para MapReduce para escrever em linguagens diferentes do Java.
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
ms.openlocfilehash: b86605c49291a99f49c4b2841d46324cfd0db56d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="7e37b-104">Desenvolver programas MapReduce de streaming do Python para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e37b-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="7e37b-105">Saiba como usar o Python no streaming para operações do MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7e37b-105">Learn how to use Python in streaming MapReduce operations.</span></span> <span data-ttu-id="7e37b-106">O Hadoop fornece uma API de streaming para o MapReduce que permite que você escreva funções de mapeamento e redução em outras linguagens além do Java.</span><span class="sxs-lookup"><span data-stu-id="7e37b-106">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="7e37b-107">As etapas neste documento implementam os componentes Map e Reduce em Python.</span><span class="sxs-lookup"><span data-stu-id="7e37b-107">The steps in this document implement the Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e37b-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7e37b-108">Prerequisites</span></span>

* <span data-ttu-id="7e37b-109">Um Hadoop baseado em Linux no cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e37b-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7e37b-110">As etapas deste documento exigem um cluster HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="7e37b-110">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="7e37b-111">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="7e37b-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7e37b-112">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7e37b-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7e37b-113">Um editor de texto</span><span class="sxs-lookup"><span data-stu-id="7e37b-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7e37b-114">O editor de texto deve usar LF com fim de linha.</span><span class="sxs-lookup"><span data-stu-id="7e37b-114">The text editor must use LF as the line ending.</span></span> <span data-ttu-id="7e37b-115">Usar CRLF como terminação de linha causará erros ao executar o trabalho MapReduce em clusters HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="7e37b-115">Using a line ending of CRLF causes errors when running the MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="7e37b-116">Os comandos `ssh` e `scp` ou o [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="7e37b-116">The `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="7e37b-117">Contagem de palavras</span><span class="sxs-lookup"><span data-stu-id="7e37b-117">Word count</span></span>

<span data-ttu-id="7e37b-118">Este exemplo é uma contagem básica de palavras implementada em um Python usando um mapeador e um redutor.</span><span class="sxs-lookup"><span data-stu-id="7e37b-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="7e37b-119">O mapeador divide frases em palavras individuais e o redutor agrega as palavras e contagens para produzir a saída.</span><span class="sxs-lookup"><span data-stu-id="7e37b-119">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span></span>

<span data-ttu-id="7e37b-120">O fluxograma a seguir ilustra o que acontece durante o mapa e reduz as fases.</span><span class="sxs-lookup"><span data-stu-id="7e37b-120">The following flowchart illustrates what happens during the map and reduce phases.</span></span>

![ilustração do processo do mapreduce](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="7e37b-122">Transmissão do MapReduce</span><span class="sxs-lookup"><span data-stu-id="7e37b-122">Streaming MapReduce</span></span>

<span data-ttu-id="7e37b-123">O Hadoop permite que você especifique um arquivo que contém o mapa e a lógica de redução usada por um trabalho.</span><span class="sxs-lookup"><span data-stu-id="7e37b-123">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span></span> <span data-ttu-id="7e37b-124">Os requisitos específicos para o mapa e lógica de redução são:</span><span class="sxs-lookup"><span data-stu-id="7e37b-124">The specific requirements for the map and reduce logic are:</span></span>

* <span data-ttu-id="7e37b-125">**Entrada**- os componentes mapa e reduzir devem ler dados de entrada de STDIN.</span><span class="sxs-lookup"><span data-stu-id="7e37b-125">**Input**: The map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="7e37b-126">**Saída**- os componentes mapa e reduzir devem gravar os dados de saída para STDOUT.</span><span class="sxs-lookup"><span data-stu-id="7e37b-126">**Output**: The map and reduce components must write output data to STDOUT.</span></span>
* <span data-ttu-id="7e37b-127">**Formato de dados**- os dados consumidos e produzidos devem ser um par chave/valor, separado por um caractere de tabulação.</span><span class="sxs-lookup"><span data-stu-id="7e37b-127">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="7e37b-128">O Python pode facilmente atender a esses requisitos usando o módulo `sys` para ler do STDIN e usando `print` para imprimir para o STDOUT.</span><span class="sxs-lookup"><span data-stu-id="7e37b-128">Python can easily handle these requirements by using the `sys` module to read from STDIN and using `print` to print to STDOUT.</span></span> <span data-ttu-id="7e37b-129">O restante é simplesmente formatar os dados com um caractere de tabulação (`\t`) entre a chave e o valor.</span><span class="sxs-lookup"><span data-stu-id="7e37b-129">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span></span>

## <a name="create-the-mapper-and-reducer"></a><span data-ttu-id="7e37b-130">Criar o mapeador e redutor</span><span class="sxs-lookup"><span data-stu-id="7e37b-130">Create the mapper and reducer</span></span>

1. <span data-ttu-id="7e37b-131">Crie um arquivo chamado `mapper.py` e use o seguinte código como o conteúdo:</span><span class="sxs-lookup"><span data-stu-id="7e37b-131">Create a file named `mapper.py` and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use the sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read the data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write to STDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="7e37b-132">Crie um arquivo chamado **reducer.py** e use o seguinte código como o conteúdo:</span><span class="sxs-lookup"><span data-stu-id="7e37b-132">Create a file named **reducer.py** and use the following code as the content:</span></span>

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
           # Strip out the separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read the data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using the word as the key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull the count(s) for the word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write to stdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="7e37b-133">Executar usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e37b-133">Run using PowerShell</span></span>

<span data-ttu-id="7e37b-134">Para assegurar que os arquivos tenham as terminações de linha corretas, use o seguinte script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7e37b-134">To ensure that your files have the right line endings, use the following PowerShell script:</span></span>

<span data-ttu-id="7e37b-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span><span class="sxs-lookup"><span data-stu-id="7e37b-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span></span>

<span data-ttu-id="7e37b-136">Use o seguinte script do PowerShell para carregar os arquivos, execute o trabalho e exiba a saída:</span><span class="sxs-lookup"><span data-stu-id="7e37b-136">Use the following PowerShell script to upload the files, run the job, and view the output:</span></span>

<span data-ttu-id="7e37b-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span><span class="sxs-lookup"><span data-stu-id="7e37b-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span></span>

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="7e37b-138">Executar de uma sessão SSH</span><span class="sxs-lookup"><span data-stu-id="7e37b-138">Run from an SSH session</span></span>

1. <span data-ttu-id="7e37b-139">No ambiente de desenvolvimento, no mesmo diretório dos arquivos `mapper.py` e `reducer.py`, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7e37b-139">From your development environment, in the same directory as `mapper.py` and `reducer.py` files, use the following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="7e37b-140">Substitua `username` pelo nome de usuário do SSH do cluster e substitua `clustername` pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="7e37b-140">Replace `username` with the SSH user name for your cluster, and `clustername` with the name of your cluster.</span></span>

    <span data-ttu-id="7e37b-141">Esse comando copia os arquivos do sistema local para o nó principal.</span><span class="sxs-lookup"><span data-stu-id="7e37b-141">This command copies the files from the local system to the head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7e37b-142">Se você tiver usado uma senha para proteger sua conta SSH, será solicitado que você forneça essa senha.</span><span class="sxs-lookup"><span data-stu-id="7e37b-142">If you used a password to secure your SSH account, you are prompted for the password.</span></span> <span data-ttu-id="7e37b-143">Se você usou uma chave SSH, talvez precise usar o parâmetro `-i` e o caminho para a chave privada.</span><span class="sxs-lookup"><span data-stu-id="7e37b-143">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span></span> <span data-ttu-id="7e37b-144">Por exemplo: `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="7e37b-144">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="7e37b-145">Conecte-se ao cluster usando o SSH:</span><span class="sxs-lookup"><span data-stu-id="7e37b-145">Connect to the cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="7e37b-146">Para obter mais informações a respeito, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7e37b-146">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="7e37b-147">Para assegurar que mapper.py e reducer.py têm as terminações de linha corretas, use os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7e37b-147">To ensure the mapper.py and reducer.py have the correct line endings, use the following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="7e37b-148">Use o seguinte comando para iniciar o trabalho MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7e37b-148">Use the following command to start the MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="7e37b-149">Esse comando tem as seguintes partes:</span><span class="sxs-lookup"><span data-stu-id="7e37b-149">This command has the following parts:</span></span>

   * <span data-ttu-id="7e37b-150">**hadoop-streaming.jar**: usado ao executar operações de transmissão do MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7e37b-150">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="7e37b-151">Faz interfaces do Hadoop com o código externo do MapReduce fornecido por você.</span><span class="sxs-lookup"><span data-stu-id="7e37b-151">It interfaces Hadoop with the external MapReduce code you provide.</span></span>

   * <span data-ttu-id="7e37b-152">**-files**: adiciona os arquivos especificados ao trabalho MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7e37b-152">**-files**: Adds the specified files to the MapReduce job.</span></span>

   * <span data-ttu-id="7e37b-153">**-mapper**: informa o Hadoop qual arquivo usar como mapeador.</span><span class="sxs-lookup"><span data-stu-id="7e37b-153">**-mapper**: Tells Hadoop which file to use as the mapper.</span></span>

   * <span data-ttu-id="7e37b-154">**-reducer**: informa o Hadoop qual arquivo usar como redutor.</span><span class="sxs-lookup"><span data-stu-id="7e37b-154">**-reducer**: Tells Hadoop which file to use as the reducer.</span></span>

   * <span data-ttu-id="7e37b-155">**-input**: o arquivo de entrada por meio do qual devemos contar palavras.</span><span class="sxs-lookup"><span data-stu-id="7e37b-155">**-input**: The input file that we should count words from.</span></span>

   * <span data-ttu-id="7e37b-156">**-output**: o diretório no qual a saída é gravada.</span><span class="sxs-lookup"><span data-stu-id="7e37b-156">**-output**: The directory that the output is written to.</span></span>

    <span data-ttu-id="7e37b-157">Conforme o trabalho MapReduce é realizado, o processo é exibido como percentuais.</span><span class="sxs-lookup"><span data-stu-id="7e37b-157">As the MapReduce job works, the process is displayed as percentages.</span></span>

        <span data-ttu-id="7e37b-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="7e37b-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="7e37b-159">Para exibir a saída, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7e37b-159">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="7e37b-160">Esse comando exibe uma lista de palavras e o número de ocorrências da palavra.</span><span class="sxs-lookup"><span data-stu-id="7e37b-160">This command displays a list of words and how many times the word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e37b-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7e37b-161">Next steps</span></span>

<span data-ttu-id="7e37b-162">Agora que você aprendeu a usar a transmissão de trabalhos MapReduce com o HDInsight, use os links abaixo para explorar outras maneiras de trabalhar com o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e37b-162">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="7e37b-163">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e37b-163">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7e37b-164">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e37b-164">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7e37b-165">Usar trabalhos do MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e37b-165">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
