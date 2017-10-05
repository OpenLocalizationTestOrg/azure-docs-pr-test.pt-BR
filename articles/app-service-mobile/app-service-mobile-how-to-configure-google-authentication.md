---
title: "Como configurar a autenticação do Google para seu aplicativo de Serviços de Aplicativos"
description: "Saiba como configurar a autenticação do Google para seu aplicativo de Serviços de Aplicativos."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d6c1707f67d986487e5a45e76ffc9a02ddf16eb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-google-login"></a><span data-ttu-id="d007f-103">Como configurar seu aplicativo do Serviço de Aplicativo para usar o logon do Google</span><span class="sxs-lookup"><span data-stu-id="d007f-103">How to configure your App Service application to use Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="d007f-104">Este tópico mostra como configurar o Serviço de Aplicativo do Azure para usar o Google como um provedor de autenticação.</span><span class="sxs-lookup"><span data-stu-id="d007f-104">This topic shows you how to configure Azure App Service to use Google as an authentication provider.</span></span>

<span data-ttu-id="d007f-105">Para concluir o procedimento neste tópico, você deve ter uma conta do Google com um endereço de email verificado.</span><span class="sxs-lookup"><span data-stu-id="d007f-105">To complete the procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="d007f-106">Para criar uma nova conta do Google, vá para [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="d007f-106">To create a new Google account, go to [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="d007f-107"><a name="register"> </a>Registre seu aplicativo com o Google</span><span class="sxs-lookup"><span data-stu-id="d007f-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="d007f-108">Faça logon no [portal do Azure]e navegue até o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d007f-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="d007f-109">Copie a **URL**, pois você a usará mais tarde para configurar seu aplicativo do Google.</span><span class="sxs-lookup"><span data-stu-id="d007f-109">Copy your **URL**, which you use later to configure your Google app.</span></span>
2. <span data-ttu-id="d007f-110">Vá até o site [de apis do Google](http://go.microsoft.com/fwlink/p/?LinkId=268303) faça logon com suas credenciais de conta do Google, clique em **Criar Projeto**, forneça um **Nome do projeto** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d007f-110">Navigate to the [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="d007f-111">Em **APIs Sociais**, clique em **API do Google+** e em **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="d007f-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="d007f-112">No painel de navegação à esquerda, clique em **Credenciais** > **Tela de consentimento de OAuth**, selecione seu **Endereço de email**, insira um **Nome do Produto** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d007f-112">In the left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="d007f-113">Na guia **Credenciais**, clique em **Criar credenciais** > **ID do cliente OAuth** e, então, selecione **Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="d007f-113">In the **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="d007f-114">Cole a **URL** do Serviço de Aplicativo que você copiou anteriormente em **Origens Autorizadas do JavaScript** e, então, cole seu URI de Redirecionamento em **URI de Redirecionamento Autorizado**.</span><span class="sxs-lookup"><span data-stu-id="d007f-114">Paste the App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="d007f-115">O URI de redirecionamento é a URL do seu aplicativo acrescentada com o caminho */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="d007f-115">The redirect URI is the URL of your application appended with the path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="d007f-116">Por exemplo: `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="d007f-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="d007f-117">Certifique-se de que você está usando o esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d007f-117">Make sure that you are using the HTTPS scheme.</span></span> <span data-ttu-id="d007f-118">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d007f-118">Then click **Create**.</span></span>
7. <span data-ttu-id="d007f-119">Na próxima tela, anote os valores de ID do cliente e de segredo do cliente.</span><span class="sxs-lookup"><span data-stu-id="d007f-119">On the next screen, make a note of the values of the client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d007f-120">O segredo do cliente é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="d007f-120">The client secret is an important security credential.</span></span> <span data-ttu-id="d007f-121">Não compartilhe essa senha com ninguém nem distribua-a em um aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="d007f-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="d007f-122"><a name="secrets"> </a>Adicionar informações do Google ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="d007f-122"><a name="secrets"> </a>Add Google information to your application</span></span>
1. <span data-ttu-id="d007f-123">De volta ao [portal do Azure], navegue até o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d007f-123">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="d007f-124">Clique em **Configurações** e em **Autenticação/Autorização**.</span><span class="sxs-lookup"><span data-stu-id="d007f-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="d007f-125">Se o recurso Autenticação / Autorização não estiver habilitado, mude a opção para **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="d007f-125">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="d007f-126">Clique em **Google**.</span><span class="sxs-lookup"><span data-stu-id="d007f-126">Click **Google**.</span></span> <span data-ttu-id="d007f-127">Cole os valores de ID do Aplicativo e de Segredo do Aplicativo que você obteve anteriormente e, opcionalmente, habilite os escopos exigidos pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d007f-127">Paste in the App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="d007f-128">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d007f-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="d007f-129">Por padrão, o Serviço de Aplicativo fornece autenticação, mas não restringe o acesso autorizado ao conteúdo do site e às APIs.</span><span class="sxs-lookup"><span data-stu-id="d007f-129">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="d007f-130">Você deve autorizar os usuários no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d007f-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="d007f-131">(Opcional) Para restringir o acesso ao seu site somente para usuários autenticados pelo Google, defina **Ação a ser executada quando a solicitação não for autenticada** como **Google**.</span><span class="sxs-lookup"><span data-stu-id="d007f-131">(Optional) To restrict access to your site to only users authenticated by Google, set **Action to take when request is not authenticated** to **Google**.</span></span> <span data-ttu-id="d007f-132">Isso exige que todas as solicitações sejam autenticadas e todas as solicitações não autenticadas sejam redirecionadas ao Google para autenticação.</span><span class="sxs-lookup"><span data-stu-id="d007f-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Google for authentication.</span></span>
5. <span data-ttu-id="d007f-133">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d007f-133">Click **Save**.</span></span>

<span data-ttu-id="d007f-134">Agora você está pronto para usar o Google para autenticação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d007f-134">You are now ready to use Google for authentication in your app.</span></span>

## <span data-ttu-id="d007f-135"><a name="related-content"> </a>Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="d007f-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portal do Azure]: https://portal.azure.com/

