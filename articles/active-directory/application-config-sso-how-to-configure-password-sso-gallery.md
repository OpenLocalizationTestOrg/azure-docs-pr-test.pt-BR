---
title: "Como configurar o logon único com senha para um aplicativo da Galeria do Azure AD | Microsoft Docs"
description: "Como configurar um aplicativo para logon único baseado em senha quando ele já estiver listado na Galeria de Aplicativos do Azure AD"
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
ms.openlocfilehash: d4dc110eb25c3e550ac4663d28e626a696b58f62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="aedde-103">Como configurar o logon único com senha para um aplicativo da Galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="aedde-103">How to configure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="aedde-104">Quando adiciona um aplicativo da [Galeria de Aplicativos do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), você tem a opção de como deseja que os usuários façam logon nesse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aedde-104">When you add an application from the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have the choice of how you want your users to sign in to that application.</span></span> <span data-ttu-id="aedde-105">É possível configurar essa opção a qualquer momento selecionando o item de navegação **Logon Único** em um aplicativo empresarial no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="aedde-105">You can configure this choice at any time by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="aedde-106">Um dos métodos de logon único disponíveis para você é a opção [Logon único baseado em senha](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="aedde-106">One of the single sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="aedde-107">Trata-se de uma ótima maneira de começar a integrar rapidamente aplicativos no Azure AD, e que lhe permite:</span><span class="sxs-lookup"><span data-stu-id="aedde-107">This is a great way to get started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="aedde-108">Habilitar o **logon único para os usuários** armazenando de forma segura e reproduzindo os nomes de usuário e senhas do aplicativo integrado ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="aedde-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="aedde-109">**Dar suporte a aplicativos que exigem vários campos de entrada**, para aplicativos que exigem mais do que apenas os campos de nome de usuário e senha para entrar</span><span class="sxs-lookup"><span data-stu-id="aedde-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="aedde-110">**Personalizar os rótulos** dos campos de entrada de nome de usuário e senha que seus usuários veem no [Painel de Acesso do Aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando digitam suas credenciais</span><span class="sxs-lookup"><span data-stu-id="aedde-110">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="aedde-111">Permitir que os **usuários** forneçam seus próprios nomes de usuário e senhas para as contas de aplicativos existentes que eles estiverem digitando manualmente no [Painel de Acesso do Aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="aedde-111">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="aedde-112">Permitir que um **membro do grupo de negócios** especifique os nomes de usuário e senhas atribuídos a um usuário usando o recurso de [Autoatendimento de Acesso ao Aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)</span><span class="sxs-lookup"><span data-stu-id="aedde-112">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="aedde-113">Permitir que um **administrador** especifique os nomes de usuário e senhas atribuídos a um usuário usando o recurso Atualizar Credenciais ao [atribuir um usuário a um aplicativo](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="aedde-113">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="aedde-114">Permitir que um **administrador** especifique a senha ou nome de usuário compartilhado por um grupo de pessoas usando o recurso Atualizar Credenciais ao [atribuir um grupo a um aplicativo](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="aedde-114">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="aedde-115">A seguir, temos uma descrição de como você pode habilitar o [Logon único baseado em senha](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) para um aplicativo que já está na [Galeria de Aplicativos do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="aedde-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to an application that is already in the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="aedde-116">Visão geral das etapas necessárias</span><span class="sxs-lookup"><span data-stu-id="aedde-116">Overview of steps required</span></span>
<span data-ttu-id="aedde-117">Para configurar um aplicativo da galeria do Azure AD, será necessário:</span><span class="sxs-lookup"><span data-stu-id="aedde-117">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="aedde-118">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="aedde-118">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="aedde-119">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="aedde-119">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="aedde-120">Atribuir o aplicativo a um usuário ou um grupo</span><span class="sxs-lookup"><span data-stu-id="aedde-120">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="aedde-121">Atribuir um usuário diretamente a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="aedde-121">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="aedde-122">Atribuir um aplicativo diretamente a um grupo</span><span class="sxs-lookup"><span data-stu-id="aedde-122">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="aedde-123">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="aedde-123">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="aedde-124">Para adicionar um aplicativo da Galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="aedde-124">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="aedde-125">Abra o [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="aedde-125">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="aedde-126">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="aedde-126">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aedde-127">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aedde-127">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aedde-128">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aedde-128">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="aedde-129">Clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**</span><span class="sxs-lookup"><span data-stu-id="aedde-129">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="aedde-130">Na caixa de texto **Inserir um nome** da seção **Adicionar da galeria**, digite o nome do aplicativo</span><span class="sxs-lookup"><span data-stu-id="aedde-130">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="aedde-131">Selecione o aplicativo para o qual deseja configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="aedde-131">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="aedde-132">Antes de adicionar o aplicativo, é possível alterar seu nome na caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="aedde-132">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="aedde-133">Clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aedde-133">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="aedde-134">Após um breve período, você verá a folha de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aedde-134">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="aedde-135">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="aedde-135">Configure the application for password single sign-on</span></span>

<span data-ttu-id="aedde-136">Para configurar o logon único para um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="aedde-136">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="aedde-137">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="aedde-137">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="aedde-138">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="aedde-138">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aedde-139">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aedde-139">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aedde-140">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aedde-140">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="aedde-141">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="aedde-141">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="aedde-142">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="aedde-142">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="aedde-143">Selecione o aplicativo para o qual deseja configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="aedde-143">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="aedde-144">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aedde-144">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="aedde-145">Selecione o modo **Logon baseado em Senha.**</span><span class="sxs-lookup"><span data-stu-id="aedde-145">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="aedde-146">[Atribuir usuários ao aplicativo](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="aedde-146">[Assign users to the application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="aedde-147">Além disso, também é possível fornecer credenciais em nome do usuário selecionando as linhas dos usuários, clicando em **Atualizar Credenciais** e digitando o nome de usuário e a senha em nome dos usuários.</span><span class="sxs-lookup"><span data-stu-id="aedde-147">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="aedde-148">Caso contrário, os usuários serão solicitados a inserir as próprias credenciais na inicialização.</span><span class="sxs-lookup"><span data-stu-id="aedde-148">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="aedde-149">Atribuir um usuário diretamente a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="aedde-149">Assign a user to an application directly</span></span>

<span data-ttu-id="aedde-150">Para atribuir um ou mais usuários diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="aedde-150">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="aedde-151">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="aedde-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="aedde-152">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="aedde-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aedde-153">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aedde-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aedde-154">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aedde-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="aedde-155">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="aedde-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="aedde-156">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="aedde-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="aedde-157">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="aedde-157">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="aedde-158">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aedde-158">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="aedde-159">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="aedde-159">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="aedde-160">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="aedde-160">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="aedde-161">Digite o **nome completo** ou o **endereço de email** do usuário que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="aedde-161">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="aedde-162">Passe o mouse sobre o **usuário** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="aedde-162">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="aedde-163">Clique na caixa de seleção ao lado do logotipo ou da foto de perfil do usuário para adicioná-lo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="aedde-163">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="aedde-164">**Opcional:** caso queira **adicionar mais de um usuário**, digite outro **nome completo** ou **endereço de email** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse usuário à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="aedde-164">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="aedde-165">Ao concluir a seleção dos usuários, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aedde-165">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="aedde-166">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="aedde-166">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="aedde-167">Clique no botão **Atribuir** para atribuir o aplicativo aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="aedde-167">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="aedde-168">Atribuir um aplicativo diretamente a um grupo</span><span class="sxs-lookup"><span data-stu-id="aedde-168">Assign an application to a group directly</span></span>

<span data-ttu-id="aedde-169">Para atribuir um ou mais grupos diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="aedde-169">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="aedde-170">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="aedde-170">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="aedde-171">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="aedde-171">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aedde-172">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aedde-172">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aedde-173">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aedde-173">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="aedde-174">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="aedde-174">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="aedde-175">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="aedde-175">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="aedde-176">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="aedde-176">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="aedde-177">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aedde-177">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="aedde-178">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="aedde-178">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="aedde-179">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="aedde-179">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="aedde-180">Digite o **nome completo do grupo** que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="aedde-180">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="aedde-181">Passe o mouse sobre o **grupo** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="aedde-181">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="aedde-182">Clique na caixa de seleção próxima ao logotipo ou ao perfil do grupo para adicionar o usuário na lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="aedde-182">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="aedde-183">**Opcional:** caso queira **adicionar mais de um grupo**, digite outro **nome de grupo completo** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse grupo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="aedde-183">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="aedde-184">Ao concluir a seleção dos grupos, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aedde-184">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="aedde-185">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="aedde-185">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="aedde-186">Clique no botão **Atribuir** para atribuir o aplicativo aos grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="aedde-186">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="aedde-187">Após um breve período, os usuários selecionados poderão iniciar esses aplicativos no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="aedde-187">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aedde-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aedde-188">Next steps</span></span>
[<span data-ttu-id="aedde-189">Fornecer logon único para seus aplicativos com Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="aedde-189">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
