---
title: Solucionar problemas com o cluster Apache Spark no Azure HDInsight | Microsoft Docs
description: "Saiba mais sobre problemas relacionados aos clusters Apache Spark no Azure HDInsight e como solucioná-los."
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
ms.openlocfilehash: 3a493a2c35a6cdd31bb1e4ff66113a8f8d97d4f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="614a9-103">Problemas conhecidos do cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="614a9-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="614a9-104">Este documento mantém o registro de todos os problemas conhecidos para a visualização pública do Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="614a9-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="614a9-105">Sessão interativa de vazamentos do Livy</span><span class="sxs-lookup"><span data-stu-id="614a9-105">Livy leaks interactive session</span></span>
<span data-ttu-id="614a9-106">Quando o Livy é reiniciado com uma sessão interativa (do Ambari ou devido a reinicialização da máquina virtual de nó principal 0) ainda ativa, uma sessão de trabalho interativo irá vazar.</span><span class="sxs-lookup"><span data-stu-id="614a9-106">When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="614a9-107">Por isso, novos trabalhos podem travar no estado Aceito, não podendo ser iniciados.</span><span class="sxs-lookup"><span data-stu-id="614a9-107">Because of this, new jobs can stuck in the Accepted state, and cannot be started.</span></span>

<span data-ttu-id="614a9-108">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="614a9-108">**Mitigation:**</span></span>

<span data-ttu-id="614a9-109">Use o procedimento a seguir para contornar o problema:</span><span class="sxs-lookup"><span data-stu-id="614a9-109">Use the following procedure to workaround the issue:</span></span>

1. <span data-ttu-id="614a9-110">SSH no nó principal.</span><span class="sxs-lookup"><span data-stu-id="614a9-110">Ssh into headnode.</span></span> <span data-ttu-id="614a9-111">Para saber mais, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="614a9-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="614a9-112">Execute o seguinte comando para encontrar as IDs de aplicativo dos trabalhos interativos iniciados por Livy.</span><span class="sxs-lookup"><span data-stu-id="614a9-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="614a9-113">Os nomes de trabalho padrão serão Livy se os trabalhos tiverem sido iniciados com uma sessão interativa Livy sem nomes explícitos especificados; para a sessão Livy iniciada pelo notebook do Jupyter, o nome do trabalho iniciará com remotesparkmagics_*.</span><span class="sxs-lookup"><span data-stu-id="614a9-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="614a9-114">Execute o seguinte comando para eliminar esses trabalhos.</span><span class="sxs-lookup"><span data-stu-id="614a9-114">Run the following command to kill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="614a9-115">A execução de novos trabalhos terá início.</span><span class="sxs-lookup"><span data-stu-id="614a9-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="614a9-116">Servidor de histórico Spark não iniciado</span><span class="sxs-lookup"><span data-stu-id="614a9-116">Spark History Server not started</span></span>
<span data-ttu-id="614a9-117">O servidor de histórico Spark não é iniciado automaticamente depois de um cluster ser criado.</span><span class="sxs-lookup"><span data-stu-id="614a9-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="614a9-118">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="614a9-118">**Mitigation:**</span></span> 

<span data-ttu-id="614a9-119">Inicie manualmente o servidor de histórico do Ambari.</span><span class="sxs-lookup"><span data-stu-id="614a9-119">Manually start the history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="614a9-120">Problema de permissão no diretório de log do Spark</span><span class="sxs-lookup"><span data-stu-id="614a9-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="614a9-121">Quando hdiuser envia um trabalho com spark-submit, há um erro java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (permissão negada) e o log do driver não é gravado.</span><span class="sxs-lookup"><span data-stu-id="614a9-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written.</span></span> 

<span data-ttu-id="614a9-122">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="614a9-122">**Mitigation:**</span></span>

1. <span data-ttu-id="614a9-123">Adicione hdiuser ao grupo Hadoop.</span><span class="sxs-lookup"><span data-stu-id="614a9-123">Add hdiuser to the Hadoop group.</span></span> 
2. <span data-ttu-id="614a9-124">Forneça 777 permissões em /var/log/spark após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="614a9-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="614a9-125">Atualize o local do log spark usando o Ambari para ser um diretório com 777 permissões.</span><span class="sxs-lookup"><span data-stu-id="614a9-125">Update the spark log location using Ambari to be a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="614a9-126">Execute spark-submit como sudo.</span><span class="sxs-lookup"><span data-stu-id="614a9-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="614a9-127">Não há suporte para o conector Spark Phoenix</span><span class="sxs-lookup"><span data-stu-id="614a9-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="614a9-128">Atualmente, o conector Spark-Phoenix não tem suporte com um cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="614a9-128">Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="614a9-129">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="614a9-129">**Mitigation:**</span></span>

