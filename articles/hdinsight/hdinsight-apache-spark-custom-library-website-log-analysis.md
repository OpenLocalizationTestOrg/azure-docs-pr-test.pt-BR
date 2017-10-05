---
title: "Analisar logs de sites com bibliotecas de Python no Spark – Azure | Microsoft Docs"
description: Este notebook demonstra como analisar dados de log usando uma biblioteca personalizada com o Spark no Azure HDInsight.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2a028beb1e9eae89d32238e61b6f67c4c059a94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="29ba0-103">Analisar logs do site usando uma biblioteca personalizada do Python com cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="29ba0-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="29ba0-104">Este notebook demonstra como analisar dados de log usando uma biblioteca personalizada com o Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="29ba0-104">This notebook demonstrates how to analyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="29ba0-105">A biblioteca personalizada que usamos é uma biblioteca Python chamada **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="29ba0-105">The custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="29ba0-106">Este tutorial também está disponível como um notebook Jupyter em um cluster do Spark (Linux) que você pode criar no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="29ba0-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="29ba0-107">A experiência de bloco de anotações permite executar os trechos de código Python no próprio bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="29ba0-107">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="29ba0-108">Para executar o tutorial de dentro de um notebook, crie um cluster Spark, inicie um notebook do Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`) e, em seguida, execute o notebook **Analisar logs com o Spark usando uma library.ipynb** personalizada na pasta **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="29ba0-108">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Analyze logs with Spark using a custom library.ipynb** under the **PySpark** folder.</span></span>
>
>

<span data-ttu-id="29ba0-109">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="29ba0-109">**Prerequisites:**</span></span>

<span data-ttu-id="29ba0-110">Você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="29ba0-110">You must have the following:</span></span>

* <span data-ttu-id="29ba0-111">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="29ba0-111">An Azure subscription.</span></span> <span data-ttu-id="29ba0-112">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="29ba0-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="29ba0-113">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="29ba0-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="29ba0-114">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="29ba0-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="29ba0-115">Salvar dados brutos como RDD</span><span class="sxs-lookup"><span data-stu-id="29ba0-115">Save raw data as an RDD</span></span>
<span data-ttu-id="29ba0-116">Nesta seção, usamos o notebook [Jupyter](https://jupyter.org) associado a um cluster do Apache Spark no HDInsight para executar trabalhos que processam dados brutos de exemplo e os salvam como uma tabela Hive.</span><span class="sxs-lookup"><span data-stu-id="29ba0-116">In this section, we use the [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight to run jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="29ba0-117">Os dados de exemplo são um arquivo .csv (hvac.csv) disponível em todos os clusters por padrão.</span><span class="sxs-lookup"><span data-stu-id="29ba0-117">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="29ba0-118">Depois que os dados são salvos como uma tabela Hive, na próxima seção, vamos nos conectar à tabela Hive usando ferramentas de BI como Power BI e Tableau.</span><span class="sxs-lookup"><span data-stu-id="29ba0-118">Once your data is saved as a Hive table, in the next section we will connect to the Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="29ba0-119">No [portal do Azure](https://portal.azure.com/), no quadro inicial, clique no bloco do cluster Spark (se você o tiver fixado no quadro inicial).</span><span class="sxs-lookup"><span data-stu-id="29ba0-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="29ba0-120">Você também pode navegar até o cluster em **Procurar Tudo** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="29ba0-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="29ba0-121">Na folha do cluster Spark, clique em **Painel do Cluster** e em **Notebook Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="29ba0-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="29ba0-122">Se você receber uma solicitação, insira as credenciais de administrador para o cluster.</span><span class="sxs-lookup"><span data-stu-id="29ba0-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="29ba0-123">Você também pode acessar o Bloco de Notas Jupyter de seu cluster abrindo a seguinte URL no navegador.</span><span class="sxs-lookup"><span data-stu-id="29ba0-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="29ba0-124">Substitua **CLUSTERNAME** pelo nome do cluster:</span><span class="sxs-lookup"><span data-stu-id="29ba0-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="29ba0-125">Crie um novo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="29ba0-125">Create a new notebook.</span></span> <span data-ttu-id="29ba0-126">Clique em **Novo** e em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="29ba0-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="29ba0-127">![Criar um novo bloco de anotações do Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Criar um novo bloco de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="29ba0-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="29ba0-128">Um novo bloco de anotações é criado e aberto com o nome Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="29ba0-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="29ba0-129">Clique no nome do bloco de anotações na parte superior e digite um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="29ba0-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="29ba0-130">![Fornecer um nome para o bloco de anotações](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Fornecer um nome para o bloco de anotações")</span><span class="sxs-lookup"><span data-stu-id="29ba0-130">![Provide a name for the notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for the notebook")</span></span>
5. <span data-ttu-id="29ba0-131">Por ter criado um notebook usando o kernel PySpark, não será necessário criar nenhum contexto explicitamente.</span><span class="sxs-lookup"><span data-stu-id="29ba0-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="29ba0-132">Os contextos do Spark e do Hive serão criados automaticamente para você ao executar a primeira célula do código.</span><span class="sxs-lookup"><span data-stu-id="29ba0-132">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="29ba0-133">Você pode começar importando os tipos que são obrigatórios para este cenário.</span><span class="sxs-lookup"><span data-stu-id="29ba0-133">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="29ba0-134">Cole o trecho a seguir em uma célula vazia e, em seguida, pressione **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="29ba0-134">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="29ba0-135">Crie um RDD usando os dados de log de exemplo já disponíveis no cluster.</span><span class="sxs-lookup"><span data-stu-id="29ba0-135">Create an RDD using the sample log data already available on the cluster.</span></span> <span data-ttu-id="29ba0-136">Você pode acessar os dados na conta de armazenamento padrão associada ao cluster em **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="29ba0-136">You can access the data in the default storage account associated with the cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="29ba0-137">Recupere um log de exemplo definido para verificar se a etapa anterior foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="29ba0-137">Retrieve a sample log set to verify that the previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="29ba0-138">Você deverá ver um resultado semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="29ba0-138">You should see an output similar to the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="29ba0-139">Analise os dados de log usando uma biblioteca Python personalizada</span><span class="sxs-lookup"><span data-stu-id="29ba0-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="29ba0-140">Na saída acima, as primeiras linhas incluem as informações de cabeçalho, e cada linha restante coincide com o esquema descrito naquele cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="29ba0-140">In the output above, the first couple lines include the header information and each remaining line matches the schema described in that header.</span></span> <span data-ttu-id="29ba0-141">Analisar esses logs pode ser complicado.</span><span class="sxs-lookup"><span data-stu-id="29ba0-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="29ba0-142">Então, usamos uma biblioteca personalizada do Python (**iislogparser.py**) que torna a análise desses logs muito mais fácil.</span><span class="sxs-lookup"><span data-stu-id="29ba0-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="29ba0-143">Por padrão, essa biblioteca é incluída com o cluster do Spark no HDInsight em **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="29ba0-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="29ba0-144">No entanto, essa biblioteca não está no `PYTHONPATH`, então não podemos usá-la com uma instrução de importação como `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="29ba0-144">However, this library is not in the `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="29ba0-145">Para usar essa biblioteca, devemos distribuí-la para todos os nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="29ba0-145">To use this library, we must distribute it to all the worker nodes.</span></span> <span data-ttu-id="29ba0-146">Execute o trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="29ba0-146">Run the following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="29ba0-147">O `iislogparser` fornece uma função `parse_log_line` que retorna `None` se uma linha do log for uma linha de cabeçalho, e retorna uma instância da classe `LogLine` se encontrar uma linha do log.</span><span class="sxs-lookup"><span data-stu-id="29ba0-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of the `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="29ba0-148">Use a classe `LogLine` para extrair somente as linhas do log do RDD:</span><span class="sxs-lookup"><span data-stu-id="29ba0-148">Use the `LogLine` class to extract only the log lines from the RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="29ba0-149">Recupere algumas linhas de log extraídas para verificar se a etapa foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="29ba0-149">Retrieve a couple of extracted log lines to verify that the step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="29ba0-150">A saída deverá ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="29ba0-150">The output should be similar to the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="29ba0-151">A classe `LogLine`, por sua vez, tem alguns métodos úteis, como `is_error()`, que retorna se uma entrada de log tem um código de erro.</span><span class="sxs-lookup"><span data-stu-id="29ba0-151">The `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="29ba0-152">Use isso para calcular o número de erros nas linhas de log extraídas e então registre todos os erros em um arquivo diferente.</span><span class="sxs-lookup"><span data-stu-id="29ba0-152">Use this to compute the number of errors in the extracted log lines, and then log all the errors to a different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="29ba0-153">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="29ba0-153">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="29ba0-154">Você também pode usar **Matplotlib** para construir uma visualização dos dados.</span><span class="sxs-lookup"><span data-stu-id="29ba0-154">You can also use **Matplotlib** to construct a visualization of the data.</span></span> <span data-ttu-id="29ba0-155">Por exemplo, se você quiser isolar a causa de solicitações executadas por um longo tempo, talvez queira localizar os arquivos que, em média, levam mais tempo para atender.</span><span class="sxs-lookup"><span data-stu-id="29ba0-155">For example, if you want to isolate the cause of requests that run for a long time, you might want to find the files that take the most time to serve on average.</span></span>
   <span data-ttu-id="29ba0-156">O trecho a seguir recupera os 25 principais recursos que levaram mais tempo para atender uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="29ba0-156">The snippet below retrieves the top 25 resources that took most time to serve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="29ba0-157">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="29ba0-157">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. <span data-ttu-id="29ba0-158">Você também pode apresentar essas informações na forma de plotagem.</span><span class="sxs-lookup"><span data-stu-id="29ba0-158">You can also present this information in the form of plot.</span></span> <span data-ttu-id="29ba0-159">Como uma primeira etapa para criar um gráfico, criaremos uma tabela **AverageTime**temporária.</span><span class="sxs-lookup"><span data-stu-id="29ba0-159">As a first step to create a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="29ba0-160">A tabela agrupa os logs por hora para ver se houve quaisquer picos incomuns de latência em um determinado momento.</span><span class="sxs-lookup"><span data-stu-id="29ba0-160">The table groups the logs by time to see if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="29ba0-161">Você pode então executar a seguinte consulta SQL para obter todos os registros da tabela **AverageTime** .</span><span class="sxs-lookup"><span data-stu-id="29ba0-161">You can then run the following SQL query to get all the records in the **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="29ba0-162">A mágica do `%%sql` seguido pelo `-o averagetime` assegura que a saída da consulta seja mantida localmente no servidor Jupyter (normalmente o nó principal do cluster).</span><span class="sxs-lookup"><span data-stu-id="29ba0-162">The `%%sql` magic followed by `-o averagetime` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="29ba0-163">A saída é mantida como uma estrutura de dados [Pandas](http://pandas.pydata.org/) com o nome especificado **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="29ba0-163">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **averagetime**.</span></span>

   <span data-ttu-id="29ba0-164">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="29ba0-164">You should see an output like the following:</span></span>

   <span data-ttu-id="29ba0-165">![Saída da consulta SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Saída da consulta SQL")</span><span class="sxs-lookup"><span data-stu-id="29ba0-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="29ba0-166">Para obter mais informações sobre a palavra mágica `%%sql`, consulte [Parâmetros com suporte na palavra mágica %%sql](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="29ba0-166">For more information about the `%%sql` magic, see [Parameters supported with the %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="29ba0-167">Agora você pode usar Matplotlib, uma biblioteca usada para construir a visualização de dados para criar um gráfico.</span><span class="sxs-lookup"><span data-stu-id="29ba0-167">You can now use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="29ba0-168">Como o gráfico deve ser criado da estrutura de dados **averagetime** mantida localmente, o trecho de código deve começar com a mágica `%%local`.</span><span class="sxs-lookup"><span data-stu-id="29ba0-168">Because the plot must be created from the locally persisted **averagetime** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="29ba0-169">Isso garante que o código seja executado localmente no servidor do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="29ba0-169">This ensures that the code is run locally on the Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="29ba0-170">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="29ba0-170">You should see an output like the following:</span></span>

   <span data-ttu-id="29ba0-171">![Saída de Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Saída de Matplotlib")</span><span class="sxs-lookup"><span data-stu-id="29ba0-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="29ba0-172">Depois de concluir a execução do aplicativo, você deve encerrar o notebook para liberar os recursos.</span><span class="sxs-lookup"><span data-stu-id="29ba0-172">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="29ba0-173">Para isso, no menu **Arquivo** do bloco de anotações, clique em **Fechar e Interromper**.</span><span class="sxs-lookup"><span data-stu-id="29ba0-173">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="29ba0-174">Isso desligará e fechará o bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="29ba0-174">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="29ba0-175"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="29ba0-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="29ba0-176">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="29ba0-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="29ba0-177">Cenários</span><span class="sxs-lookup"><span data-stu-id="29ba0-177">Scenarios</span></span>
* [<span data-ttu-id="29ba0-178">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="29ba0-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="29ba0-179">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="29ba0-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="29ba0-180">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para prever resultados da inspeção de alimentos</span><span class="sxs-lookup"><span data-stu-id="29ba0-180">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="29ba0-181">Streaming Spark: use o Spark no HDInsight para a criação de aplicativos streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="29ba0-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="29ba0-182">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="29ba0-182">Create and run applications</span></span>
* [<span data-ttu-id="29ba0-183">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="29ba0-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="29ba0-184">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="29ba0-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="29ba0-185">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="29ba0-185">Tools and extensions</span></span>
* [<span data-ttu-id="29ba0-186">Use o Plug-in de Ferramentas do HDInsight para IntelliJ IDEA para criar e enviar aplicativos Spark Scala</span><span class="sxs-lookup"><span data-stu-id="29ba0-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="29ba0-187">Usar o plug-in de Ferramentas do HDInsight para depurar aplicativos Spark remotamente</span><span class="sxs-lookup"><span data-stu-id="29ba0-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="29ba0-188">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="29ba0-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="29ba0-189">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="29ba0-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="29ba0-190">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="29ba0-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="29ba0-191">Instalar o Jupyter em seu computador e conectar-se a um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="29ba0-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="29ba0-192">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="29ba0-192">Manage resources</span></span>
* [<span data-ttu-id="29ba0-193">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="29ba0-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="29ba0-194">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="29ba0-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
