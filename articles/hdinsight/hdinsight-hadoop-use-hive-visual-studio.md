---
title: "Ferramentas do Hive com Data Lake (Hadoop) para Visual Studio – Azure HDInsight | Microsoft Docs"
description: Saiba como usar as ferramentas de Data Lake para Visual Studio para executar consultas do Apache Hive com Apache Hadoop no Azure HDInsight.
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
ms.openlocfilehash: 3411c59fee73aa2e26a05d70e1dae11cdfc865ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="6b4d8-103">Executar consultas Hive usando as ferramentas do Data Lake para o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b4d8-103">Run Hive queries using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="6b4d8-104">Saiba como usar as ferramentas do Data Lake para Visual Studio para consultar o Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-104">Learn how to use the Data Lake tools for Visual Studio to query Apache Hive.</span></span> <span data-ttu-id="6b4d8-105">As ferramentas de Data Lake permitem que você facilmente crie, envie e monitore consultas de Hive para Hadoop no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-105">The Data Lake tools allow you to easily create, submit, and monitor Hive queries to Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="6b4d8-106"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6b4d8-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="6b4d8-107">Um cluster Azure HDInsight (Hadoop no HDInsight)</span><span class="sxs-lookup"><span data-stu-id="6b4d8-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="6b4d8-108">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6b4d8-109">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6b4d8-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="6b4d8-110">Visual Studio (uma das versões a seguir):</span><span class="sxs-lookup"><span data-stu-id="6b4d8-110">Visual Studio (one of the following versions):</span></span>

    * <span data-ttu-id="6b4d8-111">Visual Studio 2013 Community/Professional/Premium/Ultimate com Atualização 4</span><span class="sxs-lookup"><span data-stu-id="6b4d8-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="6b4d8-112">Visual Studio 2015 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="6b4d8-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="6b4d8-113">Visual Studio 2017 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="6b4d8-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="6b4d8-114">Ferramentas do HDInsight para Visual Studio ou ferramentas do Azure Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="6b4d8-115">Confira [Começar a usar as ferramentas Hadoop para HDInsight do Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) para obter informações sobre como instalar e configurar as ferramentas.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring the tools.</span></span>

## <span data-ttu-id="6b4d8-116"><a id="run"></a> Executar consultas Hive usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b4d8-116"><a id="run"></a> Run Hive queries using the Visual Studio</span></span>

1. <span data-ttu-id="6b4d8-117">Abra o **Visual Studio** e selecione **Novo** > **Projeto** > **Azure Data Lake** > **HIVE** > **Aplicativo Hive**.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="6b4d8-118">Forneça um nome para esse projeto.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="6b4d8-119">Abra o arquivo **Script.hql** criado com esse projeto e cole as seguintes instruções HiveQL:</span><span class="sxs-lookup"><span data-stu-id="6b4d8-119">Open the **Script.hql** file that is created with this project, and paste in the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="6b4d8-120">As instruções executam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="6b4d8-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="6b4d8-121">`DROP TABLE`: se a tabela existir, esta instrução a excluirá.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-121">`DROP TABLE`: If the table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="6b4d8-122">`CREATE EXTERNAL TABLE`: cria uma nova tabela 'externa' no Hive.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="6b4d8-123">As tabelas externas armazenam apenas a definição da tabela no Hive (os dados são mantidos no local original).</span><span class="sxs-lookup"><span data-stu-id="6b4d8-123">External tables only store the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="6b4d8-124">As tabelas externas devem ser usadas quando você espera que os dados subjacentes sejam atualizados por uma fonte externa.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-124">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="6b4d8-125">Por exemplo, um trabalho de MapReduce ou serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="6b4d8-126">Remover uma tabela externa **não** exclui os dados, somente a definição de tabela.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="6b4d8-127">`ROW FORMAT`: informa ao Hive como os dados são formatados.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-127">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="6b4d8-128">Nesse caso, os campos em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-128">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="6b4d8-129">`STORED AS TEXTFILE LOCATION`: informa ao Hive o local em que os dados são armazenados (o diretório de exemplos/dados) e que estão armazenados como texto.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="6b4d8-130">`SELECT`: seleciona uma contagem de todas as linhas, nas quais a coluna `t4` contém o valor `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-130">`SELECT`: Select a count of all rows where column `t4` contains the value `[ERROR]`.</span></span> <span data-ttu-id="6b4d8-131">Essa instrução retorna um valor de `3`, já que há três linhas que contêm esse valor.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="6b4d8-132">`INPUT__FILE__NAME LIKE '%.log'`: informa ao Hive que só devemos retornar dados de arquivos que terminam em .log.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="6b4d8-133">Essa cláusula restringe a pesquisa para o arquivo sample.log que contém os dados.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-133">This clause restricts the search to the sample.log file that contains the data.</span></span>

