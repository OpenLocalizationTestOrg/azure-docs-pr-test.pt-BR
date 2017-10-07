---
title: 'Licenciamento: SSPR do Azure AD | Microsoft Docs'
description: "Requisitos de licenciamento para redefinição da senha de autoatendimento do Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="e5df6-103">Requisitos de licenciamento para redefinição da senha de autoatendimento do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5df6-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="e5df6-104">Para que toofunction de redefinição de senha do AD do Azure, você **deve ter pelo menos uma licença atribuída na sua organização**.</span><span class="sxs-lookup"><span data-stu-id="e5df6-104">In order for Azure AD Password Reset toofunction, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="e5df6-105">Não podemos impor Olá experiência de redefinição de senha de licenciamento por usuário.</span><span class="sxs-lookup"><span data-stu-id="e5df6-105">We do not enforce per-user licensing on hello password reset experience.</span></span> <span data-ttu-id="e5df6-106">toomaintain conformidade com seu contrato de licença da Microsoft, você precisa de usuários tooassign de tooany de licenças que usam recursos premium.</span><span class="sxs-lookup"><span data-stu-id="e5df6-106">toomaintain compliance with your Microsoft licensing agreement, you need tooassign licenses tooany users that use premium features.</span></span>

* <span data-ttu-id="e5df6-107">**Somente usuários de nuvem** – Qualquer SKU pago do Office 365 (O365) ou Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="e5df6-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="e5df6-108">Usuários na **nuvem** e/ou **locais** – Azure AD Premium P1 ou P2, Enterprise Mobility + Security (EMS) ou Secure Productive Enterprise (SPE)</span><span class="sxs-lookup"><span data-stu-id="e5df6-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="e5df6-109">Licenças necessárias para write-back de senha</span><span class="sxs-lookup"><span data-stu-id="e5df6-109">Licenses required for password writeback</span></span>

<span data-ttu-id="e5df6-110">Write-back de senha toouse, você deve ter uma saudação após a licenças atribuídas no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="e5df6-110">toouse password writeback, you must have one of hello following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="e5df6-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="e5df6-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="e5df6-112">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="e5df6-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="e5df6-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="e5df6-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="e5df6-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="e5df6-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="e5df6-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="e5df6-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="e5df6-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="e5df6-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="e5df6-117">Autônomo Office 365 planos de licenciamento por **não oferecem suporte a write-back de senha** e exigir uma saudação anterior planos para toowork essa funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="e5df6-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of hello preceding plans for this functionality toowork.</span></span>

<span data-ttu-id="e5df6-118">Informações de licenciamento adicionais, incluindo os custos podem ser encontradas no hello páginas a seguir</span><span class="sxs-lookup"><span data-stu-id="e5df6-118">Additional licensing info including costs can be found on hello following pages</span></span>

* [<span data-ttu-id="e5df6-119">Site de Preços do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e5df6-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="e5df6-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="e5df6-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="e5df6-121">Secure Productive Enterprise</span><span class="sxs-lookup"><span data-stu-id="e5df6-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="e5df6-122">Habilitar licenciamento com base em grupo ou usuário</span><span class="sxs-lookup"><span data-stu-id="e5df6-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="e5df6-123">AD do Azure agora oferece suporte baseado em grupo licenciamento permitindo licenças tooassign de administradores no grupo de tooa em massa de usuários, em vez de atribuir um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="e5df6-123">Azure AD now supports group-based licensing allowing administrators tooassign licenses in bulk tooa group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="e5df6-124">Atribuir, verificar e resolver problemas com licenças</span><span class="sxs-lookup"><span data-stu-id="e5df6-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="e5df6-125">Alguns serviços da Microsoft não estão disponíveis em todos os locais.</span><span class="sxs-lookup"><span data-stu-id="e5df6-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="e5df6-126">Usuário tooa possa ser atribuídos uma licença, administrador Olá deve especificar a propriedade de "Local de uso" de saudação em usuário hello.</span><span class="sxs-lookup"><span data-stu-id="e5df6-126">Before a license can be assigned tooa user, hello administrator must specify hello “Usage location” property on hello user.</span></span> <span data-ttu-id="e5df6-127">Atribuição de licenças pode ser feita em User > perfil > seção configurações Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5df6-127">Assignment of licenses can be done under User > Profile > Settings section in hello Azure portal.</span></span> <span data-ttu-id="e5df6-128">**Ao usar a atribuição do grupo de licença, todos os usuários sem um local de uso especificado herdam o local de saudação do diretório de saudação.**</span><span class="sxs-lookup"><span data-stu-id="e5df6-128">**When using group license assignment, any users without a usage location specified inherit hello location of hello directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5df6-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5df6-129">Next steps</span></span>

<span data-ttu-id="e5df6-130">Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5df6-130">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="e5df6-131">[**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5df6-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="e5df6-132">[**Dados** ](active-directory-passwords-data.md) - entender dados Olá necessários e como ele é usado para gerenciamento de senha</span><span class="sxs-lookup"><span data-stu-id="e5df6-132">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="e5df6-133">[**Distribuição** ](active-directory-passwords-best-practices.md) -planejar e implantar os usuários de tooyour SSPR usando Olá diretrizes encontradas aqui</span><span class="sxs-lookup"><span data-stu-id="e5df6-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="e5df6-134">[**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aparência de saudação SSPR experiência para sua empresa.</span><span class="sxs-lookup"><span data-stu-id="e5df6-134">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="e5df6-135">[**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR</span><span class="sxs-lookup"><span data-stu-id="e5df6-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="e5df6-136">[**Mergulho profundo técnica** ](active-directory-passwords-how-it-works.md) -vá atrás Olá cortina toounderstand como ele funciona</span><span class="sxs-lookup"><span data-stu-id="e5df6-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="e5df6-137">[**Perguntas frequentes**](active-directory-passwords-faq.md): como?</span><span class="sxs-lookup"><span data-stu-id="e5df6-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="e5df6-138">Por quê?</span><span class="sxs-lookup"><span data-stu-id="e5df6-138">Why?</span></span> <span data-ttu-id="e5df6-139">O quê?</span><span class="sxs-lookup"><span data-stu-id="e5df6-139">What?</span></span> <span data-ttu-id="e5df6-140">Onde?</span><span class="sxs-lookup"><span data-stu-id="e5df6-140">Where?</span></span> <span data-ttu-id="e5df6-141">Quem?</span><span class="sxs-lookup"><span data-stu-id="e5df6-141">Who?</span></span> <span data-ttu-id="e5df6-142">Quando?</span><span class="sxs-lookup"><span data-stu-id="e5df6-142">When?</span></span> <span data-ttu-id="e5df6-143">-Respostas tooquestions você sempre quis tooask</span><span class="sxs-lookup"><span data-stu-id="e5df6-143">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="e5df6-144">[**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR</span><span class="sxs-lookup"><span data-stu-id="e5df6-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

