---
title: "autenticação de aaaAdd no Apache Cordova com os aplicativos móveis | Microsoft Docs"
description: "Saiba como toouse aplicativos móveis de usuários do serviço de aplicativo do Azure tooauthenticate do seu aplicativo Apache Cordova por meio de uma variedade de provedores de identidade, como Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a><span data-ttu-id="d9153-103">Adicionar aplicativo do Apache Cordova de tooyour de autenticação</span><span class="sxs-lookup"><span data-stu-id="d9153-103">Add authentication tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="d9153-104">Resumo</span><span class="sxs-lookup"><span data-stu-id="d9153-104">Summary</span></span>
<span data-ttu-id="d9153-105">Neste tutorial, você pode adicionar projeto de início rápido do autenticação toohello todolist no Apache Cordova usando um provedor de identidade com suporte.</span><span class="sxs-lookup"><span data-stu-id="d9153-105">In this tutorial, you add authentication toohello todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="d9153-106">Este tutorial baseia-se a saudação [começar com aplicativos móveis] tutorial, que deve ser concluído primeiro.</span><span class="sxs-lookup"><span data-stu-id="d9153-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="d9153-107"><a name="register"></a>Registrar seu aplicativo para autenticação e configurar saudação do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9153-107"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="d9153-108">Assista a um vídeo que mostra etapas semelhantes</span><span class="sxs-lookup"><span data-stu-id="d9153-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="d9153-109"><a name="permissions"></a>Restringir permissões tooauthenticated usuários</span><span class="sxs-lookup"><span data-stu-id="d9153-109"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="d9153-110">Agora, você pode verificar que essa back-end do acesso anônimo tooyour foi desabilitada.</span><span class="sxs-lookup"><span data-stu-id="d9153-110">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="d9153-111">No Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d9153-111">In Visual Studio:</span></span>

* <span data-ttu-id="d9153-112">Projeto Olá abertos que você criou quando você concluiu o tutorial Olá [começar com aplicativos móveis].</span><span class="sxs-lookup"><span data-stu-id="d9153-112">Open hello project that you created when you completed hello tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="d9153-113">Executar o aplicativo no hello **emulador Android da Google**.</span><span class="sxs-lookup"><span data-stu-id="d9153-113">Run your application in hello **Google Android Emulator**.</span></span>
* <span data-ttu-id="d9153-114">Verifique se que uma falha inesperada da Conexão é exibida após o início do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d9153-114">Verify that an Unexpected Connection Failure is shown after hello app starts.</span></span>

<span data-ttu-id="d9153-115">Em seguida, atualize os usuários tooauthenticate de aplicativo hello antes de solicitar recursos de back-end de aplicativo móvel hello.</span><span class="sxs-lookup"><span data-stu-id="d9153-115">Next, update hello app tooauthenticate users before requesting resources from hello Mobile App backend.</span></span>

