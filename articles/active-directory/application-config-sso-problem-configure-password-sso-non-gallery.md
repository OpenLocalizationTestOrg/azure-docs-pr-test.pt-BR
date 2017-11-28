---
title: "aaaProblem configurando senha single sign-on para um aplicativo da Galeria não | Microsoft Docs"
description: "Entender a face de pessoas problemas comuns Olá ao configurar logon único de senha para aplicativos não-Galeria personalizados que não estão listados em Olá Galeria de aplicativos do Azure AD"
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="47ba9-103">Como configurar o logon único com senha para um aplicativo que não seja da galeria</span><span class="sxs-lookup"><span data-stu-id="47ba9-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="47ba9-104">Este artigo ajuda face de pessoas de problemas comuns do toounderstand Olá ao configurar **senha SSO** com um aplicativo não Galeria.</span><span class="sxs-lookup"><span data-stu-id="47ba9-104">This article help you toounderstand hello common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-toocapture-sign-in-fields-for-an-application"></a><span data-ttu-id="47ba9-105">Como entrar toocapture os campos para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="47ba9-105">How toocapture sign-in fields for an application</span></span>

<span data-ttu-id="47ba9-106">Captura de campo de entrada só tem suporte para páginas de entrada habilitadas por HTML e **não tem suporte para páginas de entrada não padrão**, como aquelas que usam Flash ou outras tecnologias de HTML não habilitado.</span><span class="sxs-lookup"><span data-stu-id="47ba9-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="47ba9-107">Há duas maneiras que você pode capturar campos de entrada para aplicativos personalizados:</span><span class="sxs-lookup"><span data-stu-id="47ba9-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="47ba9-108">Captura automática de campo de entrada</span><span class="sxs-lookup"><span data-stu-id="47ba9-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="47ba9-109">Captura manual de campo de entrada</span><span class="sxs-lookup"><span data-stu-id="47ba9-109">Manual sign-in field capture</span></span>

<span data-ttu-id="47ba9-110">**Captura de campo de entrada automática** funciona bem com a maioria dos habilitado HTML páginas de entrada, se eles usarem **IDs DIV conhecidos Olá nome de usuário e senha de entrada** campo.</span><span class="sxs-lookup"><span data-stu-id="47ba9-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for hello username and password input** field.</span></span> <span data-ttu-id="47ba9-111">Isso funciona de maneira de saudação é por atrito Olá HTML na página de saudação toofind IDs DIV que correspondem a certos critérios e, em seguida, salvando metadados para esse aplicativo para que pode reproduzir senhas tooit mais tarde.</span><span class="sxs-lookup"><span data-stu-id="47ba9-111">hello way this works is by scraping hello HTML on hello page toofind DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords tooit later.</span></span>

<span data-ttu-id="47ba9-112">**Captura de campo de entrada manual** pode ser usado em caso de Olá Olá aplicativo **fornecedor não rotula** Olá entrada campos usados para entrar.</span><span class="sxs-lookup"><span data-stu-id="47ba9-112">**Manual sign-in field capture** can be used in hello case that hello application **vendor does not label** hello input fields used for sign in.</span></span> <span data-ttu-id="47ba9-113">Captura de campo de entrada manual também pode ser usada no caso de Olá quando hello **fornecedor renderiza vários campos** que não pode ser detectado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="47ba9-113">Manual sign-in field capture can also be used in hello case when hello **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="47ba9-114">AD do Azure pode armazenar dados para vários campos que estejam na Olá entrar na página, desde que você Conte-nos onde esses campos estão na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="47ba9-114">Azure AD can store data for as many fields as are on hello sign in page, so long as you tell us where those fields are on hello page.</span></span>

<span data-ttu-id="47ba9-115">Em geral, **se a captura de campo de entrada automática não funcionar, sugerimos sempre tentar opção manual de saudação.**</span><span class="sxs-lookup"><span data-stu-id="47ba9-115">In general, **if automatic sign-in field capture does not work, we always suggest trying hello manual option.**</span></span>

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="47ba9-116">Como tooautomatically capturar campos de entrada para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="47ba9-116">How tooautomatically capture sign-in fields for an application</span></span>

