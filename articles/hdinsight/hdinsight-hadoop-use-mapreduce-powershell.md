---
title: "Usar o MapReduce e o PowerShell com Hadoop – Azure HDInsight | Microsoft Docs"
description: Aprenda a usar o PowerShell para executar trabalhos MapReduce remotamente com Hadoop no HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: c3801573808709f29cb1e563ac803f225a28cafc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="84137-103">Executar trabalhos MapReduce com Hadoop no HDInsight usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="84137-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="84137-104">Esse documento fornece um exemplo de uso do PowerShell do Azure para executar um trabalho MapReduce em um Hadoop no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="84137-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="84137-105"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="84137-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="84137-106">**Um cluster Azure HDInsight (Hadoop no HDInsight)**</span><span class="sxs-lookup"><span data-stu-id="84137-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="84137-107">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="84137-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="84137-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="84137-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="84137-109">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="84137-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="84137-110"><a id="powershell"></a>Executar um trabalho MapReduce usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="84137-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="84137-111">O PowerShell do Azure fornece *cmdlets* que permitem executar remotamente trabalhos MapReduce no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="84137-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="84137-112">Internamente, isso é feito por meio de chamadas REST para [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (anteriormente chamado de Templeton) em execução no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="84137-112">Internally, this is accomplished by using REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span></span>

<span data-ttu-id="84137-113">Os cmdlets a seguir são usados ao executar trabalhos MapReduce em um cluster HDInsight remoto.</span><span class="sxs-lookup"><span data-stu-id="84137-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="84137-114">**Login-AzureRmAccount**: autentica o Azure PowerShell para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="84137-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span></span>

* <span data-ttu-id="84137-115">**New-AzureRmHDInsightMapReduceJobDefinition**: cria uma nova *definição de trabalho* usando as informações especificadas do MapReduce.</span><span class="sxs-lookup"><span data-stu-id="84137-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span></span>

* <span data-ttu-id="84137-116">**Start-AzureRmHDInsightJob**: envia a definição do trabalho para o HDInsight, inicia o trabalho e retorna um objeto *job* que pode ser usado para verificar o status do trabalho.</span><span class="sxs-lookup"><span data-stu-id="84137-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job.</span></span>

* <span data-ttu-id="84137-117">**Wait-AzureRmHDInsightJob**: usa o objeto de trabalho para verificar o status do trabalho.</span><span class="sxs-lookup"><span data-stu-id="84137-117">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="84137-118">Ele aguarda até que o trabalho seja concluído ou o tempo de espera seja excedido.</span><span class="sxs-lookup"><span data-stu-id="84137-118">It waits until the job completes or the wait time is exceeded.</span></span>

* <span data-ttu-id="84137-119">**Get-AzureRmHDInsightJobOutput**: usado para recuperar a saída do trabalho.</span><span class="sxs-lookup"><span data-stu-id="84137-119">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="84137-120">As etapas a seguir demonstram como usar esses cmdlets para executar um trabalho no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="84137-120">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="84137-121">Usando um editor, salve o código a seguir como **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="84137-121">Using an editor, save the following code as **mapreducejob.ps1**.</span></span>

    <span data-ttu-id="84137-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span><span class="sxs-lookup"><span data-stu-id="84137-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span></span>

2. <span data-ttu-id="84137-123">Abra um novo prompt de comando do **PowerShell do Azure** .</span><span class="sxs-lookup"><span data-stu-id="84137-123">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="84137-124">Altere os diretórios para o local do arquivo **mapreducejob.ps1** e use o seguinte comando para executar o script:</span><span class="sxs-lookup"><span data-stu-id="84137-124">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="84137-125">Quando você executa o script, o nome do cluster do HDInsight e o nome da conta de HTTPS/Admin e a senha para o cluster são solicitados.</span><span class="sxs-lookup"><span data-stu-id="84137-125">When you run the script, you are prompted for the name of the HDInsight cluster and the HTTPS/Admin account name and password for the cluster.</span></span> <span data-ttu-id="84137-126">Você também poderá receber uma solicitação para autenticar a sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="84137-126">You may also be prompted to authenticate to your Azure subscription.</span></span>

3. <span data-ttu-id="84137-127">Quando o trabalho for concluído, você receberá uma saída semelhante ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="84137-127">When the job completes, you receive output similar to the following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="84137-128">Essa saída indica que o trabalho foi concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="84137-128">This output indicates that the job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="84137-129">Se o **ExitCode** for um valor diferente de 0, consulte [Solução de problemas](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="84137-129">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="84137-130">Este exemplo também armazena os arquivos baixados em um arquivo **output.txt** no diretório do qual você executa o script.</span><span class="sxs-lookup"><span data-stu-id="84137-130">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="84137-131">Exibir saída</span><span class="sxs-lookup"><span data-stu-id="84137-131">View output</span></span>

<span data-ttu-id="84137-132">Abra o arquivo **output.txt** em um editor de texto para ver as palavras e contagens produzidas pelo trabalho.</span><span class="sxs-lookup"><span data-stu-id="84137-132">Open the **output.txt** file in a text editor to see the words and counts produced by the job.</span></span>

> [!NOTE]
> <span data-ttu-id="84137-133">Os arquivos de saída de um trabalho MapReduce são imutáveis.</span><span class="sxs-lookup"><span data-stu-id="84137-133">The output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="84137-134">Portanto, se você executar esse exemplo novamente, será necessário alterar o nome do arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="84137-134">So if you rerun this sample, you need to change the name of the output file.</span></span>

## <span data-ttu-id="84137-135"><a id="troubleshooting"></a>Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="84137-135"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="84137-136">Se nenhuma informação for retornada quando o trabalho for concluído, um erro pode ter ocorrido durante o processamento.</span><span class="sxs-lookup"><span data-stu-id="84137-136">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="84137-137">Para exibir informações de erro para esse trabalho, adicione o seguinte comando ao final do arquivo **mapreducejob.ps1** , depois salve o arquivo e execute-o novamente.</span><span class="sxs-lookup"><span data-stu-id="84137-137">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="84137-138">Esse cmdlet retorna as informações que foram gravadas em STDERR no servidor quando o trabalho foi executado e pode ajudar a determinar por que o trabalho está falhando.</span><span class="sxs-lookup"><span data-stu-id="84137-138">This cmdlet returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="84137-139"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="84137-139"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="84137-140">Como você pode ver, o PowerShell do Azure fornece uma maneira fácil de executar trabalhos MapReduce em um cluster HDInsight, monitorar o status do trabalho e recuperar a saída.</span><span class="sxs-lookup"><span data-stu-id="84137-140">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="84137-141"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="84137-141"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="84137-142">Para obter informações gerais sobre trabalhos de MapReduce no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="84137-142">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="84137-143">Usar o MapReduce no Hadoop do HDInsight</span><span class="sxs-lookup"><span data-stu-id="84137-143">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="84137-144">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="84137-144">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="84137-145">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="84137-145">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="84137-146">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="84137-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
