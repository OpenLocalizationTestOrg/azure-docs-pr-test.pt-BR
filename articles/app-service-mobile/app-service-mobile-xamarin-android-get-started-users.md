---
title: "Introdução à autenticação para aplicativos móveis no Xamarin Android"
description: "Aprenda a usar os aplicativos móveis para autenticar usuários de seu aplicativo Xamarin Android por meio de uma variedade de provedores de identidade, incluindo AAD, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 8f9a1109018c708d52cdcb7b8bce43861cecd31c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinandroid-app"></a><span data-ttu-id="d1385-103">Adicione autenticação ao aplicativo Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="d1385-103">Add authentication to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="d1385-104">Este tópico mostra como autenticar usuários de um aplicativo móvel em seu aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="d1385-104">This topic shows you how to authenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="d1385-105">Neste tutorial, você pode adicionar autenticação ao projeto de início rápido usando um provedor de identidade suportado pelos Aplicativos Móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1385-105">In this tutorial, you add authentication to the quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="d1385-106">Após ser autenticado e autorizado com sucesso no aplicativo móvel, o valor da ID de usuário é exibido.</span><span class="sxs-lookup"><span data-stu-id="d1385-106">After being successfully authenticated and authorized in the Mobile App, the user ID value is displayed.</span></span>

