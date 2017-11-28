---
title: "Depurar trabalhos do Apache Spark em execução no Azure HDInsight | Microsoft Docs"
description: "Use a interface do usuário do YARN, a interface do usuário do Spark e o Servidor de Histórico do Spark para rastrear e depurar trabalhos em execução no cluster Spark no Azure HDInsight"
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
ms.openlocfilehash: bf66757cc9439a969c9f28abc0b95055ff697c3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="46e3d-103">Depurar trabalhos do Apache Spark em execução no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="46e3d-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="46e3d-104">Neste artigo, você aprenderá como rastrear e depurar trabalhos do Spark em execução em clusters do HDInsight usando a interface do usuário do YARN, a interface do usuário do Spark e o Servidor de histórico do Spark.</span><span class="sxs-lookup"><span data-stu-id="46e3d-104">In this article you will learn how to track and debug Spark jobs running on HDInsight clusters using the YARN UI, Spark UI, and the Spark History Server.</span></span> <span data-ttu-id="46e3d-105">Para este artigo, começaremos um trabalho do Spark usando um notebook disponível com o cluster Spark, **Machine Learning: análise preditiva nos dados de inspeção de alimentos usando MLLib**.</span><span class="sxs-lookup"><span data-stu-id="46e3d-105">For this article, we will start a Spark job using a notebook available with the Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="46e3d-106">Você pode usar as etapas a seguir para rastrear um aplicativo que foi enviado usando qualquer outra abordagem, por exemplo, **spark-submit**.</span><span class="sxs-lookup"><span data-stu-id="46e3d-106">You can use the steps below to track an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46e3d-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="46e3d-107">Prerequisites</span></span>
<span data-ttu-id="46e3d-108">Você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="46e3d-108">You must have the following:</span></span>

* <span data-ttu-id="46e3d-109">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="46e3d-109">An Azure subscription.</span></span> <span data-ttu-id="46e3d-110">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="46e3d-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="46e3d-111">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="46e3d-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="46e3d-112">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="46e3d-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="46e3d-113">Você deve ter começado a executar o notebook **[Machine Learning: análise preditiva nos dados de inspeção de alimentos usando MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="46e3d-113">You should have started running the notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="46e3d-114">Para obter instruções sobre como executar este notebook, siga o link.</span><span class="sxs-lookup"><span data-stu-id="46e3d-114">For instructions on how to run this notebook, follow the link.</span></span>  

