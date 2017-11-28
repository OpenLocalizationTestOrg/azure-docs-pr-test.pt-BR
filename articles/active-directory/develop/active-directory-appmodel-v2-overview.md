---
title: ponto de extremidade do aaaAzure do Active Directory v 2.0 | Microsoft Docs
description: "Uma introdução toobuilding os aplicativos com Account da Microsoft e o Azure Active Directory entrar."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="89c2e-103">Conecte-se os usuários da Conta da Microsoft e do Azure AD em um único aplicativo</span><span class="sxs-lookup"><span data-stu-id="89c2e-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="89c2e-104">Em Olá anteriores, um desenvolvedor de aplicativo que desejavam toosupport ambas as contas pessoais da Microsoft e contas de trabalho do Azure Active Directory era necessário toointegrate com dois sistemas separados.</span><span class="sxs-lookup"><span data-stu-id="89c2e-104">In hello past, an app developer who wanted toosupport both personal Microsoft accounts and work accounts from Azure Active Directory was required toointegrate with two separate systems.</span></span>  <span data-ttu-id="89c2e-105">Olá **o ponto de extremidade do AD do Azure v 2.0** introduz uma nova versão de API de autenticação que permite que você toosign em ambos os tipos de contas usando uma integração simples.</span><span class="sxs-lookup"><span data-stu-id="89c2e-105">hello **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you toosign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="89c2e-106">Aplicativos que usam o ponto de extremidade do hello v 2.0 também podem consumir APIs REST de saudação [Microsoft Graph](https://graph.microsoft.io) usando qualquer tipo de conta.</span><span class="sxs-lookup"><span data-stu-id="89c2e-106">Apps that use hello v2.0 endpoint can also consume REST APIs from hello [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="89c2e-107">Introdução</span><span class="sxs-lookup"><span data-stu-id="89c2e-107">Getting Started</span></span>
<span data-ttu-id="89c2e-108">Escolha sua plataforma de favorita de saudação toobuild lista a seguir um aplicativo usando nosso bibliotecas de código-fonte aberto e estruturas.</span><span class="sxs-lookup"><span data-stu-id="89c2e-108">Choose your favorite platform from hello following list toobuild an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="89c2e-109">Como alternativa, você pode usar nosso toosend de documentação do protocolo OAuth 2.0 e OpenID Connect e receber mensagens de protocolo diretamente sem usar uma biblioteca de autenticação.</span><span class="sxs-lookup"><span data-stu-id="89c2e-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation toosend & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="89c2e-110">O que há de novo</span><span class="sxs-lookup"><span data-stu-id="89c2e-110">What's New</span></span>
<span data-ttu-id="89c2e-111">informações de saudação aqui serão úteis para entender o que é e o que não é possível com o ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="89c2e-111">hello information here will be useful in understanding what is & what isn't possible with hello v2.0 endpoint.</span></span>

* <span data-ttu-id="89c2e-112">Saiba mais sobre Olá [tipos de aplicativos, você pode criar com o ponto de extremidade do hello v 2.0](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="89c2e-112">Learn about hello [types of apps you can build with hello v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="89c2e-113">Entender Olá [restrições, restrições e limitações](active-directory-v2-limitations.md) com o ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="89c2e-113">Understand hello [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with hello v2.0 endpoint.</span></span>
* <span data-ttu-id="89c2e-114">Confira esta visão geral do vídeo para o ponto de extremidade do hello v 2.0:</span><span class="sxs-lookup"><span data-stu-id="89c2e-114">Check out this overview video for hello v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="89c2e-115">Referência</span><span class="sxs-lookup"><span data-stu-id="89c2e-115">Reference</span></span>
<span data-ttu-id="89c2e-116">Esses links serão úteis para explorar a plataforma de saudação em profundidade:</span><span class="sxs-lookup"><span data-stu-id="89c2e-116">These links will be useful for exploring hello platform in depth:</span></span>

* [<span data-ttu-id="89c2e-117">Referência do Protocolo v2.0</span><span class="sxs-lookup"><span data-stu-id="89c2e-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="89c2e-118">Referência do Token v2.0</span><span class="sxs-lookup"><span data-stu-id="89c2e-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="89c2e-119">Referência da Biblioteca v2.0</span><span class="sxs-lookup"><span data-stu-id="89c2e-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="89c2e-120">Escopos e consentimento no ponto de extremidade do hello v 2.0</span><span class="sxs-lookup"><span data-stu-id="89c2e-120">Scopes and Consent in hello v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="89c2e-121">Olá Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="89c2e-121">hello Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="89c2e-122">Ajuda + suporte</span><span class="sxs-lookup"><span data-stu-id="89c2e-122">Help & Support</span></span>
<span data-ttu-id="89c2e-123">Esses são Olá melhores lugares tooget ajuda com o desenvolvimento no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="89c2e-123">These are hello best places tooget help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="89c2e-124">Marcas `azure-active-directory` e `adal` do Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="89c2e-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="89c2e-125">Feedback no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89c2e-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="89c2e-126">Se você precisar somente toosign em contas corporativas e de estudantes do Active Directory do Azure, você deve começar com nossos [guia do desenvolvedor do AD do Azure](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="89c2e-126">If you only need toosign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="89c2e-127">o ponto de extremidade do Hello v 2.0 é destinado ao uso por desenvolvedores que precisam explicitamente toosign em contas pessoais da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="89c2e-127">hello v2.0 endpoint is intended for use by developers who explicitly need toosign in Microsoft personal accounts.</span></span>

