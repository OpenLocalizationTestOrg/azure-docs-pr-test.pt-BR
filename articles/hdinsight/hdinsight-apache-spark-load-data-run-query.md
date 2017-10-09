---
title: aaaRun a consultas interativas em um cluster Spark no HDInsight | Microsoft Docs
description: "Início rápido do HDInsight Spark no como cluster de toocreate um Apache Spark no HDInsight."
keywords: "início rápido do spark,spark interativo,consulta interativa,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="7b174-104">Executar consultas interativas em um cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="7b174-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="7b174-105">Neste artigo, você deve usar um Jupyter notebook toorun interativo Spark consultas SQL em relação a um cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="7b174-105">In this article, you use a Jupyter notebook toorun interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="7b174-106">Anotações do Jupyter é um aplicativo baseado em navegador que estende Olá baseado em console interativo experiência toohello da Web.</span><span class="sxs-lookup"><span data-stu-id="7b174-106">Jupyter notebook is a browser-based application that extends hello console-based interactive experience toohello Web.</span></span> <span data-ttu-id="7b174-107">Para obter mais informações, consulte [de anotações do Jupyter Olá](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span><span class="sxs-lookup"><span data-stu-id="7b174-107">For more information, see [hello Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="7b174-108">Para este tutorial, você usar Olá **PySpark** kernel no toorun de notebook Jupyter de saudação uma consulta SQL Spark interativa.</span><span class="sxs-lookup"><span data-stu-id="7b174-108">For this tutorial, you use hello **PySpark** kernel in hello Jupyter notebook toorun an interactive Spark SQL query.</span></span> <span data-ttu-id="7b174-109">Blocos de anotações do Jupyter em de clusters HDInsight também dão suporte a dois outros kernels – **PySpark3** e **Spark**.</span><span class="sxs-lookup"><span data-stu-id="7b174-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="7b174-110">Para obter mais informações sobre kernels hello e benefícios de saudação do uso de **PySpark**, consulte [clusters kernels de notebook Jupyter de uso com o Apache Spark no HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="7b174-110">For more information about hello kernels, and hello benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b174-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7b174-111">Prerequisites</span></span>

* <span data-ttu-id="7b174-112">**Um cluster HDInsight Spark do Azure**.</span><span class="sxs-lookup"><span data-stu-id="7b174-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="7b174-113">Para obter instruções, consulte [Criar um cluster do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="7b174-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a><span data-ttu-id="7b174-114">Criar um bloco de anotações do Jupyter consultas interativas toorun</span><span class="sxs-lookup"><span data-stu-id="7b174-114">Create a Jupyter notebook toorun interactive queries</span></span>

<span data-ttu-id="7b174-115">consultas de toorun, usamos os dados de exemplo que está disponível no armazenamento de saudação associado cluster Olá por padrão.</span><span class="sxs-lookup"><span data-stu-id="7b174-115">toorun queries, we use sample data that is by default available in hello storage associated with hello cluster.</span></span> <span data-ttu-id="7b174-116">No entanto, você deve primeiro carregar esses dados no Spark como um dataframe.</span><span class="sxs-lookup"><span data-stu-id="7b174-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="7b174-117">Uma vez que o dataframe hello, você pode executar consultas nele usando anotações do Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="7b174-117">Once you have hello dataframe, you can run queries on it using hello Jupyter notebook.</span></span> <span data-ttu-id="7b174-118">Nesta seção, você vê como:</span><span class="sxs-lookup"><span data-stu-id="7b174-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="7b174-119">Registrar um conjunto de dados de exemplo como um dataframe do Spark.</span><span class="sxs-lookup"><span data-stu-id="7b174-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="7b174-120">Execute consultas no dataframe de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b174-120">Run queries on hello dataframe.</span></span>

1. <span data-ttu-id="7b174-121">Olá abrir [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7b174-121">Open hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7b174-122">Se você optou por painel de toohello toopin Olá cluster, clique em Olá cluster lado a lado na folha de cluster Olá painel toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="7b174-122">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="7b174-123">Se você não fixar Olá cluster toohello painel de controle, no painel esquerdo do hello, clique em **clusters HDInsight**e, em seguida, clique em cluster Olá que você criou.</span><span class="sxs-lookup"><span data-stu-id="7b174-123">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="7b174-124">Em **Links rápidos**, clique em **Painéis de cluster**e, em seguida, clique em **Anotações do Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="7b174-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="7b174-125">Se solicitado, insira as credenciais de administrador de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7b174-125">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="7b174-126">![Abra Jupyter notebook toorun Spark SQL consulta interativo](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "consulta toorun Spark SQL interativo notebook Jupyter aberto")</span><span class="sxs-lookup"><span data-stu-id="7b174-126">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="7b174-127">Você também pode acessar as anotações do Jupyter Olá para o cluster por Olá abrir URL a seguir em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="7b174-127">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="7b174-128">Substituir **CLUSTERNAME** com nome de saudação do cluster:</span><span class="sxs-lookup"><span data-stu-id="7b174-128">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="7b174-129">Crie um notebook.</span><span class="sxs-lookup"><span data-stu-id="7b174-129">Create a notebook.</span></span> <span data-ttu-id="7b174-130">Clique em **Novo** e em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="7b174-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="7b174-131">![Criar uma consulta SQL Spark interativa Jupyter notebook toorun](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "criar uma consulta Jupyter notebook toorun interativa Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="7b174-131">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="7b174-132">Um novo bloco de anotações é criado e aberto com o nome hello Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="7b174-132">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="7b174-133">Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável, se desejar.</span><span class="sxs-lookup"><span data-stu-id="7b174-133">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="7b174-134">![Forneça um nome para Olá Jupter notebook toorun Spark consulta interativo de](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "forneça um nome para Olá Jupter notebook toorun Spark consulta interativa do")</span><span class="sxs-lookup"><span data-stu-id="7b174-134">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5. <span data-ttu-id="7b174-135">Colar Olá seguinte código em uma célula vazia e, em seguida, pressione **SHIFT + ENTER** toorun código de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b174-135">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="7b174-136">código de saudação importa tipos de saudação requeridos para este cenário:</span><span class="sxs-lookup"><span data-stu-id="7b174-136">hello code imports hello types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="7b174-137">Como você criou um bloco de anotações com o hello PySpark kernel, não é necessário toocreate qualquer contextos explicitamente.</span><span class="sxs-lookup"><span data-stu-id="7b174-137">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="7b174-138">Olá Spark e Hive contextos são criados automaticamente para você quando você executar a primeira célula de código hello.</span><span class="sxs-lookup"><span data-stu-id="7b174-138">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span>

    <span data-ttu-id="7b174-139">![Status de consulta interativa SQL Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status de consulta interativa SQL Spark")</span><span class="sxs-lookup"><span data-stu-id="7b174-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="7b174-140">Sempre que você executa uma consulta interativa em Jupyter, o título da janela navegador web mostra um **(ocupada)** status junto com o título do bloco de anotações de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b174-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="7b174-141">Você também verá um toohello próximo do círculo sólido **PySpark** texto no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b174-141">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="7b174-142">Após o trabalho hello, ele altera o círculo vazio tooa.</span><span class="sxs-lookup"><span data-stu-id="7b174-142">After hello job is completed, it changes tooa hollow circle.</span></span>

6. <span data-ttu-id="7b174-143">Antes de carregar dados saudação em um cluster Spark, vamos examinar um instantâneo dele.</span><span class="sxs-lookup"><span data-stu-id="7b174-143">Before you load hello data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="7b174-144">Olá dados de exemplo usados neste tutorial estão disponíveis como um arquivo CSV em todos os clusters de HDInsight Spark no **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="7b174-144">hello sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="7b174-145">dados de saudação captura variações de temperatura de saudação do prédio.</span><span class="sxs-lookup"><span data-stu-id="7b174-145">hello data captures hello temperature variations of a building.</span></span> <span data-ttu-id="7b174-146">Aqui está Olá primeiras linhas de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b174-146">Here are hello first few rows of hello data.</span></span>

    <span data-ttu-id="7b174-147">![Instantâneo de dados para consulta SQL interativa do Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Instantâneo de dados para consulta SQL interativa do Spark")</span><span class="sxs-lookup"><span data-stu-id="7b174-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="7b174-148">Criar um dataframe e uma tabela temporária (**hvac**) executando Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="7b174-148">Create a dataframe and a temporary table (**hvac**) by running hello following code.</span></span> <span data-ttu-id="7b174-149">Para este tutorial, não criamos todas as colunas de saudação na tabela temporária hello como colunas de toohello comparados em dados brutos de CSV hello.</span><span class="sxs-lookup"><span data-stu-id="7b174-149">For this tutorial, we do not create all hello columns in hello temporary table as compared toohello columns in hello raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="7b174-150">Depois de criar tabela hello, executar consulta interativa nos dados hello, use Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="7b174-150">Once hello table is created, run interactive query on hello data, use hello following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="7b174-151">Como você está usando um kernel PySpark, agora você pode diretamente executar uma consulta SQL interativa na tabela temporária Olá **hvac** que você criou usando Olá `%%sql` mágica.</span><span class="sxs-lookup"><span data-stu-id="7b174-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on hello temporary table **hvac** that you created by using hello `%%sql` magic.</span></span> <span data-ttu-id="7b174-152">Para obter mais informações sobre Olá `%%sql` mágico e outros magics disponíveis com o kernel do PySpark hello, consulte [Kernels disponíveis em blocos de anotações do Jupyter com clusters HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="7b174-152">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="7b174-153">Olá após a saída tabular é exibido por padrão.</span><span class="sxs-lookup"><span data-stu-id="7b174-153">hello following tabular output is displayed by default.</span></span>

     <span data-ttu-id="7b174-154">![Tabela de saída do resultado da consulta interativa Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabela de saída do resultado da consulta interativa Spark")</span><span class="sxs-lookup"><span data-stu-id="7b174-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="7b174-155">Você também pode ver os resultados de saudação em outras visualizações também.</span><span class="sxs-lookup"><span data-stu-id="7b174-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="7b174-156">Por exemplo, um gráfico de área para Olá a mesma saída seria semelhante a seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="7b174-156">For example, an area graph for hello same output would look like hello following.</span></span>

    <span data-ttu-id="7b174-157">![Gráfico de área de resultado de consulta interativa do Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Gráfico de área de resultado de consulta interativa do Spark")</span><span class="sxs-lookup"><span data-stu-id="7b174-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="7b174-158">Desliga os recursos de cluster de saudação do hello notebook toorelease depois de terminar de executar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7b174-158">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="7b174-159">toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**.</span><span class="sxs-lookup"><span data-stu-id="7b174-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="7b174-160">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="7b174-160">Next step</span></span>

<span data-ttu-id="7b174-161">Neste artigo, você aprendeu como toorun a consultas interativas no Spark usando anotações do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="7b174-161">In this article you learned how toorun interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="7b174-162">Avançar toohello próximo artigo toosee como dados de saudação registrado no Spark podem ser removidos em uma ferramenta de análise de BI, como o Power BI e Tableau.</span><span class="sxs-lookup"><span data-stu-id="7b174-162">Advance toohello next article toosee how hello data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="7b174-163">Spark BI usando ferramentas de visualização de dados com o Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b174-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




