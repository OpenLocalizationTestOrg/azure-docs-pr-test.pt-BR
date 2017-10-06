---
title: "aaaProblems entrar no aplicativo tooan do painel de acesso de saudação | Microsoft Docs"
description: "Como acessar um aplicativo a partir de problemas de tootroubleshoot Olá painel de acesso do AD do Microsoft Azure em myapps.microsoft.com"
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
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a><span data-ttu-id="32662-103">Problemas para entrar no aplicativo tooan do painel de acesso de saudação</span><span class="sxs-lookup"><span data-stu-id="32662-103">Problems signing in tooan application from hello access panel</span></span>

<span data-ttu-id="32662-104">Olá painel de acesso é um portal baseado na web que permite que um usuário com um trabalho ou escola conta em aplicativos tooview e início baseado em nuvem do Azure Active Directory (AD do Azure) que Olá administrador do AD do Azure tem acesso-los ao.</span><span class="sxs-lookup"><span data-stu-id="32662-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="32662-105">Esses aplicativos são configurados em nome de usuário de saudação no portal do Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="32662-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="32662-106">aplicativo Hello deve ser configurado corretamente e atribuído toohello usuário ou grupo Olá é um membro de toosee aplicativo Olá Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="32662-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="32662-107">tipo Hello de aplicativos que um usuário pode ver se enquadram em Olá categorias a seguir:</span><span class="sxs-lookup"><span data-stu-id="32662-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="32662-108">Aplicativos do Office 365</span><span class="sxs-lookup"><span data-stu-id="32662-108">Office 365 Applications</span></span>

-   <span data-ttu-id="32662-109">Aplicativos da Microsoft e de terceiros configurados com o SSO baseado em federação</span><span class="sxs-lookup"><span data-stu-id="32662-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="32662-110">Aplicativos de SSO baseadas em senhas</span><span class="sxs-lookup"><span data-stu-id="32662-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="32662-111">Aplicativos com soluções de SSO existentes</span><span class="sxs-lookup"><span data-stu-id="32662-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="32662-112">Geral emite toocheck primeiro</span><span class="sxs-lookup"><span data-stu-id="32662-112">General issues toocheck first</span></span>

