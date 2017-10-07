---
title: "aaaGet iniciado com a autenticação para aplicativos móveis no aplicativo Xamarin Forms | Microsoft Docs"
description: "Saiba como usuários de tooauthenticate toouse aplicativos móveis do seu aplicativo Xamarin Forms por meio de uma variedade de provedores de identidade, incluindo AAD, Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a><span data-ttu-id="05f1c-103">Adicionar autenticação tooyour Xamarin Forms aplicativo</span><span class="sxs-lookup"><span data-stu-id="05f1c-103">Add authentication tooyour Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="05f1c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="05f1c-104">Overview</span></span>
<span data-ttu-id="05f1c-105">Este tópico mostra como tooauthenticate usuários de um serviço de aplicativo móvel aplicativo do seu aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="05f1c-105">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="05f1c-106">Neste tutorial, você pode adicionar autenticação ao projeto de início rápido do Xamarin Forms hello usando um provedor de identidade que é suportado pelo serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="05f1c-106">In this tutorial, you add authentication to hello Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="05f1c-107">Depois com êxito que está sendo autenticado e autorizado pelo seu aplicativo móvel, o valor de ID de usuário de saudação é exibida e você será capaz de tooaccess restringido dados da tabela.</span><span class="sxs-lookup"><span data-stu-id="05f1c-107">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed, and you will be able tooaccess restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05f1c-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="05f1c-108">Prerequisites</span></span>
<span data-ttu-id="05f1c-109">Para um resultado melhor de saudação com este tutorial, é recomendável concluir primeiro Olá [criar um aplicativo Xamarin Forms] [ 1] tutorial.</span><span class="sxs-lookup"><span data-stu-id="05f1c-109">For hello best result with this tutorial, we recommend that you first complete hello [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="05f1c-110">Depois de concluir este tutorial, você terá um projeto Xamarin.Forms que é um aplicativo de lista de tarefas para várias plataformas.</span><span class="sxs-lookup"><span data-stu-id="05f1c-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="05f1c-111">Se você não usar Olá baixar o projeto de servidor de início rápido, você deve adicionar o projeto de tooyour de pacote de extensão de autenticação hello.</span><span class="sxs-lookup"><span data-stu-id="05f1c-111">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="05f1c-112">Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure][2].</span><span class="sxs-lookup"><span data-stu-id="05f1c-112">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="05f1c-113">Registrar seu aplicativo para a autenticação e configurar os Serviços de Aplicativos</span><span class="sxs-lookup"><span data-stu-id="05f1c-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="05f1c-114"><a name="redirecturl"></a>Adicionar URLs de redirecionamento externo permitidos de toohello seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="05f1c-114"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="05f1c-115">A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="05f1c-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="05f1c-116">Isso permite Olá autenticação sistema tooredirect tooyour back aplicativo após a conclusão do processo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="05f1c-116">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="05f1c-117">Neste tutorial, usamos o esquema de URL Olá _appname_ em todo.</span><span class="sxs-lookup"><span data-stu-id="05f1c-117">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="05f1c-118">No entanto, você pode usar o esquema de URL que quiser.</span><span class="sxs-lookup"><span data-stu-id="05f1c-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="05f1c-119">Ele deve ser exclusivo tooyour aplicativo para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="05f1c-119">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="05f1c-120">redirecionamento de saudação tooenable no lado do servidor de saudação:</span><span class="sxs-lookup"><span data-stu-id="05f1c-120">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="05f1c-121">No hello [portal do Azure], selecione o serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="05f1c-121">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="05f1c-122">Clique em Olá **autenticação / autorização** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="05f1c-122">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="05f1c-123">Em Olá **permitidas URLs de redirecionamento externo**, digite `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="05f1c-123">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="05f1c-124">Olá **url_scheme_of_your_app** na cadeia de caracteres é hello esquema de URL para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="05f1c-124">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="05f1c-125">Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).</span><span class="sxs-lookup"><span data-stu-id="05f1c-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="05f1c-126">Assegure uma anotação de cadeia de caracteres de saudação que você escolha como você precisará tooadjust seu código de aplicativo móvel com hello esquema de URL em vários locais.</span><span class="sxs-lookup"><span data-stu-id="05f1c-126">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="05f1c-127">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="05f1c-127">Click **OK**.</span></span>

5. <span data-ttu-id="05f1c-128">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="05f1c-128">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="05f1c-129">Restringir permissões tooauthenticated usuários</span><span class="sxs-lookup"><span data-stu-id="05f1c-129">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a><span data-ttu-id="05f1c-130">Adicionar a biblioteca de classes portátil toohello autenticação</span><span class="sxs-lookup"><span data-stu-id="05f1c-130">Add authentication toohello portable class library</span></span>
<span data-ttu-id="05f1c-131">Aplicativos móveis usa Olá [LoginAsync] [ 3] método de extensão no hello [MobileServiceClient] [ 4] toosign um usuário com o serviço de aplicativo autenticação.</span><span class="sxs-lookup"><span data-stu-id="05f1c-131">Mobile Apps uses hello [LoginAsync][3] extension method on hello [MobileServiceClient][4] toosign in a user with App Service authentication.</span></span> <span data-ttu-id="05f1c-132">Este exemplo usa um fluxo de autenticação de servidor gerenciado que exibe a interface de entrada do provedor de saudação no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="05f1c-132">This sample uses a server-managed authentication flow that displays hello provider's sign-in interface in hello app.</span></span> <span data-ttu-id="05f1c-133">Para saber mais, veja [Autenticação gerenciada pelo servidor][5].</span><span class="sxs-lookup"><span data-stu-id="05f1c-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="05f1c-134">Para proporcionar uma melhor experiência ao usuário em seu aplicativo de produção, você deve considerar o uso da [Autenticação gerenciada pelo cliente][6].</span><span class="sxs-lookup"><span data-stu-id="05f1c-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="05f1c-135">Definir tooauthenticate com um projeto Xamarin Forms, um **IAuthenticate** interface Olá biblioteca de classes portátil para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="05f1c-135">tooauthenticate with a Xamarin Forms project, define an **IAuthenticate** interface in hello Portable Class Library for hello app.</span></span> <span data-ttu-id="05f1c-136">Em seguida, adicione um **entrar** interface de usuário do botão toohello definido em Olá a biblioteca de classes portátil, que você clicar em toostart autenticação.</span><span class="sxs-lookup"><span data-stu-id="05f1c-136">Then add a **Sign-in** button toohello user interface defined in hello Portable Class Library, which you click toostart authentication.</span></span> <span data-ttu-id="05f1c-137">Dados são carregados de back-end de aplicativo móvel Olá após a autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="05f1c-137">Data is loaded from hello mobile app backend after successful authentication.</span></span>

<span data-ttu-id="05f1c-138">Saudação de implementar **IAuthenticate** interface para cada plataforma com suporte pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="05f1c-138">Implement hello **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="05f1c-139">No Visual Studio ou Xamarin Studio, abra App.cs do projeto Olá com **portátil** em nome de saudação, que é o projeto de biblioteca de classes portátil, em seguida, adicione a seguir Olá `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="05f1c-139">In Visual Studio or Xamarin Studio, open App.cs from hello project with **Portable** in hello name, which is Portable Class Library project, then  add hello following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="05f1c-140">Em App.cs, adicione o seguinte Olá `IAuthenticate` interface definition imediatamente antes do hello `App` definição da classe.</span><span class="sxs-lookup"><span data-stu-id="05f1c-140">In App.cs, add hello following `IAuthenticate` interface definition immediately before hello `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="05f1c-141">interface de saudação tooinitialize com uma implementação específica de plataforma, adicionar Olá seguintes membros estáticos toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="05f1c-141">tooinitialize hello interface with a platform-specific implementation, add hello following static members toohello **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="05f1c-142">Abra TodoList.xaml do projeto de biblioteca de classes portátil hello, adicione o seguinte Olá **botão** elemento Olá *buttonsPanel* elemento de layout, depois de botão de saudação existente:</span><span class="sxs-lookup"><span data-stu-id="05f1c-142">Open TodoList.xaml from hello Portable Class Library project, add hello following **Button** element in hello *buttonsPanel* layout element, after hello existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="05f1c-143">Esse botão dispara a autenticação gerenciada por servidor com seu back-end de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="05f1c-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="05f1c-144">Abrir TodoList.xaml.cs do projeto de biblioteca de classes portátil hello, em seguida, adicionar Olá toohello de campo a seguir `TodoList` classe:</span><span class="sxs-lookup"><span data-stu-id="05f1c-144">Open TodoList.xaml.cs from hello Portable Class Library project, then add hello following field toohello `TodoList` class:</span></span>

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="05f1c-145">Substituir saudação **OnAppearing** método com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="05f1c-145">Replace hello **OnAppearing** method with hello following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="05f1c-146">Este código torna-se de que dados são atualizados somente do serviço Olá depois que você tenha sido autenticado.</span><span class="sxs-lookup"><span data-stu-id="05f1c-146">This code makes sure that data is only refreshed from hello service after you have been authenticated.</span></span>
7. <span data-ttu-id="05f1c-147">Adicionar Olá seguindo o manipulador de saudação **clicado** evento toohello **TodoList** classe:</span><span class="sxs-lookup"><span data-stu-id="05f1c-147">Add hello following handler for hello **Clicked** event toohello **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="05f1c-148">Salve suas alterações e recompilar o projeto de biblioteca de classes portátil Olá verificando sem erros.</span><span class="sxs-lookup"><span data-stu-id="05f1c-148">Save your changes and rebuild hello Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-toohello-android-app"></a><span data-ttu-id="05f1c-149">Adicionar aplicativo do Android autenticação toohello</span><span class="sxs-lookup"><span data-stu-id="05f1c-149">Add authentication toohello Android app</span></span>
<span data-ttu-id="05f1c-150">Esta seção mostra como Olá tooimplement **IAuthenticate** interface no projeto de aplicativo do Android hello.</span><span class="sxs-lookup"><span data-stu-id="05f1c-150">This section shows how tooimplement hello **IAuthenticate** interface in hello Android app project.</span></span> <span data-ttu-id="05f1c-151">Ignore esta seção se não estiver dando suporte a dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="05f1c-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="05f1c-152">No Visual Studio ou no Xamarin Studio, clique com botão direito Olá **droid** do projeto, em seguida, **definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="05f1c-152">In Visual Studio or Xamarin Studio, right-click hello **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="05f1c-153">Pressione F5 projeto de saudação de toostart no depurador Olá e verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada depois que o aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="05f1c-153">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="05f1c-154">código 401 Olá é produzido como o acesso em Olá back-end é somente usuários tooauthorized restrito.</span><span class="sxs-lookup"><span data-stu-id="05f1c-154">hello 401 code is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="05f1c-155">Abra MainActivity.cs no projeto Android hello e adicione o seguinte Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="05f1c-155">Open MainActivity.cs in hello Android project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="05f1c-156">Saudação de atualização **MainActivity** Olá de tooimplement classe **IAuthenticate** interface, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="05f1c-156">Update hello **MainActivity** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="05f1c-157">Saudação de atualização **MainActivity** classe adicionando um **MobileServiceUser** campo e um **autenticar** método, que é exigido pelo Olá **IAuthenticate**  interface, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="05f1c-157">Update hello **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

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

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="05f1c-158">Se você estiver usando um provedor de identidade diferente do Facebook, escolha outro valor para [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="05f1c-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="05f1c-159">Adicionar Olá seguindo o código dentro de <application> nó do AndroidManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="05f1c-159">Add hello following code inside <application> node of AndroidManifest.xml:</span></span>

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

1. <span data-ttu-id="05f1c-160">Adicionar Olá toohello de código a seguir **OnCreate** método hello **MainActivity** classe muito antes da chamada de saudação`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="05f1c-160">Add hello following code toohello **OnCreate** method of hello **MainActivity** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="05f1c-161">Este código assegura autenticador Olá é inicializada antes Olá aplicativo carrega.</span><span class="sxs-lookup"><span data-stu-id="05f1c-161">This code ensures hello authenticator is initialized before hello app loads.</span></span>
2. <span data-ttu-id="05f1c-162">Recompilar o aplicativo hello, executá-lo e entrar com o provedor de autenticação Olá escolhido e verifique se que você está tooaccess capaz de dados como um usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="05f1c-162">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toohello-ios-app"></a><span data-ttu-id="05f1c-163">Adicionar aplicativo do iOS toohello autenticação</span><span class="sxs-lookup"><span data-stu-id="05f1c-163">Add authentication toohello iOS app</span></span>
<span data-ttu-id="05f1c-164">Esta seção mostra como Olá tooimplement **IAuthenticate** interface no projeto de aplicativo do iOS hello.</span><span class="sxs-lookup"><span data-stu-id="05f1c-164">This section shows how tooimplement hello **IAuthenticate** interface in hello iOS app project.</span></span> <span data-ttu-id="05f1c-165">Ignore esta seção se não estiver dando suporte a dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="05f1c-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="05f1c-166">No Visual Studio ou no Xamarin Studio, clique com botão direito Olá **iOS** do projeto, em seguida, **definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="05f1c-166">In Visual Studio or Xamarin Studio, right-click hello **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="05f1c-167">Pressione F5 projeto de saudação de toostart no depurador hello e verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada após o início do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="05f1c-167">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="05f1c-168">respostas 401 Olá é produzido como o acesso em Olá back-end é somente usuários tooauthorized restrito.</span><span class="sxs-lookup"><span data-stu-id="05f1c-168">hello 401 response is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="05f1c-169">Abra appdelegate. cs no projeto do iOS hello e adicione o seguinte Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="05f1c-169">Open AppDelegate.cs in hello iOS project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="05f1c-170">Saudação de atualização **AppDelegate** Olá de tooimplement classe **IAuthenticate** interface, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="05f1c-170">Update hello **AppDelegate** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="05f1c-171">Saudação de atualização **AppDelegate** classe adicionando um **MobileServiceUser** campo e um **autenticar** método, que é exigido pelo Olá **IAuthenticate**  interface, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="05f1c-171">Update hello **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

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

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="05f1c-172">Se você estiver usando um provedor de identidade diferente do Facebook, escolha outro valor para [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="05f1c-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="05f1c-173">Atualizar classe de AppDelegate Olá adicionando sobrecarga do método Abrirurl (opções de NSDictionary do aplicativo, a url de NSUrl UIApplication)</span><span class="sxs-lookup"><span data-stu-id="05f1c-173">Update hello AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="05f1c-174">Adicione a seguinte linha de código toohello de saudação **FinishedLaunching** muito da chamada do método antes de saudação`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="05f1c-174">Add hello following line of code toohello **FinishedLaunching** method before hello call too`LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="05f1c-175">Este código assegura autenticador Olá é inicializada antes que o aplicativo hello é carregado.</span><span class="sxs-lookup"><span data-stu-id="05f1c-175">This code ensures hello authenticator is initialized before hello app is loaded.</span></span>

6. <span data-ttu-id="05f1c-176">Adicionar **{url_scheme_of_your_app}** tooURL esquemas no Info. plist.</span><span class="sxs-lookup"><span data-stu-id="05f1c-176">Add **{url_scheme_of_your_app}** tooURL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="05f1c-177">Recompilar o aplicativo hello, executá-lo e entrar com o provedor de autenticação Olá escolhido e verifique se que você está tooaccess capaz de dados como um usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="05f1c-177">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a><span data-ttu-id="05f1c-178">Adicionar autenticação tooWindows 10 (incluindo Phone) projetos de aplicativo</span><span class="sxs-lookup"><span data-stu-id="05f1c-178">Add authentication tooWindows 10 (including Phone) app projects</span></span>
<span data-ttu-id="05f1c-179">Esta seção mostra como Olá tooimplement **IAuthenticate** interface em projetos de aplicativo hello Windows 10.</span><span class="sxs-lookup"><span data-stu-id="05f1c-179">This section shows how tooimplement hello **IAuthenticate** interface in hello Windows 10 app projects.</span></span> <span data-ttu-id="05f1c-180">Olá mesmas etapas se aplicam para projetos do Windows UWP (plataforma Universal), mas usando Olá **UWP** projeto (com observadas alterações).</span><span class="sxs-lookup"><span data-stu-id="05f1c-180">hello same steps apply for Universal Windows Platform (UWP) projects, but using hello **UWP** project (with noted changes).</span></span> <span data-ttu-id="05f1c-181">Ignore esta seção se não estiver dando suporte a dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="05f1c-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="05f1c-182">"No Visual Studio, clique com botão direito ou Olá **UWP** do projeto, em seguida, **definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="05f1c-182">"In Visual Studio, right-click either hello **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="05f1c-183">Pressione F5 projeto de saudação de toostart no depurador hello e verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada após o início do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="05f1c-183">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="05f1c-184">respostas 401 Olá acontece porque o acesso em Olá back-end é somente para usuários restritos tooauthorized.</span><span class="sxs-lookup"><span data-stu-id="05f1c-184">hello 401 response happens because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="05f1c-185">Abra MainPage.xaml.cs para projeto de aplicativo do Windows hello e adicione o seguinte Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="05f1c-185">Open MainPage.xaml.cs for hello Windows app project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="05f1c-186">Substituir `<your_Portable_Class_Library_namespace>` com hello namespace para a biblioteca de classes portátil.</span><span class="sxs-lookup"><span data-stu-id="05f1c-186">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>
4. <span data-ttu-id="05f1c-187">Saudação de atualização **MainPage** Olá de tooimplement classe **IAuthenticate** interface, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="05f1c-187">Update hello **MainPage** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="05f1c-188">Saudação de atualização **MainPage** classe adicionando um **MobileServiceUser** campo e um **autenticar** método, que é exigido pelo Olá **IAuthenticate** interface, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="05f1c-188">Update hello **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

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

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="05f1c-189">Se você estiver usando um provedor de identidade diferente do Facebook, escolha outro valor para [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="05f1c-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="05f1c-190">Adicionar Olá a seguinte linha de código no construtor Olá Olá **MainPage** classe muito antes da chamada de saudação`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="05f1c-190">Add hello following line of code in hello constructor for hello **MainPage** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="05f1c-191">Substituir `<your_Portable_Class_Library_namespace>` com hello namespace para a biblioteca de classes portátil.</span><span class="sxs-lookup"><span data-stu-id="05f1c-191">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>

3. <span data-ttu-id="05f1c-192">Se você estiver usando **UWP**, adicione o seguinte Olá **OnActivated** método substituir toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="05f1c-192">If you are using **UWP**, add hello following **OnActivated** method override toohello **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="05f1c-193">Quando o método hello substituir já existe, adicione o código condicional Olá de saudação precede o trecho de código.</span><span class="sxs-lookup"><span data-stu-id="05f1c-193">When hello method override already exists, add hello conditional code from hello preceding snippet.</span></span>  <span data-ttu-id="05f1c-194">Esse código não é necessário para projetos Universais do Windows.</span><span class="sxs-lookup"><span data-stu-id="05f1c-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="05f1c-195">Adicionar **{url_scheme_of_your_app}** em Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="05f1c-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="05f1c-196">Recompilar o aplicativo hello, executá-lo e entrar com o provedor de autenticação Olá escolhido e verifique se que você está tooaccess capaz de dados como um usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="05f1c-196">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05f1c-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="05f1c-197">Next steps</span></span>
<span data-ttu-id="05f1c-198">Agora que você concluiu este tutorial de autenticação básica, considere a possibilidade de continuar tooone de saudação tutoriais a seguir:</span><span class="sxs-lookup"><span data-stu-id="05f1c-198">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="05f1c-199">Adicionar aplicativo de tooyour de notificações por push</span><span class="sxs-lookup"><span data-stu-id="05f1c-199">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="05f1c-200">Saiba como notificações por push de tooadd dão suporte ao aplicativo tooyour e configurar seu aplicativo móvel back-end toouse Hubs de notificação do Azure toosend as notificações por push.</span><span class="sxs-lookup"><span data-stu-id="05f1c-200">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="05f1c-201">Habilitar sincronização offline para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="05f1c-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="05f1c-202">Saiba como off-line tooadd dão suporte ao seu aplicativo usando um back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="05f1c-202">Learn how tooadd offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="05f1c-203">Sincronização offline permite toointeract de usuários finais com um aplicativo móvel - exibindo, adicionando ou modificando dados - mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="05f1c-203">Offline sync allows end users toointeract with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
