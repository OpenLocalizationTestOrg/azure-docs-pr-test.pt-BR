---
title: "autenticação do Google tooconfigure aaaHow para seu aplicativo de serviços de aplicativos"
description: "Saiba como autenticação do Google tooconfigure para seu aplicativo de serviços de aplicativos."
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
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a><span data-ttu-id="91a21-103">Como tooconfigure o logon do serviço de aplicativo aplicativo toouse Google</span><span class="sxs-lookup"><span data-stu-id="91a21-103">How tooconfigure your App Service application toouse Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="91a21-104">Este tópico mostra como tooconfigure do serviço de aplicativo do Azure toouse Google como um provedor de autenticação.</span><span class="sxs-lookup"><span data-stu-id="91a21-104">This topic shows you how tooconfigure Azure App Service toouse Google as an authentication provider.</span></span>

<span data-ttu-id="91a21-105">toocomplete Olá procedimento neste tópico, você deve ter uma conta do Google que tem um endereço de email verificado.</span><span class="sxs-lookup"><span data-stu-id="91a21-105">toocomplete hello procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="91a21-106">toocreate uma nova conta do Google, vá muito[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="91a21-106">toocreate a new Google account, go too[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="91a21-107"><a name="register"> </a>Registre seu aplicativo com o Google</span><span class="sxs-lookup"><span data-stu-id="91a21-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="91a21-108">Faça logon no toohello [portal do Azure]e navegue tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91a21-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="91a21-109">Copiar seu **URL**, que você usar tooconfigure posterior seu aplicativo do Google.</span><span class="sxs-lookup"><span data-stu-id="91a21-109">Copy your **URL**, which you use later tooconfigure your Google app.</span></span>
2. <span data-ttu-id="91a21-110">Navegue toohello [apis do Google](http://go.microsoft.com/fwlink/p/?LinkId=268303) site, entrar com suas credenciais de conta do Google, clique em **criar projeto**, forneça um **nome do projeto**, em seguida, clique em  **Criar**.</span><span class="sxs-lookup"><span data-stu-id="91a21-110">Navigate toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="91a21-111">Em **APIs Sociais**, clique em **API do Google+** e em **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="91a21-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="91a21-112">Na saudação à esquerda de navegação, **credenciais** > **tela de consentimento de OAuth**, em seguida, selecione seu **endereço de Email**, insira um **nome do produto**e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="91a21-112">In hello left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="91a21-113">Em Olá **credenciais** , clique em **criar credenciais** > **ID do cliente OAuth**, em seguida, selecione **aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="91a21-113">In hello **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="91a21-114">Colar Olá do serviço de aplicativo **URL** você copiou anteriormente em **origens autorizadas de JavaScript**, em seguida, cole o redirecionamento de URI em **URI de redirecionamento autorizado**.</span><span class="sxs-lookup"><span data-stu-id="91a21-114">Paste hello App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="91a21-115">Olá redirecionar URI é a URL de saudação do seu aplicativo anexado ao caminho hello, */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="91a21-115">hello redirect URI is hello URL of your application appended with hello path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="91a21-116">Por exemplo: `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="91a21-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="91a21-117">Certifique-se de que você está usando o esquema do hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="91a21-117">Make sure that you are using hello HTTPS scheme.</span></span> <span data-ttu-id="91a21-118">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="91a21-118">Then click **Create**.</span></span>
7. <span data-ttu-id="91a21-119">Na próxima tela de Olá, anote os valores de saudação do cliente de saudação segredo do cliente e a ID.</span><span class="sxs-lookup"><span data-stu-id="91a21-119">On hello next screen, make a note of hello values of hello client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="91a21-120">segredo do cliente Olá é uma credencial de segurança importantes.</span><span class="sxs-lookup"><span data-stu-id="91a21-120">hello client secret is an important security credential.</span></span> <span data-ttu-id="91a21-121">Não compartilhe essa senha com ninguém nem distribua-a em um aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="91a21-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="91a21-122"><a name="secrets"></a>Aplicativo do Google adicionar informações tooyour</span><span class="sxs-lookup"><span data-stu-id="91a21-122"><a name="secrets"> </a>Add Google information tooyour application</span></span>
1. <span data-ttu-id="91a21-123">Em Olá [portal do Azure], navegar tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91a21-123">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="91a21-124">Clique em **Configurações** e em **Autenticação/Autorização**.</span><span class="sxs-lookup"><span data-stu-id="91a21-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="91a21-125">Se Olá autenticação / autorização de recurso não está ativada, ative o comutador hello muito**em**.</span><span class="sxs-lookup"><span data-stu-id="91a21-125">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="91a21-126">Clique em **Google**.</span><span class="sxs-lookup"><span data-stu-id="91a21-126">Click **Google**.</span></span> <span data-ttu-id="91a21-127">Cole em valores de ID do aplicativo e o segredo do aplicativo hello que você obteve anteriormente e, opcionalmente, habilitar os escopos que seu aplicativo requer.</span><span class="sxs-lookup"><span data-stu-id="91a21-127">Paste in hello App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="91a21-128">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="91a21-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="91a21-129">Por padrão, o serviço de aplicativo fornece autenticação, mas não restringe o conteúdo do site tooyour acesso autorizado e APIs.</span><span class="sxs-lookup"><span data-stu-id="91a21-129">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="91a21-130">Você deve autorizar os usuários no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91a21-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="91a21-131">(Opcional) toorestrict acesso tooyour site tooonly usuários autenticados pelo Google, definir **tootake de ação quando a solicitação não está autenticada** muito**Google**.</span><span class="sxs-lookup"><span data-stu-id="91a21-131">(Optional) toorestrict access tooyour site tooonly users authenticated by Google, set **Action tootake when request is not authenticated** too**Google**.</span></span> <span data-ttu-id="91a21-132">Isso requer que todas as solicitações autenticadas e todas as solicitações não autenticadas são redirecionada tooGoogle para autenticação.</span><span class="sxs-lookup"><span data-stu-id="91a21-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooGoogle for authentication.</span></span>
5. <span data-ttu-id="91a21-133">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="91a21-133">Click **Save**.</span></span>

<span data-ttu-id="91a21-134">Agora você está pronto toouse Google para autenticação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91a21-134">You are now ready toouse Google for authentication in your app.</span></span>

## <span data-ttu-id="91a21-135"><a name="related-content"> </a>Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="91a21-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portal do Azure]: https://portal.azure.com/

