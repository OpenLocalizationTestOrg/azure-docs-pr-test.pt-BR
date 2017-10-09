---
title: "aaaMapReduce e conexão SSH com Hadoop no HDInsight - Azure | Microsoft Docs"
description: Saiba como toouse SSH toorun MapReduce trabalhos usando Hadoop no HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a>Usar o MapReduce com Hadoop no HDInsight com SSH

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Saiba como toosubmit MapReduce trabalhos um tooHDInsight de conexão Secure Shell (SSH).

> [!NOTE]
> Se você já estiver familiarizado com o uso de Hadoop baseado em Linux servidores, mas você tooHDInsight novo, consulte [HDInsight baseados em Linux dicas](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Pré-requisitos

* Um cluster do HDInsight baseado em Linux (Hadoop no HDInsight)

  > [!IMPORTANT]
  > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Um cliente SSH. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a id="ssh"></a>Conexão com o SSH

Conecte-se toohello cluster usando o SSH. Por exemplo, a saudação comando a seguir conecta tooa cluster denominado **myhdinsight**:

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

**Se você usar uma chave de certificado para autenticação de SSH**, talvez seja necessário toospecify local de saudação da chave privada Olá no sistema cliente, por exemplo:

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

**Se você usar uma senha para autenticação de SSH**, você precisa tooprovide Olá senha quando solicitado.

Para saber mais sobre como usar o SSH com HDInsight, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="hadoop"></a>Usar comandos Hadoop

1. Depois de cluster do HDInsight toohello conectado, use Olá comando toostart um trabalho de MapReduce a seguir:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    Esse comando inicia Olá `wordcount` classe, que está contida no hello `hadoop-mapreduce-examples.jar` arquivo. Ele usa Olá `/example/data/gutenberg/davinci.txt` documento como entrada e saída é armazenado em `/example/data/WordCountOutput`.

    > [!NOTE]
    > Para obter mais informações sobre esses dados de exemplo de trabalho e hello MapReduce, consulte [Use MapReduce no Hadoop no HDInsight](hdinsight-use-mapreduce.md).

2. trabalho de saudação emite detalhes como ele processa e retorna informações toohello semelhante texto a seguir quando Olá trabalho for concluído:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. Olá trabalho for concluído, use Olá arquivos de saída do comando toolist Olá a seguir:

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    Esse comando exibe dois arquivos, `_SUCCESS` e `part-r-00000`. Olá `part-r-00000` arquivo contém a saída Olá para este trabalho.

    > [!NOTE]
    > Alguns trabalhos de MapReduce podem dividir os resultados de saudação em várias **parte-r-# # #** arquivos. Nesse caso, use Olá # # # sufixo de ordem de saudação tooindicate dos arquivos de saudação.

4. Olá tooview de saída, use Olá comando a seguir:

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    Este comando exibe uma lista de palavras de saudação que estão contidos em Olá **wasb://example/data/gutenberg/davinci.txt** arquivo e Olá o número de vezes que cada palavra ocorreu. Olá, texto a seguir é um exemplo de dados Olá contidos no arquivo hello:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Resumo

Como você pode ver, o Hadoop comandos fornecem toorun uma maneira fácil trabalhos MapReduce em um cluster HDInsight e exibir saída de trabalho hello.

## <a id="nextsteps"></a>Próximas etapas

Para obter informações gerais sobre trabalhos de MapReduce no HDInsight:

* [Usar o MapReduce no Hadoop do HDInsight](hdinsight-use-mapreduce.md)

Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)