<span data-ttu-id="614a9-130">Use o conector Spark-HBase em vez disso.</span><span class="sxs-lookup"><span data-stu-id="614a9-130">You must use the Spark-HBase connector instead.</span></span> <span data-ttu-id="614a9-131">Para obter instruções, confira [Como usar o conector Spark-HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="614a9-131">For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-to-jupyter-notebooks"></a><span data-ttu-id="614a9-132">Problemas relacionados aos notebooks do Jupyter</span><span class="sxs-lookup"><span data-stu-id="614a9-132">Issues related to Jupyter notebooks</span></span>
<span data-ttu-id="614a9-133">A seguir estão alguns problemas conhecidos relacionados aos notebooks do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="614a9-133">Following are some known issues related to Jupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="614a9-134">Notebooks com caracteres não ASCII nos nomes de arquivos</span><span class="sxs-lookup"><span data-stu-id="614a9-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="614a9-135">Os notebooks do Jupyter que podem ser usados em clusters HDInsight do Spark não devem ter caracteres não ASCII nos nomes de arquivos.</span><span class="sxs-lookup"><span data-stu-id="614a9-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="614a9-136">Se você tentar carregar um arquivo por meio da interface do usuário do Jupyter que tenha um nome de arquivo não ASCII, ele falhará silenciosamente (ou seja, o Jupyter não permitirá que você carregue o arquivo, mas ele também não emitirá um erro visível).</span><span class="sxs-lookup"><span data-stu-id="614a9-136">If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="614a9-137">Erro ao carregar notebooks de tamanhos maiores</span><span class="sxs-lookup"><span data-stu-id="614a9-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="614a9-138">Você pode encontrar um erro **`Error loading notebook`** ao carregar notebooks com um tamanho maior.</span><span class="sxs-lookup"><span data-stu-id="614a9-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="614a9-139">**Atenuação:**</span><span class="sxs-lookup"><span data-stu-id="614a9-139">**Mitigation:**</span></span>

<span data-ttu-id="614a9-140">Se você visualizar esse erro, não significa que seus dados estão corrompidos ou foram perdidos.</span><span class="sxs-lookup"><span data-stu-id="614a9-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="614a9-141">Os notebooks ainda estão no disco, em `/var/lib/jupyter`, e você pode usar o SSH no cluster para acessá-los.</span><span class="sxs-lookup"><span data-stu-id="614a9-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span></span> <span data-ttu-id="614a9-142">Para saber mais, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="614a9-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="614a9-143">Depois de se conectar ao cluster usando o SSH, é possível copiar os blocos de anotações do cluster para o computador local (usando SCP ou WinSCP) como um backup para impedir a perda de quaisquer dados importantes no notebook.</span><span class="sxs-lookup"><span data-stu-id="614a9-143">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span></span> <span data-ttu-id="614a9-144">Você pode aplicar SSH no túnel no nó de cabeçalho na porta 8001 para acessar o Jupyter sem passar pelo gateway.</span><span class="sxs-lookup"><span data-stu-id="614a9-144">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span></span>  <span data-ttu-id="614a9-145">A partir daí, você pode limpar a saída do bloco de anotações e salvá-lo novamente para minimizar o tamanho dele.</span><span class="sxs-lookup"><span data-stu-id="614a9-145">From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.</span></span>

<span data-ttu-id="614a9-146">Para evitar que esse erro aconteça no futuro, você deve seguir algumas práticas recomendadas:</span><span class="sxs-lookup"><span data-stu-id="614a9-146">To prevent this error from happening in the future, you must follow some best practices:</span></span>

* <span data-ttu-id="614a9-147">É importante manter um tamanho pequeno de bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="614a9-147">It is important to keep the notebook size small.</span></span> <span data-ttu-id="614a9-148">Qualquer saída de trabalho no Spark que é enviada de volta ao Jupyter é mantida no bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="614a9-148">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span></span>  <span data-ttu-id="614a9-149">De modo geral, uma melhor prática com o Jupyter é evitar a execução de `.collect()` em RDDs ou em quadros de dados grandes. Em vez disso, se você quiser inspecionar o conteúdo de um RDD, considere a execução de `.take()` ou `.sample()` para que sua saída não fique muito grande.</span><span class="sxs-lookup"><span data-stu-id="614a9-149">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="614a9-150">Além disso, quando você salvar um bloco de anotações, limpe todas as células de saída para reduzir o tamanho.</span><span class="sxs-lookup"><span data-stu-id="614a9-150">Also, when you save a notebook, clear all output cells to reduce the size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="614a9-151">A inicialização inicial do notebook demora mais do que o esperado</span><span class="sxs-lookup"><span data-stu-id="614a9-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="614a9-152">A primeira instrução de código no notebook Jupyter usando a mágica do Spark pode demorar mais de um minuto.</span><span class="sxs-lookup"><span data-stu-id="614a9-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="614a9-153">**Explicação:**</span><span class="sxs-lookup"><span data-stu-id="614a9-153">**Explanation:**</span></span>

<span data-ttu-id="614a9-154">Isso acontece quando a primeira célula de código é executada.</span><span class="sxs-lookup"><span data-stu-id="614a9-154">This happens because when the first code cell is run.</span></span> <span data-ttu-id="614a9-155">Em segundo plano, isso inicia a configuração de sessão e os contextos de Spark, SQL e Hive são definidos.</span><span class="sxs-lookup"><span data-stu-id="614a9-155">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="614a9-156">Depois desses contextos são definidos, a primeira instrução é executada e isso dá a impressão de que a instrução levou muito tempo para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="614a9-156">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a><span data-ttu-id="614a9-157">Tempo limite do notebook do Jupyter atingido na criação da sessão</span><span class="sxs-lookup"><span data-stu-id="614a9-157">Jupyter notebook timeout in creating the session</span></span>
<span data-ttu-id="614a9-158">Quando o cluster Spark está sem recursos, os kernels Spark e Pyspark no notebook do Jupyter atingirão o tempo limite ao tentar criar a sessão.</span><span class="sxs-lookup"><span data-stu-id="614a9-158">When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session.</span></span> 

<span data-ttu-id="614a9-159">**Atenuações:**</span><span class="sxs-lookup"><span data-stu-id="614a9-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="614a9-160">Libere alguns recursos do cluster Spark:</span><span class="sxs-lookup"><span data-stu-id="614a9-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="614a9-161">Pare outros notebooks do Spark no menu Fechar e Parar ou clicando em Desligar no gerenciador de notebook.</span><span class="sxs-lookup"><span data-stu-id="614a9-161">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span></span>
   * <span data-ttu-id="614a9-162">Interrompendo outros aplicativos Spark do YARN.</span><span class="sxs-lookup"><span data-stu-id="614a9-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="614a9-163">Reinicie o notebook que você está tentando iniciar.</span><span class="sxs-lookup"><span data-stu-id="614a9-163">Restart the notebook you were trying to start up.</span></span> <span data-ttu-id="614a9-164">Recursos suficientes devem estar disponíveis para você criar uma sessão agora.</span><span class="sxs-lookup"><span data-stu-id="614a9-164">Enough resources should be available for you to create a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="614a9-165">Confira também</span><span class="sxs-lookup"><span data-stu-id="614a9-165">See also</span></span>
* [<span data-ttu-id="614a9-166">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="614a9-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="614a9-167">Cenários</span><span class="sxs-lookup"><span data-stu-id="614a9-167">Scenarios</span></span>
* [<span data-ttu-id="614a9-168">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="614a9-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="614a9-169">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="614a9-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="614a9-170">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para prever resultados da inspeção de alimentos</span><span class="sxs-lookup"><span data-stu-id="614a9-170">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="614a9-171">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="614a9-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="614a9-172">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="614a9-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="614a9-173">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="614a9-173">Create and run applications</span></span>
* [<span data-ttu-id="614a9-174">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="614a9-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="614a9-175">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="614a9-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="614a9-176">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="614a9-176">Tools and extensions</span></span>
* [<span data-ttu-id="614a9-177">Usar o plug-in de Ferramentas do HDInsight para IntelliJ IDEA para criar e enviar aplicativos Spark Scala</span><span class="sxs-lookup"><span data-stu-id="614a9-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="614a9-178">Usar o plug-in de Ferramentas do HDInsight para depurar aplicativos Spark remotamente</span><span class="sxs-lookup"><span data-stu-id="614a9-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="614a9-179">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="614a9-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="614a9-180">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="614a9-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="614a9-181">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="614a9-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="614a9-182">Instalar o Jupyter em seu computador e conectar-se a um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="614a9-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="614a9-183">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="614a9-183">Manage resources</span></span>
* [<span data-ttu-id="614a9-184">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="614a9-184">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="614a9-185">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="614a9-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

