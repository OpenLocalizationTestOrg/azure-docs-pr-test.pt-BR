---
title: aaaUse Tez UI com HDInsight baseados em Windows - Azure | Microsoft Docs
description: "Saiba como Olá toouse Tez UI toodebug Tez trabalhos no HDInsight de HDInsight baseados no Windows."
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
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="03716-103">Use Olá Tez UI toodebug Tez trabalhos no HDInsight baseados no Windows</span><span class="sxs-lookup"><span data-stu-id="03716-103">Use hello Tez UI toodebug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="03716-104">Olá Tez UI é uma página da web que pode ser usado toounderstand e depurar os trabalhos que usam Tez como mecanismo de execução de saudação em clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="03716-104">hello Tez UI is a web page that can be used toounderstand and debug jobs that use Tez as hello execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="03716-105">Olá Tez UI permite toovisualize trabalho de saudação como um gráfico de itens conectados, detalhar cada item e recuperar estatísticas e informações de registro em log.</span><span class="sxs-lookup"><span data-stu-id="03716-105">hello Tez UI allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="03716-106">etapas de saudação neste documento exigem um cluster HDInsight que usa o Windows.</span><span class="sxs-lookup"><span data-stu-id="03716-106">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="03716-107">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="03716-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="03716-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="03716-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03716-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="03716-109">Prerequisites</span></span>
* <span data-ttu-id="03716-110">Um cluster HDInsight baseado no Windows.</span><span class="sxs-lookup"><span data-stu-id="03716-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="03716-111">Para obter as etapas de criação de um novo cluster, confira [Introdução ao uso do HDInsight baseado no Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="03716-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="03716-112">Olá Tez UI só está disponível em clusters HDInsight baseados no Windows criados após 8 de fevereiro de 2016.</span><span class="sxs-lookup"><span data-stu-id="03716-112">hello Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="03716-113">Um cliente da Área de Trabalho Remota baseado no Windows.</span><span class="sxs-lookup"><span data-stu-id="03716-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="03716-114">Noções básicas sobre o Tez</span><span class="sxs-lookup"><span data-stu-id="03716-114">Understanding Tez</span></span>
<span data-ttu-id="03716-115">Tez é uma estrutura extensível para processamento de dados no Hadoop que fornece maior velocidade de processamento do que o MapReduce tradicional.</span><span class="sxs-lookup"><span data-stu-id="03716-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="03716-116">Para clusters HDInsight baseados no Windows, é um mecanismo opcional que você pode habilitar para o Hive usando o comando a seguir como parte de sua consulta de Hive de saudação:</span><span class="sxs-lookup"><span data-stu-id="03716-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using hello following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="03716-117">Quando o trabalho é enviado tooTez, ele cria um direcionado acíclico Graph (DAG) que descreve a ordem de saudação de execução das ações de saudação exigidos pelo trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="03716-117">When work is submitted tooTez, it creates a Directed Acyclic Graph (DAG) that describes hello order of execution of hello actions required by hello job.</span></span> <span data-ttu-id="03716-118">Ações individuais são chamadas de vértices e executar um pedaço de saudação trabalho geral.</span><span class="sxs-lookup"><span data-stu-id="03716-118">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="03716-119">a execução real Olá Olá trabalho descrita por um vértice é chamada de uma tarefa e pode ser distribuída em vários nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="03716-119">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-ui"></a><span data-ttu-id="03716-120">Saudação de compreensão Tez UI</span><span class="sxs-lookup"><span data-stu-id="03716-120">Understanding hello Tez UI</span></span>
<span data-ttu-id="03716-121">Olá Tez UI é que uma página da web fornece informações sobre os processos que estão em execução, ou tenha executaram anteriormente usando Tez.</span><span class="sxs-lookup"><span data-stu-id="03716-121">hello Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="03716-122">Ele permite tooview Olá DAG gerado pelo Tez, como ele é distribuído entre clusters, os contadores como a memória usada por tarefas e vértices e informações de erro.</span><span class="sxs-lookup"><span data-stu-id="03716-122">It allows you tooview hello DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="03716-123">Ele pode oferecer informações úteis no hello os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="03716-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="03716-124">Monitorando processos de longa execução, exibindo Olá progresso de mapa e reduzir as tarefas.</span><span class="sxs-lookup"><span data-stu-id="03716-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="03716-125">Analisar dados históricos para toolearn processos com êxito ou falha, como o processamento pode ser aprimorado ou razão da falha.</span><span class="sxs-lookup"><span data-stu-id="03716-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="03716-126">Gerar um DAG</span><span class="sxs-lookup"><span data-stu-id="03716-126">Generate a DAG</span></span>
<span data-ttu-id="03716-127">Olá Tez UI conterá apenas dados se um trabalho que usa Olá Tez mecanismo está em execução ou tem foi executado no hello anterior.</span><span class="sxs-lookup"><span data-stu-id="03716-127">hello Tez UI will only contain data if a job that uses hello Tez engine is currently running, or has been ran in hello past.</span></span> <span data-ttu-id="03716-128">Normalmente, as consultas simples do Hive podem ser resolvidas sem usar o Tez. Porém, as consultas mais complexas que realizam filtragem, agrupamento, ordenação, associações etc. normalmente exigirão o Tez.</span><span class="sxs-lookup"><span data-stu-id="03716-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="03716-129">Use Olá etapas toorun uma consulta de Hive que será executado usando Tez a seguir.</span><span class="sxs-lookup"><span data-stu-id="03716-129">Use hello following steps toorun a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="03716-130">Em um navegador da web, navegar toohttps://CLUSTERNAME.azurehdinsight.net, onde **CLUSTERNAME** é o nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="03716-130">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="03716-131">No menu de saudação na parte superior de saudação da página hello, selecione Olá **Editor Hive**.</span><span class="sxs-lookup"><span data-stu-id="03716-131">From hello menu at hello top of hello page, select hello **Hive Editor**.</span></span> <span data-ttu-id="03716-132">Isso exibirá uma página com hello consulta de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="03716-132">This will display a page with hello following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="03716-133">Apagar a consulta de exemplo hello e substitua-o pelo seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="03716-133">Erase hello example query and replace it with hello following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="03716-134">Selecione Olá **enviar** botão.</span><span class="sxs-lookup"><span data-stu-id="03716-134">Select hello **Submit** button.</span></span> <span data-ttu-id="03716-135">Olá **sessão de trabalho** seção final Olá Olá página exibirá o status de saudação de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="03716-135">hello **Job Session** section at hello bottom of hello page will display hello status of hello query.</span></span> <span data-ttu-id="03716-136">Uma vez Olá alterações de status muito**concluído**, selecione Olá **exibir detalhes** link tooview resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="03716-136">Once hello status changes too**Completed**, select hello **View Details** link tooview hello results.</span></span> <span data-ttu-id="03716-137">Olá **saída de trabalho** deve ser a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="03716-137">hello **Job Output** should be similar toohello following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a><span data-ttu-id="03716-138">Use Olá Tez UI</span><span class="sxs-lookup"><span data-stu-id="03716-138">Use hello Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="03716-139">Olá Tez UI só está disponível na área de trabalho Olá Olá principal de nós de cluster, você deve usar nós de cabeçalho de toohello de tooconnect de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="03716-139">hello Tez UI is only available from hello desktop of hello cluster head nodes, so you must use Remote Desktop tooconnect toohello head nodes.</span></span>
>
>

