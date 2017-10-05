---
title: "Como adicionar ou remover uma função de usuário | Microsoft Docs"
description: "Saiba como adicionar funções a identidades privilegiadas com o aplicativo Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: 3ac07bb7b070f44595c099a454b3d0dbc66126c9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-privileged-identity-management-how-to-add-or-remove-a-user-role"></a><span data-ttu-id="0a8e3-103">Privileged Identity Management do Azure AD: como adicionar ou remover uma função de usuário</span><span class="sxs-lookup"><span data-stu-id="0a8e3-103">Azure AD Privileged Identity Management: How to add or remove a user role</span></span>
<span data-ttu-id="0a8e3-104">Com o Azure AD (Active Directory), um administrador global (ou o administrador da empresa) pode atualizar os usuários que estão **permanentemente** atribuídos a funções no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-104">With Azure Active Directory (AD), a global administrator (or company administrator) can update which users are **permanently** assigned to roles in Azure AD.</span></span> <span data-ttu-id="0a8e3-105">Isso é feito com os cmdlets do PowerShell como `Add-MsolRoleMember` e `Remove-MsolRoleMember`.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-105">This is done with PowerShell cmdlets like `Add-MsolRoleMember` and `Remove-MsolRoleMember`.</span></span> <span data-ttu-id="0a8e3-106">Ou eles podem usar o portal clássico do Azure conforme descrito em [atribuindo funções de administrador no Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0a8e3-106">Or they can use the Azure classic portal as described in [assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="0a8e3-107">O aplicativo Azure AD Privileged Identity Management permite que os administradores de função com privilégios façam atribuições de função permanentes também.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-107">The Azure AD Privileged Identity Management application allows privileged role administrators to make permanent role assignments, as well.</span></span> <span data-ttu-id="0a8e3-108">Além disso, os administradores de função com privilégios podem tornar os usuários **qualificados** para funções de administrador.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-108">Additionally, privileged role administrators can make users **eligible** for admin roles.</span></span> <span data-ttu-id="0a8e3-109">Um administrador elegível pode ativar a função quando necessário e, em seguida, suas permissões expirarão assim ele tiver terminado.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-109">An eligible admin can activate the role when they need it, and then their permissions expire once they're done.</span></span>

## <a name="manage-roles-with-pim-in-the-azure-portal"></a><span data-ttu-id="0a8e3-110">Gerenciar funções com PIM no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0a8e3-110">Manage roles with PIM in the Azure portal</span></span>
<span data-ttu-id="0a8e3-111">Na sua organização, você pode atribuir usuários a diferentes funções administrativas no Azure AD, Office 365 e outros serviços e aplicativos Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-111">In your organization, you can assign users to different administrative roles in Azure AD, Office 365, and other Microsoft services and applications.</span></span>  <span data-ttu-id="0a8e3-112">É possível encontrar mais detalhes sobre as funções disponíveis em [Roles in Azure AD PIM](active-directory-privileged-identity-management-roles.md)(Funções no Azure AD PIM).</span><span class="sxs-lookup"><span data-stu-id="0a8e3-112">More details on the available roles can be found at [Roles in Azure AD PIM](active-directory-privileged-identity-management-roles.md).</span></span>

<span data-ttu-id="0a8e3-113">Para adicionar ou remover um usuário em uma função usando o Privileged Identity Management, abra o painel PIM.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-113">To add or remove a user in a role using Privileged Identity Management, bring up the PIM dashboard.</span></span> <span data-ttu-id="0a8e3-114">Em seguida, clique no botão **Usuários em Funções de Administrador** ou selecione uma função específica (como Administrador Global) na tabela de funções.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-114">Then either click the **Users in Admin Roles** button, or select a specific role (such as Global Administrator) from the roles table.</span></span>

> [!NOTE]
> <span data-ttu-id="0a8e3-115">Se você ainda não habilitou o PIM no portal do Azure, acesse [Get started with Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) (Introdução ao Azure AD PIM) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-115">If you haven't enabled PIM in the Azure portal yet, go to [Get started with Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) for details.</span></span>

<span data-ttu-id="0a8e3-116">Se você desejar conceder acesso ao próprio PIM a outro usuário, as funções que o PIM exige que o usuário tenha serão descritas detalhadamente em [como conceder acesso ao PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="0a8e3-116">If you want to give another user access to PIM itself, the roles which PIM requires the user to have are described further in [how to give access to PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="add-a-user-to-a-role"></a><span data-ttu-id="0a8e3-117">Adicionar um usuário a uma função</span><span class="sxs-lookup"><span data-stu-id="0a8e3-117">Add a user to a role</span></span>
1. <span data-ttu-id="0a8e3-118">No [Portal do Azure](https://portal.azure.com/), selecione o bloco **Azure AD Privileged Identity Management** no painel.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-118">In the [Azure portal](https://portal.azure.com/), select the **Azure AD Privileged Identity Management** tile on the dashboard.</span></span>
2. <span data-ttu-id="0a8e3-119">Selecione **Gerenciar funções privilegiadas**.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-119">Select **Manage privileged roles**.</span></span>
3. <span data-ttu-id="0a8e3-120">Na tabela **Resumo da função** , selecione a função que você deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-120">In the **Role summary** table, select the role you want to manage.</span></span>
4. <span data-ttu-id="0a8e3-121">Na folha de função, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-121">In the role blade, select **Add**.</span></span>
5. <span data-ttu-id="0a8e3-122">Clique em **Selecionar usuários** e pesquise pelo usuário na folha **Selecionar usuários**.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-122">Click **Select users** and search for the user on the **Select users** blade.</span></span>  
6. <span data-ttu-id="0a8e3-123">Selecione o usuário na lista de resultados da pesquisa e clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-123">Select the user from the search results list, and click **Done**.</span></span>
7. <span data-ttu-id="0a8e3-124">Clique em **OK** para salvar sua seleção.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-124">Click **OK** to save your selection.</span></span> <span data-ttu-id="0a8e3-125">O usuário que você selecionou aparecerá na lista como elegível para essa função.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-125">The user you have selected will appear in the list as eligible for the role.</span></span>

> [!NOTE]
> <span data-ttu-id="0a8e3-126">Novos usuários em uma função só são elegíveis para a função por padrão.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-126">New users in a role are only eligible for the role by default.</span></span> <span data-ttu-id="0a8e3-127">Se você quiser tornar a função permanente, clique no usuário na lista.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-127">If you want to make the role permanent, click the user in the list.</span></span> <span data-ttu-id="0a8e3-128">As informações do usuário serão exibidas em uma nova folha.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-128">The user's information will appear in a new blade.</span></span> <span data-ttu-id="0a8e3-129">Selecione **Tornar perm.** no menu de informações do usuário.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-129">Select **Make perm** in the user information menu.</span></span>  
> <span data-ttu-id="0a8e3-130">Se um usuário não é possível registrar para o Azure multi-Factor Authentication (MFA) ou está usando uma conta da Microsoft (geralmente @outlook.com), você precisa torná-las permanentes em todas as suas funções.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-130">If a user cannot register for Azure Multi-Factor Authentication (MFA), or is using a Microsoft account (usually @outlook.com), you need to make them permanent in all their roles.</span></span> <span data-ttu-id="0a8e3-131">Os administradores qualificados são solicitados a se registrar no MFA durante a ativação.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-131">Eligible admins are asked to register for MFA during activation.</span></span>

<span data-ttu-id="0a8e3-132">Agora que o usuário está qualificado para uma função, avise-o que ele pode ativá-la de acordo com as instruções em [Como ativar ou desativar uma função](active-directory-privileged-identity-management-how-to-activate-role.md).</span><span class="sxs-lookup"><span data-stu-id="0a8e3-132">Now that the user is eligible for a role, let them know that they can activate it according to the instructions in [How to activate or deactivate a role](active-directory-privileged-identity-management-how-to-activate-role.md).</span></span>

## <a name="remove-a-user-from-a-role"></a><span data-ttu-id="0a8e3-133">Remover um usuário de uma função</span><span class="sxs-lookup"><span data-stu-id="0a8e3-133">Remove a user from a role</span></span>
<span data-ttu-id="0a8e3-134">Você pode remover usuários de atribuições de função elegíveis, mas certifique-se de que sempre haja pelo menos um usuário que seja um administrador global permanente.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-134">You can remove users from eligible role assignments, but make sure there is always at least one user who is a permanent global administrator.</span></span>

<span data-ttu-id="0a8e3-135">Siga estas etapas para remover um usuário específico de uma função:</span><span class="sxs-lookup"><span data-stu-id="0a8e3-135">Follow these steps to remove a specific user from a role:</span></span>

1. <span data-ttu-id="0a8e3-136">Navegue até a folha na lista de funções, seja selecionando uma função no painel do Azure AD PIM ou clicando no botão **Usuários em Funções de Administrador** .</span><span class="sxs-lookup"><span data-stu-id="0a8e3-136">Navigate to the role in the role list either by selecting a role in the Azure AD PIM dashboard or by clicking on the **Users in Admin Roles** button.</span></span>
2. <span data-ttu-id="0a8e3-137">Clique no usuário na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-137">Click on the user in the user list.</span></span>
3. <span data-ttu-id="0a8e3-138">Clique em **Remover**.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-138">Click **Remove**.</span></span> <span data-ttu-id="0a8e3-139">Uma mensagem solicitará que você confirme.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-139">A message will ask you to confirm.</span></span>
4. <span data-ttu-id="0a8e3-140">Clique em **Sim** para remover a função do usuário.</span><span class="sxs-lookup"><span data-stu-id="0a8e3-140">Click **Yes** to remove the role from the user.</span></span>

<span data-ttu-id="0a8e3-141">Se não tiver certeza de quais os usuários ainda precisam de suas atribuições de função, você poderá [iniciar uma revisão de acesso para a função](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="0a8e3-141">If you're not sure which users still need their role assignments, then you can [start an access review for the role](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a8e3-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a8e3-142">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

