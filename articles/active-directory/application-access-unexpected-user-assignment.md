---
title: "Como atribuir usuários a aplicativos | Microsoft Docs"
description: "Compreenda como os usuários são atribuídos a um aplicativo em seu locatário"
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
ms.openlocfilehash: 916238ba402a2555bac620d7f08e02799d981ae0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-to-applications"></a><span data-ttu-id="da516-103">Como atribuir usuários a aplicativos</span><span class="sxs-lookup"><span data-stu-id="da516-103">How to assign users to applications</span></span>

<span data-ttu-id="da516-104">Este artigo o ajudará a compreender como usuários são atribuídos a um aplicativo em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="da516-104">This article help you to understand how users get assigned to an application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a><span data-ttu-id="da516-105">Como os usuários são atribuídos a um aplicativo no Azure AD?</span><span class="sxs-lookup"><span data-stu-id="da516-105">How do users get assigned to an application in Azure AD?</span></span>

<span data-ttu-id="da516-106">Para acessar um aplicativo, o usuário precisa primeiro ser atribuído a ele de alguma forma.</span><span class="sxs-lookup"><span data-stu-id="da516-106">For a user to access an application, they must first be assigned to it in some way.</span></span> <span data-ttu-id="da516-107">A atribuição pode ser feita por um administrador, um representante de negócios ou, às vezes, o próprio usuário.</span><span class="sxs-lookup"><span data-stu-id="da516-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span></span> <span data-ttu-id="da516-108">Abaixo, descrevemos as formas como os usuários podem ser atribuídos a aplicativos:</span><span class="sxs-lookup"><span data-stu-id="da516-108">Below describes the ways users can get assigned to applications:</span></span>

1.  <span data-ttu-id="da516-109">Um administrador [atribui um usuário](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) diretamente ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="da516-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span></span>

2.  <span data-ttu-id="da516-110">Um administrador [atribui um grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) do qual o usuário é membro ao aplicativo, incluindo:</span><span class="sxs-lookup"><span data-stu-id="da516-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span></span>

  * <span data-ttu-id="da516-111">Um grupo que foi sincronizado do local</span><span class="sxs-lookup"><span data-stu-id="da516-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="da516-112">Um grupo de segurança estático criado na nuvem</span><span class="sxs-lookup"><span data-stu-id="da516-112">A static security group created in the cloud</span></span>

  * <span data-ttu-id="da516-113">Um [grupo de segurança dinâmico](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) criado na nuvem</span><span class="sxs-lookup"><span data-stu-id="da516-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span></span>

  * <span data-ttu-id="da516-114">Um grupo do Office 365 criado na nuvem</span><span class="sxs-lookup"><span data-stu-id="da516-114">An Office 365 group created in the cloud</span></span>

  * <span data-ttu-id="da516-115">O grupo [Todos os Usuários](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups)</span><span class="sxs-lookup"><span data-stu-id="da516-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="da516-116">Um administrador habilita o [Acesso de aplicativo de autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) para permitir que um usuário adicione um aplicativo usando o recurso [Adicionar Aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) do **Painel de Acesso do Aplicativo** **sem aprovação de negócios**</span><span class="sxs-lookup"><span data-stu-id="da516-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="da516-117">Um administrador habilita o [Acesso de aplicativo de autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) para permitir que um usuário adicione um aplicativo usando o recurso [Adicionar Aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) do **Painel de Acesso do Aplicativo**, mas apenas **com aprovação anterior de um conjunto selecionado de aprovadores de negócios**</span><span class="sxs-lookup"><span data-stu-id="da516-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="da516-118">Um administrador habilita o [Gerenciamento de Grupo de Autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) para permitir que um usuário ingresse em um grupo a que um aplicativo está atribuído **sem aprovação de negócios**</span><span class="sxs-lookup"><span data-stu-id="da516-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span></span>

6.  <span data-ttu-id="da516-119">Um administrador habilita o [Gerenciamento de Grupo de Autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) para permitir que um usuário ingresse em um grupo a que um aplicativo está atribuído, mas apenas **com aprovação anterior de um conjunto selecionado de aprovadores de negócios**</span><span class="sxs-lookup"><span data-stu-id="da516-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="da516-120">Um administrador atribui uma licença diretamente a um usuário para um aplicativo interno, como o [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="da516-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="da516-121">Um administrador atribui uma licença a um grupo do qual o usuário é membro para um aplicativo interno, como o [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="da516-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="da516-122">Um [administrador dá consentimento para um aplicativo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) ser usado por todos os usuários e, em seguida, um usuário entra no aplicativo</span><span class="sxs-lookup"><span data-stu-id="da516-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span></span>

10. <span data-ttu-id="da516-123">O próprio usuário [dá consentimento para um aplicativo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) entrando no aplicativo</span><span class="sxs-lookup"><span data-stu-id="da516-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span></span>

## <a name="next-steps"></a><span data-ttu-id="da516-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="da516-124">Next steps</span></span>
[<span data-ttu-id="da516-125">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da516-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
