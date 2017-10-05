---
title: "Usar o Pig do Hadoop com REST no HDInsight – Azure | Microsoft Docs"
description: Aprenda a usar o REST para executar trabalhos do Pig Latin em um cluster do Hadoop no Azure HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a86864a779b0de1c6d5669cfbba0f3e1a27f1ff1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="a984e-103">Executar trabalhos do Pig com Hadoop no HDInsight usando o REST</span><span class="sxs-lookup"><span data-stu-id="a984e-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="a984e-104">Saiba como executar trabalhos do Pig Latin fazendo solicitações REST para um cluster HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="a984e-104">Learn how to run Pig Latin jobs by making REST requests to an Azure HDInsight cluster.</span></span> <span data-ttu-id="a984e-105">O Curl é usado para demonstrar como você pode interagir com o HDInsight usando a API REST do WebHCat.</span><span class="sxs-lookup"><span data-stu-id="a984e-105">Curl is used to demonstrate how you can interact with HDInsight using the WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="a984e-106">Se você já estiver familiarizado com o uso de servidores Hadoop baseados em Linux, mas é novo no HDInsight, consulte [Dicas do HDInsight baseado em Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="a984e-106">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="a984e-107"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a984e-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="a984e-108">Um cluster do Azure HDInsight (Hadoop no HDInsight, baseado em Windows ou Linux)</span><span class="sxs-lookup"><span data-stu-id="a984e-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a984e-109">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="a984e-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a984e-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a984e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="a984e-111">Curl</span><span class="sxs-lookup"><span data-stu-id="a984e-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="a984e-112">jq</span><span class="sxs-lookup"><span data-stu-id="a984e-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="a984e-113"><a id="curl"></a>Executar trabalhos do Pig usando Curl</span><span class="sxs-lookup"><span data-stu-id="a984e-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="a984e-114">A API REST é protegida por meio de [autenticação básica de acesso](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="a984e-114">The REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="a984e-115">Para assegurar que suas credenciais sejam enviadas com segurança para o servidor, sempre faça solicitações usando HTTPS (HTTP seguro).</span><span class="sxs-lookup"><span data-stu-id="a984e-115">Always make requests by using Secure HTTP (HTTPS) to ensure that your credentials are securely sent to the server.</span></span>
>
> <span data-ttu-id="a984e-116">Ao usar os comandos nesta seção, substitua `USERNAME` pelo usuário para autenticar o cluster e substitua `PASSWORD` pela senha da conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="a984e-116">When using the commands in this section, replace `USERNAME` with the user to authenticate to the cluster, and replace `PASSWORD` with the password for the user account.</span></span> <span data-ttu-id="a984e-117">Substitua `CLUSTERNAME` pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="a984e-117">Replace `CLUSTERNAME` with the name of your cluster.</span></span>
>


1. <span data-ttu-id="a984e-118">De uma linha de comando, use o seguinte comando para verificar se você pode se conectar ao cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a984e-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="a984e-119">Você deve receber a resposta JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="a984e-119">You should receive the following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="a984e-120">Os parâmetros usados nesse comando são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a984e-120">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="a984e-121">**-u**: o nome de usuário e a senha usados para autenticar a solicitação</span><span class="sxs-lookup"><span data-stu-id="a984e-121">**-u**: The user name and password used to authenticate the request</span></span>
    * <span data-ttu-id="a984e-122">**-G**: indica que essa solicitação é uma solicitação GET</span><span class="sxs-lookup"><span data-stu-id="a984e-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="a984e-123">O início da URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, será o mesmo para todas as solicitações.</span><span class="sxs-lookup"><span data-stu-id="a984e-123">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="a984e-124">O caminho, **/status**, indica que a solicitação é para retornar o status de WebHCat (também conhecido como Templeton) para o servidor.</span><span class="sxs-lookup"><span data-stu-id="a984e-124">The path, **/status**, indicates that the request is to return the status of WebHCat (also known as Templeton) for the server.</span></span>

