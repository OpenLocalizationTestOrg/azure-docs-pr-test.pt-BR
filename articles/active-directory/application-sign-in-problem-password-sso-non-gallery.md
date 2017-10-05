---
title: "Problemas ao entrar em um aplicativo na Galeria do Azure AD configurado para logon único com senha | Microsoft Docs"
description: "Discute as áreas problemáticas que fornecem diretrizes para solucionar problemas relacionados à entrada em aplicativos da Galeria do Azure AD configurados para login único com senha"
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
ms.openlocfilehash: c90b61812affb7e7af05cf3e302d045958da59be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="d8f13-103">Problemas ao entrar em um aplicativo na Galeria do Azure AD configurado para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="d8f13-103">Problems signing in to an Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="d8f13-104">O Painel de Acesso é um portal baseado na Web que permite a um usuário que tenha uma conta corporativa ou de estudante no Azure Active Directory (Azure AD) exibir e iniciar aplicativos baseados em nuvem para os quais o administrador do Azure AD concedeu acesso.</span><span class="sxs-lookup"><span data-stu-id="d8f13-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="d8f13-105">Um usuário com as edições do Azure AD também pode usar os recursos de gerenciamento de grupo de autoatendimento e aplicativo por meio do Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="d8f13-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="d8f13-106">O Painel de Acesso é separado do Portal do Azure e não exige que os usuários tenham uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8f13-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="d8f13-107">Para usar o SSO (logon único) baseado em senha no Painel de Acesso, a extensão do Painel de Acesso deve estar instalada no navegador do usuário.</span><span class="sxs-lookup"><span data-stu-id="d8f13-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="d8f13-108">Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.</span><span class="sxs-lookup"><span data-stu-id="d8f13-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="d8f13-109">Atender aos requisitos de navegador para o Painel de Acesso</span><span class="sxs-lookup"><span data-stu-id="d8f13-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="d8f13-110">O Painel de Acesso exige um navegador com suporte para JavaScript e CSS habilitado.</span><span class="sxs-lookup"><span data-stu-id="d8f13-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="d8f13-111">Para usar o SSO (logon único) baseado em senha no Painel de Acesso, a extensão do Painel de Acesso deve estar instalada no navegador do usuário.</span><span class="sxs-lookup"><span data-stu-id="d8f13-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="d8f13-112">Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.</span><span class="sxs-lookup"><span data-stu-id="d8f13-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="d8f13-113">Para SSO baseado em senha, os navegadores do usuário final podem ser:</span><span class="sxs-lookup"><span data-stu-id="d8f13-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="d8f13-114">Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior</span><span class="sxs-lookup"><span data-stu-id="d8f13-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="d8f13-115">Chrome – No Windows 7 ou posterior e no MacOS X ou posterior</span><span class="sxs-lookup"><span data-stu-id="d8f13-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="d8f13-116">Firefox 26.0 ou posterior, no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior</span><span class="sxs-lookup"><span data-stu-id="d8f13-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="d8f13-117">A extensão de SSO baseada em senha será disponibilizada para o Edge no Windows 10 quando as extensões de navegador tiverem suporte no Edge.</span><span class="sxs-lookup"><span data-stu-id="d8f13-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="d8f13-118">Como instalar a extensão do Navegador do Painel de Acesso</span><span class="sxs-lookup"><span data-stu-id="d8f13-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="d8f13-119">Para instalar a extensão do Navegador do Painel de Acesso, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8f13-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="d8f13-120">Abra o [Painel de Acesso](https://myapps.microsoft.com) em um dos navegadores compatíveis e entre como um **usuário** no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8f13-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="d8f13-121">Clique no **aplicativo de SSO com senha** no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="d8f13-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="d8f13-122">No prompt solicitando a instalação do software, selecione **Instalar Agora**.</span><span class="sxs-lookup"><span data-stu-id="d8f13-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="d8f13-123">Com base no seu navegador, você será direcionado para o link de download.</span><span class="sxs-lookup"><span data-stu-id="d8f13-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="d8f13-124">**Adicione** a extensão ao seu navegador.</span><span class="sxs-lookup"><span data-stu-id="d8f13-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="d8f13-125">Se o navegador solicitar, selecione como **Habilitar** ou **Permitir** a extensão.</span><span class="sxs-lookup"><span data-stu-id="d8f13-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="d8f13-126">Quando estiver instalado, **reinicie** a sessão do navegador.</span><span class="sxs-lookup"><span data-stu-id="d8f13-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="d8f13-127">Entrar no Painel de Acesso e verificar se é possível **iniciar** os aplicativos de SSO de senha</span><span class="sxs-lookup"><span data-stu-id="d8f13-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="d8f13-128">Também é possível baixar a extensão para Chrome e Firefox diretamente pelos links abaixo:</span><span class="sxs-lookup"><span data-stu-id="d8f13-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="d8f13-129">Extensão do Painel de Acesso do Chrome</span><span class="sxs-lookup"><span data-stu-id="d8f13-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="d8f13-130">Extensão do Painel de Acesso do Firefox</span><span class="sxs-lookup"><span data-stu-id="d8f13-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="d8f13-131">Configurar uma política de grupo para o Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="d8f13-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="d8f13-132">É possível configurar uma política de grupo que permita instalar remotamente a extensão do Painel de Acesso para o Internet Explorer nos computadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="d8f13-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="d8f13-133">Os pré-requisitos incluem:</span><span class="sxs-lookup"><span data-stu-id="d8f13-133">The prerequisites include:</span></span>

-   <span data-ttu-id="d8f13-134">Você configurou os [Serviços de Domínio do Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)e os computadores dos usuários ingressaram no domínio.</span><span class="sxs-lookup"><span data-stu-id="d8f13-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="d8f13-135">Você deve ter a permissão "Editar configurações" para editar o GPO (Objeto de Política de Grupo).</span><span class="sxs-lookup"><span data-stu-id="d8f13-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="d8f13-136">Por padrão, os membros dos grupos de segurança a seguir têm esta permissão: Administradores de Domínio, Administradores de Empresa e Proprietários Criadores de Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="d8f13-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="d8f13-137">[Saiba mais](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8f13-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="d8f13-138">Siga o tutorial [Como Implantar a Extensão do Painel de Acesso para o Internet Explorer usando Política de Grupo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) para obter instruções passo a passo sobre como configurar política de grupo e implantá-la nos usuários.</span><span class="sxs-lookup"><span data-stu-id="d8f13-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="d8f13-139">Solucionar problemas do Painel de Acesso no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="d8f13-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="d8f13-140">Siga o guia [Solucionar problemas da Extensão do Painel de Acesso para o Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) para acessar uma ferramenta de diagnóstico e as instruções passo a passo sobre como configurar a extensão para o IE.</span><span class="sxs-lookup"><span data-stu-id="d8f13-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="d8f13-141">Como configurar o logon único com senha para um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="d8f13-141">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="d8f13-142">Para configurar um aplicativo da galeria do Azure AD será necessário:</span><span class="sxs-lookup"><span data-stu-id="d8f13-142">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="d8f13-143">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="d8f13-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="d8f13-144">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="d8f13-144">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="d8f13-145">Atribuir usuários ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="d8f13-145">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="d8f13-146">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="d8f13-146">Add a non-gallery application</span></span>

<span data-ttu-id="d8f13-147">Para adicionar um aplicativo da galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="d8f13-147">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="d8f13-148">Abra o [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="d8f13-148">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="d8f13-149">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="d8f13-149">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d8f13-150">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8f13-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d8f13-151">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8f13-151">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d8f13-152">Clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**</span><span class="sxs-lookup"><span data-stu-id="d8f13-152">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="d8f13-153">clique em **Aplicativo inexistente na galeria.**</span><span class="sxs-lookup"><span data-stu-id="d8f13-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="d8f13-154">Insira o nome do aplicativo na caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="d8f13-154">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="d8f13-155">Selecione **Adicionar.**</span><span class="sxs-lookup"><span data-stu-id="d8f13-155">Select **Add.**</span></span>

<span data-ttu-id="d8f13-156">Após um curto período de tempo, você poderá ver a folha de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8f13-156">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="d8f13-157">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="d8f13-157">Configure the application for password single sign-on</span></span>

<span data-ttu-id="d8f13-158">Para configurar o logon único para um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="d8f13-158">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="d8f13-159">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="d8f13-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d8f13-160">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="d8f13-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d8f13-161">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8f13-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d8f13-162">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8f13-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d8f13-163">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d8f13-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="d8f13-164">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="d8f13-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d8f13-165">Selecione o aplicativo para o qual deseja configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="d8f13-165">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="d8f13-166">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8f13-166">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d8f13-167">Selecione o modo **Logon baseado em senha.**</span><span class="sxs-lookup"><span data-stu-id="d8f13-167">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="d8f13-168">Insira a **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="d8f13-168">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="d8f13-169">Trata-se da URL em que os usuários inserem o nome de usuário e senha para entrar.</span><span class="sxs-lookup"><span data-stu-id="d8f13-169">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="d8f13-170">Verifique se os campos de entrada estão visíveis na URL.</span><span class="sxs-lookup"><span data-stu-id="d8f13-170">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="d8f13-171">Atribuir usuários a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8f13-171">Assign users to the application.</span></span>

11. <span data-ttu-id="d8f13-172">Além disso, também é possível fornecer credenciais em nome do usuário selecionando as linhas dos usuários, clicando em **Atualizar Credenciais** e digitando o nome de usuário e a senha em nome dos usuários.</span><span class="sxs-lookup"><span data-stu-id="d8f13-172">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="d8f13-173">Caso contrário, os usuários serão solicitados a inserir as próprias credenciais na inicialização.</span><span class="sxs-lookup"><span data-stu-id="d8f13-173">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="assign-users-to-the-application"></a><span data-ttu-id="d8f13-174">Atribuir usuários ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="d8f13-174">Assign users to the application</span></span>

<span data-ttu-id="d8f13-175">Para atribuir um ou mais usuários diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="d8f13-175">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="d8f13-176">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="d8f13-176">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d8f13-177">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="d8f13-177">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d8f13-178">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8f13-178">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d8f13-179">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8f13-179">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d8f13-180">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d8f13-180">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="d8f13-181">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="d8f13-181">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d8f13-182">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="d8f13-182">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="d8f13-183">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8f13-183">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d8f13-184">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="d8f13-184">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d8f13-185">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="d8f13-185">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d8f13-186">Digite o **nome completo** ou o **endereço de email** do usuário que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="d8f13-186">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d8f13-187">Passe o mouse sobre o **usuário** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="d8f13-187">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="d8f13-188">Clique na caixa de seleção ao lado do logotipo ou da foto de perfil do usuário para adicioná-lo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="d8f13-188">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="d8f13-189">**Opcional:** caso queira **adicionar mais de um usuário**, digite outro **nome completo** ou **endereço de email** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse usuário à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="d8f13-189">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="d8f13-190">Ao concluir a seleção dos usuários, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8f13-190">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="d8f13-191">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="d8f13-191">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="d8f13-192">Clique no botão **Atribuir** para atribuir o aplicativo aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="d8f13-192">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="d8f13-193">Após um breve período, os usuários selecionados poderão iniciar esses aplicativos no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="d8f13-193">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="d8f13-194">Se essas etapas de solução de problemas não resolverem o problema</span><span class="sxs-lookup"><span data-stu-id="d8f13-194">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="d8f13-195">Abra um tíquete de suporte com as informações a seguir, se estiverem disponíveis:</span><span class="sxs-lookup"><span data-stu-id="d8f13-195">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="d8f13-196">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="d8f13-196">Correlation error ID</span></span>

-   <span data-ttu-id="d8f13-197">UPN (endereço de email de usuário)</span><span class="sxs-lookup"><span data-stu-id="d8f13-197">UPN (user email address)</span></span>

-   <span data-ttu-id="d8f13-198">TenantID</span><span class="sxs-lookup"><span data-stu-id="d8f13-198">TenantID</span></span>

-   <span data-ttu-id="d8f13-199">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="d8f13-199">Browser type</span></span>

-   <span data-ttu-id="d8f13-200">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="d8f13-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="d8f13-201">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="d8f13-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8f13-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8f13-202">Next steps</span></span>
[<span data-ttu-id="d8f13-203">Fornecer logon único para seus aplicativos com Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d8f13-203">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

