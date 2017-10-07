---
title: "relatórios de atividade de aaaFind em Olá portal do Azure | Microsoft Docs"
description: "Saiba como os relatórios de toofind atividade do Active Directory do Azure no hello portal do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a><span data-ttu-id="bc69c-103">Localizar relatórios de atividade no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bc69c-103">Find activity reports in hello Azure portal</span></span>

<span data-ttu-id="bc69c-104">Se você estiver movendo de saudação toohello de portal clássico do Azure portal do Azure, você obtém uma nova aparência em logs de atividades do Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="bc69c-104">If you are moving from hello Azure classic portal toohello Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="bc69c-105">Em uma recente [postagem de blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), explicaremos como você pode ver os logs de atividades no contexto de saudação do recurso Olá você está trabalhando em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc69c-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in hello context of hello resource you are working on in hello Azure portal.</span></span> <span data-ttu-id="bc69c-106">Neste artigo, descreveremos como toofind relatórios que você usou no portal clássico do Azure no portal do Azure de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="bc69c-106">In this article, we describe how toofind reports that you used in hello Azure classic portal in hello Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="bc69c-107">Novidades</span><span class="sxs-lookup"><span data-stu-id="bc69c-107">What's new</span></span>

<span data-ttu-id="bc69c-108">Relatórios no portal clássico do Azure de saudação são separados em categorias:</span><span class="sxs-lookup"><span data-stu-id="bc69c-108">Reports in hello Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="bc69c-109">Relatórios de segurança</span><span class="sxs-lookup"><span data-stu-id="bc69c-109">Security reports</span></span>
2.  <span data-ttu-id="bc69c-110">Relatórios de atividades</span><span class="sxs-lookup"><span data-stu-id="bc69c-110">Activity reports</span></span>
3.  <span data-ttu-id="bc69c-111">Relatórios de aplicativo integrados</span><span class="sxs-lookup"><span data-stu-id="bc69c-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="bc69c-112">Relatórios do aplicativo integrado e de atividade</span><span class="sxs-lookup"><span data-stu-id="bc69c-112">Activity and integrated app reports</span></span>

<span data-ttu-id="bc69c-113">Para o contexto de acordo com relatórios no hello portal do Azure, os relatórios existentes são mesclados em uma única exibição.</span><span class="sxs-lookup"><span data-stu-id="bc69c-113">For context-based reporting in hello Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="bc69c-114">Uma única API subjacente fornece Olá dados toohello exibição.</span><span class="sxs-lookup"><span data-stu-id="bc69c-114">A single, underlying API provides hello data toohello view.</span></span>

<span data-ttu-id="bc69c-115">toosee essa exibição em Olá **Active Directory do Azure** folha, em **atividade**, selecione **logs de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-115">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="bc69c-116">![Logs de auditoria](./media/active-directory-reporting-migration/482.png "Logs de auditoria")</span><span class="sxs-lookup"><span data-stu-id="bc69c-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="bc69c-117">Olá relatórios a seguir é consolidado nesta exibição:</span><span class="sxs-lookup"><span data-stu-id="bc69c-117">hello following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="bc69c-118">Relatório de auditoria</span><span class="sxs-lookup"><span data-stu-id="bc69c-118">Audit report</span></span>
-   <span data-ttu-id="bc69c-119">Atividade de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="bc69c-119">Password reset activity</span></span>
-   <span data-ttu-id="bc69c-120">Atividade de registro de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="bc69c-120">Password reset registration activity</span></span>
-   <span data-ttu-id="bc69c-121">Atividade dos grupos de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="bc69c-121">Self-service groups activity</span></span>
-   <span data-ttu-id="bc69c-122">Alterações de nome do grupo do Office365</span><span class="sxs-lookup"><span data-stu-id="bc69c-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="bc69c-123">Atividade de provisionamento de conta</span><span class="sxs-lookup"><span data-stu-id="bc69c-123">Account provisioning activity</span></span>
-   <span data-ttu-id="bc69c-124">Status de substituição de senha</span><span class="sxs-lookup"><span data-stu-id="bc69c-124">Password rollover status</span></span>
-   <span data-ttu-id="bc69c-125">Erros de provisionamento de conta</span><span class="sxs-lookup"><span data-stu-id="bc69c-125">Account provisioning errors</span></span>


