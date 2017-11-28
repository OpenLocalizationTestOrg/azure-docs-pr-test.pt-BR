---
title: "autenticação aaaAdd no Android com aplicativos móveis | Microsoft Docs"
description: "Saiba como toouse Olá recurso de aplicativos móveis de usuários do serviço de aplicativo do Azure tooauthenticate do seu aplicativo do Android por meio de uma variedade de provedores de identidade, como Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a><span data-ttu-id="eea13-103">Adicionar aplicativo do Android autenticação tooyour</span><span class="sxs-lookup"><span data-stu-id="eea13-103">Add authentication tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="eea13-104">Resumo</span><span class="sxs-lookup"><span data-stu-id="eea13-104">Summary</span></span>
<span data-ttu-id="eea13-105">Neste tutorial, você adicionar projeto de início rápido do autenticação toohello todolist no Android, usando um provedor de identidade com suporte.</span><span class="sxs-lookup"><span data-stu-id="eea13-105">In this tutorial, you add authentication toohello todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="eea13-106">Este tutorial baseia-se a saudação [começar com aplicativos móveis] tutorial, que deve ser concluído primeiro.</span><span class="sxs-lookup"><span data-stu-id="eea13-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="eea13-107"><a name="register"></a>Registrar seu aplicativo para autenticação e configurar o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="eea13-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="eea13-108"><a name="redirecturl"></a>Adicionar URLs de redirecionamento externo permitidos de toohello seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="eea13-108"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="eea13-109">A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eea13-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="eea13-110">Isso permite Olá autenticação sistema tooredirect tooyour back aplicativo após a conclusão do processo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="eea13-110">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="eea13-111">Neste tutorial, usamos o esquema de URL Olá _appname_ em todo.</span><span class="sxs-lookup"><span data-stu-id="eea13-111">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="eea13-112">No entanto, você pode usar o esquema de URL que quiser.</span><span class="sxs-lookup"><span data-stu-id="eea13-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="eea13-113">Ele deve ser exclusivo tooyour aplicativo para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="eea13-113">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="eea13-114">redirecionamento de saudação tooenable no lado do servidor de saudação:</span><span class="sxs-lookup"><span data-stu-id="eea13-114">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="eea13-115">No hello [portal do Azure], selecione o serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eea13-115">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="eea13-116">Clique em Olá **autenticação / autorização** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="eea13-116">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="eea13-117">Em Olá **permitidas URLs de redirecionamento externo**, digite `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="eea13-117">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="eea13-118">Olá _appname_ na cadeia de caracteres é hello esquema de URL para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="eea13-118">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="eea13-119">Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).</span><span class="sxs-lookup"><span data-stu-id="eea13-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="eea13-120">Assegure uma anotação de cadeia de caracteres de saudação que você escolha como você precisará tooadjust seu código de aplicativo móvel com hello esquema de URL em vários locais.</span><span class="sxs-lookup"><span data-stu-id="eea13-120">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="eea13-121">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="eea13-121">Click **OK**.</span></span>

5. <span data-ttu-id="eea13-122">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="eea13-122">Click **Save**.</span></span>

## <span data-ttu-id="eea13-123"><a name="permissions"></a>Restringir permissões tooauthenticated usuários</span><span class="sxs-lookup"><span data-stu-id="eea13-123"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="eea13-124">No Android Studio, abrir projeto de saudação é concluída com o tutorial Olá [começar com aplicativos móveis].</span><span class="sxs-lookup"><span data-stu-id="eea13-124">In Android Studio, open hello project you completed with hello tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="eea13-125">De saudação **executar** menu, clique em **executar aplicativo**e verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada após o início do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="eea13-125">From hello **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span>

     <span data-ttu-id="eea13-126">Essa exceção ocorre porque as tentativas de aplicativo hello tooaccess Olá volta encerrar como um usuário não autenticado, mas Olá *TodoItem* tabela agora requer autenticação.</span><span class="sxs-lookup"><span data-stu-id="eea13-126">This exception happens because hello app attempts tooaccess hello back end as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="eea13-127">Em seguida, você deve atualizar os usuários tooauthenticate de aplicativo hello antes de solicitar recursos do hello que terminar de volta a aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="eea13-127">Next, you update hello app tooauthenticate users before requesting resources from hello Mobile Apps back end.</span></span> 

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="eea13-128">Adicionar autenticação toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="eea13-128">Add authentication toohello app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="eea13-129"><a name="cache-tokens"></a>Tokens de autenticação de cache no cliente de saudação</span><span class="sxs-lookup"><span data-stu-id="eea13-129"><a name="cache-tokens"></a>Cache authentication tokens on hello client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="eea13-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eea13-130">Next steps</span></span>
<span data-ttu-id="eea13-131">Agora que você concluiu este tutorial de autenticação básica, considere a possibilidade de continuar tooone de saudação tutoriais a seguir:</span><span class="sxs-lookup"><span data-stu-id="eea13-131">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="eea13-132">[Adicionar aplicativo do Android push notificações tooyour](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="eea13-132">[Add push notifications tooyour Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="eea13-133">Saiba como tooconfigure fazer seus aplicativos móveis encerrar notificações por push de toosend de hubs do toouse notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="eea13-133">Learn how tooconfigure your Mobile Apps back end toouse Azure notification hubs toosend push notifications.</span></span>
* <span data-ttu-id="eea13-134">[Habilitar a sincronização offline para o aplicativo móvel Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="eea13-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="eea13-135">Saiba como o tooadd offline dão suporte ao aplicativo tooyour usando um back-end de aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="eea13-135">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="eea13-136">Com a sincronização offline, os usuários podem interagir com um aplicativo móvel &mdash; exibindo, adicionando ou modificando dados &mdash; mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="eea13-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[começar com aplicativos móveis]: app-service-mobile-android-get-started.md
