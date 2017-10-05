---
title: "Como configurar o logon único com senha para um aplicativo que não seja da galeria | Microsoft Docs"
description: "Compreender os problemas comuns que as pessoas enfrentam ao configurar o Logon Único com Senha para aplicativos personalizados que não estão listados na Galeria do Aplicativo Azure AD"
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
ms.openlocfilehash: 9c76b6f3495e2dd759a156fcef97b57aece8d632
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="79e95-103">Como configurar o logon único com senha para um aplicativo que não seja da galeria</span><span class="sxs-lookup"><span data-stu-id="79e95-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="79e95-104">Este artigo ajuda você a compreender os problemas comuns que as pessoas enfrentam ao configurar o **Logon Único com Senha** com um aplicativo que não seja da Galeria.</span><span class="sxs-lookup"><span data-stu-id="79e95-104">This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-to-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="79e95-105">Como capturar campos de entrada para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="79e95-105">How to capture sign-in fields for an application</span></span>

<span data-ttu-id="79e95-106">Captura de campo de entrada só tem suporte para páginas de entrada habilitadas por HTML e **não tem suporte para páginas de entrada não padrão**, como aquelas que usam Flash ou outras tecnologias de HTML não habilitado.</span><span class="sxs-lookup"><span data-stu-id="79e95-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="79e95-107">Há duas maneiras que você pode capturar campos de entrada para aplicativos personalizados:</span><span class="sxs-lookup"><span data-stu-id="79e95-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="79e95-108">Captura automática de campo de entrada</span><span class="sxs-lookup"><span data-stu-id="79e95-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="79e95-109">Captura manual de campo de entrada</span><span class="sxs-lookup"><span data-stu-id="79e95-109">Manual sign-in field capture</span></span>

<span data-ttu-id="79e95-110">**Captura automática de campo de entrada** funciona bem com a maioria das páginas de entrada habilitadas com HTML, se eles usarem **IDs DIV conhecidos para o campo de nome de usuário e a senha de entrada**.</span><span class="sxs-lookup"><span data-stu-id="79e95-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field.</span></span> <span data-ttu-id="79e95-111">A maneira como isso funciona é pela captura do HTML na página para localizar IDs de DIV que correspondem a determinados critérios e salvando esses metadados para este aplicativo, para que possamos repetir senhas mais tarde.</span><span class="sxs-lookup"><span data-stu-id="79e95-111">The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords to it later.</span></span>

<span data-ttu-id="79e95-112">**Captura manual de campo de entrada** pode ser usada no caso do **fornecedor do aplicativo não rotular** os campos de entrada usados para entrar.</span><span class="sxs-lookup"><span data-stu-id="79e95-112">**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign in.</span></span> <span data-ttu-id="79e95-113">Captura manual de campo de entrada também pode ser usado no caso de quando o **fornecedor renderiza vários campos** que não podem ser detectados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="79e95-113">Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="79e95-114">O Azure AD pode armazenar dados para quantos campos forem necessários na página de entrada, contanto que você nos informe onde esses campos estão na página.</span><span class="sxs-lookup"><span data-stu-id="79e95-114">Azure AD can store data for as many fields as are on the sign in page, so long as you tell us where those fields are on the page.</span></span>

<span data-ttu-id="79e95-115">Em geral, **se captura manual do campo de entrada não funcionar, é recomendável sempre tentar a opção manual.**</span><span class="sxs-lookup"><span data-stu-id="79e95-115">In general, **if automatic sign-in field capture does not work, we always suggest trying the manual option.**</span></span>

### <a name="how-to-automatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="79e95-116">Como capturar automaticamente os campos de entrada para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="79e95-116">How to automatically capture sign-in fields for an application</span></span>

