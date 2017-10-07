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
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="e67d2-104">Solucionar problemas do Spark usando o Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e67d2-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="e67d2-105">Saiba mais sobre questões hello e suas resoluções durante o trabalho com cargas Apache Spark no Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="e67d2-105">Learn about hello top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="e67d2-106">Como fazer para configurar um aplicativo Spark usando Ambari nos clusters</span><span class="sxs-lookup"><span data-stu-id="e67d2-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="e67d2-107">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="e67d2-107">Resolution steps</span></span>

<span data-ttu-id="e67d2-108">os valores de configuração de saudação para esse procedimento foram definidos anteriormente no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e67d2-108">hello configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="e67d2-109">Consulte toodetermine quais configurações Spark precisam de valores de conjunto e toowhat toobe, [o que faz com que um Spark aplicativo OutofMemoryError exceção](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="e67d2-109">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="e67d2-110">Na lista de saudação de clusters, selecionar **Spark2**.</span><span class="sxs-lookup"><span data-stu-id="e67d2-110">In hello list of clusters, select **Spark2**.</span></span>

    ![Selecione o cluster na lista](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="e67d2-112">Selecione Olá **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="e67d2-112">Select hello **Configs** tab.</span></span>

    ![Selecione a guia de configurações de saudação](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="e67d2-114">Na lista de saudação de configurações, selecione **padrões de spark2 personalizado**.</span><span class="sxs-lookup"><span data-stu-id="e67d2-114">In hello list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![Selecione custom-spark-defaults](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="e67d2-116">Procure valor Olá configuração que você precisa tooadjust, como **spark.executor.memory**.</span><span class="sxs-lookup"><span data-stu-id="e67d2-116">Look for hello value setting that you need tooadjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="e67d2-117">Olá nesse caso, o valor de **4608m** é muito alta.</span><span class="sxs-lookup"><span data-stu-id="e67d2-117">In this case, hello value of **4608m** is too high.</span></span>

    ![Selecione o campo de spark.executor.memory Olá](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="e67d2-119">Configuração recomendada do conjunto Olá valor toohello.</span><span class="sxs-lookup"><span data-stu-id="e67d2-119">Set hello value toohello recommended setting.</span></span> <span data-ttu-id="e67d2-120">Olá valor **2048m** é recomendado para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="e67d2-120">hello value **2048m** is recommended for this setting.</span></span>

    ![Alterar valor too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="e67d2-122">Salvar Olá valor e, em seguida, salvar a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="e67d2-122">Save hello value, and then save hello configuration.</span></span> <span data-ttu-id="e67d2-123">Na barra de ferramentas hello, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="e67d2-123">On hello toolbar, select **Save**.</span></span>

    ![Salvar a configuração e a configuração de saudação](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="e67d2-125">Você será notificado se todas as configurações precisarem de atenção.</span><span class="sxs-lookup"><span data-stu-id="e67d2-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="e67d2-126">Observe Olá itens e, em seguida, selecione **continuar assim mesmo**.</span><span class="sxs-lookup"><span data-stu-id="e67d2-126">Note hello items, and then select **Proceed Anyway**.</span></span> 

    ![Selecione Continuar Assim Mesmo](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="e67d2-128">Escreva uma nota sobre alterações de configuração hello e, em seguida, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="e67d2-128">Write a note about hello configuration changes, and then select **Save**.</span></span>

    ![Digite uma observação sobre alterações Olá feitas](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="e67d2-130">Sempre que uma configuração é salva, você será solicitado toorestart serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="e67d2-130">Whenever a configuration is saved, you are prompted toorestart hello service.</span></span> <span data-ttu-id="e67d2-131">Selecione **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="e67d2-131">Select **Restart**.</span></span>

    ![Selecione reiniciar](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="e67d2-133">Confirme a reinicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="e67d2-133">Confirm hello restart.</span></span>

    ![Selecione Confirmar Reiniciar Tudo](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="e67d2-135">Você pode analisar os processos de Olá que estão em execução.</span><span class="sxs-lookup"><span data-stu-id="e67d2-135">You can review hello processes that are running.</span></span>

    ![Examinar processos em execução](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="e67d2-137">Você pode adicionar configurações.</span><span class="sxs-lookup"><span data-stu-id="e67d2-137">You can add configurations.</span></span> <span data-ttu-id="e67d2-138">Na lista de saudação de configurações, selecione **padrões de spark2 personalizado**e, em seguida, selecione **adicionar propriedade**.</span><span class="sxs-lookup"><span data-stu-id="e67d2-138">In hello list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![Selecione adicionar propriedade](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="e67d2-140">Defina uma nova propriedade.</span><span class="sxs-lookup"><span data-stu-id="e67d2-140">Define a new property.</span></span> <span data-ttu-id="e67d2-141">Você pode definir uma única propriedade por meio de uma caixa de diálogo para configurações específicas, como o tipo de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e67d2-141">You can define a single property by using a dialog box for specific settings such as hello data type.</span></span> <span data-ttu-id="e67d2-142">Ou você pode definir várias propriedades usando uma definição por linha.</span><span class="sxs-lookup"><span data-stu-id="e67d2-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="e67d2-143">Neste exemplo, Olá **spark.driver.memory** propriedade é definida com um valor de **4g**.</span><span class="sxs-lookup"><span data-stu-id="e67d2-143">In this example, hello **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![Definir nova propriedade](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="e67d2-145">Salvar configuração hello e, em seguida, reinicie o serviço de saudação conforme descrito nas etapas 6 e 7.</span><span class="sxs-lookup"><span data-stu-id="e67d2-145">Save hello configuration, and then restart hello service as described in steps 6 and 7.</span></span>

<span data-ttu-id="e67d2-146">Essas alterações são todo o cluster, mas podem ser substituídas quando você enviar Olá Spark trabalho.</span><span class="sxs-lookup"><span data-stu-id="e67d2-146">These changes are cluster-wide but can be overridden when you submit hello Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="e67d2-147">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="e67d2-147">Additional reading</span></span>

[<span data-ttu-id="e67d2-148">Envio de trabalho do Spark em clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="e67d2-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="e67d2-149">Como fazer para configurar um aplicativo Spark usando um bloco de anotações do Jupyter nos clusters</span><span class="sxs-lookup"><span data-stu-id="e67d2-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="e67d2-150">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="e67d2-150">Resolution steps</span></span>

1. <span data-ttu-id="e67d2-151">Consulte toodetermine quais configurações Spark precisam de valores de conjunto e toowhat toobe, [o que faz com que um Spark aplicativo OutofMemoryError exceção](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="e67d2-151">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="e67d2-152">Na primeira célula Olá de anotações do Jupyter hello, após a saudação **% % configurar** diretiva, especifique as configurações do Spark Olá no formato JSON válido.</span><span class="sxs-lookup"><span data-stu-id="e67d2-152">In hello first cell of hello Jupyter notebook, after hello **%%configure** directive, specify hello Spark configurations in valid JSON format.</span></span> <span data-ttu-id="e67d2-153">Altere os valores reais Olá conforme necessário:</span><span class="sxs-lookup"><span data-stu-id="e67d2-153">Change hello actual values as necessary:</span></span>

    ![Adicionar uma configuração](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="e67d2-155">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="e67d2-155">Additional reading</span></span>

[<span data-ttu-id="e67d2-156">Envio de trabalho do Spark em clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="e67d2-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="e67d2-157">Como fazer para configurar um aplicativo Spark usando Livy nos clusters</span><span class="sxs-lookup"><span data-stu-id="e67d2-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="e67d2-158">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="e67d2-158">Resolution steps</span></span>

1. <span data-ttu-id="e67d2-159">Consulte toodetermine quais configurações Spark precisam de valores de conjunto e toowhat toobe, [o que faz com que um Spark aplicativo OutofMemoryError exceção](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="e67d2-159">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="e67d2-160">Envie Olá Spark aplicativo tooLivy usando um cliente REST como rotação.</span><span class="sxs-lookup"><span data-stu-id="e67d2-160">Submit hello Spark application tooLivy by using a REST client like cURL.</span></span> <span data-ttu-id="e67d2-161">Use um comando semelhante toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="e67d2-161">Use a command similar toohello following.</span></span> <span data-ttu-id="e67d2-162">Altere os valores reais Olá conforme necessário:</span><span class="sxs-lookup"><span data-stu-id="e67d2-162">Change hello actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="e67d2-163">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="e67d2-163">Additional reading</span></span>

[<span data-ttu-id="e67d2-164">Envio de trabalho do Spark em clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="e67d2-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="e67d2-165">Como fazer para configurar um aplicativo Spark usando spark-sumbit nos clusters</span><span class="sxs-lookup"><span data-stu-id="e67d2-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="e67d2-166">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="e67d2-166">Resolution steps</span></span>

1. <span data-ttu-id="e67d2-167">Consulte toodetermine quais configurações Spark precisam de valores de conjunto e toowhat toobe, [o que faz com que um Spark aplicativo OutofMemoryError exceção](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="e67d2-167">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="e67d2-168">Inicie o shell do spark usando uma comando semelhante toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="e67d2-168">Launch spark-shell by using a command similar toohello following.</span></span> <span data-ttu-id="e67d2-169">Altere o valor real de saudação das configurações de saudação conforme necessário:</span><span class="sxs-lookup"><span data-stu-id="e67d2-169">Change hello actual value of hello configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="e67d2-170">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="e67d2-170">Additional reading</span></span>

[<span data-ttu-id="e67d2-171">Envio de trabalho do Spark em clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="e67d2-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="e67d2-172">O que causa uma exceção OutofMemoryError de um aplicativo Spark</span><span class="sxs-lookup"><span data-stu-id="e67d2-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="e67d2-173">Descrição detalhada</span><span class="sxs-lookup"><span data-stu-id="e67d2-173">Detailed description</span></span>

<span data-ttu-id="e67d2-174">Olá aplicativo Spark falha, com os seguintes tipos de exceções não capturadas de saudação:</span><span class="sxs-lookup"><span data-stu-id="e67d2-174">hello Spark application fails, with hello following types of uncaught exceptions:</span></span>

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

### <a name="probable-cause"></a><span data-ttu-id="e67d2-175">Causa provável</span><span class="sxs-lookup"><span data-stu-id="e67d2-175">Probable cause</span></span>

<span data-ttu-id="e67d2-176">a causa mais provável Olá dessa exceção é que não há memória de heap é alocada a máquinas virtuais de Java toohello (JVMs).</span><span class="sxs-lookup"><span data-stu-id="e67d2-176">hello most likely cause of this exception is that not enough heap memory is allocated toohello Java virtual machines (JVMs).</span></span> <span data-ttu-id="e67d2-177">Esses JVMs são iniciados como executores ou drivers como parte da saudação aplicativo Spark.</span><span class="sxs-lookup"><span data-stu-id="e67d2-177">These JVMs are launched as executors or drivers as part of hello Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="e67d2-178">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="e67d2-178">Resolution steps</span></span>

1. <span data-ttu-id="e67d2-179">Determine o tamanho máximo de saudação de identificadores de aplicativo hello dados Olá Spark.</span><span class="sxs-lookup"><span data-stu-id="e67d2-179">Determine hello maximum size of hello data hello Spark application handles.</span></span> <span data-ttu-id="e67d2-180">Você pode fazer uma estimativa com base no tamanho máximo de saudação de dados de entrada hello, dados intermediários de saudação produzida pela transformação de dados de entrada hello e dados de saída de saudação que são gerados quando o aplicativo hello é ainda mais transformar dados intermediários hello.</span><span class="sxs-lookup"><span data-stu-id="e67d2-180">You can make a guess based on hello maximum size of hello input data, hello intermediate data that's produced by transforming hello input data, and hello output data that's produced when hello application is further transforming hello intermediate data.</span></span> <span data-ttu-id="e67d2-181">Esse processo poderá ser iterativo se você não puder fazer uma previsão inicial formal.</span><span class="sxs-lookup"><span data-stu-id="e67d2-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="e67d2-182">Certifique-se de cluster HDInsight Olá que vai toouse tem recursos suficientes em termos de memória e núcleos o aplicativo de Spark do tooaccommodate hello.</span><span class="sxs-lookup"><span data-stu-id="e67d2-182">Make sure that hello HDInsight cluster that you're going toouse has enough resources in terms of memory and cores tooaccommodate hello Spark application.</span></span> <span data-ttu-id="e67d2-183">Você pode determinar isso exibindo a seção de métricas de cluster de saudação do hello YARN da interface do usuário para valores de saudação do **memória usada** vs. **Total de Memória** e de **VCores Usados** versus **VCores Totais**.</span><span class="sxs-lookup"><span data-stu-id="e67d2-183">You can determine this by viewing hello cluster metrics section of hello YARN UI for hello values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="e67d2-184">Defina Olá seguir Spark configurações tooappropriate valores, que não devem exceder 90% da memória disponível hello e núcleos.</span><span class="sxs-lookup"><span data-stu-id="e67d2-184">Set hello following Spark configurations tooappropriate values, which should not exceed 90% of hello available memory and cores.</span></span> <span data-ttu-id="e67d2-185">Olá valores devem ser bem em requisitos de memória de saudação do hello aplicativo Spark:</span><span class="sxs-lookup"><span data-stu-id="e67d2-185">hello values should be well within hello memory requirements of hello Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="e67d2-186">tooget Olá total de memória usada por todos os executores executados Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e67d2-186">tooget hello total memory used by all executors, run hello following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="e67d2-187">tooget Olá total de memória usada pelo driver hello, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e67d2-187">tooget hello total memory used by hello driver, run hello following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="e67d2-188">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="e67d2-188">Additional reading</span></span>

- [<span data-ttu-id="e67d2-189">Visão geral do gerenciamento de memória do Spark</span><span class="sxs-lookup"><span data-stu-id="e67d2-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [<span data-ttu-id="e67d2-190">Depurar um aplicativo Spark em um cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="e67d2-190">Debug a Spark application on an HDInsight cluster</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)