3. <span data-ttu-id="6b4d8-134">Na barra de ferramentas, selecione o **Cluster HDInsight** que você deseja usar nessa consulta.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-134">From the toolbar, select the **HDInsight Cluster** that you want to use for this query.</span></span> <span data-ttu-id="6b4d8-135">Selecione **Enviar** para executar as instruções como um trabalho do Hive.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-135">Select **Submit** to run the statements as a Hive job.</span></span>

   ![Barra de envio](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="6b4d8-137">O **Resumo do Trabalho do Hive** aparecerá e exibirá informações sobre o trabalho em execução.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-137">The **Hive Job Summary** appears and displays information about the running job.</span></span> <span data-ttu-id="6b4d8-138">Use o link **Atualizar** para atualizar as informações do trabalho, até o **Status do Trabalho** ser alterado para **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-138">Use the **Refresh** link to refresh the job information, until the **Job Status** changes to **Completed**.</span></span>

   ![resumo do trabalho exibindo um trabalho concluído](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="6b4d8-140">Use o link **Saída de Trabalho** para exibir a saída desse trabalho.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-140">Use the **Job Output** link to view the output of this job.</span></span> <span data-ttu-id="6b4d8-141">Ele exibe `[ERROR] 3`, que é o valor retornado por essa consulta.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-141">It displays `[ERROR] 3`, which is the value returned by this query.</span></span>

6. <span data-ttu-id="6b4d8-142">Você também pode executar consultas Hive sem criar um projeto.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="6b4d8-143">Usando o **Gerenciador de Servidores**, expanda **Azure** > **HDInsight**, clique com o botão direito do mouse no seu servidor do HDInsight e selecione **Escrever uma Consulta de Hive**.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="6b4d8-144">No documento **temp.hql** que aparece, adicione as seguintes instruções HiveQL:</span><span class="sxs-lookup"><span data-stu-id="6b4d8-144">In the **temp.hql** document that appears, add the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="6b4d8-145">As instruções executam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="6b4d8-145">These statements perform the following actions:</span></span>

   * <span data-ttu-id="6b4d8-146">`CREATE TABLE IF NOT EXISTS`: cria uma tabela, se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="6b4d8-147">Uma vez que a palavra-chave `EXTERNAL` não é usada, essa instrução cria uma tabela interna.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-147">Because the `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="6b4d8-148">As tabelas internas são armazenadas no data warehouse do Hive e gerenciadas por ele.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-148">Internal tables are stored in the Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6b4d8-149">Ao contrário das tabelas `EXTERNAL`, o descarte de uma tabela interna excluirá também os dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes the underlying data.</span></span>

   * <span data-ttu-id="6b4d8-150">`STORED AS ORC`: armazena os dados no formato ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="6b4d8-150">`STORED AS ORC`: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="6b4d8-151">Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="6b4d8-152">`INSERT OVERWRITE ... SELECT`: seleciona linhas da tabela `log4jLogs` que contêm `[ERROR]` e, então, insere os dados na tabela `errorLogs`.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-152">`INSERT OVERWRITE ... SELECT`: Selects rows from the `log4jLogs` table that contain `[ERROR]`, then inserts the data into the `errorLogs` table.</span></span>

8. <span data-ttu-id="6b4d8-153">Na barra de ferramentas, selecione no menu suspenso de **Enviar** para executar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-153">From the toolbar, select **Submit** to run the job.</span></span> <span data-ttu-id="6b4d8-154">Use o **Status do Trabalho** para determinar se o trabalho foi concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-154">Use the **Job Status** to determine that the job has completed successfully.</span></span>

9. <span data-ttu-id="6b4d8-155">Para verificar se o trabalho criou a tabela, use o **Gerenciador de Servidores** e expanda **Azure** > **HDInsight** > seu cluster HDInsight > **Bancos de Dados do Hive** > **padrão**.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-155">To verify that the job created the table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="6b4d8-156">As tabelas **errorLogs** e **log4jLogs** são listadas.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-156">The **errorLogs** table and the **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="6b4d8-157"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6b4d8-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="6b4d8-158">Como você pode ver, as ferramentas do HDInsight para o Visual Studio fornecem uma maneira fácil de trabalhar com as consultas do Hive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6b4d8-158">As you can see, the HDInsight tools for Visual Studio provide an easy way to work with Hive queries on HDInsight.</span></span>

<span data-ttu-id="6b4d8-159">Para obter informações gerais sobre o Hive no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6b4d8-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="6b4d8-160">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b4d8-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="6b4d8-161">Para obter informações sobre outros modos possíveis de trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6b4d8-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="6b4d8-162">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b4d8-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="6b4d8-163">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b4d8-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="6b4d8-164">Para obter mais informações sobre as ferramentas do HDInsight para o Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="6b4d8-164">For more information about the HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="6b4d8-165">Introdução às ferramentas do HDInsight para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b4d8-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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
