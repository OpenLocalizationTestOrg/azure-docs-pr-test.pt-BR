---
title: Kit de Ferramentas Cognitivas da Microsoft com Azure HDInsight Spark para aprendizado aprofundado | Microsoft Docs
description: Saiba como o modelo de aprendizado aprofundado treinado das Ferramentas Cognitivas da Microsoft pode ser aplicado a um conjunto de dados usando a API Python Spark em um cluster do Azure HDInsight Spark.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: fafd738f782660b824732bab8cc3bec8405947e7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="145b6-103">Use o modelo de aprendizado profundo treinado das Ferramentas Cognitivas da Microsoft com o cluster do Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="145b6-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="145b6-104">Neste artigo, você executa as seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="145b6-104">In this article, you do the following steps.</span></span>

1. <span data-ttu-id="145b6-105">Executar um script personalizado para instalar o Kit de Ferramentas Cognitivas da Microsoft em um cluster do Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="145b6-105">Run a custom script to install Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="145b6-106">Carregar um Notebook Jupyter no cluster do Spark para ver como aplicar um modelo de aprendizado profundo treinado do Kit de Ferramentas Cognitivas da Microsoft a arquivos em uma Conta de Armazenamento de Blobs do Azure usando a [API Python Spark (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="145b6-106">Upload a Jupyter notebook to the Spark cluster to see how to apply a trained Microsoft Cognitive Toolkit deep learning model to files in an Azure Blob Storage Account using the [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="145b6-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="145b6-107">Prerequisites</span></span>

* <span data-ttu-id="145b6-108">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="145b6-108">**An Azure subscription**.</span></span> <span data-ttu-id="145b6-109">Antes de começar este tutorial, você deverá ter uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="145b6-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="145b6-110">Consulte [Criar sua conta gratuita do Azure hoje](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="145b6-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="145b6-111">**Cluster do Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="145b6-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="145b6-112">Para este artigo, crie um cluster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="145b6-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="145b6-113">Para obter instruções, consulte [Criar um cluster do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="145b6-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="145b6-114">Como é o fluxo dessa solução?</span><span class="sxs-lookup"><span data-stu-id="145b6-114">How does this solution flow?</span></span>

<span data-ttu-id="145b6-115">Essa solução é dividida entre este artigo e um Notebook Jupyter que é carregado como parte deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="145b6-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="145b6-116">Neste artigo, você realiza as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="145b6-116">In this article, you complete the following steps:</span></span>

* <span data-ttu-id="145b6-117">Executar uma ação de script em um cluster HDInsight Spark para instalar pacotes do Python e do Kit de Ferramentas Cognitivas da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="145b6-117">Run a script action on an HDInsight Spark cluster to install Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="145b6-118">Carregar o Notebook Jupyter que executa a solução no cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="145b6-118">Upload the Jupyter notebook that runs the solution to the HDInsight Spark cluster.</span></span>

<span data-ttu-id="145b6-119">As seguintes etapas restantes são abordadas no Notebook Jupyter.</span><span class="sxs-lookup"><span data-stu-id="145b6-119">The following remaining steps are covered in the Jupyter notebook.</span></span>

- <span data-ttu-id="145b6-120">Carregar imagens de exemplo em um Conjunto de dados distribuído resiliente, ou RDD, do Spark</span><span class="sxs-lookup"><span data-stu-id="145b6-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="145b6-121">Carregar módulos e definir predefinições</span><span class="sxs-lookup"><span data-stu-id="145b6-121">Load modules and define presets</span></span>
   - <span data-ttu-id="145b6-122">Baixar o conjunto de dados localmente no cluster do Spark</span><span class="sxs-lookup"><span data-stu-id="145b6-122">Download the dataset locally on the Spark cluster</span></span>
   - <span data-ttu-id="145b6-123">Converter o conjunto de dados em um RDD</span><span class="sxs-lookup"><span data-stu-id="145b6-123">Convert the dataset into an RDD</span></span>
- <span data-ttu-id="145b6-124">Classificar as imagens usando um modelo treinado do Kit de Ferramentas Cognitivas</span><span class="sxs-lookup"><span data-stu-id="145b6-124">Score the images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="145b6-125">Baixar o modelo treinado do Kit de Ferramentas Cognitivas no cluster do Spark</span><span class="sxs-lookup"><span data-stu-id="145b6-125">Download the trained Cognitive Toolkit model to the Spark cluster</span></span>
   - <span data-ttu-id="145b6-126">Definir funções a serem usadas por nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="145b6-126">Define functions to be used by worker nodes</span></span>
   - <span data-ttu-id="145b6-127">Classificar as imagens em nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="145b6-127">Score the images on worker nodes</span></span>
   - <span data-ttu-id="145b6-128">Avaliar a precisão do modelo</span><span class="sxs-lookup"><span data-stu-id="145b6-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="145b6-129">Instalar o Kit de Ferramentas Cognitivas da Microsoft</span><span class="sxs-lookup"><span data-stu-id="145b6-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="145b6-130">Você pode instalar o Kit de Ferramentas Cognitivas da Microsoft em um cluster do Spark usando ação de script.</span><span class="sxs-lookup"><span data-stu-id="145b6-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="145b6-131">A ação de script usa scripts personalizados para instalar componentes no cluster que não estão disponíveis por padrão.</span><span class="sxs-lookup"><span data-stu-id="145b6-131">Script action uses custom scripts to install components on the cluster that are not available by default.</span></span> <span data-ttu-id="145b6-132">Você pode usar o script personalizado do Portal do Azure, usando o SDK .NET do HDInsight ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="145b6-132">You can use the custom script from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="145b6-133">Você também pode usar o script para instalar o kit de ferramentas como parte da criação do cluster ou depois que o cluster estiver em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="145b6-133">You can also use the script to install the toolkit either as part of cluster creation, or after the cluster is up and running.</span></span> 

<span data-ttu-id="145b6-134">Neste artigo, usamos o portal para instalar o kit de ferramentas após o cluster ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="145b6-134">In this article, we use the portal to install the toolkit, after the cluster has been created.</span></span> <span data-ttu-id="145b6-135">Para ver outras maneiras de executar o script personalizado, consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="145b6-135">For other ways to run the custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="145b6-136">Usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="145b6-136">Using the Azure Portal</span></span>

<span data-ttu-id="145b6-137">Para obter instruções sobre como usar o Portal do Azure para executar a ação de script, consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="145b6-137">For instructions on how to use the Azure Portal to run script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="145b6-138">Certifique-se de fornecer as entradas a seguir para instalar o Kit de Ferramentas Cognitivas da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="145b6-138">Make sure you provide the following inputs to install Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="145b6-139">Forneça um valor para o nome da ação de script.</span><span class="sxs-lookup"><span data-stu-id="145b6-139">Provide a value for the script action name.</span></span>

* <span data-ttu-id="145b6-140">Para uma **URI do script Bash**, insira `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="145b6-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="145b6-141">Verifique se você executou o script apenas em nós de cabeçalho e de trabalho e desmarque todas as outras caixas de seleção.</span><span class="sxs-lookup"><span data-stu-id="145b6-141">Make sure you run the script only on the head and worker nodes and clear all the other checkboxes.</span></span>

* <span data-ttu-id="145b6-142">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="145b6-142">Click **Create**.</span></span>

## <a name="upload-the-jupyter-notebook-to-azure-hdinsight-spark-cluster"></a><span data-ttu-id="145b6-143">Carregue o Notebook Jupyter para o cluster do Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="145b6-143">Upload the Jupyter notebook to Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="145b6-144">Para usar o Kit de Ferramentas Cognitivas da Microsoft com o cluster do Azure HDInsight Spark, você precisa carregar o Notebook Jupyter **CNTK_model_scoring_on_Spark_walkthrough.ipynb** no cluster do Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="145b6-144">To use the Microsoft Cognitive Toolkit with the Azure HDInsight Spark cluster, you must load the Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** to the Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="145b6-145">Esse bloco de anotações está disponível no GitHub em [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="145b6-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="145b6-146">Clone o repositório do GitHub [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="145b6-146">Clone the GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="145b6-147">Para obter instruções para clonar, consulte [Clonando um repositório](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="145b6-147">For instructions to clone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="145b6-148">No Portal do Azure, abra a folha do cluster do Spark que você já provisionado, clique em **Painel do Cluster** e, em seguida, clique em **Notebook Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="145b6-148">From the Azure Portal, open the Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="145b6-149">Você também pode iniciar o Notebook Jupyter indo para a URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="145b6-149">You can also launch the Jupyter notebook by going to the URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="145b6-150">Substitua \<clustername> pelo nome do seu cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="145b6-150">Replace \<clustername> with the name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="145b6-151">No Notebook Jupyter, clique em **Carregar** no canto superior direito e, em seguida, navegue até o local no qual você clonou o repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="145b6-151">From the Jupyter notebook, click **Upload** in the top-right corner and then navigate to the location where you cloned the GitHub repository.</span></span>

    <span data-ttu-id="145b6-152">![Carregar o Notebook Jupyter para o cluster do Azure HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Carregar o bloco de anotações do Jupyter para o cluster do Azure HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="145b6-152">![Upload Jupyter notebook to Azure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="145b6-153">Clique em **Carregar** novamente.</span><span class="sxs-lookup"><span data-stu-id="145b6-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="145b6-154">Após o bloco de anotações ser carregado, clique em seu nome e, em seguida, siga as instruções contidas nele sobre como carregar o conjunto de dados e executar o tutorial.</span><span class="sxs-lookup"><span data-stu-id="145b6-154">After the notebook is uploaded, click the name of the notebook and then follow the instructions in the notebook itself on how to load the data set and perform the tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="145b6-155">Consulte também</span><span class="sxs-lookup"><span data-stu-id="145b6-155">See also</span></span>
* [<span data-ttu-id="145b6-156">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="145b6-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="145b6-157">Cenários</span><span class="sxs-lookup"><span data-stu-id="145b6-157">Scenarios</span></span>
* [<span data-ttu-id="145b6-158">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="145b6-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="145b6-159">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="145b6-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="145b6-160">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para prever resultados da inspeção de alimentos</span><span class="sxs-lookup"><span data-stu-id="145b6-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="145b6-161">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="145b6-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="145b6-162">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="145b6-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="145b6-163">Análise da telemetria de dados do Application Insight usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="145b6-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="145b6-164">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="145b6-164">Create and run applications</span></span>
* [<span data-ttu-id="145b6-165">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="145b6-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="145b6-166">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="145b6-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="145b6-167">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="145b6-167">Tools and extensions</span></span>
* [<span data-ttu-id="145b6-168">Use o Plug-in de Ferramentas do HDInsight para IntelliJ IDEA para criar e enviar aplicativos Spark Scala</span><span class="sxs-lookup"><span data-stu-id="145b6-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="145b6-169">Usar o plug-in de Ferramentas do HDInsight para depurar aplicativos Spark remotamente</span><span class="sxs-lookup"><span data-stu-id="145b6-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="145b6-170">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="145b6-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="145b6-171">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="145b6-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="145b6-172">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="145b6-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="145b6-173">Instalar o Jupyter em seu computador e conectar-se a um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="145b6-173">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="145b6-174">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="145b6-174">Manage resources</span></span>
* [<span data-ttu-id="145b6-175">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="145b6-175">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="145b6-176">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="145b6-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
