---
title: "aaaConditional acesso para usuários de colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "Colaboração B2B do Active Directory do Azure oferece suporte a autenticação multifator (MFA) para aplicativos corporativos do acesso seletivo tooyour"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="80d9e-103">Acesso condicional para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="80d9e-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="80d9e-104">Autenticação multifator para usuários B2B</span><span class="sxs-lookup"><span data-stu-id="80d9e-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="80d9e-105">Com a colaboração B2B do Azure AD, as organizações podem aplicar políticas de MFA (autenticação multifator) para usuários B2B.</span><span class="sxs-lookup"><span data-stu-id="80d9e-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="80d9e-106">Essas políticas podem ser aplicadas no locatário hello, aplicativo ou nível de usuário individual, hello mesma forma que são habilitadas para funcionários em tempo integral e os membros da organização hello.</span><span class="sxs-lookup"><span data-stu-id="80d9e-106">These policies can be enforced at hello tenant, app, or individual user level, hello same way that they are enabled for full-time employees and members of hello organization.</span></span> <span data-ttu-id="80d9e-107">MFA políticas são aplicadas na organização do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="80d9e-107">MFA policies are enforced at hello resource organization.</span></span>

<span data-ttu-id="80d9e-108">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="80d9e-108">Example:</span></span>
1. <span data-ttu-id="80d9e-109">Trabalho de administração ou informações na empresa A convida usuário do aplicativo de tooan empresa B *Foo* na empresa A.</span><span class="sxs-lookup"><span data-stu-id="80d9e-109">Admin or information worker in Company A invites user from company B tooan application *Foo* in company A.</span></span>
2. <span data-ttu-id="80d9e-110">Aplicativo *Foo* na empresa A é configurado toorequire MFA acesso.</span><span class="sxs-lookup"><span data-stu-id="80d9e-110">Application *Foo* in company A is configured toorequire MFA on access.</span></span>
3. <span data-ttu-id="80d9e-111">Quando o usuário de saudação da empresa B tenta aplicativo tooaccess *Foo* na empresa Olá um locatário, eles são frequentes toocomplete um desafio MFA.</span><span class="sxs-lookup"><span data-stu-id="80d9e-111">When hello user from company B attempts tooaccess app *Foo* in hello company A tenant, they are asked toocomplete an MFA challenge.</span></span>
4. <span data-ttu-id="80d9e-112">Olá usuário pode configurar o MFA com a empresa e escolhe a opção de MFA.</span><span class="sxs-lookup"><span data-stu-id="80d9e-112">hello user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="80d9e-113">Esse cenário funciona para qualquer identidade (Azure AD ou MSA, por exemplo, se os usuários na Empresa B autenticarem usando a ID social)</span><span class="sxs-lookup"><span data-stu-id="80d9e-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="80d9e-114">A empresa A deve ter licenças suficientes do Azure AD Premium que oferecem suporte a MFA.</span><span class="sxs-lookup"><span data-stu-id="80d9e-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="80d9e-115">usuário de saudação da empresa B consome esta licença da empresa A.</span><span class="sxs-lookup"><span data-stu-id="80d9e-115">hello user from company B consumes this license from company A.</span></span>

<span data-ttu-id="80d9e-116">Aluguel convidar Olá sempre é responsável por MFA para usuários da organização do parceiro hello, mesmo se a organização do parceiro de saudação tem recursos MFA.</span><span class="sxs-lookup"><span data-stu-id="80d9e-116">hello inviting tenancy is always responsible for MFA for users from hello partner organization, even if hello partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="80d9e-117">Definindo a MFA para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="80d9e-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="80d9e-118">toodiscover como tooset a MFA para usuários de colaboração B2B, é fácil ver como em Olá vídeo a seguir:</span><span class="sxs-lookup"><span data-stu-id="80d9e-118">toodiscover how easy it is tooset up MFA for B2B collaboration users, see how in hello following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="80d9e-119">Experiência de MFA de usuários B2B para resgate de oferta</span><span class="sxs-lookup"><span data-stu-id="80d9e-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="80d9e-120">Check-out Olá experiência de resgate animação toosee Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="80d9e-120">Check out hello following animation toosee hello redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="80d9e-121">Redefinição de MFA para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="80d9e-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="80d9e-122">Atualmente, Olá administrador pode exigir tooproof de usuários de colaboração B2B backup novamente usando Olá cmdlets do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="80d9e-122">Currently, hello admin can require B2B collaboration users tooproof up again only by using hello following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="80d9e-123">Conecte-se tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="80d9e-123">Connect tooAzure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="80d9e-124">Obter todos os usuários com métodos de verificação</span><span class="sxs-lookup"><span data-stu-id="80d9e-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="80d9e-125">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="80d9e-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="80d9e-126">Redefina o método MFA hello para métodos um usuário específico toorequire Olá B2B colaboração usuário tooset prova-up novamente.</span><span class="sxs-lookup"><span data-stu-id="80d9e-126">Reset hello MFA method for a specific user toorequire hello B2B collaboration user tooset proof-up methods again.</span></span> <span data-ttu-id="80d9e-127">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="80d9e-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a><span data-ttu-id="80d9e-128">Por que realizamos MFA no aluguel de recurso Olá?</span><span class="sxs-lookup"><span data-stu-id="80d9e-128">Why do we perform MFA at hello resource tenancy?</span></span>

