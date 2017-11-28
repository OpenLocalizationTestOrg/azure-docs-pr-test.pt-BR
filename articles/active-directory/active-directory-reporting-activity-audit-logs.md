---
title: "relatórios de atividade de aaaAudit no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Relatórios de atividade no portal do Azure Active Directory Olá de auditoria toohello de Introdução"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="7272c-103">Relatórios de atividade no portal do Azure Active Directory Olá de auditoria</span><span class="sxs-lookup"><span data-stu-id="7272c-103">Audit activity reports in hello Azure Active Directory portal</span></span> 

<span data-ttu-id="7272c-104">Com o relatório no Azure Active Directory (AD do Azure), você pode obter informações de saudação necessário toodetermine como seu ambiente está fazendo.</span><span class="sxs-lookup"><span data-stu-id="7272c-104">With reporting in Azure Active Directory (Azure AD), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="7272c-105">Olá arquitetura de relatórios no AD do Azure consiste em Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="7272c-105">hello reporting architecture in Azure AD consists of hello following components:</span></span>

- <span data-ttu-id="7272c-106">**Atividade**</span><span class="sxs-lookup"><span data-stu-id="7272c-106">**Activity**</span></span> 
    - <span data-ttu-id="7272c-107">**Atividades de entrada** – informações sobre o uso de saudação de aplicativos gerenciados e atividades de entrada do usuário</span><span class="sxs-lookup"><span data-stu-id="7272c-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="7272c-108">**Logs de auditoria** – informações de atividade do sistema sobre o gerenciamento de usuários e de grupos, sobre os aplicativos gerenciados e sobre as atividades de diretório.</span><span class="sxs-lookup"><span data-stu-id="7272c-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="7272c-109">**Segurança**</span><span class="sxs-lookup"><span data-stu-id="7272c-109">**Security**</span></span> 
    - <span data-ttu-id="7272c-110">**Entradas arriscadas** -uma entrada arriscado é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é proprietário legítimo Olá uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="7272c-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="7272c-111">Para obter mais detalhes, veja Entradas de risco.</span><span class="sxs-lookup"><span data-stu-id="7272c-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="7272c-112">**Usuários sinalizados para riscos** - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="7272c-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="7272c-113">Para obter mais detalhes, consulte Usuários sinalizados para risco.</span><span class="sxs-lookup"><span data-stu-id="7272c-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="7272c-114">Este tópico fornece uma visão geral das atividades de auditoria de saudação.</span><span class="sxs-lookup"><span data-stu-id="7272c-114">This topic gives you an overview of hello audit activities.</span></span>
 
## <a name="who-can-access-hello-data"></a><span data-ttu-id="7272c-115">Quem pode acessar dados Olá?</span><span class="sxs-lookup"><span data-stu-id="7272c-115">Who can access hello data?</span></span>
* <span data-ttu-id="7272c-116">Usuários na função de administrador de segurança ou segurança leitor Olá</span><span class="sxs-lookup"><span data-stu-id="7272c-116">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="7272c-117">Administradores globais</span><span class="sxs-lookup"><span data-stu-id="7272c-117">Global Admins</span></span>
* <span data-ttu-id="7272c-118">Os usuários individuais (não administradores) podem ver suas próprias atividades</span><span class="sxs-lookup"><span data-stu-id="7272c-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="7272c-119">Logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="7272c-119">Audit logs</span></span>

<span data-ttu-id="7272c-120">logs de auditoria de saudação no Active Directory do Azure fornecem registros de atividades de sistema para fins de conformidade.</span><span class="sxs-lookup"><span data-stu-id="7272c-120">hello audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="7272c-121">É o primeiro tooall de ponto de entrada dados de auditoria **logs de auditoria** em Olá **atividade** seção **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="7272c-121">Your first entry point tooall auditing data is **Audit logs** in hello **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="7272c-122">![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/61.png "Logs de auditoria")</span><span class="sxs-lookup"><span data-stu-id="7272c-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="7272c-123">Um log de auditoria tem um modo de exibição de lista padrão que mostra:</span><span class="sxs-lookup"><span data-stu-id="7272c-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="7272c-124">Data de saudação e a hora da ocorrência da saudação</span><span class="sxs-lookup"><span data-stu-id="7272c-124">hello date and time of hello occurrence</span></span>
- <span data-ttu-id="7272c-125">Olá iniciador / ator (*que*) de uma atividade</span><span class="sxs-lookup"><span data-stu-id="7272c-125">hello initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="7272c-126">Hello atividade (*que*)</span><span class="sxs-lookup"><span data-stu-id="7272c-126">hello activity (*what*)</span></span> 
- <span data-ttu-id="7272c-127">destino de saudação</span><span class="sxs-lookup"><span data-stu-id="7272c-127">hello target</span></span>

