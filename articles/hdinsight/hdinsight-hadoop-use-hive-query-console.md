---
title: aaaUse Hive do Hadoop no hello Console de consulta no HDInsight - Azure | Microsoft Docs
description: "Saiba como toouse Olá baseado na web Console de consulta toorun consultas de Hive em um HDInsight Hadoop do cluster de seu navegador."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a>Executar consultas de Hive usando Olá Console de consulta
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Neste artigo, você aprenderá como consultas de Hive toouse Olá Console de consulta do HDInsight toorun em um HDInsight Hadoop do cluster de seu navegador.

> [!IMPORTANT]
> Olá HDInsight consulta Console só está disponível em clusters HDInsight baseados no Windows. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Para HDInsight 3.4 ou superior, confira [Executar consultas do Hive no Modo de Exibição Hive do Ambari](hdinsight-hadoop-use-hive-ambari-view.md) para obter informações sobre como executar consultas do Hive em um navegador da Web.

## <a id="prereq"></a>Pré-requisitos
toocomplete Olá etapas neste artigo, você precisará seguir hello.

* Um cluster Hadoop do HDInsight baseado no Windows
* Um navegador da Web

## <a id="run"></a>Executar consultas de Hive usando Olá Console de consulta
1. Abra um navegador da web e navegue muito**https://CLUSTERNAME.azurehdinsight.net**, onde **CLUSTERNAME** é o nome de saudação do cluster HDInsight. Quando solicitado, insira o nome de usuário de saudação e a senha que você usou quando criou o cluster hello.
2. Links de saudação na parte superior de saudação da página hello, selecione **Editor Hive**. Exibe um formulário que pode ser usado tooenter Olá HiveQL instruções que você deseja toorun no cluster do HDInsight hello.

    ![editor de hive Olá](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    Substitua o texto de saudação `Select * from hivesampletable` com hello HiveQL instruções a seguir:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Essas instruções executam Olá ações a seguir:

   * **DROP TABLE**: exclui a tabela hello e arquivo de dados de saudação se Olá tabela já existir.
   * **CREATE EXTERNAL TABLE**: cria uma nova tabela “externa” em Hive. Tabelas externas armazenam a definição da tabela Olá somente no Hive; dados de saudação são deixados no local original hello.

     > [!NOTE]
     > Tabelas externas devem ser usadas quando você espera Olá subjacente toobe dados atualizado por uma origem externa (como um processo de carregamento de dados automatizado) ou por outra operação de MapReduce, mas convém sempre ter que dados mais recentes do toouse Olá de consultas de Hive.
     >
     > Descartar uma tabela externa **não** excluir dados hello, definição de tabela Olá somente.
     >
     >
   * **FORMATO de linha**: informa ao Hive como Olá dados são formatados. Nesse caso, os campos de saudação em cada log são separados por um espaço.
   * **LOCAL de arquivo de texto como armazenados**: informa ao Hive onde dados saudação são armazenado (diretório de exemplo de dados de saudação) e que ela é armazenada como texto
   * **Selecione**: selecione uma contagem de todas as linhas em que coluna **t4** conter valor Olá **[Erro]**. Isso deve retornar um valor de **3** , já que existem três linhas que contêm esse valor.
   * **INPUT__FILE__NAME LIKE '%.log'** - informa ao Hive que só devemos retornar dados de arquivos que terminam em .log. Isso restringe Olá toohello sample.log arquivo de pesquisa contém dados saudação e evita que ele retornando dados de exemplo de outros arquivos de dados que não correspondem ao esquema Olá definimos.
3. Clique em **Enviar**. Olá **sessão de trabalho** em Olá parte inferior da página de saudação deve exibir os detalhes do trabalho de saudação.
4. Olá quando **Status** campo alterações muito**concluído**, selecione **exibir detalhes** para trabalho hello. Na página de detalhes do hello, Olá **saída de trabalho** contém `[ERROR]    3`. Você pode usar o hello **baixar** botão em toodownload esse campo em um arquivo que contém a saída de saudação do trabalho de saudação.

## <a id="summary"></a>Resumo
Como você pode ver, Olá Console de consulta fornece uma maneira fácil toorun consultas de Hive em um cluster HDInsight, monitorar o status do trabalho hello e recuperar a saída de hello.

toolearn mais sobre como usar trabalhos do Console de consulta de Hive toorun Hive, selecione **Introdução** na parte superior de saudação do hello Console de consulta, em seguida, usar exemplos Olá fornecidos. Cada exemplo orienta pelo processo de saudação do uso de Hive tooanalyze dados, incluindo explicações sobre as instruções de HiveQL Olá usadas no exemplo hello.

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
