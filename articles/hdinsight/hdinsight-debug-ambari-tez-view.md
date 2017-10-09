---
title: "aaaUse Ambari Tez exibição de HDInsight - Azure | Microsoft Docs"
description: "Saiba como Olá toouse Ambari Tez exibir toodebug Tez trabalhos no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a><span data-ttu-id="3f83d-103">Usar exibições do Ambari toodebug Tez trabalhos no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3f83d-103">Use Ambari Views toodebug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="3f83d-104">Olá Ambari Web da interface do usuário para HDInsight contém uma exibição Tez que pode ser usado toounderstand e depurar os trabalhos que usam Tez.</span><span class="sxs-lookup"><span data-stu-id="3f83d-104">hello Ambari Web UI for HDInsight contains a Tez view that can be used toounderstand and debug jobs that use Tez.</span></span> <span data-ttu-id="3f83d-105">Olá Tez exibição permite trabalho de saudação toovisualize como um gráfico de itens conectados, detalhar cada item e recuperar estatísticas e informações de registro em log.</span><span class="sxs-lookup"><span data-stu-id="3f83d-105">hello Tez view allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f83d-106">etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux.</span><span class="sxs-lookup"><span data-stu-id="3f83d-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="3f83d-107">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3f83d-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3f83d-108">Para obter mais informações, consulte [Controle de versão do componente do HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3f83d-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f83d-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3f83d-109">Prerequisites</span></span>

* <span data-ttu-id="3f83d-110">Criar um cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="3f83d-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="3f83d-111">Para ver as etapas para criar um cluster, consulte [Introdução ao HDInsight baseado no Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3f83d-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="3f83d-112">Um navegador da Web moderno, com suporte a HTML5.</span><span class="sxs-lookup"><span data-stu-id="3f83d-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="3f83d-113">Noções básicas sobre o Tez</span><span class="sxs-lookup"><span data-stu-id="3f83d-113">Understanding Tez</span></span>

<span data-ttu-id="3f83d-114">Tez é uma estrutura extensível para processamento de dados no Hadoop que fornece maior velocidade de processamento do que o MapReduce tradicional.</span><span class="sxs-lookup"><span data-stu-id="3f83d-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="3f83d-115">Para clusters HDInsight baseados em Linux, é saudação padrão mecanismo para o Hive.</span><span class="sxs-lookup"><span data-stu-id="3f83d-115">For Linux-based HDInsight clusters, it is hello default engine for Hive.</span></span>

<span data-ttu-id="3f83d-116">Tez cria um direcionado acíclico Graph (DAG) que descreve a ordem de saudação das ações necessárias para trabalhos.</span><span class="sxs-lookup"><span data-stu-id="3f83d-116">Tez creates a Directed Acyclic Graph (DAG) that describes hello order of actions required by jobs.</span></span> <span data-ttu-id="3f83d-117">Ações individuais são chamadas de vértices e executar um pedaço de saudação trabalho geral.</span><span class="sxs-lookup"><span data-stu-id="3f83d-117">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="3f83d-118">a execução real Olá Olá trabalho descrita por um vértice é chamada de uma tarefa e pode ser distribuída em vários nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f83d-118">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-view"></a><span data-ttu-id="3f83d-119">Saudação de compreensão Tez exibição</span><span class="sxs-lookup"><span data-stu-id="3f83d-119">Understanding hello Tez view</span></span>

