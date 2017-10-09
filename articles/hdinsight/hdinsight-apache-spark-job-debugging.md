---
title: "aaaDebug Apache Spark trabalhos em execução no Azure HDInsight | Microsoft Docs"
description: "Usar YARN da interface do usuário, Spark da interface do usuário e o histórico de Spark servidor tootrack e depuração trabalhos em execução em um cluster Spark no HDInsight do Azure"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="0eafa-103">Depurar trabalhos do Apache Spark em execução no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0eafa-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="0eafa-104">Neste artigo, você aprenderá como tootrack e depuração despertar trabalhos executados em clusters de HDInsight usando Olá YARN da interface do usuário, Spark da interface do usuário e Olá Spark histórico de servidor.</span><span class="sxs-lookup"><span data-stu-id="0eafa-104">In this article you will learn how tootrack and debug Spark jobs running on HDInsight clusters using hello YARN UI, Spark UI, and hello Spark History Server.</span></span> <span data-ttu-id="0eafa-105">Neste artigo, vamos começar um trabalho do Spark usando um bloco de anotações disponível com o cluster do Spark hello, **aprendizado de máquina: análise de previsão em dados de inspeção de alimentos com MLLib**.</span><span class="sxs-lookup"><span data-stu-id="0eafa-105">For this article, we will start a Spark job using a notebook available with hello Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="0eafa-106">Você pode usar etapas Olá abaixo tootrack um aplicativo que é enviado usando qualquer outra abordagem, por exemplo, **o envio spark**.</span><span class="sxs-lookup"><span data-stu-id="0eafa-106">You can use hello steps below tootrack an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0eafa-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0eafa-107">Prerequisites</span></span>
<span data-ttu-id="0eafa-108">Você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="0eafa-108">You must have hello following:</span></span>

* <span data-ttu-id="0eafa-109">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0eafa-109">An Azure subscription.</span></span> <span data-ttu-id="0eafa-110">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0eafa-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0eafa-111">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0eafa-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="0eafa-112">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="0eafa-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="0eafa-113">Você deve ter começou a executar notebook Olá,  **[aprendizado de máquina: análise de previsão em dados de inspeção de alimentos com MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="0eafa-113">You should have started running hello notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="0eafa-114">Para obter instruções sobre como toorun este bloco de anotações, siga Olá link.</span><span class="sxs-lookup"><span data-stu-id="0eafa-114">For instructions on how toorun this notebook, follow hello link.</span></span>  

