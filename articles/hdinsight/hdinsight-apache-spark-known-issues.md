---
title: cluster de aaaTroubleshoot problemas com o Apache Spark no HDInsight do Azure | Microsoft Docs
description: Saiba mais sobre problemas relacionados tooApache clusters de Spark no HDInsight do Azure e como toowork em torno das.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="f1a5a-103">Problemas conhecidos do cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f1a5a-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="f1a5a-104">Este documento controla de saudação todos os problemas de saudação visualização pública do HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-104">This document keeps track of all hello known issues for hello HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="f1a5a-105">Sessão interativa de vazamentos do Livy</span><span class="sxs-lookup"><span data-stu-id="f1a5a-105">Livy leaks interactive session</span></span>
<span data-ttu-id="f1a5a-106">Quando Livy for reiniciado (do Ambari ou devido a reinicialização da máquina virtual de tooheadnode 0) com uma sessão interativa ainda existe, uma sessão interativa do trabalho será perdida.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-106">When Livy is restarted (from Ambari or due tooheadnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="f1a5a-107">Por isso, pode novo de trabalhos presa no hello estado aceito e não pode ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-107">Because of this, new jobs can stuck in hello Accepted state, and cannot be started.</span></span>

<span data-ttu-id="f1a5a-108">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="f1a5a-108">**Mitigation:**</span></span>

<span data-ttu-id="f1a5a-109">Use Olá problema de saudação tooworkaround procedimento a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1a5a-109">Use hello following procedure tooworkaround hello issue:</span></span>

1. <span data-ttu-id="f1a5a-110">SSH no nó principal.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-110">Ssh into headnode.</span></span> <span data-ttu-id="f1a5a-111">Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f1a5a-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f1a5a-112">Olá execução após o aplicativo do comando toofind hello IDs dos trabalhos interativo Olá iniciada por Livy.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-112">Run hello following command toofind hello application IDs of hello interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="f1a5a-113">Olá nomes de trabalho padrão será Livy se trabalhos de saudação foram iniciados com uma sessão interativa Livy sem nenhum nome explícito especificado por Olá sessão Livy iniciado por notebook Jupyter, o nome do trabalho Olá iniciará com remotesparkmagics_ *.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-113">hello default job names will be Livy if hello jobs were started with a Livy interactive session with no explicit names specified, For hello Livy session started by Jupyter notebook, hello job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="f1a5a-114">Execute Olá tookill de comando a seguir esses trabalhos.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-114">Run hello following command tookill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="f1a5a-115">A execução de novos trabalhos terá início.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="f1a5a-116">Servidor de histórico Spark não iniciado</span><span class="sxs-lookup"><span data-stu-id="f1a5a-116">Spark History Server not started</span></span>
<span data-ttu-id="f1a5a-117">O servidor de histórico Spark não é iniciado automaticamente depois de um cluster ser criado.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="f1a5a-118">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="f1a5a-118">**Mitigation:**</span></span> 

<span data-ttu-id="f1a5a-119">Inicie manualmente o servidor de histórico de saudação do Ambari.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-119">Manually start hello history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="f1a5a-120">Problema de permissão no diretório de log do Spark</span><span class="sxs-lookup"><span data-stu-id="f1a5a-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="f1a5a-121">Quando hdiuser enviar um trabalho com spark-submit, há um erro java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (permissão negada) e hello log de driver não será gravado.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and hello driver log is not written.</span></span> 

<span data-ttu-id="f1a5a-122">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="f1a5a-122">**Mitigation:**</span></span>

1. <span data-ttu-id="f1a5a-123">Adicione grupo de Hadoop toohello hdiuser.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-123">Add hdiuser toohello Hadoop group.</span></span> 
2. <span data-ttu-id="f1a5a-124">Forneça 777 permissões em /var/log/spark após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="f1a5a-125">Atualize Olá spark log local usando o Ambari toobe um diretório com 777 permissões.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-125">Update hello spark log location using Ambari toobe a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="f1a5a-126">Execute spark-submit como sudo.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="f1a5a-127">Não há suporte para o conector Spark Phoenix</span><span class="sxs-lookup"><span data-stu-id="f1a5a-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="f1a5a-128">Atualmente, Olá Spark Phoenix conector não tem suporte com um cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-128">Currently, hello Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="f1a5a-129">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="f1a5a-129">**Mitigation:**</span></span>

