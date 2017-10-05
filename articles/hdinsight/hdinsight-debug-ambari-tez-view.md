---
title: "Usar a exibição do Ambari Tez com o HDInsight – Azure | Microsoft Docs"
description: "Saiba como usar o modo de exibição do Ambari Tez para depurar trabalhos do Tez no HDInsight."
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
ms.openlocfilehash: 65d89309b9eea8544b85d16687baa90d49688d77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-ambari-views-to-debug-tez-jobs-on-hdinsight"></a><span data-ttu-id="3b6e9-103">Usar os modos de exibição do Ambari para depurar trabalhos do Tez no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3b6e9-103">Use Ambari Views to debug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="3b6e9-104">A interface do usuário da Web do Ambari para HDInsight contém uma exibição do Tez que pode ser usada para entender e depurar trabalhos que usam o Tez.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-104">The Ambari Web UI for HDInsight contains a Tez view that can be used to understand and debug jobs that use Tez.</span></span> <span data-ttu-id="3b6e9-105">O modo de exibição do Tez permite que você visualize o trabalho como um gráfico de itens conectados, detalhe cada item e recupere estatísticas e informações de log.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-105">The Tez view allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b6e9-106">As etapas deste documento exigem um cluster HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="3b6e9-107">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3b6e9-108">Para obter mais informações, consulte [Controle de versão do componente do HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3b6e9-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b6e9-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3b6e9-109">Prerequisites</span></span>

* <span data-ttu-id="3b6e9-110">Criar um cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="3b6e9-111">Para ver as etapas para criar um cluster, consulte [Introdução ao HDInsight baseado no Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3b6e9-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="3b6e9-112">Um navegador da Web moderno, com suporte a HTML5.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="3b6e9-113">Noções básicas sobre o Tez</span><span class="sxs-lookup"><span data-stu-id="3b6e9-113">Understanding Tez</span></span>

<span data-ttu-id="3b6e9-114">Tez é uma estrutura extensível para processamento de dados no Hadoop que fornece maior velocidade de processamento do que o MapReduce tradicional.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="3b6e9-115">Para clusters HDInsight baseados em Linux, é o mecanismo padrão para Hive.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-115">For Linux-based HDInsight clusters, it is the default engine for Hive.</span></span>

<span data-ttu-id="3b6e9-116">O Tez cria um DAG (gráfico acíclico dirigido) que descreve a ordem das ações necessárias ao trabalho.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-116">Tez creates a Directed Acyclic Graph (DAG) that describes the order of actions required by jobs.</span></span> <span data-ttu-id="3b6e9-117">As ações individuais são chamadas de vértices e executam uma parte do trabalho geral.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-117">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="3b6e9-118">A execução real do trabalho descrita por um vértice é chamada de tarefa e pode ser distribuída em vários nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-118">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-view"></a><span data-ttu-id="3b6e9-119">Noções básicas do layout da interface de usuário do Tez</span><span class="sxs-lookup"><span data-stu-id="3b6e9-119">Understanding the Tez view</span></span>

<span data-ttu-id="3b6e9-120">A exibição do Tez fornece informações históricas e sobre os processos em execução.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-120">The Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="3b6e9-121">Essas informações mostram como um trabalho é distribuído entre os clusters.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="3b6e9-122">Ele também exibe contadores usados por tarefas e vértices, bem como informações de erro relacionadas ao trabalho.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-122">It also displays counters used by tasks and vertices, and error information related to the job.</span></span> <span data-ttu-id="3b6e9-123">Ela pode oferecer informações úteis nos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="3b6e9-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="3b6e9-124">Monitoramento de processos de longa execução, exibindo o andamento de tarefas map e reduce.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="3b6e9-125">Análise de dados históricos para processos com ou sem êxito, a fim de saber como o processamento pode ser aprimorado ou qual foi o motivo da falha.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="3b6e9-126">Gerar um DAG</span><span class="sxs-lookup"><span data-stu-id="3b6e9-126">Generate a DAG</span></span>

<span data-ttu-id="3b6e9-127">A exibição do Tez só conterá dados se um trabalho que usa o mecanismo Tez estiver sendo executado ou se já foi executado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-127">The Tez view only contains data if a job that uses the Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="3b6e9-128">Consultas de Hive simples podem ser resolvidas sem usar o Tez.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="3b6e9-129">Consultas mais complexas que executam filtragem, agrupamento, ordenação, associações, etc.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="3b6e9-130">usam o mecanismo Tez.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-130">use the Tez engine.</span></span>

<span data-ttu-id="3b6e9-131">Use as etapas a seguir para executar uma consulta do Hive que usa o Tez:</span><span class="sxs-lookup"><span data-stu-id="3b6e9-131">Use the following steps to run a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="3b6e9-132">Abra um navegador da Web, navegue para https://CLUSTERNAME.azurehdinsight.net, onde **CLUSTERNAME** é o nome do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-132">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="3b6e9-133">No menu na parte superior da página, escolha o ícone **Exibições**.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-133">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="3b6e9-134">Esse ícone é semelhante a uma série de quadrados.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="3b6e9-135">No menu suspenso que aparece, escolha **Exibição do Hive**.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-135">In the dropdown that appears, select **Hive view**.</span></span>

    ![Como selecionar o modo de exibição do Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="3b6e9-137">Quando a exibição do Hive for carregada, cole a seguinte consulta no Editor de Consulta e clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-137">When the Hive view loads, paste the following query into the Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="3b6e9-138">Após a conclusão do trabalho, você deverá ver a saída exibida na seção **Resultados do Processo de Consulta**.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-138">Once the job has completed, you should see the output displayed in the **Query Process Results** section.</span></span> <span data-ttu-id="3b6e9-139">Os resultados devem ser semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="3b6e9-139">The results should be similar to the following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="3b6e9-140">Selecione a guia **Log**.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-140">Select the **Log** tab.</span></span> <span data-ttu-id="3b6e9-141">Você verá informações semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="3b6e9-141">You see information similar to the following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="3b6e9-142">Salve o valor de **ID do aplicativo**, pois ele será usado na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-142">Save the **App id** value, as this value is used in the next section.</span></span>

## <a name="use-the-tez-view"></a><span data-ttu-id="3b6e9-143">Usar o modo de exibição do Tez</span><span class="sxs-lookup"><span data-stu-id="3b6e9-143">Use the Tez View</span></span>

1. <span data-ttu-id="3b6e9-144">No menu na parte superior da página, escolha o ícone **Exibições**.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-144">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="3b6e9-145">Na lista suspensa que aparece, escolha **Exibição do Tez**.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-145">In the dropdown that appears, select **Tez view**.</span></span>

    ![Como selecionar o modo de exibição do Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="3b6e9-147">Quando a exibição do Tez for carregada, você verá uma lista de consultas do Hive que estão em execução no momento ou que foram executadas no cluster.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-147">When the Tez view loads, you see a list of hive queries that are currently running, or have been ran on the cluster.</span></span>

    ![Todos os DAGS](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="3b6e9-149">Se você tiver apenas uma entrada, ela representará a consulta que você executou na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-149">If you have only one entry, it is for the query that you ran in the previous section.</span></span> <span data-ttu-id="3b6e9-150">Se tiver várias entradas, você poderá pesquisar usando os campos na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-150">If you have multiple entries, you can search by using the fields at the top of the page.</span></span>

4. <span data-ttu-id="3b6e9-151">Selecione a **ID da consulta** para uma consulta do Hive.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-151">Select the **Query ID** for a Hive query.</span></span> <span data-ttu-id="3b6e9-152">As informações sobre a consulta são exibidas.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-152">Information about the query is displayed.</span></span>

    ![Detalhes do DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="3b6e9-154">As guias desta página permitem que você exiba as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="3b6e9-154">The tabs on this page allow you to view the following information:</span></span>

    * <span data-ttu-id="3b6e9-155">**Detalhes da consulta**: os detalhes sobre a consulta do Hive.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-155">**Query Details**: Details about the Hive query.</span></span>
    * <span data-ttu-id="3b6e9-156">**Linha do tempo**: as informações sobre quanto tempo durou cada estágio de processamento.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-156">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="3b6e9-157">**Configurações**: a configuração usada nesta consulta.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-157">**Configurations**: The configuration used for this query.</span></span>

    <span data-ttu-id="3b6e9-158">Em __Detalhes da consulta__, você pode usar os links para encontrar mais informações sobre o __Aplicativo__ ou o __DAG__ para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-158">From __Query Details__ you can use the links to find information about the __Application__ or the __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="3b6e9-159">O link __Aplicativo__ exibe informações sobre o aplicativo YARN para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-159">The __Application__ link displays information about the YARN application for this query.</span></span> <span data-ttu-id="3b6e9-160">Aqui você pode acessar os logs de aplicativo YARN.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-160">From here you can access the YARN application logs.</span></span>
    * <span data-ttu-id="3b6e9-161">O link __DAG__ exibe informações sobre o gráfico acíclico dirigido para esta consulta.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-161">The __DAG__ link displays information about the directed acyclic graph for this query.</span></span> <span data-ttu-id="3b6e9-162">Aqui você pode exibir uma representação gráfica do DAG.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-162">From here you can view a graphical representation of the DAG.</span></span> <span data-ttu-id="3b6e9-163">Você também pode encontrar informações sobre os vértices no DAG.</span><span class="sxs-lookup"><span data-stu-id="3b6e9-163">You can also find information on the vertices within the DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b6e9-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b6e9-164">Next Steps</span></span>

<span data-ttu-id="3b6e9-165">Agora que você aprendeu a usar o modo de exibição do Tez, saiba mais sobre [Como usar o Hive no HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="3b6e9-165">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="3b6e9-166">Para obter informações técnicas mais detalhadas sobre o Tez, confira a [página sobre o Tez em Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="3b6e9-166">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="3b6e9-167">Para saber mais sobre como usar o Ambari com o HDInsight, confira [Gerenciar clusters HDInsight usando a interface de usuário da Web do Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="3b6e9-167">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
