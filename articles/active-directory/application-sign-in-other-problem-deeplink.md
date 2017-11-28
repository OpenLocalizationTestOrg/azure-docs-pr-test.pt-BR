---
title: aaaProblems entrar no aplicativo tooan usando um deeplink | Microsoft Docs
description: Como os problemas de tootroubleshoot acesso a um aplicativo de uma URL deeplink usando o Azure AD
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a><span data-ttu-id="2b497-103">Problemas para entrar no aplicativo tooan usando um deeplink</span><span class="sxs-lookup"><span data-stu-id="2b497-103">Problems signing in tooan application using a deeplink</span></span>

<span data-ttu-id="2b497-104">Olá painel de acesso é um portal baseado na web que permite que um usuário com um trabalho ou escola conta em aplicativos tooview e início baseado em nuvem do Azure Active Directory (AD do Azure) que Olá administrador do AD do Azure tem acesso-los ao.</span><span class="sxs-lookup"><span data-stu-id="2b497-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="2b497-105">Esses aplicativos são configurados em nome de usuário de saudação no portal do Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="2b497-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="2b497-106">aplicativo Hello deve ser configurado corretamente e atribuído toohello usuário ou grupo Olá é um membro de toosee aplicativo Olá Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="2b497-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="2b497-107">Acesso de usuário ou links profundos URLs são links que os usuários podem usar tooaccess seus aplicativos de SSO de senha diretamente da URL de seus navegadores de barras.</span><span class="sxs-lookup"><span data-stu-id="2b497-107">Deep links or User access URLs are links your users may use tooaccess their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="2b497-108">Navegando toothis link, os usuários terão automaticamente conectado ao aplicativo hello sem ter que primeiro toogo toohello painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="2b497-108">By navigating toothis link, users be automatically signed into hello application without having toogo toohello Access Panel first.</span></span> <span data-ttu-id="2b497-109">Isso é hello link mesmo que os usuários usam tooaccess estes aplicativos de iniciador do aplicativo hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="2b497-109">This is hello same link that users use tooaccess these applications from hello Office 365 application launcher.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="2b497-110">Geral emite toocheck primeiro</span><span class="sxs-lookup"><span data-stu-id="2b497-110">General issues toocheck first</span></span>

-   <span data-ttu-id="2b497-111">Verifique se seu usando um **navegador** que atende aos requisitos mínimos Olá Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="2b497-111">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="2b497-112">Certifique-se de navegador do usuário Olá adicionou URL Olá Olá aplicativo tooits **sites confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="2b497-112">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="2b497-113">Certifique-se de aplicativo de hello toocheck é **configurado** corretamente.</span><span class="sxs-lookup"><span data-stu-id="2b497-113">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="2b497-114">Certifique-se de conta de usuário Olá **habilitado** para entradas.</span><span class="sxs-lookup"><span data-stu-id="2b497-114">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="2b497-115">Certifique-se de conta de usuário Olá **não bloqueada.**</span><span class="sxs-lookup"><span data-stu-id="2b497-115">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="2b497-116">Tornar-se de que usuário Olá **senha não está expirada ou esquecida.**</span><span class="sxs-lookup"><span data-stu-id="2b497-116">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="2b497-117">Verifique se a **Autenticação Multifator** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="2b497-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="2b497-118">Verifique se uma **Política de acesso condicional** ou política de **Proteção de Identidade** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="2b497-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="2b497-119">Certifique-se de que um usuário **informações de contato de autenticação** está ativo toodate tooallow autenticação multifator ou o acesso condicional políticas toobe imposta.</span><span class="sxs-lookup"><span data-stu-id="2b497-119">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="2b497-120">Verifique se tooalso tente eliminar os cookies do seu navegador e tentar toosign em novamente.</span><span class="sxs-lookup"><span data-stu-id="2b497-120">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="checking-hello-deeplink"></a><span data-ttu-id="2b497-121">Verificando Olá deeplink</span><span class="sxs-lookup"><span data-stu-id="2b497-121">Checking hello deeplink</span></span>

<span data-ttu-id="2b497-122">toocheck se você tiver deeplink correto do hello, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b497-122">toocheck if you have hello correct deeplink, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b497-123">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="2b497-123">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2b497-124">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b497-124">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b497-125">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b497-125">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b497-126">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b497-126">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b497-127">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b497-127">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2b497-128">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b497-128">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b497-129">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="2b497-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="2b497-130">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b497-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b497-131">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b497-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="2b497-132">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b497-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="2b497-133">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b497-133">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="2b497-134">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b497-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

