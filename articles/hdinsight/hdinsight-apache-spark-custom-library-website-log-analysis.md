---
title: logs de site aaaAnalyze com bibliotecas de Python no Spark - Azure | Microsoft Docs
description: "Este bloco de anotações demonstra como tooanalyze dados de log usando uma biblioteca personalizada com Spark no HDInsight do Azure."
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
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="b4c28-103">Analisar logs do site usando uma biblioteca personalizada do Python com cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4c28-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="b4c28-104">Este bloco de anotações demonstra como tooanalyze dados de log usando uma biblioteca personalizada com Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b4c28-104">This notebook demonstrates how tooanalyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="b4c28-105">podemos usar a biblioteca personalizada de saudação é uma biblioteca de Python chamada **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="b4c28-105">hello custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="b4c28-106">Este tutorial também está disponível como um notebook Jupyter em um cluster do Spark (Linux) que você pode criar no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b4c28-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="b4c28-107">experiência de notebook Olá permite executar trechos de Python de saudação do bloco de anotações de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="b4c28-107">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="b4c28-108">tutorial de saudação tooperform de dentro de um bloco de anotações, criar um cluster Spark, inicie um bloco de anotações do Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), e, em seguida, execute notebook Olá **analisar logs com Spark usando um library.ipynb personalizado** em Olá  **PySpark** pasta.</span><span class="sxs-lookup"><span data-stu-id="b4c28-108">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Analyze logs with Spark using a custom library.ipynb** under hello **PySpark** folder.</span></span>
>
>

<span data-ttu-id="b4c28-109">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="b4c28-109">**Prerequisites:**</span></span>

<span data-ttu-id="b4c28-110">Você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="b4c28-110">You must have hello following:</span></span>

