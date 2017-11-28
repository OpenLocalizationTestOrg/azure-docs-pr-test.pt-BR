---
title: "logon único aaaProblems entrar tooan configurado para a senha de aplicativo de galeria do AD do Azure | Microsoft Docs"
description: "Discute as áreas problemáticas que fornecem orientação tootroubleshoot problemas relacionado toosigning em tooAzure aplicativos Galeria AD configurados para logon único senha"
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
ms.openlocfilehash: f53ef4176db37dc6b1da2d61027155a6ba8f331e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="b9214-103">Problemas para entrar no tooan configurado para logon único senha de aplicativo de galeria do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9214-103">Problems signing in tooan Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="b9214-104">Olá painel de acesso é um portal baseado na web que permite que um usuário que tem um trabalho ou escola conta em aplicativos tooview e inicie baseado em nuvem do Azure Active Directory (AD do Azure) administrador Olá AD do Azure-los concedeu acesso ao.</span><span class="sxs-lookup"><span data-stu-id="b9214-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="b9214-105">Um usuário com as edições do AD do Azure também pode usar grupos de autoatendimento e recursos de gerenciamento de aplicativo por meio do painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9214-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="b9214-106">Olá painel de acesso é separado do hello portal do Azure e não exige que os usuários toohave uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9214-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="b9214-107">toouse baseado em senha-logon único (SSO) no hello painel de acesso, Olá extensão do painel de acesso deve ser instalado no navegador do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="b9214-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="b9214-108">Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.</span><span class="sxs-lookup"><span data-stu-id="b9214-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="b9214-109">Atende aos requisitos de navegador de saudação painel de acesso</span><span class="sxs-lookup"><span data-stu-id="b9214-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="b9214-110">Olá painel de acesso requer um navegador que ofereça suporte ao JavaScript e CSS habilitou.</span><span class="sxs-lookup"><span data-stu-id="b9214-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="b9214-111">toouse baseado em senha-logon único (SSO) no hello painel de acesso, Olá extensão do painel de acesso deve ser instalado no navegador do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="b9214-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="b9214-112">Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.</span><span class="sxs-lookup"><span data-stu-id="b9214-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="b9214-113">Para SSO baseado em senha, navegadores de saudação do usuário podem ser:</span><span class="sxs-lookup"><span data-stu-id="b9214-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="b9214-114">Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior</span><span class="sxs-lookup"><span data-stu-id="b9214-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="b9214-115">Chrome – No Windows 7 ou posterior e no MacOS X ou posterior</span><span class="sxs-lookup"><span data-stu-id="b9214-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="b9214-116">Firefox 26.0 ou posterior, no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior</span><span class="sxs-lookup"><span data-stu-id="b9214-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="b9214-117">extensão SSO baseada em senha Olá ficam disponíveis para o Edge no Windows 10 quando as extensões de navegador tornam-se com suporte para a borda.</span><span class="sxs-lookup"><span data-stu-id="b9214-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="b9214-118">Como tooinstall Olá extensão de navegador do painel de acesso</span><span class="sxs-lookup"><span data-stu-id="b9214-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="b9214-119">Olá tooinstall extensão de navegador do painel de acesso, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="b9214-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="b9214-120">Olá abrir [painel de acesso](https://myapps.microsoft.com) em um dos navegadores Olá com suporte e entre como um **usuário** no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9214-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="b9214-121">Clique em uma **aplicativo SSO de senha** no painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9214-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="b9214-122">Olá prompt perguntando tooinstall Olá software, selecione **instalar agora**.</span><span class="sxs-lookup"><span data-stu-id="b9214-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="b9214-123">Com base em seu navegador é direcionado toohello link para download.</span><span class="sxs-lookup"><span data-stu-id="b9214-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="b9214-124">**Adicionar** navegador de tooyour Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="b9214-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="b9214-125">Se seu navegador solicita, selecione tooeither **habilitar** ou **permitir** Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="b9214-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="b9214-126">Quando estiver instalado, **reinicie** a sessão do navegador.</span><span class="sxs-lookup"><span data-stu-id="b9214-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="b9214-127">Entrar painel de acesso de saudação e veja se é possível **iniciar** seus aplicativos de SSO de senha</span><span class="sxs-lookup"><span data-stu-id="b9214-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="b9214-128">Você também pode baixar a extensão Olá para Chrome e Firefox de links diretos da saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="b9214-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="b9214-129">Extensão do Painel de Acesso do Chrome</span><span class="sxs-lookup"><span data-stu-id="b9214-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="b9214-130">Extensão do Painel de Acesso do Firefox</span><span class="sxs-lookup"><span data-stu-id="b9214-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="b9214-131">Configurar uma política de grupo para o Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="b9214-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="b9214-132">Você pode configurar uma política de grupo que permitem que você extensão do painel de acesso de saudação do tooremotely instalar para o Internet Explorer em computadores de seus usuários.</span><span class="sxs-lookup"><span data-stu-id="b9214-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="b9214-133">os pré-requisitos de saudação incluem:</span><span class="sxs-lookup"><span data-stu-id="b9214-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="b9214-134">Você configurou o [serviços de domínio do Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), e você tiver ingressado domínio de tooyour máquinas dos usuários.</span><span class="sxs-lookup"><span data-stu-id="b9214-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="b9214-135">Você deve ter hello "Editar configurações de" permissão tooedit Olá objeto de política de grupo (GPO).</span><span class="sxs-lookup"><span data-stu-id="b9214-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="b9214-136">Por padrão, membros da saudação grupos de segurança a seguir têm essa permissão: os administradores de domínio, administradores de empresa e proprietários de criadores de diretiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="b9214-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="b9214-137">[Saiba mais](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9214-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="b9214-138">Siga o tutorial Olá [como tooDeploy Olá extensão do painel de acesso do Internet Explorer usando a política de grupo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) para obter instruções passo a passo sobre como tooconfigure Olá a política de grupo e implantá-lo toousers.</span><span class="sxs-lookup"><span data-stu-id="b9214-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="b9214-139">Solucionar problemas de saudação painel de acesso no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="b9214-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="b9214-140">Siga Olá [solucionar Olá extensão do painel de acesso para o Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guia para acessar uma ferramenta de diagnóstico e instruções passo a passo sobre como configurar a extensão de saudação do IE.</span><span class="sxs-lookup"><span data-stu-id="b9214-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="b9214-141">Como senha tooconfigure o logon único para um aplicativo não Galeria</span><span class="sxs-lookup"><span data-stu-id="b9214-141">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="b9214-142">tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:</span><span class="sxs-lookup"><span data-stu-id="b9214-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="b9214-143">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="b9214-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="b9214-144">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9214-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="b9214-145">Atribuir usuários toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="b9214-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="b9214-146">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="b9214-146">Add a non-gallery application</span></span>

<span data-ttu-id="b9214-147">tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="b9214-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="b9214-148">Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**</span><span class="sxs-lookup"><span data-stu-id="b9214-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="b9214-149">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="b9214-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b9214-150">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="b9214-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b9214-151">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="b9214-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b9214-152">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha</span><span class="sxs-lookup"><span data-stu-id="b9214-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="b9214-153">clique em **Aplicativo inexistente na galeria.**</span><span class="sxs-lookup"><span data-stu-id="b9214-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="b9214-154">Insira o nome de saudação do seu aplicativo em Olá **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="b9214-154">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="b9214-155">Selecione **Adicionar.**</span><span class="sxs-lookup"><span data-stu-id="b9214-155">Select **Add.**</span></span>

<span data-ttu-id="b9214-156">Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9214-156">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="b9214-157">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9214-157">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="b9214-158">tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="b9214-158">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="b9214-159">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="b9214-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b9214-160">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="b9214-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b9214-161">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="b9214-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b9214-162">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="b9214-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b9214-163">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b9214-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="b9214-164">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="b9214-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b9214-165">Selecionar aplicativo hello deseja tooconfigure-logon único</span><span class="sxs-lookup"><span data-stu-id="b9214-165">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="b9214-166">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b9214-166">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b9214-167">Modo de seleção Olá **com base em senha de logon.**</span><span class="sxs-lookup"><span data-stu-id="b9214-167">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="b9214-168">Digite hello **URL de logon**.</span><span class="sxs-lookup"><span data-stu-id="b9214-168">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="b9214-169">Isso é Olá URL onde os usuários digitarão seu nome de usuário e senha toosign em para.</span><span class="sxs-lookup"><span data-stu-id="b9214-169">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="b9214-170">Certifique-se de campos de entrada hello são visíveis na URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9214-170">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="b9214-171">Atribua usuários toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9214-171">Assign users toohello application.</span></span>

11. <span data-ttu-id="b9214-172">Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9214-172">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="b9214-173">Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="b9214-173">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="b9214-174">Atribuir usuários toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="b9214-174">Assign users toohello application</span></span>

<span data-ttu-id="b9214-175">tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="b9214-175">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="b9214-176">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="b9214-176">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b9214-177">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="b9214-177">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b9214-178">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="b9214-178">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b9214-179">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="b9214-179">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b9214-180">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b9214-180">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="b9214-181">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="b9214-181">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b9214-182">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="b9214-182">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="b9214-183">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b9214-183">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b9214-184">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="b9214-184">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="b9214-185">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="b9214-185">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="b9214-186">Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b9214-186">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="b9214-187">Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="b9214-187">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="b9214-188">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="b9214-188">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="b9214-189">**Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="b9214-189">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="b9214-190">Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9214-190">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="b9214-191">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="b9214-191">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="b9214-192">Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.</span><span class="sxs-lookup"><span data-stu-id="b9214-192">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="b9214-193">Após um curto período, os usuários Olá que você selecionou ser capaz de toolaunch esses aplicativos em Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="b9214-193">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="b9214-194">Se essas etapas de solução de problemas Olá não resolver o problema de saudação</span><span class="sxs-lookup"><span data-stu-id="b9214-194">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="b9214-195">Abra um tíquete de suporte com hello informações a seguir se disponíveis:</span><span class="sxs-lookup"><span data-stu-id="b9214-195">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="b9214-196">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="b9214-196">Correlation error ID</span></span>

-   <span data-ttu-id="b9214-197">UPN (endereço de email de usuário)</span><span class="sxs-lookup"><span data-stu-id="b9214-197">UPN (user email address)</span></span>

-   <span data-ttu-id="b9214-198">TenantID</span><span class="sxs-lookup"><span data-stu-id="b9214-198">TenantID</span></span>

-   <span data-ttu-id="b9214-199">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="b9214-199">Browser type</span></span>

-   <span data-ttu-id="b9214-200">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="b9214-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="b9214-201">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="b9214-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9214-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9214-202">Next steps</span></span>
[<span data-ttu-id="b9214-203">Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="b9214-203">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

