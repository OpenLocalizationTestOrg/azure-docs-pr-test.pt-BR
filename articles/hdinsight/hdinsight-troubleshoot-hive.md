---
title: Solucionar problemas do Hive usando o Azure HDInsight | Microsoft Docs
description: Obtenha respostas para perguntas comuns sobre como trabalhar com o Apache Hive e o Azure HDInsight.
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
ms.openlocfilehash: 53e9685458190efe6a586504721b8e7baadaed60
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="7de4b-104">Solucionar problemas do Hive usando o Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7de4b-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="7de4b-105">Saiba mais sobre as principais perguntas e suas resoluções ao trabalhar com cargas de Apache Hive no Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="7de4b-105">Learn about the top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="7de4b-106">Como fazer para exportar um metastore do Hive e importá-lo para outro cluster</span><span class="sxs-lookup"><span data-stu-id="7de4b-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="7de4b-107">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="7de4b-107">Resolution steps</span></span>

1. <span data-ttu-id="7de4b-108">Conecte-se ao cluster HDInsight com um cliente SSH (Secure Shell).</span><span class="sxs-lookup"><span data-stu-id="7de4b-108">Connect to the HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="7de4b-109">Para obter mais informações, consulte [Leituras adicionais](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="7de4b-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="7de4b-110">Execute o seguinte comando no cluster do HDInsight do qual você deseja exportar o metastore:</span><span class="sxs-lookup"><span data-stu-id="7de4b-110">Run the following command on the HDInsight cluster from which you want to export the metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="7de4b-111">Este comando gera um arquivo chamado allatables.sql.</span><span class="sxs-lookup"><span data-stu-id="7de4b-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="7de4b-112">Copie o arquivo alltables.sql para o novo cluster do HDInsight e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7de4b-112">Copy the file alltables.sql to the new HDInsight cluster, and then run the following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="7de4b-113">O código nas etapas de resolução supõe que os caminhos de dados no novo cluster sejam iguais aos caminhos de dados no cluster antigo.</span><span class="sxs-lookup"><span data-stu-id="7de4b-113">The code in the resolution steps assumes that data paths on the new cluster are the same as the data paths on the old cluster.</span></span> <span data-ttu-id="7de4b-114">Se os caminhos de dados forem diferentes, você poderá editar manualmente o arquivo alltables.sql gerado para refletir as alterações.</span><span class="sxs-lookup"><span data-stu-id="7de4b-114">If the data paths are different, you can manually edit the generated alltables.sql file to reflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="7de4b-115">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="7de4b-115">Additional reading</span></span>

- [<span data-ttu-id="7de4b-116">Conectar-se a um cluster HDInsight usando SSH</span><span class="sxs-lookup"><span data-stu-id="7de4b-116">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="7de4b-117">Como fazer para localizar logs do Hive em um cluster</span><span class="sxs-lookup"><span data-stu-id="7de4b-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="7de4b-118">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="7de4b-118">Resolution steps</span></span>

1. <span data-ttu-id="7de4b-119">Conectar-se ao cluster HDInsight usando SSH.</span><span class="sxs-lookup"><span data-stu-id="7de4b-119">Connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="7de4b-120">Para obter mais informações, consulte **Leituras adicionais**.</span><span class="sxs-lookup"><span data-stu-id="7de4b-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="7de4b-121">Para exibir logs de cliente do Hive, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7de4b-121">To view Hive client logs, use the following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="7de4b-122">Para exibir logs de metastore do Hive, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7de4b-122">To view Hive metastore logs, use the following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="7de4b-123">Para exibir logs do Hiveserver, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7de4b-123">To view Hiveserver logs, use the following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="7de4b-124">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="7de4b-124">Additional reading</span></span>

- [<span data-ttu-id="7de4b-125">Conectar-se a um cluster HDInsight usando SSH</span><span class="sxs-lookup"><span data-stu-id="7de4b-125">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-the-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="7de4b-126">Como fazer para inicializar o shell do Hive com configurações específicas em um cluster</span><span class="sxs-lookup"><span data-stu-id="7de4b-126">How do I launch the Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="7de4b-127">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="7de4b-127">Resolution steps</span></span>

1. <span data-ttu-id="7de4b-128">Especifique um par chave-valor de configuração quando iniciar o shell do Hive.</span><span class="sxs-lookup"><span data-stu-id="7de4b-128">Specify a configuration key-value pair when you start the Hive shell.</span></span> <span data-ttu-id="7de4b-129">Para obter mais informações, consulte [Leituras adicionais](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="7de4b-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="7de4b-130">Para listar todas as configurações efetivas no shell de Hive, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7de4b-130">To list all effective configurations on Hive shell, use the following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="7de4b-131">Por exemplo, use o seguinte comando para iniciar o shell do Hive com o registro em log de depuração habilitado no console:</span><span class="sxs-lookup"><span data-stu-id="7de4b-131">For example, use the following command to start Hive shell with debug logging enabled on the console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="7de4b-132">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="7de4b-132">Additional reading</span></span>

- [<span data-ttu-id="7de4b-133">Propriedades de configuração do Hive</span><span class="sxs-lookup"><span data-stu-id="7de4b-133">Hive configuration properties</span></span>](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <span data-ttu-id="7de4b-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Como fazer para analisar dados de DAG do Tez em um caminho crítico do cluster</span><span class="sxs-lookup"><span data-stu-id="7de4b-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="7de4b-135">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="7de4b-135">Resolution steps</span></span>
 
1. <span data-ttu-id="7de4b-136">Para analisar um DAG (gráfico acíclico direcionado) do Apache Tez em um gráfico crítico do cluster, conecte-se ao cluster do HDInsight usando SSH.</span><span class="sxs-lookup"><span data-stu-id="7de4b-136">To analyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="7de4b-137">Para saber mais, veja [Leituras adicionais](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="7de4b-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="7de4b-138">No prompt de comando, execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7de4b-138">At a command prompt, run the following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="7de4b-139">Para listar outros analisadores que podem ser usados para analisar o DAG do Tez, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7de4b-139">To list other analyzers that can be used to analyze Tez DAG, use the following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="7de4b-140">Você precisa fornecer um programa de exemplo como o primeiro argumento.</span><span class="sxs-lookup"><span data-stu-id="7de4b-140">You must provide an example program as the first argument.</span></span>

  <span data-ttu-id="7de4b-141">Nomes de programa válidos incluem:</span><span class="sxs-lookup"><span data-stu-id="7de4b-141">Valid program names include:</span></span>
    - <span data-ttu-id="7de4b-142">**ContainerReuseAnalyzer**: imprimir detalhes de reutilização do contêiner em um DAG</span><span class="sxs-lookup"><span data-stu-id="7de4b-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="7de4b-143">**CriticalPath**: localizar o caminho crítico de um DAG</span><span class="sxs-lookup"><span data-stu-id="7de4b-143">**CriticalPath**: Find the critical path of a DAG</span></span>
    - <span data-ttu-id="7de4b-144">**LocalityAnalyzer**: imprimir detalhes de localidade em um DAG</span><span class="sxs-lookup"><span data-stu-id="7de4b-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="7de4b-145">**ShuffleTimeAnalyzer**: analisar os detalhes de tempo de ordem aleatória em um DAG</span><span class="sxs-lookup"><span data-stu-id="7de4b-145">**ShuffleTimeAnalyzer**: Analyze the shuffle time details in a DAG</span></span>
    - <span data-ttu-id="7de4b-146">**SkewAnalyzer**: analisar os detalhes de distorção em um DAG</span><span class="sxs-lookup"><span data-stu-id="7de4b-146">**SkewAnalyzer**: Analyze the skew details in a DAG</span></span>
    - <span data-ttu-id="7de4b-147">**SlowNodeAnalyzer**: imprimir detalhes do nó em um DAG</span><span class="sxs-lookup"><span data-stu-id="7de4b-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="7de4b-148">**SlowTaskIdentifier**: imprimir detalhes de tarefa lenta em um DAG</span><span class="sxs-lookup"><span data-stu-id="7de4b-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="7de4b-149">**SlowestVertexAnalyzer**: imprimir detalhes do vértice mais lento em um DAG</span><span class="sxs-lookup"><span data-stu-id="7de4b-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="7de4b-150">**SpillAnalyzer**: imprimir detalhes de despejo em um DAG</span><span class="sxs-lookup"><span data-stu-id="7de4b-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="7de4b-151">**TaskConcurrencyAnalyzer**: imprimir os detalhes de simultaneidade de tarefa em um DAG</span><span class="sxs-lookup"><span data-stu-id="7de4b-151">**TaskConcurrencyAnalyzer**: Print the task concurrency details in a DAG</span></span>
    - <span data-ttu-id="7de4b-152">**VertexLevelCriticalPathAnalyzer**: encontrar o caminho crítico no nível do vértice em um DAG</span><span class="sxs-lookup"><span data-stu-id="7de4b-152">**VertexLevelCriticalPathAnalyzer**: Find the critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="7de4b-153">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="7de4b-153">Additional reading</span></span>

- [<span data-ttu-id="7de4b-154">Conectar-se a um cluster HDInsight usando SSH</span><span class="sxs-lookup"><span data-stu-id="7de4b-154">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="7de4b-155">Como fazer para baixar dados de DAG do Tez de um cluster</span><span class="sxs-lookup"><span data-stu-id="7de4b-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="7de4b-156">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="7de4b-156">Resolution steps</span></span>

<span data-ttu-id="7de4b-157">Há duas maneiras de coletar os dados de DAG do Tez:</span><span class="sxs-lookup"><span data-stu-id="7de4b-157">There are two ways to collect the Tez DAG data:</span></span>

- <span data-ttu-id="7de4b-158">Na linha de comando:</span><span class="sxs-lookup"><span data-stu-id="7de4b-158">From the command line:</span></span>
 
    <span data-ttu-id="7de4b-159">Conectar-se ao cluster HDInsight usando SSH.</span><span class="sxs-lookup"><span data-stu-id="7de4b-159">Connect to the HDInsight cluster by using SSH.</span></span> <span data-ttu-id="7de4b-160">No prompt de comando, execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7de4b-160">At the command prompt, run the following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="7de4b-161">Use o modo de exibição Tez do Ambari:</span><span class="sxs-lookup"><span data-stu-id="7de4b-161">Use the Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="7de4b-162">Vá para o Ambari.</span><span class="sxs-lookup"><span data-stu-id="7de4b-162">Go to Ambari.</span></span> 
  2. <span data-ttu-id="7de4b-163">Vá para o modo de exibição do Tez (sob o ícone de blocos no canto superior direito).</span><span class="sxs-lookup"><span data-stu-id="7de4b-163">Go to Tez view (under the tiles icon in the upper-right corner).</span></span> 
  3. <span data-ttu-id="7de4b-164">Selecione o DAG que você deseja exibir.</span><span class="sxs-lookup"><span data-stu-id="7de4b-164">Select the DAG you want to view.</span></span>
  4. <span data-ttu-id="7de4b-165">Selecione **Baixar dados**.</span><span class="sxs-lookup"><span data-stu-id="7de4b-165">Select **Download data**.</span></span>

### <span data-ttu-id="7de4b-166"><a name="additional-reading-end"></a>Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="7de4b-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="7de4b-167">Conectar-se a um cluster HDInsight usando SSH</span><span class="sxs-lookup"><span data-stu-id="7de4b-167">Connect to an HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






