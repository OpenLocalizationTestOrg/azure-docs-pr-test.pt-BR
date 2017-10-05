---
title: "Introdução à autenticação para aplicativos móveis no Xamarin iOS"
description: "Aprenda a usar os aplicativos móveis para autenticar usuários de seu aplicativo Xamarin iOS por meio de uma variedade de provedores de identidade, incluindo AAD, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 454b2df5a9bf8cfba93befea54370957ab044d95
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinios-app"></a><span data-ttu-id="dcaf9-103">Adicionar autenticação ao aplicativo Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="dcaf9-103">Add authentication to your Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="dcaf9-104">Este tópico mostra como autenticar usuários de um aplicativo móvel do Serviço de Aplicativo em seu aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-104">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="dcaf9-105">Neste tutorial, você adiciona a autenticação ao projeto de início rápido do Xamarin.iOS usando um provedor de identidade com suporte do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-105">In this tutorial, you add authentication to the Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="dcaf9-106">Depois de ser autenticado e autorizado com êxito pelo Aplicativo Móvel, o valor da ID de usuário é exibido e você poderá acessar dados da tabela restrita.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-106">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed and you will be able to access restricted table data.</span></span>

<span data-ttu-id="dcaf9-107">Você deve primeiro concluir o tutorial [Criar um aplicativo Xamarin.iOS].</span><span class="sxs-lookup"><span data-stu-id="dcaf9-107">You must first complete the tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="dcaf9-108">Se você não usar o projeto baixado de início rápido do servidor, deve adicionar o pacote de extensão de autenticação ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-108">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="dcaf9-109">Para obter mais informações sobre pacotes de extensão do servidor, confira [Trabalhar com o servidor .NET back-end do SDK para Aplicativos Móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="dcaf9-109">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="dcaf9-110">Registrar seu aplicativo para a autenticação e configurar os Serviços de Aplicativos</span><span class="sxs-lookup"><span data-stu-id="dcaf9-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-to-the-allowed-external-redirect-urls"></a><span data-ttu-id="dcaf9-111">Adicionar seu aplicativo às URLs de redirecionamento externo permitidas</span><span class="sxs-lookup"><span data-stu-id="dcaf9-111">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="dcaf9-112">A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="dcaf9-113">Isso permite que o sistema de autenticação redirecione para seu aplicativo após a conclusão do processo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-113">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="dcaf9-114">Neste tutorial, usamos sempre o esquema de URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-114">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="dcaf9-115">No entanto, você pode usar o esquema de URL que quiser.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="dcaf9-116">Ele deve ser exclusivo para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-116">It should be unique to your mobile application.</span></span> <span data-ttu-id="dcaf9-117">Para habilitar o redirecionamento no lado do servidor:</span><span class="sxs-lookup"><span data-stu-id="dcaf9-117">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="dcaf9-118">No [Portal do Azure], selecione seu Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-118">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="dcaf9-119">Clique na opção de menu **Autenticação/Autorização**.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-119">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="dcaf9-120">Em **URLs de Redirecionamento Externo Permitidas**, insira `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-120">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="dcaf9-121">O **esquema_de_URL_do_seu_aplicativo** nessa cadeia de caracteres é o esquema de URL do seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-121">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="dcaf9-122">Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).</span><span class="sxs-lookup"><span data-stu-id="dcaf9-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="dcaf9-123">Você deve anotar a cadeia de caracteres escolhida, já que precisará ajustar o código do aplicativo móvel com o esquema de URL em vários lugares.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-123">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="dcaf9-124">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-124">Click **OK**.</span></span>

5. <span data-ttu-id="dcaf9-125">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-125">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="dcaf9-126">Restringir permissões a usuários autenticados</span><span class="sxs-lookup"><span data-stu-id="dcaf9-126">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="dcaf9-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="dcaf9-128">No Visual Studio ou Xamarin Studio, execute o projeto cliente em um dispositivo ou emulador.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="dcaf9-129">Verifique se uma exceção não tratada com um código de status 401 (Não autorizado) é gerada após o aplicativo ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="dcaf9-130">A falha será registrada no console do depurador.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-130">The failure is logged to the console of the debugger.</span></span> <span data-ttu-id="dcaf9-131">Então no Visual Studio, você deve ver a falha na janela de saída.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-131">So in Visual Studio, you should see the failure in the output window.</span></span>

<span data-ttu-id="dcaf9-132">&nbsp;&nbsp;Essa falha não autorizada acontece porque o aplicativo tenta acessar o back-end do aplicativo móvel como um usuário não autenticado.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-132">&nbsp;&nbsp;This unauthorized failure happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="dcaf9-133">A tabela *TodoItem* agora exige autenticação.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-133">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="dcaf9-134">Em seguida, você atualizará o aplicativo do cliente para solicitar recursos do back-end do aplicativo móvel com um usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-134">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="dcaf9-135">Adicionar autenticação ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="dcaf9-135">Add authentication to the app</span></span>
<span data-ttu-id="dcaf9-136">Nesta seção, você modificará o aplicativo para exibir uma tela de logon antes de exibir os dados.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-136">In this section, you will modify the app to display a login screen before displaying data.</span></span> <span data-ttu-id="dcaf9-137">Quando o aplicativo for iniciado, ele não se conectará ao serviço de aplicativo e não exibirá nenhum dado.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-137">When the app starts, it will not not connect to your App Service and will not display any data.</span></span> <span data-ttu-id="dcaf9-138">Depois que o usuário executar pela primeira vez um gesto de atualização, a tela de logon aparecerá e, após o êxito no logon, a lista de itens de tarefas pendentes será exibida.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-138">After the first time that the user performs the refresh gesture, the login screen will appear; after successful login the list of todo items will be displayed.</span></span>

1. <span data-ttu-id="dcaf9-139">No projeto do cliente, abra o arquivo **QSTodoService.cs** e adicione a seguinte instrução using e `MobileServiceUser` com acessador à classe QSTodoService:</span><span class="sxs-lookup"><span data-stu-id="dcaf9-139">In the client project, open the file **QSTodoService.cs** and add the following using statement and `MobileServiceUser` with accessor to the QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="dcaf9-140">Adicione um novo método chamado **Authenticate** ao **QSTodoService** com a seguinte definição:</span><span class="sxs-lookup"><span data-stu-id="dcaf9-140">Add new method named **Authenticate** to **QSTodoService** with the following definition:</span></span>

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] <span data-ttu-id="dcaf9-141">Se você estiver usando um provedor de identidade que não seja o Facebook, altere o valor passado para **LoginAsync** acima para um dos seguintes: _MicrosoftAccount_, _Twitter_, _Google_ ou _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-141">If you are using an identity provider other than a Facebook, change the value passed to **LoginAsync** above to one of the following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="dcaf9-142">Abra o **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="dcaf9-143">Modifique a definição do método de **ViewDidLoad** removendo a chamada para **RefreshAsync()** perto do final:</span><span class="sxs-lookup"><span data-stu-id="dcaf9-143">Modify the method definition of **ViewDidLoad** removing the call to **RefreshAsync()** near the end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out the call to RefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="dcaf9-144">Modifique o método **RefreshAsync** se a propriedade **User** for null.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-144">Modify the method **RefreshAsync** to authenticate if the **User** property is null.</span></span> <span data-ttu-id="dcaf9-145">Adicione o seguinte código à parte superior da definição do método:</span><span class="sxs-lookup"><span data-stu-id="dcaf9-145">Add the following code at the top of the method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="dcaf9-146">Abra **AppDelegate.cs** e adicione o seguinte método:</span><span class="sxs-lookup"><span data-stu-id="dcaf9-146">Open **AppDelegate.cs**, add the following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="dcaf9-147">Abra o arquivo **Info.plist**, navegue até **Tipos de URL** na seção **Avançado**.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-147">Open **Info.plist** file, navigate to **URL Types** in the **Advanced** section.</span></span> <span data-ttu-id="dcaf9-148">Agora configure o **Identificador** e os **Esquemas de URL** do Tipo de URL e clique em **Adicionar Tipo de URL**.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-148">Now configure the **Identifier** and the **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="dcaf9-149">Os **Esquemas de URL** devem ser o mesmo que o {esquema_de_URL_do_seu_aplicativo}.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-149">**URL Schemes** should be the same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="dcaf9-150">No Visual Studio ou Xamarin Studio conectado ao seu Host de compilação Xamarin em seu Mac, execute o projeto de cliente direcionado a um dispositivo ou emulador.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-150">In Visual Studio or Xamarin Studio connected to your Xamarin Build Host on your Mac, run the client project targeting a device or emulator.</span></span> <span data-ttu-id="dcaf9-151">Verifique se o aplicativo não exibe dados.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-151">Verify that the app displays no data.</span></span>
   
    <span data-ttu-id="dcaf9-152">Faça um gesto de atualização pressionando a lista de itens, o que fará com que a tela de logon apareça.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-152">Perform the refresh gesture by pulling down the list of items, which will cause the login screen to appear.</span></span> <span data-ttu-id="dcaf9-153">Depois de fornecer credenciais válidas, o aplicativo exibirá a lista de itens de tarefas e você poderá atualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="dcaf9-153">Once you have successfully entered valid credentials, the app will display the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
<span data-ttu-id="dcaf9-154">[Criar um aplicativo Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="dcaf9-154">[Create a Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started.md</span></span>