## <span data-ttu-id="d9153-116"><a name="add-authentication"></a>Adicionar autenticação toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9153-116"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="d9153-117">Abra seu projeto no **Visual Studio**, em seguida, Olá `www/index.html` arquivo para edição.</span><span class="sxs-lookup"><span data-stu-id="d9153-117">Open your project in **Visual Studio**, then open hello `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="d9153-118">Localizar Olá `Content-Security-Policy` marca meta na seção de cabeçalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9153-118">Locate hello `Content-Security-Policy` meta tag in hello head section.</span></span>  <span data-ttu-id="d9153-119">Adicione Olá OAuth host toohello lista de origens permitidas.</span><span class="sxs-lookup"><span data-stu-id="d9153-119">Add hello OAuth host toohello list of allowed sources.</span></span>

   | <span data-ttu-id="d9153-120">Provedor</span><span class="sxs-lookup"><span data-stu-id="d9153-120">Provider</span></span> | <span data-ttu-id="d9153-121">Nome do provedor do SDK</span><span class="sxs-lookup"><span data-stu-id="d9153-121">SDK Provider Name</span></span> | <span data-ttu-id="d9153-122">Host OAuth</span><span class="sxs-lookup"><span data-stu-id="d9153-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="d9153-123">Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d9153-123">Azure Active Directory</span></span> | <span data-ttu-id="d9153-124">aad</span><span class="sxs-lookup"><span data-stu-id="d9153-124">aad</span></span> | <span data-ttu-id="d9153-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d9153-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="d9153-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="d9153-126">Facebook</span></span> | <span data-ttu-id="d9153-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="d9153-127">facebook</span></span> | <span data-ttu-id="d9153-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="d9153-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="d9153-129">Google</span><span class="sxs-lookup"><span data-stu-id="d9153-129">Google</span></span> | <span data-ttu-id="d9153-130">Google</span><span class="sxs-lookup"><span data-stu-id="d9153-130">google</span></span> | <span data-ttu-id="d9153-131">https://accounts.google.com</span><span class="sxs-lookup"><span data-stu-id="d9153-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="d9153-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="d9153-132">Microsoft</span></span> | <span data-ttu-id="d9153-133">microsoftaccount</span><span class="sxs-lookup"><span data-stu-id="d9153-133">microsoftaccount</span></span> | <span data-ttu-id="d9153-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="d9153-134">https://login.live.com</span></span> |
   | <span data-ttu-id="d9153-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="d9153-135">Twitter</span></span> | <span data-ttu-id="d9153-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="d9153-136">twitter</span></span> | <span data-ttu-id="d9153-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="d9153-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="d9153-138">Veja a seguir um exemplo de Política de segurança de conteúdo (implementada para o Active Directory do Azure):</span><span class="sxs-lookup"><span data-stu-id="d9153-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="d9153-139">Substituir `https://login.microsoftonline.com` com host OAuth Olá Olá anterior da tabela.</span><span class="sxs-lookup"><span data-stu-id="d9153-139">Replace `https://login.microsoftonline.com` with hello OAuth host from hello preceding table.</span></span>  <span data-ttu-id="d9153-140">Para obter mais informações sobre a marca de meta de política de segurança de conteúdo hello, consulte Olá [documentação da política de segurança de conteúdo].</span><span class="sxs-lookup"><span data-stu-id="d9153-140">For more information about hello content-security-policy meta tag, see hello [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="d9153-141">Alguns provedores de autenticação não exigem mudanças no Content-Security-Policy quando usado em dispositivos móveis apropriados.</span><span class="sxs-lookup"><span data-stu-id="d9153-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="d9153-142">Por exemplo, nenhuma mudança na Política de segurança de conteúdo será necessária ao usar a autenticação do Google em um dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="d9153-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="d9153-143">Olá abrir `www/js/index.js` para edição de arquivos, localize Olá `onDeviceReady()` método, e na criação de cliente Olá código adicionar Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9153-143">Open hello `www/js/index.js` file for editing, locate hello `onDeviceReady()` method, and under hello client  creation code add hello following code:</span></span>

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="d9153-144">Esse código substitui Olá um código existente que cria a referência de tabela hello e atualiza a saudação da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="d9153-144">This code replaces hello existing code that creates hello table reference and refreshes hello UI.</span></span>

    <span data-ttu-id="d9153-145">método de login () do Hello inicia a autenticação com o provedor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9153-145">hello login() method starts authentication with hello provider.</span></span> <span data-ttu-id="d9153-146">método do Hello login () é uma função assíncrona que retorna uma promessa de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d9153-146">hello login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="d9153-147">rest Olá da inicialização de saudação é colocada dentro Olá promessa resposta para que não será executado até que o método de login () do hello é concluído.</span><span class="sxs-lookup"><span data-stu-id="d9153-147">hello rest of hello initialization is placed inside hello promise response so that it is not executed until hello login() method completes.</span></span>

4. <span data-ttu-id="d9153-148">No código de saudação que você acabou de adicionar, substituir `SDK_Provider_Name` com nome de saudação do seu provedor de logon.</span><span class="sxs-lookup"><span data-stu-id="d9153-148">In hello code that you just added, replace `SDK_Provider_Name` with hello name of your login provider.</span></span> <span data-ttu-id="d9153-149">Por exemplo, para o Azure Active Directory, use `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="d9153-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="d9153-150">Execute seu projeto.</span><span class="sxs-lookup"><span data-stu-id="d9153-150">Run your project.</span></span>  <span data-ttu-id="d9153-151">Quando o projeto Olá concluiu a inicialização, seu aplicativo mostra a página de logon do OAuth Olá para Olá escolhido o provedor de autenticação.</span><span class="sxs-lookup"><span data-stu-id="d9153-151">When hello project has finished initializing, your application shows hello OAuth login page for hello chosen authentication provider.</span></span>

## <span data-ttu-id="d9153-152"><a name="next-steps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9153-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="d9153-153">Saiba mais [Sobre autenticação] com o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9153-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="d9153-154">Continuar o tutorial Olá adicionando [notificações por Push] tooyour Apache Cordova app.</span><span class="sxs-lookup"><span data-stu-id="d9153-154">Continue hello tutorial by adding [Push Notifications] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="d9153-155">Saiba como toouse Olá SDKs.</span><span class="sxs-lookup"><span data-stu-id="d9153-155">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="d9153-156">[SDK do Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="d9153-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="d9153-157">[SDK do Servidor ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="d9153-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="d9153-158">[SDK do Servidor Node.js]</span><span class="sxs-lookup"><span data-stu-id="d9153-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
[começar com aplicativos móveis]: app-service-mobile-cordova-get-started.md
[documentação da política de segurança de conteúdo]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[notificações por Push]: app-service-mobile-cordova-get-started-push.md
[Sobre autenticação]: app-service-mobile-auth.md
[SDK do Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[SDK do Servidor ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[SDK do Servidor Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
