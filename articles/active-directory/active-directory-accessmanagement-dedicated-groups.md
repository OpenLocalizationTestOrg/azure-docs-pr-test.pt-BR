---
title: Grupos dedicados do Azure Active Directory | Microsoft Docs
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
ms.openlocfilehash: d9decd5de6a5bafc525edc5b04c82701185088ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="55757-103">Grupos dedicados no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="55757-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="55757-104">No Azure Active Directory (AD do Azure), o recurso de grupos dedicados automaticamente cria e preenche a associação para grupos predefinidos do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55757-104">In Azure Active Directory (Azure AD), the dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="55757-105">Membros de grupos dedicados não podem ser adicionados ou removidos usando o portal clássico do Azure, cmdlets do Windows PowerShell ou programaticamente.</span><span class="sxs-lookup"><span data-stu-id="55757-105">Members of dedicated groups cannot be added or removed using the Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="55757-106">Grupos dedicados requerem que uma licença do Azure AD Premium seja atribuída ao</span><span class="sxs-lookup"><span data-stu-id="55757-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="55757-107">administrador que gerencia a regra em um grupo</span><span class="sxs-lookup"><span data-stu-id="55757-107">the administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="55757-108">todos os usuários selecionados pela regra para serem membros do grupo</span><span class="sxs-lookup"><span data-stu-id="55757-108">all users who are selected by the rule to be a member of the group</span></span>
>
>

<span data-ttu-id="55757-109">**Para habilitar grupos dedicados**</span><span class="sxs-lookup"><span data-stu-id="55757-109">**To enable dedicated groups**</span></span>

1. <span data-ttu-id="55757-110">No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory**e abra o diretório da sua organização.</span><span class="sxs-lookup"><span data-stu-id="55757-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="55757-111">Selecione a guia **Grupos** e, em seguida, abra o grupo que deseja editar.</span><span class="sxs-lookup"><span data-stu-id="55757-111">Select the **Groups** tab, and then open the group you want to edit.</span></span>
3. <span data-ttu-id="55757-112">Selecione a guia **Configurar**, em seguida, defina **Habilitar Grupos Dedicados** para **Sim**.</span><span class="sxs-lookup"><span data-stu-id="55757-112">Select the **Configure** tab, and then set **Enable Dedicated Groups** to **Yes**.</span></span>

<span data-ttu-id="55757-113">Depois do argumento Habilitar Grupos Dedicados ser definido para **Sim**, você ainda pode habilitar o diretório para criar automaticamente o grupo dedicado Todos os Usuários, definindo o argumento **Habilitar Grupo "Todos os Usuários"** para **Sim**.</span><span class="sxs-lookup"><span data-stu-id="55757-113">Once the Enable Dedicated Groups switch is set to **Yes**, you can further enable the directory to automatically create the All Users dedicated group by setting the **Enable “All Users” Group** switch to **Yes**.</span></span> <span data-ttu-id="55757-114">Você pode também editar o nome desse grupo dedicado digitando o **Nome de Exibição para o campo do Grupo “Todos os Usuários”** .</span><span class="sxs-lookup"><span data-stu-id="55757-114">You can then also edit the name of this dedicated group by typing it in the **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="55757-115">O grupo Todos os Usuários pode ser usado para atribuir as mesmas permissões a todos os usuários no diretório.</span><span class="sxs-lookup"><span data-stu-id="55757-115">The All Users group can be used to assign the same permissions to all the users in your directory.</span></span> <span data-ttu-id="55757-116">Por exemplo, você pode conceder a todos os usuários no seu acesso ao diretório para um aplicativo SaaS atribuindo acesso para o grupo dedicado de Todos os Usuários a esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55757-116">For example, you can grant all users in your directory access to a SaaS application by assigning access for the All Users dedicated group to this application.</span></span>

<span data-ttu-id="55757-117">O grupo dedicado Todos os Usuários inclui todos os usuários no diretório, inclusive convidados e usuários externos.</span><span class="sxs-lookup"><span data-stu-id="55757-117">The dedicated All Users group includes all users in the directory, including guests and external users.</span></span> <span data-ttu-id="55757-118">Se você precisar de um grupo que exclua usuários externos, pode fazer isso criando um grupo com uma regra dinâmica baseada em atributos como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="55757-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as the following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="55757-119">Para um grupo que exclui todos os Convidados, use uma regra como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="55757-119">For a group that excludes all Guests, use a rule such as the following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="55757-120">Para saber mais sobre como criar regras *avançadas* (regras que podem conter várias comparações) para a associação dinâmica de grupo, confira [Uso de atributos para criar regras avançadas](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="55757-120">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="55757-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="55757-121">Next steps</span></span>
<span data-ttu-id="55757-122">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="55757-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="55757-123">Gerenciamento de acesso a recursos com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="55757-123">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="55757-124">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="55757-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="55757-125">O que é o Active Directory do Azure?</span><span class="sxs-lookup"><span data-stu-id="55757-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="55757-126">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="55757-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
