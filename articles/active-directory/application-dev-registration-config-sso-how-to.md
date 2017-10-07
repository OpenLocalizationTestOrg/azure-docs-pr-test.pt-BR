---
title: "aaaHow tooconfigure um novo aplicativo multilocatário | Microsoft Docs"
description: "Como tooconfigure single sign-on para um aplicativo personalizado, você está desenvolvendo e registrar com o AD do Azure."
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
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a><span data-ttu-id="71dac-103">Como tooconfigure um novo aplicativo multilocatário</span><span class="sxs-lookup"><span data-stu-id="71dac-103">How tooconfigure a new multi-tenant application</span></span>

<span data-ttu-id="71dac-104">Habilitar logon único federado (SSO) em seu aplicativo é habilitado automaticamente por meio do Azure AD para OpenID Connect, SAML 2.0 ou WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="71dac-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="71dac-105">Se seus usuários finais estão tendo toosign mesmo já tendo uma sessão existente com o Azure AD, é provável que seu aplicativo pode estar configurado incorretamente.</span><span class="sxs-lookup"><span data-stu-id="71dac-105">If your end users are having toosign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="71dac-106">Se você estiver usando o ADAL/MSAL, verifique se você tem **PromptBehavior** definido muito**automática** em vez de **sempre**.</span><span class="sxs-lookup"><span data-stu-id="71dac-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set too**Auto** rather than **Always**.</span></span>

* <span data-ttu-id="71dac-107">Se você estiver criando um aplicativo móvel, talvez seja necessário configurações adicionais tooenable orientadas ou não orientadas SSO.</span><span class="sxs-lookup"><span data-stu-id="71dac-107">If you’re building a mobile app, you may need additional configurations tooenable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="71dac-108">Para o Android, consulte [Habilitando SSO entre aplicativos no Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="71dac-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="71dac-109">Para o iOS, consulte [Habilitando SSO entre aplicativos no iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="71dac-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="71dac-110">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="71dac-110">Next steps</span></span>

[<span data-ttu-id="71dac-111">SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="71dac-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="71dac-112">Habilitando SSO entre aplicativos no Android</span><span class="sxs-lookup"><span data-stu-id="71dac-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="71dac-113">Habilitando SSO entre aplicativos no iOS</span><span class="sxs-lookup"><span data-stu-id="71dac-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="71dac-114">Integrando aplicativos tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="71dac-114">Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="71dac-115">Consentimento e permissão para aplicativos convergidos do AzureAD v2.0</span><span class="sxs-lookup"><span data-stu-id="71dac-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="71dac-116">StackOverflow do AzureAD</span><span class="sxs-lookup"><span data-stu-id="71dac-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