<span data-ttu-id="47ba9-117">tooconfigure **com base em senha de logon único** para um aplicativo usando **captura automática campo entrar**, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="47ba9-117">tooconfigure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="47ba9-118">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="47ba9-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="47ba9-119">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="47ba9-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="47ba9-120">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="47ba9-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="47ba9-121">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="47ba9-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="47ba9-122">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="47ba9-122">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="47ba9-123">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="47ba9-123">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="47ba9-124">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="47ba9-124">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="47ba9-125">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="47ba9-125">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="47ba9-126">Modo de seleção Olá **com base em senha de logon.**</span><span class="sxs-lookup"><span data-stu-id="47ba9-126">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="47ba9-127">Digite hello **URL de logon**.</span><span class="sxs-lookup"><span data-stu-id="47ba9-127">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="47ba9-128">Isso é Olá URL onde os usuários digitarão seu nome de usuário e senha toosign em para.</span><span class="sxs-lookup"><span data-stu-id="47ba9-128">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="47ba9-129">**Certifique-se de campos de entrada hello são visíveis na URL Olá você fornecer**.</span><span class="sxs-lookup"><span data-stu-id="47ba9-129">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="47ba9-130">Clique em Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="47ba9-130">Click hello **Save** button.</span></span>

11. <span data-ttu-id="47ba9-131">Depois de você fazer isso, podemos será arranhar automaticamente essa URL para um nome de usuário e senha caixa de entrada e permitem que você toouse AD do Azure toosecurely transmitir aplicativos de toothat senhas usando a extensão de navegador do painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="47ba9-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span>

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="47ba9-132">Como toomanually capturar campos de entrada para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="47ba9-132">How toomanually capture sign-in fields for an application</span></span>

