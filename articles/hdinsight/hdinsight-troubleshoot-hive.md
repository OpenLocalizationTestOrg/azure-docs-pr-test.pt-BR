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
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="3e667-104">Solucionar problemas do Hive usando o Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e667-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="3e667-105">Saiba mais sobre Olá principais perguntas e suas resoluções durante o trabalho com o Apache Hive cargas no Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="3e667-105">Learn about hello top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="3e667-106">Como fazer para exportar um metastore do Hive e importá-lo para outro cluster</span><span class="sxs-lookup"><span data-stu-id="3e667-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="3e667-107">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="3e667-107">Resolution steps</span></span>

1. <span data-ttu-id="3e667-108">Conecte o cluster do HDInsight toohello usando um cliente do Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="3e667-108">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="3e667-109">Para saber mais, veja [Leituras adicionais](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="3e667-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="3e667-110">Execute Olá comando a seguir no cluster do HDInsight de saudação do qual você deseja tooexport Olá metastore:</span><span class="sxs-lookup"><span data-stu-id="3e667-110">Run hello following command on hello HDInsight cluster from which you want tooexport hello metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="3e667-111">Este comando gera um arquivo chamado allatables.sql.</span><span class="sxs-lookup"><span data-stu-id="3e667-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="3e667-112">Copiar Olá arquivo alltables.sql toohello novo cluster HDInsight e execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e667-112">Copy hello file alltables.sql toohello new HDInsight cluster, and then run hello following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="3e667-113">código de saudação nas etapas de resolução de saudação supõe que dados são caminhos no cluster novo Olá Olá mesmo como caminhos de dados Olá no cluster antigo hello.</span><span class="sxs-lookup"><span data-stu-id="3e667-113">hello code in hello resolution steps assumes that data paths on hello new cluster are hello same as hello data paths on hello old cluster.</span></span> <span data-ttu-id="3e667-114">Se os caminhos de dados Olá forem diferentes, você pode editar manualmente Olá gerado alltables.sql arquivo tooreflect quaisquer alterações.</span><span class="sxs-lookup"><span data-stu-id="3e667-114">If hello data paths are different, you can manually edit hello generated alltables.sql file tooreflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="3e667-115">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="3e667-115">Additional reading</span></span>

- [<span data-ttu-id="3e667-116">Conecte-se o cluster do HDInsight tooan usando SSH</span><span class="sxs-lookup"><span data-stu-id="3e667-116">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="3e667-117">Como fazer para localizar logs do Hive em um cluster</span><span class="sxs-lookup"><span data-stu-id="3e667-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="3e667-118">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="3e667-118">Resolution steps</span></span>

1. <span data-ttu-id="3e667-119">Conecte o cluster do HDInsight toohello usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="3e667-119">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="3e667-120">Para saber mais, veja **Leituras adicionais**.</span><span class="sxs-lookup"><span data-stu-id="3e667-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="3e667-121">logs de cliente do Hive tooview, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e667-121">tooview Hive client logs, use hello following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="3e667-122">tooview Hive metastore logs, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e667-122">tooview Hive metastore logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="3e667-123">tooview Hiveserver logs, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e667-123">tooview Hiveserver logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="3e667-124">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="3e667-124">Additional reading</span></span>

- [<span data-ttu-id="3e667-125">Conecte-se o cluster do HDInsight tooan usando SSH</span><span class="sxs-lookup"><span data-stu-id="3e667-125">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="3e667-126">Como iniciar o hello Hive shell com configurações específicas em um cluster</span><span class="sxs-lookup"><span data-stu-id="3e667-126">How do I launch hello Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="3e667-127">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="3e667-127">Resolution steps</span></span>

1. <span data-ttu-id="3e667-128">Especifique um par chave-valor de configuração quando você iniciar Olá Hive shell.</span><span class="sxs-lookup"><span data-stu-id="3e667-128">Specify a configuration key-value pair when you start hello Hive shell.</span></span> <span data-ttu-id="3e667-129">Para saber mais, veja [Leituras adicionais](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="3e667-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="3e667-130">toolist todas as configurações efetivas no shell de Hive, Olá uso a seguir de comando:</span><span class="sxs-lookup"><span data-stu-id="3e667-130">toolist all effective configurations on Hive shell, use hello following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="3e667-131">Por exemplo, use Olá a seguir do shell de comando do Hive toostart com habilitado no console de saudação do log de depuração:</span><span class="sxs-lookup"><span data-stu-id="3e667-131">For example, use hello following command toostart Hive shell with debug logging enabled on hello console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="3e667-132">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="3e667-132">Additional reading</span></span>

- [<span data-ttu-id="3e667-133">Propriedades de configuração do Hive</span><span class="sxs-lookup"><span data-stu-id="3e667-133">Hive configuration properties</span></span>](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <span data-ttu-id="3e667-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Como fazer para analisar dados de DAG do Tez em um caminho crítico do cluster</span><span class="sxs-lookup"><span data-stu-id="3e667-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="3e667-135">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="3e667-135">Resolution steps</span></span>
 
1. <span data-ttu-id="3e667-136">tooanalyze um Tez Apache direcionado gráfico acíclico (DAG) em um gráfico de cluster crítico, conecte-se o cluster do HDInsight toohello usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="3e667-136">tooanalyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="3e667-137">Para saber mais, veja [Leituras adicionais](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="3e667-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="3e667-138">Em um prompt de comando, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e667-138">At a command prompt, run hello following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="3e667-139">toolist outros analisadores que podem ser usado tooanalyze Tez DAG, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e667-139">toolist other analyzers that can be used tooanalyze Tez DAG, use hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="3e667-140">Você deve fornecer um programa de exemplo como primeiro argumento de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e667-140">You must provide an example program as hello first argument.</span></span>

  <span data-ttu-id="3e667-141">Nomes de programa válidos incluem:</span><span class="sxs-lookup"><span data-stu-id="3e667-141">Valid program names include:</span></span>
    - <span data-ttu-id="3e667-142">**ContainerReuseAnalyzer**: imprimir detalhes de reutilização do contêiner em um DAG</span><span class="sxs-lookup"><span data-stu-id="3e667-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="3e667-143">**CriticalPath**: caminho crítico de saudação de localização de um DAG</span><span class="sxs-lookup"><span data-stu-id="3e667-143">**CriticalPath**: Find hello critical path of a DAG</span></span>
    - <span data-ttu-id="3e667-144">**LocalityAnalyzer**: imprimir detalhes de localidade em um DAG</span><span class="sxs-lookup"><span data-stu-id="3e667-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="3e667-145">**ShuffleTimeAnalyzer**: analisar os detalhes de tempo de ordem aleatória Olá em um DAG</span><span class="sxs-lookup"><span data-stu-id="3e667-145">**ShuffleTimeAnalyzer**: Analyze hello shuffle time details in a DAG</span></span>
    - <span data-ttu-id="3e667-146">**SkewAnalyzer**: analisar os detalhes de distorção Olá em um DAG</span><span class="sxs-lookup"><span data-stu-id="3e667-146">**SkewAnalyzer**: Analyze hello skew details in a DAG</span></span>
    - <span data-ttu-id="3e667-147">**SlowNodeAnalyzer**: imprimir detalhes do nó em um DAG</span><span class="sxs-lookup"><span data-stu-id="3e667-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="3e667-148">**SlowTaskIdentifier**: imprimir detalhes de tarefa lenta em um DAG</span><span class="sxs-lookup"><span data-stu-id="3e667-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="3e667-149">**SlowestVertexAnalyzer**: imprimir detalhes do vértice mais lento em um DAG</span><span class="sxs-lookup"><span data-stu-id="3e667-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="3e667-150">**SpillAnalyzer**: imprimir detalhes de despejo em um DAG</span><span class="sxs-lookup"><span data-stu-id="3e667-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="3e667-151">**TaskConcurrencyAnalyzer**: Imprimir Olá detalhes de simultaneidade de tarefa em um DAG</span><span class="sxs-lookup"><span data-stu-id="3e667-151">**TaskConcurrencyAnalyzer**: Print hello task concurrency details in a DAG</span></span>
    - <span data-ttu-id="3e667-152">**VertexLevelCriticalPathAnalyzer**: caminho crítico de saudação de localizar no nível de vértice em um DAG</span><span class="sxs-lookup"><span data-stu-id="3e667-152">**VertexLevelCriticalPathAnalyzer**: Find hello critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="3e667-153">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="3e667-153">Additional reading</span></span>

- [<span data-ttu-id="3e667-154">Conecte-se o cluster do HDInsight tooan usando SSH</span><span class="sxs-lookup"><span data-stu-id="3e667-154">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="3e667-155">Como fazer para baixar dados de DAG do Tez de um cluster</span><span class="sxs-lookup"><span data-stu-id="3e667-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="3e667-156">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="3e667-156">Resolution steps</span></span>

<span data-ttu-id="3e667-157">Há duas maneiras de dados de DAG Tez toocollect saudação:</span><span class="sxs-lookup"><span data-stu-id="3e667-157">There are two ways toocollect hello Tez DAG data:</span></span>

- <span data-ttu-id="3e667-158">Olá linha de comando:</span><span class="sxs-lookup"><span data-stu-id="3e667-158">From hello command line:</span></span>
 
    <span data-ttu-id="3e667-159">Conecte o cluster do HDInsight toohello usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="3e667-159">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="3e667-160">No prompt de comando hello, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e667-160">At hello command prompt, run hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="3e667-161">Use Olá Ambari Tez exibição:</span><span class="sxs-lookup"><span data-stu-id="3e667-161">Use hello Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="3e667-162">Vá tooAmbari.</span><span class="sxs-lookup"><span data-stu-id="3e667-162">Go tooAmbari.</span></span> 
  2. <span data-ttu-id="3e667-163">Exibição de tooTez vá (no ícone de blocos de saudação no canto superior direito de saudação).</span><span class="sxs-lookup"><span data-stu-id="3e667-163">Go tooTez view (under hello tiles icon in hello upper-right corner).</span></span> 
  3. <span data-ttu-id="3e667-164">Selecione Olá DAG tooview desejado.</span><span class="sxs-lookup"><span data-stu-id="3e667-164">Select hello DAG you want tooview.</span></span>
  4. <span data-ttu-id="3e667-165">Selecione **Baixar dados**.</span><span class="sxs-lookup"><span data-stu-id="3e667-165">Select **Download data**.</span></span>

### <span data-ttu-id="3e667-166"><a name="additional-reading-end"></a>Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="3e667-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="3e667-167">Conecte-se o cluster do HDInsight tooan usando SSH</span><span class="sxs-lookup"><span data-stu-id="3e667-167">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






