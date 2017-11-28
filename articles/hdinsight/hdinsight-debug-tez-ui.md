---
title: "Usar a interface do usuário do Tez com o HDInsight baseado em Windows – Azure | Microsoft Docs"
description: "Saiba como usar a interface de usuário do Tez para depurar trabalhos do Tez no HDInsight baseado no Windows."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 3889fa1c3523eb0330cbe3b7640fd8590a5ceadf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="90102-103">Usar a interface de usuário do Tez para depurar trabalhos no HDInsight baseado no Windows</span><span class="sxs-lookup"><span data-stu-id="90102-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="90102-104">A interface de usuário do Tez é uma página da Web que pode ser usada para entender e depurar trabalhos que usam o Tez como o mecanismo de execução em clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="90102-104">The Tez UI is a web page that can be used to understand and debug jobs that use Tez as the execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="90102-105">A interface de usuário do Tez permite que você visualize o trabalho como um gráfico de itens conectados, detalhe cada item e recupere estatísticas e informações de registro.</span><span class="sxs-lookup"><span data-stu-id="90102-105">The Tez UI allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90102-106">As etapas deste documento exigem um cluster HDInsight que usa Windows.</span><span class="sxs-lookup"><span data-stu-id="90102-106">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="90102-107">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="90102-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="90102-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="90102-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90102-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="90102-109">Prerequisites</span></span>
* <span data-ttu-id="90102-110">Um cluster HDInsight baseado no Windows.</span><span class="sxs-lookup"><span data-stu-id="90102-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="90102-111">Para obter as etapas de criação de um novo cluster, confira [Introdução ao uso do HDInsight baseado no Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="90102-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="90102-112">A interface de usuário do Tez está disponível apenas em clusters HDInsight baseados no Windows criados depois de 8 de fevereiro de 2016.</span><span class="sxs-lookup"><span data-stu-id="90102-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="90102-113">Um cliente da Área de Trabalho Remota baseado no Windows.</span><span class="sxs-lookup"><span data-stu-id="90102-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="90102-114">Noções básicas sobre o Tez</span><span class="sxs-lookup"><span data-stu-id="90102-114">Understanding Tez</span></span>
<span data-ttu-id="90102-115">Tez é uma estrutura extensível para processamento de dados no Hadoop que fornece maior velocidade de processamento do que o MapReduce tradicional.</span><span class="sxs-lookup"><span data-stu-id="90102-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="90102-116">Para os clusters HDInsight baseados no Windows, é um mecanismo opcional que você pode habilitar para o Hive usando o comando a seguir como parte de sua consulta do Hive:</span><span class="sxs-lookup"><span data-stu-id="90102-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using the following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="90102-117">Quando o trabalho é enviado ao Tez, ele cria um DAG (Gráfico Acíclico Dirigido) que descreve a ordem de execução das ações exigidas pelo trabalho.</span><span class="sxs-lookup"><span data-stu-id="90102-117">When work is submitted to Tez, it creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span></span> <span data-ttu-id="90102-118">As ações individuais são chamadas de vértices e executam uma parte do trabalho geral.</span><span class="sxs-lookup"><span data-stu-id="90102-118">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="90102-119">A execução real do trabalho descrita por um vértice é chamada de tarefa e pode ser distribuída em vários nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="90102-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-ui"></a><span data-ttu-id="90102-120">Noções básicas sobre a interface de usuário do Tez</span><span class="sxs-lookup"><span data-stu-id="90102-120">Understanding the Tez UI</span></span>
<span data-ttu-id="90102-121">A interface de usuário do Tez é uma página da Web que fornece informações sobre processos em execução ou que foram executados anteriormente com o Tez.</span><span class="sxs-lookup"><span data-stu-id="90102-121">The Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="90102-122">Ela permite exibir o DAG gerado pelo Tez, como ele é distribuído entre os clusters, contadores, como a memória usada por tarefas e vértices, além de informações de erro.</span><span class="sxs-lookup"><span data-stu-id="90102-122">It allows you to view the DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="90102-123">Ela pode oferecer informações úteis nos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="90102-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="90102-124">Monitoramento de processos de longa execução, exibindo o andamento de tarefas map e reduce.</span><span class="sxs-lookup"><span data-stu-id="90102-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="90102-125">Análise de dados históricos para processos com ou sem êxito, a fim de saber como o processamento pode ser aprimorado ou qual foi o motivo da falha.</span><span class="sxs-lookup"><span data-stu-id="90102-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="90102-126">Gerar um DAG</span><span class="sxs-lookup"><span data-stu-id="90102-126">Generate a DAG</span></span>
<span data-ttu-id="90102-127">A interface de usuário do Tez conterá apenas dados se um trabalho que usa o mecanismo Tez estiver sendo executado no momento ou se tiver sido executado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="90102-127">The Tez UI will only contain data if a job that uses the Tez engine is currently running, or has been ran in the past.</span></span> <span data-ttu-id="90102-128">Normalmente, as consultas simples do Hive podem ser resolvidas sem usar o Tez. Porém, as consultas mais complexas que realizam filtragem, agrupamento, ordenação, associações etc. normalmente exigirão o Tez.</span><span class="sxs-lookup"><span data-stu-id="90102-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="90102-129">Use as etapas a seguir para executar uma consulta do Hive usando o Tez.</span><span class="sxs-lookup"><span data-stu-id="90102-129">Use the following steps to run a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="90102-130">Abra um navegador da Web, navegue para https://CLUSTERNAME.azurehdinsight.net, em que **CLUSTERNAME** é o nome do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="90102-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="90102-131">No menu, na parte superior da página, escolha o **Editor do Hive**.</span><span class="sxs-lookup"><span data-stu-id="90102-131">From the menu at the top of the page, select the **Hive Editor**.</span></span> <span data-ttu-id="90102-132">Essa ação exibirá uma página com o exemplo de consulta a seguir.</span><span class="sxs-lookup"><span data-stu-id="90102-132">This will display a page with the following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="90102-133">Apague o exemplo de consulta e substitua-o pelo que se segue.</span><span class="sxs-lookup"><span data-stu-id="90102-133">Erase the example query and replace it with the following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="90102-134">Selecione o botão **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="90102-134">Select the **Submit** button.</span></span> <span data-ttu-id="90102-135">A seção **Sessão de Trabalho**, na parte inferior da página, exibirá o status da consulta.</span><span class="sxs-lookup"><span data-stu-id="90102-135">The **Job Session** section at the bottom of the page will display the status of the query.</span></span> <span data-ttu-id="90102-136">Depois que o status mudar para **Concluído**, selecione o link **Exibir Detalhes** para exibir os resultados.</span><span class="sxs-lookup"><span data-stu-id="90102-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span></span> <span data-ttu-id="90102-137">A **Saída do Trabalho** deve ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="90102-137">The **Job Output** should be similar to the following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a><span data-ttu-id="90102-138">Usar a interface de usuário do Tez</span><span class="sxs-lookup"><span data-stu-id="90102-138">Use the Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="90102-139">A interface de usuário do Tez está disponível na área de trabalho dos nós de cabeçalho do cluster, de modo que é preciso usar a Área de Trabalho Remota para se conectar a esses nós de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="90102-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span></span>
>
>

