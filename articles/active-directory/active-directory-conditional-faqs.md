---
title: aaaAzure do Active Directory de perguntas frequentes de acesso condicional | Microsoft Docs
description: Obtenha respostas toofrequently perguntas frequentes sobre o acesso condicional no Active Directory do Azure.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="f7217-103">Perguntas frequentes sobre o acesso condicional ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7217-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="f7217-104">Quais aplicativos funcionam com políticas de acesso condicional?</span><span class="sxs-lookup"><span data-stu-id="f7217-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="f7217-105">Para obter informações sobre aplicativos que funcionam com políticas de acesso condicional, consulte [Aplicativos e navegadores que usam regras de acesso condicional no Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="f7217-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="f7217-106">As políticas de acesso condicional são impostas para colaboração B2B e usuários convidados?</span><span class="sxs-lookup"><span data-stu-id="f7217-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="f7217-107">As políticas são impostas para usuários de colaboração B2B (entre empresas).</span><span class="sxs-lookup"><span data-stu-id="f7217-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="f7217-108">No entanto, em alguns casos, um usuário não pode ser capaz de toosatisfy requisitos da política de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7217-108">However, in some cases, a user might not be able toosatisfy hello policy requirements.</span></span> <span data-ttu-id="f7217-109">Por exemplo, a organização de um usuário convidado pode não oferecer suporte à autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="f7217-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a><span data-ttu-id="f7217-110">Uma política do SharePoint Online também se aplicam tooOneDrive para a empresa?</span><span class="sxs-lookup"><span data-stu-id="f7217-110">Does a SharePoint Online policy also apply tooOneDrive for Business?</span></span>

<span data-ttu-id="f7217-111">Sim.</span><span class="sxs-lookup"><span data-stu-id="f7217-111">Yes.</span></span> <span data-ttu-id="f7217-112">Uma política do SharePoint Online também se aplica a tooOneDrive para empresas.</span><span class="sxs-lookup"><span data-stu-id="f7217-112">A SharePoint Online policy also applies tooOneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="f7217-113">Por que não é possível definir uma política em aplicativos cliente, como o Word ou o Outlook?</span><span class="sxs-lookup"><span data-stu-id="f7217-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="f7217-114">Uma política de acesso condicional define os requisitos para acessar um serviço.</span><span class="sxs-lookup"><span data-stu-id="f7217-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="f7217-115">Ela será aplicada quando o serviço de autenticação da toothat ocorre.</span><span class="sxs-lookup"><span data-stu-id="f7217-115">It's enforced when authentication toothat service occurs.</span></span> <span data-ttu-id="f7217-116">política de saudação não definida diretamente em um aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="f7217-116">hello policy is not set directly on a client application.</span></span> <span data-ttu-id="f7217-117">Em vez disso, ela será aplicada quando um cliente chamar um serviço.</span><span class="sxs-lookup"><span data-stu-id="f7217-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="f7217-118">Por exemplo, uma política definida no SharePoint aplica tooclients chamando do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f7217-118">For example, a policy set on SharePoint applies tooclients calling SharePoint.</span></span> <span data-ttu-id="f7217-119">Uma conjunto de políticas no Exchange se aplica a tooOutlook.</span><span class="sxs-lookup"><span data-stu-id="f7217-119">A policy set on Exchange applies tooOutlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a><span data-ttu-id="f7217-120">Uma política de acesso condicional se aplica a contas tooservice?</span><span class="sxs-lookup"><span data-stu-id="f7217-120">Does a conditional access policy apply tooservice accounts?</span></span>

<span data-ttu-id="f7217-121">Políticas de acesso condicional se aplicam a contas de usuário tooall.</span><span class="sxs-lookup"><span data-stu-id="f7217-121">Conditional access policies apply tooall user accounts.</span></span> <span data-ttu-id="f7217-122">Isso inclui as contas de usuário usadas como contas de serviço.</span><span class="sxs-lookup"><span data-stu-id="f7217-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="f7217-123">Geralmente, uma conta de serviço for executado autônoma não pode atender aos requisitos de saudação de uma política de acesso condicional.</span><span class="sxs-lookup"><span data-stu-id="f7217-123">Often, a service account that runs unattended can't satisfy hello requirements of a conditional access policy.</span></span> <span data-ttu-id="f7217-124">Por exemplo, autenticação multifator pode ser necessária.</span><span class="sxs-lookup"><span data-stu-id="f7217-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="f7217-125">As contas de serviços podem ser excluídas de uma política ao usar configurações de gerenciamento de política de acesso condicional.</span><span class="sxs-lookup"><span data-stu-id="f7217-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="f7217-126">As APIs do Graph estão disponíveis para configurar as políticas de acesso condicional?</span><span class="sxs-lookup"><span data-stu-id="f7217-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="f7217-127">No momento, não.</span><span class="sxs-lookup"><span data-stu-id="f7217-127">Currently, no.</span></span> 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="f7217-128">O que é política de exclusão padrão Olá para plataformas de dispositivos sem suporte?</span><span class="sxs-lookup"><span data-stu-id="f7217-128">What is hello default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="f7217-129">No momento, as políticas de acesso condicional são impostas seletivamente aos usuários de dispositivos com Android e iOS.</span><span class="sxs-lookup"><span data-stu-id="f7217-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="f7217-130">Aplicativos em outras plataformas de dispositivo, por padrão, não são afetados pela política de acesso condicional Olá para dispositivos iOS e Android.</span><span class="sxs-lookup"><span data-stu-id="f7217-130">Applications on other device platforms are, by default, not affected by hello conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="f7217-131">Um administrador de locatário pode escolher toooverride Olá política global toodisallow acesso toousers em plataformas que não são suportadas.</span><span class="sxs-lookup"><span data-stu-id="f7217-131">A tenant admin can choose toooverride hello global policy toodisallow access toousers on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="f7217-132">Como as políticas de acesso condicional funcionam para o Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="f7217-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="f7217-133">O Microsoft Teams depende muito do Exchange Online e do SharePoint Online para cenários de produtividade de núcleo, como reuniões, calendários e compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="f7217-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="f7217-134">Políticas de acesso condicional que são definidas para esses aplicativos de nuvem se aplicam a equipes tooMicrosoft quando um usuário faz logon.</span><span class="sxs-lookup"><span data-stu-id="f7217-134">Conditional access policies that are set for these cloud apps apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="f7217-135">O Microsoft Teams também tem suporte separadamente como um aplicativo de nuvem em políticas de acesso condicional do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f7217-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="f7217-136">Políticas de autoridade de certificado que são definidas para um aplicativo de nuvem se aplicam a equipes tooMicrosoft quando um usuário faz logon.</span><span class="sxs-lookup"><span data-stu-id="f7217-136">Certificate authority policies that are set for a cloud app apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="f7217-137">Os clientes de área de trabalho do Microsoft Teams para Windows e Mac oferecem suporte a autenticação moderna.</span><span class="sxs-lookup"><span data-stu-id="f7217-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="f7217-138">Autenticação moderna traz a entrada com base em aplicativos cliente do hello Azure Active Directory autenticação Library (ADAL) tooMicrosoft Office em plataformas.</span><span class="sxs-lookup"><span data-stu-id="f7217-138">Modern authentication brings sign-in based on hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office client applications across platforms.</span></span> 
