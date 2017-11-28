---
title: "aaaUsers sinalizados para relatório de risco de segurança no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Saiba mais sobre Olá usuários sinalizados para relatório de risco de segurança no portal do Azure Active Directory Olá"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="8dbdc-103">Usuários sinalizados para relatório de risco de segurança no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="8dbdc-103">Users flagged for risk security report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="8dbdc-104">Relatórios de segurança Olá no hello Azure Active Directory (AD do Azure), você pode obter ideias sobre a probabilidade de saudação de contas de usuário comprometidas em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-104">With hello security reports in hello Azure Active Directory (Azure AD), you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="8dbdc-105">Active Directory do Azure detecta suspeitas ações que são relacionadas tooyour contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-105">Azure Active Directory detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="8dbdc-106">Para cada ação detectada, um registro chamado *evento de risco* é criado.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="8dbdc-107">Para saber mais, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="8dbdc-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="8dbdc-108">Olá detectados eventos de risco são toocalculate usado:</span><span class="sxs-lookup"><span data-stu-id="8dbdc-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="8dbdc-109">**Entradas arriscadas** -uma entrada arriscado é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é proprietário legítimo Olá uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="8dbdc-110">Para obter mais informações, consulte [Entradas de risco](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="8dbdc-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="8dbdc-111">**Usuários sinalizados para riscos** - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="8dbdc-112">Para obter mais informações, consulte [Usuários sinalizados para risco](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="8dbdc-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="8dbdc-113">Olá portal do Azure, você pode encontrar relata segurança Olá Olá **Active Directory do Azure** folha em Olá **segurança** seção.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-113">In hello Azure portal, you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span>  

![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="8dbdc-115">Qual licença do AD do Azure precisa de um relatório de segurança de tooaccess?</span><span class="sxs-lookup"><span data-stu-id="8dbdc-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="8dbdc-116">Todas as edições do Azure Active Directory fornecem relatórios de usuários sinalizados como risco.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="8dbdc-117">No entanto, o nível de saudação de granularidade do relatório varia entre as edições hello:</span><span class="sxs-lookup"><span data-stu-id="8dbdc-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="8dbdc-118">Em Olá **edições do Azure Active Directory gratuito e Basic**, você já obter uma lista de usuários sinalizados riscos.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="8dbdc-119">Olá **do Azure Active Directory Premium 1** edição estende esse modelo, permitindo que você também tooexamine alguns Olá subjacente eventos de risco que foram detectados para cada relatório.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="8dbdc-120">Olá **do Azure Active Directory Premium 2** edition oferece Olá informações mais detalhadas sobre todos os eventos de risco subjacente e permite que as políticas de segurança de tooconfigure respondem automaticamente tooconfigured risco níveis.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="8dbdc-121">Edições gratuita e básica do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8dbdc-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="8dbdc-122">usuários Olá sinalizados para relatório de risco em edições de gratuita e basic do Active Directory do Azure Olá fornece uma lista de contas de usuário que podem ter sido comprometidas.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-122">hello users flagged for risk report in hello Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="8dbdc-124">Seleção de um usuário abre a folha de dados de usuário relacionado hello.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-124">Selecting a user opens hello related user data blade.</span></span>
<span data-ttu-id="8dbdc-125">Para usuários que estão em risco, você pode revisar o histórico de entrada do usuário Olá e Redefinir senha hello, se necessário.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-125">For users that are at risk, you can review hello user’s sign-in history and reset hello password if necessary.</span></span>

![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="8dbdc-127">Essa caixa de diálogo fornece uma opção para:</span><span class="sxs-lookup"><span data-stu-id="8dbdc-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="8dbdc-128">Baixar relatório Olá</span><span class="sxs-lookup"><span data-stu-id="8dbdc-128">Download hello report</span></span>

- <span data-ttu-id="8dbdc-129">Pesquisar usuários</span><span class="sxs-lookup"><span data-stu-id="8dbdc-129">Search users</span></span>

![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="8dbdc-131">Edições premium do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8dbdc-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="8dbdc-132">usuários Olá sinalizados para relatório de risco em edições de premium Olá Active Directory do Azure oferece:</span><span class="sxs-lookup"><span data-stu-id="8dbdc-132">hello users flagged for risk report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="8dbdc-133">Uma [lista de contas de usuário](active-directory-identityprotection.md#users-flagged-for-risk) que podem ter sido comprometidas</span><span class="sxs-lookup"><span data-stu-id="8dbdc-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="8dbdc-134">Informações sobre Olá agregadas [tipos de eventos de risco](active-directory-identity-protection-risk-events.md) que foram detectadas</span><span class="sxs-lookup"><span data-stu-id="8dbdc-134">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="8dbdc-135">Um relatório de saudação toodownload opção</span><span class="sxs-lookup"><span data-stu-id="8dbdc-135">An option toodownload hello report</span></span>

- <span data-ttu-id="8dbdc-136">Uma opção tooconfigure um [política de correção de risco do usuário](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="8dbdc-136">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="8dbdc-138">Ao selecionar um usuário, você obtém uma exibição detalhada do relatório deste usuário, que lhe habilita a:</span><span class="sxs-lookup"><span data-stu-id="8dbdc-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="8dbdc-139">Olá abrir, que exibir todas as entradas</span><span class="sxs-lookup"><span data-stu-id="8dbdc-139">Open hello All sign-ins view</span></span>

- <span data-ttu-id="8dbdc-140">Redefinir senha do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="8dbdc-140">Reset hello user's password</span></span>

- <span data-ttu-id="8dbdc-141">Descartar todos os eventos</span><span class="sxs-lookup"><span data-stu-id="8dbdc-141">Dismiss all events</span></span>

- <span data-ttu-id="8dbdc-142">Investigue eventos de risco relatado para o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-142">Investigate reported risk events for hello user.</span></span> 


![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="8dbdc-144">tooinvestigate um evento de risco, selecione uma opção da saudação do hello lista tooopen **detalhes** folha para esse evento de risco.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-144">tooinvestigate a risk event, select one from hello list tooopen hello **Details** blade for this risk event.</span></span> <span data-ttu-id="8dbdc-145">Em hello **detalhes** folha, você tem Olá opção tooeither [Feche manualmente um evento de risco](active-directory-identityprotection.md#closing-risk-events-manually) ou reativar um evento de risco fechado manualmente.</span><span class="sxs-lookup"><span data-stu-id="8dbdc-145">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="8dbdc-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8dbdc-147">Next steps</span></span>

- <span data-ttu-id="8dbdc-148">Para saber mais sobre o Azure Active Directory Identity Protection, veja [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="8dbdc-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

