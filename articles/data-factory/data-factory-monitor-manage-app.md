---
title: aaaMonitor e gerenciar os pipelines de dados - Azure | Microsoft Docs
description: "Saiba como toouse Olá toomonitor de aplicativo de gerenciamento e monitoramento e gerenciar canais e fábricas de dados do Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a><span data-ttu-id="38e19-103">Monitorar e gerenciar os pipelines de fábrica de dados do Azure usando o aplicativo de monitoramento e gerenciamento de saudação</span><span class="sxs-lookup"><span data-stu-id="38e19-103">Monitor and manage Azure Data Factory pipelines by using hello Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="38e19-104">Usando o Portal do Azure/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="38e19-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="38e19-105">Usando o aplicativo de Monitoramento e Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="38e19-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="38e19-106">Este artigo descreve como toouse Olá toomonitor de aplicativo de gerenciamento e monitoramento, gerenciar e depurar seus pipelines de fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="38e19-106">This article describes how toouse hello Monitoring and Management app toomonitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="38e19-107">Ela também fornece informações sobre como toocreate alertas tooget notificado em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="38e19-107">It also provides information on how toocreate alerts tooget notified on failures.</span></span> <span data-ttu-id="38e19-108">Você pode começar a usar aplicativo hello por Olá assistindo a seguir vídeo:</span><span class="sxs-lookup"><span data-stu-id="38e19-108">You can get started with using hello application by watching hello following video:</span></span>

> [!NOTE]
> <span data-ttu-id="38e19-109">interface do usuário Olá mostrado no hello vídeo pode não corresponder exatamente o que você vê no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-109">hello user interface shown in hello video may not exactly match what you see in hello portal.</span></span> <span data-ttu-id="38e19-110">É um pouco mais antigo, mas conceitos permanecem Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="38e19-110">It's slightly older, but concepts remain hello same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a><span data-ttu-id="38e19-111">Inicie o aplicativo de monitoramento e gerenciamento de saudação</span><span class="sxs-lookup"><span data-stu-id="38e19-111">Launch hello Monitoring and Management app</span></span>
<span data-ttu-id="38e19-112">Olá toolaunch Monitor e o aplicativo de gerenciamento, clique em Olá **monitorar e gerenciar** bloco Olá **Data Factory** folha sua fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="38e19-112">toolaunch hello Monitor and Management app, click hello **Monitor & Manage** tile on hello **Data Factory** blade for your data factory.</span></span>

