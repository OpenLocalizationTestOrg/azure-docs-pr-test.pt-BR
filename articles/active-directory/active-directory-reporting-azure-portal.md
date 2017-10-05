---
title: "Relatórios do Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: 738c8f4a56586b87f03973ec258b0a3023affa60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="884d5-103">Relatórios do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="884d5-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="884d5-104">Com os relatórios do Azure Active Directory, você pode ter uma ideia de como o seu ambiente está funcionando.</span><span class="sxs-lookup"><span data-stu-id="884d5-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="884d5-105">Os dados fornecidos permitem a você:</span><span class="sxs-lookup"><span data-stu-id="884d5-105">The provided data enables you to:</span></span>

- <span data-ttu-id="884d5-106">Determinar como os aplicativos e serviços estão sendo utilizados pelos usuários</span><span class="sxs-lookup"><span data-stu-id="884d5-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="884d5-107">Detectar possíveis riscos que afetem a integridade do seu ambiente</span><span class="sxs-lookup"><span data-stu-id="884d5-107">Detect potential risks affecting the health of your environment</span></span>
- <span data-ttu-id="884d5-108">Solucionar problemas que impedem a conclusão dos trabalhos pelos usuários</span><span class="sxs-lookup"><span data-stu-id="884d5-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="884d5-109">A arquitetura de relatório se baseia em dois pilares principais:</span><span class="sxs-lookup"><span data-stu-id="884d5-109">The reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="884d5-110">Relatórios de segurança</span><span class="sxs-lookup"><span data-stu-id="884d5-110">Security reports</span></span>
- <span data-ttu-id="884d5-111">Relatórios de atividades</span><span class="sxs-lookup"><span data-stu-id="884d5-111">Activity reports</span></span>