## <a name="track-an-application-in-hello-yarn-ui"></a><span data-ttu-id="0eafa-115">Controlar um aplicativo hello YARN da interface do usuário</span><span class="sxs-lookup"><span data-stu-id="0eafa-115">Track an application in hello YARN UI</span></span>
1. <span data-ttu-id="0eafa-116">Inicie Olá YARN da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="0eafa-116">Launch hello YARN UI.</span></span> <span data-ttu-id="0eafa-117">Na folha de cluster hello, clique em **painel Cluster**e, em seguida, clique em **YARN**.</span><span class="sxs-lookup"><span data-stu-id="0eafa-117">From hello cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Iniciar Interface do usuário do YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="0eafa-119">Como alternativa, você também pode iniciar Olá YARN da interface do usuário do hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="0eafa-119">Alternatively, you can also launch hello YARN UI from hello Ambari UI.</span></span> <span data-ttu-id="0eafa-120">Olá toolaunch Ambari UI, na folha de cluster hello, clique em **painel Cluster**e, em seguida, clique em **painel do Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0eafa-120">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="0eafa-121">De Olá Ambari UI, clique em **YARN**, clique em **Links rápidos**, clique em Gerenciador de recursos ativo hello e, em seguida, clique em **ResourceManager UI**.</span><span class="sxs-lookup"><span data-stu-id="0eafa-121">From hello Ambari UI, click **YARN**, click **Quick Links**, click hello active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="0eafa-122">Como você iniciou o trabalho do Spark hello usando blocos de anotações do Jupyter, o aplicativo hello tem nome hello **remotesparkmagics** (Este é o nome de Olá para todos os aplicativos que são iniciadas de blocos de anotações de saudação).</span><span class="sxs-lookup"><span data-stu-id="0eafa-122">Because you started hello Spark job using Jupyter notebooks, hello application has hello name **remotesparkmagics** (this is hello name for all applications that are started from hello notebooks).</span></span> <span data-ttu-id="0eafa-123">Clique em ID do aplicativo hello contra Olá tooget de nome de aplicativo para obter mais informações sobre o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="0eafa-123">Click hello application ID against hello application name tooget more information about hello job.</span></span> <span data-ttu-id="0eafa-124">Isso inicia o modo de exibição de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0eafa-124">This launches hello application view.</span></span>
   
    ![Localizar a ID de aplicativo Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="0eafa-126">Para aplicativos que são iniciados a partir de blocos de anotações do Jupyter hello, status de saudação é sempre **executando** até que você sair do bloco de anotações de saudação.</span><span class="sxs-lookup"><span data-stu-id="0eafa-126">For such applications that are launched from hello Jupyter notebooks, hello status is always **RUNNING** until you exit hello notebook.</span></span>
3. <span data-ttu-id="0eafa-127">Exibição do aplicativo hello, você pode fazer drill down mais toofind out contêineres Olá associados ao aplicativo hello e logs de saudação (stdout/stderr).</span><span class="sxs-lookup"><span data-stu-id="0eafa-127">From hello application view, you can drill down further toofind out hello containers associated with hello application and hello logs (stdout/stderr).</span></span> <span data-ttu-id="0eafa-128">Você também pode iniciar Olá Spark da interface do usuário clicando Olá vinculação correspondente toohello **controle URL**, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="0eafa-128">You can also launch hello Spark UI by clicking hello linking corresponding toohello **Tracking URL**, as shown below.</span></span> 
   
    ![Baixar logs de contêiner](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a><span data-ttu-id="0eafa-130">Controlar um aplicativo hello Spark da interface do usuário</span><span class="sxs-lookup"><span data-stu-id="0eafa-130">Track an application in hello Spark UI</span></span>
<span data-ttu-id="0eafa-131">Olá Spark da interface do usuário, você pode detalhar em trabalhos de Spark Olá que são gerados pelo aplicativo hello que tiver iniciado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0eafa-131">In hello Spark UI, you can drill down into hello Spark jobs that are spawned by hello application you started earlier.</span></span>

1. <span data-ttu-id="0eafa-132">Olá toolaunch Spark da interface do usuário, de modo de exibição de aplicativo hello, clique em link Olá contra Olá **controle URL**, conforme mostrado na captura de tela de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="0eafa-132">toolaunch hello Spark UI, from hello application view, click hello link against hello **Tracking URL**, as shown in hello screen capture above.</span></span> <span data-ttu-id="0eafa-133">Você pode ver todos os trabalhos do Spark Olá iniciados pelo aplicativo hello em execução em anotações do Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="0eafa-133">You can see all hello Spark jobs that are launched by hello application running in hello Jupyter notebook.</span></span>
   
    ![Exibir trabalhos do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="0eafa-135">Clique em Olá **executores** guia toosee informações de processamento e armazenamento para cada executor.</span><span class="sxs-lookup"><span data-stu-id="0eafa-135">Click hello **Executors** tab toosee processing and storage information for each executor.</span></span> <span data-ttu-id="0eafa-136">Você também pode recuperar a pilha de chamadas Olá clicando em Olá **Thread despejo** link.</span><span class="sxs-lookup"><span data-stu-id="0eafa-136">You can also retrieve hello call stack by clicking on hello **Thread Dump** link.</span></span>
   
    ![Exibir executores do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="0eafa-138">Clique em Olá **estágios** guia toosee estágios de saudação associados ao aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0eafa-138">Click hello **Stages** tab toosee hello stages associated with hello application.</span></span>
   
    ![Exibir estágios do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="0eafa-140">Cada estágio pode ter várias tarefas para as quais você pode exibir estatísticas de execução, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="0eafa-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Exibir estágios do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="0eafa-142">Na página de detalhes do estágio hello, você pode iniciar DAG visualização.</span><span class="sxs-lookup"><span data-stu-id="0eafa-142">From hello stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="0eafa-143">Expanda Olá **DAG visualização** link na parte superior de saudação da página hello, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="0eafa-143">Expand hello **DAG Visualization** link at hello top of hello page, as shown below.</span></span>
   
    ![Exibir a visualização de DAG dos estágios do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="0eafa-145">Gráfico de Aclyic direta ou DAG representa diferentes estágios Olá no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0eafa-145">DAG or Direct Aclyic Graph represents hello different stages in hello application.</span></span> <span data-ttu-id="0eafa-146">Cada caixa azul no gráfico de saudação representa uma operação de Spark chamada a partir de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0eafa-146">Each blue box in hello graph represents a Spark operation invoked from hello application.</span></span>
5. <span data-ttu-id="0eafa-147">Na página de detalhes do hello estágio, você também pode iniciar o modo de exibição de tempo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0eafa-147">From hello stage details page, you can also launch hello application timeline view.</span></span> <span data-ttu-id="0eafa-148">Expanda Olá **cronograma do evento** link na parte superior de saudação da página hello, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="0eafa-148">Expand hello **Event Timeline** link at hello top of hello page, as shown below.</span></span>
   
    ![Exibir linha do tempo de evento de estágios do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="0eafa-150">Exibe eventos de Spark Olá na forma de saudação de uma linha do tempo.</span><span class="sxs-lookup"><span data-stu-id="0eafa-150">This displays hello Spark events in hello form of a timeline.</span></span> <span data-ttu-id="0eafa-151">modo de exibição de tempo de saudação está disponível em três níveis, em trabalhos, dentro de um trabalho e em um estágio.</span><span class="sxs-lookup"><span data-stu-id="0eafa-151">hello timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="0eafa-152">imagem de saudação acima captura o modo de exibição de tempo de saudação para uma determinada fase.</span><span class="sxs-lookup"><span data-stu-id="0eafa-152">hello image above captures hello timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="0eafa-153">Se você selecionar Olá **habilitar o zoom** caixa de seleção, você pode rolar para a esquerda e direita em modo de exibição de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0eafa-153">If you select hello **Enable zooming** check box, you can scroll left and right across hello timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="0eafa-154">Outras guias Olá Spark da interface do usuário fornecem informações úteis sobre a instância do Spark Olá também.</span><span class="sxs-lookup"><span data-stu-id="0eafa-154">Other tabs in hello Spark UI provide useful information about hello Spark instance as well.</span></span>
   
   * <span data-ttu-id="0eafa-155">Guia de armazenamento - se seu aplicativo cria um RDDs, você encontrará informações sobre os na guia de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="0eafa-155">Storage tab - If your application creates an RDDs, you can find information about those in hello Storage tab.</span></span>
   * <span data-ttu-id="0eafa-156">Guia de ambiente - este guia fornece muitas informações úteis sobre sua instância do Spark como Olá</span><span class="sxs-lookup"><span data-stu-id="0eafa-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as hello</span></span> 
     * <span data-ttu-id="0eafa-157">Versão da escala</span><span class="sxs-lookup"><span data-stu-id="0eafa-157">Scala version</span></span>
     * <span data-ttu-id="0eafa-158">Diretório de log de eventos associado a saudação cluster</span><span class="sxs-lookup"><span data-stu-id="0eafa-158">Event log directory associated with hello cluster</span></span>
     * <span data-ttu-id="0eafa-159">Número de núcleos de executor de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="0eafa-159">Number of executor cores for hello application</span></span>
     * <span data-ttu-id="0eafa-160">Etc.</span><span class="sxs-lookup"><span data-stu-id="0eafa-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a><span data-ttu-id="0eafa-161">Para obter informações sobre trabalhos concluídos usando Olá Spark histórico de servidor</span><span class="sxs-lookup"><span data-stu-id="0eafa-161">Find information about completed jobs using hello Spark History Server</span></span>
<span data-ttu-id="0eafa-162">Quando um trabalho for concluído, informações de saudação sobre o trabalho de saudação são mantidas no hello Spark histórico de servidor.</span><span class="sxs-lookup"><span data-stu-id="0eafa-162">Once a job is completed, hello information about hello job is persisted in hello Spark History Server.</span></span>

1. <span data-ttu-id="0eafa-163">Olá toolaunch Spark histórico de servidor, na folha de cluster hello, clique em **painel Cluster**e, em seguida, clique em **Spark histórico servidor**.</span><span class="sxs-lookup"><span data-stu-id="0eafa-163">toolaunch hello Spark History Server, from hello cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Iniciar o Servidor de Histórico do Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="0eafa-165">Como alternativa, você também pode iniciar Olá Spark histórico servidor UI do hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="0eafa-165">Alternatively, you can also launch hello Spark History Server UI from hello Ambari UI.</span></span> <span data-ttu-id="0eafa-166">Olá toolaunch Ambari UI, na folha de cluster hello, clique em **painel Cluster**e, em seguida, clique em **painel do Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0eafa-166">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="0eafa-167">De Olá Ambari UI, clique em **Spark**, clique em **Links rápidos**e, em seguida, clique em **Spark histórico servidor UI**.</span><span class="sxs-lookup"><span data-stu-id="0eafa-167">From hello Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="0eafa-168">Você verá todos os aplicativos de saudação concluída listados.</span><span class="sxs-lookup"><span data-stu-id="0eafa-168">You will see all hello completed applications listed.</span></span> <span data-ttu-id="0eafa-169">Clique em um toodrill de ID do aplicativo para baixo em um aplicativo para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="0eafa-169">Click an application ID toodrill down into an application for more info.</span></span>
   
    ![Iniciar o Servidor de Histórico do Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="0eafa-171">Consulte também</span><span class="sxs-lookup"><span data-stu-id="0eafa-171">See also</span></span>
*  [<span data-ttu-id="0eafa-172">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="0eafa-172">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="0eafa-173">Para analistas de dados</span><span class="sxs-lookup"><span data-stu-id="0eafa-173">For data analysts</span></span>

* [<span data-ttu-id="0eafa-174">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="0eafa-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="0eafa-175">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="0eafa-175">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="0eafa-176">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0eafa-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="0eafa-177">Análise da telemetria de dados do Application Insight usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0eafa-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="0eafa-178">Usar o Caffe no Azure HDInsight Spark para aprendizado aprofundado distribuído</span><span class="sxs-lookup"><span data-stu-id="0eafa-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="0eafa-179">Para desenvolvedores do Spark</span><span class="sxs-lookup"><span data-stu-id="0eafa-179">For Spark developers</span></span>

* [<span data-ttu-id="0eafa-180">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="0eafa-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="0eafa-181">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="0eafa-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="0eafa-182">Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos</span><span class="sxs-lookup"><span data-stu-id="0eafa-182">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="0eafa-183">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="0eafa-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="0eafa-184">Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente</span><span class="sxs-lookup"><span data-stu-id="0eafa-184">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="0eafa-185">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0eafa-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="0eafa-186">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="0eafa-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="0eafa-187">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="0eafa-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="0eafa-188">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="0eafa-188">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


