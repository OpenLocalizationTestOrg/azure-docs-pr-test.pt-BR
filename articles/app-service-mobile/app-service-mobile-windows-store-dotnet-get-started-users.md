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
# <a name="add-authentication-tooyour-windows-app"></a>Adicionar aplicativo do Windows tooyour autenticação
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Este tópico mostra como aplicativo móvel do tooyour tooadd autenticação baseada em nuvem. Neste tutorial, você pode adicionar projeto de início rápido do autenticação toohello Windows UWP (plataforma Universal) para aplicativos móveis usando um provedor de identidade que é suportado pelo serviço de aplicativo do Azure. Após com êxito que está sendo autenticado e autorizado pelo seu back-end do aplicativo móvel, o valor de ID de usuário de saudação é exibida.

Este tutorial baseia-se no início rápido de aplicativos móveis hello. Você deve completar tutorial Olá [começar com aplicativos móveis](app-service-mobile-windows-store-dotnet-get-started.md).

## <a name="register"></a>Registrar seu aplicativo para autenticação e configurar saudação do serviço de aplicativo
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Adicionar URLs de redirecionamento externo permitidos de toohello seu aplicativo

A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo. Isso permite Olá autenticação sistema tooredirect tooyour back aplicativo após a conclusão do processo de autenticação de saudação. Neste tutorial, usamos o esquema de URL Olá _appname_ em todo. No entanto, você pode usar o esquema de URL que quiser. Ele deve ser exclusivo tooyour aplicativo para dispositivos móveis. redirecionamento de saudação tooenable no lado do servidor de saudação:

1. No hello [portal do Azure], selecione o serviço de aplicativo.

2. Clique em Olá **autenticação / autorização** opção de menu.

3. Em Olá **permitidas URLs de redirecionamento externo**, digite `url_scheme_of_your_app://easyauth.callback`.  Olá **url_scheme_of_your_app** na cadeia de caracteres é hello esquema de URL para seu aplicativo móvel.  Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).  Assegure uma anotação de cadeia de caracteres de saudação que você escolha como você precisará tooadjust seu código de aplicativo móvel com hello esquema de URL em vários locais.

4. Clique em **OK**.

5. Clique em **Salvar**.

## <a name="permissions"></a>Restringir permissões tooauthenticated usuários
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Agora, você pode verificar que essa back-end do acesso anônimo tooyour foi desabilitada. Com o projeto de aplicativo UWP Olá definir como projeto de inicialização hello, implantar e executar o aplicativo hello; Verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada após o início do aplicativo hello. Isso ocorre porque o aplicativo hello tentativas tooaccess seu código de aplicativo móvel como um usuário não autenticado, mas Olá *TodoItem* tabela agora requer autenticação.

Em seguida, você atualizará os usuários tooauthenticate de aplicativo hello antes de solicitar recursos do seu serviço de aplicativo.

## <a name="add-authentication"></a>Adicionar autenticação toohello aplicativo
1. No projeto de aplicativo UWP Olá arquivo MainPage.xaml.cs e adicione Olá trecho de código a seguir:
   
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
   
    Esse código autentica o usuário Olá com um logon do Facebook. Se você estiver usando um provedor de identidade diferente do Facebook, altere o valor de saudação do **MobileServiceAuthenticationProvider** acima toohello por seu provedor.
2. Substituir saudação **OnNavigatedTo** método em MainPage.xaml.cs. Em seguida, você adicionará um **entrar** botão toohello aplicativo que dispara a autenticação.

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. Adicione Olá toohello de trecho de código MainPage.xaml.cs a seguir:
   
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
4. Abrir o arquivo de projeto do hello MainPage. XAML, localize o elemento de saudação que define Olá **salvar** botão e substituí-lo com hello código a seguir:
   
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
5. Adicione Olá toohello de trecho de código App.xaml.cs a seguir:

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
6. Abra o arquivo Package. appxmanifest, navegue muito**declarações**, na **Available Declarations** lista suspensa, selecione **protocolo** e clique em **adicionar** botão. Configurar Olá **propriedades** de saudação **protocolo** declaração. Em **nome de exibição**, adicionar nome hello desejar toousers toodisplay do seu aplicativo. Em **Nome**, adicione o {esquema_de_URL_do_seu_aplicativo}.
7. Pressione Olá F5 toorun chave Olá aplicativo, clique em Olá **entrar** botão e o logon no aplicativo hello com seu provedor de identidade escolhido. Depois que a entrada for bem-sucedida, Olá aplicativo é executado sem erros e você é capaz de tooquery seu back-end e fazer atualizações toodata.

## <a name="tokens"></a>Token de autenticação do repositório Olá no cliente Olá
exemplo anterior Hello mostrou uma padrão entrar, que exige Olá cliente toocontact ambos provedor de identidade hello e Olá do serviço de aplicativo sempre que o aplicativo hello for iniciado. Não é apenas esse método ineficiente, você pode executar em uso-se relaciona problemas muitos clientes tente toostart seu aplicativo no hello simultaneamente. Uma abordagem melhor é o token de autorização de saudação toocache retornado por seu serviço de aplicativo e tente toouse isso antes de usar um provedor com base em entrar.

> [!NOTE]
> Você pode armazenar em cache token Olá emitido por serviços de aplicativos, independentemente de se você estiver usando autenticação de cliente gerenciado ou o serviço gerenciado. Este tutorial usa a autenticação gerenciada pelo serviço.
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Próximas etapas
Agora que você concluiu este tutorial de autenticação básica, considere a possibilidade de continuar tooone de saudação tutoriais a seguir:

* [Adicionar aplicativo de tooyour de notificações por push](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Saiba como notificações por push de tooadd dão suporte ao aplicativo tooyour e configurar seu aplicativo móvel back-end toouse Hubs de notificação do Azure toosend as notificações por push.
* [Habilitar sincronização offline para seu aplicativo](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Saiba como off-line tooadd dão suporte ao seu aplicativo usar um back-end do aplicativo móvel. Sincronização offline permite que os usuários finais toointeract com um aplicativo móvel&mdash;exibindo, adicionando ou modificando dados&mdash;mesmo quando não há nenhuma conexão de rede.

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
