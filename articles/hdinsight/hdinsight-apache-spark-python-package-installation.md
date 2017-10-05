---
title: "Ação de script – instalar pacotes Python com o Jupyter no Azure HDInsight | Microsoft Docs"
description: "Instruções passo a passo sobre como usar ação de script para configurar os blocos de anotações do Jupyter disponíveis com clusters Spark no HDInsight para usar pacotes Python externos."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 20cf384c96d4ff4eaf064c8880ad128d521fb9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-script-action-to-install-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="410d4-103">Usar ação de script para instalar pacotes Python externos em notebooks Jupyter em clusters do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="410d4-103">Use Script Action to install external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="410d4-104">Usando a mágica da célula</span><span class="sxs-lookup"><span data-stu-id="410d4-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="410d4-105">Usando a ação de script</span><span class="sxs-lookup"><span data-stu-id="410d4-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="410d4-106">Saiba como usar Ações de Script para configurar um cluster Apache Spark no HDInsight (Linux) para usar pacotes **Python** externos enviados pela comunidade que não estão incluídos de fábrica no cluster.</span><span class="sxs-lookup"><span data-stu-id="410d4-106">Learn how to use Script Actions to configure an Apache Spark cluster on HDInsight (Linux) to use external, community-contributed **python** packages that are not included out-of-the-box in the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="410d4-107">Você também pode configurar um notebook Jupyter usando a mágica `%%configure` para usar pacotes externos.</span><span class="sxs-lookup"><span data-stu-id="410d4-107">You can also configure a Jupyter notebook by using `%%configure` magic to use external packages.</span></span> <span data-ttu-id="410d4-108">Para obter instruções, confira [Usar pacotes externos com notebooks Jupyter em clusters do Apache Spark no HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="410d4-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="410d4-109">Você pode pesquisar o [índice do pacote](https://pypi.python.org/pypi) para obter uma lista de pacotes que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="410d4-109">You can search the [package index](https://pypi.python.org/pypi) for the complete list of packages that are available.</span></span> <span data-ttu-id="410d4-110">Você também pode obter uma lista de pacotes disponíveis de outras fontes.</span><span class="sxs-lookup"><span data-stu-id="410d4-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="410d4-111">Por exemplo, você pode instalar pacotes disponibilizados por meio de [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) ou [conda-forge](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="410d4-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="410d4-112">Neste artigo, você aprenderá como instalar o pacote [TensorFlow](https://www.tensorflow.org/) usando a Ação de Script no seu cluster e usá-lo por meio do Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="410d4-112">In this article, you will learn how to install the [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via the Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="410d4-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="410d4-113">Prerequisites</span></span>
<span data-ttu-id="410d4-114">Você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="410d4-114">You must have the following:</span></span>

* <span data-ttu-id="410d4-115">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="410d4-115">An Azure subscription.</span></span> <span data-ttu-id="410d4-116">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="410d4-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="410d4-117">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="410d4-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="410d4-118">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="410d4-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="410d4-119">Se você ainda não tiver um cluster Spark no HDInsight Linux, poderá executar ações de script durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="410d4-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="410d4-120">Acesse a documentação em [como usar ações de script personalizadas](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="410d4-120">Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="410d4-121">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="410d4-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="410d4-122">No [Portal do Azure](https://portal.azure.com/), no quadro inicial, clique no bloco do cluster Spark (se você o tiver fixado no quadro inicial).</span><span class="sxs-lookup"><span data-stu-id="410d4-122">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="410d4-123">Você também pode navegar até o cluster em **Procurar Tudo** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="410d4-123">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="410d4-124">Na folha do cluster Spark, clique em **Ações de Script** em **Uso**.</span><span class="sxs-lookup"><span data-stu-id="410d4-124">From the Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="410d4-125">Execute a ação personalizada que instala o TensorFlow nos nós principais e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="410d4-125">Run the custom action that installs TensorFlow in the head nodes and the worker nodes.</span></span> <span data-ttu-id="410d4-126">O script bash pode ser referenciado de: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visite a documentação em [como usar ações de script personalizadas](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="410d4-126">The bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="410d4-127">Há duas instalações Python no cluster.</span><span class="sxs-lookup"><span data-stu-id="410d4-127">There are two python installations in the cluster.</span></span> <span data-ttu-id="410d4-128">O Spark usará a instalação do Python Anaconda que se encontra em `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="410d4-128">Spark will use the Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="410d4-129">Faça referência a essa instalação em suas ações personalizadas por meio de `/usr/bin/anaconda/bin/pip` e `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="410d4-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="410d4-130">Abrir um PySpark Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="410d4-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="410d4-131">![Criar um novo bloco de anotações do Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Criar um novo bloco de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="410d4-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="410d4-132">Um novo bloco de anotações é criado e aberto com o nome Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="410d4-132">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="410d4-133">Clique no nome do bloco de anotações na parte superior e digite um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="410d4-133">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="410d4-134">![Fornecer um nome para o bloco de anotações](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Fornecer um nome para o bloco de anotações")</span><span class="sxs-lookup"><span data-stu-id="410d4-134">![Provide a name for the notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="410d4-135">Agora, você fará `import tensorflow` e executará um exemplo de hello world.</span><span class="sxs-lookup"><span data-stu-id="410d4-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="410d4-136">Código a ser copiado:</span><span class="sxs-lookup"><span data-stu-id="410d4-136">Code to copy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="410d4-137">O resultado terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="410d4-137">The result will look like this:</span></span>
    
    <span data-ttu-id="410d4-138">![Execução de código TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Executar código TensorFlow")</span><span class="sxs-lookup"><span data-stu-id="410d4-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="410d4-139"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="410d4-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="410d4-140">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="410d4-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="410d4-141">Cenários</span><span class="sxs-lookup"><span data-stu-id="410d4-141">Scenarios</span></span>
* [<span data-ttu-id="410d4-142">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="410d4-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="410d4-143">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="410d4-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="410d4-144">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para prever resultados da inspeção de alimentos</span><span class="sxs-lookup"><span data-stu-id="410d4-144">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="410d4-145">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="410d4-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="410d4-146">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="410d4-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="410d4-147">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="410d4-147">Create and run applications</span></span>
* [<span data-ttu-id="410d4-148">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="410d4-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="410d4-149">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="410d4-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="410d4-150">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="410d4-150">Tools and extensions</span></span>
* [<span data-ttu-id="410d4-151">Usar pacotes externos com notebooks Jupyter em clusters Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="410d4-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="410d4-152">Use o Plug-in de Ferramentas do HDInsight para IntelliJ IDEA para criar e enviar aplicativos Spark Scala</span><span class="sxs-lookup"><span data-stu-id="410d4-152">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="410d4-153">Usar o plug-in de Ferramentas do HDInsight para depurar aplicativos Spark remotamente</span><span class="sxs-lookup"><span data-stu-id="410d4-153">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="410d4-154">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="410d4-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="410d4-155">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="410d4-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="410d4-156">Instalar o Jupyter em seu computador e conectar-se a um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="410d4-156">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="410d4-157">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="410d4-157">Manage resources</span></span>
* [<span data-ttu-id="410d4-158">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="410d4-158">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="410d4-159">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="410d4-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
