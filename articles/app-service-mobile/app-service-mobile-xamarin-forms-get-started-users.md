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
# <a name="add-authentication-tooyour-xamarin-forms-app"></a>Adicionar autenticação tooyour Xamarin Forms aplicativo
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a>Visão geral
Este tópico mostra como tooauthenticate usuários de um serviço de aplicativo móvel aplicativo do seu aplicativo cliente. Neste tutorial, você pode adicionar autenticação ao projeto de início rápido do Xamarin Forms hello usando um provedor de identidade que é suportado pelo serviço de aplicativo. Depois com êxito que está sendo autenticado e autorizado pelo seu aplicativo móvel, o valor de ID de usuário de saudação é exibida e você será capaz de tooaccess restringido dados da tabela.

## <a name="prerequisites"></a>Pré-requisitos
Para um resultado melhor de saudação com este tutorial, é recomendável concluir primeiro Olá [criar um aplicativo Xamarin Forms] [ 1] tutorial. Depois de concluir este tutorial, você terá um projeto Xamarin.Forms que é um aplicativo de lista de tarefas para várias plataformas.

Se você não usar Olá baixar o projeto de servidor de início rápido, você deve adicionar o projeto de tooyour de pacote de extensão de autenticação hello. Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure][2].

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Registrar seu aplicativo para a autenticação e configurar os Serviços de Aplicativos
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Adicionar URLs de redirecionamento externo permitidos de toohello seu aplicativo

A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo. Isso permite Olá autenticação sistema tooredirect tooyour back aplicativo após a conclusão do processo de autenticação de saudação. Neste tutorial, usamos o esquema de URL Olá _appname_ em todo. No entanto, você pode usar o esquema de URL que quiser. Ele deve ser exclusivo tooyour aplicativo para dispositivos móveis. redirecionamento de saudação tooenable no lado do servidor de saudação:

1. No hello [portal do Azure], selecione o serviço de aplicativo.

2. Clique em Olá **autenticação / autorização** opção de menu.

3. Em Olá **permitidas URLs de redirecionamento externo**, digite `url_scheme_of_your_app://easyauth.callback`.  Olá **url_scheme_of_your_app** na cadeia de caracteres é hello esquema de URL para seu aplicativo móvel.  Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).  Assegure uma anotação de cadeia de caracteres de saudação que você escolha como você precisará tooadjust seu código de aplicativo móvel com hello esquema de URL em vários locais.

4. Clique em **OK**.

5. Clique em **Salvar**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Restringir permissões tooauthenticated usuários
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a>Adicionar a biblioteca de classes portátil toohello autenticação
Aplicativos móveis usa Olá [LoginAsync] [ 3] método de extensão no hello [MobileServiceClient] [ 4] toosign um usuário com o serviço de aplicativo autenticação. Este exemplo usa um fluxo de autenticação de servidor gerenciado que exibe a interface de entrada do provedor de saudação no aplicativo hello. Para saber mais, veja [Autenticação gerenciada pelo servidor][5]. Para proporcionar uma melhor experiência ao usuário em seu aplicativo de produção, você deve considerar o uso da [Autenticação gerenciada pelo cliente][6].

Definir tooauthenticate com um projeto Xamarin Forms, um **IAuthenticate** interface Olá biblioteca de classes portátil para o aplicativo hello. Em seguida, adicione um **entrar** interface de usuário do botão toohello definido em Olá a biblioteca de classes portátil, que você clicar em toostart autenticação. Dados são carregados de back-end de aplicativo móvel Olá após a autenticação bem-sucedida.

Saudação de implementar **IAuthenticate** interface para cada plataforma com suporte pelo seu aplicativo.

1. No Visual Studio ou Xamarin Studio, abra App.cs do projeto Olá com **portátil** em nome de saudação, que é o projeto de biblioteca de classes portátil, em seguida, adicione a seguir Olá `using` instrução:

        using System.Threading.Tasks;
