---
title: "relatório de Active Directory aaaAzure | Microsoft Docs"
description: "Fornece uma visão geral sobre a emissão de relatórios do Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="72653-103">Relatórios do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72653-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="72653-104">Com os relatórios do Azure Active Directory, você pode ter uma ideia de como o seu ambiente está funcionando.</span><span class="sxs-lookup"><span data-stu-id="72653-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="72653-105">dados saudação fornecido permite que você:</span><span class="sxs-lookup"><span data-stu-id="72653-105">hello provided data enables you to:</span></span>

- <span data-ttu-id="72653-106">Determinar como os aplicativos e serviços estão sendo utilizados pelos usuários</span><span class="sxs-lookup"><span data-stu-id="72653-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="72653-107">Detectar possíveis riscos que afetam a integridade de saudação do seu ambiente</span><span class="sxs-lookup"><span data-stu-id="72653-107">Detect potential risks affecting hello health of your environment</span></span>
- <span data-ttu-id="72653-108">Solucionar problemas que impedem a conclusão dos trabalhos pelos usuários</span><span class="sxs-lookup"><span data-stu-id="72653-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="72653-109">arquitetura de relatórios Olá se baseia em dois pilares principais:</span><span class="sxs-lookup"><span data-stu-id="72653-109">hello reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="72653-110">Relatórios de segurança</span><span class="sxs-lookup"><span data-stu-id="72653-110">Security reports</span></span>
- <span data-ttu-id="72653-111">Relatórios de atividades</span><span class="sxs-lookup"><span data-stu-id="72653-111">Activity reports</span></span>

