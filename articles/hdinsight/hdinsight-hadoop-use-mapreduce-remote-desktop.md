---
title: "aaaMapReduce e área de trabalho remota com Hadoop no HDInsight - Azure | Microsoft Docs"
description: "Saiba como toouse área de trabalho remota tooconnect tooHadoop no HDInsight e executados trabalhos de MapReduce."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a>Usar o MapReduce no Hadoop no HDInsight com Remote Desktop
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Neste artigo, você saiba como tooconnect tooa Hadoop no HDInsight cluster usando a área de trabalho remota e, em seguida, executar trabalhos de MapReduce usando o comando do Hadoop hello.

> [!IMPORTANT]
> A Área de Trabalho Remota está disponível somente em clusters HDInsight baseados no Windows. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Para HDInsight 3.4 ou superior, consulte [Use MapReduce com SSH](hdinsight-hadoop-use-mapreduce-ssh.md) para obter informações sobre como conectar-se o cluster do HDInsight toohello e executar trabalhos de MapReduce.

## <a id="prereq"></a>Pré-requisitos
toocomplete Olá etapas neste artigo, você precisará seguir hello:

* Um cluster HDInsight baseado em Windows (Hadoop no HDInsight)
* Um computador cliente executando o Windows 7, Windows 8 ou Windows 10

## <a id="connect"></a>Conectar com a área de trabalho remota
Habilitar área de trabalho remota para o cluster do HDInsight hello e conecte tooit seguindo as instruções de saudação em [conectar tooHDInsight clusters usando o RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hadoop"></a>Use o comando do Hadoop Olá
Quando você estiver toohello conectado a área de trabalho para o cluster do HDInsight hello, use Olá seguindo as etapas toorun um trabalho de MapReduce usando o comando do Hadoop hello:

1. Na área de trabalho do HDInsight hello, iniciar Olá **linha de comando do Hadoop**. Isso abre um novo prompt de comando no hello **c:\apps\dist\hadoop-&lt;o número de versão >** directory.

   > [!NOTE]
   > número de versão de Hello muda conforme Hadoop é atualizada. Olá **HADOOP_HOME** variável de ambiente pode ser o caminho de saudação do toofind usado. Por exemplo, `cd %HADOOP_HOME%` alterações diretórios toohello Hadoop diretório, sem a necessidade de número de versão tooknow hello.
   >
   >
2. Olá toouse **Hadoop** toorun um trabalho de MapReduce do exemplo de comando, use Olá comando a seguir:

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    Isso inicia o hello **wordcount** classe, que está contida no hello **Hadoop-Examples.jar mapreduce** arquivo no diretório atual hello. Como entrada, ele usa Olá **wasb://example/data/gutenberg/davinci.txt** documento e a saída é armazenado em: **wasb: / / / exemplo/dados/WordCountOutput**.

   > [!NOTE]
   > Para obter mais informações sobre esses dados de exemplo de trabalho e hello MapReduce, consulte <a href="hdinsight-use-mapreduce.md">Use MapReduce em HDInsight Hadoop</a>.
   >
   >
3. trabalho de saudação emite detalhes como ela é processada e retorna a seguir toohello semelhante informações quando Olá trabalho for concluído:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. Quando o trabalho de saudação for concluído, use Olá seguindo os arquivos de saída do comando toolist Olá armazenados no **wasb://example/data/WordCountOutput**:

        hadoop fs -ls wasb:///example/data/WordCountOutput

    Isso deve exibir dois arquivos, **_SUCCESS** e **part-r-00000**. Olá **parte-r-00000** arquivo contém a saída Olá para este trabalho.

   > [!NOTE]
   > Alguns trabalhos de MapReduce podem dividir os resultados de saudação em várias **parte-r-# # #** arquivos. Nesse caso, use Olá # # # sufixo de ordem de saudação tooindicate dos arquivos de saudação.
   >
   >
5. Olá tooview de saída, use Olá comando a seguir:

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    Isso exibe uma lista de palavras de saudação que estão contidos em Olá **wasb://example/data/gutenberg/davinci.txt** arquivo, juntamente com o número de saudação de vezes que cada palavra ocorreu. a seguir Olá é um exemplo de dados de saudação que estarão contidos no arquivo hello:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Resumo
Como você pode ver, o hello Hadoop comando fornece um toorun de maneira fácil trabalhos MapReduce em um cluster HDInsight e exibir saída de trabalho de saudação.

## <a id="nextsteps"></a>Próximas etapas
Para obter informações gerais sobre trabalhos de MapReduce no HDInsight:

* [Usar o MapReduce no Hadoop do HDInsight](hdinsight-use-mapreduce.md)

Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)
