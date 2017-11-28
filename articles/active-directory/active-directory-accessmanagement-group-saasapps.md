---
title: aaaUsing tooSaaS de acesso de toomanage um grupo aplicativos | Microsoft Docs
description: "Como os grupos de toouse no Azure Active Directory Premium ou básica tooassign acessar tooSaaS aplicativos integrados ao Active Directory do Azure."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a><span data-ttu-id="64ed0-103">Usando um grupo toomanage tooSaaS os aplicativos access</span><span class="sxs-lookup"><span data-stu-id="64ed0-103">Using a group toomanage access tooSaaS applications</span></span>
<span data-ttu-id="64ed0-104">Usando o Azure Active Directory (AD do Azure) com uma licença Azure AD Premium ou Azure AD Basic, você pode usar grupos tooassign acesso tooa aplicativo SaaS que esteja integrado ao AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="64ed0-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups tooassign access tooa SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="64ed0-105">Por exemplo, se você quiser acesso tooassign Olá marketing departamento toouse cinco aplicativos SaaS diferentes, você pode criar um grupo que contém usuários Olá no departamento de marketing Olá e, em seguida, atribuir esse grupo toothese cinco aplicativos SaaS que são necessárias pelo departamento de marketing hello.</span><span class="sxs-lookup"><span data-stu-id="64ed0-105">For example, if you want tooassign access for hello marketing department toouse five different SaaS applications, you can create a group that contains hello users in hello marketing department, and then assign that group toothese five SaaS applications that are needed by hello marketing department.</span></span> <span data-ttu-id="64ed0-106">Dessa forma você pode poupar tempo gerenciando participação Olá Olá marketing departamento em um único local.</span><span class="sxs-lookup"><span data-stu-id="64ed0-106">This way you can save time by managing hello membership of hello marketing department in one place.</span></span> <span data-ttu-id="64ed0-107">Em seguida, os usuários recebem toohello aplicativo quando eles são adicionados como membros do grupo marketing hello e sua atribuição é removida do aplicativo hello quando eles são removidos do grupo de marketing de saudação.</span><span class="sxs-lookup"><span data-stu-id="64ed0-107">Users then are assigned toohello application when they are added as members of hello marketing group, and have their assignments removed from hello application when they are removed from hello marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64ed0-108">A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="64ed0-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="64ed0-109">Esse recurso pode ser usado com centenas de aplicativos que você adiciona da Olá Galeria de aplicativos do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64ed0-109">This capability can be used with hundreds of applications that you can add from within hello Azure AD Application Gallery.</span></span>

<span data-ttu-id="64ed0-110">**acesso de tooassign para um grupo de tooa aplicativo SaaS**</span><span class="sxs-lookup"><span data-stu-id="64ed0-110">**tooassign access for a group tooa SaaS application**</span></span>

1. <span data-ttu-id="64ed0-111">Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory** na barra de navegação Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="64ed0-111">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on hello navigation bar on hello left hand side.</span></span>
2. <span data-ttu-id="64ed0-112">Selecione Olá **diretório** guia e diretório Olá aberto, em seguida, no qual você deseja acesso de tooassign para um grupo de tooa aplicativo SaaS.</span><span class="sxs-lookup"><span data-stu-id="64ed0-112">Select hello **Directory** tab, and then open hello directory in which you want tooassign access for a group tooa SaaS application.</span></span>
3. <span data-ttu-id="64ed0-113">Selecione Olá **aplicativos** guia. Selecione um aplicativo que você adicionou da saudação Galeria de aplicativos e, em seguida, clique em Olá **usuários e grupos** guia.</span><span class="sxs-lookup"><span data-stu-id="64ed0-113">Select hello **Applications** tab. Select an application that you added from hello Application Gallery, and then click  hello **Users and Groups** tab.</span></span>
4. <span data-ttu-id="64ed0-114">Em Olá **usuários e grupos** guia Olá **começando com** , digite o nome da saudação de saudação grupo toowhich você deseja acesso tooassign e, em seguida, selecione Olá marca de seleção no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="64ed0-114">On hello **Users and Groups** tab, in hello **Starting with** field, enter hello name of hello group toowhich you want tooassign access, and then select hello check mark in hello upper right.</span></span> <span data-ttu-id="64ed0-115">Você só precisa tootype Olá primeira parte do nome do grupo.</span><span class="sxs-lookup"><span data-stu-id="64ed0-115">You only need tootype hello first part of a group's name.</span></span>
5. <span data-ttu-id="64ed0-116">Selecione o grupo de hello, em seguida, em seguida, Olá **atribuir acesso** botão.</span><span class="sxs-lookup"><span data-stu-id="64ed0-116">Select hello group, then then select hello **Assign Access** button.</span></span> <span data-ttu-id="64ed0-117">Selecione **Sim** quando você vir a mensagem de confirmação de saudação.</span><span class="sxs-lookup"><span data-stu-id="64ed0-117">Select **Yes** when you see hello confirmation message.</span></span> <span data-ttu-id="64ed0-118">Associações de grupo aninhado não há suporte para a atribuição baseada em grupo tooapplications neste momento.</span><span class="sxs-lookup"><span data-stu-id="64ed0-118">Nested group memberships are not supported for group-based assignment tooapplications at this time.</span></span>
6. <span data-ttu-id="64ed0-119">Você também pode ver quais usuários são atribuídos toohello aplicativo, seja diretamente ou por associação em um grupo.</span><span class="sxs-lookup"><span data-stu-id="64ed0-119">You can also see which users are assigned toohello application, either directly or by membership in a group.</span></span> <span data-ttu-id="64ed0-120">toodo, Olá alteração **Mostrar lista suspensa de 'Grupos'** muito**'Todos os usuários'**.</span><span class="sxs-lookup"><span data-stu-id="64ed0-120">toodo this, change hello **Show dropdown from 'Groups'** too**'All Users'**.</span></span> <span data-ttu-id="64ed0-121">lista de saudação mostra usuários no diretório de saudação e se deseja ou não é atribuída a cada usuário toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64ed0-121">hello list shows users in hello directory and whether or not each user is assigned toohello application.</span></span> <span data-ttu-id="64ed0-122">lista de saudação também mostra se usuários Olá atribuído são atribuídos diretamente aplicativo toohello (tipo de atribuição mostrado como "Direto"), ou por meio de associação de grupo (tipo de atribuição mostrado como 'Herdado'.)</span><span class="sxs-lookup"><span data-stu-id="64ed0-122">hello list also shows whether hello assigned users are assigned toohello application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="64ed0-123">Você pode ver hello usuários e guia grupos somente depois que você tiver ativado o Azure AD Premium ou Azure AD Basic.</span><span class="sxs-lookup"><span data-stu-id="64ed0-123">You can see hello Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="64ed0-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="64ed0-124">Next steps</span></span>
<span data-ttu-id="64ed0-125">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="64ed0-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="64ed0-126">Gerenciando acesso tooresources com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="64ed0-126">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="64ed0-127">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="64ed0-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="64ed0-128">Cmdlets do Azure Active Directory para definir configurações de grupo</span><span class="sxs-lookup"><span data-stu-id="64ed0-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="64ed0-129">O que é o Active Directory do Azure?</span><span class="sxs-lookup"><span data-stu-id="64ed0-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="64ed0-130">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="64ed0-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
