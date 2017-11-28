---
title: consultas aaaOptimize Hive no HDInsight do Azure | Microsoft Docs
description: Saiba como toooptimize o Hive as consultas para Hadoop no HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="3c194-103">Otimizar consultas do Hive no Azure HDInsight | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="3c194-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="3c194-104">Por padrão, os clusters do Hadoop não são otimizados para desempenho.</span><span class="sxs-lookup"><span data-stu-id="3c194-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="3c194-105">Este artigo aborda alguns métodos de otimização de desempenho Hive mais comuns que você pode aplicar tooyour consultas.</span><span class="sxs-lookup"><span data-stu-id="3c194-105">This article covers some most common Hive performance optimization methods that you can apply tooyour queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="3c194-106">Escalar nós de trabalho horizontalmente</span><span class="sxs-lookup"><span data-stu-id="3c194-106">Scale out worker nodes</span></span>

<span data-ttu-id="3c194-107">Aumentar Olá número de nós de trabalho em um cluster pode aproveitar mais toobe mapeadores e reducers executado em paralelo.</span><span class="sxs-lookup"><span data-stu-id="3c194-107">Increasing hello number of worker nodes in a cluster can leverage more mappers and reducers toobe run in parallel.</span></span> <span data-ttu-id="3c194-108">Há duas maneiras de aumentar a escalabilidade horizontal no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3c194-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="3c194-109">No momento de provisionar hello, você pode especificar o número de saudação de nós de trabalho usando Olá portal do Azure, o Azure PowerShell ou a interface de linha de comando de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="3c194-109">At hello provision time, you can specify hello number of worker nodes using hello Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="3c194-110">Para saber mais, veja [Criar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="3c194-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="3c194-111">Olá seguinte captura de tela mostra trabalho Olá nó configuração em Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="3c194-111">hello following screenshot shows hello worker node configuration on hello Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="3c194-113">Em tempo de execução de hello, você também pode expandir um cluster sem recriar um:</span><span class="sxs-lookup"><span data-stu-id="3c194-113">At hello run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="3c194-115">Para obter mais informações sobre as máquinas virtuais diferentes Olá HDInsight com suporte, consulte [preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3c194-115">For more information about hello different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="3c194-116">Habilitar o Tez</span><span class="sxs-lookup"><span data-stu-id="3c194-116">Enable Tez</span></span>

<span data-ttu-id="3c194-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) é um alternativa de execução toohello MapReduce mecanismo:</span><span class="sxs-lookup"><span data-stu-id="3c194-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine toohello MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="3c194-119">O Tez é mais rápido porque:</span><span class="sxs-lookup"><span data-stu-id="3c194-119">Tez is faster because:</span></span>

* <span data-ttu-id="3c194-120">**Execute o gráfico acíclico direcionado (DAG) como um único trabalho no mecanismo de MapReduce Olá**.</span><span class="sxs-lookup"><span data-stu-id="3c194-120">**Execute Directed Acyclic Graph (DAG) as a single job in hello MapReduce engine**.</span></span> <span data-ttu-id="3c194-121">Olá DAG requer que cada conjunto de mapeadores toobe seguido de um conjunto de reducers.</span><span class="sxs-lookup"><span data-stu-id="3c194-121">hello DAG requires each set of mappers toobe followed by one set of reducers.</span></span> <span data-ttu-id="3c194-122">Isso faz com que vários toobe de trabalhos de MapReduce será levado para cada consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="3c194-122">This causes multiple MapReduce jobs toobe spun off for each Hive query.</span></span> <span data-ttu-id="3c194-123">O Tez não tem essa restrição e pode processar DAG complexo como um único trabalho, minimizando a sobrecarga de inicialização de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3c194-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="3c194-124">**Evita gravações desnecessárias**.</span><span class="sxs-lookup"><span data-stu-id="3c194-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="3c194-125">Devido a trabalhos toomultiple sendo girados para Olá mesma consulta de Hive no mecanismo de MapReduce hello, saída de saudação de cada trabalho é gravada tooHDFS para dados intermediários.</span><span class="sxs-lookup"><span data-stu-id="3c194-125">Due toomultiple jobs being spun for hello same Hive query in hello MapReduce engine, hello output of each job is written tooHDFS for intermediate data.</span></span> <span data-ttu-id="3c194-126">Como Tez minimiza o número de trabalhos para cada consulta de Hive é tooavoid capaz de gravação de desnecessários.</span><span class="sxs-lookup"><span data-stu-id="3c194-126">Since Tez minimizes number of jobs for each Hive query it is able tooavoid unnecessary write.</span></span>
* <span data-ttu-id="3c194-127">**Minimiza atrasos de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="3c194-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="3c194-128">Tez é melhor atraso de inicialização toominimize capaz reduzindo o número de saudação de mapeadores precisa toostart e também melhorar otimização em todo.</span><span class="sxs-lookup"><span data-stu-id="3c194-128">Tez is better able toominimize start-up delay by reducing hello number of mappers it needs toostart and also improving optimization throughout.</span></span>
* <span data-ttu-id="3c194-129">**Reutiliza contêineres**.</span><span class="sxs-lookup"><span data-stu-id="3c194-129">**Reuses containers**.</span></span> <span data-ttu-id="3c194-130">Sempre que possível Tez é capaz de tooreuse contêineres tooensure que a latência devido toostarting backup contêineres é reduzido.</span><span class="sxs-lookup"><span data-stu-id="3c194-130">Whenever possible Tez is able tooreuse containers tooensure that latency due toostarting up containers is reduced.</span></span>
* <span data-ttu-id="3c194-131">**Técnicas de otimização contínua**.</span><span class="sxs-lookup"><span data-stu-id="3c194-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="3c194-132">Tradicionalmente, a otimização ocorria durante a fase de compilação.</span><span class="sxs-lookup"><span data-stu-id="3c194-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="3c194-133">No entanto, para obter mais informações sobre entradas de saudação que permitem melhor otimização durante o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="3c194-133">However more information about hello inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="3c194-134">Tez usa técnicas de otimização contínua que permite que ele toooptimize plano de saudação adicional na fase de tempo de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c194-134">Tez uses continuous optimization techniques that allows it toooptimize hello plan further into hello runtime phase.</span></span>

<span data-ttu-id="3c194-135">Para obter mais detalhes sobre esses conceitos, consulte [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="3c194-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="3c194-136">Você pode tornar qualquer consulta de Hive Tez habilitado, prefixando consulta Olá com configuração de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="3c194-136">You can make any Hive query Tez enabled by prefixing hello query with hello setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="3c194-137">Clusters HDInsight baseados em Linux têm o Tez habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="3c194-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="3c194-138">Particionamento do Hive</span><span class="sxs-lookup"><span data-stu-id="3c194-138">Hive partitioning</span></span>

<span data-ttu-id="3c194-139">Operação de e/s é um afunilamento de desempenho principais de saudação para executar consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="3c194-139">I/O operation is hello major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="3c194-140">Olá possível melhorar o desempenho se quantidade Olá dos dados que precisam toobe leitura pode ser reduzido.</span><span class="sxs-lookup"><span data-stu-id="3c194-140">hello performance can be improved if hello amount of data that needs toobe read can be reduced.</span></span> <span data-ttu-id="3c194-141">Por padrão, consultas do Hive examinam tabelas inteiras do Hive.</span><span class="sxs-lookup"><span data-stu-id="3c194-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="3c194-142">Isso é ótimo para consultas como verificações de tabela.</span><span class="sxs-lookup"><span data-stu-id="3c194-142">This is great for queries like table scans.</span></span> <span data-ttu-id="3c194-143">No entanto para consultas que precisam apenas de tooscan uma pequena quantidade de dados (por exemplo, consultas com filtragem), esse comportamento cria sobrecarga desnecessário.</span><span class="sxs-lookup"><span data-stu-id="3c194-143">However for queries that only need tooscan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="3c194-144">Particionamento de hive permite Hive consultas tooaccess somente Olá necessário quantidade de dados nas tabelas de Hive.</span><span class="sxs-lookup"><span data-stu-id="3c194-144">Hive partitioning allows Hive queries tooaccess only hello necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="3c194-145">Particionamento de hive é implementado por reorganização de dados brutos de saudação em novos diretórios com cada partição ter seu próprio diretório - onde a partição de saudação é definida pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="3c194-145">Hive partitioning is implemented by reorganizing hello raw data into new directories with each partition having its own directory - where hello partition is defined by hello user.</span></span> <span data-ttu-id="3c194-146">Olá diagrama a seguir ilustra o particionamento de uma tabela Hive pela coluna Olá *ano*.</span><span class="sxs-lookup"><span data-stu-id="3c194-146">hello following diagram illustrates partitioning a Hive table by hello column *Year*.</span></span> <span data-ttu-id="3c194-147">Um novo diretório é criado para cada ano.</span><span class="sxs-lookup"><span data-stu-id="3c194-147">A new directory is created for each year.</span></span>

![particionamento][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="3c194-149">Algumas considerações sobre particionamento:</span><span class="sxs-lookup"><span data-stu-id="3c194-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="3c194-150">**Não particione pouco demais** – O particionamento em colunas com apenas alguns valores pode causar poucas partições.</span><span class="sxs-lookup"><span data-stu-id="3c194-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="3c194-151">Por exemplo, particionamento gênero só cria dois toobe partições criadas (masculino e feminino), reduzindo latência Olá somente por um máximo de metade.</span><span class="sxs-lookup"><span data-stu-id="3c194-151">For example, partitioning on gender only creates two partitions toobe created (male and female), thus only reduce hello latency by a maximum of half.</span></span>
* <span data-ttu-id="3c194-152">**Não estenda partição** - no Olá outro extremo, criando uma partição em uma coluna com um valor exclusivo (por exemplo, userid) faz com que várias partições.</span><span class="sxs-lookup"><span data-stu-id="3c194-152">**Do not over partition** - On hello other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="3c194-153">Partição faz com que muito estresse em Olá namenode de cluster que tem toohandle Olá grande número de diretórios.</span><span class="sxs-lookup"><span data-stu-id="3c194-153">Over partition causes much stress on hello cluster namenode as it has toohandle hello large number of directories.</span></span>
* <span data-ttu-id="3c194-154">**Evite distorção de dados** -Escolha com bom senso sua chave de particionamento para que todas as partições tenham o mesmo tamanho.</span><span class="sxs-lookup"><span data-stu-id="3c194-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="3c194-155">Um exemplo é o particionamento em *estado* pode fazer com que Olá número de registros na Califórnia toobe quase 30 x que Vermont devido toohello diferença na população.</span><span class="sxs-lookup"><span data-stu-id="3c194-155">An example is partitioning on *State* may cause hello number of records under California toobe almost 30x that of Vermont due toohello difference in population.</span></span>

<span data-ttu-id="3c194-156">toocreate uma tabela de partição, use Olá *particionada por* cláusula:</span><span class="sxs-lookup"><span data-stu-id="3c194-156">toocreate a partition table, use hello *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="3c194-157">Depois de criar a tabela particionada hello, você pode criar particionamento estático ou o particionamento dinâmico.</span><span class="sxs-lookup"><span data-stu-id="3c194-157">Once hello partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="3c194-158">**Particionamento estático** significa que você tenha dados fragmentados já no hello apropriado diretórios e solicite Hive partições manualmente com base no local do diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c194-158">**Static partitioning** means that you have already sharded data in hello appropriate directories and you can ask Hive partitions manually based on hello directory location.</span></span> <span data-ttu-id="3c194-159">saudação de trecho de código a seguir é um exemplo.</span><span class="sxs-lookup"><span data-stu-id="3c194-159">hello following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="3c194-160">**O particionamento dinâmico** significa que você deseja Hive toocreate partições automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="3c194-160">**Dynamic partitioning** means that you want Hive toocreate partitions automatically for you.</span></span> <span data-ttu-id="3c194-161">Como já criamos Olá particionamento de tabela da tabela de preparo de hello, todos os nós precisamos toodo é inserir dados toohello particionada tabela:</span><span class="sxs-lookup"><span data-stu-id="3c194-161">Since we have already created hello partitioning table from hello staging table, all we need toodo is insert data toohello partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="3c194-162">Para obter mais detalhes, consulte [Tabelas particionadas](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="3c194-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-hello-orcfile-format"></a><span data-ttu-id="3c194-163">Use o formato de saudação ORCFile</span><span class="sxs-lookup"><span data-stu-id="3c194-163">Use hello ORCFile format</span></span>
<span data-ttu-id="3c194-164">O Hive dá suporte a vários formatos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="3c194-164">Hive supports different file formats.</span></span> <span data-ttu-id="3c194-165">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c194-165">For example:</span></span>

* <span data-ttu-id="3c194-166">**Texto**: Este é o formato de arquivo padrão hello e funciona com a maioria dos cenários</span><span class="sxs-lookup"><span data-stu-id="3c194-166">**Text**: this is hello default file format and works with most scenarios</span></span>
* <span data-ttu-id="3c194-167">**Avro**: funciona bem para cenários de interoperabilidade</span><span class="sxs-lookup"><span data-stu-id="3c194-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="3c194-168">**ORC/Parquet**: mais adequada para desempenho</span><span class="sxs-lookup"><span data-stu-id="3c194-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="3c194-169">Formato ORC (Colunar otimização de linha) é um toostore de maneira altamente eficiente os dados de Hive.</span><span class="sxs-lookup"><span data-stu-id="3c194-169">ORC (Optimized Row Columnar) format is a highly efficient way toostore Hive data.</span></span> <span data-ttu-id="3c194-170">Formatos de tooother comparados, ORC tem Olá vantagens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c194-170">Compared tooother formats, ORC has hello following advantages:</span></span>

* <span data-ttu-id="3c194-171">suporte para tipos complexos, incluindo a data e hora e tipos complexos e semiestruturados</span><span class="sxs-lookup"><span data-stu-id="3c194-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="3c194-172">a compactação de % too70</span><span class="sxs-lookup"><span data-stu-id="3c194-172">up too70% compression</span></span>
* <span data-ttu-id="3c194-173">indexa a cada 10.000 linhas, o que permite ignorar linhas de índices</span><span class="sxs-lookup"><span data-stu-id="3c194-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="3c194-174">uma redução significativa no tempo de execução</span><span class="sxs-lookup"><span data-stu-id="3c194-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="3c194-175">formato ORC tooenable, primeiro você cria uma tabela com cláusula Olá *armazenado como ORC*:</span><span class="sxs-lookup"><span data-stu-id="3c194-175">tooenable ORC format, you first create a table with hello clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="3c194-176">Em seguida, você deve inserir tabela de dados de ORC toohello da tabela de preparo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c194-176">Next, you insert data toohello ORC table from hello staging table.</span></span> <span data-ttu-id="3c194-177">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c194-177">For example:</span></span>

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

<span data-ttu-id="3c194-178">Você pode ler mais no formato ORC Olá [aqui](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="3c194-178">You can read more on hello ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="3c194-179">Vetorização</span><span class="sxs-lookup"><span data-stu-id="3c194-179">Vectorization</span></span>

<span data-ttu-id="3c194-180">Vetorização permite Hive tooprocess um lote de 1024 juntos linhas em vez de processar uma linha por vez.</span><span class="sxs-lookup"><span data-stu-id="3c194-180">Vectorization allows Hive tooprocess a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="3c194-181">Isso significa que operações simples são mais rapidamente porque menos código interno precisa toorun.</span><span class="sxs-lookup"><span data-stu-id="3c194-181">It means that simple operations are done faster because less internal code needs toorun.</span></span>

<span data-ttu-id="3c194-182">tooenable vetorização prefixo sua consulta de Hive com hello configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c194-182">tooenable vectorization prefix your Hive query with hello following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="3c194-183">Para obter mais informações, consulte [Execução de consultas vetorizadas](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="3c194-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="3c194-184">Outros métodos de otimização</span><span class="sxs-lookup"><span data-stu-id="3c194-184">Other optimization methods</span></span>
<span data-ttu-id="3c194-185">Há mais métodos de otimização que você pode considerar, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c194-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="3c194-186">**Particionamento de hive:** uma técnica que permite toocluster ou segmento grandes conjuntos de desempenho de consulta de toooptimize de dados.</span><span class="sxs-lookup"><span data-stu-id="3c194-186">**Hive bucketing:** a technique that allows toocluster or segment large sets of data toooptimize query performance.</span></span>
* <span data-ttu-id="3c194-187">**Otimização da junção:** otimização da execução da consulta do Hive planejamento tooimprove Olá eficiência de junções e reduzir a necessidade de saudação de dicas de usuário.</span><span class="sxs-lookup"><span data-stu-id="3c194-187">**Join optimization:** optimization of Hive's query execution planning tooimprove hello efficiency of joins and reduce hello need for user hints.</span></span> <span data-ttu-id="3c194-188">Para obter mais informações, consulte [Otimização de junção](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="3c194-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="3c194-189">**Aumentar redutores**.</span><span class="sxs-lookup"><span data-stu-id="3c194-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c194-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3c194-190">Next steps</span></span>
<span data-ttu-id="3c194-191">Neste artigo, você aprendeu a vários métodos comuns de otimização de consultas do Hive.</span><span class="sxs-lookup"><span data-stu-id="3c194-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="3c194-192">toolearn mais, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c194-192">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="3c194-193">Usar o Apache Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c194-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="3c194-194">Analisar dados de atrasos de voos usando o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c194-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="3c194-195">Analisar dados do Twitter usando o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c194-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="3c194-196">Analisar dados de sensor usando Olá Console de consulta de Hive no Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c194-196">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="3c194-197">Use o Hive com HDInsight tooanalyze logs de sites</span><span class="sxs-lookup"><span data-stu-id="3c194-197">Use Hive with HDInsight tooanalyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