<span data-ttu-id="47ba9-133">toomanually captura campos de entrada, primeiro você deve ter extensão de navegador do painel de acesso Olá instalado e **não esteja em execução em modo privado, inPrivate ou incognito.**</span><span class="sxs-lookup"><span data-stu-id="47ba9-133">toomanually capture sign in fields, you must first have hello Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="47ba9-134">extensão de navegador tooinstall hello, siga etapas Olá Olá [como tooinstall Olá extensão de navegador do painel de acesso](#i-cannot-manually-detect-sign-in-fields-for-my-application) seção.</span><span class="sxs-lookup"><span data-stu-id="47ba9-134">tooinstall hello browser extension, follow hello steps in hello [How tooinstall hello Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="47ba9-135">tooconfigure **com base em senha de logon único** para um aplicativo usando **captura do campo de entrada manual**, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="47ba9-135">tooconfigure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="47ba9-136">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="47ba9-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="47ba9-137">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="47ba9-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="47ba9-138">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="47ba9-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="47ba9-139">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="47ba9-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="47ba9-140">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="47ba9-140">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="47ba9-141">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="47ba9-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="47ba9-142">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="47ba9-142">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="47ba9-143">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="47ba9-143">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="47ba9-144">Modo de seleção Olá **com base em senha de logon.**</span><span class="sxs-lookup"><span data-stu-id="47ba9-144">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="47ba9-145">Digite hello **URL de logon**.</span><span class="sxs-lookup"><span data-stu-id="47ba9-145">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="47ba9-146">Isso é Olá URL onde os usuários digitarão seu nome de usuário e senha toosign em para.</span><span class="sxs-lookup"><span data-stu-id="47ba9-146">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="47ba9-147">**Certifique-se de campos de entrada hello são visíveis na URL Olá você fornecer**.</span><span class="sxs-lookup"><span data-stu-id="47ba9-147">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="47ba9-148">Clique em Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="47ba9-148">Click hello **Save** button.</span></span>

11. <span data-ttu-id="47ba9-149">Depois de você fazer isso, podemos será arranhar automaticamente essa URL para um nome de usuário e senha caixa de entrada e permitem que você toouse AD do Azure toosecurely transmitir aplicativos de toothat senhas usando a extensão de navegador do painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="47ba9-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span> <span data-ttu-id="47ba9-150">No caso de Olá que isso falhar, você pode **Olá entrar no modo toouse campo de entrada manual captura de alteração** continuando toostep 12.</span><span class="sxs-lookup"><span data-stu-id="47ba9-150">In hello case that this fails, you can **change hello sign-in mode toouse manual sign-in field capture** by continuing toostep 12.</span></span>

12. <span data-ttu-id="47ba9-151">clique em **Configurar &lt;appname&gt; configurações de logon único com senha**.</span><span class="sxs-lookup"><span data-stu-id="47ba9-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="47ba9-152">Selecione Olá **detectar manualmente os campos de entrada** opção de configuração.</span><span class="sxs-lookup"><span data-stu-id="47ba9-152">Select hello **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="47ba9-153">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="47ba9-153">Click **Ok**.</span></span>

15. <span data-ttu-id="47ba9-154">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="47ba9-154">Click **Save**.</span></span>

16. <span data-ttu-id="47ba9-155">Execute Olá na tela instruções toouse Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="47ba9-155">Follow hello on screen instructions toouse hello Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="47ba9-156">Vejo o erro "Não foi possível encontrar os campos de entrada nessa URL"</span><span class="sxs-lookup"><span data-stu-id="47ba9-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="47ba9-157">Você vê este erro quando a detecção automática de campos de entrada falha.</span><span class="sxs-lookup"><span data-stu-id="47ba9-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="47ba9-158">tooresolve esse problema, tente detecção de campo de entrada manual por Olá seguindo as etapas em Olá [como toomanually capturar campos de entrada para um aplicativo](#how-to-manually-capture-sign-in-fields-for-an-application) seção.</span><span class="sxs-lookup"><span data-stu-id="47ba9-158">tooresolve this issue, try manual sign-in field detection by following hello steps in hello [How toomanually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a><span data-ttu-id="47ba9-159">Consulte o erro "não é possível toosave Single Sign-on configuração"</span><span class="sxs-lookup"><span data-stu-id="47ba9-159">I see an “Unable toosave Single Sign-on configuration” error</span></span>

<span data-ttu-id="47ba9-160">Em alguns casos raros, a configuração de logon único Olá a atualização pode falhar.</span><span class="sxs-lookup"><span data-stu-id="47ba9-160">In certain rare cases, updating hello single sign-on configuration can fail.</span></span> <span data-ttu-id="47ba9-161">tooresolve esse tente salvar Olá única configuração de logon novamente.</span><span class="sxs-lookup"><span data-stu-id="47ba9-161">tooresolve this try saving hello single sign-on configuration again.</span></span>

<span data-ttu-id="47ba9-162">Se isso continuar toofail consistentemente, abrir um caso de suporte e fornecer informações de saudação coletadas Olá [como detalhes de saudação toosee de uma notificação de portal](#i-cannot-manually-detect-sign-in-fields-for-my-application) e [como tooget ajuda enviando tooa de detalhes de notificação engenheiro de suporte](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) seções.</span><span class="sxs-lookup"><span data-stu-id="47ba9-162">If this continues toofail consistently, open a support case and provide hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="47ba9-163">Não posso manualmente detectar os campos de entrada para meu aplicativo</span><span class="sxs-lookup"><span data-stu-id="47ba9-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="47ba9-164">Alguns dos comportamentos de saudação que podem ocorrer ao detecção manual não está funcionando:</span><span class="sxs-lookup"><span data-stu-id="47ba9-164">Some of hello behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="47ba9-165">processo de captura manual Olá apareceu toowork, mas campos Olá capturados não estavam corretos</span><span class="sxs-lookup"><span data-stu-id="47ba9-165">hello manual capture process appeared toowork, but hello fields captured were not correct</span></span>

-   <span data-ttu-id="47ba9-166">Olá direita campos não destacados ao executar o processo de captura Olá</span><span class="sxs-lookup"><span data-stu-id="47ba9-166">hello right fields don’t get highlighted when performing hello capture process</span></span>

-   <span data-ttu-id="47ba9-167">o processo de captura Olá leva-me a página de logon do aplicativo toohello conforme o esperado, mas nada acontece</span><span class="sxs-lookup"><span data-stu-id="47ba9-167">hello capture process takes me toohello application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="47ba9-168">Captura manual aparece toowork, mas SSO não acontece quando os usuários navegam toohello aplicativo hello painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="47ba9-168">Manual capture appears toowork, but SSO doesn’t happen when my users navigate toohello application from hello Access Panel.</span></span>

<span data-ttu-id="47ba9-169">Se você encontrar qualquer um desses problemas, verifique o seguinte de saudação:</span><span class="sxs-lookup"><span data-stu-id="47ba9-169">check hello following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="47ba9-170">Verifique se você tem a versão mais recente de saudação da extensão de navegador do painel de acesso Olá **instalado** e **habilitado** , seguindo as etapas de Olá Olá [como tooinstall Olá navegador do painel de acesso extensão](#how-to-install-the-access-panel-browser-extension) seção.</span><span class="sxs-lookup"><span data-stu-id="47ba9-170">Ensure that you have hello latest version of hello access panel browser extension **installed** and **enabled** by following hello steps in hello [How tooinstall hello Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="47ba9-171">Certifique-se de que você está tentando não o processo de captura Olá ao seu navegador **modo privado, inPrivate ou incognito**.</span><span class="sxs-lookup"><span data-stu-id="47ba9-171">Ensure that you are not attempting hello capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="47ba9-172">Não há suporte para a extensão do painel de acesso Olá nesses modos.</span><span class="sxs-lookup"><span data-stu-id="47ba9-172">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="47ba9-173">Certifique-se de que os usuários não estão tentando toosign no aplicativo toohello do painel de acesso Olá ao mesmo tempo em **modo privado, inPrivate ou incognito**.</span><span class="sxs-lookup"><span data-stu-id="47ba9-173">Ensure that your users are not trying toosign in toohello application from hello access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="47ba9-174">Não há suporte para a extensão do painel de acesso Olá nesses modos.</span><span class="sxs-lookup"><span data-stu-id="47ba9-174">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="47ba9-175">Repita o processo de captura manual hello, garantindo marcadores Olá vermelho sobre campos corretos de saudação.</span><span class="sxs-lookup"><span data-stu-id="47ba9-175">Try hello manual capture process again, ensuring hello red markers are over hello correct fields.</span></span>

-   <span data-ttu-id="47ba9-176">Se o processo de captura manual Olá parece toohang, ou na página de entrada hello não faz nada (caso 3 acima), tente Olá captura manual processo novamente.</span><span class="sxs-lookup"><span data-stu-id="47ba9-176">If hello manual capture process seems toohang, or hello sign in page doesn’t do anything (case 3 above), try hello manual capture process again.</span></span> <span data-ttu-id="47ba9-177">Mas, desta vez depois de concluir o processo hello, pressione Olá **F12** botão tooopen console do desenvolvedor do navegador.</span><span class="sxs-lookup"><span data-stu-id="47ba9-177">But, this time after completing hello process, press hello **F12** button tooopen your browser’s developer console.</span></span> <span data-ttu-id="47ba9-178">Uma vez aberto, Olá **console** e tipo **window.location= "&lt;digite Olá logon na url que você especificou ao configurar o aplicativo hello&gt;"** e, em seguida, pressione  **Digite**.</span><span class="sxs-lookup"><span data-stu-id="47ba9-178">Once there, open hello **console** and type **window.location=”&lt;enter hello sign in url you specified when configuring hello app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="47ba9-179">Essa força uma página redirecionar que terminar o processo de captura hello e armazenar os campos de saudação que foram capturados.</span><span class="sxs-lookup"><span data-stu-id="47ba9-179">This force a page redirect which end hello capture process and store hello fields that have been captured.</span></span>

<span data-ttu-id="47ba9-180">Se nenhuma dessas abordagens funcionar para você, podemos ajudar.</span><span class="sxs-lookup"><span data-stu-id="47ba9-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="47ba9-181">Abrir um caso de suporte com detalhes de saudação do que você tentou, bem como informações de saudação coletadas Olá [como detalhes de saudação toosee de uma notificação de portal](#i-cannot-manually-detect-sign-in-fields-for-my-application) e [como tooget ajuda enviando detalhes de notificação tooa suporte engenheiro](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) seções (se aplicável).</span><span class="sxs-lookup"><span data-stu-id="47ba9-181">Open a support case with hello details of what you tried, as well as hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="47ba9-182">Como tooinstall Olá extensão de navegador do painel de acesso</span><span class="sxs-lookup"><span data-stu-id="47ba9-182">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="47ba9-183">Olá tooinstall extensão de navegador do painel de acesso, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="47ba9-183">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="47ba9-184">Olá abrir [painel de acesso](https://myapps.microsoft.com) em um dos navegadores Olá com suporte e entre como um **usuário** no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="47ba9-184">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="47ba9-185">Clique em uma **aplicativo SSO de senha** no painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="47ba9-185">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="47ba9-186">Olá prompt perguntando tooinstall Olá software, selecione **instalar agora**.</span><span class="sxs-lookup"><span data-stu-id="47ba9-186">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="47ba9-187">Com base em seu navegador é direcionado toohello link para download.</span><span class="sxs-lookup"><span data-stu-id="47ba9-187">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="47ba9-188">**Adicionar** navegador de tooyour Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="47ba9-188">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="47ba9-189">Se seu navegador solicita, selecione tooeither **habilitar** ou **permitir** Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="47ba9-189">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="47ba9-190">Quando estiver instalado, **reinicie** a sessão do navegador.</span><span class="sxs-lookup"><span data-stu-id="47ba9-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="47ba9-191">Entrar painel de acesso de saudação e veja se é possível **iniciar** seus aplicativos de SSO de senha.</span><span class="sxs-lookup"><span data-stu-id="47ba9-191">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="47ba9-192">Você também pode baixar a extensão Olá para Chrome e Firefox de links diretos da saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="47ba9-192">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="47ba9-193">Extensão do Painel de Acesso do Chrome</span><span class="sxs-lookup"><span data-stu-id="47ba9-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="47ba9-194">Extensão do Painel de Acesso do Firefox</span><span class="sxs-lookup"><span data-stu-id="47ba9-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="47ba9-195">Como detalhes de saudação toosee de uma notificação de portal</span><span class="sxs-lookup"><span data-stu-id="47ba9-195">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="47ba9-196">Você pode ver os detalhes de saudação de qualquer notificação de portal, seguindo as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="47ba9-196">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="47ba9-197">Clique em Olá **notificações** ícone (bell Olá) no canto superior direito de saudação do hello Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="47ba9-197">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="47ba9-198">Selecione qualquer notificação em um **erro** estado (aquelas com um toothem de Avançar vermelho (!)).</span><span class="sxs-lookup"><span data-stu-id="47ba9-198">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

  ><span data-ttu-id="47ba9-199">!NOTA] Não é possível clicar em notificações com estado de **Êxito** ou **Em Andamento**.</span><span class="sxs-lookup"><span data-stu-id="47ba9-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="47ba9-200">Este Olá abrir **detalhes da notificação** folha.</span><span class="sxs-lookup"><span data-stu-id="47ba9-200">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="47ba9-201">Use essas informações por conta própria toounderstand mais detalhes sobre o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="47ba9-201">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="47ba9-202">Se você ainda precisar de Ajuda, você também pode compartilhar essas informações com um suporte engenheiro ou hello grupo tooget Ajuda do produto com o problema.</span><span class="sxs-lookup"><span data-stu-id="47ba9-202">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="47ba9-203">Clique em Olá **cópia** **ícone** toohello direito da saudação **copiar erro** textbox toocopy todos os Olá tooshare de detalhes de notificação com um engenheiro de suporte ou produto de grupo.</span><span class="sxs-lookup"><span data-stu-id="47ba9-203">Click hello **copy** **icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="47ba9-204">Como ajudar a tooget enviando o engenheiro de suporte de tooa de detalhes de notificação</span><span class="sxs-lookup"><span data-stu-id="47ba9-204">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="47ba9-205">É muito importante que você compartilhe **todos os detalhes abaixo de Olá** com um engenheiro de suporte se você precisar de Ajuda, para que eles podem ajudá-lo rapidamente.</span><span class="sxs-lookup"><span data-stu-id="47ba9-205">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="47ba9-206">Você pode fazer isso facilmente por **tirar uma captura de tela,** ou clicando Olá **ícone de erro de cópia**, encontrado toohello direito da saudação **copiar erro** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="47ba9-206">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="47ba9-207">Detalhes da notificação explicados</span><span class="sxs-lookup"><span data-stu-id="47ba9-207">Notification Details Explained</span></span>

<span data-ttu-id="47ba9-208">Olá abaixo explica mais que cada um dos itens de notificação Olá significa e fornece exemplos de cada um deles.</span><span class="sxs-lookup"><span data-stu-id="47ba9-208">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="47ba9-209">Itens de notificação essenciais</span><span class="sxs-lookup"><span data-stu-id="47ba9-209">Essential Notification Items</span></span>

-   <span data-ttu-id="47ba9-210">**Título** – Olá título descritivo da notificação de saudação</span><span class="sxs-lookup"><span data-stu-id="47ba9-210">**Title** – hello descriptive title of hello notification</span></span>

    -   <span data-ttu-id="47ba9-211">Exemplo – **Configurações do proxy do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="47ba9-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="47ba9-212">**Descrição** – Olá descrição do que ocorreu como resultado da operação de saudação</span><span class="sxs-lookup"><span data-stu-id="47ba9-212">**Description** – hello description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="47ba9-213">Exemplo – **A URL interna inserida já está sendo usada por outro aplicativo**</span><span class="sxs-lookup"><span data-stu-id="47ba9-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="47ba9-214">**Id de notificação** – a id exclusiva Olá da notificação de saudação</span><span class="sxs-lookup"><span data-stu-id="47ba9-214">**Notification Id** – hello unique id of hello notification</span></span>

    -   <span data-ttu-id="47ba9-215">Exemplo – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="47ba9-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="47ba9-216">**Id de solicitação do cliente** – id de solicitação específica de saudação feita pelo seu navegador</span><span class="sxs-lookup"><span data-stu-id="47ba9-216">**Client Request Id** – hello specific request id made by your browser</span></span>

    -   <span data-ttu-id="47ba9-217">Exemplo – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="47ba9-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="47ba9-218">**Hora UTC de carimbo de data /** – Olá timestamp durante o qual ocorreu notificação hello, em UTC</span><span class="sxs-lookup"><span data-stu-id="47ba9-218">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

    -   <span data-ttu-id="47ba9-219">Exemplo – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="47ba9-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="47ba9-220">**Id de transação interna** – Olá ID interna, podemos usar erro de saudação toolook em nossos sistemas</span><span class="sxs-lookup"><span data-stu-id="47ba9-220">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

    -   <span data-ttu-id="47ba9-221">Exemplo – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="47ba9-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="47ba9-222">**UPN** – usuário Olá que realizou a operação de saudação</span><span class="sxs-lookup"><span data-stu-id="47ba9-222">**UPN** – hello user who performed hello operation</span></span>

    -   <span data-ttu-id="47ba9-223">Exemplo – **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="47ba9-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="47ba9-224">**Id do locatário** – ID exclusiva de saudação do locatário Olá Olá usuário que realizou a operação de saudação era um membro de</span><span class="sxs-lookup"><span data-stu-id="47ba9-224">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

    -   <span data-ttu-id="47ba9-225">Exemplo – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="47ba9-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="47ba9-226">**Id do objeto de usuário** – Olá ID exclusiva do usuário Olá que realizou a operação de saudação</span><span class="sxs-lookup"><span data-stu-id="47ba9-226">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

    -   <span data-ttu-id="47ba9-227">Exemplo – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="47ba9-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="47ba9-228">Itens de notificação detalhados</span><span class="sxs-lookup"><span data-stu-id="47ba9-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="47ba9-229">**Nome de exibição** – **(pode estar vazia)** um nome para exibição mais detalhado para o erro Olá</span><span class="sxs-lookup"><span data-stu-id="47ba9-229">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

    -   <span data-ttu-id="47ba9-230">Exemplo *– **Configurações do proxy do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="47ba9-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="47ba9-231">**Status** – Olá status específicos de notificação de saudação</span><span class="sxs-lookup"><span data-stu-id="47ba9-231">**Status** – hello specific status of hello notification</span></span>

    -   <span data-ttu-id="47ba9-232">Exemplo – **Falha**</span><span class="sxs-lookup"><span data-stu-id="47ba9-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="47ba9-233">**Id de objeto** – **(pode estar vazia)** Olá ID de objeto em relação a quais Olá a operação foi executada</span><span class="sxs-lookup"><span data-stu-id="47ba9-233">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

    -   <span data-ttu-id="47ba9-234">Exemplo – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="47ba9-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="47ba9-235">**Detalhes** – Olá descrição detalhada do que ocorreu como resultado da operação de saudação</span><span class="sxs-lookup"><span data-stu-id="47ba9-235">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="47ba9-236">Exemplo – **A URL interna 'http://bing.com/' é inválida, uma vez que está sendo utilizada**</span><span class="sxs-lookup"><span data-stu-id="47ba9-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="47ba9-237">**Erro de cópia** – clique Olá **ícone para copiar** toohello direito da saudação **copiar erro** textbox toocopy todos os Olá tooshare de detalhes de notificação com um engenheiro de suporte ou produto de grupo</span><span class="sxs-lookup"><span data-stu-id="47ba9-237">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

    -   <span data-ttu-id="47ba9-238">Exemplo – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="47ba9-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="47ba9-239">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47ba9-239">Next steps</span></span>
[<span data-ttu-id="47ba9-240">Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="47ba9-240">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

