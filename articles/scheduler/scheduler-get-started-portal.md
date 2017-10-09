---
title: aaaGet iniciado com o Agendador do Azure no portal do Azure | Microsoft Docs
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
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="b675a-103">Introdução ao Agendador do Azure no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b675a-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="b675a-104">É fácil toocreate agendado trabalhos no Agendador do Azure.</span><span class="sxs-lookup"><span data-stu-id="b675a-104">It's easy toocreate scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="b675a-105">Neste tutorial, você aprenderá como toocreate um trabalho.</span><span class="sxs-lookup"><span data-stu-id="b675a-105">In this tutorial, you'll learn how toocreate a job.</span></span> <span data-ttu-id="b675a-106">Você também aprenderá sobre os recursos de monitoramento e gerenciamento do Agendador.</span><span class="sxs-lookup"><span data-stu-id="b675a-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="b675a-107">Criar um trabalho</span><span class="sxs-lookup"><span data-stu-id="b675a-107">Create a job</span></span>
1. <span data-ttu-id="b675a-108">Entrar muito[portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b675a-108">Sign in too[Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="b675a-109">Clique em **+ novo** > tipo *Agendador* na caixa de pesquisa hello > selecione **Agendador** nos resultados > clique **criar**.</span><span class="sxs-lookup"><span data-stu-id="b675a-109">Click **+New** > type *Scheduler* in hello search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="b675a-110">Vamos criar um trabalho que simplesmente visita http://www.microsoft.com/ com uma solicitação GET.</span><span class="sxs-lookup"><span data-stu-id="b675a-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="b675a-111">Em Olá **trabalho do Agendador** tela, insira Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="b675a-111">In hello **Scheduler Job** screen, enter hello following information:</span></span>
   
   1. <span data-ttu-id="b675a-112">**Nome:** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="b675a-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="b675a-113">**Assinatura:** sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="b675a-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="b675a-114">**Coleção de Trabalhos:** selecione uma coleção de trabalhos existente ou clique em **Criar Novo** > insira um nome.</span><span class="sxs-lookup"><span data-stu-id="b675a-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="b675a-115">Em seguida, na **as configurações de ação**, definir Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="b675a-115">Next, in **Action Settings**, define hello following values:</span></span>
   
   1. <span data-ttu-id="b675a-116">**Tipo de ação:** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="b675a-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="b675a-117">**Método:** `GET`</span><span class="sxs-lookup"><span data-stu-id="b675a-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="b675a-118">**URL:** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="b675a-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="b675a-119">Finalmente, vamos definir uma agenda.</span><span class="sxs-lookup"><span data-stu-id="b675a-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="b675a-120">trabalho de saudação pode ser definido como um único trabalho, mas convém escolher um agendamento de recorrência:</span><span class="sxs-lookup"><span data-stu-id="b675a-120">hello job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="b675a-121">**Recorrência**: `Recurring`</span><span class="sxs-lookup"><span data-stu-id="b675a-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="b675a-122">**Iniciar**: data de hoje</span><span class="sxs-lookup"><span data-stu-id="b675a-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="b675a-123">**Repetir a cada**: `12 Hours`</span><span class="sxs-lookup"><span data-stu-id="b675a-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="b675a-124">**Terminar**: dois dias após a data de hoje</span><span class="sxs-lookup"><span data-stu-id="b675a-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="b675a-125">Clique em **Criar**</span><span class="sxs-lookup"><span data-stu-id="b675a-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="b675a-126">Gerenciar e monitorar trabalhos</span><span class="sxs-lookup"><span data-stu-id="b675a-126">Manage and monitor jobs</span></span>
<span data-ttu-id="b675a-127">Quando um trabalho é criado, ele aparece no painel do Azure principal de saudação.</span><span class="sxs-lookup"><span data-stu-id="b675a-127">Once a job is created, it appears in hello main Azure dashboard.</span></span> <span data-ttu-id="b675a-128">Clique em trabalho hello e uma nova janela é aberta com hello guias a seguir:</span><span class="sxs-lookup"><span data-stu-id="b675a-128">Click hello job and a new window opens with hello following tabs:</span></span>

1. <span data-ttu-id="b675a-129">Propriedades</span><span class="sxs-lookup"><span data-stu-id="b675a-129">Properties</span></span>  
2. <span data-ttu-id="b675a-130">Configurações de Ação</span><span class="sxs-lookup"><span data-stu-id="b675a-130">Action Settings</span></span>  
3. <span data-ttu-id="b675a-131">Agenda</span><span class="sxs-lookup"><span data-stu-id="b675a-131">Schedule</span></span>  
4. <span data-ttu-id="b675a-132">Histórico</span><span class="sxs-lookup"><span data-stu-id="b675a-132">History</span></span>
5. <span data-ttu-id="b675a-133">Usuários</span><span class="sxs-lookup"><span data-stu-id="b675a-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="b675a-134">Propriedades</span><span class="sxs-lookup"><span data-stu-id="b675a-134">Properties</span></span>
<span data-ttu-id="b675a-135">Essas propriedades somente leitura descrevem Olá gerenciamento metadados para o trabalho do Agendador hello.</span><span class="sxs-lookup"><span data-stu-id="b675a-135">These read-only properties describe hello management metadata for hello Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="b675a-136">Configurações de Ação</span><span class="sxs-lookup"><span data-stu-id="b675a-136">Action settings</span></span>
<span data-ttu-id="b675a-137">Clicar em um trabalho em Olá **trabalhos** tela permite tooconfigure de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b675a-137">Clicking on a job in hello **Jobs** screen allows you tooconfigure that job.</span></span> <span data-ttu-id="b675a-138">Isso lhe permite definir configurações avançadas, se você não configurá-las no hello criação rápida assistente.</span><span class="sxs-lookup"><span data-stu-id="b675a-138">This lets you configure advanced settings, if you didn't configure them in hello quick-create wizard.</span></span>

<span data-ttu-id="b675a-139">Para todos os tipos de ação, você pode alterar a política de repetição hello e ação de erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="b675a-139">For all action types, you may change hello retry policy and hello error action.</span></span>

<span data-ttu-id="b675a-140">Para tipos de ação do trabalho HTTP e HTTPS, você pode alterar Olá método tooany permitido verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="b675a-140">For HTTP and HTTPS job action types, you may change hello method tooany allowed HTTP verb.</span></span> <span data-ttu-id="b675a-141">Você também pode adicionar, excluir ou alterar cabeçalhos hello e informações de autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="b675a-141">You may also add, delete, or change hello headers and basic authentication information.</span></span>

<span data-ttu-id="b675a-142">Para tipos de ação da fila de armazenamento, você pode alterar a conta de armazenamento Olá, nome da fila, token SAS e corpo.</span><span class="sxs-lookup"><span data-stu-id="b675a-142">For storage queue action types, you may change hello storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="b675a-143">Para tipos de ação do barramento de serviço, você pode alterar o namespace hello, o caminho da fila/tópico, configurações de autenticação, tipo de transporte, propriedades de mensagem e corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="b675a-143">For service bus action types, you may change hello namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="b675a-144">Agenda</span><span class="sxs-lookup"><span data-stu-id="b675a-144">Schedule</span></span>
<span data-ttu-id="b675a-145">Isso permite a você reconfigurar a agenda de saudação, se você deseja que a agenda de saudação toochange criado na Olá rápida-Assistente para criar.</span><span class="sxs-lookup"><span data-stu-id="b675a-145">This lets you reconfigure hello schedule, if you'd like toochange hello schedule you created in hello quick-create wizard.</span></span>

<span data-ttu-id="b675a-146">Isso é uma oportunidade toobuild [agendas complexas e recorrência avançadas em seu trabalho](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="b675a-146">This is an opportunity toobuild [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="b675a-147">Você pode alterar a data de início hello e hora, agendamento de recorrência e Olá data de término e a hora (se o trabalho de saudação for recorrente).</span><span class="sxs-lookup"><span data-stu-id="b675a-147">You may change hello start date and time, recurrence schedule, and hello end date and time (if hello job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="b675a-148">Histórico</span><span class="sxs-lookup"><span data-stu-id="b675a-148">History</span></span>
<span data-ttu-id="b675a-149">Olá **histórico** guia exibe a métrica selecionada para cada execução do trabalho no sistema Olá para o trabalho selecionado hello.</span><span class="sxs-lookup"><span data-stu-id="b675a-149">hello **History** tab displays selected metrics for every job execution in hello system for hello selected job.</span></span> <span data-ttu-id="b675a-150">Essas métricas fornecem valores em tempo real sobre a integridade de saudação do seu Agendador:</span><span class="sxs-lookup"><span data-stu-id="b675a-150">These metrics provide real-time values regarding hello health of your Scheduler:</span></span>

1. <span data-ttu-id="b675a-151">Status</span><span class="sxs-lookup"><span data-stu-id="b675a-151">Status</span></span>  
2. <span data-ttu-id="b675a-152">Detalhes</span><span class="sxs-lookup"><span data-stu-id="b675a-152">Details</span></span>  
3. <span data-ttu-id="b675a-153">Tentativas de repetição</span><span class="sxs-lookup"><span data-stu-id="b675a-153">Retry attempts</span></span>
4. <span data-ttu-id="b675a-154">Ocorrência: 1ª, 2ª, 3ª etc.</span><span class="sxs-lookup"><span data-stu-id="b675a-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="b675a-155">Hora de início da execução</span><span class="sxs-lookup"><span data-stu-id="b675a-155">Start time of execution</span></span>  
6. <span data-ttu-id="b675a-156">Hora de término da execução</span><span class="sxs-lookup"><span data-stu-id="b675a-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="b675a-157">Você pode clicar em uma execução tooview seu **detalhes de histórico**, incluindo a resposta inteira Olá para cada execução.</span><span class="sxs-lookup"><span data-stu-id="b675a-157">You can click on a run tooview its **History Details**, including hello whole response for every execution.</span></span> <span data-ttu-id="b675a-158">Essa caixa de diálogo também permite que você toocopy Olá resposta toohello da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="b675a-158">This dialog box also allows you toocopy hello response toohello clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="b675a-159">Usuários</span><span class="sxs-lookup"><span data-stu-id="b675a-159">Users</span></span>
<span data-ttu-id="b675a-160">O RBAC (controle de acesso baseado em função) do Azure permite o gerenciamento de acesso refinado para o Agendador do Azure.</span><span class="sxs-lookup"><span data-stu-id="b675a-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="b675a-161">toolearn como Olá toouse guia de usuários, consulte muito[o controle de acesso](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="b675a-161">toolearn how toouse hello Users tab, refer too[Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="b675a-162">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b675a-162">See also</span></span>
 [<span data-ttu-id="b675a-163">O que é o Agendador?</span><span class="sxs-lookup"><span data-stu-id="b675a-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="b675a-164">Conceitos, terminologia e hierarquia de entidades do Agendador</span><span class="sxs-lookup"><span data-stu-id="b675a-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="b675a-165">Planos e Cobrança no Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="b675a-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="b675a-166">Como toobuild complexo agenda e recorrência avançadas com o Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="b675a-166">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="b675a-167">Referência da API REST do Agendador</span><span class="sxs-lookup"><span data-stu-id="b675a-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="b675a-168">Referência de cmdlets do PowerShell do Agendador</span><span class="sxs-lookup"><span data-stu-id="b675a-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="b675a-169">Alta disponibilidade e confiabilidade do Agendador</span><span class="sxs-lookup"><span data-stu-id="b675a-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="b675a-170">Limites, padrões e códigos de erro do Agendador</span><span class="sxs-lookup"><span data-stu-id="b675a-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="b675a-171">Autenticação de saída do Agendador</span><span class="sxs-lookup"><span data-stu-id="b675a-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

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
