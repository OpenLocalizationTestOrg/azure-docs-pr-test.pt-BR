---
title: "aaaHow tooAssign usuários tooapplications | Microsoft Docs"
description: "Entender como os usuários são atribuídos tooan aplicativo em seu locatário"
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
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a><span data-ttu-id="37590-103">Como tooassign usuários tooapplications</span><span class="sxs-lookup"><span data-stu-id="37590-103">How tooassign users tooapplications</span></span>

<span data-ttu-id="37590-104">Este artigo ajuda toounderstand como os usuários são atribuídos tooan aplicativo em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="37590-104">This article help you toounderstand how users get assigned tooan application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a><span data-ttu-id="37590-105">Como os usuários recebem tooan aplicativo no Azure AD?</span><span class="sxs-lookup"><span data-stu-id="37590-105">How do users get assigned tooan application in Azure AD?</span></span>

<span data-ttu-id="37590-106">Para um usuário tooaccess um aplicativo, ele devem ser atribuídos primeiro tooit de alguma forma.</span><span class="sxs-lookup"><span data-stu-id="37590-106">For a user tooaccess an application, they must first be assigned tooit in some way.</span></span> <span data-ttu-id="37590-107">Atribuição pode ser executada por um administrador, um representante de negócios ou às vezes, Olá usuário próprios.</span><span class="sxs-lookup"><span data-stu-id="37590-107">Assignment can be performed by an administrator, a business delegate, or sometimes, hello user themselves.</span></span> <span data-ttu-id="37590-108">Abaixo descreve maneiras de saudação podem ser atribuídos a usuários tooapplications:</span><span class="sxs-lookup"><span data-stu-id="37590-108">Below describes hello ways users can get assigned tooapplications:</span></span>

1.  <span data-ttu-id="37590-109">Um administrador [atribui um usuário](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello aplicativo diretamente</span><span class="sxs-lookup"><span data-stu-id="37590-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello application directly</span></span>

2.  <span data-ttu-id="37590-110">Um administrador [atribui a um grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) usuário Olá é um membro do aplicativo toohello, incluindo:</span><span class="sxs-lookup"><span data-stu-id="37590-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that hello user is a member of toohello application, including:</span></span>

  * <span data-ttu-id="37590-111">Um grupo que foi sincronizado do local</span><span class="sxs-lookup"><span data-stu-id="37590-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="37590-112">Um grupo de segurança estático criado na nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="37590-112">A static security group created in hello cloud</span></span>

  * <span data-ttu-id="37590-113">Um [o grupo de segurança dinâmica](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) criadas na nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="37590-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in hello cloud</span></span>

  * <span data-ttu-id="37590-114">Um grupo do Office 365 criado na nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="37590-114">An Office 365 group created in hello cloud</span></span>

  * <span data-ttu-id="37590-115">Olá [todos os usuários](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) grupo</span><span class="sxs-lookup"><span data-stu-id="37590-115">hello [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="37590-116">Um administrador habilita [autoatendimento acesso ao aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow um tooadd de usuário usando um aplicativo hello [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Adicionar aplicativo** recurso **sem a aprovação de negócios**</span><span class="sxs-lookup"><span data-stu-id="37590-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="37590-117">Um administrador habilita [autoatendimento acesso ao aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow um tooadd de usuário usando um aplicativo hello [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Adicionar aplicativo** recurso, mas somente w **i aprovação de um conjunto selecionado de aprovadores de negócios**</span><span class="sxs-lookup"><span data-stu-id="37590-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="37590-118">Um administrador habilita [gerenciamento de grupo de autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin um usuário um grupo de um aplicativo atribuído muito**sem a aprovação de negócios**</span><span class="sxs-lookup"><span data-stu-id="37590-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned too**without business approval**</span></span>

6.  <span data-ttu-id="37590-119">Um administrador habilita [gerenciamento de grupo de autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin um usuário um grupo de um aplicativo atribuído ao, mas apenas **com aprovação de um conjunto selecionado de aprovadores de negócios**</span><span class="sxs-lookup"><span data-stu-id="37590-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="37590-120">Um administrador atribui um licença tooa usuário diretamente um primeiro aplicativo de terceiros, como [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="37590-120">An administrator assigns a license tooa user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="37590-121">Um administrador atribui um grupo de tooa de licença que Olá usuário é um membro do primeiro aplicativo de parte tooa, como [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="37590-121">An administrator assigns a license tooa group that hello user is a member of tooa first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="37590-122">Um [consentimento do administrador do aplicativo tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe usado por todos os usuários e, em seguida, um usuário entra no aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="37590-122">An [administrator consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe used by all users and then a user signs in toohello application</span></span>

10. <span data-ttu-id="37590-123">Um usuário [consentir aplicativos tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) próprios entrando no aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="37590-123">A user [consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in toohello application</span></span>

## <a name="next-steps"></a><span data-ttu-id="37590-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37590-124">Next steps</span></span>
[<span data-ttu-id="37590-125">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37590-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
