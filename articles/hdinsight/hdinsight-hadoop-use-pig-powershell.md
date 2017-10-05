---
title: "Usar o Pig do Hadoop com o PowerShell no HDInsight – Azure | Microsoft Docs"
description: Saiba como enviar trabalhos do Pig para um cluster do Hadoop no HDInsight usando o PowerShell do Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 28904b07609ffb40a8195278fd1afd3957896733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-run-pig-jobs-with-hdinsight"></a><span data-ttu-id="87b0c-103">Usar o Azure PowerShell para executar trabalhos do Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="87b0c-103">Use Azure PowerShell to run Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="87b0c-104">Este documento fornece um exemplo de uso do PowerShell do Azure para enviar trabalhos do Pig para um Hadoop no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87b0c-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="87b0c-105">O Pig permite que você escreva trabalhos do MapReduce usando uma linguagem (Pig Latin) que modela transformações de dados, em vez das funções mapear e reduzir.</span><span class="sxs-lookup"><span data-stu-id="87b0c-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="87b0c-106">Esse documento não fornece uma descrição detalhada do que fazem as instruções Pig Latin usadas nos exemplos.</span><span class="sxs-lookup"><span data-stu-id="87b0c-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span></span> <span data-ttu-id="87b0c-107">Para obter informações sobre o Pig Latin usado neste exemplo, consulte [Usar o Pig com o Hadoop no HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="87b0c-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="87b0c-108"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="87b0c-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="87b0c-109">**Um cluster Azure HDInsight**</span><span class="sxs-lookup"><span data-stu-id="87b0c-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="87b0c-110">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="87b0c-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="87b0c-111">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="87b0c-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="87b0c-112">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="87b0c-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="87b0c-113"><a id="powershell"></a>Executar trabalhos do Pig usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="87b0c-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="87b0c-114">O PowerShell do Azure fornece *cmdlets* que permitem executar remotamente trabalhos do Pig no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87b0c-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="87b0c-115">Internamente, o PowerShell usa chamadas REST para [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) em execução no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87b0c-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span></span>

<span data-ttu-id="87b0c-116">Os seguintes cmdlets são usados ao executar trabalhos do Pig em um cluster HDInsight remoto:</span><span class="sxs-lookup"><span data-stu-id="87b0c-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="87b0c-117">**Login-AzureRmAccount**: autentica o Azure PowerShell para sua Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="87b0c-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription</span></span>
* <span data-ttu-id="87b0c-118">**New-AzureRmHDInsightPigJobDefinition**: cria uma *definição de trabalho* usando as instruções de Pig Latin especificadas</span><span class="sxs-lookup"><span data-stu-id="87b0c-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements</span></span>
* <span data-ttu-id="87b0c-119">**Start-AzureRmHDInsightJob**: envia a definição do trabalho para o HDInsight, inicia o trabalho e retorna um objeto *job* que pode ser usado para verificar o status do trabalho</span><span class="sxs-lookup"><span data-stu-id="87b0c-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="87b0c-120">**Wait-AzureRmHDInsightJob**: usa o objeto de trabalho para verificar o status do trabalho.</span><span class="sxs-lookup"><span data-stu-id="87b0c-120">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="87b0c-121">Ele aguarda até que o trabalho seja concluído ou que o tempo de espera seja excedido.</span><span class="sxs-lookup"><span data-stu-id="87b0c-121">It waits until the job has completed, or the wait time has been exceeded.</span></span>
* <span data-ttu-id="87b0c-122">**Get-AzureRmHDInsightJobOutput**: usado para recuperar a saída do trabalho</span><span class="sxs-lookup"><span data-stu-id="87b0c-122">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>

<span data-ttu-id="87b0c-123">As etapas a seguir demonstram como usar esses cmdlets para executar um trabalho no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87b0c-123">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="87b0c-124">Usando um editor, salve o código a seguir como **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="87b0c-124">Using an editor, save the following code as **pigjob.ps1**.</span></span>

    <span data-ttu-id="87b0c-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span><span class="sxs-lookup"><span data-stu-id="87b0c-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span></span>

1. <span data-ttu-id="87b0c-126">Abra um novo prompt de comando do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87b0c-126">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="87b0c-127">Altere os diretórios para o local do arquivo **pigjob.ps1** e use o seguinte comando para executar o script:</span><span class="sxs-lookup"><span data-stu-id="87b0c-127">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="87b0c-128">Você deverá fazer logon em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="87b0c-128">You are prompted to log in to your Azure subscription.</span></span> <span data-ttu-id="87b0c-129">Em seguida, você deverá fornecer o nome da conta e senha de Administrador/HTTPs do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87b0c-129">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span></span>

2. <span data-ttu-id="87b0c-130">Quando o trabalho for concluído, ele deverá retornar informações semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="87b0c-130">When the job completes, it should return information similar to the following text:</span></span>

        Start the Pig job ...
        Wait for the Pig job to complete ...
        Display the standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="87b0c-131"><a id="troubleshooting"></a>Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="87b0c-131"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="87b0c-132">Se nenhuma informação for retornada quando o trabalho for concluído, um erro pode ter ocorrido durante o processamento.</span><span class="sxs-lookup"><span data-stu-id="87b0c-132">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="87b0c-133">Para exibir informações de erro para esse trabalho, adicione o seguinte ao final do arquivo **pigjob.ps1** , salve o arquivo e execute-o novamente.</span><span class="sxs-lookup"><span data-stu-id="87b0c-133">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print the output of the Pig job.
    Write-Host "Display the standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="87b0c-134">Isso retorna as informações que foram gravadas em STDERR no servidor quando você executou o trabalho, e pode ajudar a determinar por que o trabalho está falhando.</span><span class="sxs-lookup"><span data-stu-id="87b0c-134">This returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="87b0c-135"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="87b0c-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="87b0c-136">Como você pode ver, o PowerShell do Azure fornece uma maneira fácil de executar trabalhos do Pig em um cluster HDInsight, monitorar o status do trabalho e recuperar a saída.</span><span class="sxs-lookup"><span data-stu-id="87b0c-136">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="87b0c-137"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="87b0c-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="87b0c-138">Para obter informações gerais sobre o Pig no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="87b0c-138">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="87b0c-139">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="87b0c-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="87b0c-140">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="87b0c-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="87b0c-141">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="87b0c-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="87b0c-142">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="87b0c-142">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
