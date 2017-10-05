---
title: "Usar o Hadoop Pig com o SSH em um cluster HDInsight – Azure | Microsoft Docs"
description: "Saiba como conectar a um cluster Hadoop baseado em Linux com o SSH e use o comando Pig para executar instruções Pig Latin interativamente ou como um trabalho em lotes."
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
ms.openlocfilehash: e4c893ef4bfa573dd9fbc9c9b0ae296720769842
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-the-pig-command-ssh"></a><span data-ttu-id="4a6f5-103">Executar trabalhos do Pig em um cluster baseado em Linux com o comando Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="4a6f5-103">Run Pig jobs on a Linux-based cluster with the Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="4a6f5-104">Saiba como executar trabalhos do Pig interativamente de uma conexão SSH para seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-104">Learn how to interactively run Pig jobs from an SSH connection to your HDInsight cluster.</span></span> <span data-ttu-id="4a6f5-105">A linguagem de programação Pig Latin permite descrever as transformações que são aplicadas aos dados de entrada para produzir a saída desejada.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a6f5-106">As etapas deste documento exigem um cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-106">The steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4a6f5-107">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4a6f5-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4a6f5-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="4a6f5-109"><a id="ssh"></a>Conexão com o SSH</span><span class="sxs-lookup"><span data-stu-id="4a6f5-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="4a6f5-110">Use o SSH para conectar-se ao cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-110">Use SSH to connect to your HDInsight cluster.</span></span> <span data-ttu-id="4a6f5-111">O exemplo a seguir se conecta a um cluster chamado **myhdinsight** como a conta denominada **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="4a6f5-111">The following example connects to a cluster named **myhdinsight** as the account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="4a6f5-112">**Se você tiver fornecido uma chave de certificado para autenticação de SSH** ao criar o cluster HDInsight, talvez seja necessário especificar o local da chave privada no sistema cliente.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-112">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="4a6f5-113">**Se você forneceu uma senha para autenticação SSH** ao criar o cluster HDInsight, forneça a senha quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-113">**If you provided a password for SSH authentication** when you created the HDInsight cluster, provide the password when prompted.</span></span>

<span data-ttu-id="4a6f5-114">Para saber mais sobre como usar o SSH com HDInsight, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4a6f5-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="4a6f5-115"><a id="pig"></a>Usar o comando Pig</span><span class="sxs-lookup"><span data-stu-id="4a6f5-115"><a id="pig"></a>Use the Pig command</span></span>

1. <span data-ttu-id="4a6f5-116">Uma vez conectado, inicie a CLI (interface de linha de comando) do Pig usando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a6f5-116">Once connected, start the Pig command-line interface (CLI) by using the following command:</span></span>

        pig

    <span data-ttu-id="4a6f5-117">Após um momento, você deverá ver um prompt `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="4a6f5-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="4a6f5-118">Insira a instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a6f5-118">Enter the following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="4a6f5-119">Esse comando carrega o conteúdo do arquivo sample.log em LOGS.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-119">This command loads the contents of the sample.log file into LOGS.</span></span> <span data-ttu-id="4a6f5-120">Você pode exibir o conteúdo do arquivo usando a seguinte instrução:</span><span class="sxs-lookup"><span data-stu-id="4a6f5-120">You can view the contents of the file by using the following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="4a6f5-121">Em seguida, transforme os dados aplicando uma expressão regular para extrair apenas o nível de registro em log de cada registro usando a seguinte instrução:</span><span class="sxs-lookup"><span data-stu-id="4a6f5-121">Next, transform the data by applying a regular expression to extract only the logging level from each record by using the following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="4a6f5-122">Você pode usar **DUMP** para exibir os dados após a transformação.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-122">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="4a6f5-123">Nesse caso, use `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="4a6f5-124">Continue a aplicar transformações usando as instruções na tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a6f5-124">Continue applying transformations by using the statements in the following table:</span></span>

    | <span data-ttu-id="4a6f5-125">Instrução de Pig Latin</span><span class="sxs-lookup"><span data-stu-id="4a6f5-125">Pig Latin statement</span></span> | <span data-ttu-id="4a6f5-126">O que a instrução faz</span><span class="sxs-lookup"><span data-stu-id="4a6f5-126">What the statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="4a6f5-127">Remove as linhas que contêm um valor nulo para o nível de log e armazena os resultados em `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-127">Removes rows that contain a null value for the log level and stores the results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="4a6f5-128">Agrupa as linhas pelo nível de log e armazena os resultados em `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-128">Groups the rows by log level and stores the results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="4a6f5-129">Cria um conjunto de dados que contém cada valor de nível de log exclusivo e quantas vezes ele ocorre.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="4a6f5-130">O conjunto de dados é armazenado em `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-130">The data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="4a6f5-131">Ordena os níveis de log por contagem (decrescente) e armazena em `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-131">Orders the log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="4a6f5-132">Use `DUMP` para exibir o resultado da transformação após cada etapa.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-132">Use `DUMP` to view the result of the transformation after each step.</span></span>

5. <span data-ttu-id="4a6f5-133">Você também pode salvar os resultados de uma transformação usando a instrução `STORE` .</span><span class="sxs-lookup"><span data-stu-id="4a6f5-133">You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="4a6f5-134">Por exemplo, a instrução a seguir salva o `RESULT` no diretório `/example/data/pigout` no armazenamento padrão para seu cluster:</span><span class="sxs-lookup"><span data-stu-id="4a6f5-134">For example, the following statement saves the `RESULT` to the `/example/data/pigout` directory on the default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="4a6f5-135">Os dados são armazenados no diretório especificado nos arquivos chamados `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-135">The data is stored in the specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="4a6f5-136">Se o diretório já existir, você receberá um erro.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-136">If the directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="4a6f5-137">Para sair do prompt do grunt, insira a instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a6f5-137">To exit the grunt prompt, enter the following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="4a6f5-138">Arquivos de lote do Pig Latin</span><span class="sxs-lookup"><span data-stu-id="4a6f5-138">Pig Latin batch files</span></span>

<span data-ttu-id="4a6f5-139">Você também pode usar o comando Pig para executar o Pig Latin contido em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-139">You can also use the Pig command to run Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="4a6f5-140">Depois de sair do prompt do grunt, use o seguinte comando para canalizar STDIN em um arquivo chamado `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-140">After exiting the grunt prompt, use the following command to pipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="4a6f5-141">Esse arquivo é criado no diretório inicial para a conta de usuário do SSH.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-141">This file is created in the home directory for the SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="4a6f5-142">Digite ou cole as seguintes linhas e use Ctrl+D quando terminar.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-142">Type or paste the following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="4a6f5-143">Use o seguinte comando para executar o arquivo `pigbatch.pig` utilizando o comando Pig.</span><span class="sxs-lookup"><span data-stu-id="4a6f5-143">Use the following command to run the `pigbatch.pig` file by using the Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="4a6f5-144">Quando o trabalho em lotes for concluído, você verá o seguinte resultado:</span><span class="sxs-lookup"><span data-stu-id="4a6f5-144">Once the batch job finishes, you see the following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="4a6f5-145"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a6f5-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="4a6f5-146">Para obter informações gerais sobre como usar o Pig no HDInsight, consulte o seguinte documento:</span><span class="sxs-lookup"><span data-stu-id="4a6f5-146">For general information on Pig in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="4a6f5-147">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="4a6f5-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="4a6f5-148">Para saber mais sobre outras maneiras de trabalhar com o Hadoop no HDInsight, consulte os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="4a6f5-148">For more information on other ways to work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="4a6f5-149">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="4a6f5-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="4a6f5-150">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="4a6f5-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
