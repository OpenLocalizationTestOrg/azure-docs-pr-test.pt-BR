---
title: aaaTroubleshoot Spark usando o Azure HDInsight | Microsoft Docs
description: Obter respostas a perguntas toocommon sobre como trabalhar com o Apache Spark e HDInsight do Azure.
keywords: "Azure HDInsight, Spark, perguntas frequentes, guia de solução de problemas, problemas comuns, configuração de aplicativo, Ambari"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 25D89586-DE5B-4268-B5D5-CC2CE12207ED
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: c9f910daf295462238a3143ae2589db6d383097f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a>Solucionar problemas do Spark usando o Azure HDInsight

Saiba mais sobre questões hello e suas resoluções durante o trabalho com cargas Apache Spark no Apache Ambari.

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a>Como fazer para configurar um aplicativo Spark usando Ambari nos clusters

### <a name="resolution-steps"></a>Etapas de resolução

os valores de configuração de saudação para esse procedimento foram definidos anteriormente no HDInsight. Consulte toodetermine quais configurações Spark precisam de valores de conjunto e toowhat toobe, [o que faz com que um Spark aplicativo OutofMemoryError exceção](#what-causes-a-spark-application-outofmemoryerror-exception). 

1. Na lista de saudação de clusters, selecionar **Spark2**.

    ![Selecione o cluster na lista](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. Selecione Olá **configurações** guia.

    ![Selecione a guia de configurações de saudação](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. Na lista de saudação de configurações, selecione **padrões de spark2 personalizado**.

    ![Selecione custom-spark-defaults](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. Procure valor Olá configuração que você precisa tooadjust, como **spark.executor.memory**. Olá nesse caso, o valor de **4608m** é muito alta.

    ![Selecione o campo de spark.executor.memory Olá](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. Configuração recomendada do conjunto Olá valor toohello. Olá valor **2048m** é recomendado para essa configuração.

    ![Alterar valor too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. Salvar Olá valor e, em seguida, salvar a configuração de saudação. Na barra de ferramentas hello, selecione **salvar**.

    ![Salvar a configuração e a configuração de saudação](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    Você será notificado se todas as configurações precisarem de atenção. Observe Olá itens e, em seguida, selecione **continuar assim mesmo**. 

    ![Selecione Continuar Assim Mesmo](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    Escreva uma nota sobre alterações de configuração hello e, em seguida, selecione **salvar**.

    ![Digite uma observação sobre alterações Olá feitas](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. Sempre que uma configuração é salva, você será solicitado toorestart serviço de saudação. Selecione **Reiniciar**.

    ![Selecione reiniciar](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    Confirme a reinicialização de saudação.

    ![Selecione Confirmar Reiniciar Tudo](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    Você pode analisar os processos de Olá que estão em execução.

    ![Examinar processos em execução](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. Você pode adicionar configurações. Na lista de saudação de configurações, selecione **padrões de spark2 personalizado**e, em seguida, selecione **adicionar propriedade**.

    ![Selecione adicionar propriedade](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. Defina uma nova propriedade. Você pode definir uma única propriedade por meio de uma caixa de diálogo para configurações específicas, como o tipo de dados de saudação. Ou você pode definir várias propriedades usando uma definição por linha. 

    Neste exemplo, Olá **spark.driver.memory** propriedade é definida com um valor de **4g**.

    ![Definir nova propriedade](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. Salvar configuração hello e, em seguida, reinicie o serviço de saudação conforme descrito nas etapas 6 e 7.

Essas alterações são todo o cluster, mas podem ser substituídas quando você enviar Olá Spark trabalho.

### <a name="additional-reading"></a>Leitura adicional

[Envio de trabalho do Spark em clusters do HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a>Como fazer para configurar um aplicativo Spark usando um bloco de anotações do Jupyter nos clusters

### <a name="resolution-steps"></a>Etapas de resolução

1. Consulte toodetermine quais configurações Spark precisam de valores de conjunto e toowhat toobe, [o que faz com que um Spark aplicativo OutofMemoryError exceção](#what-causes-a-spark-application-outofmemoryerror-exception).

2. Na primeira célula Olá de anotações do Jupyter hello, após a saudação **% % configurar** diretiva, especifique as configurações do Spark Olá no formato JSON válido. Altere os valores reais Olá conforme necessário:

    ![Adicionar uma configuração](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a>Leitura adicional

[Envio de trabalho do Spark em clusters do HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a>Como fazer para configurar um aplicativo Spark usando Livy nos clusters

### <a name="resolution-steps"></a>Etapas de resolução

1. Consulte toodetermine quais configurações Spark precisam de valores de conjunto e toowhat toobe, [o que faz com que um Spark aplicativo OutofMemoryError exceção](#what-causes-a-spark-application-outofmemoryerror-exception). 

2. Envie Olá Spark aplicativo tooLivy usando um cliente REST como rotação. Use um comando semelhante toohello a seguir. Altere os valores reais Olá conforme necessário:

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a>Leitura adicional

[Envio de trabalho do Spark em clusters do HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a>Como fazer para configurar um aplicativo Spark usando spark-sumbit nos clusters

### <a name="resolution-steps"></a>Etapas de resolução

1. Consulte toodetermine quais configurações Spark precisam de valores de conjunto e toowhat toobe, [o que faz com que um Spark aplicativo OutofMemoryError exceção](#what-causes-a-spark-application-outofmemoryerror-exception).

2. Inicie o shell do spark usando uma comando semelhante toohello a seguir. Altere o valor real de saudação das configurações de saudação conforme necessário: 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a>Leitura adicional

[Envio de trabalho do Spark em clusters do HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a>O que causa uma exceção OutofMemoryError de um aplicativo Spark

### <a name="detailed-description"></a>Descrição detalhada

Olá aplicativo Spark falha, com os seguintes tipos de exceções não capturadas de saudação:

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a>Causa provável

a causa mais provável Olá dessa exceção é que não há memória de heap é alocada a máquinas virtuais de Java toohello (JVMs). Esses JVMs são iniciados como executores ou drivers como parte da saudação aplicativo Spark. 

### <a name="resolution-steps"></a>Etapas de resolução

1. Determine o tamanho máximo de saudação de identificadores de aplicativo hello dados Olá Spark. Você pode fazer uma estimativa com base no tamanho máximo de saudação de dados de entrada hello, dados intermediários de saudação produzida pela transformação de dados de entrada hello e dados de saída de saudação que são gerados quando o aplicativo hello é ainda mais transformar dados intermediários hello. Esse processo poderá ser iterativo se você não puder fazer uma previsão inicial formal. 

2. Certifique-se de cluster HDInsight Olá que vai toouse tem recursos suficientes em termos de memória e núcleos o aplicativo de Spark do tooaccommodate hello. Você pode determinar isso exibindo a seção de métricas de cluster de saudação do hello YARN da interface do usuário para valores de saudação do **memória usada** vs. **Total de Memória** e de **VCores Usados** versus **VCores Totais**.

3. Defina Olá seguir Spark configurações tooappropriate valores, que não devem exceder 90% da memória disponível hello e núcleos. Olá valores devem ser bem em requisitos de memória de saudação do hello aplicativo Spark: 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    tooget Olá total de memória usada por todos os executores executados Olá comando a seguir: 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    tooget Olá total de memória usada pelo driver hello, executar Olá comando a seguir:
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a>Leitura adicional

- [Visão geral do gerenciamento de memória do Spark](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [Depurar um aplicativo Spark em um cluster HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)

