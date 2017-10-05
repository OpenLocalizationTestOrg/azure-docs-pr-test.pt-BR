---
title: "Usar o MapReduce e Curl com o Hadoop no HDInsight – Azure | Microsoft Docs"
description: Saiba como executar trabalhos MapReduce remotamente com Hadoop no HDInsight usando o Curl.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 8238bb829df95dcb8c99c0b7fff53c627a56f47c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="54746-103">Executar trabalhos MapReduce com Hadoop no HDInsight usando REST</span><span class="sxs-lookup"><span data-stu-id="54746-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="54746-104">Saiba como usar a API REST do WebHCat para executar trabalhos MapReduce em um Hadoop no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="54746-104">Learn how to use the WebHCat REST API to run MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="54746-105">O Curl é usado para demonstrar como você pode interagir com o HDInsight usando solicitações HTTP brutas para executar trabalhos MapReduce.</span><span class="sxs-lookup"><span data-stu-id="54746-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="54746-106">Se você já estiver familiarizado com o uso de servidores Hadoop baseados em Linux, mas for iniciante no HDInsight, consulte o documento [O que você precisa saber sobre Hadoop baseado em Linux no HDInsight](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="54746-106">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see the [What you need to know about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="54746-107"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="54746-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="54746-108">Um Hadoop no cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="54746-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="54746-109">Curl</span><span class="sxs-lookup"><span data-stu-id="54746-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="54746-110">jq</span><span class="sxs-lookup"><span data-stu-id="54746-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="54746-111"><a id="curl"></a>Executar trabalhos MapReduce usando o Curl</span><span class="sxs-lookup"><span data-stu-id="54746-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="54746-112">Ao usar o Curl ou quaisquer outras comunicações do REST com WebHCat, deve autenticar as solicitações fornecendo o nome de usuário de administrador de cluster HDInsight e a senha.</span><span class="sxs-lookup"><span data-stu-id="54746-112">When you use Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="54746-113">Você também deve usar o nome do cluster como parte do URI usado para enviar as solicitações para o servidor.</span><span class="sxs-lookup"><span data-stu-id="54746-113">You must use the cluster name as part of the URI that is used to send the requests to the server.</span></span>
>
> <span data-ttu-id="54746-114">Para os comandos nesta seção, substitua **USERNAME** pelo usuário para autenticar o cluster, e **PASSWORD** pela senha da conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="54746-114">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="54746-115">Substitua **CLUSTERNAME** pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="54746-115">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="54746-116">A API REST é protegida usando [autenticação básica de acesso](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="54746-116">The REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="54746-117">Você deve sempre fazer solicitações usando HTTPS para garantir que suas credenciais sejam enviadas com segurança para o servidor.</span><span class="sxs-lookup"><span data-stu-id="54746-117">You should always make requests by using HTTPS to ensure that your credentials are securely sent to the server.</span></span>


1. <span data-ttu-id="54746-118">De uma linha de comando, use o seguinte comando para verificar se você pode se conectar ao cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="54746-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="54746-119">Você deve receber uma resposta semelhante ao seguinte JSON:</span><span class="sxs-lookup"><span data-stu-id="54746-119">You should receive a response similar to the following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="54746-120">Os parâmetros usados nesse comando são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="54746-120">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="54746-121">**-u**: o nome de usuário e a senha usada para autenticar a solicitação</span><span class="sxs-lookup"><span data-stu-id="54746-121">**-u**: Indicates the user name and password used to authenticate the request</span></span>
   * <span data-ttu-id="54746-122">**-G**: indica que essa operação é uma solicitação GET</span><span class="sxs-lookup"><span data-stu-id="54746-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="54746-123">O início do URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, será o mesmo para todas as solicitações.</span><span class="sxs-lookup"><span data-stu-id="54746-123">The beginning of the URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span>

2. <span data-ttu-id="54746-124">Para enviar um trabalho MapReduce, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="54746-124">To submit a MapReduce job, use the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="54746-125">O final do URI (/mapreduce/jar) informa ao WebHCat que essa solicitação inicia um trabalho MapReduce de uma classe em um arquivo jar.</span><span class="sxs-lookup"><span data-stu-id="54746-125">The end of the URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="54746-126">Os parâmetros usados nesse comando são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="54746-126">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="54746-127">**-d** já que `-G` não é usado; a solicitação padrão será o método POST.</span><span class="sxs-lookup"><span data-stu-id="54746-127">**-d**: `-G` is not used, so the request defaults to the POST method.</span></span> <span data-ttu-id="54746-128">`-d` especifica os valores de dados que são enviados com a solicitação.</span><span class="sxs-lookup"><span data-stu-id="54746-128">`-d` specifies the data values that are sent with the request.</span></span>
    * <span data-ttu-id="54746-129">**user.name**: o usuário que está executando o comando</span><span class="sxs-lookup"><span data-stu-id="54746-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="54746-130">**jar**: o local do arquivo jar que contém a classe para ser executada</span><span class="sxs-lookup"><span data-stu-id="54746-130">**jar**: The location of the jar file that contains class to be ran</span></span>
    * <span data-ttu-id="54746-131">**class**: a classe que contém a lógica do MapReduce</span><span class="sxs-lookup"><span data-stu-id="54746-131">**class**: The class that contains the MapReduce logic</span></span>
    * <span data-ttu-id="54746-132">**arg**: os argumentos a serem passados para o trabalho MapReduce.</span><span class="sxs-lookup"><span data-stu-id="54746-132">**arg**: The arguments to be passed to the MapReduce job.</span></span> <span data-ttu-id="54746-133">Nesse caso, o arquivo de texto de entrada e o diretório usados para a saída</span><span class="sxs-lookup"><span data-stu-id="54746-133">In this case, the input text file and the directory that are used for the output</span></span>

     <span data-ttu-id="54746-134">Esse comando deve retornar uma ID de trabalho que pode ser usada para verificar o status do trabalho:</span><span class="sxs-lookup"><span data-stu-id="54746-134">This command should return a job ID that can be used to check the status of the job:</span></span>

       <span data-ttu-id="54746-135">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="54746-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="54746-136">Para verificar o status do trabalho, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="54746-136">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="54746-137">Substitua o **JOBID** pelo valor retornado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="54746-137">Replace the **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="54746-138">Por exemplo, se o valor retornado foi `{"id":"job_1415651640909_0026"}`, JOBID será `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="54746-138">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then the JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="54746-139">Se o trabalho for concluído, o estado retornado será `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="54746-139">If the job is complete, the state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54746-140">Essa solicitação de Curl retorna um documento JSON com informações sobre o trabalho.</span><span class="sxs-lookup"><span data-stu-id="54746-140">This Curl request returns a JSON document with information about the job.</span></span> <span data-ttu-id="54746-141">Jq é usado para recuperar apenas o valor de estado.</span><span class="sxs-lookup"><span data-stu-id="54746-141">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="54746-142">Depois que o estado do trabalho for alterado para `SUCCEEDED`, você poderá recuperar os resultados do trabalho do Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="54746-142">When the state of the job has changed to `SUCCEEDED`, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="54746-143">O parâmetro `statusdir` transmitido com a consulta contém o local do arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="54746-143">The `statusdir` parameter that is passed with the query contains the location of the output file.</span></span> <span data-ttu-id="54746-144">Neste exemplo, o local é `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="54746-144">In this example, the location is `/example/curl`.</span></span> <span data-ttu-id="54746-145">Esse endereço armazena a saída do trabalho no armazenamento padrão de clusters em `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="54746-145">This address stores the output of the job in the clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="54746-146">Você pode listar e baixar esses arquivos usando a [CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="54746-146">You can list and download these files by using the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="54746-147">Para obter mais informações sobre como trabalhar com blobs na CLI do Azure, consulte o documento [Usar a CLI 2.0 do Azure com o Armazenamento do Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs).</span><span class="sxs-lookup"><span data-stu-id="54746-147">For more information on working with blobs from the Azure CLI, see the [Using the Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="54746-148"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="54746-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="54746-149">Para obter informações gerais sobre trabalhos de MapReduce no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="54746-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="54746-150">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="54746-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="54746-151">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="54746-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="54746-152">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="54746-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="54746-153">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="54746-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="54746-154">Para obter mais informações sobre a interface REST usada nesse artigo, consulte a [Referência de WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="54746-154">For more information about the REST interface that is used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>