---
title: aaaMicrosoft cognitivas Toolkit com Spark no HDInsight para aprendizado | Microsoft Docs
description: "Saiba como um treinado Microsoft cognitivas Toolkit profunda modelo de aprendizado pode ser o conjunto de dados de tooa aplicada usando Olá Spark Python API em um cluster Spark no HDInsight."
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
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="b41d0-103">Use o modelo de aprendizado profundo treinado das Ferramentas Cognitivas da Microsoft com o cluster do Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b41d0-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="b41d0-104">Neste artigo, você Olá seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="b41d0-104">In this article, you do hello following steps.</span></span>

1. <span data-ttu-id="b41d0-105">Execute um script personalizado de tooinstall cognitivas Kit de ferramentas do Microsoft em um cluster do Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b41d0-105">Run a custom script tooinstall Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="b41d0-106">Carregar um Jupyter notebook toohello Spark cluster toosee como tooapply um treinado Microsoft cognitivas Toolkit profunda aprendizado toofiles de modelo em uma conta de armazenamento de Blob do Azure usando Olá [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="b41d0-106">Upload a Jupyter notebook toohello Spark cluster toosee how tooapply a trained Microsoft Cognitive Toolkit deep learning model toofiles in an Azure Blob Storage Account using hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b41d0-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b41d0-107">Prerequisites</span></span>

