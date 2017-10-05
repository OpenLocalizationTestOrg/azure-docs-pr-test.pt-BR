---
title: "Adicionar autenticação no Apache Cordova com os Aplicativos Móveis| Microsoft Docs"
description: "Saiba como usar os Aplicativos Móveis no Serviço de Aplicativo do Azure para autenticar usuários de seu aplicativo Apache Cordova usando vários provedores de identidade, incluindo Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: b7362b7f26859de541f792e714502851d74c98e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-apache-cordova-app"></a><span data-ttu-id="57748-103">Adicionar autenticação ao aplicativo Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="57748-103">Add authentication to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="57748-104">Resumo</span><span class="sxs-lookup"><span data-stu-id="57748-104">Summary</span></span>
<span data-ttu-id="57748-105">Neste tutorial, você adiciona a autenticação ao projeto de início rápido todolist no Apache Cordova usando um provedor de identidade com suporte.</span><span class="sxs-lookup"><span data-stu-id="57748-105">In this tutorial, you add authentication to the todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="57748-106">Este tutorial se baseia no tutorial [Introdução aos Aplicativos Móveis] , que você deve concluir primeiro.</span><span class="sxs-lookup"><span data-stu-id="57748-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="57748-107"><a name="register"></a>Registrar seu aplicativo para autenticação e configurar o Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="57748-107"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="57748-108">Assista a um vídeo que mostra etapas semelhantes</span><span class="sxs-lookup"><span data-stu-id="57748-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="57748-109"><a name="permissions"></a>Restringir permissões a usuários autenticados</span><span class="sxs-lookup"><span data-stu-id="57748-109"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="57748-110">Agora, é possível verificar se o acesso anônimo para o back-end foi desabilitado.</span><span class="sxs-lookup"><span data-stu-id="57748-110">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="57748-111">No Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="57748-111">In Visual Studio:</span></span>

* <span data-ttu-id="57748-112">Abra o projeto criado quando você concluiu o tutorial [Introdução aos Aplicativos Móveis].</span><span class="sxs-lookup"><span data-stu-id="57748-112">Open the project that you created when you completed the tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="57748-113">Executar o aplicativo no **Emulador do Google Android**.</span><span class="sxs-lookup"><span data-stu-id="57748-113">Run your application in the **Google Android Emulator**.</span></span>
* <span data-ttu-id="57748-114">Verifique se uma Falha Inesperada de Conexão é mostrada após o aplicativo ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="57748-114">Verify that an Unexpected Connection Failure is shown after the app starts.</span></span>

<span data-ttu-id="57748-115">Em seguida, atualize o aplicativo para autenticar os usuários antes de solicitar recursos do back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="57748-115">Next, update the app to authenticate users before requesting resources from the Mobile App backend.</span></span>

