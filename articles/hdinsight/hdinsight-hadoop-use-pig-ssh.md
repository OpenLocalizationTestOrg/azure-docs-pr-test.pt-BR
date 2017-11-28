---
title: aaaUse Pig do Hadoop com SSH em um cluster HDInsight - Azure | Microsoft Docs
description: "Saiba como se conectar tooa cluster de Hadoop baseado em Linux com SSH, e, em seguida, usar Olá Pig comando toorun Pig latino instruções interativamente ou como um lote de trabalho."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a><span data-ttu-id="04e15-103">Executar trabalhos de Pig em um cluster baseado em Linux com hello comando Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="04e15-103">Run Pig jobs on a Linux-based cluster with hello Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="04e15-104">Saiba como toointeractively executar trabalhos de Pig de um cluster de HDInsight de tooyour de conexão SSH.</span><span class="sxs-lookup"><span data-stu-id="04e15-104">Learn how toointeractively run Pig jobs from an SSH connection tooyour HDInsight cluster.</span></span> <span data-ttu-id="04e15-105">Olá linguagem de programação de Pig latino permite toodescribe transformações que são aplicadas toohello entrada dados tooproduce Olá desejado saída.</span><span class="sxs-lookup"><span data-stu-id="04e15-105">hello Pig Latin programming language allows you toodescribe transformations that are applied toohello input data tooproduce hello desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04e15-106">Olá, as etapas neste documento exigem um cluster HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="04e15-106">hello steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="04e15-107">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="04e15-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="04e15-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="04e15-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="04e15-109"><a id="ssh"></a>Conexão com o SSH</span><span class="sxs-lookup"><span data-stu-id="04e15-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="04e15-110">Use SSH tooconnect tooyour HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="04e15-110">Use SSH tooconnect tooyour HDInsight cluster.</span></span> <span data-ttu-id="04e15-111">exemplo a seguir Hello conecta tooa cluster denominado **myhdinsight** como Olá conta denominada **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="04e15-111">hello following example connects tooa cluster named **myhdinsight** as hello account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="04e15-112">**Se você forneceu uma chave de certificado para autenticação de SSH** quando você criou o cluster do HDInsight hello, talvez seja necessário toospecify local de saudação da chave privada Olá no sistema cliente.</span><span class="sxs-lookup"><span data-stu-id="04e15-112">**If you provided a certificate key for SSH authentication** when you created hello HDInsight cluster, you may need toospecify hello location of hello private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="04e15-113">**Se você forneceu uma senha para autenticação de SSH** quando você criou o cluster do HDInsight hello, forneça a senha de saudação quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="04e15-113">**If you provided a password for SSH authentication** when you created hello HDInsight cluster, provide hello password when prompted.</span></span>

<span data-ttu-id="04e15-114">Para saber mais sobre como usar o SSH com HDInsight, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="04e15-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="04e15-115"><a id="pig"></a>Use o comando de Pig de saudação</span><span class="sxs-lookup"><span data-stu-id="04e15-115"><a id="pig"></a>Use hello Pig command</span></span>

