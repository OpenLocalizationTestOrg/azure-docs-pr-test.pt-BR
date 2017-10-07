---
title: "aaaUse Hubs de notificação toosend últimas notícias (Windows Phone)"
description: "Use a marca de toouse de Hubs de notificação do Azure em registros toosend últimas notícias tooa do Windows Phone app."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 42726bf5-cc82-438d-9eaa-238da3322d80
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 3519a8701105f88198afe288e59e9204420234db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Usar Hubs de notificação toosend últimas notícias
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Visão geral
Este tópico mostra como Hubs de notificação do Azure toouse toobroadcast últimas notícias notificações tooa Windows Phone 8.0/8.1 Silverlight aplicativo. Se você estiver direcionando da Windows Store ou aplicativo do Windows Phone 8.1, consulte tootoohello [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) versão. Ao concluir, será ser capaz de tooregister para quebrar novas categorias que você está interessado e receber notificações de envio apenas para essas categorias. Esse cenário é um padrão comum para muitos aplicativos onde notificações têm toogroups toobe enviada de usuários que têm sido declarado anteriormente interesse neles, por exemplo, o leitor de RSS, aplicativos para ventiladores de música, etc.

Cenários de transmissão são habilitados, incluindo um ou mais *marcas* ao criar um registro no hub de notificação de saudação. Quando as notificações são enviadas tooa marca, todos os dispositivos que foram registrados para marca de saudação receberão a notificação de saudação. Como as marcas são simplesmente cadeias de caracteres, eles não têm toobe provisionado com antecedência. Para obter mais informações sobre marcas, consulte muito[expressões de marca e roteamento de Hubs de notificação](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Pré-requisitos
Este tópico se baseia no aplicativo hello criado na [começar com Hubs de notificação]. Antes de iniciar o tutorial, você deve primeiro concluir a [começar com Hubs de notificação].

## <a name="add-category-selection-toohello-app"></a>Adicionar aplicativo de toohello de seleção de categoria
Olá primeira etapa é tooadd Olá da interface do usuário tooyour existente principal página de elementos que permitem Olá usuário tooselect categorias tooregister. categorias de saudação selecionadas por um usuário são armazenadas no dispositivo de saudação. Quando o aplicativo hello é iniciado, um registro de dispositivo é criado em seu hub de notificação com categorias de saudação selecionada como marcas.

1. Abrir o arquivo de projeto do hello MainPage. XAML e substitua Olá **grade** elementos nomeados `TitlePanel` e `ContentPanel` com hello código a seguir:
   
        <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
            <TextBlock Text="Breaking News" Style="{StaticResource PhoneTextNormalStyle}" Margin="12,0"/>
            <TextBlock Text="Categories" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
        </StackPanel>
   
        <Grid Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
            <Grid.RowDefinitions>
                <RowDefinition Height="auto"/>
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <CheckBox Name="WorldCheckBox" Grid.Row="0" Grid.Column="0">World</CheckBox>
            <CheckBox Name="PoliticsCheckBox" Grid.Row="1" Grid.Column="0">Politics</CheckBox>
            <CheckBox Name="BusinessCheckBox" Grid.Row="2" Grid.Column="0">Business</CheckBox>
            <CheckBox Name="TechnologyCheckBox" Grid.Row="0" Grid.Column="1">Technology</CheckBox>
            <CheckBox Name="ScienceCheckBox" Grid.Row="1" Grid.Column="1">Science</CheckBox>
            <CheckBox Name="SportsCheckBox" Grid.Row="2" Grid.Column="1">Sports</CheckBox>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
        </Grid>
2. No projeto de hello, crie uma nova classe chamada **notificações**, adicionar Olá **pública** toohello modificador definição da classe e adicione o seguinte Olá **usando** instruções toohello novo arquivo de código:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. De código a seguir de saudação de cópia em Olá novo **notificações** classe:
   
        private NotificationHub hub;
   
        // Registration task toocomplete registration in hello ChannelUriUpdated event handler
        private TaskCompletionSource<Registration> registrationTask;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string)IsolatedStorageSettings.ApplicationSettings["categories"];
            return categories != null ? categories.Split(',') : new string[0];
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            var categoriesAsString = string.Join(",", categories);
            var settings = IsolatedStorageSettings.ApplicationSettings;
            if (!settings.Contains("categories"))
            {
                settings.Add("categories", categoriesAsString);
            }
            else
            {
                settings["categories"] = categoriesAsString;
            }
            settings.Save();
   
            return await SubscribeToCategories();
        }
   
        public async Task<Registration> SubscribeToCategories()
        {
            registrationTask = new TaskCompletionSource<Registration>();
   
            var channel = HttpNotificationChannel.Find("MyPushChannel");
   
            if (channel == null)
            {
                channel = new HttpNotificationChannel("MyPushChannel");
                channel.Open();
                channel.BindToShellToast();
                channel.ChannelUriUpdated += channel_ChannelUriUpdated;
   
                // This is optional, used tooreceive notifications while hello app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete hello registrationTask here.  
            // If it is null, hello registrationTask will be completed in hello ChannelUriUpdated event handler.
            if (channel.ChannelUri != null)
            {
                await RegisterTemplate(channel.ChannelUri);
            }
   
            return await registrationTask.Task;
        }
   
        async void channel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
        {
            await RegisterTemplate(e.ChannelUri);
        }
   
        async Task<Registration> RegisterTemplate(Uri channelUri)
        {
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // hello stored categories tags are passed with hello template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used tooreceive notifications while hello app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out hello information that was part of hello message.
            foreach (string key in e.Collection.Keys)
            {
                message.AppendFormat("{0}: {1}\n", key, e.Collection[key]);
   
                if (string.Compare(
                    key,
                    "wp:Param",
                    System.Globalization.CultureInfo.InvariantCulture,
                    System.Globalization.CompareOptions.IgnoreCase) == 0)
                {
                    relativeUri = e.Collection[key];
                }
            }
   
            // Display a dialog of all hello fields in hello toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    Essa classe usa hello isolado armazenamento toostore Olá categorias de notícias este dispositivo está tooreceive. Ele também contém métodos tooregister para estas categorias usando uma [modelo](notification-hubs-templates-cross-platform-push-messages.md) registro de notificação.


1. No arquivo de projeto App.xaml.cs hello, adicionar Olá toohello de propriedade a seguir **aplicativo** classe. Substituir saudação `<hub name>` e `<connection string with listen access>` espaços reservados com seu hub nome e hello conexão cadeia de notificação para *DefaultListenSharedAccessSignature* que você obteve anteriormente.
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > Porque as credenciais que são distribuídas com um aplicativo cliente não são seguras em geral, você só deve distribuir chave Olá para acesso de escuta com o aplicativo cliente. Escutar permite acesso que tooregister seu aplicativo para notificações, mas os registros existentes não pode ser modificada e não não possível enviar notificações. chave de acesso completo de saudação é usada em um serviço de back-end seguro para enviar notificações e alterar os registros existentes.
   > 
   > 
2. Em seu MainPage.xaml.cs, adicione Olá seguinte linha:
   
        using Windows.UI.Popups;
3. No arquivo de projeto MainPage.xaml.cs hello, adicione Olá método a seguir:
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
          var categories = new HashSet<string>();
          if (WorldCheckBox.IsChecked == true) categories.Add("World");
          if (PoliticsCheckBox.IsChecked == true) categories.Add("Politics");
          if (BusinessCheckBox.IsChecked == true) categories.Add("Business");
          if (TechnologyCheckBox.IsChecked == true) categories.Add("Technology");
          if (ScienceCheckBox.IsChecked == true) categories.Add("Science");
          if (SportsCheckBox.IsChecked == true) categories.Add("Sports");
   
          var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
          MessageBox.Show("Subscribed to: " + string.Join(",", categories) + " on registration id : " +
             result.RegistrationId);
        }
   
    Esse método cria uma lista de categorias e usa Olá **notificações** classe toostore lista de saudação no armazenamento local hello e registre marcas correspondentes Olá com seu hub de notificação. Quando as categorias são alteradas, registro de saudação é recriado com novas categorias de saudação.

Seu aplicativo agora é capaz de toostore um conjunto de categorias no armazenamento local no dispositivo hello e registrar com o hub de notificação Olá sempre que as alterações do usuário Olá Olá seleção de categorias.

## <a name="register-for-notifications"></a>Registrar-se para receber notificações
Estas etapas se registrar com o hub de notificação de saudação na inicialização usando as categorias de saudação que foram armazenadas no armazenamento local.

> [!NOTE]
> Como canal Olá URI atribuído pelo Olá serviço de notificação por Push da Microsoft (MPNS) pode ser alterado a qualquer momento, você deve registrar para notificações frequentemente tooavoid falhas de notificação. Este exemplo registra para notificações sempre que o aplicativo hello for iniciado. Para aplicativos que são executados com frequência, mais de uma vez por dia, você poderá provavelmente Ignorar largura de banda do registro toopreserve se menos de um dia se passou desde o registro anterior hello.
> 
> 

1. Abrir o arquivo de App.xaml.cs hello e adicione Olá **async** modificador muito**Application_Launching** método e substituir Olá Hubs de notificação código de registro que você adicionou na [começar com Hubs de notificação] com hello código a seguir:
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    Isso torna-se de que sempre que o aplicativo hello é iniciado, ele recupera as categorias de saudação do armazenamento local e solicita um registro para estas categorias.
2. No arquivo de projeto MainPage.xaml.cs hello, adicionar Olá seguindo o código que implementa Olá **OnNavigatedTo** método:
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldCheckBox.IsChecked = true;
            if (categories.Contains("Politics")) PoliticsCheckBox.IsChecked = true;
            if (categories.Contains("Business")) BusinessCheckBox.IsChecked = true;
            if (categories.Contains("Technology")) TechnologyCheckBox.IsChecked = true;
            if (categories.Contains("Science")) ScienceCheckBox.IsChecked = true;
            if (categories.Contains("Sports")) SportsCheckBox.IsChecked = true;
        }
   
    Esta página principal do hello atualizações com base no status de saudação do previamente salvo categorias.