## <span data-ttu-id="57748-116"><a name="add-authentication"></a>Adicionar autenticação ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="57748-116"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="57748-117">Abra o projeto no **Visual Studio** e abra o arquivo `www/index.html` para edição.</span><span class="sxs-lookup"><span data-stu-id="57748-117">Open your project in **Visual Studio**, then open the `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="57748-118">Localize a marca meta `Content-Security-Policy` na seção de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="57748-118">Locate the `Content-Security-Policy` meta tag in the head section.</span></span>  <span data-ttu-id="57748-119">Adicione o host OAuth à lista de fontes permitidas.</span><span class="sxs-lookup"><span data-stu-id="57748-119">Add the OAuth host to the list of allowed sources.</span></span>

   | <span data-ttu-id="57748-120">Provedor</span><span class="sxs-lookup"><span data-stu-id="57748-120">Provider</span></span> | <span data-ttu-id="57748-121">Nome do provedor do SDK</span><span class="sxs-lookup"><span data-stu-id="57748-121">SDK Provider Name</span></span> | <span data-ttu-id="57748-122">Host OAuth</span><span class="sxs-lookup"><span data-stu-id="57748-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="57748-123">Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="57748-123">Azure Active Directory</span></span> | <span data-ttu-id="57748-124">aad</span><span class="sxs-lookup"><span data-stu-id="57748-124">aad</span></span> | <span data-ttu-id="57748-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="57748-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="57748-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="57748-126">Facebook</span></span> | <span data-ttu-id="57748-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="57748-127">facebook</span></span> | <span data-ttu-id="57748-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="57748-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="57748-129">Google</span><span class="sxs-lookup"><span data-stu-id="57748-129">Google</span></span> | <span data-ttu-id="57748-130">Google</span><span class="sxs-lookup"><span data-stu-id="57748-130">google</span></span> | <span data-ttu-id="57748-131">https://accounts.google.com</span><span class="sxs-lookup"><span data-stu-id="57748-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="57748-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="57748-132">Microsoft</span></span> | <span data-ttu-id="57748-133">microsoftaccount</span><span class="sxs-lookup"><span data-stu-id="57748-133">microsoftaccount</span></span> | <span data-ttu-id="57748-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="57748-134">https://login.live.com</span></span> |
   | <span data-ttu-id="57748-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="57748-135">Twitter</span></span> | <span data-ttu-id="57748-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="57748-136">twitter</span></span> | <span data-ttu-id="57748-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="57748-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="57748-138">Veja a seguir um exemplo de Política de segurança de conteúdo (implementada para o Active Directory do Azure):</span><span class="sxs-lookup"><span data-stu-id="57748-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="57748-139">Substitua `https://login.microsoftonline.com` pelo host OAuth da tabela anterior.</span><span class="sxs-lookup"><span data-stu-id="57748-139">Replace `https://login.microsoftonline.com` with the OAuth host from the preceding table.</span></span>  <span data-ttu-id="57748-140">Para obter mais informações sobre a marcação meta content-security-policy, consulte a [Documentação de Content-Security-Policy].</span><span class="sxs-lookup"><span data-stu-id="57748-140">For more information about the content-security-policy meta tag, see the [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="57748-141">Alguns provedores de autenticação não exigem mudanças no Content-Security-Policy quando usado em dispositivos móveis apropriados.</span><span class="sxs-lookup"><span data-stu-id="57748-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="57748-142">Por exemplo, nenhuma mudança na Política de segurança de conteúdo será necessária ao usar a autenticação do Google em um dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="57748-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="57748-143">Abra o arquivo `www/js/index.js` para edição, localize o método `onDeviceReady()` e adicione o seguinte sob o código de criação do cliente:</span><span class="sxs-lookup"><span data-stu-id="57748-143">Open the `www/js/index.js` file for editing, locate the `onDeviceReady()` method, and under the client  creation code add the following code:</span></span>

        // Login to the service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="57748-144">Esse código substitui o código existente que cria a referência de tabela e atualiza a interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="57748-144">This code replaces the existing code that creates the table reference and refreshes the UI.</span></span>

    <span data-ttu-id="57748-145">O método logon() inicia a autenticação com o provedor.</span><span class="sxs-lookup"><span data-stu-id="57748-145">The login() method starts authentication with the provider.</span></span> <span data-ttu-id="57748-146">O método login() é uma função assíncrona que retorna uma promessa de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="57748-146">The login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="57748-147">O restante da inicialização é colocado dentro da resposta de promessa para que não seja executado até a conclusão do método login().</span><span class="sxs-lookup"><span data-stu-id="57748-147">The rest of the initialization is placed inside the promise response so that it is not executed until the login() method completes.</span></span>

4. <span data-ttu-id="57748-148">No código que você acabou de adicionar, substitua `SDK_Provider_Name` pelo nome de seu provedor de logon.</span><span class="sxs-lookup"><span data-stu-id="57748-148">In the code that you just added, replace `SDK_Provider_Name` with the name of your login provider.</span></span> <span data-ttu-id="57748-149">Por exemplo, para o Azure Active Directory, use `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="57748-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="57748-150">Execute seu projeto.</span><span class="sxs-lookup"><span data-stu-id="57748-150">Run your project.</span></span>  <span data-ttu-id="57748-151">Após a conclusão da inicialização do projeto, o aplicativo mostrará a página de logon do OAuth para o provedor de autenticação escolhido.</span><span class="sxs-lookup"><span data-stu-id="57748-151">When the project has finished initializing, your application shows the OAuth login page for the chosen authentication provider.</span></span>

## <span data-ttu-id="57748-152"><a name="next-steps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="57748-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="57748-153">Saiba mais [Sobre autenticação] com o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="57748-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="57748-154">Continue o tutorial adicionando [Notificações por push] a seu aplicativo do Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="57748-154">Continue the tutorial by adding [Push Notifications] to your Apache Cordova app.</span></span>

<span data-ttu-id="57748-155">Saiba como usar os SDKs.</span><span class="sxs-lookup"><span data-stu-id="57748-155">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="57748-156">[SDK do Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="57748-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="57748-157">[SDK do Servidor ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="57748-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="57748-158">[SDK do Servidor Node.js]</span><span class="sxs-lookup"><span data-stu-id="57748-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
<span data-ttu-id="57748-159">[Introdução aos Aplicativos Móveis]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="57748-159">[Get started with Mobile Apps]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="57748-160">[Documentação de Content-Security-Policy]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span><span class="sxs-lookup"><span data-stu-id="57748-160">[Content-Security-Policy documentation]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span></span>
<span data-ttu-id="57748-161">[Notificações por push]: app-service-mobile-cordova-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="57748-161">[Push Notifications]: app-service-mobile-cordova-get-started-push.md</span></span>
<span data-ttu-id="57748-162">[Sobre autenticação]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="57748-162">[About Authentication]: app-service-mobile-auth.md</span></span>
<span data-ttu-id="57748-163">[SDK do Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md</span><span class="sxs-lookup"><span data-stu-id="57748-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span></span>
<span data-ttu-id="57748-164">[SDK do Servidor ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="57748-164">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
<span data-ttu-id="57748-165">[SDK do Servidor Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="57748-165">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span></span>
