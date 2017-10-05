---
title: "Introdução ao Agendador do Azure no portal do Azure | Microsoft Docs"
description: "Introdução ao Agendador do Azure no Portal do Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 3861ee121ed1c4d086ea81640e84d924d7d17ea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="6f143-103">Introdução ao Agendador do Azure no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6f143-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="6f143-104">É fácil criar trabalhos agendados no Agendador do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f143-104">It's easy to create scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="6f143-105">Neste tutorial, você aprenderá a criar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="6f143-105">In this tutorial, you'll learn how to create a job.</span></span> <span data-ttu-id="6f143-106">Você também aprenderá sobre os recursos de monitoramento e gerenciamento do Agendador.</span><span class="sxs-lookup"><span data-stu-id="6f143-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="6f143-107">Criar um trabalho</span><span class="sxs-lookup"><span data-stu-id="6f143-107">Create a job</span></span>
1. <span data-ttu-id="6f143-108">Entre no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6f143-108">Sign in to [Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="6f143-109">Clique em **+Novo** > digite *Agendador* na caixa de pesquisa > selecione **Agendador** nos resultados > clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6f143-109">Click **+New** > type *Scheduler* in the search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="6f143-110">Vamos criar um trabalho que simplesmente visita http://www.microsoft.com/ com uma solicitação GET.</span><span class="sxs-lookup"><span data-stu-id="6f143-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="6f143-111">Na tela **Trabalho do Agendador** , insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="6f143-111">In the **Scheduler Job** screen, enter the following information:</span></span>
   
   1. <span data-ttu-id="6f143-112">**Nome:** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="6f143-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="6f143-113">**Assinatura:** sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="6f143-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="6f143-114">**Coleção de Trabalhos:** selecione uma coleção de trabalhos existente ou clique em **Criar Novo** > insira um nome.</span><span class="sxs-lookup"><span data-stu-id="6f143-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="6f143-115">Em seguida, nas **Configurações de Ação**, defina os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="6f143-115">Next, in **Action Settings**, define the following values:</span></span>
   
   1. <span data-ttu-id="6f143-116">**Tipo de ação:** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="6f143-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="6f143-117">**Método:** `GET`</span><span class="sxs-lookup"><span data-stu-id="6f143-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="6f143-118">**URL:** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="6f143-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="6f143-119">Finalmente, vamos definir uma agenda.</span><span class="sxs-lookup"><span data-stu-id="6f143-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="6f143-120">O trabalho pode ser definido como um único trabalho, mas convém escolher uma agenda de recorrência:</span><span class="sxs-lookup"><span data-stu-id="6f143-120">The job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="6f143-121">**Recorrência**: `Recurring`</span><span class="sxs-lookup"><span data-stu-id="6f143-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="6f143-122">**Iniciar**: data de hoje</span><span class="sxs-lookup"><span data-stu-id="6f143-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="6f143-123">**Repetir a cada**: `12 Hours`</span><span class="sxs-lookup"><span data-stu-id="6f143-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="6f143-124">**Terminar**: dois dias após a data de hoje</span><span class="sxs-lookup"><span data-stu-id="6f143-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="6f143-125">Clique em **Criar**</span><span class="sxs-lookup"><span data-stu-id="6f143-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="6f143-126">Gerenciar e monitorar trabalhos</span><span class="sxs-lookup"><span data-stu-id="6f143-126">Manage and monitor jobs</span></span>
<span data-ttu-id="6f143-127">Depois que um trabalho é criado, ele aparece no painel principal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f143-127">Once a job is created, it appears in the main Azure dashboard.</span></span> <span data-ttu-id="6f143-128">Clique no trabalho e uma nova janela será aberta com as seguintes guias:</span><span class="sxs-lookup"><span data-stu-id="6f143-128">Click the job and a new window opens with the following tabs:</span></span>

1. <span data-ttu-id="6f143-129">Propriedades</span><span class="sxs-lookup"><span data-stu-id="6f143-129">Properties</span></span>  
2. <span data-ttu-id="6f143-130">Configurações de Ação</span><span class="sxs-lookup"><span data-stu-id="6f143-130">Action Settings</span></span>  
3. <span data-ttu-id="6f143-131">Agenda</span><span class="sxs-lookup"><span data-stu-id="6f143-131">Schedule</span></span>  
4. <span data-ttu-id="6f143-132">Histórico</span><span class="sxs-lookup"><span data-stu-id="6f143-132">History</span></span>
5. <span data-ttu-id="6f143-133">Usuários</span><span class="sxs-lookup"><span data-stu-id="6f143-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="6f143-134">Propriedades</span><span class="sxs-lookup"><span data-stu-id="6f143-134">Properties</span></span>
<span data-ttu-id="6f143-135">Essas propriedades somente leitura descrevem os metadados de gerenciamento para o trabalho do Agendador.</span><span class="sxs-lookup"><span data-stu-id="6f143-135">These read-only properties describe the management metadata for the Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="6f143-136">Configurações de Ação</span><span class="sxs-lookup"><span data-stu-id="6f143-136">Action settings</span></span>
<span data-ttu-id="6f143-137">Clicar em um trabalho na tela **Trabalhos** permite que você configure esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="6f143-137">Clicking on a job in the **Jobs** screen allows you to configure that job.</span></span> <span data-ttu-id="6f143-138">Isso permitirá definir configurações avançadas, se você não as tiver configurado no assistente de criação rápida.</span><span class="sxs-lookup"><span data-stu-id="6f143-138">This lets you configure advanced settings, if you didn't configure them in the quick-create wizard.</span></span>

<span data-ttu-id="6f143-139">Para todos os tipos de ação, você pode alterar a política de repetição e a ação de erro.</span><span class="sxs-lookup"><span data-stu-id="6f143-139">For all action types, you may change the retry policy and the error action.</span></span>

