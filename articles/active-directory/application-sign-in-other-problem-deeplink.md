---
title: Problemas para entrar em um aplicativo usando um DeepLink| Microsoft Docs
description: Como solucionar problemas de acesso a um aplicativo de uma URL de Deeplink usando o Azure AD
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
ms.openlocfilehash: 798015ab68afc65378cffc75afec9c7f91fc1926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-using-a-deeplink"></a><span data-ttu-id="30f83-103">Problemas para entrar em um aplicativo usando um DeepLink</span><span class="sxs-lookup"><span data-stu-id="30f83-103">Problems signing in to an application using a deeplink</span></span>

<span data-ttu-id="30f83-104">O Painel de Acesso é um portal baseado na Web que permite a um usuário com uma conta corporativa ou de estudante no Azure Active Directory (Azure AD) exibir e iniciar aplicativos baseados em nuvem para os quais o administrador do Azure AD concedeu acesso.</span><span class="sxs-lookup"><span data-stu-id="30f83-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="30f83-105">Esses aplicativos são configurados em nome do usuário no portal do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30f83-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="30f83-106">O aplicativo deve ser configurado corretamente e atribuído ao usuário ou a um grupo no qual o usuário é membro para ver o aplicativo no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="30f83-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="30f83-107">DeepLinks ou URLs de acesso do Usuário são links que seus usuários podem usar para acessar seus aplicativos SSO de senha diretamente de suas barras de URLs de navegadores.</span><span class="sxs-lookup"><span data-stu-id="30f83-107">Deep links or User access URLs are links your users may use to access their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="30f83-108">Ao navegar até esse link, os usuários serão automaticamente conectados ao aplicativo sem ter que ir primeiro ao Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="30f83-108">By navigating to this link, users be automatically signed into the application without having to go to the Access Panel first.</span></span> <span data-ttu-id="30f83-109">Esse é o mesmo link que os usuários usam para acessar esses aplicativos a partir do aplicativo de inicialização do Office 365.</span><span class="sxs-lookup"><span data-stu-id="30f83-109">This is the same link that users use to access these applications from the Office 365 application launcher.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="30f83-110">Questões gerais que primeiro devem ser verificadas</span><span class="sxs-lookup"><span data-stu-id="30f83-110">General issues to check first</span></span>

-   <span data-ttu-id="30f83-111">Verifique se você está usando um **navegador** que atenda aos requisitos mínimos para o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="30f83-111">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="30f83-112">Verifique se o navegador do usuário adicionou a URL do aplicativo ao seus **sites confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="30f83-112">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="30f83-113">Verifique se o aplicativo está **configurado** corretamente.</span><span class="sxs-lookup"><span data-stu-id="30f83-113">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="30f83-114">Verifique se a conta do usuário está **habilitada** para entradas.</span><span class="sxs-lookup"><span data-stu-id="30f83-114">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="30f83-115">Verifique se a conta do usuário **não está bloqueada.**</span><span class="sxs-lookup"><span data-stu-id="30f83-115">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="30f83-116">Verifique se a **senha do usuário não expirou ou foi esquecida.**</span><span class="sxs-lookup"><span data-stu-id="30f83-116">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="30f83-117">Verifique se a **Autenticação Multifator** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="30f83-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="30f83-118">Verifique se uma **Política de acesso condicional** ou política de **Proteção de Identidade** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="30f83-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="30f83-119">Verifique se as **informações de contato de autenticação** de um usuário estão atualizadas para permitir a aplicação da Autenticação Multifator ou de políticas de Acesso Condicional.</span><span class="sxs-lookup"><span data-stu-id="30f83-119">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="30f83-120">Tente também eliminar os cookies do navegador e tente entrar novamente.</span><span class="sxs-lookup"><span data-stu-id="30f83-120">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="checking-the-deeplink"></a><span data-ttu-id="30f83-121">Verificar o DeepLink</span><span class="sxs-lookup"><span data-stu-id="30f83-121">Checking the deeplink</span></span>

<span data-ttu-id="30f83-122">Para verificar se você tem o DeepLink correto, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="30f83-122">To check if you have the correct deeplink, follow the steps below:</span></span>

1.  <span data-ttu-id="30f83-123">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="30f83-123">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="30f83-124">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="30f83-124">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30f83-125">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30f83-125">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30f83-126">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30f83-126">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30f83-127">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="30f83-127">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="30f83-128">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="30f83-128">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="30f83-129">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="30f83-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="30f83-130">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="30f83-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

8.  <span data-ttu-id="30f83-131">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30f83-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="30f83-132">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30f83-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="30f83-133">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="30f83-133">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="30f83-134">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="30f83-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

11. <span data-ttu-id="30f83-135">Selecione o aplicativo que você deseja verificar o DeepLink.</span><span class="sxs-lookup"><span data-stu-id="30f83-135">Select the application you want the check the deeplink for.</span></span>

