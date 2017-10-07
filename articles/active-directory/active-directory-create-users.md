---
title: "aaaAdd novo tooAzure de usuários do Active Directory | Microsoft Docs"
description: "Explica como tooadd novos usuários ou alterar informações de usuário no Active Directory do Azure."
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
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a><span data-ttu-id="daa14-103">Adicionar novos usuários ou usuários com tooAzure de contas do Microsoft Active Directory</span><span class="sxs-lookup"><span data-stu-id="daa14-103">Add new users or users with Microsoft accounts tooAzure Active Directory</span></span>
<span data-ttu-id="daa14-104">Adicione usuários toopopulate seu diretório.</span><span class="sxs-lookup"><span data-stu-id="daa14-104">Add users toopopulate your directory.</span></span> <span data-ttu-id="daa14-105">Este artigo explica como tooadd novos usuários em sua organização e como os usuários de tooadd com contas da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="daa14-105">This article explains how tooadd new users in your organization, and how tooadd users who have Microsoft accounts.</span></span> <span data-ttu-id="daa14-106">Para saber mais sobre como adicionar usuários de outros diretórios ao Azure Active Directory ou como adicionar usuários de empresas parceiras, veja [Adicionar usuários de outros diretórios ou de empresas parceiras ao Azure Active Directory](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="daa14-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="daa14-107">Usuários adicionados não tem permissões de administrador, por padrão, mas você pode atribuir funções toothem a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="daa14-107">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="daa14-108">A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="daa14-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="daa14-109">Para como tooadd um usuário no Centro de administração de saudação do AD do Azure, consulte [adicionar nova tooAzure de usuários do Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="daa14-109">For how tooadd a user in hello Azure AD admin center, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="daa14-110">Adicionar um usuário</span><span class="sxs-lookup"><span data-stu-id="daa14-110">Add a user</span></span>
1. <span data-ttu-id="daa14-111">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="daa14-111">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="daa14-112">Selecione **do Active Directory**e, em seguida, selecione o nome de saudação do diretório de sua organização.</span><span class="sxs-lookup"><span data-stu-id="daa14-112">Select **Active Directory**, and then select hello name of your organization directory.</span></span>
3. <span data-ttu-id="daa14-113">Selecione Olá **usuários** guia e, em seguida, na barra de comandos hello, selecione **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="daa14-113">Select hello **Users** tab, and then, in hello command bar, select **Add User**.</span></span>
4. <span data-ttu-id="daa14-114">Em Olá **Conte-nos sobre este usuário** página em **tipo de usuário**, selecione:</span><span class="sxs-lookup"><span data-stu-id="daa14-114">On hello **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="daa14-115">**Novo usuário em sua organização** – adiciona uma nova conta de usuário a seu diretório.</span><span class="sxs-lookup"><span data-stu-id="daa14-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="daa14-116">**Usuário com uma conta existente do Microsoft** – adiciona um Microsoft consumidor conta tooyour diretório existente (por exemplo, uma conta do Outlook)</span><span class="sxs-lookup"><span data-stu-id="daa14-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account tooyour directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="daa14-117">Dependendo da **Tipo de usuário**, insira um nome de usuário (para o novo usuário) ou um endereço de email (para um usuário com uma conta da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="daa14-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="daa14-118">Usuário Olá **perfil** , forneça um nome e sobrenome, um nome amigável e uma função de usuário do hello **funções** lista.</span><span class="sxs-lookup"><span data-stu-id="daa14-118">On hello user **Profile** page, provide a first and last name, a user-friendly name, and a user role from hello **Roles** list.</span></span> <span data-ttu-id="daa14-119">Para obter mais informações sobre funções de usuário e administrador, consulte [Atribuindo funções de administrador no Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="daa14-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="daa14-120">Especifique se muito**habilitar autenticação multifator** para usuário hello.</span><span class="sxs-lookup"><span data-stu-id="daa14-120">Specify whether too**Enable Multi-Factor Authentication** for hello user.</span></span>
7. <span data-ttu-id="daa14-121">Em Olá **obter senha temporária** página, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="daa14-121">On hello **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="daa14-122">Se sua organização usa mais de um domínio, você deve saber sobre Olá problemas a seguir quando você adicionar uma conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="daa14-122">If your organization uses more than one domain, you should know about hello following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="daa14-123">contas de usuário tooadd com hello mesmo nome principal de usuário (UPN) entre domínios, **primeiro** adicionar, por exemplo, geoffgrisso@contoso.onmicrosoft.com, **seguido por** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="daa14-123">tooadd user accounts with hello same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="daa14-124">**Não** adicione geoffgrisso@contoso.com antes de adicionar geoffgrisso@contoso.onmicrosoft.com. Essa ordem é importante e pode ser complicado tooundo.</span><span class="sxs-lookup"><span data-stu-id="daa14-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com. This order is important, and can be cumbersome tooundo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="daa14-125">Alterar as informações do usuário</span><span class="sxs-lookup"><span data-stu-id="daa14-125">Change user information</span></span>
<span data-ttu-id="daa14-126">Você pode alterar qualquer atributo de usuário, exceto Olá ID de objeto.</span><span class="sxs-lookup"><span data-stu-id="daa14-126">You can change any user attribute except for hello object ID.</span></span>

1. <span data-ttu-id="daa14-127">Abra seu diretório.</span><span class="sxs-lookup"><span data-stu-id="daa14-127">Open your directory.</span></span>
2. <span data-ttu-id="daa14-128">Selecione Olá **usuários** guia e nome para exibição, em seguida, selecione Olá do hello usuário a ser toochange.</span><span class="sxs-lookup"><span data-stu-id="daa14-128">Select hello **Users** tab, and then select hello display name of hello user you want toochange.</span></span>
3. <span data-ttu-id="daa14-129">Conclua suas alterações e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="daa14-129">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="daa14-130">Se o usuário de saudação que você está alterando está sincronizado com o serviço do Active Directory local, você não pode alterar informações do usuário hello usando esse procedimento.</span><span class="sxs-lookup"><span data-stu-id="daa14-130">If hello user that you're changing is synchronized with your on-premises Active Directory service, you can't change hello user information using this procedure.</span></span> <span data-ttu-id="daa14-131">usuário de saudação toochange, use as ferramentas de gerenciamento do Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="daa14-131">toochange hello user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="daa14-132">Limitações e gerenciamento de usuário convidado</span><span class="sxs-lookup"><span data-stu-id="daa14-132">Guest user management and limitations</span></span>
<span data-ttu-id="daa14-133">As contas de convidados são usuários de outros diretórios que foram convidados tooyour directory tooaccess SharePoint documentos, aplicativos ou outros recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="daa14-133">Guest accounts are users from other directories who were invited tooyour directory tooaccess SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="daa14-134">Uma conta de convidado em seu diretório tem o atributo de UserType subjacente definido muito "convidado".</span><span class="sxs-lookup"><span data-stu-id="daa14-134">A guest account in your directory has its underlying UserType attribute set too"Guest."</span></span> <span data-ttu-id="daa14-135">Usuários regulares (especificamente, os membros do diretório) tem o atributo de UserType do hello "Member".</span><span class="sxs-lookup"><span data-stu-id="daa14-135">Regular users (specifically, members of your directory) have hello UserType attribute "Member."</span></span>

<span data-ttu-id="daa14-136">Os convidados têm um conjunto limitado de direitos no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="daa14-136">Guests have a limited set of rights in hello directory.</span></span> <span data-ttu-id="daa14-137">Esses direitos limitam a capacidade de saudação para obter informações sobre outros usuários no diretório Olá toodiscover convidados.</span><span class="sxs-lookup"><span data-stu-id="daa14-137">These rights limit hello ability for Guests toodiscover information about other users in hello directory.</span></span> <span data-ttu-id="daa14-138">No entanto, os usuários convidados ainda podem interagir com usuários hello e grupos associados a recursos hello está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="daa14-138">However, guest users can still interact with hello users and groups associated with hello resources they're working on.</span></span> <span data-ttu-id="daa14-139">Os usuários convidados podem:</span><span class="sxs-lookup"><span data-stu-id="daa14-139">Guest users can:</span></span>

* <span data-ttu-id="daa14-140">Ver outros usuários e grupos associados a um toowhich de assinatura do Azure que estão atribuídas</span><span class="sxs-lookup"><span data-stu-id="daa14-140">See other users and groups associated with an Azure subscription toowhich they're assigned</span></span>
* <span data-ttu-id="daa14-141">Consulte Olá membros de grupos toowhich pertencem</span><span class="sxs-lookup"><span data-stu-id="daa14-141">See hello members of groups toowhich they belong</span></span>
* <span data-ttu-id="daa14-142">Pesquisar outros usuários no diretório hello, se eles saibam o endereço de email completo de saudação do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="daa14-142">Look up other users in hello directory, if they know hello full email address of hello user</span></span>
* <span data-ttu-id="daa14-143">Consulte apenas um conjunto limitado de atributos de usuários Olá que eles pesquisar – toodisplay limitado nome, endereço de email, nome de usuário principal (UPN) e foto em miniatura</span><span class="sxs-lookup"><span data-stu-id="daa14-143">See only a limited set of attributes of hello users they look up--limited toodisplay name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="daa14-144">Obter uma lista de domínios verificados no diretório Olá</span><span class="sxs-lookup"><span data-stu-id="daa14-144">Get a list of verified domains in hello directory</span></span>
* <span data-ttu-id="daa14-145">Consentimento tooapplications, conceder-lhes Olá mesmo acesso que os membros têm em seu diretório</span><span class="sxs-lookup"><span data-stu-id="daa14-145">Consent tooapplications, granting them hello same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="daa14-146">Definir políticas de acesso de usuário convidado</span><span class="sxs-lookup"><span data-stu-id="daa14-146">Set guest user access policies</span></span>
<span data-ttu-id="daa14-147">Olá **configurar** guia de um diretório inclui opções toocontrol acesso para usuários convidados.</span><span class="sxs-lookup"><span data-stu-id="daa14-147">hello **Configure** tab of a directory includes options toocontrol access for guest users.</span></span> <span data-ttu-id="daa14-148">Essas opções só podem ser alteradas no portal clássico do Azure por um administrador global.</span><span class="sxs-lookup"><span data-stu-id="daa14-148">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="daa14-149">Atualmente, não existe um método de API ou do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="daa14-149">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="daa14-150">Olá tooopen **configurar** guia Olá select de portal clássico do Azure **do Active Directory**e, em seguida, selecione nome de saudação do diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="daa14-150">tooopen hello **Configure** tab in hello Azure classic portal, select **Active Directory**, and then select hello name of hello directory.</span></span>

![Configurar a guia no Azure Active Directory][1]

<span data-ttu-id="daa14-152">Em seguida, você pode editar Olá opções toocontrol acesso para usuários convidados.</span><span class="sxs-lookup"><span data-stu-id="daa14-152">Then you can edit hello options toocontrol access for guest users.</span></span>

![opções de controle de acesso para usuários convidados][2]

## <a name="whats-next"></a><span data-ttu-id="daa14-154">O que vem a seguir</span><span class="sxs-lookup"><span data-stu-id="daa14-154">What's next</span></span>
* [<span data-ttu-id="daa14-155">Adicionar usuários de outros diretórios ou de empresas parceiras no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="daa14-155">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="daa14-156">Administrando o Azure AD</span><span class="sxs-lookup"><span data-stu-id="daa14-156">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="daa14-157">Gerenciar senhas no Azure AD</span><span class="sxs-lookup"><span data-stu-id="daa14-157">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="daa14-158">Gerenciar grupos no Azure AD</span><span class="sxs-lookup"><span data-stu-id="daa14-158">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
