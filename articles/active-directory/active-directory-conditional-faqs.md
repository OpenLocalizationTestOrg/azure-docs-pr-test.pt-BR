---
title: Perguntas frequentes sobre o acesso condicional ao Azure Active Directory | Microsoft Docs
description: Obtenha respostas para as perguntas frequentes sobre o acesso condicional no Azure Active Directory.
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
ms.openlocfilehash: e9a5af41b08b593e4d97475f29da4e5fe8df7042
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="73561-103">Perguntas frequentes sobre o acesso condicional ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73561-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="73561-104">Quais aplicativos funcionam com políticas de acesso condicional?</span><span class="sxs-lookup"><span data-stu-id="73561-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="73561-105">Para obter informações sobre aplicativos que funcionam com políticas de acesso condicional, consulte [Aplicativos e navegadores que usam regras de acesso condicional no Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="73561-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="73561-106">As políticas de acesso condicional são impostas para colaboração B2B e usuários convidados?</span><span class="sxs-lookup"><span data-stu-id="73561-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="73561-107">As políticas são impostas para usuários de colaboração B2B (entre empresas).</span><span class="sxs-lookup"><span data-stu-id="73561-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="73561-108">No entanto, em alguns casos, um usuário pode não ser capaz de atender aos requisitos da política.</span><span class="sxs-lookup"><span data-stu-id="73561-108">However, in some cases, a user might not be able to satisfy the policy requirements.</span></span> <span data-ttu-id="73561-109">Por exemplo, a organização de um usuário convidado pode não oferecer suporte à autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="73561-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-to-onedrive-for-business"></a><span data-ttu-id="73561-110">A política do SharePoint Online também se aplica ao OneDrive for Business?</span><span class="sxs-lookup"><span data-stu-id="73561-110">Does a SharePoint Online policy also apply to OneDrive for Business?</span></span>

<span data-ttu-id="73561-111">Sim.</span><span class="sxs-lookup"><span data-stu-id="73561-111">Yes.</span></span> <span data-ttu-id="73561-112">A política do SharePoint Online também se aplica ao OneDrive for Business.</span><span class="sxs-lookup"><span data-stu-id="73561-112">A SharePoint Online policy also applies to OneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="73561-113">Por que não é possível definir uma política em aplicativos cliente, como o Word ou o Outlook?</span><span class="sxs-lookup"><span data-stu-id="73561-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="73561-114">Uma política de acesso condicional define os requisitos para acessar um serviço.</span><span class="sxs-lookup"><span data-stu-id="73561-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="73561-115">É imposta quando ocorre a autenticação para esse serviço.</span><span class="sxs-lookup"><span data-stu-id="73561-115">It's enforced when authentication to that service occurs.</span></span> <span data-ttu-id="73561-116">A política não é definida diretamente em um aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="73561-116">The policy is not set directly on a client application.</span></span> <span data-ttu-id="73561-117">Em vez disso, ela será aplicada quando um cliente chamar um serviço.</span><span class="sxs-lookup"><span data-stu-id="73561-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="73561-118">Por exemplo, um conjunto de políticas no SharePoint se aplica aos clientes que chamam o SharePoint.</span><span class="sxs-lookup"><span data-stu-id="73561-118">For example, a policy set on SharePoint applies to clients calling SharePoint.</span></span> <span data-ttu-id="73561-119">Um conjunto de políticas no Exchange se aplica ao Outlook.</span><span class="sxs-lookup"><span data-stu-id="73561-119">A policy set on Exchange applies to Outlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-to-service-accounts"></a><span data-ttu-id="73561-120">Uma política de acesso condicional se aplica a contas de serviço?</span><span class="sxs-lookup"><span data-stu-id="73561-120">Does a conditional access policy apply to service accounts?</span></span>

<span data-ttu-id="73561-121">As políticas de acesso condicional se aplicam a todas as contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="73561-121">Conditional access policies apply to all user accounts.</span></span> <span data-ttu-id="73561-122">Isso inclui as contas de usuário usadas como contas de serviço.</span><span class="sxs-lookup"><span data-stu-id="73561-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="73561-123">Geralmente, uma conta de serviço executada de forma autônoma não pode satisfazer os requisitos da política de acesso condicional.</span><span class="sxs-lookup"><span data-stu-id="73561-123">Often, a service account that runs unattended can't satisfy the requirements of a conditional access policy.</span></span> <span data-ttu-id="73561-124">Por exemplo, autenticação multifator pode ser necessária.</span><span class="sxs-lookup"><span data-stu-id="73561-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="73561-125">As contas de serviços podem ser excluídas de uma política ao usar configurações de gerenciamento de política de acesso condicional.</span><span class="sxs-lookup"><span data-stu-id="73561-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="73561-126">As APIs do Graph estão disponíveis para configurar as políticas de acesso condicional?</span><span class="sxs-lookup"><span data-stu-id="73561-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="73561-127">No momento, não.</span><span class="sxs-lookup"><span data-stu-id="73561-127">Currently, no.</span></span> 

## <a name="what-is-the-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="73561-128">Qual é a política de exclusão padrão para plataformas de dispositivos sem suporte?</span><span class="sxs-lookup"><span data-stu-id="73561-128">What is the default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="73561-129">No momento, as políticas de acesso condicional são impostas seletivamente aos usuários de dispositivos com Android e iOS.</span><span class="sxs-lookup"><span data-stu-id="73561-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="73561-130">Os aplicativos em outras plataformas de dispositivo não são, por padrão, afetados pela política de acesso condicional para dispositivos iOS e Android.</span><span class="sxs-lookup"><span data-stu-id="73561-130">Applications on other device platforms are, by default, not affected by the conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="73561-131">A administração de locatário poderá substituir a política global para não permitir o acesso a usuários em plataformas sem suporte.</span><span class="sxs-lookup"><span data-stu-id="73561-131">A tenant admin can choose to override the global policy to disallow access to users on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="73561-132">Como as políticas de acesso condicional funcionam para o Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="73561-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="73561-133">O Microsoft Teams depende muito do Exchange Online e do SharePoint Online para cenários de produtividade de núcleo, como reuniões, calendários e compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="73561-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="73561-134">As políticas de acesso condicional definidas para esses aplicativos de nuvem se aplicam ao Microsoft Teams quando um usuário se conecta.</span><span class="sxs-lookup"><span data-stu-id="73561-134">Conditional access policies that are set for these cloud apps apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="73561-135">O Microsoft Teams também tem suporte separadamente como um aplicativo de nuvem em políticas de acesso condicional do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="73561-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="73561-136">As políticas de autoridade de certificado definidas para um aplicativo de nuvem se aplicam ao Microsoft Teams quando um usuário se conecta.</span><span class="sxs-lookup"><span data-stu-id="73561-136">Certificate authority policies that are set for a cloud app apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="73561-137">Os clientes de área de trabalho do Microsoft Teams para Windows e Mac oferecem suporte a autenticação moderna.</span><span class="sxs-lookup"><span data-stu-id="73561-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="73561-138">A autenticação moderna traz a entrada com base no Azure Active Directory Authentication Library (ADAL) para aplicativos cliente do Microsoft Office entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="73561-138">Modern authentication brings sign-in based on the Azure Active Directory Authentication Library (ADAL) to Microsoft Office client applications across platforms.</span></span> 