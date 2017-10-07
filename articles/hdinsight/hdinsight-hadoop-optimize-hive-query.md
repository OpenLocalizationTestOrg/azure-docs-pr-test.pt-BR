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
# <a name="optimize-hive-queries-in-azure-hdinsight"></a>Otimizar consultas do Hive no Azure HDInsight | Microsoft Docs

Por padrão, os clusters do Hadoop não são otimizados para desempenho. Este artigo aborda alguns métodos de otimização de desempenho Hive mais comuns que você pode aplicar tooyour consultas.

## <a name="scale-out-worker-nodes"></a>Escalar nós de trabalho horizontalmente

Aumentar Olá número de nós de trabalho em um cluster pode aproveitar mais toobe mapeadores e reducers executado em paralelo. Há duas maneiras de aumentar a escalabilidade horizontal no HDInsight:

* No momento de provisionar hello, você pode especificar o número de saudação de nós de trabalho usando Olá portal do Azure, o Azure PowerShell ou a interface de linha de comando de plataforma cruzada.  Para saber mais, veja [Criar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Olá seguinte captura de tela mostra trabalho Olá nó configuração em Olá portal do Azure:
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* Em tempo de execução de hello, você também pode expandir um cluster sem recriar um:

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

Para obter mais informações sobre as máquinas virtuais diferentes Olá HDInsight com suporte, consulte [preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="enable-tez"></a>Habilitar o Tez

[Apache Tez](http://hortonworks.com/hadoop/tez/) é um alternativa de execução toohello MapReduce mecanismo:

![tez_1][image-hdi-optimize-hive-tez_1]

O Tez é mais rápido porque:

* **Execute o gráfico acíclico direcionado (DAG) como um único trabalho no mecanismo de MapReduce Olá**. Olá DAG requer que cada conjunto de mapeadores toobe seguido de um conjunto de reducers. Isso faz com que vários toobe de trabalhos de MapReduce será levado para cada consulta de Hive. O Tez não tem essa restrição e pode processar DAG complexo como um único trabalho, minimizando a sobrecarga de inicialização de trabalho.
* **Evita gravações desnecessárias**. Devido a trabalhos toomultiple sendo girados para Olá mesma consulta de Hive no mecanismo de MapReduce hello, saída de saudação de cada trabalho é gravada tooHDFS para dados intermediários. Como Tez minimiza o número de trabalhos para cada consulta de Hive é tooavoid capaz de gravação de desnecessários.
* **Minimiza atrasos de inicialização**. Tez é melhor atraso de inicialização toominimize capaz reduzindo o número de saudação de mapeadores precisa toostart e também melhorar otimização em todo.
* **Reutiliza contêineres**. Sempre que possível Tez é capaz de tooreuse contêineres tooensure que a latência devido toostarting backup contêineres é reduzido.
* **Técnicas de otimização contínua**. Tradicionalmente, a otimização ocorria durante a fase de compilação. No entanto, para obter mais informações sobre entradas de saudação que permitem melhor otimização durante o tempo de execução. Tez usa técnicas de otimização contínua que permite que ele toooptimize plano de saudação adicional na fase de tempo de execução de saudação.

Para obter mais detalhes sobre esses conceitos, consulte [Apache TEZ](http://hortonworks.com/hadoop/tez/).

Você pode tornar qualquer consulta de Hive Tez habilitado, prefixando consulta Olá com configuração de saudação abaixo:

    set hive.execution.engine=tez;

Clusters HDInsight baseados em Linux têm o Tez habilitado por padrão.


## <a name="hive-partitioning"></a>Particionamento do Hive

Operação de e/s é um afunilamento de desempenho principais de saudação para executar consultas de Hive. Olá possível melhorar o desempenho se quantidade Olá dos dados que precisam toobe leitura pode ser reduzido. Por padrão, consultas do Hive examinam tabelas inteiras do Hive. Isso é ótimo para consultas como verificações de tabela. No entanto para consultas que precisam apenas de tooscan uma pequena quantidade de dados (por exemplo, consultas com filtragem), esse comportamento cria sobrecarga desnecessário. Particionamento de hive permite Hive consultas tooaccess somente Olá necessário quantidade de dados nas tabelas de Hive.

Particionamento de hive é implementado por reorganização de dados brutos de saudação em novos diretórios com cada partição ter seu próprio diretório - onde a partição de saudação é definida pelo usuário hello. Olá diagrama a seguir ilustra o particionamento de uma tabela Hive pela coluna Olá *ano*. Um novo diretório é criado para cada ano.

![particionamento][image-hdi-optimize-hive-partitioning_1]

Algumas considerações sobre particionamento:

* **Não particione pouco demais** – O particionamento em colunas com apenas alguns valores pode causar poucas partições. Por exemplo, particionamento gênero só cria dois toobe partições criadas (masculino e feminino), reduzindo latência Olá somente por um máximo de metade.
* **Não estenda partição** - no Olá outro extremo, criando uma partição em uma coluna com um valor exclusivo (por exemplo, userid) faz com que várias partições. Partição faz com que muito estresse em Olá namenode de cluster que tem toohandle Olá grande número de diretórios.
* **Evite distorção de dados** -Escolha com bom senso sua chave de particionamento para que todas as partições tenham o mesmo tamanho. Um exemplo é o particionamento em *estado* pode fazer com que Olá número de registros na Califórnia toobe quase 30 x que Vermont devido toohello diferença na população.

toocreate uma tabela de partição, use Olá *particionada por* cláusula:

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

Depois de criar a tabela particionada hello, você pode criar particionamento estático ou o particionamento dinâmico.

* **Particionamento estático** significa que você tenha dados fragmentados já no hello apropriado diretórios e solicite Hive partições manualmente com base no local do diretório de saudação. saudação de trecho de código a seguir é um exemplo.
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* **O particionamento dinâmico** significa que você deseja Hive toocreate partições automaticamente para você. Como já criamos Olá particionamento de tabela da tabela de preparo de hello, todos os nós precisamos toodo é inserir dados toohello particionada tabela:
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

Para obter mais detalhes, consulte [Tabelas particionadas](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).

## <a name="use-hello-orcfile-format"></a>Use o formato de saudação ORCFile
O Hive dá suporte a vários formatos de arquivo. Por exemplo:

* **Texto**: Este é o formato de arquivo padrão hello e funciona com a maioria dos cenários
* **Avro**: funciona bem para cenários de interoperabilidade
* **ORC/Parquet**: mais adequada para desempenho

Formato ORC (Colunar otimização de linha) é um toostore de maneira altamente eficiente os dados de Hive. Formatos de tooother comparados, ORC tem Olá vantagens a seguir:

* suporte para tipos complexos, incluindo a data e hora e tipos complexos e semiestruturados
* a compactação de % too70
* indexa a cada 10.000 linhas, o que permite ignorar linhas de índices
* uma redução significativa no tempo de execução

formato ORC tooenable, primeiro você cria uma tabela com cláusula Olá *armazenado como ORC*:

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

Em seguida, você deve inserir tabela de dados de ORC toohello da tabela de preparo de saudação. Por exemplo:

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

Você pode ler mais no formato ORC Olá [aqui](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).

## <a name="vectorization"></a>Vetorização

Vetorização permite Hive tooprocess um lote de 1024 juntos linhas em vez de processar uma linha por vez. Isso significa que operações simples são mais rapidamente porque menos código interno precisa toorun.

tooenable vetorização prefixo sua consulta de Hive com hello configuração a seguir:

    set hive.vectorized.execution.enabled = true;

Para obter mais informações, consulte [Execução de consultas vetorizadas](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).

## <a name="other-optimization-methods"></a>Outros métodos de otimização
Há mais métodos de otimização que você pode considerar, por exemplo:

* **Particionamento de hive:** uma técnica que permite toocluster ou segmento grandes conjuntos de desempenho de consulta de toooptimize de dados.
* **Otimização da junção:** otimização da execução da consulta do Hive planejamento tooimprove Olá eficiência de junções e reduzir a necessidade de saudação de dicas de usuário. Para obter mais informações, consulte [Otimização de junção](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).
* **Aumentar redutores**.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu a vários métodos comuns de otimização de consultas do Hive. toolearn mais, consulte Olá artigos a seguir:

* [Usar o Apache Hive no HDInsight](hdinsight-use-hive.md)
* [Analisar dados de atrasos de voos usando o Hive no HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Analisar dados do Twitter usando o Hive no HDInsight](hdinsight-analyze-twitter-data.md)
* [Analisar dados de sensor usando Olá Console de consulta de Hive no Hadoop no HDInsight](hdinsight-hive-analyze-sensor-data.md)
* [Use o Hive com HDInsight tooanalyze logs de sites](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
