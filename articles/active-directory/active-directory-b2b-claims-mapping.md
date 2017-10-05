---
title: "Mapeamento de declarações de usuário de colaboração B2B no Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: 5f8559450b24effd40a38879aeae3a8dd03944a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="c4818-103">Mapeamento de declarações de usuário de colaboração B2B no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4818-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="c4818-104">O Azure AD (Azure Active Directory) dá suporte à personalização das declarações emitidas no token SAML para usuários da colaboração B2B.</span><span class="sxs-lookup"><span data-stu-id="c4818-104">Azure Active Directory (Azure AD) supports customizing the claims issued in the SAML token for B2B collaboration users.</span></span> <span data-ttu-id="c4818-105">Quando um usuário é autenticado no aplicativo, o Azure AD emite um token SAML para o aplicativo que contém informações (ou declarações) sobre o usuário que o identifica com exclusividade.</span><span class="sxs-lookup"><span data-stu-id="c4818-105">When a user authenticates to the application, Azure AD issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span></span> <span data-ttu-id="c4818-106">Por padrão, isso inclui o nome de usuário, o endereço de email, o nome e sobrenome do usuário.</span><span class="sxs-lookup"><span data-stu-id="c4818-106">By default, this includes the user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="c4818-107">Você pode exibir ou editar as declarações enviadas no token SAML para o aplicativo na guia Atributos.</span><span class="sxs-lookup"><span data-stu-id="c4818-107">You can view or edit the claims sent in the SAML token to the application under the Attributes tab.</span></span>

<span data-ttu-id="c4818-108">Há dois possíveis motivos para você precisar editar as declarações emitidas no token SAML.</span><span class="sxs-lookup"><span data-stu-id="c4818-108">There are two possible reasons why you might need to edit the claims issued in the SAML token.</span></span>

1. <span data-ttu-id="c4818-109">O aplicativo foi escrito para exigir um conjunto diferente de URIs de declaração ou valores de declaração</span><span class="sxs-lookup"><span data-stu-id="c4818-109">The application has been written to require a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="c4818-110">O aplicativo exige que a declaração NameIdentifier seja algo diferente do nome UPN armazenado no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c4818-110">Your application requires the NameIdentifier claim to be something other than the user principal name stored in Azure Active Directory.</span></span>

  ![exibir declarações no token SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="c4818-112">Para obter mais informações sobre como adicionar e editar declarações, confira este artigo sobre personalização de declarações, [Personalizando declarações emitidas no token SAML para aplicativos pré-integrados no Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="c4818-112">For information on how to add and edit claims, check out this article on claims customization, [Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="c4818-113">Para usuários da colaboração B2B, o mapeamento de NameID e UPN entre locatários é impedido, por motivos de segurança.</span><span class="sxs-lookup"><span data-stu-id="c4818-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c4818-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4818-114">Next steps</span></span>

<span data-ttu-id="c4818-115">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="c4818-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c4818-116">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="c4818-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c4818-117">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="c4818-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="c4818-118">Adicionar um usuário de colaboração B2B a uma função</span><span class="sxs-lookup"><span data-stu-id="c4818-118">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="c4818-119">Delegar convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="c4818-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="c4818-120">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="c4818-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="c4818-121">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4818-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="c4818-122">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="c4818-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="c4818-123">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="c4818-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="c4818-124">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="c4818-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="c4818-125">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="c4818-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