<span data-ttu-id="3f83d-120">Olá Tez exibição fornece informações de histórico e informações sobre processos em execução.</span><span class="sxs-lookup"><span data-stu-id="3f83d-120">hello Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="3f83d-121">Essas informações mostram como um trabalho é distribuído entre os clusters.</span><span class="sxs-lookup"><span data-stu-id="3f83d-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="3f83d-122">Ele também exibe os contadores usados por tarefas e vértices e informações de erro relacionadas toohello trabalho.</span><span class="sxs-lookup"><span data-stu-id="3f83d-122">It also displays counters used by tasks and vertices, and error information related toohello job.</span></span> <span data-ttu-id="3f83d-123">Ele pode oferecer informações úteis no hello os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="3f83d-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="3f83d-124">Monitorando processos de longa execução, exibindo Olá progresso de mapa e reduzir as tarefas.</span><span class="sxs-lookup"><span data-stu-id="3f83d-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="3f83d-125">Analisar dados históricos para toolearn processos com êxito ou falha, como o processamento pode ser aprimorado ou razão da falha.</span><span class="sxs-lookup"><span data-stu-id="3f83d-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="3f83d-126">Gerar um DAG</span><span class="sxs-lookup"><span data-stu-id="3f83d-126">Generate a DAG</span></span>

<span data-ttu-id="3f83d-127">Olá Tez exibição contém dados somente se um trabalho que usa Olá Tez mecanismo está atualmente em execução ou tiver sido executado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3f83d-127">hello Tez view only contains data if a job that uses hello Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="3f83d-128">Consultas de Hive simples podem ser resolvidas sem usar o Tez.</span><span class="sxs-lookup"><span data-stu-id="3f83d-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="3f83d-129">Consultas mais complexas que executam filtragem, agrupamento, ordenação, associações, etc.</span><span class="sxs-lookup"><span data-stu-id="3f83d-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="3f83d-130">Use o mecanismo de Tez hello.</span><span class="sxs-lookup"><span data-stu-id="3f83d-130">use hello Tez engine.</span></span>

