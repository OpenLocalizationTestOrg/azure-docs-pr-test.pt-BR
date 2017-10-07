---
title: aplicativo de Windows UWP (plataforma Universal) aaaAdd authentication tooyour | Microsoft Docs
description: "Saiba como usuários de tooauthenticate toouse aplicativos de celular do serviço de aplicativo do Azure do aplicativo Windows UWP (plataforma Universal) usando uma variedade de provedores de identidade, incluindo: AAD, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a><span data-ttu-id="bf1a3-103">Adicionar aplicativo do Windows tooyour autenticação</span><span class="sxs-lookup"><span data-stu-id="bf1a3-103">Add authentication tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="bf1a3-104">Este tópico mostra como aplicativo móvel do tooyour tooadd autenticação baseada em nuvem.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-104">This topic shows you how tooadd cloud-based authentication tooyour mobile app.</span></span> <span data-ttu-id="bf1a3-105">Neste tutorial, você pode adicionar projeto de início rápido do autenticação toohello Windows UWP (plataforma Universal) para aplicativos móveis usando um provedor de identidade que é suportado pelo serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-105">In this tutorial, you add authentication toohello Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="bf1a3-106">Após com êxito que está sendo autenticado e autorizado pelo seu back-end do aplicativo móvel, o valor de ID de usuário de saudação é exibida.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-106">After being successfully authenticated and authorized by your Mobile App backend, hello user ID value is displayed.</span></span>

<span data-ttu-id="bf1a3-107">Este tutorial baseia-se no início rápido de aplicativos móveis hello.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-107">This tutorial is based on hello Mobile Apps quickstart.</span></span> <span data-ttu-id="bf1a3-108">Você deve completar tutorial Olá [começar com aplicativos móveis](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bf1a3-108">You must first complete hello tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="bf1a3-109"><a name="register"></a>Registrar seu aplicativo para autenticação e configurar saudação do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="bf1a3-109"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="bf1a3-110"><a name="redirecturl"></a>Adicionar URLs de redirecionamento externo permitidos de toohello seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="bf1a3-110"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="bf1a3-111">A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="bf1a3-112">Isso permite Olá autenticação sistema tooredirect tooyour back aplicativo após a conclusão do processo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-112">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="bf1a3-113">Neste tutorial, usamos o esquema de URL Olá _appname_ em todo.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-113">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="bf1a3-114">No entanto, você pode usar o esquema de URL que quiser.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="bf1a3-115">Ele deve ser exclusivo tooyour aplicativo para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-115">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="bf1a3-116">redirecionamento de saudação tooenable no lado do servidor de saudação:</span><span class="sxs-lookup"><span data-stu-id="bf1a3-116">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="bf1a3-117">No hello [portal do Azure], selecione o serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-117">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="bf1a3-118">Clique em Olá **autenticação / autorização** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-118">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="bf1a3-119">Em Olá **permitidas URLs de redirecionamento externo**, digite `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-119">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="bf1a3-120">Olá **url_scheme_of_your_app** na cadeia de caracteres é hello esquema de URL para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-120">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="bf1a3-121">Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).</span><span class="sxs-lookup"><span data-stu-id="bf1a3-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="bf1a3-122">Assegure uma anotação de cadeia de caracteres de saudação que você escolha como você precisará tooadjust seu código de aplicativo móvel com hello esquema de URL em vários locais.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-122">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="bf1a3-123">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-123">Click **OK**.</span></span>

5. <span data-ttu-id="bf1a3-124">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-124">Click **Save**.</span></span>

