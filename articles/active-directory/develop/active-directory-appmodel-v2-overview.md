---
title: Ponto de extremidade do Azure Active Directory v.2.0 | Microsoft Docs
description: "Uma introdução à criação de aplicativos com conexão à conta da Microsoft e ao Active Directory do Azure."
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
ms.openlocfilehash: 1e286044fb1a1b367fcac2dc14c47f68d5ed120d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="f6831-103">Conecte-se os usuários da Conta da Microsoft e do Azure AD em um único aplicativo</span><span class="sxs-lookup"><span data-stu-id="f6831-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="f6831-104">No passado, um desenvolvedor de aplicativos que quisesse dar suporte a contas da Microsoft pessoas e contas profissionais do Azure Active Directory precisava fazer a integração com dois sistemas separados.</span><span class="sxs-lookup"><span data-stu-id="f6831-104">In the past, an app developer who wanted to support both personal Microsoft accounts and work accounts from Azure Active Directory was required to integrate with two separate systems.</span></span>  <span data-ttu-id="f6831-105">O **ponto de extremidade do Azure AD v2.0** introduz uma nova versão da API de autenticação que permite que você entre nos dois tipos de contas usando uma integração simples.</span><span class="sxs-lookup"><span data-stu-id="f6831-105">The **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you to sign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="f6831-106">Aplicativos que usam o ponto de extremidade v2.0 também consomem APIs REST do [Microsoft Graph](https://graph.microsoft.io) usando qualquer um dos tipos de conta.</span><span class="sxs-lookup"><span data-stu-id="f6831-106">Apps that use the v2.0 endpoint can also consume REST APIs from the [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f6831-107">Introdução</span><span class="sxs-lookup"><span data-stu-id="f6831-107">Getting Started</span></span>
<span data-ttu-id="f6831-108">Escolha sua plataforma favorita na lista a seguir para compilar um aplicativo usando nossas bibliotecas e estruturas de software livre.</span><span class="sxs-lookup"><span data-stu-id="f6831-108">Choose your favorite platform from the following list to build an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="f6831-109">Como alternativa, é possível usar nossa documentação do protocolo do OAuth 2.0 e OpenID Connect para enviar e receber mensagens de protocolo diretamente sem o uso de uma biblioteca de autenticação.</span><span class="sxs-lookup"><span data-stu-id="f6831-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation to send & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="f6831-110">O que há de novo</span><span class="sxs-lookup"><span data-stu-id="f6831-110">What's New</span></span>
<span data-ttu-id="f6831-111">As informações aqui serão úteis para entender o que é possível e o que não é com o ponto de extremidade v2.0.</span><span class="sxs-lookup"><span data-stu-id="f6831-111">The information here will be useful in understanding what is & what isn't possible with the v2.0 endpoint.</span></span>

* <span data-ttu-id="f6831-112">Saiba mais sobre os [tipos de aplicativos que podem ser criados com o ponto de extremidade v2.0](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="f6831-112">Learn about the [types of apps you can build with the v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="f6831-113">Entenda as [limitações e restrições](active-directory-v2-limitations.md) do ponto de extremidade v2.0.</span><span class="sxs-lookup"><span data-stu-id="f6831-113">Understand the [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with the v2.0 endpoint.</span></span>
* <span data-ttu-id="f6831-114">Confira este vídeo de visão geral para o ponto de extremidade v2.0:</span><span class="sxs-lookup"><span data-stu-id="f6831-114">Check out this overview video for the v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="f6831-115">Referência</span><span class="sxs-lookup"><span data-stu-id="f6831-115">Reference</span></span>
<span data-ttu-id="f6831-116">Estes links serão úteis na exploração em profundidade da plataforma:</span><span class="sxs-lookup"><span data-stu-id="f6831-116">These links will be useful for exploring the platform in depth:</span></span>

* [<span data-ttu-id="f6831-117">Referência do Protocolo v2.0</span><span class="sxs-lookup"><span data-stu-id="f6831-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="f6831-118">Referência do Token v2.0</span><span class="sxs-lookup"><span data-stu-id="f6831-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="f6831-119">Referência da Biblioteca v2.0</span><span class="sxs-lookup"><span data-stu-id="f6831-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="f6831-120">Escopos e Consentimento no ponto de extremidade v2.0</span><span class="sxs-lookup"><span data-stu-id="f6831-120">Scopes and Consent in the v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="f6831-121">O Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="f6831-121">The Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="f6831-122">Ajuda + suporte</span><span class="sxs-lookup"><span data-stu-id="f6831-122">Help & Support</span></span>
<span data-ttu-id="f6831-123">Esses são os melhores locais para obter ajuda com o desenvolvimento no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6831-123">These are the best places to get help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="f6831-124">Marcas `azure-active-directory` e `adal` do Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="f6831-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="f6831-125">Feedback no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6831-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="f6831-126">Se você precisar apenas entrar em contas corporativas e de estudante usando o Azure Active Directory, comece com nosso [guia do desenvolvedor do Azure AD](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="f6831-126">If you only need to sign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="f6831-127">O ponto de extremidade v2.0 destina-se ao uso por desenvolvedores que precisam explicitamente entrar em contas pessoais da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f6831-127">The v2.0 endpoint is intended for use by developers who explicitly need to sign in Microsoft personal accounts.</span></span>

