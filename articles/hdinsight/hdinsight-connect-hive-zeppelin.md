---
title: Usar Zeppelin para executar consultas do Hive no Azure HDInsight | Microsoft Docs
description: Saiba como usar o Zeppelin para executar consultas do Hive.
keywords: hdinsight, hadoop, hive, consulta interativa, LLAP
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2017
ms.author: jgao
ms.openlocfilehash: 39f99bef252e93db55e0493ee284ef78b7d087a1
ms.sourcegitcommit: 4bd369fc472dced985239aef736fece42fecfb3b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2018
---
# <a name="use-zeppelin-to-run-hive-queries-in-azure-hdinsight"></a>Usar Zeppelin para executar consultas do Hive no Azure HDInsight 

Clusters de Consulta Interativa do HDInsight incluem blocos de anotações do Zeppelin que você pode usar para executar consultas interativas do Hive. Neste artigo, você aprenderá a usar Zeppelin para executar consultas interativas do Hive no Azure HDInsight. 

## <a name="prerequisites"></a>pré-requisitos
Antes de prosseguir com este artigo, você deve ter os seguintes itens:

* **Cluster de Consulta Interativa do HDInsight**. Consulte [Criar cluster](hadoop/apache-hadoop-linux-tutorial-get-started.md#create-cluster) para criar um cluster HDInsight.  Verifique se você escolheu o tipo de Consulta Interativa. 

## <a name="create-a-zeppelin-note"></a>Criar uma Anotação do Zeppelin

1. Navegue até a URL a seguir:

        https://CLUSTERNAME.azurehdinsight.net/zeppelin
    Substitua **CLUSTERNAME** pelo nome do cluster.

2. Insira seu nome de usuário e senha do Hadoop. Na página do Zeppelin, você pode criar uma nova anotação ou abrir anotações existentes. O HiveSample contém algumas amostras de consultas do Hive.  

    ![HDInsight Consulta Interativa Zeppelin](./media/hdinsight-connect-hive-zeppelin/hdinsight-hive-zeppelin.png)
3. Clique em **Criar nova Anotação**.
4. Digite ou selecione os valores a seguir:

    - Nome da anotação: digite um nome para a anotação.
    - Interpretador padrão: selecione **JDBC**.

5. Clique em **Criar Anotação**.
6. Execute a consulta do Hive a seguir:

        %jdbc(hive)
        show tables

    ![HDInsight Consulta Interativa Zeppelin executa a consulta](./media/hdinsight-connect-hive-zeppelin/hdinsight-hive-zeppelin-query.png)

    A instrução **%jdbc(hive)** na primeira linha informa o bloco de anotações para usar o interpretador JDBC do Hive.

    A consulta deverá retornar uma tabela de Hive denominada *hivesampletable*.

    A seguir estão mais duas consultas de Hive que podem ser executadas na hivesampletable. 

        %jdbc(hive)
        select * from hivesampletable limit 10

        %jdbc(hive)
        select ${group_name}, count(*) as total_count
        from hivesampletable
        group by ${group_name=market,market|deviceplatform|devicemake}
        limit ${total_count=10}

    Em comparação com o Hive tradicional, os resultados da consulta retornam muito mais rapidamente.


## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como visualizar os dados de HDInsight usando o Power BI.  Para saber mais, consulte os seguintes artigos:

* [Visualizar dados de Hive com o Microsoft Power BI no Azure HDInsight](hadoop/apache-hadoop-connect-hive-power-bi.md).
* [Visualizar dados da consulta interativa do Hive com o Power BI no Azure HDInsight](./interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).
* [Conectar o Excel ao HDInsight com o Driver ODBC do Microsoft Hive](hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).
* [Conectar o Excel ao Hadoop usando Power Query](hadoop/apache-hadoop-connect-excel-power-query.md).
* [Conectar-se ao Azure HDInsight e executar consultas Hive usando Ferramentas do Data Lake para Visual Studio](hadoop/apache-hadoop-visual-studio-tools-get-started.md).
* [Use a Ferramenta do Azure HDInsight para Visual Studio Code](hdinsight-for-vscode.md).
* [Carregue os Dados no HDInsight](./hdinsight-upload-data.md).
