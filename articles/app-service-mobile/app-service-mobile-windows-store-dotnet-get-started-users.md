---
title: "Adicionar autenticação ao seu aplicativo da UWP (Plataforma Universal do Windows) | Microsoft Docs"
description: "Aprenda a usar os aplicativos móveis do Serviço de Aplicativos do Azure para autenticar usuários de seu aplicativo da UWP (Plataforma Universal do Windows) usando uma variedade de provedores de identidade, incluindo: AAD, Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: 47da343d4ec956ec2e669757f56e853675f887a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-windows-app"></a><span data-ttu-id="b880a-103">Adicionar autenticação ao seu aplicativo do Windows</span><span class="sxs-lookup"><span data-stu-id="b880a-103">Add authentication to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="b880a-104">Este tópico mostra como adicionar autenticação baseada em nuvem ao seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="b880a-104">This topic shows you how to add cloud-based authentication to your mobile app.</span></span> <span data-ttu-id="b880a-105">Neste tutorial, você aprenderá a adicionar autenticação ao projeto de início rápido da UWP (Plataforma Universal do Windows) para aplicativos móveis usando um provedor de identidade com suporte no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="b880a-105">In this tutorial, you add authentication to the Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="b880a-106">Após ser autenticado e autorizado com sucesso pelo back-end do Aplicativo Móvel, o valor da ID de usuário é exibido.</span><span class="sxs-lookup"><span data-stu-id="b880a-106">After being successfully authenticated and authorized by your Mobile App backend, the user ID value is displayed.</span></span>