<span data-ttu-id="79e95-117">Configurar **Logon único baseado em senha** para um aplicativo usando **captura automática do campo de entrada**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="79e95-117">To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="79e95-118">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="79e95-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="79e95-119">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="79e95-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="79e95-120">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79e95-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="79e95-121">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="79e95-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="79e95-122">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="79e95-122">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="79e95-123">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="79e95-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="79e95-124">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="79e95-124">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="79e95-125">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79e95-125">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="79e95-126">Selecione o modo **Logon baseado em senha.**</span><span class="sxs-lookup"><span data-stu-id="79e95-126">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="79e95-127">Insira a **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="79e95-127">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="79e95-128">Esta é a URL no qual os usuários introduzem o nome de usuário e a senha para se conectarem.</span><span class="sxs-lookup"><span data-stu-id="79e95-128">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="79e95-129">**Verifique se os campos de entrada estão visíveis na URL que você fornece**.</span><span class="sxs-lookup"><span data-stu-id="79e95-129">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="79e95-130">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="79e95-130">Click the **Save** button.</span></span>

11. <span data-ttu-id="79e95-131">Depois de fazer isso, vamos extrair automaticamente essa URL para uma caixa de entrada de nome de usuário e de senha e permitir que você use o Azure AD para transmitir com segurança as senhas para o aplicativo usando a extensão de navegador de painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="79e95-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="how-to-manually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="79e95-132">Como capturar manualmente campos de entrada para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="79e95-132">How to manually capture sign-in fields for an application</span></span>