aplicativo Hello agora está concluído e pode armazenar um conjunto de categorias em Olá dispositivo local de armazenamento usado tooregister com o hub de notificação Olá sempre que as alterações do usuário Olá Olá seleção de categorias. Em seguida, definiremos um back-end que pode enviar categoria notificações toothis aplicativo.

## <a name="sending-tagged-notifications"></a>Enviando notificações marcadas
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Execute o aplicativo hello e geram notificações
1. No Visual Studio, pressione F5 toocompile e iniciar o aplicativo hello.
   
    ![][1]
   
    Observe que o aplicativo hello de que interface do usuário fornece um conjunto alterna que permite que você escolha Olá categorias toosubscribe para.
2. Habilite uma ou mais alternâncias de categorias e depois clique em **Assinar**.
   
    aplicativo Hello converte categorias Olá selecionado em marcas e solicita um novo registro de dispositivo para marcas de saudação selecionada do hub de notificação de saudação. Olá categorias registradas são retornadas e exibidas em uma caixa de diálogo.
   
    ![][2]
3. Depois de receber uma confirmação de que suas categorias foram assinatura concluída, execute notificações de toosend de aplicativo hello console para cada categorias. Verifique se que você só receberá uma notificação para categorias de saudação que você se inscreveu.
   
    ![][3]

Você concluiu este tópico.

<!--##Next steps

In this tutorial we learned how toobroadcast breaking news by category. Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs toobroadcast localized breaking news]

    Learn how tooexpand hello breaking news app tooenable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how toopush notifications toospecific authenticated users. This is a good solution for sending notifications only toospecific users.
-->

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
[começar com Hubs de notificação]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/
[Use Notification Hubs toobroadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Phone]: ??

