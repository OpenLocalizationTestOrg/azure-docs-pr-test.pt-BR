---
title: "Usar o Hive do Hadoop e a área de trabalho remota no HDInsight – Azure | Microsoft Docs"
description: "Aprenda a conectar-se a um cluster do Hadoop no HDInsight usando a área de trabalho remota e então executar consultas Hive usando a Interface de Linha de Comando do Hive."
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
ms.openlocfilehash: 187c7cb413b3707e58eea387857375053d267189
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="8d6cd-103">Usar o Hive com Hadoop no HDInsight com Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="8d6cd-104">Neste artigo, você aprenderá como se conectar a um cluster HDInsight usando a Área de Trabalho Remota e então executar consultas Hive usando a CLI (Interface de Linha de Comando) do Hive.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-104">In this article, you will learn how to connect to an HDInsight cluster by using Remote Desktop, and then run Hive queries by using the Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8d6cd-105">A Área de Trabalho Remota está disponível somente em clusters HDInsight que usam o Windows como o sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-105">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="8d6cd-106">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8d6cd-107">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8d6cd-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="8d6cd-108">No caso do HDInsight 3.4 ou superior, confira [Usar o Hive com o HDInsight e o Beeline](hdinsight-hadoop-use-hive-beeline.md) para obter informações sobre como executar consultas do Hive diretamente no cluster de uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="8d6cd-109"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8d6cd-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="8d6cd-110">Para concluir as etapas neste artigo, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="8d6cd-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="8d6cd-111">Um cluster HDInsight baseado em Windows (Hadoop no HDInsight)</span><span class="sxs-lookup"><span data-stu-id="8d6cd-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="8d6cd-112">Um computador cliente executando o Windows 7, Windows 8 ou Windows 10</span><span class="sxs-lookup"><span data-stu-id="8d6cd-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="8d6cd-113"><a id="connect"></a>Conectar com a área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="8d6cd-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="8d6cd-114">Habilite a área de trabalho remota para o cluster HDInsight e conecte-se a ele seguindo as instruções em [Conectar aos clusters HDInsight usando o RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="8d6cd-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="8d6cd-115"><a id="hive"></a>Usar o comando do Hive</span><span class="sxs-lookup"><span data-stu-id="8d6cd-115"><a id="hive"></a>Use the Hive command</span></span>
<span data-ttu-id="8d6cd-116">Quando conectado à área de trabalho para o cluster HDInsight, use as etapas a seguir para trabalhar com o Hive:</span><span class="sxs-lookup"><span data-stu-id="8d6cd-116">When you have connected to the desktop for the HDInsight cluster, use the following steps to work with Hive:</span></span>

1. <span data-ttu-id="8d6cd-117">Na área de trabalho do HDInsight, inicie a **Linha de Comando do Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="8d6cd-118">Digite o seguinte comando para iniciar a CLI do Hive:</span><span class="sxs-lookup"><span data-stu-id="8d6cd-118">Enter the following command to start the Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="8d6cd-119">Depois de iniciar a CLI, você verá o prompt da CLI do Hive: `hive>`.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-119">When the CLI has started, you will see the Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="8d6cd-120">Usando a CLI, digite as instruções a seguir para criar uma nova tabela chamada **log4jLogs** usando os dados de exemplo:</span><span class="sxs-lookup"><span data-stu-id="8d6cd-120">Using the CLI, enter the following statements to create a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="8d6cd-121">As instruções executam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="8d6cd-121">These statements perform the following actions:</span></span>

   * <span data-ttu-id="8d6cd-122">**DROP TABLE**: exclui a tabela e o arquivo de dados, caso a tabela já exista.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-122">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="8d6cd-123">**CREATE EXTERNAL TABLE**: cria uma nova tabela “externa” em Hive.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="8d6cd-124">As tabelas externas armazenam apenas a definição da tabela no Hive (os dados são deixados no local original).</span><span class="sxs-lookup"><span data-stu-id="8d6cd-124">External tables store only the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="8d6cd-125">As tabelas externas devem ser usadas quando você espera que os dados subjacentes sejam atualizados por uma fonte externa (como um processo automático de carregamento de dados) ou por outra operação MapReduce, mas você sempre quer que as consultas Hive utilizem os dados mais recentes.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-125">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="8d6cd-126">Remover uma tabela externa **não** exclui os dados, somente a definição de tabela.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="8d6cd-127">**ROW FORMAT**: informa ao Hive como os dados são formatados.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-127">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="8d6cd-128">Nesse caso, os campos em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-128">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="8d6cd-129">**STORED AS TEXTFILE LOCATION**: informa ao Hive onde os dados são armazenados (o diretório de exemplos/dados) e que estão armazenados como texto.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="8d6cd-130">**SELECT**: seleciona uma contagem de todas as linhas em que a coluna **t4** contém o valor **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-130">**SELECT**: Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="8d6cd-131">Isso deve retornar um valor de **3** , já que existem três linhas que contêm esse valor.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="8d6cd-132">**INPUT__FILE__NAME LIKE '%.log'** - informa ao Hive que só devemos retornar dados de arquivos que terminam em .log.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="8d6cd-133">Isso restringe a pesquisa ao arquivo sample.log que contém os dados e impede que ela retorne dados de outros arquivos de dados de exemplo que não correspondem ao esquema que definimos.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-133">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
4. <span data-ttu-id="8d6cd-134">Use as instruções a seguir para criar uma nova tabela "interna" chamada **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="8d6cd-134">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="8d6cd-135">As instruções executam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="8d6cd-135">These statements perform the following actions:</span></span>

   * <span data-ttu-id="8d6cd-136">**CREATE TABLE IF NOT EXISTS**: cria uma tabela, se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="8d6cd-137">Já que a palavra-chave **EXTERNAL** não é utilizada, essa é uma tabela interna, armazenada no depósito de dados do Hive e gerenciada totalmente pelo Hive.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-137">Because the **EXTERNAL** keyword is not used, this is an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="8d6cd-138">Diferentemente de tabelas **EXTERNAS** , o descarte de uma tabela interna excluirá também os dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes the underlying data.</span></span>
     >
     >
   * <span data-ttu-id="8d6cd-139">**STORED AS ORC**: armazena os dados no formato ORC (colunar de linhas otimizadas).</span><span class="sxs-lookup"><span data-stu-id="8d6cd-139">**STORED AS ORC**: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="8d6cd-140">Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="8d6cd-141">**INSERT OVERWRITE ... SELECT**: seleciona linhas da tabela **log4jLogs** que contêm **[ERROR]** e insere os dados na tabela **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-141">**INSERT OVERWRITE ... SELECT**: Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="8d6cd-142">Para verificar se apenas as linhas que contêm **[ERROR]** na coluna t4 foram armazenadas na tabela **errorLogs**, use a seguinte instrução para retornar todas as linhas de **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="8d6cd-142">To verify that only rows that contain **[ERROR]** in column t4 were stored to the **errorLogs** table, use the following statement to return all the rows from **errorLogs**:</span></span>

       <span data-ttu-id="8d6cd-143">SELECT * de errorLogs;</span><span class="sxs-lookup"><span data-stu-id="8d6cd-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="8d6cd-144">Três linhas de dados devem ser devolvidas, todas contendo **[ERROR]** na coluna t4.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="8d6cd-145"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="8d6cd-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="8d6cd-146">Como você pode ver, o comando do Hive fornece uma maneira fácil de executar consultas Hive interativamente em um cluster HDInsight, monitorar o status do trabalho e recuperar a saída.</span><span class="sxs-lookup"><span data-stu-id="8d6cd-146">As you can see, the the Hive command provides an easy way to interactively run Hive queries on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="8d6cd-147"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8d6cd-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="8d6cd-148">Para obter informações gerais sobre o Hive no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8d6cd-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="8d6cd-149">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d6cd-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="8d6cd-150">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8d6cd-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="8d6cd-151">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d6cd-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="8d6cd-152">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d6cd-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="8d6cd-153">Se você estiver usando o Tez com o Hive, consulte os seguintes documentos para as informações de depuração:</span><span class="sxs-lookup"><span data-stu-id="8d6cd-153">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="8d6cd-154">Usar a interface de usuário do Tez no HDInsight baseado em Windows</span><span class="sxs-lookup"><span data-stu-id="8d6cd-154">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="8d6cd-155">Usar a exibição de Ambari Tez no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="8d6cd-155">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
