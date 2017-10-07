---
title: "aaaGet iniciado com a autenticação para aplicativos móveis no Xamarin Android"
description: "Saiba como usuários de tooauthenticate toouse aplicativos móveis do seu aplicativo Xamarin Android por meio de uma variedade de provedores de identidade, incluindo AAD, Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a><span data-ttu-id="4d08d-103">Adicionar autenticação tooyour xamarin aplicativo</span><span class="sxs-lookup"><span data-stu-id="4d08d-103">Add authentication tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="4d08d-104">Este tópico mostra como tooauthenticate usuários de um aplicativo móvel do seu aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="4d08d-104">This topic shows you how tooauthenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="4d08d-105">Neste tutorial, você deve adicionar projeto de início rápido de toohello de autenticação usando um provedor de identidade que é compatível com aplicativos móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d08d-105">In this tutorial, you add authentication toohello quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="4d08d-106">Após com êxito que está sendo autenticado e autorizado no hello aplicativo móvel, o valor de ID de usuário de saudação é exibida.</span><span class="sxs-lookup"><span data-stu-id="4d08d-106">After being successfully authenticated and authorized in hello Mobile App, hello user ID value is displayed.</span></span>

<span data-ttu-id="4d08d-107">Este tutorial baseia-se no início rápido de aplicativo móvel hello.</span><span class="sxs-lookup"><span data-stu-id="4d08d-107">This tutorial is based on hello Mobile App quickstart.</span></span> <span data-ttu-id="4d08d-108">Primeiro, você deve concluir o tutorial de saudação [criar um aplicativo xamarin].</span><span class="sxs-lookup"><span data-stu-id="4d08d-108">You must also first complete hello tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="4d08d-109">Se você não usar Olá baixar o projeto de servidor de início rápido, você deve adicionar o projeto de tooyour de pacote de extensão de autenticação hello.</span><span class="sxs-lookup"><span data-stu-id="4d08d-109">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="4d08d-110">Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4d08d-110">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="4d08d-111"><a name="register"></a>Registrar seu aplicativo para autenticação e configurar os Serviços de Aplicativos</span><span class="sxs-lookup"><span data-stu-id="4d08d-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="4d08d-112"><a name="redirecturl"></a>Adicionar URLs de redirecionamento externo permitidos de toohello seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="4d08d-112"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="4d08d-113">A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4d08d-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="4d08d-114">Isso permite Olá autenticação sistema tooredirect tooyour back aplicativo após a conclusão do processo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d08d-114">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="4d08d-115">Neste tutorial, usamos o esquema de URL Olá _appname_ em todo.</span><span class="sxs-lookup"><span data-stu-id="4d08d-115">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="4d08d-116">No entanto, você pode usar o esquema de URL que quiser.</span><span class="sxs-lookup"><span data-stu-id="4d08d-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="4d08d-117">Ele deve ser exclusivo tooyour aplicativo para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="4d08d-117">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="4d08d-118">redirecionamento de saudação tooenable no lado do servidor de saudação:</span><span class="sxs-lookup"><span data-stu-id="4d08d-118">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="4d08d-119">No hello [portal do Azure], selecione o serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4d08d-119">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="4d08d-120">Clique em Olá **autenticação / autorização** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="4d08d-120">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="4d08d-121">Em Olá **permitidas URLs de redirecionamento externo**, digite `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="4d08d-121">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="4d08d-122">Olá **url_scheme_of_your_app** na cadeia de caracteres é hello esquema de URL para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="4d08d-122">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="4d08d-123">Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).</span><span class="sxs-lookup"><span data-stu-id="4d08d-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="4d08d-124">Assegure uma anotação de cadeia de caracteres de saudação que você escolha como você precisará tooadjust seu código de aplicativo móvel com hello esquema de URL em vários locais.</span><span class="sxs-lookup"><span data-stu-id="4d08d-124">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="4d08d-125">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d08d-125">Click **OK**.</span></span>

5. <span data-ttu-id="4d08d-126">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4d08d-126">Click **Save**.</span></span>

