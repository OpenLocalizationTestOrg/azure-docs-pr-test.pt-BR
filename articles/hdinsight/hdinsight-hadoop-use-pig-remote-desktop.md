---
title: "aaaUse Pig do Hadoop com área de trabalho remota no HDInsight - Azure | Microsoft Docs"
description: "Saiba como toouse Olá Pig comando toorun Pig latino as instruções de um área de trabalho remota conexão tooa baseados no Windows de cluster Hadoop no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="e4a9e-103">Executar trabalhos do Pig por meio de uma conexão de área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="e4a9e-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="e4a9e-104">Este documento fornece um passo a passo para usar o hello Pig comando toorun Pig latino as instruções de um cluster HDInsight baseados no Windows de tooa de conexão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-104">This document provides a walkthrough for using hello Pig command toorun Pig Latin statements from a Remote Desktop connection tooa Windows-based HDInsight cluster.</span></span> <span data-ttu-id="e4a9e-105">Latino pig permite que aplicativos de MapReduce toocreate descrevendo as transformações de dados, em vez de mapear e reduzir as funções.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-105">Pig Latin allows you toocreate MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4a9e-106">Área de trabalho remota só está disponível em clusters de HDInsight que usam o Windows como sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-106">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="e4a9e-107">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e4a9e-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e4a9e-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="e4a9e-109">Para HDInsight 3.4 ou superior, consulte [usar o Pig com HDInsight e SSH](hdinsight-hadoop-use-pig-ssh.md) para obter informações sobre como executar interativamente Pig trabalhos diretamente no saudação do cluster de uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="e4a9e-110"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e4a9e-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="e4a9e-111">toocomplete Olá etapas neste artigo, você precisará seguir hello.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-111">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="e4a9e-112">Um cluster HDInsight baseado em Windows (Hadoop no HDInsight)</span><span class="sxs-lookup"><span data-stu-id="e4a9e-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="e4a9e-113">Um computador cliente executando o Windows 7, Windows 8 ou Windows 10</span><span class="sxs-lookup"><span data-stu-id="e4a9e-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="e4a9e-114"><a id="connect"></a>Conectar com a área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="e4a9e-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="e4a9e-115">Habilitar área de trabalho remota para o cluster do HDInsight hello e conecte tooit seguindo as instruções de saudação em [conectar tooHDInsight clusters usando o RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="e4a9e-115">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="e4a9e-116"><a id="pig"></a>Use o comando de Pig de saudação</span><span class="sxs-lookup"><span data-stu-id="e4a9e-116"><a id="pig"></a>Use hello Pig command</span></span>
1. <span data-ttu-id="e4a9e-117">Depois que você tiver uma conexão de área de trabalho remota, inicie Olá **linha de comando do Hadoop** usando o ícone de saudação na área de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-117">After you have a Remote Desktop connection, start hello **Hadoop Command Line** by using hello icon on hello desktop.</span></span>
2. <span data-ttu-id="e4a9e-118">Use Olá toostart Olá Pig comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e4a9e-118">Use hello following toostart hello Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="e4a9e-119">Você verá um prompt `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="e4a9e-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="e4a9e-120">Digite hello instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="e4a9e-120">Enter hello following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="e4a9e-121">Esse comando carrega conteúdo de saudação do arquivo de sample.log de saudação no arquivo de LOGS de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-121">This command loads hello contents of hello sample.log file into hello LOGS file.</span></span> <span data-ttu-id="e4a9e-122">Você pode exibir o conteúdo de saudação do arquivo hello usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e4a9e-122">You can view hello contents of hello file by using hello following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="e4a9e-123">Transforme dados saudação aplicando um nível de log de saudação somente tooextract de expressão regular de cada registro:</span><span class="sxs-lookup"><span data-stu-id="e4a9e-123">Transform hello data by applying a regular expression tooextract only hello logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="e4a9e-124">Você pode usar **DESPEJAR** dados de saudação tooview após a transformação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-124">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="e4a9e-125">Nesse caso, `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="e4a9e-126">Continue a aplicar transformações usando Olá instruções a seguir.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-126">Continue applying transformations by using hello following statements.</span></span> <span data-ttu-id="e4a9e-127">Use `DUMP` tooview resultados de saudação da transformação Olá depois de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-127">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="e4a9e-128">Instrução</span><span class="sxs-lookup"><span data-stu-id="e4a9e-128">Statement</span></span></th><th><span data-ttu-id="e4a9e-129">O que faz</span><span class="sxs-lookup"><span data-stu-id="e4a9e-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="e4a9e-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="e4a9e-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="e4a9e-131">Remove as linhas que contêm um valor nulo para o nível de log hello e armazena os resultados de saudação em FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-131">Removes rows that contain a null value for hello log level and stores hello results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e4a9e-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="e4a9e-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="e4a9e-133">Olá grupos linhas por nível de log e armazena os resultados de saudação em GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-133">Groups hello rows by log level and stores hello results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e4a9e-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="e4a9e-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="e4a9e-135">Cria um novo conjunto de dados que contém cada valor de nível de log exclusivo e quantas vezes ele ocorre.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="e4a9e-136">Isso é armazenado em FREQUENCIES</span><span class="sxs-lookup"><span data-stu-id="e4a9e-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e4a9e-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="e4a9e-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="e4a9e-138">Ordena os níveis de log Olá por contagem (decrescente) e armazena em resultado</span><span class="sxs-lookup"><span data-stu-id="e4a9e-138">Orders hello log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="e4a9e-139">
6.Você também pode salvar os resultados de saudação de uma transformação usando Olá `STORE` instrução.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-139">
6. You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="e4a9e-140">Por exemplo, a saudação comando a seguir salva Olá `RESULT` toohello **/example/data/pigout** diretório no contêiner de armazenamento padrão Olá para o cluster:</span><span class="sxs-lookup"><span data-stu-id="e4a9e-140">For example, hello following command saves hello `RESULT` toohello **/example/data/pigout** directory in hello default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="e4a9e-141">Olá dados são armazenados no diretório especificado do hello nos arquivos denominados **parte nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-141">hello data is stored in hello specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="e4a9e-142">Se o diretório de saudação já existir, você receberá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-142">If hello directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="e4a9e-143">Olá tooexit pesado prompt, digite Olá instrução a seguir.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-143">tooexit hello grunt prompt, enter hello following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="e4a9e-144">Arquivos de lote do Pig Latin</span><span class="sxs-lookup"><span data-stu-id="e4a9e-144">Pig Latin batch files</span></span>
<span data-ttu-id="e4a9e-145">Você também pode usar o hello Pig comando toorun latino Pig que está contido em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-145">You can also use hello Pig command toorun Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="e4a9e-146">Depois de sair do prompt de pesado hello, abra **o bloco de notas** e criar um novo arquivo denominado **pigbatch.pig** em Olá **PIG_HOME %** directory.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-146">After exiting hello grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in hello **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="e4a9e-147">Tipo ou a seguir Olá colar linhas em Olá **pigbatch.pig** de arquivo e, em seguida, salvá-lo:</span><span class="sxs-lookup"><span data-stu-id="e4a9e-147">Type or paste hello following lines into hello **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="e4a9e-148">Olá Use toorun Olá a seguir **pigbatch.pig** arquivo usando o comando de pig de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-148">Use hello following toorun hello **pigbatch.pig** file using hello pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="e4a9e-149">Quando o trabalho em lotes de saudação for concluída, você deverá ver Olá saída, que deve ser Olá mesmo como quando você usou a seguir `DUMP RESULT;` nas etapas anteriores hello:</span><span class="sxs-lookup"><span data-stu-id="e4a9e-149">When hello batch job completes, you should see hello following output, which should be hello same as when you used `DUMP RESULT;` in hello previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="e4a9e-150"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="e4a9e-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="e4a9e-151">Como você pode ver, Olá comando Pig permite toointeractively executar operações de MapReduce ou executar trabalhos de Pig latino que são armazenados em um arquivo em lotes.</span><span class="sxs-lookup"><span data-stu-id="e4a9e-151">As you can see, hello Pig command allows you toointeractively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="e4a9e-152"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e4a9e-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="e4a9e-153">Para obter informações gerais sobre o Pig no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e4a9e-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="e4a9e-154">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4a9e-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="e4a9e-155">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e4a9e-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="e4a9e-156">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4a9e-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e4a9e-157">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4a9e-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
