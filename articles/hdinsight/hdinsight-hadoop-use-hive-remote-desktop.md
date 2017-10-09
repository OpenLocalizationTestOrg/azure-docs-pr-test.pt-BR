---
title: "aaaUse Hive do Hadoop e a área de trabalho remota no HDInsight - Azure | Microsoft Docs"
description: "Saiba como tooconnect tooHadoop cluster no HDInsight usando a área de trabalho remota e, em seguida, executar consultas de Hive usando Olá Hive Interface de linha de comando."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="edca4-103">Usar o Hive com Hadoop no HDInsight com Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="edca4-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="edca4-104">Neste artigo, você aprenderá como tooconnect tooan HDInsight cluster usando a área de trabalho remota e, em seguida, execute o Hive as consultas usando Olá Hive Interface de linha de comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="edca4-104">In this article, you will learn how tooconnect tooan HDInsight cluster by using Remote Desktop, and then run Hive queries by using hello Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="edca4-105">Área de trabalho remota só está disponível em clusters de HDInsight que usam o Windows como sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="edca4-105">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="edca4-106">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="edca4-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="edca4-107">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="edca4-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="edca4-108">Para HDInsight 3.4 ou superior, consulte [Use Hive com HDInsight e Beeline](hdinsight-hadoop-use-hive-beeline.md) para obter informações sobre como executar consultas de Hive diretamente no cluster de saudação de uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="edca4-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="edca4-109"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="edca4-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="edca4-110">toocomplete Olá etapas neste artigo, você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="edca4-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="edca4-111">Um cluster HDInsight baseado em Windows (Hadoop no HDInsight)</span><span class="sxs-lookup"><span data-stu-id="edca4-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="edca4-112">Um computador cliente executando o Windows 7, Windows 8 ou Windows 10</span><span class="sxs-lookup"><span data-stu-id="edca4-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="edca4-113"><a id="connect"></a>Conectar com a área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="edca4-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="edca4-114">Habilitar área de trabalho remota para o cluster do HDInsight hello e conecte tooit seguindo as instruções de saudação em [conectar tooHDInsight clusters usando o RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="edca4-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="edca4-115"><a id="hive"></a>Use o comando de Hive Olá</span><span class="sxs-lookup"><span data-stu-id="edca4-115"><a id="hive"></a>Use hello Hive command</span></span>
<span data-ttu-id="edca4-116">Quando você se conectou toohello a área de trabalho para o cluster do HDInsight hello, use Olá toowork etapas com a seção a seguir:</span><span class="sxs-lookup"><span data-stu-id="edca4-116">When you have connected toohello desktop for hello HDInsight cluster, use hello following steps toowork with Hive:</span></span>

