---
title: aaaUse Hive do Hadoop com o PowerShell no HDInsight - Azure | Microsoft Docs
description: Use consultas de Hive do PowerShell toorun no Hadoop no HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="674ed-103">Executar consultas Hive usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="674ed-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="674ed-104">Este documento fornece um exemplo de uso do Azure PowerShell Olá grupo de recursos do Azure toorun Hive em consultas em modo em uma Hadoop no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="674ed-104">This document provides an example of using Azure PowerShell in hello Azure Resource Group mode toorun Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="674ed-105">Este documento não fornece uma descrição detalhada do que fazem declarações do HiveQL Olá que são usadas nos exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="674ed-105">This document does not provide a detailed description of what hello HiveQL statements that are used in hello examples do.</span></span> <span data-ttu-id="674ed-106">Para obter informações sobre Olá HiveQL que é usado neste exemplo, consulte [uso de Hive do Hadoop no HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="674ed-106">For information on hello HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="674ed-107">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="674ed-107">**Prerequisites**</span></span>

* <span data-ttu-id="674ed-108">**Um cluster Azure HDInsight**: não importa se o cluster de saudação é Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="674ed-108">**An Azure HDInsight cluster**: It does not matter whether hello cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="674ed-109">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="674ed-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="674ed-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="674ed-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="674ed-111">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="674ed-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="674ed-112">Executar consultas do Hive usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="674ed-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="674ed-113">PowerShell do Azure fornece *cmdlets* que permitem que você tooremotely executar consultas de Hive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="674ed-113">Azure PowerShell provides *cmdlets* that allow you tooremotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="674ed-114">Internamente, os cmdlets Olá fazer chamadas REST muito[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="674ed-114">Internally, hello cmdlets make REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on hello HDInsight cluster.</span></span>

<span data-ttu-id="674ed-115">cmdlets a seguir Hello são usados ao executar consultas de Hive em um cluster HDInsight remoto:</span><span class="sxs-lookup"><span data-stu-id="674ed-115">hello following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="674ed-116">**Adicionar AzureRmAccount**: autentica o Azure PowerShell tooyour assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="674ed-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription</span></span>
* <span data-ttu-id="674ed-117">**Novo AzureRmHDInsightHiveJobDefinition**: cria um *definição de trabalho* usando Olá especificado HiveQL instruções</span><span class="sxs-lookup"><span data-stu-id="674ed-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using hello specified HiveQL statements</span></span>
* <span data-ttu-id="674ed-118">**Iniciar AzureRmHDInsightJob**: envia Olá tooHDInsight de definição de trabalho, inicia o trabalho de saudação e retorna um *trabalho* objeto que pode ser toocheck usado Olá status do trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="674ed-118">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="674ed-119">**Espera-AzureRmHDInsightJob**: usa Olá objeto toocheck Olá status do trabalho do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="674ed-119">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="674ed-120">Ele aguardará até Olá trabalho for concluído ou tempo de espera de saudação for excedido.</span><span class="sxs-lookup"><span data-stu-id="674ed-120">It waits until hello job completes or hello wait time is exceeded.</span></span>
* <span data-ttu-id="674ed-121">**Get-AzureRmHDInsightJobOutput**: usado tooretrieve saída de saudação do trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="674ed-121">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>
* <span data-ttu-id="674ed-122">**Invocar AzureRmHDInsightHiveJob**: usado toorun HiveQL instruções.</span><span class="sxs-lookup"><span data-stu-id="674ed-122">**Invoke-AzureRmHDInsightHiveJob**: Used toorun HiveQL statements.</span></span> <span data-ttu-id="674ed-123">Esta consulta de saudação do cmdlet blocos for concluída, em seguida, retorna os resultados de saudação</span><span class="sxs-lookup"><span data-stu-id="674ed-123">This cmdlet blocks hello query completes, then returns hello results</span></span>
* <span data-ttu-id="674ed-124">**Use AzureRmHDInsightCluster**: conjuntos Olá toouse de cluster atual para Olá **AzureRmHDInsightHiveJob Invoke** comando</span><span class="sxs-lookup"><span data-stu-id="674ed-124">**Use-AzureRmHDInsightCluster**: Sets hello current cluster toouse for hello **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="674ed-125">Olá etapas a seguir demonstram como toouse toorun esses cmdlets um trabalho em seu cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="674ed-125">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="674ed-126">Usando um editor, salvar Olá código como a seguir **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="674ed-126">Using an editor, save hello following code as **hivejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="674ed-127">Abra um novo prompt de comando do **PowerShell do Azure** .</span><span class="sxs-lookup"><span data-stu-id="674ed-127">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="674ed-128">Alterar diretórios toohello local de saudação **hivejob.ps1** de arquivo e use Olá script do comando toorun Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="674ed-128">Change directories toohello location of hello **hivejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="674ed-129">Quando a execução do script hello, você está tooenter solicitadas Olá cluster nome e hello HTTPS/Admin credenciais de conta para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="674ed-129">When hello script runs, you are prompted tooenter hello cluster name and hello HTTPS/Admin account credentials for hello cluster.</span></span> <span data-ttu-id="674ed-130">Você também pode ser solicitado toolog em tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="674ed-130">You may also be prompted toolog in tooyour Azure subscription.</span></span>