![Relatórios](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="72653-113">Relatórios de segurança</span><span class="sxs-lookup"><span data-stu-id="72653-113">Security reports</span></span>

<span data-ttu-id="72653-114">Olá relatórios de segurança no Active Directory do Azure ajudam você tooprotect identidades da organização.</span><span class="sxs-lookup"><span data-stu-id="72653-114">hello security reports in Azure Active Directory help you tooprotect your organization's identities.</span></span>  
<span data-ttu-id="72653-115">Há dois tipos de relatórios de segurança no Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="72653-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="72653-116">**Usuários sinalizados riscos** - da saudação [usuários sinalizados para relatório de risco de segurança](active-directory-reporting-security-user-at-risk.md), obter uma visão geral das contas de usuário que possa ter sido comprometido.</span><span class="sxs-lookup"><span data-stu-id="72653-116">**Users flagged for risk** - From hello [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="72653-117">**Entradas arriscadas** - com hello [relatório de segurança de entrada arriscados](active-directory-reporting-security-risky-sign-ins.md), obterá um indicador para tentativas de logon que podem ter sido realizadas por alguém que é não Olá legítimo proprietário de uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="72653-117">**Risky sign-ins** - With hello [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 

<span data-ttu-id="72653-118">**Qual licença do AD do Azure precisa de um relatório de segurança de tooaccess?**</span><span class="sxs-lookup"><span data-stu-id="72653-118">**What Azure AD license do you need tooaccess a security report?**</span></span>  
<span data-ttu-id="72653-119">Todas as edições do Azure Active Directory fornecem relatórios de usuários sinalizados como risco e de entradas de risco.</span><span class="sxs-lookup"><span data-stu-id="72653-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="72653-120">No entanto, o nível de saudação de granularidade do relatório varia entre as edições hello:</span><span class="sxs-lookup"><span data-stu-id="72653-120">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="72653-121">Em Olá **edições do Azure Active Directory gratuito e Basic**, você já obter uma lista de usuários sinalizados para riscos e entradas arriscadas.</span><span class="sxs-lookup"><span data-stu-id="72653-121">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="72653-122">Olá **do Azure Active Directory Premium 1** edição estende esse modelo, permitindo que você também tooexamine alguns Olá subjacente eventos de risco que foram detectados para cada relatório.</span><span class="sxs-lookup"><span data-stu-id="72653-122">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="72653-123">Olá **do Azure Active Directory Premium 2** edition fornece com hello mais informações detalhadas sobre Olá subjacente eventos de risco e ele também permite políticas de segurança tooconfigure respondem automaticamente tooconfigured níveis de risco.</span><span class="sxs-lookup"><span data-stu-id="72653-123">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about hello underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="72653-124">Relatórios de atividades</span><span class="sxs-lookup"><span data-stu-id="72653-124">Activity reports</span></span>

<span data-ttu-id="72653-125">Há dois tipos de relatórios de atividade no Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="72653-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="72653-126">**Logs de auditoria** - Olá [relatório de atividade de logs de auditoria](active-directory-reporting-activity-audit-logs.md) fornece toohello acesse o histórico de todas as tarefas executadas em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="72653-126">**Audit logs** - hello [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access toohello history of every task performed in your tenant.</span></span>

- <span data-ttu-id="72653-127">**Entradas** - com hello [relatório de atividade de entradas](active-directory-reporting-activity-sign-ins.md), você pode determinar, quem executou tarefas Olá relatadas pelo relatório de logs de auditoria de saudação.</span><span class="sxs-lookup"><span data-stu-id="72653-127">**Sign-ins** -  With hello [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed hello tasks reported by hello audit logs report.</span></span>



<span data-ttu-id="72653-128">Olá **relatório dos logs de auditoria** fornece registros de atividades de sistema para fins de conformidade.</span><span class="sxs-lookup"><span data-stu-id="72653-128">hello **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="72653-129">Entre outros, Olá fornecidos dados permite que você tooaddress os cenários comuns, como:</span><span class="sxs-lookup"><span data-stu-id="72653-129">Amongst others, hello provided data enables you tooaddress common scenarios such as:</span></span>

- <span data-ttu-id="72653-130">Alguém em meu locatário tem o grupo de administradores de tooan de acesso.</span><span class="sxs-lookup"><span data-stu-id="72653-130">Someone in my tenant got access tooan admin group.</span></span> <span data-ttu-id="72653-131">Quem deu o acesso?</span><span class="sxs-lookup"><span data-stu-id="72653-131">Who gave them access?</span></span> 

- <span data-ttu-id="72653-132">Desejo tooknow lista de saudação de usuários de assinatura em um aplicativo específico desde recentemente incorporada Olá aplicativo e deseja tooknow se ela está bem</span><span class="sxs-lookup"><span data-stu-id="72653-132">I want tooknow hello list of users signing into a specific app since I recently onboarded hello app and want tooknow if it’s doing well</span></span>

- <span data-ttu-id="72653-133">Desejo tooknow senha quantas redefinições estão ocorrendo em meu locatário</span><span class="sxs-lookup"><span data-stu-id="72653-133">I want tooknow how many password resets are happening in my tenant</span></span>


<span data-ttu-id="72653-134">**Qual licença do AD do Azure precisa de relatório de logs de auditoria do tooaccess Olá?**</span><span class="sxs-lookup"><span data-stu-id="72653-134">**What Azure AD license do you need tooaccess hello audit logs report?**</span></span>  
<span data-ttu-id="72653-135">relatório de logs de auditoria de saudação está disponível para os recursos para os quais você possui licenças.</span><span class="sxs-lookup"><span data-stu-id="72653-135">hello audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="72653-136">Se você tiver uma licença para um recurso específico, você também tem acesso toohello informações de log para ele de auditoria.</span><span class="sxs-lookup"><span data-stu-id="72653-136">If you have a license for a specific feature, you also have access toohello audit log information for it.</span></span>

<span data-ttu-id="72653-137">Para obter mais detalhes, consulte **compara recursos disponíveis de edições de gratuito, Basic e Premium Olá** na [recursos do Active Directory do Azure](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="72653-137">For more details, see **Comparing generally available features of hello Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="72653-138">Olá **relatório de atividade de entradas** tootoofind habilita responde tooquestions como:</span><span class="sxs-lookup"><span data-stu-id="72653-138">hello **sign-ins activity report** enables tootoofind answers tooquestions such as:</span></span>

- <span data-ttu-id="72653-139">O que é Olá entrar padrão de um usuário?</span><span class="sxs-lookup"><span data-stu-id="72653-139">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="72653-140">Quantos usuários entraram em uma semana?</span><span class="sxs-lookup"><span data-stu-id="72653-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="72653-141">Qual é o status de saudação destas entradas?</span><span class="sxs-lookup"><span data-stu-id="72653-141">What’s hello status of these sign-ins?</span></span>


<span data-ttu-id="72653-142">**Qual licença do AD do Azure é que você precisa tooaccess Olá relatório de atividade de entradas?**</span><span class="sxs-lookup"><span data-stu-id="72653-142">**What Azure AD license do you need tooaccess hello sign-ins activity report?**</span></span>  
<span data-ttu-id="72653-143">tooaccess Olá relatório de atividade de entradas, seu locatário deve ter uma licença Azure AD Premium associada a ele.</span><span class="sxs-lookup"><span data-stu-id="72653-143">tooaccess hello sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="72653-144">Acesso Programático</span><span class="sxs-lookup"><span data-stu-id="72653-144">Programmatic access</span></span>

<span data-ttu-id="72653-145">Na interface do usuário toohello adição, relatórios do Active Directory do Azure também fornece a você [acesso programático](active-directory-reporting-api-getting-started-azure-portal.md) toohello dados de relatório.</span><span class="sxs-lookup"><span data-stu-id="72653-145">In addition toohello user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) toohello reporting data.</span></span> <span data-ttu-id="72653-146">dados Olá desses relatórios podem ser muito útil tooyour aplicativos, como sistemas SIEM, auditoria e ferramentas de business intelligence.</span><span class="sxs-lookup"><span data-stu-id="72653-146">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="72653-147">Olá AD do Azure reporting que APIs fornecem dados de toohello acesso programático por meio de um conjunto de APIs com base em REST.</span><span class="sxs-lookup"><span data-stu-id="72653-147">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="72653-148">Você pode chamar essas APIs de várias ferramentas e linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="72653-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="72653-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72653-149">Next steps</span></span>

<span data-ttu-id="72653-150">Se você quiser tooknow mais sobre Olá vários tipos de relatório no Azure Active Directory, consulte:</span><span class="sxs-lookup"><span data-stu-id="72653-150">If you want tooknow more about hello various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="72653-151">Usuários sinalizados como risco</span><span class="sxs-lookup"><span data-stu-id="72653-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="72653-152">Relatório de entradas de risco</span><span class="sxs-lookup"><span data-stu-id="72653-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="72653-153">Relatório de trilhas de auditoria</span><span class="sxs-lookup"><span data-stu-id="72653-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="72653-154">Relatório de logs de entrada</span><span class="sxs-lookup"><span data-stu-id="72653-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="72653-155">Se você quiser tooknow mais sobre como acessar Olá Olá usando Olá API de relatórios de dados de relatórios, consulte:</span><span class="sxs-lookup"><span data-stu-id="72653-155">If you want tooknow more about accessing hello hello reporting data using hello reporting API, see:</span></span> 

- [<span data-ttu-id="72653-156">Guia de Introdução ao Olá do Active Directory do Azure API de relatório</span><span class="sxs-lookup"><span data-stu-id="72653-156">Getting started with hello Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png