---
title: "aaaUse Hadoop Sqoop com ondulação no HDInsight - Azure | Microsoft Docs"
description: "Saiba como tooremotely enviar Sqoop trabalhos tooHDInsight usando rotação."
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
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="8c1b6-103">Executar trabalhos do Sqoop com Hadoop no HDInsight com Curl</span><span class="sxs-lookup"><span data-stu-id="8c1b6-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="8c1b6-104">Saiba como cluster de toouse ondulação toorun Sqoop trabalhos em um Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-104">Learn how toouse Curl toorun Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="8c1b6-105">Ondulação é usado toodemonstrate como você pode interagir com o HDInsight usando toorun bruto de solicitações HTTP, o monitor e recuperar resultados de saudação de trabalhos de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun, monitor, and retrieve hello results of Sqoop jobs.</span></span> <span data-ttu-id="8c1b6-106">Isso funciona usando Olá WebHCat REST API (anteriormente conhecido como Templeton) fornecida pelo seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-106">This works by using hello WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="8c1b6-107">Se você já estiver familiarizado com o uso de servidores baseados em Linux Hadoop, mas é tooHDInsight novo, consulte [informações sobre como usar o HDInsight no Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="8c1b6-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="8c1b6-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8c1b6-108">Prerequisites</span></span>
<span data-ttu-id="8c1b6-109">toocomplete Olá etapas neste artigo, você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="8c1b6-109">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="8c1b6-110">Um Hadoop no cluster HDInsight (baseado em Linux ou Windows)</span><span class="sxs-lookup"><span data-stu-id="8c1b6-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="8c1b6-111">Curl</span><span class="sxs-lookup"><span data-stu-id="8c1b6-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="8c1b6-112">jq</span><span class="sxs-lookup"><span data-stu-id="8c1b6-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="8c1b6-113">Enviar trabalhos do Sqoop usando o Curl</span><span class="sxs-lookup"><span data-stu-id="8c1b6-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="8c1b6-114">Ondulação ou com qualquer outra comunicação REST WebHCat, você deve autenticar solicitações de saudação fornecendo Olá nome e a senha de administrador de cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-114">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="8c1b6-115">Você também deve usar o nome do cluster hello como parte do identificador de recurso uniforme (URI) do hello usado server de toohello toosend Olá solicitações.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-115">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server.</span></span>
> 
> <span data-ttu-id="8c1b6-116">Para comandos Olá nesta seção, substitua **USERNAME** com cluster do hello usuário tooauthenticate toohello e substituir **senha** com senha Olá Olá conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-116">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="8c1b6-117">Substituir **CLUSTERNAME** com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-117">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
> 
> <span data-ttu-id="8c1b6-118">Olá API REST é protegida por meio de [autenticação básica](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="8c1b6-118">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="8c1b6-119">Você sempre deve fazer solicitações usando Secure HTTP (HTTPS) toohelp Certifique-se de que suas credenciais são enviadas com segurança toohello server.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-119">You should always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>
> 
> 

1. <span data-ttu-id="8c1b6-120">De uma linha de comando, use Olá tooverify de comando que você pode conectar o cluster do HDInsight tooyour a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c1b6-120">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="8c1b6-121">Você deve receber uma resposta semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c1b6-121">You should receive a response similar toohello following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="8c1b6-122">Estes são os parâmetros de saudação usados neste comando:</span><span class="sxs-lookup"><span data-stu-id="8c1b6-122">hello parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="8c1b6-123">**-u** -Olá nome de usuário e senha usados tooauthenticate solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-123">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="8c1b6-124">**-G** - indica que se trata de uma solicitação GET.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="8c1b6-125">Olá a partir da URL de saudação **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, será hello mesmo para todas as solicitações.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-125">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be hello same for all requests.</span></span> <span data-ttu-id="8c1b6-126">caminho de saudação **/status**, indica que a solicitação Olá tooreturn um status de WebHCat (também conhecido como Templeton) para o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-126">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> 
2. <span data-ttu-id="8c1b6-127">Use Olá toosubmit um trabalho de sqoop a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c1b6-127">Use hello following toosubmit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="8c1b6-128">Estes são os parâmetros de saudação usados neste comando:</span><span class="sxs-lookup"><span data-stu-id="8c1b6-128">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="8c1b6-129">**-d** - desde `-G` não for usado, solicitação Olá padrões toohello método de POSTAGEM.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-129">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="8c1b6-130">`-d`Especifica valores de dados de saudação que são enviados com a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-130">`-d` specifies hello data values that are sent with hello request.</span></span>

        * <span data-ttu-id="8c1b6-131">**User.Name** -usuário Olá que está executando o comando hello.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-131">**user.name** - hello user that is running hello command.</span></span>

        * <span data-ttu-id="8c1b6-132">**comando** -Olá Sqoop tooexecute de comando.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-132">**command** - hello Sqoop command tooexecute.</span></span>

        * <span data-ttu-id="8c1b6-133">**statusdir** -diretório Olá Olá status para esse trabalho será gravada.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-133">**statusdir** - hello directory that hello status for this job will be written to.</span></span>

    <span data-ttu-id="8c1b6-134">Este comando deve retornar uma ID de trabalho que pode ser toocheck usado Olá status do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-134">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="8c1b6-135">status de saudação toocheck de trabalho de hello, Olá use comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-135">toocheck hello status of hello job, use hello following command.</span></span> <span data-ttu-id="8c1b6-136">Substituir **JOBID** com hello valor retornado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-136">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="8c1b6-137">Por exemplo, se hello retornar o valor era `{"id":"job_1415651640909_0026"}`, em seguida, **JOBID** seria `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-137">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="8c1b6-138">Se o trabalho de saudação tiver sido concluída, o estado de Olá será **êxito**.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-138">If hello job has finished, hello state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8c1b6-139">Essa solicitação de ondulação retorna um documento JSON JavaScript Object Notation () com informações sobre o trabalho de saudação; jq é usada tooretrieve Olá apenas o valor de estado.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job; jq is used tooretrieve only hello state value.</span></span>
   > 
   > 
2. <span data-ttu-id="8c1b6-140">Depois que o estado de saudação do trabalho Olá mudou muito**êxito**, você pode recuperar os resultados de saudação do trabalho de saudação do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-140">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="8c1b6-141">Olá `statusdir` parâmetro passado com hello consulta contém o local de Olá Olá do arquivo de saída; nesse caso, **wasb: / / / exemplo/ondulação**.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="8c1b6-142">Esse endereço armazena saída de saudação do trabalho de saudação em Olá **exemplo/ondulação** diretório no contêiner de armazenamento padrão de saudação usada por seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-142">This address stores hello output of hello job in hello **example/curl** directory on hello default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="8c1b6-143">Você pode listar e baixar esses arquivos usando Olá [CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8c1b6-143">You can list and download these files by using hello [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="8c1b6-144">Por exemplo, arquivos toolist **exemplo/ondulação**, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c1b6-144">For example, toolist files in **example/curl**, use hello following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="8c1b6-145">toodownload um arquivo, use a seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="8c1b6-145">toodownload a file, use hello following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="8c1b6-146">Você deve especificar nome de conta de armazenamento Olá que contém o blob hello usando Olá `-a` e `-k` parâmetros ou conjunto Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_acesso\_chave** variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-146">You must either specify hello storage account name that contains hello blob by using hello `-a` and `-k` parameters, or set hello **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="8c1b6-147">Consulte <a href="hdinsight-upload-data.md" target="_blank"para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="8c1b6-148">Limitações</span><span class="sxs-lookup"><span data-stu-id="8c1b6-148">Limitations</span></span>
* <span data-ttu-id="8c1b6-149">A exportação em massa - HDInsight baseados em Linux com, Olá Sqoop conector usado tooexport dados tooMicrosoft do SQL Server ou banco de dados do SQL Azure atualmente não dá suporte para inserções em massa.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-149">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="8c1b6-150">Envio em lote - com HDInsight baseados em Linux, ao usar o hello `-batch` opção ao executar inserções, Sqoop executará várias inserções em vez de envio em lote as operações de inserção hello.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-150">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="8c1b6-151">Resumo</span><span class="sxs-lookup"><span data-stu-id="8c1b6-151">Summary</span></span>
<span data-ttu-id="8c1b6-152">Conforme demonstrado neste documento, você pode usar um toorun de solicitação HTTP bruto, o monitor e exibir os resultados dos trabalhos de Sqoop Olá no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-152">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="8c1b6-153">Para obter mais informações sobre a interface REST de saudação usado neste artigo, consulte Olá <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">guia Sqoop REST API</a>.</span><span class="sxs-lookup"><span data-stu-id="8c1b6-153">For more information on hello REST interface used in this article, see hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c1b6-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8c1b6-154">Next steps</span></span>
<span data-ttu-id="8c1b6-155">Para obter informações gerais sobre o Hive com HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8c1b6-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="8c1b6-156">Usar o Sqoop com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8c1b6-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="8c1b6-157">Para obter informações sobre outras maneiras que você pode trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8c1b6-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="8c1b6-158">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8c1b6-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="8c1b6-159">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8c1b6-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="8c1b6-160">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8c1b6-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