<span data-ttu-id="d1385-107">Este tutorial baseia-se no início rápido do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d1385-107">This tutorial is based on the Mobile App quickstart.</span></span> <span data-ttu-id="d1385-108">Você também deve primeiro concluir o tutorial [Criar um aplicativo Xamarin.Android].</span><span class="sxs-lookup"><span data-stu-id="d1385-108">You must also first complete the tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="d1385-109">Se você não usar o projeto baixado de início rápido do servidor, deve adicionar o pacote de extensão de autenticação ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="d1385-109">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="d1385-110">Para obter mais informações sobre pacotes de extensão do servidor, confira [Trabalhar com o servidor .NET back-end do SDK para Aplicativos Móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d1385-110">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="d1385-111"><a name="register"></a>Registrar seu aplicativo para autenticação e configurar os Serviços de Aplicativos</span><span class="sxs-lookup"><span data-stu-id="d1385-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="d1385-112"><a name="redirecturl"></a>Adicionar seu aplicativo às URLs de redirecionamento externo permitidas</span><span class="sxs-lookup"><span data-stu-id="d1385-112"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="d1385-113">A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1385-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="d1385-114">Isso permite que o sistema de autenticação redirecione para seu aplicativo após a conclusão do processo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="d1385-114">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="d1385-115">Neste tutorial, usamos sempre o esquema de URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="d1385-115">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="d1385-116">No entanto, você pode usar o esquema de URL que quiser.</span><span class="sxs-lookup"><span data-stu-id="d1385-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="d1385-117">Ele deve ser exclusivo para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d1385-117">It should be unique to your mobile application.</span></span> <span data-ttu-id="d1385-118">Para habilitar o redirecionamento no lado do servidor:</span><span class="sxs-lookup"><span data-stu-id="d1385-118">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="d1385-119">No [Portal do Azure], selecione seu Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1385-119">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="d1385-120">Clique na opção de menu **Autenticação/Autorização**.</span><span class="sxs-lookup"><span data-stu-id="d1385-120">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="d1385-121">Em **URLs de Redirecionamento Externo Permitidas**, insira `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="d1385-121">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="d1385-122">O **esquema_de_URL_do_seu_aplicativo** nessa cadeia de caracteres é o esquema de URL do seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d1385-122">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="d1385-123">Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).</span><span class="sxs-lookup"><span data-stu-id="d1385-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="d1385-124">Você deve anotar a cadeia de caracteres escolhida, já que precisará ajustar o código do aplicativo móvel com o esquema de URL em vários lugares.</span><span class="sxs-lookup"><span data-stu-id="d1385-124">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="d1385-125">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1385-125">Click **OK**.</span></span>

5. <span data-ttu-id="d1385-126">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d1385-126">Click **Save**.</span></span>

## <span data-ttu-id="d1385-127"><a name="permissions"></a>Restringir permissões a usuários autenticados</span><span class="sxs-lookup"><span data-stu-id="d1385-127"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="d1385-128">No Visual Studio ou Xamarin Studio, execute o projeto cliente em um dispositivo ou emulador.</span><span class="sxs-lookup"><span data-stu-id="d1385-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="d1385-129">Verifique se uma exceção não tratada com um código de status 401 (Não autorizado) é gerada após o aplicativo ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="d1385-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="d1385-130">Isso acontece porque o aplicativo tenta acessar o back-end do aplicativo móvel como um usuário não autenticado.</span><span class="sxs-lookup"><span data-stu-id="d1385-130">This happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="d1385-131">A tabela *TodoItem* agora exige autenticação.</span><span class="sxs-lookup"><span data-stu-id="d1385-131">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="d1385-132">Em seguida, você atualizará o aplicativo do cliente para solicitar recursos do back-end do aplicativo móvel com um usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="d1385-132">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="d1385-133"><a name="add-authentication"></a>Adicionar autenticação ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="d1385-133"><a name="add-authentication"></a>Add authentication to the app</span></span>
<span data-ttu-id="d1385-134">O aplicativo é atualizado para exigir que os usuários toquem no botão **Entrar** e se autentiquem para que os dados sejam exibidos.</span><span class="sxs-lookup"><span data-stu-id="d1385-134">The app is updated to require users to tap the **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="d1385-135">Adicione o seguinte código à classe **TodoActivity** :</span><span class="sxs-lookup"><span data-stu-id="d1385-135">Add the following code to the **TodoActivity** class:</span></span>
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide the button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load the data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="d1385-136">Isso cria um novo método para autenticar um usuário e um manipulador de método para um novo botão **Entrar** .</span><span class="sxs-lookup"><span data-stu-id="d1385-136">This creates a new method to authenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="d1385-137">O usuário no código de exemplo acima é autenticado usando um logon do Facebook.</span><span class="sxs-lookup"><span data-stu-id="d1385-137">The user in the example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="d1385-138">Uma caixa de diálogo é usada para exibir a ID de usuário após a autenticação.</span><span class="sxs-lookup"><span data-stu-id="d1385-138">A dialog is used to display the user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d1385-139">Se estiver usando um provedor de identidade que não seja o Facebook, altere o valor transmitido para **LoginAsync** acima para um dos seguintes: *MicrosoftAccount*, *Twitter*, *Google* ou *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="d1385-139">If you are using an identity provider other than Facebook, change the value passed to **LoginAsync** above to one of the following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="d1385-140">No método **OnCreate** , exclua ou comente a linha de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1385-140">In the **OnCreate** method, delete or comment-out the following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="d1385-141">No arquivo Activity_To_Do.axml, adicione a definição do botão *LoginUser* a seguir antes do botão *AddItem* existente:</span><span class="sxs-lookup"><span data-stu-id="d1385-141">In the Activity_To_Do.axml file, add the following *LoginUser* button definition before the existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="d1385-142">Adicione o elemento a seguir no arquivo de recursos de Strings.xml:</span><span class="sxs-lookup"><span data-stu-id="d1385-142">Add the following element to the Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="d1385-143">Abra o arquivo AndroidManifest.xml e adicione o seguinte código dentro do elemento XML `<application>`:</span><span class="sxs-lookup"><span data-stu-id="d1385-143">Open the AndroidManifest.xml file, add the following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="d1385-144">No Visual Studio ou Xamarin Studio, execute o projeto cliente em um dispositivo ou emulador e entre com o seu provedor de identidade preferido.</span><span class="sxs-lookup"><span data-stu-id="d1385-144">In Visual Studio or Xamarin Studio, run the client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="d1385-145">Quando você entrar com êxito, o aplicativo exibirá o sua ID de logon e a lista de itens de tarefas e você poderá fazer atualizações aos dados.</span><span class="sxs-lookup"><span data-stu-id="d1385-145">When you are successfully logged-in, the app will display your login ID and the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
<span data-ttu-id="d1385-146">[Criar um aplicativo Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="d1385-146">[Create a Xamarin.Android app]: app-service-mobile-xamarin-android-get-started.md</span></span>