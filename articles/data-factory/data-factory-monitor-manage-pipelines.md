---
title: aaaMonitor e gerenciar pipelines usando hello portal do Azure e do PowerShell | Microsoft Docs
description: "Saiba como toouse Olá portal do Azure e o Azure PowerShell toomonitor e gerenciar as fábricas de dados do Azure hello e pipelines que você criou."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a><span data-ttu-id="08c78-103">Monitorar e gerenciar os pipelines de fábrica de dados do Azure usando hello portal do Azure e do PowerShell</span><span class="sxs-lookup"><span data-stu-id="08c78-103">Monitor and manage Azure Data Factory pipelines by using hello Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08c78-104">Usando o Portal do Azure/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="08c78-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="08c78-105">Usando o aplicativo de Monitoramento e Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="08c78-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="08c78-106">aplicativo de gerenciamento e monitoramento Hello fornece um melhor suporte para monitorar e gerenciar seus pipelines de dados e os problemas de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="08c78-106">hello monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="08c78-107">Para obter detalhes sobre como usar o aplicativo hello, consulte [monitorar e gerenciar os pipelines de fábrica de dados usando o aplicativo de monitoramento e gerenciamento Olá](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="08c78-107">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="08c78-108">Este artigo descreve como toomonitor, gerenciar e depurar seus pipelines usando o portal do Azure e o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08c78-108">This article describes how toomonitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="08c78-109">Olá artigo também fornece informações sobre como toocreate alertas e obter notificado sobre falhas.</span><span class="sxs-lookup"><span data-stu-id="08c78-109">hello article also provides information on how toocreate alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="08c78-110">Entenda os pipelines e os estados de atividade</span><span class="sxs-lookup"><span data-stu-id="08c78-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="08c78-111">Usando Olá portal do Azure, você pode:</span><span class="sxs-lookup"><span data-stu-id="08c78-111">By using hello Azure portal, you can:</span></span>

* <span data-ttu-id="08c78-112">Exibir sua data factory como um diagrama.</span><span class="sxs-lookup"><span data-stu-id="08c78-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="08c78-113">Exibir atividades dentro de um pipeline.</span><span class="sxs-lookup"><span data-stu-id="08c78-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="08c78-114">Exibir conjuntos de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="08c78-114">View input and output datasets.</span></span>

<span data-ttu-id="08c78-115">Esta seção também descreve como uma fatia do conjunto de dados faz a transição de um estado de tooanother.</span><span class="sxs-lookup"><span data-stu-id="08c78-115">This section also describes how a dataset slice transitions from one state tooanother state.</span></span>   

