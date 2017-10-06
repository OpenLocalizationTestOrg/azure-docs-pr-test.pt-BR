---
title: "cluster de blocos de anotações do aaaUse Zeppelin com o Apache Spark no Azure HDInsight | Microsoft Docs"
description: "Instruções passo a passo sobre como clusters de blocos de anotações do toouse Zeppelin com o Apache Spark no HDInsight do Azure."
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
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="9711f-103">Usar notebooks Zeppelin com cluster Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9711f-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="9711f-104">Clusters de HDInsight Spark incluem notebooks Zeppelin que você pode usar trabalhos do Spark toorun.</span><span class="sxs-lookup"><span data-stu-id="9711f-104">HDInsight Spark clusters include Zeppelin notebooks that you can use toorun Spark jobs.</span></span> <span data-ttu-id="9711f-105">Neste artigo, você aprenderá como toouse Olá notebook Zeppelin em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9711f-105">In this article, you learn how toouse hello Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="9711f-106">Os blocos de anotações Zeppelin estão disponíveis apenas para Spark 1.6.3 no HDInsight 3.5 e Spark 2.1.0 no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="9711f-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="9711f-107">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="9711f-107">**Prerequisites:**</span></span>

* <span data-ttu-id="9711f-108">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9711f-108">An Azure subscription.</span></span> <span data-ttu-id="9711f-109">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9711f-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="9711f-110">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9711f-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="9711f-111">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="9711f-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="9711f-112">Inicie um notebook Zeppelin</span><span class="sxs-lookup"><span data-stu-id="9711f-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="9711f-113">Na folha de cluster do Spark hello, clique em **painel Cluster**e, em seguida, clique em **Zeppelin Notebook**.</span><span class="sxs-lookup"><span data-stu-id="9711f-113">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="9711f-114">Se solicitado, insira as credenciais de administrador de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9711f-114">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9711f-115">Você também pode acessar Olá Zeppelin Notebook para seu cluster por Olá abrir URL a seguir em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="9711f-115">You may also reach hello Zeppelin Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="9711f-116">Substituir **CLUSTERNAME** com nome de saudação do cluster:</span><span class="sxs-lookup"><span data-stu-id="9711f-116">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="9711f-117">Crie um novo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="9711f-117">Create a new notebook.</span></span> <span data-ttu-id="9711f-118">No painel de cabeçalho hello, clique em **Notebook**e, em seguida, clique em **criar nova anotação**.</span><span class="sxs-lookup"><span data-stu-id="9711f-118">From hello header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="9711f-119">![Criar um novo notebook Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Criar um novo notebook Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="9711f-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="9711f-120">Insira um nome para o bloco de anotações hello e, em seguida, clique em **criar anotação**.</span><span class="sxs-lookup"><span data-stu-id="9711f-120">Enter a name for hello notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="9711f-121">Além disso, certifique-se de cabeçalho do bloco de anotações de saudação mostrará um status conectado.</span><span class="sxs-lookup"><span data-stu-id="9711f-121">Also, make sure hello notebook header shows a connected status.</span></span> <span data-ttu-id="9711f-122">Ele é indicado por um ponto verde no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="9711f-122">It is denoted by a green dot in hello top-right corner.</span></span>
   
    <span data-ttu-id="9711f-123">![Status do notebook Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Status do notebook Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="9711f-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="9711f-124">Carregar dados de exemplo em uma tabela temporária.</span><span class="sxs-lookup"><span data-stu-id="9711f-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="9711f-125">Quando você cria um cluster Spark no HDInsight, arquivo de dados de exemplo hello, **hvac.csv**, é copiado toohello associado a conta de armazenamento em **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="9711f-125">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="9711f-126">No parágrafo vazio Olá que é criado por padrão no novo bloco de anotações de hello, cole Olá trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="9711f-126">In hello empty paragraph that is created by default in hello new notebook, paste hello following snippet.</span></span>
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
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
   
    <span data-ttu-id="9711f-127">Pressione **SHIFT + ENTER** ou clique em Olá **reproduzir** botão de trecho de código da saudação toorun Olá parágrafo.</span><span class="sxs-lookup"><span data-stu-id="9711f-127">Press **SHIFT + ENTER** or click hello **Play** button for hello paragraph toorun hello snippet.</span></span> <span data-ttu-id="9711f-128">status Olá no canto direito de saudação do parágrafo Olá deve avançar de READY, pendente, tooFINISHED em execução.</span><span class="sxs-lookup"><span data-stu-id="9711f-128">hello status on hello right-corner of hello paragraph should progress from READY, PENDING, RUNNING tooFINISHED.</span></span> <span data-ttu-id="9711f-129">saída de Hello aparece na parte inferior de saudação do hello mesmo paragraph.</span><span class="sxs-lookup"><span data-stu-id="9711f-129">hello output shows up at hello bottom of hello same paragraph.</span></span> <span data-ttu-id="9711f-130">captura de tela de saudação semelhante ao seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9711f-130">hello screenshot looks like hello following:</span></span>
   
    <span data-ttu-id="9711f-131">![Criar uma tabela temporária a partir de dados brutos](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Criar uma tabela temporária a partir de dados brutos")</span><span class="sxs-lookup"><span data-stu-id="9711f-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="9711f-132">Você também pode fornecer um parágrafo de tooeach do título.</span><span class="sxs-lookup"><span data-stu-id="9711f-132">You can also provide a title tooeach paragraph.</span></span> <span data-ttu-id="9711f-133">No canto superior direito da saudação, clique em Olá **configurações** ícone e clique **Mostrar título**.</span><span class="sxs-lookup"><span data-stu-id="9711f-133">From hello right-hand corner, click hello **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="9711f-134">Agora você pode executar instruções SQL Spark no hello **hvac** tabela.</span><span class="sxs-lookup"><span data-stu-id="9711f-134">You can now run Spark SQL statements on hello **hvac** table.</span></span> <span data-ttu-id="9711f-135">Colar Olá consulta em um novo parágrafo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9711f-135">Paste hello following query in a new paragraph.</span></span> <span data-ttu-id="9711f-136">consulta Olá recupera a ID de construção de hello e diferença de saudação entre destino hello e temperaturas reais para cada prédio em uma determinada data.</span><span class="sxs-lookup"><span data-stu-id="9711f-136">hello query retrieves hello building ID and hello difference between hello target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="9711f-137">Pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="9711f-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="9711f-138">Olá **% sql** instrução no início de saudação informa ao interpretador de Livy Scala Olá notebook toouse hello.</span><span class="sxs-lookup"><span data-stu-id="9711f-138">hello **%sql** statement at hello beginning tells hello notebook toouse hello Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="9711f-139">Hello seguinte captura de tela mostra a saída de hello.</span><span class="sxs-lookup"><span data-stu-id="9711f-139">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="9711f-140">![Executar uma instrução SQL do Spark usando notebook Olá](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "executar uma instrução SQL Spark usando o bloco de anotações de saudação")</span><span class="sxs-lookup"><span data-stu-id="9711f-140">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using hello notebook")</span></span>
   
     <span data-ttu-id="9711f-141">Clique em Olá exibição Opções (destacado no retângulo) tooswitch entre diferentes representações de saudação mesma saída.</span><span class="sxs-lookup"><span data-stu-id="9711f-141">Click hello display options (highlighted in rectangle) tooswitch between different representations for hello same output.</span></span> <span data-ttu-id="9711f-142">Clique em **configurações** toochoose que consitutes Olá chave e valores na saída de hello.</span><span class="sxs-lookup"><span data-stu-id="9711f-142">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="9711f-143">Olá captura de tela acima usa **buildingID** hello e média de saudação do **temp_diff** como valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="9711f-143">hello screen capture above uses **buildingID** as hello key and hello average of **temp_diff** as hello value.</span></span>
6. <span data-ttu-id="9711f-144">Você também pode executar instruções SQL Spark usando variáveis na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9711f-144">You can also run Spark SQL statements using variables in hello query.</span></span> <span data-ttu-id="9711f-145">Olá Avançar mostra de trecho de código como toodefine uma variável, **Temp**, na consulta Olá com os valores possíveis Olá deseja tooquery com.</span><span class="sxs-lookup"><span data-stu-id="9711f-145">hello next snippet shows how toodefine a variable, **Temp**, in hello query with hello possible values you want tooquery with.</span></span> <span data-ttu-id="9711f-146">Ao executar consulta Olá pela primeira vez, uma lista suspensa automaticamente é preenchida com valores de saudação especificado para a variável de saudação.</span><span class="sxs-lookup"><span data-stu-id="9711f-146">When you first run hello query, a drop-down is automatically populated with hello values you specified for hello variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="9711f-147">Cole esse trecho em um novo parágrafo e pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="9711f-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="9711f-148">Hello seguinte captura de tela mostra a saída de hello.</span><span class="sxs-lookup"><span data-stu-id="9711f-148">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="9711f-149">![Executar uma instrução SQL do Spark usando notebook Olá](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "executar uma instrução SQL Spark usando o bloco de anotações de saudação")</span><span class="sxs-lookup"><span data-stu-id="9711f-149">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using hello notebook")</span></span>
   
    <span data-ttu-id="9711f-150">Para as consultas subsequentes, você pode selecionar um novo valor na lista suspensa hello e execute a consulta de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="9711f-150">For subsequent queries, you can select a new value from hello drop-down and run hello query again.</span></span> <span data-ttu-id="9711f-151">Clique em **configurações** toochoose que consitutes Olá chave e valores na saída de hello.</span><span class="sxs-lookup"><span data-stu-id="9711f-151">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="9711f-152">Olá captura de tela acima usa **buildingID** como chave Olá Olá médio de **temp_diff** como valor de saudação e **targettemp** como grupo hello.</span><span class="sxs-lookup"><span data-stu-id="9711f-152">hello screen capture above uses **buildingID** as hello key, hello average of **temp_diff** as hello value, and **targettemp** as hello group.</span></span>
7. <span data-ttu-id="9711f-153">Reinicie Olá aplicativo hello do Livy interpretador tooexit.</span><span class="sxs-lookup"><span data-stu-id="9711f-153">Restart hello Livy interpreter tooexit hello application.</span></span> <span data-ttu-id="9711f-154">toodo isso, abra as configurações do interpretador clicando Olá registrado no nome de usuário do canto superior direito de saudação e, em seguida, clique em **interpretador**.</span><span class="sxs-lookup"><span data-stu-id="9711f-154">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="9711f-155">![Iniciar o intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Saída do Hive")</span><span class="sxs-lookup"><span data-stu-id="9711f-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="9711f-156">Role a tela de configurações do interpretador tooLivy e, em seguida, clique em **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="9711f-156">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="9711f-157">![Reiniciar Olá Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "reiniciar Olá Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="9711f-157">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a><span data-ttu-id="9711f-158">Como usar pacotes externos com notebook Olá?</span><span class="sxs-lookup"><span data-stu-id="9711f-158">How do I use external packages with hello notebook?</span></span>
<span data-ttu-id="9711f-159">Você pode configurar o bloco de anotações do hello Zeppelin no cluster do Apache Spark no HDInsight (Linux) toouse externo contribuído pela comunidade de pacotes que não são incluídos-a-prontos cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9711f-159">You can configure hello Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed packages that are not included out-of-the-box in hello cluster.</span></span> <span data-ttu-id="9711f-160">Você pode pesquisar Olá [Repositório Maven](http://search.maven.org/) para a lista completa de saudação dos pacotes que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="9711f-160">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="9711f-161">Você também pode obter uma lista de pacotes disponíveis de outras fontes.</span><span class="sxs-lookup"><span data-stu-id="9711f-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="9711f-162">Por exemplo, uma lista completa dos pacotes enviados pela comunidade está disponível em [Pacotes do Spark](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="9711f-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="9711f-163">Neste artigo, você verá como Olá toouse [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pacote com anotações do Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="9711f-163">In this article, you will see how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>

1. <span data-ttu-id="9711f-164">Abra as configurações do interpretador.</span><span class="sxs-lookup"><span data-stu-id="9711f-164">Open interpreter settings.</span></span> <span data-ttu-id="9711f-165">Do canto superior direito de saudação, clique em Olá registrado no nome de usuário e, em seguida, clique em **interpretador**.</span><span class="sxs-lookup"><span data-stu-id="9711f-165">From hello top-right corner, click hello logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="9711f-166">![Iniciar o intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Saída do Hive")</span><span class="sxs-lookup"><span data-stu-id="9711f-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="9711f-167">Role a tela de configurações do interpretador tooLivy e, em seguida, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="9711f-167">Scroll tooLivy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="9711f-168">![Alterar configurações do intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Alterar configurações do intérprete")</span><span class="sxs-lookup"><span data-stu-id="9711f-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="9711f-169">Adicionar uma nova chave chamada **livy.spark.jars.packages** e defina seu valor no formato de saudação `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="9711f-169">Add a new key, called **livy.spark.jars.packages** and set its value in hello format `group:id:version`.</span></span> <span data-ttu-id="9711f-170">Portanto, se você deseja Olá toouse [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pacote, você deve definir a saudação valor da chave de saudação muito`com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="9711f-170">So, if you want toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set hello value of hello key too`com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="9711f-171">![Alterar configurações do intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Alterar configurações do intérprete")</span><span class="sxs-lookup"><span data-stu-id="9711f-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="9711f-172">Clique em **salvar** e, em seguida, reinicie Olá interpretador Livy.</span><span class="sxs-lookup"><span data-stu-id="9711f-172">Click **Save** and then restart hello Livy interpreter.</span></span>
4. <span data-ttu-id="9711f-173">**Dica**: se você quiser toounderstand como tooarrive no valor de saudação da chave Olá inserido acima, aqui está como.</span><span class="sxs-lookup"><span data-stu-id="9711f-173">**Tip**: If you want toounderstand how tooarrive at hello value of hello key entered above, here's how.</span></span>
   
    <span data-ttu-id="9711f-174">a.</span><span class="sxs-lookup"><span data-stu-id="9711f-174">a.</span></span> <span data-ttu-id="9711f-175">Localize o pacote de saudação em Olá Repositório Maven.</span><span class="sxs-lookup"><span data-stu-id="9711f-175">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="9711f-176">Para este tutorial, usamos [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="9711f-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="9711f-177">b.</span><span class="sxs-lookup"><span data-stu-id="9711f-177">b.</span></span> <span data-ttu-id="9711f-178">Do repositório de saudação reunir os valores hello para **GroupId**, **ArtifactId**, e **versão**.</span><span class="sxs-lookup"><span data-stu-id="9711f-178">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="9711f-179">![Usar pacotes externos com blocos de anotações do Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Usar pacotes externos com blocos de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="9711f-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="9711f-180">c.</span><span class="sxs-lookup"><span data-stu-id="9711f-180">c.</span></span> <span data-ttu-id="9711f-181">Concatenar valores hello três, separados por dois-pontos (**:**).</span><span class="sxs-lookup"><span data-stu-id="9711f-181">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a><span data-ttu-id="9711f-182">Onde está Olá notebooks Zeppelin salvados?</span><span class="sxs-lookup"><span data-stu-id="9711f-182">Where are hello Zeppelin notebooks saved?</span></span>
<span data-ttu-id="9711f-183">blocos de anotações do Hello Zeppelin são salvos toohello headnodes de cluster.</span><span class="sxs-lookup"><span data-stu-id="9711f-183">hello Zeppelin notebooks are saved toohello cluster headnodes.</span></span> <span data-ttu-id="9711f-184">Portanto, se você excluir o cluster hello, notebooks Olá também serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="9711f-184">So, if you delete hello cluster, hello notebooks will be deleted as well.</span></span> <span data-ttu-id="9711f-185">Se você quiser toopreserve seus blocos de anotações para uso posterior em outros clusters, você deve exportá-los depois de concluir a saudação de trabalhos em execução.</span><span class="sxs-lookup"><span data-stu-id="9711f-185">If you want toopreserve your notebooks for later use on other clusters, you must export them after you have finished running hello jobs.</span></span> <span data-ttu-id="9711f-186">tooexport um bloco de anotações, clique em Olá **exportar** ícone conforme mostrado na imagem de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="9711f-186">tooexport a notebook, click hello **Export** icon as shown in hello image below.</span></span>

<span data-ttu-id="9711f-187">![Baixar notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "notebook de saudação do Download")</span><span class="sxs-lookup"><span data-stu-id="9711f-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download hello notebook")</span></span>

<span data-ttu-id="9711f-188">Isso economiza notebook hello como um arquivo JSON em seu local de download.</span><span class="sxs-lookup"><span data-stu-id="9711f-188">This saves hello notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="9711f-189">Gerenciamento de sessões do Livy</span><span class="sxs-lookup"><span data-stu-id="9711f-189">Livy session management</span></span>
<span data-ttu-id="9711f-190">Quando você executa o primeiro parágrafo de código Olá no bloco de anotações Zeppelin, uma nova sessão Livy é criada em seu cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="9711f-190">When you run hello first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="9711f-191">Essa sessão será compartilhada entre todos os notebooks Zeppelin que você criar posteriormente.</span><span class="sxs-lookup"><span data-stu-id="9711f-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="9711f-192">Se, por algum Olá motivo Livy sessão for interrompida (reinicialização de cluster, etc.), não será capaz de toorun trabalhos do bloco de anotações de Zeppelin hello.</span><span class="sxs-lookup"><span data-stu-id="9711f-192">If for some reason hello Livy session is killed (cluster reboot, etc.), you will not be able toorun jobs from hello Zeppelin notebook.</span></span>

<span data-ttu-id="9711f-193">Nesse caso, você deve executar Olá etapas a seguir antes de iniciar trabalhos em execução de um bloco de anotações de Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="9711f-193">In such a case, you must perform hello following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="9711f-194">Reinicie Olá interpretador Livy do bloco de anotações de Zeppelin hello.</span><span class="sxs-lookup"><span data-stu-id="9711f-194">Restart hello Livy interpreter from hello Zeppelin notebook.</span></span> <span data-ttu-id="9711f-195">toodo isso, abra as configurações do interpretador clicando Olá registrado no nome de usuário do canto superior direito de saudação e, em seguida, clique em **interpretador**.</span><span class="sxs-lookup"><span data-stu-id="9711f-195">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="9711f-196">![Iniciar o intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Saída do Hive")</span><span class="sxs-lookup"><span data-stu-id="9711f-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="9711f-197">Role a tela de configurações do interpretador tooLivy e, em seguida, clique em **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="9711f-197">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="9711f-198">![Reiniciar Olá Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "reiniciar Olá Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="9711f-198">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>
3. <span data-ttu-id="9711f-199">Execute uma célula de código de um notebook Zeppelin existente.</span><span class="sxs-lookup"><span data-stu-id="9711f-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="9711f-200">Isso cria uma nova sessão Livy no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="9711f-200">This creates a new Livy session in hello HDInsight cluster.</span></span>

## <span data-ttu-id="9711f-201"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="9711f-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="9711f-202">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9711f-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="9711f-203">Cenários</span><span class="sxs-lookup"><span data-stu-id="9711f-203">Scenarios</span></span>
* [<span data-ttu-id="9711f-204">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="9711f-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="9711f-205">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="9711f-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="9711f-206">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="9711f-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="9711f-207">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="9711f-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="9711f-208">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9711f-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="9711f-209">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="9711f-209">Create and run applications</span></span>
* [<span data-ttu-id="9711f-210">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="9711f-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="9711f-211">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="9711f-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="9711f-212">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="9711f-212">Tools and extensions</span></span>
* [<span data-ttu-id="9711f-213">Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar maiores Spark Scala aplicativos</span><span class="sxs-lookup"><span data-stu-id="9711f-213">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="9711f-214">Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente</span><span class="sxs-lookup"><span data-stu-id="9711f-214">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="9711f-215">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="9711f-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="9711f-216">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="9711f-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="9711f-217">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="9711f-217">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="9711f-218">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="9711f-218">Manage resources</span></span>
* [<span data-ttu-id="9711f-219">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="9711f-219">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="9711f-220">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9711f-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







