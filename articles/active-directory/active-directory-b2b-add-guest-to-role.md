---
title: "Adicionar um usuário de colaboração B2B do Azure Active Directory a uma função | Microsoft Docs"
description: "Adicionar um usuário convidado a uma função no Azure Active Directory"
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
ms.openlocfilehash: e816349ea971c997f655b4d51672dba666bc3e89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permissions-to-users-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="827d6-103">Conceder permissões a usuários de organizações parceiras em seu locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="827d6-103">Grant permissions to users from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="827d6-104">Os usuários da colaboração B2B do Azure AD (Azure Active Directory) são adicionados como usuários convidados ao diretório e as permissões de convidado no diretório são restritas por padrão.</span><span class="sxs-lookup"><span data-stu-id="827d6-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users to the directory, and guest permissions in the directory are restricted by default.</span></span> <span data-ttu-id="827d6-105">Sua empresa pode precisar de alguns usuários convidados para preencher as funções de privilégio mais elevado na organização.</span><span class="sxs-lookup"><span data-stu-id="827d6-105">Your business may need some guest users to fill higher-privilege roles in your organization.</span></span> <span data-ttu-id="827d6-106">Para dar suporte à definição de funções de privilégio mais elevado, os usuários convidados podem ser adicionados às funções desejadas, de acordo com as necessidades de sua organização.</span><span class="sxs-lookup"><span data-stu-id="827d6-106">To support defining higher-privilege roles, guest users can be added to any roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="827d6-107">Função padrão</span><span class="sxs-lookup"><span data-stu-id="827d6-107">Default role</span></span>

![função padrão](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="827d6-109">Função Administrador Global</span><span class="sxs-lookup"><span data-stu-id="827d6-109">Global Administrator Role</span></span>

![função administrador global](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="827d6-111">Função Administrador Limitado</span><span class="sxs-lookup"><span data-stu-id="827d6-111">Limited Administrator Role</span></span>

![função administrador limitado](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="827d6-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="827d6-113">Next steps</span></span>

<span data-ttu-id="827d6-114">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="827d6-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="827d6-115">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="827d6-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="827d6-116">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="827d6-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="827d6-117">Delegar convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="827d6-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="827d6-118">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="827d6-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="827d6-119">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="827d6-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="827d6-120">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="827d6-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="827d6-121">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="827d6-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="827d6-122">Mapeamento de declarações de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="827d6-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="827d6-123">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="827d6-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="827d6-124">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="827d6-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
