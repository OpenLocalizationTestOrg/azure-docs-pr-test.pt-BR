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
# <a name="add-authentication-tooyour-xamarinios-app"></a>Adicionar autenticação tooyour xamarin aplicativo
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Este tópico mostra como tooauthenticate usuários de um serviço de aplicativo móvel aplicativo do seu aplicativo cliente. Neste tutorial, você deve adicionar projeto de início rápido do autenticação toohello xamarin usando um provedor de identidade que é suportado pelo serviço de aplicativo. Depois com êxito que está sendo autenticado e autorizado pelo seu aplicativo móvel, o valor de ID de usuário de saudação é exibida e você será capaz de tooaccess restringido dados da tabela.

Você deve completar tutorial Olá [criar um aplicativo xamarin]. Se você não usar Olá baixar o projeto de servidor de início rápido, você deve adicionar o projeto de tooyour de pacote de extensão de autenticação hello. Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Registrar seu aplicativo para a autenticação e configurar os Serviços de Aplicativos
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a>Adicionar URLs de redirecionamento externo permitidos de toohello seu aplicativo

A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo. Isso permite Olá autenticação sistema tooredirect tooyour back aplicativo após a conclusão do processo de autenticação de saudação. Neste tutorial, usamos o esquema de URL Olá _appname_ em todo. No entanto, você pode usar o esquema de URL que quiser. Ele deve ser exclusivo tooyour aplicativo para dispositivos móveis. redirecionamento de saudação tooenable no lado do servidor de saudação:

1. No hello [portal do Azure], selecione o serviço de aplicativo.

2. Clique em Olá **autenticação / autorização** opção de menu.

3. Em Olá **permitidas URLs de redirecionamento externo**, digite `url_scheme_of_your_app://easyauth.callback`.  Olá **url_scheme_of_your_app** na cadeia de caracteres é hello esquema de URL para seu aplicativo móvel.  Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).  Assegure uma anotação de cadeia de caracteres de saudação que você escolha como você precisará tooadjust seu código de aplicativo móvel com hello esquema de URL em vários locais.

4. Clique em **OK**.

5. Clique em **Salvar**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Restringir permissões tooauthenticated usuários
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

&nbsp;&nbsp;4. No Visual Studio ou no Xamarin Studio, execute o projeto de cliente de saudação em um dispositivo ou emulador. Verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada após o início do aplicativo hello. Falha de saudação é conectado toohello console do depurador de saudação. Portanto no Visual Studio, você deve ver falha Olá na janela de saída de hello.

&nbsp;&nbsp;Essa falha não autorizada acontece porque o aplicativo hello tentativas tooaccess seu back-end do aplicativo móvel como um usuário não autenticado. Olá *TodoItem* tabela agora requer autenticação.

Em seguida, você irá atualizar recursos de toorequest de back-end de aplicativo móvel de saudação do aplicativo hello cliente com um usuário autenticado.

## <a name="add-authentication-toohello-app"></a>Adicionar autenticação toohello aplicativo
Nesta seção, você modificará o hello aplicativo toodisplay uma tela de logon antes de exibir dados. Quando o aplicativo hello é iniciado, ele não não se conectará tooyour do serviço de aplicativo e não exibirá nenhum dado. Depois de Olá primeira vez que o usuário Olá executa Olá gesto de atualização, será exibida a tela de logon do hello; Após o logon bem-sucedido hello lista de itens de tarefas será exibida.

1. No projeto de cliente de hello, abra o arquivo hello **QSTodoService.cs** e adicione o seguinte hello usando a instrução e `MobileServiceUser` com toohello acessador QSTodoService classe:
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. Adicionar um novo método chamado **autenticar** muito**QSTodoService** com hello definição a seguir:

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

    >[AZURE.NOTE] Se você estiver usando um provedor de identidade que não seja um Facebook, altere o valor de saudação passado muito**LoginAsync** acima tooone seguinte Olá: _MicrosoftAccount_, _Twitter_, _Google_, ou _WindowsAzureActiveDirectory_.

3. Abra o **QSTodoListViewController.cs**. Modificar a definição de método de saudação do **ViewDidLoad** removendo chamada hello muito**RefreshAsync()** final hello:
   
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
4. Modifique o método hello **RefreshAsync** tooauthenticate se hello **usuário** propriedade é nula. Adicione Olá código na parte superior de saudação da definição de método hello a seguir:
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. Abra **appdelegate. CS**, adicionar Olá método a seguir:

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. Abra **Info. plist** de arquivos, navegue até muito**tipos de URL** em Olá **avançado** seção. Configurar Olá **identificador** e hello **esquemas de URL** de seu tipo de URL e clique em **Adicionar tipo de URL**. **Esquemas de URL** devem ser Olá mesmo como {url_scheme_of_your_app}.
7. No Visual Studio ou no Xamarin Studio conectado tooyour Xamarin criar Host no seu Mac, executar o projeto de cliente Olá direcionando um dispositivo ou emulador. Verifique se que o aplicativo hello não exibe nenhum dado.
   
    Execute Olá atualização gesto colocando-o para baixo na lista de saudação de itens, o que fará com que a saudação tooappear de tela de logon. Depois que você forneceu credenciais válidas, o aplicativo hello exibirá a lista de saudação de itens de tarefas, e você pode fazer toohello atualiza os dados.

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[criar um aplicativo xamarin]: app-service-mobile-xamarin-ios-get-started.md