1. <span data-ttu-id="03716-140">De saudação [portal do Azure](https://portal.azure.com), selecione o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="03716-140">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="03716-141">Da parte superior de saudação da folha de HDInsight hello, selecione Olá **área de trabalho remota** ícone.</span><span class="sxs-lookup"><span data-stu-id="03716-141">From hello top of hello HDInsight blade, select hello **Remote Desktop** icon.</span></span> <span data-ttu-id="03716-142">Isso exibirá a folha de área de trabalho remota Olá</span><span class="sxs-lookup"><span data-stu-id="03716-142">This will display hello remote desktop blade</span></span>

    ![Ícone da área de trabalho remota](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="03716-144">Na folha de área de trabalho remota hello, selecione **conectar** nó principal do cluster tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="03716-144">From hello Remote Desktop blade, select **Connect** tooconnect toohello cluster head node.</span></span> <span data-ttu-id="03716-145">Quando solicitado, use Olá cluster área de trabalho remota usuário nome e senha tooauthenticate Olá conexão.</span><span class="sxs-lookup"><span data-stu-id="03716-145">When prompted, use hello cluster Remote Desktop user name and password tooauthenticate hello connection.</span></span>

    ![Ícone de conexão da área de trabalho remota](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="03716-147">Se você não tiver habilitado a conectividade de área de trabalho remota, forneça um nome de usuário, senha e data de validade, e selecione **habilitar** tooenable área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="03716-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** tooenable Remote Desktop.</span></span> <span data-ttu-id="03716-148">Depois que ele tiver sido habilitado, use Olá tooconnect de etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="03716-148">Once it has been enabled, use hello previous steps tooconnect.</span></span>
   >
   >
3. <span data-ttu-id="03716-149">Uma vez conectado, abra o Internet Explorer na área de trabalho de remota do hello, ícone de engrenagem Olá select no superior Olá direita do navegador Olá e, em seguida, selecione **configurações de exibição de compatibilidade**.</span><span class="sxs-lookup"><span data-stu-id="03716-149">Once connected, open Internet Explorer on hello remote desktop, select hello gear icon in hello upper right of hello browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="03716-150">Na parte inferior de saudação do **configurações de exibição de compatibilidade**, desmarque Olá a caixa de seleção para **exibir sites da intranet na exibição de compatibilidade** e **listas de compatibilidade de usar o Microsoft**, e, em seguida, selecione **fechar**.</span><span class="sxs-lookup"><span data-stu-id="03716-150">From hello bottom of **Compatibility View Settings**, clear hello check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="03716-151">No Internet Explorer, navegue toohttp://headnodehost:8188/tezui / #/.</span><span class="sxs-lookup"><span data-stu-id="03716-151">In Internet Explorer, browse toohttp://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="03716-152">Isso exibirá Olá Tez UI</span><span class="sxs-lookup"><span data-stu-id="03716-152">This will display hello Tez UI</span></span>

    ![Interface de usuário do Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="03716-154">Quando carregado Olá Tez UI, você verá uma lista de DAGs que estão sendo executados, ou ter sido executado no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="03716-154">When hello Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on hello cluster.</span></span> <span data-ttu-id="03716-155">exibição padrão de saudação inclui Olá Dag Name, Id, emissor, Status, hora de início, hora de término, duração, ID do aplicativo e fila.</span><span class="sxs-lookup"><span data-stu-id="03716-155">hello default view includes hello Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="03716-156">Mais colunas podem ser adicionadas usando o ícone de engrenagem Olá na saudação à direita da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="03716-156">More columns can be added using hello gear icon at hello right of hello page.</span></span>

    <span data-ttu-id="03716-157">Se você tiver apenas uma entrada, ele será usado para consulta Olá que você executou na seção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="03716-157">If you have only one entry, it will be for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="03716-158">Se você tiver várias entradas, você pode pesquisar inserindo critérios de pesquisa nos campos de saudação acima Olá DAGs e ocorrências **Enter**.</span><span class="sxs-lookup"><span data-stu-id="03716-158">If you have multiple entries, you can search by entering search criteria in hello fields above hello DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="03716-159">Selecione Olá **Dag Name** para a entrada mais recente DAG hello.</span><span class="sxs-lookup"><span data-stu-id="03716-159">Select hello **Dag Name** for hello most recent DAG entry.</span></span> <span data-ttu-id="03716-160">Isso exibirá informações sobre Olá DAG, bem como toodownload de opção Olá um zip dos arquivos JSON que contêm informações sobre Olá DAG.</span><span class="sxs-lookup"><span data-stu-id="03716-160">This will display information about hello DAG, as well as hello option toodownload a zip of JSON files that contain information about hello DAG.</span></span>

    ![Detalhes do DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="03716-162">Acima Olá **DAG detalhes** são vários links que podem ser usados toodisplay informações sobre Olá DAG.</span><span class="sxs-lookup"><span data-stu-id="03716-162">Above hello **DAG Details** are several links that can be used toodisplay information about hello DAG.</span></span>

   * <span data-ttu-id="03716-163">**Contadores de DAG** exibe informações de contadores do DAG em questão.</span><span class="sxs-lookup"><span data-stu-id="03716-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="03716-164">**Modo de Exibição Gráfico** exibe uma representação gráfica deste DAG.</span><span class="sxs-lookup"><span data-stu-id="03716-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="03716-165">**Todos os vértices** exibe uma lista dos vértices de saudação neste DAG.</span><span class="sxs-lookup"><span data-stu-id="03716-165">**All Vertices** displays a list of hello vertices in this DAG.</span></span>
   * <span data-ttu-id="03716-166">**Todas as tarefas** exibe uma lista de tarefas Olá para todos os vértices neste DAG.</span><span class="sxs-lookup"><span data-stu-id="03716-166">**All Tasks** displays a list of hello tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="03716-167">**Todos os TaskAttempts** exibe informações sobre Olá tentativas toorun tarefas para esta DAG.</span><span class="sxs-lookup"><span data-stu-id="03716-167">**All TaskAttempts** displays information about hello attempts toorun tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="03716-168">Se você rolar a exibição da coluna Olá vértices, tarefas e TaskAttempts, observe que há links tooview **contadores** e **exibir ou baixar os logs** para cada linha.</span><span class="sxs-lookup"><span data-stu-id="03716-168">If you scroll hello column display for Vertices, Tasks and TaskAttempts, notice that there are links tooview **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="03716-169">Se houver uma falha com o trabalho Olá, Olá DAG detalhes exibirá um status de falha, junto com links tooinformation sobre Olá tarefa que falhou.</span><span class="sxs-lookup"><span data-stu-id="03716-169">If there was a failure with hello job, hello DAG Details will display a status of FAILED, along with links tooinformation about hello failed task.</span></span> <span data-ttu-id="03716-170">Informações de diagnóstico serão exibidas abaixo detalhes Olá DAG.</span><span class="sxs-lookup"><span data-stu-id="03716-170">Diagnostics information will be displayed beneath hello DAG details.</span></span>
8. <span data-ttu-id="03716-171">Escolha **Modo de Exibição Gráfico**.</span><span class="sxs-lookup"><span data-stu-id="03716-171">Select **Graphical View**.</span></span> <span data-ttu-id="03716-172">Isso exibe uma representação gráfica da saudação DAG.</span><span class="sxs-lookup"><span data-stu-id="03716-172">This displays a graphical representation of hello DAG.</span></span> <span data-ttu-id="03716-173">Você pode colocar o mouse Olá sobre cada vértice no hello exibir toodisplay informações sobre ele.</span><span class="sxs-lookup"><span data-stu-id="03716-173">You can place hello mouse over each vertex in hello view toodisplay information about it.</span></span>

    ![Modo de Exibição Gráfico](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="03716-175">Clicar em um vértice carregará Olá **detalhes de vértice** para aquele item.</span><span class="sxs-lookup"><span data-stu-id="03716-175">Clicking on a vertex will load hello **Vertex Details** for that item.</span></span> <span data-ttu-id="03716-176">Clique em Olá **mapa 1** detalhes de toodisplay de vértice para este item.</span><span class="sxs-lookup"><span data-stu-id="03716-176">Click on hello **Map 1** vertex toodisplay details for this item.</span></span> <span data-ttu-id="03716-177">Selecione **confirmar** tooconfirm navegação de saudação.</span><span class="sxs-lookup"><span data-stu-id="03716-177">Select **Confirm** tooconfirm hello navigation.</span></span>

    ![Detalhes do Vértice](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="03716-179">Observe que agora tem links na parte superior de saudação da página de saudação que são as tarefas e toovertices relacionados.</span><span class="sxs-lookup"><span data-stu-id="03716-179">Note that you now have links at hello top of hello page that are related toovertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="03716-180">Você também pode chegar a essa página voltando muito**DAG detalhes**, selecionando **detalhes de vértice**e, em seguida, selecionando Olá **mapa 1** vértice.</span><span class="sxs-lookup"><span data-stu-id="03716-180">You can also arrive at this page by going back too**DAG Details**, selecting **Vertex Details**, and then selecting hello **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="03716-181">**Contadores de Vértice** exibe informações de contadores do vértice em questão.</span><span class="sxs-lookup"><span data-stu-id="03716-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="03716-182">**Tarefas** exibe tarefas do vértice em questão.</span><span class="sxs-lookup"><span data-stu-id="03716-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="03716-183">**Tentativas de tarefas** exibe informações sobre tentativas toorun tarefas para esta vértice.</span><span class="sxs-lookup"><span data-stu-id="03716-183">**Task Attempts** displays information about attempts toorun tasks for this vertex.</span></span>
    * <span data-ttu-id="03716-184">**Fontes e Coletores** exibe fontes de dados e coletores do vértice em questão.</span><span class="sxs-lookup"><span data-stu-id="03716-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="03716-185">Como com menu anterior do hello, você pode rolar a exibição da coluna Olá para tarefas, tentativas de tarefa e fontes & Sinks__ toodisplay vincula toomore informações para cada item.</span><span class="sxs-lookup"><span data-stu-id="03716-185">As with hello previous menu, you can scroll hello column display for Tasks, Task Attempts, and Sources & Sinks__ toodisplay links toomore information for each item.</span></span>
      >
      >
11. <span data-ttu-id="03716-186">Selecione **tarefas**, e, em seguida, o item de saudação selecione chamado **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="03716-186">Select **Tasks**, and then select hello item named **00_000000**.</span></span> <span data-ttu-id="03716-187">Isso exibirá os **Detalhes da Tarefa** desta tarefa.</span><span class="sxs-lookup"><span data-stu-id="03716-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="03716-188">Nessa tela, você pode exibir **Contadores de Tarefa** e **Tentativas de Tarefa**.</span><span class="sxs-lookup"><span data-stu-id="03716-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Detalhes de tarefa](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="03716-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03716-190">Next Steps</span></span>
<span data-ttu-id="03716-191">Agora que você aprendeu como exibir hello toouse Tez, saiba mais sobre [usando Hive no HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="03716-191">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="03716-192">Para obter mais informações técnicas sobre Tez, consulte Olá [Tez página no Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="03716-192">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
