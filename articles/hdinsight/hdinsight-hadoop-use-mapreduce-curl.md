---
title: aaaUse MapReduce e Curl com Hadoop no HDInsight - Azure | Microsoft Docs
description: "Saiba como tooremotely executar trabalhos de MapReduce com Hadoop no HDInsight usando a rotação."
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
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="cb035-103">Executar trabalhos MapReduce com Hadoop no HDInsight usando REST</span><span class="sxs-lookup"><span data-stu-id="cb035-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="cb035-104">Saiba como toouse Olá WebHCat REST API toorun MapReduce trabalhos em um Hadoop no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cb035-104">Learn how toouse hello WebHCat REST API toorun MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="cb035-105">Ondulação é usado toodemonstrate como você pode interagir com o HDInsight usando bruto toorun de solicitações HTTP trabalhos MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cb035-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="cb035-106">Se você já estiver familiarizado com o uso de servidores baseados em Linux Hadoop, mas são tooHDInsight novo, consulte Olá [o que você precisa tooknow sobre baseados em Linux Hadoop no HDInsight](hdinsight-hadoop-linux-information.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cb035-106">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see hello [What you need tooknow about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="cb035-107"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cb035-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="cb035-108">Um Hadoop no cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb035-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="cb035-109">Curl</span><span class="sxs-lookup"><span data-stu-id="cb035-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="cb035-110">jq</span><span class="sxs-lookup"><span data-stu-id="cb035-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="cb035-111"><a id="curl"></a>Executar trabalhos MapReduce usando o Curl</span><span class="sxs-lookup"><span data-stu-id="cb035-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="cb035-112">Quando você usa Ondulação ou quaisquer outras comunicações do REST com WebHCat, você deve autenticar solicitações de hello, fornecendo a senha e nome de usuário do administrador de cluster de HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cb035-112">When you use Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="cb035-113">Você deve usar o nome do cluster hello como parte do URI é usado toosend Olá solicitações toohello servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb035-113">You must use hello cluster name as part of hello URI that is used toosend hello requests toohello server.</span></span>
>
> <span data-ttu-id="cb035-114">Para comandos Olá nesta seção, substitua **USERNAME** com cluster de toohello tooauthenticate do usuário Olá, e **senha** com senha Olá Olá conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="cb035-114">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="cb035-115">Substituir **CLUSTERNAME** com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="cb035-115">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="cb035-116">Olá API REST é protegida usando [autenticação de acesso básico](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="cb035-116">hello REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="cb035-117">Você sempre deve fazer solicitações usando HTTPS tooensure que suas credenciais são enviadas com segurança toohello server.</span><span class="sxs-lookup"><span data-stu-id="cb035-117">You should always make requests by using HTTPS tooensure that your credentials are securely sent toohello server.</span></span>


1. <span data-ttu-id="cb035-118">De uma linha de comando, use Olá tooverify de comando que você pode conectar o cluster do HDInsight tooyour a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb035-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="cb035-119">Você deve receber um toohello semelhante de resposta JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb035-119">You should receive a response similar toohello following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="cb035-120">Estes são os parâmetros de saudação usados neste comando:</span><span class="sxs-lookup"><span data-stu-id="cb035-120">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="cb035-121">**-u**: indica Olá nome de usuário e a senha usada tooauthenticate solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="cb035-121">**-u**: Indicates hello user name and password used tooauthenticate hello request</span></span>
   * <span data-ttu-id="cb035-122">**-G**: indica que essa operação é uma solicitação GET</span><span class="sxs-lookup"><span data-stu-id="cb035-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="cb035-123">Olá a partir de saudação URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, Olá mesmo para todas as solicitações.</span><span class="sxs-lookup"><span data-stu-id="cb035-123">hello beginning of hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span>

2. <span data-ttu-id="cb035-124">toosubmit um trabalho de MapReduce, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb035-124">toosubmit a MapReduce job, use hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="cb035-125">fim de saudação do hello URI (mapreduce/jar) informa WebHCat que essa solicitação inicia um trabalho de MapReduce de uma classe em um arquivo jar.</span><span class="sxs-lookup"><span data-stu-id="cb035-125">hello end of hello URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="cb035-126">Estes são os parâmetros de saudação usados neste comando:</span><span class="sxs-lookup"><span data-stu-id="cb035-126">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="cb035-127">**-d**: `-G` não é usado, então a solicitação Olá padrão é o método POST de toohello.</span><span class="sxs-lookup"><span data-stu-id="cb035-127">**-d**: `-G` is not used, so hello request defaults toohello POST method.</span></span> <span data-ttu-id="cb035-128">`-d`Especifica valores de dados de saudação que são enviados com a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb035-128">`-d` specifies hello data values that are sent with hello request.</span></span>
    * <span data-ttu-id="cb035-129">**User.Name**: usuário de saudação que está executando o comando Olá</span><span class="sxs-lookup"><span data-stu-id="cb035-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="cb035-130">**JAR**: local de saudação do arquivo jar Olá que contém a classe toobe foi executado</span><span class="sxs-lookup"><span data-stu-id="cb035-130">**jar**: hello location of hello jar file that contains class toobe ran</span></span>
    * <span data-ttu-id="cb035-131">**classe**: Olá classe que contém a lógica de MapReduce Olá</span><span class="sxs-lookup"><span data-stu-id="cb035-131">**class**: hello class that contains hello MapReduce logic</span></span>
    * <span data-ttu-id="cb035-132">**arg**: Olá toobe de argumentos passado toohello trabalho de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cb035-132">**arg**: hello arguments toobe passed toohello MapReduce job.</span></span> <span data-ttu-id="cb035-133">Nesse caso, o diretório de arquivo e hello de texto que são usados para saída de hello de entrada hello</span><span class="sxs-lookup"><span data-stu-id="cb035-133">In this case, hello input text file and hello directory that are used for hello output</span></span>

     <span data-ttu-id="cb035-134">Este comando deve retornar uma ID de trabalho que pode ser toocheck usado Olá status do trabalho de saudação:</span><span class="sxs-lookup"><span data-stu-id="cb035-134">This command should return a job ID that can be used toocheck hello status of hello job:</span></span>

       <span data-ttu-id="cb035-135">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="cb035-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="cb035-136">status de Olá toocheck de trabalho Olá Olá use comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb035-136">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="cb035-137">Substituir saudação **JOBID** com hello valor retornado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="cb035-137">Replace hello **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="cb035-138">Por exemplo, se hello retornar o valor era `{"id":"job_1415651640909_0026"}`, em seguida, Olá JOBID seria `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="cb035-138">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then hello JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="cb035-139">Se o trabalho de saudação for concluído, o estado de saudação retornado é `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="cb035-139">If hello job is complete, hello state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cb035-140">Essa solicitação de ondulação retorna um documento JSON com informações sobre o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb035-140">This Curl request returns a JSON document with information about hello job.</span></span> <span data-ttu-id="cb035-141">Jq é usada tooretrieve Olá apenas o valor de estado.</span><span class="sxs-lookup"><span data-stu-id="cb035-141">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="cb035-142">Quando o estado de saudação do trabalho Olá foi alterado muito`SUCCEEDED`, você pode recuperar os resultados de saudação do trabalho de saudação do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb035-142">When hello state of hello job has changed too`SUCCEEDED`, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="cb035-143">Olá `statusdir` parâmetro que é passado com hello consulta contém o local de Olá Olá do arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="cb035-143">hello `statusdir` parameter that is passed with hello query contains hello location of hello output file.</span></span> <span data-ttu-id="cb035-144">Neste exemplo, o local de saudação é `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="cb035-144">In this example, hello location is `/example/curl`.</span></span> <span data-ttu-id="cb035-145">Esse endereço armazena a saída de saudação do trabalho Olá no armazenamento padrão da saudação clusters em `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="cb035-145">This address stores hello output of hello job in hello clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="cb035-146">Você pode listar e baixar esses arquivos usando Olá [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cb035-146">You can list and download these files by using hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="cb035-147">Para obter mais informações sobre como trabalhar com blobs de saudação CLI do Azure, consulte Olá [usando Olá 2.0 do CLI do Azure com o armazenamento do Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs) documento.</span><span class="sxs-lookup"><span data-stu-id="cb035-147">For more information on working with blobs from hello Azure CLI, see hello [Using hello Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="cb035-148"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb035-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="cb035-149">Para obter informações gerais sobre trabalhos de MapReduce no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cb035-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="cb035-150">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb035-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="cb035-151">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cb035-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="cb035-152">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb035-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="cb035-153">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="cb035-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="cb035-154">Para obter mais informações sobre a interface REST Olá que é usada neste artigo, consulte Olá [WebHCat referência](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="cb035-154">For more information about hello REST interface that is used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>