![Relatórios](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="884d5-113">Relatórios de segurança</span><span class="sxs-lookup"><span data-stu-id="884d5-113">Security reports</span></span>

<span data-ttu-id="884d5-114">Os relatórios de segurança no Azure Active Directory o ajudam a proteger as identidades da organização.</span><span class="sxs-lookup"><span data-stu-id="884d5-114">The security reports in Azure Active Directory help you to protect your organization's identities.</span></span>  
<span data-ttu-id="884d5-115">Há dois tipos de relatórios de segurança no Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="884d5-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="884d5-116">**Usuários sinalizados como risco**: no [relatório de usuários sinalizados como risco de segurança](active-directory-reporting-security-user-at-risk.md), obtenha uma visão geral das contas de usuário que podem ter sido comprometidas.</span><span class="sxs-lookup"><span data-stu-id="884d5-116">**Users flagged for risk** - From the [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="884d5-117">**Entradas de risco**: com o [relatório de entradas de risco](active-directory-reporting-security-risky-sign-ins.md), você tem um indicador de tentativas de logon que pode ter sido realizadas por alguém que não é o proprietário legítimo de uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="884d5-117">**Risky sign-ins** - With the [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 

<span data-ttu-id="884d5-118">**Qual licença do Azure AD você precisa para acessar a atividade de entrada?**</span><span class="sxs-lookup"><span data-stu-id="884d5-118">**What Azure AD license do you need to access a security report?**</span></span>  
<span data-ttu-id="884d5-119">Todas as edições do Azure Active Directory fornecem relatórios de usuários sinalizados como risco e de entradas de risco.</span><span class="sxs-lookup"><span data-stu-id="884d5-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="884d5-120">No entanto, o nível de granularidade do relatório varia entre as edições:</span><span class="sxs-lookup"><span data-stu-id="884d5-120">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="884d5-121">Nas **edições do Azure Active Directory Gratuita e Basic**, você obtém uma lista de usuários sinalizados como risco e de entradas de risco.</span><span class="sxs-lookup"><span data-stu-id="884d5-121">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="884d5-122">A edição do **Azure Active Directory Premium 1** estende esse modelo, também permitindo que você examine alguns dos eventos de risco subjacentes que foram detectados para cada relatório.</span><span class="sxs-lookup"><span data-stu-id="884d5-122">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="884d5-123">A edição do **Azure Active Directory Premium 2** fornece as informações mais detalhadas sobre os eventos de risco subjacentes e também permite configurar políticas de segurança que atendem automaticamente a níveis de risco configurados.</span><span class="sxs-lookup"><span data-stu-id="884d5-123">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about the underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="884d5-124">Relatórios de atividades</span><span class="sxs-lookup"><span data-stu-id="884d5-124">Activity reports</span></span>

<span data-ttu-id="884d5-125">Há dois tipos de relatórios de atividade no Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="884d5-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="884d5-126">**Trilhas de auditoria**: o [relatório de atividade das trilhas de auditoria](active-directory-reporting-activity-audit-logs.md) fornece acesso ao histórico de todas as tarefas executadas em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="884d5-126">**Audit logs** - The [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access to the history of every task performed in your tenant.</span></span>

- <span data-ttu-id="884d5-127">**Entradas**: com o [relatório de atividades de entradas](active-directory-reporting-activity-sign-ins.md), você pode determinar quem realizou as tarefas indicadas pelo relatório das trilhas de auditoria.</span><span class="sxs-lookup"><span data-stu-id="884d5-127">**Sign-ins** -  With the [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed the tasks reported by the audit logs report.</span></span>



<span data-ttu-id="884d5-128">O **relatório das trilhas de auditoria** fornece registros de atividades de sistema para fins de conformidade.</span><span class="sxs-lookup"><span data-stu-id="884d5-128">The **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="884d5-129">Entre outros, os dados fornecidos permitem tratar cenários comuns, como:</span><span class="sxs-lookup"><span data-stu-id="884d5-129">Amongst others, the provided data enables you to address common scenarios such as:</span></span>

- <span data-ttu-id="884d5-130">Alguém em meu locatário tem acesso a um grupo de administração.</span><span class="sxs-lookup"><span data-stu-id="884d5-130">Someone in my tenant got access to an admin group.</span></span> <span data-ttu-id="884d5-131">Quem deu o acesso?</span><span class="sxs-lookup"><span data-stu-id="884d5-131">Who gave them access?</span></span> 

- <span data-ttu-id="884d5-132">Quero saber a lista de usuários que estão entrando em um aplicativo específico, já que integrei o aplicativo recentemente e desejo saber se ele está tendo boa recepção</span><span class="sxs-lookup"><span data-stu-id="884d5-132">I want to know the list of users signing into a specific app since I recently onboarded the app and want to know if it’s doing well</span></span>

- <span data-ttu-id="884d5-133">Quero saber quantas redefinições de senha estão ocorrendo em meu locatário</span><span class="sxs-lookup"><span data-stu-id="884d5-133">I want to know how many password resets are happening in my tenant</span></span>


<span data-ttu-id="884d5-134">**Qual é a licença do Azure AD necessária para acessar o relatório das trilhas de auditoria?**</span><span class="sxs-lookup"><span data-stu-id="884d5-134">**What Azure AD license do you need to access the audit logs report?**</span></span>  
<span data-ttu-id="884d5-135">O relatório das trilhas de auditoria está disponível para os recursos para os quais você possui licenças.</span><span class="sxs-lookup"><span data-stu-id="884d5-135">The audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="884d5-136">Se você tem uma licença para um recurso específico, também tem acesso às informações da trilha de auditoria dele.</span><span class="sxs-lookup"><span data-stu-id="884d5-136">If you have a license for a specific feature, you also have access to the audit log information for it.</span></span>

<span data-ttu-id="884d5-137">Para obter mais detalhes, confira **Comparando recursos geralmente disponíveis das edições Gratuita, Basic e Premium** em [Recursos do Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="884d5-137">For more details, see **Comparing generally available features of the Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="884d5-138">O **relatório de atividades de entrada** permite encontrar respostas a perguntas como:</span><span class="sxs-lookup"><span data-stu-id="884d5-138">The **sign-ins activity report** enables to to find answers to questions such as:</span></span>

- <span data-ttu-id="884d5-139">O que é o padrão de entrada de um usuário?</span><span class="sxs-lookup"><span data-stu-id="884d5-139">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="884d5-140">Quantos usuários entraram em uma semana?</span><span class="sxs-lookup"><span data-stu-id="884d5-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="884d5-141">Qual é o status dessas entradas?</span><span class="sxs-lookup"><span data-stu-id="884d5-141">What’s the status of these sign-ins?</span></span>


<span data-ttu-id="884d5-142">**Qual licença do Azure AD você precisa para acessar o relatório de atividades de entrada?**</span><span class="sxs-lookup"><span data-stu-id="884d5-142">**What Azure AD license do you need to access the sign-ins activity report?**</span></span>  
<span data-ttu-id="884d5-143">Para acessar o relatório de atividades de entrada, seu locatário deve ter uma licença do Azure AD Premium associada a ele.</span><span class="sxs-lookup"><span data-stu-id="884d5-143">To access the sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="884d5-144">Acesso Programático</span><span class="sxs-lookup"><span data-stu-id="884d5-144">Programmatic access</span></span>

<span data-ttu-id="884d5-145">Além da interface do usuário, os relatórios do Azure Active Directory também fornecem a você [acesso programático](active-directory-reporting-api-getting-started-azure-portal.md) aos dados de relatórios.</span><span class="sxs-lookup"><span data-stu-id="884d5-145">In addition to the user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) to the reporting data.</span></span> <span data-ttu-id="884d5-146">Os dados desses relatórios podem ser muito úteis para seus aplicativos, como sistemas SIEM, auditoria e ferramentas de business intelligence.</span><span class="sxs-lookup"><span data-stu-id="884d5-146">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="884d5-147">As APIs de relatório do Azure AD fornecem acesso programático aos dados através de um conjunto de APIs baseadas em REST.</span><span class="sxs-lookup"><span data-stu-id="884d5-147">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="884d5-148">Você pode chamar essas APIs de várias ferramentas e linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="884d5-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="884d5-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="884d5-149">Next steps</span></span>

<span data-ttu-id="884d5-150">Se você quiser saber mais sobre os vários tipos de relatório no Azure Active Directory, confira:</span><span class="sxs-lookup"><span data-stu-id="884d5-150">If you want to know more about the various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="884d5-151">Usuários sinalizados como risco</span><span class="sxs-lookup"><span data-stu-id="884d5-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="884d5-152">Relatório de entradas de risco</span><span class="sxs-lookup"><span data-stu-id="884d5-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="884d5-153">Relatório de trilhas de auditoria</span><span class="sxs-lookup"><span data-stu-id="884d5-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="884d5-154">Relatório de logs de entrada</span><span class="sxs-lookup"><span data-stu-id="884d5-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="884d5-155">Se você quiser saber mais sobre como acessar os dados de relatório usando a API de relatório, confira:</span><span class="sxs-lookup"><span data-stu-id="884d5-155">If you want to know more about accessing the the reporting data using the reporting API, see:</span></span> 

- [<span data-ttu-id="884d5-156">Introdução à API de relatório do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="884d5-156">Getting started with the Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png