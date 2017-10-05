---
title: "Adicionar novos usuários ao Azure Active Directory | Microsoft Docs"
description: "Explica como adicionar novos usuários ou como alterar informações do usuário no Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: ff4b742e772a6062885313e9bb49e55907fe125a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-to-azure-active-directory"></a><span data-ttu-id="0adf2-103">Adicionar novos usuários ou usuários com contas da Microsoft ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0adf2-103">Add new users or users with Microsoft accounts to Azure Active Directory</span></span>
<span data-ttu-id="0adf2-104">Adicione usuários para preencher seu diretório.</span><span class="sxs-lookup"><span data-stu-id="0adf2-104">Add users to populate your directory.</span></span> <span data-ttu-id="0adf2-105">Este artigo explica como adicionar novos usuários na sua organização e como adicionar usuários que tenham contas da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0adf2-105">This article explains how to add new users in your organization, and how to add users who have Microsoft accounts.</span></span> <span data-ttu-id="0adf2-106">Para saber mais sobre como adicionar usuários de outros diretórios ao Azure Active Directory ou como adicionar usuários de empresas parceiras, veja [Adicionar usuários de outros diretórios ou de empresas parceiras ao Azure Active Directory](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="0adf2-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="0adf2-107">Os usuários adicionados não têm permissões de administrador, mas você pode atribuir funções a eles a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="0adf2-107">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0adf2-108">A Microsoft recomenda que você gerencie o Azure AD usando o [Centro de administração do AD do Azure](https://aad.portal.azure.com) no portal do Azure em vez de usar o portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="0adf2-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="0adf2-109">Para saber como adicionar um usuário no Centro de administração do Azure AD, consulte [Adicionar novos usuários ao Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0adf2-109">For how to add a user in the Azure AD admin center, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="0adf2-110">Adicionar um usuário</span><span class="sxs-lookup"><span data-stu-id="0adf2-110">Add a user</span></span>
1. <span data-ttu-id="0adf2-111">Entre no [portal clássico do Azure](https://manage.windowsazure.com) com uma conta que seja um administrador global para o diretório.</span><span class="sxs-lookup"><span data-stu-id="0adf2-111">Sign in to the [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="0adf2-112">Selecione **Active Directory**e selecione o nome do diretório da sua organização.</span><span class="sxs-lookup"><span data-stu-id="0adf2-112">Select **Active Directory**, and then select the name of your organization directory.</span></span>
3. <span data-ttu-id="0adf2-113">Selecione a guia **Usuários** e, na barra de comandos, selecione **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="0adf2-113">Select the **Users** tab, and then, in the command bar, select **Add User**.</span></span>
4. <span data-ttu-id="0adf2-114">Na página **Conte-nos sobre este usuário**, em **Tipo de usuário**, selecione:</span><span class="sxs-lookup"><span data-stu-id="0adf2-114">On the **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="0adf2-115">**Novo usuário em sua organização** – adiciona uma nova conta de usuário a seu diretório.</span><span class="sxs-lookup"><span data-stu-id="0adf2-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="0adf2-116">**Usuário com uma conta da Microsoft existente** – adiciona uma conta de consumidor da Microsoft existente a seu diretório (por exemplo, uma conta do Outlook)</span><span class="sxs-lookup"><span data-stu-id="0adf2-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account to your directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="0adf2-117">Dependendo da **Tipo de usuário**, insira um nome de usuário (para o novo usuário) ou um endereço de email (para um usuário com uma conta da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="0adf2-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="0adf2-118">Na página **Perfil** do usuário, forneça um nome e um sobrenome, um nome amigável e uma função de usuário da lista **Funções**.</span><span class="sxs-lookup"><span data-stu-id="0adf2-118">On the user **Profile** page, provide a first and last name, a user-friendly name, and a user role from the **Roles** list.</span></span> <span data-ttu-id="0adf2-119">Para obter mais informações sobre funções de usuário e administrador, consulte [Atribuindo funções de administrador no Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0adf2-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="0adf2-120">Especifique se deseja **Habilitar Autenticação Multifator** para o usuário.</span><span class="sxs-lookup"><span data-stu-id="0adf2-120">Specify whether to **Enable Multi-Factor Authentication** for the user.</span></span>
7. <span data-ttu-id="0adf2-121">Na página **Obter senha temporária**, selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0adf2-121">On the **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0adf2-122">Se sua organização usa mais de um domínio, você deve saber sobre os seguintes problemas ao adicionar uma conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="0adf2-122">If your organization uses more than one domain, you should know about the following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="0adf2-123">PARA adicionar contas de usuário com o mesmo nome UPN entre domínios, **primeiro** adicione, por exemplo, geoffgrisso@contoso.onmicrosoft.com **seguido de** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0adf2-123">TO add user accounts with the same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="0adf2-124">**Não** adicione geoffgrisso@contoso.com antes de adicionar geoffgrisso@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="0adf2-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span></span> <span data-ttu-id="0adf2-125">Essa ordem é extremamente importante e pode ser inconveniente para desfazer.</span><span class="sxs-lookup"><span data-stu-id="0adf2-125">This order is important, and can be cumbersome to undo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="0adf2-126">Alterar as informações do usuário</span><span class="sxs-lookup"><span data-stu-id="0adf2-126">Change user information</span></span>
<span data-ttu-id="0adf2-127">Você pode alterar qualquer atributo de usuário, exceto a ID de objeto.</span><span class="sxs-lookup"><span data-stu-id="0adf2-127">You can change any user attribute except for the object ID.</span></span>

1. <span data-ttu-id="0adf2-128">Abra seu diretório.</span><span class="sxs-lookup"><span data-stu-id="0adf2-128">Open your directory.</span></span>
2. <span data-ttu-id="0adf2-129">Selecione a guia **Usuários** e selecione o nome de exibição do usuário que você deseja alterar.</span><span class="sxs-lookup"><span data-stu-id="0adf2-129">Select the **Users** tab, and then select the display name of the user you want to change.</span></span>
3. <span data-ttu-id="0adf2-130">Conclua suas alterações e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0adf2-130">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="0adf2-131">Se o usuário que você está alterando estiver sincronizado com seu serviço do Active Directory local, não poderá alterar as informações do usuário usando este procedimento.</span><span class="sxs-lookup"><span data-stu-id="0adf2-131">If the user that you're changing is synchronized with your on-premises Active Directory service, you can't change the user information using this procedure.</span></span> <span data-ttu-id="0adf2-132">Para alterar o usuário, use suas ferramentas de gerenciamento do Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="0adf2-132">To change the user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="0adf2-133">Limitações e gerenciamento de usuário convidado</span><span class="sxs-lookup"><span data-stu-id="0adf2-133">Guest user management and limitations</span></span>
<span data-ttu-id="0adf2-134">Contas de convidados são usuários de outros diretórios que foram convidados a seu diretório para acessar documentos do SharePoint, aplicativos ou outros recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0adf2-134">Guest accounts are users from other directories who were invited to your directory to access SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="0adf2-135">Uma conta de convidado no diretório que tem o atributo UserType subjacente definido como "Convidado".</span><span class="sxs-lookup"><span data-stu-id="0adf2-135">A guest account in your directory has its underlying UserType attribute set to "Guest."</span></span> <span data-ttu-id="0adf2-136">Usuários normais (especificamente, membros de seu diretório) têm o atributo UserType "Membro".</span><span class="sxs-lookup"><span data-stu-id="0adf2-136">Regular users (specifically, members of your directory) have the UserType attribute "Member."</span></span>

<span data-ttu-id="0adf2-137">Os convidados têm um conjunto limitado de direitos no diretório.</span><span class="sxs-lookup"><span data-stu-id="0adf2-137">Guests have a limited set of rights in the directory.</span></span> <span data-ttu-id="0adf2-138">Esses direitos limitam a capacidade dos Convidados para descobrir informações sobre outros usuários no diretório.</span><span class="sxs-lookup"><span data-stu-id="0adf2-138">These rights limit the ability for Guests to discover information about other users in the directory.</span></span> <span data-ttu-id="0adf2-139">No entanto, os usuários convidados ainda podem interagir com os usuários e os grupos associados aos recursos em que estão trabalhando.</span><span class="sxs-lookup"><span data-stu-id="0adf2-139">However, guest users can still interact with the users and groups associated with the resources they're working on.</span></span> <span data-ttu-id="0adf2-140">Os usuários convidados podem:</span><span class="sxs-lookup"><span data-stu-id="0adf2-140">Guest users can:</span></span>

* <span data-ttu-id="0adf2-141">Ver outros usuários e grupos associados a uma assinatura do Azure à qual estão atribuídos</span><span class="sxs-lookup"><span data-stu-id="0adf2-141">See other users and groups associated with an Azure subscription to which they're assigned</span></span>
* <span data-ttu-id="0adf2-142">Ver os membros de grupos aos quais eles pertencem</span><span class="sxs-lookup"><span data-stu-id="0adf2-142">See the members of groups to which they belong</span></span>
* <span data-ttu-id="0adf2-143">Pesquisar outros usuários no diretório, desde que saibam o endereço de email completo do usuário</span><span class="sxs-lookup"><span data-stu-id="0adf2-143">Look up other users in the directory, if they know the full email address of the user</span></span>
* <span data-ttu-id="0adf2-144">ver apenas um conjunto limitado de atributos dos usuários pesquisados - limitados ao nome de exibição, o endereço de email, o nome UPN e a foto em miniatura</span><span class="sxs-lookup"><span data-stu-id="0adf2-144">See only a limited set of attributes of the users they look up--limited to display name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="0adf2-145">Obter uma lista dos domínios verificados no diretório</span><span class="sxs-lookup"><span data-stu-id="0adf2-145">Get a list of verified domains in the directory</span></span>
* <span data-ttu-id="0adf2-146">consentir o acesso a aplicativos, concedendo a eles o mesmo acesso que os Membros têm em seu diretório</span><span class="sxs-lookup"><span data-stu-id="0adf2-146">Consent to applications, granting them the same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="0adf2-147">Definir políticas de acesso de usuário convidado</span><span class="sxs-lookup"><span data-stu-id="0adf2-147">Set guest user access policies</span></span>
<span data-ttu-id="0adf2-148">A guia **Configurar** do diretório inclui opções para controlar o acesso para usuários convidados.</span><span class="sxs-lookup"><span data-stu-id="0adf2-148">The **Configure** tab of a directory includes options to control access for guest users.</span></span> <span data-ttu-id="0adf2-149">Essas opções só podem ser alteradas no portal clássico do Azure por um administrador global.</span><span class="sxs-lookup"><span data-stu-id="0adf2-149">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="0adf2-150">Atualmente, não existe um método de API ou do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0adf2-150">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="0adf2-151">Para abrir a guia **Configurar** no Portal Clássico do Azure, selecione **Active Directory** e selecione o nome do diretório.</span><span class="sxs-lookup"><span data-stu-id="0adf2-151">To open the **Configure** tab in the Azure classic portal, select **Active Directory**, and then select the name of the directory.</span></span>

![Configurar a guia no Azure Active Directory][1]

<span data-ttu-id="0adf2-153">Então você pode editar as opções para controlar o acesso para os usuários convidados.</span><span class="sxs-lookup"><span data-stu-id="0adf2-153">Then you can edit the options to control access for guest users.</span></span>

![opções de controle de acesso para usuários convidados][2]

## <a name="whats-next"></a><span data-ttu-id="0adf2-155">O que vem a seguir</span><span class="sxs-lookup"><span data-stu-id="0adf2-155">What's next</span></span>
* [<span data-ttu-id="0adf2-156">Adicionar usuários de outros diretórios ou de empresas parceiras no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0adf2-156">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="0adf2-157">Administrando o Azure AD</span><span class="sxs-lookup"><span data-stu-id="0adf2-157">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="0adf2-158">Gerenciar senhas no Azure AD</span><span class="sxs-lookup"><span data-stu-id="0adf2-158">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="0adf2-159">Gerenciar grupos no Azure AD</span><span class="sxs-lookup"><span data-stu-id="0adf2-159">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
