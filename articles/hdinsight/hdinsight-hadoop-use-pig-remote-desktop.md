---
title: "Usar o Pig do Hadoop com área de trabalho remota no HDInsight – Azure | Microsoft Docs"
description: "Aprenda a usar o comando Pig para executar instruções Pig Latin por meio de uma conexão de área de trabalho remota a um cluster Hadoop em HDInsight baseado em Windows."
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
ms.openlocfilehash: 5e8d4fbd8afc54c8bbc1a9a71c66d7022a7d5986
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="d4b15-103">Executar trabalhos do Pig por meio de uma conexão de área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="d4b15-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="d4b15-104">Este documento fornece uma explicação passo a passo para usar o comando Pig para executar instruções Pig Latin por meio de uma conexão de área de trabalho remota a um cluster HDInsight baseado em Windows.</span><span class="sxs-lookup"><span data-stu-id="d4b15-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="d4b15-105">O Pig Latin permite que você crie aplicativos MapReduce descrevendo as transformações de dados, em vez das funções mapear e reduzir.</span><span class="sxs-lookup"><span data-stu-id="d4b15-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4b15-106">A Área de Trabalho Remota está disponível somente em clusters HDInsight que usam o Windows como o sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="d4b15-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="d4b15-107">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="d4b15-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d4b15-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d4b15-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="d4b15-109">No caso do HDInsight 3.4 ou superior, confira [Usar Pig com o HDInsight e SSH](hdinsight-hadoop-use-pig-ssh.md) para obter informações sobre como executar interativamente trabalhos do Pig diretamente no cluster de uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="d4b15-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="d4b15-110"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d4b15-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="d4b15-111">Para concluir as etapas neste artigo, você precisará do seguinte.</span><span class="sxs-lookup"><span data-stu-id="d4b15-111">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="d4b15-112">Um cluster HDInsight baseado em Windows (Hadoop no HDInsight)</span><span class="sxs-lookup"><span data-stu-id="d4b15-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="d4b15-113">Um computador cliente executando o Windows 7, Windows 8 ou Windows 10</span><span class="sxs-lookup"><span data-stu-id="d4b15-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="d4b15-114"><a id="connect"></a>Conectar com a área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="d4b15-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="d4b15-115">Habilite a área de trabalho remota para o cluster HDInsight e conecte-se a ele seguindo as instruções em [Conectar aos clusters HDInsight usando o RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="d4b15-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="d4b15-116"><a id="pig"></a>Usar o comando Pig</span><span class="sxs-lookup"><span data-stu-id="d4b15-116"><a id="pig"></a>Use the Pig command</span></span>
1. <span data-ttu-id="d4b15-117">Após ter estabelecido uma conexão de área de trabalho remota, inicie a **Linha de Comando do Hadoop** usando o ícone correspondente na área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d4b15-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span></span>
2. <span data-ttu-id="d4b15-118">Use o seguinte para iniciar o comando do Pig:</span><span class="sxs-lookup"><span data-stu-id="d4b15-118">Use the following to start the Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="d4b15-119">Você verá um prompt `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="d4b15-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="d4b15-120">Insira a instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4b15-120">Enter the following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="d4b15-121">Esse comando carrega o conteúdo do arquivo sample.log no arquivo LOGS.</span><span class="sxs-lookup"><span data-stu-id="d4b15-121">This command loads the contents of the sample.log file into the LOGS file.</span></span> <span data-ttu-id="d4b15-122">Você pode exibir o conteúdo do arquivo usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d4b15-122">You can view the contents of the file by using the following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="d4b15-123">Transforme os dados aplicando uma expressão regular para extrair apenas o nível de registro em log de cada registro:</span><span class="sxs-lookup"><span data-stu-id="d4b15-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="d4b15-124">Você pode usar **DUMP** para exibir os dados após a transformação.</span><span class="sxs-lookup"><span data-stu-id="d4b15-124">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="d4b15-125">Nesse caso, `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="d4b15-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="d4b15-126">Continue a aplicar transformações usando as instruções a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4b15-126">Continue applying transformations by using the following statements.</span></span> <span data-ttu-id="d4b15-127">Use `DUMP` para exibir o resultado da transformação após cada etapa.</span><span class="sxs-lookup"><span data-stu-id="d4b15-127">Use `DUMP` to view the result of the transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="d4b15-128">Instrução</span><span class="sxs-lookup"><span data-stu-id="d4b15-128">Statement</span></span></th><th><span data-ttu-id="d4b15-129">O que faz</span><span class="sxs-lookup"><span data-stu-id="d4b15-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="d4b15-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="d4b15-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="d4b15-131">Remove as linhas que contêm um valor nulo para o nível de log e armazena os resultados em FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="d4b15-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d4b15-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="d4b15-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="d4b15-133">Agrupa as linhas pelo nível de log e armazena os resultados em GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="d4b15-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d4b15-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="d4b15-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="d4b15-135">Cria um novo conjunto de dados que contém cada valor de nível de log exclusivo e quantas vezes ele ocorre.</span><span class="sxs-lookup"><span data-stu-id="d4b15-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="d4b15-136">Isso é armazenado em FREQUENCIES</span><span class="sxs-lookup"><span data-stu-id="d4b15-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d4b15-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="d4b15-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="d4b15-138">Ordena os níveis de log por contagem (decrescente) e armazena em RESULT</span><span class="sxs-lookup"><span data-stu-id="d4b15-138">Orders the log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="d4b15-139">
6. Você também pode salvar os resultados de uma transformação usando a instrução `STORE`.</span><span class="sxs-lookup"><span data-stu-id="d4b15-139">
6. You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="d4b15-140">Por exemplo, o comando a seguir salva o `RESULT` no diretório **/example/data/pigout** , no contêiner de armazenamento padrão para seu cluster:</span><span class="sxs-lookup"><span data-stu-id="d4b15-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="d4b15-141">Os dados são armazenados no diretório especificado nos arquivos chamados **part-nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="d4b15-141">The data is stored in the specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="d4b15-142">Se o diretório já existir, você receberá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="d4b15-142">If the directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="d4b15-143">Para sair do prompt do assistente, insira a instrução a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4b15-143">To exit the grunt prompt, enter the following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="d4b15-144">Arquivos de lote do Pig Latin</span><span class="sxs-lookup"><span data-stu-id="d4b15-144">Pig Latin batch files</span></span>
<span data-ttu-id="d4b15-145">Você também pode usar o comando Pig para executar o Pig Latin contido em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="d4b15-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="d4b15-146">Depois de sair do prompt do grunt, abra o **Bloco de Notas** e crie um novo arquivo chamado **pigbatch.pig** no diretório **%PIG_HOME%**.</span><span class="sxs-lookup"><span data-stu-id="d4b15-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="d4b15-147">Digite ou cole as seguintes linhas no arquivo **pigbatch.pig** e salve-o quando terminar:</span><span class="sxs-lookup"><span data-stu-id="d4b15-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="d4b15-148">Use o demonstrado a seguir para executar o arquivo **pigbatch.pig** utilizando o comando pig.</span><span class="sxs-lookup"><span data-stu-id="d4b15-148">Use the following to run the **pigbatch.pig** file using the pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="d4b15-149">Quando o trabalho em lotes for concluído, você verá a seguinte saída, que deverá ser igual àquela de quando você usou `DUMP RESULT;` nas etapas anteriores:</span><span class="sxs-lookup"><span data-stu-id="d4b15-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="d4b15-150"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="d4b15-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="d4b15-151">Como você pode ver, o comando Pig permite executar operações do MapReduce, ou usar trabalhos do Pig Latin armazenados em arquivos em lotes.</span><span class="sxs-lookup"><span data-stu-id="d4b15-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="d4b15-152"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4b15-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="d4b15-153">Para obter informações gerais sobre o Pig no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d4b15-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="d4b15-154">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4b15-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="d4b15-155">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d4b15-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="d4b15-156">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4b15-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d4b15-157">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4b15-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
