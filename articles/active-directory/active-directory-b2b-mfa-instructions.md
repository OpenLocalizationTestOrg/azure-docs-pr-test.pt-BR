---
title: "Acesso condicional para usuários de colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "A colaboração B2B do Azure Active Directory dá suporte à autenticação multifator (MF) para acesso seletivo aos seus aplicativos corporativos"
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
ms.openlocfilehash: d85f711d6551a68d1248ae8ec61e2ecc1ddc8ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="7eda9-103">Acesso condicional para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="7eda9-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="7eda9-104">Autenticação multifator para usuários B2B</span><span class="sxs-lookup"><span data-stu-id="7eda9-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="7eda9-105">Com a colaboração B2B do Azure AD, as organizações podem aplicar políticas de MFA (autenticação multifator) para usuários B2B.</span><span class="sxs-lookup"><span data-stu-id="7eda9-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="7eda9-106">Essas políticas podem ser impostas no nível do locatário, aplicativo ou usuário individual, da mesma maneira que podem ser habilitadas para membros e funcionários em tempo integral da organização.</span><span class="sxs-lookup"><span data-stu-id="7eda9-106">These policies can be enforced at the tenant, app, or individual user level, the same way that they are enabled for full-time employees and members of the organization.</span></span> <span data-ttu-id="7eda9-107">Politicas de MFA são impostas na organização do recurso.</span><span class="sxs-lookup"><span data-stu-id="7eda9-107">MFA policies are enforced at the resource organization.</span></span>

<span data-ttu-id="7eda9-108">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="7eda9-108">Example:</span></span>
1. <span data-ttu-id="7eda9-109">O Administrador ou operador de informações na Empresa A convida o usuário da Empresa B para um aplicativo *Foo* na empresa A.</span><span class="sxs-lookup"><span data-stu-id="7eda9-109">Admin or information worker in Company A invites user from company B to an application *Foo* in company A.</span></span>
2. <span data-ttu-id="7eda9-110">O aplicativo *Foo* na empresa A está configurado para exigir MFA no acesso.</span><span class="sxs-lookup"><span data-stu-id="7eda9-110">Application *Foo* in company A is configured to require MFA on access.</span></span>
3. <span data-ttu-id="7eda9-111">Quando o usuário da empresa B tenta acessar o aplicativo *Foo* no locatário da empresa A, recebe uma solicitação para concluir um desafio de MFA.</span><span class="sxs-lookup"><span data-stu-id="7eda9-111">When the user from company B attempts to access app *Foo* in the company A tenant, they are asked to complete an MFA challenge.</span></span>
4. <span data-ttu-id="7eda9-112">O usuário pode configurar sua MFA com a empresa A, e escolher a opção de MFA.</span><span class="sxs-lookup"><span data-stu-id="7eda9-112">The user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="7eda9-113">Esse cenário funciona para qualquer identidade (Azure AD ou MSA, por exemplo, se os usuários na Empresa B autenticarem usando a ID social)</span><span class="sxs-lookup"><span data-stu-id="7eda9-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="7eda9-114">A empresa A deve ter licenças suficientes do Azure AD Premium que oferecem suporte a MFA.</span><span class="sxs-lookup"><span data-stu-id="7eda9-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="7eda9-115">O usuário da empresa B consumirá essa licença da empresa A.</span><span class="sxs-lookup"><span data-stu-id="7eda9-115">The user from company B consumes this license from company A.</span></span>

<span data-ttu-id="7eda9-116">O locatário que convida sempre é responsável pela MFA dos usuários da organização parceira, mesmo se a organização parceira tiver recursos de MFA.</span><span class="sxs-lookup"><span data-stu-id="7eda9-116">The inviting tenancy is always responsible for MFA for users from the partner organization, even if the partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="7eda9-117">Definindo a MFA para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="7eda9-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="7eda9-118">Para descobrir como é fácil configurar a MFA para usuários de colaboração B2B, confira o vídeo a seguir:</span><span class="sxs-lookup"><span data-stu-id="7eda9-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="7eda9-119">Experiência de MFA de usuários B2B para resgate de oferta</span><span class="sxs-lookup"><span data-stu-id="7eda9-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="7eda9-120">Confira a animação abaixo para ver a experiência de resgate:</span><span class="sxs-lookup"><span data-stu-id="7eda9-120">Check out the following animation to see the redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="7eda9-121">Redefinição de MFA para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="7eda9-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="7eda9-122">Atualmente, o administrador pode exigir que os usuários de colaboração B2B façam uma verificação novamente usando somente os seguintes cmdlets do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7eda9-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="7eda9-123">Conecte-se ao AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7eda9-123">Connect to Azure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="7eda9-124">Obter todos os usuários com métodos de verificação</span><span class="sxs-lookup"><span data-stu-id="7eda9-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="7eda9-125">Veja um exemplo:</span><span class="sxs-lookup"><span data-stu-id="7eda9-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="7eda9-126">Redefina o método MFA para um usuário específico a fim de exigir que o usuário de colaboração B2B defina métodos de prova novamente.</span><span class="sxs-lookup"><span data-stu-id="7eda9-126">Reset the MFA method for a specific user to require the B2B collaboration user to set proof-up methods again.</span></span> <span data-ttu-id="7eda9-127">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="7eda9-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-the-resource-tenancy"></a><span data-ttu-id="7eda9-128">Por que realizamos MFA na locação de recursos?</span><span class="sxs-lookup"><span data-stu-id="7eda9-128">Why do we perform MFA at the resource tenancy?</span></span>

