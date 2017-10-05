---
title: Usar um grupo para gerenciar o acesso a aplicativos SaaS| Microsoft Docs
description: "Como usar grupos no Azure Active Directory Premium ou Basic para atribuir acesso a aplicativos SaaS que estão integrados ao Azure Active Directory."
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
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a><span data-ttu-id="1745c-103">Usar um grupo para gerenciar o acesso a aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="1745c-103">Using a group to manage access to SaaS applications</span></span>
<span data-ttu-id="1745c-104">Usando o Azure AD (Azure Active Directory) com a licença do Azure AD Premium ou do Azure AD Basic, você pode usar grupos para atribuir acesso a um aplicativo SaaS que esteja integrado ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1745c-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="1745c-105">Por exemplo, se você quiser atribuir acesso ao departamento de marketing usar cinco aplicativos SaaS diferentes, você pode criar um grupo que contém os usuários no departamento de marketing e atribuir esse grupo a esses cinco aplicativos SaaS que são necessários para o departamento de marketing.</span><span class="sxs-lookup"><span data-stu-id="1745c-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span></span> <span data-ttu-id="1745c-106">Dessa forma, você pode poupar tempo gerenciando a associação no departamento de marketing em um único lugar.</span><span class="sxs-lookup"><span data-stu-id="1745c-106">This way you can save time by managing the membership of the marketing department in one place.</span></span> <span data-ttu-id="1745c-107">Os usuários são atribuídos ao aplicativo quando eles são adicionados como membros do grupo de marketing, e sua atribuição é removida do aplicativo quando eles são removidos do grupo de marketing.</span><span class="sxs-lookup"><span data-stu-id="1745c-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1745c-108">A Microsoft recomenda que você gerencie o Azure AD usando o [Centro de administração do AD do Azure](https://aad.portal.azure.com) no portal do Azure em vez de usar o portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="1745c-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="1745c-109">Esse recurso pode ser usado com centenas de aplicativos que você adiciona na Galeria de aplicativos do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1745c-109">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span></span>

<span data-ttu-id="1745c-110">**Para atribuir acesso de um grupo a um aplicativo SaaS**</span><span class="sxs-lookup"><span data-stu-id="1745c-110">**To assign access for a group to a SaaS application**</span></span>

1. <span data-ttu-id="1745c-111">No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory** na barra de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="1745c-111">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on the navigation bar on the left hand side.</span></span>
2. <span data-ttu-id="1745c-112">Selecione a guia **Diretório** e abra o diretório no qual você deseja atribuir o acesso de um grupo a um aplicativo SaaS.</span><span class="sxs-lookup"><span data-stu-id="1745c-112">Select the **Directory** tab, and then open the directory in which you want to assign access for a group to a SaaS application.</span></span>
3. <span data-ttu-id="1745c-113">Selecione a guia **Aplicativos** . Selecione um aplicativo que você adicionou da Galeria de Aplicativos e clique na guia **Usuários e Grupos**.</span><span class="sxs-lookup"><span data-stu-id="1745c-113">Select the **Applications** tab. Select an application that you added from the Application Gallery, and then click  the **Users and Groups** tab.</span></span>
4. <span data-ttu-id="1745c-114">Na guia **Usuários e Grupos**, no campo **Iniciando com**, insira o nome do grupo ao qual você deseja atribuir acesso e escolha a de seleção no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="1745c-114">On the **Users and Groups** tab, in the **Starting with** field, enter the name of the group to which you want to assign access, and then select the check mark in the upper right.</span></span> <span data-ttu-id="1745c-115">Você só precisa digitar a primeira parte do nome do grupo.</span><span class="sxs-lookup"><span data-stu-id="1745c-115">You only need to type the first part of a group's name.</span></span>
5. <span data-ttu-id="1745c-116">Selecione o grupo e selecione o botão **Atribuir Acesso** .</span><span class="sxs-lookup"><span data-stu-id="1745c-116">Select the group, then then select the **Assign Access** button.</span></span> <span data-ttu-id="1745c-117">Selecione **Sim** quando visualizar a mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="1745c-117">Select **Yes** when you see the confirmation message.</span></span> <span data-ttu-id="1745c-118">No momento, as associações de grupo aninhadas não têm suporte para atribuição com base em grupo de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1745c-118">Nested group memberships are not supported for group-based assignment to applications at this time.</span></span>
6. <span data-ttu-id="1745c-119">Você também pode ver quais usuários são atribuídos ao aplicativo, diretamente ou por associação em um grupo.</span><span class="sxs-lookup"><span data-stu-id="1745c-119">You can also see which users are assigned to the application, either directly or by membership in a group.</span></span> <span data-ttu-id="1745c-120">Para fazer isso, altere **Mostrar lista suspensa de “Grupos”** para **“Todos os Usuários”**.</span><span class="sxs-lookup"><span data-stu-id="1745c-120">To do this, change the **Show dropdown from 'Groups'** to **'All Users'**.</span></span> <span data-ttu-id="1745c-121">A lista mostra usuários no diretório e se cada usuário está ou não atribuído ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1745c-121">The list shows users in the directory and whether or not each user is assigned to the application.</span></span> <span data-ttu-id="1745c-122">A lista também mostra se os usuários atribuídos estão atribuídos diretamente ao aplicativo (tipo de atribuição mostrado como "Direto"), ou por meio de associação de grupo (tipo de atribuição mostrado como "Herdado".)</span><span class="sxs-lookup"><span data-stu-id="1745c-122">The list also shows whether the assigned users are assigned to the application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="1745c-123">Você pode ver a guia Usuários e Grupos somente depois que tiver habilitado Azure AD Premium e Azure AD Basic.</span><span class="sxs-lookup"><span data-stu-id="1745c-123">You can see the Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="1745c-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1745c-124">Next steps</span></span>
<span data-ttu-id="1745c-125">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="1745c-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="1745c-126">Gerenciamento de acesso a recursos com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1745c-126">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="1745c-127">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1745c-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="1745c-128">Cmdlets do Azure Active Directory para definir configurações de grupo</span><span class="sxs-lookup"><span data-stu-id="1745c-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="1745c-129">O que é o Active Directory do Azure?</span><span class="sxs-lookup"><span data-stu-id="1745c-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="1745c-130">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1745c-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
