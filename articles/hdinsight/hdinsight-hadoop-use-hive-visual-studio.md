---
title: aaaHive com ferramentas de Data Lake (Hadoop) para Visual Studio - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse Olá Data Lake ferramentas para Visual Studio toorun Apache Hive consultas com Apache Hadoop em HDInsight do Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="9e0ad-103">Executar consultas do Hive usando ferramentas de Data Lake Olá para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e0ad-103">Run Hive queries using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="9e0ad-104">Saiba como toouse Olá Data Lake ferramentas para Visual Studio tooquery Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-104">Learn how toouse hello Data Lake tools for Visual Studio tooquery Apache Hive.</span></span> <span data-ttu-id="9e0ad-105">Olá Data Lake ferramentas permitem que você tooeasily criar, enviar e monitorar tooHadoop de consultas de Hive no HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-105">hello Data Lake tools allow you tooeasily create, submit, and monitor Hive queries tooHadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="9e0ad-106"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9e0ad-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="9e0ad-107">Um cluster Azure HDInsight (Hadoop no HDInsight)</span><span class="sxs-lookup"><span data-stu-id="9e0ad-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9e0ad-108">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9e0ad-109">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9e0ad-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="9e0ad-110">O Visual Studio (um dos Olá versões a seguir):</span><span class="sxs-lookup"><span data-stu-id="9e0ad-110">Visual Studio (one of hello following versions):</span></span>

    * <span data-ttu-id="9e0ad-111">Visual Studio 2013 Community/Professional/Premium/Ultimate com Atualização 4</span><span class="sxs-lookup"><span data-stu-id="9e0ad-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="9e0ad-112">Visual Studio 2015 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="9e0ad-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="9e0ad-113">Visual Studio 2017 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="9e0ad-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="9e0ad-114">Ferramentas do HDInsight para Visual Studio ou ferramentas do Azure Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="9e0ad-115">Consulte [começar a usar ferramentas Hadoop do Visual Studio para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) para obter informações sobre como instalar e configurar as ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring hello tools.</span></span>

## <span data-ttu-id="9e0ad-116"><a id="run"></a>Executar consultas de Hive usando Olá Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e0ad-116"><a id="run"></a> Run Hive queries using hello Visual Studio</span></span>

1. <span data-ttu-id="9e0ad-117">Abra o **Visual Studio** e selecione **Novo** > **Projeto** > **Azure Data Lake** > **HIVE** > **Aplicativo Hive**.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="9e0ad-118">Forneça um nome para esse projeto.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="9e0ad-119">Olá abrir **Script.hql** arquivo criado com esse projeto e colar em Olá HiveQL instruções a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e0ad-119">Open hello **Script.hql** file that is created with this project, and paste in hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="9e0ad-120">Essas instruções executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e0ad-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="9e0ad-121">`DROP TABLE`: Se a tabela de saudação existir, esta instrução exclui-lo.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-121">`DROP TABLE`: If hello table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="9e0ad-122">`CREATE EXTERNAL TABLE`: cria uma nova tabela 'externa' no Hive.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="9e0ad-123">Tabelas externas apenas armazenam a definição de tabela Olá no Hive (dados são deixados no local original Olá Olá).</span><span class="sxs-lookup"><span data-stu-id="9e0ad-123">External tables only store hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="9e0ad-124">Tabelas externas devem ser usadas quando você espera Olá toobe de dados subjacentes atualizado por uma fonte externa.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-124">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="9e0ad-125">Por exemplo, um trabalho de MapReduce ou serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="9e0ad-126">Descartar uma tabela externa **não** excluir dados hello, definição de tabela Olá somente.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="9e0ad-127">`ROW FORMAT`: Informa ao Hive como Olá dados são formatados.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-127">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="9e0ad-128">Nesse caso, os campos de saudação em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-128">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="9e0ad-129">`STORED AS TEXTFILE LOCATION`: Informa ao Hive onde hello os dados são armazenados (diretório de exemplo de dados de saudação) e que ela é armazenada como texto.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="9e0ad-130">`SELECT`: Selecione uma contagem de todas as linhas em que coluna `t4` contém valor Olá `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-130">`SELECT`: Select a count of all rows where column `t4` contains hello value `[ERROR]`.</span></span> <span data-ttu-id="9e0ad-131">Essa instrução retorna um valor de `3`, já que há três linhas que contêm esse valor.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="9e0ad-132">`INPUT__FILE__NAME LIKE '%.log'`: informa ao Hive que só devemos retornar dados de arquivos que terminam em .log.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="9e0ad-133">Essa cláusula restringe Olá toohello sample.log arquivo de pesquisa contém dados saudação.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-133">This clause restricts hello search toohello sample.log file that contains hello data.</span></span>

