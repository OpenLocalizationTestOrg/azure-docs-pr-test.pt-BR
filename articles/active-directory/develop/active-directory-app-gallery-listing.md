---
title: "aaaListing seu aplicativo na Galeria de aplicativo do Active Directory do Azure Olá"
description: "Como toolist um aplicativo que oferece suporte a logon único no hello Galeria do Active Directory do Azure | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a><span data-ttu-id="e68a7-103">Listando seu aplicativo na Galeria de aplicativo do Active Directory do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="e68a7-103">Listing your application in hello Azure Active Directory application gallery</span></span>
<span data-ttu-id="e68a7-104">toolist um aplicativo que oferece suporte a logon único com o Azure Active Directory em Olá [Galeria do Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), aplicativo hello primeiro precisa tooimplement de saudação modos de integração a seguir:</span><span class="sxs-lookup"><span data-stu-id="e68a7-104">toolist an application that supports single sign-on with Azure Active Directory in hello [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), hello application first needs tooimplement one of hello following integration modes:</span></span>

* <span data-ttu-id="e68a7-105">**OpenID Connect** - a integração direta com o Azure AD usando o OpenID Connect para autenticação e Olá consentimento do AD do Azure API para a configuração.</span><span class="sxs-lookup"><span data-stu-id="e68a7-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="e68a7-106">Se você estiver apenas começando uma integração e seu aplicativo não suporta SAML, isso é o modo recomendado hello.</span><span class="sxs-lookup"><span data-stu-id="e68a7-106">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
* <span data-ttu-id="e68a7-107">**SAML** – seu aplicativo já tem provedores de identidade de terceiros Olá capacidade tooconfigure usando o protocolo do SAML hello.</span><span class="sxs-lookup"><span data-stu-id="e68a7-107">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="e68a7-108">Os requisitos de listagem para cada modo estão abaixo.</span><span class="sxs-lookup"><span data-stu-id="e68a7-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="e68a7-109">Integração do OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="e68a7-109">OpenID Connect Integration</span></span>
<span data-ttu-id="e68a7-110">toointegrate seu aplicativo com o Azure AD, Olá seguir [instruções de desenvolvedor](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="e68a7-110">toointegrate your application with Azure AD, following hello [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="e68a7-111">Em seguida, concluir perguntas de saudação abaixo e enviar toowaadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="e68a7-111">Then complete hello questions below and send toowaadpartners@microsoft.com.</span></span>

* <span data-ttu-id="e68a7-112">Forneça credenciais para uma conta ou Locatário de teste com o aplicativo que pode ser usado por Olá integração do AD do Azure team tootest hello.</span><span class="sxs-lookup"><span data-stu-id="e68a7-112">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="e68a7-113">Fornece instruções sobre como team Olá AD do Azure pode entrar e se conectar a uma instância do aplicativo do AD do Azure tooyour usando Olá [estrutura de consentimento do AD do Azure](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="e68a7-113">Provide instructions on how hello Azure AD team can sign in and connect an instance of Azure AD tooyour application using hello [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="e68a7-114">Forneça quaisquer instruções adicionais necessárias para Olá AD do Azure da equipe tootest logon único com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e68a7-114">Provide any further instructions required for hello Azure AD team tootest single sign-on with your application.</span></span> 
* <span data-ttu-id="e68a7-115">Fornece informações de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="e68a7-115">Provide hello info below:</span></span>

> <span data-ttu-id="e68a7-116">Nome da empresa:</span><span class="sxs-lookup"><span data-stu-id="e68a7-116">Company Name:</span></span>
> 
> <span data-ttu-id="e68a7-117">Site da empresa:</span><span class="sxs-lookup"><span data-stu-id="e68a7-117">Company Website:</span></span>
> 
> <span data-ttu-id="e68a7-118">Nome do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="e68a7-118">Application Name:</span></span>
> 
> <span data-ttu-id="e68a7-119">Descrição do aplicativo (limite de 200 caracteres):</span><span class="sxs-lookup"><span data-stu-id="e68a7-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="e68a7-120">Site do aplicativo (informativo):</span><span class="sxs-lookup"><span data-stu-id="e68a7-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="e68a7-121">Site de suporte técnico do aplicativo ou informações de contato:</span><span class="sxs-lookup"><span data-stu-id="e68a7-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="e68a7-122">ID do aplicativo hello, conforme mostrado nos detalhes do aplicativo hello em https://portal.azure.com:</span><span class="sxs-lookup"><span data-stu-id="e68a7-122">Application  ID of hello application, as shown in hello application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="e68a7-123">URL de inscrição do aplicativo onde os clientes estão toosign para e/ou comprar o aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="e68a7-123">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="e68a7-124">Escolha as categorias de toothree para sua toobe aplicativo listado em (para categorias disponíveis, consulte Olá Marketplace do Azure Active Directory):</span><span class="sxs-lookup"><span data-stu-id="e68a7-124">Choose up toothree categories for your application toobe listed under (for available categories see hello Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="e68a7-125">Anexe o ícone pequeno do aplicativo (arquivo PNG, 45px por 45px, cor de plano de fundo sólida):</span><span class="sxs-lookup"><span data-stu-id="e68a7-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="e68a7-126">Anexe o ícone grande do aplicativo (arquivo PNG, 215px por 215px, cor de plano de fundo transparente):</span><span class="sxs-lookup"><span data-stu-id="e68a7-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="e68a7-127">Anexe o logotipo do aplicativo (arquivo PNG, 150px por 122px, cor de plano de fundo transparente):</span><span class="sxs-lookup"><span data-stu-id="e68a7-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="e68a7-128">Integração SAML</span><span class="sxs-lookup"><span data-stu-id="e68a7-128">SAML Integration</span></span>
<span data-ttu-id="e68a7-129">Qualquer aplicativo que suporte o SAML 2.0 pode ser integrado diretamente com um locatário Azure AD usando [tooadd essas instruções um aplicativo personalizado](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="e68a7-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions tooadd a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="e68a7-130">Depois de testar se a integração de aplicativo funciona com o Azure AD, enviar Olá informações a seguir muito<mailto:waadpartners@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="e68a7-130">Once you have tested that your application integration works with Azure AD, send hello following information too<mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="e68a7-131">Forneça credenciais para uma conta ou Locatário de teste com o aplicativo que pode ser usado por Olá integração do AD do Azure team tootest hello.</span><span class="sxs-lookup"><span data-stu-id="e68a7-131">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="e68a7-132">Fornecer Olá SAML URL de logon, a URL do emissor (ID da entidade), e valores de URL de resposta (serviço do consumidor de declaração) para seu aplicativo, conforme descrito [aqui](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="e68a7-132">Provide hello SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="e68a7-133">Se você geralmente fornece esses valores como parte de um arquivo de metadados do SAML, envie este também.</span><span class="sxs-lookup"><span data-stu-id="e68a7-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="e68a7-134">Forneça uma breve descrição de como tooconfigure AD do Azure como um provedor de identidade em seu aplicativo usando o SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="e68a7-134">Provide a brief description of how tooconfigure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="e68a7-135">Se seu aplicativo dá suporte à configuração do AD do Azure como um provedor de identidade por meio de um portal administrativo de autoatendimento, em seguida, verifique se as credenciais de saudação fornecidas acima incluem hello capacidade tooset esse.</span><span class="sxs-lookup"><span data-stu-id="e68a7-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure hello credentials provided above include hello ability tooset this up.</span></span>
* <span data-ttu-id="e68a7-136">Fornece informações de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="e68a7-136">Provide hello info below:</span></span>

> <span data-ttu-id="e68a7-137">Nome da empresa:</span><span class="sxs-lookup"><span data-stu-id="e68a7-137">Company Name:</span></span>
> 
> <span data-ttu-id="e68a7-138">Site da empresa:</span><span class="sxs-lookup"><span data-stu-id="e68a7-138">Company Website:</span></span>
> 
> <span data-ttu-id="e68a7-139">Nome do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="e68a7-139">Application Name:</span></span>
> 
> <span data-ttu-id="e68a7-140">Descrição do aplicativo (limite de 200 caracteres):</span><span class="sxs-lookup"><span data-stu-id="e68a7-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="e68a7-141">Site do aplicativo (informativo):</span><span class="sxs-lookup"><span data-stu-id="e68a7-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="e68a7-142">Site de suporte técnico do aplicativo ou informações de contato:</span><span class="sxs-lookup"><span data-stu-id="e68a7-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="e68a7-143">URL de inscrição do aplicativo onde os clientes estão toosign para e/ou comprar o aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="e68a7-143">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="e68a7-144">Escolha as categorias de toothree para sua toobe aplicativo listado em (para categorias disponíveis, consulte Olá [Marketplace do Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="e68a7-144">Choose up toothree categories for your application toobe listed under (for available categories see hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="e68a7-145">Anexe o ícone pequeno do aplicativo (arquivo PNG, 45px por 45px, cor de plano de fundo sólida):</span><span class="sxs-lookup"><span data-stu-id="e68a7-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="e68a7-146">Anexe o ícone grande do aplicativo (arquivo PNG, 215px por 215px, cor de plano de fundo transparente):</span><span class="sxs-lookup"><span data-stu-id="e68a7-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="e68a7-147">Anexe o logotipo do aplicativo (arquivo PNG, 150px por 122px, cor de plano de fundo transparente):</span><span class="sxs-lookup"><span data-stu-id="e68a7-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