<span data-ttu-id="6f143-140">Para tipos de ação do trabalho HTTP e HTTPS, você pode alterar o método para qualquer verbo HTTP permitido.</span><span class="sxs-lookup"><span data-stu-id="6f143-140">For HTTP and HTTPS job action types, you may change the method to any allowed HTTP verb.</span></span> <span data-ttu-id="6f143-141">Você também pode adicionar, excluir ou alterar os cabeçalhos e informações de autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="6f143-141">You may also add, delete, or change the headers and basic authentication information.</span></span>

<span data-ttu-id="6f143-142">Para tipos de ação de fila de armazenamento, você pode alterar a conta de armazenamento, nome da fila, token SAS e corpo.</span><span class="sxs-lookup"><span data-stu-id="6f143-142">For storage queue action types, you may change the storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="6f143-143">Para tipos de ação do barramento de serviço, você pode alterar o namespace, o caminho da fila/tópico, as configurações de autenticação, o tipo de transporte, as propriedades de mensagem e o corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="6f143-143">For service bus action types, you may change the namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="6f143-144">Agenda</span><span class="sxs-lookup"><span data-stu-id="6f143-144">Schedule</span></span>
<span data-ttu-id="6f143-145">Isso permite reconfigurar o agendamento, se você desejar alterar o agendamento que criou no assistente de criação rápida.</span><span class="sxs-lookup"><span data-stu-id="6f143-145">This lets you reconfigure the schedule, if you'd like to change the schedule you created in the quick-create wizard.</span></span>

<span data-ttu-id="6f143-146">Essa é uma oportunidade de criar [agendas complexas e recorrência avançada no trabalho](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="6f143-146">This is an opportunity to build [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="6f143-147">Você pode alterar a data e hora de início, o agendamento de recorrência e a data e hora de término (se o trabalho é recorrente).</span><span class="sxs-lookup"><span data-stu-id="6f143-147">You may change the start date and time, recurrence schedule, and the end date and time (if the job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="6f143-148">Histórico</span><span class="sxs-lookup"><span data-stu-id="6f143-148">History</span></span>
<span data-ttu-id="6f143-149">A guia **Histórico** exibe as métricas selecionadas para cada execução do trabalho do sistema para o trabalho selecionado.</span><span class="sxs-lookup"><span data-stu-id="6f143-149">The **History** tab displays selected metrics for every job execution in the system for the selected job.</span></span> <span data-ttu-id="6f143-150">Essas métricas fornecem valores em tempo real relacionados à integridade de seu Agendador:</span><span class="sxs-lookup"><span data-stu-id="6f143-150">These metrics provide real-time values regarding the health of your Scheduler:</span></span>

1. <span data-ttu-id="6f143-151">Status</span><span class="sxs-lookup"><span data-stu-id="6f143-151">Status</span></span>  
2. <span data-ttu-id="6f143-152">Detalhes</span><span class="sxs-lookup"><span data-stu-id="6f143-152">Details</span></span>  
3. <span data-ttu-id="6f143-153">Tentativas de repetição</span><span class="sxs-lookup"><span data-stu-id="6f143-153">Retry attempts</span></span>
4. <span data-ttu-id="6f143-154">Ocorrência: 1ª, 2ª, 3ª etc.</span><span class="sxs-lookup"><span data-stu-id="6f143-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="6f143-155">Hora de início da execução</span><span class="sxs-lookup"><span data-stu-id="6f143-155">Start time of execution</span></span>  
6. <span data-ttu-id="6f143-156">Hora de término da execução</span><span class="sxs-lookup"><span data-stu-id="6f143-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="6f143-157">Você pode clicar em uma execução para exibir seus **Detalhes de Histórico**, incluindo a resposta inteira para cada execução.</span><span class="sxs-lookup"><span data-stu-id="6f143-157">You can click on a run to view its **History Details**, including the whole response for every execution.</span></span> <span data-ttu-id="6f143-158">Essa caixa de diálogo também permite que você copie a resposta para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="6f143-158">This dialog box also allows you to copy the response to the clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="6f143-159">Usuários</span><span class="sxs-lookup"><span data-stu-id="6f143-159">Users</span></span>
<span data-ttu-id="6f143-160">O RBAC (controle de acesso baseado em função) do Azure permite o gerenciamento de acesso refinado para o Agendador do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f143-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="6f143-161">Para saber como usar a guia Usuários, confira [Controle de Acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="6f143-161">To learn how to use the Users tab, refer to [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="6f143-162">Consulte também</span><span class="sxs-lookup"><span data-stu-id="6f143-162">See also</span></span>
 [<span data-ttu-id="6f143-163">O que é o Agendador?</span><span class="sxs-lookup"><span data-stu-id="6f143-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="6f143-164">Conceitos, terminologia e hierarquia de entidades do Agendador</span><span class="sxs-lookup"><span data-stu-id="6f143-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="6f143-165">Planos e Cobrança no Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="6f143-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="6f143-166">Como criar agendas complexas e recorrência avançada com o Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="6f143-166">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="6f143-167">Referência da API REST do Agendador</span><span class="sxs-lookup"><span data-stu-id="6f143-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="6f143-168">Referência de cmdlets do PowerShell do Agendador</span><span class="sxs-lookup"><span data-stu-id="6f143-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="6f143-169">Alta disponibilidade e confiabilidade do Agendador</span><span class="sxs-lookup"><span data-stu-id="6f143-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="6f143-170">Limites, padrões e códigos de erro do Agendador</span><span class="sxs-lookup"><span data-stu-id="6f143-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="6f143-171">Autenticação de saída do Agendador</span><span class="sxs-lookup"><span data-stu-id="6f143-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