<span data-ttu-id="f1a5a-130">Você deve usar o conector do HBase Spark hello.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-130">You must use hello Spark-HBase connector instead.</span></span> <span data-ttu-id="f1a5a-131">Para obter instruções, consulte [como conector toouse Spark HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="f1a5a-131">For instructions see [How toouse Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-toojupyter-notebooks"></a><span data-ttu-id="f1a5a-132">Problemas relacionados tooJupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="f1a5a-132">Issues related tooJupyter notebooks</span></span>
<span data-ttu-id="f1a5a-133">A seguir estão alguns problemas conhecidos relacionados tooJupyter blocos de anotações.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-133">Following are some known issues related tooJupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="f1a5a-134">Notebooks com caracteres não ASCII nos nomes de arquivos</span><span class="sxs-lookup"><span data-stu-id="f1a5a-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="f1a5a-135">Os notebooks do Jupyter que podem ser usados em clusters HDInsight do Spark não devem ter caracteres não ASCII nos nomes de arquivos.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="f1a5a-136">Se você tentar tooupload um arquivo por meio de saudação UI Jupyter que tem um nome de arquivo não-ASCII, ele falhará em modo silencioso (ou seja, Jupyter não permite que você carregar o arquivo hello, mas ela não gerar um erro visível ou).</span><span class="sxs-lookup"><span data-stu-id="f1a5a-136">If you try tooupload a file through hello Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload hello file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="f1a5a-137">Erro ao carregar notebooks de tamanhos maiores</span><span class="sxs-lookup"><span data-stu-id="f1a5a-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="f1a5a-138">Você pode encontrar um erro **`Error loading notebook`** ao carregar notebooks com um tamanho maior.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="f1a5a-139">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="f1a5a-139">**Mitigation:**</span></span>

<span data-ttu-id="f1a5a-140">Se você visualizar esse erro, não significa que seus dados estão corrompidos ou foram perdidos.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="f1a5a-141">Os blocos de anotações ainda estão no disco no `/var/lib/jupyter`, e poderá SSH para Olá cluster tooaccess-los.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into hello cluster tooaccess them.</span></span> <span data-ttu-id="f1a5a-142">Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f1a5a-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="f1a5a-143">Depois de conectar o cluster toohello usando SSH, você pode copiar seus blocos de anotações do cluster tooyour computador local (usando o SCP ou WinSCP) como uma perda de saudação tooprevent backup de quaisquer dados importantes no bloco de anotações de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-143">Once you have connected toohello cluster using SSH, you can copy your notebooks from your cluster tooyour local machine (using SCP or WinSCP) as a backup tooprevent hello loss of any important data in hello notebook.</span></span> <span data-ttu-id="f1a5a-144">Você pode, em seguida, túnel SSH no seu nó principal na porta 8001 tooaccess Jupyter sem passar pelo gateway hello.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-144">You can then SSH tunnel into your headnode at port 8001 tooaccess Jupyter without going through hello gateway.</span></span>  <span data-ttu-id="f1a5a-145">A partir daí, você pode limpar a saída de saudação do bloco de notas e salvá-lo novamente tamanho toominimize saudação do bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-145">From there, you can clear hello output of your notebook and re-save it toominimize hello notebook’s size.</span></span>

<span data-ttu-id="f1a5a-146">tooprevent esse erro ocorra em Olá futura, você deve seguir algumas práticas recomendadas:</span><span class="sxs-lookup"><span data-stu-id="f1a5a-146">tooprevent this error from happening in hello future, you must follow some best practices:</span></span>

* <span data-ttu-id="f1a5a-147">É tookeep importante pequenos de tamanho de bloco de anotações de hello.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-147">It is important tookeep hello notebook size small.</span></span> <span data-ttu-id="f1a5a-148">Todas as saídas de seus trabalhos Spark que é enviada de volta tooJupyter é mantido no bloco de anotações de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-148">Any output from your Spark jobs that is sent back tooJupyter is persisted in hello notebook.</span></span>  <span data-ttu-id="f1a5a-149">É uma prática recomendada Jupyter geral tooavoid executando `.collect()` em RDD grandes ou quadros de dados; em vez disso, se você quiser toopeek no conteúdo de um RDD, considere executar `.take()` ou `.sample()` para que a saída não fica muito grande.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-149">It is a best practice with Jupyter in general tooavoid running `.collect()` on large RDD’s or dataframes; instead, if you want toopeek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="f1a5a-150">Além disso, quando você salva um bloco de anotações, desmarque todas as saída tamanho de saudação tooreduce células.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-150">Also, when you save a notebook, clear all output cells tooreduce hello size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="f1a5a-151">A inicialização inicial do notebook demora mais do que o esperado</span><span class="sxs-lookup"><span data-stu-id="f1a5a-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="f1a5a-152">A primeira instrução de código no notebook Jupyter usando a mágica do Spark pode demorar mais de um minuto.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="f1a5a-153">**Explicação:**</span><span class="sxs-lookup"><span data-stu-id="f1a5a-153">**Explanation:**</span></span>

