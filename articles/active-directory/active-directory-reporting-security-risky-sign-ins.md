---
title: "relatório de entradas de aaaRisky no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Saiba mais sobre o relatório de entradas arriscados Olá no portal do Azure Active Directory Olá"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="5fe62-103">Relatório de entradas arriscados no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="5fe62-103">Risky sign-ins report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="5fe62-104">Com os relatórios de segurança Olá no Azure Active Directory (AD do Azure), você pode obter ideias sobre a probabilidade de saudação de contas de usuário comprometidas em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="5fe62-104">With hello security reports in Azure Active Directory (Azure AD) you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="5fe62-105">O AD do Azure detecta suspeitas ações que são relacionadas tooyour contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="5fe62-105">Azure AD detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="5fe62-106">Para cada ação detectada, um registro chamado *evento de risco* é criado.</span><span class="sxs-lookup"><span data-stu-id="5fe62-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="5fe62-107">Para obter mais detalhes, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="5fe62-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="5fe62-108">Olá detectados eventos de risco são toocalculate usado:</span><span class="sxs-lookup"><span data-stu-id="5fe62-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="5fe62-109">**Entradas arriscadas** -uma entrada arriscado é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é proprietário legítimo Olá uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="5fe62-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="5fe62-110">Para obter mais detalhes, veja [Entradas arriscadas](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="5fe62-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="5fe62-111">**Usuários sinalizados para riscos** - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="5fe62-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="5fe62-112">Para obter mais detalhes, veja [Usuários sinalizados para riscos](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="5fe62-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="5fe62-113">Em [Olá portal do Azure](https://portal.azure.com), você pode encontrar relata segurança Olá Olá **Active Directory do Azure** folha em Olá **segurança** seção.</span><span class="sxs-lookup"><span data-stu-id="5fe62-113">In [hello Azure portal](https://portal.azure.com), you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span> 

![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="5fe62-115">Qual licença do AD do Azure precisa de um relatório de segurança de tooaccess?</span><span class="sxs-lookup"><span data-stu-id="5fe62-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="5fe62-116">Todas as edições do Azure Active Directory fornecem relatórios de entradas de risco.</span><span class="sxs-lookup"><span data-stu-id="5fe62-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="5fe62-117">No entanto, o nível de saudação de granularidade do relatório varia entre as edições hello:</span><span class="sxs-lookup"><span data-stu-id="5fe62-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="5fe62-118">Em Olá **edições do Azure Active Directory gratuito e Basic**, você já obter uma lista de entradas arriscadas.</span><span class="sxs-lookup"><span data-stu-id="5fe62-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="5fe62-119">Olá **do Azure Active Directory Premium 1** edição estende esse modelo, permitindo que você também tooexamine alguns Olá subjacente eventos de risco que foram detectados para cada relatório.</span><span class="sxs-lookup"><span data-stu-id="5fe62-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="5fe62-120">Olá **do Azure Active Directory Premium 2** edition fornece com hello mais informações detalhadas sobre todos os eventos de risco subjacente e também permite políticas de segurança tooconfigure respondem automaticamente tooconfigured níveis de risco.</span><span class="sxs-lookup"><span data-stu-id="5fe62-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="5fe62-121">Edições gratuita e básica do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fe62-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="5fe62-122">Hello Azure Active Directory gratuito e edições basic fornecem uma lista de entradas arriscadas que foram detectados para os usuários.</span><span class="sxs-lookup"><span data-stu-id="5fe62-122">hello Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="5fe62-123">O relatório lista:</span><span class="sxs-lookup"><span data-stu-id="5fe62-123">This report lists:</span></span>

- <span data-ttu-id="5fe62-124">**Usuário** - Olá nome de usuário de saudação que foi usado durante a operação de entrada hello</span><span class="sxs-lookup"><span data-stu-id="5fe62-124">**User** - hello name of hello user that was used during hello sign-in operation</span></span>
- <span data-ttu-id="5fe62-125">**IP** -Olá o endereço IP do dispositivo de saudação que foi usado tooconnect tooAzure do Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fe62-125">**IP** - hello IP address of hello device that was used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="5fe62-126">**Local** -local Olá usado tooconnect tooAzure do Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fe62-126">**Location** - hello location used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="5fe62-127">**Hora da entrada em** -tempo de saudação quando entrar Olá foi executado</span><span class="sxs-lookup"><span data-stu-id="5fe62-127">**Sign-in time** - hello time when hello sign-in was performed</span></span>
- <span data-ttu-id="5fe62-128">**Status** -Olá status de entrada hello</span><span class="sxs-lookup"><span data-stu-id="5fe62-128">**Status** - hello status of hello sign-in</span></span>


![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="5fe62-130">Com base em sua investigação de entrada arriscados hello, você pode fornecer comentários tooAzure do Active Directory na forma de saudação ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="5fe62-130">Based on your investigation of hello risky sign-in, you can provide feedback tooAzure Active Directory in form of hello following actions:</span></span>

- <span data-ttu-id="5fe62-131">Resolver</span><span class="sxs-lookup"><span data-stu-id="5fe62-131">Resolve</span></span>
- <span data-ttu-id="5fe62-132">Marcar como falso positivo</span><span class="sxs-lookup"><span data-stu-id="5fe62-132">Mark as false positive</span></span>
- <span data-ttu-id="5fe62-133">Ignorar</span><span class="sxs-lookup"><span data-stu-id="5fe62-133">Ignore</span></span>
- <span data-ttu-id="5fe62-134">Reativar</span><span class="sxs-lookup"><span data-stu-id="5fe62-134">Reactivate</span></span>

![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="5fe62-136">Para obter mais detalhes, veja [Fechando eventos de risco manualmente](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="5fe62-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="5fe62-137">Esse relatório fornece uma opção para:</span><span class="sxs-lookup"><span data-stu-id="5fe62-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="5fe62-138">Recursos de pesquisa</span><span class="sxs-lookup"><span data-stu-id="5fe62-138">Searh resources</span></span>
- <span data-ttu-id="5fe62-139">Baixar dados de relatório de saudação</span><span class="sxs-lookup"><span data-stu-id="5fe62-139">Download hello report data</span></span>


![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="5fe62-141">Edições premium do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fe62-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="5fe62-142">relatório de entradas arriscados Olá em edições de premium Olá Active Directory do Azure oferece:</span><span class="sxs-lookup"><span data-stu-id="5fe62-142">hello risky sign-ins report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="5fe62-143">Informações sobre Olá agregadas [tipos de eventos de risco](active-directory-identity-protection-risk-events.md) que foram detectadas</span><span class="sxs-lookup"><span data-stu-id="5fe62-143">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="5fe62-144">Um relatório de saudação toodownload opção</span><span class="sxs-lookup"><span data-stu-id="5fe62-144">An option toodownload hello report</span></span>


![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="5fe62-146">Ao selecionar um evento de risco, você obtém uma exibição detalhada do relatório deste evento de risco que habilita:</span><span class="sxs-lookup"><span data-stu-id="5fe62-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="5fe62-147">Uma opção tooconfigure um [política de correção de risco do usuário](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="5fe62-147">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="5fe62-148">Examine Olá detecção da linha do tempo para eventos de risco Olá</span><span class="sxs-lookup"><span data-stu-id="5fe62-148">Review hello detection timeline for hello risk event</span></span>  

- <span data-ttu-id="5fe62-149">O exame de uma lista de usuários para os quais esse evento de risco foi detectado</span><span class="sxs-lookup"><span data-stu-id="5fe62-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="5fe62-150">Que você [feche manualmente eventos de risco](active-directory-identityprotection.md#closing-risk-events-manually) ou reative um evento de risco fechado manualmente.</span><span class="sxs-lookup"><span data-stu-id="5fe62-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="5fe62-152">Ao selecionar um usuário, você obtém uma exibição detalhada do relatório deste usuário, que lhe habilita a:</span><span class="sxs-lookup"><span data-stu-id="5fe62-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="5fe62-153">Olá abrir, que exibir todas as entradas</span><span class="sxs-lookup"><span data-stu-id="5fe62-153">Open hello All sign-ins view</span></span>

- <span data-ttu-id="5fe62-154">Redefinir senha do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="5fe62-154">Reset hello user's password</span></span>

- <span data-ttu-id="5fe62-155">Descartar todos os eventos</span><span class="sxs-lookup"><span data-stu-id="5fe62-155">Dismiss all events</span></span>

- <span data-ttu-id="5fe62-156">Investigue eventos de risco relatado para o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="5fe62-156">Investigate reported risk events for hello user.</span></span> 


![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="5fe62-158">tooinvestigate um evento de risco, selecione um na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fe62-158">tooinvestigate a risk event, select one from hello list.</span></span>  
<span data-ttu-id="5fe62-159">Isso abre o hello **detalhes** folha para esse evento de risco.</span><span class="sxs-lookup"><span data-stu-id="5fe62-159">This opens hello **Details** blade for this risk event.</span></span> <span data-ttu-id="5fe62-160">Em hello **detalhes** folha, você tem Olá opção tooeither [Feche manualmente um evento de risco](active-directory-identityprotection.md#closing-risk-events-manually) ou reativar um evento de risco fechado manualmente.</span><span class="sxs-lookup"><span data-stu-id="5fe62-160">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="5fe62-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5fe62-162">Next steps</span></span>

- <span data-ttu-id="5fe62-163">Para saber mais sobre o Azure Active Directory Identity Protection, veja [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="5fe62-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

