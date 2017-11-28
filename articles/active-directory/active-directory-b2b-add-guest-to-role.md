---
title: "função de tooa de usuário de colaboração aaaAdd um B2B do Azure Active Directory | Microsoft Docs"
description: "Adicionar uma função de tooa de usuário convidado no Active Directory do Azure"
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
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ccc58a0c8ecc73f8e79a8d827efdc0ff93846a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permissions-toousers-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="4d95c-103">Conceder permissões toousers de organizações parceiras no seu locatário do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4d95c-103">Grant permissions toousers from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="4d95c-104">Usuários de colaboração B2B do Active Directory (AD do Azure) do Azure são adicionados como diretório de toohello convidado usuários e permissões de convidado no diretório de saudação são restritos por padrão.</span><span class="sxs-lookup"><span data-stu-id="4d95c-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users toohello directory, and guest permissions in hello directory are restricted by default.</span></span> <span data-ttu-id="4d95c-105">Sua empresa pode ser necessário algumas funções de privilégio mais alto do convidado usuários toofill em sua organização.</span><span class="sxs-lookup"><span data-stu-id="4d95c-105">Your business may need some guest users toofill higher-privilege roles in your organization.</span></span> <span data-ttu-id="4d95c-106">toosupport definir funções de privilégio mais alto, os usuários convidados podem ser funções tooany adicionado desejada, com base nas necessidades da sua organização.</span><span class="sxs-lookup"><span data-stu-id="4d95c-106">toosupport defining higher-privilege roles, guest users can be added tooany roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="4d95c-107">Função padrão</span><span class="sxs-lookup"><span data-stu-id="4d95c-107">Default role</span></span>

![função padrão](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="4d95c-109">Função Administrador Global</span><span class="sxs-lookup"><span data-stu-id="4d95c-109">Global Administrator Role</span></span>

![função administrador global](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="4d95c-111">Função Administrador Limitado</span><span class="sxs-lookup"><span data-stu-id="4d95c-111">Limited Administrator Role</span></span>

![função administrador limitado](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="4d95c-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4d95c-113">Next steps</span></span>

<span data-ttu-id="4d95c-114">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="4d95c-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="4d95c-115">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="4d95c-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="4d95c-116">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4d95c-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="4d95c-117">Delegar convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4d95c-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="4d95c-118">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4d95c-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="4d95c-119">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d95c-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="4d95c-120">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4d95c-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="4d95c-121">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4d95c-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="4d95c-122">Mapeamento de declarações de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4d95c-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="4d95c-123">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="4d95c-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="4d95c-124">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4d95c-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
