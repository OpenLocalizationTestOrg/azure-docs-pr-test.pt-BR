---
title: "Usar o Sqoop do Hadoop com Curl no HDInsight – Azure | Microsoft Docs"
description: Saiba como enviar remotamente trabalhos do Sqoop para o HDInsight usando o Curl.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="ff024-103">Executar trabalhos do Sqoop com Hadoop no HDInsight com Curl</span><span class="sxs-lookup"><span data-stu-id="ff024-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="ff024-104">Saiba como usar o Curl para executar trabalhos do Sqoop em um cluster Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff024-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="ff024-105">Curl é usado para demonstrar como você pode interagir com o HDInsight usando solicitações HTTP brutas para executar, monitorar e recuperar os resultados de trabalhos do Sqoop.</span><span class="sxs-lookup"><span data-stu-id="ff024-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span></span> <span data-ttu-id="ff024-106">Isso funciona usando a API REST do WebHCat (anteriormente conhecido como Templeton) fornecida pelo seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff024-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="ff024-107">Se você já estiver familiarizado com o uso de servidores Hadoop baseados em Linux, mas não conhece o HDInsight, confira [Informações sobre o uso do HDInsight no Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="ff024-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ff024-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ff024-108">Prerequisites</span></span>
<span data-ttu-id="ff024-109">Para concluir as etapas neste artigo, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="ff024-109">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="ff024-110">Um Hadoop no cluster HDInsight (baseado em Linux ou Windows)</span><span class="sxs-lookup"><span data-stu-id="ff024-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="ff024-111">Curl</span><span class="sxs-lookup"><span data-stu-id="ff024-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="ff024-112">jq</span><span class="sxs-lookup"><span data-stu-id="ff024-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="ff024-113">Enviar trabalhos do Sqoop usando o Curl</span><span class="sxs-lookup"><span data-stu-id="ff024-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="ff024-114">Ao usar o Curl ou qualquer outra comunicação do REST com WebHCat, você deve autenticar as solicitações, fornecendo o nome de usuário e a senha para o administrador do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff024-114">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="ff024-115">Você também deve usar o nome do cluster como parte do URI (Uniform Resource Identifier) usado para enviar as solicitações ao servidor.</span><span class="sxs-lookup"><span data-stu-id="ff024-115">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="ff024-116">Para os comandos nesta seção, substitua **USERNAME** pelo usuário para autenticar o cluster e substitua **PASSWORD** pela senha da conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="ff024-116">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="ff024-117">Substitua **CLUSTERNAME** pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="ff024-117">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="ff024-118">A API REST é protegida por meio de [autenticação básica](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="ff024-118">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="ff024-119">Você deve sempre fazer solicitações usando HTTPS (HTTP seguro) para ajudar a garantir que suas credenciais sejam enviadas com segurança para o servidor.</span><span class="sxs-lookup"><span data-stu-id="ff024-119">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="ff024-120">De uma linha de comando, use o seguinte comando para verificar se você pode se conectar ao cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ff024-120">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="ff024-121">Você deve receber uma resposta com esta aparência:</span><span class="sxs-lookup"><span data-stu-id="ff024-121">You should receive a response similar to the following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="ff024-122">Os parâmetros usados nesse comando são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ff024-122">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="ff024-123">**-u** - o nome de usuário e a senha usada para autenticar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="ff024-123">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="ff024-124">**-G** - indica que se trata de uma solicitação GET.</span><span class="sxs-lookup"><span data-stu-id="ff024-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="ff024-125">O início da URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, será o mesmo para todas as solicitações.</span><span class="sxs-lookup"><span data-stu-id="ff024-125">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span></span> <span data-ttu-id="ff024-126">O caminho, **/status**, indica que a solicitação é para retornar o status de WebHCat (também conhecido como Templeton) ao servidor.</span><span class="sxs-lookup"><span data-stu-id="ff024-126">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> 
2. <span data-ttu-id="ff024-127">Use o seguinte para enviar um trabalho do sqoop:</span><span class="sxs-lookup"><span data-stu-id="ff024-127">Use the following to submit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="ff024-128">Os parâmetros usados nesse comando são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ff024-128">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="ff024-129">**-d** – uma vez que `-G` não é usado; a solicitação padrão é o método POST.</span><span class="sxs-lookup"><span data-stu-id="ff024-129">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="ff024-130">`-d` especifica os valores de dados que são enviados com a solicitação.</span><span class="sxs-lookup"><span data-stu-id="ff024-130">`-d` specifies the data values that are sent with the request.</span></span>

        * <span data-ttu-id="ff024-131">**user.name** - o usuário que está executando o comando.</span><span class="sxs-lookup"><span data-stu-id="ff024-131">**user.name** - The user that is running the command.</span></span>

        * <span data-ttu-id="ff024-132">**command** - o comando Sqoop a ser executado.</span><span class="sxs-lookup"><span data-stu-id="ff024-132">**command** - The Sqoop command to execute.</span></span>

        * <span data-ttu-id="ff024-133">**statusdir** - o diretório no qual o status deste trabalho será gravado.</span><span class="sxs-lookup"><span data-stu-id="ff024-133">**statusdir** - The directory that the status for this job will be written to.</span></span>

    <span data-ttu-id="ff024-134">Esse comando deve retornar uma ID de trabalho que pode ser usada para verificar o status do trabalho.</span><span class="sxs-lookup"><span data-stu-id="ff024-134">This command should return a job ID that can be used to check the status of the job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="ff024-135">Para verificar o status do trabalho, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="ff024-135">To check the status of the job, use the following command.</span></span> <span data-ttu-id="ff024-136">Substitua **JOBID** pelo valor retornado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="ff024-136">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="ff024-137">Por exemplo, se o valor retornado for **, `{"id":"job_1415651640909_0026"}`JOBID** será `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="ff024-137">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="ff024-138">Se o trabalho foi concluído, o estado será **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="ff024-138">If the job has finished, the state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ff024-139">Essa solicitação de Curl retorna um documento JSON (JavaScript Object Notation) com informações sobre o trabalho; jq é usado para recuperar o valor de estado.</span><span class="sxs-lookup"><span data-stu-id="ff024-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span></span>
   > 
   > 
2. <span data-ttu-id="ff024-140">Depois que o estado do trabalho for alterado para **SUCCEEDED**, você poderá recuperar os resultados do trabalho no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff024-140">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="ff024-141">O parâmetro `statusdir` transmitido com a consulta contém o local do arquivo de saída; nesse caso, **wasb:///example/curl**.</span><span class="sxs-lookup"><span data-stu-id="ff024-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="ff024-142">Esse endereço armazena a saída do trabalho no diretório **example/curl** do contêiner de armazenamento padrão usado pelo cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff024-142">This address stores the output of the job in the **example/curl** directory on the default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="ff024-143">Você pode listar e baixar esses arquivos usando a [CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ff024-143">You can list and download these files by using the [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="ff024-144">Por exemplo, para listar arquivos em **example/curl**, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ff024-144">For example, to list files in **example/curl**, use the following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="ff024-145">Para baixar um arquivo, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ff024-145">To download a file, use the following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="ff024-146">Você deve especificar o nome da conta de armazenamento que contém o blob usando os parâmetros `-a` e `-k` ou definir as variáveis de ambiente **AZURE\_STORAGE\_ACCOUNT** e **AZURE\_STORAGE\_ACCESS\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="ff024-146">You must either specify the storage account name that contains the blob by using the `-a` and `-k` parameters, or set the **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="ff024-147">Consulte <a href="hdinsight-upload-data.md" target="_blank"para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ff024-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="ff024-148">Limitações</span><span class="sxs-lookup"><span data-stu-id="ff024-148">Limitations</span></span>
* <span data-ttu-id="ff024-149">Exportação em massa — com HDInsight baseado em Linux, o conector Sqoop usado para exportar dados no Microsoft SQL Server ou no Banco de Dados SQL do Azure, atualmente, não permite inserções em massa.</span><span class="sxs-lookup"><span data-stu-id="ff024-149">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="ff024-150">Envio em lote — com HDInsight baseado em Linux, ao usar o comutador `-batch` na execução de inserções, Sqoop executará várias inserções em vez de operações de inserção em lotes.</span><span class="sxs-lookup"><span data-stu-id="ff024-150">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="ff024-151">Resumo</span><span class="sxs-lookup"><span data-stu-id="ff024-151">Summary</span></span>
<span data-ttu-id="ff024-152">Conforme demonstrado neste documento, você pode usar uma solicitação HTTP bruta para executar, monitorar e exibir os resultados de trabalhos do Sqoop no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff024-152">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="ff024-153">Para saber mais sobre a interface REST usada neste artigo, confira o <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Guia da API REST do Sqoop</a>.</span><span class="sxs-lookup"><span data-stu-id="ff024-153">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff024-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ff024-154">Next steps</span></span>
<span data-ttu-id="ff024-155">Para obter informações gerais sobre o Hive com HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ff024-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="ff024-156">Usar o Sqoop com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff024-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="ff024-157">Para obter informações sobre outras maneiras que você pode trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ff024-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ff024-158">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff024-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ff024-159">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff024-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ff024-160">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff024-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