<span data-ttu-id="7272c-128">![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/18.png "Logs de auditoria")</span><span class="sxs-lookup"><span data-stu-id="7272c-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="7272c-129">Você pode personalizar o modo de exibição de lista Olá clicando **colunas** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="7272c-129">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="7272c-130">![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/19.png "Logs de auditoria")</span><span class="sxs-lookup"><span data-stu-id="7272c-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="7272c-131">Isso permite que os campos adicionais toodisplay ou remover campos que já estão sendo exibidos.</span><span class="sxs-lookup"><span data-stu-id="7272c-131">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="7272c-132">![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/21.png "Logs de auditoria")</span><span class="sxs-lookup"><span data-stu-id="7272c-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="7272c-133">Ao clicar em um item na exibição de lista Olá, você deve obter todos os detalhes disponíveis sobre ele.</span><span class="sxs-lookup"><span data-stu-id="7272c-133">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="7272c-134">![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/22.png "Logs de auditoria")</span><span class="sxs-lookup"><span data-stu-id="7272c-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="7272c-135">Filtragem de logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="7272c-135">Filtering audit logs</span></span>

<span data-ttu-id="7272c-136">toonarrow inativo saudação relatados nível tooa de dados que funciona para você, você pode filtrar os dados de auditoria hello usando Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7272c-136">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="7272c-137">Intervalo de datas</span><span class="sxs-lookup"><span data-stu-id="7272c-137">Date range</span></span>
- <span data-ttu-id="7272c-138">Iniciado por (ator)</span><span class="sxs-lookup"><span data-stu-id="7272c-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="7272c-139">Categoria</span><span class="sxs-lookup"><span data-stu-id="7272c-139">Category</span></span>
- <span data-ttu-id="7272c-140">Tipo de recurso de atividade</span><span class="sxs-lookup"><span data-stu-id="7272c-140">Activity resource type</span></span>
- <span data-ttu-id="7272c-141">Atividade</span><span class="sxs-lookup"><span data-stu-id="7272c-141">Activity</span></span>

<span data-ttu-id="7272c-142">![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/23.png "Logs de auditoria")</span><span class="sxs-lookup"><span data-stu-id="7272c-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="7272c-143">Olá **intervalo de datas** filtro habilita tooyou toodefine um período de tempo para Olá retornou dados.</span><span class="sxs-lookup"><span data-stu-id="7272c-143">hello **date range** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="7272c-144">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="7272c-144">Possible values are:</span></span>

- <span data-ttu-id="7272c-145">1 mês</span><span class="sxs-lookup"><span data-stu-id="7272c-145">1 month</span></span>
- <span data-ttu-id="7272c-146">7 dias</span><span class="sxs-lookup"><span data-stu-id="7272c-146">7 days</span></span>
- <span data-ttu-id="7272c-147">24 horas</span><span class="sxs-lookup"><span data-stu-id="7272c-147">24 hours</span></span>
- <span data-ttu-id="7272c-148">Personalizado</span><span class="sxs-lookup"><span data-stu-id="7272c-148">Custom</span></span>

<span data-ttu-id="7272c-149">Quando você seleciona um período de tempo personalizado, pode configurar uma hora de início e uma hora de término.</span><span class="sxs-lookup"><span data-stu-id="7272c-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="7272c-150">Olá **iniciada pelo** filtro permite que você toodefine nome de um ator ou seu nome de entidade de segurança universal (UPN).</span><span class="sxs-lookup"><span data-stu-id="7272c-150">hello **initiated by** filter enables you toodefine an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="7272c-151">Olá **categoria** filtro permite tooselect de saudação filtro a seguir:</span><span class="sxs-lookup"><span data-stu-id="7272c-151">hello **category** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="7272c-152">Todos</span><span class="sxs-lookup"><span data-stu-id="7272c-152">All</span></span>
- <span data-ttu-id="7272c-153">Categoria principal</span><span class="sxs-lookup"><span data-stu-id="7272c-153">Core category</span></span>
- <span data-ttu-id="7272c-154">Diretório principal</span><span class="sxs-lookup"><span data-stu-id="7272c-154">Core directory</span></span>
- <span data-ttu-id="7272c-155">Gerenciamento de senhas de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="7272c-155">Self-service password management</span></span>
- <span data-ttu-id="7272c-156">Gerenciamento de grupo de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="7272c-156">Self-service group management</span></span>
- <span data-ttu-id="7272c-157">Provisionamento de conta - Substituição de senha automática</span><span class="sxs-lookup"><span data-stu-id="7272c-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="7272c-158">Usuários convidados</span><span class="sxs-lookup"><span data-stu-id="7272c-158">Invited users</span></span>
- <span data-ttu-id="7272c-159">Serviço MIM</span><span class="sxs-lookup"><span data-stu-id="7272c-159">MIM service</span></span>
- <span data-ttu-id="7272c-160">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="7272c-160">Identity Protection</span></span>
- <span data-ttu-id="7272c-161">B2C</span><span class="sxs-lookup"><span data-stu-id="7272c-161">B2C</span></span>