<span data-ttu-id="bc69c-126">Olá relatório de uso do aplicativo foi aprimorada e está incluído no hello **entradas** exibição.</span><span class="sxs-lookup"><span data-stu-id="bc69c-126">hello Application Usage report has been enhanced and is included in hello **Sign-ins** view.</span></span> <span data-ttu-id="bc69c-127">toosee essa exibição em Olá **Active Directory do Azure** folha, em **atividade**, selecione **entradas**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-127">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="bc69c-128">![Exibição de entradas](./media/active-directory-reporting-migration/483.png "Exibição de entradas")</span><span class="sxs-lookup"><span data-stu-id="bc69c-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="bc69c-129">Olá **entradas** exibição inclui todas as entradas do usuário. Você pode usar essas informações de uso de aplicativo de tooget informações.</span><span class="sxs-lookup"><span data-stu-id="bc69c-129">hello **Sign-ins** view includes all user sign-ins. You can use this information tooget application usage information.</span></span> <span data-ttu-id="bc69c-130">Você também pode exibir informações de uso do aplicativo no hello **aplicativos empresariais** visão geral, em Olá **gerenciar** seção.</span><span class="sxs-lookup"><span data-stu-id="bc69c-130">You also can view application usage information in hello **Enterprise applications** overview, in hello **MANAGE** section.</span></span>

<span data-ttu-id="bc69c-131">![Aplicativos empresariais](./media/active-directory-reporting-migration/484.png "Aplicativos empresariais")</span><span class="sxs-lookup"><span data-stu-id="bc69c-131">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="bc69c-132">Acessar uma porta específica</span><span class="sxs-lookup"><span data-stu-id="bc69c-132">Access a specific report</span></span>

<span data-ttu-id="bc69c-133">Embora Olá portal do Azure oferece uma única exibição, você também pode examinar relatórios específicos.</span><span class="sxs-lookup"><span data-stu-id="bc69c-133">Although hello Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="bc69c-134">Logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="bc69c-134">Audit logs</span></span>

<span data-ttu-id="bc69c-135">Comentários de toocustomer de resposta, no Olá portal do Azure, você pode usar avançada filtragem tooaccess Olá de dados desejado.</span><span class="sxs-lookup"><span data-stu-id="bc69c-135">In response toocustomer feedback, in hello Azure portal, you can use advanced filtering tooaccess hello data you want.</span></span> <span data-ttu-id="bc69c-136">É um filtro que você pode usar um *categoria de atividade*, que lista os tipos diferentes de saudação da atividade de logs no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc69c-136">One filter you can use is an *activity category*, which lists hello different types of activity logs in Azure AD.</span></span> <span data-ttu-id="bc69c-137">toonarrow resulta toowhat que você está procurando, você pode selecionar uma categoria.</span><span class="sxs-lookup"><span data-stu-id="bc69c-137">toonarrow results toowhat you are looking for, you can select a category.</span></span>

<span data-ttu-id="bc69c-138">Por exemplo, se você estiver interessado apenas em redefinições de senha de serviço tooself relacionados de atividades, você pode escolher Olá **gerenciamento de senha de autoatendimento** categoria.</span><span class="sxs-lookup"><span data-stu-id="bc69c-138">For example, if you are interested only in activities related tooself-service password resets, you can choose hello **Self-service Password Management** category.</span></span> <span data-ttu-id="bc69c-139">categorias de saudação que você ver se baseiam em recursos Olá que você está trabalhando no.</span><span class="sxs-lookup"><span data-stu-id="bc69c-139">hello categories you see are based on hello resource you are working in.</span></span>  

