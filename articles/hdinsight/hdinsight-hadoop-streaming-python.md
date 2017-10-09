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
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a>Desenvolver programas MapReduce de streaming do Python para o HDInsight

Saiba como toouse Python em MapReduce operações de fluxo contínuo. Hadoop fornece uma API de streaming para MapReduce que permite que você toowrite mapa e reduzir as funções em idiomas diferentes do Java. Olá etapas deste documento implementam Olá mapa e reduzem componentes em Python.

## <a name="prerequisites"></a>Pré-requisitos

* Um Hadoop baseado em Linux no cluster HDInsight

  > [!IMPORTANT]
  > etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Um editor de texto

  > [!IMPORTANT]
  > editor de texto de saudação deve usar LF terminação de linha de saudação. Usar uma terminação de linha de CRLF causa erros durante a execução do trabalho MapReduce Olá em clusters HDInsight baseados em Linux.

* Olá `ssh` e `scp` comandos, ou [PowerShell do Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)

## <a name="word-count"></a>Contagem de palavras

Este exemplo é uma contagem básica de palavras implementada em um Python usando um mapeador e um redutor. Mapeador de saudação quebras de frase em palavras individuais e Redutor Olá agrega palavras hello e contagens de saída de hello tooproduce.

Olá fluxograma a seguir ilustra o que acontece durante saudação e reduzir as fases.

![ilustração do processo de mapreduce Olá](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a>Transmissão do MapReduce

Hadoop permite que você toospecify um arquivo que contém o mapa de saudação e reduzir a lógica que é usada por um trabalho. requisitos específicos Olá Olá mapear e reduzir lógica são:

* **Entrada**: Olá mapa e reduzir componentes devem ler dados de entrada de STDIN.
* **Saída**: Olá mapa e reduzir componentes devem gravar tooSTDOUT de dados de saída.
* **Formato de dados**: dados Olá consumido e produzido devem ser um par chave/valor, separado por um caractere de tabulação.

Python facilmente possa lidar com esses requisitos usando Olá `sys` tooread do módulo de STDIN e usar `print` tooprint tooSTDOUT. Olá tarefas restantes é simplesmente formatar Olá dados com uma guia (`\t`) caractere entre Olá chave e valor.

## <a name="create-hello-mapper-and-reducer"></a>Criar Redutor e mapeador Olá

1. Crie um arquivo chamado `mapper.py` e use Olá seguindo o código como o conteúdo de saudação:

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

2. Crie um arquivo chamado **reducer.py** e use Olá seguindo o código como o conteúdo de saudação:

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

## <a name="run-using-powershell"></a>Executar usando PowerShell

tooensure os arquivos tenham terminações de linha à direita do hello, Olá usar script do PowerShell a seguir:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

Usar Olá arquivos de saudação de tooupload de script do PowerShell a seguir, executar trabalho hello e exibir saída de hello:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a>Executar de uma sessão SSH

1. De seu ambiente de desenvolvimento em Olá mesmo diretório como `mapper.py` e `reducer.py` arquivos, use Olá comando a seguir:

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    Substituir `username` com nome de usuário SSH Olá para o cluster, e `clustername` com nome de saudação do cluster.

    Este comando copia os arquivos de saudação do nó principal do toohello Olá sistema local.

    > [!NOTE]
    > Se você usou uma senha toosecure sua conta SSH, você será solicitado a senha hello. Se você usou uma chave SSH, você pode ter Olá toouse `-i` chave privada do toohello de caminho do parâmetro e hello. Por exemplo: `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.

2. Conecte o cluster toohello usando SSH:

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    Para obter mais informações a respeito, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. reducer.py e tooensure Olá mapper.py têm Olá corrigir terminações de linha, use Olá comandos a seguir:

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. Use Olá trabalho MapReduce do comando toostart Olá a seguir.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    Esse comando tem Olá partes a seguir:

   * **hadoop-streaming.jar**: usado ao executar operações de transmissão do MapReduce. Ele interfaces Hadoop com código de MapReduce externo Olá que você fornecer.

   * **-arquivos**: adiciona Olá especificado do trabalho MapReduce arquivos toohello.

   * **-Mapeador**: Hadoop informa quais arquivos toouse como Olá mapeador.

   * **-Redutor**: Hadoop informa quais arquivos toouse como Olá Redutor.

   * **-entrada**: arquivo de entrada hello que podemos deve contar palavras do.

   * **-saída**: diretório Olá Olá saída é gravado.

    Como funciona o trabalho de MapReduce Olá, o processo de saudação é exibido como porcentagens.

        15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%


5. Olá tooview de saída, use Olá comando a seguir:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Este comando exibe uma lista de palavras e quantas vezes o word Olá ocorreu.

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como toouse streaming MapRedcue trabalhos com HDInsight, use Olá tooexplore links a seguir toowork outras maneiras com HDInsight do Azure.

* [Usar o Hive com o HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com o HDInsight](hdinsight-use-pig.md)
* [Usar trabalhos do MapReduce com o HDInsight](hdinsight-use-mapreduce.md)
