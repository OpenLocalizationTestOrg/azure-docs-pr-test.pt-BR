---
title: "Usar o Hive do Hadoop no Console de Consulta no HDInsight – Azure | Microsoft Docs"
description: "Neste artigo, você aprenderá como usar o Console de Consulta do HDInsight para executar consultas do Hive em um cluster HDInsight Hadoop por meio do seu navegador."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 9ccac43ae365d79bfd6ac1edf4d9a799c11356a1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-query-console"></a><span data-ttu-id="11253-103">Executar consultas Hive usando o Console de Consulta</span><span class="sxs-lookup"><span data-stu-id="11253-103">Run Hive queries using the Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="11253-104">Neste artigo, você aprenderá como usar o Console de Consulta do HDInsight para executar consultas do Hive em um cluster HDInsight Hadoop pelo seu navegador.</span><span class="sxs-lookup"><span data-stu-id="11253-104">In this article, you will learn how to use the HDInsight Query Console to run Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11253-105">O Console de Consulta do HDInsight está disponível somente em clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="11253-105">The HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="11253-106">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="11253-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="11253-107">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="11253-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="11253-108">Para HDInsight 3.4 ou superior, confira [Executar consultas do Hive no Modo de Exibição Hive do Ambari](hdinsight-hadoop-use-hive-ambari-view.md) para obter informações sobre como executar consultas do Hive em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="11253-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="11253-109"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="11253-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="11253-110">Para concluir as etapas neste artigo, você precisará do seguinte.</span><span class="sxs-lookup"><span data-stu-id="11253-110">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="11253-111">Um cluster Hadoop do HDInsight baseado no Windows</span><span class="sxs-lookup"><span data-stu-id="11253-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="11253-112">Um navegador da Web</span><span class="sxs-lookup"><span data-stu-id="11253-112">A modern web browser</span></span>

