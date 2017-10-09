---
title: "aaaUse Pig do Hadoop com área de trabalho remota no HDInsight - Azure | Microsoft Docs"
description: "Saiba como toouse Olá Pig comando toorun Pig latino as instruções de um área de trabalho remota conexão tooa baseados no Windows de cluster Hadoop no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a>Executar trabalhos do Pig por meio de uma conexão de área de trabalho remota
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Este documento fornece um passo a passo para usar o hello Pig comando toorun Pig latino as instruções de um cluster HDInsight baseados no Windows de tooa de conexão de área de trabalho remota. Latino pig permite que aplicativos de MapReduce toocreate descrevendo as transformações de dados, em vez de mapear e reduzir as funções.

> [!IMPORTANT]
> Área de trabalho remota só está disponível em clusters de HDInsight que usam o Windows como sistema operacional de saudação. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Para HDInsight 3.4 ou superior, consulte [usar o Pig com HDInsight e SSH](hdinsight-hadoop-use-pig-ssh.md) para obter informações sobre como executar interativamente Pig trabalhos diretamente no saudação do cluster de uma linha de comando.

## <a id="prereq"></a>Pré-requisitos
toocomplete Olá etapas neste artigo, você precisará seguir hello.

* Um cluster HDInsight baseado em Windows (Hadoop no HDInsight)
* Um computador cliente executando o Windows 7, Windows 8 ou Windows 10

## <a id="connect"></a>Conectar com a área de trabalho remota
Habilitar área de trabalho remota para o cluster do HDInsight hello e conecte tooit seguindo as instruções de saudação em [conectar tooHDInsight clusters usando o RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="pig"></a>Use o comando de Pig de saudação
1. Depois que você tiver uma conexão de área de trabalho remota, inicie Olá **linha de comando do Hadoop** usando o ícone de saudação na área de trabalho de saudação.
2. Use Olá toostart Olá Pig comando a seguir:

        %pig_home%\bin\pig

    Você verá um prompt `grunt>` .
3. Digite hello instrução a seguir:

        LOGS = LOAD 'wasb:///example/data/sample.log';

    Esse comando carrega conteúdo de saudação do arquivo de sample.log de saudação no arquivo de LOGS de saudação. Você pode exibir o conteúdo de saudação do arquivo hello usando Olá comando a seguir:

        DUMP LOGS;
4. Transforme dados saudação aplicando um nível de log de saudação somente tooextract de expressão regular de cada registro:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Você pode usar **DESPEJAR** dados de saudação tooview após a transformação de saudação. Nesse caso, `DUMP LEVELS;`.
5. Continue a aplicar transformações usando Olá instruções a seguir. Use `DUMP` tooview resultados de saudação da transformação Olá depois de cada etapa.

    <table>
    <tr>
    <th>Instrução</th><th>O que faz</th>
    </tr>
    <tr>
    <td>FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</td><td>Remove as linhas que contêm um valor nulo para o nível de log hello e armazena os resultados de saudação em FILTEREDLEVELS.</td>
    </tr>
    <tr>
    <td>GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</td><td>Olá grupos linhas por nível de log e armazena os resultados de saudação em GROUPEDLEVELS.</td>
    </tr>
    <tr>
    <td>FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</td><td>Cria um novo conjunto de dados que contém cada valor de nível de log exclusivo e quantas vezes ele ocorre. Isso é armazenado em FREQUENCIES</td>
    </tr>
    <tr>
    <td>RESULT = order FREQUENCIES by COUNT desc;</td><td>Ordena os níveis de log Olá por contagem (decrescente) e armazena em resultado</td>
    </tr>
    </table>
6.Você também pode salvar os resultados de saudação de uma transformação usando Olá `STORE` instrução. Por exemplo, a saudação comando a seguir salva Olá `RESULT` toohello **/example/data/pigout** diretório no contêiner de armazenamento padrão Olá para o cluster:

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > Olá dados são armazenados no diretório especificado do hello nos arquivos denominados **parte nnnnn**. Se o diretório de saudação já existir, você receberá uma mensagem de erro.
   >
   >
7. Olá tooexit pesado prompt, digite Olá instrução a seguir.

        QUIT;

### <a name="pig-latin-batch-files"></a>Arquivos de lote do Pig Latin
Você também pode usar o hello Pig comando toorun latino Pig que está contido em um arquivo.

1. Depois de sair do prompt de pesado hello, abra **o bloco de notas** e criar um novo arquivo denominado **pigbatch.pig** em Olá **PIG_HOME %** directory.
2. Tipo ou a seguir Olá colar linhas em Olá **pigbatch.pig** de arquivo e, em seguida, salvá-lo:

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. Olá Use toorun Olá a seguir **pigbatch.pig** arquivo usando o comando de pig de saudação.

        pig %PIG_HOME%\pigbatch.pig

    Quando o trabalho em lotes de saudação for concluída, você deverá ver Olá saída, que deve ser Olá mesmo como quando você usou a seguir `DUMP RESULT;` nas etapas anteriores hello:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="summary"></a>Resumo
Como você pode ver, Olá comando Pig permite toointeractively executar operações de MapReduce ou executar trabalhos de Pig latino que são armazenados em um arquivo em lotes.

## <a id="nextsteps"></a>Próximas etapas
Para obter informações gerais sobre o Pig no HDInsight:

* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)

Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)
* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)
