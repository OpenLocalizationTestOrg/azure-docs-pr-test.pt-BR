---
title: "Azure AD Connect: autenticação de passagem – Limitações atuais | Microsoft Docs"
description: "Este artigo descreve as limitações atuais da autenticação de passagem do Azure AD (Azure Active Directory)."
services: active-directory
keywords: "Autenticação de Passagem do Azure AD Connect, instalar o Active Directory, componentes necessários para o Azure AD, SSO, Logon único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 37c0ea094d02208f2516a4a040f75894e046c670
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="21eeb-104">Autenticação de passagem do Azure Active Directory: limitações atuais</span><span class="sxs-lookup"><span data-stu-id="21eeb-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="21eeb-105">A autenticação de passagem do Azure AD está atualmente na versão prévia.</span><span class="sxs-lookup"><span data-stu-id="21eeb-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="21eeb-106">Essa é um recurso gratuito e você não precisa de nenhuma edição paga do Azure AD para usá-lo.</span><span class="sxs-lookup"><span data-stu-id="21eeb-106">It is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="21eeb-107">A autenticação de passagem só está disponível na instância mundial do Azure AD e não no [Microsoft Cloud Alemanha](http://www.microsoft.de/cloud-deutschland) nem na [Nuvem do Microsoft Azure Governamental](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="21eeb-107">Pass-through Authentication is only available in the world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="21eeb-108">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="21eeb-108">Supported scenarios</span></span>

<span data-ttu-id="21eeb-109">Os cenários a seguir têm suporte total durante a visualização:</span><span class="sxs-lookup"><span data-stu-id="21eeb-109">The following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="21eeb-110">Entradas de usuário em todos os aplicativos baseados em navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="21eeb-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="21eeb-111">Entradas de usuário em aplicativos cliente Office 365 com suporte para [autenticação moderna](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="21eeb-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="21eeb-112">Ingresso do Azure AD para dispositivos Windows 10.</span><span class="sxs-lookup"><span data-stu-id="21eeb-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="21eeb-113">Suporte ao Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="21eeb-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="21eeb-114">Cenários sem suporte</span><span class="sxs-lookup"><span data-stu-id="21eeb-114">Unsupported scenarios</span></span>

<span data-ttu-id="21eeb-115">Os cenários a seguir _não_ têm suporte durante a versão prévia:</span><span class="sxs-lookup"><span data-stu-id="21eeb-115">The following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="21eeb-116">Entradas do usuário em aplicativos de cliente herdados do Office (Office 2013 ou anterior).</span><span class="sxs-lookup"><span data-stu-id="21eeb-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="21eeb-117">As organizações são incentivadas a mudar para autenticação moderna se possível.</span><span class="sxs-lookup"><span data-stu-id="21eeb-117">Organizations are encouraged to switch to modern authentication, if possible.</span></span> <span data-ttu-id="21eeb-118">A autenticação moderna permite o suporte à Autenticação de Passagem, mas também ajuda a proteger suas contas de usuário usando recursos de [acesso condicional](../active-directory-conditional-access.md) como a MFA (Autenticação Multifator).</span><span class="sxs-lookup"><span data-stu-id="21eeb-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="21eeb-119">O usuário entra em aplicativos cliente do Skype for Business, incluindo o Skype for Business 2016.</span><span class="sxs-lookup"><span data-stu-id="21eeb-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="21eeb-120">Logons de usuário no PowerShell v1.0.</span><span class="sxs-lookup"><span data-stu-id="21eeb-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="21eeb-121">É recomendável usar o PowerShell v2.0.</span><span class="sxs-lookup"><span data-stu-id="21eeb-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="21eeb-122">Como alternativa para cenários sem suporte, habilite a sincronização de hash de senha na página [Recursos opcionais](active-directory-aadconnect-get-started-custom.md#optional-features) do assistente do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="21eeb-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on the [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in the Azure AD Connect wizard.</span></span> <span data-ttu-id="21eeb-123">A sincronização de hash de senha age como um fallback _somente_ para os cenários anteriores (e _não_ como um fallback genérico para autenticação de passagem).</span><span class="sxs-lookup"><span data-stu-id="21eeb-123">Password Hash Synchronization acts as a fallback for the preceding scenarios _only_ (and _not_ as a generic fallback to Pass-through Authentication).</span></span> <span data-ttu-id="21eeb-124">Se você não precisar desses cenários, desligue a sincronização de hash de senha.</span><span class="sxs-lookup"><span data-stu-id="21eeb-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21eeb-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="21eeb-125">Next steps</span></span>
- <span data-ttu-id="21eeb-126">[**Início rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md) – instale e execute a autenticação de passagem do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21eeb-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="21eeb-127">[**Aprofundamento técnico**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) – entenda como esse recurso funciona.</span><span class="sxs-lookup"><span data-stu-id="21eeb-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="21eeb-128">[**Perguntas frequentes**](active-directory-aadconnect-pass-through-authentication-faq.md) – respostas para perguntas frequentes.</span><span class="sxs-lookup"><span data-stu-id="21eeb-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="21eeb-129">[**Solução de problemas**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) – Saiba como resolver problemas comuns do recurso.</span><span class="sxs-lookup"><span data-stu-id="21eeb-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="21eeb-130">[**SSO contínuo do Azure AD**](active-directory-aadconnect-sso.md) – Saiba mais sobre esse recurso complementar.</span><span class="sxs-lookup"><span data-stu-id="21eeb-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="21eeb-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.</span><span class="sxs-lookup"><span data-stu-id="21eeb-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