-   <span data-ttu-id="32662-113">Verifique se seu usando um **navegador** que atende aos requisitos mínimos Olá Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="32662-113">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="32662-114">Certifique-se de navegador do usuário Olá adicionou URL Olá Olá aplicativo tooits **sites confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="32662-114">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="32662-115">Certifique-se de aplicativo de hello toocheck é **configurado** corretamente.</span><span class="sxs-lookup"><span data-stu-id="32662-115">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="32662-116">Certifique-se de conta de usuário Olá **habilitado** para entradas.</span><span class="sxs-lookup"><span data-stu-id="32662-116">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="32662-117">Certifique-se de conta de usuário Olá **não bloqueada.**</span><span class="sxs-lookup"><span data-stu-id="32662-117">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="32662-118">Tornar-se de que usuário Olá **senha não está expirada ou esquecida.**</span><span class="sxs-lookup"><span data-stu-id="32662-118">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="32662-119">Verifique se a **Autenticação Multifator** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="32662-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="32662-120">Verifique se uma **Política de acesso condicional** ou política de **Proteção de Identidade** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="32662-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="32662-121">Certifique-se de que um usuário **informações de contato de autenticação** está ativo toodate tooallow autenticação multifator ou o acesso condicional políticas toobe imposta.</span><span class="sxs-lookup"><span data-stu-id="32662-121">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="32662-122">Verifique se tooalso tente eliminar os cookies do seu navegador e tentar toosign em novamente.</span><span class="sxs-lookup"><span data-stu-id="32662-122">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="32662-123">Atende aos requisitos de navegador de saudação painel de acesso</span><span class="sxs-lookup"><span data-stu-id="32662-123">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="32662-124">Olá painel de acesso requer um navegador que ofereça suporte ao JavaScript e CSS habilitou.</span><span class="sxs-lookup"><span data-stu-id="32662-124">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="32662-125">toouse baseado em senha-logon único (SSO) no hello painel de acesso, Olá extensão do painel de acesso deve ser instalado no navegador do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="32662-125">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="32662-126">Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.</span><span class="sxs-lookup"><span data-stu-id="32662-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="32662-127">Para SSO baseado em senha, navegadores de saudação do usuário podem ser:</span><span class="sxs-lookup"><span data-stu-id="32662-127">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="32662-128">Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior</span><span class="sxs-lookup"><span data-stu-id="32662-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="32662-129">Edge no Windows 10 Anniversary Edition ou posterior</span><span class="sxs-lookup"><span data-stu-id="32662-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="32662-130">Chrome – No Windows 7 ou posterior e no MacOS X ou posterior</span><span class="sxs-lookup"><span data-stu-id="32662-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="32662-131">Firefox 26.0 ou posterior, no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior</span><span class="sxs-lookup"><span data-stu-id="32662-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="32662-132">Como tooinstall Olá extensão de navegador do painel de acesso</span><span class="sxs-lookup"><span data-stu-id="32662-132">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="32662-133">Olá tooinstall extensão de navegador do painel de acesso, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-133">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-134">Olá abrir [painel de acesso](https://myapps.microsoft.com) em um dos navegadores Olá com suporte e entre como um **usuário** no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="32662-134">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="32662-135">Clique em uma **aplicativo SSO de senha** no painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-135">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="32662-136">Olá prompt perguntando tooinstall Olá software, selecione **instalar agora**.</span><span class="sxs-lookup"><span data-stu-id="32662-136">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="32662-137">Com base em seu navegador é direcionado toohello link para download.</span><span class="sxs-lookup"><span data-stu-id="32662-137">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="32662-138">**Adicionar** navegador de tooyour Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="32662-138">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="32662-139">Se seu navegador solicita, selecione tooeither **habilitar** ou **permitir** Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="32662-139">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="32662-140">Quando estiver instalado, **reinicie** a sessão do navegador.</span><span class="sxs-lookup"><span data-stu-id="32662-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="32662-141">Entrar painel de acesso de saudação e veja se é possível **iniciar** seus aplicativos de SSO de senha</span><span class="sxs-lookup"><span data-stu-id="32662-141">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="32662-142">Você também pode baixar a extensão Olá para Chrome e borda de links diretos da saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-142">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="32662-143">Extensão do Painel de Acesso do Chrome</span><span class="sxs-lookup"><span data-stu-id="32662-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="32662-144">Extensão do Painel de Acesso do Edge</span><span class="sxs-lookup"><span data-stu-id="32662-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="32662-145">Logon único para um aplicativo da Galeria do Azure AD como federado tooconfigure</span><span class="sxs-lookup"><span data-stu-id="32662-145">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="32662-146">Todos os aplicativos na Galeria do Azure AD Olá habilitado com a funcionalidade do Enterprise Single Sign-On tem um tutorial passo a passo disponível.</span><span class="sxs-lookup"><span data-stu-id="32662-146">All application in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="32662-147">Você pode acessar Olá [lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para uma orientação passo a passo detalhadas.</span><span class="sxs-lookup"><span data-stu-id="32662-147">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="32662-148">tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:</span><span class="sxs-lookup"><span data-stu-id="32662-148">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="32662-149">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="32662-149">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="32662-150">Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)</span><span class="sxs-lookup"><span data-stu-id="32662-150">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="32662-151">Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="32662-151">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="32662-152">Recuperar certificado e metadados Azure AD</span><span class="sxs-lookup"><span data-stu-id="32662-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="32662-153">Configurar valores de metadados do AD do Azure no aplicativo hello (logon URL, o emissor, o URL de Logout e certificado)</span><span class="sxs-lookup"><span data-stu-id="32662-153">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="32662-154">Atribuir usuários toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="32662-154">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="32662-155">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="32662-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="32662-156">tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-157">Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**</span><span class="sxs-lookup"><span data-stu-id="32662-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="32662-158">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="32662-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32662-159">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="32662-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32662-160">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="32662-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32662-161">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha</span><span class="sxs-lookup"><span data-stu-id="32662-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="32662-162">Em Olá **Insira um nome** caixa de texto de saudação **adicionar da Galeria Olá** seção, digite o nome de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="32662-163">Selecione aplicativo hello desejar tooconfigure para logon único.</span><span class="sxs-lookup"><span data-stu-id="32662-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="32662-164">Antes de adicionar o aplicativo hello, você pode alterar seu nome de saudação **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="32662-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="32662-165">Clique em **adicionar** botão, o aplicativo de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="32662-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="32662-166">Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="32662-167">Configurar logon único para um aplicativo da Galeria do AD do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="32662-167">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="32662-168">tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="32662-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="32662-170">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="32662-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32662-171">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="32662-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32662-172">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="32662-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32662-173">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="32662-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="32662-174">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="32662-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="32662-175">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="32662-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="32662-176">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="32662-177">Selecione **baseado no SAML logon** de saudação **modo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="32662-177">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="32662-178">Digite os valores hello necessárias nas **URLs e domínio.**</span><span class="sxs-lookup"><span data-stu-id="32662-178">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="32662-179">Você deve obter esses valores do fornecedor do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-179">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="32662-180">aplicativo de hello tooconfigure como SSO iniciado por SP, Olá logon na URL é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="32662-180">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="32662-181">Para alguns aplicativos, Olá identificador também é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="32662-181">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="32662-182">aplicativo de hello tooconfigure como iniciado pelo IdP SSO, Olá URL de resposta é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="32662-182">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="32662-183">Para alguns aplicativos, Olá identificador também é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="32662-183">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="32662-184">**Opcional:** clique **Mostrar configurações de URL avançadas** se você quiser toosee Olá não obrigatórios valores.</span><span class="sxs-lookup"><span data-stu-id="32662-184">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="32662-185">Em Olá **atributos de usuário**, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="32662-185">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="32662-186">**Opcional:** clique **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="32662-186">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="32662-187">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="32662-187">tooadd an attribute:</span></span>

   1. <span data-ttu-id="32662-188">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="32662-188">click **Add attribute**.</span></span> <span data-ttu-id="32662-189">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-189">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="32662-190">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="32662-190">Click **Save.**</span></span> <span data-ttu-id="32662-191">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-191">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="32662-192">Clique em **configurar &lt;nome do aplicativo&gt;**  tooaccess documentação sobre como tooconfigure logon único no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-192">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="32662-193">Além disso, você tem Olá URLs de metadados e o certificado necessário toosetup SSO com o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-193">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="32662-194">Clique em **salvar** toosave configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-194">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="32662-195">Atribua usuários toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32662-195">Assign users toohello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="32662-196">Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="32662-196">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="32662-197">tooselect Olá identificador de usuário ou adicione atributos de usuário, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-197">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-198">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="32662-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="32662-199">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="32662-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32662-200">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="32662-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32662-201">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="32662-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32662-202">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="32662-202">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="32662-203">Se você não vir o aplicativo hello deseja tooshow aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="32662-203">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="32662-204">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="32662-204">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="32662-205">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="32662-206">Em Olá **atributos de usuário** seção, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="32662-206">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="32662-207">Olá opção selecionada deve toomatch Olá esperado valor no usuário de saudação do hello aplicativo tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="32662-207">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="32662-208">Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="32662-208">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="32662-209">Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) em Olá seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="32662-209">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="32662-210">tooadd atributos de usuário, clique em **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="32662-210">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="32662-211">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="32662-211">tooadd an attribute:</span></span>

   1. <span data-ttu-id="32662-212">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="32662-212">click **Add attribute**.</span></span> <span data-ttu-id="32662-213">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-213">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="32662-214">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="32662-214">Click **Save.**</span></span> <span data-ttu-id="32662-215">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-215">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="32662-216">Download de metadados do AD do Azure hello ou certificado</span><span class="sxs-lookup"><span data-stu-id="32662-216">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="32662-217">os metadados do aplicativo hello toodownload ou o certificado do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-217">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-218">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="32662-218">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="32662-219">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="32662-219">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32662-220">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="32662-220">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32662-221">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="32662-221">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32662-222">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="32662-222">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="32662-223">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="32662-223">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="32662-224">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="32662-224">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="32662-225">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-225">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="32662-226">Vá muito**o certificado de autenticação SAML** seção e, em seguida, clique em **baixar** valor da coluna.</span><span class="sxs-lookup"><span data-stu-id="32662-226">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="32662-227">Dependendo de qual aplicativo hello requer a configuração de logon único, você ver qualquer toodownload de opção Olá Olá Metadata XML ou Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="32662-227">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="32662-228">AD do Azure não fornece um URL de metadados de saudação de tooget.</span><span class="sxs-lookup"><span data-stu-id="32662-228">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="32662-229">Olá metadados somente podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="32662-229">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="32662-230">Logon único para um aplicativo da Galeria não como federado tooconfigure</span><span class="sxs-lookup"><span data-stu-id="32662-230">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="32662-231">tooconfigure um aplicativo não galeria, é necessário toohave do Azure AD premium e aplicativo hello suporta SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="32662-231">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="32662-232">Para obter mais informações sobre as versões do Azure AD, visite [Preços do Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="32662-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="32662-233">Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)</span><span class="sxs-lookup"><span data-stu-id="32662-233">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="32662-234">Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="32662-234">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="32662-235">Recuperar certificado e metadados Azure AD</span><span class="sxs-lookup"><span data-stu-id="32662-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="32662-236">Configurar valores de metadados do AD do Azure no aplicativo hello (logon URL, o emissor, o URL de Logout e certificado)</span><span class="sxs-lookup"><span data-stu-id="32662-236">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="32662-237">Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)</span><span class="sxs-lookup"><span data-stu-id="32662-237">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="32662-238">tooconfigure logon único para um aplicativo que não está na Galeria do Azure AD hello, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-238">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-239">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="32662-239">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="32662-240">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="32662-240">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32662-241">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="32662-241">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32662-242">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="32662-242">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32662-243">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha</span><span class="sxs-lookup"><span data-stu-id="32662-243">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="32662-244">Clique em **aplicativo Galeria não** em Olá **adicionar seu próprio aplicativo** seção</span><span class="sxs-lookup"><span data-stu-id="32662-244">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="32662-245">Digite o nome de saudação do aplicativo hello em hello **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="32662-245">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="32662-246">Clique em **adicionar** botão, o aplicativo de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="32662-246">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="32662-247">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-247">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="32662-248">Selecione **baseado no SAML logon** em Olá **modo** suspenso</span><span class="sxs-lookup"><span data-stu-id="32662-248">Select **SAML-based Sign-on** in hello **Mode** dropdown</span></span>

