---
title: "Solicitação de consentimento inesperada ao entrar em um aplicativo | Microsoft Docs"
description: "Como solucionar problemas quando um usuário vê uma solicitação de consentimento para um aplicativo integrado com o Azure AD inesperada"
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
ms.openlocfilehash: e5b823e1251a7221f73efe6838d439f827f9665d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-to-an-application"></a><span data-ttu-id="b3300-103">Um usuário vê uma solicitação de consentimento inesperada ao entrar em um aplicativo</span><span class="sxs-lookup"><span data-stu-id="b3300-103">Unexpected consent prompt when signing in to an application</span></span>

<span data-ttu-id="b3300-104">Muitos aplicativos que se integram com o Azure Active Directory exigem permissões a vários recursos para serem executados.</span><span class="sxs-lookup"><span data-stu-id="b3300-104">Many applications that integrate with Azure Active Directory require permissions to various resources in order to run.</span></span> <span data-ttu-id="b3300-105">Quando esses recursos também são integrados com o Azure Active Directory, as permissões para acessá-los são solicitadas usando a estrutura de consentimento do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3300-105">When these resources are also integrated with Azure Active Directory, permissions to access them is requested using the Azure AD consent framework.</span></span> 

<span data-ttu-id="b3300-106">Isso resulta em uma solicitação de consentimento que é exibida na primeira vez em que um aplicativo é usado o que, frequentemente, é uma operação única.</span><span class="sxs-lookup"><span data-stu-id="b3300-106">This results in a consent prompt being shown the first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="b3300-107">Cenários nos quais os usuários visualizam solicitações de consentimento</span><span class="sxs-lookup"><span data-stu-id="b3300-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="b3300-108">Solicitações adicionais podem ser esperadas em vários cenários:</span><span class="sxs-lookup"><span data-stu-id="b3300-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="b3300-109">O conjunto de permissões exigidas pelo aplicativo foi alterado.</span><span class="sxs-lookup"><span data-stu-id="b3300-109">The set of permissions required by the application have changed.</span></span>

* <span data-ttu-id="b3300-110">O usuário que originalmente consentiu para o aplicativo não era um administrador e agora um Usuário diferente (não administrador) está usando o aplicativo pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="b3300-110">The user who originally consented to the application was not an administrator, and now a different (non-admin) User is using the application for the first time.</span></span>

* <span data-ttu-id="b3300-111">O usuário que originalmente consentiu para o aplicativo era um administrador, mas ele não consentiu em nome de toda a organização.</span><span class="sxs-lookup"><span data-stu-id="b3300-111">The user who originally consented to the application was an administrator, but they did not consent on-behalf of the entire organization.</span></span>

* <span data-ttu-id="b3300-112">O aplicativo está usando [consentimento incremental e dinâmico](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) para solicitar permissões adicionais após consentimento inicialmente concedido.</span><span class="sxs-lookup"><span data-stu-id="b3300-112">The application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) to request additional permissions after consent was initially granted.</span></span> <span data-ttu-id="b3300-113">Isso é frequentemente usado quando recursos opcionais de um aplicativo adicional exigem permissões além das exigidas para a funcionalidade de linha de base.</span><span class="sxs-lookup"><span data-stu-id="b3300-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="b3300-114">O consentimento foi revogado após ter sido inicialmente concedido.</span><span class="sxs-lookup"><span data-stu-id="b3300-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="b3300-115">O desenvolvedor configurou o aplicativo para solicitar uma solicitação de consentimento sempre que for usado (observação: essa não é a prática recomendada).</span><span class="sxs-lookup"><span data-stu-id="b3300-115">The developer has configured the application to require a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3300-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b3300-116">Next steps</span></span>

-   [<span data-ttu-id="b3300-117">Aplicativos, permissões e consentimento no Azure Active Directory (ponto de extremidade v1.0)</span><span class="sxs-lookup"><span data-stu-id="b3300-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="b3300-118">Escopos, permissões e consentimento no Azure Active Directory (ponto de extremidade v2.0)</span><span class="sxs-lookup"><span data-stu-id="b3300-118">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


