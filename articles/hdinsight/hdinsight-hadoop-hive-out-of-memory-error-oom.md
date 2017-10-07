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
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="e17b9-105">Corrigir um erro Hive sem memória no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e17b9-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="e17b9-106">Saiba como toofix um Hive erro de memória insuficiente quando processar grandes tabelas, definindo configurações de memória de Hive.</span><span class="sxs-lookup"><span data-stu-id="e17b9-106">Learn how toofix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="e17b9-107">Executar a consulta do Hive em tabelas grandes</span><span class="sxs-lookup"><span data-stu-id="e17b9-107">Run Hive query against large tables</span></span>

<span data-ttu-id="e17b9-108">Um cliente executou uma consulta do Hive:</span><span class="sxs-lookup"><span data-stu-id="e17b9-108">A customer ran a Hive query:</span></span>

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

<span data-ttu-id="e17b9-109">Algumas nuances desta consulta:</span><span class="sxs-lookup"><span data-stu-id="e17b9-109">Some nuances of this query:</span></span>

* <span data-ttu-id="e17b9-110">T1 é uma alias tooa grande tabela, TABLE1, que tem vários tipos de coluna de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="e17b9-110">T1 is an alias tooa big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="e17b9-111">Outras tabelas não são tão grandes, mas têm muitas colunas.</span><span class="sxs-lookup"><span data-stu-id="e17b9-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="e17b9-112">Todas as tabelas estão associadas umas às outras, em alguns casos com várias colunas em TABLE 1 e em outras.</span><span class="sxs-lookup"><span data-stu-id="e17b9-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="e17b9-113">consulta de Hive Olá levou toofinish 26 minutos em um cluster do HDInsight A3 24 nó.</span><span class="sxs-lookup"><span data-stu-id="e17b9-113">hello Hive query took 26 minutes toofinish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="e17b9-114">Olá cliente observado Olá mensagens de aviso a seguir:</span><span class="sxs-lookup"><span data-stu-id="e17b9-114">hello customer noticed hello following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="e17b9-115">Usando o mecanismo de execução Tez hello.</span><span class="sxs-lookup"><span data-stu-id="e17b9-115">By using hello Tez execution engine.</span></span> <span data-ttu-id="e17b9-116">Olá a mesma consulta foi executado por 15 minutos e, em seguida, lançou Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="e17b9-116">hello same query ran for 15 minutes, and then threw hello following error:</span></span>

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

<span data-ttu-id="e17b9-117">Erro de saudação permanece quando usar uma máquina virtual de maior (por exemplo, D12).</span><span class="sxs-lookup"><span data-stu-id="e17b9-117">hello error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-hello-out-of-memory-error"></a><span data-ttu-id="e17b9-118">Depurar Olá erro de memória insuficiente</span><span class="sxs-lookup"><span data-stu-id="e17b9-118">Debug hello out of memory error</span></span>

<span data-ttu-id="e17b9-119">Nosso suporte e as equipes de engenharia juntos encontrado um dos problemas de saudação causando Olá erro de memória insuficiente foi um [conhecido problema descrito no hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span><span class="sxs-lookup"><span data-stu-id="e17b9-119">Our support and engineering teams together found one of hello issues causing hello out of memory error was a [known issue described in hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="e17b9-120">Olá **hive.auto.convert.join.noconditionaltask** Olá hive-site.XML arquivo foi definido muito**true**:</span><span class="sxs-lookup"><span data-stu-id="e17b9-120">hello **hive.auto.convert.join.noconditionaltask** in hello hive-site.xml file was set too**true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="e17b9-121">É provável junção mapa foi causa Olá Olá espaço de pilha Java nosso erro de memória.</span><span class="sxs-lookup"><span data-stu-id="e17b9-121">It is likely map join was hello cause of hello Java Heap Space our of memory error.</span></span> <span data-ttu-id="e17b9-122">Conforme explicado na postagem de blog Olá [as configurações de memória de Hadoop Yarn no HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), quando Tez mecanismo de execução é o espaço de heap de saudação usado usado pertence, na verdade, toohello Tez contêiner.</span><span class="sxs-lookup"><span data-stu-id="e17b9-122">As explained in hello blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used hello heap space used actually belongs toohello Tez container.</span></span> <span data-ttu-id="e17b9-123">Consulte Olá memória de contêiner para imagem descrevendo Olá Tez a seguir.</span><span class="sxs-lookup"><span data-stu-id="e17b9-123">See hello following image describing hello Tez container memory.</span></span>

![Diagrama de memória de contêiner Tez: erro de falta de memória do Hive](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="e17b9-125">Como sugere a postagem do blog Olá, Olá duas configurações de memória a seguir define memória de contêiner Olá heap Olá: **hive.tez.container.size** e **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="e17b9-125">As hello blog post suggests, hello following two memory settings define hello container memory for hello heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="e17b9-126">Nossa experiência, Olá exceção de memória não significa Olá tamanho de contêiner é muito pequeno.</span><span class="sxs-lookup"><span data-stu-id="e17b9-126">From our experience, hello out of memory exception does not mean hello container size is too small.</span></span> <span data-ttu-id="e17b9-127">Isso significa Olá tamanho do heap do Java (hive.tez.java.opts) é muito pequeno.</span><span class="sxs-lookup"><span data-stu-id="e17b9-127">It means hello Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="e17b9-128">Para que sempre que houver memória insuficiente, você pode tentar tooincrease **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="e17b9-128">So whenever you see out of memory, you can try tooincrease **hive.tez.java.opts**.</span></span> <span data-ttu-id="e17b9-129">Se necessário você pode ter tooincrease **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="e17b9-129">If needed you might have tooincrease **hive.tez.container.size**.</span></span> <span data-ttu-id="e17b9-130">Olá **java.opts** configuração deve ser aproximadamente 80% da **container.size**.</span><span class="sxs-lookup"><span data-stu-id="e17b9-130">hello **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="e17b9-131">configuração de saudação **hive.tez.java.opts** sempre deve ser menor do que **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="e17b9-131">hello setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="e17b9-132">Como uma máquina D12 tem 28GB de memória, é decidido toouse um tamanho de contêiner de 10GB (10240MB) e atribuir a 80% toojava.opts:</span><span class="sxs-lookup"><span data-stu-id="e17b9-132">Because a D12 machine has 28GB memory, we decided toouse a container size of 10GB (10240MB) and assign 80% toojava.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="e17b9-133">Com as novas configurações de saudação, consulta Olá executou com êxito em menos de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="e17b9-133">With hello new settings, hello query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e17b9-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e17b9-134">Next steps</span></span>

<span data-ttu-id="e17b9-135">Recebendo uma mensagem de erro OOM não significa necessariamente Olá tamanho de contêiner é muito pequeno.</span><span class="sxs-lookup"><span data-stu-id="e17b9-135">Getting an OOM error doesn't necessarily mean hello container size is too small.</span></span> <span data-ttu-id="e17b9-136">Em vez disso, você deve configurar as configurações de memória Olá para que o tamanho de heap Olá é aumentado e é pelo menos 80% do tamanho de memória do contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="e17b9-136">Instead, you should configure hello memory settings so that hello heap size is increased and is at least 80% of hello container memory size.</span></span> <span data-ttu-id="e17b9-137">Para otimizar consultas do Hive, consulte [Otimizar consultas do Hive para Hadoop no HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="e17b9-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>