* <span data-ttu-id="b41d0-108">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="b41d0-108">**An Azure subscription**.</span></span> <span data-ttu-id="b41d0-109">Antes de começar este tutorial, você deverá ter uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b41d0-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="b41d0-110">Consulte [Criar sua conta gratuita do Azure hoje](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="b41d0-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="b41d0-111">**Cluster do Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="b41d0-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="b41d0-112">Para este artigo, crie um cluster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="b41d0-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="b41d0-113">Para obter instruções, consulte [Criar um cluster do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b41d0-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="b41d0-114">Como é o fluxo dessa solução?</span><span class="sxs-lookup"><span data-stu-id="b41d0-114">How does this solution flow?</span></span>

<span data-ttu-id="b41d0-115">Essa solução é dividida entre este artigo e um Notebook Jupyter que é carregado como parte deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b41d0-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="b41d0-116">Neste artigo, você deve concluir Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b41d0-116">In this article, you complete hello following steps:</span></span>

* <span data-ttu-id="b41d0-117">Execute uma ação de script em um cluster do HDInsight Spark tooinstall Microsoft cognitivas Toolkit e Python pacotes.</span><span class="sxs-lookup"><span data-stu-id="b41d0-117">Run a script action on an HDInsight Spark cluster tooinstall Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="b41d0-118">Carregamento de anotações do Jupyter Olá executado Olá solução toohello cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="b41d0-118">Upload hello Jupyter notebook that runs hello solution toohello HDInsight Spark cluster.</span></span>

<span data-ttu-id="b41d0-119">Olá seguir etapas restantes são abordadas em anotações do Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="b41d0-119">hello following remaining steps are covered in hello Jupyter notebook.</span></span>

- <span data-ttu-id="b41d0-120">Carregar imagens de exemplo em um Conjunto de dados distribuído resiliente, ou RDD, do Spark</span><span class="sxs-lookup"><span data-stu-id="b41d0-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="b41d0-121">Carregar módulos e definir predefinições</span><span class="sxs-lookup"><span data-stu-id="b41d0-121">Load modules and define presets</span></span>
   - <span data-ttu-id="b41d0-122">Baixar o dataset Olá localmente no cluster do Spark Olá</span><span class="sxs-lookup"><span data-stu-id="b41d0-122">Download hello dataset locally on hello Spark cluster</span></span>
   - <span data-ttu-id="b41d0-123">Converter o conjunto de dados de saudação em um RDD</span><span class="sxs-lookup"><span data-stu-id="b41d0-123">Convert hello dataset into an RDD</span></span>
- <span data-ttu-id="b41d0-124">Imagens de saudação de pontuação usando um kit de ferramentas cognitivas treinado</span><span class="sxs-lookup"><span data-stu-id="b41d0-124">Score hello images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="b41d0-125">Baixar Olá treinado Toolkit cognitivas modelo toohello Spark cluster</span><span class="sxs-lookup"><span data-stu-id="b41d0-125">Download hello trained Cognitive Toolkit model toohello Spark cluster</span></span>
   - <span data-ttu-id="b41d0-126">Definir funções toobe usada por nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="b41d0-126">Define functions toobe used by worker nodes</span></span>
   - <span data-ttu-id="b41d0-127">Imagens de pontuação Olá em nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="b41d0-127">Score hello images on worker nodes</span></span>
   - <span data-ttu-id="b41d0-128">Avaliar a precisão do modelo</span><span class="sxs-lookup"><span data-stu-id="b41d0-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="b41d0-129">Instalar o Kit de Ferramentas Cognitivas da Microsoft</span><span class="sxs-lookup"><span data-stu-id="b41d0-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="b41d0-130">Você pode instalar o Kit de Ferramentas Cognitivas da Microsoft em um cluster do Spark usando ação de script.</span><span class="sxs-lookup"><span data-stu-id="b41d0-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="b41d0-131">Ação de script usa componentes de tooinstall scripts personalizados no cluster Olá que não estão disponíveis por padrão.</span><span class="sxs-lookup"><span data-stu-id="b41d0-131">Script action uses custom scripts tooinstall components on hello cluster that are not available by default.</span></span> <span data-ttu-id="b41d0-132">Você pode usar o script personalizado de saudação do hello Portal do Azure, usando o SDK do HDInsight .NET ou usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="b41d0-132">You can use hello custom script from hello Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="b41d0-133">Você também pode usar o Kit de ferramentas do hello script tooinstall hello ou como parte da criação do cluster, ou depois que o cluster hello está em execução.</span><span class="sxs-lookup"><span data-stu-id="b41d0-133">You can also use hello script tooinstall hello toolkit either as part of cluster creation, or after hello cluster is up and running.</span></span> 

<span data-ttu-id="b41d0-134">Neste artigo, usamos Olá tooinstall portal Olá toolkit, depois Olá cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="b41d0-134">In this article, we use hello portal tooinstall hello toolkit, after hello cluster has been created.</span></span> <span data-ttu-id="b41d0-135">Para outro maneiras toorun Olá script personalizado, consulte [HDInsight personalizar clusters usando a ação de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b41d0-135">For other ways toorun hello custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="b41d0-136">Usando Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b41d0-136">Using hello Azure Portal</span></span>

<span data-ttu-id="b41d0-137">Para obter instruções sobre como toouse hello Azure Portal toorun scripts de ação, consulte [HDInsight personalizar clusters usando a ação de Script](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span><span class="sxs-lookup"><span data-stu-id="b41d0-137">For instructions on how toouse hello Azure Portal toorun script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="b41d0-138">Certifique-se de que fornecer Olá entradas tooinstall cognitivas Kit de ferramentas da Microsoft a seguir.</span><span class="sxs-lookup"><span data-stu-id="b41d0-138">Make sure you provide hello following inputs tooinstall Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="b41d0-139">Forneça um valor para o nome de ação de script hello.</span><span class="sxs-lookup"><span data-stu-id="b41d0-139">Provide a value for hello script action name.</span></span>

* <span data-ttu-id="b41d0-140">Para uma **URI do script Bash**, insira `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span><span class="sxs-lookup"><span data-stu-id="b41d0-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="b41d0-141">Verifique se você executar script hello apenas em Olá nós de cabeçalho e de trabalho e desmarque todas Olá outras caixas de seleção.</span><span class="sxs-lookup"><span data-stu-id="b41d0-141">Make sure you run hello script only on hello head and worker nodes and clear all hello other checkboxes.</span></span>

* <span data-ttu-id="b41d0-142">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b41d0-142">Click **Create**.</span></span>

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a><span data-ttu-id="b41d0-143">Carregar tooAzure de notebook Jupyter de saudação cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b41d0-143">Upload hello Jupyter notebook tooAzure HDInsight Spark cluster</span></span>

<span data-ttu-id="b41d0-144">Olá toouse Microsoft cognitivas Toolkit com cluster do Azure HDInsight Spark hello, você deve carregar anotações do Jupyter Olá **CNTK_model_scoring_on_Spark_walkthrough.ipynb** cluster do Spark no HDInsight toohello.</span><span class="sxs-lookup"><span data-stu-id="b41d0-144">toouse hello Microsoft Cognitive Toolkit with hello Azure HDInsight Spark cluster, you must load hello Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="b41d0-145">Esse bloco de anotações está disponível no GitHub em [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="b41d0-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="b41d0-146">Repositório do GitHub Olá clone [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span><span class="sxs-lookup"><span data-stu-id="b41d0-146">Clone hello GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="b41d0-147">Para obter instruções tooclone, consulte [clonando um repositório](https://help.github.com/articles/cloning-a-repository/).</span><span class="sxs-lookup"><span data-stu-id="b41d0-147">For instructions tooclone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="b41d0-148">Em Olá Portal do Azure, abra a folha de cluster do Spark Olá já provisionada, clique **painel Cluster**e, em seguida, clique em **notebook Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="b41d0-148">From hello Azure Portal, open hello Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="b41d0-149">Você também pode iniciar de anotações do Jupyter Olá indo URL toohello `https://<clustername>.azurehdinsight.net/jupyter/`.</span><span class="sxs-lookup"><span data-stu-id="b41d0-149">You can also launch hello Jupyter notebook by going toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="b41d0-150">Substituir \<clustername > pelo nome de saudação do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b41d0-150">Replace \<clustername> with hello name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="b41d0-151">De anotações do Jupyter hello, clique em **carregar** em Olá canto superior direito e navegue toohello local em que você clonou repositório do GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="b41d0-151">From hello Jupyter notebook, click **Upload** in hello top-right corner and then navigate toohello location where you cloned hello GitHub repository.</span></span>

    <span data-ttu-id="b41d0-152">![Carregar tooAzure de notebook Jupyter cluster HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "tooAzure de notebook Jupyter carregar cluster HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="b41d0-152">![Upload Jupyter notebook tooAzure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook tooAzure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="b41d0-153">Clique em **Carregar** novamente.</span><span class="sxs-lookup"><span data-stu-id="b41d0-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="b41d0-154">Depois notebook Olá é carregado, clique em nome de saudação do bloco de anotações de saudação e siga as instruções de Olá no bloco de anotações de saudação em si no como tooload Olá conjunto de dados e executar o tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="b41d0-154">After hello notebook is uploaded, click hello name of hello notebook and then follow hello instructions in hello notebook itself on how tooload hello data set and perform hello tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="b41d0-155">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b41d0-155">See also</span></span>
* [<span data-ttu-id="b41d0-156">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b41d0-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="b41d0-157">Cenários</span><span class="sxs-lookup"><span data-stu-id="b41d0-157">Scenarios</span></span>
* [<span data-ttu-id="b41d0-158">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="b41d0-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b41d0-159">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="b41d0-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b41d0-160">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="b41d0-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b41d0-161">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="b41d0-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b41d0-162">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b41d0-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="b41d0-163">Análise da telemetria de dados do Application Insight usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b41d0-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b41d0-164">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="b41d0-164">Create and run applications</span></span>
* [<span data-ttu-id="b41d0-165">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="b41d0-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b41d0-166">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="b41d0-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b41d0-167">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="b41d0-167">Tools and extensions</span></span>
* [<span data-ttu-id="b41d0-168">Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos</span><span class="sxs-lookup"><span data-stu-id="b41d0-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b41d0-169">Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente</span><span class="sxs-lookup"><span data-stu-id="b41d0-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b41d0-170">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b41d0-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b41d0-171">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="b41d0-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b41d0-172">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="b41d0-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b41d0-173">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b41d0-173">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b41d0-174">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="b41d0-174">Manage resources</span></span>
* [<span data-ttu-id="b41d0-175">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="b41d0-175">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b41d0-176">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b41d0-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
