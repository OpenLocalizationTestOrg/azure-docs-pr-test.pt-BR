---
title: "Como configurar o logon único com senha para um aplicativo inexistente na galeria | Microsoft Docs"
description: "Como configurar um aplicativo personalizado inexistente na galeria para logon único baseado em senha quando ele não está listado na Galeria de Aplicativos do Azure AD"
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
ms.openlocfilehash: f629ec99824199306ebf825901beaa99d83d434d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="29fa6-103">Como configurar o logon único com senha para um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="29fa6-103">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="29fa6-104">Além das opções encontradas na Galeria de Aplicativos do Azure AD, você também tem a opção de adicionar um **aplicativo inexistente na galeria** quando o aplicativo desejado não estiver nela.</span><span class="sxs-lookup"><span data-stu-id="29fa6-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span></span> <span data-ttu-id="29fa6-105">Usando esse recurso, é possível adicionar qualquer aplicativo que já existe em sua organização ou qualquer aplicativo de terceiros que você usa e que é de um fornecedor que ainda não faz parte da [Galeria de Aplicativos do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="29fa6-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="29fa6-106">Após adicionar um aplicativo inexistente na galeria, você pode configurar o método de logon único usado por esse aplicativo selecionando o item de navegação **Logon único** em um aplicativo empresarial no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="29fa6-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="29fa6-107">Um dos métodos de logon único disponíveis para você é a opção [Logon único baseado em senha](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="29fa6-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="29fa6-108">Com a experiência de **adicionar um aplicativo inexistente na galeria**, você pode integrar qualquer aplicativo que renderiza um campo de entrada de nome de usuário e senha em HTML, mesmo que ele não esteja em nosso conjunto de aplicativos pré-integrados.</span><span class="sxs-lookup"><span data-stu-id="29fa6-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="29fa6-109">Isso funciona com uma tecnologia de verificação de página que faz parte da extensão do Painel de Acesso e que permite a detecção automática de campos de entrada de usuário e senha, bem como seu armazenamento seguro para a instância do aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="29fa6-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="29fa6-110">Em seguida, reproduza com segurança os nomes de usuário e senhas nesses campos quando um usuário navegar para o aplicativo no painel de acesso do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29fa6-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span></span>