1. <span data-ttu-id="edca4-117">Na área de trabalho do HDInsight hello, iniciar Olá **linha de comando do Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="edca4-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="edca4-118">Digite Olá Olá toostart de comando CLI do Hive a seguir:</span><span class="sxs-lookup"><span data-stu-id="edca4-118">Enter hello following command toostart hello Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="edca4-119">Quando a saudação CLI foi iniciada, você verá prompt de Hive CLI Olá: `hive>`.</span><span class="sxs-lookup"><span data-stu-id="edca4-119">When hello CLI has started, you will see hello Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="edca4-120">Usando Olá CLI, insira Olá seguindo as instruções toocreate uma nova tabela nomeada **log4jLogs** usando dados de exemplo:</span><span class="sxs-lookup"><span data-stu-id="edca4-120">Using hello CLI, enter hello following statements toocreate a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="edca4-121">Essas instruções executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="edca4-121">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="edca4-122">**DROP TABLE**: exclui a tabela hello e arquivo de dados de saudação se Olá tabela já existir.</span><span class="sxs-lookup"><span data-stu-id="edca4-122">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="edca4-123">**CREATE EXTERNAL TABLE**: cria uma nova tabela “externa” em Hive.</span><span class="sxs-lookup"><span data-stu-id="edca4-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="edca4-124">Tabelas externas armazenam somente a definição de tabela Olá no Hive (dados são deixados no local original Olá Olá).</span><span class="sxs-lookup"><span data-stu-id="edca4-124">External tables store only hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="edca4-125">Tabelas externas devem ser usadas quando você espera Olá subjacente toobe dados atualizado por uma origem externa (como um processo de carregamento de dados automatizado) ou por outra operação de MapReduce, mas convém sempre ter que dados mais recentes do toouse Olá de consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="edca4-125">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="edca4-126">Descartar uma tabela externa **não** excluir dados hello, definição de tabela Olá somente.</span><span class="sxs-lookup"><span data-stu-id="edca4-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="edca4-127">**FORMATO de linha**: informa ao Hive como Olá dados são formatados.</span><span class="sxs-lookup"><span data-stu-id="edca4-127">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="edca4-128">Nesse caso, os campos de saudação em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="edca4-128">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="edca4-129">**LOCAL de arquivo de texto como armazenados**: informa ao Hive onde dados saudação são armazenado (diretório de exemplo de dados de saudação) e que ela é armazenada como texto.</span><span class="sxs-lookup"><span data-stu-id="edca4-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="edca4-130">**Selecione**: seleciona uma contagem de todas as linhas em que coluna **t4** contém valor Olá **[Erro]**.</span><span class="sxs-lookup"><span data-stu-id="edca4-130">**SELECT**: Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="edca4-131">Isso deve retornar um valor de **3** , já que existem três linhas que contêm esse valor.</span><span class="sxs-lookup"><span data-stu-id="edca4-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="edca4-132">**INPUT__FILE__NAME LIKE '%.log'** - informa ao Hive que só devemos retornar dados de arquivos que terminam em .log.</span><span class="sxs-lookup"><span data-stu-id="edca4-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="edca4-133">Isso restringe Olá toohello sample.log arquivo de pesquisa contém dados saudação e evita que ele retornando dados de exemplo de outros arquivos de dados que não correspondem ao esquema Olá definimos.</span><span class="sxs-lookup"><span data-stu-id="edca4-133">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
4. <span data-ttu-id="edca4-134">Olá Use seguindo as instruções toocreate uma nova tabela 'internal' nomeada **em decorrência**:</span><span class="sxs-lookup"><span data-stu-id="edca4-134">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="edca4-135">Essas instruções executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="edca4-135">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="edca4-136">**CREATE TABLE IF NOT EXISTS**: cria uma tabela, se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="edca4-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="edca4-137">Porque Olá **externo** palavra-chave não é usada, essa é uma tabela interna que é armazenada no data warehouse do hello Hive e é totalmente gerenciada pelo Hive.</span><span class="sxs-lookup"><span data-stu-id="edca4-137">Because hello **EXTERNAL** keyword is not used, this is an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="edca4-138">Ao contrário de **externo** tabelas, descartar uma tabela interna também exclui Olá dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="edca4-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes hello underlying data.</span></span>
     >
     >
   * <span data-ttu-id="edca4-139">**ARMAZENADOS como ORC**: armazena dados de Olá em formato (ORC) de coluna linha otimizado.</span><span class="sxs-lookup"><span data-stu-id="edca4-139">**STORED AS ORC**: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="edca4-140">Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="edca4-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="edca4-141">**INSERT OVERWRITE ... Selecione**: seleciona linhas de saudação **log4jLogs** tabela que contém **[Erro]**, em seguida, insere Olá dados em hello **em decorrência** tabela.</span><span class="sxs-lookup"><span data-stu-id="edca4-141">**INSERT OVERWRITE ... SELECT**: Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="edca4-142">tooverify que apenas as linhas que contêm **[Erro]** na coluna t4 foram armazenado toohello **em decorrência** de tabela, use Olá após a instrução tooreturn todos Olá linhas de **em decorrência**:</span><span class="sxs-lookup"><span data-stu-id="edca4-142">tooverify that only rows that contain **[ERROR]** in column t4 were stored toohello **errorLogs** table, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

       <span data-ttu-id="edca4-143">SELECT * de errorLogs;</span><span class="sxs-lookup"><span data-stu-id="edca4-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="edca4-144">Três linhas de dados devem ser devolvidas, todas contendo **[ERROR]** na coluna t4.</span><span class="sxs-lookup"><span data-stu-id="edca4-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="edca4-145"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="edca4-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="edca4-146">Como você pode ver, Olá Olá comando Hive fornece um toointeractively de maneira fácil executar consultas de Hive em um cluster HDInsight, o status do trabalho de saudação do monitor e recuperar a saída de hello.</span><span class="sxs-lookup"><span data-stu-id="edca4-146">As you can see, hello hello Hive command provides an easy way toointeractively run Hive queries on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="edca4-147"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="edca4-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="edca4-148">Para obter informações gerais sobre o Hive no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="edca4-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="edca4-149">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="edca4-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="edca4-150">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="edca4-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="edca4-151">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="edca4-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="edca4-152">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="edca4-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="edca4-153">Se você estiver usando Tez com Hive, consulte Olá documentos para as informações de depuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="edca4-153">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="edca4-154">Use Olá Tez UI no HDInsight baseados no Windows</span><span class="sxs-lookup"><span data-stu-id="edca4-154">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="edca4-155">Use Olá exibição Ambari Tez no HDInsight baseados em Linux</span><span class="sxs-lookup"><span data-stu-id="edca4-155">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
