---
title: "ação de aaaScript - pacotes do Python instalar com Jupyter no Azure HDInsight | Microsoft Docs"
description: "Instruções passo a passo sobre como toouse script ação tooconfigure Jupyter notebooks disponíveis com o HDInsight Spark clusters toouse pacotes de python externo."
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
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="152c5-103">Usar pacotes de Python ação de Script tooinstall externos para blocos de anotações do Jupyter em clusters Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="152c5-103">Use Script Action tooinstall external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="152c5-104">Usando a mágica da célula</span><span class="sxs-lookup"><span data-stu-id="152c5-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="152c5-105">Usando a ação de script</span><span class="sxs-lookup"><span data-stu-id="152c5-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="152c5-106">Saiba como toouse ações de Script tooconfigure um cluster do Apache Spark no HDInsight (Linux) toouse externo, contribuído pela comunidade **python** pacotes que não são incluídas de caixa Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="152c5-106">Learn how toouse Script Actions tooconfigure an Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed **python** packages that are not included out-of-the-box in hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="152c5-107">Você também pode configurar um bloco de anotações do Jupyter usando `%%configure` magic pacotes externos toouse.</span><span class="sxs-lookup"><span data-stu-id="152c5-107">You can also configure a Jupyter notebook by using `%%configure` magic toouse external packages.</span></span> <span data-ttu-id="152c5-108">Para obter instruções, confira [Usar pacotes externos com notebooks Jupyter em clusters do Apache Spark no HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span><span class="sxs-lookup"><span data-stu-id="152c5-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="152c5-109">Você pode pesquisar Olá [índice pacote](https://pypi.python.org/pypi) para a lista completa de saudação dos pacotes que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="152c5-109">You can search hello [package index](https://pypi.python.org/pypi) for hello complete list of packages that are available.</span></span> <span data-ttu-id="152c5-110">Você também pode obter uma lista de pacotes disponíveis de outras fontes.</span><span class="sxs-lookup"><span data-stu-id="152c5-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="152c5-111">Por exemplo, você pode instalar pacotes disponibilizados por meio de [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) ou [conda-forge](https://conda-forge.github.io/feedstocks.html).</span><span class="sxs-lookup"><span data-stu-id="152c5-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="152c5-112">Neste artigo, você aprenderá como Olá tooinstall [TensorFlow](https://www.tensorflow.org/) pacote usando o Script Actoin no cluster e usá-lo por meio de anotações do Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="152c5-112">In this article, you will learn how tooinstall hello [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via hello Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="152c5-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="152c5-113">Prerequisites</span></span>
<span data-ttu-id="152c5-114">Você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="152c5-114">You must have hello following:</span></span>

* <span data-ttu-id="152c5-115">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="152c5-115">An Azure subscription.</span></span> <span data-ttu-id="152c5-116">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="152c5-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="152c5-117">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="152c5-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="152c5-118">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="152c5-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="152c5-119">Se você ainda não tiver um cluster Spark no HDInsight Linux, poderá executar ações de script durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="152c5-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="152c5-120">Visite documentação Olá no [como ações de script personalizado toouse](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="152c5-120">Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="152c5-121">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="152c5-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="152c5-122">De saudação [Portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial).</span><span class="sxs-lookup"><span data-stu-id="152c5-122">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="152c5-123">Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="152c5-123">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="152c5-124">Na folha de cluster do Spark hello, clique em **ações de Script** em **uso**.</span><span class="sxs-lookup"><span data-stu-id="152c5-124">From hello Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="152c5-125">Execute a ação personalizada de saudação que instala TensorFlow em nós de cabeçalho hello e nós de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="152c5-125">Run hello custom action that installs TensorFlow in hello head nodes and hello worker nodes.</span></span> <span data-ttu-id="152c5-126">scripts de bash Olá podem ser referenciado de: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh visita Olá documentação [como ações de script personalizado toouse](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="152c5-126">hello bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="152c5-127">Há dois python instalações em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="152c5-127">There are two python installations in hello cluster.</span></span> <span data-ttu-id="152c5-128">Spark usará a instalação de python Anaconda Olá localizada em `/usr/bin/anaconda/bin`.</span><span class="sxs-lookup"><span data-stu-id="152c5-128">Spark will use hello Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="152c5-129">Faça referência a essa instalação em suas ações personalizadas por meio de `/usr/bin/anaconda/bin/pip` e `/usr/bin/anaconda/bin/conda`.</span><span class="sxs-lookup"><span data-stu-id="152c5-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="152c5-130">Abrir um PySpark Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="152c5-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="152c5-131">![Criar um novo bloco de anotações do Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Criar um novo bloco de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="152c5-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="152c5-132">Um novo bloco de anotações é criado e aberto com o nome hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="152c5-132">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="152c5-133">Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="152c5-133">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="152c5-134">![Forneça um nome para o bloco de anotações de saudação](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "forneça um nome para o bloco de anotações de saudação")</span><span class="sxs-lookup"><span data-stu-id="152c5-134">![Provide a name for hello notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="152c5-135">Agora, você fará `import tensorflow` e executará um exemplo de hello world.</span><span class="sxs-lookup"><span data-stu-id="152c5-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="152c5-136">Toocopy de código:</span><span class="sxs-lookup"><span data-stu-id="152c5-136">Code toocopy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="152c5-137">resultado de saudação será assim:</span><span class="sxs-lookup"><span data-stu-id="152c5-137">hello result will look like this:</span></span>
    
    <span data-ttu-id="152c5-138">![Execução de código TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Executar código TensorFlow")</span><span class="sxs-lookup"><span data-stu-id="152c5-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="152c5-139"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="152c5-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="152c5-140">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="152c5-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="152c5-141">Cenários</span><span class="sxs-lookup"><span data-stu-id="152c5-141">Scenarios</span></span>
* [<span data-ttu-id="152c5-142">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="152c5-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="152c5-143">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="152c5-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="152c5-144">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="152c5-144">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="152c5-145">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="152c5-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="152c5-146">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="152c5-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="152c5-147">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="152c5-147">Create and run applications</span></span>
* [<span data-ttu-id="152c5-148">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="152c5-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="152c5-149">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="152c5-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="152c5-150">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="152c5-150">Tools and extensions</span></span>
* [<span data-ttu-id="152c5-151">Usar pacotes externos com notebooks Jupyter em clusters Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="152c5-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="152c5-152">Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos</span><span class="sxs-lookup"><span data-stu-id="152c5-152">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="152c5-153">Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente</span><span class="sxs-lookup"><span data-stu-id="152c5-153">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="152c5-154">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="152c5-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="152c5-155">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="152c5-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="152c5-156">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="152c5-156">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="152c5-157">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="152c5-157">Manage resources</span></span>
* [<span data-ttu-id="152c5-158">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="152c5-158">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="152c5-159">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="152c5-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
