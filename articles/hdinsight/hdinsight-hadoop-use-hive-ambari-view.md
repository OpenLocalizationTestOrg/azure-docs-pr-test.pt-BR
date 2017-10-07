---
title: "aaaUse Ambari exibições toowork com Hive no HDInsight (Hadoop) - Azure | Microsoft Docs"
description: "Saiba como toouse Olá Hive exibição de suas consultas de Hive do toosubmit de navegador da web. Olá exibição Hive faz parte da saudação de que interface do usuário do Ambari Web fornecido com seu cluster HDInsight baseados em Linux."
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
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="3cb23-104">Use Olá exibição Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3cb23-104">Use hello Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="3cb23-105">Saiba como toorun Hive consultas usando o modo de exibição de Hive do Ambari.</span><span class="sxs-lookup"><span data-stu-id="3cb23-105">Learn how toorun Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="3cb23-106">O Ambari é um utilitário de monitoramento e de gerenciamento fornecido com clusters HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="3cb23-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="3cb23-107">Um dos recursos de saudação fornecidos por meio do Ambari é uma interface de usuário da Web que pode ser usado toorun consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="3cb23-107">One of hello features provided through Ambari is a Web UI that can be used toorun Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="3cb23-108">O Ambari possui muitos recursos que não são abordados neste documento.</span><span class="sxs-lookup"><span data-stu-id="3cb23-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="3cb23-109">Para obter mais informações, consulte [HDInsight gerenciar clusters usando Olá da interface do usuário do Ambari Web](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="3cb23-109">For more information, see [Manage HDInsight clusters by using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cb23-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3cb23-110">Prerequisites</span></span>

* <span data-ttu-id="3cb23-111">Criar um cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="3cb23-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="3cb23-112">Para saber mais sobre como criar um cluster, confira [Introdução ao HDInsight baseado no Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3cb23-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3cb23-113">etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux.</span><span class="sxs-lookup"><span data-stu-id="3cb23-113">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="3cb23-114">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3cb23-114">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3cb23-115">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3cb23-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-hello-hive-view"></a><span data-ttu-id="3cb23-116">Abrir modo de exibição de Hive Olá</span><span class="sxs-lookup"><span data-stu-id="3cb23-116">Open hello Hive view</span></span>

<span data-ttu-id="3cb23-117">Você pode Ambari exibições de saudação portal do Azure; Selecione seu cluster HDInsight e, em seguida, selecione **Ambari exibições** de saudação **Links rápidos** seção.</span><span class="sxs-lookup"><span data-stu-id="3cb23-117">You can Ambari Views from hello Azure portal; select your HDInsight cluster and then select **Ambari Views** from hello **Quick Links** section.</span></span>

