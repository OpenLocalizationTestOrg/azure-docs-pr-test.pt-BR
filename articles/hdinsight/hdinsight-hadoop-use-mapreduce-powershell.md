---
title: aaaUse MapReduce e PowerShell com o Hadoop - HDInsight do Azure | Microsoft Docs
description: Saiba como toouse PowerShell tooremotely executar trabalhos de MapReduce com Hadoop no HDInsight.
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
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="e2bd0-103">Executar trabalhos MapReduce com Hadoop no HDInsight usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2bd0-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="e2bd0-104">Este documento fornece um exemplo de uso do Azure PowerShell toorun um trabalho de MapReduce em um Hadoop no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-104">This document provides an example of using Azure PowerShell toorun a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="e2bd0-105"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e2bd0-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="e2bd0-106">**Um cluster Azure HDInsight (Hadoop no HDInsight)**</span><span class="sxs-lookup"><span data-stu-id="e2bd0-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e2bd0-107">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e2bd0-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e2bd0-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="e2bd0-109">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="e2bd0-110"><a id="powershell"></a>Executar um trabalho MapReduce usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="e2bd0-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="e2bd0-111">PowerShell do Azure fornece *cmdlets* que permitem que você tooremotely executar trabalhos de MapReduce no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-111">Azure PowerShell provides *cmdlets* that allow you tooremotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="e2bd0-112">Internamente, isso é feito por meio de chamadas REST muito[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (anteriormente chamado de Templeton) em execução no hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-112">Internally, this is accomplished by using REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="e2bd0-113">cmdlets a seguir Hello são usados durante a execução de trabalhos de MapReduce em um cluster HDInsight remoto.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-113">hello following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="e2bd0-114">**Logon AzureRmAccount**: autentica o Azure PowerShell tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription.</span></span>

* <span data-ttu-id="e2bd0-115">**Novo AzureRmHDInsightMapReduceJobDefinition**: cria um novo *definição de trabalho* usando Olá especificar informações de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using hello specified MapReduce information.</span></span>

* <span data-ttu-id="e2bd0-116">**Iniciar AzureRmHDInsightJob**: envia Olá tooHDInsight de definição de trabalho, inicia o trabalho de saudação e retorna um *trabalho* objeto que pode ser toocheck usado Olá status do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-116">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job.</span></span>

* <span data-ttu-id="e2bd0-117">**Espera-AzureRmHDInsightJob**: usa Olá objeto toocheck Olá status do trabalho do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-117">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="e2bd0-118">Ele aguardará até Olá trabalho for concluído ou tempo de espera de saudação for excedido.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-118">It waits until hello job completes or hello wait time is exceeded.</span></span>

* <span data-ttu-id="e2bd0-119">**Get-AzureRmHDInsightJobOutput**: usado tooretrieve saída de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-119">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job.</span></span>

<span data-ttu-id="e2bd0-120">Olá etapas a seguir demonstram como toouse toorun esses cmdlets um trabalho em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-120">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="e2bd0-121">Usando um editor, salvar Olá código como a seguir **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-121">Using an editor, save hello following code as **mapreducejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. <span data-ttu-id="e2bd0-122">Abra um novo prompt de comando do **PowerShell do Azure** .</span><span class="sxs-lookup"><span data-stu-id="e2bd0-122">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="e2bd0-123">Alterar diretórios toohello local de saudação **mapreducejob.ps1** de arquivo e use Olá script do comando toorun Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2bd0-123">Change directories toohello location of hello **mapreducejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="e2bd0-124">Quando você executa o script hello, você será solicitado a nome de saudação do cluster do HDInsight hello e nome de conta do hello HTTPS/administrador e senha para cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-124">When you run hello script, you are prompted for hello name of hello HDInsight cluster and hello HTTPS/Admin account name and password for hello cluster.</span></span> <span data-ttu-id="e2bd0-125">Você também pode ser solicitados tooauthenticate tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-125">You may also be prompted tooauthenticate tooyour Azure subscription.</span></span>

3. <span data-ttu-id="e2bd0-126">Ao Olá trabalho for concluído, você recebe saída toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2bd0-126">When hello job completes, you receive output similar toohello following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="e2bd0-127">Essa saída indica que o trabalho Olá foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-127">This output indicates that hello job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2bd0-128">Se hello **ExitCode** é um valor diferente de 0, consulte [solução de problemas](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="e2bd0-128">If hello **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="e2bd0-129">Este exemplo também armazena Olá baixado arquivos tooan **txt** arquivo hello no diretório em que você executar o script hello.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-129">This example also stores hello downloaded files tooan **output.txt** file in hello directory that you run hello script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="e2bd0-130">Exibir saída</span><span class="sxs-lookup"><span data-stu-id="e2bd0-130">View output</span></span>

<span data-ttu-id="e2bd0-131">Olá abrir **txt** palavras de arquivo em uma saudação de toosee do editor de texto e contagens produzido pelo trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-131">Open hello **output.txt** file in a text editor toosee hello words and counts produced by hello job.</span></span>

> [!NOTE]
> <span data-ttu-id="e2bd0-132">saudação de arquivos de saída de um trabalho de MapReduce são imutáveis.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-132">hello output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="e2bd0-133">Então se você executar novamente este exemplo, você precisa de nome de saudação do toochange saudação do arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-133">So if you rerun this sample, you need toochange hello name of hello output file.</span></span>

## <span data-ttu-id="e2bd0-134"><a id="troubleshooting"></a>Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="e2bd0-134"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="e2bd0-135">Se nenhuma informação é retornada quando Olá trabalho for concluído, um erro pode ter ocorrido durante o processamento.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-135">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="e2bd0-136">informações de erro tooview para este trabalho, adicionar Olá após o término do comando toohello de saudação **mapreducejob.ps1** arquivo, salve-o e, em seguida, execute-o novamente.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-136">tooview error information for this job, add hello following command toohello end of hello **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="e2bd0-137">Esse cmdlet retorna informações de saudação escrito tooSTDERR no servidor de saudação quando você executou o trabalho de saudação e pode ajudar a determinar por que o trabalho de saudação está falhando.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-137">This cmdlet returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="e2bd0-138"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="e2bd0-138"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="e2bd0-139">Como você pode ver, o Azure PowerShell fornece uma maneira fácil de toorun trabalhos MapReduce em um cluster HDInsight, monitora o status de trabalho hello e recuperar Olá saída.</span><span class="sxs-lookup"><span data-stu-id="e2bd0-139">As you can see, Azure PowerShell provides an easy way toorun MapReduce jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="e2bd0-140"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2bd0-140"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="e2bd0-141">Para obter informações gerais sobre trabalhos de MapReduce no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e2bd0-141">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="e2bd0-142">Usar o MapReduce no Hadoop do HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2bd0-142">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="e2bd0-143">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e2bd0-143">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="e2bd0-144">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2bd0-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e2bd0-145">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2bd0-145">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
