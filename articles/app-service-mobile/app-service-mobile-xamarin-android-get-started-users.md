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
# <a name="add-authentication-tooyour-xamarinandroid-app"></a>Adicionar autenticação tooyour xamarin aplicativo
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Este tópico mostra como tooauthenticate usuários de um aplicativo móvel do seu aplicativo cliente. Neste tutorial, você deve adicionar projeto de início rápido de toohello de autenticação usando um provedor de identidade que é compatível com aplicativos móveis do Azure. Após com êxito que está sendo autenticado e autorizado no hello aplicativo móvel, o valor de ID de usuário de saudação é exibida.

Este tutorial baseia-se no início rápido de aplicativo móvel hello. Primeiro, você deve concluir o tutorial de saudação [criar um aplicativo xamarin]. Se você não usar Olá baixar o projeto de servidor de início rápido, você deve adicionar o projeto de tooyour de pacote de extensão de autenticação hello. Para obter mais informações sobre pacotes de extensão do servidor, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register"></a>Registrar seu aplicativo para autenticação e configurar os Serviços de Aplicativos
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

No Visual Studio ou no Xamarin Studio, execute o projeto de cliente de saudação em um dispositivo ou emulador. Verifique se que uma exceção sem tratamento com um código de status de 401 (não autorizado) é gerada após o início do aplicativo hello. Isso acontece porque o aplicativo hello tentativas tooaccess seu back-end do aplicativo móvel como um usuário não autenticado. Olá *TodoItem* tabela agora requer autenticação.

Em seguida, você irá atualizar recursos de toorequest de back-end de aplicativo móvel de saudação do aplicativo hello cliente com um usuário autenticado.

## <a name="add-authentication"></a>Adicionar autenticação toohello aplicativo
aplicativo Hello é saudação do toorequire atualizado os usuários tootap **entrar** botão e autenticar antes que os dados são exibidos.

1. Adicionar Olá toohello de código a seguir **TodoActivity** classe:
   
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
   
    Isso cria um novo tooauthenticate de método de um usuário e um manipulador de método para um novo **entrar** botão. usuário Olá no código de exemplo hello acima é autenticado usando um logon do Facebook. Uma caixa de diálogo é a ID de usuário de saudação toodisplay usado uma vez autenticado.
   
   > [!NOTE]
   > Se você estiver usando um provedor de identidade diferente do Facebook, altere o valor de saudação passado muito**LoginAsync** acima tooone seguinte Olá: *MicrosoftAccount*, *Twitter*, *Google*, ou *WindowsAzureActiveDirectory*.
   > 
   > 
2. Em Olá **OnCreate** método, excluir ou Olá comentários de linha de código a seguir:
   
        OnRefreshItemsSelected ();
3. No arquivo de Activity_To_Do.axml de saudação, adicione o seguinte Olá *LoginUser* botão definição antes Olá existente *AddItem* botão:
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. Adicione Olá arquivo de recursos do elemento toohello Strings.xml a seguir:
   
        <string name="login_button_text">Sign in</string>
5. Abrir o arquivo de AndroidManifest.xml hello, adicione Olá seguindo o código dentro de `<application>` elemento XML:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. No Visual Studio ou no Xamarin Studio, execute o projeto de saudação do cliente em um dispositivo ou emulador e entrar com seu provedor de identidade escolhido. Quando você está conectado com êxito, aplicativo hello exibirá sua ID de logon e lista de saudação de itens de tarefas e você pode fazer atualizações toohello dados.

<!-- URLs. -->
[criar um aplicativo xamarin]: app-service-mobile-xamarin-android-get-started.md