<span data-ttu-id="29fa6-111">Trata-se de uma ótima maneira de começar a integrar rapidamente qualquer tipo de aplicativo no Azure AD, e que lhe permite:</span><span class="sxs-lookup"><span data-stu-id="29fa6-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="29fa6-112">Integrar **qualquer aplicativo do mundo** a seu locatário do Azure AD, desde que ele renderize um campo de entrada de nome de usuário e senha em HTML</span><span class="sxs-lookup"><span data-stu-id="29fa6-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="29fa6-113">Habilitar o **logon único para os usuários** armazenando de forma segura e reproduzindo nomes de usuário e senhas do aplicativo integrado ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="29fa6-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="29fa6-114">**Detectar automaticamente campos de entrada** para qualquer aplicativo e permitir que você detecte manualmente esses campos usando a extensão de Navegador do Painel de Acesso, caso a detecção automática não os encontre</span><span class="sxs-lookup"><span data-stu-id="29fa6-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="29fa6-115">**Dar suporte a aplicativos que exigem vários campos de entrada**, para aplicativos que exigem mais do que apenas os campos de nome de usuário e senha para entrar</span><span class="sxs-lookup"><span data-stu-id="29fa6-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="29fa6-116">**Personalizar os rótulos** dos campos de entrada de nome de usuário e senha que seus usuários veem no [Painel de Acesso do Aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando digitam suas credenciais</span><span class="sxs-lookup"><span data-stu-id="29fa6-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="29fa6-117">Permitir que os **usuários** forneçam seus próprios nomes de usuário e senhas para as contas de aplicativos existentes que eles estiverem digitando manualmente no [Painel de Acesso do Aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="29fa6-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="29fa6-118">Permitir que um **membro do grupo de negócios** especifique os nomes de usuário e senhas atribuídos a um usuário usando o recurso de [Autoatendimento de Acesso ao Aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)</span><span class="sxs-lookup"><span data-stu-id="29fa6-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="29fa6-119">Permitir que um **administrador** especifique os nomes de usuário e senhas atribuídos a um usuário usando o recurso Atualizar Credenciais ao [atribuir um usuário a um aplicativo](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="29fa6-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="29fa6-120">Permitir que um **administrador** especifique a senha ou nome de usuário compartilhado por um grupo de pessoas usando o recurso Atualizar Credenciais ao [atribuir um grupo a um aplicativo](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="29fa6-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="29fa6-121">A seguir, temos uma descrição de como você pode habilitar o [Logon único baseado em senha](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) para qualquer aplicativo que você adicionar usando a experiência de **adicionar um aplicativo inexistente na galeria**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="29fa6-122">Visão geral das etapas necessárias</span><span class="sxs-lookup"><span data-stu-id="29fa6-122">Overview of steps required</span></span>

<span data-ttu-id="29fa6-123">Para configurar um aplicativo da galeria do Azure AD, será necessário:</span><span class="sxs-lookup"><span data-stu-id="29fa6-123">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="29fa6-124">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="29fa6-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="29fa6-125">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="29fa6-125">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="29fa6-126">Atribuir o aplicativo a um usuário ou um grupo</span><span class="sxs-lookup"><span data-stu-id="29fa6-126">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="29fa6-127">Atribuir um usuário diretamente a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="29fa6-127">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="29fa6-128">Atribuir um aplicativo diretamente a um grupo</span><span class="sxs-lookup"><span data-stu-id="29fa6-128">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="29fa6-129">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="29fa6-129">Add a non-gallery application</span></span>

<span data-ttu-id="29fa6-130">Para adicionar um aplicativo da galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="29fa6-130">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="29fa6-131">Abra o [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="29fa6-131">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="29fa6-132">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="29fa6-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="29fa6-133">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="29fa6-134">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29fa6-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="29fa6-135">Clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**</span><span class="sxs-lookup"><span data-stu-id="29fa6-135">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="29fa6-136">clique em **Aplicativo inexistente na galeria.**</span><span class="sxs-lookup"><span data-stu-id="29fa6-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="29fa6-137">Insira o nome do aplicativo na caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-137">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="29fa6-138">Selecione **Adicionar.**</span><span class="sxs-lookup"><span data-stu-id="29fa6-138">Select **Add.**</span></span>

<span data-ttu-id="29fa6-139">Após um curto período de tempo, você poderá ver a folha de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29fa6-139">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="29fa6-140">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="29fa6-140">Configure the application for password single sign-on</span></span>

<span data-ttu-id="29fa6-141">Para configurar o logon único para um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="29fa6-141">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="29fa6-142">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="29fa6-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="29fa6-143">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="29fa6-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="29fa6-144">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="29fa6-145">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29fa6-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="29fa6-146">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="29fa6-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="29fa6-147">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="29fa6-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="29fa6-148">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="29fa6-148">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="29fa6-149">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29fa6-149">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="29fa6-150">Selecione o modo **Logon baseado em senha.**</span><span class="sxs-lookup"><span data-stu-id="29fa6-150">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="29fa6-151">Insira a **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-151">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="29fa6-152">Trata-se da URL em que os usuários inserem o nome de usuário e senha para entrar.</span><span class="sxs-lookup"><span data-stu-id="29fa6-152">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="29fa6-153">Verifique se os campos de entrada estão visíveis na URL.</span><span class="sxs-lookup"><span data-stu-id="29fa6-153">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="29fa6-154">Atribuir usuários a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29fa6-154">Assign users to the application.</span></span>

11. <span data-ttu-id="29fa6-155">Além disso, também é possível fornecer credenciais em nome do usuário selecionando as linhas dos usuários, clicando em **Atualizar Credenciais** e digitando o nome de usuário e a senha em nome dos usuários.</span><span class="sxs-lookup"><span data-stu-id="29fa6-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="29fa6-156">Caso contrário, os usuários serão solicitados a inserir as próprias credenciais na inicialização.</span><span class="sxs-lookup"><span data-stu-id="29fa6-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="29fa6-157">Atribuir um usuário diretamente a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="29fa6-157">Assign a user to an application directly</span></span>

<span data-ttu-id="29fa6-158">Para atribuir um ou mais usuários diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="29fa6-158">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="29fa6-159">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="29fa6-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="29fa6-160">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="29fa6-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="29fa6-161">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="29fa6-162">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29fa6-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="29fa6-163">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="29fa6-163">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="29fa6-164">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="29fa6-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="29fa6-165">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="29fa6-165">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="29fa6-166">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29fa6-166">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="29fa6-167">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-167">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="29fa6-168">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-168">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="29fa6-169">Digite o **nome completo** ou o **endereço de email** do usuário que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-169">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="29fa6-170">Passe o mouse sobre o **usuário** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-170">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="29fa6-171">Clique na caixa de seleção ao lado do logotipo ou da foto de perfil do usuário para adicioná-lo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-171">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="29fa6-172">**Opcional:** caso queira **adicionar mais de um usuário**, digite outro **nome completo** ou **endereço de email** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse usuário à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-172">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="29fa6-173">Ao concluir a seleção dos usuários, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29fa6-173">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="29fa6-174">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="29fa6-174">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="29fa6-175">Clique no botão **Atribuir** para atribuir o aplicativo aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="29fa6-175">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="29fa6-176">Atribuir um aplicativo diretamente a um grupo</span><span class="sxs-lookup"><span data-stu-id="29fa6-176">Assign an application to a group directly</span></span>

<span data-ttu-id="29fa6-177">Para atribuir um ou mais grupos diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="29fa6-177">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="29fa6-178">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="29fa6-178">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="29fa6-179">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="29fa6-179">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="29fa6-180">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-180">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="29fa6-181">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29fa6-181">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="29fa6-182">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="29fa6-182">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="29fa6-183">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="29fa6-183">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="29fa6-184">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="29fa6-184">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="29fa6-185">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29fa6-185">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="29fa6-186">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-186">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="29fa6-187">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-187">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="29fa6-188">Digite o **nome completo do grupo** que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-188">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="29fa6-189">Passe o mouse sobre o **grupo** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-189">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="29fa6-190">Clique na caixa de seleção próxima ao logotipo ou ao perfil do grupo para adicionar o usuário na lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-190">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="29fa6-191">**Opcional:** caso queira **adicionar mais de um grupo**, digite outro **nome de grupo completo** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse grupo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="29fa6-191">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="29fa6-192">Ao concluir a seleção dos grupos, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29fa6-192">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="29fa6-193">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="29fa6-193">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="29fa6-194">Clique no botão **Atribuir** para atribuir o aplicativo aos grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="29fa6-194">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="29fa6-195">Após um breve período, os usuários selecionados poderão iniciar esses aplicativos no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="29fa6-195">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29fa6-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="29fa6-196">Next steps</span></span>
[<span data-ttu-id="29fa6-197">Fornecer logon único para seus aplicativos com Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="29fa6-197">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