<span data-ttu-id="3f83d-131">Use Olá etapas toorun uma consulta de Hive que usa Tez a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f83d-131">Use hello following steps toorun a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="3f83d-132">Em um navegador da web, navegar toohttps://CLUSTERNAME.azurehdinsight.net, onde **CLUSTERNAME** é o nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3f83d-132">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="3f83d-133">No menu de saudação na parte superior de saudação da página hello, selecione Olá **exibições** ícone.</span><span class="sxs-lookup"><span data-stu-id="3f83d-133">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="3f83d-134">Esse ícone é semelhante a uma série de quadrados.</span><span class="sxs-lookup"><span data-stu-id="3f83d-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="3f83d-135">No menu suspenso de saudação que aparece, selecione **Hive exibição**.</span><span class="sxs-lookup"><span data-stu-id="3f83d-135">In hello dropdown that appears, select **Hive view**.</span></span>

    ![Como selecionar o modo de exibição do Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="3f83d-137">Quando Olá Hive exibição carrega, colar Olá seguinte consulta em Olá Editor de consultas e, em seguida, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="3f83d-137">When hello Hive view loads, paste hello following query into hello Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="3f83d-138">Depois de concluído o trabalho de saudação, você verá a saída de hello exibida no hello **resultados do processo de consulta** seção.</span><span class="sxs-lookup"><span data-stu-id="3f83d-138">Once hello job has completed, you should see hello output displayed in hello **Query Process Results** section.</span></span> <span data-ttu-id="3f83d-139">resultados de saudação devem ser semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f83d-139">hello results should be similar toohello following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="3f83d-140">Selecione Olá **Log** guia. Você verá informações toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f83d-140">Select hello **Log** tab. You see information similar toohello following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="3f83d-141">Salvar Olá **id do aplicativo** de valor, como esse valor é usado na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="3f83d-141">Save hello **App id** value, as this value is used in hello next section.</span></span>

## <a name="use-hello-tez-view"></a><span data-ttu-id="3f83d-142">Use Olá Tez exibição</span><span class="sxs-lookup"><span data-stu-id="3f83d-142">Use hello Tez View</span></span>

1. <span data-ttu-id="3f83d-143">No menu de saudação na parte superior de saudação da página hello, selecione Olá **exibições** ícone.</span><span class="sxs-lookup"><span data-stu-id="3f83d-143">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="3f83d-144">No menu suspenso de saudação que aparece, selecione **Tez exibição**.</span><span class="sxs-lookup"><span data-stu-id="3f83d-144">In hello dropdown that appears, select **Tez view**.</span></span>

    ![Como selecionar o modo de exibição do Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="3f83d-146">Quando Olá Tez exibição carregado, você verá uma lista de consultas de hive que estão sendo executados, ou ter sido executado no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f83d-146">When hello Tez view loads, you see a list of hive queries that are currently running, or have been ran on hello cluster.</span></span>

    ![Todos os DAGS](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="3f83d-148">Se você tiver apenas uma entrada, é para consulta de saudação que você executou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="3f83d-148">If you have only one entry, it is for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="3f83d-149">Se você tiver várias entradas, você pode pesquisar usando campos de saudação na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f83d-149">If you have multiple entries, you can search by using hello fields at hello top of hello page.</span></span>

4. <span data-ttu-id="3f83d-150">Selecione Olá **ID da consulta** para uma consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="3f83d-150">Select hello **Query ID** for a Hive query.</span></span> <span data-ttu-id="3f83d-151">Informações sobre consulta Olá são exibidas.</span><span class="sxs-lookup"><span data-stu-id="3f83d-151">Information about hello query is displayed.</span></span>

    ![Detalhes do DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="3f83d-153">guias de saudação nessa página permitem que você Olá tooview informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f83d-153">hello tabs on this page allow you tooview hello following information:</span></span>

    * <span data-ttu-id="3f83d-154">**Detalhes da consulta**: detalhes sobre a consulta de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="3f83d-154">**Query Details**: Details about hello Hive query.</span></span>
    * <span data-ttu-id="3f83d-155">**Linha do tempo**: as informações sobre quanto tempo durou cada estágio de processamento.</span><span class="sxs-lookup"><span data-stu-id="3f83d-155">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="3f83d-156">**Configurações**: configuração de saudação usada para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="3f83d-156">**Configurations**: hello configuration used for this query.</span></span>

    <span data-ttu-id="3f83d-157">De __detalhes da consulta__ você pode usar Olá links toofind informações sobre Olá __aplicativo__ ou hello __DAG__ para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="3f83d-157">From __Query Details__ you can use hello links toofind information about hello __Application__ or hello __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="3f83d-158">Olá __aplicativo__ link exibe informações sobre Olá aplicativo YARN para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="3f83d-158">hello __Application__ link displays information about hello YARN application for this query.</span></span> <span data-ttu-id="3f83d-159">Aqui você pode acessar logs de aplicativo hello YARN.</span><span class="sxs-lookup"><span data-stu-id="3f83d-159">From here you can access hello YARN application logs.</span></span>
    * <span data-ttu-id="3f83d-160">Olá __DAG__ link exibe informações sobre o gráfico acíclico direcionado de saudação para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="3f83d-160">hello __DAG__ link displays information about hello directed acyclic graph for this query.</span></span> <span data-ttu-id="3f83d-161">Aqui você pode exibir uma representação gráfica da saudação DAG.</span><span class="sxs-lookup"><span data-stu-id="3f83d-161">From here you can view a graphical representation of hello DAG.</span></span> <span data-ttu-id="3f83d-162">Você também pode localizar informações sobre vértices hello dentro Olá DAG.</span><span class="sxs-lookup"><span data-stu-id="3f83d-162">You can also find information on hello vertices within hello DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f83d-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f83d-163">Next Steps</span></span>

<span data-ttu-id="3f83d-164">Agora que você aprendeu como exibir hello toouse Tez, saiba mais sobre [usando Hive no HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="3f83d-164">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="3f83d-165">Para obter mais informações técnicas sobre Tez, consulte Olá [Tez página no Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="3f83d-165">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="3f83d-166">Para obter mais informações sobre como usar o Ambari com HDInsight, consulte [gerenciar clusters HDInsight usando Olá Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="3f83d-166">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