<span data-ttu-id="7272c-162">Olá **tipo de recurso de atividade** filtro permite tooselect Olá seguinte filtros:</span><span class="sxs-lookup"><span data-stu-id="7272c-162">hello **activity resource type** filter enables you tooselect one of hello following filters:</span></span>

- <span data-ttu-id="7272c-163">Todos</span><span class="sxs-lookup"><span data-stu-id="7272c-163">All</span></span> 
- <span data-ttu-id="7272c-164">Agrupar</span><span class="sxs-lookup"><span data-stu-id="7272c-164">Group</span></span>
- <span data-ttu-id="7272c-165">Diretório</span><span class="sxs-lookup"><span data-stu-id="7272c-165">Directory</span></span>
- <span data-ttu-id="7272c-166">Usuário</span><span class="sxs-lookup"><span data-stu-id="7272c-166">User</span></span>
- <span data-ttu-id="7272c-167">Aplicativo</span><span class="sxs-lookup"><span data-stu-id="7272c-167">Application</span></span>
- <span data-ttu-id="7272c-168">Política</span><span class="sxs-lookup"><span data-stu-id="7272c-168">Policy</span></span>
- <span data-ttu-id="7272c-169">Dispositivo</span><span class="sxs-lookup"><span data-stu-id="7272c-169">Device</span></span>
- <span data-ttu-id="7272c-170">outro</span><span class="sxs-lookup"><span data-stu-id="7272c-170">Other</span></span>

<span data-ttu-id="7272c-171">Quando você seleciona **grupo** como **tipo de recurso de atividade**, você obtém uma categoria de filtro adicional que permite que você tooalso fornecem uma **origem**:</span><span class="sxs-lookup"><span data-stu-id="7272c-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you tooalso provide a **Source**:</span></span>

- <span data-ttu-id="7272c-172">AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7272c-172">Azure AD</span></span>
- <span data-ttu-id="7272c-173">O365</span><span class="sxs-lookup"><span data-stu-id="7272c-173">O365</span></span>


<span data-ttu-id="7272c-174">Olá **atividade** filtro se baseia na categoria hello e seleção do tipo de recurso de atividade feitas.</span><span class="sxs-lookup"><span data-stu-id="7272c-174">hello **activity** filter is based on hello category and Activity resource type selection you make.</span></span> <span data-ttu-id="7272c-175">Você pode selecionar uma atividade específica que deseja toosee ou escolha todas as.</span><span class="sxs-lookup"><span data-stu-id="7272c-175">You can select a specific activity you want toosee or choose all.</span></span> 

<span data-ttu-id="7272c-176">Você pode obter a lista de saudação de todas as atividades de auditoria usando Olá Graph API https://graph.windows.net/$ atividades/tenantdomain/auditActivityTypes? api-version = beta, onde $tenantdomain = seu nome de domínio ou consulte o artigo toohello [relatório de auditoria eventos](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="7272c-176">You can get hello list of all Audit Activities using hello Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer toohello article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="7272c-177">Atalhos de logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="7272c-177">Audit logs shortcuts</span></span>

<span data-ttu-id="7272c-178">Além disso muito**Active Directory do Azure**, hello portal do Azure oferece dois pontos de entrada adicional tooaudit dados:</span><span class="sxs-lookup"><span data-stu-id="7272c-178">In addition too**Azure Active Directory**, hello Azure portal provides you with two additional entry points tooaudit data:</span></span>

- <span data-ttu-id="7272c-179">Usuários e grupos</span><span class="sxs-lookup"><span data-stu-id="7272c-179">Users and groups</span></span>
- <span data-ttu-id="7272c-180">Aplicativos empresariais</span><span class="sxs-lookup"><span data-stu-id="7272c-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="7272c-181">Logs de auditoria de usuários e grupos</span><span class="sxs-lookup"><span data-stu-id="7272c-181">Users and groups audit logs</span></span>

<span data-ttu-id="7272c-182">Com relatórios de auditoria com base em grupo e usuário, você pode obter respostas tooquestions como:</span><span class="sxs-lookup"><span data-stu-id="7272c-182">With user and group-based audit reports, you can get answers tooquestions such as:</span></span>

- <span data-ttu-id="7272c-183">Que tipos de atualizações foram usuários Olá aplicadas?</span><span class="sxs-lookup"><span data-stu-id="7272c-183">What types of updates have been applied hello users?</span></span>

