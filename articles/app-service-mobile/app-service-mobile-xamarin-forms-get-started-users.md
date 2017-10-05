---
title: "Introdução à autenticação para os Aplicativos Móveis no aplicativo Xamarin.Forms | Microsoft Docs"
description: "Saiba como usar os Aplicativos Móveis para autenticar usuários de seu aplicativo Xamarin Forms por meio de uma variedade de provedores de identidade, incluindo o AAD, o Google, o Facebook, o Twitter e o Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 9e14e95793bcc81ad46783fd50ba223eec4ea360
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="add-authentication-to-your-xamarin-forms-app"></a><span data-ttu-id="48baa-103">Adicionar autenticação ao seu aplicativo Xamarin Forms</span><span class="sxs-lookup"><span data-stu-id="48baa-103">Add authentication to your Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="48baa-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="48baa-104">Overview</span></span>
<span data-ttu-id="48baa-105">Este tópico mostra como autenticar usuários de um aplicativo móvel do Serviço de Aplicativo em seu aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="48baa-105">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="48baa-106">Neste tutorial, você adiciona a autenticação ao projeto de início rápido do Xamarin.Forms usando um provedor de identidade com suporte do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48baa-106">In this tutorial, you add authentication to the Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="48baa-107">Depois de ser autenticado e autorizado com êxito pelo Aplicativo Móvel, o valor da ID de usuário é exibido e você poderá acessar dados da tabela restrita.</span><span class="sxs-lookup"><span data-stu-id="48baa-107">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed, and you will be able to access restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48baa-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="48baa-108">Prerequisites</span></span>
<span data-ttu-id="48baa-109">Para obter o melhor resultado com este tutorial, é recomendável concluir primeiro o tutorial [Criar um aplicativo Xamarin.Forms][1].</span><span class="sxs-lookup"><span data-stu-id="48baa-109">For the best result with this tutorial, we recommend that you first complete the [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="48baa-110">Depois de concluir este tutorial, você terá um projeto Xamarin.Forms que é um aplicativo de lista de tarefas para várias plataformas.</span><span class="sxs-lookup"><span data-stu-id="48baa-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="48baa-111">Se você não usar o projeto baixado de início rápido do servidor, deve adicionar o pacote de extensão de autenticação ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="48baa-111">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="48baa-112">Para saber mais sobre pacotes de extensão do servidor, confira [Trabalhar com o servidor .NET back-end do SDK para Aplicativos Móveis do Azure][2].</span><span class="sxs-lookup"><span data-stu-id="48baa-112">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="48baa-113">Registrar seu aplicativo para a autenticação e configurar os Serviços de Aplicativos</span><span class="sxs-lookup"><span data-stu-id="48baa-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="48baa-114"><a name="redirecturl"></a>Adicionar seu aplicativo às URLs de redirecionamento externo permitidas</span><span class="sxs-lookup"><span data-stu-id="48baa-114"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="48baa-115">A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48baa-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="48baa-116">Isso permite que o sistema de autenticação redirecione para seu aplicativo após a conclusão do processo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="48baa-116">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="48baa-117">Neste tutorial, usamos sempre o esquema de URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="48baa-117">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="48baa-118">No entanto, você pode usar o esquema de URL que quiser.</span><span class="sxs-lookup"><span data-stu-id="48baa-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="48baa-119">Ele deve ser exclusivo para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="48baa-119">It should be unique to your mobile application.</span></span> <span data-ttu-id="48baa-120">Para habilitar o redirecionamento no lado do servidor:</span><span class="sxs-lookup"><span data-stu-id="48baa-120">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="48baa-121">No [Portal do Azure], selecione seu Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48baa-121">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="48baa-122">Clique na opção de menu **Autenticação/Autorização**.</span><span class="sxs-lookup"><span data-stu-id="48baa-122">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="48baa-123">Em **URLs de Redirecionamento Externo Permitidas**, insira `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="48baa-123">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="48baa-124">O **esquema_de_URL_do_seu_aplicativo** nessa cadeia de caracteres é o esquema de URL do seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="48baa-124">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="48baa-125">Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).</span><span class="sxs-lookup"><span data-stu-id="48baa-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="48baa-126">Você deve anotar a cadeia de caracteres escolhida, já que precisará ajustar o código do aplicativo móvel com o esquema de URL em vários lugares.</span><span class="sxs-lookup"><span data-stu-id="48baa-126">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="48baa-127">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="48baa-127">Click **OK**.</span></span>

5. <span data-ttu-id="48baa-128">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="48baa-128">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="48baa-129">Restringir permissões a usuários autenticados</span><span class="sxs-lookup"><span data-stu-id="48baa-129">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-to-the-portable-class-library"></a><span data-ttu-id="48baa-130">Adicionar autenticação à biblioteca de classes portátil</span><span class="sxs-lookup"><span data-stu-id="48baa-130">Add authentication to the portable class library</span></span>
<span data-ttu-id="48baa-131">Os Aplicativos Móveis usam o método de extensão [LoginAsync][3] no [MobileServiceClient][4] para que um usuário entre com a autenticação do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48baa-131">Mobile Apps uses the [LoginAsync][3] extension method on the [MobileServiceClient][4] to sign in a user with App Service authentication.</span></span> <span data-ttu-id="48baa-132">Este exemplo usa um fluxo de autenticação gerenciado por servidor que exibe a interface de entrada do provedor no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48baa-132">This sample uses a server-managed authentication flow that displays the provider's sign-in interface in the app.</span></span> <span data-ttu-id="48baa-133">Para saber mais, veja [Autenticação gerenciada pelo servidor][5].</span><span class="sxs-lookup"><span data-stu-id="48baa-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="48baa-134">Para proporcionar uma melhor experiência ao usuário em seu aplicativo de produção, você deve considerar o uso da [Autenticação gerenciada pelo cliente][6].</span><span class="sxs-lookup"><span data-stu-id="48baa-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="48baa-135">Para se autenticar em um projeto Xamarin.Forms, defina uma interface **IAuthenticate** na Biblioteca de Classes Portátil para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48baa-135">To authenticate with a Xamarin Forms project, define an **IAuthenticate** interface in the Portable Class Library for the app.</span></span> <span data-ttu-id="48baa-136">Em seguida, adicione um botão **Entrar** à interface de usuário definida na Biblioteca de Classes Portátil, em que você possa clicar para iniciar a autenticação.</span><span class="sxs-lookup"><span data-stu-id="48baa-136">Then add a **Sign-in** button to the user interface defined in the Portable Class Library, which you click to start authentication.</span></span> <span data-ttu-id="48baa-137">Os dados são carregados do back-end do aplicativo móvel depois da autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="48baa-137">Data is loaded from the mobile app backend after successful authentication.</span></span>

<span data-ttu-id="48baa-138">Implemente a interface **IAuthenticate** para cada plataforma compatível com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48baa-138">Implement the **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="48baa-139">No Visual Studio ou no Xamarin Studio, abra App.cs do projeto com **Portable no nome**, que é o projeto da Biblioteca de Classes Portátil, e adicione a seguinte instrução `using`:</span><span class="sxs-lookup"><span data-stu-id="48baa-139">In Visual Studio or Xamarin Studio, open App.cs from the project with **Portable** in the name, which is Portable Class Library project, then  add the following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="48baa-140">Em App.cs, adicione a definição de interface `IAuthenticate` a seguir imediatamente antes da definição de classe `App`.</span><span class="sxs-lookup"><span data-stu-id="48baa-140">In App.cs, add the following `IAuthenticate` interface definition immediately before the `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="48baa-141">Para inicializar a interface com uma implementação específica de plataforma, adicione os membros estáticos a seguir à classe **App**.</span><span class="sxs-lookup"><span data-stu-id="48baa-141">To initialize the interface with a platform-specific implementation, add the following static members to the **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="48baa-142">Abra TodoList.xaml do projeto da Biblioteca de Classes Portátil, adicione o elemento **Button** a seguir ao elemento de layout *buttonsPanel* após o botão existente:</span><span class="sxs-lookup"><span data-stu-id="48baa-142">Open TodoList.xaml from the Portable Class Library project, add the following **Button** element in the *buttonsPanel* layout element, after the existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="48baa-143">Esse botão dispara a autenticação gerenciada por servidor com seu back-end de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="48baa-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="48baa-144">Abra TodoList.xaml.cs do projeto da Biblioteca de Classes Portátil e adicione o seguinte campo à classe `TodoList` :</span><span class="sxs-lookup"><span data-stu-id="48baa-144">Open TodoList.xaml.cs from the Portable Class Library project, then add the following field to the `TodoList` class:</span></span>

        // Track whether the user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="48baa-145">Substitua o método **OnAppearing** pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="48baa-145">Replace the **OnAppearing** method with the following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems to true in order to synchronize the data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide the Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="48baa-146">Esse código garante que os dados só serão atualizados do serviço depois que você tiver sido autenticado.</span><span class="sxs-lookup"><span data-stu-id="48baa-146">This code makes sure that data is only refreshed from the service after you have been authenticated.</span></span>
7. <span data-ttu-id="48baa-147">Adicione o seguinte manipulador para o evento **Clicked** à classe **TodoList**:</span><span class="sxs-lookup"><span data-stu-id="48baa-147">Add the following handler for the **Clicked** event to the **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems to true to synchronize the data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="48baa-148">Salve suas alterações e compile o projeto de Biblioteca de Classes Portátil verificando se não há erros.</span><span class="sxs-lookup"><span data-stu-id="48baa-148">Save your changes and rebuild the Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-to-the-android-app"></a><span data-ttu-id="48baa-149">Adicionar autenticação ao aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="48baa-149">Add authentication to the Android app</span></span>
<span data-ttu-id="48baa-150">Esta seção mostra como implementar a interface **IAuthenticate** no projeto do aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="48baa-150">This section shows how to implement the **IAuthenticate** interface in the Android app project.</span></span> <span data-ttu-id="48baa-151">Ignore esta seção se não estiver dando suporte a dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="48baa-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="48baa-152">No Visual Studio ou no Xamarin Studio, clique com botão direito do mouse no projeto **droid** e em **Definir como Projeto de Inicialização**.</span><span class="sxs-lookup"><span data-stu-id="48baa-152">In Visual Studio or Xamarin Studio, right-click the **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="48baa-153">Pressione F5 para iniciar o projeto no depurador e verifique se uma exceção sem tratamento com um código de status de 401 (Não autorizado) foi gerada depois que o aplicativo foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="48baa-153">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="48baa-154">O código 401 é gerado porque o acesso no back-end é restrito apenas aos usuários autorizados.</span><span class="sxs-lookup"><span data-stu-id="48baa-154">The 401 code is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="48baa-155">Abra MainActivity.cs no projeto Android e adicione estas instruções `using` :</span><span class="sxs-lookup"><span data-stu-id="48baa-155">Open MainActivity.cs in the Android project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="48baa-156">Atualize a classe **MainActivity** para implementar a interface **IAuthenticate** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="48baa-156">Update the **MainActivity** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="48baa-157">Atualize a classe **MainActivity** adicionando um campo **MobileServiceUser** e um método **Authenticate**, que é necessário para a interface **IAuthenticate**, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="48baa-157">Update the **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display the success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="48baa-158">Se você estiver usando um provedor de identidade diferente do Facebook, escolha outro valor para [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="48baa-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="48baa-159">Adicione o código a seguir dentro do nó <application> do AndroidManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="48baa-159">Add the following code inside <application> node of AndroidManifest.xml:</span></span>

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. <span data-ttu-id="48baa-160">Adicione o seguinte código ao método **onCreate** da classe **MainActivity** antes de chamar `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="48baa-160">Add the following code to the **OnCreate** method of the **MainActivity** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="48baa-161">Esse código garante que o autenticador seja inicializado antes que o aplicativo seja carregado.</span><span class="sxs-lookup"><span data-stu-id="48baa-161">This code ensures the authenticator is initialized before the app loads.</span></span>
2. <span data-ttu-id="48baa-162">Recompile o aplicativo, execute-o, entre com o provedor de autenticação escolhido e verifique se você consegue acessar os dados como um usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="48baa-162">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-the-ios-app"></a><span data-ttu-id="48baa-163">Adicionar autenticação ao aplicativo do iOS</span><span class="sxs-lookup"><span data-stu-id="48baa-163">Add authentication to the iOS app</span></span>
<span data-ttu-id="48baa-164">Esta seção mostra como implementar a interface **IAuthenticate** no projeto do aplicativo iOS.</span><span class="sxs-lookup"><span data-stu-id="48baa-164">This section shows how to implement the **IAuthenticate** interface in the iOS app project.</span></span> <span data-ttu-id="48baa-165">Ignore esta seção se não estiver dando suporte a dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="48baa-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="48baa-166">No Visual Studio ou no Xamarin Studio, clique com o botão direito do mouse no projeto **iOS** e em **Definir como Projeto de Inicialização**.</span><span class="sxs-lookup"><span data-stu-id="48baa-166">In Visual Studio or Xamarin Studio, right-click the **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="48baa-167">Pressione F5 para iniciar o projeto no depurador e verifique se uma exceção sem tratamento com um código de status de 401 (Não autorizado) foi gerada depois que o aplicativo foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="48baa-167">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="48baa-168">A resposta 401 é gerada porque o acesso no back-end é restrito apenas aos usuários autorizados.</span><span class="sxs-lookup"><span data-stu-id="48baa-168">The 401 response is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="48baa-169">Abra AppDelegate.cs no projeto do iOS e adicione as seguintes instruções `using` :</span><span class="sxs-lookup"><span data-stu-id="48baa-169">Open AppDelegate.cs in the iOS project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="48baa-170">Atualize a classe **AppDelegate** para implementar a interface **IAuthenticate** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="48baa-170">Update the **AppDelegate** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="48baa-171">Atualize a classe **AppDelegate** adicionando um campo **MobileServiceUser** e um método **Authenticate**, que é necessário para a interface **IAuthenticate**, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="48baa-171">Update the **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display the success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="48baa-172">Se você estiver usando um provedor de identidade diferente do Facebook, escolha outro valor para [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="48baa-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="48baa-173">Atualizar a classe AppDelegate adicionando a sobrecarga do método OpenUrl(aplicativo UIApplication, URL NSUrl e opções NSDictionary)</span><span class="sxs-lookup"><span data-stu-id="48baa-173">Update the AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="48baa-174">Adicione a seguinte linha de código ao método **FinishedLaunching** antes de chamar `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="48baa-174">Add the following line of code to the **FinishedLaunching** method before the call to `LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="48baa-175">Esse código garante que o autenticador seja inicializado antes que o aplicativo seja carregado.</span><span class="sxs-lookup"><span data-stu-id="48baa-175">This code ensures the authenticator is initialized before the app is loaded.</span></span>

6. <span data-ttu-id="48baa-176">Adicione **{url_scheme_of_your_app}** para Esquemas de URL em Info.plist.</span><span class="sxs-lookup"><span data-stu-id="48baa-176">Add **{url_scheme_of_your_app}** to URL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="48baa-177">Recompile o aplicativo, execute-o, entre com o provedor de autenticação escolhido e verifique se você consegue acessar os dados como um usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="48baa-177">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-windows-10-including-phone-app-projects"></a><span data-ttu-id="48baa-178">Adicionar autenticação a projetos de aplicativo do Windows 10 (incluindo o Phone)</span><span class="sxs-lookup"><span data-stu-id="48baa-178">Add authentication to Windows 10 (including Phone) app projects</span></span>
<span data-ttu-id="48baa-179">Esta seção mostra como implementar a interface **IAuthenticate** nos projetos de aplicativo do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="48baa-179">This section shows how to implement the **IAuthenticate** interface in the Windows 10 app projects.</span></span> <span data-ttu-id="48baa-180">As mesmas etapas se aplicam aos projetos UWP (Plataforma Universal do Windows), mas usando o projeto **UWP** (com alterações indicadas).</span><span class="sxs-lookup"><span data-stu-id="48baa-180">The same steps apply for Universal Windows Platform (UWP) projects, but using the **UWP** project (with noted changes).</span></span> <span data-ttu-id="48baa-181">Ignore esta seção se não estiver dando suporte a dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="48baa-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="48baa-182">"No Visual Studio, clique com o botão direito do mouse no projeto **UWP** e depois em **Definir como Projeto de Inicialização**.</span><span class="sxs-lookup"><span data-stu-id="48baa-182">"In Visual Studio, right-click either the **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="48baa-183">Pressione F5 para iniciar o projeto no depurador e verifique se uma exceção sem tratamento com um código de status de 401 (Não autorizado) foi gerada depois que o aplicativo foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="48baa-183">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="48baa-184">Essa resposta 401 é gerada porque o acesso no back-end é restrito apenas aos usuários autorizados.</span><span class="sxs-lookup"><span data-stu-id="48baa-184">The 401 response happens because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="48baa-185">Abra MainPage.xaml.cs para o projeto do aplicativo do Windows e adicione as seguintes instruções `using` :</span><span class="sxs-lookup"><span data-stu-id="48baa-185">Open MainPage.xaml.cs for the Windows app project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="48baa-186">Substitua `<your_Portable_Class_Library_namespace>` pelo namespace para sua biblioteca de classes portátil.</span><span class="sxs-lookup"><span data-stu-id="48baa-186">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>
4. <span data-ttu-id="48baa-187">Atualize a classe **MainPage** para implementar a interface **IAuthenticate** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="48baa-187">Update the **MainPage** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="48baa-188">Atualize a classe **MainPage** adicionando um campo **MobileServiceUser** e um método **Authenticate**, que é necessário para a interface **IAuthenticate**, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="48baa-188">Update the **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display the success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="48baa-189">Se você estiver usando um provedor de identidade diferente do Facebook, escolha outro valor para [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="48baa-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="48baa-190">Adicione a seguinte linha de código no construtor para a classe **MainPage** antes de chamar `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="48baa-190">Add the following line of code in the constructor for the **MainPage** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="48baa-191">Substitua `<your_Portable_Class_Library_namespace>` pelo namespace para sua biblioteca de classes portátil.</span><span class="sxs-lookup"><span data-stu-id="48baa-191">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>

3. <span data-ttu-id="48baa-192">Se estiver usando a **UWP**, adicione a seguinte substituição do método **OnActivated** à classe **App**:</span><span class="sxs-lookup"><span data-stu-id="48baa-192">If you are using **UWP**, add the following **OnActivated** method override to the **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="48baa-193">Quando a substituição do método já existir, adicione o código condicional do trecho anterior.</span><span class="sxs-lookup"><span data-stu-id="48baa-193">When the method override already exists, add the conditional code from the preceding snippet.</span></span>  <span data-ttu-id="48baa-194">Esse código não é necessário para projetos Universais do Windows.</span><span class="sxs-lookup"><span data-stu-id="48baa-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="48baa-195">Adicionar **{url_scheme_of_your_app}** em Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="48baa-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="48baa-196">Recompile o aplicativo, execute-o, entre com o provedor de autenticação escolhido e verifique se você consegue acessar os dados como um usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="48baa-196">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48baa-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48baa-197">Next steps</span></span>
<span data-ttu-id="48baa-198">Agora que você concluiu este tutorial de autenticação básica, considere continuar com um dos seguintes tutoriais:</span><span class="sxs-lookup"><span data-stu-id="48baa-198">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="48baa-199">Adicionar notificações por push ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="48baa-199">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="48baa-200">Saiba como adicionar suporte a notificações por push ao aplicativo e configurar o back-end do Aplicativo Móvel para usar os Hubs de Notificação do Azure para enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="48baa-200">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="48baa-201">Habilitar sincronização offline para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="48baa-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="48baa-202">Saiba como adicionar suporte offline ao seu aplicativo usando um back-end de Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="48baa-202">Learn how to add offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="48baa-203">A sincronização offline permite que os usuários finais interajam com um aplicativo móvel, exibindo, adicionando ou modificando dados, mesmo quando não há conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="48baa-203">Offline sync allows end users to interact with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
