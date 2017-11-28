---
title: "fluxos de trabalho de aprovação de gerenciamento de identidade com privilégios de aaaAzure | Microsoft Docs"
description: "Saiba mais sobre os fluxos de trabalho de aprovação do PIM (Privileged Identity Management)"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="51278-103">Aprovações (Visualização)</span><span class="sxs-lookup"><span data-stu-id="51278-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="51278-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="51278-104">Overview</span></span>

<span data-ttu-id="51278-105">Com aprovações para Privileged Identity Management, você pode configurar funções toorequire aprovação para ativação e escolha um ou vários usuários ou grupos de aprovadores como delegados.</span><span class="sxs-lookup"><span data-stu-id="51278-105">With Approvals for Privileged Identity Management, you can configure roles toorequire approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="51278-106">Continue lendo toolearn como tooconfigure funções e selecione aprovadores.</span><span class="sxs-lookup"><span data-stu-id="51278-106">Keep reading toolearn how tooconfigure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="51278-107">Tenha em mente que esse recurso ainda está em desenvolvimento e você poderá encontrar bugs.</span><span class="sxs-lookup"><span data-stu-id="51278-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="51278-108">Olá funcionalidade, incluindo texto e convenções de nomenclatura estão sujeitos a alterações e não devem ser considerados finais.</span><span class="sxs-lookup"><span data-stu-id="51278-108">hello functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="51278-109">Terminologia principal</span><span class="sxs-lookup"><span data-stu-id="51278-109">Key Terminology</span></span>

<span data-ttu-id="51278-110">*Usuário de função qualificado* – uma função qualificado é um usuário dentro de sua organização que foi atribuído a função tooan AD do Azure como qualificados (função exige a ativação).</span><span class="sxs-lookup"><span data-stu-id="51278-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned tooan Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="51278-111">*Aprovador Delegado* – um aprovador delegado é um ou vários indivíduos ou grupos do Azure AD responsáveis por aprovar solicitações de ativação de função.</span><span class="sxs-lookup"><span data-stu-id="51278-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="51278-112">Cenários</span><span class="sxs-lookup"><span data-stu-id="51278-112">Scenarios</span></span>

<span data-ttu-id="51278-113">visualização privada Olá dá suporte a saudação os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="51278-113">hello private preview supports hello following scenarios:</span></span>

<span data-ttu-id="51278-114">**Como um PRA (Administrador de Função com Privilégios), você pode:**</span><span class="sxs-lookup"><span data-stu-id="51278-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="51278-115">habilitar a aprovação para funções específicas</span><span class="sxs-lookup"><span data-stu-id="51278-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="51278-116">especificar as solicitações de tooapprove de usuários e/ou grupos do aprovador</span><span class="sxs-lookup"><span data-stu-id="51278-116">specify approver users and/or groups tooapprove requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="51278-117">exibir o histórico de solicitações e aprovações de todas as funções com privilégios</span><span class="sxs-lookup"><span data-stu-id="51278-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="51278-118">**Como um aprovador designado, você pode:**</span><span class="sxs-lookup"><span data-stu-id="51278-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="51278-119">exibir as aprovações pendentes (solicitações)</span><span class="sxs-lookup"><span data-stu-id="51278-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="51278-120">aprovar ou rejeitar solicitações de elevação de função (única e/ou em massa)</span><span class="sxs-lookup"><span data-stu-id="51278-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="51278-121">fornecer uma justificativa para minha aprovação/rejeição</span><span class="sxs-lookup"><span data-stu-id="51278-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="51278-122">**Como um Usuário de Função Qualificada, você pode:**</span><span class="sxs-lookup"><span data-stu-id="51278-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="51278-123">solicitar a ativação de uma função que exige aprovação</span><span class="sxs-lookup"><span data-stu-id="51278-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="51278-124">Exibir o status Olá tooactivate sua solicitação</span><span class="sxs-lookup"><span data-stu-id="51278-124">view hello status of your request tooactivate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="51278-125">concluir a tarefa no Azure AD caso a ativação tenha sido aprovada</span><span class="sxs-lookup"><span data-stu-id="51278-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="51278-126">Navegação</span><span class="sxs-lookup"><span data-stu-id="51278-126">Navigation</span></span>

