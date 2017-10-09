---
title: aaaTroubleshoot Hive usando o Azure HDInsight | Microsoft Docs
description: Obter respostas a perguntas toocommon sobre como trabalhar com o Apache Hive e do Azure HDInsight.
keywords: "Azure HDInsight, Hive, perguntas frequentes, guia de solução de problemas, perguntas comuns"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a>Solucionar problemas do Hive usando o Azure HDInsight

Saiba mais sobre Olá principais perguntas e suas resoluções durante o trabalho com o Apache Hive cargas no Apache Ambari.


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a>Como fazer para exportar um metastore do Hive e importá-lo para outro cluster


### <a name="resolution-steps"></a>Etapas de resolução

1. Conecte o cluster do HDInsight toohello usando um cliente do Secure Shell (SSH). Para saber mais, veja [Leituras adicionais](#additional-reading-end).

2. Execute Olá comando a seguir no cluster do HDInsight de saudação do qual você deseja tooexport Olá metastore:

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  Este comando gera um arquivo chamado allatables.sql.

3. Copiar Olá arquivo alltables.sql toohello novo cluster HDInsight e execute Olá comando a seguir:

  ```apache
  hive -f alltables.sql
  ```

código de saudação nas etapas de resolução de saudação supõe que dados são caminhos no cluster novo Olá Olá mesmo como caminhos de dados Olá no cluster antigo hello. Se os caminhos de dados Olá forem diferentes, você pode editar manualmente Olá gerado alltables.sql arquivo tooreflect quaisquer alterações.

### <a name="additional-reading"></a>Leitura adicional

- [Conecte-se o cluster do HDInsight tooan usando SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a>Como fazer para localizar logs do Hive em um cluster

### <a name="resolution-steps"></a>Etapas de resolução

1. Conecte o cluster do HDInsight toohello usando o SSH. Para saber mais, veja **Leituras adicionais**.

2. logs de cliente do Hive tooview, use Olá comando a seguir:

  ```apache
  /tmp/<username>/hive.log 
  ```

3. tooview Hive metastore logs, use Olá comando a seguir:

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. tooview Hiveserver logs, use Olá comando a seguir:

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a>Leitura adicional

- [Conecte-se o cluster do HDInsight tooan usando SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a>Como iniciar o hello Hive shell com configurações específicas em um cluster

### <a name="resolution-steps"></a>Etapas de resolução

1. Especifique um par chave-valor de configuração quando você iniciar Olá Hive shell. Para saber mais, veja [Leituras adicionais](#additional-reading-end).

  ```apache
  hive -hiveconf a=b 
  ```

2. toolist todas as configurações efetivas no shell de Hive, Olá uso a seguir de comando:

  ```apache
  hive> set;
  ```

  Por exemplo, use Olá a seguir do shell de comando do Hive toostart com habilitado no console de saudação do log de depuração:

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a>Leitura adicional

- [Propriedades de configuração do Hive](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Como fazer para analisar dados de DAG do Tez em um caminho crítico do cluster


### <a name="resolution-steps"></a>Etapas de resolução
 
1. tooanalyze um Tez Apache direcionado gráfico acíclico (DAG) em um gráfico de cluster crítico, conecte-se o cluster do HDInsight toohello usando o SSH. Para saber mais, veja [Leituras adicionais](#additional-reading-end).

2. Em um prompt de comando, execute Olá comando a seguir:
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. toolist outros analisadores que podem ser usado tooanalyze Tez DAG, use Olá comando a seguir:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  Você deve fornecer um programa de exemplo como primeiro argumento de saudação.

  Nomes de programa válidos incluem:
    - **ContainerReuseAnalyzer**: imprimir detalhes de reutilização do contêiner em um DAG
    - **CriticalPath**: caminho crítico de saudação de localização de um DAG
    - **LocalityAnalyzer**: imprimir detalhes de localidade em um DAG
    - **ShuffleTimeAnalyzer**: analisar os detalhes de tempo de ordem aleatória Olá em um DAG
    - **SkewAnalyzer**: analisar os detalhes de distorção Olá em um DAG
    - **SlowNodeAnalyzer**: imprimir detalhes do nó em um DAG
    - **SlowTaskIdentifier**: imprimir detalhes de tarefa lenta em um DAG
    - **SlowestVertexAnalyzer**: imprimir detalhes do vértice mais lento em um DAG
    - **SpillAnalyzer**: imprimir detalhes de despejo em um DAG
    - **TaskConcurrencyAnalyzer**: Imprimir Olá detalhes de simultaneidade de tarefa em um DAG
    - **VertexLevelCriticalPathAnalyzer**: caminho crítico de saudação de localizar no nível de vértice em um DAG


### <a name="additional-reading"></a>Leitura adicional

- [Conecte-se o cluster do HDInsight tooan usando SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a>Como fazer para baixar dados de DAG do Tez de um cluster


#### <a name="resolution-steps"></a>Etapas de resolução

Há duas maneiras de dados de DAG Tez toocollect saudação:

- Olá linha de comando:
 
    Conecte o cluster do HDInsight toohello usando o SSH. No prompt de comando hello, execute Olá comando a seguir:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- Use Olá Ambari Tez exibição:
   
  1. Vá tooAmbari. 
  2. Exibição de tooTez vá (no ícone de blocos de saudação no canto superior direito de saudação). 
  3. Selecione Olá DAG tooview desejado.
  4. Selecione **Baixar dados**.

### <a name="additional-reading-end"></a>Leitura adicional

[Conecte-se o cluster do HDInsight tooan usando SSH](hdinsight-hadoop-linux-use-ssh-unix.md)






