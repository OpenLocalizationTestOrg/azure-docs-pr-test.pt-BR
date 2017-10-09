---
title: "aaaUse Ambari Tez exibição de HDInsight - Azure | Microsoft Docs"
description: "Saiba como Olá toouse Ambari Tez exibir toodebug Tez trabalhos no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a>Usar exibições do Ambari toodebug Tez trabalhos no HDInsight

Olá Ambari Web da interface do usuário para HDInsight contém uma exibição Tez que pode ser usado toounderstand e depurar os trabalhos que usam Tez. Olá Tez exibição permite trabalho de saudação toovisualize como um gráfico de itens conectados, detalhar cada item e recuperar estatísticas e informações de registro em log.

> [!IMPORTANT]
> etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, consulte [Controle de versão do componente do HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Pré-requisitos

* Criar um cluster HDInsight baseado em Linux. Para ver as etapas para criar um cluster, consulte [Introdução ao HDInsight baseado no Linux](hdinsight-hadoop-linux-tutorial-get-started.md).
* Um navegador da Web moderno, com suporte a HTML5.

## <a name="understanding-tez"></a>Noções básicas sobre o Tez

Tez é uma estrutura extensível para processamento de dados no Hadoop que fornece maior velocidade de processamento do que o MapReduce tradicional. Para clusters HDInsight baseados em Linux, é saudação padrão mecanismo para o Hive.

Tez cria um direcionado acíclico Graph (DAG) que descreve a ordem de saudação das ações necessárias para trabalhos. Ações individuais são chamadas de vértices e executar um pedaço de saudação trabalho geral. a execução real Olá Olá trabalho descrita por um vértice é chamada de uma tarefa e pode ser distribuída em vários nós no cluster de saudação.

### <a name="understanding-hello-tez-view"></a>Saudação de compreensão Tez exibição

Olá Tez exibição fornece informações de histórico e informações sobre processos em execução. Essas informações mostram como um trabalho é distribuído entre os clusters. Ele também exibe os contadores usados por tarefas e vértices e informações de erro relacionadas toohello trabalho. Ele pode oferecer informações úteis no hello os seguintes cenários:

* Monitorando processos de longa execução, exibindo Olá progresso de mapa e reduzir as tarefas.
* Analisar dados históricos para toolearn processos com êxito ou falha, como o processamento pode ser aprimorado ou razão da falha.

## <a name="generate-a-dag"></a>Gerar um DAG

Olá Tez exibição contém dados somente se um trabalho que usa Olá Tez mecanismo está atualmente em execução ou tiver sido executado anteriormente. Consultas de Hive simples podem ser resolvidas sem usar o Tez. Consultas mais complexas que executam filtragem, agrupamento, ordenação, associações, etc. Use o mecanismo de Tez hello.

Use Olá etapas toorun uma consulta de Hive que usa Tez a seguir:

1. Em um navegador da web, navegar toohttps://CLUSTERNAME.azurehdinsight.net, onde **CLUSTERNAME** é o nome de saudação do cluster HDInsight.

2. No menu de saudação na parte superior de saudação da página hello, selecione Olá **exibições** ícone. Esse ícone é semelhante a uma série de quadrados. No menu suspenso de saudação que aparece, selecione **Hive exibição**.

    ![Como selecionar o modo de exibição do Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. Quando Olá Hive exibição carrega, colar Olá seguinte consulta em Olá Editor de consultas e, em seguida, clique em **executar**.

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    Depois de concluído o trabalho de saudação, você verá a saída de hello exibida no hello **resultados do processo de consulta** seção. resultados de saudação devem ser semelhante toohello texto a seguir:

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. Selecione Olá **Log** guia. Você verá informações toohello semelhante texto a seguir:

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    Salvar Olá **id do aplicativo** de valor, como esse valor é usado na próxima seção, Olá.

## <a name="use-hello-tez-view"></a>Use Olá Tez exibição

1. No menu de saudação na parte superior de saudação da página hello, selecione Olá **exibições** ícone. No menu suspenso de saudação que aparece, selecione **Tez exibição**.

    ![Como selecionar o modo de exibição do Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. Quando Olá Tez exibição carregado, você verá uma lista de consultas de hive que estão sendo executados, ou ter sido executado no cluster de saudação.

    ![Todos os DAGS](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. Se você tiver apenas uma entrada, é para consulta de saudação que você executou na seção anterior hello. Se você tiver várias entradas, você pode pesquisar usando campos de saudação na parte superior de saudação da página de saudação.

4. Selecione Olá **ID da consulta** para uma consulta de Hive. Informações sobre consulta Olá são exibidas.

    ![Detalhes do DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. guias de saudação nessa página permitem que você Olá tooview informações a seguir:

    * **Detalhes da consulta**: detalhes sobre a consulta de Hive hello.
    * **Linha do tempo**: as informações sobre quanto tempo durou cada estágio de processamento.
    * **Configurações**: configuração de saudação usada para esta consulta.

    De __detalhes da consulta__ você pode usar Olá links toofind informações sobre Olá __aplicativo__ ou hello __DAG__ para esta consulta.
    
    * Olá __aplicativo__ link exibe informações sobre Olá aplicativo YARN para esta consulta. Aqui você pode acessar logs de aplicativo hello YARN.
    * Olá __DAG__ link exibe informações sobre o gráfico acíclico direcionado de saudação para esta consulta. Aqui você pode exibir uma representação gráfica da saudação DAG. Você também pode localizar informações sobre vértices hello dentro Olá DAG.

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como exibir hello toouse Tez, saiba mais sobre [usando Hive no HDInsight](hdinsight-use-hive.md).

Para obter mais informações técnicas sobre Tez, consulte Olá [Tez página no Hortonworks](http://hortonworks.com/hadoop/tez/).

Para obter mais informações sobre como usar o Ambari com HDInsight, consulte [gerenciar clusters HDInsight usando Olá Ambari Web UI](hdinsight-hadoop-manage-ambari.md)