- <span data-ttu-id="7272c-184">Quantos usuários foram alterados?</span><span class="sxs-lookup"><span data-stu-id="7272c-184">How many users were changed?</span></span>

- <span data-ttu-id="7272c-185">Quantas senhas foram alteradas?</span><span class="sxs-lookup"><span data-stu-id="7272c-185">How many passwords were changed?</span></span>

- <span data-ttu-id="7272c-186">O que um administrador fez em um diretório?</span><span class="sxs-lookup"><span data-stu-id="7272c-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="7272c-187">O que são grupos de saudação que foram adicionados?</span><span class="sxs-lookup"><span data-stu-id="7272c-187">What are hello groups that have been added?</span></span>

- <span data-ttu-id="7272c-188">Existem grupos com alterações de associação?</span><span class="sxs-lookup"><span data-stu-id="7272c-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="7272c-189">Os proprietários de saudação do grupo foram alterados?</span><span class="sxs-lookup"><span data-stu-id="7272c-189">Have hello owners of group been changed?</span></span>

- <span data-ttu-id="7272c-190">Quais licenças tiverem recebidas um usuário ou grupo tooa?</span><span class="sxs-lookup"><span data-stu-id="7272c-190">What licenses have been assigned tooa group or a user?</span></span>

<span data-ttu-id="7272c-191">Se você quiser apenas tooreview dados toousers relacionados e grupos de auditoria, você pode encontrar uma exibição filtrada em **logs de auditoria** em Olá **atividade** seção Olá **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7272c-191">If you just want tooreview auditing data that is related toousers and groups, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Users and Groups**.</span></span> <span data-ttu-id="7272c-192">Esse ponto de entrada tem **Usuários e grupos** como **Tipo de Recurso de Atividade** pré-selecionado.</span><span class="sxs-lookup"><span data-stu-id="7272c-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="7272c-193">![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/93.png "Logs de auditoria")</span><span class="sxs-lookup"><span data-stu-id="7272c-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="7272c-194">Logs de auditoria de aplicativos empresariais</span><span class="sxs-lookup"><span data-stu-id="7272c-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="7272c-195">Com o aplicativo com base em relatórios de auditoria, você pode obter respostas tooquestions como:</span><span class="sxs-lookup"><span data-stu-id="7272c-195">With application-based audit reports, you can get answers tooquestions such as:</span></span>

* <span data-ttu-id="7272c-196">Quais são os aplicativos de saudação que foram adicionados ou atualizados?</span><span class="sxs-lookup"><span data-stu-id="7272c-196">What are hello applications that have been added or updated?</span></span>
* <span data-ttu-id="7272c-197">Quais são os aplicativos de saudação que foram removidos?</span><span class="sxs-lookup"><span data-stu-id="7272c-197">What are hello applications that have been removed?</span></span>
* <span data-ttu-id="7272c-198">Um princípio de serviço para um aplicativo foi alterado?</span><span class="sxs-lookup"><span data-stu-id="7272c-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="7272c-199">Nomes de saudação de aplicativos foram alterados?</span><span class="sxs-lookup"><span data-stu-id="7272c-199">Have hello names of applications been changed?</span></span>
* <span data-ttu-id="7272c-200">Que forneceu o consentimento tooan aplicativo?</span><span class="sxs-lookup"><span data-stu-id="7272c-200">Who gave consent tooan application?</span></span>

<span data-ttu-id="7272c-201">Se você quiser apenas tooreview dados de aplicativos tooyour relacionadas a auditoria, você pode encontrar uma exibição filtrada em **logs de auditoria** em Olá **atividade** seção Olá **aplicativos empresariais**  folha.</span><span class="sxs-lookup"><span data-stu-id="7272c-201">If you just want tooreview auditing data that is related tooyour applications, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Enterprise applications** blade.</span></span> <span data-ttu-id="7272c-202">Esse ponto de entrada tem **aplicativos empresariais** como **tipo de recurso de atividade** pré-selecionado.</span><span class="sxs-lookup"><span data-stu-id="7272c-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="7272c-203">![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/134.png "Logs de auditoria")</span><span class="sxs-lookup"><span data-stu-id="7272c-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="7272c-204">Você pode filtrar essa exibição para baixo toojust **grupos** ou apenas **usuários**.</span><span class="sxs-lookup"><span data-stu-id="7272c-204">You can filter this view further down toojust **groups** or just **users**.</span></span>

<span data-ttu-id="7272c-205">![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/25.png "Logs de auditoria")</span><span class="sxs-lookup"><span data-stu-id="7272c-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="7272c-206">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7272c-206">Next steps</span></span>

<span data-ttu-id="7272c-207">Para obter uma visão geral de emissão de relatórios, consulte Olá [reporting do Active Directory do Azure](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7272c-207">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

