---
title: "Azure AD Connect: autenticação de passagem – Limitações atuais | Microsoft Docs"
description: "Este artigo descreve as limitações atuais de saudação de autenticação de passagem do Azure Active Directory (AD do Azure)."
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
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="0f7af-104">Autenticação de passagem do Azure Active Directory: limitações atuais</span><span class="sxs-lookup"><span data-stu-id="0f7af-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="0f7af-105">A autenticação de passagem do Azure AD está atualmente na versão prévia.</span><span class="sxs-lookup"><span data-stu-id="0f7af-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="0f7af-106">É um recurso gratuito e você não terá quaisquer edições pagas do AD do Azure toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="0f7af-106">It is a free feature, and you don't need any paid editions of Azure AD toouse it.</span></span> <span data-ttu-id="0f7af-107">Autenticação de passagem só está disponível na instância de todo o mundo de saudação do AD do Azure e não no [Microsoft Cloud Alemanha](http://www.microsoft.de/cloud-deutschland) e [nuvem do Microsoft Azure Government](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="0f7af-107">Pass-through Authentication is only available in hello world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="0f7af-108">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="0f7af-108">Supported scenarios</span></span>

<span data-ttu-id="0f7af-109">Olá cenários a seguir têm suporte total durante a visualização:</span><span class="sxs-lookup"><span data-stu-id="0f7af-109">hello following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="0f7af-110">Entradas de usuário em todos os aplicativos baseados em navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="0f7af-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="0f7af-111">Entradas de usuário em aplicativos cliente Office 365 com suporte para [autenticação moderna](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="0f7af-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="0f7af-112">Ingresso do Azure AD para dispositivos Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0f7af-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="0f7af-113">Suporte ao Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="0f7af-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="0f7af-114">Cenários sem suporte</span><span class="sxs-lookup"><span data-stu-id="0f7af-114">Unsupported scenarios</span></span>

<span data-ttu-id="0f7af-115">Olá cenários a seguir estão _não_ suporte durante a visualização:</span><span class="sxs-lookup"><span data-stu-id="0f7af-115">hello following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="0f7af-116">Entradas do usuário em aplicativos de cliente herdados do Office (Office 2013 ou anterior).</span><span class="sxs-lookup"><span data-stu-id="0f7af-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="0f7af-117">As organizações são incentivados tooswitch toomodern autenticação, se possível.</span><span class="sxs-lookup"><span data-stu-id="0f7af-117">Organizations are encouraged tooswitch toomodern authentication, if possible.</span></span> <span data-ttu-id="0f7af-118">A autenticação moderna permite o suporte à Autenticação de Passagem, mas também ajuda a proteger suas contas de usuário usando recursos de [acesso condicional](../active-directory-conditional-access.md) como a MFA (Autenticação Multifator).</span><span class="sxs-lookup"><span data-stu-id="0f7af-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="0f7af-119">O usuário entra em aplicativos cliente do Skype for Business, incluindo o Skype for Business 2016.</span><span class="sxs-lookup"><span data-stu-id="0f7af-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="0f7af-120">Logons de usuário no PowerShell v1.0.</span><span class="sxs-lookup"><span data-stu-id="0f7af-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="0f7af-121">É recomendável usar o PowerShell v2.0.</span><span class="sxs-lookup"><span data-stu-id="0f7af-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0f7af-122">Como alternativa para cenários com suporte, habilitar sincronização de Hash de senha em Olá [recursos opcionais](active-directory-aadconnect-get-started-custom.md#optional-features) página no Assistente para conectar-se de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f7af-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on hello [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in hello Azure AD Connect wizard.</span></span> <span data-ttu-id="0f7af-123">Sincronização de Hash de senha age como um fallback para Olá anterior cenários _somente_ (e _não_ como genérica autenticação de fallback por meio do tooPass).</span><span class="sxs-lookup"><span data-stu-id="0f7af-123">Password Hash Synchronization acts as a fallback for hello preceding scenarios _only_ (and _not_ as a generic fallback tooPass-through Authentication).</span></span> <span data-ttu-id="0f7af-124">Se você não precisar desses cenários, desligue a sincronização de hash de senha.</span><span class="sxs-lookup"><span data-stu-id="0f7af-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f7af-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0f7af-125">Next steps</span></span>
- <span data-ttu-id="0f7af-126">[**Início rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md) – instale e execute a autenticação de passagem do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f7af-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="0f7af-127">[**Aprofundamento técnico**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) – entenda como esse recurso funciona.</span><span class="sxs-lookup"><span data-stu-id="0f7af-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="0f7af-128">[**Perguntas frequentes sobre** ](active-directory-aadconnect-pass-through-authentication-faq.md) -respostas toofrequently perguntas frequentes.</span><span class="sxs-lookup"><span data-stu-id="0f7af-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="0f7af-129">[**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Saiba como tooresolve comum problemas com o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f7af-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="0f7af-130">[**SSO contínuo do Azure AD**](active-directory-aadconnect-sso.md) – Saiba mais sobre esse recurso complementar.</span><span class="sxs-lookup"><span data-stu-id="0f7af-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="0f7af-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.</span><span class="sxs-lookup"><span data-stu-id="0f7af-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