12. <span data-ttu-id="30f83-136">Localize o rótulo **URL de acesso do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="30f83-136">Find the label **User Access URL**.</span></span> <span data-ttu-id="30f83-137">O DeepLink deve corresponder a essa URL.</span><span class="sxs-lookup"><span data-stu-id="30f83-137">You deeplink should match this URL.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="30f83-138">Como instalar a extensão do Navegador do Painel de Acesso</span><span class="sxs-lookup"><span data-stu-id="30f83-138">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="30f83-139">Para instalar a extensão do Navegador do Painel de Acesso, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="30f83-139">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="30f83-140">Abra o [Painel de Acesso](https://myapps.microsoft.com) em um dos navegadores compatíveis e entre como um **usuário** no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30f83-140">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="30f83-141">Clique no **aplicativo de SSO com senha** no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="30f83-141">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="30f83-142">No prompt solicitando a instalação do software, selecione **Instalar Agora**.</span><span class="sxs-lookup"><span data-stu-id="30f83-142">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="30f83-143">Com base no seu navegador, você será direcionado para o link de download.</span><span class="sxs-lookup"><span data-stu-id="30f83-143">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="30f83-144">**Adicione** a extensão ao seu navegador.</span><span class="sxs-lookup"><span data-stu-id="30f83-144">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="30f83-145">Se o navegador solicitar, selecione como **Habilitar** ou **Permitir** a extensão.</span><span class="sxs-lookup"><span data-stu-id="30f83-145">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="30f83-146">Quando estiver instalado, **reinicie** a sessão do navegador.</span><span class="sxs-lookup"><span data-stu-id="30f83-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="30f83-147">Entrar no Painel de Acesso e verificar se é possível **iniciar** os aplicativos de SSO de senha</span><span class="sxs-lookup"><span data-stu-id="30f83-147">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="30f83-148">Também é possível baixar a extensão para Chrome e Firefox diretamente pelos links abaixo:</span><span class="sxs-lookup"><span data-stu-id="30f83-148">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="30f83-149">Extensão do Painel de Acesso do Chrome</span><span class="sxs-lookup"><span data-stu-id="30f83-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="30f83-150">Extensão do Painel de Acesso do Firefox</span><span class="sxs-lookup"><span data-stu-id="30f83-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="30f83-151">Como configurar o login único com senha para um aplicativo na galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="30f83-151">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="30f83-152">Para configurar um aplicativo da galeria do Azure AD será necessário:</span><span class="sxs-lookup"><span data-stu-id="30f83-152">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="30f83-153">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="30f83-153">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="30f83-154">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="30f83-154">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="30f83-155">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="30f83-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="30f83-156">Para adicionar um aplicativo da Galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="30f83-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="30f83-157">Abra o [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="30f83-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="30f83-158">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="30f83-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30f83-159">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30f83-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30f83-160">clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30f83-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30f83-161">clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**.</span><span class="sxs-lookup"><span data-stu-id="30f83-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="30f83-162">Na caixa de texto **Inserir um nome** da seção **Adicionar da galeria**, digite o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30f83-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="30f83-163">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="30f83-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="30f83-164">Antes de adicionar o aplicativo, é possível alterar seu nome pela caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="30f83-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="30f83-165">Clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30f83-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="30f83-166">Após um breve período, você verá a folha de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30f83-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="30f83-167">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="30f83-167">Configure the application for password single sign-on</span></span>

<span data-ttu-id="30f83-168">Para configurar o logon único para um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="30f83-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="30f83-169">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="30f83-169">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="30f83-170">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="30f83-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30f83-171">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30f83-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30f83-172">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30f83-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30f83-173">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="30f83-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="30f83-174">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="30f83-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="30f83-175">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="30f83-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="30f83-176">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30f83-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="30f83-177">Selecione o modo **Logon baseado em Senha.**</span><span class="sxs-lookup"><span data-stu-id="30f83-177">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="30f83-178">[Atribuir usuários ao aplicativo](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="30f83-178">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="30f83-179">Além disso, também é possível fornecer credenciais em nome do usuário selecionando as linhas dos usuários, clicando em **Atualizar Credenciais** e digitando o nome de usuário e a senha em nome dos usuários.</span><span class="sxs-lookup"><span data-stu-id="30f83-179">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="30f83-180">Caso contrário, os usuários serão solicitados a inserir as próprias credenciais na inicialização.</span><span class="sxs-lookup"><span data-stu-id="30f83-180">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="30f83-181">Como configurar o logon único com senha para um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="30f83-181">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="30f83-182">Para configurar um aplicativo da galeria do Azure AD será necessário:</span><span class="sxs-lookup"><span data-stu-id="30f83-182">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="30f83-183">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="30f83-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="30f83-184">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="30f83-184">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="30f83-185">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="30f83-185">Add a non-gallery application</span></span>

<span data-ttu-id="30f83-186">Para adicionar um aplicativo da Galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="30f83-186">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="30f83-187">Abra o [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="30f83-187">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="30f83-188">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="30f83-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30f83-189">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30f83-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30f83-190">clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30f83-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30f83-191">clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**.</span><span class="sxs-lookup"><span data-stu-id="30f83-191">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="30f83-192">clique em **Aplicativo inexistente na galeria.**</span><span class="sxs-lookup"><span data-stu-id="30f83-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="30f83-193">Insira o nome do aplicativo na caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="30f83-193">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="30f83-194">Selecione **Adicionar.**</span><span class="sxs-lookup"><span data-stu-id="30f83-194">Select **Add.**</span></span>

<span data-ttu-id="30f83-195">Após um curto período de tempo, você poderá ver a folha de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30f83-195">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="30f83-196">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="30f83-196">Configure the application for password single sign-on</span></span>

<span data-ttu-id="30f83-197">Para configurar o logon único para um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="30f83-197">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="30f83-198">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="30f83-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="30f83-199">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="30f83-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30f83-200">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30f83-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30f83-201">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30f83-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30f83-202">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="30f83-202">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="30f83-203">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="30f83-203">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="30f83-204">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="30f83-204">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="30f83-205">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30f83-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="30f83-206">Selecione o modo **Logon baseado em senha.**</span><span class="sxs-lookup"><span data-stu-id="30f83-206">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="30f83-207">Insira a **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="30f83-207">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="30f83-208">Trata-se da URL em que os usuários inserem o nome de usuário e senha para entrar.</span><span class="sxs-lookup"><span data-stu-id="30f83-208">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="30f83-209">Verifique se os campos de entrada estão visíveis na URL.</span><span class="sxs-lookup"><span data-stu-id="30f83-209">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="30f83-210">Atribuir usuários a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30f83-210">Assign users to the application.</span></span>

11. <span data-ttu-id="30f83-211">Além disso, também é possível fornecer credenciais em nome do usuário selecionando as linhas dos usuários, clicando em **Atualizar Credenciais** e digitando o nome de usuário e a senha em nome dos usuários.</span><span class="sxs-lookup"><span data-stu-id="30f83-211">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="30f83-212">Caso contrário, os usuários serão solicitados a inserir as próprias credenciais na inicialização.</span><span class="sxs-lookup"><span data-stu-id="30f83-212">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="30f83-213">Como atribuir um usuário diretamente a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="30f83-213">How to assign a user to an application directly</span></span>

<span data-ttu-id="30f83-214">Para atribuir um ou mais usuários diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="30f83-214">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="30f83-215">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="30f83-215">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="30f83-216">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="30f83-216">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30f83-217">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30f83-217">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30f83-218">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30f83-218">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30f83-219">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="30f83-219">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="30f83-220">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="30f83-220">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="30f83-221">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="30f83-221">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="30f83-222">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30f83-222">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="30f83-223">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="30f83-223">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="30f83-224">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="30f83-224">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="30f83-225">Digite o **nome completo** ou o **endereço de email** do usuário que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="30f83-225">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="30f83-226">Passe o mouse sobre o **usuário** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="30f83-226">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="30f83-227">Clique na caixa de seleção ao lado do logotipo ou da foto de perfil do usuário para adicioná-lo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="30f83-227">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="30f83-228">**Opcional:** caso queira **adicionar mais de um usuário**, digite outro **nome completo** ou **endereço de email** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse usuário à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="30f83-228">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="30f83-229">Ao concluir a seleção dos usuários, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="30f83-229">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="30f83-230">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="30f83-230">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="30f83-231">Clique no botão **Atribuir** para atribuir o aplicativo aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="30f83-231">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="30f83-232">Após um breve período, os usuários selecionados poderão iniciar esses aplicativos no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="30f83-232">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="30f83-233">Se essas etapas de solução de problemas não resolverem o problema.</span><span class="sxs-lookup"><span data-stu-id="30f83-233">If these troubleshooting steps do not the resolve the issue.</span></span> 

<span data-ttu-id="30f83-234">Abra um tíquete de suporte com as informações a seguir, se estiverem disponíveis:</span><span class="sxs-lookup"><span data-stu-id="30f83-234">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="30f83-235">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="30f83-235">Correlation error ID</span></span>

-   <span data-ttu-id="30f83-236">UPN (endereço de email de usuário)</span><span class="sxs-lookup"><span data-stu-id="30f83-236">UPN (user email address)</span></span>

-   <span data-ttu-id="30f83-237">TenantID</span><span class="sxs-lookup"><span data-stu-id="30f83-237">TenantID</span></span>

-   <span data-ttu-id="30f83-238">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="30f83-238">Browser type</span></span>

-   <span data-ttu-id="30f83-239">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="30f83-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="30f83-240">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="30f83-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="30f83-241">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="30f83-241">Next steps</span></span>
[<span data-ttu-id="30f83-242">Fornecer logon único para seus aplicativos com Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="30f83-242">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
