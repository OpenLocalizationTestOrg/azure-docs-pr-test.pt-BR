---
title: "aaaMapReduce e conexão SSH com Hadoop no HDInsight - Azure | Microsoft Docs"
description: Saiba como toouse SSH toorun MapReduce trabalhos usando Hadoop no HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="c11cd-103">Usar o MapReduce com Hadoop no HDInsight com SSH</span><span class="sxs-lookup"><span data-stu-id="c11cd-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="c11cd-104">Saiba como toosubmit MapReduce trabalhos um tooHDInsight de conexão Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="c11cd-104">Learn how toosubmit MapReduce jobs from a Secure Shell (SSH) connection tooHDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="c11cd-105">Se você já estiver familiarizado com o uso de Hadoop baseado em Linux servidores, mas você tooHDInsight novo, consulte [HDInsight baseados em Linux dicas](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="c11cd-105">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="c11cd-106"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c11cd-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="c11cd-107">Um cluster do HDInsight baseado em Linux (Hadoop no HDInsight)</span><span class="sxs-lookup"><span data-stu-id="c11cd-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c11cd-108">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c11cd-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c11cd-109">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c11cd-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c11cd-110">Um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="c11cd-110">An SSH client.</span></span> <span data-ttu-id="c11cd-111">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="c11cd-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="c11cd-112"><a id="ssh"></a>Conexão com o SSH</span><span class="sxs-lookup"><span data-stu-id="c11cd-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="c11cd-113">Conecte-se toohello cluster usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="c11cd-113">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="c11cd-114">Por exemplo, a saudação comando a seguir conecta tooa cluster denominado **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="c11cd-114">For example, hello following command connects tooa cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="c11cd-115">**Se você usar uma chave de certificado para autenticação de SSH**, talvez seja necessário toospecify local de saudação da chave privada Olá no sistema cliente, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c11cd-115">**If you use a certificate key for SSH authentication**, you may need toospecify hello location of hello private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="c11cd-116">**Se você usar uma senha para autenticação de SSH**, você precisa tooprovide Olá senha quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="c11cd-116">**If you use a password for SSH authentication**, you need tooprovide hello password when prompted.</span></span>

<span data-ttu-id="c11cd-117">Para saber mais sobre como usar o SSH com HDInsight, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c11cd-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="c11cd-118"><a id="hadoop"></a>Usar comandos Hadoop</span><span class="sxs-lookup"><span data-stu-id="c11cd-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="c11cd-119">Depois de cluster do HDInsight toohello conectado, use Olá comando toostart um trabalho de MapReduce a seguir:</span><span class="sxs-lookup"><span data-stu-id="c11cd-119">After you are connected toohello HDInsight cluster, use hello following command toostart a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="c11cd-120">Esse comando inicia Olá `wordcount` classe, que está contida no hello `hadoop-mapreduce-examples.jar` arquivo.</span><span class="sxs-lookup"><span data-stu-id="c11cd-120">This command starts hello `wordcount` class, which is contained in hello `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="c11cd-121">Ele usa Olá `/example/data/gutenberg/davinci.txt` documento como entrada e saída é armazenado em `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="c11cd-121">It uses hello `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c11cd-122">Para obter mais informações sobre esses dados de exemplo de trabalho e hello MapReduce, consulte [Use MapReduce no Hadoop no HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="c11cd-122">For more information about this MapReduce job and hello example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="c11cd-123">trabalho de saudação emite detalhes como ele processa e retorna informações toohello semelhante texto a seguir quando Olá trabalho for concluído:</span><span class="sxs-lookup"><span data-stu-id="c11cd-123">hello job emits details as it processes, and it returns information similar toohello following text when hello job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="c11cd-124">Olá trabalho for concluído, use Olá arquivos de saída do comando toolist Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c11cd-124">When hello job completes, use hello following command toolist hello output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="c11cd-125">Esse comando exibe dois arquivos, `_SUCCESS` e `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="c11cd-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="c11cd-126">Olá `part-r-00000` arquivo contém a saída Olá para este trabalho.</span><span class="sxs-lookup"><span data-stu-id="c11cd-126">hello `part-r-00000` file contains hello output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c11cd-127">Alguns trabalhos de MapReduce podem dividir os resultados de saudação em várias **parte-r-# # #** arquivos.</span><span class="sxs-lookup"><span data-stu-id="c11cd-127">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="c11cd-128">Nesse caso, use Olá # # # sufixo de ordem de saudação tooindicate dos arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c11cd-128">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>

4. <span data-ttu-id="c11cd-129">Olá tooview de saída, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c11cd-129">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="c11cd-130">Este comando exibe uma lista de palavras de saudação que estão contidos em Olá **wasb://example/data/gutenberg/davinci.txt** arquivo e Olá o número de vezes que cada palavra ocorreu.</span><span class="sxs-lookup"><span data-stu-id="c11cd-130">This command displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file and hello number of times each word occurred.</span></span> <span data-ttu-id="c11cd-131">Olá, texto a seguir é um exemplo de dados Olá contidos no arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="c11cd-131">hello following text is an example of hello data that is contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="c11cd-132"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="c11cd-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="c11cd-133">Como você pode ver, o Hadoop comandos fornecem toorun uma maneira fácil trabalhos MapReduce em um cluster HDInsight e exibir saída de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="c11cd-133">As you can see, Hadoop commands provide an easy way toorun MapReduce jobs in an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="c11cd-134"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c11cd-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="c11cd-135">Para obter informações gerais sobre trabalhos de MapReduce no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c11cd-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="c11cd-136">Usar o MapReduce no Hadoop do HDInsight</span><span class="sxs-lookup"><span data-stu-id="c11cd-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="c11cd-137">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c11cd-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="c11cd-138">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c11cd-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c11cd-139">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c11cd-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