2. <span data-ttu-id="a984e-125">Use o seguinte para enviar um trabalho de Pig Latin para o cluster:</span><span class="sxs-lookup"><span data-stu-id="a984e-125">Use the following code to submit a Pig Latin job to the cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="a984e-126">Os parâmetros usados nesse comando são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a984e-126">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="a984e-127">**-d**: como `-G` não é usado; a solicitação padrão é o método POST.</span><span class="sxs-lookup"><span data-stu-id="a984e-127">**-d**: Because `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="a984e-128">`-d` especifica os valores de dados que são enviados com a solicitação.</span><span class="sxs-lookup"><span data-stu-id="a984e-128">`-d` specifies the data values that are sent with the request.</span></span>

    * <span data-ttu-id="a984e-129">**user.name**: o usuário que está executando o comando</span><span class="sxs-lookup"><span data-stu-id="a984e-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="a984e-130">**execute**: as instruções de Pig Latin a executar</span><span class="sxs-lookup"><span data-stu-id="a984e-130">**execute**: The Pig Latin statements to execute</span></span>
    * <span data-ttu-id="a984e-131">**statusdir**: o diretório no qual o status deste trabalho é gravado</span><span class="sxs-lookup"><span data-stu-id="a984e-131">**statusdir**: The directory that the status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="a984e-132">Observe que os espaços em instruções do Pig Latin são substituídos pelo caractere `+` quando usado com o Curl.</span><span class="sxs-lookup"><span data-stu-id="a984e-132">Notice that the spaces in Pig Latin statements are replaced by the `+` character when used with Curl.</span></span>

    <span data-ttu-id="a984e-133">Esse comando deve retornar uma ID de trabalho que pode ser usada para verificar o status do trabalho, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a984e-133">This command should return a job ID that can be used to check the status of the job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="a984e-134">Para verificar o status do trabalho, use o comando a seguir</span><span class="sxs-lookup"><span data-stu-id="a984e-134">To check the status of the job, use the following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="a984e-135">Substitua `JOBID` pelo valor retornado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="a984e-135">Replace `JOBID` with the value returned in the previous step.</span></span> <span data-ttu-id="a984e-136">Por exemplo, se o valor retornado era `{"id":"job_1415651640909_0026"}`, então `JOBID` é `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="a984e-136">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="a984e-137">Se o trabalho foi concluído, o estado será **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="a984e-137">If the job has finished, the state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a984e-138">Essa solicitação de Curl retorna um documento JSON (JavaScript Object Notation) com informações sobre o trabalho; jq é usado para recuperar o valor de estado.</span><span class="sxs-lookup"><span data-stu-id="a984e-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job, and jq is used to retrieve only the state value.</span></span>

## <span data-ttu-id="a984e-139"><a id="results"></a>Exibir resultados</span><span class="sxs-lookup"><span data-stu-id="a984e-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="a984e-140">Depois que o estado do trabalho for alterado para **SUCCEEDED**, você poderá recuperar os resultados do trabalho.</span><span class="sxs-lookup"><span data-stu-id="a984e-140">When the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job.</span></span> <span data-ttu-id="a984e-141">O parâmetro `statusdir` transmitido com a consulta contém a localização do arquivo de saída; nesse caso, `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="a984e-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="a984e-142">O HDInsight pode usar o Armazenamento do Azure ou o Azure Data Lake Store como o armazenamento de dados padrão.</span><span class="sxs-lookup"><span data-stu-id="a984e-142">HDInsight can use either Azure Storage or Azure Data Lake Store as the default data store.</span></span> <span data-ttu-id="a984e-143">Há várias maneiras de obter os dados, dependendo de qual deles você usa.</span><span class="sxs-lookup"><span data-stu-id="a984e-143">There are various ways to get at the data depending on which one you use.</span></span> <span data-ttu-id="a984e-144">Para obter mais informações, consulte a seção armazenamento do documento [Informações do HDInsight baseado em Linux](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="a984e-144">For more information, see the storage section of the [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="a984e-145"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="a984e-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="a984e-146">Conforme demonstrado nesse documento, você pode usar a solicitação HTTP bruta para executar, monitorar e exibir os resultados de trabalhos Pig no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a984e-146">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="a984e-147">Para obter mais informações sobre a interface REST usada nesse artigo, consulte a [Referência de WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="a984e-147">For more information about the REST interface used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="a984e-148"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a984e-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="a984e-149">Para obter informações gerais sobre o Pig no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a984e-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="a984e-150">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="a984e-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="a984e-151">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a984e-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="a984e-152">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="a984e-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a984e-153">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="a984e-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
