---
title: "aaaFix um Hive fora do erro de memória no Azure HDInsight | Microsoft Docs"
description: "Corrija um erro Hive sem memória no HDInsight. cenário de saudação do cliente é uma consulta em várias tabelas grandes."
keywords: "erro de memória insuficiente, OOM, configurações do Hive"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 7bce3dff-9825-4fa0-a568-c52a9f7d1dad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: 00a12969322c1e74434ba6593ffd098f342edd84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a>Corrigir um erro Hive sem memória no Azure HDInsight

Saiba como toofix um Hive erro de memória insuficiente quando processar grandes tabelas, definindo configurações de memória de Hive.

## <a name="run-hive-query-against-large-tables"></a>Executar a consulta do Hive em tabelas grandes

Um cliente executou uma consulta do Hive:

    SELECT
        COUNT (T1.COLUMN1) as DisplayColumn1,
        …
        …
        ….
    FROM
        TABLE1 T1,
        TABLE2 T2,
        TABLE3 T3,
        TABLE5 T4,
        TABLE6 T5,
        TABLE7 T6
    where (T1.KEY1 = T2.KEY1….
        …
        …

Algumas nuances desta consulta:

* T1 é uma alias tooa grande tabela, TABLE1, que tem vários tipos de coluna de cadeia de caracteres.
* Outras tabelas não são tão grandes, mas têm muitas colunas.
* Todas as tabelas estão associadas umas às outras, em alguns casos com várias colunas em TABLE 1 e em outras.

consulta de Hive Olá levou toofinish 26 minutos em um cluster do HDInsight A3 24 nó. Olá cliente observado Olá mensagens de aviso a seguir:

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

Usando o mecanismo de execução Tez hello. Olá a mesma consulta foi executado por 15 minutos e, em seguida, lançou Olá erro a seguir:

    Status: Failed
    Vertex failed, vertexName=Map 5, vertexId=vertex_1443634917922_0008_1_05, diagnostics=[Task failed, taskId=task_1443634917922_0008_1_05_000006, diagnostics=[TaskAttempt 0 failed, info=[Error: Failure while running task:java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at
    org.apache.hadoop.hive.ql.exec.tez.TezProcessor.initializeAndRunProcessor(TezProcessor.java:172)
        at org.apache.hadoop.hive.ql.exec.tez.TezProcessor.run(TezProcessor.java:138)
        at
    org.apache.tez.runtime.LogicalIOProcessorRuntimeTask.run(LogicalIOProcessorRuntimeTask.java:324)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:176)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:168)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1628)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:168)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:163)
        at java.util.concurrent.FutureTask.run(FutureTask.java:262)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
        at java.lang.Thread.run(Thread.java:745)
    Caused by: java.lang.OutOfMemoryError: Java heap space

Erro de saudação permanece quando usar uma máquina virtual de maior (por exemplo, D12).


## <a name="debug-hello-out-of-memory-error"></a>Depurar Olá erro de memória insuficiente

Nosso suporte e as equipes de engenharia juntos encontrado um dos problemas de saudação causando Olá erro de memória insuficiente foi um [conhecido problema descrito no hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

Olá **hive.auto.convert.join.noconditionaltask** Olá hive-site.XML arquivo foi definido muito**true**:

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

É provável junção mapa foi causa Olá Olá espaço de pilha Java nosso erro de memória. Conforme explicado na postagem de blog Olá [as configurações de memória de Hadoop Yarn no HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), quando Tez mecanismo de execução é o espaço de heap de saudação usado usado pertence, na verdade, toohello Tez contêiner. Consulte Olá memória de contêiner para imagem descrevendo Olá Tez a seguir.

![Diagrama de memória de contêiner Tez: erro de falta de memória do Hive](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

Como sugere a postagem do blog Olá, Olá duas configurações de memória a seguir define memória de contêiner Olá heap Olá: **hive.tez.container.size** e **hive.tez.java.opts**. Nossa experiência, Olá exceção de memória não significa Olá tamanho de contêiner é muito pequeno. Isso significa Olá tamanho do heap do Java (hive.tez.java.opts) é muito pequeno. Para que sempre que houver memória insuficiente, você pode tentar tooincrease **hive.tez.java.opts**. Se necessário você pode ter tooincrease **hive.tez.container.size**. Olá **java.opts** configuração deve ser aproximadamente 80% da **container.size**.

> [!NOTE]
> configuração de saudação **hive.tez.java.opts** sempre deve ser menor do que **hive.tez.container.size**.
> 
> 

Como uma máquina D12 tem 28GB de memória, é decidido toouse um tamanho de contêiner de 10GB (10240MB) e atribuir a 80% toojava.opts:

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

Com as novas configurações de saudação, consulta Olá executou com êxito em menos de 10 minutos.

## <a name="next-steps"></a>Próximas etapas

Recebendo uma mensagem de erro OOM não significa necessariamente Olá tamanho de contêiner é muito pequeno. Em vez disso, você deve configurar as configurações de memória Olá para que o tamanho de heap Olá é aumentado e é pelo menos 80% do tamanho de memória do contêiner de saudação. Para otimizar consultas do Hive, consulte [Otimizar consultas do Hive para Hadoop no HDInsight](hdinsight-hadoop-optimize-hive-query.md).
