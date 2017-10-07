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
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a>Executar Olá MapReduce exemplos incluídos no HDInsight

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Saiba como exemplos de MapReduce Olá toorun incluídos com Hadoop no HDInsight.

## <a name="prerequisites"></a>Pré-requisitos

* **Um cluster HDInsight**: consulte [Introdução ao uso do Hadoop com o Hive no HDInsight no Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

    > [!IMPORTANT]
    > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Um cliente SSH**: para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="hello-mapreduce-examples"></a>exemplos de MapReduce Olá

**Local**: Olá exemplos estão localizados em Olá cluster HDInsight no `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.

**Conteúdo**: Olá exemplos a seguir está contido neste arquivo:

* `aggregatewordcount`: Uma agregação com base em programa mapreduce que conta Olá palavras nos arquivos de entrada hello.
* `aggregatewordhist`: Uma agregação com base em programa mapreduce que calcula o histograma Olá palavras Olá nos arquivos de entrada hello.
* `bbp`: Um programa mapreduce que usa Bailey-Borwein-Plouffe toocompute exatos dígitos de Pi.
* `dbcount`: Um trabalho de exemplo que conta logs de página Olá armazenados em um banco de dados.
* `distbbp`: Um programa mapreduce que usa uma fórmula toocompute de BBP tipo exato bits de Pi.
* `grep`: Um programa mapreduce que conta Olá faz a correspondência de um regex na entrada hello.
* `join`: um trabalho que faz a união de bancos de dados classificados, particionados igualmente.
* `multifilewc`: um trabalho que conta palavras de vários arquivos.
* `pentomino`: Um bloco de mapreduce layout soluções do programa toofind toopentomino problemas.
* `pi`: um programa de MapReduce que estima Pi usando um método semelhante ao de Monte Carlo.
* `randomtextwriter`: um programa de MapReduce que grava 10 GB de dados textuais aleatórios por nó.
* `randomwriter`: um programa de MapReduce que grava 10 GB de dados aleatórios por nó.
* `secondarysort`: Um exemplo definindo uma classificação secundária toohello reduzir fase.
* `sort`: Um programa mapreduce que classifica dados Olá gravados pelo gravador aleatório hello.
* `sudoku`: um solucionador de sudoku.
* `teragen`: Gere dados para terasort hello.
* `terasort`: Execute terasort hello.
* `teravalidate`: verifica os resultados do terasort.
* `wordcount`: Um programa mapreduce que conta Olá palavras nos arquivos de entrada hello.
* `wordmean`: Um programa mapreduce que conta o comprimento médio de saudação de palavras Olá nos arquivos de entrada hello.
* `wordmedian`: Arquivos de entrada um programa mapreduce que conta o comprimento médio de saudação de palavras Olá Olá.
* `wordstandarddeviation`: Arquivos de entrada um programa mapreduce que conta o desvio padrão de saudação de comprimento de saudação do palavras Olá Olá.

**Código-fonte**: código-fonte para esses exemplos está incluído na Olá cluster HDInsight no `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.

> [!NOTE]
> Olá `2.2.4.9-1` no hello caminho é versão de saudação do hello Hortonworks Data Platform para o cluster do HDInsight hello e pode ser diferente para seu cluster.

## <a name="run-hello-wordcount-example"></a>Executar o exemplo de wordcount hello

1. Conecte-se tooHDInsight usando o SSH. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. De saudação `username@#######:~$` prompt, use Olá exemplos do comando toolist Olá a seguir:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    Este comando gera a lista de saudação do exemplo da seção anterior Olá deste documento.

3. Saudação de uso após o comando tooget ajuda sobre um exemplo específico. Nesse caso, Olá **wordcount** exemplo:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    Você receberá a seguinte mensagem de saudação:

        Usage: wordcount <in> [<in>...] <out>

    Esta mensagem indica que você pode fornecer vários caminhos de entrada para documentos de origem hello. caminho de final de saudação é onde a saída de hello (contagem de palavras em documentos de origem Olá) é armazenada.

4. Use Olá toocount a seguir todas as palavras Olá blocos de anotações de Leonardo Da Vinci, que são fornecidos como dados de exemplo com o cluster:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    A entrada para esse trabalho é lida pela entrada `/example/data/gutenberg/davinci.txt`. A saída desse exemplo é armazenada em `/example/data/davinciwordcount`. Ambos os caminhos estão localizados no armazenamento padrão para o cluster hello, sistema de arquivos local do hello.

   > [!NOTE]
   > Conforme observado na Ajuda da saudação para exemplo de wordcount hello, você também pode especificar vários arquivos de entrada. Por exemplo, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` contaria as palavras em davinci.txt e ulysses.txt.

5. Após a conclusão do trabalho hello, use Olá saída do comando tooview Olá a seguir:

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    Este comando concatena todos os arquivos de saída de hello produzidos pelo trabalho de saudação. Ele exibe o console do hello saída toohello. saudação de saída é similar toohello texto a seguir:

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    Cada linha representa uma palavra e dados de entrada de número de vezes que ocorreu no hello.

## <a name="hello-sudoku-example"></a>exemplo de Sudoku Hello

[Sudoku](https://en.wikipedia.org/wiki/Sudoku) é um quebra-cabeça lógico composto por nove grades de 3x3. Algumas células na grade de saudação têm números, enquanto outros são em branco, e a meta de saudação é toosolve para células em branco hello. link anterior Olá tem mais informações sobre quebra-cabeça de hello, mas finalidade deste exemplo hello é toosolve para células em branco hello. Portanto, nossa entrada deve ser um arquivo que está no hello formato a seguir:

* Nove linhas de nove colunas
* Cada coluna pode conter um número ou `?` (que indica uma célula em branco)
* As células são separadas por um espaço

Há um determinado tooconstruct de maneira quebra-cabeças Sudoku; Você não pode repetir um número em uma coluna ou linha. Há um exemplo no cluster HDInsight Olá que é construído corretamente. Ele está localizado em `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` e contém Olá texto a seguir:

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

toorun esse problema de exemplo por meio de saudação Sudoku exemplo, use Olá seguinte comando:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

resultados de saudação aparecem semelhante toohello texto a seguir:

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a>Exemplo de pi (π)

exemplo de pi Hello usa uma estatística (quase Monte Carlo) valor de saudação do método tooestimate de pi. Pontos são colocados aleatoriamente em um quadrado de unidade. Quadrado Olá também contém um círculo. probabilidade de que os pontos de saudação se enquadra círculo Olá Olá são área toohello igual de saudação círculo, pi/4. valor de saudação de pi pode ser estimada do valor de saudação do 4R. R é a taxa de saudação do número de saudação de pontos que estão dentro de saudação círculo toohello número total de pontos que estão dentro do quadrado hello. Olá exemplo a saudação maior de pontos usados, melhor estimativa de Olá Olá é.

Use este exemplo de hello toorun de comando a seguir. Esse comando usa 16 mapas com valor de saudação tooestimate 10.000.000 exemplos de pi:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

Olá valor retornado por este comando é semelhante muito**3.14159155000000000000**. Para obter referências, hello 10 primeiros casas decimais de pi são 3.1415926535.

## <a name="10-gb-greysort-example"></a>Exemplo de GraySort de 10 GB

GraySort é um tipo de parâmetro de comparação. métrica de saudação é a taxa de classificação de hello (TB por minuto) que é obtida durante a classificação de grandes quantidades de dados, geralmente um 100 TB mínimo.

Este exemplo usa uma quantidade modesta de 10 GB de dados para que possa ser executado de modo relativamente rápido. Ele usa os aplicativos de MapReduce Olá desenvolvidos por Owen O'Malley e Arun Murthy. Esses aplicativos ganhou o parâmetro de comparação do hello anual para fins gerais ("daytona") terabyte classificação em 2009, com uma taxa de 0.578 TB/min (100 TB em 173 minutos). Para obter mais informações sobre este e outros parâmetros de comparação de classificação, consulte Olá [Sortbenchmark](http://sortbenchmark.org/) site.

Este exemplo usa três conjuntos de programas MapReduce:

* **TeraGen**: MapReduce um programa que gera linhas de dados toosort

* **TeraSort**: exemplos de dados de entrada hello e usa dados de saudação do MapReduce toosort em uma ordem de total

    A TeraSort é uma classificação de MapReduce padrão, exceto por um particionador personalizado. o particionador Olá usa uma lista classificada de chaves de n-1 de amostra que definem o intervalo de chave Olá para cada reduza. Em particular, todas as chaves de tal que exemplo [i-1] < = chave < exemplo [i] são enviadas tooreduce i. Este particionador garantias de saídas de saudação do reduzem i são todos com menos de reduzir a saída de saudação do i + 1.

* **TeraValidate**: programa MapReduce A valida essa saída Olá global é classificado

    Ele cria um mapa por arquivo no diretório de saída de hello e cada mapa garante que cada chave é menor ou igual a toohello anterior. função de mapa Hello gera registros de saudação primeiro e último chaves de cada arquivo. Olá reduzir função garante que Olá primeira chave de arquivo i é maior que a chave do último Olá de i-1 de arquivo. Todos os problemas são relatados como uma saída de hello reduzir fase, com as chaves de saudação que estão fora de ordem.

Toogenerate dados, as etapas a seguir do uso Olá classificar e, em seguida, validar a saída de hello:

1. Gerar 10 GB de dados, que é o armazenamento padrão do cluster do HDInsight toohello armazenado em `/example/data/10GB-sort-input`:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    Olá `-Dmapred.map.tasks` informa quantos toouse tarefas de mapa para este trabalho de Hadoop. Olá final dois parâmetros instruem o hello trabalho toocreate 10 GB de dados e toostore-lo em `/example/data/10GB-sort-input`.

2. Saudação de usar dados de saudação do toosort de comando a seguir:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    Olá `-Dmapred.reduce.tasks` informa Hadoop reduzem quantas tarefas toouse para trabalho hello. parâmetros de saudação final dois são Olá apenas de entrada e locais para dados de saída.

3. Use Olá seguintes toovalidate Olá dados gerados por classificação hello:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a>Próximas etapas

Neste artigo, você aprendeu como exemplos de saudação toorun incluídos com hello clusters HDInsight baseados em Linux. Para tutoriais sobre como usar o Pig, Hive e MapReduce com HDInsight, consulte Olá seguintes tópicos:

* [Usar o Pig com Hadoop no HDInsight][hdinsight-use-pig]
* [Usar o Hive com Hadoop no HDInsight][hdinsight-use-hive]
* [Usar o MapReduce com Hadoop no HDInsight][hdinsight-use-mapreduce]

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
