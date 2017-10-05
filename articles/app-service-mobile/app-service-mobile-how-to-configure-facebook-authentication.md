---
title: "Como configurar a autenticação do Facebook para seu aplicativo de Serviços de Aplicativos"
description: "Saiba como configurar a autenticação do Facebook para seu aplicativo de Serviços de Aplicativos."
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
ms.openlocfilehash: c1b4c91d384c56c4f55bf8d31ced250f51c0d837
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-facebook-login"></a><span data-ttu-id="49cec-103">Como configurar seu aplicativo do Serviço do Aplicativo para usar o logon do Facebook</span><span class="sxs-lookup"><span data-stu-id="49cec-103">How to configure your App Service application to use Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="49cec-104">Este tópico mostra como configurar o Serviço de Aplicativo do Azure para usar o Facebook como um provedor de autenticação.</span><span class="sxs-lookup"><span data-stu-id="49cec-104">This topic shows you how to configure Azure App Service to use Facebook as an authentication provider.</span></span>

<span data-ttu-id="49cec-105">Para concluir o procedimento neste tópico, você deve ter uma conta do Facebook com um endereço de email verificado e um número de telefone celular.</span><span class="sxs-lookup"><span data-stu-id="49cec-105">To complete the procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="49cec-106">Para criar uma nova conta do Facebook, vá para [facebook.com].</span><span class="sxs-lookup"><span data-stu-id="49cec-106">To create a new Facebook account, go to [facebook.com].</span></span>