![Monitoramento do lado a lado na home page do hello fábrica de dados](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="38e19-114">Você deve ver o aplicativo de monitoramento e gerenciamento de saudação abrir em uma janela separada.</span><span class="sxs-lookup"><span data-stu-id="38e19-114">You should see hello Monitoring and Management app open in a separate window.</span></span>  

![Aplicativo de Monitoramento e Gerenciamento](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="38e19-116">Se você vir esse navegador da web hello está preso em "Autorizar...", desmarque Olá **bloquear cookies de terceiros e dados do site** caixa de seleção — ou manter essa opção selecionada, criar uma exceção para **login.microsoftonline.com** e, em seguida, tente tooopen Olá aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="38e19-116">If you see that hello web browser is stuck at "Authorizing...", clear hello **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try tooopen hello app again.</span></span>


<span data-ttu-id="38e19-117">Na lista de atividade Windows hello no painel do meio hello, você vê uma janela de atividade para cada execução de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="38e19-117">In hello Activity Windows list in hello middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="38e19-118">Por exemplo, se você tiver hello atividade agendada toorun por hora por cinco horas, você vê cinco janelas de atividade associadas com fatias de cinco dados.</span><span class="sxs-lookup"><span data-stu-id="38e19-118">For example, if you have hello activity scheduled toorun hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="38e19-119">Se você não vir o windows de atividade na lista de saudação na parte inferior do hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="38e19-119">If you don't see activity windows in hello list at hello bottom, do hello following:</span></span>
 
- <span data-ttu-id="38e19-120">Saudação de atualização **hora de início** e **hora de término** filtros em Olá toomatch superior Olá início e término do pipeline e clique em Olá **aplicar** botão.</span><span class="sxs-lookup"><span data-stu-id="38e19-120">Update hello **start time** and **end time** filters at hello top toomatch hello start and end times of your pipeline, and then click hello **Apply** button.</span></span>  
- <span data-ttu-id="38e19-121">lista de atividade Windows Hello não será atualizada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="38e19-121">hello Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="38e19-122">Clique em Olá **atualizar** botão na barra de ferramentas de saudação em Olá **atividade Windows** lista.</span><span class="sxs-lookup"><span data-stu-id="38e19-122">Click hello **Refresh** button on hello toolbar in hello **Activity Windows** list.</span></span>  

<span data-ttu-id="38e19-123">Se você não tiver um tootest de aplicativo da fábrica de dados essas etapas com, Olá tutorial: [copiar dados de armazenamento de Blob tooSQL banco de dados usando a fábrica de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="38e19-123">If you don't have a Data Factory application tootest these steps with, do hello tutorial: [copy data from Blob Storage tooSQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-hello-monitoring-and-management-app"></a><span data-ttu-id="38e19-124">Entender o aplicativo de monitoramento e gerenciamento de saudação</span><span class="sxs-lookup"><span data-stu-id="38e19-124">Understand hello Monitoring and Management app</span></span>
<span data-ttu-id="38e19-125">Há três guias Olá esquerda: **Resource Explorer**, **modos de exibição de monitoramento**, e **alertas**.</span><span class="sxs-lookup"><span data-stu-id="38e19-125">There are three tabs on hello left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="38e19-126">guia primeiro Hello (**Resource Explorer**) é selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="38e19-126">hello first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="38e19-127">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="38e19-127">Resource Explorer</span></span>
<span data-ttu-id="38e19-128">Consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="38e19-128">You see hello following:</span></span>

* <span data-ttu-id="38e19-129">Olá Resource Explorer **exibição de árvore** no painel esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-129">hello Resource Explorer **tree view** in hello left pane.</span></span>
* <span data-ttu-id="38e19-130">Olá **exibição de diagrama** na parte superior de saudação no painel do meio hello.</span><span class="sxs-lookup"><span data-stu-id="38e19-130">hello **Diagram View** at hello top in hello middle pane.</span></span>
* <span data-ttu-id="38e19-131">Olá **atividade Windows** lista na parte inferior da saudação no painel do meio hello.</span><span class="sxs-lookup"><span data-stu-id="38e19-131">hello **Activity Windows** list at hello bottom in hello middle pane.</span></span>
* <span data-ttu-id="38e19-132">Olá **propriedades**, **Pesquisador de objetos de janela de atividade**, e **Script** guias no painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-132">hello **Properties**, **Activity Window Explorer**, and **Script** tabs in hello right pane.</span></span>

<span data-ttu-id="38e19-133">No Gerenciador de recursos, você vê todos os recursos (pipelines, conjuntos de dados, serviços vinculados) na fábrica de dados de saudação em uma exibição de árvore.</span><span class="sxs-lookup"><span data-stu-id="38e19-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in hello data factory in a tree view.</span></span> <span data-ttu-id="38e19-134">Ao selecionar um objeto no Gerenciador de Recursos, você nota o seguinte:</span><span class="sxs-lookup"><span data-stu-id="38e19-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="38e19-135">Olá associados a entidade está realçada na saudação de exibição de diagrama de fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="38e19-135">hello associated Data Factory entity is highlighted in hello Diagram View.</span></span>
* <span data-ttu-id="38e19-136">[Associados windows atividade](data-factory-scheduling-and-execution.md) são realçados na lista de atividade Windows hello na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in hello Activity Windows list at hello bottom.</span></span>  
* <span data-ttu-id="38e19-137">Propriedades de saudação do objeto selecionado Olá são mostradas na janela de propriedades de saudação no painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-137">hello properties of hello selected object are shown in hello Properties window in hello right pane.</span></span>
* <span data-ttu-id="38e19-138">Olá definição JSON do objeto selecionado Olá é mostrado, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="38e19-138">hello JSON definition of hello selected object is shown, if applicable.</span></span> <span data-ttu-id="38e19-139">Por exemplo: um serviço vinculado, um conjunto de dados ou um pipeline.</span><span class="sxs-lookup"><span data-stu-id="38e19-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Gerenciador de Recursos](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="38e19-141">Consulte Olá [de agendamento e execução](data-factory-scheduling-and-execution.md) artigo para obter informações conceituais detalhadas sobre janelas de atividade.</span><span class="sxs-lookup"><span data-stu-id="38e19-141">See hello [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="38e19-142">Exibição de diagrama</span><span class="sxs-lookup"><span data-stu-id="38e19-142">Diagram View</span></span>
<span data-ttu-id="38e19-143">saudação de exibição de diagrama de uma fábrica de dados fornece um único painel de vidro toomonitor e gerenciar uma fábrica de dados e seus ativos.</span><span class="sxs-lookup"><span data-stu-id="38e19-143">hello Diagram View of a data factory provides a single pane of glass toomonitor and manage a data factory and its assets.</span></span> <span data-ttu-id="38e19-144">Quando você seleciona uma entidade de fábrica de dados (conjunto de dados/pipeline) na saudação de exibição de diagrama:</span><span class="sxs-lookup"><span data-stu-id="38e19-144">When you select a Data Factory entity (dataset/pipeline) in hello Diagram View:</span></span>

* <span data-ttu-id="38e19-145">entidade Olá da fábrica de dados é selecionada na exibição de árvore de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-145">hello data factory entity is selected in hello tree view.</span></span>
* <span data-ttu-id="38e19-146">Olá associados atividade windows é realçado na lista de atividade Windows hello.</span><span class="sxs-lookup"><span data-stu-id="38e19-146">hello associated activity windows are highlighted in hello Activity Windows list.</span></span>
* <span data-ttu-id="38e19-147">Propriedades de saudação do objeto selecionado Olá são mostradas na janela de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-147">hello properties of hello selected object are shown in hello Properties window.</span></span>

<span data-ttu-id="38e19-148">Quando o pipeline de saudação está habilitado (não em um estado de pausa), ela é mostrada com uma linha verde:</span><span class="sxs-lookup"><span data-stu-id="38e19-148">When hello pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Execução do pipeline](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="38e19-150">Você pode pausar, retomar ou encerrar um pipeline, selecionando-o no modo de exibição de diagrama hello e usando os botões de saudação na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-150">You can pause, resume, or terminate a pipeline by selecting it in hello diagram view and using hello buttons on hello command bar.</span></span>

![Pausar/retomar na barra de comandos Olá](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="38e19-152">Existem três botões de barra de comandos para o pipeline Olá Olá exibição de diagrama.</span><span class="sxs-lookup"><span data-stu-id="38e19-152">There are three command bar buttons for hello pipeline in hello Diagram View.</span></span> <span data-ttu-id="38e19-153">Você pode usar o pipeline do hello segundo botão toopause hello.</span><span class="sxs-lookup"><span data-stu-id="38e19-153">You can use hello second button toopause hello pipeline.</span></span> <span data-ttu-id="38e19-154">Pausando não encerrar Olá em atividades em execução no momento e permite que eles continuar toocompletion.</span><span class="sxs-lookup"><span data-stu-id="38e19-154">Pausing doesn't terminate hello currently running activities and lets them proceed toocompletion.</span></span> <span data-ttu-id="38e19-155">botão terceiro Olá pausa pipeline hello e finaliza a execução de atividades existente.</span><span class="sxs-lookup"><span data-stu-id="38e19-155">hello third button pauses hello pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="38e19-156">botão de primeira Olá retoma pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="38e19-156">hello first button resumes hello pipeline.</span></span> <span data-ttu-id="38e19-157">Quando o pipeline é pausado, a cor de saudação do pipeline Olá muda.</span><span class="sxs-lookup"><span data-stu-id="38e19-157">When your pipeline is paused, hello color of hello pipeline changes.</span></span> <span data-ttu-id="38e19-158">Por exemplo, um pipeline pausa aparece no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="38e19-158">For example, a paused pipeline looks like in hello following image:</span></span> 

![Pipeline em pausa](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="38e19-160">Você pode selecionar vários pipelines de dois ou mais usando a tecla Ctrl de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-160">You can multi-select two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="38e19-161">Você pode usar botões de barra de comando toopause/retomar Olá pipelines várias por vez.</span><span class="sxs-lookup"><span data-stu-id="38e19-161">You can use hello command bar buttons toopause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="38e19-162">Você pode também clique um pipeline e selecione as opções toosuspend, retome ou finalize um pipeline.</span><span class="sxs-lookup"><span data-stu-id="38e19-162">You can also right-click a pipeline and select options toosuspend, resume, or terminate a pipeline.</span></span> 

![Menu de contexto do pipeline](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="38e19-164">Clique em Olá **abrir pipeline** opção toosee todas as atividades de saudação no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-164">Click hello **Open pipeline** option toosee all hello activities in hello pipeline.</span></span> 

![Menu do pipeline aberto](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="38e19-166">No modo de pipeline de saudação aberto, você verá todas as atividades no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-166">In hello opened pipeline view, you see all activities in hello pipeline.</span></span> <span data-ttu-id="38e19-167">Neste exemplo, há apenas uma atividade: Copiar Atividade.</span><span class="sxs-lookup"><span data-stu-id="38e19-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Pipeline aberto](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="38e19-169">toogo fazer toohello modo de exibição anterior, clique em nome de fábrica de dados Olá no menu de navegação estrutural Olá na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-169">toogo back toohello previous view, click hello data factory name in hello breadcrumb menu at hello top.</span></span>

<span data-ttu-id="38e19-170">No modo de pipeline hello, quando você seleciona um conjunto de dados de saída ou quando você move o mouse sobre o conjunto de dados de saída Olá, consulte janela pop-up do Windows de atividade Olá para esse conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="38e19-170">In hello pipeline view, when you select an output dataset or when you move your mouse over hello output dataset, you see hello Activity Windows pop-up window for that dataset.</span></span>

![Janela pop-up de Atividades do Windows](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="38e19-172">Você pode clicar em um toosee detalhes da janela de atividade para ele no hello **propriedades** janela no painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-172">You can click an activity window toosee details for it in hello **Properties** window in hello right pane.</span></span>

![Propriedades da Janela de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="38e19-174">No painel direito da saudação, alterne toohello **Pesquisador de objetos de janela de atividade** guia toosee obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="38e19-174">In hello right pane, switch toohello **Activity Window Explorer** tab toosee more details.</span></span>

![Gerenciador de Janelas de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="38e19-176">Consulte também **resolvido variáveis** para cada tentativa de execução de uma atividade em Olá **tentativas** seção.</span><span class="sxs-lookup"><span data-stu-id="38e19-176">You also see **resolved variables** for each run attempt for an activity in hello **Attempts** section.</span></span>

![Variáveis resolvidas](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="38e19-178">Alternar toohello **Script** guia definição de script toosee Olá JSON para o objeto selecionado hello.</span><span class="sxs-lookup"><span data-stu-id="38e19-178">Switch toohello **Script** tab toosee hello JSON script definition for hello selected object.</span></span>   

![Guia Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="38e19-180">Você pode ver janelas de atividades em três locais:</span><span class="sxs-lookup"><span data-stu-id="38e19-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="38e19-181">Hello atividade Windows pop-up no hello modo de exibição de diagrama (painel central).</span><span class="sxs-lookup"><span data-stu-id="38e19-181">hello Activity Windows pop-up in hello Diagram View (middle pane).</span></span>
* <span data-ttu-id="38e19-182">Hello atividade janela Explorer no painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-182">hello Activity Window Explorer in hello right pane.</span></span>
* <span data-ttu-id="38e19-183">lista de atividade Windows Hello no painel inferior de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-183">hello Activity Windows list in hello bottom pane.</span></span>

<span data-ttu-id="38e19-184">No pop-up de atividade Windows hello e Gerenciador de janela de atividade, você pode rolar toohello semana anterior e Olá próxima semana usando Olá setas à esquerda e à direita.</span><span class="sxs-lookup"><span data-stu-id="38e19-184">In hello Activity Windows pop-up and Activity Window Explorer, you can scroll toohello previous week and hello next week by using hello left and right arrows.</span></span>

![Setas para a direita/esquerda do Gerenciador de Janelas de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="38e19-186">Final Olá Olá exibição de diagrama, você pode ver esses botões: ampliar, zoom, tooFit de Zoom, Zoom 100%, o layout de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="38e19-186">At hello bottom of hello Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom tooFit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="38e19-187">Olá **layout de bloqueio** botão impede que você mova acidentalmente tabelas e pipelines no hello exibição de diagrama.</span><span class="sxs-lookup"><span data-stu-id="38e19-187">hello **Lock layout** button prevents you from accidentally moving tables and pipelines in hello Diagram View.</span></span> <span data-ttu-id="38e19-188">Ele está ligado por padrão.</span><span class="sxs-lookup"><span data-stu-id="38e19-188">It's on by default.</span></span> <span data-ttu-id="38e19-189">Você pode desativá-lo e mover os entidades no diagrama de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-189">You can turn it off and move entities around in hello diagram.</span></span> <span data-ttu-id="38e19-190">Quando você pode desativá-lo, você pode usar pipelines e tabelas do hello último botão tooautomatically posição.</span><span class="sxs-lookup"><span data-stu-id="38e19-190">When you turn it off, you can use hello last button tooautomatically position tables and pipelines.</span></span> <span data-ttu-id="38e19-191">Você também pode ampliar ou reduzir usando a roda do mouse hello.</span><span class="sxs-lookup"><span data-stu-id="38e19-191">You can also zoom in or out by using hello mouse wheel.</span></span>

![Comandos de zoom da Exibição de Diagrama](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="38e19-193">Lista Janelas de Atividades</span><span class="sxs-lookup"><span data-stu-id="38e19-193">Activity Windows list</span></span>
<span data-ttu-id="38e19-194">lista de atividade Windows Hello na parte inferior de saudação do painel do meio Olá exibe todas as janelas de atividade para Olá conjunto de dados que você selecionou na Olá Gerenciador de recursos ou hello exibição de diagrama.</span><span class="sxs-lookup"><span data-stu-id="38e19-194">hello Activity Windows list at hello bottom of hello middle pane displays all activity windows for hello dataset that you selected in hello Resource Explorer or hello Diagram View.</span></span> <span data-ttu-id="38e19-195">Por padrão, a lista de hello está em ordem decrescente, que significa que você verá a janela de atividade mais recente Olá na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-195">By default, hello list is in descending order, which means that you see hello latest activity window at hello top.</span></span>

![Lista Janelas de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="38e19-197">Esta lista não atualiza automaticamente, portanto use Olá botão Olá barra de ferramentas toomanually atualizá-lo.</span><span class="sxs-lookup"><span data-stu-id="38e19-197">This list doesn't refresh automatically, so use hello refresh button on hello toolbar toomanually refresh it.</span></span>  

<span data-ttu-id="38e19-198">Windows de atividade podem ser em uma saudação status a seguir:</span><span class="sxs-lookup"><span data-stu-id="38e19-198">Activity windows can be in one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="38e19-199">Status</span><span class="sxs-lookup"><span data-stu-id="38e19-199">Status</span></span></th><th align="left"><span data-ttu-id="38e19-200">Substatus</span><span class="sxs-lookup"><span data-stu-id="38e19-200">Substatus</span></span></th><th align="left"><span data-ttu-id="38e19-201">Descrição</span><span class="sxs-lookup"><span data-stu-id="38e19-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="38e19-202">Aguardando</span><span class="sxs-lookup"><span data-stu-id="38e19-202">Waiting</span></span></td><td><span data-ttu-id="38e19-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="38e19-203">ScheduleTime</span></span></td><td><span data-ttu-id="38e19-204">tempo de saudação não são fornecidos para hello atividade janela toorun.</span><span class="sxs-lookup"><span data-stu-id="38e19-204">hello time hasn't come for hello activity window toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="38e19-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="38e19-205">DatasetDependencies</span></span></td><td><span data-ttu-id="38e19-206">dependências de upstream Olá não estão prontas.</span><span class="sxs-lookup"><span data-stu-id="38e19-206">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="38e19-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="38e19-207">ComputeResources</span></span></td><td><span data-ttu-id="38e19-208">recursos de computação de saudação não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="38e19-208">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="38e19-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="38e19-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="38e19-210">Todas as instâncias do hello atividade estão ocupadas executando outras janelas de atividade.</span><span class="sxs-lookup"><span data-stu-id="38e19-210">All hello activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="38e19-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="38e19-211">ActivityResume</span></span></td><td><span data-ttu-id="38e19-212">atividade de saudação é pausada e não é possível executar o windows de atividade Olá até que ela seja retomada.</span><span class="sxs-lookup"><span data-stu-id="38e19-212">hello activity is paused and can't run hello activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="38e19-213">Retry</span><span class="sxs-lookup"><span data-stu-id="38e19-213">Retry</span></span></td><td><span data-ttu-id="38e19-214">a execução da atividade Hello está sendo repetida.</span><span class="sxs-lookup"><span data-stu-id="38e19-214">hello activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="38e19-215">Validação</span><span class="sxs-lookup"><span data-stu-id="38e19-215">Validation</span></span></td><td><span data-ttu-id="38e19-216">A validação ainda não foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="38e19-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="38e19-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="38e19-217">ValidationRetry</span></span></td><td><span data-ttu-id="38e19-218">A validação é toobe espera repetida.</span><span class="sxs-lookup"><span data-stu-id="38e19-218">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="38e19-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="38e19-219">InProgress</span></span></td><td><span data-ttu-id="38e19-220">Validando</span><span class="sxs-lookup"><span data-stu-id="38e19-220">Validating</span></span></td><td><span data-ttu-id="38e19-221">Validação em andamento.</span><span class="sxs-lookup"><span data-stu-id="38e19-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="38e19-222">janela de atividade Hello está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="38e19-222">hello activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="38e19-223">Com falha</span><span class="sxs-lookup"><span data-stu-id="38e19-223">Failed</span></span></td><td><span data-ttu-id="38e19-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="38e19-224">TimedOut</span></span></td><td><span data-ttu-id="38e19-225">a execução da atividade Olá demorou mais do que o permitido pela atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-225">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="38e19-226">Cancelado</span><span class="sxs-lookup"><span data-stu-id="38e19-226">Canceled</span></span></td><td><span data-ttu-id="38e19-227">janela de atividade Olá foi cancelada por ação do usuário.</span><span class="sxs-lookup"><span data-stu-id="38e19-227">hello activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="38e19-228">Validação</span><span class="sxs-lookup"><span data-stu-id="38e19-228">Validation</span></span></td><td><span data-ttu-id="38e19-229">A validação falhou.</span><span class="sxs-lookup"><span data-stu-id="38e19-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="38e19-230">janela de atividade Olá falha toobe gerado ou validado.</span><span class="sxs-lookup"><span data-stu-id="38e19-230">hello activity window failed toobe generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="38e19-231">Ready</span><span class="sxs-lookup"><span data-stu-id="38e19-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="38e19-232">janela de atividade Hello está pronta para consumo.</span><span class="sxs-lookup"><span data-stu-id="38e19-232">hello activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="38e19-233">Ignorado</span><span class="sxs-lookup"><span data-stu-id="38e19-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="38e19-234">janela de atividade de saudação não foi processada.</span><span class="sxs-lookup"><span data-stu-id="38e19-234">hello activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="38e19-235">Nenhum</span><span class="sxs-lookup"><span data-stu-id="38e19-235">None</span></span></td><td>-</td><td><span data-ttu-id="38e19-236">Uma janela de atividade usado tooexist com um status diferente, mas foi redefinida.</span><span class="sxs-lookup"><span data-stu-id="38e19-236">An activity window used tooexist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="38e19-237">Quando você clica em uma janela de atividade na lista hello, você verá detalhes sobre ele no hello **atividade Windows Explorer** ou hello **propriedades** janela saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="38e19-237">When you click an activity window in hello list, you see details about it in hello **Activity Windows Explorer** or hello **Properties** window on hello right.</span></span>

![Gerenciador de Janelas de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="38e19-239">Atualizar janelas de atividades</span><span class="sxs-lookup"><span data-stu-id="38e19-239">Refresh activity windows</span></span>
<span data-ttu-id="38e19-240">detalhes de saudação não são atualizados automaticamente, portanto, use Olá atualização botão (Olá segundo) na lista de windows toomanually atualização hello atividade da barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-240">hello details aren't automatically refreshed, so use hello refresh button (hello second button) on hello command bar toomanually refresh hello activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="38e19-241">Janela Propriedades</span><span class="sxs-lookup"><span data-stu-id="38e19-241">Properties window</span></span>
<span data-ttu-id="38e19-242">janela de propriedades de saudação estiver no painel de mais à direita de saudação do aplicativo de monitoramento e gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-242">hello Properties window is in hello right-most pane of hello Monitoring and Management app.</span></span>

![Janela Propriedades](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="38e19-244">Exibe as propriedades do item de saudação que você selecionou na saudação (exibição de árvore), Gerenciador de recursos de exibição de diagrama ou lista do Windows de atividade.</span><span class="sxs-lookup"><span data-stu-id="38e19-244">It displays properties for hello item that you selected in hello Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="38e19-245">Gerenciador de Janelas de Atividades</span><span class="sxs-lookup"><span data-stu-id="38e19-245">Activity Window Explorer</span></span>
<span data-ttu-id="38e19-246">Olá **atividade janela Explorer** janela está no painel de mais à direita de saudação do aplicativo de monitoramento e gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-246">hello **Activity Window Explorer** window is in hello right-most pane of hello Monitoring and Management app.</span></span> <span data-ttu-id="38e19-247">Exibe detalhes sobre a janela de atividade de saudação que você selecionou na janela pop-up de atividade Windows hello ou lista de atividade Windows hello.</span><span class="sxs-lookup"><span data-stu-id="38e19-247">It displays details about hello activity window that you selected in hello Activity Windows pop-up window or hello Activity Windows list.</span></span>

![Gerenciador de Janelas de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="38e19-249">Você pode alternar a janela de atividade tooanother clicando na exibição do calendário Olá na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-249">You can switch tooanother activity window by clicking it in hello calendar view at hello top.</span></span> <span data-ttu-id="38e19-250">Também pode usar botões de seta de seta para a esquerda/direita Olá em janelas de atividade de toosee superior de saudação do hello semana anterior ou Olá próxima semana.</span><span class="sxs-lookup"><span data-stu-id="38e19-250">You can also use hello left arrow/right arrow buttons at hello top toosee activity windows from hello previous week or hello next week.</span></span>

<span data-ttu-id="38e19-251">Você pode usar os botões da barra de ferramentas de saudação na janela de atividade de Olá Olá inferior painel toorerun ou atualizar os detalhes de saudação no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-251">You can use hello toolbar buttons in hello bottom pane toorerun hello activity window or refresh hello details in hello pane.</span></span>

### <a name="script"></a><span data-ttu-id="38e19-252">Script</span><span class="sxs-lookup"><span data-stu-id="38e19-252">Script</span></span>
<span data-ttu-id="38e19-253">Você pode usar o hello **Script** Olá tooview de guia definição JSON da saudação selecionado entidade da fábrica de dados (serviço vinculado, o conjunto de dados ou pipeline).</span><span class="sxs-lookup"><span data-stu-id="38e19-253">You can use hello **Script** tab tooview hello JSON definition of hello selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Guia Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="38e19-255">Exibições do sistema</span><span class="sxs-lookup"><span data-stu-id="38e19-255">Use system views</span></span>
<span data-ttu-id="38e19-256">Monitoramento e gerenciamento de aplicativo Hello contém exibições do sistema predefinidos (**windows de atividade recente**, **falha windows atividade**, **windows atividade em andamento**) que permitir janelas de atividade recente/falha/em andamento de tooview para sua fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="38e19-256">hello Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you tooview recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="38e19-257">Alternar toohello **modos de exibição de monitoramento** guia esquerda Olá clicando nele.</span><span class="sxs-lookup"><span data-stu-id="38e19-257">Switch toohello **Monitoring Views** tab on hello left by clicking it.</span></span>

![Guia Exibições de Monitoramento](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="38e19-259">Atualmente, há três exibições do sistema com suporte.</span><span class="sxs-lookup"><span data-stu-id="38e19-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="38e19-260">Selecione uma opção toosee windows de atividade recente, a atividade com falha windows ou windows atividades em andamento na lista de atividade Windows hello (na parte inferior de saudação do painel do meio Olá).</span><span class="sxs-lookup"><span data-stu-id="38e19-260">Select an option toosee recent activity windows, failed activity windows, or in-progress activity windows in hello Activity Windows list (at hello bottom of hello middle pane).</span></span>

<span data-ttu-id="38e19-261">Quando você seleciona Olá **windows de atividade recente** opção, você verá todas as janelas de atividade recente em ordem decrescente de saudação **hora da última tentativa**.</span><span class="sxs-lookup"><span data-stu-id="38e19-261">When you select hello **Recent activity windows** option, you see all recent activity windows in descending order of hello **last attempt time**.</span></span>

<span data-ttu-id="38e19-262">Você pode usar o hello **falha windows atividade** exibir janelas de atividade de todos os toosee falhado na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-262">You can use hello **Failed activity windows** view toosee all failed activity windows in hello list.</span></span> <span data-ttu-id="38e19-263">Selecione uma janela de atividade com falha nos detalhes do hello lista toosee sobre ele no hello **propriedades** janela ou hello **Pesquisador de objetos de janela de atividade**.</span><span class="sxs-lookup"><span data-stu-id="38e19-263">Select a failed activity window in hello list toosee details about it in hello **Properties** window or hello **Activity Window Explorer**.</span></span> <span data-ttu-id="38e19-264">Você também pode baixar todos os logs de uma janela de atividades com falha.</span><span class="sxs-lookup"><span data-stu-id="38e19-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="38e19-265">Classificar e filtrar janelas de atividades</span><span class="sxs-lookup"><span data-stu-id="38e19-265">Sort and filter activity windows</span></span>
<span data-ttu-id="38e19-266">Saudação de alteração **hora de início** e **hora de término** configurações no windows de atividade toofilter da barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-266">Change hello **start time** and **end time** settings in hello command bar toofilter activity windows.</span></span> <span data-ttu-id="38e19-267">Depois de alterar a hora de início hello e a hora de término, clique em Olá botão Avançar toohello final tempo toorefresh hello atividade lista Windows.</span><span class="sxs-lookup"><span data-stu-id="38e19-267">After you change hello start time and end time, click hello button next toohello end time toorefresh hello Activity Windows list.</span></span>

![Horas de início e término](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="38e19-269">No momento, todos os tempos estão em formato UTC no aplicativo de monitoramento e gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-269">Currently, all times are in UTC format in hello Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="38e19-270">Em Olá **lista atividade Windows**, clique em nome de saudação de uma coluna (por exemplo: Status).</span><span class="sxs-lookup"><span data-stu-id="38e19-270">In hello **Activity Windows list**, click hello name of a column (for example: Status).</span></span>

![Menu da coluna da lista de Janelas de Atividades](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="38e19-272">Você pode fazer a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="38e19-272">You can do hello following:</span></span>

* <span data-ttu-id="38e19-273">Classificar em ordem crescente.</span><span class="sxs-lookup"><span data-stu-id="38e19-273">Sort in ascending order.</span></span>
* <span data-ttu-id="38e19-274">Classificar em ordem decrescente.</span><span class="sxs-lookup"><span data-stu-id="38e19-274">Sort in descending order.</span></span>
* <span data-ttu-id="38e19-275">Filtrar por um ou mais valores (Pronto, Aguardando etc.).</span><span class="sxs-lookup"><span data-stu-id="38e19-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="38e19-276">Quando você especificar um filtro em uma coluna, você vê o botão de filtro de saudação habilitado para aquela coluna, que indica que Olá valores na coluna de saudação são filtrados.</span><span class="sxs-lookup"><span data-stu-id="38e19-276">When you specify a filter on a column, you see hello filter button enabled for that column, which indicates that hello values in hello column are filtered values.</span></span>

![Filtrar uma coluna da lista de atividade Windows hello](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="38e19-278">Você pode usar Olá mesmo filtros de tooclear janela pop-up.</span><span class="sxs-lookup"><span data-stu-id="38e19-278">You can use hello same pop-up window tooclear filters.</span></span> <span data-ttu-id="38e19-279">tooclear todos os filtros para a lista de atividade Windows hello, botão Olá Limpar filtro na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-279">tooclear all filters for hello Activity Windows list, click hello clear filter button on hello command bar.</span></span>

![Limpar todos os filtros para a lista de atividade Windows hello](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="38e19-281">Execute ações em lote</span><span class="sxs-lookup"><span data-stu-id="38e19-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="38e19-282">Executar novamente as janelas de atividades selecionadas</span><span class="sxs-lookup"><span data-stu-id="38e19-282">Rerun selected activity windows</span></span>
<span data-ttu-id="38e19-283">Selecione uma janela de atividade, clique Olá para baixo para o primeiro botão da barra de comando hello e selecione **execute** / **novamente com upstream no pipeline**.</span><span class="sxs-lookup"><span data-stu-id="38e19-283">Select an activity window, click hello down arrow for hello first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="38e19-284">Quando você seleciona Olá **novamente com upstream no pipeline** opção, ele repete todas as janelas de atividade de upstream.</span><span class="sxs-lookup"><span data-stu-id="38e19-284">When you select hello **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="38e19-285">![Executar novamente uma janela de atividades](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="38e19-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="38e19-286">Você também pode selecionar várias janelas de atividade na lista de saudação e executá-los novamente no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="38e19-286">You can also select multiple activity windows in hello list and rerun them at hello same time.</span></span> <span data-ttu-id="38e19-287">Talvez você queira toofilter windows de atividade com base no status da saudação (por exemplo: **falha**) – e, em seguida, execute novamente Olá Falha na atividade windows depois de corrigir o problema de saudação que faz com que o hello atividade windows toofail.</span><span class="sxs-lookup"><span data-stu-id="38e19-287">You might want toofilter activity windows based on hello status (for example: **Failed**)--and then rerun hello failed activity windows after correcting hello issue that causes hello activity windows toofail.</span></span> <span data-ttu-id="38e19-288">Consulte Olá seção para obter detalhes sobre a filtragem do windows de atividade na lista de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="38e19-288">See hello following section for details about filtering activity windows in hello list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="38e19-289">Pausar/retomar vários pipelines</span><span class="sxs-lookup"><span data-stu-id="38e19-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="38e19-290">Você pode multiselect pipelines de dois ou mais usando a tecla Ctrl de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-290">You can multiselect two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="38e19-291">Você pode usar os botões da barra de comando hello (que serão destacados no retângulo Olá vermelho Olá a imagem a seguir) toopause/retomá-los.</span><span class="sxs-lookup"><span data-stu-id="38e19-291">You can use hello command bar buttons (which are highlighted in hello red rectangle in hello following image) toopause/resume them.</span></span>

![Pausar/retomar na barra de comandos Olá](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="38e19-293">Criar alertas</span><span class="sxs-lookup"><span data-stu-id="38e19-293">Create alerts</span></span>
<span data-ttu-id="38e19-294">Olá **alertas** página permite que você criar um alerta e exibir/editar/excluir os alertas existentes.</span><span class="sxs-lookup"><span data-stu-id="38e19-294">hello **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="38e19-295">Também é possível desabilitar/habilitar um alerta.</span><span class="sxs-lookup"><span data-stu-id="38e19-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="38e19-296">toosee Olá página alertas, clique em Olá **alertas** guia.</span><span class="sxs-lookup"><span data-stu-id="38e19-296">toosee hello Alerts page, click hello **Alerts** tab.</span></span>

![Guia Alertas](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a><span data-ttu-id="38e19-298">toocreate um alerta</span><span class="sxs-lookup"><span data-stu-id="38e19-298">toocreate an alert</span></span>
1. <span data-ttu-id="38e19-299">Clique em **adicionar alerta** tooadd um alerta.</span><span class="sxs-lookup"><span data-stu-id="38e19-299">Click **Add Alert** tooadd an alert.</span></span> <span data-ttu-id="38e19-300">Consulte Olá **detalhes** página.</span><span class="sxs-lookup"><span data-stu-id="38e19-300">You see hello **Details** page.</span></span>

    ![Criar Alertas - página Detalhes](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="38e19-302">Especifique a saudação **nome** e **descrição** alerta hello e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="38e19-302">Specify hello **Name** and **Description** for hello alert, and click **Next**.</span></span> <span data-ttu-id="38e19-303">Você deve ver Olá **filtros** página.</span><span class="sxs-lookup"><span data-stu-id="38e19-303">You should see hello **Filters** page.</span></span>

    ![Criar Alertas - página Filtros](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="38e19-305">Selecione Olá **evento**, **status**, e **substatus** (opcional) que você deseja toocreate um serviço de fábrica de dados de alerta para e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="38e19-305">Select hello **event**, **status**, and **substatus** (optional) that you want toocreate a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="38e19-306">Você deve ver Olá **destinatários** página.</span><span class="sxs-lookup"><span data-stu-id="38e19-306">You should see hello **Recipients** page.</span></span>

    ![Criar Alertas - página Destinatários](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="38e19-308">Selecione Olá **administradores de assinatura de Email** opção e/ou insira um **email adicional do administrador**e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="38e19-308">Select hello **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="38e19-309">Você deve ver o alerta de saudação na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="38e19-309">You should see hello alert in hello list.</span></span>

    ![Lista Alertas](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="38e19-311">Na lista de alertas hello, use os botões de saudação que estão associados a saudação alerta tooedit/excluir/desabilitar/habilitar um alerta.</span><span class="sxs-lookup"><span data-stu-id="38e19-311">In hello Alerts list, use hello buttons that are associated with hello alert tooedit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="38e19-312">Evento/status/substatus</span><span class="sxs-lookup"><span data-stu-id="38e19-312">Event/status/substatus</span></span>
<span data-ttu-id="38e19-313">Olá, tabela a seguir fornece Olá lista de eventos disponíveis e status (e substatus).</span><span class="sxs-lookup"><span data-stu-id="38e19-313">hello following table provides hello list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="38e19-314">Nome do evento</span><span class="sxs-lookup"><span data-stu-id="38e19-314">Event name</span></span> | <span data-ttu-id="38e19-315">Status</span><span class="sxs-lookup"><span data-stu-id="38e19-315">Status</span></span> | <span data-ttu-id="38e19-316">Substatus</span><span class="sxs-lookup"><span data-stu-id="38e19-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38e19-317">Execução de Atividade Iniciada</span><span class="sxs-lookup"><span data-stu-id="38e19-317">Activity Run Started</span></span> |<span data-ttu-id="38e19-318">Iniciado</span><span class="sxs-lookup"><span data-stu-id="38e19-318">Started</span></span> |<span data-ttu-id="38e19-319">Iniciando</span><span class="sxs-lookup"><span data-stu-id="38e19-319">Starting</span></span> |
| <span data-ttu-id="38e19-320">Execução de Atividade Concluída</span><span class="sxs-lookup"><span data-stu-id="38e19-320">Activity Run Finished</span></span> |<span data-ttu-id="38e19-321">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="38e19-321">Succeeded</span></span> |<span data-ttu-id="38e19-322">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="38e19-322">Succeeded</span></span> |
| <span data-ttu-id="38e19-323">Execução de Atividade Concluída</span><span class="sxs-lookup"><span data-stu-id="38e19-323">Activity Run Finished</span></span> |<span data-ttu-id="38e19-324">Com falha</span><span class="sxs-lookup"><span data-stu-id="38e19-324">Failed</span></span> |<span data-ttu-id="38e19-325">Alocação de Recursos com Falha</span><span class="sxs-lookup"><span data-stu-id="38e19-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="38e19-326">Execução com falha</span><span class="sxs-lookup"><span data-stu-id="38e19-326">Failed Execution</span></span><br/><br/><span data-ttu-id="38e19-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="38e19-327">Timed Out</span></span><br/><br/><span data-ttu-id="38e19-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="38e19-328">Failed Validation</span></span><br/><br/><span data-ttu-id="38e19-329">Abandoned</span><span class="sxs-lookup"><span data-stu-id="38e19-329">Abandoned</span></span> |
| <span data-ttu-id="38e19-330">Criação de Cluster HDI sob Demanda Iniciada</span><span class="sxs-lookup"><span data-stu-id="38e19-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="38e19-331">Iniciado</span><span class="sxs-lookup"><span data-stu-id="38e19-331">Started</span></span> |-|
| <span data-ttu-id="38e19-332">Cluster HDI sob Demanda Criado com Êxito</span><span class="sxs-lookup"><span data-stu-id="38e19-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="38e19-333">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="38e19-333">Succeeded</span></span> |-|
| <span data-ttu-id="38e19-334">Cluster HDI sob Demanda Excluído</span><span class="sxs-lookup"><span data-stu-id="38e19-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="38e19-335">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="38e19-335">Succeeded</span></span> |-|

### <a name="tooedit-delete-or-disable-an-alert"></a><span data-ttu-id="38e19-336">tooedit, excluir ou desabilitar um alerta</span><span class="sxs-lookup"><span data-stu-id="38e19-336">tooedit, delete, or disable an alert</span></span>

<span data-ttu-id="38e19-337">Use Olá tooedit botões (realçado em vermelho), excluir ou desabilitar um alerta a seguir.</span><span class="sxs-lookup"><span data-stu-id="38e19-337">Use hello following buttons (highlighted in red) tooedit, delete, or disable an alert.</span></span>

![Botões Alertas](./media/data-factory-monitor-manage-app/AlertButtons.png)
