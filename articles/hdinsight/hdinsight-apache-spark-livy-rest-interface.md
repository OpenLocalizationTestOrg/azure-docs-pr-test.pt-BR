---
title: Usar Livy Spark para enviar trabalhos para o cluster do Spark no Azure HDInsight | Microsoft Docs
description: Saiba como usar a API REST do Apache Spark para enviar trabalhos do Spark remotamente para um cluster do Azure HDInsight.
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
ms.openlocfilehash: e1a28d69bbf40ea3134a7899a0d2fe70e5fc9e71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-apache-spark-rest-api-to-submit-remote-jobs-to-an-hdinsight-spark-cluster"></a><span data-ttu-id="f2457-104">Use a API REST do Apache Spark para enviar trabalhos remotos para um cluster do HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="f2457-104">Use Apache Spark REST API to submit remote jobs to an HDInsight Spark cluster</span></span>

<span data-ttu-id="f2457-105">Saiba como usar Livy, a API REST do Apache Spark, que é usado para enviar trabalhos remotos para um cluster do Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f2457-105">Learn how to use Livy, the Apache Spark REST API, which is used to submit remote jobs to an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="f2457-106">Para obter a documentação detalhada, confira [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="f2457-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="f2457-107">Você pode usar a Livy para executar shells interativos do Spark ou enviar trabalhos em lotes a serem executados no Spark.</span><span class="sxs-lookup"><span data-stu-id="f2457-107">You can use Livy to run interactive Spark shells or submit batch jobs to be run on Spark.</span></span> <span data-ttu-id="f2457-108">Este artigo aborda como usar a Livy para enviar trabalhos em lotes.</span><span class="sxs-lookup"><span data-stu-id="f2457-108">This article talks about using Livy to submit batch jobs.</span></span> <span data-ttu-id="f2457-109">Os trechos nesse artigo usam cURL para fazer chamadas à API REST para o ponto de extremidade da Livy Spark.</span><span class="sxs-lookup"><span data-stu-id="f2457-109">The snippets in this article use cURL to make REST API calls to the Livy Spark endpoint.</span></span>

<span data-ttu-id="f2457-110">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="f2457-110">**Prerequisites:**</span></span>

* <span data-ttu-id="f2457-111">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f2457-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="f2457-112">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f2457-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="f2457-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="f2457-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="f2457-114">Este artigo usa cURL para demonstrar como fazer chamadas à API REST em relação a um cluster do HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f2457-114">This article uses cURL to demonstrate how to make REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="f2457-115">Enviar um trabalho em lotes do Livy Spark</span><span class="sxs-lookup"><span data-stu-id="f2457-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="f2457-116">Antes de enviar um trabalho em lotes, você deve carregar o jar do aplicativo no armazenamento de cluster associado ao cluster.</span><span class="sxs-lookup"><span data-stu-id="f2457-116">Before you submit a batch job, you must upload the application jar on the cluster storage associated with the cluster.</span></span> <span data-ttu-id="f2457-117">Você pode usar [**AzCopy**](../storage/common/storage-use-azcopy.md), um utilitário de linha de comando, para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="f2457-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, to do so.</span></span> <span data-ttu-id="f2457-118">Há muitos outros clientes que podem ser usados para carregar dados.</span><span class="sxs-lookup"><span data-stu-id="f2457-118">There are various other clients you can use to upload data.</span></span> <span data-ttu-id="f2457-119">É possível saber mais sobre eles em [Carregar dados para trabalhos do Hadoop no HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="f2457-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path to application jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="f2457-120">**Exemplos**:</span><span class="sxs-lookup"><span data-stu-id="f2457-120">**Examples**:</span></span>

* <span data-ttu-id="f2457-121">Se o arquivo jar estiver no armazenamento de cluster (WASB)</span><span class="sxs-lookup"><span data-stu-id="f2457-121">If the jar file is on the cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="f2457-122">Se quiser passar o nome do arquivo jar e o nome da classe como parte de um arquivo de entrada (nesse exemplo, input.txt)</span><span class="sxs-lookup"><span data-stu-id="f2457-122">If you want to pass the jar filename and the classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-the-cluster"></a><span data-ttu-id="f2457-123">Obter informações sobre lotes Livy Spark em execução no cluster</span><span class="sxs-lookup"><span data-stu-id="f2457-123">Get information on Livy Spark batches running on the cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="f2457-124">**Exemplos**:</span><span class="sxs-lookup"><span data-stu-id="f2457-124">**Examples**:</span></span>