![seção de links rápidos do portal de saudação](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="3cb23-119">Saudação de modos de exibição, selecione lista Olá __exibição Hive__.</span><span class="sxs-lookup"><span data-stu-id="3cb23-119">From hello list of views, select hello __Hive View__.</span></span>

![Olá Hive exibição selecionada](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="3cb23-121">Ao acessar o Ambari, será solicitada tooauthenticate toohello site.</span><span class="sxs-lookup"><span data-stu-id="3cb23-121">When accessing Ambari, you are prompted tooauthenticate toohello site.</span></span> <span data-ttu-id="3cb23-122">Digite Olá administrador (padrão `admin`) conta de nome e a senha usada ao criar hello cluster.</span><span class="sxs-lookup"><span data-stu-id="3cb23-122">Enter hello admin (default `admin`) account name and password you used when creating hello cluster.</span></span>

<span data-ttu-id="3cb23-123">Você verá um toohello semelhante página imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cb23-123">You should see a page similar toohello following image:</span></span>

![Imagem da planilha de consulta Olá para o modo de exibição do hello Hive](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="3cb23-125"><a name="hivequery"></a>Executar uma consulta</span><span class="sxs-lookup"><span data-stu-id="3cb23-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="3cb23-126">toorun uma consulta de hive, use Olá seguindo as etapas da exibição de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="3cb23-126">toorun a hive query, use hello following steps from hello Hive view.</span></span>

1. <span data-ttu-id="3cb23-127">De saudação __consulta__ guia, cole Olá HiveQL instruções a seguir na planilha de saudação:</span><span class="sxs-lookup"><span data-stu-id="3cb23-127">From hello __Query__ tab, paste hello following HiveQL statements into hello worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="3cb23-128">Essas instruções executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cb23-128">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="3cb23-129">`DROP TABLE`-Exclui a tabela hello e arquivo de dados hello, no caso de Olá tabela já existir.</span><span class="sxs-lookup"><span data-stu-id="3cb23-129">`DROP TABLE` - Deletes hello table and hello data file, in case hello table already exists.</span></span>

   * <span data-ttu-id="3cb23-130">`CREATE EXTERNAL TABLE` – cria uma nova tabela "externa" no Hive.</span><span class="sxs-lookup"><span data-stu-id="3cb23-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="3cb23-131">Tabelas externas armazenam a definição da tabela somente Olá no Hive.</span><span class="sxs-lookup"><span data-stu-id="3cb23-131">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="3cb23-132">dados de saudação são deixados no local original hello.</span><span class="sxs-lookup"><span data-stu-id="3cb23-132">hello data is left in hello original location.</span></span>

   * <span data-ttu-id="3cb23-133">`ROW FORMAT`-Como dados de saudação são formatados.</span><span class="sxs-lookup"><span data-stu-id="3cb23-133">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="3cb23-134">Nesse caso, os campos de saudação em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="3cb23-134">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="3cb23-135">`STORED AS TEXTFILE LOCATION`-Onde Olá dados são armazenados e que ela é armazenada como texto.</span><span class="sxs-lookup"><span data-stu-id="3cb23-135">`STORED AS TEXTFILE LOCATION` - Where hello data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="3cb23-136">`SELECT`-Seleciona uma contagem de todas as linhas em que coluna t4 contém valor Olá [Erro].</span><span class="sxs-lookup"><span data-stu-id="3cb23-136">`SELECT` - Selects a count of all rows where column t4 contains hello value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="3cb23-137">Tabelas externas devem ser usadas quando você espera Olá toobe de dados subjacentes atualizado por uma fonte externa.</span><span class="sxs-lookup"><span data-stu-id="3cb23-137">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="3cb23-138">Por exemplo, um processo de carregamento de dados automatizados ou por outra operação MapReduce.</span><span class="sxs-lookup"><span data-stu-id="3cb23-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="3cb23-139">Descartar uma tabela externa *não* excluir dados hello, definição de tabela Olá somente.</span><span class="sxs-lookup"><span data-stu-id="3cb23-139">Dropping an external table does *not* delete hello data, only hello table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3cb23-140">Deixe Olá __banco de dados__ seleção em __padrão__.</span><span class="sxs-lookup"><span data-stu-id="3cb23-140">Leave hello __Database__ selection at __default__.</span></span> <span data-ttu-id="3cb23-141">exemplos de saudação neste documento usam banco de dados de padrão de saudação incluído no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3cb23-141">hello examples in this document use hello default database included with HDInsight.</span></span>

2. <span data-ttu-id="3cb23-142">consulta de saudação toostart, use Olá **Execute** botão abaixo planilha hello.</span><span class="sxs-lookup"><span data-stu-id="3cb23-142">toostart hello query, use hello **Execute** button below hello worksheet.</span></span> <span data-ttu-id="3cb23-143">Ele transforma laranja e hello alterações de texto muito**parar**.</span><span class="sxs-lookup"><span data-stu-id="3cb23-143">It turns orange and hello text changes too**Stop**.</span></span>

3. <span data-ttu-id="3cb23-144">Quando tiver terminado de consulta hello, Olá **resultados** guia exibe os resultados de saudação da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="3cb23-144">Once hello query has finished, hello **Results** tab displays hello results of hello operation.</span></span> <span data-ttu-id="3cb23-145">Olá texto a seguir é o resultado de saudação de consulta de saudação:</span><span class="sxs-lookup"><span data-stu-id="3cb23-145">hello following text is hello result of hello query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="3cb23-146">Olá **Logs** guia pode ser usado tooview informações de log de Olá criadas pelo trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="3cb23-146">hello **Logs** tab can be used tooview hello logging information created by hello job.</span></span>

   > [!TIP]
   > <span data-ttu-id="3cb23-147">Olá **salvar resultados** caixa de diálogo lista suspensa na Olá superior esquerdo da saudação **resultados do processo de consulta** seção permite que você toodownload ou salvar os resultados.</span><span class="sxs-lookup"><span data-stu-id="3cb23-147">hello **Save results** drop-down dialog in hello upper left of hello **Query Process Results** section allows you toodownload or save results.</span></span>

4. <span data-ttu-id="3cb23-148">Selecione Olá quatro primeiras linhas dessa consulta, em seguida, selecione **Execute**.</span><span class="sxs-lookup"><span data-stu-id="3cb23-148">Select hello first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="3cb23-149">Observe que não há nenhum resultado quando Olá trabalho é concluído.</span><span class="sxs-lookup"><span data-stu-id="3cb23-149">Notice that there are no results when hello job completes.</span></span> <span data-ttu-id="3cb23-150">Usando Olá **Execute** botão quando parte de consulta de saudação é selecionado, somente é executado Olá instruções selecionadas.</span><span class="sxs-lookup"><span data-stu-id="3cb23-150">Using hello **Execute** button when part of hello query is selected only runs hello selected statements.</span></span> <span data-ttu-id="3cb23-151">Nesse caso, a seleção de saudação não incluir instrução final de saudação que recupera linhas da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="3cb23-151">In this case, hello selection didn't include hello final statement that retrieves rows from hello table.</span></span> <span data-ttu-id="3cb23-152">Se você selecionar apenas a linha e usar **Execute**, você deve ver os resultados de saudação esperado.</span><span class="sxs-lookup"><span data-stu-id="3cb23-152">If you select just that line and use **Execute**, you should see hello expected results.</span></span>

5. <span data-ttu-id="3cb23-153">tooadd uma planilha, use Olá **nova planilha** botão na parte inferior de saudação do hello **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="3cb23-153">tooadd a worksheet, use hello **New Worksheet** button at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="3cb23-154">Na nova planilha de hello, digite Olá HiveQL instruções a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cb23-154">In hello new worksheet, enter hello following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="3cb23-155">Essas instruções executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cb23-155">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="3cb23-156">**CREATE TABLE IF NOT EXISTS** - cria uma tabela, se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="3cb23-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="3cb23-157">Desde Olá **externo** palavra-chave não for usado, uma tabela interna é criada.</span><span class="sxs-lookup"><span data-stu-id="3cb23-157">Since hello **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="3cb23-158">Uma tabela interna é armazenada no data warehouse do hello Hive e é totalmente gerenciada pelo Hive.</span><span class="sxs-lookup"><span data-stu-id="3cb23-158">An internal table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="3cb23-159">Ao contrário das tabelas externas, descartar uma tabela interna exclui dados subjacentes Olá também.</span><span class="sxs-lookup"><span data-stu-id="3cb23-159">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="3cb23-160">**ARMAZENADOS como ORC** -armazena dados de saudação em formato de linha de otimização Colunar (ORC).</span><span class="sxs-lookup"><span data-stu-id="3cb23-160">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="3cb23-161">Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="3cb23-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="3cb23-162">**INSERT OVERWRITE ... Selecione** -seleciona linhas de saudação **log4jLogs** tabela que contêm `[ERROR]`, e, em seguida, insere Olá dados em Olá **em decorrência** tabela.</span><span class="sxs-lookup"><span data-stu-id="3cb23-162">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain `[ERROR]`, and then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="3cb23-163">Saudação de uso **Execute** botão toorun esta consulta.</span><span class="sxs-lookup"><span data-stu-id="3cb23-163">Use hello **Execute** button toorun this query.</span></span> <span data-ttu-id="3cb23-164">Olá **resultados** guia não contém todas as informações quando Olá consulta retorna zero linhas.</span><span class="sxs-lookup"><span data-stu-id="3cb23-164">hello **Results** tab does not contain any information when hello query returns zero rows.</span></span> <span data-ttu-id="3cb23-165">Olá status deve aparecer como **êxito** após a conclusão da consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="3cb23-165">hello status should show as **SUCCEEDED** once hello query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="3cb23-166">Explicação visual</span><span class="sxs-lookup"><span data-stu-id="3cb23-166">Visual explain</span></span>

<span data-ttu-id="3cb23-167">toodisplay uma visualização de saudação do plano de consulta, selecione Olá **explicam Visual** guia abaixo planilha hello.</span><span class="sxs-lookup"><span data-stu-id="3cb23-167">toodisplay a visualization of hello query plan, select hello **Visual Explain** tab below hello worksheet.</span></span>

<span data-ttu-id="3cb23-168">Olá **explicam Visual** exibição de consulta Olá pode ser útil na compreensão do fluxo de saudação de consultas complexas.</span><span class="sxs-lookup"><span data-stu-id="3cb23-168">hello **Visual Explain** view of hello query can be helpful in understanding hello flow of complex queries.</span></span> <span data-ttu-id="3cb23-169">Você pode exibir um equivalente textual deste modo de exibição usando Olá **explicar** botão Olá Editor de consultas.</span><span class="sxs-lookup"><span data-stu-id="3cb23-169">You can view a textual equivalent of this view by using hello **Explain** button in hello Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="3cb23-170">Interface de usuário do Tez</span><span class="sxs-lookup"><span data-stu-id="3cb23-170">Tez UI</span></span>

<span data-ttu-id="3cb23-171">toodisplay hello Tez UI para consulta hello, selecione Olá **Tez** guia abaixo planilha hello.</span><span class="sxs-lookup"><span data-stu-id="3cb23-171">toodisplay hello Tez UI for hello query, select hello **Tez** tab below hello worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3cb23-172">Tez é tooresolve não usado em todas as consultas.</span><span class="sxs-lookup"><span data-stu-id="3cb23-172">Tez is not used tooresolve all queries.</span></span> <span data-ttu-id="3cb23-173">Muitas consultas de Hive podem ser resolvidas sem usar o Tez.</span><span class="sxs-lookup"><span data-stu-id="3cb23-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="3cb23-174">Se tiver sido Tez consulta tooresolve usado Olá Olá gráfico acíclico direcionado (DAG) é exibido.</span><span class="sxs-lookup"><span data-stu-id="3cb23-174">If Tez was used tooresolve hello query, hello Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="3cb23-175">Se você quiser Olá tooview DAG para consultas que você executou no hello anterior ou depura Olá Tez processo, use Olá [Tez exibição](hdinsight-debug-ambari-tez-view.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="3cb23-175">If you want tooview hello DAG for queries you've ran in hello past, or debug hello Tez process, use hello [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="3cb23-176">Exibir histórico de trabalho</span><span class="sxs-lookup"><span data-stu-id="3cb23-176">View job history</span></span>

<span data-ttu-id="3cb23-177">Olá __trabalhos__ guia exibe um histórico das consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="3cb23-177">hello __Jobs__ tab displays a history of Hive queries.</span></span>

![Imagem do histórico do trabalho Olá](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="3cb23-179">Tabelas de banco de dados</span><span class="sxs-lookup"><span data-stu-id="3cb23-179">Database tables</span></span>

<span data-ttu-id="3cb23-180">Você pode usar o hello __tabelas__ guia toowork com as tabelas em um banco de dados de Hive.</span><span class="sxs-lookup"><span data-stu-id="3cb23-180">You can use hello __Tables__ tab toowork with tables within a Hive database.</span></span>

![Imagem da guia de tabelas Olá](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="3cb23-182">Consultas salvas</span><span class="sxs-lookup"><span data-stu-id="3cb23-182">Saved queries</span></span>

<span data-ttu-id="3cb23-183">Guia de consulta Olá, opcionalmente, é possível salvar consultas.</span><span class="sxs-lookup"><span data-stu-id="3cb23-183">From hello Query tab, you can optionally save queries.</span></span> <span data-ttu-id="3cb23-184">Uma vez salvo, você pode reutilizar a consulta de saudação do hello __consultas salvas__ guia.</span><span class="sxs-lookup"><span data-stu-id="3cb23-184">Once saved, you can reuse hello query from hello __Saved Queries__ tab.</span></span>

![Imagem da guia Consultas Salvas](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="3cb23-186">Funções definidas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="3cb23-186">User-defined functions</span></span>

<span data-ttu-id="3cb23-187">O Hive também pode ser estendido por meio de UDFs (funções definidas pelo usuário).</span><span class="sxs-lookup"><span data-stu-id="3cb23-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="3cb23-188">Um UDF permite funcionalidade tooimplement ou lógica que não é modelada facilmente no estilo.</span><span class="sxs-lookup"><span data-stu-id="3cb23-188">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="3cb23-189">Olá guia UDF na parte superior de saudação do hello Hive exibição permite toodeclare e salvar um conjunto de UDFs.</span><span class="sxs-lookup"><span data-stu-id="3cb23-189">hello UDF tab at hello top of hello Hive View allows you toodeclare and save a set of UDFs.</span></span> <span data-ttu-id="3cb23-190">Esses UDFs podem ser usados com hello **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="3cb23-190">These UDFs can be used with hello **Query Editor**.</span></span>

![Imagem da guia UDF](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="3cb23-192">Depois que você adicionou um toohello UDF exibição Hive, um **inserir udfs** botão é exibido na parte inferior de saudação do hello **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="3cb23-192">Once you have added a UDF toohello Hive View, an **Insert udfs** button appears at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="3cb23-193">Selecionar essa entrada exibe uma lista de lista suspensa de Olá UDFs definidos no hello exibição Hive.</span><span class="sxs-lookup"><span data-stu-id="3cb23-193">Selecting this entry displays a drop-down list of hello UDFs defined in hello Hive View.</span></span> <span data-ttu-id="3cb23-194">Selecionar um UDF adiciona HiveQL instruções tooyour consulta tooenable Olá UDF.</span><span class="sxs-lookup"><span data-stu-id="3cb23-194">Selecting a UDF adds HiveQL statements tooyour query tooenable hello UDF.</span></span>

<span data-ttu-id="3cb23-195">Por exemplo, se você tiver definido um UDF com hello propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cb23-195">For example, if you have defined a UDF with hello following properties:</span></span>

* <span data-ttu-id="3cb23-196">Nome de recurso: myudfs</span><span class="sxs-lookup"><span data-stu-id="3cb23-196">Resource name: myudfs</span></span>

* <span data-ttu-id="3cb23-197">Caminho do recurso: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="3cb23-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="3cb23-198">Nome da UDF: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="3cb23-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="3cb23-199">Nome de classe da  UDF: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="3cb23-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="3cb23-200">Usando Olá **inserir udfs** botão exibe uma entrada de chamada **myudfs**, com outra lista suspensa para cada UDF é definido para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3cb23-200">Using hello **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="3cb23-201">Nesse caso, **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="3cb23-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="3cb23-202">Selecionar essa entrada adiciona Olá toohello início da consulta Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cb23-202">Selecting this entry adds hello following toohello beginning of hello query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="3cb23-203">Em seguida, você pode usar o hello UDF em sua consulta.</span><span class="sxs-lookup"><span data-stu-id="3cb23-203">You can then use hello UDF in your query.</span></span> <span data-ttu-id="3cb23-204">Por exemplo: `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="3cb23-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="3cb23-205">Para obter mais informações sobre como usar UDFs com Hive no HDInsight, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cb23-205">For more information on using UDFs with Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="3cb23-206">Usando o Python com o Hive e com o Pig no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3cb23-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="3cb23-207">Como tooadd uma tooHDInsight UDF Hive personalizada</span><span class="sxs-lookup"><span data-stu-id="3cb23-207">How tooadd a custom Hive UDF tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="3cb23-208">Configurações do Hive</span><span class="sxs-lookup"><span data-stu-id="3cb23-208">Hive settings</span></span>

<span data-ttu-id="3cb23-209">As configurações podem ser usada toochange várias configurações de Hive.</span><span class="sxs-lookup"><span data-stu-id="3cb23-209">Settings can be used toochange various Hive settings.</span></span> <span data-ttu-id="3cb23-210">Por exemplo, alterando o mecanismo de execução Olá para o Hive de tooMapReduce Tez (padrão de saudação).</span><span class="sxs-lookup"><span data-stu-id="3cb23-210">For example, changing hello execution engine for Hive from Tez (hello default) tooMapReduce.</span></span>

## <span data-ttu-id="3cb23-211"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3cb23-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="3cb23-212">Para informações gerais sobre o Hive no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3cb23-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="3cb23-213">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3cb23-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="3cb23-214">Para obter informações sobre outras maneiras que você pode trabalhar com Hadoop no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3cb23-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="3cb23-215">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3cb23-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="3cb23-216">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3cb23-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
