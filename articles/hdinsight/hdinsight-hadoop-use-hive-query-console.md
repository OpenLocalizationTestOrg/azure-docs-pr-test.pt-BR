---
title: aaaUse Hive do Hadoop no hello Console de consulta no HDInsight - Azure | Microsoft Docs
description: "Saiba como toouse Olá baseado na web Console de consulta toorun consultas de Hive em um HDInsight Hadoop do cluster de seu navegador."
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
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a><span data-ttu-id="7dda3-103">Executar consultas de Hive usando Olá Console de consulta</span><span class="sxs-lookup"><span data-stu-id="7dda3-103">Run Hive queries using hello Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="7dda3-104">Neste artigo, você aprenderá como consultas de Hive toouse Olá Console de consulta do HDInsight toorun em um HDInsight Hadoop do cluster de seu navegador.</span><span class="sxs-lookup"><span data-stu-id="7dda3-104">In this article, you will learn how toouse hello HDInsight Query Console toorun Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7dda3-105">Olá HDInsight consulta Console só está disponível em clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="7dda3-105">hello HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="7dda3-106">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7dda3-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7dda3-107">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7dda3-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="7dda3-108">Para HDInsight 3.4 ou superior, confira [Executar consultas do Hive no Modo de Exibição Hive do Ambari](hdinsight-hadoop-use-hive-ambari-view.md) para obter informações sobre como executar consultas do Hive em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="7dda3-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="7dda3-109"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7dda3-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="7dda3-110">toocomplete Olá etapas neste artigo, você precisará seguir hello.</span><span class="sxs-lookup"><span data-stu-id="7dda3-110">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="7dda3-111">Um cluster Hadoop do HDInsight baseado no Windows</span><span class="sxs-lookup"><span data-stu-id="7dda3-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="7dda3-112">Um navegador da Web</span><span class="sxs-lookup"><span data-stu-id="7dda3-112">A modern web browser</span></span>

