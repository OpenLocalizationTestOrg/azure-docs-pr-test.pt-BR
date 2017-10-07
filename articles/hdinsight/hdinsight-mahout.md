---
title: "recomendações de aaaGenerate usando Mahout HDInsight do PowerShell - Azure | Microsoft Docs"
description: "Saiba como toouse Olá Apache Mahout máquina aprendizado recomendações de filme toogenerate biblioteca com HDInsight (Hadoop) de um script do PowerShell em execução no seu cliente."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 07b57208-32aa-4e59-900a-6c934fa1b7a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 675a2cd8ecaf7fc797d6cd094e4e58f9aca7ed92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="427a3-103">Gerar recomendações de vídeo usando o Apache Mahout com o Hadoop no HDInsight (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="427a3-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="427a3-104">Saiba como Olá toouse [Mahout Apache](http://mahout.apache.org) biblioteca de aprendizado de máquina com recomendações de filme toogenerate HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="427a3-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span> <span data-ttu-id="427a3-105">exemplo Hello neste documento usa o Azure PowerShell toorun Mahout trabalhos.</span><span class="sxs-lookup"><span data-stu-id="427a3-105">hello example in this document uses Azure PowerShell toorun Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="427a3-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="427a3-106">Prerequisites</span></span>

* <span data-ttu-id="427a3-107">Criar um cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="427a3-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="427a3-108">Para saber mais sobre como criar um, confira [Introdução ao uso do Hadoop baseado em Linux no HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="427a3-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="427a3-109">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="427a3-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="427a3-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="427a3-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="427a3-111">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="427a3-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="427a3-112"><a name="recommendations"></a>Gerar recomendações usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="427a3-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="427a3-113">trabalho Olá nesta seção funciona usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="427a3-113">hello job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="427a3-114">Muitas das classes de saudação fornecidos com Mahout atualmente não funcionam com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="427a3-114">Many of hello classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="427a3-115">Para obter uma lista de classes que não funcionam com o Azure PowerShell, consulte Olá [solução de problemas](#troubleshooting) seção.</span><span class="sxs-lookup"><span data-stu-id="427a3-115">For a list of classes that do not work with Azure PowerShell, see hello [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="427a3-116">Para obter um exemplo do uso de SSH tooconnect tooHDInsight e exemplos de Mahout execução diretamente no cluster hello, consulte [gerar recomendações de filme usando Mahout e HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="427a3-116">For an example of using SSH tooconnect tooHDInsight and run Mahout examples directly on hello cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="427a3-117">Uma das funções de saudação que é fornecido por Mahout é um mecanismo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="427a3-117">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="427a3-118">Esse mecanismo aceita dados em formato de saudação do `userID`, `itemId`, e `prefValue` (Olá a preferência de usuários para o item de saudação).</span><span class="sxs-lookup"><span data-stu-id="427a3-118">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello users preference for hello item).</span></span> <span data-ttu-id="427a3-119">Mahout usa usuários de toodetermine Olá dados com as preferências de tipo de item, que podem ser usado toomake recomendações.</span><span class="sxs-lookup"><span data-stu-id="427a3-119">Mahout uses hello data toodetermine users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="427a3-120">Hello exemplo a seguir é uma apresentação simplificada de como funciona o processo de recomendação de saudação:</span><span class="sxs-lookup"><span data-stu-id="427a3-120">hello following example is a simplified walk-through of how hello recommendation process works:</span></span>

* <span data-ttu-id="427a3-121">**ocorrência colegas**: Joe, Alice e Bob vinculadas todos os *estrela guerras*, *Olá Empire greves volta*, e *retorno de saudação Jedi*.</span><span class="sxs-lookup"><span data-stu-id="427a3-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="427a3-122">Mahout determina que os usuários que também como qualquer um desses filmes Olá outras duas.</span><span class="sxs-lookup"><span data-stu-id="427a3-122">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="427a3-123">**ocorrência colegas**: Bob e Alice também gostaram *Olá fantasma ameaça*, *ataque de Clones Olá*, e *Vingança de saudação Sith*.</span><span class="sxs-lookup"><span data-stu-id="427a3-123">**co-occurrence**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="427a3-124">Mahout determina que os usuários que gostaram filmes de três anterior Olá também como esses filmes.</span><span class="sxs-lookup"><span data-stu-id="427a3-124">Mahout determines that users who liked hello previous three movies also like these movies.</span></span>

* <span data-ttu-id="427a3-125">**Recomendação de similaridade**: Joe porque gostou Olá três primeiros filmes, Mahout examina filmes que outras pessoas com as preferências semelhantes gostou, mas Joe não tem observados (gostou/classificado).</span><span class="sxs-lookup"><span data-stu-id="427a3-125">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="427a3-126">Nesse caso, recomenda Mahout *Olá fantasma ameaça*, *ataque de Clones Olá*, e *Vingança de saudação Sith*.</span><span class="sxs-lookup"><span data-stu-id="427a3-126">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="427a3-127">Noções básicas sobre dados saudação</span><span class="sxs-lookup"><span data-stu-id="427a3-127">Understanding hello data</span></span>

<span data-ttu-id="427a3-128">A [GroupLens Research][movielens] oferece dados de classificação para filmes em um formato compatível com o Mahout.</span><span class="sxs-lookup"><span data-stu-id="427a3-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="427a3-129">Esses dados estão disponíveis no armazenamento de padrão de saudação para seu cluster em `/HdiSamples//HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="427a3-129">This data is available on hello default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="427a3-130">Há dois arquivos, `moviedb.txt` (informações sobre filmes Olá) e `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="427a3-130">There are two files, `moviedb.txt` (information about hello movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="427a3-131">Olá `user-ratings.txt` arquivo é usado durante a análise.</span><span class="sxs-lookup"><span data-stu-id="427a3-131">hello `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="427a3-132">Olá `moviedb.txt` arquivo é texto amigável tooprovide usado ao exibir os resultados de saudação da análise de saudação.</span><span class="sxs-lookup"><span data-stu-id="427a3-132">hello `moviedb.txt` file is used tooprovide user-friendly text when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="427a3-133">dados contidos no usuário ratings.txt Hello tem uma estrutura de `userID`, `movieID`, `userRating`, e `timestamp`, que informa como altamente cada usuário classificado como um filme.</span><span class="sxs-lookup"><span data-stu-id="427a3-133">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="427a3-134">Aqui está um exemplo de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="427a3-134">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a><span data-ttu-id="427a3-135">Executar trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="427a3-135">Run hello job</span></span>

<span data-ttu-id="427a3-136">Use Olá toorun de script do Windows PowerShell um trabalho que usa o mecanismo de recomendação Olá Mahout com dados do filme Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="427a3-136">Use hello following Windows PowerShell script toorun a job that uses hello Mahout recommendation engine with hello movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="427a3-137">Esse arquivo solicita informações de cluster do HDInsight tooyour tooconnect usado e execução de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="427a3-137">This file prompts you for information that is used tooconnect tooyour HDInsight cluster and run jobs.</span></span> <span data-ttu-id="427a3-138">Pode levar vários minutos para Olá trabalhos toocomplete e baixar o arquivo do hello txt.</span><span class="sxs-lookup"><span data-stu-id="427a3-138">It may take several minutes for hello jobs toocomplete and download hello output.txt file.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> <span data-ttu-id="427a3-139">Trabalhos mahout não remova os dados temporários que são criados durante o processamento de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="427a3-139">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="427a3-140">Olá `--tempDir` parâmetro é especificado em Olá exemplo trabalho tooisolate Olá os arquivos temporários em um diretório específico.</span><span class="sxs-lookup"><span data-stu-id="427a3-140">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific directory.</span></span>

<span data-ttu-id="427a3-141">trabalho de Mahout Olá não retorna Olá tooSTDOUT de saída.</span><span class="sxs-lookup"><span data-stu-id="427a3-141">hello Mahout job does not return hello output tooSTDOUT.</span></span> <span data-ttu-id="427a3-142">Em vez disso, ele os armazena no diretório de saída especificado hello como **parte-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="427a3-142">Instead, it stores it in hello specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="427a3-143">script Hello baixa esse arquivo muito**txt** no diretório atual de saudação na estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="427a3-143">hello script downloads this file too**output.txt** in hello current directory on your workstation.</span></span>

<span data-ttu-id="427a3-144">Olá, texto a seguir é um exemplo de conteúdo desse arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="427a3-144">hello following text is an example of hello content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="427a3-145">Olá primeira coluna é Olá `userID`.</span><span class="sxs-lookup"><span data-stu-id="427a3-145">hello first column is hello `userID`.</span></span> <span data-ttu-id="427a3-146">Olá valores contidos em ' [' e ']' são `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="427a3-146">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="427a3-147">script Hello também baixa Olá `moviedb.txt` e `user-ratings.txt` arquivos, que são necessários tooformat Olá saída toobe mais legível.</span><span class="sxs-lookup"><span data-stu-id="427a3-147">hello script also downloads hello `moviedb.txt` and `user-ratings.txt` files, which are needed tooformat hello output toobe more readable.</span></span>

### <a name="view-hello-output"></a><span data-ttu-id="427a3-148">Exibir saída de hello</span><span class="sxs-lookup"><span data-stu-id="427a3-148">View hello output</span></span>

<span data-ttu-id="427a3-149">Embora hello saída gerada possa ser Okey para uso em um aplicativo, não é fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="427a3-149">Although hello generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="427a3-150">Olá `moviedb.txt` de saudação servidor pode ser usado tooresolve Olá `movieId` tooa nome do filme.</span><span class="sxs-lookup"><span data-stu-id="427a3-150">hello `moviedb.txt` from hello server can be used tooresolve hello `movieId` tooa movie name.</span></span> <span data-ttu-id="427a3-151">Use Olá seguindo as recomendações de toodisplay de script do PowerShell com nomes de filme:</span><span class="sxs-lookup"><span data-stu-id="427a3-151">Use hello following PowerShell script toodisplay recommendations with movie names:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

<span data-ttu-id="427a3-152">Use Olá comando toodisplay Olá recomendações em um formato amigável a seguir:</span><span class="sxs-lookup"><span data-stu-id="427a3-152">Use hello following command toodisplay hello recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="427a3-153">saudação de saída é similar toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="427a3-153">hello output is similar toohello following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, hello (1997)                  1
    Alien: Resurrection (1997)               3
    187 (1997)                               2
    (lines ommitted)

    ---------------------------
    Recommended movies
    ---------------------------

    Movie                                    Score
    -----                                    -----
    Good Will Hunting (1997)                 4.6504064
    Swingers (1996)                          4.6862745
    Wings of hello Dove, hello (1997)            4.6666665
    People vs. Larry Flynt, hello (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="427a3-154"><a name="troubleshooting"></a>Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="427a3-154"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="427a3-155">Não foi possível substituir os arquivos</span><span class="sxs-lookup"><span data-stu-id="427a3-155">Cannot overwrite files</span></span>

<span data-ttu-id="427a3-156">Os trabalhos do Mahout não limpam arquivos temporários criados durante o processamento.</span><span class="sxs-lookup"><span data-stu-id="427a3-156">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="427a3-157">Além disso, os trabalhos de saudação não substituir o arquivo de saída existente.</span><span class="sxs-lookup"><span data-stu-id="427a3-157">In addition, hello jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="427a3-158">tooavoid erros ao executar trabalhos de Mahout, excluir arquivos temporários e de saída entre as execuções.</span><span class="sxs-lookup"><span data-stu-id="427a3-158">tooavoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="427a3-159">arquivos de saudação tooremove criados pelo Olá scripts anteriores neste documento, use Olá script do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="427a3-159">tooremove hello files created by hello earlier scripts in this document, use hello following PowerShell script:</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

#Get hello cluster info so we can get hello resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have tooget a list and delete one at a time
# Start with hello output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next hello temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="427a3-160"><a name="nopowershell"></a>Classes que não funcionam com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="427a3-160"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="427a3-161">Trabalhos de mahout que usam Olá classes a seguir retornam várias mensagens de erro quando usados no Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="427a3-161">Mahout jobs that use hello following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="427a3-162">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="427a3-162">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="427a3-163">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="427a3-163">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="427a3-164">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="427a3-164">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="427a3-165">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="427a3-165">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="427a3-166">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="427a3-166">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="427a3-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="427a3-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="427a3-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="427a3-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="427a3-169">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="427a3-169">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="427a3-170">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="427a3-170">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="427a3-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="427a3-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="427a3-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="427a3-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="427a3-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="427a3-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="427a3-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="427a3-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="427a3-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="427a3-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="427a3-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="427a3-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="427a3-177">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="427a3-177">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="427a3-178">trabalhos de toorun que usam essas classes, conecte-se o cluster do HDInsight toohello usando SSH e executar trabalhos de saudação da linha de comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="427a3-178">toorun jobs that use these classes, connect toohello HDInsight cluster using SSH and run hello jobs from hello command line.</span></span> <span data-ttu-id="427a3-179">Para obter um exemplo de como usar SSH toorun Mahout trabalhos, consulte [gerar recomendações de filme usando Mahout e HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="427a3-179">For an example of using SSH toorun Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="427a3-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="427a3-180">Next steps</span></span>

<span data-ttu-id="427a3-181">Agora que você aprendeu como toouse Mahout, descubra outras maneiras de trabalhar com dados no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="427a3-181">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="427a3-182">Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="427a3-182">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="427a3-183">Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="427a3-183">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="427a3-184">MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="427a3-184">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[aps]: /powershell/azureps-cmdlets-docs
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