2. Em App.cs, adicione o seguinte Olá `IAuthenticate` interface definition imediatamente antes do hello `App` definição da classe.

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. interface de saudação tooinitialize com uma implementação específica de plataforma, adicionar Olá seguintes membros estáticos toohello **aplicativo** classe.

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. Abra TodoList.xaml do projeto de biblioteca de classes portátil hello, adicione o seguinte Olá **botão** elemento Olá *buttonsPanel* elemento de layout, depois de botão de saudação existente:

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    Esse botão dispara a autenticação gerenciada por servidor com seu back-end de aplicativo móvel.
5. Abrir TodoList.xaml.cs do projeto de biblioteca de classes portátil hello, em seguida, adicionar Olá toohello de campo a seguir `TodoList` classe:

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. Substituir saudação **OnAppearing** método com hello código a seguir:

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

    Este código torna-se de que dados são atualizados somente do serviço Olá depois que você tenha sido autenticado.
7. Adicionar Olá seguindo o manipulador de saudação **clicado** evento toohello **TodoList** classe:

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. Salve suas alterações e recompilar o projeto de biblioteca de classes portátil Olá verificando sem erros.

## <a name="add-authentication-toohello-android-app"></a>Adicionar aplicativo do Android autenticação toohello
Esta seção mostra como Olá tooimplement **IAuthenticate** interface no projeto de aplicativo do Android hello. Ignore esta seção se não estiver dando suporte a dispositivos Android.

1. No Visual Studio ou no Xamarin Studio, clique com botão direito Olá **droid** do projeto, em seguida, **definir como projeto de inicialização**.
2. Pressione F5 projeto de saudação de toostart no depurador Olá e verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada depois que o aplicativo é iniciado. código 401 Olá é produzido como o acesso em Olá back-end é somente usuários tooauthorized restrito.
3. Abra MainActivity.cs no projeto Android hello e adicione o seguinte Olá `using` instruções:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Saudação de atualização **MainActivity** Olá de tooimplement classe **IAuthenticate** interface, da seguinte maneira:

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. Saudação de atualização **MainActivity** classe adicionando um **MobileServiceUser** campo e um **autenticar** método, que é exigido pelo Olá **IAuthenticate**  interface, da seguinte maneira:

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

    Se você estiver usando um provedor de identidade diferente do Facebook, escolha outro valor para [MobileServiceAuthenticationProvider][7].

6. Adicionar Olá seguindo o código dentro de <application> nó do AndroidManifest.xml:

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

