---
title: "declarações de usuário de colaboração de aaaB2B mapeamento no Active Directory do Azure | Microsoft Docs"
description: "referência ao mapeamento de declarações para colaboração B2B do Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="63d2b-103">Mapeamento de declarações de usuário de colaboração B2B no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63d2b-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="63d2b-104">Azure Active Directory (AD do Azure) é compatível com personalizando Olá declarações emitidas no token SAML Olá para usuários de colaboração B2B.</span><span class="sxs-lookup"><span data-stu-id="63d2b-104">Azure Active Directory (Azure AD) supports customizing hello claims issued in hello SAML token for B2B collaboration users.</span></span> <span data-ttu-id="63d2b-105">Quando um usuário se autentica toohello aplicativo, o Azure AD emite um aplicativo de toohello token SAML que contém informações (ou declarações) sobre o usuário Olá que identifica com exclusividade.</span><span class="sxs-lookup"><span data-stu-id="63d2b-105">When a user authenticates toohello application, Azure AD issues a SAML token toohello app that contains information (or claims) about hello user that uniquely identifies them.</span></span> <span data-ttu-id="63d2b-106">Por padrão, isso inclui o nome de usuário, endereço de email, nome e sobrenome do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="63d2b-106">By default, this includes hello user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="63d2b-107">Você pode exibir ou editar declarações Olá enviadas em Olá aplicativo de toohello token SAML no guia de atributos de saudação.</span><span class="sxs-lookup"><span data-stu-id="63d2b-107">You can view or edit hello claims sent in hello SAML token toohello application under hello Attributes tab.</span></span>

<span data-ttu-id="63d2b-108">Há dois motivos possíveis quais declarações de saudação tooedit emitidas no token SAML Olá pode ser necessário.</span><span class="sxs-lookup"><span data-stu-id="63d2b-108">There are two possible reasons why you might need tooedit hello claims issued in hello SAML token.</span></span>

1. <span data-ttu-id="63d2b-109">aplicativo Hello foi gravado toorequire outro conjunto de declaração URIs ou valores de declaração</span><span class="sxs-lookup"><span data-stu-id="63d2b-109">hello application has been written toorequire a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="63d2b-110">Seu aplicativo requer toobe de declaração NameIdentifier Olá algo diferente de nome principal do usuário Olá armazenado no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="63d2b-110">Your application requires hello NameIdentifier claim toobe something other than hello user principal name stored in Azure Active Directory.</span></span>

  ![exibir declarações no token SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="63d2b-112">Para obter informações sobre como tooadd e editar declarações, confira este artigo sobre a personalização de declarações, [personalizando declarações emitidas no token SAML Olá para aplicativos pré-integrados no Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="63d2b-112">For information on how tooadd and edit claims, check out this article on claims customization, [Customizing claims issued in hello SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="63d2b-113">Para usuários da colaboração B2B, o mapeamento de NameID e UPN entre locatários é impedido, por motivos de segurança.</span><span class="sxs-lookup"><span data-stu-id="63d2b-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="63d2b-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="63d2b-114">Next steps</span></span>

<span data-ttu-id="63d2b-115">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="63d2b-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="63d2b-116">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="63d2b-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="63d2b-117">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="63d2b-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="63d2b-118">Adicionando uma função de tooa de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="63d2b-118">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="63d2b-119">Delegar convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="63d2b-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="63d2b-120">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="63d2b-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="63d2b-121">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="63d2b-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="63d2b-122">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="63d2b-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="63d2b-123">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="63d2b-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="63d2b-124">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="63d2b-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="63d2b-125">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="63d2b-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
