---
title: "Grupos dinâmicos e Colaboração do Azure Active Directory B2B | Microsoft Docs"
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
ms.openlocfilehash: 5818c41610c8c5df89abcb0dcd058bcbe9579ce7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="d7ad1-103">Grupos dinâmicos e Colaboração do Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="d7ad1-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="d7ad1-104">O que são grupos dinâmicos?</span><span class="sxs-lookup"><span data-stu-id="d7ad1-104">What are dynamic groups?</span></span>
<span data-ttu-id="d7ad1-105">A configuração dinâmica da associação de grupo de segurança para o Azure AD (Azure Active Directory) está disponível [no portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d7ad1-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [the Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d7ad1-106">Os administradores podem definir regras para preencher os grupos criados no Azure Active Directory com base nos atributos do usuário (como userType, departamento ou país).</span><span class="sxs-lookup"><span data-stu-id="d7ad1-106">Administrators can set rules to populate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="d7ad1-107">Os membros podem ser adicionados ou removidos automaticamente de um grupo de segurança com base nas alterações de seus atributos.</span><span class="sxs-lookup"><span data-stu-id="d7ad1-107">Members can be automatically added to or removed from a security group based on their attributes.</span></span> <span data-ttu-id="d7ad1-108">Esses grupos podem fornecer acesso a aplicativos ou a recursos de nuvem (como sites e documentos do SharePoint) e para atribuir licenças a membros.</span><span class="sxs-lookup"><span data-stu-id="d7ad1-108">These groups can provide access to applications or cloud resources (SharePoint sites, documents) and to assign licenses to members.</span></span> <span data-ttu-id="d7ad1-109">Leia mais sobre grupos dinâmicos em [Grupos dedicados no Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="d7ad1-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="d7ad1-110">O [licenciamento do Azure AD Premium P1 ou P2](https://azure.microsoft.com/pricing/details/active-directory/) apropriado é necessário para criar e usar grupos dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="d7ad1-110">The appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required to create and use dynamic groups.</span></span> <span data-ttu-id="d7ad1-111">Saiba mais no artigo [Criar regras baseadas em atributo para associação dinâmica de grupo no Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d7ad1-111">Learn more in the article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-the-built-in-dynamic-groups"></a><span data-ttu-id="d7ad1-112">O que são os grupos dinâmicos internos?</span><span class="sxs-lookup"><span data-stu-id="d7ad1-112">What are the built-in dynamic groups?</span></span>
<span data-ttu-id="d7ad1-113">O grupo dinâmico **Todos os usuários**permite que administradores de locatário criem um grupo contendo todos os usuários no locatário com um único clique.</span><span class="sxs-lookup"><span data-stu-id="d7ad1-113">The **All users** dynamic group enables tenant admins to create a group containing all users in the tenant with a single click.</span></span> <span data-ttu-id="d7ad1-114">Por padrão, o grupo **Todos os usuários** inclui todos os usuários no diretório, incluindo Membros e Convidados.</span><span class="sxs-lookup"><span data-stu-id="d7ad1-114">By default, the **All users** group includes all users in the directory, including Members and Guests.</span></span>
<span data-ttu-id="d7ad1-115">No novo portal de administração do Azure Active Directory, você pode optar por habilitar o grupo **Todos os usuários** na exibição Configurações de Grupo.</span><span class="sxs-lookup"><span data-stu-id="d7ad1-115">Within the new Azure Active Directory admin portal, you can choose to enable the **All users** group in the Group Settings view.</span></span>

![grupos internos](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-the-all-users-dynamic-group"></a><span data-ttu-id="d7ad1-117">Fortalecendo a proteção do grupo dinâmico Todos os usuários</span><span class="sxs-lookup"><span data-stu-id="d7ad1-117">Hardening the All users dynamic group</span></span>
<span data-ttu-id="d7ad1-118">Por padrão, o grupo **Todos os usuários** também contém os usuários de colaboração B2B (convidados).</span><span class="sxs-lookup"><span data-stu-id="d7ad1-118">By default, the **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="d7ad1-119">Você pode proteger ainda mais o grupo **Todos os usuários** usando uma regra para remover os usuários convidados.</span><span class="sxs-lookup"><span data-stu-id="d7ad1-119">You can further secure your **All users** group by using a rule to remove guest users.</span></span> <span data-ttu-id="d7ad1-120">A ilustração a seguir mostra o grupo **Todos os usuários** modificado para excluir os convidados.</span><span class="sxs-lookup"><span data-stu-id="d7ad1-120">The following illustration shows the **All users** group modified to exclude guests.</span></span>

![habilitar o grupo todos os usuários](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="d7ad1-122">Também pode ser útil criar um novo grupo dinâmico que contenha apenas os usuários convidados, para que você possa aplicar políticas (como as políticas de acesso condicional do Azure AD) a eles.</span><span class="sxs-lookup"><span data-stu-id="d7ad1-122">You might also find it useful to create a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) to them.</span></span>
<span data-ttu-id="d7ad1-123">Como esse grupo poderia ser:</span><span class="sxs-lookup"><span data-stu-id="d7ad1-123">What such a group might look like:</span></span>

![excluir usuários convidados](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="d7ad1-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d7ad1-125">Next steps</span></span>

<span data-ttu-id="d7ad1-126">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="d7ad1-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="d7ad1-127">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="d7ad1-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="d7ad1-128">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d7ad1-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="d7ad1-129">Como adicionar um usuário de colaboração B2B a uma função</span><span class="sxs-lookup"><span data-stu-id="d7ad1-129">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="d7ad1-130">Delegação de convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d7ad1-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="d7ad1-131">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7ad1-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="d7ad1-132">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d7ad1-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="d7ad1-133">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d7ad1-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="d7ad1-134">Mapeamento de declarações de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d7ad1-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="d7ad1-135">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="d7ad1-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="d7ad1-136">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d7ad1-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
