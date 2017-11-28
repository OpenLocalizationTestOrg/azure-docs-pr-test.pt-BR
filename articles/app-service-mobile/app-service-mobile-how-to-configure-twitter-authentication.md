---
title: "autenticação do Twitter tooconfigure aaaHow para seu aplicativo de serviços de aplicativos"
description: "Saiba como autenticação do Twitter tooconfigure para seu aplicativo de serviços de aplicativos."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a><span data-ttu-id="902bb-103">Como tooconfigure seu logon do serviço de aplicativo aplicativo toouse Twitter</span><span class="sxs-lookup"><span data-stu-id="902bb-103">How tooconfigure your App Service application toouse Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="902bb-104">Este tópico mostra como tooconfigure do serviço de aplicativo do Azure toouse Twitter como um provedor de autenticação.</span><span class="sxs-lookup"><span data-stu-id="902bb-104">This topic shows you how tooconfigure Azure App Service toouse Twitter as an authentication provider.</span></span>

<span data-ttu-id="902bb-105">toocomplete Olá procedimento neste tópico, você deve ter uma conta do Twitter que tem um número de telefone e endereço de email verificado.</span><span class="sxs-lookup"><span data-stu-id="902bb-105">toocomplete hello procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="902bb-106">toocreate uma nova conta do Twitter, ir muito<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="902bb-106">toocreate a new Twitter account, go too<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="902bb-107"><a name="register"> </a>Registre seu aplicativo com o Twitter</span><span class="sxs-lookup"><span data-stu-id="902bb-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="902bb-108">Faça logon no toohello [portal do Azure]e navegue tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="902bb-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="902bb-109">Copie a **URL**.</span><span class="sxs-lookup"><span data-stu-id="902bb-109">Copy your **URL**.</span></span> <span data-ttu-id="902bb-110">Você usará esse tooconfigure seu aplicativo do Twitter.</span><span class="sxs-lookup"><span data-stu-id="902bb-110">You will use this tooconfigure your Twitter app.</span></span>
2. <span data-ttu-id="902bb-111">Navegue toohello [Twitter desenvolvedores] site da Web, entre com suas credenciais de conta do Twitter e clique em **criar novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="902bb-111">Navigate toohello [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="902bb-112">Tipo de saudação **nome** e um **descrição** para seu novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="902bb-112">Type in hello **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="902bb-113">Colar em seu aplicativo **URL** para Olá **site** valor.</span><span class="sxs-lookup"><span data-stu-id="902bb-113">Paste in your application's **URL** for hello **Website** value.</span></span> <span data-ttu-id="902bb-114">Em seguida, para Olá **URL de retorno de chamada**, cole Olá **URL de retorno de chamada** copiados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="902bb-114">Then, for hello **Callback URL**, paste hello **Callback URL** you copied earlier.</span></span> <span data-ttu-id="902bb-115">Este é o seu gateway de aplicativo móvel anexado ao caminho hello, */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="902bb-115">This is your Mobile App gateway appended with hello path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="902bb-116">Por exemplo: `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="902bb-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="902bb-117">Certifique-se de que você está usando o esquema do hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="902bb-117">Make sure that you are using hello HTTPS scheme.</span></span>
4. <span data-ttu-id="902bb-118">Na página de saudação do hello inferior, leia e aceite os termos de saudação.</span><span class="sxs-lookup"><span data-stu-id="902bb-118">At hello bottom hello page, read and accept hello terms.</span></span> <span data-ttu-id="902bb-119">Em seguida, clique em **Criar seu Aplicativo do Twitter**.</span><span class="sxs-lookup"><span data-stu-id="902bb-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="902bb-120">Este aplicativo de saudação registra exibe detalhes do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="902bb-120">This registers hello app displays hello application details.</span></span>
5. <span data-ttu-id="902bb-121">Clique Olá **configurações** guia seleção **permitir toosign de toobe usado neste aplicativo com o Twitter**, em seguida, clique em **configurações de atualização**.</span><span class="sxs-lookup"><span data-stu-id="902bb-121">Click hello **Settings** tab, check **Allow this application toobe used toosign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="902bb-122">Selecione Olá **chaves e Tokens de acesso** guia. Anote os valores de saudação do **chave do consumidor (chave de API)** e **segredo do consumidor (segredo de API)**.</span><span class="sxs-lookup"><span data-stu-id="902bb-122">Select hello **Keys and Access Tokens** tab. Make a note of hello values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="902bb-123">segredo do consumidor Olá é uma credencial de segurança importantes.</span><span class="sxs-lookup"><span data-stu-id="902bb-123">hello consumer secret is an important security credential.</span></span> <span data-ttu-id="902bb-124">Não compartilhe esse segredo com ninguém nem o distribua com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="902bb-124">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="902bb-125"><a name="secrets"></a>Twitter Adicionar aplicativo do information tooyour</span><span class="sxs-lookup"><span data-stu-id="902bb-125"><a name="secrets"> </a>Add Twitter information tooyour application</span></span>
1. <span data-ttu-id="902bb-126">Em Olá [portal do Azure], navegar tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="902bb-126">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="902bb-127">Clique em **Configurações** e em **Autenticação/Autorização**.</span><span class="sxs-lookup"><span data-stu-id="902bb-127">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="902bb-128">Se Olá autenticação / autorização de recurso não está ativada, ative o comutador hello muito**em**.</span><span class="sxs-lookup"><span data-stu-id="902bb-128">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="902bb-129">Clique em **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="902bb-129">Click **Twitter**.</span></span> <span data-ttu-id="902bb-130">Cole em hello ID do aplicativo e o segredo do aplicativo valores que você obteve anteriormente.</span><span class="sxs-lookup"><span data-stu-id="902bb-130">Paste in hello App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="902bb-131">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="902bb-131">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="902bb-132">Por padrão, o serviço de aplicativo fornece autenticação, mas não restringe o conteúdo do site tooyour acesso autorizado e APIs.</span><span class="sxs-lookup"><span data-stu-id="902bb-132">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="902bb-133">Você deve autorizar os usuários no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="902bb-133">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="902bb-134">(Opcional) toorestrict acesso tooyour site tooonly usuários autenticados pelo Twitter, definir **tootake de ação quando a solicitação não está autenticada** muito**Twitter**.</span><span class="sxs-lookup"><span data-stu-id="902bb-134">(Optional) toorestrict access tooyour site tooonly users authenticated by Twitter, set **Action tootake when request is not authenticated** too**Twitter**.</span></span> <span data-ttu-id="902bb-135">Isso requer que todas as solicitações autenticadas e todas as solicitações não autenticadas são redirecionada tooTwitter para autenticação.</span><span class="sxs-lookup"><span data-stu-id="902bb-135">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooTwitter for authentication.</span></span>
5. <span data-ttu-id="902bb-136">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="902bb-136">Click **Save**.</span></span>

<span data-ttu-id="902bb-137">Agora você está pronto toouse Twitter para autenticação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="902bb-137">You are now ready toouse Twitter for authentication in your app.</span></span>

## <span data-ttu-id="902bb-138"><a name="related-content"> </a>Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="902bb-138"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter desenvolvedores]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[portal do Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
