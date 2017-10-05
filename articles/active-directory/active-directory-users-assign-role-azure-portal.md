---
title: "Atribuir um usuário às funções de administrador no Azure Active Directory | Microsoft Docs"
description: "Explica como alterar informações administrativas de usuário no Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: bfadf133154488f9827cfbeaa98ddb0eb84b52f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a><span data-ttu-id="37d35-103">Atribuir um usuário às funções de administrador no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37d35-103">Assign a user to administrator roles in Azure Active Directory</span></span>
<span data-ttu-id="37d35-104">Este artigo explica como atribuir uma função administrativa a um usuário no Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="37d35-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="37d35-105">Para obter informações sobre como adicionar novos usuários em sua organização, consulte [Adicionar novos usuários ao Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37d35-105">For information about adding new users in your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="37d35-106">Os usuários adicionados não têm permissões de administrador, mas você pode atribuir funções a eles a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="37d35-106">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="37d35-107">Atribuir uma função a um usuário</span><span class="sxs-lookup"><span data-stu-id="37d35-107">Assign a role to a user</span></span>
1. <span data-ttu-id="37d35-108">Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="37d35-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="37d35-109">Escolha **Mais serviços**, insira **Usuários e grupos** na caixa de texto e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="37d35-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Abrir o gerenciamento de usuários](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="37d35-111">Na folha **Usuários e grupos**, selecione **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="37d35-111">On the **Users and groups** blade, select **All users**.</span></span>

   ![Abrindo a folha Todos os usuários](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="37d35-113">Na folha **Usuários e grupos - Todos os usuários** , escolha um usuário na lista.</span><span class="sxs-lookup"><span data-stu-id="37d35-113">On the **Users and groups - All users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="37d35-114">Na folha do usuário selecionado, selecione **Função de diretório**, em seguida, atribua o usuário a uma função na lista **Função de diretório**.</span><span class="sxs-lookup"><span data-stu-id="37d35-114">On the blade for the selected user, select **Directory role**, and then assign the user to a role from the **Directory role** list.</span></span> <span data-ttu-id="37d35-115">Para obter mais informações sobre funções de usuário e administrador, consulte [Atribuindo funções de administrador no Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="37d35-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Atribuindo um usuário a uma função](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="37d35-117">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="37d35-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37d35-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37d35-118">Next steps</span></span>
* [<span data-ttu-id="37d35-119">Adicionar um usuário</span><span class="sxs-lookup"><span data-stu-id="37d35-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="37d35-120">Redefinir a senha do usuário no novo Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="37d35-120">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="37d35-121">Alterar as informações de trabalho do usuário</span><span class="sxs-lookup"><span data-stu-id="37d35-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="37d35-122">Gerenciar perfis de usuário</span><span class="sxs-lookup"><span data-stu-id="37d35-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="37d35-123">Excluir um usuário no Azure AD</span><span class="sxs-lookup"><span data-stu-id="37d35-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
