---
title: Otimizar consultas do Hive no Azure HDInsight | Microsoft Docs
description: Saiba como otimizar suas consultas do Hive no HDInsight.
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
ms.openlocfilehash: edbf797e6277a65b5311e4939f5ab72776b11557
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="32740-103">Otimizar consultas do Hive no Azure HDInsight | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="32740-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="32740-104">Por padrão, os clusters do Hadoop não são otimizados para desempenho.</span><span class="sxs-lookup"><span data-stu-id="32740-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="32740-105">Este artigo aborda alguns dos métodos de otimização de desempenho do Hive mais comuns que você pode aplicar às suas consultas.</span><span class="sxs-lookup"><span data-stu-id="32740-105">This article covers some most common Hive performance optimization methods that you can apply to your queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="32740-106">Escalar nós de trabalho horizontalmente</span><span class="sxs-lookup"><span data-stu-id="32740-106">Scale out worker nodes</span></span>

<span data-ttu-id="32740-107">O aumento do número de nós de trabalho em um cluster pode aproveitar mais mapeadores e redutores para execução paralela.</span><span class="sxs-lookup"><span data-stu-id="32740-107">Increasing the number of worker nodes in a cluster can leverage more mappers and reducers to be run in parallel.</span></span> <span data-ttu-id="32740-108">Há duas maneiras de aumentar a escalabilidade horizontal no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="32740-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="32740-109">No momento do provisionamento, você pode especificar o número de nós de trabalho usando o Portal do Azure, o Azure PowerShell ou a interface de linha de comando de Plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="32740-109">At the provision time, you can specify the number of worker nodes using the Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="32740-110">Para saber mais, veja [Criar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="32740-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="32740-111">A seguinte captura de tela mostra a configuração de nó de trabalho no Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="32740-111">The following screenshot shows the worker node configuration on the Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="32740-113">Em tempo de execução, você também pode escalar um cluster horizontalmente sem recriar um:</span><span class="sxs-lookup"><span data-stu-id="32740-113">At the run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="32740-115">Para obter informações sobre as diferentes máquinas virtuais com suporte no HDInsight, consulte [preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="32740-115">For more information about the different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="32740-116">Habilitar o Tez</span><span class="sxs-lookup"><span data-stu-id="32740-116">Enable Tez</span></span>

<span data-ttu-id="32740-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) é um mecanismo de execução alternativo ao mecanismo MapReduce:</span><span class="sxs-lookup"><span data-stu-id="32740-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine to the MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="32740-119">O Tez é mais rápido porque:</span><span class="sxs-lookup"><span data-stu-id="32740-119">Tez is faster because:</span></span>

* <span data-ttu-id="32740-120">**Execute gráfico acíclico dirigido (DAG) como um trabalho único no mecanismo MapReduce**.</span><span class="sxs-lookup"><span data-stu-id="32740-120">**Execute Directed Acyclic Graph (DAG) as a single job in the MapReduce engine**.</span></span> <span data-ttu-id="32740-121">O DAG requer que cada conjunto de mapeadores seja seguido por um conjunto de redutores.</span><span class="sxs-lookup"><span data-stu-id="32740-121">The DAG requires each set of mappers to be followed by one set of reducers.</span></span> <span data-ttu-id="32740-122">Isso faz com que vários trabalhos do MapReduce sejam gerados para cada consulta do Hive.</span><span class="sxs-lookup"><span data-stu-id="32740-122">This causes multiple MapReduce jobs to be spun off for each Hive query.</span></span> <span data-ttu-id="32740-123">O Tez não tem essa restrição e pode processar DAG complexo como um único trabalho, minimizando a sobrecarga de inicialização de trabalho.</span><span class="sxs-lookup"><span data-stu-id="32740-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="32740-124">**Evita gravações desnecessárias**.</span><span class="sxs-lookup"><span data-stu-id="32740-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="32740-125">Devido a vários trabalhos que estão sendo gerados para a mesma consulta do Hive no mecanismo MapReduce, a saída de cada trabalho é gravada no HDFS para dados intermediários.</span><span class="sxs-lookup"><span data-stu-id="32740-125">Due to multiple jobs being spun for the same Hive query in the MapReduce engine, the output of each job is written to HDFS for intermediate data.</span></span> <span data-ttu-id="32740-126">Como o Tez minimiza o número de trabalhos para cada consulta do Hive, ele pode evitar gravação desnecessária.</span><span class="sxs-lookup"><span data-stu-id="32740-126">Since Tez minimizes number of jobs for each Hive query it is able to avoid unnecessary write.</span></span>
* <span data-ttu-id="32740-127">**Minimiza atrasos de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="32740-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="32740-128">O Tez é mais capaz de minimizar o atraso de inicialização, reduzindo o número de mapeadores de que precisa para ser iniciado, além de aumentar a otimização de maneira geral.</span><span class="sxs-lookup"><span data-stu-id="32740-128">Tez is better able to minimize start-up delay by reducing the number of mappers it needs to start and also improving optimization throughout.</span></span>
* <span data-ttu-id="32740-129">**Reutiliza contêineres**.</span><span class="sxs-lookup"><span data-stu-id="32740-129">**Reuses containers**.</span></span> <span data-ttu-id="32740-130">Sempre que possível, o Tez é capaz de reutilizar contêineres para garantir que a latência devido à inicialização de contêineres seja reduzida.</span><span class="sxs-lookup"><span data-stu-id="32740-130">Whenever possible Tez is able to reuse containers to ensure that latency due to starting up containers is reduced.</span></span>
* <span data-ttu-id="32740-131">**Técnicas de otimização contínua**.</span><span class="sxs-lookup"><span data-stu-id="32740-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="32740-132">Tradicionalmente, a otimização ocorria durante a fase de compilação.</span><span class="sxs-lookup"><span data-stu-id="32740-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="32740-133">No entanto, há disponibilidade de mais informações sobre as entradas que permitem maior otimização durante o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="32740-133">However more information about the inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="32740-134">O Tez usa técnicas de otimização contínua que permitem otimizar ainda mais o plano mais adiante na fase de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="32740-134">Tez uses continuous optimization techniques that allows it to optimize the plan further into the runtime phase.</span></span>

<span data-ttu-id="32740-135">Para obter mais detalhes sobre esses conceitos, consulte [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="32740-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="32740-136">Você pode fazer qualquer consulta do Hive habilitada pelo Tez prefixando a consulta com a configuração abaixo:</span><span class="sxs-lookup"><span data-stu-id="32740-136">You can make any Hive query Tez enabled by prefixing the query with the setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="32740-137">Clusters HDInsight baseados em Linux têm o Tez habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="32740-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="32740-138">Particionamento do Hive</span><span class="sxs-lookup"><span data-stu-id="32740-138">Hive partitioning</span></span>

<span data-ttu-id="32740-139">A operação de E/S é o principal gargalo de desempenho para executar consultas do Hive.</span><span class="sxs-lookup"><span data-stu-id="32740-139">I/O operation is the major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="32740-140">O desempenho pode ser melhorado se a quantidade de dados que precisam ser lidos puder ser reduzida.</span><span class="sxs-lookup"><span data-stu-id="32740-140">The performance can be improved if the amount of data that needs to be read can be reduced.</span></span> <span data-ttu-id="32740-141">Por padrão, consultas do Hive examinam tabelas inteiras do Hive.</span><span class="sxs-lookup"><span data-stu-id="32740-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="32740-142">Isso é ótimo para consultas como verificações de tabela.</span><span class="sxs-lookup"><span data-stu-id="32740-142">This is great for queries like table scans.</span></span> <span data-ttu-id="32740-143">Porém, para consultas que só precisam verificar uma pequena quantidade de dados (por exemplo, consultas com filtragem), esse comportamento cria uma sobrecarga desnecessária.</span><span class="sxs-lookup"><span data-stu-id="32740-143">However for queries that only need to scan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="32740-144">O particionamento do Hive permite que as consultas do Hive acessem somente a quantidade necessária de dados nas tabelas do Hive.</span><span class="sxs-lookup"><span data-stu-id="32740-144">Hive partitioning allows Hive queries to access only the necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="32740-145">O particionamento do Hive é implementado reorganizando os dados brutos em novos diretórios, em que cada partição tem seu próprio diretório - onde a partição é definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="32740-145">Hive partitioning is implemented by reorganizing the raw data into new directories with each partition having its own directory - where the partition is defined by the user.</span></span> <span data-ttu-id="32740-146">O diagrama a seguir ilustra o particionamento de uma tabela do Hive pela coluna *Ano*.</span><span class="sxs-lookup"><span data-stu-id="32740-146">The following diagram illustrates partitioning a Hive table by the column *Year*.</span></span> <span data-ttu-id="32740-147">Um novo diretório é criado para cada ano.</span><span class="sxs-lookup"><span data-stu-id="32740-147">A new directory is created for each year.</span></span>

![particionamento][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="32740-149">Algumas considerações sobre particionamento:</span><span class="sxs-lookup"><span data-stu-id="32740-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="32740-150">**Não particione pouco demais** – O particionamento em colunas com apenas alguns valores pode causar poucas partições.</span><span class="sxs-lookup"><span data-stu-id="32740-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="32740-151">Por exemplo, o particionamento por gênero só cria duas partições (“masculino” e “feminino”), reduzindo a latência no máximo pela metade.</span><span class="sxs-lookup"><span data-stu-id="32740-151">For example, partitioning on gender only creates two partitions to be created (male and female), thus only reduce the latency by a maximum of half.</span></span>
* <span data-ttu-id="32740-152">**Não particione muito demais** – No outro extremo, criar uma partição em uma coluna com um valor exclusivo (por exemplo, userid) causa várias partições.</span><span class="sxs-lookup"><span data-stu-id="32740-152">**Do not over partition** - On the other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="32740-153">Partição demais causa muita carga sobre namenode do cluster porque ele precisa manipular o grande número de diretórios.</span><span class="sxs-lookup"><span data-stu-id="32740-153">Over partition causes much stress on the cluster namenode as it has to handle the large number of directories.</span></span>
* <span data-ttu-id="32740-154">**Evite distorção de dados** -Escolha com bom senso sua chave de particionamento para que todas as partições tenham o mesmo tamanho.</span><span class="sxs-lookup"><span data-stu-id="32740-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="32740-155">Um exemplo: o particionamento em *Estado* pode fazer com que o número de registros em “Califórnia” seja quase 30 vezes o número em “Vermont” devido à diferença de população.</span><span class="sxs-lookup"><span data-stu-id="32740-155">An example is partitioning on *State* may cause the number of records under California to be almost 30x that of Vermont due to the difference in population.</span></span>

<span data-ttu-id="32740-156">Para criar uma tabela de partição, use a cláusula *Particionado por* :</span><span class="sxs-lookup"><span data-stu-id="32740-156">To create a partition table, use the *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="32740-157">Depois de criar a tabela particionada, você pode criar particionamento estático ou dinâmico.</span><span class="sxs-lookup"><span data-stu-id="32740-157">Once the partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="32740-158">**Particionamento estático** significa que você já fragmentou os dados nos diretórios apropriados e pode solicitar partições do Hive manualmente com base no local do diretório.</span><span class="sxs-lookup"><span data-stu-id="32740-158">**Static partitioning** means that you have already sharded data in the appropriate directories and you can ask Hive partitions manually based on the directory location.</span></span> <span data-ttu-id="32740-159">O trecho de código a seguir é um exemplo.</span><span class="sxs-lookup"><span data-stu-id="32740-159">The following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="32740-160">**Particionamento dinâmico** significa que você deseja que o Hive crie partições automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="32740-160">**Dynamic partitioning** means that you want Hive to create partitions automatically for you.</span></span> <span data-ttu-id="32740-161">Como já criamos a tabela de partição a partir da tabela de preparo, só precisamos inserir dados na tabela particionada:</span><span class="sxs-lookup"><span data-stu-id="32740-161">Since we have already created the partitioning table from the staging table, all we need to do is insert data to the partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="32740-162">Para obter mais detalhes, consulte [Tabelas particionadas](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="32740-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-the-orcfile-format"></a><span data-ttu-id="32740-163">Use o formato ORCFile</span><span class="sxs-lookup"><span data-stu-id="32740-163">Use the ORCFile format</span></span>
<span data-ttu-id="32740-164">O Hive dá suporte a vários formatos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="32740-164">Hive supports different file formats.</span></span> <span data-ttu-id="32740-165">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="32740-165">For example:</span></span>

* <span data-ttu-id="32740-166">**Texto**: esse é o formato de arquivo padrão e funciona com a maioria dos cenários</span><span class="sxs-lookup"><span data-stu-id="32740-166">**Text**: this is the default file format and works with most scenarios</span></span>
* <span data-ttu-id="32740-167">**Avro**: funciona bem para cenários de interoperabilidade</span><span class="sxs-lookup"><span data-stu-id="32740-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="32740-168">**ORC/Parquet**: mais adequada para desempenho</span><span class="sxs-lookup"><span data-stu-id="32740-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="32740-169">O formato ORC é uma maneira altamente eficiente para armazenar dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="32740-169">ORC (Optimized Row Columnar) format is a highly efficient way to store Hive data.</span></span> <span data-ttu-id="32740-170">Comparado a outros formatos, o ORC tem as seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="32740-170">Compared to other formats, ORC has the following advantages:</span></span>

* <span data-ttu-id="32740-171">suporte para tipos complexos, incluindo a data e hora e tipos complexos e semiestruturados</span><span class="sxs-lookup"><span data-stu-id="32740-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="32740-172">até 70% de compactação</span><span class="sxs-lookup"><span data-stu-id="32740-172">up to 70% compression</span></span>
* <span data-ttu-id="32740-173">indexa a cada 10.000 linhas, o que permite ignorar linhas de índices</span><span class="sxs-lookup"><span data-stu-id="32740-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="32740-174">uma redução significativa no tempo de execução</span><span class="sxs-lookup"><span data-stu-id="32740-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="32740-175">Para habilitar o formato ORC, primeiro você deve criar uma tabela com a cláusula *Armazenado como ORC*:</span><span class="sxs-lookup"><span data-stu-id="32740-175">To enable ORC format, you first create a table with the clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="32740-176">Em seguida, insira dados na tabela ORC a partir da tabela de preparo.</span><span class="sxs-lookup"><span data-stu-id="32740-176">Next, you insert data to the ORC table from the staging table.</span></span> <span data-ttu-id="32740-177">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="32740-177">For example:</span></span>

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

<span data-ttu-id="32740-178">Você pode ler mais sobre o formato ORC [aqui](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="32740-178">You can read more on the ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="32740-179">Vetorização</span><span class="sxs-lookup"><span data-stu-id="32740-179">Vectorization</span></span>

<span data-ttu-id="32740-180">A vetorização permite que o Hive processe um lote de 1.024 linhas juntas em vez de processar uma linha por vez.</span><span class="sxs-lookup"><span data-stu-id="32740-180">Vectorization allows Hive to process a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="32740-181">Isso significa que operações simples são concluídas mais rapidamente porque menos código interno precisa ser executado.</span><span class="sxs-lookup"><span data-stu-id="32740-181">It means that simple operations are done faster because less internal code needs to run.</span></span>

<span data-ttu-id="32740-182">Para habilitar a vetorização, prefixe sua consulta do Hive com a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="32740-182">To enable vectorization prefix your Hive query with the following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="32740-183">Para obter mais informações, consulte [Execução de consultas vetorizadas](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="32740-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="32740-184">Outros métodos de otimização</span><span class="sxs-lookup"><span data-stu-id="32740-184">Other optimization methods</span></span>
<span data-ttu-id="32740-185">Há mais métodos de otimização que você pode considerar, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="32740-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="32740-186">**Bucketing do Hive:** uma técnica que permite clusterizar ou segmentar grandes conjuntos de dados para otimizar o desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="32740-186">**Hive bucketing:** a technique that allows to cluster or segment large sets of data to optimize query performance.</span></span>
* <span data-ttu-id="32740-187">**Otimização de junção:** otimização do planejamento da execução de consultas do Hive para melhorar a eficiência de junções e reduzir a necessidade de dicas de usuário.</span><span class="sxs-lookup"><span data-stu-id="32740-187">**Join optimization:** optimization of Hive's query execution planning to improve the efficiency of joins and reduce the need for user hints.</span></span> <span data-ttu-id="32740-188">Para obter mais informações, consulte [Otimização de junção](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="32740-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="32740-189">**Aumentar redutores**.</span><span class="sxs-lookup"><span data-stu-id="32740-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32740-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="32740-190">Next steps</span></span>
<span data-ttu-id="32740-191">Neste artigo, você aprendeu a vários métodos comuns de otimização de consultas do Hive.</span><span class="sxs-lookup"><span data-stu-id="32740-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="32740-192">Para saber mais, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="32740-192">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="32740-193">Usar o Apache Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="32740-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="32740-194">Analisar dados de atrasos de voos usando o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="32740-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="32740-195">Analisar dados do Twitter usando o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="32740-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="32740-196">Analisar dados de sensor usando o Console de Consulta do Hive no Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="32740-196">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="32740-197">Usar o Hive com o HDInsight para analisar logs de sites</span><span class="sxs-lookup"><span data-stu-id="32740-197">Use Hive with HDInsight to analyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