<span data-ttu-id="b880a-107">Este tutorial baseia-se no início rápido dos Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="b880a-107">This tutorial is based on the Mobile Apps quickstart.</span></span> <span data-ttu-id="b880a-108">Você deve primeiro concluir o tutorial [Introdução aos Aplicativos Móveis](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b880a-108">You must first complete the tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="b880a-109"><a name="register"></a>Registrar seu aplicativo para autenticação e configurar o Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="b880a-109"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="b880a-110"><a name="redirecturl"></a>Adicionar seu aplicativo às URLs de redirecionamento externo permitidas</span><span class="sxs-lookup"><span data-stu-id="b880a-110"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="b880a-111">A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b880a-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="b880a-112">Isso permite que o sistema de autenticação redirecione para seu aplicativo após a conclusão do processo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="b880a-112">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="b880a-113">Neste tutorial, usamos sempre o esquema de URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="b880a-113">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="b880a-114">No entanto, você pode usar o esquema de URL que quiser.</span><span class="sxs-lookup"><span data-stu-id="b880a-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="b880a-115">Ele deve ser exclusivo para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="b880a-115">It should be unique to your mobile application.</span></span> <span data-ttu-id="b880a-116">Para habilitar o redirecionamento no lado do servidor:</span><span class="sxs-lookup"><span data-stu-id="b880a-116">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="b880a-117">No [Portal do Azure], selecione seu Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b880a-117">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="b880a-118">Clique na opção de menu **Autenticação/Autorização**.</span><span class="sxs-lookup"><span data-stu-id="b880a-118">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="b880a-119">Em **URLs de Redirecionamento Externo Permitidas**, insira `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="b880a-119">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="b880a-120">O **esquema_de_URL_do_seu_aplicativo** nessa cadeia de caracteres é o esquema de URL do seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="b880a-120">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="b880a-121">Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).</span><span class="sxs-lookup"><span data-stu-id="b880a-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="b880a-122">Você deve anotar a cadeia de caracteres escolhida, já que precisará ajustar o código do aplicativo móvel com o esquema de URL em vários lugares.</span><span class="sxs-lookup"><span data-stu-id="b880a-122">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="b880a-123">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b880a-123">Click **OK**.</span></span>

5. <span data-ttu-id="b880a-124">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b880a-124">Click **Save**.</span></span>

## <span data-ttu-id="b880a-125"><a name="permissions"></a>Restringir permissões a usuários autenticados</span><span class="sxs-lookup"><span data-stu-id="b880a-125"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="b880a-126">Agora, é possível verificar se o acesso anônimo para o back-end foi desabilitado.</span><span class="sxs-lookup"><span data-stu-id="b880a-126">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="b880a-127">Com o projeto de aplicativo da UWP configurado como projeto de inicialização, implante e execute o aplicativo; verifique se uma exceção sem tratamento com um código de status 401 (não autorizado) é gerada depois que o aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="b880a-127">With the UWP app project set as the start-up project, deploy and run the app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="b880a-128">Isso acontece porque o aplicativo tenta acessar o código do aplicativo móvel como um usuário não autenticado, mas a tabela *TodoItem* agora exige autenticação.</span><span class="sxs-lookup"><span data-stu-id="b880a-128">This happens because the app attempts to access your Mobile App Code as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="b880a-129">Em seguida, você atualizará o aplicativo para autenticar usuários antes de solicitar recursos do seu Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b880a-129">Next, you will update the app to authenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="b880a-130"><a name="add-authentication"></a>Adicionar autenticação ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="b880a-130"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="b880a-131">No arquivo de projeto de aplicativo da UWP MainPage.xaml.cs, adicione o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="b880a-131">In the UWP app project file MainPage.xaml.cs and add the following code snippet:</span></span>
   
        // Define a member variable for storing the signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs the authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' to the name of your MobileServiceClient instance.
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
   
    <span data-ttu-id="b880a-132">Esse código autentica o usuário com um logon do Facebook.</span><span class="sxs-lookup"><span data-stu-id="b880a-132">This code authenticates the user with a Facebook login.</span></span> <span data-ttu-id="b880a-133">Se você estiver usando um provedor de identidade além do Facebook, altere o valor **MobileServiceAuthenticationProvider** acima para o valor de seu provedor.</span><span class="sxs-lookup"><span data-stu-id="b880a-133">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span></span>
2. <span data-ttu-id="b880a-134">Substitua o método **OnNavigatedTo** em MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="b880a-134">Replace the **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="b880a-135">Em seguida, você adicionará um botão **Entrar** ao aplicativo que dispara a autenticação.</span><span class="sxs-lookup"><span data-stu-id="b880a-135">Next, you will add a **Sign in** button to the app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="b880a-136">Adicione o seguinte trecho de código à classe MainPage.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="b880a-136">Add the following code snippet to the MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login the user and then load data from the mobile app.
            if (await AuthenticateAsync())
            {
                // Switch the buttons and load items from the mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="b880a-137">Abra o arquivo de projeto MainPage.xaml, localize o elemento que define o botão **Salvar** e substitua-o pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="b880a-137">Open the MainPage.xaml project file, locate the element that defines the **Save** button and replace it with the following code:</span></span>
   
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
5. <span data-ttu-id="b880a-138">Adicione o seguinte trecho de código ao App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="b880a-138">Add the following code snippet to the App.xaml.cs:</span></span>

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
6. <span data-ttu-id="b880a-139">Abra o arquivo Package.appxmanifest, navegue até **Declarações**, na lista suspensa **Declarações Disponíveis**, selecione **Protocolo** e clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b880a-139">Open Package.appxmanifest file, navigate to **Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="b880a-140">Agora, configure as **Propriedades** da declaração do **Protocolo**.</span><span class="sxs-lookup"><span data-stu-id="b880a-140">Now configure the **Properties** of the **Protocol** declaration.</span></span> <span data-ttu-id="b880a-141">Em **Nome de exibição**, adicione o nome que você deseja exibir aos usuários do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b880a-141">In **Display name**, add the name you wish to display to users of your application.</span></span> <span data-ttu-id="b880a-142">Em **Nome**, adicione o {esquema_de_URL_do_seu_aplicativo}.</span><span class="sxs-lookup"><span data-stu-id="b880a-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="b880a-143">Pressione a tecla F5 para executar o aplicativo, clique no botão **Entrar** e entre no aplicativo com o provedor de identidade escolhido.</span><span class="sxs-lookup"><span data-stu-id="b880a-143">Press the F5 key to run the app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span></span> <span data-ttu-id="b880a-144">Depois que o seu logon for bem-sucedido, o aplicativo será executado sem erros, e você poderá consultar o seu back-end e fazer atualizações nos dados.</span><span class="sxs-lookup"><span data-stu-id="b880a-144">After your sign-in is successful, the app runs without errors and you are able to query your backend and make updates to data.</span></span>

## <span data-ttu-id="b880a-145"><a name="tokens"></a>Armazenar o token de autenticação no cliente</span><span class="sxs-lookup"><span data-stu-id="b880a-145"><a name="tokens"></a>Store the authentication token on the client</span></span>
<span data-ttu-id="b880a-146">O exemplo anterior mostrou uma entrada padrão, que requer que o cliente contate o provedor de identidade e o Serviço de Aplicativo sempre que o aplicativo for iniciado.</span><span class="sxs-lookup"><span data-stu-id="b880a-146">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the App Service every time that the app starts.</span></span> <span data-ttu-id="b880a-147">Além de esse método ser ineficiente, você pode se deparar com problemas relacionados ao uso caso muitos consumidores tentem iniciar o aplicativo ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="b880a-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try to start you app at the same time.</span></span> <span data-ttu-id="b880a-148">Uma abordagem melhor é armazenar em cache o token de autorização retornado pelo Serviço de Aplicativo e tentar usá-lo antes de usar um logon baseado em provedor.</span><span class="sxs-lookup"><span data-stu-id="b880a-148">A better approach is to cache the authorization token returned by your App Service and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="b880a-149">Você pode armazenar em cache o token emitido pelos Serviços de Aplicativos usando tanto a autenticação gerenciada pelo cliente quanto a autenticação gerenciada pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="b880a-149">You can cache the token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="b880a-150">Este tutorial usa a autenticação gerenciada pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="b880a-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="b880a-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b880a-151">Next steps</span></span>
<span data-ttu-id="b880a-152">Agora que você concluiu este tutorial de autenticação básica, considere continuar com um dos seguintes tutoriais:</span><span class="sxs-lookup"><span data-stu-id="b880a-152">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="b880a-153">Adicionar notificações por push ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="b880a-153">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="b880a-154">Saiba como adicionar suporte a notificações por push ao aplicativo e configurar o back-end do Aplicativo Móvel para usar os Hubs de Notificação do Azure para enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="b880a-154">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="b880a-155">Habilitar sincronização offline para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b880a-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="b880a-156">Saiba como adicionar suporte offline ao seu aplicativo usando um back-end de Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="b880a-156">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="b880a-157">Sincronização offline permite que os usuários finais interajam com um aplicativo móvel, &mdash;exibindo, adicionando ou modificando dados&mdash;, mesmo quando não há conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="b880a-157">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
