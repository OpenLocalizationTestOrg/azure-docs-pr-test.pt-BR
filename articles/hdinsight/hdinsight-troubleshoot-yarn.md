---
title: aaaTroubleshoot YARN usando o Azure HDInsight | Microsoft Docs
description: Obter respostas a perguntas toocommon sobre como trabalhar com o Apache Hadoop YARN e HDInsight do Azure.
keywords: "Azure HDInsight, YARN, perguntas frequentes, guia de solução de problemas, perguntas comuns"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a>Solucionar problemas de YARN usando o Azure HDInsight

Saiba mais sobre questões hello e suas resoluções durante o trabalho com cargas Apache Hadoop YARN no Apache Ambari.

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a>Como fazer para criar uma nova fila do YARN em um cluster


### <a name="resolution-steps"></a>Etapas de resolução 

Use Olá seguinte etapas Ambari toocreate uma nova fila YARN e, em seguida, equilibrar a alocação de capacidade de saudação entre todas as filas de saudação. 

Neste exemplo, duas filas existentes (**padrão** e **thriftsvr**) são alterados de 50% capacidade too25% da capacidade, que fornece a nova capacidade de 50% de fila (spark) hello.
| Fila | Capacity | Capacidade máxima |
| --- | --- | --- | --- |
| padrão | 25% | 50% |
| thrftsvr | 25% | 50% |
| spark | 50% | 50% |

1. Selecione Olá **Ambari exibições** ícone e, em seguida, selecione Olá grade padrão. Em seguida, selecione **Gerenciador de Filas do YARN**.

    ![Selecione o ícone de modos de exibição do Ambari do hello](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. Selecione Olá **padrão** fila.

    ![Selecione a fila de padrão de saudação](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. Para Olá **padrão** de fila, altere Olá **capacidade** de too25 de 50% %. Para Olá **thriftsvr** de fila, altere Olá **capacidade** too25%.

    ![Alterar Olá capacidade too25% para filas de saudação padrão e thriftsvr](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. toocreate uma nova fila, selecione **adicionar fila**.

    ![Selecionar Adicionar Fila](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. Nome hello nova fila.

    ![Nome da fila de saudação Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. Deixe Olá **capacidade** valores em 50% e, em seguida, selecione hello **ações** botão.

    ![Selecione o botão de ações de saudação](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. Escolha **Salvar e Atualizar Filas**.

    ![Escolha Salvar e Atualizar Filas](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

Essas alterações são visíveis imediatamente em Olá YARN da interface do usuário de Agendador.

### <a name="additional-reading"></a>Leitura adicional

- [YARN CapacityScheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a>Como fazer para baixar logs do YARN de um cluster


### <a name="resolution-steps"></a>Etapas de resolução 

1. Conecte o cluster do HDInsight toohello usando um cliente do Secure Shell (SSH). Para saber mais, veja [Leituras adicionais](#additional-reading-2).

2. toolist todos Olá IDs de aplicativo dos aplicativos de YARN Olá atualmente em execução, execute Olá comando a seguir:

    ```apache
    yarn top
    ```
    Olá IDs são listadas na Olá **APPLICATIONID** coluna. Você pode baixar os logs do hello **APPLICATIONID** coluna.

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. logs de contêiner YARN toodownload para todos os mestres de aplicativo, use Olá comando a seguir:
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    Este comando cria um arquivo de log chamado amlogs.txt. 

4. logs de contêiner YARN toodownload somente mestre mais recente de aplicativo de hello, use Olá comando a seguir:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    Este comando cria um arquivo de log chamado latestamlogs.txt. 

4. logs de contêiner YARN toodownload para mestres de dois aplicativos primeiro hello, use Olá comando a seguir:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    Este comando cria um arquivo de log chamado first2amlogs.txt. 

5. toodownload todos os logs de contêiner YARN, use Olá seguinte comando:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    Este comando cria um arquivo de log chamado logs.txt. 

6. log de contêiner toodownload Olá YARN para um contêiner específico, use Olá comando a seguir:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    Este comando cria um arquivo de log chamado containerlogs.txt.

### <a name="additional-reading-2"></a>Leitura adicional

- [Conecte-se tooHDInsight (Hadoop) usando o SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [Aplicativos e conceitos do Apache Hadoop YARN](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)