* <span data-ttu-id="b4c28-111">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c28-111">An Azure subscription.</span></span> <span data-ttu-id="b4c28-112">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b4c28-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="b4c28-113">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b4c28-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b4c28-114">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b4c28-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="b4c28-115">Salvar dados brutos como RDD</span><span class="sxs-lookup"><span data-stu-id="b4c28-115">Save raw data as an RDD</span></span>
<span data-ttu-id="b4c28-116">Nesta seção, usamos Olá [Jupyter](https://jupyter.org) notebook associado a um cluster do Apache Spark no HDInsight toorun trabalhos que processam os dados brutos de exemplo e salvá-lo como uma tabela de Hive.</span><span class="sxs-lookup"><span data-stu-id="b4c28-116">In this section, we use hello [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight toorun jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="b4c28-117">dados de exemplo Hello são um arquivo. csv (hvac.csv) disponível em todos os clusters por padrão.</span><span class="sxs-lookup"><span data-stu-id="b4c28-117">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="b4c28-118">Depois que seus dados é salvo como uma tabela Hive, nós conectará toohello tabela de Hive usando ferramentas de BI como Power BI e Tableau na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="b4c28-118">Once your data is saved as a Hive table, in hello next section we will connect toohello Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="b4c28-119">De saudação [portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial).</span><span class="sxs-lookup"><span data-stu-id="b4c28-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="b4c28-120">Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b4c28-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="b4c28-121">Na folha de cluster do Spark hello, clique em **painel Cluster**e, em seguida, clique em **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="b4c28-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="b4c28-122">Se solicitado, insira as credenciais de administrador de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b4c28-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b4c28-123">Você também poderá atingir Olá anotações do Jupyter para o cluster por Olá abrir URL a seguir em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="b4c28-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="b4c28-124">Substituir **CLUSTERNAME** com nome de saudação do cluster:</span><span class="sxs-lookup"><span data-stu-id="b4c28-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="b4c28-125">Crie um novo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="b4c28-125">Create a new notebook.</span></span> <span data-ttu-id="b4c28-126">Clique em **Novo** e em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="b4c28-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="b4c28-127">![Criar um novo bloco de anotações do Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Criar um novo bloco de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="b4c28-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="b4c28-128">Um novo bloco de anotações é criado e aberto com o nome hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="b4c28-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="b4c28-129">Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="b4c28-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="b4c28-130">![Forneça um nome para o bloco de anotações de saudação](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "forneça um nome para o bloco de anotações de saudação")</span><span class="sxs-lookup"><span data-stu-id="b4c28-130">![Provide a name for hello notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for hello notebook")</span></span>
5. <span data-ttu-id="b4c28-131">Como você criou um bloco de anotações com o hello PySpark kernel, não é necessário toocreate qualquer contextos explicitamente.</span><span class="sxs-lookup"><span data-stu-id="b4c28-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="b4c28-132">contextos de Spark e Hive Olá serão automaticamente criados para você quando você executar a primeira célula de código hello.</span><span class="sxs-lookup"><span data-stu-id="b4c28-132">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="b4c28-133">Você pode começar importando tipos Olá que são necessários para este cenário.</span><span class="sxs-lookup"><span data-stu-id="b4c28-133">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="b4c28-134">Cole Olá seguindo o trecho de código em uma célula vazia e, em seguida, pressione **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b4c28-134">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="b4c28-135">Crie um RDD usando dados de log de exemplo hello já disponíveis no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4c28-135">Create an RDD using hello sample log data already available on hello cluster.</span></span> <span data-ttu-id="b4c28-136">Você pode acessar dados Olá na conta de armazenamento padrão de saudação associada Olá cluster em **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="b4c28-136">You can access hello data in hello default storage account associated with hello cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="b4c28-137">Recupere um tooverify de conjunto de log de exemplo que Olá a etapa anterior foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="b4c28-137">Retrieve a sample log set tooverify that hello previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="b4c28-138">Você verá uma saída semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4c28-138">You should see an output similar toohello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="b4c28-139">Analise os dados de log usando uma biblioteca Python personalizada</span><span class="sxs-lookup"><span data-stu-id="b4c28-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="b4c28-140">Na saída de hello acima, primeiras linhas de alguns Olá incluem informações de cabeçalho hello e corresponde a cada linha restante esquema Olá descrita nesse cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="b4c28-140">In hello output above, hello first couple lines include hello header information and each remaining line matches hello schema described in that header.</span></span> <span data-ttu-id="b4c28-141">Analisar esses logs pode ser complicado.</span><span class="sxs-lookup"><span data-stu-id="b4c28-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="b4c28-142">Então, usamos uma biblioteca personalizada do Python (**iislogparser.py**) que torna a análise desses logs muito mais fácil.</span><span class="sxs-lookup"><span data-stu-id="b4c28-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="b4c28-143">Por padrão, essa biblioteca é incluída com o cluster do Spark no HDInsight em **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="b4c28-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="b4c28-144">No entanto, essa biblioteca não fica Olá `PYTHONPATH` para nós não pode usá-lo usando uma instrução de importação como `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="b4c28-144">However, this library is not in hello `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="b4c28-145">toouse nessa biblioteca, é necessário distribuir nós de trabalho tooall hello.</span><span class="sxs-lookup"><span data-stu-id="b4c28-145">toouse this library, we must distribute it tooall hello worker nodes.</span></span> <span data-ttu-id="b4c28-146">Execute Olá trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4c28-146">Run hello following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="b4c28-147">`iislogparser`Fornece uma função `parse_log_line` que retorna `None` se uma linha de log é uma linha de cabeçalho e retorna uma instância da saudação `LogLine` classe se ele encontrar uma linha de log.</span><span class="sxs-lookup"><span data-stu-id="b4c28-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of hello `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="b4c28-148">Olá Use `LogLine` classe tooextract Olá apenas linhas de log de saudação RDD:</span><span class="sxs-lookup"><span data-stu-id="b4c28-148">Use hello `LogLine` class tooextract only hello log lines from hello RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="b4c28-149">Recupere algumas linhas de log extraídos tooverify que Olá etapa foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="b4c28-149">Retrieve a couple of extracted log lines tooverify that hello step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="b4c28-150">saída de Hello deve ser a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="b4c28-150">hello output should be similar toohello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="b4c28-151">Olá `LogLine` classe, por sua vez, tem alguns métodos úteis, como `is_error()`, que retorna se uma entrada de log tem um código de erro.</span><span class="sxs-lookup"><span data-stu-id="b4c28-151">hello `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="b4c28-152">Use esse número de saudação de toocompute de erros nas linhas de log Olá extraído, em seguida, arquivo de log e todos os Olá erros tooa diferentes.</span><span class="sxs-lookup"><span data-stu-id="b4c28-152">Use this toocompute hello number of errors in hello extracted log lines, and then log all hello errors tooa different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="b4c28-153">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="b4c28-153">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="b4c28-154">Você também pode usar **Matplotlib** tooconstruct uma visualização de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4c28-154">You can also use **Matplotlib** tooconstruct a visualization of hello data.</span></span> <span data-ttu-id="b4c28-155">Por exemplo, se você quiser tooisolate causa de saudação de solicitações que são executados por um longo tempo, convém arquivos Olá toofind levar hello mais tooserve de tempo em média.</span><span class="sxs-lookup"><span data-stu-id="b4c28-155">For example, if you want tooisolate hello cause of requests that run for a long time, you might want toofind hello files that take hello most time tooserve on average.</span></span>
   <span data-ttu-id="b4c28-156">trecho de saudação abaixo recupera Olá superior 25 recursos que levou a maioria dos tooserve de tempo uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="b4c28-156">hello snippet below retrieves hello top 25 resources that took most time tooserve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="b4c28-157">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="b4c28-157">You should see an output like hello following:</span></span>

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
5. <span data-ttu-id="b4c28-158">Você também pode apresentar essas informações no formulário de saudação de plotagem.</span><span class="sxs-lookup"><span data-stu-id="b4c28-158">You can also present this information in hello form of plot.</span></span> <span data-ttu-id="b4c28-159">Como uma primeira toocreate etapa um gráfico, vamos primeiro criar uma tabela temporária **AverageTime**.</span><span class="sxs-lookup"><span data-stu-id="b4c28-159">As a first step toocreate a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="b4c28-160">saudação de grupos de tabela Olá registra por toosee tempo se houver qualquer picos de latência incomum em um determinado momento.</span><span class="sxs-lookup"><span data-stu-id="b4c28-160">hello table groups hello logs by time toosee if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="b4c28-161">Você pode executar Olá tooget de consulta SQL a seguir todos os registros de saudação em Olá **AverageTime** tabela.</span><span class="sxs-lookup"><span data-stu-id="b4c28-161">You can then run hello following SQL query tooget all hello records in hello **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="b4c28-162">Olá `%%sql` mágico seguido `-o averagetime` garante que saída Olá de consulta de saudação é persistentes localmente no servidor de Jupyter de saudação (normalmente Olá nó principal do cluster Olá).</span><span class="sxs-lookup"><span data-stu-id="b4c28-162">hello `%%sql` magic followed by `-o averagetime` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="b4c28-163">saída de Hello é mantida como um [Pandas](http://pandas.pydata.org/) dataframe com hello especificado nome **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="b4c28-163">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **averagetime**.</span></span>

   <span data-ttu-id="b4c28-164">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="b4c28-164">You should see an output like hello following:</span></span>

   <span data-ttu-id="b4c28-165">![Saída da consulta SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Saída da consulta SQL")</span><span class="sxs-lookup"><span data-stu-id="b4c28-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="b4c28-166">Para obter mais informações sobre Olá `%%sql` magic, consulte [suporte para parâmetros com Olá % % sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="b4c28-166">For more information about hello `%%sql` magic, see [Parameters supported with hello %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="b4c28-167">Agora você pode usar Matplotlib, uma biblioteca usada tooconstruct visualização de dados, toocreate um gráfico.</span><span class="sxs-lookup"><span data-stu-id="b4c28-167">You can now use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="b4c28-168">Porque plotagem Olá deve ser criada de saudação localmente persistente **averagetime** dataframe, o trecho de código Olá deve começar com hello `%%local` mágica.</span><span class="sxs-lookup"><span data-stu-id="b4c28-168">Because hello plot must be created from hello locally persisted **averagetime** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="b4c28-169">Isso garante que o código de Olá é executado localmente no servidor do Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="b4c28-169">This ensures that hello code is run locally on hello Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="b4c28-170">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="b4c28-170">You should see an output like hello following:</span></span>

   <span data-ttu-id="b4c28-171">![Saída de Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Saída de Matplotlib")</span><span class="sxs-lookup"><span data-stu-id="b4c28-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="b4c28-172">Depois de terminar de executar o aplicativo hello, você deverá recursos de saudação do desligamento Olá notebook toorelease.</span><span class="sxs-lookup"><span data-stu-id="b4c28-172">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="b4c28-173">toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**.</span><span class="sxs-lookup"><span data-stu-id="b4c28-173">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="b4c28-174">Esta desligará e notebook Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="b4c28-174">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="b4c28-175"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="b4c28-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="b4c28-176">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4c28-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="b4c28-177">Cenários</span><span class="sxs-lookup"><span data-stu-id="b4c28-177">Scenarios</span></span>
* [<span data-ttu-id="b4c28-178">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="b4c28-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b4c28-179">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="b4c28-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b4c28-180">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="b4c28-180">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b4c28-181">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="b4c28-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b4c28-182">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="b4c28-182">Create and run applications</span></span>
* [<span data-ttu-id="b4c28-183">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="b4c28-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b4c28-184">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="b4c28-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b4c28-185">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="b4c28-185">Tools and extensions</span></span>
* [<span data-ttu-id="b4c28-186">Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos</span><span class="sxs-lookup"><span data-stu-id="b4c28-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b4c28-187">Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente</span><span class="sxs-lookup"><span data-stu-id="b4c28-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b4c28-188">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4c28-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b4c28-189">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4c28-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b4c28-190">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="b4c28-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b4c28-191">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b4c28-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b4c28-192">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="b4c28-192">Manage resources</span></span>
* [<span data-ttu-id="b4c28-193">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="b4c28-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b4c28-194">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4c28-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