1. Adicionar Olá toohello de código a seguir **OnCreate** método hello **MainActivity** classe muito antes da chamada de saudação`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    Este código assegura autenticador Olá é inicializada antes Olá aplicativo carrega.
2. Recompilar o aplicativo hello, executá-lo e entrar com o provedor de autenticação Olá escolhido e verifique se que você está tooaccess capaz de dados como um usuário autenticado.

## <a name="add-authentication-toohello-ios-app"></a>Adicionar aplicativo do iOS toohello autenticação
Esta seção mostra como Olá tooimplement **IAuthenticate** interface no projeto de aplicativo do iOS hello. Ignore esta seção se não estiver dando suporte a dispositivos iOS.

1. No Visual Studio ou no Xamarin Studio, clique com botão direito Olá **iOS** do projeto, em seguida, **definir como projeto de inicialização**.
2. Pressione F5 projeto de saudação de toostart no depurador hello e verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada após o início do aplicativo hello. respostas 401 Olá é produzido como o acesso em Olá back-end é somente usuários tooauthorized restrito.
3. Abra appdelegate. cs no projeto do iOS hello e adicione o seguinte Olá `using` instruções:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Saudação de atualização **AppDelegate** Olá de tooimplement classe **IAuthenticate** interface, da seguinte maneira:

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. Saudação de atualização **AppDelegate** classe adicionando um **MobileServiceUser** campo e um **autenticar** método, que é exigido pelo Olá **IAuthenticate**  interface, da seguinte maneira:

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

    Se você estiver usando um provedor de identidade diferente do Facebook, escolha outro valor para [MobileServiceAuthenticationProvider].

6. Atualizar classe de AppDelegate Olá adicionando sobrecarga do método Abrirurl (opções de NSDictionary do aplicativo, a url de NSUrl UIApplication)

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. Adicione a seguinte linha de código toohello de saudação **FinishedLaunching** muito da chamada do método antes de saudação`LoadApplication()`:

        App.Init(this);

    Este código assegura autenticador Olá é inicializada antes que o aplicativo hello é carregado.

6. Adicionar **{url_scheme_of_your_app}** tooURL esquemas no Info. plist.

7. Recompilar o aplicativo hello, executá-lo e entrar com o provedor de autenticação Olá escolhido e verifique se que você está tooaccess capaz de dados como um usuário autenticado.

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a>Adicionar autenticação tooWindows 10 (incluindo Phone) projetos de aplicativo
Esta seção mostra como Olá tooimplement **IAuthenticate** interface em projetos de aplicativo hello Windows 10. Olá mesmas etapas se aplicam para projetos do Windows UWP (plataforma Universal), mas usando Olá **UWP** projeto (com observadas alterações). Ignore esta seção se não estiver dando suporte a dispositivos Windows.

1. "No Visual Studio, clique com botão direito ou Olá **UWP** do projeto, em seguida, **definir como projeto de inicialização**.
2. Pressione F5 projeto de saudação de toostart no depurador hello e verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada após o início do aplicativo hello. respostas 401 Olá acontece porque o acesso em Olá back-end é somente para usuários restritos tooauthorized.
3. Abra MainPage.xaml.cs para projeto de aplicativo do Windows hello e adicione o seguinte Olá `using` instruções:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    Substituir `<your_Portable_Class_Library_namespace>` com hello namespace para a biblioteca de classes portátil.
4. Saudação de atualização **MainPage** Olá de tooimplement classe **IAuthenticate** interface, da seguinte maneira:

        public sealed partial class MainPage : IAuthenticate
5. Saudação de atualização **MainPage** classe adicionando um **MobileServiceUser** campo e um **autenticar** método, que é exigido pelo Olá **IAuthenticate** interface, da seguinte maneira:

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

    Se você estiver usando um provedor de identidade diferente do Facebook, escolha outro valor para [MobileServiceAuthenticationProvider].

1. Adicionar Olá a seguinte linha de código no construtor Olá Olá **MainPage** classe muito antes da chamada de saudação`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    Substituir `<your_Portable_Class_Library_namespace>` com hello namespace para a biblioteca de classes portátil.

3. Se você estiver usando **UWP**, adicione o seguinte Olá **OnActivated** método substituir toohello **aplicativo** classe:

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   Quando o método hello substituir já existe, adicione o código condicional Olá de saudação precede o trecho de código.  Esse código não é necessário para projetos Universais do Windows.

3. Adicionar **{url_scheme_of_your_app}** em Package.appxmanifest. 

4. Recompilar o aplicativo hello, executá-lo e entrar com o provedor de autenticação Olá escolhido e verifique se que você está tooaccess capaz de dados como um usuário autenticado.

## <a name="next-steps"></a>Próximas etapas
Agora que você concluiu este tutorial de autenticação básica, considere a possibilidade de continuar tooone de saudação tutoriais a seguir:

* [Adicionar aplicativo de tooyour de notificações por push](app-service-mobile-xamarin-forms-get-started-push.md)

  Saiba como notificações por push de tooadd dão suporte ao aplicativo tooyour e configurar seu aplicativo móvel back-end toouse Hubs de notificação do Azure toosend as notificações por push.
* [Habilitar sincronização offline para seu aplicativo](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  Saiba como off-line tooadd dão suporte ao seu aplicativo usando um back-end do aplicativo móvel. Sincronização offline permite toointeract de usuários finais com um aplicativo móvel - exibindo, adicionando ou modificando dados - mesmo quando não há nenhuma conexão de rede.

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
