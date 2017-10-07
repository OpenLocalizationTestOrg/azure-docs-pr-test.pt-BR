---
title: "autenticação aaaHow tooconfigure Account da Microsoft para o seu aplicativo de serviços de aplicativos"
description: "Saiba como a autenticação tooconfigure Account da Microsoft para o seu aplicativo de serviços de aplicativos."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a><span data-ttu-id="cf774-103">Como tooconfigure seu logon do serviço de aplicativo aplicativo toouse Account da Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf774-103">How tooconfigure your App Service application toouse Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="cf774-104">Este tópico mostra como tooconfigure do serviço de aplicativo do Azure toouse Account da Microsoft como um provedor de autenticação.</span><span class="sxs-lookup"><span data-stu-id="cf774-104">This topic shows you how tooconfigure Azure App Service toouse Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="cf774-105"><a name="register-microsoft-account"> </a>Registrar seu aplicativo na conta da Microsoft</span><span class="sxs-lookup"><span data-stu-id="cf774-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="cf774-106">Faça logon no toohello [portal do Azure]e navegue tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf774-106">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="cf774-107">Copiar seu **URL**, que posteriormente você usar tooconfigure seu aplicativo com Account da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cf774-107">Copy your **URL**, which later you use tooconfigure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="cf774-108">Navegue toohello [meus aplicativos] página Olá Microsoft Account Developer Center e faça logon com sua conta da Microsoft, se necessário.</span><span class="sxs-lookup"><span data-stu-id="cf774-108">Navigate toohello [My Applications] page in hello Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="cf774-109">Clique em **Adicionar um aplicativo** e digite um nome de aplicativo e clique em **Criar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="cf774-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="cf774-110">Anote Olá **ID do aplicativo**, pois você precisará dele mais tarde.</span><span class="sxs-lookup"><span data-stu-id="cf774-110">Make a note of hello **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="cf774-111">Em "Plataformas", clique em **Adicionar plataforma** e selecione "Web".</span><span class="sxs-lookup"><span data-stu-id="cf774-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="cf774-112">Em "URIs de redirecionamento" fonte Olá ponto de extremidade para seu aplicativo, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="cf774-112">Under "Redirect URIs" supply hello endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="cf774-113">O redirecionamento de URI é a URL de saudação do seu aplicativo anexado ao caminho hello, */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="cf774-113">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="cf774-114">Por exemplo: `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="cf774-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="cf774-115">Certifique-se de que você está usando o esquema do hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cf774-115">Make sure that you are using hello HTTPS scheme.</span></span>
   
7. <span data-ttu-id="cf774-116">Em "Segredos do Aplicativo", clique em **Gerar nova senha**.</span><span class="sxs-lookup"><span data-stu-id="cf774-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="cf774-117">Anote o valor de saudação que aparece.</span><span class="sxs-lookup"><span data-stu-id="cf774-117">Make note of hello value that appears.</span></span> <span data-ttu-id="cf774-118">Depois que você sair página hello, ele não aparecerá novamente.</span><span class="sxs-lookup"><span data-stu-id="cf774-118">Once you leave hello page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="cf774-119">senha Olá é uma credencial de segurança importantes.</span><span class="sxs-lookup"><span data-stu-id="cf774-119">hello password is an important security credential.</span></span> <span data-ttu-id="cf774-120">Não compartilhe Olá senha com ninguém ou distribuí-lo em um aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="cf774-120">Do not share hello password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="cf774-121"><a name="secrets"></a>Adicionar conta da Microsoft informações tooyour aplicativo de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="cf774-121"><a name="secrets"> </a>Add Microsoft Account information tooyour App Service application</span></span>
1. <span data-ttu-id="cf774-122">Em Olá [portal do Azure], navegar tooyour aplicativo, clique em **configurações** > **autenticação / autorização**.</span><span class="sxs-lookup"><span data-stu-id="cf774-122">Back in hello [Azure portal], navigate tooyour application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="cf774-123">Se Olá autenticação / autorização de recurso não está habilitada, alternar **em**.</span><span class="sxs-lookup"><span data-stu-id="cf774-123">If hello Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="cf774-124">Clique em **Conta da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="cf774-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="cf774-125">Cole em valores hello ID do aplicativo e a senha que você obteve anteriormente e, opcionalmente, habilitar os escopos que seu aplicativo requer.</span><span class="sxs-lookup"><span data-stu-id="cf774-125">Paste in hello Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="cf774-126">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf774-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="cf774-127">Por padrão, o serviço de aplicativo fornece autenticação, mas não restringe o conteúdo do site tooyour acesso autorizado e APIs.</span><span class="sxs-lookup"><span data-stu-id="cf774-127">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="cf774-128">Você deve autorizar os usuários no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf774-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="cf774-129">(Opcional) toorestrict acesso tooyour site tooonly usuários autenticados por conta da Microsoft, definir **tootake de ação quando a solicitação não está autenticada** muito**Microsoft Account**.</span><span class="sxs-lookup"><span data-stu-id="cf774-129">(Optional) toorestrict access tooyour site tooonly users authenticated by Microsoft account, set **Action tootake when request is not authenticated** too**Microsoft Account**.</span></span> <span data-ttu-id="cf774-130">Isso requer que todas as solicitações autenticadas, e todas as solicitações não autenticadas são redirecionadas tooMicrosoft conta para autenticação.</span><span class="sxs-lookup"><span data-stu-id="cf774-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooMicrosoft account for authentication.</span></span>
5. <span data-ttu-id="cf774-131">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cf774-131">Click **Save**.</span></span>

<span data-ttu-id="cf774-132">Agora você está pronto toouse Account da Microsoft para autenticação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf774-132">You are now ready toouse Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="cf774-133"><a name="related-content"> </a>Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="cf774-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[meus aplicativos]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[portal do Azure]: https://portal.azure.com/