<span data-ttu-id="80d9e-129">Na versão atual do hello, MFA é sempre de aluguel de recurso hello, por motivos de previsibilidade.</span><span class="sxs-lookup"><span data-stu-id="80d9e-129">In hello current release, MFA is always in hello resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="80d9e-130">Por exemplo, digamos que um usuário Contoso (Sally) é tooFabrikam convidado e Fabrikam habilitou MFA para usuários de B2B.</span><span class="sxs-lookup"><span data-stu-id="80d9e-130">For example, let’s say a Contoso user (Sally) is invited tooFabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="80d9e-131">Se Contoso política da MFA habilitada para o App1, mas não App2, em seguida, se observarmos Olá declaração Contoso MFA no token de saudação pode vemos Olá problema a seguir:</span><span class="sxs-lookup"><span data-stu-id="80d9e-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at hello Contoso MFA claim in hello token, we might see hello following issue:</span></span>

* <span data-ttu-id="80d9e-132">Dia 1: um usuário tem MFA na Contoso e está acessando o App1, então nenhuma solicitação de MFA adicional é mostrada na Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="80d9e-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="80d9e-133">Dia 2: Olá usuário acessou 2 de aplicativo na Contoso, agora ao acessar a Fabrikam, eles devem se registrar para MFA existe.</span><span class="sxs-lookup"><span data-stu-id="80d9e-133">Day 2: hello user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="80d9e-134">Esse processo pode ser confuso e causar toodrop na entrada conclusões.</span><span class="sxs-lookup"><span data-stu-id="80d9e-134">This process can be confusing and could lead toodrop in sign-in completions.</span></span>

<span data-ttu-id="80d9e-135">Além disso, mesmo que a Contoso tem a capacidade MFA, nem sempre é Olá Olá caso Fabrikam deve confiar Olá política da MFA da Contoso.</span><span class="sxs-lookup"><span data-stu-id="80d9e-135">Moreover, even if Contoso has MFA capability, it is not always hello case hello Fabrikam would trust hello Contoso MFA policy.</span></span>

<span data-ttu-id="80d9e-136">Finalmente, a MFA de locatários de recursos também funciona para IDs sociais e MSAs e para organizações parceiras que não tenham a MFA configurada.</span><span class="sxs-lookup"><span data-stu-id="80d9e-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="80d9e-137">Portanto, a recomendação Olá para MFA para usuários de B2B é tooalways exigir a MFA no hello convidar locatário.</span><span class="sxs-lookup"><span data-stu-id="80d9e-137">Therefore, hello recommendation for MFA for B2B users is tooalways require MFA in hello inviting tenant.</span></span> <span data-ttu-id="80d9e-138">Esse requisito pode causar toodouble MFA em alguns casos, mas sempre que acessar o locatário convidar Olá, experiência de usuários finais Olá é previsível: Sally deve registrar para MFA com locatário convidar hello.</span><span class="sxs-lookup"><span data-stu-id="80d9e-138">This requirement could lead toodouble MFA in some cases, but whenever accessing hello inviting tenant, hello end-users experience is predictable: Sally must register for MFA with hello inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="80d9e-139">Acesso condicional com base em risco, no local e no dispositivo para usuários B2B</span><span class="sxs-lookup"><span data-stu-id="80d9e-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="80d9e-140">Quando Contoso permite que as políticas de acesso condicional com base no dispositivo para seus dados corporativos, acesso será impedido de dispositivos que não são gerenciados pela Contoso e não compatíveis com políticas de dispositivo Olá Contoso.</span><span class="sxs-lookup"><span data-stu-id="80d9e-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with hello Contoso device policies.</span></span>

<span data-ttu-id="80d9e-141">Se o dispositivo do usuário Olá B2B não é gerenciado pela Contoso, acesso de usuários de B2B de organizações de parceiros de saudação é bloqueado em qualquer contexto essas políticas são aplicadas.</span><span class="sxs-lookup"><span data-stu-id="80d9e-141">If hello B2B user’s device isn't managed by Contoso, access of B2B users from hello partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="80d9e-142">No entanto, a Contoso pode criar exclusão listas contendo tooexclude de usuários do parceiro específico de Olá política de acesso condicional com base no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="80d9e-142">However, Contoso can create exclusion lists containing specific partner users tooexclude them from hello device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="80d9e-143">Acesso condicional com base em local para B2B</span><span class="sxs-lookup"><span data-stu-id="80d9e-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="80d9e-144">Políticas de acesso condicional com base no local podem ser impostas para usuários de B2B se a organização convidar Olá é capaz de toocreate um intervalo de endereços IP confiável que define suas organizações de parceiro.</span><span class="sxs-lookup"><span data-stu-id="80d9e-144">Location-based conditional access policies can be enforced for B2B users if hello inviting organization is able toocreate a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="80d9e-145">Acesso condicional com base em risco para B2B</span><span class="sxs-lookup"><span data-stu-id="80d9e-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="80d9e-146">No momento, políticas com base em risco de entrada não podem ser aplicado tooB2B usuários porque avaliação de risco hello está sendo executada na organização inicial do usuário Olá B2B.</span><span class="sxs-lookup"><span data-stu-id="80d9e-146">Currently, risk-based sign-in policies cannot be applied tooB2B users because hello risk evaluation is performed at hello B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80d9e-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="80d9e-147">Next steps</span></span>

<span data-ttu-id="80d9e-148">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="80d9e-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="80d9e-149">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="80d9e-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="80d9e-150">Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="80d9e-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="80d9e-151">Como os operadores de informação adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="80d9e-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="80d9e-152">elementos de saudação do hello email de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="80d9e-152">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="80d9e-153">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="80d9e-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="80d9e-154">Licenciamento da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="80d9e-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="80d9e-155">Solução de problemas de colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80d9e-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="80d9e-156">Perguntas frequentes sobre a colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80d9e-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="80d9e-157">API e personalização da colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80d9e-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="80d9e-158">Adicionar usuários de colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="80d9e-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="80d9e-159">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="80d9e-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
