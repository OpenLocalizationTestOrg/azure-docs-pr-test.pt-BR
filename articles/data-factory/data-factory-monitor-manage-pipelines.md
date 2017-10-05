---
title: Monitorar e gerenciar pipelines usando o Portal do Azure e o PowerShell | Microsoft Docs
description: "Saiba como usar o Portal do Azure e o Azure PowerShell para monitorar e gerenciar as data factories e os pipelines do Azure que você criou."
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
ms.openlocfilehash: 61bb5379cd94dd00814e14420947e7783999ff0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-azure-portal-and-powershell"></a><span data-ttu-id="86b8a-103">Monitorar e gerenciar os pipelines do Azure Data Factory usando o Portal do Azure e o PowerShell</span><span class="sxs-lookup"><span data-stu-id="86b8a-103">Monitor and manage Azure Data Factory pipelines by using the Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="86b8a-104">Usando o Portal do Azure/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="86b8a-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="86b8a-105">Usando o aplicativo de Monitoramento e Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="86b8a-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="86b8a-106">O aplicativo de monitoramento e gerenciamento fornece um melhor suporte para monitorar e gerenciar seus pipelines de dados e solucionar os problemas.</span><span class="sxs-lookup"><span data-stu-id="86b8a-106">The monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="86b8a-107">Para obter detalhes sobre como usar o aplicativo, consulte [Monitorar e gerenciar os pipelines do Data Factory usando o aplicativo de Monitoramento e Gerenciamento](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="86b8a-107">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="86b8a-108">Este artigo descreve como monitorar, gerenciar e depurar seus pipelines usando o portal do Azure e o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86b8a-108">This article describes how to monitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="86b8a-109">Também fornece informações sobre como criar alertas e ser notificado sobre falhas.</span><span class="sxs-lookup"><span data-stu-id="86b8a-109">The article also provides information on how to create alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="86b8a-110">Entenda os pipelines e os estados de atividade</span><span class="sxs-lookup"><span data-stu-id="86b8a-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="86b8a-111">No Portal do Azure, você pode:</span><span class="sxs-lookup"><span data-stu-id="86b8a-111">By using the Azure portal, you can:</span></span>

* <span data-ttu-id="86b8a-112">Exibir sua data factory como um diagrama.</span><span class="sxs-lookup"><span data-stu-id="86b8a-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="86b8a-113">Exibir atividades dentro de um pipeline.</span><span class="sxs-lookup"><span data-stu-id="86b8a-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="86b8a-114">Exibir conjuntos de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="86b8a-114">View input and output datasets.</span></span>

<span data-ttu-id="86b8a-115">Esta seção também descreve como uma fatia do conjunto de dados faz a transição de um estado para outro.</span><span class="sxs-lookup"><span data-stu-id="86b8a-115">This section also describes how a dataset slice transitions from one state to another state.</span></span>   

