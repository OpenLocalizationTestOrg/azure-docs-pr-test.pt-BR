---
title: prompt de consentimento aaaUnexpected ao entrar no aplicativo tooan | Microsoft Docs
description: "Como tootroubleshoot quando um usuário vê um prompt de consentimento para um aplicativo que você tiver integrado ao AD do Azure que você não esperava"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a><span data-ttu-id="fb7fd-103">Prompt de consentimento inesperado ao entrar no aplicativo tooan</span><span class="sxs-lookup"><span data-stu-id="fb7fd-103">Unexpected consent prompt when signing in tooan application</span></span>

<span data-ttu-id="fb7fd-104">Muitos aplicativos que se integram com o Active Directory do Azure exigem recursos toovarious permissões toorun de ordem.</span><span class="sxs-lookup"><span data-stu-id="fb7fd-104">Many applications that integrate with Azure Active Directory require permissions toovarious resources in order toorun.</span></span> <span data-ttu-id="fb7fd-105">Quando esses recursos também são integrados com o Active Directory do Azure, permissões tooaccess-los é solicitada usando Olá AD do Azure consentimento do framework.</span><span class="sxs-lookup"><span data-stu-id="fb7fd-105">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is requested using hello Azure AD consent framework.</span></span> 

<span data-ttu-id="fb7fd-106">Isso resulta em um prompt de consentimento sendo mostrado Olá primeira vez que um aplicativo for usado, que geralmente é uma operação única.</span><span class="sxs-lookup"><span data-stu-id="fb7fd-106">This results in a consent prompt being shown hello first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="fb7fd-107">Cenários nos quais os usuários visualizam solicitações de consentimento</span><span class="sxs-lookup"><span data-stu-id="fb7fd-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="fb7fd-108">Solicitações adicionais podem ser esperadas em vários cenários:</span><span class="sxs-lookup"><span data-stu-id="fb7fd-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="fb7fd-109">Olá conjunto de permissões exigido pelo aplicativo hello foi alterado.</span><span class="sxs-lookup"><span data-stu-id="fb7fd-109">hello set of permissions required by hello application have changed.</span></span>

* <span data-ttu-id="fb7fd-110">usuário Olá originalmente consentimento aplicativo toohello não era um administrador, e agora um usuário diferente (não administrativa) está usando aplicativo hello para Olá primeira vez.</span><span class="sxs-lookup"><span data-stu-id="fb7fd-110">hello user who originally consented toohello application was not an administrator, and now a different (non-admin) User is using hello application for hello first time.</span></span>

* <span data-ttu-id="fb7fd-111">usuário Olá originalmente consentimento toohello aplicativo era um administrador, mas eles não consentimento em nome de toda a organização hello.</span><span class="sxs-lookup"><span data-stu-id="fb7fd-111">hello user who originally consented toohello application was an administrator, but they did not consent on-behalf of hello entire organization.</span></span>

* <span data-ttu-id="fb7fd-112">usando o aplicativo Hello [consentimento incremental e dinâmico](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest as permissões adicionais após a autorização inicialmente foi concedida.</span><span class="sxs-lookup"><span data-stu-id="fb7fd-112">hello application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest additional permissions after consent was initially granted.</span></span> <span data-ttu-id="fb7fd-113">Isso é frequentemente usado quando recursos opcionais de um aplicativo adicional exigem permissões além das exigidas para a funcionalidade de linha de base.</span><span class="sxs-lookup"><span data-stu-id="fb7fd-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="fb7fd-114">O consentimento foi revogado após ter sido inicialmente concedido.</span><span class="sxs-lookup"><span data-stu-id="fb7fd-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="fb7fd-115">desenvolvedor Olá configurou Olá aplicativo toorequire uma solicitação de consentimento toda vez que ele é usado (Observação: isso não é prática recomendada).</span><span class="sxs-lookup"><span data-stu-id="fb7fd-115">hello developer has configured hello application toorequire a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb7fd-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fb7fd-116">Next steps</span></span>

-   [<span data-ttu-id="fb7fd-117">Aplicativos, permissões e consentimento no Azure Active Directory (ponto de extremidade v1.0)</span><span class="sxs-lookup"><span data-stu-id="fb7fd-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="fb7fd-118">Escopos, permissões e consentimento de saudação do Active Directory do Azure (ponto de extremidade v 2.0)</span><span class="sxs-lookup"><span data-stu-id="fb7fd-118">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


