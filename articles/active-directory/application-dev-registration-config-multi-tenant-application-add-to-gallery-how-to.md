---
title: "Como adicionar um aplicativo multilocatário à galeria de aplicativos do Azure AD | Microsoft Docs"
description: "Explica como listar seu aplicativo multilocatário personalizado na Galeria de Aplicativos do Azure AD"
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
ms.openlocfilehash: 208f0d40bd7a8e8f35f16e1fcb09c305d833dbb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-add-a-multi-tenant-application-to-the-azure-ad-application-gallery"></a><span data-ttu-id="d71bf-103">Como adicionar um aplicativo multilocatário à Galeria de Aplicativos do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d71bf-103">How to add a multi-tenant application to the Azure AD application gallery</span></span>

## <a name="what-is-the-azure-ad-application-gallery"></a><span data-ttu-id="d71bf-104">O que é a Galeria de Aplicativos do Azure AD?</span><span class="sxs-lookup"><span data-stu-id="d71bf-104">What is the Azure AD Application Gallery?</span></span>

<span data-ttu-id="d71bf-105">A Galeria de Aplicativos do Azure AD é uma ótima maneira de colocar seu aplicativo diante de milhões de clientes do Azure Active Directory para ampliar o impacto e o alcance do aplicativo no mercado.</span><span class="sxs-lookup"><span data-stu-id="d71bf-105">The Azure AD Application Gallery is a great way to get your application in front of all the millions of Azure Active Directory customers to broaden the impact and reach of your application in the marketplace.</span></span> <span data-ttu-id="d71bf-106">As etapas a seguir explicam como listar seu aplicativo na Galeria de Aplicativos do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d71bf-106">The below steps explain how you can list your application in the Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="d71bf-107">Se seu aplicativo der suporte a SAML ou OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="d71bf-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="d71bf-108">Se tiver um aplicativo multilocatário que queira listar na Galeria de Aplicativos do Azure AD, você precisa primeiro assegurar que seu aplicativo dê suporte a uma das seguintes tecnologias de logon único:</span><span class="sxs-lookup"><span data-stu-id="d71bf-108">If you have a multi-tenant application you'd like to list in the Azure AD Application Gallery, you must first make sure that your application supports one of the following single sign-on technologies:</span></span>

1. <span data-ttu-id="d71bf-109">**OpenID Connect** : integração direta com o Azure AD usando o OpenID Connect para autenticação e a API de consentimento do AD do Azure para configuração.</span><span class="sxs-lookup"><span data-stu-id="d71bf-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="d71bf-110">Se você estiver apenas começando uma integração e seu aplicativo não der suporte a SAML, esse é o modo recomendado.</span><span class="sxs-lookup"><span data-stu-id="d71bf-110">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
2. <span data-ttu-id="d71bf-111">**SAML** : seu aplicativo já tem a capacidade de configurar provedores de identidade de terceiros usando o protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="d71bf-111">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="d71bf-112">Se seu aplicativo der suporte a um desses modos de logon único e você quiser listar seu aplicativo multilocatário na Galeria de Aplicativos do Azure AD, siga as etapas no documento abaixo.</span><span class="sxs-lookup"><span data-stu-id="d71bf-112">If your application supports one of these single sign-on modes and you'd like to list your multi-tenant application in the Azure AD Application Gallery, you can follow the steps in the document below.</span></span> <span data-ttu-id="d71bf-113">Para iniciar rapidamente, envie um email para **waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="d71bf-113">To get started quickly send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="d71bf-114">Se seu aplicativo não der suporte a SAML ou OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="d71bf-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="d71bf-115">Mesmo que seu aplicativo não dê suporte a um desses modos, ainda assim podemos integrá-lo a nossa galeria usando nossa tecnologia de Logon único com senha.</span><span class="sxs-lookup"><span data-stu-id="d71bf-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="d71bf-116">Para explorar essa opção, envie um email para **waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="d71bf-116">If you'd like to explore this option, you can send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d71bf-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d71bf-117">Next steps</span></span>
[<span data-ttu-id="d71bf-118">Como listar seu aplicativo na galeria de aplicativos do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d71bf-118">How to list your application in the Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