## <span data-ttu-id="4d08d-127"><a name="permissions"></a>Restringir permissões tooauthenticated usuários</span><span class="sxs-lookup"><span data-stu-id="4d08d-127"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="4d08d-128">No Visual Studio ou no Xamarin Studio, execute o projeto de cliente de saudação em um dispositivo ou emulador.</span><span class="sxs-lookup"><span data-stu-id="4d08d-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="4d08d-129">Verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada após o início do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="4d08d-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="4d08d-130">Isso acontece porque o aplicativo hello tentativas tooaccess seu back-end do aplicativo móvel como um usuário não autenticado.</span><span class="sxs-lookup"><span data-stu-id="4d08d-130">This happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="4d08d-131">Olá *TodoItem* tabela agora requer autenticação.</span><span class="sxs-lookup"><span data-stu-id="4d08d-131">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="4d08d-132">Em seguida, você irá atualizar recursos de toorequest de back-end de aplicativo móvel de saudação do aplicativo hello cliente com um usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="4d08d-132">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="4d08d-133"><a name="add-authentication"></a>Adicionar autenticação toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="4d08d-133"><a name="add-authentication"></a>Add authentication toohello app</span></span>
<span data-ttu-id="4d08d-134">aplicativo Hello é saudação do toorequire atualizado os usuários tootap **entrar** botão e autenticar antes que os dados são exibidos.</span><span class="sxs-lookup"><span data-stu-id="4d08d-134">hello app is updated toorequire users tootap hello **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="4d08d-135">Adicionar Olá toohello de código a seguir **TodoActivity** classe:</span><span class="sxs-lookup"><span data-stu-id="4d08d-135">Add hello following code toohello **TodoActivity** class:</span></span>
   
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
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="4d08d-136">Isso cria um novo tooauthenticate de método de um usuário e um manipulador de método para um novo **entrar** botão.</span><span class="sxs-lookup"><span data-stu-id="4d08d-136">This creates a new method tooauthenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="4d08d-137">usuário Olá no código de exemplo hello acima é autenticado usando um logon do Facebook.</span><span class="sxs-lookup"><span data-stu-id="4d08d-137">hello user in hello example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="4d08d-138">Uma caixa de diálogo é a ID de usuário de saudação toodisplay usado uma vez autenticado.</span><span class="sxs-lookup"><span data-stu-id="4d08d-138">A dialog is used toodisplay hello user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4d08d-139">Se você estiver usando um provedor de identidade diferente do Facebook, altere o valor de saudação passado muito**LoginAsync** acima tooone seguinte Olá: *MicrosoftAccount*, *Twitter*, *Google*, ou *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="4d08d-139">If you are using an identity provider other than Facebook, change hello value passed too**LoginAsync** above tooone of hello following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="4d08d-140">Em Olá **OnCreate** método, excluir ou Olá comentários de linha de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d08d-140">In hello **OnCreate** method, delete or comment-out hello following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="4d08d-141">No arquivo de Activity_To_Do.axml de saudação, adicione o seguinte Olá *LoginUser* botão definição antes Olá existente *AddItem* botão:</span><span class="sxs-lookup"><span data-stu-id="4d08d-141">In hello Activity_To_Do.axml file, add hello following *LoginUser* button definition before hello existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="4d08d-142">Adicione Olá arquivo de recursos do elemento toohello Strings.xml a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d08d-142">Add hello following element toohello Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="4d08d-143">Abrir o arquivo de AndroidManifest.xml hello, adicione Olá seguindo o código dentro de `<application>` elemento XML:</span><span class="sxs-lookup"><span data-stu-id="4d08d-143">Open hello AndroidManifest.xml file, add hello following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="4d08d-144">No Visual Studio ou no Xamarin Studio, execute o projeto de saudação do cliente em um dispositivo ou emulador e entrar com seu provedor de identidade escolhido.</span><span class="sxs-lookup"><span data-stu-id="4d08d-144">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="4d08d-145">Quando você está conectado com êxito, aplicativo hello exibirá sua ID de logon e lista de saudação de itens de tarefas e você pode fazer atualizações toohello dados.</span><span class="sxs-lookup"><span data-stu-id="4d08d-145">When you are successfully logged-in, hello app will display your login ID and hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[criar um aplicativo xamarin]: app-service-mobile-xamarin-android-get-started.md