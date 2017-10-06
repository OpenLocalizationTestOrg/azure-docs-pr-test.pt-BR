---
title: "aaaGet iniciado com a autenticação para aplicativos móveis no Xamarin iOS"
description: "Saiba como os usuários tooauthenticate de aplicativos móveis toouse do aplicativo Xamarin iOS por meio de uma variedade de provedores de identidade, incluindo AAD, Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a><span data-ttu-id="2a96f-103">Adicionar autenticação tooyour xamarin aplicativo</span><span class="sxs-lookup"><span data-stu-id="2a96f-103">Add authentication tooyour Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="2a96f-104">Este tópico mostra como tooauthenticate usuários de um serviço de aplicativo móvel aplicativo do seu aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="2a96f-104">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="2a96f-105">Neste tutorial, você deve adicionar projeto de início rápido do autenticação toohello xamarin usando um provedor de identidade que é suportado pelo serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2a96f-105">In this tutorial, you add authentication toohello Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="2a96f-106">Depois com êxito que está sendo autenticado e autorizado pelo seu aplicativo móvel, o valor de ID de usuário de saudação é exibida e você será capaz de tooaccess restringido dados da tabela.</span><span class="sxs-lookup"><span data-stu-id="2a96f-106">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed and you will be able tooaccess restricted table data.</span></span>

