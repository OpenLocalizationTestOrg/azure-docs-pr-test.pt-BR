---
title: "Como configurar a autenticação do Twitter para seu aplicativo de Serviços de Aplicativos"
description: "Saiba como configurar a autenticação do Twitter para seu aplicativo de Serviços de Aplicativos."
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
ms.openlocfilehash: afde020b7817dc58ecea24eb4a09cf93d0986eb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-twitter-login"></a><span data-ttu-id="e50ee-103">Como configurar seu aplicativo do Serviço de Aplicativo para usar o logon do Twitter</span><span class="sxs-lookup"><span data-stu-id="e50ee-103">How to configure your App Service application to use Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="e50ee-104">Este tópico mostra como configurar o Serviço de Aplicativo do Azure para usar o Twitter como um provedor de autenticação.</span><span class="sxs-lookup"><span data-stu-id="e50ee-104">This topic shows you how to configure Azure App Service to use Twitter as an authentication provider.</span></span>

<span data-ttu-id="e50ee-105">Para concluir o procedimento deste tópico, você deve ter uma conta do Twitter com um endereço de email verificado e um número de telefone.</span><span class="sxs-lookup"><span data-stu-id="e50ee-105">To complete the procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="e50ee-106">Para criar uma nova conta do Twitter, vá para <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="e50ee-106">To create a new Twitter account, go to <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="e50ee-107"><a name="register"> </a>Registre seu aplicativo com o Twitter</span><span class="sxs-lookup"><span data-stu-id="e50ee-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="e50ee-108">Faça logon no [portal do Azure]e navegue até o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e50ee-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="e50ee-109">Copie a **URL**.</span><span class="sxs-lookup"><span data-stu-id="e50ee-109">Copy your **URL**.</span></span> <span data-ttu-id="e50ee-110">Você a usará para configurar o seu aplicativo do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e50ee-110">You will use this to configure your Twitter app.</span></span>
2. <span data-ttu-id="e50ee-111">Navegue até o site de [Desenvolvedores do Twitter,] entre com suas credenciais da conta do Twitter e clique em **Criar Novo Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e50ee-111">Navigate to the [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="e50ee-112">Digite o **Nome** e uma **Descrição** para o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e50ee-112">Type in the **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="e50ee-113">Cole a **URL** do aplicativo no valor **Site**.</span><span class="sxs-lookup"><span data-stu-id="e50ee-113">Paste in your application's **URL** for the **Website** value.</span></span> <span data-ttu-id="e50ee-114">Em seguida, em **URL de Callback**, cole a **URL de Callback** copiada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e50ee-114">Then, for the **Callback URL**, paste the **Callback URL** you copied earlier.</span></span> <span data-ttu-id="e50ee-115">Esse é o seu gateway de Aplicativo Móvel, acrescentado com o caminho */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="e50ee-115">This is your Mobile App gateway appended with the path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="e50ee-116">Por exemplo: `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="e50ee-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="e50ee-117">Certifique-se de que você está usando o esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e50ee-117">Make sure that you are using the HTTPS scheme.</span></span>
4. <span data-ttu-id="e50ee-118">Na parte inferior da página, leia e aceite os termos.</span><span class="sxs-lookup"><span data-stu-id="e50ee-118">At the bottom the page, read and accept the terms.</span></span> <span data-ttu-id="e50ee-119">Em seguida, clique em **Criar seu Aplicativo do Twitter**.</span><span class="sxs-lookup"><span data-stu-id="e50ee-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="e50ee-120">Isso registrará o aplicativo e exibirá os detalhes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e50ee-120">This registers the app displays the application details.</span></span>
5. <span data-ttu-id="e50ee-121">Clique na guia **Configurações**, marque **Permitir que este aplicativo seja usado para entrar com o Twitter** e, em seguida, clique em **Atualizar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="e50ee-121">Click the **Settings** tab, check **Allow this application to be used to sign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="e50ee-122">Selecione a guia **Chaves e Tokens de Acesso** .</span><span class="sxs-lookup"><span data-stu-id="e50ee-122">Select the **Keys and Access Tokens** tab.</span></span> <span data-ttu-id="e50ee-123">Tome nota dos valores da **Chave do Consumidor (Chave de API)** e **Segredo do consumidor (Segredo de API)**.</span><span class="sxs-lookup"><span data-stu-id="e50ee-123">Make a note of the values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e50ee-124">O segredo do consumidor é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="e50ee-124">The consumer secret is an important security credential.</span></span> <span data-ttu-id="e50ee-125">Não compartilhe esse segredo com ninguém nem o distribua com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e50ee-125">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="e50ee-126"><a name="secrets"> </a>Adicione informações do Twitter ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="e50ee-126"><a name="secrets"> </a>Add Twitter information to your application</span></span>
1. <span data-ttu-id="e50ee-127">De volta ao [portal do Azure], navegue até o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e50ee-127">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="e50ee-128">Clique em **Configurações** e em **Autenticação/Autorização**.</span><span class="sxs-lookup"><span data-stu-id="e50ee-128">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="e50ee-129">Se o recurso Autenticação / Autorização não estiver habilitado, mude a opção para **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="e50ee-129">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="e50ee-130">Clique em **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="e50ee-130">Click **Twitter**.</span></span> <span data-ttu-id="e50ee-131">Cole os valores de ID do aplicativo e segredo do aplicativo obtidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e50ee-131">Paste in the App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="e50ee-132">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e50ee-132">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="e50ee-133">Por padrão, o Serviço de Aplicativo fornece autenticação, mas não restringe o acesso autorizado ao conteúdo do site e às APIs.</span><span class="sxs-lookup"><span data-stu-id="e50ee-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="e50ee-134">Você deve autorizar os usuários no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e50ee-134">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="e50ee-135">(Opcional) Para restringir o acesso ao seu site somente para usuários autenticados pelo Twitter, defina **Ação a ser executada quando a solicitação não for autenticada** como **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="e50ee-135">(Optional) To restrict access to your site to only users authenticated by Twitter, set **Action to take when request is not authenticated** to **Twitter**.</span></span> <span data-ttu-id="e50ee-136">Isso exige que todas as solicitações sejam autenticadas e todas as solicitações não autenticadas sejam redirecionadas ao Twitter para autenticação.</span><span class="sxs-lookup"><span data-stu-id="e50ee-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Twitter for authentication.</span></span>
5. <span data-ttu-id="e50ee-137">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e50ee-137">Click **Save**.</span></span>

<span data-ttu-id="e50ee-138">Agora você está pronto para usar o Twitter para autenticação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e50ee-138">You are now ready to use Twitter for authentication in your app.</span></span>

## <span data-ttu-id="e50ee-139"><a name="related-content"> </a>Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="e50ee-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

<span data-ttu-id="e50ee-140">[Desenvolvedores do Twitter,]: http://go.microsoft.com/fwlink/p/?LinkId=268300</span><span class="sxs-lookup"><span data-stu-id="e50ee-140">[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300</span></span>
<span data-ttu-id="e50ee-141">[portal do Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="e50ee-141">[Azure portal]: https://portal.azure.com/</span></span>
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