11. <span data-ttu-id="2b497-135">Selecione aplicativo hello para que deseja Olá seleção Olá deeplink.</span><span class="sxs-lookup"><span data-stu-id="2b497-135">Select hello application you want hello check hello deeplink for.</span></span>

12. <span data-ttu-id="2b497-136">Localizar o rótulo de saudação **URL de acesso do usuário**.</span><span class="sxs-lookup"><span data-stu-id="2b497-136">Find hello label **User Access URL**.</span></span> <span data-ttu-id="2b497-137">O DeepLink deve corresponder a essa URL.</span><span class="sxs-lookup"><span data-stu-id="2b497-137">You deeplink should match this URL.</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="2b497-138">Como tooinstall Olá extensão de navegador do painel de acesso</span><span class="sxs-lookup"><span data-stu-id="2b497-138">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="2b497-139">Olá tooinstall extensão de navegador do painel de acesso, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b497-139">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b497-140">Olá abrir [painel de acesso](https://myapps.microsoft.com) em um dos navegadores Olá com suporte e entre como um **usuário** no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b497-140">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="2b497-141">Clique em uma **aplicativo SSO de senha** no painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b497-141">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="2b497-142">Olá prompt perguntando tooinstall Olá software, selecione **instalar agora**.</span><span class="sxs-lookup"><span data-stu-id="2b497-142">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="2b497-143">Com base em seu navegador é direcionado toohello link para download.</span><span class="sxs-lookup"><span data-stu-id="2b497-143">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="2b497-144">**Adicionar** navegador de tooyour Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="2b497-144">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="2b497-145">Se seu navegador solicita, selecione tooeither **habilitar** ou **permitir** Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="2b497-145">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="2b497-146">Quando estiver instalado, **reinicie** a sessão do navegador.</span><span class="sxs-lookup"><span data-stu-id="2b497-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="2b497-147">Entrar painel de acesso de saudação e veja se é possível **iniciar** seus aplicativos de SSO de senha</span><span class="sxs-lookup"><span data-stu-id="2b497-147">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="2b497-148">Você também pode baixar a extensão Olá para Chrome e Firefox de links diretos da saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b497-148">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="2b497-149">Extensão do Painel de Acesso do Chrome</span><span class="sxs-lookup"><span data-stu-id="2b497-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="2b497-150">Extensão do Painel de Acesso do Firefox</span><span class="sxs-lookup"><span data-stu-id="2b497-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="2b497-151">Como senha tooconfigure o logon único para um aplicativo da Galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b497-151">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="2b497-152">tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:</span><span class="sxs-lookup"><span data-stu-id="2b497-152">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="2b497-153">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="2b497-153">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="2b497-154">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b497-154">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="2b497-155">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="2b497-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="2b497-156">tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b497-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b497-157">Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="2b497-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="2b497-158">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b497-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b497-159">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b497-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b497-160">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b497-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b497-161">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha.</span><span class="sxs-lookup"><span data-stu-id="2b497-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="2b497-162">Em Olá **Insira um nome** caixa de texto de saudação **adicionar da Galeria Olá** seção, digite o nome de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b497-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="2b497-163">Selecione aplicativo hello desejar tooconfigure para logon único.</span><span class="sxs-lookup"><span data-stu-id="2b497-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="2b497-164">Antes de adicionar o aplicativo hello, você pode alterar seu nome de saudação **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2b497-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="2b497-165">Clique em **adicionar** botão, o aplicativo de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2b497-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="2b497-166">Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b497-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="2b497-167">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b497-167">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="2b497-168">tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b497-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b497-169">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="2b497-169">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2b497-170">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b497-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b497-171">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b497-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b497-172">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b497-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b497-173">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b497-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2b497-174">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b497-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b497-175">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="2b497-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="2b497-176">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b497-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b497-177">Modo de seleção Olá **com base em senha de logon.**</span><span class="sxs-lookup"><span data-stu-id="2b497-177">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="2b497-178">[Atribuir usuários toohello aplicativo](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="2b497-178">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="2b497-179">Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b497-179">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="2b497-180">Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="2b497-180">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="2b497-181">Como senha tooconfigure o logon único para um aplicativo não Galeria</span><span class="sxs-lookup"><span data-stu-id="2b497-181">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="2b497-182">tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:</span><span class="sxs-lookup"><span data-stu-id="2b497-182">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="2b497-183">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="2b497-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="2b497-184">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b497-184">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="2b497-185">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="2b497-185">Add a non-gallery application</span></span>

<span data-ttu-id="2b497-186">tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b497-186">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b497-187">Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="2b497-187">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="2b497-188">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b497-188">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b497-189">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b497-189">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b497-190">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b497-190">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b497-191">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha.</span><span class="sxs-lookup"><span data-stu-id="2b497-191">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="2b497-192">clique em **Aplicativo inexistente na galeria.**</span><span class="sxs-lookup"><span data-stu-id="2b497-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="2b497-193">Insira o nome de saudação do seu aplicativo em Olá **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2b497-193">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="2b497-194">Selecione **Adicionar.**</span><span class="sxs-lookup"><span data-stu-id="2b497-194">Select **Add.**</span></span>

<span data-ttu-id="2b497-195">Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b497-195">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="2b497-196">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b497-196">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="2b497-197">tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b497-197">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b497-198">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="2b497-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2b497-199">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b497-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b497-200">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b497-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b497-201">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b497-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b497-202">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b497-202">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="2b497-203">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b497-203">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b497-204">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="2b497-204">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="2b497-205">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b497-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b497-206">Modo de seleção Olá **com base em senha de logon.**</span><span class="sxs-lookup"><span data-stu-id="2b497-206">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="2b497-207">Digite hello **URL de logon**.</span><span class="sxs-lookup"><span data-stu-id="2b497-207">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="2b497-208">Isso é Olá URL onde os usuários digitarão seu nome de usuário e senha toosign em para.</span><span class="sxs-lookup"><span data-stu-id="2b497-208">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="2b497-209">Certifique-se de campos de entrada hello são visíveis na URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b497-209">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="2b497-210">Atribua usuários toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2b497-210">Assign users toohello application.</span></span>

11. <span data-ttu-id="2b497-211">Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b497-211">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="2b497-212">Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="2b497-212">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="2b497-213">Como tooassign tooan aplicativo do usuário diretamente</span><span class="sxs-lookup"><span data-stu-id="2b497-213">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="2b497-214">tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b497-214">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b497-215">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2b497-215">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2b497-216">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b497-216">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b497-217">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b497-217">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b497-218">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b497-218">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b497-219">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b497-219">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2b497-220">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b497-220">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b497-221">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="2b497-221">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="2b497-222">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b497-222">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b497-223">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="2b497-223">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="2b497-224">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="2b497-224">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="2b497-225">Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="2b497-225">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="2b497-226">Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="2b497-226">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="2b497-227">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="2b497-227">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="2b497-228">**Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="2b497-228">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="2b497-229">Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2b497-229">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="2b497-230">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="2b497-230">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="2b497-231">Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.</span><span class="sxs-lookup"><span data-stu-id="2b497-231">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="2b497-232">Após um curto período, os usuários Olá que você selecionou ser capaz de toolaunch esses aplicativos em Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="2b497-232">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="2b497-233">Se essas etapas de solução de problemas Olá não resolva o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b497-233">If these troubleshooting steps do not hello resolve hello issue.</span></span> 

<span data-ttu-id="2b497-234">Abra um tíquete de suporte com hello informações a seguir se disponíveis:</span><span class="sxs-lookup"><span data-stu-id="2b497-234">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="2b497-235">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="2b497-235">Correlation error ID</span></span>

-   <span data-ttu-id="2b497-236">UPN (endereço de email de usuário)</span><span class="sxs-lookup"><span data-stu-id="2b497-236">UPN (user email address)</span></span>

-   <span data-ttu-id="2b497-237">TenantID</span><span class="sxs-lookup"><span data-stu-id="2b497-237">TenantID</span></span>

-   <span data-ttu-id="2b497-238">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="2b497-238">Browser type</span></span>

-   <span data-ttu-id="2b497-239">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="2b497-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="2b497-240">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="2b497-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b497-241">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b497-241">Next steps</span></span>
[<span data-ttu-id="2b497-242">Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="2b497-242">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
