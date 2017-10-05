---
title: "Adicionar autenticação no Android com os Aplicativos Móveis| Microsoft Docs"
description: "Saiba como usar o recurso Aplicativos Móveis do Serviço de Aplicativo do Azure para autenticar usuários de seu aplicativo Android por meio de uma variedade de provedores de identidade, incluindo Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: 81331142aa6110d4e29e6fb30a90ce6e3a853439
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-android-app"></a><span data-ttu-id="f218c-103">Adicionar autenticação ao aplicativo do Android</span><span class="sxs-lookup"><span data-stu-id="f218c-103">Add authentication to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="f218c-104">Resumo</span><span class="sxs-lookup"><span data-stu-id="f218c-104">Summary</span></span>
<span data-ttu-id="f218c-105">Neste tutorial, você adiciona autenticação ao projeto de início rápido da lista de tarefas pendentes no Android usando um provedor de identidade com suporte.</span><span class="sxs-lookup"><span data-stu-id="f218c-105">In this tutorial, you add authentication to the todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="f218c-106">Este tutorial se baseia no tutorial [Introdução aos Aplicativos Móveis] , que você deve concluir primeiro.</span><span class="sxs-lookup"><span data-stu-id="f218c-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="f218c-107"><a name="register"></a>Registrar seu aplicativo para autenticação e configurar o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="f218c-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="f218c-108"><a name="redirecturl"></a>Adicionar seu aplicativo às URLs de redirecionamento externo permitidas</span><span class="sxs-lookup"><span data-stu-id="f218c-108"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="f218c-109">A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f218c-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="f218c-110">Isso permite que o sistema de autenticação redirecione para seu aplicativo após a conclusão do processo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="f218c-110">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="f218c-111">Neste tutorial, usamos sempre o esquema de URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="f218c-111">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="f218c-112">No entanto, você pode usar o esquema de URL que quiser.</span><span class="sxs-lookup"><span data-stu-id="f218c-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="f218c-113">Ele deve ser exclusivo para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="f218c-113">It should be unique to your mobile application.</span></span> <span data-ttu-id="f218c-114">Para habilitar o redirecionamento no lado do servidor:</span><span class="sxs-lookup"><span data-stu-id="f218c-114">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="f218c-115">No [Portal do Azure], selecione seu Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f218c-115">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="f218c-116">Clique na opção de menu **Autenticação/Autorização**.</span><span class="sxs-lookup"><span data-stu-id="f218c-116">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="f218c-117">Em **URLs de Redirecionamento Externo Permitidas**, insira `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="f218c-117">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="f218c-118">O _appname_ na cadeia de caracteres é o esquema de URL para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="f218c-118">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="f218c-119">Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).</span><span class="sxs-lookup"><span data-stu-id="f218c-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="f218c-120">Você deve anotar a cadeia de caracteres escolhida, já que precisará ajustar o código do aplicativo móvel com o esquema de URL em vários lugares.</span><span class="sxs-lookup"><span data-stu-id="f218c-120">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="f218c-121">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f218c-121">Click **OK**.</span></span>

5. <span data-ttu-id="f218c-122">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f218c-122">Click **Save**.</span></span>

## <span data-ttu-id="f218c-123"><a name="permissions"></a>Restringir permissões a usuários autenticados</span><span class="sxs-lookup"><span data-stu-id="f218c-123"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="f218c-124">No Android Studio, abra o projeto concluído com o tutorial [Introdução aos Aplicativos Móveis].</span><span class="sxs-lookup"><span data-stu-id="f218c-124">In Android Studio, open the project you completed with the tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="f218c-125">No menu **Executar**, clique em **Executar aplicativo** e verifique se uma exceção sem tratamento com um código de status 401 (Não autorizado) é acionada depois que o aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="f218c-125">From the **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span>

     <span data-ttu-id="f218c-126">Essa exceção ocorre porque o aplicativo tenta acessar o back-end como um usuário não autenticado, mas a tabela *TodoItem* agora exige autenticação.</span><span class="sxs-lookup"><span data-stu-id="f218c-126">This exception happens because the app attempts to access the back end as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="f218c-127">Em seguida, você atualiza o aplicativo para autenticar os usuários antes de solicitar recursos do back-end dos Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="f218c-127">Next, you update the app to authenticate users before requesting resources from the Mobile Apps back end.</span></span> 

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="f218c-128">Adicionar autenticação ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="f218c-128">Add authentication to the app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="f218c-129"><a name="cache-tokens"></a>Armazenar em cache tokens de autenticação no cliente</span><span class="sxs-lookup"><span data-stu-id="f218c-129"><a name="cache-tokens"></a>Cache authentication tokens on the client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="f218c-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f218c-130">Next steps</span></span>
<span data-ttu-id="f218c-131">Agora que você concluiu este tutorial de autenticação básica, considere continuar com um dos seguintes tutoriais:</span><span class="sxs-lookup"><span data-stu-id="f218c-131">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="f218c-132">[Adicionar notificações por push ao aplicativo Android](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="f218c-132">[Add push notifications to your Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="f218c-133">Saiba como configurar o back-end dos Aplicativos Móveis para usar os hubs de notificação do Azure para enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="f218c-133">Learn how to configure your Mobile Apps back end to use Azure notification hubs to send push notifications.</span></span>
* <span data-ttu-id="f218c-134">[Habilitar a sincronização offline para o aplicativo móvel Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="f218c-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="f218c-135">Saiba como adicionar suporte offline ao aplicativo usando um back-end dos Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="f218c-135">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="f218c-136">Com a sincronização offline, os usuários podem interagir com um aplicativo móvel &mdash; exibindo, adicionando ou modificando dados &mdash; mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="f218c-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions to authenticated users]: #permissions
[Add authentication to the app]: #add-authentication
[Store authentication tokens on the client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
<span data-ttu-id="f218c-137">[Introdução aos Aplicativos Móveis]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="f218c-137">[Get started with Mobile Apps]: app-service-mobile-android-get-started.md</span></span>