1. <span data-ttu-id="90102-140">No [Portal do Azure](https://portal.azure.com), escolha o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="90102-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="90102-141">Na parte superior da folha HDInsight, selecione o ícone **Área de Trabalho Remota**.</span><span class="sxs-lookup"><span data-stu-id="90102-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span></span> <span data-ttu-id="90102-142">Isso exibirá a folha da área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="90102-142">This will display the remote desktop blade</span></span>

    ![Ícone da área de trabalho remota](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="90102-144">Na folha Área de Trabalho Remota, selecione **Conectar** para se conectar ao nó de cabeçalho do cluster.</span><span class="sxs-lookup"><span data-stu-id="90102-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span></span> <span data-ttu-id="90102-145">Quando solicitado, use o nome do usuário e a senha da Área de Trabalho Remota do cluster para autenticar a conexão.</span><span class="sxs-lookup"><span data-stu-id="90102-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span></span>

    ![Ícone de conexão da área de trabalho remota](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="90102-147">Se você não tiver habilitado a conectividade da Área de Trabalho Remota, forneça um nome de usuário, uma senha e a data de vencimento, então selecione **Habilitar** para habilitar a Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="90102-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span></span> <span data-ttu-id="90102-148">Depois da habilitação, use as etapas anteriores para se conectar.</span><span class="sxs-lookup"><span data-stu-id="90102-148">Once it has been enabled, use the previous steps to connect.</span></span>
   >
   >
3. <span data-ttu-id="90102-149">Depois de conectado, abra o Internet Explorer na área de trabalho remota, selecione o ícone de engrenagem no canto superior direito do navegador e selecione **Configurações do Modo de Exibição de Compatibilidade**.</span><span class="sxs-lookup"><span data-stu-id="90102-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="90102-150">Na parte inferior de **Configurações do Modo de Exibição de Compatibilidade**, desmarque a caixa de seleção de **Exibir sites da intranet no Modo de Exibição de Compatibilidade** e **Usar listas de compatibilidade da Microsoft** e selecione **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="90102-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="90102-151">No Internet Explorer, navegue até http://headnodehost:8188/tezui/#/.</span><span class="sxs-lookup"><span data-stu-id="90102-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="90102-152">Isso exibirá a interface de usuário do Tez</span><span class="sxs-lookup"><span data-stu-id="90102-152">This will display the Tez UI</span></span>

    ![Interface de usuário do Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="90102-154">Quando a interface de usuário do Tez for carregada, você verá uma lista de DAGs atualmente em execução ou que foram executados no cluster.</span><span class="sxs-lookup"><span data-stu-id="90102-154">When the Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on the cluster.</span></span> <span data-ttu-id="90102-155">O modo de exibição padrão inclui Nome, Id, Remetente, Status, Hora de Início, Hora de Término, Duração, ID do Aplicativo e Fila do Dag.</span><span class="sxs-lookup"><span data-stu-id="90102-155">The default view includes the Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="90102-156">É possível adicionar mais colunas usando o ícone de engrenagem no canto direito da página.</span><span class="sxs-lookup"><span data-stu-id="90102-156">More columns can be added using the gear icon at the right of the page.</span></span>

    <span data-ttu-id="90102-157">Se você tiver apenas uma entrada, ela será para a consulta que você executou na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="90102-157">If you have only one entry, it will be for the query that you ran in the previous section.</span></span> <span data-ttu-id="90102-158">Se você tiver várias entradas, será possível pesquisar ao inserir critérios de pesquisa nos campos acima dos DAGs e pressionar **Enter**.</span><span class="sxs-lookup"><span data-stu-id="90102-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="90102-159">Escolha o **Nome do Dag** para a entrada mais recente do DAG.</span><span class="sxs-lookup"><span data-stu-id="90102-159">Select the **Dag Name** for the most recent DAG entry.</span></span> <span data-ttu-id="90102-160">Isso exibirá informações sobre o DAG, bem como a opção para baixar um zip de arquivos JSON que contêm informações sobre o DAG.</span><span class="sxs-lookup"><span data-stu-id="90102-160">This will display information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span></span>

    ![Detalhes do DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="90102-162">Acima dos **Detalhes do DAG**, há vários links que podem ser usados para exibir informações sobre o DAG.</span><span class="sxs-lookup"><span data-stu-id="90102-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="90102-163">**Contadores de DAG** exibe informações de contadores do DAG em questão.</span><span class="sxs-lookup"><span data-stu-id="90102-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="90102-164">**Modo de Exibição Gráfico** exibe uma representação gráfica deste DAG.</span><span class="sxs-lookup"><span data-stu-id="90102-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="90102-165">**Todos os Vértices** exibe uma lista dos vértices neste DAG.</span><span class="sxs-lookup"><span data-stu-id="90102-165">**All Vertices** displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="90102-166">**Todas as Tarefas** exibe uma lista das tarefas de todos os vértices neste DAG.</span><span class="sxs-lookup"><span data-stu-id="90102-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="90102-167">**Todas as Tentativas de Tarefa** exibe informações sobre as tentativas de execução de tarefas para este DAG.</span><span class="sxs-lookup"><span data-stu-id="90102-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="90102-168">Se você rolar a exibição da coluna até Vértices, Tarefas e Tentativas de Tarefa, observe que há links para exibir **contadores** e **exibir ou baixar logs** para cada linha.</span><span class="sxs-lookup"><span data-stu-id="90102-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="90102-169">Se houver uma falha com o trabalho, os Detalhes do DAG exibirão um status de FALHA, juntamente com links para informações sobre a tarefa com falha.</span><span class="sxs-lookup"><span data-stu-id="90102-169">If there was a failure with the job, the DAG Details will display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="90102-170">As informações de diagnóstico serão exibidas abaixo dos detalhes do DAG.</span><span class="sxs-lookup"><span data-stu-id="90102-170">Diagnostics information will be displayed beneath the DAG details.</span></span>
8. <span data-ttu-id="90102-171">Escolha **Modo de Exibição Gráfico**.</span><span class="sxs-lookup"><span data-stu-id="90102-171">Select **Graphical View**.</span></span> <span data-ttu-id="90102-172">Isso exibe uma representação gráfica do DAG.</span><span class="sxs-lookup"><span data-stu-id="90102-172">This displays a graphical representation of the DAG.</span></span> <span data-ttu-id="90102-173">Você pode colocar o mouse sobre cada vértice no modo de exibição para exibir informações sobre ele.</span><span class="sxs-lookup"><span data-stu-id="90102-173">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![Modo de Exibição Gráfico](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="90102-175">Clicar em um vértice carregará os **Detalhes do Vértice** para esse item.</span><span class="sxs-lookup"><span data-stu-id="90102-175">Clicking on a vertex will load the **Vertex Details** for that item.</span></span> <span data-ttu-id="90102-176">Clique no vértice **Mapa 1** para exibir detalhes do item em questão.</span><span class="sxs-lookup"><span data-stu-id="90102-176">Click on the **Map 1** vertex to display details for this item.</span></span> <span data-ttu-id="90102-177">Selecione **Confirmar** para confirmar a navegação.</span><span class="sxs-lookup"><span data-stu-id="90102-177">Select **Confirm** to confirm the navigation.</span></span>

    ![Detalhes do Vértice](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="90102-179">Observe que agora você tem links relacionados às tarefas e aos vértices na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="90102-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="90102-180">Você também pode chegar a essa página voltando para **Detalhes do DAG**, selecionando **Detalhes do Vértice** e selecionando o vértice **Mapa 1**.</span><span class="sxs-lookup"><span data-stu-id="90102-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="90102-181">**Contadores de Vértice** exibe informações de contadores do vértice em questão.</span><span class="sxs-lookup"><span data-stu-id="90102-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="90102-182">**Tarefas** exibe tarefas do vértice em questão.</span><span class="sxs-lookup"><span data-stu-id="90102-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="90102-183">**Tentativas de Tarefa** exibe informações sobre as tentativas de execução de tarefas do vértice em questão.</span><span class="sxs-lookup"><span data-stu-id="90102-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span></span>
    * <span data-ttu-id="90102-184">**Fontes e Coletores** exibe fontes de dados e coletores do vértice em questão.</span><span class="sxs-lookup"><span data-stu-id="90102-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="90102-185">Assim como no menu anterior, você pode rolar a exibição da coluna para Tarefas, Tentativas de Tarefa e Fontes de Coletores para exibir links para outras informações sobre cada item.</span><span class="sxs-lookup"><span data-stu-id="90102-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>
      >
      >
11. <span data-ttu-id="90102-186">Escolha **Tarefas** e selecione o item chamado **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="90102-186">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="90102-187">Isso exibirá os **Detalhes da Tarefa** desta tarefa.</span><span class="sxs-lookup"><span data-stu-id="90102-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="90102-188">Nessa tela, você pode exibir **Contadores de Tarefa** e **Tentativas de Tarefa**.</span><span class="sxs-lookup"><span data-stu-id="90102-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Detalhes de tarefa](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="90102-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="90102-190">Next Steps</span></span>
<span data-ttu-id="90102-191">Agora que você aprendeu a usar o modo de exibição do Tez, saiba mais sobre [Como usar o Hive no HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="90102-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="90102-192">Para obter informações técnicas mais detalhadas sobre o Tez, confira a [página sobre o Tez em Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="90102-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
