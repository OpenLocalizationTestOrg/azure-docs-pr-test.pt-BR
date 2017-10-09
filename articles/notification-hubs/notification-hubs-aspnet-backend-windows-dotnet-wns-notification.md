---
title: "aaaAzure notificar usuários de Hubs de notificação com o back-end .NET"
description: "Saiba como toosend segura notificações por push no Azure. Exemplos de código escritos em c# usando Olá API .NET."
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a>Notificar usuários nos Hubs de Notificação do Azure com o back-end do .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Visão geral
Suporte de notificação por push no Azure permite que você tooaccess uma fácil de usar, multiplatform e infraestrutura de envio expandido, o que simplifica bastante a implementação de saudação de notificações por push para aplicativos de consumidor e empresariais para dispositivos móveis plataformas. Este tutorial mostra como toouse Hubs de notificação do Azure toosend envio usuário de aplicativo específico de tooa notificações em um dispositivo específico. Um back-end ASP.NET WebAPI é usado tooauthenticate clientes. Usar Olá autenticou o usuário do cliente e marca será adicionada automaticamente pelo registro de toonotification Olá back-end. Essa marca será toosend usado por notificações de toogenerate Olá back-end para um usuário específico. Para obter mais informações sobre como registrar para notificações de usar um back-end do aplicativo, consulte o tópico de orientação de saudação [registro do seu back-end do aplicativo](http://msdn.microsoft.com/library/dn743807.aspx). Este tutorial baseia-se no projeto que você criou no hello e hub de notificação Olá [começar com Hubs de notificação] tutorial.

Este tutorial também é toohello pré-requisito Olá [proteger Push] tutorial. Depois de concluir as etapas de saudação neste tutorial, você poderá toohello [proteger Push] tutorial, que mostra como toomodify Olá código neste tutorial toosend uma notificação por push com segurança.

## <a name="before-you-begin"></a>Antes de começar
Levamos seus comentários a sério. Se você tiver dificuldade para concluir este tópico ou recomendações para melhorar este conteúdo, Apreciamos seus comentários na parte inferior da saudação da página de saudação.

código de saudação concluído para este tutorial pode ser encontrado no GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). 

## <a name="prerequisites"></a>Pré-requisitos
Antes de iniciar este tutorial, você já deve ter concluído estes tutoriais dos Serviços Móveis:

* [começar com Hubs de notificação]<br/>Criar seu hub de notificação e reservar nome do aplicativo hello e registrar notificações tooreceive neste tutorial. Este tutorial presume que você já concluiu essas etapas. Se não estiver, siga as etapas de saudação em [Introdução aos Hubs de notificação (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); especificamente, Olá seções [registrar seu aplicativo para saudação da Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) e [configurar o Hub de notificação](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). Em particular, certifique-se de que você inseriu Olá **SID do pacote** e **segredo do cliente** valores no portal de saudação em hello **configurar** guia hub de notificação. Este procedimento de configuração é descrito na seção de saudação [configurar seu Hub de notificação](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). Essa é uma etapa importante: se credenciais Olá no portal de saudação não correspondem àquelas especificadas para o nome do aplicativo hello escolhido, notificação por push de saudação não terá êxito.

> [!NOTE]
> Se você estiver usando aplicativos móveis no serviço de aplicativo do Azure como seu serviço de back-end, consulte Olá [versão de aplicativos móveis](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) deste tutorial.
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a>Atualizar o código de saudação do projeto de cliente de saudação
Nesta seção, você atualizar o código de saudação no projeto Olá concluída para Olá [começar com Hubs de notificação] tutorial. Olá já deve ser associado com o repositório de saudação e configurado para o hub de notificação. Nesta seção, você irá adicionar código toocall Olá novo WebAPI back-end e usá-lo para registrar e enviar notificações.

1. No Visual Studio, abra a solução de saudação de saudação criada para Olá [começar com Hubs de notificação] tutorial.
2. No Gerenciador de soluções, clique com botão direito Olá **(Windows 8.1)** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.
3. No lado esquerdo do hello, clique em **Online**.
4. Em Olá **pesquisa** , digite **cliente Http**.
5. Na lista de resultados de saudação, clique em **bibliotecas de cliente HTTP Microsoft**e, em seguida, clique em **instalar**. Concluir a instalação de saudação.
6. Em Olá NuGet **pesquisa** , digite **Json.net**. Instalar Olá **Json.NET** pacote e feche Olá NuGet Package Manager janela.
7. Repita as etapas de saudação acima para Olá **(Windows Phone 8.1)** saudação do projeto tooinstall **JSON.NET** pacote NuGet para o projeto do Windows Phone hello.
8. No Solution Explorer, no hello **(Windows 8.1)** de projeto, clique duas vezes em **MainPage. XAML** tooopen-lo no editor do Visual Studio hello.
9. Em Olá **MainPage. XAML** código XML, substitua Olá `<Grid>` seção com hello código a seguir. Esse código adiciona uma caixa de texto nome de usuário e senha que Olá usuário será autenticado com. Ele também adiciona caixas de texto de mensagem de notificação de saudação e marca de nome de usuário de saudação que deve receber a notificação de saudação:
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. No Solution Explorer, no hello **(Windows Phone 8.1)** projeto, abra **MainPage. XAML** e substitua Olá Windows Phone 8.1 `<Grid>` seção com esse mesmo código acima. interface Olá deve ter aparência semelhante toowhats mostrado abaixo.
    
    ![][13]
11. No Gerenciador de soluções, abra Olá **MainPage.xaml.cs** arquivo hello **(Windows 8.1)** e **(Windows Phone 8.1)** projetos. Adicione o seguinte Olá `using` instruções na parte superior da saudação dos dois arquivos:
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. Em **MainPage.xaml.cs** para Olá **(Windows 8.1)** e **(Windows Phone 8.1)** projetos, adicionar Olá toohello membro a seguir `MainPage` classe. Ser tooreplace se `<Enter Your Backend Endpoint>` com hello seu ponto de extremidade de back-end real obtido anteriormente. Por exemplo: `http://mybackend.azurewebsites.net`.
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. Adicione código Olá abaixo classe MainPage toohello **MainPage.xaml.cs** para Olá **(Windows 8.1)** e **(Windows Phone 8.1)** projetos.
    
    Olá `PushClick` método é hello manipulador de clique do hello **enviar por Push** botão. Chama Olá back-end tootrigger tooall uma notificação dispositivos com uma marca de nome de usuário que corresponde a saudação `to_tag` parâmetro. mensagem de notificação de saudação é enviada como conteúdo JSON no corpo da solicitação de saudação.
    
    Olá `LoginAndRegisterClick` método é hello manipulador de clique do hello **efetuar login e registrar** botão. Ele armazena Olá basic, em seguida, usa o token de autenticação no armazenamento local (Observe que isso representa qualquer token usa o esquema de autenticação), `RegisterClient` tooregister para notificações usando Olá back-end.

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. No Gerenciador de soluções, em Olá **compartilhado** projeto, abra Olá **App.xaml.cs** arquivo. Localizar chamada hello muito`InitNotificationsAsync()` em Olá `OnLaunched()` manipulador de eventos. Comentar ou excluir chamada hello muito`InitNotificationsAsync()`. manipulador de saudação do botão adicionado acima inicializará registros de notificação.

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. No Gerenciador de soluções, clique com botão direito Olá **compartilhado** projeto e, em seguida, clique em **adicionar**e, em seguida, clique em **classe**. Nome de classe Olá **RegisterClient.cs**, em seguida, clique em **Okey** toogenerate classe de saudação.
   
   Essa classe será ajustado Olá REST chamadas toocontact necessário Olá aplicativo back-end, em ordem tooregister para notificações por push. Também localmente armazena Olá *registrationIds* criado pelo Olá Hub de notificação, conforme detalhado no [registro do seu back-end do aplicativo](http://msdn.microsoft.com/library/dn743807.aspx). Observe que ele usa um token de autorização armazenado no armazenamento local quando você clica em Olá **efetuar login e registrar** botão.
2. Adicione o seguinte Olá `using` instruções na parte superior de saudação do arquivo de RegisterClient.cs hello:
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. Adicionar Olá seguindo o código dentro de saudação `RegisterClient` definição da classe.
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. Salve todas as alterações.

## <a name="testing-hello-application"></a>Aplicativo em teste
1. Inicie o aplicativo hello no Windows 8.1 e Windows Phone 8.1. Para Windows Phone 8.1, você pode executar instância Olá no emulador de saudação ou um dispositivo real.
2. Na instância de saudação do Windows 8.1 do aplicativo hello, insira um **Username** e **senha** conforme mostrado na tela hello abaixo. Ele deve diferir de saudação nome e a senha que você inserir no Windows Phone.
3. Clique em **Fazer logon e registrar** e verifique se um diálogo mostra que você fez logon. Isso também permitirá Olá **enviar por Push** botão.
   
    ![][14]
4. Na instância de saudação Windows Phone 8.1, insira uma cadeia de caracteres de nome de usuário em ambos os Olá **Username** e **senha** campos, em seguida, clique em **logon e registrar**.
5. Em seguida, em Olá **marca de nome de usuário do destinatário** , digite o nome de usuário Olá registrado no Windows 8.1. Digite uma mensagem de notificação e clique em **Enviar notificação por push**.
   
    ![][16]
6. Somente os dispositivos de saudação que foram registrados com marca de nome de usuário correspondente Olá recebem a mensagem de notificação de saudação.
   
    ![][15]

## <a name="next-steps"></a>Próximas etapas
* Se você quiser toosegment os usuários, grupos de interesse, consulte [toosend de Hubs de notificação de uso últimas notícias].
* toolearn mais informações sobre como toouse Hubs de notificação, consulte [orientação de Hubs de notificação].

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[começar com Hubs de notificação]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[proteger Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[toosend de Hubs de notificação de uso últimas notícias]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[orientação de Hubs de notificação]: http://msdn.microsoft.com/library/jj927170.aspx