11. <span data-ttu-id="32662-249">Digite os valores hello necessárias nas **URLs e domínio.**</span><span class="sxs-lookup"><span data-stu-id="32662-249">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="32662-250">Você deve obter esses valores do fornecedor do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-250">You should get these values from hello application vendor.</span></span>

  1. <span data-ttu-id="32662-251">aplicativo de hello tooconfigure como iniciado pelo IdP SSO, digite Olá URL de resposta e Olá identificador.</span><span class="sxs-lookup"><span data-stu-id="32662-251">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

  2. <span data-ttu-id="32662-252">**Opcional:** tooconfigure aplicativo de hello como SSO iniciado por SP, Olá logon na URL é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="32662-252">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="32662-253">Em Olá **atributos de usuário**, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="32662-253">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="32662-254">**Opcional:** clique **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="32662-254">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="32662-255">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="32662-255">tooadd an attribute:</span></span>

   1. <span data-ttu-id="32662-256">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="32662-256">click **Add attribute**.</span></span> <span data-ttu-id="32662-257">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-257">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="32662-258">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="32662-258">Click **Save.**</span></span> <span data-ttu-id="32662-259">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-259">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="32662-260">Clique em **configurar &lt;nome do aplicativo&gt;**  tooaccess documentação sobre como tooconfigure logon único no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-260">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="32662-261">Além disso, você tem URLs do AD do Azure e o certificado necessário para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-261">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="32662-262">Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="32662-262">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="32662-263">tooselect Olá identificador de usuário ou adicione atributos de usuário, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-263">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-264">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="32662-264">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="32662-265">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="32662-265">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32662-266">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="32662-266">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32662-267">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="32662-267">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32662-268">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="32662-268">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="32662-269">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="32662-269">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="32662-270">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="32662-270">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="32662-271">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-271">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="32662-272">Em Olá **atributos de usuário** seção, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="32662-272">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="32662-273">Olá opção selecionada deve toomatch Olá esperado valor no usuário de saudação do hello aplicativo tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="32662-273">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="32662-274">Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="32662-274">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="32662-275">Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) em Olá seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="32662-275">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="32662-276">tooadd atributos de usuário, clique em **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="32662-276">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="32662-277">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="32662-277">tooadd an attribute:</span></span>

   <span data-ttu-id="32662-278">1. Clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="32662-278">1.click **Add attribute**.</span></span> <span data-ttu-id="32662-279">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-279">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   <span data-ttu-id="32662-280">2 Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="32662-280">2 Click **Save.**</span></span> <span data-ttu-id="32662-281">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-281">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="32662-282">Download de metadados do AD do Azure hello ou certificado</span><span class="sxs-lookup"><span data-stu-id="32662-282">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="32662-283">os metadados do aplicativo hello toodownload ou o certificado do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-283">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-284">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="32662-284">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="32662-285">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="32662-285">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32662-286">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="32662-286">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32662-287">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="32662-287">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32662-288">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="32662-288">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="32662-289">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="32662-289">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="32662-290">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="32662-290">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="32662-291">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-291">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="32662-292">Vá muito**o certificado de autenticação SAML** seção e, em seguida, clique em **baixar** valor da coluna.</span><span class="sxs-lookup"><span data-stu-id="32662-292">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="32662-293">Dependendo de qual aplicativo hello requer a configuração de logon único, você ver qualquer toodownload de opção Olá Olá Metadata XML ou Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="32662-293">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="32662-294">AD do Azure não fornece um URL de metadados de saudação de tooget.</span><span class="sxs-lookup"><span data-stu-id="32662-294">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="32662-295">Olá metadados somente podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="32662-295">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="32662-296">Como senha tooconfigure o logon único para um aplicativo da Galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="32662-296">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="32662-297">tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:</span><span class="sxs-lookup"><span data-stu-id="32662-297">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="32662-298">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="32662-298">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="32662-299">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="32662-299">Configure hello application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="32662-300">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="32662-300">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="32662-301">tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-301">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-302">Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**</span><span class="sxs-lookup"><span data-stu-id="32662-302">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="32662-303">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="32662-303">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32662-304">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="32662-304">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32662-305">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="32662-305">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32662-306">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha</span><span class="sxs-lookup"><span data-stu-id="32662-306">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="32662-307">Em Olá **Insira um nome** caixa de texto de saudação **adicionar da Galeria Olá** seção, digite o nome de saudação do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="32662-307">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="32662-308">Selecionar aplicativo hello desejar tooconfigure para logon único</span><span class="sxs-lookup"><span data-stu-id="32662-308">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="32662-309">Antes de adicionar o aplicativo hello, você pode alterar seu nome de saudação **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="32662-309">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="32662-310">Clique em **adicionar** botão, o aplicativo de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="32662-310">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="32662-311">Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-311">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="32662-312">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="32662-312">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="32662-313">tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-313">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-314">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="32662-314">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="32662-315">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="32662-315">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32662-316">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="32662-316">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32662-317">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="32662-317">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32662-318">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="32662-318">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="32662-319">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="32662-319">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="32662-320">Selecionar aplicativo hello deseja tooconfigure-logon único</span><span class="sxs-lookup"><span data-stu-id="32662-320">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="32662-321">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-321">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="32662-322">Modo de seleção Olá **com base em senha de logon.**</span><span class="sxs-lookup"><span data-stu-id="32662-322">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="32662-323">Atribua usuários toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32662-323">Assign users toohello application.</span></span>