<span data-ttu-id="bc69c-140">![Opções de categoria na página de Logs de auditoria de filtro Olá](./media/active-directory-reporting-migration/06.png "opções de categoria na página de Logs de auditoria de filtro de saudação")</span><span class="sxs-lookup"><span data-stu-id="bc69c-140">![Category options on hello Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on hello Filter Audit Logs page")</span></span>

<span data-ttu-id="bc69c-141">As categorias de atividades incluem:</span><span class="sxs-lookup"><span data-stu-id="bc69c-141">Activity categories include:</span></span>

- <span data-ttu-id="bc69c-142">Diretório principal</span><span class="sxs-lookup"><span data-stu-id="bc69c-142">Core Directory</span></span>
- <span data-ttu-id="bc69c-143">Gerenciamento de senhas de auto-atendimento</span><span class="sxs-lookup"><span data-stu-id="bc69c-143">Self-service Password Management</span></span>
- <span data-ttu-id="bc69c-144">Gerenciamento de grupos de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="bc69c-144">Self-service Group Management</span></span>
- <span data-ttu-id="bc69c-145">Provisionamento de conta de usuário</span><span class="sxs-lookup"><span data-stu-id="bc69c-145">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="bc69c-146">Uso do aplicativo</span><span class="sxs-lookup"><span data-stu-id="bc69c-146">Application usage</span></span>

<span data-ttu-id="bc69c-147">tooview detalhes sobre o uso do aplicativo para todos os aplicativos ou para um único aplicativo, em **atividade**, selecione **entradas**. resultados de saudação toonarrow, você pode filtrar no nome de usuário ou nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bc69c-147">tooview details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. toonarrow hello results, you can filter on user name or application name.</span></span>

<span data-ttu-id="bc69c-148">![Página Filtrar Eventos de Entrada](./media/active-directory-reporting-migration/07.png "Página Filtrar Eventos de Entrada")</span><span class="sxs-lookup"><span data-stu-id="bc69c-148">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="bc69c-149">Relatórios de segurança</span><span class="sxs-lookup"><span data-stu-id="bc69c-149">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="bc69c-150">Relatórios de atividades anômalas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc69c-150">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="bc69c-151">Segurança de atividade anormal do AD do Azure relatórios de saudação portal clássico do Azure foram consolidado tooprovide você com um modo de exibição central.</span><span class="sxs-lookup"><span data-stu-id="bc69c-151">Azure AD anomalous activity security reports from hello Azure classic portal have been consolidated tooprovide you with one, central view.</span></span> <span data-ttu-id="bc69c-152">Essa exibição mostra todos os eventos de risco relacionado à segurança que o Azure AD pode detectar e relatar.</span><span class="sxs-lookup"><span data-stu-id="bc69c-152">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="bc69c-153">Olá a tabela a seguir lista os relatórios de segurança de atividade anormal de saudação do AD do Azure e tipos de eventos de risco correspondentes no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc69c-153">hello following table lists hello Azure AD anomalous activity security reports, and corresponding risk event types in hello Azure portal.</span></span>

| <span data-ttu-id="bc69c-154">Relatório de atividades anômalas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc69c-154">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="bc69c-155">Tipo de evento de risco do Identity Protection</span><span class="sxs-lookup"><span data-stu-id="bc69c-155">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="bc69c-156">Usuários com credenciais vazadas</span><span class="sxs-lookup"><span data-stu-id="bc69c-156">Users with leaked credentials</span></span> | <span data-ttu-id="bc69c-157">Credenciais vazadas</span><span class="sxs-lookup"><span data-stu-id="bc69c-157">Leaked credentials</span></span> |
| <span data-ttu-id="bc69c-158">Atividades de entrada irregulares</span><span class="sxs-lookup"><span data-stu-id="bc69c-158">Irregular sign-in activity</span></span> | <span data-ttu-id="bc69c-159">Viagem impossível tooatypical locais</span><span class="sxs-lookup"><span data-stu-id="bc69c-159">Impossible travel tooatypical locations</span></span> |
| <span data-ttu-id="bc69c-160">Entradas de dispositivos possivelmente infectados</span><span class="sxs-lookup"><span data-stu-id="bc69c-160">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="bc69c-161">Entradas de dispositivos infectados</span><span class="sxs-lookup"><span data-stu-id="bc69c-161">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="bc69c-162">Entradas de fontes desconhecidas</span><span class="sxs-lookup"><span data-stu-id="bc69c-162">Sign-ins from unknown sources</span></span> | <span data-ttu-id="bc69c-163">Entradas de endereços IP anônimos</span><span class="sxs-lookup"><span data-stu-id="bc69c-163">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="bc69c-164">Entradas de endereços IP com atividade suspeita</span><span class="sxs-lookup"><span data-stu-id="bc69c-164">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="bc69c-165">Entradas de endereços IP com atividade suspeita</span><span class="sxs-lookup"><span data-stu-id="bc69c-165">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="bc69c-166">Entradas de locais desconhecidos</span><span class="sxs-lookup"><span data-stu-id="bc69c-166">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="bc69c-167">Olá, segurança de atividade anormal do AD do Azure a seguir relata não são incluídos como eventos de risco em Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="bc69c-167">hello following Azure AD anomalous activity security reports are not included as risk events in hello Azure portal:</span></span>

* <span data-ttu-id="bc69c-168">Entradas após várias falhas</span><span class="sxs-lookup"><span data-stu-id="bc69c-168">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="bc69c-169">Entradas de várias geografias</span><span class="sxs-lookup"><span data-stu-id="bc69c-169">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="bc69c-170">Esses relatórios ainda estão disponíveis no portal clássico do Azure de hello, mas eles serão substituídos em algum momento futuro de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc69c-170">These reports are still available in hello Azure classic portal, but they will be deprecated at some time in hello future.</span></span>

<span data-ttu-id="bc69c-171">Para saber mais, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="bc69c-171">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="bc69c-172">Eventos de risco detectados</span><span class="sxs-lookup"><span data-stu-id="bc69c-172">Detected risk events</span></span>

<span data-ttu-id="bc69c-173">No hello portal do Azure, você pode acessar relatórios sobre eventos de risco detectados em Olá **Active Directory do Azure** folha, em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-173">In hello Azure portal, you can access reports about detected risk events on hello **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="bc69c-174">Eventos de risco detectados são rastreados em Olá relatórios a seguir:</span><span class="sxs-lookup"><span data-stu-id="bc69c-174">Detected risk events are tracked in hello following reports:</span></span>   

- <span data-ttu-id="bc69c-175">Usuários em risco</span><span class="sxs-lookup"><span data-stu-id="bc69c-175">Users at Risk</span></span>
- <span data-ttu-id="bc69c-176">Entradas de risco</span><span class="sxs-lookup"><span data-stu-id="bc69c-176">Risky Sign-ins</span></span>

<span data-ttu-id="bc69c-177">![Relatórios de segurança](./media/active-directory-reporting-migration/04.png "Relatórios de segurança")</span><span class="sxs-lookup"><span data-stu-id="bc69c-177">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="bc69c-178">Para saber mais sobre relatórios de segurança, veja:</span><span class="sxs-lookup"><span data-stu-id="bc69c-178">For more information about security reports, see:</span></span>

- [<span data-ttu-id="bc69c-179">Usuários no relatório de riscos de segurança no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="bc69c-179">Users at Risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="bc69c-180">Relatório de entradas arriscado no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="bc69c-180">Risky Sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a><span data-ttu-id="bc69c-181">Relatórios de atividade no hello portal clássico do Azure versus Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bc69c-181">Activity reports in hello Azure classic portal vs. hello Azure portal</span></span>

<span data-ttu-id="bc69c-182">tabela Olá nesta seção lista os relatórios existentes em Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc69c-182">hello table in this section lists existing reports in hello Azure classic portal.</span></span> <span data-ttu-id="bc69c-183">Ele também descreve como você pode obter Olá as mesmas informações no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc69c-183">It also describes how you can get hello same information in hello Azure portal.</span></span>

<span data-ttu-id="bc69c-184">tooview todos os dados na saudação de auditoria **Active Directory do Azure** folha, em **atividade**, ir muito**logs de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-184">tooview all auditing data, on hello **Azure Active Directory** blade, under **ACTIVITY**, go too**Audit logs**.</span></span>

<span data-ttu-id="bc69c-185">![Logs de auditoria](./media/active-directory-reporting-migration/61.png "Logs de auditoria")</span><span class="sxs-lookup"><span data-stu-id="bc69c-185">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="bc69c-186">portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="bc69c-186">Azure classic portal</span></span>                 | <span data-ttu-id="bc69c-187">toofind em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bc69c-187">toofind in hello Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="bc69c-188">Logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="bc69c-188">Audit logs</span></span>                           | <span data-ttu-id="bc69c-189">Para **Categoria da Atividade**, selecione **Diretório Principal**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-189">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="bc69c-190">Atividade de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="bc69c-190">Password reset activity</span></span>              | <span data-ttu-id="bc69c-191">Para **Categoria da Atividade**, selecione **Gerenciamento de Senhas de Autoatendimento**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-191">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="bc69c-192">Atividade de registro de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="bc69c-192">Password reset registration activity</span></span> | <span data-ttu-id="bc69c-193">Para **Categoria da Atividade**, selecione **Gerenciamento de Senhas de Autoatendimento**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-193">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="bc69c-194">Atividade dos grupos de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="bc69c-194">Self-service groups activity</span></span>         | <span data-ttu-id="bc69c-195">Para **Categoria da Atividade**, selecione **Gerenciamento de Grupos de Autoatendimento**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-195">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="bc69c-196">Atividade de provisionamento de conta</span><span class="sxs-lookup"><span data-stu-id="bc69c-196">Account provisioning activity</span></span>        | <span data-ttu-id="bc69c-197">Para **Categoria da Atividade**, selecione **Provisionamento do Usuário da Conta**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-197">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="bc69c-198">Status de substituição de senha</span><span class="sxs-lookup"><span data-stu-id="bc69c-198">Password rollover status</span></span>             | <span data-ttu-id="bc69c-199">Para **Categoria da Atividade**, selecione **Substituição Automática de Senha do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-199">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="bc69c-200">Erros de provisionamento de conta</span><span class="sxs-lookup"><span data-stu-id="bc69c-200">Account provisioning errors</span></span>          | <span data-ttu-id="bc69c-201">Para **Categoria da Atividade**, selecione **Provisionamento do Usuário da Conta**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-201">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="bc69c-202">Alterações de nome do grupo do Office365</span><span class="sxs-lookup"><span data-stu-id="bc69c-202">Office365 Group Name Changes</span></span>         | <span data-ttu-id="bc69c-203">Para **Categoria da Atividade**, selecione **Gerenciamento de Senhas de Autoatendimento**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-203">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="bc69c-204">Para **Tipo de Recurso de Atividade**, selecione **Grupo**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-204">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="bc69c-205">Para **Origem da Atividade**, selecione **Grupos do O365**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-205">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="bc69c-206">Olá tooview **uso do aplicativo** relatório, no hello **Active Directory do Azure** folha, em **gerenciar**, selecione **aplicativos empresariais**e, em seguida, selecione **entradas**.</span><span class="sxs-lookup"><span data-stu-id="bc69c-206">tooview hello **Application Usage** report, on hello **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="bc69c-207">![Relatório de Entradas de aplicativos empresariais](./media/active-directory-reporting-migration/199.png "Relatório de Entradas de aplicativos empresariais")</span><span class="sxs-lookup"><span data-stu-id="bc69c-207">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc69c-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bc69c-208">Next steps</span></span>

<span data-ttu-id="bc69c-209">Para obter uma visão geral de emissão de relatórios, consulte Olá [reporting do Active Directory do Azure](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bc69c-209">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
