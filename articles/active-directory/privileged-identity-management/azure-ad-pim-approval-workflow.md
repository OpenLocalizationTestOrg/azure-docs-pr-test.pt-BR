---
title: "Fluxos de trabalho de aprovação do Azure Privileged Identity Management | Microsoft Docs"
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
ms.openlocfilehash: cf6a9213fa0a1cba8725aabb42abe51b805ece7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="f713c-103">Aprovações (Visualização)</span><span class="sxs-lookup"><span data-stu-id="f713c-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="f713c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f713c-104">Overview</span></span>

<span data-ttu-id="f713c-105">Com Aprovações para o Privileged Identity Management, você pode configurar funções para solicitar aprovação para ativação e escolher um ou vários usuários ou grupos como aprovadores delegados.</span><span class="sxs-lookup"><span data-stu-id="f713c-105">With Approvals for Privileged Identity Management, you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="f713c-106">Continue lendo para saber como configurar funções e selecionar aprovadores.</span><span class="sxs-lookup"><span data-stu-id="f713c-106">Keep reading to learn how to configure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="f713c-107">Tenha em mente que esse recurso ainda está em desenvolvimento e você poderá encontrar bugs.</span><span class="sxs-lookup"><span data-stu-id="f713c-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="f713c-108">A funcionalidade, incluindo o texto e as convenções de nomenclatura, está sujeita a alterações e não deverá ser considerada definitiva.</span><span class="sxs-lookup"><span data-stu-id="f713c-108">The functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="f713c-109">Terminologia principal</span><span class="sxs-lookup"><span data-stu-id="f713c-109">Key Terminology</span></span>

<span data-ttu-id="f713c-110">*Usuário de Função Qualificada* – um usuário de função qualificada é um usuário de sua organização que foi atribuído a uma função do Azure AD como qualificada (a função exige a ativação).</span><span class="sxs-lookup"><span data-stu-id="f713c-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned to an Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="f713c-111">*Aprovador Delegado* – um aprovador delegado é um ou vários indivíduos ou grupos do Azure AD responsáveis por aprovar solicitações de ativação de função.</span><span class="sxs-lookup"><span data-stu-id="f713c-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="f713c-112">Cenários</span><span class="sxs-lookup"><span data-stu-id="f713c-112">Scenarios</span></span>

<span data-ttu-id="f713c-113">A visualização particular dá suporte aos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="f713c-113">The private preview supports the following scenarios:</span></span>

<span data-ttu-id="f713c-114">**Como um PRA (Administrador de Função com Privilégios), você pode:**</span><span class="sxs-lookup"><span data-stu-id="f713c-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="f713c-115">habilitar a aprovação para funções específicas</span><span class="sxs-lookup"><span data-stu-id="f713c-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="f713c-116">especificar usuários e/ou grupos aprovadores para aprovar solicitações</span><span class="sxs-lookup"><span data-stu-id="f713c-116">specify approver users and/or groups to approve requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="f713c-117">exibir o histórico de solicitações e aprovações de todas as funções com privilégios</span><span class="sxs-lookup"><span data-stu-id="f713c-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="f713c-118">**Como um aprovador designado, você pode:**</span><span class="sxs-lookup"><span data-stu-id="f713c-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="f713c-119">exibir as aprovações pendentes (solicitações)</span><span class="sxs-lookup"><span data-stu-id="f713c-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="f713c-120">aprovar ou rejeitar solicitações de elevação de função (única e/ou em massa)</span><span class="sxs-lookup"><span data-stu-id="f713c-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="f713c-121">fornecer uma justificativa para minha aprovação/rejeição</span><span class="sxs-lookup"><span data-stu-id="f713c-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="f713c-122">**Como um Usuário de Função Qualificada, você pode:**</span><span class="sxs-lookup"><span data-stu-id="f713c-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="f713c-123">solicitar a ativação de uma função que exige aprovação</span><span class="sxs-lookup"><span data-stu-id="f713c-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="f713c-124">exibir o status de sua solicitação a ser ativada</span><span class="sxs-lookup"><span data-stu-id="f713c-124">view the status of your request to activate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="f713c-125">concluir a tarefa no Azure AD caso a ativação tenha sido aprovada</span><span class="sxs-lookup"><span data-stu-id="f713c-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="f713c-126">Navegação</span><span class="sxs-lookup"><span data-stu-id="f713c-126">Navigation</span></span>

