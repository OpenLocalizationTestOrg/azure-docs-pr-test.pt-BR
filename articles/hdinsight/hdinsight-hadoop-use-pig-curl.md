---
title: aaaUse Pig do Hadoop com REST no HDInsight - Azure | Microsoft Docs
description: Saiba como cluster de trabalhos de Pig latino de toorun toouse restante em um Hadoop no HDInsight do Azure.
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
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="8d84d-103">Executar trabalhos do Pig com Hadoop no HDInsight usando o REST</span><span class="sxs-lookup"><span data-stu-id="8d84d-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="8d84d-104">Saiba como toorun Pig latino trabalhos, tornando o cluster do REST solicitações tooan HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d84d-104">Learn how toorun Pig Latin jobs by making REST requests tooan Azure HDInsight cluster.</span></span> <span data-ttu-id="8d84d-105">Ondulação é usado toodemonstrate como você pode interagir com o HDInsight usando Olá WebHCat REST API.</span><span class="sxs-lookup"><span data-stu-id="8d84d-105">Curl is used toodemonstrate how you can interact with HDInsight using hello WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="8d84d-106">Se você já estiver familiarizado com o uso de servidores baseados em Linux Hadoop, mas é tooHDInsight novo, consulte [dicas de HDInsight baseados em Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="8d84d-106">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="8d84d-107"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8d84d-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="8d84d-108">Um cluster do Azure HDInsight (Hadoop no HDInsight, baseado em Windows ou Linux)</span><span class="sxs-lookup"><span data-stu-id="8d84d-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8d84d-109">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8d84d-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8d84d-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8d84d-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="8d84d-111">Curl</span><span class="sxs-lookup"><span data-stu-id="8d84d-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="8d84d-112">jq</span><span class="sxs-lookup"><span data-stu-id="8d84d-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="8d84d-113"><a id="curl"></a>Executar trabalhos do Pig usando Curl</span><span class="sxs-lookup"><span data-stu-id="8d84d-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="8d84d-114">Olá API REST é protegida por meio de [autenticação de acesso básico](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="8d84d-114">hello REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="8d84d-115">Sempre fazem solicitações usando o HTTP seguro (HTTPS) tooensure que suas credenciais são enviadas com segurança toohello server.</span><span class="sxs-lookup"><span data-stu-id="8d84d-115">Always make requests by using Secure HTTP (HTTPS) tooensure that your credentials are securely sent toohello server.</span></span>
>
> <span data-ttu-id="8d84d-116">Ao usar os comandos de saudação nesta seção, substitua `USERNAME` com cluster do hello usuário tooauthenticate toohello e substituir `PASSWORD` com senha Olá Olá conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="8d84d-116">When using hello commands in this section, replace `USERNAME` with hello user tooauthenticate toohello cluster, and replace `PASSWORD` with hello password for hello user account.</span></span> <span data-ttu-id="8d84d-117">Substituir `CLUSTERNAME` com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="8d84d-117">Replace `CLUSTERNAME` with hello name of your cluster.</span></span>
>


1. <span data-ttu-id="8d84d-118">De uma linha de comando, use Olá tooverify de comando que você pode conectar o cluster do HDInsight tooyour a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d84d-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="8d84d-119">Você deve receber Olá resposta JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d84d-119">You should receive hello following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="8d84d-120">Estes são os parâmetros de saudação usados neste comando:</span><span class="sxs-lookup"><span data-stu-id="8d84d-120">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="8d84d-121">**-u**: Olá nome de usuário e senha usados tooauthenticate solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="8d84d-121">**-u**: hello user name and password used tooauthenticate hello request</span></span>
    * <span data-ttu-id="8d84d-122">**-G**: indica que essa solicitação é uma solicitação GET</span><span class="sxs-lookup"><span data-stu-id="8d84d-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="8d84d-123">Olá a partir da URL de saudação **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, Olá mesmo para todas as solicitações.</span><span class="sxs-lookup"><span data-stu-id="8d84d-123">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="8d84d-124">caminho de saudação **/status**, indica que a solicitação Olá status Olá tooreturn WebHCat (também conhecido como Templeton) para o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d84d-124">hello path, **/status**, indicates that hello request is tooreturn hello status of WebHCat (also known as Templeton) for hello server.</span></span>

2. <span data-ttu-id="8d84d-125">Use Olá código toosubmit um cluster de toohello de trabalho de Pig latino a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d84d-125">Use hello following code toosubmit a Pig Latin job toohello cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="8d84d-126">Estes são os parâmetros de saudação usados neste comando:</span><span class="sxs-lookup"><span data-stu-id="8d84d-126">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="8d84d-127">**-d**: porque `-G` não for usado, solicitação Olá padrões toohello método de POSTAGEM.</span><span class="sxs-lookup"><span data-stu-id="8d84d-127">**-d**: Because `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="8d84d-128">`-d`Especifica valores de dados de saudação que são enviados com a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d84d-128">`-d` specifies hello data values that are sent with hello request.</span></span>

    * <span data-ttu-id="8d84d-129">**User.Name**: usuário de saudação que está executando o comando Olá</span><span class="sxs-lookup"><span data-stu-id="8d84d-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="8d84d-130">**executar**: Olá Pig latino instruções tooexecute</span><span class="sxs-lookup"><span data-stu-id="8d84d-130">**execute**: hello Pig Latin statements tooexecute</span></span>
    * <span data-ttu-id="8d84d-131">**statusdir**: diretório Olá Olá status para esse trabalho é gravado</span><span class="sxs-lookup"><span data-stu-id="8d84d-131">**statusdir**: hello directory that hello status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="8d84d-132">Observe que os espaços de saudação em instruções de Pig latino serão substituídos por Olá `+` quando usado com a rotação de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8d84d-132">Notice that hello spaces in Pig Latin statements are replaced by hello `+` character when used with Curl.</span></span>

    <span data-ttu-id="8d84d-133">Este comando deve retornar uma ID de trabalho que pode ser usado toocheck Olá status do trabalho Olá, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8d84d-133">This command should return a job ID that can be used toocheck hello status of hello job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="8d84d-134">status de Olá toocheck de trabalho Olá Olá use comandos a seguir</span><span class="sxs-lookup"><span data-stu-id="8d84d-134">toocheck hello status of hello job, use hello following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="8d84d-135">Substituir `JOBID` com hello valor retornado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="8d84d-135">Replace `JOBID` with hello value returned in hello previous step.</span></span> <span data-ttu-id="8d84d-136">Por exemplo, se hello retornar o valor era `{"id":"job_1415651640909_0026"}`, em seguida, `JOBID` é `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="8d84d-136">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="8d84d-137">Se o trabalho de saudação tiver sido concluída, o estado de Olá é **êxito**.</span><span class="sxs-lookup"><span data-stu-id="8d84d-137">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8d84d-138">Essa solicitação de ondulação retorna um JavaScript Object Notation (JSON) um documento com informações sobre o trabalho de saudação e jq é tooretrieve usado Olá somente o valor de estado.</span><span class="sxs-lookup"><span data-stu-id="8d84d-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job, and jq is used tooretrieve only hello state value.</span></span>

## <span data-ttu-id="8d84d-139"><a id="results"></a>Exibir resultados</span><span class="sxs-lookup"><span data-stu-id="8d84d-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="8d84d-140">Quando o estado de saudação do trabalho Olá foi alterado muito**êxito**, você pode recuperar os resultados de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d84d-140">When hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job.</span></span> <span data-ttu-id="8d84d-141">Olá `statusdir` parâmetro passado com hello consulta contém o local de Olá Olá do arquivo de saída; nesse caso, `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="8d84d-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="8d84d-142">HDInsight pode usar o armazenamento do Azure ou repositório Azure Data Lake como armazenamento de dados padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d84d-142">HDInsight can use either Azure Storage or Azure Data Lake Store as hello default data store.</span></span> <span data-ttu-id="8d84d-143">Há tooget de várias maneiras em dados Olá dependendo de qual delas você usar.</span><span class="sxs-lookup"><span data-stu-id="8d84d-143">There are various ways tooget at hello data depending on which one you use.</span></span> <span data-ttu-id="8d84d-144">Para obter mais informações, consulte a seção de armazenamento de saudação do hello [HDInsight baseados em Linux informações](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) documento.</span><span class="sxs-lookup"><span data-stu-id="8d84d-144">For more information, see hello storage section of hello [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="8d84d-145"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="8d84d-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="8d84d-146">Conforme demonstrado neste documento, você pode usar um toorun de solicitação HTTP bruto, o monitor e exibir resultados de saudação de trabalhos de Pig no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8d84d-146">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="8d84d-147">Para obter mais informações sobre a interface REST de saudação usado neste artigo, consulte Olá [WebHCat referência](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="8d84d-147">For more information about hello REST interface used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="8d84d-148"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8d84d-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="8d84d-149">Para obter informações gerais sobre o Pig no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8d84d-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="8d84d-150">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d84d-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="8d84d-151">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8d84d-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="8d84d-152">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d84d-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="8d84d-153">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d84d-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
