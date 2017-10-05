---
title: "Adicionar novos usuários ao Azure Active Directory | Microsoft Docs"
description: "Explica como adicionar novos usuários ou como alterar informações do usuário no Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a><span data-ttu-id="11767-103">Adicionar novos usuários ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11767-103">Add new users to Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11767-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="11767-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="11767-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="11767-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="11767-106">Este artigo explica como adicionar novos usuários em sua organização no Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="11767-106">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="11767-107">Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="11767-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="11767-108">Escolha **Mais serviços**, insira **Usuários e grupos** na caixa de texto e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="11767-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Abrir usuários e grupos](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="11767-110">Na folha **Usuários e grupos**, selecione **Todos os usuários**, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="11767-110">On the **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![Selecionando o comando Adicionar](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="11767-112">Insira os detalhes do usuário, como **Nome** e **Nome de usuário**.</span><span class="sxs-lookup"><span data-stu-id="11767-112">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="11767-113">A parte do nome do domínio do nome do usuário deve ser o nome do domínio padrão inicial "foo.onmicrosoft.com", ou um nome de domínio verificado não federado, como "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="11767-113">The domain name portion of the user name must either be the initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="11767-114">Copie ou anote a senha de usuário gerada para que você possa fornecê-la ao usuário depois que esse processo estiver concluído.</span><span class="sxs-lookup"><span data-stu-id="11767-114">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="11767-115">Opcionalmente, você pode abrir e preencher as informações na folha **Perfil**, folha **Grupos** ou folha **Função de diretório** para o usuário.</span><span class="sxs-lookup"><span data-stu-id="11767-115">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="11767-116">Para obter mais informações sobre funções de usuário e administrador, consulte [Atribuindo funções de administrador no Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="11767-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="11767-117">Na folha **Usuário**, selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="11767-117">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="11767-118">Distribua com segurança a senha gerada para o novo usuário para que ele possa entrar.</span><span class="sxs-lookup"><span data-stu-id="11767-118">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="11767-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11767-119">Next steps</span></span>
* [<span data-ttu-id="11767-120">Adicionar um usuário externo</span><span class="sxs-lookup"><span data-stu-id="11767-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="11767-121">Redefinir a senha do usuário no novo Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="11767-121">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="11767-122">Alterar as informações de trabalho do usuário</span><span class="sxs-lookup"><span data-stu-id="11767-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="11767-123">Gerenciar perfis de usuário</span><span class="sxs-lookup"><span data-stu-id="11767-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="11767-124">Excluir um usuário no Azure AD</span><span class="sxs-lookup"><span data-stu-id="11767-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="11767-125">Atribuir um usuário a uma função no Azure AD</span><span class="sxs-lookup"><span data-stu-id="11767-125">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