<span data-ttu-id="79e95-133">Para capturar manualmente os campos de entrada, você deve primeiramente ter a extensão de navegador do painel de acesso instalada e **não estar sendo executado no modo inPrivate, incógnito ou privado.**</span><span class="sxs-lookup"><span data-stu-id="79e95-133">To manually capture sign in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="79e95-134">Para instalar a extensão do navegador, siga as etapas na seção [Como instalar a extensão de navegador do painel de acesso](#i-cannot-manually-detect-sign-in-fields-for-my-application).</span><span class="sxs-lookup"><span data-stu-id="79e95-134">To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="79e95-135">Para configurar **Logon único baseado em senha** para um aplicativo usando **captura manual do campo de entrada**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="79e95-135">To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="79e95-136">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="79e95-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="79e95-137">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="79e95-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="79e95-138">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79e95-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="79e95-139">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="79e95-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="79e95-140">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="79e95-140">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="79e95-141">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="79e95-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="79e95-142">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="79e95-142">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="79e95-143">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79e95-143">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="79e95-144">Selecione o modo **Logon baseado em senha.**</span><span class="sxs-lookup"><span data-stu-id="79e95-144">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="79e95-145">Insira a **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="79e95-145">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="79e95-146">Esta é a URL no qual os usuários introduzem o nome de usuário e a senha para se conectarem.</span><span class="sxs-lookup"><span data-stu-id="79e95-146">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="79e95-147">**Verifique se os campos de entrada estão visíveis na URL que você fornece**.</span><span class="sxs-lookup"><span data-stu-id="79e95-147">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="79e95-148">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="79e95-148">Click the **Save** button.</span></span>

11. <span data-ttu-id="79e95-149">Depois de fazer isso, vamos extrair automaticamente essa URL para uma caixa de entrada de nome de usuário e de senha e permitir que você use o Azure AD para transmitir com segurança as senhas para o aplicativo usando a extensão de navegador de painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="79e95-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span> <span data-ttu-id="79e95-150">No caso em que isso falhar, você pode **alterar o modo de entrada para usar a captura manual do campo de entrada** continuando para a etapa 12.</span><span class="sxs-lookup"><span data-stu-id="79e95-150">In the case that this fails, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.</span></span>

12. <span data-ttu-id="79e95-151">clique em **Configurar &lt;appname&gt; configurações de logon único com senha**.</span><span class="sxs-lookup"><span data-stu-id="79e95-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="79e95-152">Selecione a opção de configuração **Detectar manualmente os campos de entrada**.</span><span class="sxs-lookup"><span data-stu-id="79e95-152">Select the **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="79e95-153">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="79e95-153">Click **Ok**.</span></span>

15. <span data-ttu-id="79e95-154">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="79e95-154">Click **Save**.</span></span>

16. <span data-ttu-id="79e95-155">Siga as instruções na tela para usar o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="79e95-155">Follow the on screen instructions to use the Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="79e95-156">Vejo o erro "Não foi possível encontrar os campos de entrada nessa URL"</span><span class="sxs-lookup"><span data-stu-id="79e95-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="79e95-157">Você vê este erro quando a detecção automática de campos de entrada falha.</span><span class="sxs-lookup"><span data-stu-id="79e95-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="79e95-158">Para resolver esse problema, tente detecção de campo de entrada manual, seguindo as etapas na seção [Como capturar manualmente os campos de entrada para um aplicativo](#how-to-manually-capture-sign-in-fields-for-an-application).</span><span class="sxs-lookup"><span data-stu-id="79e95-158">To resolve this issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-to-save-single-sign-on-configuration-error"></a><span data-ttu-id="79e95-159">Vejo um erro de "não é possível salvar a configuração de logon único"</span><span class="sxs-lookup"><span data-stu-id="79e95-159">I see an “Unable to save Single Sign-on configuration” error</span></span>

<span data-ttu-id="79e95-160">Em alguns casos raros, atualizar a configuração de logon único pode falhar.</span><span class="sxs-lookup"><span data-stu-id="79e95-160">In certain rare cases, updating the single sign-on configuration can fail.</span></span> <span data-ttu-id="79e95-161">Para resolver isso, tente salvar a configuração de logon único novamente.</span><span class="sxs-lookup"><span data-stu-id="79e95-161">TO resolve this try saving the single sign-on configuration again.</span></span>

<span data-ttu-id="79e95-162">Se isso continuar falhando consistentemente, abra um caso de suporte e forneça as informações coletadas das seções [Como ver os detalhes de uma notificação no portal](#i-cannot-manually-detect-sign-in-fields-for-my-application) e [Como obter ajuda enviando detalhes de notificação a um engenheiro de suporte](#how-to-get-help-by-sending-notification-details-to-a-support-engineer).</span><span class="sxs-lookup"><span data-stu-id="79e95-162">If this continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="79e95-163">Não posso manualmente detectar os campos de entrada para meu aplicativo</span><span class="sxs-lookup"><span data-stu-id="79e95-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="79e95-164">Alguns dos comportamentos que você pode ver quando a detecção manual não está funcionando incluem:</span><span class="sxs-lookup"><span data-stu-id="79e95-164">Some of the behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="79e95-165">O processo de captura manual pareceu funcionar, mas os campos capturados não estavam corretos</span><span class="sxs-lookup"><span data-stu-id="79e95-165">The manual capture process appeared to work, but the fields captured were not correct</span></span>

-   <span data-ttu-id="79e95-166">Os campos à direita não são destacados ao executar o processo de captura</span><span class="sxs-lookup"><span data-stu-id="79e95-166">The right fields don’t get highlighted when performing the capture process</span></span>

-   <span data-ttu-id="79e95-167">O processo de captura me leva à página de logon do aplicativo conforme o esperado, mas nada acontece</span><span class="sxs-lookup"><span data-stu-id="79e95-167">The capture process takes me to the application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="79e95-168">Captura manual parece funcionar, mas SSO não acontece quando meus usuários navegam para o aplicativo de painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="79e95-168">Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.</span></span>

<span data-ttu-id="79e95-169">Verifique se você encontra algum desses problemas:</span><span class="sxs-lookup"><span data-stu-id="79e95-169">check the following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="79e95-170">Verifique se você tem a versão mais recente da extensão de navegador do painel de acesso **instalada** e **habilitada**, seguindo as etapas na seção [Como instalar a extensão de navegador do painel de acesso](#how-to-install-the-access-panel-browser-extension).</span><span class="sxs-lookup"><span data-stu-id="79e95-170">Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="79e95-171">Certifique-se de que você não está tentando o processo de captura ao seu navegador em **modo incógnito, inPrivate ou privado**.</span><span class="sxs-lookup"><span data-stu-id="79e95-171">Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="79e95-172">Não há suporte para a extensão do painel de acesso nesses modos.</span><span class="sxs-lookup"><span data-stu-id="79e95-172">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="79e95-173">Certifique-se de que os usuários não estão tentando entrar no aplicativo usando o painel de acesso no **modo incógnita, inPrivate ou privado**.</span><span class="sxs-lookup"><span data-stu-id="79e95-173">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="79e95-174">Não há suporte para a extensão do painel de acesso nesses modos.</span><span class="sxs-lookup"><span data-stu-id="79e95-174">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="79e95-175">Tente o processo de captura manual novamente, garantindo que os marcadores vermelhos estão sobre os campos corretos.</span><span class="sxs-lookup"><span data-stu-id="79e95-175">Try the manual capture process again, ensuring the red markers are over the correct fields.</span></span>

-   <span data-ttu-id="79e95-176">Se o processo de captura manual parece parar de responder, ou na página de entrada não faz nada (caso 3 acima), repita o processo de captura manual.</span><span class="sxs-lookup"><span data-stu-id="79e95-176">If the manual capture process seems to hang, or the sign in page doesn’t do anything (case 3 above), try the manual capture process again.</span></span> <span data-ttu-id="79e95-177">Mas, desta vez depois de concluir o processo, pressione **F12** para abrir o console do desenvolvedor do navegador.</span><span class="sxs-lookup"><span data-stu-id="79e95-177">But, this time after completing the process, press the **F12** button to open your browser’s developer console.</span></span> <span data-ttu-id="79e95-178">Uma vez lá, abra o **console** e digite **window.location= "&lt; insira o símbolo na URL de conexão que você especificou ao configurar o aplicativo&gt;"** e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="79e95-178">Once there, open the **console** and type **window.location=”&lt;enter the sign in url you specified when configuring the app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="79e95-179">Isso força um redirecionamento da página que termina o processo de captura e armazena os campos que foram capturados.</span><span class="sxs-lookup"><span data-stu-id="79e95-179">This force a page redirect which end the capture process and store the fields that have been captured.</span></span>

<span data-ttu-id="79e95-180">Se nenhuma dessas abordagens funcionar para você, podemos ajudar.</span><span class="sxs-lookup"><span data-stu-id="79e95-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="79e95-181">Abra um caso de suporte com os detalhes de que você tentou, bem como as informações coletadas das seções [Como ver os detalhes de uma notificação no portal](#i-cannot-manually-detect-sign-in-fields-for-my-application) e [Como obter ajuda enviando detalhes de notificação a um engenheiro de suporte](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) (se aplicável).</span><span class="sxs-lookup"><span data-stu-id="79e95-181">Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="79e95-182">Como instalar a extensão do Navegador do Painel de Acesso</span><span class="sxs-lookup"><span data-stu-id="79e95-182">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="79e95-183">Para instalar a extensão do Navegador do Painel de Acesso, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="79e95-183">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="79e95-184">Abra o [Painel de Acesso](https://myapps.microsoft.com) em um dos navegadores compatíveis e entre como um **usuário** no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79e95-184">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="79e95-185">Clique no **aplicativo de SSO com senha** no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="79e95-185">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="79e95-186">No prompt solicitando a instalação do software, selecione **Instalar Agora**.</span><span class="sxs-lookup"><span data-stu-id="79e95-186">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="79e95-187">Com base no seu navegador, você será direcionado para o link de download.</span><span class="sxs-lookup"><span data-stu-id="79e95-187">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="79e95-188">**Adicione** a extensão ao seu navegador.</span><span class="sxs-lookup"><span data-stu-id="79e95-188">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="79e95-189">Se o navegador solicitar, selecione como **Habilitar** ou **Permitir** a extensão.</span><span class="sxs-lookup"><span data-stu-id="79e95-189">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="79e95-190">Quando estiver instalado, **reinicie** a sessão do navegador.</span><span class="sxs-lookup"><span data-stu-id="79e95-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="79e95-191">Entrar no Painel de Acesso e ver se é possível **iniciar** os aplicativos de SSO de senha.</span><span class="sxs-lookup"><span data-stu-id="79e95-191">Sign in into the Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="79e95-192">Também é possível baixar a extensão para Chrome e Firefox diretamente pelos links abaixo:</span><span class="sxs-lookup"><span data-stu-id="79e95-192">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="79e95-193">Extensão do Painel de Acesso do Chrome</span><span class="sxs-lookup"><span data-stu-id="79e95-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="79e95-194">Extensão do Painel de Acesso do Firefox</span><span class="sxs-lookup"><span data-stu-id="79e95-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="79e95-195">Como ver os detalhes de uma notificação do portal</span><span class="sxs-lookup"><span data-stu-id="79e95-195">How to see the details of a portal notification</span></span>

<span data-ttu-id="79e95-196">Veja os detalhes de qualquer notificação do portal executando as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="79e95-196">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="79e95-197">Clique no ícone **Notificações** (o sino) na parte superior direita do Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="79e95-197">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="79e95-198">Selecione qualquer notificação com estado de **Erro** (aquelas com um (!) vermelho ao lado).</span><span class="sxs-lookup"><span data-stu-id="79e95-198">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

  ><span data-ttu-id="79e95-199">!NOTA] Não é possível clicar em notificações com estado de **Êxito** ou **Em Andamento**.</span><span class="sxs-lookup"><span data-stu-id="79e95-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="79e95-200">Isso abre a folha **Detalhes da Notificação**.</span><span class="sxs-lookup"><span data-stu-id="79e95-200">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="79e95-201">Use essas informações para saber mais detalhes sobre o problema.</span><span class="sxs-lookup"><span data-stu-id="79e95-201">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="79e95-202">Se ainda precisar de ajuda, você também poderá compartilhar essas informações com um engenheiro de suporte ou com o grupo de produtos para obter ajuda com o problema.</span><span class="sxs-lookup"><span data-stu-id="79e95-202">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="79e95-203">Clique no **ícone** de **cópia** à direita da caixa de texto **Copiar erro** para copiar todos os detalhes da notificação para compartilhar com um engenheiro de suporte ou de grupo de produtos.</span><span class="sxs-lookup"><span data-stu-id="79e95-203">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="79e95-204">Como obter ajuda enviando detalhes da notificação a um engenheiro de suporte</span><span class="sxs-lookup"><span data-stu-id="79e95-204">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="79e95-205">É muito importante que você compartilhe **todos os detalhes abaixo** com um engenheiro de suporte caso precise de ajuda, para que ele possa ajudar rapidamente.</span><span class="sxs-lookup"><span data-stu-id="79e95-205">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="79e95-206">Faça isso facilmente **tirando uma captura de tela** ou clicando no **ícone Copiar erro**, localizado à direita da caixa de texto **Copiar erro**.</span><span class="sxs-lookup"><span data-stu-id="79e95-206">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="79e95-207">Detalhes da notificação explicados</span><span class="sxs-lookup"><span data-stu-id="79e95-207">Notification Details Explained</span></span>

<span data-ttu-id="79e95-208">Abaixo, explicamos mais sobre o significado de cada item de notificação e fornecemos exemplos de cada um deles.</span><span class="sxs-lookup"><span data-stu-id="79e95-208">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="79e95-209">Itens de notificação essenciais</span><span class="sxs-lookup"><span data-stu-id="79e95-209">Essential Notification Items</span></span>

-   <span data-ttu-id="79e95-210">**Título** – o título descritivo da notificação</span><span class="sxs-lookup"><span data-stu-id="79e95-210">**Title** – the descriptive title of the notification</span></span>

    -   <span data-ttu-id="79e95-211">Exemplo – **Configurações do proxy do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="79e95-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="79e95-212">**Descrição** – a descrição do que ocorreu como resultado da operação</span><span class="sxs-lookup"><span data-stu-id="79e95-212">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="79e95-213">Exemplo – **A URL interna inserida já está sendo usada por outro aplicativo**</span><span class="sxs-lookup"><span data-stu-id="79e95-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="79e95-214">**ID da Notificação** – a ID exclusiva da notificação</span><span class="sxs-lookup"><span data-stu-id="79e95-214">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="79e95-215">Exemplo – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="79e95-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="79e95-216">**ID de Solicitação do Cliente** – a ID de solicitação específica feita por seu navegador</span><span class="sxs-lookup"><span data-stu-id="79e95-216">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="79e95-217">Exemplo – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="79e95-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="79e95-218">**Carimbo de Data/Hora UTC** – o carimbo de data/hora durante o qual a notificação ocorreu, em UTC</span><span class="sxs-lookup"><span data-stu-id="79e95-218">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="79e95-219">Exemplo – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="79e95-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="79e95-220">**ID de Transação Interna** – a ID interna que podemos usar para procurar o erro em nossos sistemas</span><span class="sxs-lookup"><span data-stu-id="79e95-220">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="79e95-221">Exemplo – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="79e95-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="79e95-222">**UPN** – o usuário que realizou a operação</span><span class="sxs-lookup"><span data-stu-id="79e95-222">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="79e95-223">Exemplo – **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="79e95-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="79e95-224">**Id do Locatário** – a ID exclusiva do locatário do qual o usuário que realizou a operação era membro</span><span class="sxs-lookup"><span data-stu-id="79e95-224">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="79e95-225">Exemplo – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="79e95-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="79e95-226">**Id de objeto de usuário** – a ID exclusiva do usuário que realizou a operação</span><span class="sxs-lookup"><span data-stu-id="79e95-226">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="79e95-227">Exemplo – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="79e95-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="79e95-228">Itens de notificação detalhados</span><span class="sxs-lookup"><span data-stu-id="79e95-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="79e95-229">**Nome de Exibição** – **(pode estar vazio)** um nome de exibição mais detalhado do erro</span><span class="sxs-lookup"><span data-stu-id="79e95-229">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="79e95-230">Exemplo *– **Configurações do proxy do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="79e95-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="79e95-231">**Status** – o status específico da notificação</span><span class="sxs-lookup"><span data-stu-id="79e95-231">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="79e95-232">Exemplo – **Falha**</span><span class="sxs-lookup"><span data-stu-id="79e95-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="79e95-233">**Id do Objeto** – **(pode estar vazio)** a ID do objeto em que a operação foi executada</span><span class="sxs-lookup"><span data-stu-id="79e95-233">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="79e95-234">Exemplo – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="79e95-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="79e95-235">**Detalhes** – a descrição detalhada do que ocorreu como resultado da operação</span><span class="sxs-lookup"><span data-stu-id="79e95-235">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="79e95-236">Exemplo – **A URL interna 'http://bing.com/' é inválida, uma vez que está sendo utilizada**</span><span class="sxs-lookup"><span data-stu-id="79e95-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="79e95-237">**Copiar erro** – clique no **ícone de cópia** à direita da caixa de texto **Copiar erro** para copiar todos os detalhes de notificação para compartilhar com um engenheiro de suporte ou de grupo de produtos</span><span class="sxs-lookup"><span data-stu-id="79e95-237">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="79e95-238">Exemplo – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="79e95-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="79e95-239">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79e95-239">Next steps</span></span>
[<span data-ttu-id="79e95-240">Fornecer logon único para seus aplicativos com Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="79e95-240">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

