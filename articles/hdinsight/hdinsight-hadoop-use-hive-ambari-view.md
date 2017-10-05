---
title: "Usar os Modos de Exibição do Ambari para trabalhar com o Hive no HDInsight (Hadoop) – Azure | Microsoft Docs"
description: "Saiba como usar o Modo de Exibição do Hive em seu navegador da Web para enviar consultas do Hive. O Modo de exibição do Hive faz parte da Interface de Usuário da Web do Ambari fornecida com o cluster HDInsight baseado em Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 80df3da4d62feb814ea2dd97c96e57954093c5c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="9a8b4-104">Use o Modo de Exibição do Hive com o Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-104">Use the Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="9a8b4-105">Aprenda a executar consultas do Hive usando a Exibição do Hive do Ambari.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-105">Learn how to run Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="9a8b4-106">O Ambari é um utilitário de monitoramento e de gerenciamento fornecido com clusters HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="9a8b4-107">Um dos recursos fornecidos pelo Ambari é uma interface de usuário da Web que pode ser usada para executar consultas do Hive.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-107">One of the features provided through Ambari is a Web UI that can be used to run Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="9a8b4-108">O Ambari possui muitos recursos que não são abordados neste documento.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="9a8b4-109">Para saber mais, confira [Gerenciar clusters HDInsight usando a interface do usuário da Web do Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="9a8b4-109">For more information, see [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a8b4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9a8b4-110">Prerequisites</span></span>

* <span data-ttu-id="9a8b4-111">Criar um cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9a8b4-112">Para saber mais sobre como criar um cluster, confira [Introdução ao HDInsight baseado no Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9a8b4-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a8b4-113">As etapas deste documento exigem um cluster HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-113">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="9a8b4-114">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-114">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9a8b4-115">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9a8b4-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-the-hive-view"></a><span data-ttu-id="9a8b4-116">Abrir o modo de exibição Hive</span><span class="sxs-lookup"><span data-stu-id="9a8b4-116">Open the Hive view</span></span>

<span data-ttu-id="9a8b4-117">Você pode abrir os Modos de exibição do Ambari do portal do Azure; selecione seu cluster HDInsight e escolha **Modos de exibição do Ambari** na seção **Links Rápidos**.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-117">You can Ambari Views from the Azure portal; select your HDInsight cluster and then select **Ambari Views** from the **Quick Links** section.</span></span>

![seção de links rápidos do portal](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="9a8b4-119">Na lista de exibições, selecione __Exibição de Hive__.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-119">From the list of views, select the __Hive View__.</span></span>

![A exibição de Hive selecionada](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="9a8b4-121">Ao acessar o Ambari, você receberá uma solicitação para se autenticar no site.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-121">When accessing Ambari, you are prompted to authenticate to the site.</span></span> <span data-ttu-id="9a8b4-122">Insira o nome da conta e senha de administrador (o padrão é `admin`) que você usou ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-122">Enter the admin (default `admin`) account name and password you used when creating the cluster.</span></span>

<span data-ttu-id="9a8b4-123">Você deverá ver uma página semelhante à seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="9a8b4-123">You should see a page similar to the following image:</span></span>

![Imagem da planilha de consulta para a exibição de Hive](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="9a8b4-125"><a name="hivequery"></a>Executar uma consulta</span><span class="sxs-lookup"><span data-stu-id="9a8b4-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="9a8b4-126">Use as seguintes etapas da exibição do Hive para executar uma consulta do Hive.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-126">To run a hive query, use the following steps from the Hive view.</span></span>

1. <span data-ttu-id="9a8b4-127">Da guia __Consulta__, cole as seguintes instruções HiveQL na planilha:</span><span class="sxs-lookup"><span data-stu-id="9a8b4-127">From the __Query__ tab, paste the following HiveQL statements into the worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="9a8b4-128">As instruções executam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="9a8b4-128">These statements perform the following actions:</span></span>

   * <span data-ttu-id="9a8b4-129">`DROP TABLE` – exclui a tabela e o arquivo de dados, caso a tabela já exista.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-129">`DROP TABLE` - Deletes the table and the data file, in case the table already exists.</span></span>

   * <span data-ttu-id="9a8b4-130">`CREATE EXTERNAL TABLE` – cria uma nova tabela "externa" no Hive.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="9a8b4-131">As tabelas externas armazenam apenas a definição da tabela no Hive.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-131">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="9a8b4-132">Os dados são mantidos no local original.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-132">The data is left in the original location.</span></span>

   * <span data-ttu-id="9a8b4-133">`ROW FORMAT` – o modo como os dados são formatados.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-133">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="9a8b4-134">Nesse caso, os campos em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-134">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="9a8b4-135">`STORED AS TEXTFILE LOCATION` – informa ao Hive o local em que os dados são armazenados e se estão armazenados como texto.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-135">`STORED AS TEXTFILE LOCATION` - Where the data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="9a8b4-136">`SELECT` – seleciona uma contagem de todas as linhas em que a coluna t4 contém o valor [ERROR].</span><span class="sxs-lookup"><span data-stu-id="9a8b4-136">`SELECT` - Selects a count of all rows where column t4 contains the value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="9a8b4-137">As tabelas externas devem ser usadas quando você espera que os dados subjacentes sejam atualizados por uma fonte externa.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-137">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="9a8b4-138">Por exemplo, um processo de carregamento de dados automatizados ou por outra operação MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="9a8b4-139">Remover uma tabela externa *não* exclui os dados, somente a definição de tabela.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-139">Dropping an external table does *not* delete the data, only the table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9a8b4-140">Deixe a seleção __Banco de dados__ em __padrão__.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-140">Leave the __Database__ selection at __default__.</span></span> <span data-ttu-id="9a8b4-141">Os exemplos neste documento usam o banco de dados padrão incluído no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-141">The examples in this document use the default database included with HDInsight.</span></span>

2. <span data-ttu-id="9a8b4-142">Para iniciar a consulta, use o botão **Executar** abaixo da planilha.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-142">To start the query, use the **Execute** button below the worksheet.</span></span> <span data-ttu-id="9a8b4-143">Ele fica laranja e o texto é alterado para **Parar**.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-143">It turns orange and the text changes to **Stop**.</span></span>

3. <span data-ttu-id="9a8b4-144">Depois que a consulta for concluída, a seção **Resultados** exibirá os resultados da operação.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-144">Once the query has finished, The **Results** tab displays the results of the operation.</span></span> <span data-ttu-id="9a8b4-145">O texto a seguir é o resultado da consulta:</span><span class="sxs-lookup"><span data-stu-id="9a8b4-145">The following text is the result of the query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="9a8b4-146">A guia **Logs** pode ser usada para exibir as informações de log criadas pelo trabalho.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-146">The **Logs** tab can be used to view the logging information created by the job.</span></span>

   > [!TIP]
   > <span data-ttu-id="9a8b4-147">O diálogo suspenso **Salvar resultados** no canto superior esquerdo da seção **Resultados do Processo de Consulta** permite que você baixe ou salve os resultados.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-147">The **Save results** drop-down dialog in the upper left of the **Query Process Results** section allows you to download or save results.</span></span>

4. <span data-ttu-id="9a8b4-148">Selecione as quatro primeiras linhas dessa consulta e escolha **Executar**.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-148">Select the first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="9a8b4-149">Observe que não há resultados quando o trabalho é concluído.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-149">Notice that there are no results when the job completes.</span></span> <span data-ttu-id="9a8b4-150">O uso do botão **Executar** quando parte da consulta está selecionada executa apenas as instruções escolhidas.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-150">Using the **Execute** button when part of the query is selected only runs the selected statements.</span></span> <span data-ttu-id="9a8b4-151">Nesse caso, a seleção não incluiu a instrução final que recupera linhas da tabela.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-151">In this case, the selection didn't include the final statement that retrieves rows from the table.</span></span> <span data-ttu-id="9a8b4-152">Se escolher apenas essa linha e usar **Executar**, você verá os resultados esperados.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-152">If you select just that line and use **Execute**, you should see the expected results.</span></span>

5. <span data-ttu-id="9a8b4-153">Para adicionar uma planilha, use o botão **Nova Planilha** na parte inferior do **Editor de Consultas**.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-153">To add a worksheet, use the **New Worksheet** button at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="9a8b4-154">Na nova planilha, digite as seguintes instruções HiveQL:</span><span class="sxs-lookup"><span data-stu-id="9a8b4-154">In the new worksheet, enter the following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="9a8b4-155">As instruções executam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="9a8b4-155">These statements perform the following actions:</span></span>

   * <span data-ttu-id="9a8b4-156">**CREATE TABLE IF NOT EXISTS** - cria uma tabela, se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="9a8b4-157">Como a palavra-chave **EXTERNAL** não é usada, uma tabela interna é criada.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-157">Since the **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="9a8b4-158">Uma tabela interna é armazenada no data warehouse do Hive e é totalmente gerenciada pelo Hive.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-158">An internal table is stored in the Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="9a8b4-159">Diferentemente de tabelas externas, o descarte de uma tabela interna excluirá também os dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-159">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="9a8b4-160">**STORES AS ORC** : armazena os dados no formato ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="9a8b4-160">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="9a8b4-161">Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="9a8b4-162">**INSERT OVERWRITE ... SELECT** – seleciona linhas da tabela **log4jLogs** que contêm `[ERROR]` e insere os dados na tabela **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-162">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain `[ERROR]`, and then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="9a8b4-163">Use o botão **Executar** para executar essa consulta.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-163">Use the **Execute** button to run this query.</span></span> <span data-ttu-id="9a8b4-164">A guia **Resultados** não contém nenhuma informação quando a consulta retorna zero linhas.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-164">The **Results** tab does not contain any information when the query returns zero rows.</span></span> <span data-ttu-id="9a8b4-165">O status deve mostrar **SUCCEEDED** após a conclusão da consulta.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-165">The status should show as **SUCCEEDED** once the query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="9a8b4-166">Explicação visual</span><span class="sxs-lookup"><span data-stu-id="9a8b4-166">Visual explain</span></span>

<span data-ttu-id="9a8b4-167">Para exibir uma visualização do plano de consulta, selecione a guia **Explicação Visual** abaixo da planilha.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-167">To display a visualization of the query plan, select the **Visual Explain** tab below the worksheet.</span></span>

<span data-ttu-id="9a8b4-168">O modo de exibição **Explicação Visual** da consulta pode ser útil na compreensão do fluxo de consultas complexas.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-168">The **Visual Explain** view of the query can be helpful in understanding the flow of complex queries.</span></span> <span data-ttu-id="9a8b4-169">Você pode exibir um equivalente textual desse modo de exibição usando o botão **Explicar** no Editor de Consultas.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-169">You can view a textual equivalent of this view by using the **Explain** button in the Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="9a8b4-170">Interface de usuário do Tez</span><span class="sxs-lookup"><span data-stu-id="9a8b4-170">Tez UI</span></span>

<span data-ttu-id="9a8b4-171">Para exibir a interface do usuário do Tez para a consulta, selecione a guia **Tez** abaixo da planilha.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-171">To display the Tez UI for the query, select the **Tez** tab below the worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a8b4-172">O Tez não é usado para resolver todas as consultas.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-172">Tez is not used to resolve all queries.</span></span> <span data-ttu-id="9a8b4-173">Muitas consultas de Hive podem ser resolvidas sem usar o Tez.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="9a8b4-174">Se o Tez foi usado para resolver a consulta, o DAG (gráfico acíclico dirigido) é exibido.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-174">If Tez was used to resolve the query, the Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="9a8b4-175">Se você quiser exibir o DAG de consultas executadas anteriormente ou depurar o processo do Tez, use [Modo de Exibição do Tez exibição](hdinsight-debug-ambari-tez-view.md) .</span><span class="sxs-lookup"><span data-stu-id="9a8b4-175">If you want to view the DAG for queries you've ran in the past, or debug the Tez process, use the [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="9a8b4-176">Exibir histórico de trabalho</span><span class="sxs-lookup"><span data-stu-id="9a8b4-176">View job history</span></span>

<span data-ttu-id="9a8b4-177">A guia __Trabalhos__ exibe um histórico das consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-177">The __Jobs__ tab displays a history of Hive queries.</span></span>

![Imagem do histórico de trabalhos](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="9a8b4-179">Tabelas de banco de dados</span><span class="sxs-lookup"><span data-stu-id="9a8b4-179">Database tables</span></span>

<span data-ttu-id="9a8b4-180">Você pode usar a guia __tabelas__ para trabalhar com tabelas em um banco de dados de Hive.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-180">You can use the __Tables__ tab to work with tables within a Hive database.</span></span>

![Imagem da guia tabelas](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="9a8b4-182">Consultas salvas</span><span class="sxs-lookup"><span data-stu-id="9a8b4-182">Saved queries</span></span>

<span data-ttu-id="9a8b4-183">Na guia consulta você pode, opcionalmente, salvar consultas.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-183">From the Query tab, you can optionally save queries.</span></span> <span data-ttu-id="9a8b4-184">Uma vez salva, você pode reutilizar a consulta por meio da guia __Consultas Salvas__.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-184">Once saved, you can reuse the query from the __Saved Queries__ tab.</span></span>

![Imagem da guia Consultas Salvas](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="9a8b4-186">Funções definidas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="9a8b4-186">User-defined functions</span></span>

<span data-ttu-id="9a8b4-187">O Hive também pode ser estendido por meio de UDFs (funções definidas pelo usuário).</span><span class="sxs-lookup"><span data-stu-id="9a8b4-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="9a8b4-188">As UDF permitem que você implemente funcionalidade ou lógica que não é facilmente modelada em HiveQL.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-188">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="9a8b4-189">A guia UDF na parte superior da exibição do Hive permite que você declare e salve um conjunto de UDFs.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-189">The UDF tab at the top of the Hive View allows you to declare and save a set of UDFs.</span></span> <span data-ttu-id="9a8b4-190">Essas UDFs podem ser usadas com o **Editor de Consultas**.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-190">These UDFs can be used with the **Query Editor**.</span></span>

![Imagem da guia UDF](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="9a8b4-192">Depois de adicionar uma UDF ao Modo de Exibição do Hive, um botão **Inserir udfs** será exibido na parte inferior do **Editor de Consultas**.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-192">Once you have added a UDF to the Hive View, an **Insert udfs** button appears at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="9a8b4-193">Ao selecionar essa entrada, uma lista suspensa de UDFs definidas na Exibição do Hive será exibida.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-193">Selecting this entry displays a drop-down list of the UDFs defined in the Hive View.</span></span> <span data-ttu-id="9a8b4-194">A seleção de uma UDF adiciona instruções HiveQL à sua consulta para habilitar a UDF.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-194">Selecting a UDF adds HiveQL statements to your query to enable the UDF.</span></span>

<span data-ttu-id="9a8b4-195">Por exemplo, se você tiver definido uma UDF com as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="9a8b4-195">For example, if you have defined a UDF with the following properties:</span></span>

* <span data-ttu-id="9a8b4-196">Nome de recurso: myudfs</span><span class="sxs-lookup"><span data-stu-id="9a8b4-196">Resource name: myudfs</span></span>

* <span data-ttu-id="9a8b4-197">Caminho do recurso: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="9a8b4-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="9a8b4-198">Nome da UDF: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="9a8b4-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="9a8b4-199">Nome de classe da  UDF: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="9a8b4-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="9a8b4-200">O botão **Inserir udfs** exibe uma entrada denominada **myudfs**, com outra lista suspensa para cada UDF definida para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-200">Using the **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="9a8b4-201">Nesse caso, **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="9a8b4-202">A seleção dessa entrada adiciona o seguinte ao início da consulta:</span><span class="sxs-lookup"><span data-stu-id="9a8b4-202">Selecting this entry adds the following to the beginning of the query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="9a8b4-203">Você pode usar a UDF em sua consulta.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-203">You can then use the UDF in your query.</span></span> <span data-ttu-id="9a8b4-204">Por exemplo: `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="9a8b4-205">Para saber mais sobre como usar UDFs com o Hive no HDInsight, consulte os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="9a8b4-205">For more information on using UDFs with Hive on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="9a8b4-206">Usando o Python com o Hive e com o Pig no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a8b4-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="9a8b4-207">Como adicionar UDF personalizadas do Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a8b4-207">How to add a custom Hive UDF to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="9a8b4-208">Configurações do Hive</span><span class="sxs-lookup"><span data-stu-id="9a8b4-208">Hive settings</span></span>

<span data-ttu-id="9a8b4-209">A opção Configurações pode ser usada para alterar várias configurações de Hive.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-209">Settings can be used to change various Hive settings.</span></span> <span data-ttu-id="9a8b4-210">Por exemplo, alterar o mecanismo de execução para o Hive de Tez (o padrão) para MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9a8b4-210">For example, changing the execution engine for Hive from Tez (the default) to MapReduce.</span></span>

## <span data-ttu-id="9a8b4-211"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9a8b4-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="9a8b4-212">Para informações gerais sobre o Hive no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9a8b4-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="9a8b4-213">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a8b4-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="9a8b4-214">Para obter informações sobre outras maneiras que você pode trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9a8b4-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="9a8b4-215">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a8b4-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9a8b4-216">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a8b4-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