<span data-ttu-id="f713c-127">Atualizamos a navegação para dar suporte a aprovações</span><span class="sxs-lookup"><span data-stu-id="f713c-127">We've updated the navigation to support approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="f713c-128">A página de aterrissagem padrão fornece acesso conveniente às informações sobre o PIM e à nova documentação de aprovações.</span><span class="sxs-lookup"><span data-stu-id="f713c-128">The default landing page provides convenient access to information about PIM and the new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="f713c-129">Também adicionamos uma nova seção para todos os usuários do PIM, “Meu Histórico de Auditoria”.</span><span class="sxs-lookup"><span data-stu-id="f713c-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="f713c-130">Aqui você pode encontrar todas as informações relevantes à sua identidade.</span><span class="sxs-lookup"><span data-stu-id="f713c-130">Here you can find all the information relevant to your identity.</span></span> <span data-ttu-id="f713c-131">Isso inclui todas as suas solicitações pendentes e concluídas, decisões feitas sobre as solicitações resolvidas e todas as ativações de função anteriores em um único local conveniente.</span><span class="sxs-lookup"><span data-stu-id="f713c-131">This includes all your pending and completed requests, any decisions you’ve made about the requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="f713c-132">Habilitar a aprovação para funções específicas</span><span class="sxs-lookup"><span data-stu-id="f713c-132">Enable approval for specific roles</span></span>

<span data-ttu-id="f713c-133">Para habilitar a aprovação para uma função específica, primeiro selecione Funções de Diretório na barra de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="f713c-133">To enable approval for a specific role, first select Directory Roles from the left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="f713c-134">Localizar e selecionar as configurações na barra de navegação à esquerda de Funções de Diretório</span><span class="sxs-lookup"><span data-stu-id="f713c-134">Find and select settings in the Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="f713c-135">Selecionar Funções com privilégios:</span><span class="sxs-lookup"><span data-stu-id="f713c-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="f713c-136">Selecione “Habilitar” na seção Exigir aprovação:</span><span class="sxs-lookup"><span data-stu-id="f713c-136">Select “Enable” in the Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="f713c-137">Depois de habilitada, a folha será expandida para mostrar os seguintes detalhes:</span><span class="sxs-lookup"><span data-stu-id="f713c-137">Once enabled, the blade will expand to show the following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="f713c-138">Se você NÃO especificar nenhum aprovador, os PRAs se tornarão os aprovadores padrão.</span><span class="sxs-lookup"><span data-stu-id="f713c-138">If you DO NOT specify any approvers, the PRA(s) become the default approver(s).</span></span> <span data-ttu-id="f713c-139">Os PRAs precisarão aprovar TODAS as solicitações de ativação dessa função.</span><span class="sxs-lookup"><span data-stu-id="f713c-139">PRA(s) would be required to approve ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-to-approve-requests"></a><span data-ttu-id="f713c-140">Especificar usuários e/ou grupos aprovadores para aprovar solicitações</span><span class="sxs-lookup"><span data-stu-id="f713c-140">Specify approver users and/or groups to approve requests</span></span>

<span data-ttu-id="f713c-141">Para delegar a aprovação, clique na opção para “Selecionar aprovadores”:</span><span class="sxs-lookup"><span data-stu-id="f713c-141">To delegate approval, click the option to “Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="f713c-142">Quando a folha Selecionar aprovadores for carregada, você poderá pesquisar um usuário ou grupo específico usando a barra de pesquisa na parte superior ou selecionando na lista pré-populada e, em seguida, clicar em “Selecionar” quando terminar:</span><span class="sxs-lookup"><span data-stu-id="f713c-142">When the Select approvers blade loads, you may search for a specific user or group using the search bar at the top, or selecting from the pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="f713c-143">Observação: é possível selecionar vários usuários ou grupos por vez.</span><span class="sxs-lookup"><span data-stu-id="f713c-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="f713c-144">Sua seleção será exibida na lista de aprovadores selecionados, conforme visto abaixo:</span><span class="sxs-lookup"><span data-stu-id="f713c-144">Your selection will appear in the list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="f713c-145">Para remover um aprovador, basta clicar no botão Remover ao lado do nome.</span><span class="sxs-lookup"><span data-stu-id="f713c-145">To remove an approver, simply click the Remove button next to their name.</span></span>

<span data-ttu-id="f713c-146">Para adicionar outros aprovadores, repita o processo.</span><span class="sxs-lookup"><span data-stu-id="f713c-146">To add additional approvers, repeat the process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="f713c-147">Exibir o histórico de solicitações e aprovações de todas as funções com privilégios</span><span class="sxs-lookup"><span data-stu-id="f713c-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="f713c-148">Para exibir o histórico de solicitações e aprovações de todas as funções com privilégios, selecione Histórico de Auditoria do painel:</span><span class="sxs-lookup"><span data-stu-id="f713c-148">To view request and approval history for all privileged roles, select Audit History from the dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="f713c-149">É possível classificar os dados por Ação e procurar “Ativação Aprovada”</span><span class="sxs-lookup"><span data-stu-id="f713c-149">You can sort the data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="f713c-150">Exibir as aprovações pendentes (solicitações)</span><span class="sxs-lookup"><span data-stu-id="f713c-150">View pending approvals (requests)</span></span>