### <a name="navigate-to-your-data-factory"></a><span data-ttu-id="86b8a-116">Navegue até sua data factory</span><span class="sxs-lookup"><span data-stu-id="86b8a-116">Navigate to your data factory</span></span>
1. <span data-ttu-id="86b8a-117">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="86b8a-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="86b8a-118">Clique em **Data factories** no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="86b8a-118">Click **Data factories** on the menu on the left.</span></span> <span data-ttu-id="86b8a-119">Se você não o vir, clique em **Mais serviços >**e clique em **Data factories** na categoria **INTELIGÊNCIA + ANÁLISE**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-119">If you don't see it, click **More services >**, and then click **Data factories** under the **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Procurar tudo > Data factories](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="86b8a-121">Na folha **Data factories**, selecione o data factory no qual você está interessado.</span><span class="sxs-lookup"><span data-stu-id="86b8a-121">On the **Data factories** blade, select the data factory that you're interested in.</span></span>

    ![Selecionar o data factory](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="86b8a-123">Você deverá ver a home page do data factory.</span><span class="sxs-lookup"><span data-stu-id="86b8a-123">You should see the home page for the data factory.</span></span>

   ![Folha Data factory](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="86b8a-125">Modo de exibição de diagrama de uma data factory</span><span class="sxs-lookup"><span data-stu-id="86b8a-125">Diagram view of your data factory</span></span>
<span data-ttu-id="86b8a-126">O modo de exibição de **Diagrama** de uma data factory fornece um único painel onde você pode monitorar e gerenciar o data factory e seus ativos.</span><span class="sxs-lookup"><span data-stu-id="86b8a-126">The **Diagram** view of a data factory provides a single pane of glass to monitor and manage the data factory and its assets.</span></span> <span data-ttu-id="86b8a-127">Para ver o modo de exibição de **Diagrama** de seu data factory, clique em **Diagrama** na home page do data factory.</span><span class="sxs-lookup"><span data-stu-id="86b8a-127">To see the **Diagram** view of your data factory, click **Diagram** on the home page for the data factory.</span></span>

![Exibição de diagrama](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="86b8a-129">Você pode ampliar, reduzir, ajustar o nível de zoom, aplicar zoom para 100%, bloquear o layout do diagrama e posicionar pipelines e conjuntos de dados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="86b8a-129">You can zoom in, zoom out, zoom to fit, zoom to 100%, lock the layout of the diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="86b8a-130">Você também pode ver as informações de linhagem de dados (ou seja, mostrar itens upstream e downstream dos itens selecionados).</span><span class="sxs-lookup"><span data-stu-id="86b8a-130">You can also see the data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="86b8a-131">Atividades dentro de um pipeline</span><span class="sxs-lookup"><span data-stu-id="86b8a-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="86b8a-132">Clique com o botão direito do mouse no pipeline e depois clique em **Abrir pipeline** para ver todas as atividades no pipeline junto com conjuntos de dados de entrada e saída para as atividades.</span><span class="sxs-lookup"><span data-stu-id="86b8a-132">Right-click the pipeline, and then click **Open pipeline** to see all activities in the pipeline, along with input and output datasets for the activities.</span></span> <span data-ttu-id="86b8a-133">Esse recurso é útil quando o pipeline é composto por mais de uma atividade, e você deseja compreender a linhagem operacional de um único pipeline.</span><span class="sxs-lookup"><span data-stu-id="86b8a-133">This feature is useful when your pipeline includes more than one activity and you want to understand the operational lineage of a single pipeline.</span></span>

    ![Menu do pipeline aberto](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="86b8a-135">No exemplo a seguir, você vê uma atividade de cópia no pipeline com uma entrada e uma saída.</span><span class="sxs-lookup"><span data-stu-id="86b8a-135">In the following example, you see a copy activity in the pipeline with an input and an output.</span></span> 

    ![Atividades dentro de um pipeline](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="86b8a-137">Você pode voltar à home page do data factory clicando no link **Data factory** na trilha no canto superior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="86b8a-137">You can navigate back to the home page of the data factory by clicking the **Data factory** link in the breadcrumb at the top-left corner.</span></span>

    ![Navegue de volta para a data factory](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-the-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="86b8a-139">Exibir o estado de cada atividade dentro de um pipeline</span><span class="sxs-lookup"><span data-stu-id="86b8a-139">View the state of each activity inside a pipeline</span></span>
<span data-ttu-id="86b8a-140">Veja o estado atual de uma atividade exibindo o status de qualquer um dos conjuntos de dados produzidos pela atividade.</span><span class="sxs-lookup"><span data-stu-id="86b8a-140">You can view the current state of an activity by viewing the status of any of the datasets that are produced by the activity.</span></span>

<span data-ttu-id="86b8a-141">Clicar duas vezes em **OutputBlobTable** no **Diagrama** exibirá todas as fatias produzidas por diferentes execuções de atividade dentro de um pipeline.</span><span class="sxs-lookup"><span data-stu-id="86b8a-141">By double-clicking the **OutputBlobTable** in the **Diagram**, you can see all the slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="86b8a-142">Você pode ver que a atividade de cópia foi executada com êxito pelas últimas oito horas e produziu as fatias com estado **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-142">You can see that the copy activity ran successfully for the last eight hours and produced the slices in the **Ready** state.</span></span>  

![Estado do pipeline](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="86b8a-144">As fatias do conjunto de dados no data factory podem ter um dos seguintes status:</span><span class="sxs-lookup"><span data-stu-id="86b8a-144">The dataset slices in the data factory can have one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="86b8a-145">Estado</span><span class="sxs-lookup"><span data-stu-id="86b8a-145">State</span></span></th><th align="left"><span data-ttu-id="86b8a-146">Subestado</span><span class="sxs-lookup"><span data-stu-id="86b8a-146">Substate</span></span></th><th align="left"><span data-ttu-id="86b8a-147">Descrição</span><span class="sxs-lookup"><span data-stu-id="86b8a-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="86b8a-148">Aguardando</span><span class="sxs-lookup"><span data-stu-id="86b8a-148">Waiting</span></span></td><td><span data-ttu-id="86b8a-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="86b8a-149">ScheduleTime</span></span></td><td><span data-ttu-id="86b8a-150">Não chegou o momento de execução da fatia.</span><span class="sxs-lookup"><span data-stu-id="86b8a-150">The time hasn't come for the slice to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="86b8a-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="86b8a-151">DatasetDependencies</span></span></td><td><span data-ttu-id="86b8a-152">As dependências de upstream não estão prontas.</span><span class="sxs-lookup"><span data-stu-id="86b8a-152">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="86b8a-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="86b8a-153">ComputeResources</span></span></td><td><span data-ttu-id="86b8a-154">Os recursos de computação não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="86b8a-154">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="86b8a-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="86b8a-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="86b8a-156">Todas as instâncias de atividade estão ocupadas executando outras fatias.</span><span class="sxs-lookup"><span data-stu-id="86b8a-156">All the activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="86b8a-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="86b8a-157">ActivityResume</span></span></td><td><span data-ttu-id="86b8a-158">A atividade está em pausa e não pode executar as fatias até que a atividades seja retomada.</span><span class="sxs-lookup"><span data-stu-id="86b8a-158">The activity is paused and can't run the slices until the activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="86b8a-159">Retry</span><span class="sxs-lookup"><span data-stu-id="86b8a-159">Retry</span></span></td><td><span data-ttu-id="86b8a-160">A execução da atividade está sendo repetida.</span><span class="sxs-lookup"><span data-stu-id="86b8a-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="86b8a-161">Validação</span><span class="sxs-lookup"><span data-stu-id="86b8a-161">Validation</span></span></td><td><span data-ttu-id="86b8a-162">A validação ainda não foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="86b8a-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="86b8a-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="86b8a-163">ValidationRetry</span></span></td><td><span data-ttu-id="86b8a-164">A validação está aguardando para ser repetida.</span><span class="sxs-lookup"><span data-stu-id="86b8a-164">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="86b8a-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="86b8a-165">InProgress</span></span></td><td><span data-ttu-id="86b8a-166">Validando</span><span class="sxs-lookup"><span data-stu-id="86b8a-166">Validating</span></span></td><td><span data-ttu-id="86b8a-167">Validação em andamento.</span><span class="sxs-lookup"><span data-stu-id="86b8a-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="86b8a-168">A fatia está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="86b8a-168">The slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="86b8a-169">Falha</span><span class="sxs-lookup"><span data-stu-id="86b8a-169">Failed</span></span></td><td><span data-ttu-id="86b8a-170">TimedOut</span><span class="sxs-lookup"><span data-stu-id="86b8a-170">TimedOut</span></span></td><td><span data-ttu-id="86b8a-171">A execução demorou mais do que o permitido pela atividade.</span><span class="sxs-lookup"><span data-stu-id="86b8a-171">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="86b8a-172">Cancelado</span><span class="sxs-lookup"><span data-stu-id="86b8a-172">Canceled</span></span></td><td><span data-ttu-id="86b8a-173">A fatia foi cancelada por ação do usuário.</span><span class="sxs-lookup"><span data-stu-id="86b8a-173">The slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="86b8a-174">Validação</span><span class="sxs-lookup"><span data-stu-id="86b8a-174">Validation</span></span></td><td><span data-ttu-id="86b8a-175">A validação falhou.</span><span class="sxs-lookup"><span data-stu-id="86b8a-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="86b8a-176">Não foi possível gerar e/ou validar a fatia.</span><span class="sxs-lookup"><span data-stu-id="86b8a-176">The slice failed to be generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="86b8a-177">Ready</span><span class="sxs-lookup"><span data-stu-id="86b8a-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="86b8a-178">A fatia está pronta para consumo.</span><span class="sxs-lookup"><span data-stu-id="86b8a-178">The slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="86b8a-179">Ignorado</span><span class="sxs-lookup"><span data-stu-id="86b8a-179">Skipped</span></span></td><td><span data-ttu-id="86b8a-180">Nenhum</span><span class="sxs-lookup"><span data-stu-id="86b8a-180">None</span></span></td><td><span data-ttu-id="86b8a-181">A fatia não está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="86b8a-181">The slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="86b8a-182">Nenhum</span><span class="sxs-lookup"><span data-stu-id="86b8a-182">None</span></span></td><td>-</td><td><span data-ttu-id="86b8a-183">Uma fatia costumava existir com um status diferente, mas foi redefinida.</span><span class="sxs-lookup"><span data-stu-id="86b8a-183">A slice used to exist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="86b8a-184">Veja os detalhes de uma fatia clicando em uma entrada de fatia na folha **Fatias Atualizadas Recentemente** .</span><span class="sxs-lookup"><span data-stu-id="86b8a-184">You can view the details about a slice by clicking a slice entry on the **Recently Updated Slices** blade.</span></span>

![Detalhes da fatia](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="86b8a-186">Se a fatia tiver sido executada várias vezes, você verá várias linhas na lista **Execuções de atividade** .</span><span class="sxs-lookup"><span data-stu-id="86b8a-186">If the slice has been executed multiple times, you see multiple rows in the **Activity runs** list.</span></span> <span data-ttu-id="86b8a-187">Você pode exibir detalhes sobre uma execução de atividade clicando na entrada da execução na lista **Execuções de atividade** .</span><span class="sxs-lookup"><span data-stu-id="86b8a-187">You can view details about an activity run by clicking the run entry in the **Activity runs** list.</span></span> <span data-ttu-id="86b8a-188">A lista mostra todos os arquivos de log, junto com uma mensagem de erro, se houver.</span><span class="sxs-lookup"><span data-stu-id="86b8a-188">The list shows all the log files, along with an error message if there is one.</span></span> <span data-ttu-id="86b8a-189">Esse recurso é útil para exibir e depurar logs sem precisar sair de sua data factory.</span><span class="sxs-lookup"><span data-stu-id="86b8a-189">This feature is useful to view and debug logs without having to leave your data factory.</span></span>

![Detalhes da execução da atividade](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="86b8a-191">Quando a fatia não está no estado **Pronto**, você pode ver as fatias upstream que não estão prontas e estão impedindo a execução da fatia atual na lista **Fatias upstream que não estão prontas**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-191">If the slice isn't in the **Ready** state, you can see the upstream slices that aren't ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="86b8a-192">Esse recurso é útil quando a fatia estiver no estado **Aguardando** e você quiser entender as dependências de upstream em que a fatia está aguardando.</span><span class="sxs-lookup"><span data-stu-id="86b8a-192">This feature is useful when your slice is in **Waiting** state and you want to understand the upstream dependencies that the slice is waiting on.</span></span>

![Fatias de upstream que não estão prontas](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="86b8a-194">Diagrama de estado do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="86b8a-194">Dataset state diagram</span></span>
<span data-ttu-id="86b8a-195">Após a implantação de uma data factory e a atribuição de um período de atividade válido para os pipelines, as fatias do conjunto de dados fazem a transição de um estado para outro.</span><span class="sxs-lookup"><span data-stu-id="86b8a-195">After you deploy a data factory and the pipelines have a valid active period, the dataset slices transition from one state to another.</span></span> <span data-ttu-id="86b8a-196">Atualmente, o status da fatia segue o seguinte diagrama de estado:</span><span class="sxs-lookup"><span data-stu-id="86b8a-196">Currently, the slice status follows the following state diagram:</span></span>

![Diagrama de estado](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="86b8a-198">O fluxo de transição de estado do conjunto de dados no data factory é o seguinte: Waiting-> In-Progress/In-Progress (Validating) -> Ready/Failed.</span><span class="sxs-lookup"><span data-stu-id="86b8a-198">The dataset state transition flow in data factory is the following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="86b8a-199">A fatia começa em um estado de **Aguardando**, esperando pelo atendimento de pré-condições antes da execução.</span><span class="sxs-lookup"><span data-stu-id="86b8a-199">The slice starts in a **Waiting** state, waiting for preconditions to be met before it executes.</span></span> <span data-ttu-id="86b8a-200">Depois disso, a atividade começa a ser executada e a fatia passa para um estado **Em Andamento** .</span><span class="sxs-lookup"><span data-stu-id="86b8a-200">Then, the activity starts executing, and the slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="86b8a-201">A execução da atividade pode ser bem-sucedida ou falhar.</span><span class="sxs-lookup"><span data-stu-id="86b8a-201">The activity execution might succeed or fail.</span></span> <span data-ttu-id="86b8a-202">A fatia é marcada como **Pronta** ou **Falha** com base no resultado da execução.</span><span class="sxs-lookup"><span data-stu-id="86b8a-202">The slice is marked as **Ready** or **Failed**, based on the result of the execution.</span></span>

<span data-ttu-id="86b8a-203">Você pode redefinir a fatia para voltar do estado **Pronto** ou **Falha** para o estado **Aguardando**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-203">You can reset the slice to go back from the **Ready** or **Failed** state to the **Waiting** state.</span></span> <span data-ttu-id="86b8a-204">Você também pode marcar o estado da fatia como **Ignorar**, o que impedirá a execução da atividade e não processará a fatia.</span><span class="sxs-lookup"><span data-stu-id="86b8a-204">You can also mark the slice state to **Skip**, which prevents the activity from executing and not processing the slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="86b8a-205">Pausar e retomar pipelines</span><span class="sxs-lookup"><span data-stu-id="86b8a-205">Pause and resume pipelines</span></span>
<span data-ttu-id="86b8a-206">Você pode gerenciar seus pipelines usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86b8a-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="86b8a-207">Por exemplo, você pode pausar e retomar pipelines executando cmdlets do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86b8a-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="86b8a-208">A exibição de diagrama não dá suporte à pausa e continuação de pipelines.</span><span class="sxs-lookup"><span data-stu-id="86b8a-208">The diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="86b8a-209">Se você desejar usar uma interface do usuário, use o aplicativo de monitoramento e gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="86b8a-209">If you want to use an user interface, use the monitoring and managing application.</span></span> <span data-ttu-id="86b8a-210">Para obter detalhes sobre como usar o aplicativo, consulte o artigo [Monitorar e gerenciar os pipelines do Data Factory usando o aplicativo de Monitoramento e Gerenciamento](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="86b8a-210">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="86b8a-211">Você pode pausar/suspender pipelines usando o cmdlet **Suspend-AzureDataFactoryPipeline** do Powershell.</span><span class="sxs-lookup"><span data-stu-id="86b8a-211">You can pause/suspend pipelines by using the **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="86b8a-212">Esse cmdlet é útil quando você não quiser executar o pipeline até que um problema seja corrigido.</span><span class="sxs-lookup"><span data-stu-id="86b8a-212">This cmdlet is useful when you don’t want to run your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="86b8a-213">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="86b8a-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="86b8a-214">Depois que o problema com o pipeline for corrigido, você poderá retomar o pipeline suspenso executando o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="86b8a-214">After the issue has been fixed with the pipeline, you can resume the suspended pipeline by running the following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="86b8a-215">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="86b8a-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="86b8a-216">Depurar pipelines</span><span class="sxs-lookup"><span data-stu-id="86b8a-216">Debug pipelines</span></span>
<span data-ttu-id="86b8a-217">O Azure Data Factory fornece recursos avançados para depurar e solucionar problemas com pipelines usando do Portal do Azure e o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86b8a-217">Azure Data Factory provides rich capabilities for you to debug and troubleshoot pipelines by using the Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="86b8a-218">[!NOTE] É muito mais fácil resolver erros usando o Aplicativo de Monitoramento e Gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="86b8a-218">[!NOTE} It is much easier to troubleshot errors using the Monitoring & Management App.</span></span> <span data-ttu-id="86b8a-219">Para obter detalhes sobre como usar o aplicativo, consulte o artigo [Monitorar e gerenciar os pipelines do Data Factory usando o aplicativo de Monitoramento e Gerenciamento](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="86b8a-219">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="86b8a-220">Localizar erros em um pipeline</span><span class="sxs-lookup"><span data-stu-id="86b8a-220">Find errors in a pipeline</span></span>
<span data-ttu-id="86b8a-221">Se a execução da atividade falhar em um pipeline, o conjunto de dados produzido pelo pipeline ficará em um estado de erro devido à falha.</span><span class="sxs-lookup"><span data-stu-id="86b8a-221">If the activity run fails in a pipeline, the dataset that is produced by the pipeline is in an error state because of the failure.</span></span> <span data-ttu-id="86b8a-222">Você pode depurar e solucionar erros no Azure Data Factory usando os seguintes métodos.</span><span class="sxs-lookup"><span data-stu-id="86b8a-222">You can debug and troubleshoot errors in Azure Data Factory by using the following methods.</span></span>

#### <a name="use-the-azure-portal-to-debug-an-error"></a><span data-ttu-id="86b8a-223">Usar o Portal do Azure para depurar um erro</span><span class="sxs-lookup"><span data-stu-id="86b8a-223">Use the Azure portal to debug an error</span></span>
1. <span data-ttu-id="86b8a-224">Na folha **Tabela**, clique na fatia de problema com o **Status** definido como **Falha**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-224">On the **Table** blade, click the problem slice that has the **Status** set to **Failed**.</span></span>

   ![Folha de tabela com fatia com problema](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="86b8a-226">Na folha **Fatia de dados**, clique na execução de atividade com falha.</span><span class="sxs-lookup"><span data-stu-id="86b8a-226">On the **Data slice** blade, click the activity run that failed.</span></span>

   ![Fatia de dados com erro](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="86b8a-228">Na folha **Detalhes de execução da atividade**, você pode baixar os arquivos associados ao processamento do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86b8a-228">On the **Activity run details** blade, you can download the files that are associated with the HDInsight processing.</span></span> <span data-ttu-id="86b8a-229">Clique em **Download** para que Status/stderr baixe o arquivo de log de erros que contém detalhes sobre o erro.</span><span class="sxs-lookup"><span data-stu-id="86b8a-229">Click **Download** for Status/stderr to download the error log file that contains details about the error.</span></span>

   ![Folha de detalhes da execução da atividade com erro](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-to-debug-an-error"></a><span data-ttu-id="86b8a-231">Usar o PowerShell para depurar um erro</span><span class="sxs-lookup"><span data-stu-id="86b8a-231">Use PowerShell to debug an error</span></span>
1. <span data-ttu-id="86b8a-232">Inicie o **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="86b8a-233">Execute o comando **Get-AzureDataFactorySlice** para ver as fatias e seus status.</span><span class="sxs-lookup"><span data-stu-id="86b8a-233">Run the **Get-AzureRmDataFactorySlice** command to see the slices and their statuses.</span></span> <span data-ttu-id="86b8a-234">Você deve ver uma fatia com o status **Falha**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-234">You should see a slice with the status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="86b8a-235">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="86b8a-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="86b8a-236">Substitua **StartDateTime** pela hora de início do pipeline.</span><span class="sxs-lookup"><span data-stu-id="86b8a-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="86b8a-237">Agora, execute o cmdlet **Get-AzureRmDataFactoryRun** para obter detalhes sobre a execução da atividade para a fatia.</span><span class="sxs-lookup"><span data-stu-id="86b8a-237">Now, run the **Get-AzureRmDataFactoryRun** cmdlet to get details about the activity run for the slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="86b8a-238">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="86b8a-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="86b8a-239">O valor de StartDateTime é a hora de início do erro/fatia com problema observada na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="86b8a-239">The value of StartDateTime is the start time for the error/problem slice that you noted from the previous step.</span></span> <span data-ttu-id="86b8a-240">A data e hora devem ser colocadas entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="86b8a-240">The date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="86b8a-241">Você deve ver uma saída semelhante à seguinte com detalhes sobre o erro:</span><span class="sxs-lookup"><span data-stu-id="86b8a-241">You should see output with details about the error that is similar to the following:</span></span>

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
5. <span data-ttu-id="86b8a-242">Você pode executar o cmdlet **Save-AzureRmDataFactoryLog** com o valor de Id que você vê na saída e baixar os arquivos de log usando a opção **-DownloadLogsoption** para o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="86b8a-242">You can run the **Save-AzureRmDataFactoryLog** cmdlet with the Id value that you see from the output, and download the log files by using the **-DownloadLogsoption** for the cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="86b8a-243">Executar novamente as falhas em um pipeline</span><span class="sxs-lookup"><span data-stu-id="86b8a-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86b8a-244">É mais fácil resolver erros e executar novamente as fatias com falha usando o Aplicativo de Monitoramento e Gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="86b8a-244">It's easier to troubleshoot errors and rerun failed slices by using the Monitoring & Management App.</span></span> <span data-ttu-id="86b8a-245">Para obter detalhes sobre como usar o aplicativo, consulte [Monitorar e gerenciar os pipelines do Data Factory usando o aplicativo de Monitoramento e Gerenciamento](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="86b8a-245">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-the-azure-portal"></a><span data-ttu-id="86b8a-246">Use o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="86b8a-246">Use the Azure portal</span></span>
<span data-ttu-id="86b8a-247">Depois de solucionar problemas e depurar falhas em um pipeline, você pode executar as falhas novamente navegando até a fatia com erro e clicando no botão **Executar** na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="86b8a-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating to the error slice and clicking the **Run** button on the command bar.</span></span>

![Executar novamente uma fatia com falha](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="86b8a-249">Em caso de falha na validação da fatia devido a uma falha de política (por exemplo, se nenhum dado estiver disponível), é possível corrigir a falha e validar novamente clicando no botão **Validar** na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="86b8a-249">In case the slice has failed validation because of a policy failure (for example, if data isn't available), you can fix the failure and validate again by clicking the **Validate** button on the command bar.</span></span>

![Corrigir os erros e validar](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="86b8a-251">Usar PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="86b8a-251">Use Azure PowerShell</span></span>
<span data-ttu-id="86b8a-252">Você pode executar novamente as falhas usando o cmdlet **Set-AzureRmDataFactorySliceStatus**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-252">You can rerun failures by using the **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="86b8a-253">Confira o tópico [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) para obter a sintaxe e outros detalhes sobre o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="86b8a-253">See the [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about the cmdlet.</span></span>

<span data-ttu-id="86b8a-254">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86b8a-254">**Example:**</span></span>

<span data-ttu-id="86b8a-255">O exemplo a seguir define o status de todas as fatias da tabela "DAWikiAggregatedData" como "Aguardando" no Azure Data Factory "WikiADF".</span><span class="sxs-lookup"><span data-stu-id="86b8a-255">The following example sets the status of all slices for the table 'DAWikiAggregatedData' to 'Waiting' in the Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="86b8a-256">UpdateType é definido como UpstreamInPipeline, o que significa que o status de cada fatia da tabela e todas as tabelas dependentes (upstream) é definido como "Aguardando".</span><span class="sxs-lookup"><span data-stu-id="86b8a-256">The 'UpdateType' is set to 'UpstreamInPipeline', which means that statuses of each slice for the table and all the dependent (upstream) tables are set to 'Waiting'.</span></span> <span data-ttu-id="86b8a-257">O outro valor possível para esse parâmetro é "Individual".</span><span class="sxs-lookup"><span data-stu-id="86b8a-257">The other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="86b8a-258">Criar alertas</span><span class="sxs-lookup"><span data-stu-id="86b8a-258">Create alerts</span></span>
<span data-ttu-id="86b8a-259">O Azure registra eventos do usuário quando um recurso do Azure (por exemplo, Data Factory) é criado, atualizado ou excluído.</span><span class="sxs-lookup"><span data-stu-id="86b8a-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="86b8a-260">Você pode criar alertas para esses eventos.</span><span class="sxs-lookup"><span data-stu-id="86b8a-260">You can create alerts on these events.</span></span> <span data-ttu-id="86b8a-261">Use o Data Factory para capturar várias métricas e criar alertas para as métricas.</span><span class="sxs-lookup"><span data-stu-id="86b8a-261">You can use Data Factory to capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="86b8a-262">Recomendamos que você use os eventos para monitoramento em tempo real e métricas para fins de histórico.</span><span class="sxs-lookup"><span data-stu-id="86b8a-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="86b8a-263">Alertas de eventos</span><span class="sxs-lookup"><span data-stu-id="86b8a-263">Alerts on events</span></span>
<span data-ttu-id="86b8a-264">Eventos do Azure fornecem percepções úteis sobre o que está acontecendo em seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="86b8a-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="86b8a-265">Ao usar o Azure Data Factory, os eventos são gerados quando:</span><span class="sxs-lookup"><span data-stu-id="86b8a-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="86b8a-266">Um data factory é criado, atualizado ou excluído.</span><span class="sxs-lookup"><span data-stu-id="86b8a-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="86b8a-267">O processamento de dados (como "execuções") foi iniciado ou concluído.</span><span class="sxs-lookup"><span data-stu-id="86b8a-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="86b8a-268">Um cluster de HDInsight sob demanda é criado ou removido.</span><span class="sxs-lookup"><span data-stu-id="86b8a-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="86b8a-269">Você pode criar alertas para esses eventos de usuário e configurá-los para enviar notificações por email para o administrador e os coadministradores da assinatura.</span><span class="sxs-lookup"><span data-stu-id="86b8a-269">You can create alerts on these user events and configure them to send email notifications to the administrator and coadministrators of the subscription.</span></span> <span data-ttu-id="86b8a-270">Além disso, você pode especificar endereços de email adicionais de usuários que precisem receber notificações por email quando as condições forem atendidas.</span><span class="sxs-lookup"><span data-stu-id="86b8a-270">In addition, you can specify additional email addresses of users who need to receive email notifications when the conditions are met.</span></span> <span data-ttu-id="86b8a-271">Esse recurso é útil quando você deseja ser notificado sobre falhas e não quer monitorar continuamente sua data factory.</span><span class="sxs-lookup"><span data-stu-id="86b8a-271">This feature is useful when you want to get notified on failures and don’t want to continuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="86b8a-272">Atualmente, o portal não mostra alertas em eventos.</span><span class="sxs-lookup"><span data-stu-id="86b8a-272">Currently, the portal doesn't show alerts on events.</span></span> <span data-ttu-id="86b8a-273">Use o [Aplicativo de Monitoramento e Gerenciamento](data-factory-monitor-manage-app.md) para ver todos os alertas.</span><span class="sxs-lookup"><span data-stu-id="86b8a-273">Use the [Monitoring and Management app](data-factory-monitor-manage-app.md) to see all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="86b8a-274">Especificar uma definição de alerta</span><span class="sxs-lookup"><span data-stu-id="86b8a-274">Specify an alert definition</span></span>
<span data-ttu-id="86b8a-275">Para especificar uma definição de alerta, crie um arquivo JSON que descreva as operações sobre as quais você deseja ser alertado.</span><span class="sxs-lookup"><span data-stu-id="86b8a-275">To specify an alert definition, you create a JSON file that describes the operations that you want to be alerted on.</span></span> <span data-ttu-id="86b8a-276">No exemplo a seguir, o alerta enviará uma notificação por email para a operação RunFinished.</span><span class="sxs-lookup"><span data-stu-id="86b8a-276">In the following example, the alert sends an email notification for the RunFinished operation.</span></span> <span data-ttu-id="86b8a-277">Para ser específico, uma notificação por email será enviado quando uma execução no Data Factory for concluída e essa execução falhar (Status = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="86b8a-277">To be specific, an email notification is sent when a run in the data factory has completed and the run has failed (Status = FailedExecution).</span></span>

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
                "description": "One or more of the data slices for the Azure Data Factory has failed processing.",
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

<span data-ttu-id="86b8a-278">Remova **subStatus** da definição do JSON acima se você não quiser receber um alerta sobre uma falha específica.</span><span class="sxs-lookup"><span data-stu-id="86b8a-278">You can remove **subStatus** from the JSON definition if you don’t want to be alerted on a specific failure.</span></span>

<span data-ttu-id="86b8a-279">Esse exemplo configura o alerta para todas as fábricas de dados em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="86b8a-279">This example sets up the alert for all data factories in your subscription.</span></span> <span data-ttu-id="86b8a-280">Se você quiser que o alerta seja configurado para um data factory específico, será possível especificar o **resourceUri** do data factory no bloco **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="86b8a-280">If you want the alert to be set up for a particular data factory, you can specify data factory **resourceUri** in the **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="86b8a-281">A tabela a seguir fornece a lista de operações e status (e substatus) disponíveis.</span><span class="sxs-lookup"><span data-stu-id="86b8a-281">The following table provides the list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="86b8a-282">Nome da operação</span><span class="sxs-lookup"><span data-stu-id="86b8a-282">Operation name</span></span> | <span data-ttu-id="86b8a-283">Status</span><span class="sxs-lookup"><span data-stu-id="86b8a-283">Status</span></span> | <span data-ttu-id="86b8a-284">Substatus</span><span class="sxs-lookup"><span data-stu-id="86b8a-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="86b8a-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="86b8a-285">RunStarted</span></span> |<span data-ttu-id="86b8a-286">Iniciado</span><span class="sxs-lookup"><span data-stu-id="86b8a-286">Started</span></span> |<span data-ttu-id="86b8a-287">Iniciando</span><span class="sxs-lookup"><span data-stu-id="86b8a-287">Starting</span></span> |
| <span data-ttu-id="86b8a-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="86b8a-288">RunFinished</span></span> |<span data-ttu-id="86b8a-289">Falhou / Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="86b8a-289">Failed / Succeeded</span></span> |<span data-ttu-id="86b8a-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="86b8a-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="86b8a-291">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="86b8a-291">Succeeded</span></span><br/><br/><span data-ttu-id="86b8a-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="86b8a-292">FailedExecution</span></span><br/><br/><span data-ttu-id="86b8a-293">TimedOut</span><span class="sxs-lookup"><span data-stu-id="86b8a-293">TimedOut</span></span><br/><br/><span data-ttu-id="86b8a-294"><Cancelado</span><span class="sxs-lookup"><span data-stu-id="86b8a-294"><Canceled</span></span><br/><br/><span data-ttu-id="86b8a-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="86b8a-295">FailedValidation</span></span><br/><br/><span data-ttu-id="86b8a-296">Abandoned</span><span class="sxs-lookup"><span data-stu-id="86b8a-296">Abandoned</span></span> |
| <span data-ttu-id="86b8a-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="86b8a-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="86b8a-298">Iniciado</span><span class="sxs-lookup"><span data-stu-id="86b8a-298">Started</span></span> | |
| <span data-ttu-id="86b8a-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="86b8a-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="86b8a-300">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="86b8a-300">Succeeded</span></span> | |
| <span data-ttu-id="86b8a-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="86b8a-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="86b8a-302">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="86b8a-302">Succeeded</span></span> | |

<span data-ttu-id="86b8a-303">Veja [Criar Regra de Alerta](https://msdn.microsoft.com/library/azure/dn510366.aspx) para obter detalhes sobre os elementos JSON usados no exemplo.</span><span class="sxs-lookup"><span data-stu-id="86b8a-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about the JSON elements that are used in the example.</span></span>

#### <a name="deploy-the-alert"></a><span data-ttu-id="86b8a-304">Implantar o alerta</span><span class="sxs-lookup"><span data-stu-id="86b8a-304">Deploy the alert</span></span>
<span data-ttu-id="86b8a-305">Para implantar o alerta, use o cmdlet do Azure PowerShell: **New-AzureRmResourceGroupDeployment**, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="86b8a-305">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="86b8a-306">Após a implantação do grupo de recursos, você verá as seguintes mensagens:</span><span class="sxs-lookup"><span data-stu-id="86b8a-306">After the resource group deployment has finished successfully, you see the following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - The StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts to remove this parameter.
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
> <span data-ttu-id="86b8a-307">Você pode usar a API REST [Criar Regra de Alerta](https://msdn.microsoft.com/library/azure/dn510366.aspx) para criar uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="86b8a-307">You can use the [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API to create an alert rule.</span></span> <span data-ttu-id="86b8a-308">O conteúdo JSON é semelhante ao exemplo JSON.</span><span class="sxs-lookup"><span data-stu-id="86b8a-308">The JSON payload is similar to the JSON example.</span></span>  


#### <a name="retrieve-the-list-of-azure-resource-group-deployments"></a><span data-ttu-id="86b8a-309">Recuperar a lista de implantações de grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="86b8a-309">Retrieve the list of Azure resource group deployments</span></span>
<span data-ttu-id="86b8a-310">Para recuperar a lista de implantações já realizadas do grupo de recursos do Azure, use o cmdlet **Get-AzureRmResourceGroupDeployment**, conforme mostra o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="86b8a-310">To retrieve the list of deployed Azure resource group deployments, use the cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

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

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="86b8a-311">Solucionar problemas de eventos de usuário</span><span class="sxs-lookup"><span data-stu-id="86b8a-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="86b8a-312">Veja todos os eventos gerados depois de clicar no bloco **Métricas e operações**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-312">You can see all the events that are generated after clicking the **Metrics and operations** tile.</span></span>

    ![Bloco Métricas e operações](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="86b8a-314">Clique no bloco **Eventos** para ver os eventos.</span><span class="sxs-lookup"><span data-stu-id="86b8a-314">Click the **Events** tile to see the events.</span></span>

    ![Bloco de eventos](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="86b8a-316">Na folha **Eventos**, veja detalhes sobre eventos, eventos filtrados e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="86b8a-316">On the **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Folha Eventos](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="86b8a-318">Clique em uma **Operação** na lista de operações que causam um erro.</span><span class="sxs-lookup"><span data-stu-id="86b8a-318">Click an **Operation** in the operations list that causes an error.</span></span>

    ![Selecionar uma operação](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="86b8a-320">Clique em um evento de **Erro** para ver detalhes sobre o erro.</span><span class="sxs-lookup"><span data-stu-id="86b8a-320">Click an **Error** event to see details about the error.</span></span>

    ![Erro de evento](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="86b8a-322">Confira [Cmdlets do Azure Insight](https://msdn.microsoft.com/library/mt282452.aspx) para ver os cmdlets do PowerShell que você pode usar para adicionar, obter ou remover alertas.</span><span class="sxs-lookup"><span data-stu-id="86b8a-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use to add, get, or remove alerts.</span></span> <span data-ttu-id="86b8a-323">Aqui estão alguns exemplos de como usar o cmdlet **Get-AlertRule** :</span><span class="sxs-lookup"><span data-stu-id="86b8a-323">Here are a few examples of using the **Get-AlertRule** cmdlet:</span></span>

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
Description : One or more of the data slices for the Azure Data Factory has failed processing.
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

<span data-ttu-id="86b8a-324">Execute os seguintes comandos get-help para ver detalhes e exemplos para o cmdlet Get-AlertRule.</span><span class="sxs-lookup"><span data-stu-id="86b8a-324">Run the following get-help commands to see details and examples for the Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="86b8a-325">Se você vir os eventos de geração de alerta na folha do portal, mas não receber notificações por email, verifique se o endereço de email especificado está configurado para receber emails de remetentes externos.</span><span class="sxs-lookup"><span data-stu-id="86b8a-325">If you see the alert generation events on the portal blade but you don't receive email notifications, check whether the email address that is specified is set to receive emails from external senders.</span></span> <span data-ttu-id="86b8a-326">Os emails de alerta podem ter sido bloqueados por suas configurações de email.</span><span class="sxs-lookup"><span data-stu-id="86b8a-326">The alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="86b8a-327">Alertas sobre métricas</span><span class="sxs-lookup"><span data-stu-id="86b8a-327">Alerts on metrics</span></span>
<span data-ttu-id="86b8a-328">No Data Factory, você pode capturar várias métricas e criar alertas sobre as métricas.</span><span class="sxs-lookup"><span data-stu-id="86b8a-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="86b8a-329">Você pode monitorar e criar alertas nas seguintes métricas para as fatias em seu data factory:</span><span class="sxs-lookup"><span data-stu-id="86b8a-329">You can monitor and create alerts on the following metrics for the slices in your data factory:</span></span>

* <span data-ttu-id="86b8a-330">**Execuções com falha**</span><span class="sxs-lookup"><span data-stu-id="86b8a-330">**Failed Runs**</span></span>
* <span data-ttu-id="86b8a-331">**Execuções com êxito**</span><span class="sxs-lookup"><span data-stu-id="86b8a-331">**Successful Runs**</span></span>

<span data-ttu-id="86b8a-332">Essas métricas são úteis e ajudam você a ter uma visão geral das execuções com falha e êxito em seu data factory.</span><span class="sxs-lookup"><span data-stu-id="86b8a-332">These metrics are useful and help you to get an overview of overall failed and successful runs in the data factory.</span></span> <span data-ttu-id="86b8a-333">Métricas são emitidas sempre que há uma fatia de execução.</span><span class="sxs-lookup"><span data-stu-id="86b8a-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="86b8a-334">No início de uma hora, essas métricas são agregadas e enviadas para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="86b8a-334">At the beginning of the hour, these metrics are aggregated and pushed to your storage account.</span></span> <span data-ttu-id="86b8a-335">Para habilitar as métricas, configure uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="86b8a-335">To enable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="86b8a-336">Habilitar a métrica</span><span class="sxs-lookup"><span data-stu-id="86b8a-336">Enable metrics</span></span>
<span data-ttu-id="86b8a-337">Para habilitar as métricas, clique no seguinte na folha do **Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="86b8a-337">To enable metrics, click the following from the **Data Factory** blade:</span></span>

<span data-ttu-id="86b8a-338">**Monitoramento** > **Métrica** > **Configurações de diagnóstico** > **Diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="86b8a-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Link de diagnóstico](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="86b8a-340">Na folha **Diagnóstico**, clique em **Ativar**, selecione a conta de armazenamento e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-340">On the **Diagnostics** blade, click **On**, select the storage account, and click **Save**.</span></span>

![Folha de diagnósticos](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="86b8a-342">Talvez demore até uma hora para que as métricas fiquem visíveis na folha **Monitoramento**, porque a agregação de métricas acontece de hora em hora.</span><span class="sxs-lookup"><span data-stu-id="86b8a-342">It might take up to one hour for the metrics to be visible on the **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="86b8a-343">Configurar alertas sobre métricas</span><span class="sxs-lookup"><span data-stu-id="86b8a-343">Set up an alert on metrics</span></span>
<span data-ttu-id="86b8a-344">Clique no bloco **Métricas do Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="86b8a-344">Click the **Data Factory metrics** tile:</span></span>

![Bloco Métricas de data factory](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="86b8a-346">Na folha **Métrica**, clique em **+ Adicionar alerta** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="86b8a-346">On the **Metric** blade, click **+ Add alert** on the toolbar.</span></span>
<span data-ttu-id="86b8a-347">![Folha Métricas do data factory > Adicionar alerta](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="86b8a-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="86b8a-348">Na página **Adicionar uma regra de alerta**, siga as etapas a seguir e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-348">On the **Add an alert rule** page, do the following steps, and click **OK**.</span></span>

* <span data-ttu-id="86b8a-349">Insira um nome para o alerta (exemplo: "alerta de falha").</span><span class="sxs-lookup"><span data-stu-id="86b8a-349">Enter a name for the alert (example: "failed alert").</span></span>
* <span data-ttu-id="86b8a-350">Insira uma descrição para o alerta (exemplo: "enviar um email quando ocorre uma falha").</span><span class="sxs-lookup"><span data-stu-id="86b8a-350">Enter a description for the alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="86b8a-351">Selecione uma métrica ("Execuções com falha" versus "Execuções com êxito").</span><span class="sxs-lookup"><span data-stu-id="86b8a-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="86b8a-352">Especifique uma condição e um valor de limite.</span><span class="sxs-lookup"><span data-stu-id="86b8a-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="86b8a-353">Especifique o período.</span><span class="sxs-lookup"><span data-stu-id="86b8a-353">Specify the period of time.</span></span>
* <span data-ttu-id="86b8a-354">Especifique se um email deve ser enviado para proprietários, colaboradores e leitores.</span><span class="sxs-lookup"><span data-stu-id="86b8a-354">Specify whether an email should be sent to owners, contributors, and readers.</span></span>

![Folha Métricas de data factory > Adicionar regra de alerta](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="86b8a-356">Após a adição da regra, a folha fechará e você verá o novo alerta na folha **Métrica**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-356">After the alert rule is added successfully, the blade closes and you see the new alert on the **Metric** blade.</span></span>

![Folha Métrica do data factory > Novo alerta adicionado](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="86b8a-358">Você também verá o número de alertas no bloco **Regras de alerta**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-358">You should also see the number of alerts in the **Alert rules** tile.</span></span> <span data-ttu-id="86b8a-359">Clique no bloco **Regras de alerta**.</span><span class="sxs-lookup"><span data-stu-id="86b8a-359">Click the **Alert rules** tile.</span></span>

![Folha Métrica de data factory - Regras de alerta](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="86b8a-361">Na folha **Regras de alertas**, você verá todos os alertas existentes.</span><span class="sxs-lookup"><span data-stu-id="86b8a-361">On the **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="86b8a-362">Para adicionar um alerta, clique em **Adicionar alerta** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="86b8a-362">To add an alert, click **Add alert** on the toolbar.</span></span>

![Folha Regras de alerta](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="86b8a-364">Notificações de alerta</span><span class="sxs-lookup"><span data-stu-id="86b8a-364">Alert notifications</span></span>
<span data-ttu-id="86b8a-365">Quando a regra de alerta corresponder à condição, você deverá receber um email informando que o alerta está ativo.</span><span class="sxs-lookup"><span data-stu-id="86b8a-365">After the alert rule matches the condition, you should get an email that says the alert is activated.</span></span> <span data-ttu-id="86b8a-366">Depois que o problema for resolvido e a condição do alerta deixar de corresponder, você receberá um email informando que o alerta foi resolvido.</span><span class="sxs-lookup"><span data-stu-id="86b8a-366">After the issue is resolved and the alert condition doesn’t match anymore, you get an email that says the alert is resolved.</span></span>

<span data-ttu-id="86b8a-367">Esse comportamento é diferente dos eventos, para os quais uma notificação é enviada em cada falha para a qual a regra de alerta se qualifica.</span><span class="sxs-lookup"><span data-stu-id="86b8a-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="86b8a-368">Implantar alertas usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="86b8a-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="86b8a-369">Você pode implantar alertas para métricas da mesma maneira que faz para eventos.</span><span class="sxs-lookup"><span data-stu-id="86b8a-369">You can deploy alerts for metrics the same way that you do for events.</span></span>

<span data-ttu-id="86b8a-370">**Definição do alerta**</span><span class="sxs-lookup"><span data-stu-id="86b8a-370">**Alert definition**</span></span>

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

<span data-ttu-id="86b8a-371">Substitua *subscriptionId*, *resourceGroupName* e *dataFactoryName* no exemplo pelos valores adequados.</span><span class="sxs-lookup"><span data-stu-id="86b8a-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in the sample with appropriate values.</span></span>

<span data-ttu-id="86b8a-372">No momento, *metricName* dá suporte a dois valores:</span><span class="sxs-lookup"><span data-stu-id="86b8a-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="86b8a-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="86b8a-373">FailedRuns</span></span>
* <span data-ttu-id="86b8a-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="86b8a-374">SuccessfulRuns</span></span>

<span data-ttu-id="86b8a-375">**Implantar o alerta**</span><span class="sxs-lookup"><span data-stu-id="86b8a-375">**Deploy the alert**</span></span>

<span data-ttu-id="86b8a-376">Para implantar o alerta, use o cmdlet do Azure PowerShell: **New-AzureRmResourceGroupDeployment**, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="86b8a-376">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="86b8a-377">Você verá a seguinte mensagem após uma implantação bem-sucedida:</span><span class="sxs-lookup"><span data-stu-id="86b8a-377">You should see following message after a successful deployment:</span></span>

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

<span data-ttu-id="86b8a-378">Você também usar o cmdlet **Add-AlertRule** para implantar uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="86b8a-378">You can also use the **Add-AlertRule** cmdlet to deploy an alert rule.</span></span> <span data-ttu-id="86b8a-379">Consulte o tópico sobre [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) para obter detalhes e exemplos.</span><span class="sxs-lookup"><span data-stu-id="86b8a-379">See the [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-to-a-different-resource-group-or-subscription"></a><span data-ttu-id="86b8a-380">Mover um data factory para outro grupo de recursos ou assinatura</span><span class="sxs-lookup"><span data-stu-id="86b8a-380">Move a data factory to a different resource group or subscription</span></span>
<span data-ttu-id="86b8a-381">Você pode mover um data factory para outro grupo de recursos ou assinatura diferente usando o botão **Mover** da barra de comandos na home page do seu data factory.</span><span class="sxs-lookup"><span data-stu-id="86b8a-381">You can move a data factory to a different resource group or a different subscription by using the **Move** command bar button on the home page of your data factory.</span></span>

![Mover o Data Factory](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="86b8a-383">Você também pode mover todos os recursos relacionados (como alertas associados ao data factory) juntamente com ele.</span><span class="sxs-lookup"><span data-stu-id="86b8a-383">You can also move any related resources (such as alerts that are associated with the data factory), along with the data factory.</span></span>

![Caixa de diálogo Mover recursos](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