## <span data-ttu-id="49cec-107"><a name="register"> </a>Registrar seu aplicativo com o Facebook</span><span class="sxs-lookup"><span data-stu-id="49cec-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="49cec-108">Faça logon no [portal do Azure]e navegue até o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49cec-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="49cec-109">Copie a **URL**.</span><span class="sxs-lookup"><span data-stu-id="49cec-109">Copy your **URL**.</span></span> <span data-ttu-id="49cec-110">Você a usará para configurar o seu aplicativo do Facebook.</span><span class="sxs-lookup"><span data-stu-id="49cec-110">You will use this to configure your Facebook app.</span></span>
2. <span data-ttu-id="49cec-111">Em outra janela do navegador, navegue até o site de [Desenvolvedores do Facebook] e entre com suas credenciais de conta do Facebook.</span><span class="sxs-lookup"><span data-stu-id="49cec-111">In another browser window, navigate to the [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="49cec-112">(Opcional) Se você ainda não se registrou, clique em **Aplicativos** > **Registrar como um Desenvolvedor**, aceite a política e siga as etapas do registro.</span><span class="sxs-lookup"><span data-stu-id="49cec-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept the policy and follow the registration steps.</span></span>
4. <span data-ttu-id="49cec-113">Clique em **Meus Aplicativos** > **Adicionar um Novo Aplicativo** > **Site** > **Ignore e Criar ID do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="49cec-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="49cec-114">Em **Nome de Exibição**, digite um nome exclusivo para seu aplicativo, digite seu **Email de Contato**, escolha uma **Categoria** para seu aplicativo, em seguida, clique em **Criar ID do Aplicativo** e conclua a verificação de segurança.</span><span class="sxs-lookup"><span data-stu-id="49cec-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete the security check.</span></span> <span data-ttu-id="49cec-115">Isso o levará ao painel do desenvolvedor de seu novo aplicativo do Facebook.</span><span class="sxs-lookup"><span data-stu-id="49cec-115">This takes you to the developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="49cec-116">Em "Logon no Facebook", clique em **Introdução**.</span><span class="sxs-lookup"><span data-stu-id="49cec-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="49cec-117">Adicione o **URI de Redirecionamento** do aplicativo aos **URIs de redirecionamento OAuth válidos**, em seguida, clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="49cec-117">Add your application's **Redirect URI** to **Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="49cec-118">O URI de redirecionamento é a URL do seu aplicativo adicionada ao caminho */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="49cec-118">Your redirect URI is the URL of your application appended with the path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="49cec-119">Por exemplo: `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="49cec-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="49cec-120">Certifique-se de que você está usando o esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="49cec-120">Make sure that you are using the HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="49cec-121">No painel de navegação à esquerda, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="49cec-121">In the left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="49cec-122">No campo **Segredo do Aplicativo**, clique em **Mostrar**, forneça sua senha se solicitado e anote os valores do **ID do aplicativo** e do **Segredo do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="49cec-122">On the **App Secret** field, click **Show**, provide your password if requested, then make a note of the values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="49cec-123">Você os utilizará mais tarde para configurar seu aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="49cec-123">You use these later to configure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="49cec-124">O segredo do aplicativo é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="49cec-124">The app secret is an important security credential.</span></span> <span data-ttu-id="49cec-125">Não compartilhe essa senha com ninguém nem distribua-a em um aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="49cec-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="49cec-126">A conta do Facebook usada para registrar o aplicativo é um administrador do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49cec-126">The Facebook account which was used to register the application is an administrator of the app.</span></span> <span data-ttu-id="49cec-127">Neste ponto, apenas os administradores podem entrar neste aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49cec-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="49cec-128">Para autenticar outras contas do Facebook, clique em **Revisão do Aplicativo** e habilite **Tornar público o < nome-aplicativo >** para habilitar o acesso do público geral usando a autenticação do Facebook.</span><span class="sxs-lookup"><span data-stu-id="49cec-128">To authenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** to enable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="49cec-129"><a name="secrets"> </a>Adicionar informações do Facebook ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="49cec-129"><a name="secrets"> </a>Add Facebook information to your application</span></span>
1. <span data-ttu-id="49cec-130">De volta ao [portal do Azure], navegue até o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49cec-130">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="49cec-131">Clique em **Configurações** > **Autenticação/Autorização** e verifique se a **Autenticação do Serviço de Aplicativo** está **Ativada**.</span><span class="sxs-lookup"><span data-stu-id="49cec-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="49cec-132">Clique em **Facebook**, cole os valores do ID do Aplicativo e do Segredo do Aplicativo obtidos anteriormente e, como opção, habilite os escopos necessários para seu aplicativo, então, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="49cec-132">Click **Facebook**, paste in the App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="49cec-133">Por padrão, o Serviço de Aplicativo fornece autenticação, mas não restringe o acesso autorizado ao conteúdo do site e às APIs.</span><span class="sxs-lookup"><span data-stu-id="49cec-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="49cec-134">Você deve autorizar os usuários no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49cec-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="49cec-135">(Opcional) Para restringir o acesso ao seu site para apenas os usuários autenticados pelo Facebook, defina a **Ação a tomar quando a solicitação não está autenticada** para **Facebook**.</span><span class="sxs-lookup"><span data-stu-id="49cec-135">(Optional) To restrict access to your site to only users authenticated by Facebook, set **Action to take when request is not authenticated** to **Facebook**.</span></span> <span data-ttu-id="49cec-136">Isso exige que todas as solicitações sejam autenticadas e todas as solicitações não autenticadas sejam redirecionadas ao Facebook para autenticação.</span><span class="sxs-lookup"><span data-stu-id="49cec-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Facebook for authentication.</span></span>
4. <span data-ttu-id="49cec-137">Ao concluir a configuração de autenticação, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="49cec-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="49cec-138">Agora você está pronto para usar o Facebook para autenticação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49cec-138">You are now ready to use Facebook for authentication in your app.</span></span>

## <span data-ttu-id="49cec-139"><a name="related-content"> </a>Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="49cec-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
<span data-ttu-id="49cec-140">[Desenvolvedores do Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span><span class="sxs-lookup"><span data-stu-id="49cec-140">[Facebook Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span></span>
<span data-ttu-id="49cec-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span><span class="sxs-lookup"><span data-stu-id="49cec-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span></span>
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
<span data-ttu-id="49cec-142">[portal do Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="49cec-142">[Azure portal]: https://portal.azure.com/</span></span>