<span data-ttu-id="51278-127">Nós atualizamos aprovações de toosupport de navegação Olá</span><span class="sxs-lookup"><span data-stu-id="51278-127">We've updated hello navigation toosupport approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="51278-128">página de aterrissagem Olá fornece acesso conveniente tooinformation sobre a documentação de aprovações PIM e hello novo.</span><span class="sxs-lookup"><span data-stu-id="51278-128">hello default landing page provides convenient access tooinformation about PIM and hello new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="51278-129">Também adicionamos uma nova seção para todos os usuários do PIM, “Meu Histórico de Auditoria”.</span><span class="sxs-lookup"><span data-stu-id="51278-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="51278-130">Aqui você pode encontrar todas as identidades do hello informações tooyour relevantes.</span><span class="sxs-lookup"><span data-stu-id="51278-130">Here you can find all hello information relevant tooyour identity.</span></span> <span data-ttu-id="51278-131">Isso inclui todas as suas solicitações pendentes e concluídas, qualquer decisões feitas sobre solicitações de saudação resolver e todas as suas ativações de função anteriores em um local conveniente.</span><span class="sxs-lookup"><span data-stu-id="51278-131">This includes all your pending and completed requests, any decisions you’ve made about hello requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="51278-132">Habilitar a aprovação para funções específicas</span><span class="sxs-lookup"><span data-stu-id="51278-132">Enable approval for specific roles</span></span>

<span data-ttu-id="51278-133">tooenable aprovação para uma função específica, primeiro selecione as funções de diretório de navegação à esquerda da saudação.</span><span class="sxs-lookup"><span data-stu-id="51278-133">tooenable approval for a specific role, first select Directory Roles from hello left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="51278-134">Localizar e selecionar as configurações no hello navegação à esquerda de funções de diretório</span><span class="sxs-lookup"><span data-stu-id="51278-134">Find and select settings in hello Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="51278-135">Selecionar Funções com privilégios:</span><span class="sxs-lookup"><span data-stu-id="51278-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="51278-136">Selecione "Ativar" na saudação exigem a seção de aprovação:</span><span class="sxs-lookup"><span data-stu-id="51278-136">Select “Enable” in hello Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="51278-137">Uma vez habilitada, folha Olá expandirá Olá tooshow detalhes a seguir:</span><span class="sxs-lookup"><span data-stu-id="51278-137">Once enabled, hello blade will expand tooshow hello following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="51278-138">Se você não especificar qualquer aprovadores, Olá PRA(s) se tornam saudação padrão aprovadores.</span><span class="sxs-lookup"><span data-stu-id="51278-138">If you DO NOT specify any approvers, hello PRA(s) become hello default approver(s).</span></span> <span data-ttu-id="51278-139">PRA(s) seria necessário tooapprove ativação todas as solicitações para essa função.</span><span class="sxs-lookup"><span data-stu-id="51278-139">PRA(s) would be required tooapprove ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a><span data-ttu-id="51278-140">Especificar as solicitações de tooapprove de usuários e/ou grupos do aprovador</span><span class="sxs-lookup"><span data-stu-id="51278-140">Specify approver users and/or groups tooapprove requests</span></span>

<span data-ttu-id="51278-141">aprovação de toodelegate, clique em opção de saudação muito "Selecionar aprovadores":</span><span class="sxs-lookup"><span data-stu-id="51278-141">toodelegate approval, click hello option too“Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="51278-142">Quando a folha de aprovadores selecione Olá carrega, você pode procurar por um usuário ou grupo específico utilizando barra de pesquisa Olá Olá superior ou selecionando na lista pré-populada hello e clique em "Select" quando terminar:</span><span class="sxs-lookup"><span data-stu-id="51278-142">When hello Select approvers blade loads, you may search for a specific user or group using hello search bar at hello top, or selecting from hello pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="51278-143">Observação: é possível selecionar vários usuários ou grupos por vez.</span><span class="sxs-lookup"><span data-stu-id="51278-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="51278-144">Sua seleção aparecerá na lista de saudação de aprovadores selecionados, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="51278-144">Your selection will appear in hello list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="51278-145">tooremove um aprovador, simplesmente clique Olá remover botão próximo tootheir nome.</span><span class="sxs-lookup"><span data-stu-id="51278-145">tooremove an approver, simply click hello Remove button next tootheir name.</span></span>

<span data-ttu-id="51278-146">tooadd aprovadores adicionais, o processo de repetição hello.</span><span class="sxs-lookup"><span data-stu-id="51278-146">tooadd additional approvers, repeat hello process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="51278-147">Exibir o histórico de solicitações e aprovações de todas as funções com privilégios</span><span class="sxs-lookup"><span data-stu-id="51278-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="51278-148">histórico de solicitação e aprovação de tooview para todas as funções privilegiadas, selecione Histórico de auditoria do painel hello:</span><span class="sxs-lookup"><span data-stu-id="51278-148">tooview request and approval history for all privileged roles, select Audit History from hello dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="51278-149">Você pode classificar dados Olá por ação e procure "Ativação aprovado"</span><span class="sxs-lookup"><span data-stu-id="51278-149">You can sort hello data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="51278-150">Exibir as aprovações pendentes (solicitações)</span><span class="sxs-lookup"><span data-stu-id="51278-150">View pending approvals (requests)</span></span>

