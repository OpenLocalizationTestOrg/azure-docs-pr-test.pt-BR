---
title: "aaaMapReduce e área de trabalho remota com Hadoop no HDInsight - Azure | Microsoft Docs"
description: "Saiba como toouse área de trabalho remota tooconnect tooHadoop no HDInsight e executados trabalhos de MapReduce."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="61706-103">Usar o MapReduce no Hadoop no HDInsight com Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="61706-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="61706-104">Neste artigo, você saiba como tooconnect tooa Hadoop no HDInsight cluster usando a área de trabalho remota e, em seguida, executar trabalhos de MapReduce usando o comando do Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="61706-104">In this article, you will learn how tooconnect tooa Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using hello Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61706-105">A Área de Trabalho Remota está disponível somente em clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="61706-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="61706-106">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="61706-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="61706-107">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="61706-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="61706-108">Para HDInsight 3.4 ou superior, consulte [Use MapReduce com SSH](hdinsight-hadoop-use-mapreduce-ssh.md) para obter informações sobre como conectar-se o cluster do HDInsight toohello e executar trabalhos de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="61706-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting toohello HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="61706-109"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="61706-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="61706-110">toocomplete Olá etapas neste artigo, você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="61706-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="61706-111">Um cluster HDInsight baseado em Windows (Hadoop no HDInsight)</span><span class="sxs-lookup"><span data-stu-id="61706-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="61706-112">Um computador cliente executando o Windows 7, Windows 8 ou Windows 10</span><span class="sxs-lookup"><span data-stu-id="61706-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="61706-113"><a id="connect"></a>Conectar com a área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="61706-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="61706-114">Habilitar área de trabalho remota para o cluster do HDInsight hello e conecte tooit seguindo as instruções de saudação em [conectar tooHDInsight clusters usando o RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="61706-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="61706-115"><a id="hadoop"></a>Use o comando do Hadoop Olá</span><span class="sxs-lookup"><span data-stu-id="61706-115"><a id="hadoop"></a>Use hello Hadoop command</span></span>
<span data-ttu-id="61706-116">Quando você estiver toohello conectado a área de trabalho para o cluster do HDInsight hello, use Olá seguindo as etapas toorun um trabalho de MapReduce usando o comando do Hadoop hello:</span><span class="sxs-lookup"><span data-stu-id="61706-116">When you are connected toohello desktop for hello HDInsight cluster, use hello following steps toorun a MapReduce job by using hello Hadoop command:</span></span>

1. <span data-ttu-id="61706-117">Na área de trabalho do HDInsight hello, iniciar Olá **linha de comando do Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="61706-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span> <span data-ttu-id="61706-118">Isso abre um novo prompt de comando no hello **c:\apps\dist\hadoop-&lt;o número de versão >** directory.</span><span class="sxs-lookup"><span data-stu-id="61706-118">This opens a new command prompt in hello **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="61706-119">número de versão de Hello muda conforme Hadoop é atualizada.</span><span class="sxs-lookup"><span data-stu-id="61706-119">hello version number changes as Hadoop is updated.</span></span> <span data-ttu-id="61706-120">Olá **HADOOP_HOME** variável de ambiente pode ser o caminho de saudação do toofind usado.</span><span class="sxs-lookup"><span data-stu-id="61706-120">hello **HADOOP_HOME** environment variable can be used toofind hello path.</span></span> <span data-ttu-id="61706-121">Por exemplo, `cd %HADOOP_HOME%` alterações diretórios toohello Hadoop diretório, sem a necessidade de número de versão tooknow hello.</span><span class="sxs-lookup"><span data-stu-id="61706-121">For example, `cd %HADOOP_HOME%` changes directories toohello Hadoop directory, without requiring you tooknow hello version number.</span></span>
   >
   >
2. <span data-ttu-id="61706-122">Olá toouse **Hadoop** toorun um trabalho de MapReduce do exemplo de comando, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="61706-122">toouse hello **Hadoop** command toorun an example MapReduce job, use hello following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="61706-123">Isso inicia o hello **wordcount** classe, que está contida no hello **Hadoop-Examples.jar mapreduce** arquivo no diretório atual hello.</span><span class="sxs-lookup"><span data-stu-id="61706-123">This starts hello **wordcount** class, which is contained in hello **hadoop-mapreduce-examples.jar** file in hello current directory.</span></span> <span data-ttu-id="61706-124">Como entrada, ele usa Olá **wasb://example/data/gutenberg/davinci.txt** documento e a saída é armazenado em: **wasb: / / / exemplo/dados/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="61706-124">As input, it uses hello **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="61706-125">Para obter mais informações sobre esses dados de exemplo de trabalho e hello MapReduce, consulte <a href="hdinsight-use-mapreduce.md">Use MapReduce em HDInsight Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="61706-125">for more information about this MapReduce job and hello example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="61706-126">trabalho de saudação emite detalhes como ela é processada e retorna a seguir toohello semelhante informações quando Olá trabalho for concluído:</span><span class="sxs-lookup"><span data-stu-id="61706-126">hello job emits details as it is processed, and it returns information similar toohello following when hello job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="61706-127">Quando o trabalho de saudação for concluído, use Olá seguindo os arquivos de saída do comando toolist Olá armazenados no **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="61706-127">When hello job is complete, use hello following command toolist hello output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="61706-128">Isso deve exibir dois arquivos, **_SUCCESS** e **part-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="61706-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="61706-129">Olá **parte-r-00000** arquivo contém a saída Olá para este trabalho.</span><span class="sxs-lookup"><span data-stu-id="61706-129">hello **part-r-00000** file contains hello output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="61706-130">Alguns trabalhos de MapReduce podem dividir os resultados de saudação em várias **parte-r-# # #** arquivos.</span><span class="sxs-lookup"><span data-stu-id="61706-130">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="61706-131">Nesse caso, use Olá # # # sufixo de ordem de saudação tooindicate dos arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="61706-131">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>
   >
   >
5. <span data-ttu-id="61706-132">Olá tooview de saída, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="61706-132">tooview hello output, use hello following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="61706-133">Isso exibe uma lista de palavras de saudação que estão contidos em Olá **wasb://example/data/gutenberg/davinci.txt** arquivo, juntamente com o número de saudação de vezes que cada palavra ocorreu.</span><span class="sxs-lookup"><span data-stu-id="61706-133">This displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file, along with hello number of times each word occured.</span></span> <span data-ttu-id="61706-134">a seguir Olá é um exemplo de dados de saudação que estarão contidos no arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="61706-134">hello following is an example of hello data that will be contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="61706-135"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="61706-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="61706-136">Como você pode ver, o hello Hadoop comando fornece um toorun de maneira fácil trabalhos MapReduce em um cluster HDInsight e exibir saída de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="61706-136">As you can see, hello Hadoop command provides an easy way toorun MapReduce jobs on an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="61706-137"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="61706-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="61706-138">Para obter informações gerais sobre trabalhos de MapReduce no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="61706-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="61706-139">Usar o MapReduce no Hadoop do HDInsight</span><span class="sxs-lookup"><span data-stu-id="61706-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="61706-140">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="61706-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="61706-141">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="61706-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="61706-142">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="61706-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