1. <span data-ttu-id="04e15-116">Uma vez conectado, inicie interface de linha de comando de Pig de saudação (CLI) usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e15-116">Once connected, start hello Pig command-line interface (CLI) by using hello following command:</span></span>

        pig

    <span data-ttu-id="04e15-117">Após um momento, você deverá ver um prompt `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="04e15-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="04e15-118">Digite hello instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e15-118">Enter hello following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="04e15-119">Esse comando carrega o conteúdo de saudação do arquivo de sample.log Olá nos LOGS.</span><span class="sxs-lookup"><span data-stu-id="04e15-119">This command loads hello contents of hello sample.log file into LOGS.</span></span> <span data-ttu-id="04e15-120">Você pode exibir o conteúdo de saudação do arquivo hello usando Olá instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e15-120">You can view hello contents of hello file by using hello following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="04e15-121">Em seguida, transformar dados saudação aplicando um nível de log de saudação somente tooextract de expressão regular de cada registro usando Olá instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e15-121">Next, transform hello data by applying a regular expression tooextract only hello logging level from each record by using hello following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="04e15-122">Você pode usar **DESPEJAR** dados de saudação tooview após a transformação de saudação.</span><span class="sxs-lookup"><span data-stu-id="04e15-122">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="04e15-123">Nesse caso, use `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="04e15-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="04e15-124">Continue a aplicar transformações usando instruções Olá em Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e15-124">Continue applying transformations by using hello statements in hello following table:</span></span>

    | <span data-ttu-id="04e15-125">Instrução de Pig Latin</span><span class="sxs-lookup"><span data-stu-id="04e15-125">Pig Latin statement</span></span> | <span data-ttu-id="04e15-126">O demonstrativo de saudação não diz</span><span class="sxs-lookup"><span data-stu-id="04e15-126">What hello statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="04e15-127">Remove as linhas que contêm um valor nulo para o nível de log hello e armazena os resultados de saudação em `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="04e15-127">Removes rows that contain a null value for hello log level and stores hello results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="04e15-128">Olá grupos linhas por nível de log e armazena os resultados de saudação em `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="04e15-128">Groups hello rows by log level and stores hello results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="04e15-129">Cria um conjunto de dados que contém cada valor de nível de log exclusivo e quantas vezes ele ocorre.</span><span class="sxs-lookup"><span data-stu-id="04e15-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="04e15-130">Olá conjunto de dados é armazenado em `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="04e15-130">hello data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="04e15-131">Ordena os níveis de log Olá por contagem (decrescente) e armazena em `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="04e15-131">Orders hello log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="04e15-132">Use `DUMP` tooview resultados de saudação da transformação Olá depois de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="04e15-132">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

5. <span data-ttu-id="04e15-133">Você também pode salvar os resultados de saudação de uma transformação usando Olá `STORE` instrução.</span><span class="sxs-lookup"><span data-stu-id="04e15-133">You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="04e15-134">Por exemplo, a saudação instrução a seguir salva Olá `RESULT` toohello `/example/data/pigout` diretório no armazenamento padrão da saudação para seu cluster:</span><span class="sxs-lookup"><span data-stu-id="04e15-134">For example, hello following statement saves hello `RESULT` toohello `/example/data/pigout` directory on hello default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="04e15-135">Olá dados são armazenados no diretório especificado do hello nos arquivos denominados `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="04e15-135">hello data is stored in hello specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="04e15-136">Se já existe um diretório de saudação, você receberá um erro.</span><span class="sxs-lookup"><span data-stu-id="04e15-136">If hello directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="04e15-137">Olá tooexit pesado prompt, digite Olá instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e15-137">tooexit hello grunt prompt, enter hello following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="04e15-138">Arquivos de lote do Pig Latin</span><span class="sxs-lookup"><span data-stu-id="04e15-138">Pig Latin batch files</span></span>

<span data-ttu-id="04e15-139">Você também pode usar o hello Pig comando toorun Pig latino contido em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="04e15-139">You can also use hello Pig command toorun Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="04e15-140">Depois de sair do prompt de pesado Olá, uso a seguir Olá comando toopipe STDIN em um arquivo denominado `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="04e15-140">After exiting hello grunt prompt, use hello following command toopipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="04e15-141">Esse arquivo é criado no diretório base Olá Olá conta de usuário SSH.</span><span class="sxs-lookup"><span data-stu-id="04e15-141">This file is created in hello home directory for hello SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="04e15-142">Digite ou cole Olá linhas a seguir e, em seguida, use Ctrl + D quando terminar.</span><span class="sxs-lookup"><span data-stu-id="04e15-142">Type or paste hello following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="04e15-143">Olá toorun do comando de uso a seguir de saudação `pigbatch.pig` arquivo usando o comando de Pig de saudação.</span><span class="sxs-lookup"><span data-stu-id="04e15-143">Use hello following command toorun hello `pigbatch.pig` file by using hello Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="04e15-144">Quando termina de trabalho em lotes de saudação, você verá Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e15-144">Once hello batch job finishes, you see hello following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="04e15-145"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04e15-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="04e15-146">Para obter informações gerais sobre Pig no HDInsight, consulte Olá documento a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e15-146">For general information on Pig in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="04e15-147">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="04e15-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="04e15-148">Para obter mais informações sobre outra maneiras toowork com Hadoop no HDInsight, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e15-148">For more information on other ways toowork with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="04e15-149">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="04e15-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="04e15-150">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="04e15-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
