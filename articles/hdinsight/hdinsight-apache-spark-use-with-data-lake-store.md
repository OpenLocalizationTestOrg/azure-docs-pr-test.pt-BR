---
title: Usar o Apache Spark para analisar os dados no Azure Data Lake Store | Microsoft Docs
description: Usar o Power BI para analisar os dados armazenados no Azure Data Lake Store
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 66f115c4f348ccaeb8855568ba1ad50faa442173
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-hdinsight-spark-cluster-to-analyze-data-in-data-lake-store"></a><span data-ttu-id="47a83-103">Usar o cluster Spark HDInsight para analisar dados no Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="47a83-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>

<span data-ttu-id="47a83-104">Neste tutorial, você usará no notebook Jupyter disponível com os clusters Spark HDInsight para executar um trabalho que lê dados de uma conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47a83-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47a83-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="47a83-105">Prerequisites</span></span>

* <span data-ttu-id="47a83-106">Conta do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47a83-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="47a83-107">Siga as instruções em [Introdução ao Repositório Azure Data Lake usando o Portal do Azure](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47a83-107">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="47a83-108">Cluster Spark HDInsight do Azure com o Data Lake Store como armazenamento.</span><span class="sxs-lookup"><span data-stu-id="47a83-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="47a83-109">Siga as instruções em [Criar um cluster HDInsight com o Data Lake Store usando o Portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47a83-109">Follow the instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-the-data"></a><span data-ttu-id="47a83-110">Preparar os dados</span><span class="sxs-lookup"><span data-stu-id="47a83-110">Prepare the data</span></span>

> [!NOTE]
> <span data-ttu-id="47a83-111">Não é necessário realizar essa etapa se você criou o cluster HDInsight com o Data Lake Store como armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="47a83-111">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="47a83-112">Os processos de criação de cluster adicionam alguns dados de exemplo à conta do Data Lake Store, especificados durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="47a83-112">The cluster creation processes adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span></span> <span data-ttu-id="47a83-113">Vá para a seção [Usar o cluster HDInsight Spark com o Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="47a83-113">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="47a83-114">Se você criou um cluster HDInsight com o Data Lake Store como armazenamento adicional e o Azure Storage Blob como armazenamento padrão, copie primeiro alguns dados de exemplo para a conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47a83-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span></span> <span data-ttu-id="47a83-115">Use os dados de exemplo do Blob de Armazenamento do Azure associado ao cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47a83-115">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span></span> <span data-ttu-id="47a83-116">Você pode usar a [ferramenta ADLCopy](http://aka.ms/downloadadlcopy) para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="47a83-116">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span></span> <span data-ttu-id="47a83-117">Baixe e instale a ferramenta a partir do link.</span><span class="sxs-lookup"><span data-stu-id="47a83-117">Download and install the tool from the link.</span></span>

1. <span data-ttu-id="47a83-118">Abra um prompt de comando e navegue até o diretório onde AdlCopy está instalado, normalmente `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="47a83-118">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="47a83-119">Execute o seguinte comando para copiar um blob específico do contêiner de origem para um Repositório Data Lake:</span><span class="sxs-lookup"><span data-stu-id="47a83-119">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="47a83-120">Copie o arquivo de exemplo de dados **HVAC.csv** em **/HdiSamples/HdiSamples/SensorSampleData/hvac/** para a conta do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47a83-120">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span></span> <span data-ttu-id="47a83-121">O trecho de código deve parecer com:</span><span class="sxs-lookup"><span data-stu-id="47a83-121">The code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="47a83-122">Verifique se os nomes de arquivo e caminho estão com a capitalização apropriada.</span><span class="sxs-lookup"><span data-stu-id="47a83-122">Make sure you the file and path names are in the proper case.</span></span>
   >
   >
3. <span data-ttu-id="47a83-123">Você precisará inserir as credenciais da assinatura do Azure vinculadas à conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47a83-123">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="47a83-124">Você verá uma saída semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="47a83-124">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="47a83-125">O arquivo de dados (**HVAC.csv**) será copiado em uma pasta **/hvac** na conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47a83-125">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="47a83-126">Usar um cluster Spark HDInsight com o Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="47a83-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="47a83-127">No [Portal do Azure](https://portal.azure.com/), no quadro inicial, clique no bloco do cluster Spark (se você o tiver fixado no quadro inicial).</span><span class="sxs-lookup"><span data-stu-id="47a83-127">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="47a83-128">Você também pode navegar até o cluster em **Procurar Tudo** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="47a83-128">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="47a83-129">Na folha do cluster Spark, clique em **Links Rápidos** e, na folha **Painel do Cluster**, clique em **Notebook do Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="47a83-129">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="47a83-130">Se você receber uma solicitação, insira as credenciais de administrador para o cluster.</span><span class="sxs-lookup"><span data-stu-id="47a83-130">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="47a83-131">Você também pode acessar o Bloco de Notas Jupyter de seu cluster abrindo a seguinte URL no navegador.</span><span class="sxs-lookup"><span data-stu-id="47a83-131">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="47a83-132">Substitua **CLUSTERNAME** pelo nome do cluster:</span><span class="sxs-lookup"><span data-stu-id="47a83-132">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="47a83-133">Crie um novo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="47a83-133">Create a new notebook.</span></span> <span data-ttu-id="47a83-134">Clique em **Novo** e em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="47a83-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="47a83-135">![Criar um novo bloco de anotações do Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Criar um novo bloco de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="47a83-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="47a83-136">Por ter criado um notebook usando o kernel PySpark, não será necessário criar nenhum contexto explicitamente.</span><span class="sxs-lookup"><span data-stu-id="47a83-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="47a83-137">Os contextos do Spark e do Hive serão criados automaticamente para você ao executar a primeira célula do código.</span><span class="sxs-lookup"><span data-stu-id="47a83-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="47a83-138">Você pode começar importando os tipos obrigatórios para este cenário.</span><span class="sxs-lookup"><span data-stu-id="47a83-138">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="47a83-139">Para fazer isso, cole o trecho de código a seguir em uma célula vazia e pressione **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="47a83-139">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="47a83-140">Toda vez que você executar um trabalho no Jupyter, o título da janela do navegador da Web mostrará um status **(Ocupado)** com o título do bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="47a83-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="47a83-141">Você também verá um círculo sólido ao lado do texto **PySpark** no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="47a83-141">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="47a83-142">Depois que o trabalho for concluído, isso será alterado para um círculo vazio.</span><span class="sxs-lookup"><span data-stu-id="47a83-142">After the job is completed, this will change to a hollow circle.</span></span>

     <span data-ttu-id="47a83-143">![Status de um trabalho de bloco de anotações Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status de um trabalho de bloco de anotações Jupyter")</span><span class="sxs-lookup"><span data-stu-id="47a83-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="47a83-144">Carregue os dados de exemplo em uma tabela temporária usando o arquivo **HVAC.csv** copiado para a conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47a83-144">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span></span> <span data-ttu-id="47a83-145">Você pode acessar os dados na conta do Repositório Data Lake usando o seguinte padrão de URL.</span><span class="sxs-lookup"><span data-stu-id="47a83-145">You can access the data in the Data Lake Store account using the following URL pattern.</span></span>

    * <span data-ttu-id="47a83-146">Se o Data Lake Store for seu armazenamento padrão, HVAC.csv estará em um caminho semelhante à URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="47a83-146">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="47a83-147">Ou, você também pode usar um formato reduzido como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="47a83-147">Or, you could also use a shortened format such as the following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="47a83-148">Se o Data Lake Store for seu armazenamento adicional, HVAC.csv estará no local onde você o copiou, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="47a83-148">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="47a83-149">Em uma célula vazia, cole o seguinte exemplo de código, substitua **MYDATALAKESTORE** pelo nome de sua conta do Data Lake Store e pressione **Shift+Enter**.</span><span class="sxs-lookup"><span data-stu-id="47a83-149">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="47a83-150">Esse exemplo de código registra os dados em uma tabela temporária chamada **hvac**.</span><span class="sxs-lookup"><span data-stu-id="47a83-150">This code example registers the data into a temporary table called **hvac**.</span></span>

            # Load the data. The path below assumes Data Lake Store is default storage for the Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create the schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse the data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register the data fram as a table to run queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="47a83-151">Como está usando um kernel PySpark, agora você pode executar diretamente uma consulta SQL na tabela temporária **hvac** que acabou de criar usando a mágica de `%%sql`.</span><span class="sxs-lookup"><span data-stu-id="47a83-151">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span></span> <span data-ttu-id="47a83-152">Para obter mais informações sobre a mágica de `%%sql` , bem como outras mágicas disponíveis com o kernel PySpark, confira [Kernels disponíveis em notebooks Jupyter com clusters HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="47a83-152">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="47a83-153">Depois que o trabalho for concluído com êxito, a saída tabular a seguir será exibida por padrão.</span><span class="sxs-lookup"><span data-stu-id="47a83-153">Once the job is completed successfully, the following tabular output is displayed by default.</span></span>

      <span data-ttu-id="47a83-154">![Saída do resultado de consulta de tabela](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Saída do resultado de consulta de tabela")</span><span class="sxs-lookup"><span data-stu-id="47a83-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="47a83-155">Você também pode ver os resultados em outras visualizações.</span><span class="sxs-lookup"><span data-stu-id="47a83-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="47a83-156">Por exemplo, um gráfico de área para a mesma saída seria semelhante ao seguinte.</span><span class="sxs-lookup"><span data-stu-id="47a83-156">For example, an area graph for the same output would look like the following.</span></span>

     <span data-ttu-id="47a83-157">![Gráfico de área de resultado da consulta](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Gráfico de área de resultado da consulta")</span><span class="sxs-lookup"><span data-stu-id="47a83-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="47a83-158">Depois de concluir a execução do aplicativo, você deve encerrar o notebook para liberar os recursos.</span><span class="sxs-lookup"><span data-stu-id="47a83-158">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="47a83-159">Para isso, no menu **Arquivo** do bloco de anotações, clique em **Fechar e Interromper**.</span><span class="sxs-lookup"><span data-stu-id="47a83-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="47a83-160">Isso desligará e fechará o bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="47a83-160">This will shutdown and close the notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="47a83-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47a83-161">Next steps</span></span>

* [<span data-ttu-id="47a83-162">Criar um aplicativo Scala autônomo para ser executado no cluster do Apache Spark</span><span class="sxs-lookup"><span data-stu-id="47a83-162">Create a standalone Scala application to run on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="47a83-163">Usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ a fim de criar aplicativos Spark para um cluster HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="47a83-163">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="47a83-164">Usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para Eclipse a fim de criar aplicativos Spark para um cluster HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="47a83-164">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
