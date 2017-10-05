---
title: "Corrigir um erro de Hive sem memória no Azure HDInsight | Microsoft Docs"
description: "Corrija um erro Hive sem memória no HDInsight. O cenário de cliente é uma consulta em várias tabelas grandes."
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
ms.openlocfilehash: da1247070ade11f78b505524f5e970e18eb16d10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="73f7f-105">Corrigir um erro Hive sem memória no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="73f7f-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="73f7f-106">Saiba como corrigir um erro Hive sem memória quando processar tabelas grandes definindo as configurações de memória do Hive.</span><span class="sxs-lookup"><span data-stu-id="73f7f-106">Learn how to fix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="73f7f-107">Executar a consulta do Hive em tabelas grandes</span><span class="sxs-lookup"><span data-stu-id="73f7f-107">Run Hive query against large tables</span></span>

<span data-ttu-id="73f7f-108">Um cliente executou uma consulta do Hive:</span><span class="sxs-lookup"><span data-stu-id="73f7f-108">A customer ran a Hive query:</span></span>

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

<span data-ttu-id="73f7f-109">Algumas nuances desta consulta:</span><span class="sxs-lookup"><span data-stu-id="73f7f-109">Some nuances of this query:</span></span>

* <span data-ttu-id="73f7f-110">T1 é um alias para uma grande tabela, TABLE1, com vários tipos de coluna STRING.</span><span class="sxs-lookup"><span data-stu-id="73f7f-110">T1 is an alias to a big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="73f7f-111">Outras tabelas não são tão grandes, mas têm muitas colunas.</span><span class="sxs-lookup"><span data-stu-id="73f7f-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="73f7f-112">Todas as tabelas estão associadas umas às outras, em alguns casos com várias colunas em TABLE 1 e em outras.</span><span class="sxs-lookup"><span data-stu-id="73f7f-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="73f7f-113">A consulta do Hive demorou 26 minutos para ser concluída em um cluster HDInsight A3 de 24 nós.</span><span class="sxs-lookup"><span data-stu-id="73f7f-113">The Hive query took 26 minutes to finish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="73f7f-114">O cliente percebeu as seguintes mensagens de aviso:</span><span class="sxs-lookup"><span data-stu-id="73f7f-114">The customer noticed the following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="73f7f-115">Usando o mecanismo de execução Tez.</span><span class="sxs-lookup"><span data-stu-id="73f7f-115">By using the Tez execution engine.</span></span> <span data-ttu-id="73f7f-116">A mesma consulta foi executada por 15 minutos e depois lançou o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="73f7f-116">The same query ran for 15 minutes, and then threw the following error:</span></span>

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

<span data-ttu-id="73f7f-117">O erro permanece ao usar uma máquina virtual maior (por exemplo, D12).</span><span class="sxs-lookup"><span data-stu-id="73f7f-117">The error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-the-out-of-memory-error"></a><span data-ttu-id="73f7f-118">Depurar o erro de memória insuficiente</span><span class="sxs-lookup"><span data-stu-id="73f7f-118">Debug the out of memory error</span></span>