## <span data-ttu-id="11253-113"><a id="run"></a> Executar consultas Hive usando o Console de Consulta</span><span class="sxs-lookup"><span data-stu-id="11253-113"><a id="run"></a> Run Hive queries using the Query Console</span></span>
1. <span data-ttu-id="11253-114">Abra um navegador da Web, navegue até **https://CLUSTERNAME.azurehdinsight.net**, onde **CLUSTERNAME** é o nome do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11253-114">Open a web browser and navigate to **https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span> <span data-ttu-id="11253-115">Se solicitado, insira o nome de usuário e senha que você inseriu ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="11253-115">If prompted, enter the user name and password that you used when you created the cluster.</span></span>
2. <span data-ttu-id="11253-116">Nos links na parte superior da página, selecione **Editor Hive**.</span><span class="sxs-lookup"><span data-stu-id="11253-116">From the links at the top of the page, select **Hive Editor**.</span></span> <span data-ttu-id="11253-117">Isso exibe um formulário que pode ser usado para inserir instruções HiveQL que você deseja executar no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11253-117">This displays a form that can be used to enter the HiveQL statements that you want to run in the HDInsight cluster.</span></span>

    ![o editor de hive](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="11253-119">Substitua o texto `Select * from hivesampletable` pelas seguintes instruções HiveQL:</span><span class="sxs-lookup"><span data-stu-id="11253-119">Replace the text `Select * from hivesampletable` with the following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="11253-120">As instruções executam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="11253-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="11253-121">**DROP TABLE**: exclui a tabela e o arquivo de dados, caso a tabela já exista.</span><span class="sxs-lookup"><span data-stu-id="11253-121">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="11253-122">**CREATE EXTERNAL TABLE**: cria uma nova tabela “externa” em Hive.</span><span class="sxs-lookup"><span data-stu-id="11253-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="11253-123">As tabelas externas armazenam apenas a definição da tabela no Hive; os dados são deixados no local original.</span><span class="sxs-lookup"><span data-stu-id="11253-123">External tables store only the table definition in Hive; the data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="11253-124">As tabelas externas devem ser usadas quando você espera que os dados subjacentes sejam atualizados por uma fonte externa (como um processo automático de carregamento de dados) ou por outra operação MapReduce, mas você sempre quer que as consultas Hive utilizem os dados mais recentes.</span><span class="sxs-lookup"><span data-stu-id="11253-124">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="11253-125">Remover uma tabela externa **não** exclui os dados, somente a definição de tabela.</span><span class="sxs-lookup"><span data-stu-id="11253-125">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="11253-126">**ROW FORMAT**: informa ao Hive como os dados são formatados.</span><span class="sxs-lookup"><span data-stu-id="11253-126">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="11253-127">Nesse caso, os campos em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="11253-127">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="11253-128">**STORED AS TEXTFILE LOCATION**: informa ao Hive onde os dados são armazenados (o diretório de exemplos/dados) e que estão armazenados como texto</span><span class="sxs-lookup"><span data-stu-id="11253-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="11253-129">**SELECT**: seleciona uma contagem de todas as linhas em que a coluna **t4** contém o valor **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="11253-129">**SELECT**: Select a count of all rows where column **t4** contain the value **[ERROR]**.</span></span> <span data-ttu-id="11253-130">Isso deve retornar um valor de **3** , já que existem três linhas que contêm esse valor.</span><span class="sxs-lookup"><span data-stu-id="11253-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="11253-131">**INPUT__FILE__NAME LIKE '%.log'** - informa ao Hive que só devemos retornar dados de arquivos que terminam em .log.</span><span class="sxs-lookup"><span data-stu-id="11253-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="11253-132">Isso restringe a pesquisa ao arquivo sample.log que contém os dados e impede que ela retorne dados de outros arquivos de dados de exemplo que não correspondem ao esquema que definimos.</span><span class="sxs-lookup"><span data-stu-id="11253-132">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
3. <span data-ttu-id="11253-133">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="11253-133">Click **Submit**.</span></span> <span data-ttu-id="11253-134">A **Sessão de Trabalho** na parte inferior da página deve exibir detalhes do trabalho.</span><span class="sxs-lookup"><span data-stu-id="11253-134">The **Job Session** at the bottom of the page should display details for the job.</span></span>
4. <span data-ttu-id="11253-135">Quando o campo **Status** for alterado para **Concluído**, selecione **Exibir Detalhes** do trabalho.</span><span class="sxs-lookup"><span data-stu-id="11253-135">When the **Status** field changes to **Completed**, select **View Details** for the job.</span></span> <span data-ttu-id="11253-136">Na página de detalhes, a **Saída de Trabalho** contém `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="11253-136">On the details page, the **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="11253-137">Você pode usar o botão **Download** abaixo desse campo para baixar um arquivo que contém a saída do trabalho.</span><span class="sxs-lookup"><span data-stu-id="11253-137">You can use the **Download** button under this field to download a file that contains the output of the job.</span></span>

## <span data-ttu-id="11253-138"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="11253-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="11253-139">Como você pode ver, o Console de Consulta fornece uma maneira fácil de executar consultas do Hive em um cluster HDInsight, monitorar o status do trabalho e recuperar a saída.</span><span class="sxs-lookup"><span data-stu-id="11253-139">As you can see, the Query Console provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

<span data-ttu-id="11253-140">Para saber mais sobre o Hive usando o Console de Consulta para executar trabalhos Hive, selecione **Introdução** na parte superior do Console de Consulta e use os exemplos fornecidos.</span><span class="sxs-lookup"><span data-stu-id="11253-140">To learn more about using Hive Query Console to run Hive jobs, select **Getting Started** at the top of the Query Console, then use the samples that are provided.</span></span> <span data-ttu-id="11253-141">Cada exemplo percorre o processo de análise de dados usando o Hive, incluindo explicações sobre as instruções HiveQL usadas no exemplo.</span><span class="sxs-lookup"><span data-stu-id="11253-141">Each sample walks through the process of using Hive to analyze data, including explanations about the HiveQL statements used in the sample.</span></span>

## <span data-ttu-id="11253-142"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11253-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="11253-143">Para obter informações gerais sobre o Hive no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="11253-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="11253-144">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="11253-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="11253-145">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="11253-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="11253-146">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="11253-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="11253-147">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="11253-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="11253-148">Se você estiver usando o Tez com o Hive, consulte os seguintes documentos para as informações de depuração:</span><span class="sxs-lookup"><span data-stu-id="11253-148">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="11253-149">Usar a interface de usuário do Tez no HDInsight baseado em Windows</span><span class="sxs-lookup"><span data-stu-id="11253-149">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="11253-150">Usar a exibição de Ambari Tez no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="11253-150">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