## <a name="track-an-application-in-the-yarn-ui"></a><span data-ttu-id="46e3d-115">Rastrear um aplicativo na interface do usuário do YARN</span><span class="sxs-lookup"><span data-stu-id="46e3d-115">Track an application in the YARN UI</span></span>
1. <span data-ttu-id="46e3d-116">Inicie a interface do usuário do YARN.</span><span class="sxs-lookup"><span data-stu-id="46e3d-116">Launch the YARN UI.</span></span> <span data-ttu-id="46e3d-117">Na folha do cluster, clique em **Painel do Cluster** e em **YARN**.</span><span class="sxs-lookup"><span data-stu-id="46e3d-117">From the cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Iniciar Interface do usuário do YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="46e3d-119">Alternativamente, também é possível iniciar a interface do usuário do YARN na interface do usuário do Ambari.</span><span class="sxs-lookup"><span data-stu-id="46e3d-119">Alternatively, you can also launch the YARN UI from the Ambari UI.</span></span> <span data-ttu-id="46e3d-120">Para iniciar a interface de usuário do Ambari, na folha do cluster, clique em **Painel do Cluster** e em **Painel do Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="46e3d-120">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="46e3d-121">Na interface de usuário do Ambari, clique em **YARN**, em **Links Rápidos**, no gerenciador de recursos ativo e, por fim, em **Interface de Usuário do Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="46e3d-121">From the Ambari UI, click **YARN**, click **Quick Links**, click the active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="46e3d-122">Como você iniciou o trabalho do Spark usando notebooks Jupyter, o aplicativo tem o nome **remotesparkmagics** (esse é o nome de todos os aplicativos que são iniciados do notebook).</span><span class="sxs-lookup"><span data-stu-id="46e3d-122">Because you started the Spark job using Jupyter notebooks, the application has the name **remotesparkmagics** (this is the name for all applications that are started from the notebooks).</span></span> <span data-ttu-id="46e3d-123">Clique na ID de aplicativo com o nome do aplicativo para obter mais informações sobre o trabalho.</span><span class="sxs-lookup"><span data-stu-id="46e3d-123">Click the application ID against the application name to get more information about the job.</span></span> <span data-ttu-id="46e3d-124">Isso inicia o modo de exibição do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46e3d-124">This launches the application view.</span></span>
   
    ![Localizar a ID de aplicativo Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="46e3d-126">Para aplicativos que são iniciados do notebook Jupyter, o status é sempre **EM EXECUÇÃO** até que você saia do notebook.</span><span class="sxs-lookup"><span data-stu-id="46e3d-126">For such applications that are launched from the Jupyter notebooks, the status is always **RUNNING** until you exit the notebook.</span></span>
3. <span data-ttu-id="46e3d-127">Na exibição de aplicativo, você pode fazer drill down para descobrir os contêineres associados ao aplicativo e os logs (stdout/stderr).</span><span class="sxs-lookup"><span data-stu-id="46e3d-127">From the application view, you can drill down further to find out the containers associated with the application and the logs (stdout/stderr).</span></span> <span data-ttu-id="46e3d-128">Você também pode iniciar a interface do usuário do Spark clicando no link correspondente para a **URL de Rastreamento**, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="46e3d-128">You can also launch the Spark UI by clicking the linking corresponding to the **Tracking URL**, as shown below.</span></span> 
   
    ![Baixar logs de contêiner](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a><span data-ttu-id="46e3d-130">Rastrear um aplicativo na interface do usuário do Spark</span><span class="sxs-lookup"><span data-stu-id="46e3d-130">Track an application in the Spark UI</span></span>
<span data-ttu-id="46e3d-131">Na interface do usuário do Spark, é possível fazer drill down em trabalhos do Spark que são gerados pelo aplicativo iniciado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="46e3d-131">In the Spark UI, you can drill down into the Spark jobs that are spawned by the application you started earlier.</span></span>

1. <span data-ttu-id="46e3d-132">Para iniciar a interface do usuário do Spark, da exibição do aplicativo, clique no link em **URL de Rastreamento**, conforme mostrado na captura de tela acima.</span><span class="sxs-lookup"><span data-stu-id="46e3d-132">To launch the Spark UI, from the application view, click the link against the **Tracking URL**, as shown in the screen capture above.</span></span> <span data-ttu-id="46e3d-133">Você pode ver todos os trabalhos do Spark que são iniciados pelo aplicativo em execução no notebook do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="46e3d-133">You can see all the Spark jobs that are launched by the application running in the Jupyter notebook.</span></span>
   
    ![Exibir trabalhos do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="46e3d-135">Clique na guia **Executores** para ver informações de processamento e armazenamento de cada executor.</span><span class="sxs-lookup"><span data-stu-id="46e3d-135">Click the **Executors** tab to see processing and storage information for each executor.</span></span> <span data-ttu-id="46e3d-136">Você também pode recuperar a pilha de chamadas clicando no link **Thread Dump** (Despejo de Thread).</span><span class="sxs-lookup"><span data-stu-id="46e3d-136">You can also retrieve the call stack by clicking on the **Thread Dump** link.</span></span>
   
    ![Exibir executores do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="46e3d-138">Clique na guia **Estágios** para ver os estágios associados ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46e3d-138">Click the **Stages** tab to see the stages associated with the application.</span></span>
   
    ![Exibir estágios do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="46e3d-140">Cada estágio pode ter várias tarefas para as quais você pode exibir estatísticas de execução, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="46e3d-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Exibir estágios do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="46e3d-142">Na página de detalhes do estágio, você pode iniciar Visualização de DAG.</span><span class="sxs-lookup"><span data-stu-id="46e3d-142">From the stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="46e3d-143">Expanda o link **DAG Visualization** (Visualização de DAG) na parte superior da página, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="46e3d-143">Expand the **DAG Visualization** link at the top of the page, as shown below.</span></span>
   
    ![Exibir a visualização de DAG dos estágios do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="46e3d-145">O DAG ou Gráfico Acíclico Direto representa os diferentes estágios no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46e3d-145">DAG or Direct Aclyic Graph represents the different stages in the application.</span></span> <span data-ttu-id="46e3d-146">Cada caixa azul no gráfico representa uma operação do Spark iniciada do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46e3d-146">Each blue box in the graph represents a Spark operation invoked from the application.</span></span>
5. <span data-ttu-id="46e3d-147">Na página de detalhes do estágio, você também pode iniciar o modo de exibição de linha do tempo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46e3d-147">From the stage details page, you can also launch the application timeline view.</span></span> <span data-ttu-id="46e3d-148">Expanda o link **Event Timeline** (Linha do Tempo do Evento) na parte superior da página, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="46e3d-148">Expand the **Event Timeline** link at the top of the page, as shown below.</span></span>
   
    ![Exibir linha do tempo de evento de estágios do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="46e3d-150">Isso exibe os eventos do Spark na forma de uma linha do tempo.</span><span class="sxs-lookup"><span data-stu-id="46e3d-150">This displays the Spark events in the form of a timeline.</span></span> <span data-ttu-id="46e3d-151">O modo de exibição de tempo está disponível em três níveis, entre trabalhos, dentro de um trabalho e dentro de um estágio.</span><span class="sxs-lookup"><span data-stu-id="46e3d-151">The timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="46e3d-152">A imagem acima captura o modo de exibição de linha do tempo de um determinado estágio.</span><span class="sxs-lookup"><span data-stu-id="46e3d-152">The image above captures the timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="46e3d-153">Se você selecionar a caixa de seleção **Enable zooming** (Habilitar zoom), poderá rolar para a esquerda e para a direita no modo de exibição de linha do tempo.</span><span class="sxs-lookup"><span data-stu-id="46e3d-153">If you select the **Enable zooming** check box, you can scroll left and right across the timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="46e3d-154">Outras guias na interface do usuário do Spark fornecem informações úteis sobre a instância do Spark.</span><span class="sxs-lookup"><span data-stu-id="46e3d-154">Other tabs in the Spark UI provide useful information about the Spark instance as well.</span></span>
   
   * <span data-ttu-id="46e3d-155">Guia Armazenamento: se seu aplicativo criar RDDs, você encontrará informações sobre isso na guia Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="46e3d-155">Storage tab - If your application creates an RDDs, you can find information about those in the Storage tab.</span></span>
   * <span data-ttu-id="46e3d-156">Guia Ambiente: esta guia fornece muitas informações úteis sobre sua instância do Spark, como a</span><span class="sxs-lookup"><span data-stu-id="46e3d-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as the</span></span> 
     * <span data-ttu-id="46e3d-157">Versão da escala</span><span class="sxs-lookup"><span data-stu-id="46e3d-157">Scala version</span></span>
     * <span data-ttu-id="46e3d-158">Diretório de log de eventos associado ao cluster</span><span class="sxs-lookup"><span data-stu-id="46e3d-158">Event log directory associated with the cluster</span></span>
     * <span data-ttu-id="46e3d-159">Número de núcleos de executor do aplicativo</span><span class="sxs-lookup"><span data-stu-id="46e3d-159">Number of executor cores for the application</span></span>
     * <span data-ttu-id="46e3d-160">Etc.</span><span class="sxs-lookup"><span data-stu-id="46e3d-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a><span data-ttu-id="46e3d-161">Encontrar informações sobre trabalhos concluídos usando o Servidor de Histórico do Spark</span><span class="sxs-lookup"><span data-stu-id="46e3d-161">Find information about completed jobs using the Spark History Server</span></span>
<span data-ttu-id="46e3d-162">Quando um trabalho é concluído, as informações sobre ele são mantidas no Servidor de Histórico do Spark.</span><span class="sxs-lookup"><span data-stu-id="46e3d-162">Once a job is completed, the information about the job is persisted in the Spark History Server.</span></span>

1. <span data-ttu-id="46e3d-163">Para iniciar o Servidor de Histórico do Spark, na folha do cluster, clique em **Painel do Cluster** e, em seguida, clique em **Servidor de Histórico do Spark**.</span><span class="sxs-lookup"><span data-stu-id="46e3d-163">To launch the Spark History Server, from the cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Iniciar o Servidor de Histórico do Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="46e3d-165">Alternativamente, também é possível iniciar a interface do usuário do Servidor de Histórico do Spark na interface do usuário do Ambari.</span><span class="sxs-lookup"><span data-stu-id="46e3d-165">Alternatively, you can also launch the Spark History Server UI from the Ambari UI.</span></span> <span data-ttu-id="46e3d-166">Para iniciar a interface de usuário do Ambari, na folha do cluster, clique em **Painel do Cluster** e em **Painel do Cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="46e3d-166">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="46e3d-167">Na interface do usuário do Ambari, clique em **Spark**, clique em **Links Rápidos**, e, em seguida, clique em **Spark History Server UI** (Interface do usuário do Servidor de Histórico do Spark).</span><span class="sxs-lookup"><span data-stu-id="46e3d-167">From the Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="46e3d-168">Você verá todos os aplicativos concluídos listados.</span><span class="sxs-lookup"><span data-stu-id="46e3d-168">You will see all the completed applications listed.</span></span> <span data-ttu-id="46e3d-169">Clique em uma ID de aplicativo para fazer o drill down em um aplicativo para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="46e3d-169">Click an application ID to drill down into an application for more info.</span></span>
   
    ![Iniciar o Servidor de Histórico do Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="46e3d-171">Consulte também</span><span class="sxs-lookup"><span data-stu-id="46e3d-171">See also</span></span>
*  [<span data-ttu-id="46e3d-172">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="46e3d-172">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="46e3d-173">Para analistas de dados</span><span class="sxs-lookup"><span data-stu-id="46e3d-173">For data analysts</span></span>

* [<span data-ttu-id="46e3d-174">Spark com Machine Learning: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="46e3d-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* <span data-ttu-id="46e3d-175">
            [Spark com Machine Learning: usar o Spark no HDInsight para prever resultados da inspeção de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)</span><span class="sxs-lookup"><span data-stu-id="46e3d-175">[Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results](hdinsight-apache-spark-machine-learning-mllib-ipython.md)</span></span>
* [<span data-ttu-id="46e3d-176">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="46e3d-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="46e3d-177">Análise da telemetria de dados do Application Insight usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="46e3d-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="46e3d-178">Usar o Caffe no Azure HDInsight Spark para aprendizado aprofundado distribuído</span><span class="sxs-lookup"><span data-stu-id="46e3d-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="46e3d-179">Para desenvolvedores do Spark</span><span class="sxs-lookup"><span data-stu-id="46e3d-179">For Spark developers</span></span>

* [<span data-ttu-id="46e3d-180">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="46e3d-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="46e3d-181">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="46e3d-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="46e3d-182">Use o Plug-in de Ferramentas do HDInsight para IntelliJ IDEA para criar e enviar aplicativos Spark Scala</span><span class="sxs-lookup"><span data-stu-id="46e3d-182">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="46e3d-183">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="46e3d-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="46e3d-184">Usar o plug-in de Ferramentas do HDInsight para depurar aplicativos Spark remotamente</span><span class="sxs-lookup"><span data-stu-id="46e3d-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="46e3d-185">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="46e3d-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="46e3d-186">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="46e3d-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="46e3d-187">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="46e3d-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="46e3d-188">Instalar o Jupyter em seu computador e conectar-se a um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="46e3d-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