<span data-ttu-id="73f7f-119">Nosso suporte e as equipes de engenharia juntos descobriram que um dos problemas que causou o erro de memória insuficiente era um [problema conhecido descrito no Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span><span class="sxs-lookup"><span data-stu-id="73f7f-119">Our support and engineering teams together found one of the issues causing the out of memory error was a [known issue described in the Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if the sum  of tables sizes in the map join is less than noconditionaltask.size the plan would generate a Map join, the issue with this is that the calculation doesnt take into account the overhead introduced by different HashTable implementation as results if the sum of input sizes is smaller than the noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="73f7f-120">O **hive.auto.convert.join.noconditionaltask** no arquivo hive-site.xml estava definido como **true**:</span><span class="sxs-lookup"><span data-stu-id="73f7f-120">The **hive.auto.convert.join.noconditionaltask** in the hive-site.xml file was set to **true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables the optimization about converting common join into mapjoin based on the input file size.
              If this parameter is on, and the sum of size for n-1 of the tables/partitions for a n-way join is smaller than the
              specified size, the join is directly converted to a mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="73f7f-121">É provável que junção de mapa tenha sido a causa do erro de falta de memória do Java Heap Space.</span><span class="sxs-lookup"><span data-stu-id="73f7f-121">It is likely map join was the cause of the Java Heap Space our of memory error.</span></span> <span data-ttu-id="73f7f-122">Conforme explicado na postagem no blog [Configurações de memória Yarn do Hadoop no HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), quando o mecanismo de execução Tez é usado, o espaço heap usado realmente pertence ao contêiner Tez.</span><span class="sxs-lookup"><span data-stu-id="73f7f-122">As explained in the blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used the heap space used actually belongs to the Tez container.</span></span> <span data-ttu-id="73f7f-123">Confira a imagem a seguir que descreve a memória do contêiner Tez.</span><span class="sxs-lookup"><span data-stu-id="73f7f-123">See the following image describing the Tez container memory.</span></span>

![Diagrama de memória de contêiner Tez: erro de falta de memória do Hive](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="73f7f-125">Como sugere a postagem no blog, as duas configurações de memória a seguir definem a memória de contêiner para o heap: **hive.tez.container.size** e **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="73f7f-125">As the blog post suggests, the following two memory settings define the container memory for the heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="73f7f-126">Em nossa experiência, a exceção de falta de memória não significa que o tamanho do contêiner seja muito pequeno.</span><span class="sxs-lookup"><span data-stu-id="73f7f-126">From our experience, the out of memory exception does not mean the container size is too small.</span></span> <span data-ttu-id="73f7f-127">Isso significa que o tamanho do heap de Java (hive.tez.java.opts) é muito pequeno.</span><span class="sxs-lookup"><span data-stu-id="73f7f-127">It means the Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="73f7f-128">Portanto, sempre que você vir falta de memória, poderá tentar aumentar **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="73f7f-128">So whenever you see out of memory, you can try to increase **hive.tez.java.opts**.</span></span> <span data-ttu-id="73f7f-129">Se necessário, pode ser que você precise aumentar **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="73f7f-129">If needed you might have to increase **hive.tez.container.size**.</span></span> <span data-ttu-id="73f7f-130">A configuração **java.opts** deve ser aproximadamente 80% do **container.size**.</span><span class="sxs-lookup"><span data-stu-id="73f7f-130">The **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="73f7f-131">A configuração **hive.tez.java.opts** deve ser menor que **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="73f7f-131">The setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="73f7f-132">Como uma máquina D12 tem 28 GB de memória, decidimos usar um tamanho de contêiner de 10 GB (10240 MB) e atribuir 80% para java.opts:</span><span class="sxs-lookup"><span data-stu-id="73f7f-132">Because a D12 machine has 28GB memory, we decided to use a container size of 10GB (10240MB) and assign 80% to java.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="73f7f-133">Com as novas configurações, a consulta foi executada com êxito em menos de dez minutos.</span><span class="sxs-lookup"><span data-stu-id="73f7f-133">With the new settings, the query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73f7f-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73f7f-134">Next steps</span></span>

<span data-ttu-id="73f7f-135">O recebimento de um erro de memória insuficiente não significa necessariamente que o tamanho do contêiner é muito pequeno.</span><span class="sxs-lookup"><span data-stu-id="73f7f-135">Getting an OOM error doesn't necessarily mean the container size is too small.</span></span> <span data-ttu-id="73f7f-136">Em vez disso, você deve definir as configurações de memória para que o tamanho do heap seja aumentado para pelo menos 80% do tamanho da memória do contêiner.</span><span class="sxs-lookup"><span data-stu-id="73f7f-136">Instead, you should configure the memory settings so that the heap size is increased and is at least 80% of the container memory size.</span></span> <span data-ttu-id="73f7f-137">Para otimizar consultas do Hive, consulte [Otimizar consultas do Hive para Hadoop no HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="73f7f-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>