<span data-ttu-id="7eda9-129">Na versão atual, a MFA está sempre na locação de recursos, por motivos de previsibilidade.</span><span class="sxs-lookup"><span data-stu-id="7eda9-129">In the current release, MFA is always in the resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="7eda9-130">Por exemplo, digamos que um usuário da Contoso (Sally) é convidado para a Fabrikam e a Fabrikam habilitou MFA para usuários B2B.</span><span class="sxs-lookup"><span data-stu-id="7eda9-130">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="7eda9-131">Se a Contoso tiver a política de MFA habilitada para App1, mas não para App2, se olharmos para a declaração de MFA da Contoso no token, veremos o seguinte problema:</span><span class="sxs-lookup"><span data-stu-id="7eda9-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at the Contoso MFA claim in the token, we might see the following issue:</span></span>

* <span data-ttu-id="7eda9-132">Dia 1: um usuário tem MFA na Contoso e está acessando o App1, então nenhuma solicitação de MFA adicional é mostrada na Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="7eda9-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="7eda9-133">Dia 2: o usuário acessou o App 2 na Contoso, então agora ao acessar a Fabrikam, ele deve se registrar na MFA.</span><span class="sxs-lookup"><span data-stu-id="7eda9-133">Day 2: The user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="7eda9-134">Esse processo pode ser confuso e pode levar a causar preenchimentos incompletos na entrada.</span><span class="sxs-lookup"><span data-stu-id="7eda9-134">This process can be confusing and could lead to drop in sign-in completions.</span></span>

<span data-ttu-id="7eda9-135">Além disso, mesmo se a Contoso tiver o recurso MFA, nem sempre aconteceria da Fabrikam confiar na política do MFA.</span><span class="sxs-lookup"><span data-stu-id="7eda9-135">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span></span>

<span data-ttu-id="7eda9-136">Finalmente, a MFA de locatários de recursos também funciona para IDs sociais e MSAs e para organizações parceiras que não tenham a MFA configurada.</span><span class="sxs-lookup"><span data-stu-id="7eda9-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="7eda9-137">Portanto, a recomendação para MFA para usuários B2B é sempre exigir MFA no locatário que convida.</span><span class="sxs-lookup"><span data-stu-id="7eda9-137">Therefore, the recommendation for MFA for B2B users is to always require MFA in the inviting tenant.</span></span> <span data-ttu-id="7eda9-138">Esse requisito poderia conduzir a uma MFA dupla em alguns casos, mas sempre que acessa o locatário que convida, a experiência dos usuários finais será previsível: Sally deve se registrar na MFA com o locatário que convida.</span><span class="sxs-lookup"><span data-stu-id="7eda9-138">This requirement could lead to double MFA in some cases, but whenever accessing the inviting tenant, the end-users experience is predictable: Sally must register for MFA with the inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="7eda9-139">Acesso condicional com base em risco, no local e no dispositivo para usuários B2B</span><span class="sxs-lookup"><span data-stu-id="7eda9-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="7eda9-140">Quando a Contoso habilita políticas de acesso condicional com base em dispositivo para seus dados corporativos, o acesso é impedido em dispositivos não gerenciados pela Contoso e incompatíveis com as políticas de dispositivo da Contoso.</span><span class="sxs-lookup"><span data-stu-id="7eda9-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with the Contoso device policies.</span></span>

<span data-ttu-id="7eda9-141">Se o dispositivo do usuário B2B não for gerenciado pela Contoso, o acesso de usuários B2B das organizações parceiras será bloqueado em quaisquer contextos em que essas políticas são impostas.</span><span class="sxs-lookup"><span data-stu-id="7eda9-141">If the B2B user’s device isn't managed by Contoso, access of B2B users from the partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="7eda9-142">Entretanto, a Contoso pode criar listas de exclusão contendo usuários parceiros específicos para excluí-los da política de acesso condicional com base em dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7eda9-142">However, Contoso can create exclusion lists containing specific partner users to exclude them from the device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="7eda9-143">Acesso condicional com base em local para B2B</span><span class="sxs-lookup"><span data-stu-id="7eda9-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="7eda9-144">Políticas de acesso condicional com base em local podem ser impostas para usuários B2B se a organização que convida for capaz de criar um intervalo de endereços IP confiável que define suas organizações parceiras.</span><span class="sxs-lookup"><span data-stu-id="7eda9-144">Location-based conditional access policies can be enforced for B2B users if the inviting organization is able to create a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="7eda9-145">Acesso condicional com base em risco para B2B</span><span class="sxs-lookup"><span data-stu-id="7eda9-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="7eda9-146">Atualmente, as políticas de entrada baseadas em risco não podem ser aplicadas a usuários B2B, pois a avaliação de risco é realizada na organização inicial do usuário B2B.</span><span class="sxs-lookup"><span data-stu-id="7eda9-146">Currently, risk-based sign-in policies cannot be applied to B2B users because the risk evaluation is performed at the B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7eda9-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7eda9-147">Next steps</span></span>

<span data-ttu-id="7eda9-148">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="7eda9-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="7eda9-149">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="7eda9-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="7eda9-150">Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="7eda9-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="7eda9-151">Como os operadores de informação adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="7eda9-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* <span data-ttu-id="7eda9-152">[The elements of the B2B collaboration invitation email](active-directory-b2b-invitation-email.md) (Os elementos do email de convite para colaboração B2B)</span><span class="sxs-lookup"><span data-stu-id="7eda9-152">[The elements of the B2B collaboration invitation email](active-directory-b2b-invitation-email.md)</span></span>
* [<span data-ttu-id="7eda9-153">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="7eda9-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="7eda9-154">Licenciamento da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7eda9-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="7eda9-155">Solução de problemas de colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7eda9-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="7eda9-156">Perguntas frequentes sobre a colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7eda9-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="7eda9-157">API e personalização da colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7eda9-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="7eda9-158">Adicionar usuários de colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="7eda9-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="7eda9-159">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7eda9-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
