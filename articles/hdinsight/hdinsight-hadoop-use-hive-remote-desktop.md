---
title: "aaaUse Hive do Hadoop e a área de trabalho remota no HDInsight - Azure | Microsoft Docs"
description: "Saiba como tooconnect tooHadoop cluster no HDInsight usando a área de trabalho remota e, em seguida, executar consultas de Hive usando Olá Hive Interface de linha de comando."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a>Usar o Hive com Hadoop no HDInsight com Remote Desktop.
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Neste artigo, você aprenderá como tooconnect tooan HDInsight cluster usando a área de trabalho remota e, em seguida, execute o Hive as consultas usando Olá Hive Interface de linha de comando (CLI).

> [!IMPORTANT]
> Área de trabalho remota só está disponível em clusters de HDInsight que usam o Windows como sistema operacional de saudação. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Para HDInsight 3.4 ou superior, consulte [Use Hive com HDInsight e Beeline](hdinsight-hadoop-use-hive-beeline.md) para obter informações sobre como executar consultas de Hive diretamente no cluster de saudação de uma linha de comando.

## <a id="prereq"></a>Pré-requisitos
toocomplete Olá etapas neste artigo, você precisará seguir hello:

* Um cluster HDInsight baseado em Windows (Hadoop no HDInsight)
* Um computador cliente executando o Windows 7, Windows 8 ou Windows 10

## <a id="connect"></a>Conectar com a área de trabalho remota
Habilitar área de trabalho remota para o cluster do HDInsight hello e conecte tooit seguindo as instruções de saudação em [conectar tooHDInsight clusters usando o RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hive"></a>Use o comando de Hive Olá
Quando você se conectou toohello a área de trabalho para o cluster do HDInsight hello, use Olá toowork etapas com a seção a seguir:

1. Na área de trabalho do HDInsight hello, iniciar Olá **linha de comando do Hadoop**.
2. Digite Olá Olá toostart de comando CLI do Hive a seguir:

        %hive_home%\bin\hive

    Quando a saudação CLI foi iniciada, você verá prompt de Hive CLI Olá: `hive>`.
3. Usando Olá CLI, insira Olá seguindo as instruções toocreate uma nova tabela nomeada **log4jLogs** usando dados de exemplo:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Essas instruções executam Olá ações a seguir:

   * **DROP TABLE**: exclui a tabela hello e arquivo de dados de saudação se Olá tabela já existir.
   * **CREATE EXTERNAL TABLE**: cria uma nova tabela “externa” em Hive. Tabelas externas armazenam somente a definição de tabela Olá no Hive (dados são deixados no local original Olá Olá).

     > [!NOTE]
     > Tabelas externas devem ser usadas quando você espera Olá subjacente toobe dados atualizado por uma origem externa (como um processo de carregamento de dados automatizado) ou por outra operação de MapReduce, mas convém sempre ter que dados mais recentes do toouse Olá de consultas de Hive.
     >
     > Descartar uma tabela externa **não** excluir dados hello, definição de tabela Olá somente.
     >
     >
   * **FORMATO de linha**: informa ao Hive como Olá dados são formatados. Nesse caso, os campos de saudação em cada log são separados por um espaço.
   * **LOCAL de arquivo de texto como armazenados**: informa ao Hive onde dados saudação são armazenado (diretório de exemplo de dados de saudação) e que ela é armazenada como texto.
   * **Selecione**: seleciona uma contagem de todas as linhas em que coluna **t4** contém valor Olá **[Erro]**. Isso deve retornar um valor de **3** , já que existem três linhas que contêm esse valor.
   * **INPUT__FILE__NAME LIKE '%.log'** - informa ao Hive que só devemos retornar dados de arquivos que terminam em .log. Isso restringe Olá toohello sample.log arquivo de pesquisa contém dados saudação e evita que ele retornando dados de exemplo de outros arquivos de dados que não correspondem ao esquema Olá definimos.
4. Olá Use seguindo as instruções toocreate uma nova tabela 'internal' nomeada **em decorrência**:

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    Essas instruções executam Olá ações a seguir:

   * **CREATE TABLE IF NOT EXISTS**: cria uma tabela, se ela ainda não existir. Porque Olá **externo** palavra-chave não é usada, essa é uma tabela interna que é armazenada no data warehouse do hello Hive e é totalmente gerenciada pelo Hive.

     > [!NOTE]
     > Ao contrário de **externo** tabelas, descartar uma tabela interna também exclui Olá dados subjacentes.
     >
     >
   * **ARMAZENADOS como ORC**: armazena dados de Olá em formato (ORC) de coluna linha otimizado. Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.
   * **INSERT OVERWRITE ... Selecione**: seleciona linhas de saudação **log4jLogs** tabela que contém **[Erro]**, em seguida, insere Olá dados em hello **em decorrência** tabela.

     tooverify que apenas as linhas que contêm **[Erro]** na coluna t4 foram armazenado toohello **em decorrência** de tabela, use Olá após a instrução tooreturn todos Olá linhas de **em decorrência**:

       SELECT * de errorLogs;

     Três linhas de dados devem ser devolvidas, todas contendo **[ERROR]** na coluna t4.

## <a id="summary"></a>Resumo
Como você pode ver, Olá Olá comando Hive fornece um toointeractively de maneira fácil executar consultas de Hive em um cluster HDInsight, o status do trabalho de saudação do monitor e recuperar a saída de hello.

## <a id="nextsteps"></a>Próximas etapas
Para obter informações gerais sobre o Hive no HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)

Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:

* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)

Se você estiver usando Tez com Hive, consulte Olá documentos para as informações de depuração a seguir:

* [Use Olá Tez UI no HDInsight baseados no Windows](hdinsight-debug-tez-ui.md)
* [Use Olá exibição Ambari Tez no HDInsight baseados em Linux](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
