---
title: "Como configurar um novo aplicativo multilocatário | Microsoft Docs"
description: "Como configurar o logon único para um aplicativo personalizado que você está desenvolvendo e registrar com o Azure AD."
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
ms.openlocfilehash: 0fdc58d82d9cd2e7edac33cc5af4b98d2fd06c56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-a-new-multi-tenant-application"></a><span data-ttu-id="04fef-103">Como configurar um novo aplicativo multilocatário</span><span class="sxs-lookup"><span data-stu-id="04fef-103">How to configure a new multi-tenant application</span></span>

<span data-ttu-id="04fef-104">Habilitar logon único federado (SSO) em seu aplicativo é habilitado automaticamente por meio do Azure AD para OpenID Connect, SAML 2.0 ou WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="04fef-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="04fef-105">Se os usuários finais estão precisando entrar, mesmo já tendo uma sessão existente com o Azure AD, é provável que seu aplicativo possa estar configurado incorretamente.</span><span class="sxs-lookup"><span data-stu-id="04fef-105">If your end users are having to sign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="04fef-106">Se você estiver usando o ADAL/MSAL, verifique se você tem o **PromptBehavior** definido como **Automático** em vez de **Sempre**.</span><span class="sxs-lookup"><span data-stu-id="04fef-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set to **Auto** rather than **Always**.</span></span>

* <span data-ttu-id="04fef-107">Se você estiver criando um aplicativo móvel, talvez seja necessário configurações adicionais para habilitar SSO orientado ou não orientado.</span><span class="sxs-lookup"><span data-stu-id="04fef-107">If you’re building a mobile app, you may need additional configurations to enable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="04fef-108">Para o Android, consulte [Habilitando SSO entre aplicativos no Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="04fef-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="04fef-109">Para o iOS, consulte [Habilitando SSO entre aplicativos no iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="04fef-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04fef-110">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04fef-110">Next steps</span></span>

[<span data-ttu-id="04fef-111">SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="04fef-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="04fef-112">Habilitando SSO entre aplicativos no Android</span><span class="sxs-lookup"><span data-stu-id="04fef-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="04fef-113">Habilitando SSO entre aplicativos no iOS</span><span class="sxs-lookup"><span data-stu-id="04fef-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="04fef-114">Integrando aplicativos ao AzureAD</span><span class="sxs-lookup"><span data-stu-id="04fef-114">Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="04fef-115">Consentimento e permissão para aplicativos convergidos do AzureAD v2.0</span><span class="sxs-lookup"><span data-stu-id="04fef-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="04fef-116">StackOverflow do AzureAD</span><span class="sxs-lookup"><span data-stu-id="04fef-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