* <span data-ttu-id="f2457-125">Se quiser recuperar todos os lotes Livy spark em execução no cluster:</span><span class="sxs-lookup"><span data-stu-id="f2457-125">If you want to retrieve all the Livy Spark batches running on the cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="f2457-126">Se quiser recuperar um lote específico com uma batchID fornecida</span><span class="sxs-lookup"><span data-stu-id="f2457-126">If you want to retrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="f2457-127">Excluir um trabalho em lotes do Livy Spark</span><span class="sxs-lookup"><span data-stu-id="f2457-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="f2457-128">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="f2457-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="f2457-129">Livy Spark e alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="f2457-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="f2457-130">O Livy fornece alta disponibilidade para trabalhos Spark em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="f2457-130">Livy provides high-availability for Spark jobs running on the cluster.</span></span> <span data-ttu-id="f2457-131">Aqui estão alguns exemplos.</span><span class="sxs-lookup"><span data-stu-id="f2457-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="f2457-132">Se o serviço Livy falhar depois de você enviar um trabalho remotamente a um cluster Spark, o trabalho continuará em execução em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="f2457-132">If the Livy service goes down after you have submitted a job remotely to a Spark cluster, the job continues to run in the background.</span></span> <span data-ttu-id="f2457-133">Quando o Livy for backup, ele restaurará o status do trabalho e enviará o relatório de volta.</span><span class="sxs-lookup"><span data-stu-id="f2457-133">When Livy is back up, it restores the status of the job and reports it back.</span></span>
* <span data-ttu-id="f2457-134">Os blocos de notas Jupyter para HDInsight são ativados pelo Livy no back-end.</span><span class="sxs-lookup"><span data-stu-id="f2457-134">Jupyter notebooks for HDInsight are powered by Livy in the backend.</span></span> <span data-ttu-id="f2457-135">Se um bloco de anotações estiver executando um trabalho do Spark e o serviço Livy for reiniciado, o bloco de notas continuará a executar as células de código.</span><span class="sxs-lookup"><span data-stu-id="f2457-135">If a notebook is running a Spark job and the Livy service gets restarted, the notebook continues to run the code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="f2457-136">Mostrar um exemplo</span><span class="sxs-lookup"><span data-stu-id="f2457-136">Show me an example</span></span>
<span data-ttu-id="f2457-137">Nesta seção, vamos examinar exemplos sobre como usar a Livy Spark para enviar um trabalho em lotes, monitorar o progresso do trabalho e excluir o trabalho.</span><span class="sxs-lookup"><span data-stu-id="f2457-137">In this section, we look at examples to use Livy Spark to submit batch job, monitor the progress of the job, and then delete it.</span></span> <span data-ttu-id="f2457-138">O aplicativo que usamos neste exemplo é o desenvolvido no artigo [Criar um aplicativo Scala autônomo para ser executado no cluster Spark no HDInsight](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="f2457-138">The application we use in this example is the one developed in the article [Create a standalone Scala application and to run on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="f2457-139">As etapas aqui supõem que:</span><span class="sxs-lookup"><span data-stu-id="f2457-139">The steps here assume that:</span></span>

* <span data-ttu-id="f2457-140">Você já copiou o jar do aplicativo para a conta de armazenamento associada ao cluster.</span><span class="sxs-lookup"><span data-stu-id="f2457-140">You have already copied over the application jar to the storage account associated with the cluster.</span></span>
* <span data-ttu-id="f2457-141">Você tem o CuRL instalado no computador, onde está executando essas etapas.</span><span class="sxs-lookup"><span data-stu-id="f2457-141">You have CuRL installed on the computer where you are trying these steps.</span></span>

<span data-ttu-id="f2457-142">Execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f2457-142">Perform the following steps:</span></span>

1. <span data-ttu-id="f2457-143">Primeiramente, vamos verificar se a Livy Spark está em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="f2457-143">Let us first verify that Livy Spark is running on the cluster.</span></span> <span data-ttu-id="f2457-144">Podemos fazer isso obtendo uma lista de lotes em execução.</span><span class="sxs-lookup"><span data-stu-id="f2457-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="f2457-145">Se estiver executando um trabalho usando a Livy pela primeira vez, a saída deverá ser zero.</span><span class="sxs-lookup"><span data-stu-id="f2457-145">If you are running a job using Livy for the first time, the output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="f2457-146">Você deverá obter uma saída semelhante ao seguinte trecho:</span><span class="sxs-lookup"><span data-stu-id="f2457-146">You should get an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="f2457-147">Observe que a última linha da saída informa **total:0**, o que sugere que não há lotes em execução.</span><span class="sxs-lookup"><span data-stu-id="f2457-147">Notice how the last line in the output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="f2457-148">Agora vamos enviar um trabalho em lotes.</span><span class="sxs-lookup"><span data-stu-id="f2457-148">Let us now submit a batch job.</span></span> <span data-ttu-id="f2457-149">O trecho a seguir usa um arquivo de entrada (input.txt) para passar o nome do jar e o nome de classe como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="f2457-149">The following snippet uses an input file (input.txt) to pass the jar name and the class name as parameters.</span></span> <span data-ttu-id="f2457-150">Se você estiver executando essas etapas em um computador Windows, usar um arquivo de entrada será a abordagem recomendada.</span><span class="sxs-lookup"><span data-stu-id="f2457-150">If you are running these steps from a Windows computer, using an input file is the recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="f2457-151">Os parâmetros no arquivo **input.txt** são definidos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f2457-151">The parameters in the file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="f2457-152">Você deverá ver uma saída semelhante ao seguinte trecho:</span><span class="sxs-lookup"><span data-stu-id="f2457-152">You should see an output similar to the  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="f2457-153">Observe que a última linha da saída informa **state:starting**.</span><span class="sxs-lookup"><span data-stu-id="f2457-153">Notice how the last line of the output says **state:starting**.</span></span> <span data-ttu-id="f2457-154">Assim como, **id:0**.</span><span class="sxs-lookup"><span data-stu-id="f2457-154">It also says, **id:0**.</span></span> <span data-ttu-id="f2457-155">Aqui, **0** é a ID do lote.</span><span class="sxs-lookup"><span data-stu-id="f2457-155">Here, **0** is the batch ID.</span></span>

3. <span data-ttu-id="f2457-156">Agora você pode recuperar o status desse lote específico usando a ID do lote.</span><span class="sxs-lookup"><span data-stu-id="f2457-156">You can now retrieve the status of this specific batch using the batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="f2457-157">Você deverá ver uma saída semelhante ao seguinte trecho:</span><span class="sxs-lookup"><span data-stu-id="f2457-157">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="f2457-158">Agora a saída mostra **state:success**, o que sugere que o trabalho foi concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="f2457-158">The output now shows **state:success**, which suggests that the job was successfully completed.</span></span>

4. <span data-ttu-id="f2457-159">Se quiser, você pode excluir o lote.</span><span class="sxs-lookup"><span data-stu-id="f2457-159">If you want, you can now delete the batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="f2457-160">Você deverá ver uma saída semelhante ao seguinte trecho:</span><span class="sxs-lookup"><span data-stu-id="f2457-160">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="f2457-161">A última linha da saída mostra que o lote foi excluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="f2457-161">The last line of the output shows that the batch was successfully deleted.</span></span> <span data-ttu-id="f2457-162">Excluir um trabalho, enquanto ele está em execução, também encerra o trabalho.</span><span class="sxs-lookup"><span data-stu-id="f2457-162">Deleting a job, while it is running, also kills the job.</span></span> <span data-ttu-id="f2457-163">Se você excluir um trabalho que foi concluído, com êxito ou não, essa ação excluirá por completo as informações sobre o trabalho.</span><span class="sxs-lookup"><span data-stu-id="f2457-163">If you delete a job that has completed, successfully or otherwise, it deletes the job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="f2457-164">Uso do Livy Spark em clusters do HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="f2457-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="f2457-165">O cluster HDInsight 3.5, por padrão, desabilita o uso de caminhos de arquivo local para acessar arquivos de dados de exemplo ou jars.</span><span class="sxs-lookup"><span data-stu-id="f2457-165">HDInsight 3.5 cluster, by default, disables use of local file paths to access sample data files or jars.</span></span> <span data-ttu-id="f2457-166">Incentivamos o uso do caminho `wasb://` em vez disso, para acessar os jars ou os arquivos de dados de exemplo do cluster.</span><span class="sxs-lookup"><span data-stu-id="f2457-166">We encourage you to use the `wasb://` path instead to access jars or sample data files from the cluster.</span></span> <span data-ttu-id="f2457-167">Se você quiser usar o caminho local, atualize a configuração do Ambari adequadamente.</span><span class="sxs-lookup"><span data-stu-id="f2457-167">If you do want to use local path, you must update the Ambari configuration accordingly.</span></span> <span data-ttu-id="f2457-168">Para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="f2457-168">To do so:</span></span>

1. <span data-ttu-id="f2457-169">Acesse o portal do Ambari para o cluster.</span><span class="sxs-lookup"><span data-stu-id="f2457-169">Go to the Ambari portal for the cluster.</span></span> <span data-ttu-id="f2457-170">A interface de usuário da Web do Ambari está disponível no seu cluster HDInsight em https://**CLUSTERNAME**.azurehdidnsight.net, em que CLUSTERNAME é o nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="f2457-170">The Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is the name of your cluster.</span></span>

2. <span data-ttu-id="f2457-171">Na navegação à esquerda, clique em **Livy** e em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="f2457-171">From the left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="f2457-172">Em **livy-default** adicione o nome da propriedade `livy.file.local-dir-whitelist` e defina seu valor como **"/"** se você quiser permitir acesso total ao sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="f2457-172">Under **livy-default** add the property name `livy.file.local-dir-whitelist` and set it's value to **"/"** if you want to allow full access to file system.</span></span> <span data-ttu-id="f2457-173">Se você quiser permitir o acesso somente a um diretório específico, forneça o caminho ao diretório como o valor.</span><span class="sxs-lookup"><span data-stu-id="f2457-173">If you want to allow access only to a specific directory, provide the path to that directory as the value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="f2457-174">Enviar trabalhos da Livy para um cluster em uma rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="f2457-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="f2457-175">Se você se conectar a um cluster do HDInsight Spark de dentro de uma Rede Virtual do Azure, você poderá se conectar diretamente à Livy no cluster.</span><span class="sxs-lookup"><span data-stu-id="f2457-175">If you connect to an HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect to Livy on the cluster.</span></span> <span data-ttu-id="f2457-176">Nesse caso, a URL de ponto de extremidade da Livy é `http://<IP address of the headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="f2457-176">In such a case, the URL for Livy endpoint is `http://<IP address of the headnode>:8998/batches`.</span></span> <span data-ttu-id="f2457-177">Aqui, **8998** é a porta na qual a Livy é executada em um nó de cabeçalho do cluster.</span><span class="sxs-lookup"><span data-stu-id="f2457-177">Here, **8998** is the port on which Livy runs on the cluster headnode.</span></span> <span data-ttu-id="f2457-178">Para obter mais informações sobre como acessar serviços em portas não públicas, consulte [Portas usadas pelos serviços de Hadoop no HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="f2457-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f2457-179">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="f2457-179">Troubleshooting</span></span>

<span data-ttu-id="f2457-180">Veja aqui alguns dos problemas que você pode enfrentar ao usar o Livy para envio de trabalho remoto aos clusters Spark.</span><span class="sxs-lookup"><span data-stu-id="f2457-180">Here are some issues that you might run into while using Livy for remote job submission to Spark clusters.</span></span>

### <a name="using-an-external-jar-from-the-additional-storage-is-not-supported"></a><span data-ttu-id="f2457-181">Não há suporte para o uso de um jar externo no armazenamento adicional</span><span class="sxs-lookup"><span data-stu-id="f2457-181">Using an external jar from the additional storage is not supported</span></span>

<span data-ttu-id="f2457-182">**Problema:** se o trabalho da Livy Spark fizer referência a um jar externo da conta de armazenamento adicional associada ao cluster, o trabalho falhará.</span><span class="sxs-lookup"><span data-stu-id="f2457-182">**Problem:** If your Livy Spark job references an external jar from the additional storage account associated with the cluster, the job fails.</span></span>

<span data-ttu-id="f2457-183">**Resolução:** verifique se o jar que deseja usar está disponível no armazenamento padrão associado ao cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f2457-183">**Resolution:** Make sure that the jar you want to use is available in the default storage associated with the HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="f2457-184">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="f2457-184">Next step</span></span>

* [<span data-ttu-id="f2457-185">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2457-185">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f2457-186">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2457-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

