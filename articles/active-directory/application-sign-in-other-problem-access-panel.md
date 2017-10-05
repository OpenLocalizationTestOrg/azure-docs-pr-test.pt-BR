---
title: Problemas para entrar em um aplicativo a partir do Painel de Acesso| Microsoft Docs
description: Como solucionar problemas de acesso a um aplicativo a partir do Painel de Acesso do Microsoft Azure AD em myapps.microsoft.com
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
ms.reviewer: japere
ms.openlocfilehash: 188a00db59b0aa8d26facc678fb52d96272183b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-from-the-access-panel"></a><span data-ttu-id="46623-103">Problemas para entrar em um aplicativo a partir do Painel de Acesso</span><span class="sxs-lookup"><span data-stu-id="46623-103">Problems signing in to an application from the access panel</span></span>

<span data-ttu-id="46623-104">O Painel de Acesso é um portal baseado na Web que permite a um usuário com uma conta corporativa ou de estudante no Azure Active Directory (Azure AD) exibir e iniciar aplicativos baseados em nuvem para os quais o administrador do Azure AD concedeu acesso.</span><span class="sxs-lookup"><span data-stu-id="46623-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="46623-105">Esses aplicativos são configurados em nome do usuário no portal do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46623-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="46623-106">O aplicativo deve ser configurado corretamente e atribuído ao usuário ou a um grupo no qual o usuário é membro para ver o aplicativo no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="46623-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="46623-107">Os tipos de aplicativos que um usuário pode ver se enquadram nas categorias a seguir:</span><span class="sxs-lookup"><span data-stu-id="46623-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="46623-108">Aplicativos do Office 365</span><span class="sxs-lookup"><span data-stu-id="46623-108">Office 365 Applications</span></span>

-   <span data-ttu-id="46623-109">Aplicativos da Microsoft e de terceiros configurados com o SSO baseado em federação</span><span class="sxs-lookup"><span data-stu-id="46623-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="46623-110">Aplicativos de SSO baseadas em senhas</span><span class="sxs-lookup"><span data-stu-id="46623-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="46623-111">Aplicativos com soluções de SSO existentes</span><span class="sxs-lookup"><span data-stu-id="46623-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="46623-112">Questões gerais que primeiro devem ser verificadas</span><span class="sxs-lookup"><span data-stu-id="46623-112">General issues to check first</span></span>