3. <span data-ttu-id="674ed-131">Quando o trabalho de saudação for concluído, ele retorna informações toohello semelhante thext a seguir:</span><span class="sxs-lookup"><span data-stu-id="674ed-131">When hello job completes, it returns information similar toohello following thext:</span></span>

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="674ed-132">Como mencionado anteriormente, **Invoke-Hive** pode ser usado toorun uma consulta e aguardar resposta hello.</span><span class="sxs-lookup"><span data-stu-id="674ed-132">As mentioned earlier, **Invoke-Hive** can be used toorun a query and wait for hello response.</span></span> <span data-ttu-id="674ed-133">Use Olá toosee script como funciona o Invoke-Hive a seguir:</span><span class="sxs-lookup"><span data-stu-id="674ed-133">Use hello following script toosee how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="674ed-134">saída de Hello aparência Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="674ed-134">hello output looks like hello following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="674ed-135">Para mais consultas de HiveQL, você pode usar o hello Azure PowerShell **cadeias de caracteres Here** cmdlet ou HiveQL arquivos de script.</span><span class="sxs-lookup"><span data-stu-id="674ed-135">For longer HiveQL queries, you can use hello Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="674ed-136">Olá trecho a seguir mostra como Olá toouse **Invoke-Hive** cmdlet toorun um arquivo de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="674ed-136">hello following snippet shows how toouse hello **Invoke-Hive** cmdlet toorun a HiveQL script file.</span></span> <span data-ttu-id="674ed-137">Olá, HiveQL arquivo de script deve ser carregado toowasb: / /.</span><span class="sxs-lookup"><span data-stu-id="674ed-137">hello HiveQL script file must be uploaded toowasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="674ed-138">Para obter mais informações sobre **Here-Strings**, consulte <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Como usar Here-Strings do Windows PowerShell</a>.</span><span class="sxs-lookup"><span data-stu-id="674ed-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="674ed-139">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="674ed-139">Troubleshooting</span></span>

<span data-ttu-id="674ed-140">Se nenhuma informação é retornada quando Olá trabalho for concluído, um erro pode ter ocorrido durante o processamento.</span><span class="sxs-lookup"><span data-stu-id="674ed-140">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="674ed-141">informações de erro tooview para este trabalho, adicionar Olá seguindo toohello final de saudação **hivejob.ps1** arquivo, salve-o e, em seguida, execute-o novamente.</span><span class="sxs-lookup"><span data-stu-id="674ed-141">tooview error information for this job, add hello following toohello end of hello **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="674ed-142">Esse cmdlet retorna informações de saudação escrito tooSTDERR no servidor de saudação quando você executou o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="674ed-142">This cmdlet returns hello information that is written tooSTDERR on hello server when you ran hello job.</span></span>

## <a name="summary"></a><span data-ttu-id="674ed-143">Resumo</span><span class="sxs-lookup"><span data-stu-id="674ed-143">Summary</span></span>

<span data-ttu-id="674ed-144">Como você pode ver, PowerShell do Azure fornece uma maneira fácil toorun consultas de Hive em um cluster HDInsight, o status do trabalho de saudação do monitor e recuperar a saída de hello.</span><span class="sxs-lookup"><span data-stu-id="674ed-144">As you can see, Azure PowerShell provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="674ed-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="674ed-145">Next steps</span></span>

<span data-ttu-id="674ed-146">Para obter informações gerais sobre o Hive no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="674ed-146">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="674ed-147">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="674ed-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="674ed-148">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="674ed-148">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="674ed-149">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="674ed-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="674ed-150">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="674ed-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