## <span data-ttu-id="bf1a3-125"><a name="permissions"></a>Restringir permissões tooauthenticated usuários</span><span class="sxs-lookup"><span data-stu-id="bf1a3-125"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="bf1a3-126">Agora, você pode verificar que essa back-end do acesso anônimo tooyour foi desabilitada.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-126">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="bf1a3-127">Com o projeto de aplicativo UWP Olá definir como projeto de inicialização hello, implantar e executar o aplicativo hello; Verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada após o início do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-127">With hello UWP app project set as hello start-up project, deploy and run hello app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="bf1a3-128">Isso ocorre porque o aplicativo hello tentativas tooaccess seu código de aplicativo móvel como um usuário não autenticado, mas Olá *TodoItem* tabela agora requer autenticação.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-128">This happens because hello app attempts tooaccess your Mobile App Code as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="bf1a3-129">Em seguida, você atualizará os usuários tooauthenticate de aplicativo hello antes de solicitar recursos do seu serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-129">Next, you will update hello app tooauthenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="bf1a3-130"><a name="add-authentication"></a>Adicionar autenticação toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="bf1a3-130"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="bf1a3-131">No projeto de aplicativo UWP Olá arquivo MainPage.xaml.cs e adicione Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf1a3-131">In hello UWP app project file MainPage.xaml.cs and add hello following code snippet:</span></span>
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    <span data-ttu-id="bf1a3-132">Esse código autentica o usuário Olá com um logon do Facebook.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-132">This code authenticates hello user with a Facebook login.</span></span> <span data-ttu-id="bf1a3-133">Se você estiver usando um provedor de identidade diferente do Facebook, altere o valor de saudação do **MobileServiceAuthenticationProvider** acima toohello por seu provedor.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-133">If you are using an identity provider other than Facebook, change hello value of **MobileServiceAuthenticationProvider** above toohello value for your provider.</span></span>
2. <span data-ttu-id="bf1a3-134">Substituir saudação **OnNavigatedTo** método em MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-134">Replace hello **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="bf1a3-135">Em seguida, você adicionará um **entrar** botão toohello aplicativo que dispara a autenticação.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-135">Next, you will add a **Sign in** button toohello app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="bf1a3-136">Adicione Olá toohello de trecho de código MainPage.xaml.cs a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf1a3-136">Add hello following code snippet toohello MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="bf1a3-137">Abrir o arquivo de projeto do hello MainPage. XAML, localize o elemento de saudação que define Olá **salvar** botão e substituí-lo com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf1a3-137">Open hello MainPage.xaml project file, locate hello element that defines hello **Save** button and replace it with hello following code:</span></span>
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. <span data-ttu-id="bf1a3-138">Adicione Olá toohello de trecho de código App.xaml.cs a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf1a3-138">Add hello following code snippet toohello App.xaml.cs:</span></span>

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. <span data-ttu-id="bf1a3-139">Abra o arquivo Package. appxmanifest, navegue muito**declarações**, na **Available Declarations** lista suspensa, selecione **protocolo** e clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-139">Open Package.appxmanifest file, navigate too**Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="bf1a3-140">Configurar Olá **propriedades** de saudação **protocolo** declaração.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-140">Now configure hello **Properties** of hello **Protocol** declaration.</span></span> <span data-ttu-id="bf1a3-141">Em **nome de exibição**, adicionar nome hello desejar toousers toodisplay do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-141">In **Display name**, add hello name you wish toodisplay toousers of your application.</span></span> <span data-ttu-id="bf1a3-142">Em **Nome**, adicione o {esquema_de_URL_do_seu_aplicativo}.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="bf1a3-143">Pressione Olá F5 toorun chave Olá aplicativo, clique em Olá **entrar** botão e o logon no aplicativo hello com seu provedor de identidade escolhido.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-143">Press hello F5 key toorun hello app, click hello **Sign in** button, and sign into hello app with your chosen identity provider.</span></span> <span data-ttu-id="bf1a3-144">Depois que a entrada for bem-sucedida, Olá aplicativo é executado sem erros e você é capaz de tooquery seu back-end e fazer atualizações toodata.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-144">After your sign-in is successful, hello app runs without errors and you are able tooquery your backend and make updates toodata.</span></span>

## <span data-ttu-id="bf1a3-145"><a name="tokens"></a>Token de autenticação do repositório Olá no cliente Olá</span><span class="sxs-lookup"><span data-stu-id="bf1a3-145"><a name="tokens"></a>Store hello authentication token on hello client</span></span>
<span data-ttu-id="bf1a3-146">exemplo anterior Hello mostrou uma padrão entrar, que exige Olá cliente toocontact ambos provedor de identidade hello e Olá do serviço de aplicativo sempre que o aplicativo hello for iniciado.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-146">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello App Service every time that hello app starts.</span></span> <span data-ttu-id="bf1a3-147">Não é apenas esse método ineficiente, você pode executar em uso-se relaciona problemas muitos clientes tente toostart seu aplicativo no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try toostart you app at hello same time.</span></span> <span data-ttu-id="bf1a3-148">Uma abordagem melhor é o token de autorização de saudação toocache retornado por seu serviço de aplicativo e tente toouse isso antes de usar um provedor com base em entrar.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-148">A better approach is toocache hello authorization token returned by your App Service and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="bf1a3-149">Você pode armazenar em cache token Olá emitido por serviços de aplicativos, independentemente de se você estiver usando autenticação de cliente gerenciado ou o serviço gerenciado.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-149">You can cache hello token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="bf1a3-150">Este tutorial usa a autenticação gerenciada pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="bf1a3-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf1a3-151">Next steps</span></span>
<span data-ttu-id="bf1a3-152">Agora que você concluiu este tutorial de autenticação básica, considere a possibilidade de continuar tooone de saudação tutoriais a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf1a3-152">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="bf1a3-153">Adicionar aplicativo de tooyour de notificações por push</span><span class="sxs-lookup"><span data-stu-id="bf1a3-153">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="bf1a3-154">Saiba como notificações por push de tooadd dão suporte ao aplicativo tooyour e configurar seu aplicativo móvel back-end toouse Hubs de notificação do Azure toosend as notificações por push.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-154">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="bf1a3-155">Habilitar sincronização offline para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="bf1a3-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="bf1a3-156">Saiba como off-line tooadd dão suporte ao seu aplicativo usar um back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-156">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="bf1a3-157">Sincronização offline permite que os usuários finais toointeract com um aplicativo móvel&mdash;exibindo, adicionando ou modificando dados&mdash;mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="bf1a3-157">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