-   <span data-ttu-id="46623-113">Verifique se você está usando um **navegador** que atenda aos requisitos mínimos para o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="46623-113">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="46623-114">Verifique se o navegador do usuário adicionou a URL do aplicativo ao seus **sites confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="46623-114">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="46623-115">Verifique se o aplicativo está **configurado** corretamente.</span><span class="sxs-lookup"><span data-stu-id="46623-115">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="46623-116">Verifique se a conta do usuário está **habilitada** para entradas.</span><span class="sxs-lookup"><span data-stu-id="46623-116">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="46623-117">Verifique se a conta do usuário **não está bloqueada.**</span><span class="sxs-lookup"><span data-stu-id="46623-117">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="46623-118">Verifique se a **senha do usuário não expirou ou foi esquecida.**</span><span class="sxs-lookup"><span data-stu-id="46623-118">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="46623-119">Verifique se a **Autenticação Multifator** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="46623-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="46623-120">Verifique se uma **Política de acesso condicional** ou política de **Proteção de Identidade** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="46623-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="46623-121">Verifique se as **informações de contato de autenticação** de um usuário estão atualizadas para permitir a aplicação da Autenticação Multifator ou de políticas de Acesso Condicional.</span><span class="sxs-lookup"><span data-stu-id="46623-121">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="46623-122">Tente também eliminar os cookies do navegador e tente entrar novamente.</span><span class="sxs-lookup"><span data-stu-id="46623-122">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="46623-123">Atender aos requisitos de navegador para o Painel de Acesso</span><span class="sxs-lookup"><span data-stu-id="46623-123">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="46623-124">O Painel de Acesso exige um navegador com suporte para JavaScript e CSS habilitado.</span><span class="sxs-lookup"><span data-stu-id="46623-124">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="46623-125">Para usar o SSO (logon único) baseado em senha no Painel de Acesso, a extensão do Painel de Acesso deve estar instalada no navegador do usuário.</span><span class="sxs-lookup"><span data-stu-id="46623-125">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="46623-126">Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.</span><span class="sxs-lookup"><span data-stu-id="46623-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="46623-127">Para SSO baseado em senha, os navegadores do usuário final podem ser:</span><span class="sxs-lookup"><span data-stu-id="46623-127">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="46623-128">Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior</span><span class="sxs-lookup"><span data-stu-id="46623-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="46623-129">Edge no Windows 10 Anniversary Edition ou posterior</span><span class="sxs-lookup"><span data-stu-id="46623-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="46623-130">Chrome – No Windows 7 ou posterior e no MacOS X ou posterior</span><span class="sxs-lookup"><span data-stu-id="46623-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="46623-131">Firefox 26.0 ou posterior, no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior</span><span class="sxs-lookup"><span data-stu-id="46623-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="46623-132">Como instalar a extensão do Navegador do Painel de Acesso</span><span class="sxs-lookup"><span data-stu-id="46623-132">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="46623-133">Para instalar a extensão do Navegador do Painel de Acesso, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="46623-133">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-134">Abra o [Painel de Acesso](https://myapps.microsoft.com) em um dos navegadores compatíveis e entre como um **usuário** no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46623-134">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="46623-135">Clique em um **aplicativo de SSO com senha** no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="46623-135">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="46623-136">No prompt solicitando a instalação do software, selecione **Instalar Agora**.</span><span class="sxs-lookup"><span data-stu-id="46623-136">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="46623-137">Com base no seu navegador, você será direcionado para o link de download.</span><span class="sxs-lookup"><span data-stu-id="46623-137">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="46623-138">**Adicione** a extensão ao seu navegador.</span><span class="sxs-lookup"><span data-stu-id="46623-138">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="46623-139">Se o navegador solicitar, selecione como **Habilitar** ou **Permitir** a extensão.</span><span class="sxs-lookup"><span data-stu-id="46623-139">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="46623-140">Quando estiver instalado, **reinicie** a sessão do navegador.</span><span class="sxs-lookup"><span data-stu-id="46623-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="46623-141">Entrar no Painel de Acesso e verificar se é possível **iniciar** os aplicativos de SSO de senha</span><span class="sxs-lookup"><span data-stu-id="46623-141">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="46623-142">Também é possível baixar a extensão para Chrome e Edge diretamente pelos links abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-142">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="46623-143">Extensão do Painel de Acesso do Chrome</span><span class="sxs-lookup"><span data-stu-id="46623-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="46623-144">Extensão do Painel de Acesso do Edge</span><span class="sxs-lookup"><span data-stu-id="46623-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="46623-145">Como configurar o logon único federado para um aplicativo na galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="46623-145">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="46623-146">Todos os aplicativos na galeria do Azure AD habilitados com o recurso de Logon Único Corporativo possuem um tutorial passo a passo disponível.</span><span class="sxs-lookup"><span data-stu-id="46623-146">All application in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="46623-147">É possível acessar a [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para uma orientação passo a passo detalhada.</span><span class="sxs-lookup"><span data-stu-id="46623-147">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="46623-148">Para configurar um aplicativo da galeria do Azure AD será necessário:</span><span class="sxs-lookup"><span data-stu-id="46623-148">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="46623-149">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="46623-149">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="46623-150">Configurar os valores de metadados do aplicativo no Azure AD (URL de Logon, Identificador, URL de Resposta)</span><span class="sxs-lookup"><span data-stu-id="46623-150">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="46623-151">Selecionar o Identificador de Usuário e adicionar os atributos de usuário a serem enviados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="46623-151">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="46623-152">Recuperar certificado e metadados Azure AD</span><span class="sxs-lookup"><span data-stu-id="46623-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="46623-153">Configurar os valores de metadados do Azure AD no aplicativo (URL de Logon, Emissor, URL de Logoff e certificado)</span><span class="sxs-lookup"><span data-stu-id="46623-153">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="46623-154">Atribuir usuários ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="46623-154">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="46623-155">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="46623-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="46623-156">Para adicionar um aplicativo da Galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-157">Abra o [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="46623-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="46623-158">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="46623-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46623-159">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46623-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46623-160">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46623-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46623-161">Clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**</span><span class="sxs-lookup"><span data-stu-id="46623-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="46623-162">Na caixa de texto **Inserir um nome** da seção **Adicionar da galeria**, digite o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="46623-163">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="46623-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="46623-164">Antes de adicionar o aplicativo, é possível alterar seu nome pela caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="46623-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="46623-165">Clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="46623-166">Após um curto período de tempo, você poderá ver a folha de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="46623-167">Configurar o logon único para um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="46623-167">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="46623-168">Para configurar o logon único para um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="46623-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="46623-170">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="46623-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46623-171">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46623-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46623-172">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46623-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46623-173">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="46623-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="46623-174">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="46623-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="46623-175">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="46623-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="46623-176">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="46623-177">Selecione **Logon com base em SAML** da lista suspensa **Modo**.</span><span class="sxs-lookup"><span data-stu-id="46623-177">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="46623-178">Insira os valores necessários em **Domínio e URLs.**</span><span class="sxs-lookup"><span data-stu-id="46623-178">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="46623-179">É possível obter esses valores do fornecedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-179">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="46623-180">Para configurar o aplicativo como SSO iniciado por SP, a URL de Logon é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="46623-180">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="46623-181">Para alguns aplicativos, o Identificador também é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="46623-181">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="46623-182">Para configurar o aplicativo como SSO iniciado por IdP, a URL de Resposta é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="46623-182">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="46623-183">Para alguns aplicativos, o Identificador também é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="46623-183">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="46623-184">**Opcional:** clique **Mostrar configurações avançadas de URL** se quiser ver os valores não obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="46623-184">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="46623-185">Nos **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="46623-185">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="46623-186">**Opcional:** clique em **Exibir e editar todos os outros atributos de usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="46623-186">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="46623-187">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="46623-187">To add an attribute:</span></span>

   1. <span data-ttu-id="46623-188">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="46623-188">click **Add attribute**.</span></span> <span data-ttu-id="46623-189">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="46623-189">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="46623-190">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="46623-190">Click **Save.**</span></span> <span data-ttu-id="46623-191">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="46623-191">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="46623-192">clique em **Configurar &lt;nome do aplicativo&gt;**  para acessar a documentação sobre como configurar o logon único no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-192">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="46623-193">Além disso, você tem URLs de metadados e o certificado necessários para configurar o SSO com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-193">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="46623-194">Clique em **Salvar** para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="46623-194">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="46623-195">Atribuir usuários a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-195">Assign users to the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="46623-196">Selecionar o Identificador de Usuário e adicionar os atributos de usuário a serem enviados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="46623-196">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="46623-197">Para selecionar o Identificador de Usuário ou adicionar os atributos de usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-197">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-198">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="46623-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="46623-199">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="46623-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46623-200">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46623-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46623-201">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46623-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46623-202">clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="46623-202">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="46623-203">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="46623-203">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="46623-204">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="46623-204">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="46623-205">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="46623-206">Na seção **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="46623-206">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="46623-207">A opção selecionada precisa corresponder ao valor esperado no aplicativo para autenticar o usuário.</span><span class="sxs-lookup"><span data-stu-id="46623-207">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="46623-208">O Azure AD seleciona o formato para o atributo NameID (Identificador de Usuário) com base no valor selecionado ou no formato solicitado pelo aplicativo no AuthRequest do SAML.</span><span class="sxs-lookup"><span data-stu-id="46623-208">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="46623-209">Para obter mais informações, consulte o artigo [Protocolo SAML de Logon Único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="46623-209">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="46623-210">Para adicionar atributos de usuário, clique em **Exibir e editar todos os outros atributos de usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="46623-210">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="46623-211">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="46623-211">To add an attribute:</span></span>

   1. <span data-ttu-id="46623-212">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="46623-212">click **Add attribute**.</span></span> <span data-ttu-id="46623-213">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="46623-213">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="46623-214">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="46623-214">Click **Save.**</span></span> <span data-ttu-id="46623-215">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="46623-215">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="46623-216">Baixar o certificado ou metadados do Azure AD</span><span class="sxs-lookup"><span data-stu-id="46623-216">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="46623-217">Para baixar o certificado ou metadados do aplicativo Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-217">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-218">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="46623-218">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="46623-219">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="46623-219">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46623-220">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46623-220">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46623-221">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46623-221">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46623-222">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="46623-222">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="46623-223">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="46623-223">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="46623-224">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="46623-224">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="46623-225">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-225">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="46623-226">Vá para a seção **Certificado de Autenticação SAML** e, em seguida, clique no valor da coluna **Download**.</span><span class="sxs-lookup"><span data-stu-id="46623-226">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="46623-227">Dependendo do aplicativo que exigir a configuração de logon único, você verá a opção para baixar o Certificado ou o XML de Metadados.</span><span class="sxs-lookup"><span data-stu-id="46623-227">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="46623-228">O Azure AD não fornece uma URL para obter os metadados.</span><span class="sxs-lookup"><span data-stu-id="46623-228">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="46623-229">Os metadados apenas podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="46623-229">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="46623-230">Como configurar o logon único federado para um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="46623-230">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="46623-231">Para configurar um aplicativo inexistente na galeria, é necessário ter o Azure AD Premium e o aplicativo com suporte SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="46623-231">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="46623-232">Para obter mais informações sobre as versões do Azure AD, visite [Preços do Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="46623-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="46623-233">Configurar os valores de metadados do aplicativo no Azure AD (URL de Logon, Identificador, URL de Resposta)</span><span class="sxs-lookup"><span data-stu-id="46623-233">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="46623-234">Selecionar o Identificador de Usuário e adicionar os atributos de usuário a serem enviados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="46623-234">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="46623-235">Recuperar certificado e metadados Azure AD</span><span class="sxs-lookup"><span data-stu-id="46623-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="46623-236">Configurar os valores de metadados do Azure AD no aplicativo (URL de Logon, Emissor, URL de Logoff e certificado)</span><span class="sxs-lookup"><span data-stu-id="46623-236">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="46623-237">Configurar os valores de metadados do aplicativo no Azure AD (URL de Logon, Identificador, URL de Resposta)</span><span class="sxs-lookup"><span data-stu-id="46623-237">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="46623-238">Para configurar o logon único para um aplicativo que não está na galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-238">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-239">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="46623-239">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="46623-240">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="46623-240">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46623-241">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46623-241">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46623-242">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46623-242">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46623-243">clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**</span><span class="sxs-lookup"><span data-stu-id="46623-243">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="46623-244">clique em **Aplicativo inexistente na galeria** na seção **Adicionar seu próprio aplicativo**</span><span class="sxs-lookup"><span data-stu-id="46623-244">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="46623-245">Digite o nome do aplicativo na caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="46623-245">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="46623-246">Clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-246">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="46623-247">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-247">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="46623-248">Selecione **Logon com base em SAML** na lista suspensa **Modo**</span><span class="sxs-lookup"><span data-stu-id="46623-248">Select **SAML-based Sign-on** in the **Mode** dropdown</span></span>

11. <span data-ttu-id="46623-249">Insira os valores necessários em **Domínio e URLs.**</span><span class="sxs-lookup"><span data-stu-id="46623-249">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="46623-250">É possível obter esses valores do fornecedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-250">You should get these values from the application vendor.</span></span>

  1. <span data-ttu-id="46623-251">Para configurar o aplicativo como SSO iniciado por IdP, insira a URL de Resposta e o Identificador.</span><span class="sxs-lookup"><span data-stu-id="46623-251">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

  2. <span data-ttu-id="46623-252">**Opcional:** Para configurar o aplicativo como SSO iniciado por SP, a URL de Logon é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="46623-252">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="46623-253">Nos **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="46623-253">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="46623-254">**Opcional:** clique em **Exibir e editar todos os outros atributos de usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="46623-254">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="46623-255">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="46623-255">To add an attribute:</span></span>

   1. <span data-ttu-id="46623-256">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="46623-256">click **Add attribute**.</span></span> <span data-ttu-id="46623-257">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="46623-257">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="46623-258">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="46623-258">Click **Save.**</span></span> <span data-ttu-id="46623-259">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="46623-259">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="46623-260">clique em **Configurar &lt;nome do aplicativo&gt;**  para acessar a documentação sobre como configurar o logon único no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-260">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="46623-261">Além disso, você tem URLs do Azure AD e o certificado necessários para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-261">Also, you has Azure AD URLs and certificate required for the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="46623-262">Selecionar o Identificador de Usuário e adicionar os atributos de usuário a serem enviados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="46623-262">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="46623-263">Para selecionar o Identificador de Usuário ou adicionar os atributos de usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-263">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-264">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="46623-264">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="46623-265">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="46623-265">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46623-266">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46623-266">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46623-267">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46623-267">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46623-268">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="46623-268">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="46623-269">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="46623-269">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="46623-270">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="46623-270">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="46623-271">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-271">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="46623-272">Na seção **Atributos de usuário**, selecione o identificador exclusivo para os usuários na lista suspensa **Identificador de usuário**.</span><span class="sxs-lookup"><span data-stu-id="46623-272">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="46623-273">A opção selecionada precisa corresponder ao valor esperado no aplicativo para autenticar o usuário.</span><span class="sxs-lookup"><span data-stu-id="46623-273">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="46623-274">O Azure AD seleciona o formato para o atributo NameID (Identificador de Usuário) com base no valor selecionado ou no formato solicitado pelo aplicativo no AuthRequest do SAML.</span><span class="sxs-lookup"><span data-stu-id="46623-274">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="46623-275">Para obter mais informações, consulte o artigo [Protocolo SAML de Logon Único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="46623-275">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="46623-276">Para adicionar atributos de usuário, clique em **Exibir e editar todos os outros atributos de usuário** para editar os atributos a serem enviados ao aplicativo no token SAML quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="46623-276">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="46623-277">Para adicionar um atributo:</span><span class="sxs-lookup"><span data-stu-id="46623-277">To add an attribute:</span></span>

   <span data-ttu-id="46623-278">1. Clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="46623-278">1.click **Add attribute**.</span></span> <span data-ttu-id="46623-279">Insira o **Nome** e selecione o **Valor** da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="46623-279">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   <span data-ttu-id="46623-280">2 Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="46623-280">2 Click **Save.**</span></span> <span data-ttu-id="46623-281">Você verá o novo atributo na tabela.</span><span class="sxs-lookup"><span data-stu-id="46623-281">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="46623-282">Baixar o certificado ou metadados do Azure AD</span><span class="sxs-lookup"><span data-stu-id="46623-282">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="46623-283">Para baixar o certificado ou metadados do aplicativo Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-283">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-284">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="46623-284">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="46623-285">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="46623-285">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46623-286">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46623-286">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46623-287">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46623-287">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46623-288">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="46623-288">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="46623-289">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="46623-289">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="46623-290">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="46623-290">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="46623-291">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-291">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="46623-292">Vá para a seção **Certificado de Autenticação SAML** e, em seguida, clique no valor da coluna **Download**.</span><span class="sxs-lookup"><span data-stu-id="46623-292">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="46623-293">Dependendo do aplicativo que exigir a configuração de logon único, você verá a opção para baixar o Certificado ou o XML de Metadados.</span><span class="sxs-lookup"><span data-stu-id="46623-293">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="46623-294">O Azure AD não fornece uma URL para obter os metadados.</span><span class="sxs-lookup"><span data-stu-id="46623-294">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="46623-295">Os metadados apenas podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="46623-295">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="46623-296">Como configurar o login único com senha para um aplicativo na galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="46623-296">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="46623-297">Para configurar um aplicativo da galeria do Azure AD será necessário:</span><span class="sxs-lookup"><span data-stu-id="46623-297">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="46623-298">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="46623-298">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="46623-299">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="46623-299">Configure the application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="46623-300">Adicionar um aplicativo da galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="46623-300">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="46623-301">Para adicionar um aplicativo da Galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-301">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-302">Abra o [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="46623-302">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="46623-303">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="46623-303">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46623-304">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46623-304">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46623-305">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46623-305">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46623-306">Clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**</span><span class="sxs-lookup"><span data-stu-id="46623-306">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="46623-307">Na caixa de texto **Inserir um nome** da seção **Adicionar da galeria**, digite o nome do aplicativo</span><span class="sxs-lookup"><span data-stu-id="46623-307">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="46623-308">Selecione o aplicativo para o qual deseja configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="46623-308">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="46623-309">Antes de adicionar o aplicativo, é possível alterar seu nome na caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="46623-309">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="46623-310">Clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-310">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="46623-311">Após um breve período, você verá a folha de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-311">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="46623-312">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="46623-312">Configure the application for password single sign-on</span></span>

<span data-ttu-id="46623-313">Para configurar o logon único para um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-313">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-314">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="46623-314">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="46623-315">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="46623-315">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46623-316">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46623-316">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46623-317">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46623-317">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46623-318">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="46623-318">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="46623-319">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="46623-319">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="46623-320">Selecione o aplicativo para o qual deseja configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="46623-320">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="46623-321">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-321">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="46623-322">Selecione o modo **Logon baseado em Senha.**</span><span class="sxs-lookup"><span data-stu-id="46623-322">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="46623-323">Atribuir usuários a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-323">Assign users to the application.</span></span>

10. <span data-ttu-id="46623-324">Além disso, também é possível fornecer credenciais em nome do usuário selecionando as linhas dos usuários, clicando em **Atualizar Credenciais** e digitando o nome de usuário e a senha em nome dos usuários.</span><span class="sxs-lookup"><span data-stu-id="46623-324">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="46623-325">Caso contrário, os usuários serão solicitados a inserir as próprias credenciais na inicialização.</span><span class="sxs-lookup"><span data-stu-id="46623-325">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="46623-326">Como configurar o logon único com senha para um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="46623-326">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="46623-327">Para configurar um aplicativo da galeria do Azure AD será necessário:</span><span class="sxs-lookup"><span data-stu-id="46623-327">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="46623-328">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="46623-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="46623-329">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="46623-329">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="46623-330">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="46623-330">Add a non-gallery application</span></span>

<span data-ttu-id="46623-331">Para adicionar um aplicativo da galeria do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-331">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-332">Abra o [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="46623-332">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="46623-333">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="46623-333">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46623-334">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46623-334">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46623-335">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46623-335">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46623-336">Clique no botão **Adicionar** no canto superior direito da folha **Aplicativos Empresariais**</span><span class="sxs-lookup"><span data-stu-id="46623-336">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="46623-337">clique em **Aplicativo inexistente na galeria.**</span><span class="sxs-lookup"><span data-stu-id="46623-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="46623-338">Insira o nome do aplicativo na caixa de texto **Nome**.</span><span class="sxs-lookup"><span data-stu-id="46623-338">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="46623-339">Selecione **Adicionar.**</span><span class="sxs-lookup"><span data-stu-id="46623-339">Select **Add.**</span></span>

<span data-ttu-id="46623-340">Após um curto período de tempo, você poderá ver a folha de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-340">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="46623-341">Configurar o aplicativo para logon único com senha</span><span class="sxs-lookup"><span data-stu-id="46623-341">Configure the application for password single sign-on</span></span>

<span data-ttu-id="46623-342">Para configurar o logon único para um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-342">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-343">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="46623-343">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="46623-344">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="46623-344">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46623-345">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46623-345">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46623-346">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46623-346">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46623-347">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="46623-347">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="46623-348">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="46623-348">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="46623-349">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="46623-349">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="46623-350">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-350">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="46623-351">Selecione o modo **Logon baseado em senha.**</span><span class="sxs-lookup"><span data-stu-id="46623-351">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="46623-352">Insira a **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="46623-352">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="46623-353">Trata-se da URL em que os usuários inserem o nome de usuário e senha para entrar.</span><span class="sxs-lookup"><span data-stu-id="46623-353">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="46623-354">Verifique se os campos de entrada estão visíveis na URL.</span><span class="sxs-lookup"><span data-stu-id="46623-354">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="46623-355">Atribuir usuários a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-355">Assign users to the application.</span></span>

11. <span data-ttu-id="46623-356">Além disso, também é possível fornecer credenciais em nome do usuário selecionando as linhas dos usuários, clicando em **Atualizar Credenciais** e digitando o nome de usuário e a senha em nome dos usuários.</span><span class="sxs-lookup"><span data-stu-id="46623-356">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="46623-357">Caso contrário, os usuários serão solicitados a inserir as próprias credenciais na inicialização.</span><span class="sxs-lookup"><span data-stu-id="46623-357">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="46623-358">Como atribuir um usuário diretamente a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="46623-358">How to assign a user to an application directly</span></span>

<span data-ttu-id="46623-359">Para atribuir um ou mais usuários diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="46623-359">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="46623-360">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="46623-360">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="46623-361">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="46623-361">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="46623-362">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46623-362">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="46623-363">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46623-363">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="46623-364">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="46623-364">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="46623-365">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="46623-365">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="46623-366">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="46623-366">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="46623-367">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-367">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="46623-368">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="46623-368">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="46623-369">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="46623-369">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="46623-370">Digite o **nome completo** ou o **endereço de email** do usuário que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="46623-370">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="46623-371">Passe o mouse sobre o **usuário** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="46623-371">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="46623-372">Clique na caixa de seleção ao lado do logotipo ou da foto de perfil do usuário para adicioná-lo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="46623-372">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="46623-373">**Opcional:** caso queira **adicionar mais de um usuário**, digite outro **nome completo** ou **endereço de email** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse usuário à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="46623-373">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="46623-374">Ao concluir a seleção dos usuários, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46623-374">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="46623-375">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="46623-375">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="46623-376">Clique no botão **Atribuir** para atribuir o aplicativo aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="46623-376">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="46623-377">Após um breve período, os usuários selecionados poderão iniciar esses aplicativos no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="46623-377">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="46623-378">Se essas etapas de solução de problemas não resolverem o problema</span><span class="sxs-lookup"><span data-stu-id="46623-378">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="46623-379">Abra um tíquete de suporte com as informações a seguir, se estiverem disponíveis:</span><span class="sxs-lookup"><span data-stu-id="46623-379">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="46623-380">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="46623-380">Correlation error ID</span></span>

-   <span data-ttu-id="46623-381">UPN (endereço de email de usuário)</span><span class="sxs-lookup"><span data-stu-id="46623-381">UPN (user email address)</span></span>

-   <span data-ttu-id="46623-382">TenantID</span><span class="sxs-lookup"><span data-stu-id="46623-382">TenantID</span></span>

-   <span data-ttu-id="46623-383">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="46623-383">Browser type</span></span>

-   <span data-ttu-id="46623-384">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="46623-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="46623-385">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="46623-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="46623-386">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46623-386">Next steps</span></span>
[<span data-ttu-id="46623-387">Fornecer logon único para seus aplicativos com Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="46623-387">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