<span data-ttu-id="2a96f-107">Você deve completar tutorial Olá [criar um aplicativo xamarin].</span><span class="sxs-lookup"><span data-stu-id="2a96f-107">You must first complete hello tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="2a96f-108">Se você não usar Olá baixar o projeto de servidor de início rápido, você deve adicionar o projeto de tooyour de pacote de extensão de autenticação hello.</span><span class="sxs-lookup"><span data-stu-id="2a96f-108">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="2a96f-109">Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="2a96f-109">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="2a96f-110">Registrar seu aplicativo para a autenticação e configurar os Serviços de Aplicativos</span><span class="sxs-lookup"><span data-stu-id="2a96f-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a><span data-ttu-id="2a96f-111">Adicionar URLs de redirecionamento externo permitidos de toohello seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="2a96f-111">Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="2a96f-112">A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2a96f-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="2a96f-113">Isso permite Olá autenticação sistema tooredirect tooyour back aplicativo após a conclusão do processo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a96f-113">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="2a96f-114">Neste tutorial, usamos o esquema de URL Olá _appname_ em todo.</span><span class="sxs-lookup"><span data-stu-id="2a96f-114">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="2a96f-115">No entanto, você pode usar o esquema de URL que quiser.</span><span class="sxs-lookup"><span data-stu-id="2a96f-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="2a96f-116">Ele deve ser exclusivo tooyour aplicativo para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="2a96f-116">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="2a96f-117">redirecionamento de saudação tooenable no lado do servidor de saudação:</span><span class="sxs-lookup"><span data-stu-id="2a96f-117">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="2a96f-118">No hello [portal do Azure], selecione o serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2a96f-118">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="2a96f-119">Clique em Olá **autenticação / autorização** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="2a96f-119">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="2a96f-120">Em Olá **permitidas URLs de redirecionamento externo**, digite `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="2a96f-120">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="2a96f-121">Olá **url_scheme_of_your_app** na cadeia de caracteres é hello esquema de URL para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="2a96f-121">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="2a96f-122">Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).</span><span class="sxs-lookup"><span data-stu-id="2a96f-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="2a96f-123">Assegure uma anotação de cadeia de caracteres de saudação que você escolha como você precisará tooadjust seu código de aplicativo móvel com hello esquema de URL em vários locais.</span><span class="sxs-lookup"><span data-stu-id="2a96f-123">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="2a96f-124">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2a96f-124">Click **OK**.</span></span>

5. <span data-ttu-id="2a96f-125">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2a96f-125">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="2a96f-126">Restringir permissões tooauthenticated usuários</span><span class="sxs-lookup"><span data-stu-id="2a96f-126">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="2a96f-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="2a96f-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="2a96f-128">No Visual Studio ou no Xamarin Studio, execute o projeto de cliente de saudação em um dispositivo ou emulador.</span><span class="sxs-lookup"><span data-stu-id="2a96f-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="2a96f-129">Verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada após o início do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2a96f-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="2a96f-130">Falha de saudação é conectado toohello console do depurador de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a96f-130">hello failure is logged toohello console of hello debugger.</span></span> <span data-ttu-id="2a96f-131">Portanto no Visual Studio, você deve ver falha Olá na janela de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="2a96f-131">So in Visual Studio, you should see hello failure in hello output window.</span></span>

<span data-ttu-id="2a96f-132">&nbsp;&nbsp;Essa falha não autorizada acontece porque o aplicativo hello tentativas tooaccess seu back-end do aplicativo móvel como um usuário não autenticado.</span><span class="sxs-lookup"><span data-stu-id="2a96f-132">&nbsp;&nbsp;This unauthorized failure happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="2a96f-133">Olá *TodoItem* tabela agora requer autenticação.</span><span class="sxs-lookup"><span data-stu-id="2a96f-133">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="2a96f-134">Em seguida, você irá atualizar recursos de toorequest de back-end de aplicativo móvel de saudação do aplicativo hello cliente com um usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="2a96f-134">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="2a96f-135">Adicionar autenticação toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="2a96f-135">Add authentication toohello app</span></span>
<span data-ttu-id="2a96f-136">Nesta seção, você modificará o hello aplicativo toodisplay uma tela de logon antes de exibir dados.</span><span class="sxs-lookup"><span data-stu-id="2a96f-136">In this section, you will modify hello app toodisplay a login screen before displaying data.</span></span> <span data-ttu-id="2a96f-137">Quando o aplicativo hello é iniciado, ele não não se conectará tooyour do serviço de aplicativo e não exibirá nenhum dado.</span><span class="sxs-lookup"><span data-stu-id="2a96f-137">When hello app starts, it will not not connect tooyour App Service and will not display any data.</span></span> <span data-ttu-id="2a96f-138">Depois de Olá primeira vez que o usuário Olá executa Olá gesto de atualização, será exibida a tela de logon do hello; Após o logon bem-sucedido hello lista de itens de tarefas será exibida.</span><span class="sxs-lookup"><span data-stu-id="2a96f-138">After hello first time that hello user performs hello refresh gesture, hello login screen will appear; after successful login hello list of todo items will be displayed.</span></span>

1. <span data-ttu-id="2a96f-139">No projeto de cliente de hello, abra o arquivo hello **QSTodoService.cs** e adicione o seguinte hello usando a instrução e `MobileServiceUser` com toohello acessador QSTodoService classe:</span><span class="sxs-lookup"><span data-stu-id="2a96f-139">In hello client project, open hello file **QSTodoService.cs** and add hello following using statement and `MobileServiceUser` with accessor toohello QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="2a96f-140">Adicionar um novo método chamado **autenticar** muito**QSTodoService** com hello definição a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a96f-140">Add new method named **Authenticate** too**QSTodoService** with hello following definition:</span></span>

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

    >[AZURE.NOTE] <span data-ttu-id="2a96f-141">Se você estiver usando um provedor de identidade que não seja um Facebook, altere o valor de saudação passado muito**LoginAsync** acima tooone seguinte Olá: _MicrosoftAccount_, _Twitter_, _Google_, ou _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="2a96f-141">If you are using an identity provider other than a Facebook, change hello value passed too**LoginAsync** above tooone of hello following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="2a96f-142">Abra o **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="2a96f-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="2a96f-143">Modificar a definição de método de saudação do **ViewDidLoad** removendo chamada hello muito**RefreshAsync()** final hello:</span><span class="sxs-lookup"><span data-stu-id="2a96f-143">Modify hello method definition of **ViewDidLoad** removing hello call too**RefreshAsync()** near hello end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="2a96f-144">Modifique o método hello **RefreshAsync** tooauthenticate se hello **usuário** propriedade é nula.</span><span class="sxs-lookup"><span data-stu-id="2a96f-144">Modify hello method **RefreshAsync** tooauthenticate if hello **User** property is null.</span></span> <span data-ttu-id="2a96f-145">Adicione Olá código na parte superior de saudação da definição de método hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a96f-145">Add hello following code at hello top of hello method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="2a96f-146">Abra **appdelegate. CS**, adicionar Olá método a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a96f-146">Open **AppDelegate.cs**, add hello following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="2a96f-147">Abra **Info. plist** de arquivos, navegue até muito**tipos de URL** em Olá **avançado** seção.</span><span class="sxs-lookup"><span data-stu-id="2a96f-147">Open **Info.plist** file, navigate too**URL Types** in hello **Advanced** section.</span></span> <span data-ttu-id="2a96f-148">Configurar Olá **identificador** e hello **esquemas de URL** de seu tipo de URL e clique em **Adicionar tipo de URL**.</span><span class="sxs-lookup"><span data-stu-id="2a96f-148">Now configure hello **Identifier** and hello **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="2a96f-149">**Esquemas de URL** devem ser Olá mesmo como {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="2a96f-149">**URL Schemes** should be hello same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="2a96f-150">No Visual Studio ou no Xamarin Studio conectado tooyour Xamarin criar Host no seu Mac, executar o projeto de cliente Olá direcionando um dispositivo ou emulador.</span><span class="sxs-lookup"><span data-stu-id="2a96f-150">In Visual Studio or Xamarin Studio connected tooyour Xamarin Build Host on your Mac, run hello client project targeting a device or emulator.</span></span> <span data-ttu-id="2a96f-151">Verifique se que o aplicativo hello não exibe nenhum dado.</span><span class="sxs-lookup"><span data-stu-id="2a96f-151">Verify that hello app displays no data.</span></span>
   
    <span data-ttu-id="2a96f-152">Execute Olá atualização gesto colocando-o para baixo na lista de saudação de itens, o que fará com que a saudação tooappear de tela de logon.</span><span class="sxs-lookup"><span data-stu-id="2a96f-152">Perform hello refresh gesture by pulling down hello list of items, which will cause hello login screen tooappear.</span></span> <span data-ttu-id="2a96f-153">Depois que você forneceu credenciais válidas, o aplicativo hello exibirá a lista de saudação de itens de tarefas, e você pode fazer toohello atualiza os dados.</span><span class="sxs-lookup"><span data-stu-id="2a96f-153">Once you have successfully entered valid credentials, hello app will display hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[criar um aplicativo xamarin]: app-service-mobile-xamarin-ios-get-started.md