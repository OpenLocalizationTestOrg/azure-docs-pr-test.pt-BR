---
title: "Spark BI usando ferramentas de visualização de dados no Azure HDInsight | Microsoft Docs"
description: "Usar ferramentas de visualização de dados para análise usando Apache Spark BI em clusters HDInsight"
keywords: "apache spark bi, spark bi, visualização de dados spark, spark business intelligence"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 49dd161049ac442081fe6d26cf8bd3a56a2e0687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a><span data-ttu-id="e1b74-104">Apache Spark BI usando ferramentas de visualização de dados com o Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1b74-104">Apache Spark BI using data visualization tools with Azure HDInsight</span></span>

<span data-ttu-id="e1b74-105">Saiba como usar ferramentas de visualização de dados, como o Power BI e o Tableau para analisar um conjunto de dados brutos de exemplo usando o Apache Spark BI em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1b74-105">Learn how to use data visualization tools such as Power BI and Tableau to analyze a raw sample data set using Apache Spark BI on HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="e1b74-106">A conectividade com as ferramentas BI descritas neste artigo não tem suporte no Spark 2.1 no modo Preview do Azure HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="e1b74-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="e1b74-107">Somente as versões 1.6 e 2.0 do Spark (HDInsight 3.4 e 3.5, respectivamente) têm suporte.</span><span class="sxs-lookup"><span data-stu-id="e1b74-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="e1b74-108">Este tutorial também está disponível como um notebook Jupyter em um cluster do Spark HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1b74-108">This tutorial is also available as a Jupyter notebook on an HDInsight Spark cluster.</span></span> <span data-ttu-id="e1b74-109">A experiência de bloco de anotações permite executar os trechos de código Python no próprio bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="e1b74-109">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="e1b74-110">Para executar o tutorial em um bloco de anotações, crie um cluster Spark, inicie um bloco de anotações do Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`) e execute o bloco de anotações **Usar ferramentas de BI com Apache Spark no HDInsight.ipynb** na pasta **Python**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-110">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under the **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1b74-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e1b74-111">Prerequisites</span></span>

* <span data-ttu-id="e1b74-112">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1b74-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e1b74-113">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e1b74-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <span data-ttu-id="e1b74-114"><a name="hivetable"></a>Preparar dados para visualização de dados o Spark</span><span class="sxs-lookup"><span data-stu-id="e1b74-114"><a name="hivetable"></a>Prepare data for Spark data visualization</span></span>

<span data-ttu-id="e1b74-115">Nesta seção, usamos o bloco de anotações do [Jupyter](https://jupyter.org) de um cluster Spark no HDInsight para executar trabalhos que processam os dados brutos de exemplo e os salvam como uma tabela.</span><span class="sxs-lookup"><span data-stu-id="e1b74-115">In this section, we use the [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster to run jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="e1b74-116">Os dados de exemplo são um arquivo .csv (hvac.csv) disponível em todos os clusters por padrão.</span><span class="sxs-lookup"><span data-stu-id="e1b74-116">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span> <span data-ttu-id="e1b74-117">Depois que os dados são salvos como uma tabela, na próxima seção, usamos ferramentas de BI para conectar à tabela e realizar visualizações de dados.</span><span class="sxs-lookup"><span data-stu-id="e1b74-117">Once your data is saved as a table, in the next section we use BI tools to connect to the table and perform data visualizations.</span></span>

> [!NOTE]
> <span data-ttu-id="e1b74-118">Se executar as etapas neste artigo depois de concluir as instruções em [Executar consultas interativas em um cluster HDInsight Spark](hdinsight-apache-spark-load-data-run-query.md), você poderá pular para a Etapa 8 abaixo.</span><span class="sxs-lookup"><span data-stu-id="e1b74-118">If you are performing the steps in this article after completing the instructions in [Run interactive queries on an HDInsight Spark cluster](hdinsight-apache-spark-load-data-run-query.md), you can skip to Step 8 below.</span></span>
>

1. <span data-ttu-id="e1b74-119">No [portal do Azure](https://portal.azure.com/), no quadro inicial, clique no bloco do cluster Spark (se você o tiver fixado no quadro inicial).</span><span class="sxs-lookup"><span data-stu-id="e1b74-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="e1b74-120">Você também pode navegar até o cluster em **Procurar Tudo** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="e1b74-121">Na folha do cluster Spark, clique em **Painel do Cluster** e em **Notebook Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="e1b74-122">Se você receber uma solicitação, insira as credenciais de administrador para o cluster.</span><span class="sxs-lookup"><span data-stu-id="e1b74-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e1b74-123">Você também pode acessar o Bloco de Notas Jupyter de seu cluster abrindo a seguinte URL no navegador.</span><span class="sxs-lookup"><span data-stu-id="e1b74-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="e1b74-124">Substitua **CLUSTERNAME** pelo nome do cluster:</span><span class="sxs-lookup"><span data-stu-id="e1b74-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="e1b74-125">Crie um notebook.</span><span class="sxs-lookup"><span data-stu-id="e1b74-125">Create a notebook.</span></span> <span data-ttu-id="e1b74-126">Clique em **Novo** e em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="e1b74-127">![Criar um notebook Jupyter para o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Criar um notebook Jupyter para o Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-127">![Create a Jupyter notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Create a Jupyter notebook for Apache Spark BI")</span></span>

4. <span data-ttu-id="e1b74-128">Um novo bloco de anotações é criado e aberto com o nome Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="e1b74-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="e1b74-129">Clique no nome do bloco de anotações na parte superior e digite um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="e1b74-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="e1b74-130">![Fornecer um nome para o notebook do Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Fornecer um nome para o notebook do Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-130">![Provide a name for the notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Provide a name for the notebook for Apache Spark BI")</span></span>

5. <span data-ttu-id="e1b74-131">Por ter criado um notebook usando o kernel PySpark, não será necessário criar nenhum contexto explicitamente.</span><span class="sxs-lookup"><span data-stu-id="e1b74-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="e1b74-132">Os contextos do Spark e do Hive são criados automaticamente para você ao executar a primeira célula do código.</span><span class="sxs-lookup"><span data-stu-id="e1b74-132">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="e1b74-133">Você pode começar importando os tipos obrigatórios para este cenário.</span><span class="sxs-lookup"><span data-stu-id="e1b74-133">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="e1b74-134">Para fazer isso, coloque o cursor na célula e pressione **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-134">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="e1b74-135">Carregar dados de exemplo em uma tabela temporária.</span><span class="sxs-lookup"><span data-stu-id="e1b74-135">Load sample data into a temporary table.</span></span> <span data-ttu-id="e1b74-136">Quando você cria um cluster Spark no HDInsight, o arquivo de dados de exemplo, **hvac.csv**, é copiado para a conta de armazenamento associada em **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-136">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="e1b74-137">Em uma célula vazia, cole o trecho a seguir e pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-137">In an empty cell, paste the following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="e1b74-138">Esse trecho registra os dados em uma tabela chamada **hvac**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-138">This snippet registers the data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. <span data-ttu-id="e1b74-139">Verifique se a tabela foi criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="e1b74-139">Verify that the table was successfully created.</span></span> <span data-ttu-id="e1b74-140">Você pode usar a mágica do `%%sql` para executar as consultas do Hive diretamente.</span><span class="sxs-lookup"><span data-stu-id="e1b74-140">You can use the `%%sql` magic to run Hive queries directly.</span></span> <span data-ttu-id="e1b74-141">Para saber mais sobre a palavra mágica `%%sql`, e outras palavras mágicas disponíveis com o kernel PySpark, confira [Kernels disponíveis em notebooks Jupyter com clusters HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="e1b74-141">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="e1b74-142">Você vê uma saída como a mostrada abaixo:</span><span class="sxs-lookup"><span data-stu-id="e1b74-142">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="e1b74-143">Somente as tabelas que têm falso na coluna **isTemporary** são tabelas hive que ficam armazenadas no metastore e podem ser acessadas por meio das ferramentas de BI.</span><span class="sxs-lookup"><span data-stu-id="e1b74-143">Only the tables that have false under the **isTemporary** column are hive tables that are stored in the metastore and can be accessed from the BI tools.</span></span> <span data-ttu-id="e1b74-144">Neste tutorial, vamos nos conectar à tabela **hvac** criada.</span><span class="sxs-lookup"><span data-stu-id="e1b74-144">In this tutorial, we connect to the **hvac** table we created.</span></span>

8. <span data-ttu-id="e1b74-145">Verifique se a tabela contém os dados pretendidos.</span><span class="sxs-lookup"><span data-stu-id="e1b74-145">Verify that the table contains the intended data.</span></span> <span data-ttu-id="e1b74-146">Em uma célula vazia no bloco de anotações, copie o seguinte trecho e pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-146">In an empty cell in the notebook, copy the following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="e1b74-147">Feche o bloco de anotações para liberar os recursos.</span><span class="sxs-lookup"><span data-stu-id="e1b74-147">Shut down the notebook to release the resources.</span></span> <span data-ttu-id="e1b74-148">Para isso, no menu **Arquivo** do bloco de anotações, clique em **Fechar e Interromper**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-148">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <span data-ttu-id="e1b74-149"><a name="powerbi"></a>Usar o Power BI para visualização de dados do Spark</span><span class="sxs-lookup"><span data-stu-id="e1b74-149"><a name="powerbi"></a>Use Power BI for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="e1b74-150">Esta seção é aplicável somente ao Spark 1.6 no HDInsight 3.4 e ao Spark 2.0 no HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="e1b74-150">This section is applicable only for Spark 1.6 on HDInsight 3.4 and Spark 2.0 on HDInsight 3.5.</span></span>
>
>

<span data-ttu-id="e1b74-151">Depois de salvar os dados como uma tabela, você poderá usar o Power BI para conectar aos dados e visualizá-los para criar relatórios, painéis, etc.</span><span class="sxs-lookup"><span data-stu-id="e1b74-151">Once you have saved the data as a table, you can use Power BI to connect to the data and visualize it to create reports, dashboards, etc.</span></span>

1. <span data-ttu-id="e1b74-152">Verifique se que você tem acesso ao Power BI.</span><span class="sxs-lookup"><span data-stu-id="e1b74-152">Make sure you have access to Power BI.</span></span> <span data-ttu-id="e1b74-153">Você pode obter uma assinatura gratuita de visualização do Power BI em [http://www.powerbi.com/](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="e1b74-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="e1b74-154">Entre no [Power BI](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="e1b74-154">Sign in to [Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="e1b74-155">Na parte inferior do painel esquerdo, clique em **Obter Dados**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-155">From the bottom of the left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="e1b74-156">Na página **Obter Dados**, em **Importar ou Conectar-se a Dados**, para **Bancos de Dados**, clique em **Obter**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-156">On the **Get Data** page, under **Import or Connect to Data**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="e1b74-157">![Colocar dados no Power BI para o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Colocar dados no Power BI para o Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-157">![Get data into Power BI for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI for Apache Spark BI")</span></span>

5. <span data-ttu-id="e1b74-158">Na próxima tela, clique em **Spark no Azure HDInsight** e em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-158">On the next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="e1b74-159">Quando solicitado, insira a URL do cluster (`mysparkcluster.azurehdinsight.net`) e as credenciais para se conectar a ele</span><span class="sxs-lookup"><span data-stu-id="e1b74-159">When prompted, enter the cluster URL (`mysparkcluster.azurehdinsight.net`) and the credentials to connect to the cluster.</span></span>

    <span data-ttu-id="e1b74-160">![Conectar-se ao Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Conectar-se ao Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-160">![Connect to Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connect to Apache Spark BI")</span></span>

    <span data-ttu-id="e1b74-161">Depois que a conexão é estabelecida, o Power BI inicia a importação de dados do cluster Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1b74-161">After the connection is established, Power BI starts importing data from the Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="e1b74-162">O Power BI importa os dados e adiciona um conjunto de dados **Spark** sob o título **Conjuntos de dados**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-162">Power BI imports the data and adds a **Spark** dataset under the **Datasets** heading.</span></span> <span data-ttu-id="e1b74-163">Clique no conjunto de dados para abrir uma nova planilha e visualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="e1b74-163">Click the data set to open a new worksheet to visualize the data.</span></span> <span data-ttu-id="e1b74-164">Também é possível salvar a planilha como um relatório.</span><span class="sxs-lookup"><span data-stu-id="e1b74-164">You can also save the worksheet as a report.</span></span> <span data-ttu-id="e1b74-165">Para salvar uma planilha, no menu **Arquivo**, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-165">To save a worksheet, from the **File** menu, click **Save**.</span></span>

    <span data-ttu-id="e1b74-166">![Bloco do Apache Spark BI no painel do Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Bloco do Apache Spark BI no painel do Power BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-166">![Apache Spark BI tile on Power BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="e1b74-167">Observe que a lista **Campos**, à direita, lista a tabela **hvac** que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e1b74-167">Notice that the **Fields** list on the right lists the **hvac** table you created earlier.</span></span> <span data-ttu-id="e1b74-168">Expanda a tabela para ver seus campos, conforme você definiu anteriormente no bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="e1b74-168">Expand the table to see the fields in the table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="e1b74-169">![Listar tabelas no painel do Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Listar tabelas no painel do Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-169">![List tables on Apache Spark BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "List tables on Apache Spark BI dashboard")</span></span>

8. <span data-ttu-id="e1b74-170">Crie uma visualização para mostrar a variação entre a temperatura almejada e a temperatura real para cada edifício.</span><span class="sxs-lookup"><span data-stu-id="e1b74-170">Build a visualization to show the variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="e1b74-171">Para visualizar seus dados, selecione **Gráfico de Áreas** (mostrado na caixa vermelha).</span><span class="sxs-lookup"><span data-stu-id="e1b74-171">To visualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="e1b74-172">Para definir o eixo, arraste e solte o campo **BuildingID** em **Eixo** e os campos **ActualTemp**/**TargetTemp** em **Valor**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-172">To define the axis, drag-and-drop the **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="e1b74-173">![Criar visualizações de dados Spark usando o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Criar visualizações de dados Spark usando o Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-173">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

9. <span data-ttu-id="e1b74-174">Por padrão, a visualização mostra a soma de **ActualTemp** e **TargetTemp**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-174">By default the visualization shows the sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="e1b74-175">Para os campos, na lista suspensa, selecione **Média** para obter uma média das temperaturas almejada e real para ambos os prédios.</span><span class="sxs-lookup"><span data-stu-id="e1b74-175">For both the fields, from the drop-down, select **Average** to get an average of actual and target temperatures for both buildings.</span></span>

    <span data-ttu-id="e1b74-176">![Criar visualizações de dados Spark usando o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Criar visualizações de dados Spark usando o Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-176">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

10. <span data-ttu-id="e1b74-177">A visualização de dados deve ser semelhante à que aparece na captura de tela.</span><span class="sxs-lookup"><span data-stu-id="e1b74-177">Your data visualization should be similar to the one in the screenshot.</span></span> <span data-ttu-id="e1b74-178">Mova o cursor sobre a visualização para obter dicas de ferramenta com dados relevantes.</span><span class="sxs-lookup"><span data-stu-id="e1b74-178">Move your cursor over the visualization to get tool tips with relevant data.</span></span>

    <span data-ttu-id="e1b74-179">![Criar visualizações de dados Spark usando o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Criar visualizações de dados Spark usando o Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-179">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

11. <span data-ttu-id="e1b74-180">Clique em **Salvar** no menu superior e forneça um nome de relatório.</span><span class="sxs-lookup"><span data-stu-id="e1b74-180">Click **Save** from the top menu and provide a report name.</span></span> <span data-ttu-id="e1b74-181">Você também pode fixar o visual.</span><span class="sxs-lookup"><span data-stu-id="e1b74-181">You can also pin the visual.</span></span> <span data-ttu-id="e1b74-182">Quando você fixa uma visualização, ela fica armazenada no painel para permitir o controle do valor mais recente rapidamente.</span><span class="sxs-lookup"><span data-stu-id="e1b74-182">When you pin a visualization, it is stored on your dashboard so you can track the latest value at a glance.</span></span>

   <span data-ttu-id="e1b74-183">Você pode adicionar quantas visualizações desejar para o mesmo conjunto de dados e fixá-las no painel para um instantâneo dos dados.</span><span class="sxs-lookup"><span data-stu-id="e1b74-183">You can add as many visualizations as you want for the same dataset and pin them to the dashboard for a snapshot of your data.</span></span> <span data-ttu-id="e1b74-184">Além disso, os clusters do Spark no HDInsight são conectados ao Power BI com conexão direta.</span><span class="sxs-lookup"><span data-stu-id="e1b74-184">Also, Spark clusters on HDInsight are connected to Power BI with direct connect.</span></span> <span data-ttu-id="e1b74-185">Isso faz com que o Power BI tenha sempre os dados mais atualizadas de seu cluster para que você não precise agendar atualizações para o conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="e1b74-185">This ensures that Power BI always has the most up-to-date data from your cluster so you do not need to schedule refreshes for the dataset.</span></span>

## <span data-ttu-id="e1b74-186"><a name="tableau"></a>Usar o Tableau Desktop para visualização de dados do Spark</span><span class="sxs-lookup"><span data-stu-id="e1b74-186"><a name="tableau"></a>Use Tableau Desktop for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="e1b74-187">Esta seção é aplicável somente para clusters do Spark 1.5.2 criados no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1b74-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="e1b74-188">Instale o [Tableau Desktop](http://www.tableau.com/products/desktop) no computador em que você está executando este tutorial do Apache Spark BI.</span><span class="sxs-lookup"><span data-stu-id="e1b74-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on the computer where you are running this Apache Spark BI tutorial.</span></span>

2. <span data-ttu-id="e1b74-189">Verifique se o computador também tem o driver ODBC do Microsoft Spark instalado.</span><span class="sxs-lookup"><span data-stu-id="e1b74-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="e1b74-190">Você pode instalar o driver clicando [aqui](http://go.microsoft.com/fwlink/?LinkId=616229).</span><span class="sxs-lookup"><span data-stu-id="e1b74-190">You can install the driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="e1b74-191">Inicie o Tableau Desktop.</span><span class="sxs-lookup"><span data-stu-id="e1b74-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="e1b74-192">No painel esquerdo, na lista de servidores aos quais se conectar, clique em **Spark SQL**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-192">In the left pane, from the list of server to connect to, click **Spark SQL**.</span></span> <span data-ttu-id="e1b74-193">Se Spark SQL não estiver listado por padrão no painel esquerdo, você poderá encontrá-lo ao clicar em **Mais Servidores**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-193">If Spark SQL is not listed by default in the left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="e1b74-194">Na caixa de diálogo de conexão do Spark SQL, forneça os valores conforme mostrado na captura de tela e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-194">In the Spark SQL connection dialog box, provide the values as shown in the screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="e1b74-195">![Conectar-se a um cluster do Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Conectar-se a um cluster do Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-195">![Connect to a cluster for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect to a cluster for Apache Spark BI")</span></span>

    <span data-ttu-id="e1b74-196">O menu suspenso de autenticação listará o **Serviço Microsoft Azure HDInsight** como uma opção somente se você tiver instalado o [Driver ODBC do Microsoft Spark](http://go.microsoft.com/fwlink/?LinkId=616229) no computador.</span><span class="sxs-lookup"><span data-stu-id="e1b74-196">The authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed the [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on the computer.</span></span>
3. <span data-ttu-id="e1b74-197">Na próxima tela, no menu suspenso **Esquema**, clique no ícone **Localizar** e clique em **padrão**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-197">On the next screen, from the **Schema** drop-down, click the **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="e1b74-198">![Localizar o esquema para o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Localizar o esquema para o Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-198">![Find schema for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")</span></span>
4. <span data-ttu-id="e1b74-199">Para o campo **Tabela**, clique no ícone **Localizar** novamente para listar todas as tabelas Hive disponíveis no cluster.</span><span class="sxs-lookup"><span data-stu-id="e1b74-199">For the **Table** field, click the **Find** icon again to list all the Hive tables available in the cluster.</span></span> <span data-ttu-id="e1b74-200">Você deve ver a tabela **hvac** criada anteriormente usando o bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="e1b74-200">You should see the **hvac** table you created earlier using the notebook.</span></span>

    <span data-ttu-id="e1b74-201">![Localizar tabela para o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Localizar a tabela para o Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-201">![Find table for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")</span></span>
5. <span data-ttu-id="e1b74-202">Arraste e solte a tabela para a caixa superior à direita.</span><span class="sxs-lookup"><span data-stu-id="e1b74-202">Drag and drop the table to the top box on the right.</span></span> <span data-ttu-id="e1b74-203">O Tableau importa os dados e exibe o esquema conforme destacado pela caixa vermelha.</span><span class="sxs-lookup"><span data-stu-id="e1b74-203">Tableau imports the data and displays the schema as highlighted by the red box.</span></span>

    <span data-ttu-id="e1b74-204">![Adicionar tabelas ao Tableau para o Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Adicionar tabelas ao Tableau para o Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e1b74-204">![Add tables to Tableau for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables to Tableau for Apache Spark BI")</span></span>
6. <span data-ttu-id="e1b74-205">Clique na guia **Sheet1** na parte inferior esquerda.</span><span class="sxs-lookup"><span data-stu-id="e1b74-205">Click the **Sheet1** tab at the bottom left.</span></span> <span data-ttu-id="e1b74-206">Faça uma visualização que mostre as temperaturas almejada e real para todos os edifícios para cada data.</span><span class="sxs-lookup"><span data-stu-id="e1b74-206">Make a visualization that shows the average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="e1b74-207">Arraste **Data** e **ID do Prédio** para **Colunas** e **Temp. real**/**Temp. almejada** para **Linhas**.</span><span class="sxs-lookup"><span data-stu-id="e1b74-207">Drag **Date** and **Building ID** to **Columns** and **Actual Temp**/**Target Temp** to **Rows**.</span></span> <span data-ttu-id="e1b74-208">Em **Marcas**, selecione **Área** para usar uma mapa de área para a visualização de dados do Spark.</span><span class="sxs-lookup"><span data-stu-id="e1b74-208">Under **Marks**, select **Area** to use an area map for Spark data visualization.</span></span>

     <span data-ttu-id="e1b74-209">![Adicionar campos para visualização de dados do Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Adicionar campos para visualização de dados do Spark")</span><span class="sxs-lookup"><span data-stu-id="e1b74-209">![Add fields for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")</span></span>
7. <span data-ttu-id="e1b74-210">Por padrão, os campos de temperatura são mostrados em agregado.</span><span class="sxs-lookup"><span data-stu-id="e1b74-210">By default, the temperature fields are shown as aggregate.</span></span> <span data-ttu-id="e1b74-211">Se você desejar mostrar a temperatura média em vez disso, pode fazer isso na lista suspensa, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e1b74-211">If you want to show the average temperatures instead, you can do so from the drop-down, as shown below.</span></span>

    <span data-ttu-id="e1b74-212">![Obter a temperatura média para visualização de dados do Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Obter a temperatura média para visualização de dados do Spark")</span><span class="sxs-lookup"><span data-stu-id="e1b74-212">![Take average of temperature for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")</span></span>

8. <span data-ttu-id="e1b74-213">Você também pode sobrepor um mapa de temperatura a outro para ter uma ideia melhor da diferença entre as temperaturas almejada e real.</span><span class="sxs-lookup"><span data-stu-id="e1b74-213">You can also super-impose one temperature map over the other to get a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="e1b74-214">Mova o mouse para o canto do mapa da área inferior até ver a forma da alça realçada em um círculo vermelho.</span><span class="sxs-lookup"><span data-stu-id="e1b74-214">Move the mouse to the corner of the lower area map till you see the handle shape highlighted in a red circle.</span></span> <span data-ttu-id="e1b74-215">Arraste o mapa para o outro mapa na parte superior e solte o mouse ao ver a forma realçada no retângulo vermelho.</span><span class="sxs-lookup"><span data-stu-id="e1b74-215">Drag the map to the other map on the top and release the mouse when you see the shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="e1b74-216">![Mesclar mapas para visualização de dados do Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Mesclar mapas para visualização de dados do Spark")</span><span class="sxs-lookup"><span data-stu-id="e1b74-216">![Merge maps for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")</span></span>

     <span data-ttu-id="e1b74-217">A visualização de dados deve ser alterada conforme mostrado na captura de tela:</span><span class="sxs-lookup"><span data-stu-id="e1b74-217">Your data visualization should change as shown in the screenshot:</span></span>

    <span data-ttu-id="e1b74-218">![Saída do Tableau para visualização de dados do Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Saída do Tableau para visualização de dados do Spark")</span><span class="sxs-lookup"><span data-stu-id="e1b74-218">![Tableau output for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")</span></span>
9. <span data-ttu-id="e1b74-219">Clique em **Salvar** para salvar a planilha.</span><span class="sxs-lookup"><span data-stu-id="e1b74-219">Click **Save** to save the worksheet.</span></span> <span data-ttu-id="e1b74-220">Você pode criar painéis e adicionar uma ou mais planilhas a ele.</span><span class="sxs-lookup"><span data-stu-id="e1b74-220">You can create dashboards and add one or more sheets to it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1b74-221">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e1b74-221">Next steps</span></span>

<span data-ttu-id="e1b74-222">Até agora, você aprendeu como criar um cluster, criar quadros de dados do Spark para consultar dados e, em seguida, acessar esses dados de ferramentas de BI.</span><span class="sxs-lookup"><span data-stu-id="e1b74-222">So far you learned how to create a cluster, create Spark data frames to query data, and then access that data from BI tools.</span></span> <span data-ttu-id="e1b74-223">Agora você pode examinar as instruções sobre como gerenciar os recursos de cluster e depurar os trabalhos que são executados em um cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="e1b74-223">You can now look at instructions on how to manage the cluster resources and debug jobs that are running in an HDInsight Spark cluster.</span></span>

* [<span data-ttu-id="e1b74-224">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1b74-224">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e1b74-225">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1b74-225">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

