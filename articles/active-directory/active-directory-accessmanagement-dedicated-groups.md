---
title: grupos de aaaDedicated no Active Directory do Azure | Microsoft Docs
description: "Visão geral do funcionamento e da criação de grupos dedicados no Active Directory do Azure."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="ab418-103">Grupos dedicados no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ab418-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="ab418-104">No Azure Active Directory (AD do Azure), o recurso de grupos dedicados Olá automaticamente cria e preenche a associação de grupos predefinido do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab418-104">In Azure Active Directory (Azure AD), hello dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="ab418-105">Membros de grupos dedicados não podem ser adicionados ou removido usando hello Azure clássico portal, cmdlets do Windows PowerShell, ou programaticamente.</span><span class="sxs-lookup"><span data-stu-id="ab418-105">Members of dedicated groups cannot be added or removed using hello Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="ab418-106">Grupos dedicados requerem que uma licença do Azure AD Premium seja atribuída ao</span><span class="sxs-lookup"><span data-stu-id="ab418-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="ab418-107">administrador de saudação que gerencia a regra Olá em um grupo</span><span class="sxs-lookup"><span data-stu-id="ab418-107">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="ab418-108">todos os usuários que são selecionados por Olá toobe um membro do grupo de saudação de regra</span><span class="sxs-lookup"><span data-stu-id="ab418-108">all users who are selected by hello rule toobe a member of hello group</span></span>
>
>

<span data-ttu-id="ab418-109">**grupos de tooenable dedicado**</span><span class="sxs-lookup"><span data-stu-id="ab418-109">**tooenable dedicated groups**</span></span>

1. <span data-ttu-id="ab418-110">Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e, em seguida, abra o diretório da sua organização.</span><span class="sxs-lookup"><span data-stu-id="ab418-110">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="ab418-111">Selecione Olá **grupos** guia e grupo hello, em seguida, abra tooedit desejado.</span><span class="sxs-lookup"><span data-stu-id="ab418-111">Select hello **Groups** tab, and then open hello group you want tooedit.</span></span>
3. <span data-ttu-id="ab418-112">Selecione Olá **configurar** guia e, em seguida, defina **habilitar grupos dedicados** muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="ab418-112">Select hello **Configure** tab, and then set **Enable Dedicated Groups** too**Yes**.</span></span>

<span data-ttu-id="ab418-113">Depois de saudação alternar habilitar grupos dedicados está definida muito**Sim**, você pode habilitar Olá diretório tooautomatically criar grupo dedicado de todos os usuários de saudação por configuração Olá **habilitar "Todos os usuários" grupo** Alternar muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="ab418-113">Once hello Enable Dedicated Groups switch is set too**Yes**, you can further enable hello directory tooautomatically create hello All Users dedicated group by setting hello **Enable “All Users” Group** switch too**Yes**.</span></span> <span data-ttu-id="ab418-114">Você pode também editar nome hello desse grupo dedicado digitando-o em hello **nome para exibição para "Todos os usuários" grupo** campo.</span><span class="sxs-lookup"><span data-stu-id="ab418-114">You can then also edit hello name of this dedicated group by typing it in hello **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="ab418-115">grupo de todos os usuários Olá pode ser usado tooassign Olá mesmo permissões tooall Olá os usuários em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="ab418-115">hello All Users group can be used tooassign hello same permissions tooall hello users in your directory.</span></span> <span data-ttu-id="ab418-116">Por exemplo, você pode conceder a todos os usuários no seu acesso de diretório tooa aplicativo SaaS, atribuindo acesso Olá grupo dedicado de todos os usuários toothis de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab418-116">For example, you can grant all users in your directory access tooa SaaS application by assigning access for hello All Users dedicated group toothis application.</span></span>

<span data-ttu-id="ab418-117">grupo de todos os usuários Olá dedicado inclui todos os usuários no diretório hello, inclusive convidados e usuários externos.</span><span class="sxs-lookup"><span data-stu-id="ab418-117">hello dedicated All Users group includes all users in hello directory, including guests and external users.</span></span> <span data-ttu-id="ab418-118">Se você precisar de um grupo que exclui os usuários externos, você pode fazer isso criando um grupo com uma regra dinâmica baseada em atributo como seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="ab418-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as hello following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="ab418-119">Para um grupo que exclui todos os convidados, use uma regra, como a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="ab418-119">For a group that excludes all Guests, use a rule such as hello following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="ab418-120">toolearn sobre como toocreate *avançados* regra (regras que podem conter várias comparações) para a associação de grupo dinâmico, consulte [usar atributos toocreate regras avançadas](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="ab418-120">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="ab418-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab418-121">Next steps</span></span>
<span data-ttu-id="ab418-122">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab418-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="ab418-123">Gerenciando acesso tooresources com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ab418-123">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="ab418-124">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ab418-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="ab418-125">O que é o Active Directory do Azure?</span><span class="sxs-lookup"><span data-stu-id="ab418-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="ab418-126">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ab418-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