### <a name="navigate-tooyour-data-factory"></a><span data-ttu-id="08c78-116">Navegue tooyour fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="08c78-116">Navigate tooyour data factory</span></span>
1. <span data-ttu-id="08c78-117">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="08c78-117">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="08c78-118">Clique em **fábricas de dados** no menu Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="08c78-118">Click **Data factories** on hello menu on hello left.</span></span> <span data-ttu-id="08c78-119">Se você não estiver visível, clique em **mais serviços >**e, em seguida, clique em **fábricas de dados** em Olá **INTELLIGENCE + análise** categoria.</span><span class="sxs-lookup"><span data-stu-id="08c78-119">If you don't see it, click **More services >**, and then click **Data factories** under hello **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Procurar tudo > Data factories](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="08c78-121">Em Olá **fábricas de dados** folha, a fábrica de dados Olá select que você está interessado.</span><span class="sxs-lookup"><span data-stu-id="08c78-121">On hello **Data factories** blade, select hello data factory that you're interested in.</span></span>

    ![Selecionar o data factory](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="08c78-123">Você verá a página inicial de Olá Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="08c78-123">You should see hello home page for hello data factory.</span></span>

   ![Folha Data factory](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="08c78-125">Modo de exibição de diagrama de uma data factory</span><span class="sxs-lookup"><span data-stu-id="08c78-125">Diagram view of your data factory</span></span>
<span data-ttu-id="08c78-126">Olá **diagrama** de uma fábrica de dados fornece um único painel de vidro toomonitor e gerencia Olá data factory e seus ativos.</span><span class="sxs-lookup"><span data-stu-id="08c78-126">hello **Diagram** view of a data factory provides a single pane of glass toomonitor and manage hello data factory and its assets.</span></span> <span data-ttu-id="08c78-127">Olá toosee **diagrama** exibir sua fábrica de dados, clique em **diagrama** na página inicial do Olá Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="08c78-127">toosee hello **Diagram** view of your data factory, click **Diagram** on hello home page for hello data factory.</span></span>

![Exibição de diagrama](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="08c78-129">Você pode ampliar, zoom, toofit de zoom, zoom too100%, layout de saudação do bloqueio do diagrama de saudação e posicione automaticamente pipelines e conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="08c78-129">You can zoom in, zoom out, zoom toofit, zoom too100%, lock hello layout of hello diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="08c78-130">Você também pode ver informações de linhagem de dados hello (ou seja, Mostrar itens upstream e downstream dos itens selecionados).</span><span class="sxs-lookup"><span data-stu-id="08c78-130">You can also see hello data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="08c78-131">Atividades dentro de um pipeline</span><span class="sxs-lookup"><span data-stu-id="08c78-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="08c78-132">Clique com botão direito pipeline hello e, em seguida, clique em **pipeline abrir** toosee todas as atividades em Olá pipeline, juntamente com conjuntos de dados de entrada e saídos para atividades de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-132">Right-click hello pipeline, and then click **Open pipeline** toosee all activities in hello pipeline, along with input and output datasets for hello activities.</span></span> <span data-ttu-id="08c78-133">Esse recurso é útil quando seu pipeline inclui mais de uma atividade e desejar linhagem operacionais do hello toounderstand de um único pipeline.</span><span class="sxs-lookup"><span data-stu-id="08c78-133">This feature is useful when your pipeline includes more than one activity and you want toounderstand hello operational lineage of a single pipeline.</span></span>

    ![Menu do pipeline aberto](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="08c78-135">Saudação de exemplo a seguir, você verá uma atividade de cópia no pipeline de saudação com uma entrada e uma saída.</span><span class="sxs-lookup"><span data-stu-id="08c78-135">In hello following example, you see a copy activity in hello pipeline with an input and an output.</span></span> 

    ![Atividades dentro de um pipeline](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="08c78-137">Você pode navegar toohello back home page da fábrica de dados Olá clicando Olá **fábrica de dados** link na navegação de trilha Olá no canto superior esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-137">You can navigate back toohello home page of hello data factory by clicking hello **Data factory** link in hello breadcrumb at hello top-left corner.</span></span>

    ![Navegue fábrica toodata back](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="08c78-139">Estado de saudação de exibição de cada atividade dentro de um pipeline</span><span class="sxs-lookup"><span data-stu-id="08c78-139">View hello state of each activity inside a pipeline</span></span>
<span data-ttu-id="08c78-140">Você pode exibir o estado atual de saudação de uma atividade exibindo status de saudação de qualquer um dos conjuntos de dados de saudação que são produzidos pela atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-140">You can view hello current state of an activity by viewing hello status of any of hello datasets that are produced by hello activity.</span></span>

<span data-ttu-id="08c78-141">Clicando duas vezes em Olá **OutputBlobTable** em Olá **diagrama**, você pode ver todas as fatias de saudação que são produzidas pela atividade diferente executa dentro de um pipeline.</span><span class="sxs-lookup"><span data-stu-id="08c78-141">By double-clicking hello **OutputBlobTable** in hello **Diagram**, you can see all hello slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="08c78-142">Você pode ver que a atividade de cópia Olá foi executado com êxito para Olá últimas oito horas e produzido fatias Olá Olá **pronto** estado.</span><span class="sxs-lookup"><span data-stu-id="08c78-142">You can see that hello copy activity ran successfully for hello last eight hours and produced hello slices in hello **Ready** state.</span></span>  

![Estado do pipeline de saudação](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="08c78-144">fatias de conjunto de dados de saudação na fábrica de dados Olá podem ter um dos Olá status a seguir:</span><span class="sxs-lookup"><span data-stu-id="08c78-144">hello dataset slices in hello data factory can have one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="08c78-145">Estado</span><span class="sxs-lookup"><span data-stu-id="08c78-145">State</span></span></th><th align="left"><span data-ttu-id="08c78-146">Subestado</span><span class="sxs-lookup"><span data-stu-id="08c78-146">Substate</span></span></th><th align="left"><span data-ttu-id="08c78-147">Descrição</span><span class="sxs-lookup"><span data-stu-id="08c78-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="08c78-148">Aguardando</span><span class="sxs-lookup"><span data-stu-id="08c78-148">Waiting</span></span></td><td><span data-ttu-id="08c78-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="08c78-149">ScheduleTime</span></span></td><td><span data-ttu-id="08c78-150">tempo de saudação não são fornecidos para Olá fatia toorun.</span><span class="sxs-lookup"><span data-stu-id="08c78-150">hello time hasn't come for hello slice toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="08c78-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="08c78-151">DatasetDependencies</span></span></td><td><span data-ttu-id="08c78-152">dependências de upstream Olá não estão prontas.</span><span class="sxs-lookup"><span data-stu-id="08c78-152">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="08c78-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="08c78-153">ComputeResources</span></span></td><td><span data-ttu-id="08c78-154">recursos de computação de saudação não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="08c78-154">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="08c78-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="08c78-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="08c78-156">Todas as instâncias do hello atividade estão ocupadas executando outras fatias.</span><span class="sxs-lookup"><span data-stu-id="08c78-156">All hello activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="08c78-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="08c78-157">ActivityResume</span></span></td><td><span data-ttu-id="08c78-158">atividade de saudação está em pausa e fatias Olá não pode ser executado até que a atividade de saudação é retomada.</span><span class="sxs-lookup"><span data-stu-id="08c78-158">hello activity is paused and can't run hello slices until hello activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="08c78-159">Retry</span><span class="sxs-lookup"><span data-stu-id="08c78-159">Retry</span></span></td><td><span data-ttu-id="08c78-160">A execução da atividade está sendo repetida.</span><span class="sxs-lookup"><span data-stu-id="08c78-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="08c78-161">Validação</span><span class="sxs-lookup"><span data-stu-id="08c78-161">Validation</span></span></td><td><span data-ttu-id="08c78-162">A validação ainda não foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="08c78-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="08c78-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="08c78-163">ValidationRetry</span></span></td><td><span data-ttu-id="08c78-164">A validação é toobe espera repetida.</span><span class="sxs-lookup"><span data-stu-id="08c78-164">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="08c78-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="08c78-165">InProgress</span></span></td><td><span data-ttu-id="08c78-166">Validando</span><span class="sxs-lookup"><span data-stu-id="08c78-166">Validating</span></span></td><td><span data-ttu-id="08c78-167">Validação em andamento.</span><span class="sxs-lookup"><span data-stu-id="08c78-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="08c78-168">fatia Hello está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="08c78-168">hello slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="08c78-169">Com falha</span><span class="sxs-lookup"><span data-stu-id="08c78-169">Failed</span></span></td><td><span data-ttu-id="08c78-170">TimedOut</span><span class="sxs-lookup"><span data-stu-id="08c78-170">TimedOut</span></span></td><td><span data-ttu-id="08c78-171">a execução da atividade Olá demorou mais do que o permitido pela atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-171">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="08c78-172">Cancelado</span><span class="sxs-lookup"><span data-stu-id="08c78-172">Canceled</span></span></td><td><span data-ttu-id="08c78-173">fatia Olá foi cancelada por ação do usuário.</span><span class="sxs-lookup"><span data-stu-id="08c78-173">hello slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="08c78-174">Validação</span><span class="sxs-lookup"><span data-stu-id="08c78-174">Validation</span></span></td><td><span data-ttu-id="08c78-175">A validação falhou.</span><span class="sxs-lookup"><span data-stu-id="08c78-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="08c78-176">fatia Olá falha toobe gerado e/ou validado.</span><span class="sxs-lookup"><span data-stu-id="08c78-176">hello slice failed toobe generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="08c78-177">Ready</span><span class="sxs-lookup"><span data-stu-id="08c78-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="08c78-178">fatia Hello está pronta para consumo.</span><span class="sxs-lookup"><span data-stu-id="08c78-178">hello slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="08c78-179">Ignorado</span><span class="sxs-lookup"><span data-stu-id="08c78-179">Skipped</span></span></td><td><span data-ttu-id="08c78-180">Nenhum</span><span class="sxs-lookup"><span data-stu-id="08c78-180">None</span></span></td><td><span data-ttu-id="08c78-181">fatia Olá não está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="08c78-181">hello slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="08c78-182">Nenhum</span><span class="sxs-lookup"><span data-stu-id="08c78-182">None</span></span></td><td>-</td><td><span data-ttu-id="08c78-183">Uma fatia usada tooexist com um status diferente, mas foi redefinida.</span><span class="sxs-lookup"><span data-stu-id="08c78-183">A slice used tooexist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="08c78-184">Você pode exibir detalhes de saudação sobre uma fatia, clicando em uma entrada de fatia Olá **recentemente atualizado fatias** folha.</span><span class="sxs-lookup"><span data-stu-id="08c78-184">You can view hello details about a slice by clicking a slice entry on hello **Recently Updated Slices** blade.</span></span>

![Detalhes da fatia](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="08c78-186">Se fatia Olá tiver sido executada várias vezes, você verá várias linhas de saudação **atividade é executada** lista.</span><span class="sxs-lookup"><span data-stu-id="08c78-186">If hello slice has been executed multiple times, you see multiple rows in hello **Activity runs** list.</span></span> <span data-ttu-id="08c78-187">Você pode exibir detalhes sobre uma atividade executar clicando em entrada hello executar Olá **atividade é executada** lista.</span><span class="sxs-lookup"><span data-stu-id="08c78-187">You can view details about an activity run by clicking hello run entry in hello **Activity runs** list.</span></span> <span data-ttu-id="08c78-188">lista de saudação mostra todos os arquivos de log hello, juntamente com uma mensagem de erro se houver um.</span><span class="sxs-lookup"><span data-stu-id="08c78-188">hello list shows all hello log files, along with an error message if there is one.</span></span> <span data-ttu-id="08c78-189">Esse recurso é útil logs tooview e depuração sem ter que tooleave sua fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="08c78-189">This feature is useful tooview and debug logs without having tooleave your data factory.</span></span>

![Detalhes da execução da atividade](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="08c78-191">Se não fatia Olá Olá **pronto** estado, você pode ver fatias de upstream Olá que não estão prontos e estão bloqueando a fatia atual Olá executadas em Olá **fatias de Upstream que não estão prontas** lista.</span><span class="sxs-lookup"><span data-stu-id="08c78-191">If hello slice isn't in hello **Ready** state, you can see hello upstream slices that aren't ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="08c78-192">Esse recurso é útil quando a fatia é em **esperando** estado e você desejar que toounderstand Olá dependências de upstream que Olá fatia está aguardando.</span><span class="sxs-lookup"><span data-stu-id="08c78-192">This feature is useful when your slice is in **Waiting** state and you want toounderstand hello upstream dependencies that hello slice is waiting on.</span></span>

![Fatias de upstream que não estão prontas](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="08c78-194">Diagrama de estado do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="08c78-194">Dataset state diagram</span></span>
<span data-ttu-id="08c78-195">Depois de implantar uma fábrica de dados e pipelines Olá têm um período de ativo válido, Olá dataset fatias de transição de um estado tooanother.</span><span class="sxs-lookup"><span data-stu-id="08c78-195">After you deploy a data factory and hello pipelines have a valid active period, hello dataset slices transition from one state tooanother.</span></span> <span data-ttu-id="08c78-196">Atualmente, status da fatia Olá segue Olá diagrama de estado a seguir:</span><span class="sxs-lookup"><span data-stu-id="08c78-196">Currently, hello slice status follows hello following state diagram:</span></span>

![Diagrama de estado](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="08c78-198">Olá, fluxo de transição de estado do conjunto de dados na fábrica de dados é a seguir Olá: espera -> em andamento/em execução (Validando) -> pronto/falha.</span><span class="sxs-lookup"><span data-stu-id="08c78-198">hello dataset state transition flow in data factory is hello following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="08c78-199">fatia Olá inicia em uma **esperando** estado, aguardando pré-condições toobe atendido antes de ele ser executado.</span><span class="sxs-lookup"><span data-stu-id="08c78-199">hello slice starts in a **Waiting** state, waiting for preconditions toobe met before it executes.</span></span> <span data-ttu-id="08c78-200">Em seguida, inicia a execução da atividade hello e fatia Olá entra em um **em andamento** estado.</span><span class="sxs-lookup"><span data-stu-id="08c78-200">Then, hello activity starts executing, and hello slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="08c78-201">a execução da atividade Olá pode ter êxito ou falhar.</span><span class="sxs-lookup"><span data-stu-id="08c78-201">hello activity execution might succeed or fail.</span></span> <span data-ttu-id="08c78-202">fatia Hello está marcada como **pronto** ou **falha**, com base no resultado de saudação da execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-202">hello slice is marked as **Ready** or **Failed**, based on hello result of hello execution.</span></span>

<span data-ttu-id="08c78-203">Você pode redefinir Olá fatia toogo da saudação **pronto** ou **falha** estado toohello **esperando** estado.</span><span class="sxs-lookup"><span data-stu-id="08c78-203">You can reset hello slice toogo back from hello **Ready** or **Failed** state toohello **Waiting** state.</span></span> <span data-ttu-id="08c78-204">Você também pode marcar o estado de fatia Olá muito**ignorar**, que impede que a atividade de saudação de execução e não processando fatia hello.</span><span class="sxs-lookup"><span data-stu-id="08c78-204">You can also mark hello slice state too**Skip**, which prevents hello activity from executing and not processing hello slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="08c78-205">Pausar e retomar pipelines</span><span class="sxs-lookup"><span data-stu-id="08c78-205">Pause and resume pipelines</span></span>
<span data-ttu-id="08c78-206">Você pode gerenciar seus pipelines usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08c78-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="08c78-207">Por exemplo, você pode pausar e retomar pipelines executando cmdlets do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08c78-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="08c78-208">modo de exibição de diagrama de saudação não dá suporte a pausa e retomada de pipelines.</span><span class="sxs-lookup"><span data-stu-id="08c78-208">hello diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="08c78-209">Se você quiser toouse uma interface do usuário, use Olá monitoramento e gerenciamento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08c78-209">If you want toouse an user interface, use hello monitoring and managing application.</span></span> <span data-ttu-id="08c78-210">Para obter detalhes sobre como usar o aplicativo hello, consulte [monitorar e gerenciar os pipelines de fábrica de dados usando o aplicativo de monitoramento e gerenciamento Olá](data-factory-monitor-manage-app.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="08c78-210">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="08c78-211">Você pode pausar/suspender pipelines usando Olá **AzureRmDataFactoryPipeline Suspend** cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08c78-211">You can pause/suspend pipelines by using hello **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="08c78-212">Esse cmdlet é útil quando você não deseja toorun seus pipelines até que um problema seja corrigido.</span><span class="sxs-lookup"><span data-stu-id="08c78-212">This cmdlet is useful when you don’t want toorun your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="08c78-213">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="08c78-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="08c78-214">Após Olá problema foi corrigido com pipeline hello, você pode retomar pipeline Olá suspenso executando Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="08c78-214">After hello issue has been fixed with hello pipeline, you can resume hello suspended pipeline by running hello following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="08c78-215">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="08c78-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="08c78-216">Depurar pipelines</span><span class="sxs-lookup"><span data-stu-id="08c78-216">Debug pipelines</span></span>
<span data-ttu-id="08c78-217">A fábrica de dados do Azure fornece recursos avançados para você toodebug e solucionar problemas de pipelines usando hello portal do Azure e o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08c78-217">Azure Data Factory provides rich capabilities for you toodebug and troubleshoot pipelines by using hello Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="08c78-218">[! Observe} é muito mais fácil tootroubleshot erros usando Olá monitoramento e gerenciamento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08c78-218">[!NOTE} It is much easier tootroubleshot errors using hello Monitoring & Management App.</span></span> <span data-ttu-id="08c78-219">Para obter detalhes sobre como usar o aplicativo hello, consulte [monitorar e gerenciar os pipelines de fábrica de dados usando o aplicativo de monitoramento e gerenciamento Olá](data-factory-monitor-manage-app.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="08c78-219">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="08c78-220">Localizar erros em um pipeline</span><span class="sxs-lookup"><span data-stu-id="08c78-220">Find errors in a pipeline</span></span>
<span data-ttu-id="08c78-221">Se a execução da atividade Olá falhar em um pipeline, Olá conjunto de dados que é produzido pelo pipeline de saudação está em um estado de erro devido a falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-221">If hello activity run fails in a pipeline, hello dataset that is produced by hello pipeline is in an error state because of hello failure.</span></span> <span data-ttu-id="08c78-222">Você pode depurar e solucionar problemas de erros na fábrica de dados do Azure usando Olá métodos a seguir.</span><span class="sxs-lookup"><span data-stu-id="08c78-222">You can debug and troubleshoot errors in Azure Data Factory by using hello following methods.</span></span>

#### <a name="use-hello-azure-portal-toodebug-an-error"></a><span data-ttu-id="08c78-223">Use Olá toodebug portal do Azure um erro</span><span class="sxs-lookup"><span data-stu-id="08c78-223">Use hello Azure portal toodebug an error</span></span>
1. <span data-ttu-id="08c78-224">Em Olá **tabela** folha, clique Olá problema fatia que tenha Olá **Status** definido muito**falha**.</span><span class="sxs-lookup"><span data-stu-id="08c78-224">On hello **Table** blade, click hello problem slice that has hello **Status** set too**Failed**.</span></span>

   ![Folha de tabela com fatia com problema](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="08c78-226">Em Olá **fatia de dados** folha, clique em que a falha de execução da atividade hello.</span><span class="sxs-lookup"><span data-stu-id="08c78-226">On hello **Data slice** blade, click hello activity run that failed.</span></span>

   ![Fatia de dados com erro](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="08c78-228">Em Olá **detalhes da execução de atividade** folha, você pode baixar arquivos de saudação que estão associados com o processamento do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="08c78-228">On hello **Activity run details** blade, you can download hello files that are associated with hello HDInsight processing.</span></span> <span data-ttu-id="08c78-229">Clique em **baixar** Status/stderr toodownload Olá erro arquivo de log que contém detalhes sobre o erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-229">Click **Download** for Status/stderr toodownload hello error log file that contains details about hello error.</span></span>

   ![Folha de detalhes da execução da atividade com erro](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a><span data-ttu-id="08c78-231">Use o PowerShell toodebug um erro</span><span class="sxs-lookup"><span data-stu-id="08c78-231">Use PowerShell toodebug an error</span></span>
1. <span data-ttu-id="08c78-232">Inicie o **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="08c78-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="08c78-233">Executar Olá **AzureRmDataFactorySlice Get** comando fatias de saudação toosee e seus status.</span><span class="sxs-lookup"><span data-stu-id="08c78-233">Run hello **Get-AzureRmDataFactorySlice** command toosee hello slices and their statuses.</span></span> <span data-ttu-id="08c78-234">Você deve ver uma fatia com o status de saudação do **falha**.</span><span class="sxs-lookup"><span data-stu-id="08c78-234">You should see a slice with hello status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="08c78-235">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="08c78-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="08c78-236">Substitua **StartDateTime** pela hora de início do pipeline.</span><span class="sxs-lookup"><span data-stu-id="08c78-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="08c78-237">Agora, execute Olá **AzureRmDataFactoryRun Get** cmdlet tooget detalhes sobre a atividade de saudação executar fatia hello.</span><span class="sxs-lookup"><span data-stu-id="08c78-237">Now, run hello **Get-AzureRmDataFactoryRun** cmdlet tooget details about hello activity run for hello slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="08c78-238">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="08c78-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="08c78-239">valor de saudação do StartDateTime é hora de início de saudação de fatia de erro/problema Olá que você anotou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="08c78-239">hello value of StartDateTime is hello start time for hello error/problem slice that you noted from hello previous step.</span></span> <span data-ttu-id="08c78-240">Olá data e hora deve ser colocada entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="08c78-240">hello date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="08c78-241">Você deve ver a saída com detalhes sobre o erro Olá a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="08c78-241">You should see output with details about hello error that is similar toohello following:</span></span>

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. <span data-ttu-id="08c78-242">Você pode executar Olá **salvar AzureRmDataFactoryLog** cmdlet com hello valor da Id que você consulte da saída de hello e baixar arquivos de log hello usando Olá **- DownloadLogsoption** Olá cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08c78-242">You can run hello **Save-AzureRmDataFactoryLog** cmdlet with hello Id value that you see from hello output, and download hello log files by using hello **-DownloadLogsoption** for hello cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="08c78-243">Executar novamente as falhas em um pipeline</span><span class="sxs-lookup"><span data-stu-id="08c78-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08c78-244">É mais fácil erros de tootroubleshoot e execute fatias com falha usando Olá monitoramento e gerenciamento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08c78-244">It's easier tootroubleshoot errors and rerun failed slices by using hello Monitoring & Management App.</span></span> <span data-ttu-id="08c78-245">Para obter detalhes sobre como usar o aplicativo hello, consulte [monitorar e gerenciar os pipelines de fábrica de dados usando o aplicativo de monitoramento e gerenciamento Olá](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="08c78-245">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-hello-azure-portal"></a><span data-ttu-id="08c78-246">Use Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="08c78-246">Use hello Azure portal</span></span>
<span data-ttu-id="08c78-247">Depois de solucionar problemas e falhas em um pipeline de depuração, você pode executar novamente falhas navegando toohello fatia de erro e clicando em Olá **executar** botão na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating toohello error slice and clicking hello **Run** button on hello command bar.</span></span>

![Executar novamente uma fatia com falha](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="08c78-249">Caso fatia Olá Falha na validação devido a uma falha de política (por exemplo, se dados não estiver disponíveis), você pode corrigir falha hello e valide novamente clicando em Olá **validar** botão na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-249">In case hello slice has failed validation because of a policy failure (for example, if data isn't available), you can fix hello failure and validate again by clicking hello **Validate** button on hello command bar.</span></span>

![Corrigir os erros e validar](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="08c78-251">Usar PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="08c78-251">Use Azure PowerShell</span></span>
<span data-ttu-id="08c78-252">Você pode executar novamente a falhas usando Olá **AzureRmDataFactorySliceStatus conjunto** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08c78-252">You can rerun failures by using hello **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="08c78-253">Consulte Olá [AzureRmDataFactorySliceStatus conjunto](https://msdn.microsoft.com/library/mt603522.aspx) tópico para sintaxe e outros detalhes sobre o cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="08c78-253">See hello [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about hello cmdlet.</span></span>

<span data-ttu-id="08c78-254">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="08c78-254">**Example:**</span></span>

<span data-ttu-id="08c78-255">Olá, exemplo a seguir define Olá status de todas as fatias de saudação tabela 'DAWikiAggregatedData' too'Waiting' hello Azure data Factory 'WikiADF'.</span><span class="sxs-lookup"><span data-stu-id="08c78-255">hello following example sets hello status of all slices for hello table 'DAWikiAggregatedData' too'Waiting' in hello Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="08c78-256">Olá 'Tipo de atualização' é definido too'UpstreamInPipeline ', que significa que o status de cada fatia para tabela hello e todas as tabelas (upstream) de dependente de saudação são definidas too'Waiting'.</span><span class="sxs-lookup"><span data-stu-id="08c78-256">hello 'UpdateType' is set too'UpstreamInPipeline', which means that statuses of each slice for hello table and all hello dependent (upstream) tables are set too'Waiting'.</span></span> <span data-ttu-id="08c78-257">Olá, outro valor possível para esse parâmetro é "Individual".</span><span class="sxs-lookup"><span data-stu-id="08c78-257">hello other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="08c78-258">Criar alertas</span><span class="sxs-lookup"><span data-stu-id="08c78-258">Create alerts</span></span>
<span data-ttu-id="08c78-259">O Azure registra eventos do usuário quando um recurso do Azure (por exemplo, Data Factory) é criado, atualizado ou excluído.</span><span class="sxs-lookup"><span data-stu-id="08c78-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="08c78-260">Você pode criar alertas para esses eventos.</span><span class="sxs-lookup"><span data-stu-id="08c78-260">You can create alerts on these events.</span></span> <span data-ttu-id="08c78-261">Você pode usar várias métricas de toocapture da fábrica de dados e criar alertas em métricas.</span><span class="sxs-lookup"><span data-stu-id="08c78-261">You can use Data Factory toocapture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="08c78-262">Recomendamos que você use os eventos para monitoramento em tempo real e métricas para fins de histórico.</span><span class="sxs-lookup"><span data-stu-id="08c78-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="08c78-263">Alertas de eventos</span><span class="sxs-lookup"><span data-stu-id="08c78-263">Alerts on events</span></span>
<span data-ttu-id="08c78-264">Eventos do Azure fornecem percepções úteis sobre o que está acontecendo em seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="08c78-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="08c78-265">Ao usar o Azure Data Factory, os eventos são gerados quando:</span><span class="sxs-lookup"><span data-stu-id="08c78-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="08c78-266">Um data factory é criado, atualizado ou excluído.</span><span class="sxs-lookup"><span data-stu-id="08c78-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="08c78-267">O processamento de dados (como "execuções") foi iniciado ou concluído.</span><span class="sxs-lookup"><span data-stu-id="08c78-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="08c78-268">Um cluster de HDInsight sob demanda é criado ou removido.</span><span class="sxs-lookup"><span data-stu-id="08c78-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="08c78-269">Você pode criar alertas nesses eventos de usuário e configurá-los toosend administrador de toohello de notificações de email e coadministrators de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-269">You can create alerts on these user events and configure them toosend email notifications toohello administrator and coadministrators of hello subscription.</span></span> <span data-ttu-id="08c78-270">Além disso, você pode especificar endereços de email adicionais de usuários que precisam de notificações de email tooreceive quando Olá condições forem atendidas.</span><span class="sxs-lookup"><span data-stu-id="08c78-270">In addition, you can specify additional email addresses of users who need tooreceive email notifications when hello conditions are met.</span></span> <span data-ttu-id="08c78-271">Esse recurso é útil quando você deseja tooget notificado sobre as falhas e não quiser que o monitor de toocontinuously sua fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="08c78-271">This feature is useful when you want tooget notified on failures and don’t want toocontinuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="08c78-272">Atualmente, portal de saudação não mostra alertas em eventos.</span><span class="sxs-lookup"><span data-stu-id="08c78-272">Currently, hello portal doesn't show alerts on events.</span></span> <span data-ttu-id="08c78-273">Saudação de uso [monitoramento e gerenciamento de aplicativo](data-factory-monitor-manage-app.md) toosee todos os alertas.</span><span class="sxs-lookup"><span data-stu-id="08c78-273">Use hello [Monitoring and Management app](data-factory-monitor-manage-app.md) toosee all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="08c78-274">Especificar uma definição de alerta</span><span class="sxs-lookup"><span data-stu-id="08c78-274">Specify an alert definition</span></span>
<span data-ttu-id="08c78-275">toospecify uma definição de alerta, você criar um arquivo JSON que descreve as operações de saudação que você deseja toobe alertado no.</span><span class="sxs-lookup"><span data-stu-id="08c78-275">toospecify an alert definition, you create a JSON file that describes hello operations that you want toobe alerted on.</span></span> <span data-ttu-id="08c78-276">Saudação de exemplo a seguir, alerta Olá envia uma notificação por email para Olá RunFinished operação.</span><span class="sxs-lookup"><span data-stu-id="08c78-276">In hello following example, hello alert sends an email notification for hello RunFinished operation.</span></span> <span data-ttu-id="08c78-277">toobe específico, uma notificação por email é enviada quando uma execução de fábrica de dados Olá foi concluída e Olá executar falhou (Status = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="08c78-277">toobe specific, an email notification is sent when a run in hello data factory has completed and hello run has failed (Status = FailedExecution).</span></span>

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

<span data-ttu-id="08c78-278">Você pode remover **subStatus** de saudação definição JSON se você não quiser toobe alertado sobre uma falha específica.</span><span class="sxs-lookup"><span data-stu-id="08c78-278">You can remove **subStatus** from hello JSON definition if you don’t want toobe alerted on a specific failure.</span></span>

<span data-ttu-id="08c78-279">Este exemplo define o alerta de saudação para todas as fábricas de dados em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="08c78-279">This example sets up hello alert for all data factories in your subscription.</span></span> <span data-ttu-id="08c78-280">Se você quiser Olá toobe alerta configurado para uma fábrica de dados específico, você pode especificar a fábrica de dados **resourceUri** em Olá **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="08c78-280">If you want hello alert toobe set up for a particular data factory, you can specify data factory **resourceUri** in hello **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="08c78-281">Olá, tabela a seguir fornece Olá lista de operações disponíveis e status (e substatus).</span><span class="sxs-lookup"><span data-stu-id="08c78-281">hello following table provides hello list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="08c78-282">Nome da operação</span><span class="sxs-lookup"><span data-stu-id="08c78-282">Operation name</span></span> | <span data-ttu-id="08c78-283">Status</span><span class="sxs-lookup"><span data-stu-id="08c78-283">Status</span></span> | <span data-ttu-id="08c78-284">Substatus</span><span class="sxs-lookup"><span data-stu-id="08c78-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08c78-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="08c78-285">RunStarted</span></span> |<span data-ttu-id="08c78-286">Iniciado</span><span class="sxs-lookup"><span data-stu-id="08c78-286">Started</span></span> |<span data-ttu-id="08c78-287">Iniciando</span><span class="sxs-lookup"><span data-stu-id="08c78-287">Starting</span></span> |
| <span data-ttu-id="08c78-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="08c78-288">RunFinished</span></span> |<span data-ttu-id="08c78-289">Falhou / Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="08c78-289">Failed / Succeeded</span></span> |<span data-ttu-id="08c78-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="08c78-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="08c78-291">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="08c78-291">Succeeded</span></span><br/><br/><span data-ttu-id="08c78-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="08c78-292">FailedExecution</span></span><br/><br/><span data-ttu-id="08c78-293">TimedOut</span><span class="sxs-lookup"><span data-stu-id="08c78-293">TimedOut</span></span><br/><br/><span data-ttu-id="08c78-294"><Cancelado</span><span class="sxs-lookup"><span data-stu-id="08c78-294"><Canceled</span></span><br/><br/><span data-ttu-id="08c78-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="08c78-295">FailedValidation</span></span><br/><br/><span data-ttu-id="08c78-296">Abandoned</span><span class="sxs-lookup"><span data-stu-id="08c78-296">Abandoned</span></span> |
| <span data-ttu-id="08c78-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="08c78-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="08c78-298">Iniciado</span><span class="sxs-lookup"><span data-stu-id="08c78-298">Started</span></span> | |
| <span data-ttu-id="08c78-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="08c78-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="08c78-300">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="08c78-300">Succeeded</span></span> | |
| <span data-ttu-id="08c78-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="08c78-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="08c78-302">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="08c78-302">Succeeded</span></span> | |

<span data-ttu-id="08c78-303">Consulte [criar regra de alerta](https://msdn.microsoft.com/library/azure/dn510366.aspx) para obter detalhes sobre os elementos JSON Olá que são usados no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="08c78-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about hello JSON elements that are used in hello example.</span></span>

#### <a name="deploy-hello-alert"></a><span data-ttu-id="08c78-304">Implantar o alerta Olá</span><span class="sxs-lookup"><span data-stu-id="08c78-304">Deploy hello alert</span></span>
<span data-ttu-id="08c78-305">alerta de Olá toodeploy, use o cmdlet do hello Azure PowerShell **AzureRmResourceGroupDeployment novo**, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="08c78-305">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="08c78-306">Após a implantação do grupo de recursos de saudação foi concluído com êxito, você verá Olá mensagens a seguir:</span><span class="sxs-lookup"><span data-stu-id="08c78-306">After hello resource group deployment has finished successfully, you see hello following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> <span data-ttu-id="08c78-307">Você pode usar o hello [criar regra de alerta](https://msdn.microsoft.com/library/azure/dn510366.aspx) API REST toocreate uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="08c78-307">You can use hello [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate an alert rule.</span></span> <span data-ttu-id="08c78-308">carga JSON Olá é exemplo JSON toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="08c78-308">hello JSON payload is similar toohello JSON example.</span></span>  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a><span data-ttu-id="08c78-309">Recuperar a lista de saudação de implantações de grupos de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="08c78-309">Retrieve hello list of Azure resource group deployments</span></span>
<span data-ttu-id="08c78-310">lista de saudação tooretrieve de implantado implantações de grupos de recursos do Azure, use o cmdlet Olá **Get-AzureRmResourceGroupDeployment**, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="08c78-310">tooretrieve hello list of deployed Azure resource group deployments, use hello cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="08c78-311">Solucionar problemas de eventos de usuário</span><span class="sxs-lookup"><span data-stu-id="08c78-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="08c78-312">Você pode ver todos os eventos de saudação que são gerados depois de clicar em Olá **métricas e operações** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="08c78-312">You can see all hello events that are generated after clicking hello **Metrics and operations** tile.</span></span>

    ![Bloco Métricas e operações](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="08c78-314">Clique em Olá **eventos** eventos de saudação toosee lado a lado.</span><span class="sxs-lookup"><span data-stu-id="08c78-314">Click hello **Events** tile toosee hello events.</span></span>

    ![Bloco de eventos](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="08c78-316">Em Olá **eventos** folha, você pode ver detalhes sobre eventos, eventos filtrados e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="08c78-316">On hello **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Folha Eventos](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="08c78-318">Clique em uma **operação** na lista de operações de saudação que causa um erro.</span><span class="sxs-lookup"><span data-stu-id="08c78-318">Click an **Operation** in hello operations list that causes an error.</span></span>

    ![Selecionar uma operação](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="08c78-320">Clique em uma **erro** detalhes do evento toosee sobre o erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-320">Click an **Error** event toosee details about hello error.</span></span>

    ![Erro de evento](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="08c78-322">Consulte [cmdlets do Azure Insight](https://msdn.microsoft.com/library/mt282452.aspx) cmdlets do PowerShell que você pode usar tooadd, obter ou remover alertas.</span><span class="sxs-lookup"><span data-stu-id="08c78-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use tooadd, get, or remove alerts.</span></span> <span data-ttu-id="08c78-323">Aqui estão alguns exemplos de como usar o hello **AlertRule Get** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="08c78-323">Here are a few examples of using hello **Get-AlertRule** cmdlet:</span></span>

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

<span data-ttu-id="08c78-324">Execute Olá detalhes de toosee comandos get-help e exemplos para Olá Get-AlertRule cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="08c78-324">Run hello following get-help commands toosee details and examples for hello Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="08c78-325">Se ocorrerem eventos de geração de alerta Olá Olá portal folha, mas você não recebe notificações por email, verifique se o endereço de email de saudação especificado está definido tooreceive emails de remetentes externos.</span><span class="sxs-lookup"><span data-stu-id="08c78-325">If you see hello alert generation events on hello portal blade but you don't receive email notifications, check whether hello email address that is specified is set tooreceive emails from external senders.</span></span> <span data-ttu-id="08c78-326">emails de alerta Olá podem ter bloqueados por suas configurações de email.</span><span class="sxs-lookup"><span data-stu-id="08c78-326">hello alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="08c78-327">Alertas sobre métricas</span><span class="sxs-lookup"><span data-stu-id="08c78-327">Alerts on metrics</span></span>
<span data-ttu-id="08c78-328">No Data Factory, você pode capturar várias métricas e criar alertas sobre as métricas.</span><span class="sxs-lookup"><span data-stu-id="08c78-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="08c78-329">Você pode monitorar e criar alertas em Olá métricas para fatias Olá sua fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="08c78-329">You can monitor and create alerts on hello following metrics for hello slices in your data factory:</span></span>

* <span data-ttu-id="08c78-330">**Execuções com falha**</span><span class="sxs-lookup"><span data-stu-id="08c78-330">**Failed Runs**</span></span>
* <span data-ttu-id="08c78-331">**Execuções com êxito**</span><span class="sxs-lookup"><span data-stu-id="08c78-331">**Successful Runs**</span></span>

<span data-ttu-id="08c78-332">Essas métricas são úteis e ajudarão-lo a tooget que uma visão geral de geral com falha e bem-sucedida é executado na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="08c78-332">These metrics are useful and help you tooget an overview of overall failed and successful runs in hello data factory.</span></span> <span data-ttu-id="08c78-333">Métricas são emitidas sempre que há uma fatia de execução.</span><span class="sxs-lookup"><span data-stu-id="08c78-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="08c78-334">No início de saudação de hora hello, essas métricas são agregadas e enviados por push tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="08c78-334">At hello beginning of hello hour, these metrics are aggregated and pushed tooyour storage account.</span></span> <span data-ttu-id="08c78-335">métricas de tooenable, configure uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="08c78-335">tooenable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="08c78-336">Habilitar a métrica</span><span class="sxs-lookup"><span data-stu-id="08c78-336">Enable metrics</span></span>
<span data-ttu-id="08c78-337">tooenable métricas, clique em seguinte de saudação do hello **Data Factory** folha:</span><span class="sxs-lookup"><span data-stu-id="08c78-337">tooenable metrics, click hello following from hello **Data Factory** blade:</span></span>

<span data-ttu-id="08c78-338">**Monitoramento** > **Métrica** > **Configurações de diagnóstico** > **Diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="08c78-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Link de diagnóstico](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="08c78-340">Em Olá **diagnóstico** folha, clique em **na**, selecione a conta de armazenamento hello e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="08c78-340">On hello **Diagnostics** blade, click **On**, select hello storage account, and click **Save**.</span></span>

![Folha de diagnósticos](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="08c78-342">Pode levar até tooone horas para Olá métricas toobe visível em hello **monitoramento** folha porque a agregação de métricas acontece por hora.</span><span class="sxs-lookup"><span data-stu-id="08c78-342">It might take up tooone hour for hello metrics toobe visible on hello **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="08c78-343">Configurar alertas sobre métricas</span><span class="sxs-lookup"><span data-stu-id="08c78-343">Set up an alert on metrics</span></span>
<span data-ttu-id="08c78-344">Clique em Olá **métricas de fábrica de dados** lado a lado:</span><span class="sxs-lookup"><span data-stu-id="08c78-344">Click hello **Data Factory metrics** tile:</span></span>

![Bloco Métricas de data factory](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="08c78-346">Em Olá **métrica** folha, clique em **+ adicionar alerta** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-346">On hello **Metric** blade, click **+ Add alert** on hello toolbar.</span></span>
<span data-ttu-id="08c78-347">![Folha Métricas do data factory > Adicionar alerta](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="08c78-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="08c78-348">Em Olá **adicionar uma regra de alerta** página Olá etapas a seguir e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="08c78-348">On hello **Add an alert rule** page, do hello following steps, and click **OK**.</span></span>

* <span data-ttu-id="08c78-349">Insira um nome para o alerta de saudação (exemplo: "Falha no alerta").</span><span class="sxs-lookup"><span data-stu-id="08c78-349">Enter a name for hello alert (example: "failed alert").</span></span>
* <span data-ttu-id="08c78-350">Insira uma descrição do alerta de saudação (exemplo: "enviar um email quando ocorre uma falha").</span><span class="sxs-lookup"><span data-stu-id="08c78-350">Enter a description for hello alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="08c78-351">Selecione uma métrica ("Execuções com falha" versus "Execuções com êxito").</span><span class="sxs-lookup"><span data-stu-id="08c78-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="08c78-352">Especifique uma condição e um valor de limite.</span><span class="sxs-lookup"><span data-stu-id="08c78-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="08c78-353">Especifica Olá período de tempo.</span><span class="sxs-lookup"><span data-stu-id="08c78-353">Specify hello period of time.</span></span>
* <span data-ttu-id="08c78-354">Especifique se deve ser enviado um email tooowners, colaboradores e leitores.</span><span class="sxs-lookup"><span data-stu-id="08c78-354">Specify whether an email should be sent tooowners, contributors, and readers.</span></span>

![Folha Métricas de data factory > Adicionar regra de alerta](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="08c78-356">Depois de regra de alerta de saudação é adicionada com êxito, folha Olá fecha e ver o novo alerta de saudação em Olá **métrica** folha.</span><span class="sxs-lookup"><span data-stu-id="08c78-356">After hello alert rule is added successfully, hello blade closes and you see hello new alert on hello **Metric** blade.</span></span>

![Folha Métrica do data factory > Novo alerta adicionado](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="08c78-358">Você também deve ver o número de saudação de alertas no hello **regras de alerta** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="08c78-358">You should also see hello number of alerts in hello **Alert rules** tile.</span></span> <span data-ttu-id="08c78-359">Clique em Olá **regras de alerta** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="08c78-359">Click hello **Alert rules** tile.</span></span>

![Folha Métrica de data factory - Regras de alerta](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="08c78-361">Em Olá **alertas regras** folha, consulte todos os alertas existentes.</span><span class="sxs-lookup"><span data-stu-id="08c78-361">On hello **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="08c78-362">tooadd um alerta, clique em **adicionar alerta** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-362">tooadd an alert, click **Add alert** on hello toolbar.</span></span>

![Folha Regras de alerta](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="08c78-364">Notificações de alerta</span><span class="sxs-lookup"><span data-stu-id="08c78-364">Alert notifications</span></span>
<span data-ttu-id="08c78-365">Depois de regra de alerta Olá corresponde a condição de saudação, você deve obter um email informando Olá alerta for ativado.</span><span class="sxs-lookup"><span data-stu-id="08c78-365">After hello alert rule matches hello condition, you should get an email that says hello alert is activated.</span></span> <span data-ttu-id="08c78-366">Depois de Olá resolvido e a condição de alerta de saudação não corresponde mais, você obterá um email informando Olá alerta é resolvido.</span><span class="sxs-lookup"><span data-stu-id="08c78-366">After hello issue is resolved and hello alert condition doesn’t match anymore, you get an email that says hello alert is resolved.</span></span>

<span data-ttu-id="08c78-367">Esse comportamento é diferente dos eventos, para os quais uma notificação é enviada em cada falha para a qual a regra de alerta se qualifica.</span><span class="sxs-lookup"><span data-stu-id="08c78-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="08c78-368">Implantar alertas usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="08c78-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="08c78-369">Você pode implantar os alertas para métricas Olá mesma maneira que faria para eventos.</span><span class="sxs-lookup"><span data-stu-id="08c78-369">You can deploy alerts for metrics hello same way that you do for events.</span></span>

<span data-ttu-id="08c78-370">**Definição do alerta**</span><span class="sxs-lookup"><span data-stu-id="08c78-370">**Alert definition**</span></span>

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

<span data-ttu-id="08c78-371">Substituir *subscriptionId*, *resourceGroupName*, e *dataFactoryName* no exemplo hello com valores apropriados.</span><span class="sxs-lookup"><span data-stu-id="08c78-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in hello sample with appropriate values.</span></span>

<span data-ttu-id="08c78-372">No momento, *metricName* dá suporte a dois valores:</span><span class="sxs-lookup"><span data-stu-id="08c78-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="08c78-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="08c78-373">FailedRuns</span></span>
* <span data-ttu-id="08c78-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="08c78-374">SuccessfulRuns</span></span>

<span data-ttu-id="08c78-375">**Implantar o alerta Olá**</span><span class="sxs-lookup"><span data-stu-id="08c78-375">**Deploy hello alert**</span></span>

<span data-ttu-id="08c78-376">alerta de Olá toodeploy, use o cmdlet do hello Azure PowerShell **AzureRmResourceGroupDeployment novo**, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="08c78-376">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="08c78-377">Você verá a seguinte mensagem após uma implantação bem-sucedida:</span><span class="sxs-lookup"><span data-stu-id="08c78-377">You should see following message after a successful deployment:</span></span>

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

<span data-ttu-id="08c78-378">Você também pode usar o hello **AlertRule adicionar** cmdlet toodeploy uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="08c78-378">You can also use hello **Add-AlertRule** cmdlet toodeploy an alert rule.</span></span> <span data-ttu-id="08c78-379">Consulte Olá [AlertRule adicionar](https://msdn.microsoft.com/library/mt282468.aspx) tópico para obter detalhes e exemplos.</span><span class="sxs-lookup"><span data-stu-id="08c78-379">See hello [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a><span data-ttu-id="08c78-380">Mover um grupo de recursos diferente de tooa de fábrica de dados ou a assinatura</span><span class="sxs-lookup"><span data-stu-id="08c78-380">Move a data factory tooa different resource group or subscription</span></span>
<span data-ttu-id="08c78-381">Você pode mover um grupo de recursos diferentes de tooa de fábrica de dados ou uma assinatura diferente usando Olá **mover** botão Olá home page de sua fábrica de dados de barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="08c78-381">You can move a data factory tooa different resource group or a different subscription by using hello **Move** command bar button on hello home page of your data factory.</span></span>

![Mover o Data Factory](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="08c78-383">Você também pode mover os recursos relacionados (como alertas que estão associados a fábrica de dados Olá), juntamente com a fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="08c78-383">You can also move any related resources (such as alerts that are associated with hello data factory), along with hello data factory.</span></span>

![Caixa de diálogo Mover recursos](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
