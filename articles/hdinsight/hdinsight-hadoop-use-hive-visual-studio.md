---
title: aaaHive com ferramentas de Data Lake (Hadoop) para Visual Studio - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse Olá Data Lake ferramentas para Visual Studio toorun Apache Hive consultas com Apache Hadoop em HDInsight do Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a>Executar consultas do Hive usando ferramentas de Data Lake Olá para Visual Studio

Saiba como toouse Olá Data Lake ferramentas para Visual Studio tooquery Apache Hive. Olá Data Lake ferramentas permitem que você tooeasily criar, enviar e monitorar tooHadoop de consultas de Hive no HDInsight do Azure.

## <a id="prereq"></a>Pré-requisitos

* Um cluster Azure HDInsight (Hadoop no HDInsight)

  > [!IMPORTANT]
  > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* O Visual Studio (um dos Olá versões a seguir):

    * Visual Studio 2013 Community/Professional/Premium/Ultimate com Atualização 4

    * Visual Studio 2015 (qualquer edição)

    * Visual Studio 2017 (qualquer edição)

* Ferramentas do HDInsight para Visual Studio ou ferramentas do Azure Data Lake para Visual Studio. Consulte [começar a usar ferramentas Hadoop do Visual Studio para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) para obter informações sobre como instalar e configurar as ferramentas de saudação.

## <a id="run"></a>Executar consultas de Hive usando Olá Visual Studio

1. Abra o **Visual Studio** e selecione **Novo** > **Projeto** > **Azure Data Lake** > **HIVE** > **Aplicativo Hive**. Forneça um nome para esse projeto.

2. Olá abrir **Script.hql** arquivo criado com esse projeto e colar em Olá HiveQL instruções a seguir:

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    Essas instruções executam Olá ações a seguir:

   * `DROP TABLE`: Se a tabela de saudação existir, esta instrução exclui-lo.

   * `CREATE EXTERNAL TABLE`: cria uma nova tabela 'externa' no Hive. Tabelas externas apenas armazenam a definição de tabela Olá no Hive (dados são deixados no local original Olá Olá).

     > [!NOTE]
     > Tabelas externas devem ser usadas quando você espera Olá toobe de dados subjacentes atualizado por uma fonte externa. Por exemplo, um trabalho de MapReduce ou serviço do Azure.
     >
     > Descartar uma tabela externa **não** excluir dados hello, definição de tabela Olá somente.

   * `ROW FORMAT`: Informa ao Hive como Olá dados são formatados. Nesse caso, os campos de saudação em cada log são separados por um espaço.

   * `STORED AS TEXTFILE LOCATION`: Informa ao Hive onde hello os dados são armazenados (diretório de exemplo de dados de saudação) e que ela é armazenada como texto.

   * `SELECT`: Selecione uma contagem de todas as linhas em que coluna `t4` contém valor Olá `[ERROR]`. Essa instrução retorna um valor de `3`, já que há três linhas que contêm esse valor.

   * `INPUT__FILE__NAME LIKE '%.log'`: informa ao Hive que só devemos retornar dados de arquivos que terminam em .log. Essa cláusula restringe Olá toohello sample.log arquivo de pesquisa contém dados saudação.

3. Na barra de ferramentas hello, selecione Olá **HDInsight Cluster** que você deseja toouse para esta consulta. Selecione **enviar** instruções de saudação toorun como um trabalho de Hive.

   ![Barra de envio](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. Olá **resumo do trabalho de Hive** aparece e exibe informações sobre Olá executando o trabalho. Saudação de uso **atualizar** link toorefresh Olá informações de trabalho até Olá **Status do trabalho** muda muito**concluído**.

   ![resumo do trabalho exibindo um trabalho concluído](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. Saudação de uso **saída de trabalho** vincular a saída de hello tooview deste trabalho. Ele exibe `[ERROR] 3`, que é o valor de saudação retornado por essa consulta.

6. Você também pode executar consultas Hive sem criar um projeto. Usando o **Gerenciador de Servidores**, expanda **Azure** > **HDInsight**, clique com o botão direito do mouse no seu servidor do HDInsight e selecione **Escrever uma Consulta de Hive**.

7. Em Olá **temp.hql** documento que é exibido, adicionar Olá HiveQL instruções a seguir:

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    Essas instruções executam Olá ações a seguir:

   * `CREATE TABLE IF NOT EXISTS`: cria uma tabela, se ela ainda não existir. Porque Olá `EXTERNAL` palavra-chave não for usada, essa instrução cria uma tabela interna. Tabelas internas são armazenadas no data warehouse do hello Hive e são gerenciadas pelo Hive.

     > [!NOTE]
     > Ao contrário de `EXTERNAL` tabelas, descartar uma tabela interna também exclui Olá dados subjacentes.

   * `STORED AS ORC`: Repositórios Olá dados em linha otimizado Colunar (ORC) formato. Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.

   * `INSERT OVERWRITE ... SELECT`: Seleciona linhas Olá `log4jLogs` tabela que contêm `[ERROR]`, em seguida, insere Olá dados em hello `errorLogs` tabela.

8. Na barra de ferramentas hello, selecione **enviar** toorun trabalho de saudação. Saudação de uso **Status do trabalho** toodetermine trabalho Olá foi concluída com êxito.

9. tooverify que Olá trabalho criado tabela hello, use **Server Explorer** e expanda **Azure** > **HDInsight** > seu cluster HDInsight > **Bancos de dados de hive** > **padrão**. Olá **em decorrência** tabela e hello **log4jLogs** tabela são listadas.

## <a id="nextsteps"></a>Próximas etapas

Como você pode ver, ferramentas do HDInsight Olá para o Visual Studio fornecem um toowork de maneira fácil com consultas de Hive no HDInsight.

Para obter informações gerais sobre o Hive no HDInsight:

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)

Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:

* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)

* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)

Para obter mais informações sobre as ferramentas do HDInsight Olá para o Visual Studio:

* [Introdução às ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)

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

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