<span data-ttu-id="51278-151">Como aprovador delegado, você receberá notificações por email quando uma solicitação estiver aguardando sua aprovação.</span><span class="sxs-lookup"><span data-stu-id="51278-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="51278-152">tooview essas solicitações no portal do PIM hello, na guia Painel (em nova navegação de saudação) selecione hello "aprovação solicitações pendentes" em hello esquerda a barra de navegação.</span><span class="sxs-lookup"><span data-stu-id="51278-152">tooview these requests in hello PIM portal, from the dashboard (in hello new navigation) select hello “Pending Approval Requests” tab in hello left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="51278-153">Aqui, você verá uma lista de solicitações com aprovação pendente:</span><span class="sxs-lookup"><span data-stu-id="51278-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="51278-154">Aprovar ou rejeitar solicitações de elevação de função (única e/ou em massa)</span><span class="sxs-lookup"><span data-stu-id="51278-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="51278-155">Selecione solicitações Olá deseja tooapprove ou negar e Olá botão na barra de ação que corresponde à sua decisão:</span><span class="sxs-lookup"><span data-stu-id="51278-155">Select hello requests you wish tooapprove or deny, and click hello button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="51278-156">Fornecer uma justificativa para minha aprovação/rejeição</span><span class="sxs-lookup"><span data-stu-id="51278-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="51278-157">Isso abre um novo tooapprove de folha ou negar as solicitações de vários ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="51278-157">This will open a new blade tooapprove or deny multiple requests at once.</span></span> <span data-ttu-id="51278-158">Inserir uma justificativa para sua decisão, e clique em Aprovar (ou negar) na inferior de saudação ou folha hello:</span><span class="sxs-lookup"><span data-stu-id="51278-158">Enter a justification for your decision, and click approve (or deny) at hello bottom or hello blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="51278-159">Quando o processo de solicitação de saudação for concluído, símbolo de status Olá refletirá a decisão tomada (neste exemplo, Olá decisão é aprovar):</span><span class="sxs-lookup"><span data-stu-id="51278-159">When hello request process is complete, hello status symbol will reflect the decision you made (in this example, hello decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="51278-160">Solicitar a ativação de uma função que exige aprovação</span><span class="sxs-lookup"><span data-stu-id="51278-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="51278-161">Solicitando a ativação de uma função que requer aprovação pode ser iniciada de navegação de PIM antiga hello ou navegação nova hello, como um processo de saudação para função ativação permanece Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="51278-161">Requesting activation of a role that requires approval may be initiated from either hello old PIM navigation, or hello new navigation, as hello process for role activation remains hello same.</span></span> <span data-ttu-id="51278-162">Basta selecione uma função na lista de saudação de funções para ativar:</span><span class="sxs-lookup"><span data-stu-id="51278-162">Simply select a role from hello list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="51278-163">Se uma função com privilégios exigir a Autenticação Multifator, você deverá concluir essa tarefa primeiro:</span><span class="sxs-lookup"><span data-stu-id="51278-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="51278-164">Depois de concluída, clique em Ativar e forneça uma justificativa (se necessário):</span><span class="sxs-lookup"><span data-stu-id="51278-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="51278-165">solicitante de saudação será exibida uma notificação que Olá solicitação está com aprovação pendente:</span><span class="sxs-lookup"><span data-stu-id="51278-165">hello requestor will see a notification that hello request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a><span data-ttu-id="51278-166">Exibir o status Olá tooactivate sua solicitação</span><span class="sxs-lookup"><span data-stu-id="51278-166">View hello status of your request tooactivate</span></span>

<span data-ttu-id="51278-167">Exibindo o status de saudação de uma solicitação pendente tooactivate deve ser acessado do novo painel de navegação.</span><span class="sxs-lookup"><span data-stu-id="51278-167">Viewing hello status of a pending request tooactivate must be accessed from the new navigation.</span></span> <span data-ttu-id="51278-168">Na barra de navegação à esquerda do hello, selecione guia de "Minhas solicitações de" hello:</span><span class="sxs-lookup"><span data-stu-id="51278-168">From hello left navigation bar, select hello “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="51278-169">estado da solicitação da saudação padrão é muito "Pendente", mas você pode alternar toosee todos ou solicitações negadas.</span><span class="sxs-lookup"><span data-stu-id="51278-169">hello request state defaults too“Pending”, but you can toggle toosee all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="51278-170">Concluir a tarefa no Azure AD caso a ativação tenha sido aprovada</span><span class="sxs-lookup"><span data-stu-id="51278-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="51278-171">Após a aprovação de solicitação hello, função hello está ativa e você pode continuar com qualquer trabalho que exija a essa função.</span><span class="sxs-lookup"><span data-stu-id="51278-171">Once hello request is approved, hello role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="51278-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="51278-172">Next steps</span></span>

<span data-ttu-id="51278-173">Seu comentário é valioso toous.</span><span class="sxs-lookup"><span data-stu-id="51278-173">Your feedback is valuable toous.</span></span> <span data-ttu-id="51278-174">Sinta-se livre tooshare comentários conosco aqui!</span><span class="sxs-lookup"><span data-stu-id="51278-174">Please feel free tooshare comments or feedback with us here!</span></span>
