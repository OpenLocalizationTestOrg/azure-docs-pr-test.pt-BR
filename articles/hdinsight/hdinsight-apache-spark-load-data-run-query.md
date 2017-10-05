---
title: Executar consultas interativas em um cluster HDInsight Spark do Azure | Microsoft Docs
description: "Guia de início rápido sobre como criar um cluster do Apache Spark no HDInsight."
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
ms.openlocfilehash: ada1c3d1482c68834dbbf5eabbd045a7e0c01f9f
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="ad00e-104">Executar consultas interativas em um cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="ad00e-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="ad00e-105">Neste artigo, você pode usar um bloco de anotações do Jupyter para executar consultas interativas do Spark SQL com relação a um cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="ad00e-105">In this article, you use a Jupyter notebook to run interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="ad00e-106">O bloco de anotações do Jupyter é um aplicativo baseado em navegador que estende a experiência interativa baseada em console para a Web.</span><span class="sxs-lookup"><span data-stu-id="ad00e-106">Jupyter notebook is a browser-based application that extends the console-based interactive experience to the Web.</span></span> <span data-ttu-id="ad00e-107">Para obter mais informações, consulte [O bloco de anotações do Jupyter](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span><span class="sxs-lookup"><span data-stu-id="ad00e-107">For more information, see [The Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="ad00e-108">Para este tutorial, você deve usar o kernel **PySpark** do bloco de anotações do Jupyter para executar uma consulta SQL Spark interativa.</span><span class="sxs-lookup"><span data-stu-id="ad00e-108">For this tutorial, you use the **PySpark** kernel in the Jupyter notebook to run an interactive Spark SQL query.</span></span> <span data-ttu-id="ad00e-109">Blocos de anotações do Jupyter em de clusters HDInsight também dão suporte a dois outros kernels – **PySpark3** e **Spark**.</span><span class="sxs-lookup"><span data-stu-id="ad00e-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="ad00e-110">Para saber mais sobre os três kernels e os benefícios de usar o **PySpark**, consulte [Usar kernels de blocos de anotações do Jupyter com clusters do Apache Spark no HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="ad00e-110">For more information about the kernels, and the benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad00e-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ad00e-111">Prerequisites</span></span>

* <span data-ttu-id="ad00e-112">**Um cluster HDInsight Spark do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ad00e-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="ad00e-113">Para obter instruções, consulte [Criar um cluster do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="ad00e-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-to-run-interactive-queries"></a><span data-ttu-id="ad00e-114">Criar um bloco de anotações do Jupyter para executar consultas interativas</span><span class="sxs-lookup"><span data-stu-id="ad00e-114">Create a Jupyter notebook to run interactive queries</span></span>

<span data-ttu-id="ad00e-115">Para executar consultas, usamos dados de exemplo que estão disponíveis por padrão no armazenamento associado ao cluster.</span><span class="sxs-lookup"><span data-stu-id="ad00e-115">To run queries, we use sample data that is by default available in the storage associated with the cluster.</span></span> <span data-ttu-id="ad00e-116">No entanto, você deve primeiro carregar esses dados no Spark como um dataframe.</span><span class="sxs-lookup"><span data-stu-id="ad00e-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="ad00e-117">Quando tiver o dataframe, você poderá executar consultas nele usando o bloco de anotações do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="ad00e-117">Once you have the dataframe, you can run queries on it using the Jupyter notebook.</span></span> <span data-ttu-id="ad00e-118">Nesta seção, você vê como:</span><span class="sxs-lookup"><span data-stu-id="ad00e-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="ad00e-119">Registrar um conjunto de dados de exemplo como um dataframe do Spark.</span><span class="sxs-lookup"><span data-stu-id="ad00e-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="ad00e-120">Executar consultas no dataframe.</span><span class="sxs-lookup"><span data-stu-id="ad00e-120">Run queries on the dataframe.</span></span>

1. <span data-ttu-id="ad00e-121">Abra o [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ad00e-121">Open the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="ad00e-122">Se você tiver optado por fixar o cluster ao painel, clique no bloco do cluster no painel para iniciar a folha de cluster.</span><span class="sxs-lookup"><span data-stu-id="ad00e-122">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="ad00e-123">Se você não fixar o cluster ao painel, no painel esquerdo, clique em **Clusters HDInsight** e clique no cluster que você criou.</span><span class="sxs-lookup"><span data-stu-id="ad00e-123">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="ad00e-124">Em **Links rápidos**, clique em **Painéis de cluster**e, em seguida, clique em **Anotações do Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="ad00e-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="ad00e-125">Se você receber uma solicitação, insira as credenciais de administrador para o cluster.</span><span class="sxs-lookup"><span data-stu-id="ad00e-125">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="ad00e-126">![Abrir um bloco de anotações Jupyter para executar uma consulta interativa SQL do Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Abrir um bloco de anotações Jupyter para executar uma consulta interativa SQL do Spark")</span><span class="sxs-lookup"><span data-stu-id="ad00e-126">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="ad00e-127">Você também pode acessar o bloco de anotações Jupyter de seu cluster abrindo a seguinte URL no navegador.</span><span class="sxs-lookup"><span data-stu-id="ad00e-127">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="ad00e-128">Substitua **CLUSTERNAME** pelo nome do cluster:</span><span class="sxs-lookup"><span data-stu-id="ad00e-128">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="ad00e-129">Crie um notebook.</span><span class="sxs-lookup"><span data-stu-id="ad00e-129">Create a notebook.</span></span> <span data-ttu-id="ad00e-130">Clique em **Novo** e em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="ad00e-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="ad00e-131">![Criar um bloco de anotações Jupyter para executar consulta interativa SQL do Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Criar um bloco de anotações Jupyter para executar uma consulta interativa SQL do Spark")</span><span class="sxs-lookup"><span data-stu-id="ad00e-131">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="ad00e-132">Um novo bloco de anotações é criado e aberto com o nome Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="ad00e-132">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="ad00e-133">Clique no nome do bloco de anotações na parte superior e, se desejar, digite um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="ad00e-133">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="ad00e-134">![Forneça um nome para o bloco de anotações Jupyter para executar a consulta interativa Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Forneça um nome para o bloco de anotações Jupyter para executar a consulta interativa Spark")</span><span class="sxs-lookup"><span data-stu-id="ad00e-134">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5. <span data-ttu-id="ad00e-135">Cole o código a seguir em uma célula vazia e pressione **SHIFT + ENTER** para executar o código.</span><span class="sxs-lookup"><span data-stu-id="ad00e-135">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="ad00e-136">O código importa os tipos obrigatórios necessários para este cenário:</span><span class="sxs-lookup"><span data-stu-id="ad00e-136">The code imports the types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="ad00e-137">Por ter criado um notebook usando o kernel PySpark, não será necessário criar nenhum contexto explicitamente.</span><span class="sxs-lookup"><span data-stu-id="ad00e-137">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="ad00e-138">Os contextos do Spark e do Hive são criados automaticamente para você ao executar a primeira célula do código.</span><span class="sxs-lookup"><span data-stu-id="ad00e-138">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span>

    <span data-ttu-id="ad00e-139">![Status de consulta interativa SQL Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status de consulta interativa SQL Spark")</span><span class="sxs-lookup"><span data-stu-id="ad00e-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="ad00e-140">Toda vez que você executar uma consulta interativa no Jupyter, o título da janela do navegador da Web mostrará um status **(Ocupado)** com o título do bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="ad00e-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="ad00e-141">Você também verá um círculo sólido ao lado do texto **PySpark** no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="ad00e-141">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="ad00e-142">Após a conclusão do trabalho, isso será alterado para um círculo vazio.</span><span class="sxs-lookup"><span data-stu-id="ad00e-142">After the job is completed, it changes to a hollow circle.</span></span>

6. <span data-ttu-id="ad00e-143">Antes de você carregar os dados em um cluster Spark, examinaremos um instantâneo dele.</span><span class="sxs-lookup"><span data-stu-id="ad00e-143">Before you load the data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="ad00e-144">Os dados de exemplo usados neste tutorial estão disponíveis como um arquivo CSV em todos os clusters HDInsight Spark em **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="ad00e-144">The sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="ad00e-145">Os dados capturam as variações de temperatura de um prédio.</span><span class="sxs-lookup"><span data-stu-id="ad00e-145">The data captures the temperature variations of a building.</span></span> <span data-ttu-id="ad00e-146">Aqui estão as primeiras linhas dos dados.</span><span class="sxs-lookup"><span data-stu-id="ad00e-146">Here are the first few rows of the data.</span></span>

    <span data-ttu-id="ad00e-147">![Instantâneo de dados para consulta SQL interativa do Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Instantâneo de dados para consulta SQL interativa do Spark")</span><span class="sxs-lookup"><span data-stu-id="ad00e-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="ad00e-148">Crie um dataframe e uma tabela temporária (**hvac**) executando o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="ad00e-148">Create a dataframe and a temporary table (**hvac**) by running the following code.</span></span> <span data-ttu-id="ad00e-149">Para este tutorial, nós não criamos todas as colunas na tabela temporária em comparação com as colunas nos dados brutos de CSV.</span><span class="sxs-lookup"><span data-stu-id="ad00e-149">For this tutorial, we do not create all the columns in the temporary table as compared to the columns in the raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse the data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer the schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="ad00e-150">Uma vez criada a tabela, execute a consulta interativa nos dados, use o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="ad00e-150">Once the table is created, run interactive query on the data, use the following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="ad00e-151">Como está usando um kernel PySpark, agora você pode executar diretamente uma consulta interativa SQL na tabela temporária **hvac** que você criou usando a palavra mágica `%%sql`.</span><span class="sxs-lookup"><span data-stu-id="ad00e-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on the temporary table **hvac** that you created by using the `%%sql` magic.</span></span> <span data-ttu-id="ad00e-152">Para saber mais sobre a palavra mágica `%%sql`, e outras palavras mágicas disponíveis com o kernel PySpark, confira [Kernels disponíveis em notebooks Jupyter com clusters HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="ad00e-152">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="ad00e-153">A saída tabular a seguir é exibida por padrão.</span><span class="sxs-lookup"><span data-stu-id="ad00e-153">The following tabular output is displayed by default.</span></span>

     <span data-ttu-id="ad00e-154">![Tabela de saída do resultado da consulta interativa Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabela de saída do resultado da consulta interativa Spark")</span><span class="sxs-lookup"><span data-stu-id="ad00e-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="ad00e-155">Você também pode ver os resultados em outras visualizações.</span><span class="sxs-lookup"><span data-stu-id="ad00e-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="ad00e-156">Por exemplo, um gráfico de área para a mesma saída seria semelhante ao seguinte.</span><span class="sxs-lookup"><span data-stu-id="ad00e-156">For example, an area graph for the same output would look like the following.</span></span>

    <span data-ttu-id="ad00e-157">![Gráfico de área de resultado de consulta interativa do Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Gráfico de área de resultado de consulta interativa do Spark")</span><span class="sxs-lookup"><span data-stu-id="ad00e-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="ad00e-158">Depois de concluir a execução do aplicativo, encerre o notebook para liberar os recursos.</span><span class="sxs-lookup"><span data-stu-id="ad00e-158">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="ad00e-159">Para isso, no menu **Arquivo** do bloco de anotações, clique em **Fechar e Interromper**.</span><span class="sxs-lookup"><span data-stu-id="ad00e-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="ad00e-160">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="ad00e-160">Next step</span></span>

<span data-ttu-id="ad00e-161">Neste artigo, você aprendeu como executar consultas interativas no Spark usando o bloco de anotações do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="ad00e-161">In this article you learned how to run interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="ad00e-162">Avance para o próximo artigo para ver como os dados que você registrou no Spark podem ser removidos em uma ferramenta de análise de BI, assim como Power BI e Tableau.</span><span class="sxs-lookup"><span data-stu-id="ad00e-162">Advance to the next article to see how the data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="ad00e-163">Spark BI usando ferramentas de visualização de dados com o Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ad00e-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




