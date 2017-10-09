---
title: aaaUse Pig do Hadoop com o PowerShell no HDInsight - Azure | Microsoft Docs
description: Saiba como cluster de toosubmit Pig trabalhos tooa Hadoop no HDInsight usando o PowerShell do Azure.
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
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a><span data-ttu-id="3913f-103">Use trabalhos de Pig do Azure PowerShell toorun com HDInsight</span><span class="sxs-lookup"><span data-stu-id="3913f-103">Use Azure PowerShell toorun Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="3913f-104">Este documento fornece um exemplo de uso do Azure PowerShell toosubmit Pig trabalhos tooa Hadoop no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3913f-104">This document provides an example of using Azure PowerShell toosubmit Pig jobs tooa Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="3913f-105">Pig permite que os trabalhos de MapReduce toowrite usando uma linguagem (Pig latino) que modela transformações de dados, em vez de mapear e reduzir as funções.</span><span class="sxs-lookup"><span data-stu-id="3913f-105">Pig allows you toowrite MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="3913f-106">Este documento não fornece uma descrição detalhada do que fazem instruções de Pig latino Olá usadas nos exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="3913f-106">This document does not provide a detailed description of what hello Pig Latin statements used in hello examples do.</span></span> <span data-ttu-id="3913f-107">Para obter informações sobre Olá Pig latino usado neste exemplo, consulte [usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="3913f-107">For information about hello Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="3913f-108"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3913f-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="3913f-109">**Um cluster Azure HDInsight**</span><span class="sxs-lookup"><span data-stu-id="3913f-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3913f-110">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3913f-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3913f-111">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3913f-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="3913f-112">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="3913f-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="3913f-113"><a id="powershell"></a>Executar trabalhos do Pig usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="3913f-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="3913f-114">PowerShell do Azure fornece *cmdlets* que permitem que você tooremotely executar trabalhos de Pig no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3913f-114">Azure PowerShell provides *cmdlets* that allow you tooremotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="3913f-115">Internamente, o PowerShell usa chamadas REST muito[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) em execução no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="3913f-115">Internally, PowerShell uses REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="3913f-116">cmdlets a seguir Hello são usados durante a execução de trabalhos de Pig em um cluster HDInsight remoto:</span><span class="sxs-lookup"><span data-stu-id="3913f-116">hello following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="3913f-117">**Logon AzureRmAccount**: autentica o Azure PowerShell tooyour assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="3913f-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure Subscription</span></span>
* <span data-ttu-id="3913f-118">**Novo AzureRmHDInsightPigJobDefinition**: cria um *definição de trabalho* usando Olá especificado Pig latino instruções</span><span class="sxs-lookup"><span data-stu-id="3913f-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using hello specified Pig Latin statements</span></span>
* <span data-ttu-id="3913f-119">**Iniciar AzureRmHDInsightJob**: envia Olá tooHDInsight de definição de trabalho, inicia o trabalho de saudação e retorna um *trabalho* objeto que pode ser toocheck usado Olá status do trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="3913f-119">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="3913f-120">**Espera-AzureRmHDInsightJob**: usa Olá objeto toocheck Olá status do trabalho do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="3913f-120">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="3913f-121">Ele aguarda até que o trabalho Olá foi concluído ou tempo de espera de saudação foi excedido.</span><span class="sxs-lookup"><span data-stu-id="3913f-121">It waits until hello job has completed, or hello wait time has been exceeded.</span></span>
* <span data-ttu-id="3913f-122">**Get-AzureRmHDInsightJobOutput**: usado tooretrieve saída de saudação do trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="3913f-122">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>

<span data-ttu-id="3913f-123">Olá etapas a seguir demonstram como toouse toorun esses cmdlets um trabalho em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3913f-123">hello following steps demonstrate how toouse these cmdlets toorun a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="3913f-124">Usando um editor, salvar Olá código como a seguir **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="3913f-124">Using an editor, save hello following code as **pigjob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. <span data-ttu-id="3913f-125">Abra um novo prompt de comando do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3913f-125">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="3913f-126">Alterar diretórios toohello local de saudação **pigjob.ps1** de arquivo e use Olá script do comando toorun Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3913f-126">Change directories toohello location of hello **pigjob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="3913f-127">Você está toolog solicitada no tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="3913f-127">You are prompted toolog in tooyour Azure subscription.</span></span> <span data-ttu-id="3913f-128">Em seguida, você será solicitado para Olá HTTPs/Admin nome e a senha para o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="3913f-128">Then, you are asked for hello HTTPs/Admin account name and password for hello HDInsight cluster.</span></span>

2. <span data-ttu-id="3913f-129">Quando o trabalho de saudação for concluído, ele deverá retornar informações toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="3913f-129">When hello job completes, it should return information similar toohello following text:</span></span>

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="3913f-130"><a id="troubleshooting"></a>Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="3913f-130"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="3913f-131">Se nenhuma informação é retornada quando Olá trabalho for concluído, um erro pode ter ocorrido durante o processamento.</span><span class="sxs-lookup"><span data-stu-id="3913f-131">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="3913f-132">informações de erro tooview para este trabalho, adicionar Olá após o término do comando toohello de saudação **pigjob.ps1** arquivo, salve-o e, em seguida, execute-o novamente.</span><span class="sxs-lookup"><span data-stu-id="3913f-132">tooview error information for this job, add hello following command toohello end of hello **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="3913f-133">Isso retorna informações de saudação escrito tooSTDERR no servidor de saudação quando você executou o trabalho de saudação e pode ajudar a determinar por que o trabalho de saudação está falhando.</span><span class="sxs-lookup"><span data-stu-id="3913f-133">This returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="3913f-134"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="3913f-134"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="3913f-135">Como você pode ver, o Azure PowerShell fornece uma maneira fácil de toorun trabalhos de Pig em um cluster HDInsight, monitora o status de trabalho hello e recuperar Olá saída.</span><span class="sxs-lookup"><span data-stu-id="3913f-135">As you can see, Azure PowerShell provides an easy way toorun Pig jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="3913f-136"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3913f-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="3913f-137">Para obter informações gerais sobre o Pig no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3913f-137">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="3913f-138">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3913f-138">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="3913f-139">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3913f-139">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="3913f-140">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3913f-140">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="3913f-141">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3913f-141">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
