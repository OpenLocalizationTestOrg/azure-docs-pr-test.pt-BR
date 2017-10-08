---
title: "autenticação do Facebook tooconfigure aaaHow para seu aplicativo de serviços de aplicativos"
description: "Saiba como a autenticação do Facebook tooconfigure para seu aplicativo de serviços de aplicativos."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a><span data-ttu-id="91851-103">Como tooconfigure o logon do Facebook do serviço de aplicativo aplicativo toouse</span><span class="sxs-lookup"><span data-stu-id="91851-103">How tooconfigure your App Service application toouse Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="91851-104">Este tópico mostra como tooconfigure do serviço de aplicativo do Azure toouse Facebook como um provedor de autenticação.</span><span class="sxs-lookup"><span data-stu-id="91851-104">This topic shows you how tooconfigure Azure App Service toouse Facebook as an authentication provider.</span></span>

<span data-ttu-id="91851-105">toocomplete Olá procedimento neste tópico, você deve ter uma conta do Facebook que tem um endereço de email verificado e o número de telefone celular.</span><span class="sxs-lookup"><span data-stu-id="91851-105">toocomplete hello procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="91851-106">toocreate uma nova conta do Facebook, ir muito[facebook.com].</span><span class="sxs-lookup"><span data-stu-id="91851-106">toocreate a new Facebook account, go too[facebook.com].</span></span>

## <span data-ttu-id="91851-107"><a name="register"> </a>Registrar seu aplicativo com o Facebook</span><span class="sxs-lookup"><span data-stu-id="91851-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="91851-108">Faça logon no toohello [portal do Azure]e navegue tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91851-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="91851-109">Copie a **URL**.</span><span class="sxs-lookup"><span data-stu-id="91851-109">Copy your **URL**.</span></span> <span data-ttu-id="91851-110">Você usará esse tooconfigure seu aplicativo do Facebook.</span><span class="sxs-lookup"><span data-stu-id="91851-110">You will use this tooconfigure your Facebook app.</span></span>
2. <span data-ttu-id="91851-111">Em outra janela do navegador, navegue toohello [os desenvolvedores do Facebook] as credenciais de conta de site da Web e entrar com o Facebook.</span><span class="sxs-lookup"><span data-stu-id="91851-111">In another browser window, navigate toohello [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="91851-112">(Opcional) Se você já não tiver registrado, clique em **aplicativos** > **registrar como um desenvolvedor**, aceite a política de saudação e siga as etapas de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="91851-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept hello policy and follow hello registration steps.</span></span>
4. <span data-ttu-id="91851-113">Clique em **Meus Aplicativos** > **Adicionar um Novo Aplicativo** > **Site** > **Ignore e Criar ID do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="91851-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="91851-114">Em **nome de exibição**, digite um nome exclusivo para seu aplicativo, o tipo de sua **Contact Email**, escolha um **categoria** para seu aplicativo, em seguida, clique em **criar ID do aplicativo**e concluir a verificação de segurança de saudação.</span><span class="sxs-lookup"><span data-stu-id="91851-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete hello security check.</span></span> <span data-ttu-id="91851-115">Isso leva toohello painel do desenvolvedor para o novo aplicativo do Facebook.</span><span class="sxs-lookup"><span data-stu-id="91851-115">This takes you toohello developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="91851-116">Em "Logon no Facebook", clique em **Introdução**.</span><span class="sxs-lookup"><span data-stu-id="91851-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="91851-117">Adicionar o aplicativo **URI de redirecionamento** muito**URIs de redirecionamento OAuth válido**, em seguida, clique em **salvar alterações**.</span><span class="sxs-lookup"><span data-stu-id="91851-117">Add your application's **Redirect URI** too**Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="91851-118">O redirecionamento de URI é a URL de saudação do seu aplicativo anexado ao caminho hello, */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="91851-118">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="91851-119">Por exemplo: `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="91851-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="91851-120">Certifique-se de que você está usando o esquema do hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="91851-120">Make sure that you are using hello HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="91851-121">Na navegação saudação do lado esquerdo, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="91851-121">In hello left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="91851-122">Em Olá **segredo do aplicativo** , clique em **Mostrar**, forneça a senha, se solicitado, em seguida, anote os valores de saudação do **ID do aplicativo** e **segredo do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="91851-122">On hello **App Secret** field, click **Show**, provide your password if requested, then make a note of hello values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="91851-123">Use esses tooconfigure posterior seu aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="91851-123">You use these later tooconfigure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="91851-124">segredo do aplicativo Hello é uma credencial de segurança importantes.</span><span class="sxs-lookup"><span data-stu-id="91851-124">hello app secret is an important security credential.</span></span> <span data-ttu-id="91851-125">Não compartilhe essa senha com ninguém nem distribua-a em um aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="91851-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="91851-126">Olá conta do Facebook que foi usado tooregister Olá aplicativo é um administrador do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="91851-126">hello Facebook account which was used tooregister hello application is an administrator of hello app.</span></span> <span data-ttu-id="91851-127">Neste ponto, apenas os administradores podem entrar neste aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91851-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="91851-128">tooauthenticate outras contas do Facebook, clique em **revisão de aplicativo** e habilitar **Verifique < seu nome do aplicativo-> público** acesso público geral tooenable usando a autenticação do Facebook.</span><span class="sxs-lookup"><span data-stu-id="91851-128">tooauthenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** tooenable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="91851-129"><a name="secrets"></a>Aplicativo do Facebook adicionar informações tooyour</span><span class="sxs-lookup"><span data-stu-id="91851-129"><a name="secrets"> </a>Add Facebook information tooyour application</span></span>
1. <span data-ttu-id="91851-130">Em Olá [portal do Azure], navegar tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91851-130">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="91851-131">Clique em **Configurações** > **Autenticação/Autorização** e verifique se a **Autenticação do Serviço de Aplicativo** está **Ativada**.</span><span class="sxs-lookup"><span data-stu-id="91851-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="91851-132">Clique em **Facebook**, cole em valores de ID do aplicativo e o segredo do aplicativo hello que você obteve anteriormente, se desejar habilitar escopos necessitados para seu aplicativo e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="91851-132">Click **Facebook**, paste in hello App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="91851-133">Por padrão, o serviço de aplicativo fornece autenticação, mas não restringe o conteúdo do site tooyour acesso autorizado e APIs.</span><span class="sxs-lookup"><span data-stu-id="91851-133">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="91851-134">Você deve autorizar os usuários no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91851-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="91851-135">(Opcional) toorestrict acesso tooyour site tooonly usuários autenticados pelo Facebook, definir **tootake de ação quando a solicitação não está autenticada** muito**Facebook**.</span><span class="sxs-lookup"><span data-stu-id="91851-135">(Optional) toorestrict access tooyour site tooonly users authenticated by Facebook, set **Action tootake when request is not authenticated** too**Facebook**.</span></span> <span data-ttu-id="91851-136">Isso requer que todas as solicitações autenticadas e todas as solicitações não autenticadas são redirecionada tooFacebook para autenticação.</span><span class="sxs-lookup"><span data-stu-id="91851-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooFacebook for authentication.</span></span>
4. <span data-ttu-id="91851-137">Ao concluir a configuração de autenticação, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="91851-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="91851-138">Agora você está pronto toouse Facebook para autenticação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91851-138">You are now ready toouse Facebook for authentication in your app.</span></span>

## <span data-ttu-id="91851-139"><a name="related-content"> </a>Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="91851-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[os desenvolvedores do Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[portal do Azure]: https://portal.azure.com/
