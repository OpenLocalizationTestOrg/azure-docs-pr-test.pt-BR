---
title: "aaaUse dados de tooanalyze Apache Spark no repositório Azure Data Lake | Microsoft Docs"
description: "Executar trabalhos do Spark tooanalyze dados armazenados no repositório Azure Data Lake"
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
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a><span data-ttu-id="c2bd5-103">Usar dados de tooanalyze de cluster do HDInsight Spark no repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="c2bd5-103">Use HDInsight Spark cluster tooanalyze data in Data Lake Store</span></span>

<span data-ttu-id="c2bd5-104">Neste tutorial, você pode usar anotações do Jupyter disponível com clusters de HDInsight Spark toorun um trabalho que lê dados de uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters toorun a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2bd5-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c2bd5-105">Prerequisites</span></span>

* <span data-ttu-id="c2bd5-106">Conta do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="c2bd5-107">Siga as instruções de saudação em [Introdução ao repositório Azure Data Lake usando hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c2bd5-107">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="c2bd5-108">Cluster Spark HDInsight do Azure com o Data Lake Store como armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="c2bd5-109">Siga as instruções de saudação em [criar um cluster HDInsight com repositório Data Lake usando o Portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c2bd5-109">Follow hello instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-hello-data"></a><span data-ttu-id="c2bd5-110">Preparar dados Olá</span><span class="sxs-lookup"><span data-stu-id="c2bd5-110">Prepare hello data</span></span>

> [!NOTE]
> <span data-ttu-id="c2bd5-111">Não é necessário tooperform esta etapa se você tiver criado o cluster do HDInsight Olá com repositório Data Lake como armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-111">You do not need tooperform this step if you have created hello HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="c2bd5-112">processos de criação de cluster Olá adiciona alguns dados de exemplo na conta do repositório Data Lake Olá que você especificar durante a criação de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-112">hello cluster creation processes adds some sample data in hello Data Lake Store account that you specify while creating hello cluster.</span></span> <span data-ttu-id="c2bd5-113">Ignorar a seção toohello [cluster Use HDInsight Spark com repositório Data Lake](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="c2bd5-113">Skip toohello section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="c2bd5-114">Se você criou um cluster HDInsight com repositório Data Lake como armazenamento adicional e Blob de armazenamento do Azure como armazenamento padrão, você deve primeiro copiar sobre alguns dados de exemplo toohello conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data toohello Data Lake Store account.</span></span> <span data-ttu-id="c2bd5-115">Você pode usar dados de exemplo de saudação do hello que blob de armazenamento do Azure associado com o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-115">You can use hello sample data from hello Azure Storage Blob associated with hello HDInsight cluster.</span></span> <span data-ttu-id="c2bd5-116">Você pode usar o hello [ADLCopy ferramenta](http://aka.ms/downloadadlcopy) toodo para.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-116">You can use hello [ADLCopy tool](http://aka.ms/downloadadlcopy) toodo so.</span></span> <span data-ttu-id="c2bd5-117">Baixe e instale a ferramenta de saudação do link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-117">Download and install hello tool from hello link.</span></span>

1. <span data-ttu-id="c2bd5-118">Abra um prompt de comando e navegue diretório toohello onde AdlCopy é instalado, normalmente `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-118">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="c2bd5-119">Execute Olá toocopy de comando a seguir um blob específico de saudação fonte contêiner tooa repositório Data Lake:</span><span class="sxs-lookup"><span data-stu-id="c2bd5-119">Run hello following command toocopy a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="c2bd5-120">Saudação de cópia **HVAC.csv** do arquivo de dados de exemplo no **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello conta do repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-120">Copy hello **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store account.</span></span> <span data-ttu-id="c2bd5-121">trecho de código Olá deve parecer com:</span><span class="sxs-lookup"><span data-stu-id="c2bd5-121">hello code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="c2bd5-122">Certifique-se de Olá arquivo e nomes de caminho estão em letra maiuscula hello.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-122">Make sure you hello file and path names are in hello proper case.</span></span>
   >
   >
3. <span data-ttu-id="c2bd5-123">Será tooenter solicitada credenciais Olá Olá assinatura do Azure sob a qual você tem a sua conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-123">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="c2bd5-124">Você verá uma saída semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2bd5-124">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="c2bd5-125">arquivo de dados da saudação (**HVAC.csv**) serão copiados em uma pasta **/hvac** em Olá conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-125">hello data file (**HVAC.csv**) will be copied under a folder **/hvac** in hello Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="c2bd5-126">Usar um cluster Spark HDInsight com o Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c2bd5-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="c2bd5-127">De saudação [Portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial).</span><span class="sxs-lookup"><span data-stu-id="c2bd5-127">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="c2bd5-128">Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-128">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="c2bd5-129">Na folha de cluster do Spark hello, clique em **Links rápidos**e, em seguida, Olá **painel Cluster** folha, clique em **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-129">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="c2bd5-130">Se solicitado, insira as credenciais de administrador de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-130">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c2bd5-131">Você também poderá atingir Olá anotações do Jupyter para o cluster por Olá abrir URL a seguir em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-131">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="c2bd5-132">Substituir **CLUSTERNAME** com nome de saudação do cluster:</span><span class="sxs-lookup"><span data-stu-id="c2bd5-132">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="c2bd5-133">Crie um novo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-133">Create a new notebook.</span></span> <span data-ttu-id="c2bd5-134">Clique em **Novo** e em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="c2bd5-135">![Criar um novo bloco de anotações do Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Criar um novo bloco de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="c2bd5-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="c2bd5-136">Como você criou um bloco de anotações com o hello PySpark kernel, não é necessário toocreate qualquer contextos explicitamente.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="c2bd5-137">contextos de Spark e Hive Olá serão automaticamente criados para você quando você executar a primeira célula de código hello.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="c2bd5-138">Você pode começar importando tipos de saudação necessários para este cenário.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-138">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="c2bd5-139">toodo assim, cole Olá seguindo o trecho de código em uma célula e pressione **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-139">toodo so, paste hello following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="c2bd5-140">Toda vez que você executa um trabalho em Jupyter, o título de janela de navegador da web mostrará uma **(ocupada)** status junto com o título do bloco de anotações de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="c2bd5-141">Você também verá um toohello próximo do círculo sólido **PySpark** texto no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-141">You will also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="c2bd5-142">Após o trabalho hello, isso alterará o círculo vazio tooa.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-142">After hello job is completed, this will change tooa hollow circle.</span></span>

     <span data-ttu-id="c2bd5-143">![Status de um trabalho de bloco de anotações Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status de um trabalho de bloco de anotações Jupyter")</span><span class="sxs-lookup"><span data-stu-id="c2bd5-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="c2bd5-144">Carregar dados de amostra em uma tabela temporária usando Olá **HVAC.csv** arquivo copiado toohello conta de repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-144">Load sample data into a temporary table using hello **HVAC.csv** file you copied toohello Data Lake Store account.</span></span> <span data-ttu-id="c2bd5-145">Você pode acessar dados de saudação na conta do repositório Data Lake hello usando saudação padrão de URL a seguir.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-145">You can access hello data in hello Data Lake Store account using hello following URL pattern.</span></span>

    * <span data-ttu-id="c2bd5-146">Se você tiver o repositório Data Lake como armazenamento padrão, HVAC.csv será toohello semelhante de caminho Olá URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2bd5-146">If you have Data Lake Store as default storage, HVAC.csv will be at hello path similar toohello following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="c2bd5-147">Ou, você também pode usar um formato abreviado como seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c2bd5-147">Or, you could also use a shortened format such as hello following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="c2bd5-148">Se você tiver o repositório Data Lake como armazenamento adicional, HVAC.csv será no hello local onde você copiou, tais como:</span><span class="sxs-lookup"><span data-stu-id="c2bd5-148">If you have Data Lake Store as additional storage, HVAC.csv will be at hello location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="c2bd5-149">Em uma célula vazia, Olá cole o exemplo de código a seguir, substitua **MYDATALAKESTORE** com seu nome de conta do repositório Data Lake e pressione **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-149">In an empty cell, paste hello following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="c2bd5-150">Este exemplo de código registra dados saudação em uma tabela temporária chamada **hvac**.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-150">This code example registers hello data into a temporary table called **hvac**.</span></span>

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="c2bd5-151">Como você está usando um kernel PySpark, agora você pode diretamente executar uma consulta SQL na tabela temporária Olá **hvac** que você acabou de criar usando Olá `%%sql` mágica.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-151">Because you are using a PySpark kernel, you can now directly run a SQL query on hello temporary table **hvac** that you just created by using hello `%%sql` magic.</span></span> <span data-ttu-id="c2bd5-152">Para obter mais informações sobre Olá `%%sql` magic, bem como outros magics disponíveis com o kernel do PySpark hello, consulte [Kernels disponíveis em blocos de anotações do Jupyter com clusters HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="c2bd5-152">For more information about hello `%%sql` magic, as well as other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="c2bd5-153">Depois que o trabalho de saudação é concluído com êxito, Olá após a saída tabular é exibido por padrão.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-153">Once hello job is completed successfully, hello following tabular output is displayed by default.</span></span>

      <span data-ttu-id="c2bd5-154">![Saída do resultado de consulta de tabela](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Saída do resultado de consulta de tabela")</span><span class="sxs-lookup"><span data-stu-id="c2bd5-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="c2bd5-155">Você também pode ver os resultados de saudação em outras visualizações também.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="c2bd5-156">Por exemplo, um gráfico de área para Olá a mesma saída seria semelhante a seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-156">For example, an area graph for hello same output would look like hello following.</span></span>

     <span data-ttu-id="c2bd5-157">![Gráfico de área de resultado da consulta](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Gráfico de área de resultado da consulta")</span><span class="sxs-lookup"><span data-stu-id="c2bd5-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="c2bd5-158">Depois de terminar de executar o aplicativo hello, você deverá recursos de saudação do desligamento Olá notebook toorelease.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-158">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="c2bd5-159">toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="c2bd5-160">Esta desligará e notebook Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="c2bd5-160">This will shutdown and close hello notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c2bd5-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2bd5-161">Next steps</span></span>

* [<span data-ttu-id="c2bd5-162">Crie um toorun de aplicativo autônomo Scala Apache Spark cluster</span><span class="sxs-lookup"><span data-stu-id="c2bd5-162">Create a standalone Scala application toorun on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c2bd5-163">Usar ferramentas do HDInsight no Kit de ferramentas do Azure para aplicativos de Spark toocreate IntelliJ para o cluster HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="c2bd5-163">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c2bd5-164">Use as ferramentas do HDInsight no Kit de ferramentas do Azure para aplicativos do Eclipse toocreate Spark para HDInsight Spark Linux cluster</span><span class="sxs-lookup"><span data-stu-id="c2bd5-164">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