<span data-ttu-id="f713c-151">Como aprovador delegado, você receberá notificações por email quando uma solicitação estiver aguardando sua aprovação.</span><span class="sxs-lookup"><span data-stu-id="f713c-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="f713c-152">Para exibir essas solicitações no portal do PIM, no painel (na nova barra de navegação), selecione a guia “Solicitações com Aprovação Pendente” na barra de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="f713c-152">To view these requests in the PIM portal, from the dashboard (in the new navigation) select the “Pending Approval Requests” tab in the left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="f713c-153">Aqui, você verá uma lista de solicitações com aprovação pendente:</span><span class="sxs-lookup"><span data-stu-id="f713c-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="f713c-154">Aprovar ou rejeitar solicitações de elevação de função (única e/ou em massa)</span><span class="sxs-lookup"><span data-stu-id="f713c-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="f713c-155">Selecione as solicitações que você deseja aprovar ou negar e clique no botão na barra de ação que corresponde à sua decisão:</span><span class="sxs-lookup"><span data-stu-id="f713c-155">Select the requests you wish to approve or deny, and click the button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="f713c-156">Fornecer uma justificativa para minha aprovação/rejeição</span><span class="sxs-lookup"><span data-stu-id="f713c-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="f713c-157">Isso abrirá uma nova folha para aprovar ou negar várias solicitações ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="f713c-157">This will open a new blade to approve or deny multiple requests at once.</span></span> <span data-ttu-id="f713c-158">Insira uma justificativa para sua decisão e clique em Aprovar (ou Negar) na parte inferior ou na folha:</span><span class="sxs-lookup"><span data-stu-id="f713c-158">Enter a justification for your decision, and click approve (or deny) at the bottom or the blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="f713c-159">Quando o processo de solicitação for concluído, o símbolo de status refletirá a decisão tomada (neste exemplo, a decisão é aprovar):</span><span class="sxs-lookup"><span data-stu-id="f713c-159">When the request process is complete, the status symbol will reflect the decision you made (in this example, the decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="f713c-160">Solicitar a ativação de uma função que exige aprovação</span><span class="sxs-lookup"><span data-stu-id="f713c-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="f713c-161">A solicitação da ativação de uma função que exige aprovação pode ser iniciada na barra de navegação antiga do PIM ou na nova barra de navegação, pois o processo de ativação de função permanece o mesmo.</span><span class="sxs-lookup"><span data-stu-id="f713c-161">Requesting activation of a role that requires approval may be initiated from either the old PIM navigation, or the new navigation, as the process for role activation remains the same.</span></span> <span data-ttu-id="f713c-162">Basta selecionar uma função na lista de funções a ser ativada:</span><span class="sxs-lookup"><span data-stu-id="f713c-162">Simply select a role from the list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="f713c-163">Se uma função com privilégios exigir a Autenticação Multifator, você deverá concluir essa tarefa primeiro:</span><span class="sxs-lookup"><span data-stu-id="f713c-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="f713c-164">Depois de concluída, clique em Ativar e forneça uma justificativa (se necessário):</span><span class="sxs-lookup"><span data-stu-id="f713c-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="f713c-165">O solicitante verá uma notificação indicando que a solicitação está com aprovação pendente:</span><span class="sxs-lookup"><span data-stu-id="f713c-165">The requestor will see a notification that the request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-the-status-of-your-request-to-activate"></a><span data-ttu-id="f713c-166">Exibir o status de sua solicitação a ser ativada</span><span class="sxs-lookup"><span data-stu-id="f713c-166">View the status of your request to activate</span></span>

<span data-ttu-id="f713c-167">A exibição do status de uma solicitação pendente a ser ativada deve ser acessada na nova barra de navegação.</span><span class="sxs-lookup"><span data-stu-id="f713c-167">Viewing the status of a pending request to activate must be accessed from the new navigation.</span></span> <span data-ttu-id="f713c-168">Na barra de navegação à esquerda, selecione a guia “Minhas Solicitações”:</span><span class="sxs-lookup"><span data-stu-id="f713c-168">From the left navigation bar, select the “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="f713c-169">O estado de solicitação usa “Pendente” como padrão, mas é possível ativar/desativar para ver todas as solicitações ou as solicitações negadas.</span><span class="sxs-lookup"><span data-stu-id="f713c-169">The request state defaults to “Pending”, but you can toggle to see all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="f713c-170">Concluir a tarefa no Azure AD caso a ativação tenha sido aprovada</span><span class="sxs-lookup"><span data-stu-id="f713c-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="f713c-171">Depois que a solicitação for aprovada, a função ficará ativa e você poderá continuar com qualquer trabalho que exige essa função.</span><span class="sxs-lookup"><span data-stu-id="f713c-171">Once the request is approved, the role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="f713c-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f713c-172">Next steps</span></span>

<span data-ttu-id="f713c-173">Seu comentário é valioso para nós.</span><span class="sxs-lookup"><span data-stu-id="f713c-173">Your feedback is valuable to us.</span></span> <span data-ttu-id="f713c-174">Fique à vontade compartilhar seus comentários conosco aqui!</span><span class="sxs-lookup"><span data-stu-id="f713c-174">Please feel free to share comments or feedback with us here!</span></span>
