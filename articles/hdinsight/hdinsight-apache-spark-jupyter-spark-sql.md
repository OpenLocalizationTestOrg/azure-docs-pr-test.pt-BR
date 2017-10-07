---
title: cluster de aaaCreate um Apache Spark no HDInsight do Azure | Microsoft Docs
description: "Início rápido do HDInsight Spark no como cluster de toocreate um Apache Spark no HDInsight."
keywords: "início rápido do spark,spark interativo,consulta interativa,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="b9c46-104">Criar um cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9c46-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="b9c46-105">Neste artigo, você aprenderá como cluster de toocreate um Apache Spark no HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9c46-105">In this article, you learn how toocreate an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="b9c46-106">Para obter informações sobre o Spark no HDInsight, confira [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9c46-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="b9c46-107">![Diagrama de início rápido que descreve as etapas toocreate um cluster do Apache Spark no Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "início rápido do Spark usando o Apache Spark no HDInsight. Etapas ilustradas: criar um cluster; executar consulta interativa do Spark")</span><span class="sxs-lookup"><span data-stu-id="b9c46-107">![Quickstart diagram describing steps toocreate an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9c46-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b9c46-108">Prerequisites</span></span>

* <span data-ttu-id="b9c46-109">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="b9c46-109">**An Azure subscription**.</span></span> <span data-ttu-id="b9c46-110">Antes de começar este tutorial, você deverá ter uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9c46-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="b9c46-111">Consulte [Criar sua conta gratuita do Azure hoje](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="b9c46-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="b9c46-112">Criar cluster do Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b9c46-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="b9c46-113">Nesta seção, você criará um cluster Spark do HDInsight usando um [modelo do Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="b9c46-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="b9c46-114">Para obter outros métodos de criação de cluster, confira [Criar clusters do HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b9c46-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="b9c46-115">Clique em Olá seguindo o modelo de saudação tooopen imagem em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9c46-115">Click hello following image tooopen hello template in hello Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="b9c46-116">Digite hello valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9c46-116">Enter hello following values:</span></span>

    <span data-ttu-id="b9c46-117">![Criar um cluster Spark do HDInsight usando um modelo do Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Criar um cluster Spark no HDInsight usando um modelo do Azure Resource Manager")</span><span class="sxs-lookup"><span data-stu-id="b9c46-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="b9c46-118">**Assinatura**: selecione sua assinatura do Azure para esse cluster.</span><span class="sxs-lookup"><span data-stu-id="b9c46-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="b9c46-119">No **Grupo de recursos**: crie um grupo de recursos ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="b9c46-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="b9c46-120">Grupo de recursos é usado toomanage recursos do Azure para seus projetos.</span><span class="sxs-lookup"><span data-stu-id="b9c46-120">Resource group is used toomanage Azure resources for your projects.</span></span>
    * <span data-ttu-id="b9c46-121">**Local**: selecione um local para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9c46-121">**Location**: Select a location for hello resource group.</span></span> <span data-ttu-id="b9c46-122">modelo Olá usa esse local para a criação de cluster Olá bem como para o armazenamento de cluster saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="b9c46-122">hello template uses this location for creating hello cluster as well as for hello default cluster storage.</span></span>
    * <span data-ttu-id="b9c46-123">**ClusterName**: insira um nome para o cluster do HDInsight Olá que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="b9c46-123">**ClusterName**: Enter a name for hello HDInsight cluster that you want toocreate.</span></span>
    * <span data-ttu-id="b9c46-124">**Versão do Spark**: selecione **2.0** como versão Olá que você deseja tooinstall no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b9c46-124">**Spark version**: Select **2.0** as hello version that you want tooinstall on hello cluster.</span></span>
    * <span data-ttu-id="b9c46-125">**Nome de logon e senha do cluster**: nome de logon do saudação padrão é Admin.</span><span class="sxs-lookup"><span data-stu-id="b9c46-125">**Cluster login name and password**: hello default login name is admin.</span></span>
    * <span data-ttu-id="b9c46-126">**Nome de usuário e senha de SSH**.</span><span class="sxs-lookup"><span data-stu-id="b9c46-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="b9c46-127">Anote esses valores.</span><span class="sxs-lookup"><span data-stu-id="b9c46-127">Write down these values.</span></span>  <span data-ttu-id="b9c46-128">Você precisa-los mais tarde no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9c46-128">You need them later in hello tutorial.</span></span>

3. <span data-ttu-id="b9c46-129">Selecione **concordo toohello termos e condições declaradas acima**, selecione **Pin toodashboard**e, em seguida, clique em **compra**.</span><span class="sxs-lookup"><span data-stu-id="b9c46-129">Select **I agree toohello terms and conditions stated above**, select **Pin toodashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="b9c46-130">Você poderá ver um novo bloco intitulado Como enviar a implantação para a implantação do modelo.</span><span class="sxs-lookup"><span data-stu-id="b9c46-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="b9c46-131">Ele usa um cluster de saudação toocreate cerca de 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="b9c46-131">It takes about 20 minutes toocreate hello cluster.</span></span>

<span data-ttu-id="b9c46-132">Se você tiver um problema com a criação de clusters HDInsight, é possível que você não tem Olá permissões corretas toodo assim.</span><span class="sxs-lookup"><span data-stu-id="b9c46-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have hello right permissions toodo so.</span></span> <span data-ttu-id="b9c46-133">Confira [requisitos do controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="b9c46-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="b9c46-134">Este artigo cria um cluster Spark usa [armazenamento de Blobs de armazenamento do Azure como Olá cluster](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b9c46-134">This article creates a Spark cluster that uses [Azure Storage Blobs as hello cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="b9c46-135">Você também pode criar um cluster Spark que usa [repositório Azure Data Lake](hdinsight-hadoop-use-data-lake-store.md) como armazenamento de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9c46-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as hello default storage.</span></span> <span data-ttu-id="b9c46-136">Para obter instruções, confira [Criar um cluster HDInsight com o Repositório Data Lake](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b9c46-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="b9c46-137">Executar uma consulta de Hive usando o Spark SQL</span><span class="sxs-lookup"><span data-stu-id="b9c46-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="b9c46-138">Quando você usa um bloco de anotações do Jupyter configurado para o cluster HDInsight Spark, você obtém uma predefinição `sqlContext` que você pode usar consultas de Hive toorun usando Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="b9c46-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use toorun Hive queries using Spark SQL.</span></span> <span data-ttu-id="b9c46-139">Nesta seção, você aprenderá como toostart um bloco de anotações do Jupyter e, em seguida, execute uma consulta de Hive básica.</span><span class="sxs-lookup"><span data-stu-id="b9c46-139">In this section, you learn how toostart a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="b9c46-140">Olá abrir [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b9c46-140">Open hello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="b9c46-141">Se você optou por painel de toohello toopin Olá cluster, clique em Olá cluster lado a lado na folha de cluster Olá painel toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="b9c46-141">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="b9c46-142">Se você não fixar Olá cluster toohello painel de controle, no painel esquerdo do hello, clique em **clusters HDInsight**e, em seguida, clique em cluster Olá que você criou.</span><span class="sxs-lookup"><span data-stu-id="b9c46-142">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="b9c46-143">Em **Links rápidos**, clique em **Painéis de cluster**e, em seguida, clique em **Anotações do Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="b9c46-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="b9c46-144">Se solicitado, insira as credenciais de administrador de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b9c46-144">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="b9c46-145">![Abra Jupyter notebook toorun Spark SQL consulta interativo](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "consulta toorun Spark SQL interativo notebook Jupyter aberto")</span><span class="sxs-lookup"><span data-stu-id="b9c46-145">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="b9c46-146">Você também pode acessar as anotações do Jupyter Olá para o cluster por Olá abrir URL a seguir em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="b9c46-146">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="b9c46-147">Substituir **CLUSTERNAME** com nome de saudação do cluster:</span><span class="sxs-lookup"><span data-stu-id="b9c46-147">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="b9c46-148">Crie um notebook.</span><span class="sxs-lookup"><span data-stu-id="b9c46-148">Create a notebook.</span></span> <span data-ttu-id="b9c46-149">Clique em **Novo** e em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="b9c46-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="b9c46-150">![Criar uma consulta SQL Spark interativa Jupyter notebook toorun](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "criar uma consulta Jupyter notebook toorun interativa Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="b9c46-150">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="b9c46-151">Um novo bloco de anotações é criado e aberto com o nome hello Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="b9c46-151">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="b9c46-152">Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável, se desejar.</span><span class="sxs-lookup"><span data-stu-id="b9c46-152">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="b9c46-153">![Forneça um nome para Olá Jupter notebook toorun Spark consulta interativo de](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "forneça um nome para Olá Jupter notebook toorun Spark consulta interativa do")</span><span class="sxs-lookup"><span data-stu-id="b9c46-153">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5.  <span data-ttu-id="b9c46-154">Colar Olá seguinte código em uma célula vazia e, em seguida, pressione **SHIFT + ENTER** toorun código de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9c46-154">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="b9c46-155">Código de saudação abaixo `%%sql` (mágico de sql chamado hello) informa a predefinição Olá de toouse de notebook Jupyter `sqlContext` consulta de Hive toorun hello.</span><span class="sxs-lookup"><span data-stu-id="b9c46-155">In hello code below `%%sql` (called hello sql magic) tells Jupyter notebook toouse hello preset `sqlContext` toorun hello Hive query.</span></span> <span data-ttu-id="b9c46-156">consulta de saudação recupera Olá 10 primeiras linhas de uma tabela de Hive (**hivesampletable**) que está disponível por padrão em todos os clusters de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b9c46-156">hello query retrieves hello top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="b9c46-157">![Consulta de Hive no HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Consulta de Hive no HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="b9c46-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="b9c46-158">Para obter mais informações sobre Olá `%%sql` mágico e hello predefinição contextos, consulte [Jupyter kernels disponíveis para um cluster HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="b9c46-158">For more information on hello `%%sql` magic and hello preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="b9c46-159">Sempre que você executa uma consulta em Jupyter, o título da janela navegador web mostra um **(ocupada)** status junto com o título do bloco de anotações de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9c46-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="b9c46-160">Você também verá um toohello próximo do círculo sólido **PySpark** texto no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9c46-160">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="b9c46-161">Após o trabalho hello, ele altera o círculo vazio tooa.</span><span class="sxs-lookup"><span data-stu-id="b9c46-161">After hello job is completed, it changes tooa hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="b9c46-162">tela Hello deve atualizar a saída da consulta tooshow hello.</span><span class="sxs-lookup"><span data-stu-id="b9c46-162">hello screen should refresh tooshow hello query output.</span></span>

    <span data-ttu-id="b9c46-163">![Saída da consulta de Hive no HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Saída da consulta de Hive no HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="b9c46-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="b9c46-164">Desliga os recursos de cluster de saudação do hello notebook toorelease depois de terminar de executar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b9c46-164">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="b9c46-165">toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**.</span><span class="sxs-lookup"><span data-stu-id="b9c46-165">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="b9c46-166">Se você planejar as próximas etapas do toocomplete hello mais tarde, certifique-se de que excluir o cluster do HDInsight Olá criado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b9c46-166">If you plan toocomplete hello next steps at a later time, make sure you delete hello HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="b9c46-167">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="b9c46-167">Next step</span></span> 

<span data-ttu-id="b9c46-168">Neste artigo, você aprendeu como toocreate uma HDInsight Spark cluster e execute um Spark SQL básica de consulta.</span><span class="sxs-lookup"><span data-stu-id="b9c46-168">In this article you learned how toocreate an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="b9c46-169">Avança toohello próximo artigo toolearn como toouse uma HDInsight Spark cluster consultas interativas toorun em dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b9c46-169">Advance toohello next article toolearn how toouse an HDInsight Spark cluster toorun interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="b9c46-170">Executar consultas interativas em um cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b9c46-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



