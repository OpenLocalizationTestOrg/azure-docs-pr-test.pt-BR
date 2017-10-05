---
title: Usar notebooks Zeppelin com cluster Apache Spark no Azure HDInsight | Microsoft Docs
description: "Instruções passo a passo sobre como usar notebooks Zeppelin com clusters Apache Spark no Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7fe5e3ec68e82945b972d2dd44f2cc3b8cf395d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="96e8e-103">Usar notebooks Zeppelin com cluster Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="96e8e-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="96e8e-104">Os clusters de HDInsight Spark incluem notebooks Zeppelin que você pode usar para executar trabalhos do Spark.</span><span class="sxs-lookup"><span data-stu-id="96e8e-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span></span> <span data-ttu-id="96e8e-105">Neste artigo, você aprenderá a usar o notebook Zeppelin em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="96e8e-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="96e8e-106">Os blocos de anotações Zeppelin estão disponíveis apenas para Spark 1.6.3 no HDInsight 3.5 e Spark 2.1.0 no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="96e8e-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="96e8e-107">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="96e8e-107">**Prerequisites:**</span></span>

* <span data-ttu-id="96e8e-108">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="96e8e-108">An Azure subscription.</span></span> <span data-ttu-id="96e8e-109">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="96e8e-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="96e8e-110">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="96e8e-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="96e8e-111">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="96e8e-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="96e8e-112">Inicie um notebook Zeppelin</span><span class="sxs-lookup"><span data-stu-id="96e8e-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="96e8e-113">Na folha do cluster Spark, clique em **Painel do Cluster** e em **Notebook Zeppelin**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-113">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="96e8e-114">Se você receber uma solicitação, insira as credenciais de administrador para o cluster.</span><span class="sxs-lookup"><span data-stu-id="96e8e-114">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="96e8e-115">Você também pode acessar o Bloco de Notas Zeppelin de seu cluster abrindo a seguinte URL no navegador.</span><span class="sxs-lookup"><span data-stu-id="96e8e-115">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="96e8e-116">Substitua **CLUSTERNAME** pelo nome do cluster:</span><span class="sxs-lookup"><span data-stu-id="96e8e-116">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="96e8e-117">Crie um novo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="96e8e-117">Create a new notebook.</span></span> <span data-ttu-id="96e8e-118">No painel de cabeçalho, clique em **Notebook** e em **Criar Nova Anotação**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-118">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="96e8e-119">![Criar um novo notebook Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Criar um novo notebook Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="96e8e-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="96e8e-120">Insira um nome para o notebook e, em seguida, clique em **Criar Anotação**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-120">Enter a name for the notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="96e8e-121">Além disso, verifique se o cabeçalho do bloco de anotações mostra um status conectado.</span><span class="sxs-lookup"><span data-stu-id="96e8e-121">Also, make sure the notebook header shows a connected status.</span></span> <span data-ttu-id="96e8e-122">Isso é indicado por um ponto verde no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="96e8e-122">It is denoted by a green dot in the top-right corner.</span></span>
   
    <span data-ttu-id="96e8e-123">![Status do notebook Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Status do notebook Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="96e8e-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="96e8e-124">Carregar dados de exemplo em uma tabela temporária.</span><span class="sxs-lookup"><span data-stu-id="96e8e-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="96e8e-125">Quando você cria um cluster Spark no HDInsight, o arquivo de dados de exemplo, **hvac.csv**, é copiado para a conta de armazenamento associada em **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-125">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="96e8e-126">No parágrafo vazio criado por padrão no novo bloco de anotações, cole o trecho a seguir.</span><span class="sxs-lookup"><span data-stu-id="96e8e-126">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>
   
        %livy.spark
        //The above magic instructs Zeppelin to use the Livy Scala interpreter
   
        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map the values in the .csv file to the schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    <span data-ttu-id="96e8e-127">Pressione **SHIFT + ENTER** ou clique no botão **Reproduzir** para o parágrafo executar o trecho.</span><span class="sxs-lookup"><span data-stu-id="96e8e-127">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="96e8e-128">O status no canto direito do parágrafo deve progredir de PRONTO, PENDENTE, EM EXCECUÇÃO para CONCLUÍDO.</span><span class="sxs-lookup"><span data-stu-id="96e8e-128">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="96e8e-129">A saída é exibida na parte inferior do mesmo parágrafo.</span><span class="sxs-lookup"><span data-stu-id="96e8e-129">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="96e8e-130">A captura de tela é semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="96e8e-130">The screenshot looks like the following:</span></span>
   
    <span data-ttu-id="96e8e-131">![Criar uma tabela temporária a partir de dados brutos](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Criar uma tabela temporária a partir de dados brutos")</span><span class="sxs-lookup"><span data-stu-id="96e8e-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="96e8e-132">Você também pode fornecer um título para cada parágrafo.</span><span class="sxs-lookup"><span data-stu-id="96e8e-132">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="96e8e-133">No canto direito, clique no ícone **Configurações** e em **Mostrar título**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-133">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="96e8e-134">Agora você pode executar instruções do Spark SQL na tabela **hvac** .</span><span class="sxs-lookup"><span data-stu-id="96e8e-134">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="96e8e-135">Cole a seguinte consulta em um novo parágrafo.</span><span class="sxs-lookup"><span data-stu-id="96e8e-135">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="96e8e-136">A consulta recupera a ID do prédio e a diferença entre as temperaturas almejada e real para cada prédio em uma determinada data.</span><span class="sxs-lookup"><span data-stu-id="96e8e-136">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="96e8e-137">Pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="96e8e-138">A instrução **%sql** no início informa ao bloco de anotações para usar o interpretador Scala Livy.</span><span class="sxs-lookup"><span data-stu-id="96e8e-138">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="96e8e-139">A captura de tela a seguir mostra o resultado.</span><span class="sxs-lookup"><span data-stu-id="96e8e-139">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="96e8e-140">![Executar uma instrução SQL do Spark usando o notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Executar uma instrução SQL do Spark usando o notebook")</span><span class="sxs-lookup"><span data-stu-id="96e8e-140">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using the notebook")</span></span>
   
     <span data-ttu-id="96e8e-141">Clique nas opções de exibição (realçadas no retângulo) para alternar entre diferentes representações para o mesmo resultado.</span><span class="sxs-lookup"><span data-stu-id="96e8e-141">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="96e8e-142">Clique em **Configurações** para escolher o que constitui a chave e os valores na saída.</span><span class="sxs-lookup"><span data-stu-id="96e8e-142">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="96e8e-143">A captura de tela acima usa **buildingID** como a chave e a média de **temp_diff** como o valor.</span><span class="sxs-lookup"><span data-stu-id="96e8e-143">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
6. <span data-ttu-id="96e8e-144">Você também pode executar instruções Spark SQL usando variáveis na consulta.</span><span class="sxs-lookup"><span data-stu-id="96e8e-144">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="96e8e-145">O seguinte trecho mostra como definir uma variável, **Temp**, na consulta com os possíveis valores com os quais você deseja consultar.</span><span class="sxs-lookup"><span data-stu-id="96e8e-145">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="96e8e-146">Quando você executa a consulta pela primeira vez, uma lista suspensa é preenchida automaticamente com os valores especificados para a variável.</span><span class="sxs-lookup"><span data-stu-id="96e8e-146">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="96e8e-147">Cole esse trecho em um novo parágrafo e pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="96e8e-148">A captura de tela a seguir mostra o resultado.</span><span class="sxs-lookup"><span data-stu-id="96e8e-148">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="96e8e-149">![Executar uma instrução SQL do Spark usando o notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Executar uma instrução SQL do Spark usando o notebook")</span><span class="sxs-lookup"><span data-stu-id="96e8e-149">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using the notebook")</span></span>
   
    <span data-ttu-id="96e8e-150">Em consultas subsequentes, você pode selecionar um novo valor na lista suspensa e executar a consulta novamente.</span><span class="sxs-lookup"><span data-stu-id="96e8e-150">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="96e8e-151">Clique em **Configurações** para escolher o que constitui a chave e os valores na saída.</span><span class="sxs-lookup"><span data-stu-id="96e8e-151">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="96e8e-152">A captura de tela acima usa o **buildingID** como chave, a média de **temp_diff** como valor e a **targettemp** como grupo.</span><span class="sxs-lookup"><span data-stu-id="96e8e-152">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
7. <span data-ttu-id="96e8e-153">Reinicie o interpretador Livy para sair do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="96e8e-153">Restart the Livy interpreter to exit the application.</span></span> <span data-ttu-id="96e8e-154">Para fazer isso, abra as configurações do interpretador clicando no nome do usuário conectado no canto superior direito e clique em **Interpretador**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-154">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="96e8e-155">![Iniciar o intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Saída do Hive")</span><span class="sxs-lookup"><span data-stu-id="96e8e-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="96e8e-156">Role até as configurações do interpretador Livy e clique em **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-156">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="96e8e-157">![Reiniciar o intérprete do Livy](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Reiniciar o intérprete do Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="96e8e-157">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-the-notebook"></a><span data-ttu-id="96e8e-158">Como usar pacotes externos com o notebook?</span><span class="sxs-lookup"><span data-stu-id="96e8e-158">How do I use external packages with the notebook?</span></span>
<span data-ttu-id="96e8e-159">Você pode configurar o Zeppelin no cluster Apache Spark no HDInsight (Linux) para usar pacotes externos enviados pela comunidade que não estão incluídos prontos no cluster.</span><span class="sxs-lookup"><span data-stu-id="96e8e-159">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span></span> <span data-ttu-id="96e8e-160">Você pode pesquisar o [Repositório do Maven](http://search.maven.org/) para obter uma lista de pacotes que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="96e8e-160">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="96e8e-161">Você também pode obter uma lista de pacotes disponíveis de outras fontes.</span><span class="sxs-lookup"><span data-stu-id="96e8e-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="96e8e-162">Por exemplo, uma lista completa dos pacotes enviados pela comunidade está disponível em [Pacotes do Spark](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="96e8e-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="96e8e-163">Neste artigo, você aprenderá a usar o pacote [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) com o bloco de notas Jupyter.</span><span class="sxs-lookup"><span data-stu-id="96e8e-163">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

1. <span data-ttu-id="96e8e-164">Abra as configurações do interpretador.</span><span class="sxs-lookup"><span data-stu-id="96e8e-164">Open interpreter settings.</span></span> <span data-ttu-id="96e8e-165">No canto superior direito, clique no nome do usuário conectado e clique em **Interpretador**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-165">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="96e8e-166">![Iniciar o intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Saída do Hive")</span><span class="sxs-lookup"><span data-stu-id="96e8e-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="96e8e-167">Vá para configurações do interpretador Livy e clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-167">Scroll to Livy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="96e8e-168">![Alterar configurações do intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Alterar configurações do intérprete")</span><span class="sxs-lookup"><span data-stu-id="96e8e-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="96e8e-169">Adicionar uma nova chave chamada **livy.spark.jars.packages** e defina seu valor no formato `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="96e8e-169">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span></span> <span data-ttu-id="96e8e-170">Dessa forma, se você quiser usar o pacote [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar), deverá definir o valor da chave como `com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="96e8e-170">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="96e8e-171">![Alterar configurações do intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Alterar configurações do intérprete")</span><span class="sxs-lookup"><span data-stu-id="96e8e-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="96e8e-172">Clique em **Salvar** e reinicie o interpretador Livy.</span><span class="sxs-lookup"><span data-stu-id="96e8e-172">Click **Save** and then restart the Livy interpreter.</span></span>
4. <span data-ttu-id="96e8e-173">**Dica**: se você quiser entender como chegar ao valor da chave inserida acima, veja aqui como.</span><span class="sxs-lookup"><span data-stu-id="96e8e-173">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span></span>
   
    <span data-ttu-id="96e8e-174">a.</span><span class="sxs-lookup"><span data-stu-id="96e8e-174">a.</span></span> <span data-ttu-id="96e8e-175">Localize o pacote no Repositório Maven.</span><span class="sxs-lookup"><span data-stu-id="96e8e-175">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="96e8e-176">Para este tutorial, usamos [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="96e8e-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="96e8e-177">b.</span><span class="sxs-lookup"><span data-stu-id="96e8e-177">b.</span></span> <span data-ttu-id="96e8e-178">No repositório, colete os valores para **GroupId**, **ArtifactId** e **Version**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-178">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="96e8e-179">![Usar pacotes externos com blocos de anotações do Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Usar pacotes externos com blocos de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="96e8e-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="96e8e-180">c.</span><span class="sxs-lookup"><span data-stu-id="96e8e-180">c.</span></span> <span data-ttu-id="96e8e-181">Concatene os três valores, separados por dois pontos (**:**).</span><span class="sxs-lookup"><span data-stu-id="96e8e-181">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-the-zeppelin-notebooks-saved"></a><span data-ttu-id="96e8e-182">Onde os notebooks Zeppelin são salvos?</span><span class="sxs-lookup"><span data-stu-id="96e8e-182">Where are the Zeppelin notebooks saved?</span></span>
<span data-ttu-id="96e8e-183">Os notebooks Zeppelin são salvos nos nós de cabeçalho do cluster.</span><span class="sxs-lookup"><span data-stu-id="96e8e-183">The Zeppelin notebooks are saved to the cluster headnodes.</span></span> <span data-ttu-id="96e8e-184">Portanto, se você excluir o cluster, os notebooks também serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="96e8e-184">So, if you delete the cluster, the notebooks will be deleted as well.</span></span> <span data-ttu-id="96e8e-185">Se você quiser preservar os notebooks para uso posterior em outros clusters, deverá exportá-los depois de concluir os trabalhos em execução.</span><span class="sxs-lookup"><span data-stu-id="96e8e-185">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span></span> <span data-ttu-id="96e8e-186">Para exportar um notebook, clique no ícone **Exportar** como mostrado na imagem abaixo.</span><span class="sxs-lookup"><span data-stu-id="96e8e-186">To export a notebook, click the **Export** icon as shown in the image below.</span></span>

<span data-ttu-id="96e8e-187">![Baixar o notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Baixar o notebook")</span><span class="sxs-lookup"><span data-stu-id="96e8e-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span></span>

<span data-ttu-id="96e8e-188">Isso salva o notebook como um arquivo JSON em seu local de download.</span><span class="sxs-lookup"><span data-stu-id="96e8e-188">This saves the notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="96e8e-189">Gerenciamento de sessões do Livy</span><span class="sxs-lookup"><span data-stu-id="96e8e-189">Livy session management</span></span>
<span data-ttu-id="96e8e-190">Quando você executa o primeiro parágrafo de código no notebook Zeppelin, uma nova sessão do Livy é criada em seu cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="96e8e-190">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="96e8e-191">Essa sessão será compartilhada entre todos os notebooks Zeppelin que você criar posteriormente.</span><span class="sxs-lookup"><span data-stu-id="96e8e-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="96e8e-192">Se por algum motivo a sessão do Livy for interrompida (reinicialização do cluster etc.), você não poderá executar trabalhos no notebook Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="96e8e-192">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span></span>

<span data-ttu-id="96e8e-193">Nesse caso, você deverá executar as etapas a seguir antes de iniciar a execução de trabalhos de um notebook do Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="96e8e-193">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="96e8e-194">Reinicie o interpretador Livy no notebook Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="96e8e-194">Restart the Livy interpreter from the Zeppelin notebook.</span></span> <span data-ttu-id="96e8e-195">Para fazer isso, abra as configurações do interpretador clicando no nome do usuário conectado no canto superior direito e clique em **Interpretador**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-195">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="96e8e-196">![Iniciar o intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Saída do Hive")</span><span class="sxs-lookup"><span data-stu-id="96e8e-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="96e8e-197">Role até as configurações do interpretador Livy e clique em **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="96e8e-197">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="96e8e-198">![Reiniciar o intérprete do Livy](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Reiniciar o intérprete do Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="96e8e-198">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>
3. <span data-ttu-id="96e8e-199">Execute uma célula de código de um notebook Zeppelin existente.</span><span class="sxs-lookup"><span data-stu-id="96e8e-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="96e8e-200">Isso cria uma nova sessão do Livy no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="96e8e-200">This creates a new Livy session in the HDInsight cluster.</span></span>

## <span data-ttu-id="96e8e-201"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="96e8e-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="96e8e-202">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="96e8e-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="96e8e-203">Cenários</span><span class="sxs-lookup"><span data-stu-id="96e8e-203">Scenarios</span></span>
* [<span data-ttu-id="96e8e-204">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="96e8e-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="96e8e-205">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="96e8e-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="96e8e-206">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para prever resultados da inspeção de alimentos</span><span class="sxs-lookup"><span data-stu-id="96e8e-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="96e8e-207">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="96e8e-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="96e8e-208">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="96e8e-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="96e8e-209">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="96e8e-209">Create and run applications</span></span>
* [<span data-ttu-id="96e8e-210">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="96e8e-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="96e8e-211">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="96e8e-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="96e8e-212">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="96e8e-212">Tools and extensions</span></span>
* [<span data-ttu-id="96e8e-213">Usar o plug-in de Ferramentas do HDInsight para IntelliJ IDEA para criar e enviar aplicativos Spark Scala</span><span class="sxs-lookup"><span data-stu-id="96e8e-213">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="96e8e-214">Usar o plug-in de Ferramentas do HDInsight para o IntelliJ IDEA para depurar aplicativos Spark remotamente</span><span class="sxs-lookup"><span data-stu-id="96e8e-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="96e8e-215">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="96e8e-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="96e8e-216">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="96e8e-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="96e8e-217">Instalar o Jupyter em seu computador e conectar-se a um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="96e8e-217">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="96e8e-218">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="96e8e-218">Manage resources</span></span>
* [<span data-ttu-id="96e8e-219">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="96e8e-219">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="96e8e-220">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="96e8e-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