10. <span data-ttu-id="32662-324">Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-324">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="32662-325">Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="32662-325">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="32662-326">Como senha tooconfigure o logon único para um aplicativo não Galeria</span><span class="sxs-lookup"><span data-stu-id="32662-326">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="32662-327">tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:</span><span class="sxs-lookup"><span data-stu-id="32662-327">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="32662-328">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="32662-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="32662-329">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="32662-329">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="32662-330">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="32662-330">Add a non-gallery application</span></span>

<span data-ttu-id="32662-331">tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-331">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-332">Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**</span><span class="sxs-lookup"><span data-stu-id="32662-332">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="32662-333">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="32662-333">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32662-334">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="32662-334">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32662-335">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="32662-335">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32662-336">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha</span><span class="sxs-lookup"><span data-stu-id="32662-336">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="32662-337">clique em **Aplicativo inexistente na galeria.**</span><span class="sxs-lookup"><span data-stu-id="32662-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="32662-338">Insira o nome de saudação do seu aplicativo em Olá **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="32662-338">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="32662-339">Selecione **Adicionar.**</span><span class="sxs-lookup"><span data-stu-id="32662-339">Select **Add.**</span></span>

<span data-ttu-id="32662-340">Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-340">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="32662-341">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="32662-341">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="32662-342">tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-342">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-343">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="32662-343">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="32662-344">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="32662-344">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32662-345">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="32662-345">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32662-346">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="32662-346">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32662-347">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="32662-347">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="32662-348">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="32662-348">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="32662-349">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="32662-349">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="32662-350">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-350">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="32662-351">Modo de seleção Olá **com base em senha de logon.**</span><span class="sxs-lookup"><span data-stu-id="32662-351">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="32662-352">Digite hello **URL de logon**.</span><span class="sxs-lookup"><span data-stu-id="32662-352">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="32662-353">Isso é Olá URL onde os usuários digitarão seu nome de usuário e senha toosign em para.</span><span class="sxs-lookup"><span data-stu-id="32662-353">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="32662-354">Certifique-se de campos de entrada hello são visíveis na URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-354">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="32662-355">Atribua usuários toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32662-355">Assign users toohello application.</span></span>

