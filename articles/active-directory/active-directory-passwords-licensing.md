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
ms.openlocfilehash: 936134bddad19964f809a17f200ebbeed5aa853c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="0b937-103">Requisitos de licenciamento para redefinição da senha de autoatendimento do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b937-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="0b937-104">Para a redefinição de senhas do AD do Azure funcionar, você **deverá ter pelo menos uma licença atribuída na sua organização**.</span><span class="sxs-lookup"><span data-stu-id="0b937-104">In order for Azure AD Password Reset to function, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="0b937-105">Não impomos licenciamento por usuário na experiência de redefinição da senha.</span><span class="sxs-lookup"><span data-stu-id="0b937-105">We do not enforce per-user licensing on the password reset experience.</span></span> <span data-ttu-id="0b937-106">Para manter a conformidade com o contrato de licenciamento da Microsoft, você precisa atribuir licenças a todos os usuários que usam recursos premium.</span><span class="sxs-lookup"><span data-stu-id="0b937-106">To maintain compliance with your Microsoft licensing agreement, you need to assign licenses to any users that use premium features.</span></span>

* <span data-ttu-id="0b937-107">**Somente usuários de nuvem** – Qualquer SKU pago do Office 365 (O365) ou Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="0b937-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="0b937-108">Usuários na **nuvem** e/ou **locais** – Azure AD Premium P1 ou P2, Enterprise Mobility + Security (EMS) ou Secure Productive Enterprise (SPE)</span><span class="sxs-lookup"><span data-stu-id="0b937-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="0b937-109">Licenças necessárias para write-back de senha</span><span class="sxs-lookup"><span data-stu-id="0b937-109">Licenses required for password writeback</span></span>

<span data-ttu-id="0b937-110">Para usar o write-back de senha, você deve ter uma das licenças a seguir atribuídas no locatário.</span><span class="sxs-lookup"><span data-stu-id="0b937-110">To use password writeback, you must have one of the following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="0b937-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="0b937-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="0b937-112">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="0b937-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="0b937-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="0b937-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="0b937-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="0b937-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="0b937-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="0b937-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="0b937-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="0b937-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="0b937-117">Os planos de licenciamento do Standalone Office 365 **não dão suporte ao write-back de senha** e exigem um dos planos anteriores para que essa funcionalidade funcione.</span><span class="sxs-lookup"><span data-stu-id="0b937-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of the preceding plans for this functionality to work.</span></span>

<span data-ttu-id="0b937-118">As informações de licenciamento adicionais, inclusive custos, podem ser encontradas nas páginas a seguir</span><span class="sxs-lookup"><span data-stu-id="0b937-118">Additional licensing info including costs can be found on the following pages</span></span>

* [<span data-ttu-id="0b937-119">Site de Preços do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b937-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="0b937-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="0b937-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="0b937-121">Secure Productive Enterprise</span><span class="sxs-lookup"><span data-stu-id="0b937-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="0b937-122">Habilitar licenciamento com base em grupo ou usuário</span><span class="sxs-lookup"><span data-stu-id="0b937-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="0b937-123">O Azure AD já dá suporte ao licenciamento com base em grupo, permitindo que os administradores atribuam licenças em massa a um grupo de usuários, em vez de atribuí-los um por vez.</span><span class="sxs-lookup"><span data-stu-id="0b937-123">Azure AD now supports group-based licensing allowing administrators to assign licenses in bulk to a group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="0b937-124">Atribuir, verificar e resolver problemas com licenças</span><span class="sxs-lookup"><span data-stu-id="0b937-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="0b937-125">Alguns serviços da Microsoft não estão disponíveis em todos os locais.</span><span class="sxs-lookup"><span data-stu-id="0b937-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="0b937-126">Para que uma licença possa ser atribuída a um usuário, o administrador precisa especificar a propriedade “Local de uso” para o usuário.</span><span class="sxs-lookup"><span data-stu-id="0b937-126">Before a license can be assigned to a user, the administrator must specify the “Usage location” property on the user.</span></span> <span data-ttu-id="0b937-127">A atribuição de licenças pode ser feita em Usuário > Perfil > seção Configurações no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b937-127">Assignment of licenses can be done under User > Profile > Settings section in the Azure portal.</span></span> <span data-ttu-id="0b937-128">**Ao usar a atribuição de grupo de licenças, qualquer usuário sem um local de uso especificado herda o local do diretório.**</span><span class="sxs-lookup"><span data-stu-id="0b937-128">**When using group license assignment, any users without a usage location specified inherit the location of the directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b937-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0b937-129">Next steps</span></span>

<span data-ttu-id="0b937-130">Os links a seguir fornecem informações adicionais sobre a redefinição de senha usando o Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b937-130">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="0b937-131">[**Início rápido** ](active-directory-passwords-getting-started.md) - Para deixar em funcionamento com o gerenciamento de senha de autoatendimento do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b937-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="0b937-132">[**Dados** ](active-directory-passwords-data.md) - Entender os dados necessários e como são usados para o gerenciamento de senhas</span><span class="sxs-lookup"><span data-stu-id="0b937-132">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="0b937-133">[**Distribuição**](active-directory-passwords-best-practices.md): planeje e implante o SSPR para seus usuários usando as diretrizes descritas aqui</span><span class="sxs-lookup"><span data-stu-id="0b937-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="0b937-134">[**Personalizar**](active-directory-passwords-customize.md): personalize a aparência da experiência do SSPR em sua empresa.</span><span class="sxs-lookup"><span data-stu-id="0b937-134">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="0b937-135">[**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR</span><span class="sxs-lookup"><span data-stu-id="0b937-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="0b937-136">[**Detalhamento Técnico**](active-directory-passwords-how-it-works.md): veja os bastidores para entender como o recurso funciona</span><span class="sxs-lookup"><span data-stu-id="0b937-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="0b937-137">[**Perguntas frequentes**](active-directory-passwords-faq.md): como?</span><span class="sxs-lookup"><span data-stu-id="0b937-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="0b937-138">Por quê?</span><span class="sxs-lookup"><span data-stu-id="0b937-138">Why?</span></span> <span data-ttu-id="0b937-139">O quê?</span><span class="sxs-lookup"><span data-stu-id="0b937-139">What?</span></span> <span data-ttu-id="0b937-140">Onde?</span><span class="sxs-lookup"><span data-stu-id="0b937-140">Where?</span></span> <span data-ttu-id="0b937-141">Quem?</span><span class="sxs-lookup"><span data-stu-id="0b937-141">Who?</span></span> <span data-ttu-id="0b937-142">Quando?</span><span class="sxs-lookup"><span data-stu-id="0b937-142">When?</span></span> <span data-ttu-id="0b937-143">– respostas para perguntas que você sempre quis fazer</span><span class="sxs-lookup"><span data-stu-id="0b937-143">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="0b937-144">[**Solução de problemas**](active-directory-passwords-troubleshoot.md) - Saiba como resolver problemas comuns que vemos com a SSPR</span><span class="sxs-lookup"><span data-stu-id="0b937-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