3. <span data-ttu-id="9e0ad-134">Na barra de ferramentas hello, selecione Olá **HDInsight Cluster** que você deseja toouse para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-134">From hello toolbar, select hello **HDInsight Cluster** that you want toouse for this query.</span></span> <span data-ttu-id="9e0ad-135">Selecione **enviar** instruções de saudação toorun como um trabalho de Hive.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-135">Select **Submit** toorun hello statements as a Hive job.</span></span>

   ![Barra de envio](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="9e0ad-137">Olá **resumo do trabalho de Hive** aparece e exibe informações sobre Olá executando o trabalho.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-137">hello **Hive Job Summary** appears and displays information about hello running job.</span></span> <span data-ttu-id="9e0ad-138">Saudação de uso **atualizar** link toorefresh Olá informações de trabalho até Olá **Status do trabalho** muda muito**concluído**.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-138">Use hello **Refresh** link toorefresh hello job information, until hello **Job Status** changes too**Completed**.</span></span>

   ![resumo do trabalho exibindo um trabalho concluído](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="9e0ad-140">Saudação de uso **saída de trabalho** vincular a saída de hello tooview deste trabalho.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-140">Use hello **Job Output** link tooview hello output of this job.</span></span> <span data-ttu-id="9e0ad-141">Ele exibe `[ERROR] 3`, que é o valor de saudação retornado por essa consulta.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-141">It displays `[ERROR] 3`, which is hello value returned by this query.</span></span>

6. <span data-ttu-id="9e0ad-142">Você também pode executar consultas Hive sem criar um projeto.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="9e0ad-143">Usando o **Gerenciador de Servidores**, expanda **Azure** > **HDInsight**, clique com o botão direito do mouse no seu servidor do HDInsight e selecione **Escrever uma Consulta de Hive**.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="9e0ad-144">Em Olá **temp.hql** documento que é exibido, adicionar Olá HiveQL instruções a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e0ad-144">In hello **temp.hql** document that appears, add hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="9e0ad-145">Essas instruções executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e0ad-145">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="9e0ad-146">`CREATE TABLE IF NOT EXISTS`: cria uma tabela, se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="9e0ad-147">Porque Olá `EXTERNAL` palavra-chave não for usada, essa instrução cria uma tabela interna.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-147">Because hello `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="9e0ad-148">Tabelas internas são armazenadas no data warehouse do hello Hive e são gerenciadas pelo Hive.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-148">Internal tables are stored in hello Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="9e0ad-149">Ao contrário de `EXTERNAL` tabelas, descartar uma tabela interna também exclui Olá dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes hello underlying data.</span></span>

   * <span data-ttu-id="9e0ad-150">`STORED AS ORC`: Repositórios Olá dados em linha otimizado Colunar (ORC) formato.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-150">`STORED AS ORC`: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="9e0ad-151">Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="9e0ad-152">`INSERT OVERWRITE ... SELECT`: Seleciona linhas Olá `log4jLogs` tabela que contêm `[ERROR]`, em seguida, insere Olá dados em hello `errorLogs` tabela.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-152">`INSERT OVERWRITE ... SELECT`: Selects rows from hello `log4jLogs` table that contain `[ERROR]`, then inserts hello data into hello `errorLogs` table.</span></span>

8. <span data-ttu-id="9e0ad-153">Na barra de ferramentas hello, selecione **enviar** toorun trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-153">From hello toolbar, select **Submit** toorun hello job.</span></span> <span data-ttu-id="9e0ad-154">Saudação de uso **Status do trabalho** toodetermine trabalho Olá foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-154">Use hello **Job Status** toodetermine that hello job has completed successfully.</span></span>

9. <span data-ttu-id="9e0ad-155">tooverify que Olá trabalho criado tabela hello, use **Server Explorer** e expanda **Azure** > **HDInsight** > seu cluster HDInsight > **Bancos de dados de hive** > **padrão**.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-155">tooverify that hello job created hello table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="9e0ad-156">Olá **em decorrência** tabela e hello **log4jLogs** tabela são listadas.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-156">hello **errorLogs** table and hello **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="9e0ad-157"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9e0ad-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="9e0ad-158">Como você pode ver, ferramentas do HDInsight Olá para o Visual Studio fornecem um toowork de maneira fácil com consultas de Hive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e0ad-158">As you can see, hello HDInsight tools for Visual Studio provide an easy way toowork with Hive queries on HDInsight.</span></span>

<span data-ttu-id="9e0ad-159">Para obter informações gerais sobre o Hive no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9e0ad-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="9e0ad-160">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e0ad-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="9e0ad-161">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9e0ad-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="9e0ad-162">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e0ad-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="9e0ad-163">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e0ad-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="9e0ad-164">Para obter mais informações sobre as ferramentas do HDInsight Olá para o Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="9e0ad-164">For more information about hello HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="9e0ad-165">Introdução às ferramentas do HDInsight para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e0ad-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
