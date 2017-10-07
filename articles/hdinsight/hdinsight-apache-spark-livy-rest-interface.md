---
title: aaaUse Livy Spark toosubmit trabalhos tooSpark cluster HDInsight do Azure | Microsoft Docs
description: Saiba como toouse Apache Spark REST API toosubmit Spark trabalhos de cluster do Azure HDInsight tooan remotamente.
keywords: api rest do apache spark, spark livy
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a><span data-ttu-id="e9e30-104">Use a API de REST do Apache Spark toosubmit trabalhos remotos tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="e9e30-104">Use Apache Spark REST API toosubmit remote jobs tooan HDInsight Spark cluster</span></span>

<span data-ttu-id="e9e30-105">Saiba como toouse Livy, Olá Apache Spark REST API, que é usado toosubmit remoto trabalhos de cluster do Azure HDInsight Spark tooan.</span><span class="sxs-lookup"><span data-stu-id="e9e30-105">Learn how toouse Livy, hello Apache Spark REST API, which is used toosubmit remote jobs tooan Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="e9e30-106">Para obter a documentação detalhada, confira [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="e9e30-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="e9e30-107">Você pode usar os shells de Spark Livy toorun interativos ou enviar lote toobe de trabalhos executado em Spark.</span><span class="sxs-lookup"><span data-stu-id="e9e30-107">You can use Livy toorun interactive Spark shells or submit batch jobs toobe run on Spark.</span></span> <span data-ttu-id="e9e30-108">Este artigo aborda usando trabalhos de lote Livy toosubmit.</span><span class="sxs-lookup"><span data-stu-id="e9e30-108">This article talks about using Livy toosubmit batch jobs.</span></span> <span data-ttu-id="e9e30-109">trechos de código Olá neste artigo usam toomake ondulação de ponto de extremidade Livy Spark toohello de chamadas de API REST.</span><span class="sxs-lookup"><span data-stu-id="e9e30-109">hello snippets in this article use cURL toomake REST API calls toohello Livy Spark endpoint.</span></span>

<span data-ttu-id="e9e30-110">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="e9e30-110">**Prerequisites:**</span></span>

* <span data-ttu-id="e9e30-111">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e9e30-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e9e30-112">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e9e30-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="e9e30-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="e9e30-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="e9e30-114">Este artigo usa ondulação toodemonstrate como toomake API REST chama em relação a um cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="e9e30-114">This article uses cURL toodemonstrate how toomake REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="e9e30-115">Enviar um trabalho em lotes do Livy Spark</span><span class="sxs-lookup"><span data-stu-id="e9e30-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="e9e30-116">Antes de enviar um trabalho em lotes, você deve carregar Olá aplicativo jar no armazenamento de cluster Olá associado Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="e9e30-116">Before you submit a batch job, you must upload hello application jar on hello cluster storage associated with hello cluster.</span></span> <span data-ttu-id="e9e30-117">Você pode usar [ **AzCopy**](../storage/common/storage-use-azcopy.md), um utilitário de linha de comando, toodo para.</span><span class="sxs-lookup"><span data-stu-id="e9e30-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, toodo so.</span></span> <span data-ttu-id="e9e30-118">Há vários outros clientes que você pode usar dados tooupload.</span><span class="sxs-lookup"><span data-stu-id="e9e30-118">There are various other clients you can use tooupload data.</span></span> <span data-ttu-id="e9e30-119">É possível saber mais sobre eles em [Carregar dados para trabalhos do Hadoop no HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="e9e30-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="e9e30-120">**Exemplos**:</span><span class="sxs-lookup"><span data-stu-id="e9e30-120">**Examples**:</span></span>

* <span data-ttu-id="e9e30-121">Se o arquivo jar do hello está no armazenamento de cluster da saudação (WASB)</span><span class="sxs-lookup"><span data-stu-id="e9e30-121">If hello jar file is on hello cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="e9e30-122">Se você quiser toopass Olá o nome do arquivo jar e Olá classname como parte de um arquivo de entrada (neste exemplo, txt)</span><span class="sxs-lookup"><span data-stu-id="e9e30-122">If you want toopass hello jar filename and hello classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a><span data-ttu-id="e9e30-123">Obter informações sobre lotes Livy Spark em execução no cluster Olá</span><span class="sxs-lookup"><span data-stu-id="e9e30-123">Get information on Livy Spark batches running on hello cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="e9e30-124">**Exemplos**:</span><span class="sxs-lookup"><span data-stu-id="e9e30-124">**Examples**:</span></span>

* <span data-ttu-id="e9e30-125">Se você quiser que todos os lotes de Livy Spark Olá em execução no cluster Olá tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="e9e30-125">If you want tooretrieve all hello Livy Spark batches running on hello cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="e9e30-126">Se você quiser tooretrieve um lote específico com um determinado batchId</span><span class="sxs-lookup"><span data-stu-id="e9e30-126">If you want tooretrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="e9e30-127">Excluir um trabalho em lotes do Livy Spark</span><span class="sxs-lookup"><span data-stu-id="e9e30-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="e9e30-128">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="e9e30-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="e9e30-129">Livy Spark e alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="e9e30-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="e9e30-130">Livy fornece alta disponibilidade para trabalhos Spark em execução no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9e30-130">Livy provides high-availability for Spark jobs running on hello cluster.</span></span> <span data-ttu-id="e9e30-131">Aqui estão alguns exemplos.</span><span class="sxs-lookup"><span data-stu-id="e9e30-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="e9e30-132">Se Olá serviço Livy falhar depois de ter enviado um trabalho remotamente tooa Spark cluster, hello trabalho continua toorun no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9e30-132">If hello Livy service goes down after you have submitted a job remotely tooa Spark cluster, hello job continues toorun in hello background.</span></span> <span data-ttu-id="e9e30-133">Quando Livy é fazer backup, restaura os status de saudação do trabalho hello e relatórios-o novamente.</span><span class="sxs-lookup"><span data-stu-id="e9e30-133">When Livy is back up, it restores hello status of hello job and reports it back.</span></span>
* <span data-ttu-id="e9e30-134">Blocos de anotações do Jupyter para HDInsight são ativados pelas Livy em Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="e9e30-134">Jupyter notebooks for HDInsight are powered by Livy in hello backend.</span></span> <span data-ttu-id="e9e30-135">Se um bloco de anotações estiver executando um trabalho Spark e Olá serviço Livy é reiniciado, notebook Olá continua células de código Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="e9e30-135">If a notebook is running a Spark job and hello Livy service gets restarted, hello notebook continues toorun hello code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="e9e30-136">Mostrar um exemplo</span><span class="sxs-lookup"><span data-stu-id="e9e30-136">Show me an example</span></span>
<span data-ttu-id="e9e30-137">Nesta seção, podemos examinar o trabalho do exemplos toouse Livy Spark toosubmit em lotes, monitorar o progresso de saudação do trabalho hello e, em seguida, excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="e9e30-137">In this section, we look at examples toouse Livy Spark toosubmit batch job, monitor hello progress of hello job, and then delete it.</span></span> <span data-ttu-id="e9e30-138">Olá, usamos neste exemplo de aplicativo é hello um desenvolvidos no artigo Olá [criar um aplicativo de Scala autônomo e toorun no cluster HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="e9e30-138">hello application we use in this example is hello one developed in hello article [Create a standalone Scala application and toorun on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="e9e30-139">etapas de saudação aqui supõem que:</span><span class="sxs-lookup"><span data-stu-id="e9e30-139">hello steps here assume that:</span></span>

* <span data-ttu-id="e9e30-140">Você já copiou Olá aplicativo jar toohello armazenamento conta associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="e9e30-140">You have already copied over hello application jar toohello storage account associated with hello cluster.</span></span>
* <span data-ttu-id="e9e30-141">Você tem ondulação instalada no computador de saudação em que você estiver experimentando essas etapas.</span><span class="sxs-lookup"><span data-stu-id="e9e30-141">You have CuRL installed on hello computer where you are trying these steps.</span></span>

<span data-ttu-id="e9e30-142">Execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9e30-142">Perform hello following steps:</span></span>

1. <span data-ttu-id="e9e30-143">Vamos primeiro verificar se Livy Spark está em execução no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9e30-143">Let us first verify that Livy Spark is running on hello cluster.</span></span> <span data-ttu-id="e9e30-144">Podemos fazer isso obtendo uma lista de lotes em execução.</span><span class="sxs-lookup"><span data-stu-id="e9e30-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="e9e30-145">Se você estiver executando um trabalho usando Livy para Olá primeira vez, a saída de hello deve retornar zero.</span><span class="sxs-lookup"><span data-stu-id="e9e30-145">If you are running a job using Livy for hello first time, hello output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="e9e30-146">Você deve obter um toohello semelhante saída trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9e30-146">You should get an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="e9e30-147">Observe como a última linha hello na saída de hello informa **total: 0**, que sugere sem lotes em execução.</span><span class="sxs-lookup"><span data-stu-id="e9e30-147">Notice how hello last line in hello output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="e9e30-148">Agora vamos enviar um trabalho em lotes.</span><span class="sxs-lookup"><span data-stu-id="e9e30-148">Let us now submit a batch job.</span></span> <span data-ttu-id="e9e30-149">saudação de trecho de código a seguir usa um nome do arquivo de entrada (txt) toopass Olá jar e o nome da classe hello como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e9e30-149">hello following snippet uses an input file (input.txt) toopass hello jar name and hello class name as parameters.</span></span> <span data-ttu-id="e9e30-150">Se você estiver executando essas etapas em um computador Windows, usar um arquivo de entrada é hello abordagem recomendada.</span><span class="sxs-lookup"><span data-stu-id="e9e30-150">If you are running these steps from a Windows computer, using an input file is hello recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="e9e30-151">Olá parâmetros no arquivo hello **txt** são definidas da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e9e30-151">hello parameters in hello file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="e9e30-152">Você verá um toohello semelhante saída trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9e30-152">You should see an output similar toohello  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="e9e30-153">Observe como a última linha hello de saída de hello informa **estado: iniciando**.</span><span class="sxs-lookup"><span data-stu-id="e9e30-153">Notice how hello last line of hello output says **state:starting**.</span></span> <span data-ttu-id="e9e30-154">Assim como, **id:0**.</span><span class="sxs-lookup"><span data-stu-id="e9e30-154">It also says, **id:0**.</span></span> <span data-ttu-id="e9e30-155">Aqui, **0** é a ID do lote hello.</span><span class="sxs-lookup"><span data-stu-id="e9e30-155">Here, **0** is hello batch ID.</span></span>

3. <span data-ttu-id="e9e30-156">Agora você pode recuperar o status Olá deste lote específico usando a ID do lote hello.</span><span class="sxs-lookup"><span data-stu-id="e9e30-156">You can now retrieve hello status of this specific batch using hello batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="e9e30-157">Você verá um toohello semelhante saída trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9e30-157">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="e9e30-158">Olá saída agora mostra **estado: êxito**, que sugere que o trabalho Olá foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="e9e30-158">hello output now shows **state:success**, which suggests that hello job was successfully completed.</span></span>

4. <span data-ttu-id="e9e30-159">Se você quiser, agora você pode excluir lote hello.</span><span class="sxs-lookup"><span data-stu-id="e9e30-159">If you want, you can now delete hello batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="e9e30-160">Você verá um toohello semelhante saída trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9e30-160">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="e9e30-161">Olá última linha da saída de hello mostra que esse lote Olá foi excluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="e9e30-161">hello last line of hello output shows that hello batch was successfully deleted.</span></span> <span data-ttu-id="e9e30-162">Excluir um trabalho, enquanto ele está em execução, também elimina trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="e9e30-162">Deleting a job, while it is running, also kills hello job.</span></span> <span data-ttu-id="e9e30-163">Se você excluir um trabalho que foi concluída com êxito ou caso contrário, ele exclui informações de trabalho Olá completamente.</span><span class="sxs-lookup"><span data-stu-id="e9e30-163">If you delete a job that has completed, successfully or otherwise, it deletes hello job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="e9e30-164">Uso do Livy Spark em clusters do HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="e9e30-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="e9e30-165">Cluster HDInsight 3.5, por padrão, desabilita o uso de arquivos de dados de exemplo do arquivo local caminhos tooaccess ou jars.</span><span class="sxs-lookup"><span data-stu-id="e9e30-165">HDInsight 3.5 cluster, by default, disables use of local file paths tooaccess sample data files or jars.</span></span> <span data-ttu-id="e9e30-166">Recomendamos que você Olá toouse `wasb://` caminho em vez disso, tooaccess jars ou dados de exemplo dos arquivos do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9e30-166">We encourage you toouse hello `wasb://` path instead tooaccess jars or sample data files from hello cluster.</span></span> <span data-ttu-id="e9e30-167">Se você quiser caminho local toouse, você deve atualizar a configuração do Ambari Olá adequadamente.</span><span class="sxs-lookup"><span data-stu-id="e9e30-167">If you do want toouse local path, you must update hello Ambari configuration accordingly.</span></span> <span data-ttu-id="e9e30-168">toodo para:</span><span class="sxs-lookup"><span data-stu-id="e9e30-168">toodo so:</span></span>

1. <span data-ttu-id="e9e30-169">Vá toohello Ambari portal para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e9e30-169">Go toohello Ambari portal for hello cluster.</span></span> <span data-ttu-id="e9e30-170">Saudação da interface do usuário do Ambari Web está disponível no seu cluster HDInsight no https://**CLUSTERNAME**. azurehdidnsight.net, onde CLUSTERNAME é o nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="e9e30-170">hello Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is hello name of your cluster.</span></span>

2. <span data-ttu-id="e9e30-171">De Olá barra de navegação esquerda, clique em **Livy**e, em seguida, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="e9e30-171">From hello left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="e9e30-172">Em **livy padrão** adicionar o nome da propriedade Olá `livy.file.local-dir-whitelist` e defina seu valor muito**"/"** se desejar que o sistema de toofile tooallow acesso completo.</span><span class="sxs-lookup"><span data-stu-id="e9e30-172">Under **livy-default** add hello property name `livy.file.local-dir-whitelist` and set it's value too**"/"** if you want tooallow full access toofile system.</span></span> <span data-ttu-id="e9e30-173">Se você quiser acessar o tooallow tooa somente diretório específico, forneça Olá caminho toothat diretório como valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9e30-173">If you want tooallow access only tooa specific directory, provide hello path toothat directory as hello value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="e9e30-174">Enviar trabalhos da Livy para um cluster em uma rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="e9e30-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="e9e30-175">Se você conectar tooan cluster HDInsight Spark de dentro de uma rede Virtual do Azure, você pode conectar-se diretamente tooLivy no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9e30-175">If you connect tooan HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect tooLivy on hello cluster.</span></span> <span data-ttu-id="e9e30-176">Nesse caso, Olá URL de ponto de extremidade Livy é `http://<IP address of hello headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="e9e30-176">In such a case, hello URL for Livy endpoint is `http://<IP address of hello headnode>:8998/batches`.</span></span> <span data-ttu-id="e9e30-177">Aqui, **8998** Olá porta na qual Livy é executado no nó principal do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e9e30-177">Here, **8998** is hello port on which Livy runs on hello cluster headnode.</span></span> <span data-ttu-id="e9e30-178">Para obter mais informações sobre como acessar serviços em portas não públicas, consulte [Portas usadas pelos serviços de Hadoop no HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="e9e30-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e9e30-179">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="e9e30-179">Troubleshooting</span></span>

<span data-ttu-id="e9e30-180">Aqui estão alguns problemas que você possa encontrar ao usar Livy para clusters de tooSpark de envio de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="e9e30-180">Here are some issues that you might run into while using Livy for remote job submission tooSpark clusters.</span></span>

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a><span data-ttu-id="e9e30-181">Não há suporte para o usar um jar externa de armazenamento adicional da saudação</span><span class="sxs-lookup"><span data-stu-id="e9e30-181">Using an external jar from hello additional storage is not supported</span></span>

<span data-ttu-id="e9e30-182">**Problema:** se seu trabalho Livy Spark referencia um jar externa Olá adicionais da conta de armazenamento associada Olá cluster, o trabalho de saudação falhar.</span><span class="sxs-lookup"><span data-stu-id="e9e30-182">**Problem:** If your Livy Spark job references an external jar from hello additional storage account associated with hello cluster, hello job fails.</span></span>

<span data-ttu-id="e9e30-183">**Resolução:** Certifique-se de que jar Olá deseja toouse está disponível no armazenamento padrão da saudação associado Olá cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e9e30-183">**Resolution:** Make sure that hello jar you want toouse is available in hello default storage associated with hello HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="e9e30-184">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="e9e30-184">Next step</span></span>

* [<span data-ttu-id="e9e30-185">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="e9e30-185">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e9e30-186">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e9e30-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

