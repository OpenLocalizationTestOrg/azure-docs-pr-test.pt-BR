---
title: "aaaDynamic grupos e colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "A colaboração B2B do Azure Active Directory pode ser usada com grupos dinâmicos do Azure AD"
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="ba2ee-103">Grupos dinâmicos e Colaboração do Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="ba2ee-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="ba2ee-104">O que são grupos dinâmicos?</span><span class="sxs-lookup"><span data-stu-id="ba2ee-104">What are dynamic groups?</span></span>
<span data-ttu-id="ba2ee-105">Configuração dinâmica de associação de grupo de segurança do Azure Active Directory (AD do Azure) está disponível em [Olá portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba2ee-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [hello Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ba2ee-106">Os administradores podem definir regras toopopulate grupos são criados no Active Directory do Azure com base em atributos de usuário (como userType, departamento ou país).</span><span class="sxs-lookup"><span data-stu-id="ba2ee-106">Administrators can set rules toopopulate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="ba2ee-107">Membros podem ser adicionados automaticamente tooor removido de um grupo de segurança com base em seus atributos.</span><span class="sxs-lookup"><span data-stu-id="ba2ee-107">Members can be automatically added tooor removed from a security group based on their attributes.</span></span> <span data-ttu-id="ba2ee-108">Esses grupos podem fornecer acesso a recursos de nuvem ou tooapplications (sites do SharePoint, documentos) e tooassign toomembers de licenças.</span><span class="sxs-lookup"><span data-stu-id="ba2ee-108">These groups can provide access tooapplications or cloud resources (SharePoint sites, documents) and tooassign licenses toomembers.</span></span> <span data-ttu-id="ba2ee-109">Leia mais sobre grupos dinâmicos em [Grupos dedicados no Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="ba2ee-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="ba2ee-110">Olá apropriado [licenciamento do Azure AD Premium P1 ou P2](https://azure.microsoft.com/pricing/details/active-directory/) é necessário toocreate e use grupos dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="ba2ee-110">hello appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required toocreate and use dynamic groups.</span></span> <span data-ttu-id="ba2ee-111">Saiba mais no artigo Olá [criar regras com base em atributo para associação de grupo dinâmico no Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ba2ee-111">Learn more in hello article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-hello-built-in-dynamic-groups"></a><span data-ttu-id="ba2ee-112">Quais são os grupos internos de dinâmico Olá?</span><span class="sxs-lookup"><span data-stu-id="ba2ee-112">What are hello built-in dynamic groups?</span></span>
<span data-ttu-id="ba2ee-113">Olá **todos os usuários** grupo dinâmico permite toocreate de administradores de inquilinos um grupo contendo todos os usuários no locatário Olá com um único clique.</span><span class="sxs-lookup"><span data-stu-id="ba2ee-113">hello **All users** dynamic group enables tenant admins toocreate a group containing all users in hello tenant with a single click.</span></span> <span data-ttu-id="ba2ee-114">Por padrão, Olá **todos os usuários** grupo inclui todos os usuários no diretório hello, incluindo membros e convidados.</span><span class="sxs-lookup"><span data-stu-id="ba2ee-114">By default, hello **All users** group includes all users in hello directory, including Members and Guests.</span></span>
<span data-ttu-id="ba2ee-115">No portal de administração do Active Directory do Azure nova hello, você pode escolher Olá tooenable **todos os usuários** grupo Olá exibir configurações de grupo.</span><span class="sxs-lookup"><span data-stu-id="ba2ee-115">Within hello new Azure Active Directory admin portal, you can choose tooenable hello **All users** group in hello Group Settings view.</span></span>

![grupos internos](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a><span data-ttu-id="ba2ee-117">Proteção Olá grupo dinâmico de todos os usuários</span><span class="sxs-lookup"><span data-stu-id="ba2ee-117">Hardening hello All users dynamic group</span></span>
<span data-ttu-id="ba2ee-118">Por padrão, Olá **todos os usuários** grupo contém os usuários de colaboração (convidado) B2B também.</span><span class="sxs-lookup"><span data-stu-id="ba2ee-118">By default, hello **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="ba2ee-119">Você pode proteger ainda mais seu **todos os usuários** grupo usando usuários de convidado de tooremove uma regra.</span><span class="sxs-lookup"><span data-stu-id="ba2ee-119">You can further secure your **All users** group by using a rule tooremove guest users.</span></span> <span data-ttu-id="ba2ee-120">Olá, ilustração a seguir mostra Olá **todos os usuários** grupo modificado tooexclude convidados.</span><span class="sxs-lookup"><span data-stu-id="ba2ee-120">hello following illustration shows hello **All users** group modified tooexclude guests.</span></span>

![habilitar o grupo todos os usuários](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="ba2ee-122">Talvez também seja útil toocreate um novo grupo dinâmico que contém apenas os usuários convidados, para que você possa aplicar políticas (como políticas de acesso condicional do Azure AD) toothem.</span><span class="sxs-lookup"><span data-stu-id="ba2ee-122">You might also find it useful toocreate a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) toothem.</span></span>
<span data-ttu-id="ba2ee-123">Como esse grupo poderia ser:</span><span class="sxs-lookup"><span data-stu-id="ba2ee-123">What such a group might look like:</span></span>

![excluir usuários convidados](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="ba2ee-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ba2ee-125">Next steps</span></span>

<span data-ttu-id="ba2ee-126">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="ba2ee-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="ba2ee-127">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="ba2ee-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="ba2ee-128">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="ba2ee-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="ba2ee-129">Adicionando uma função de tooa de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="ba2ee-129">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="ba2ee-130">Delegação de convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="ba2ee-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="ba2ee-131">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba2ee-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="ba2ee-132">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="ba2ee-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="ba2ee-133">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="ba2ee-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="ba2ee-134">Mapeamento de declarações de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="ba2ee-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="ba2ee-135">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="ba2ee-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="ba2ee-136">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="ba2ee-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