## <span data-ttu-id="7dda3-113"><a id="run"></a>Executar consultas de Hive usando Olá Console de consulta</span><span class="sxs-lookup"><span data-stu-id="7dda3-113"><a id="run"></a> Run Hive queries using hello Query Console</span></span>
1. <span data-ttu-id="7dda3-114">Abra um navegador da web e navegue muito**https://CLUSTERNAME.azurehdinsight.net**, onde **CLUSTERNAME** é o nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7dda3-114">Open a web browser and navigate too**https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="7dda3-115">Quando solicitado, insira o nome de usuário de saudação e a senha que você usou quando criou o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7dda3-115">If prompted, enter hello user name and password that you used when you created hello cluster.</span></span>
2. <span data-ttu-id="7dda3-116">Links de saudação na parte superior de saudação da página hello, selecione **Editor Hive**.</span><span class="sxs-lookup"><span data-stu-id="7dda3-116">From hello links at hello top of hello page, select **Hive Editor**.</span></span> <span data-ttu-id="7dda3-117">Exibe um formulário que pode ser usado tooenter Olá HiveQL instruções que você deseja toorun no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7dda3-117">This displays a form that can be used tooenter hello HiveQL statements that you want toorun in hello HDInsight cluster.</span></span>

    ![editor de hive Olá](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="7dda3-119">Substitua o texto de saudação `Select * from hivesampletable` com hello HiveQL instruções a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dda3-119">Replace hello text `Select * from hivesampletable` with hello following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="7dda3-120">Essas instruções executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dda3-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="7dda3-121">**DROP TABLE**: exclui a tabela hello e arquivo de dados de saudação se Olá tabela já existir.</span><span class="sxs-lookup"><span data-stu-id="7dda3-121">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="7dda3-122">**CREATE EXTERNAL TABLE**: cria uma nova tabela “externa” em Hive.</span><span class="sxs-lookup"><span data-stu-id="7dda3-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="7dda3-123">Tabelas externas armazenam a definição da tabela Olá somente no Hive; dados de saudação são deixados no local original hello.</span><span class="sxs-lookup"><span data-stu-id="7dda3-123">External tables store only hello table definition in Hive; hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7dda3-124">Tabelas externas devem ser usadas quando você espera Olá subjacente toobe dados atualizado por uma origem externa (como um processo de carregamento de dados automatizado) ou por outra operação de MapReduce, mas convém sempre ter que dados mais recentes do toouse Olá de consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="7dda3-124">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="7dda3-125">Descartar uma tabela externa **não** excluir dados hello, definição de tabela Olá somente.</span><span class="sxs-lookup"><span data-stu-id="7dda3-125">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="7dda3-126">**FORMATO de linha**: informa ao Hive como Olá dados são formatados.</span><span class="sxs-lookup"><span data-stu-id="7dda3-126">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="7dda3-127">Nesse caso, os campos de saudação em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="7dda3-127">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="7dda3-128">**LOCAL de arquivo de texto como armazenados**: informa ao Hive onde dados saudação são armazenado (diretório de exemplo de dados de saudação) e que ela é armazenada como texto</span><span class="sxs-lookup"><span data-stu-id="7dda3-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="7dda3-129">**Selecione**: selecione uma contagem de todas as linhas em que coluna **t4** conter valor Olá **[Erro]**.</span><span class="sxs-lookup"><span data-stu-id="7dda3-129">**SELECT**: Select a count of all rows where column **t4** contain hello value **[ERROR]**.</span></span> <span data-ttu-id="7dda3-130">Isso deve retornar um valor de **3** , já que existem três linhas que contêm esse valor.</span><span class="sxs-lookup"><span data-stu-id="7dda3-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="7dda3-131">**INPUT__FILE__NAME LIKE '%.log'** - informa ao Hive que só devemos retornar dados de arquivos que terminam em .log.</span><span class="sxs-lookup"><span data-stu-id="7dda3-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="7dda3-132">Isso restringe Olá toohello sample.log arquivo de pesquisa contém dados saudação e evita que ele retornando dados de exemplo de outros arquivos de dados que não correspondem ao esquema Olá definimos.</span><span class="sxs-lookup"><span data-stu-id="7dda3-132">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
3. <span data-ttu-id="7dda3-133">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="7dda3-133">Click **Submit**.</span></span> <span data-ttu-id="7dda3-134">Olá **sessão de trabalho** em Olá parte inferior da página de saudação deve exibir os detalhes do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="7dda3-134">hello **Job Session** at hello bottom of hello page should display details for hello job.</span></span>
4. <span data-ttu-id="7dda3-135">Olá quando **Status** campo alterações muito**concluído**, selecione **exibir detalhes** para trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="7dda3-135">When hello **Status** field changes too**Completed**, select **View Details** for hello job.</span></span> <span data-ttu-id="7dda3-136">Na página de detalhes do hello, Olá **saída de trabalho** contém `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="7dda3-136">On hello details page, hello **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="7dda3-137">Você pode usar o hello **baixar** botão em toodownload esse campo em um arquivo que contém a saída de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="7dda3-137">You can use hello **Download** button under this field toodownload a file that contains hello output of hello job.</span></span>

## <span data-ttu-id="7dda3-138"><a id="summary"></a>Resumo</span><span class="sxs-lookup"><span data-stu-id="7dda3-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="7dda3-139">Como você pode ver, Olá Console de consulta fornece uma maneira fácil toorun consultas de Hive em um cluster HDInsight, monitorar o status do trabalho hello e recuperar a saída de hello.</span><span class="sxs-lookup"><span data-stu-id="7dda3-139">As you can see, hello Query Console provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

<span data-ttu-id="7dda3-140">toolearn mais sobre como usar trabalhos do Console de consulta de Hive toorun Hive, selecione **Introdução** na parte superior de saudação do hello Console de consulta, em seguida, usar exemplos Olá fornecidos.</span><span class="sxs-lookup"><span data-stu-id="7dda3-140">toolearn more about using Hive Query Console toorun Hive jobs, select **Getting Started** at hello top of hello Query Console, then use hello samples that are provided.</span></span> <span data-ttu-id="7dda3-141">Cada exemplo orienta pelo processo de saudação do uso de Hive tooanalyze dados, incluindo explicações sobre as instruções de HiveQL Olá usadas no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="7dda3-141">Each sample walks through hello process of using Hive tooanalyze data, including explanations about hello HiveQL statements used in hello sample.</span></span>

## <span data-ttu-id="7dda3-142"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7dda3-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="7dda3-143">Para obter informações gerais sobre o Hive no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7dda3-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="7dda3-144">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dda3-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="7dda3-145">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7dda3-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="7dda3-146">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dda3-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7dda3-147">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dda3-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="7dda3-148">Se você estiver usando Tez com Hive, consulte Olá documentos para as informações de depuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dda3-148">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="7dda3-149">Use Olá Tez UI no HDInsight baseados no Windows</span><span class="sxs-lookup"><span data-stu-id="7dda3-149">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="7dda3-150">Use Olá exibição Ambari Tez no HDInsight baseados em Linux</span><span class="sxs-lookup"><span data-stu-id="7dda3-150">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