11. <span data-ttu-id="32662-356">Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="32662-356">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="32662-357">Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="32662-357">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="32662-358">Como tooassign tooan aplicativo do usuário diretamente</span><span class="sxs-lookup"><span data-stu-id="32662-358">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="32662-359">tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="32662-359">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="32662-360">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="32662-360">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="32662-361">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="32662-361">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32662-362">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="32662-362">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32662-363">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="32662-363">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32662-364">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="32662-364">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="32662-365">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="32662-365">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="32662-366">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="32662-366">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="32662-367">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32662-367">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="32662-368">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="32662-368">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="32662-369">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="32662-369">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="32662-370">Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="32662-370">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="32662-371">Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="32662-371">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="32662-372">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="32662-372">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="32662-373">**Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="32662-373">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="32662-374">Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32662-374">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="32662-375">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="32662-375">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="32662-376">Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.</span><span class="sxs-lookup"><span data-stu-id="32662-376">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="32662-377">Após um curto período, os usuários Olá que você selecionou ser capaz de toolaunch esses aplicativos em Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="32662-377">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="32662-378">Se essas etapas de solução de problemas Olá não resolver o problema de saudação</span><span class="sxs-lookup"><span data-stu-id="32662-378">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="32662-379">Abra um tíquete de suporte com hello informações a seguir se disponíveis:</span><span class="sxs-lookup"><span data-stu-id="32662-379">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="32662-380">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="32662-380">Correlation error ID</span></span>

-   <span data-ttu-id="32662-381">UPN (endereço de email de usuário)</span><span class="sxs-lookup"><span data-stu-id="32662-381">UPN (user email address)</span></span>

-   <span data-ttu-id="32662-382">TenantID</span><span class="sxs-lookup"><span data-stu-id="32662-382">TenantID</span></span>

-   <span data-ttu-id="32662-383">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="32662-383">Browser type</span></span>

-   <span data-ttu-id="32662-384">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="32662-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="32662-385">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="32662-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="32662-386">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="32662-386">Next steps</span></span>
[<span data-ttu-id="32662-387">Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="32662-387">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