<span data-ttu-id="f1a5a-154">Isso ocorre porque quando a primeira célula de código Olá é executada.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-154">This happens because when hello first code cell is run.</span></span> <span data-ttu-id="f1a5a-155">No plano de fundo Olá Isso inicia a configuração de sessão e Spark, SQL e contextos de Hive são definidos.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-155">In hello background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="f1a5a-156">Após configurar nesses contextos, Olá primeira instrução é executada e isso oferece impressão Olá instrução Olá levou toocomplete um longo tempo.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-156">After these contexts are set, hello first statement is run and this gives hello impression that hello statement took a long time toocomplete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a><span data-ttu-id="f1a5a-157">Tempo limite de notebook Jupyter na criação de sessão Olá</span><span class="sxs-lookup"><span data-stu-id="f1a5a-157">Jupyter notebook timeout in creating hello session</span></span>
<span data-ttu-id="f1a5a-158">Quando o cluster Spark está sem recursos, hello Spark e kernels Pyspark em anotações do Jupyter Olá atingirá o tempo limite tentar toocreate sessão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-158">When Spark cluster is out of resources, hello Spark and Pyspark kernels in hello Jupyter notebook will timeout trying toocreate hello session.</span></span> 

<span data-ttu-id="f1a5a-159">**Atenuações:**</span><span class="sxs-lookup"><span data-stu-id="f1a5a-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="f1a5a-160">Libere alguns recursos do cluster Spark:</span><span class="sxs-lookup"><span data-stu-id="f1a5a-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="f1a5a-161">Parar outros blocos de anotações do Spark toohello vai fechar e menu de parada ou clicando desligamento no explorer de notebook hello.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-161">Stopping other Spark notebooks by going toohello Close and Halt menu or clicking Shutdown in hello notebook explorer.</span></span>
   * <span data-ttu-id="f1a5a-162">Interrompendo outros aplicativos Spark do YARN.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="f1a5a-163">Reinicie o notebook Olá que estivesse tentando toostart backup.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-163">Restart hello notebook you were trying toostart up.</span></span> <span data-ttu-id="f1a5a-164">Há recursos suficientes devem estar disponíveis para você toocreate agora uma sessão.</span><span class="sxs-lookup"><span data-stu-id="f1a5a-164">Enough resources should be available for you toocreate a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="f1a5a-165">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f1a5a-165">See also</span></span>
* [<span data-ttu-id="f1a5a-166">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f1a5a-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="f1a5a-167">Cenários</span><span class="sxs-lookup"><span data-stu-id="f1a5a-167">Scenarios</span></span>
* [<span data-ttu-id="f1a5a-168">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="f1a5a-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f1a5a-169">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="f1a5a-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f1a5a-170">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="f1a5a-170">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f1a5a-171">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="f1a5a-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="f1a5a-172">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f1a5a-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="f1a5a-173">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="f1a5a-173">Create and run applications</span></span>
* [<span data-ttu-id="f1a5a-174">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="f1a5a-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f1a5a-175">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="f1a5a-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f1a5a-176">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="f1a5a-176">Tools and extensions</span></span>
* [<span data-ttu-id="f1a5a-177">Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar maiores Spark Scala aplicativos</span><span class="sxs-lookup"><span data-stu-id="f1a5a-177">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="f1a5a-178">Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente</span><span class="sxs-lookup"><span data-stu-id="f1a5a-178">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f1a5a-179">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f1a5a-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f1a5a-180">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="f1a5a-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f1a5a-181">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="f1a5a-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="f1a5a-182">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="f1a5a-182">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="f1a5a-183">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="f1a5a-183">Manage resources</span></span>
* [<span data-ttu-id="f1a5a-184">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="f1a5a-184">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f1a5a-185">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f1a5a-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

