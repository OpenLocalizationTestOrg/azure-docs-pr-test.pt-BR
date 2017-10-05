---
title: Listando seu aplicativo na galeria de aplicativos do Azure Active Directory
description: "Como listar um aplicativo que oferece suporte a logon único na galeria do Active Directory do Azure | Microsoft Azure"
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
ms.openlocfilehash: cf25772bd9d92b59401aa5da76e6bbd5fa5ee3e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="listing-your-application-in-the-azure-active-directory-application-gallery"></a><span data-ttu-id="31e4c-103">Listando seu aplicativo na galeria de aplicativos do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31e4c-103">Listing your application in the Azure Active Directory application gallery</span></span>
<span data-ttu-id="31e4c-104">Para listar um aplicativo que dê suporte a logon único com o Active Directory do Azure na [galeria do Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), o aplicativo primeiro precisa implementar um dos seguintes modos de integração:</span><span class="sxs-lookup"><span data-stu-id="31e4c-104">To list an application that supports single sign-on with Azure Active Directory in the [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), the application first needs to implement one of the following integration modes:</span></span>

* <span data-ttu-id="31e4c-105">**OpenID Connect** : integração direta com o Azure AD usando o OpenID Connect para autenticação e a API de consentimento do AD do Azure para configuração.</span><span class="sxs-lookup"><span data-stu-id="31e4c-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="31e4c-106">Se você estiver apenas começando uma integração e seu aplicativo não der suporte a SAML, esse é o modo recomendado.</span><span class="sxs-lookup"><span data-stu-id="31e4c-106">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
* <span data-ttu-id="31e4c-107">**SAML** : seu aplicativo já tem a capacidade de configurar provedores de identidade de terceiros usando o protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="31e4c-107">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="31e4c-108">Os requisitos de listagem para cada modo estão abaixo.</span><span class="sxs-lookup"><span data-stu-id="31e4c-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="31e4c-109">Integração do OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="31e4c-109">OpenID Connect Integration</span></span>
<span data-ttu-id="31e4c-110">Para integrar seu aplicativo ao Azure AD, siga as [instruções de desenvolvedor](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="31e4c-110">To integrate your application with Azure AD, following the [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="31e4c-111">Responda às perguntas abaixo e envie para waadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="31e4c-111">Then complete the questions below and send to waadpartners@microsoft.com.</span></span>

* <span data-ttu-id="31e4c-112">Fornece credenciais para uma conta ou locatário de teste com o aplicativo que pode ser usado pela equipe do Azure AD para testar a integração.</span><span class="sxs-lookup"><span data-stu-id="31e4c-112">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="31e4c-113">Forneça instruções sobre como a equipe do AD do Azure pode entrar e conectar uma instância do AD do Azure em seu aplicativo usando a [estrutura de consentimento do AD do Azure](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="31e4c-113">Provide instructions on how the Azure AD team can sign in and connect an instance of Azure AD to your application using the [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="31e4c-114">Forneça instruções adicionais necessárias à equipe do AD do Azure para testar o logon único no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="31e4c-114">Provide any further instructions required for the Azure AD team to test single sign-on with your application.</span></span> 
* <span data-ttu-id="31e4c-115">Forneça as informações abaixo:</span><span class="sxs-lookup"><span data-stu-id="31e4c-115">Provide the info below:</span></span>

> <span data-ttu-id="31e4c-116">Nome da empresa:</span><span class="sxs-lookup"><span data-stu-id="31e4c-116">Company Name:</span></span>
> 
> <span data-ttu-id="31e4c-117">Site da empresa:</span><span class="sxs-lookup"><span data-stu-id="31e4c-117">Company Website:</span></span>
> 
> <span data-ttu-id="31e4c-118">Nome do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="31e4c-118">Application Name:</span></span>
> 
> <span data-ttu-id="31e4c-119">Descrição do aplicativo (limite de 200 caracteres):</span><span class="sxs-lookup"><span data-stu-id="31e4c-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="31e4c-120">Site do aplicativo (informativo):</span><span class="sxs-lookup"><span data-stu-id="31e4c-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="31e4c-121">Site de suporte técnico do aplicativo ou informações de contato:</span><span class="sxs-lookup"><span data-stu-id="31e4c-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="31e4c-122">ID do aplicativo, conforme mostrado nos detalhes do aplicativo em https://portal.azure.com:</span><span class="sxs-lookup"><span data-stu-id="31e4c-122">Application  ID of the application, as shown in the application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="31e4c-123">URL de inscrição do aplicativo onde os clientes vão para se inscrever e/ou comprar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="31e4c-123">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="31e4c-124">Escolha até três categorias em que seu aplicativo deva ser listado (para saber as categorias disponíveis, consulte o Azure Active Directory Marketplace):</span><span class="sxs-lookup"><span data-stu-id="31e4c-124">Choose up to three categories for your application to be listed under (for available categories see the Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="31e4c-125">Anexe o ícone pequeno do aplicativo (arquivo PNG, 45px por 45px, cor de plano de fundo sólida):</span><span class="sxs-lookup"><span data-stu-id="31e4c-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="31e4c-126">Anexe o ícone grande do aplicativo (arquivo PNG, 215px por 215px, cor de plano de fundo transparente):</span><span class="sxs-lookup"><span data-stu-id="31e4c-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="31e4c-127">Anexe o logotipo do aplicativo (arquivo PNG, 150px por 122px, cor de plano de fundo transparente):</span><span class="sxs-lookup"><span data-stu-id="31e4c-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="31e4c-128">Integração SAML</span><span class="sxs-lookup"><span data-stu-id="31e4c-128">SAML Integration</span></span>
<span data-ttu-id="31e4c-129">Qualquer aplicativo que dê suporte ao SAML 2.0 pode ser integrado diretamente a um locatário do AD do Azure usando [estas instruções para adicionar um aplicativo personalizado](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="31e4c-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions to add a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="31e4c-130">Depois de testar se a integração do aplicativo funciona com o AD do Azure, envie as informações a seguir para <mailto:waadpartners@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="31e4c-130">Once you have tested that your application integration works with Azure AD, send the following information to <mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="31e4c-131">Fornece credenciais para uma conta ou locatário de teste com o aplicativo que pode ser usado pela equipe do Azure AD para testar a integração.</span><span class="sxs-lookup"><span data-stu-id="31e4c-131">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="31e4c-132">Forneça os valores da URL de logon do SAML, da URL de emissor (ID da entidade) e da URL de resposta (serviço do consumidor de declaração) para seu aplicativo, conforme descrito [aqui](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="31e4c-132">Provide the SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="31e4c-133">Se você geralmente fornece esses valores como parte de um arquivo de metadados do SAML, envie este também.</span><span class="sxs-lookup"><span data-stu-id="31e4c-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="31e4c-134">Forneça uma breve descrição de como configurar o AD do Azure como um provedor de identidade em seu aplicativo usando o SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="31e4c-134">Provide a brief description of how to configure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="31e4c-135">Se seu aplicativo der suporte à configuração do AD do Azure como um provedor de identidade por meio de um portal administrativo de autoatendimento, verifique se as credenciais fornecidas acima incluem a capacidade de configurá-la.</span><span class="sxs-lookup"><span data-stu-id="31e4c-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure the credentials provided above include the ability to set this up.</span></span>
* <span data-ttu-id="31e4c-136">Forneça as informações abaixo:</span><span class="sxs-lookup"><span data-stu-id="31e4c-136">Provide the info below:</span></span>

> <span data-ttu-id="31e4c-137">Nome da empresa:</span><span class="sxs-lookup"><span data-stu-id="31e4c-137">Company Name:</span></span>
> 
> <span data-ttu-id="31e4c-138">Site da empresa:</span><span class="sxs-lookup"><span data-stu-id="31e4c-138">Company Website:</span></span>
> 
> <span data-ttu-id="31e4c-139">Nome do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="31e4c-139">Application Name:</span></span>
> 
> <span data-ttu-id="31e4c-140">Descrição do aplicativo (limite de 200 caracteres):</span><span class="sxs-lookup"><span data-stu-id="31e4c-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="31e4c-141">Site do aplicativo (informativo):</span><span class="sxs-lookup"><span data-stu-id="31e4c-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="31e4c-142">Site de suporte técnico do aplicativo ou informações de contato:</span><span class="sxs-lookup"><span data-stu-id="31e4c-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="31e4c-143">URL de inscrição do aplicativo onde os clientes vão para se inscrever e/ou comprar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="31e4c-143">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="31e4c-144">Escolha até três categorias em que seu aplicativo deva ser listado (para saber as categorias disponíveis, consulte o [Marketplace do Active Directory do Azure](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="31e4c-144">Choose up to three categories for your application to be listed under (for available categories see the [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="31e4c-145">Anexe o ícone pequeno do aplicativo (arquivo PNG, 45px por 45px, cor de plano de fundo sólida):</span><span class="sxs-lookup"><span data-stu-id="31e4c-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="31e4c-146">Anexe o ícone grande do aplicativo (arquivo PNG, 215px por 215px, cor de plano de fundo transparente):</span><span class="sxs-lookup"><span data-stu-id="31e4c-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="31e4c-147">Anexe o logotipo do aplicativo (arquivo PNG, 150px por 122px, cor de plano de fundo transparente):</span><span class="sxs-lookup"><span data-stu-id="31e4c-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

