---
title: pacotes de Maven personalizados aaaUse com Jupyter no Spark do Azure | Microsoft Docs
description: "Instruções passo a passo sobre como os clusters de anotações do Jupyter tooconfigure disponíveis com o HDInsight Spark pacotes personalizados de Maven toouse."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="4ad40-103">Usar pacotes externos com blocos de anotações Jupyter em clusters Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ad40-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ad40-104">Usando a mágica da célula</span><span class="sxs-lookup"><span data-stu-id="4ad40-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="4ad40-105">Usando a ação de script</span><span class="sxs-lookup"><span data-stu-id="4ad40-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="4ad40-106">Saiba como tooconfigure um bloco de anotações do Jupyter no cluster do Apache Spark no HDInsight toouse externo, contribuído pela comunidade **maven** pacotes que não são incluídas de caixa Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="4ad40-106">Learn how tooconfigure a Jupyter notebook in Apache Spark cluster on HDInsight toouse external, community-contributed **maven** packages that are not included out-of-the-box in hello cluster.</span></span> 

<span data-ttu-id="4ad40-107">Você pode pesquisar Olá [Repositório Maven](http://search.maven.org/) para a lista completa de saudação dos pacotes que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4ad40-107">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="4ad40-108">Você também pode obter uma lista de pacotes disponíveis de outras fontes.</span><span class="sxs-lookup"><span data-stu-id="4ad40-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="4ad40-109">Por exemplo, uma lista completa dos pacotes enviados pela comunidade está disponível em [Pacotes do Spark](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="4ad40-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="4ad40-110">Neste artigo, você aprenderá como Olá toouse [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pacote com anotações do Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="4ad40-110">In this article, you will learn how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="4ad40-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4ad40-111">Prerequisites</span></span>
<span data-ttu-id="4ad40-112">Você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="4ad40-112">You must have hello following:</span></span>

* <span data-ttu-id="4ad40-113">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ad40-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="4ad40-114">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="4ad40-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="4ad40-115">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="4ad40-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="4ad40-116">De saudação [Portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial).</span><span class="sxs-lookup"><span data-stu-id="4ad40-116">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="4ad40-117">Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4ad40-117">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="4ad40-118">Na folha de cluster do Spark hello, clique em **Links rápidos**e, em seguida, Olá **painel Cluster** folha, clique em **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="4ad40-118">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="4ad40-119">Se solicitado, insira as credenciais de administrador de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4ad40-119">If prompted, enter hello admin credentials for hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4ad40-120">Você também poderá atingir Olá anotações do Jupyter para o cluster por Olá abrir URL a seguir em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="4ad40-120">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="4ad40-121">Substituir **CLUSTERNAME** com nome de saudação do cluster:</span><span class="sxs-lookup"><span data-stu-id="4ad40-121">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="4ad40-122">Crie um novo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="4ad40-122">Create a new notebook.</span></span> <span data-ttu-id="4ad40-123">Clique em **Novo** e em **Spark**.</span><span class="sxs-lookup"><span data-stu-id="4ad40-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="4ad40-124">![Criar um novo bloco de anotações do Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Criar um novo bloco de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="4ad40-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="4ad40-125">Um novo bloco de anotações é criado e aberto com o nome hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="4ad40-125">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="4ad40-126">Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="4ad40-126">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="4ad40-127">![Forneça um nome para o bloco de anotações de saudação](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "forneça um nome para o bloco de anotações de saudação")</span><span class="sxs-lookup"><span data-stu-id="4ad40-127">![Provide a name for hello notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="4ad40-128">Você usará Olá `%%configure` tooconfigure magic Olá notebook toouse um pacote externo.</span><span class="sxs-lookup"><span data-stu-id="4ad40-128">You will use hello `%%configure` magic tooconfigure hello notebook toouse an external package.</span></span> <span data-ttu-id="4ad40-129">Em blocos de anotações que usam pacotes externos, certifique-se de chamar hello `%%configure` magic na primeira célula de código hello.</span><span class="sxs-lookup"><span data-stu-id="4ad40-129">In notebooks that use external packages, make sure you call hello `%%configure` magic in hello first code cell.</span></span> <span data-ttu-id="4ad40-130">Isso garante que kernel Olá pacote de saudação toouse configurado antes do início da sessão de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ad40-130">This ensures that hello kernel is configured toouse hello package before hello session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="4ad40-131">Se você esquecer tooconfigure kernel de saudação na primeira célula do hello, você pode usar o hello `%%configure` com hello `-f` parâmetro, mas que irá reiniciar a sessão de saudação e andamento todos serão perdido.</span><span class="sxs-lookup"><span data-stu-id="4ad40-131">If you forget tooconfigure hello kernel in hello first cell, you can use hello `%%configure` with hello `-f` parameter, but that will restart hello session and all progress will be lost.</span></span>

    | <span data-ttu-id="4ad40-132">Versão do HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ad40-132">HDInsight version</span></span> | <span data-ttu-id="4ad40-133">Command</span><span class="sxs-lookup"><span data-stu-id="4ad40-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="4ad40-134">Para HDInsight 3.3 e HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="4ad40-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="4ad40-135">Para HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="4ad40-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="4ad40-136">trecho de saudação acima espera Olá maven coordenadas para o pacote de saudação externo no repositório Central Maven.</span><span class="sxs-lookup"><span data-stu-id="4ad40-136">hello snippet above expects hello maven coordinates for hello external package in Maven Central Repository.</span></span> <span data-ttu-id="4ad40-137">Neste trecho, `com.databricks:spark-csv_2.10:1.4.0` é coordenada maven Olá **spark csv** pacote.</span><span class="sxs-lookup"><span data-stu-id="4ad40-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is hello maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="4ad40-138">Aqui está como você constrói Olá coordenadas de um pacote.</span><span class="sxs-lookup"><span data-stu-id="4ad40-138">Here's how you construct hello coordinates for a package.</span></span>
   
    <span data-ttu-id="4ad40-139">a.</span><span class="sxs-lookup"><span data-stu-id="4ad40-139">a.</span></span> <span data-ttu-id="4ad40-140">Localize o pacote de saudação em Olá Repositório Maven.</span><span class="sxs-lookup"><span data-stu-id="4ad40-140">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="4ad40-141">Para este tutorial, usamos [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="4ad40-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="4ad40-142">b.</span><span class="sxs-lookup"><span data-stu-id="4ad40-142">b.</span></span> <span data-ttu-id="4ad40-143">Do repositório de saudação reunir os valores hello para **GroupId**, **ArtifactId**, e **versão**.</span><span class="sxs-lookup"><span data-stu-id="4ad40-143">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="4ad40-144">Verifique se você coletar os valores hello correspondem seu cluster.</span><span class="sxs-lookup"><span data-stu-id="4ad40-144">Make sure that hello values you gather match your cluster.</span></span> <span data-ttu-id="4ad40-145">Nesse caso, estamos usando um pacote de Spark 1.4.0 e Scala 2.10, mas talvez seja necessário tooselect diferentes versões de versão apropriada Olá Scala ou Spark no cluster.</span><span class="sxs-lookup"><span data-stu-id="4ad40-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need tooselect different versions for hello appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="4ad40-146">Você pode descobrir Olá Scala versão no cluster executando `scala.util.Properties.versionString` no kernel do Spark Jupyter hello ou em envio Spark.</span><span class="sxs-lookup"><span data-stu-id="4ad40-146">You can find out hello Scala version on your cluster by running `scala.util.Properties.versionString` on hello Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="4ad40-147">Você pode descobrir Olá Spark versão no cluster executando `sc.version` em blocos de anotações do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="4ad40-147">You can find out hello Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="4ad40-148">![Usar pacotes externos com blocos de anotações do Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Usar pacotes externos com blocos de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="4ad40-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="4ad40-149">c.</span><span class="sxs-lookup"><span data-stu-id="4ad40-149">c.</span></span> <span data-ttu-id="4ad40-150">Concatenar valores hello três, separados por dois-pontos (**:**).</span><span class="sxs-lookup"><span data-stu-id="4ad40-150">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="4ad40-151">Execute a célula de código Olá com hello `%%configure` mágica.</span><span class="sxs-lookup"><span data-stu-id="4ad40-151">Run hello code cell with hello `%%configure` magic.</span></span> <span data-ttu-id="4ad40-152">Isso configurará Olá subjacente Livy sessão toouse Olá pacote fornecido.</span><span class="sxs-lookup"><span data-stu-id="4ad40-152">This will configure hello underlying Livy session toouse hello package you provided.</span></span> <span data-ttu-id="4ad40-153">Nas células de subsequentes Olá no bloco de anotações Olá, agora você pode usar o pacote de saudação, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4ad40-153">In hello subsequent cells in hello notebook, you can now use hello package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="4ad40-154">Você pode executar trechos Olá, como mostrado abaixo, tooview hello dados de dataframe de saudação você criou na etapa anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="4ad40-154">You can then run hello snippets, like shown below, tooview hello data from hello dataframe you created in hello previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="4ad40-155"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="4ad40-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="4ad40-156">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ad40-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="4ad40-157">Cenários</span><span class="sxs-lookup"><span data-stu-id="4ad40-157">Scenarios</span></span>
* [<span data-ttu-id="4ad40-158">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="4ad40-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="4ad40-159">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="4ad40-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="4ad40-160">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="4ad40-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="4ad40-161">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="4ad40-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="4ad40-162">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ad40-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="4ad40-163">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="4ad40-163">Create and run applications</span></span>
* [<span data-ttu-id="4ad40-164">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="4ad40-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="4ad40-165">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="4ad40-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="4ad40-166">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="4ad40-166">Tools and extensions</span></span>

* [<span data-ttu-id="4ad40-167">Usar pacotes Python externos com notebooks Jupyter em clusters do Apache Spark no HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="4ad40-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="4ad40-168">Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos</span><span class="sxs-lookup"><span data-stu-id="4ad40-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="4ad40-169">Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente</span><span class="sxs-lookup"><span data-stu-id="4ad40-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="4ad40-170">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ad40-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="4ad40-171">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ad40-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="4ad40-172">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="4ad40-172">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="4ad40-173">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="4ad40-173">Manage resources</span></span>
* [<span data-ttu-id="4ad40-174">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="4ad40-174">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="4ad40-175">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ad40-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

