---
title: "aaaUse Hubs de notificação toosend últimas notícias (universais do Windows)"
description: "Use Hubs de notificação do Azure com marcas Olá registro toosend últimas notícias tooa aplicativo universal do Windows."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 994d2eed-f62e-433c-bf65-4afebf1c0561
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f102d286d2c7bd387fcfa2c7eab2ba31a0298517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Usar Hubs de notificação toosend últimas notícias
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Visão geral
Este tópico mostra como toouse Hubs de notificação do Azure toobroadcast últimas notícias notificações tooa Windows Store ou aplicativo do Windows Phone 8.1 (não Silverlight). Se você estiver direcionando o Windows Phone 8.1 Silverlight, consulte toohello [do Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) versão. Ao concluir, será ser capaz de tooregister para quebrar novas categorias que você está interessado e receber notificações de envio apenas para essas categorias. Esse cenário é um padrão comum para muitos aplicativos onde notificações têm toogroups toobe enviada de usuários que têm sido declarado anteriormente interesse em-los, por exemplo, leitor de RSS, aplicativos para ventiladores de música e assim por diante. 

Cenários de transmissão são habilitados, incluindo um ou mais *marcas* ao criar um registro no hub de notificação de saudação. Quando as notificações são enviadas tooa marca, todos os dispositivos que foram registrados para marca de saudação receberão a notificação de saudação. Como as marcas são simplesmente cadeias de caracteres, eles não têm toobe provisionado com antecedência. Para obter mais informações sobre marcas, consulte muito[expressões de marca e roteamento de Hubs de notificação](notification-hubs-tags-segment-push-message.md).

> [!NOTE]
> Windows Store e a versão de projetos do Windows Phone 8.1 e versões anteriores não têm suporte no Visual Studio de 2017.  Para saber mais, confira [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs). 

## <a name="prerequisites"></a>Pré-requisitos
Este tópico se baseia no aplicativo hello criado na [começar com Hubs de notificação][get-started]. Antes de iniciar o tutorial, você deve primeiro concluir a [Introdução aos Hubs de Notificação][get-started].

## <a name="add-category-selection-toohello-app"></a>Adicionar aplicativo de toohello de seleção de categoria
Olá primeira etapa é tooadd Olá da interface do usuário tooyour existente principal página de elementos que permitem Olá usuário tooselect categorias tooregister. categorias de saudação selecionadas por um usuário são armazenadas no dispositivo de saudação. Quando o aplicativo hello é iniciado, um registro de dispositivo é criado em seu hub de notificação com categorias de saudação selecionada como marcas.

1. Abra o arquivo de projeto do hello MainPage. XAML e Olá cópia Olá código a seguir **grade** elemento:
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition/>
            </Grid.ColumnDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="2" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="1" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="2" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="3" Grid.Column="1" HorizontalAlignment="Center"/>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click"/>
        </Grid>
2. Olá clique com botão direito **compartilhado** do projeto e adicione uma nova classe chamada **notificações**, adicionar Olá **pública** modificador toohello definição da classe, em seguida, adicionar Olá após **usando** instruções toohello novo arquivo de código:
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. De código a seguir de saudação de cópia em Olá novo **notificações** classe:
   
        private NotificationHub hub;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            return await SubscribeToCategories(categories);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string) ApplicationData.Current.LocalSettings.Values["categories"];
            return categories != null ? categories.Split(','): new string[0];
        }
   
        public async Task<Registration> SubscribeToCategories(IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    Essa classe usa categorias de saudação do hello armazenamento local toostore de notícias este dispositivo tem tooreceive. Observe que, em vez de chamar hello *RegisterNativeAsync* método chamamos *RegisterTemplateAsync* tooregister para categorias de saudação usando um registro do modelo. 
   
    Nós também fornecemos um nome para o modelo de saudação ("simpleWNSTemplateExample"), porque que talvez desejemos tooregister mais de um modelo (por exemplo uma notificações do sistema) e outra para blocos e precisamos tooname em ordem tooupdate capaz de toobe ou excluí-los.
   
    Observe que, se um dispositivo registra vários modelos com hello mesma marca, uma mensagem de entrada direcionando que marca resultará em várias notificações entregues dispositivo toohello (um para cada modelo). Esse comportamento é útil quando hello mesma mensagem lógica tem tooresult em várias notificações visuais, por exemplo, mostrar uma notificação e uma notificação do sistema em um aplicativo da Windows Store.
   
    Para obter mais informações sobre o uso de modelos, consulte [Modelos](notification-hubs-templates-cross-platform-push-messages.md).
4. No arquivo de projeto App.xaml.cs hello, adicionar Olá toohello de propriedade a seguir **aplicativo** classe:
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    Esta propriedade é usada toocreate e acesso uma **notificações** instância.
   
    Olá acima código, substitua Olá `<hub name>` e `<connection string with listen access>` espaços reservados com seu hub nome e hello conexão cadeia de notificação para *DefaultListenSharedAccessSignature* que você obteve anteriormente.
   
   > [!NOTE]
   > Porque as credenciais que são distribuídas com um aplicativo cliente não são seguras em geral, você só deve distribuir chave Olá para acesso de escuta com o aplicativo cliente. Escutar permite acesso que tooregister seu aplicativo para notificações, mas os registros existentes não pode ser modificada e não não possível enviar notificações. chave de acesso completo de saudação é usada em um serviço de back-end seguro para enviar notificações e alterar os registros existentes.
   > 
   > 
5. Em seu MainPage.xaml.cs, adicione Olá seguinte linha:
   
        using Windows.UI.Popups;
6. No arquivo de projeto MainPage.xaml.cs hello, adicione Olá método a seguir:
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
            var dialog = new MessageDialog("Subscribed to: " + string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
   
    Esse método cria uma lista de categorias e usa Olá **notificações** classe toostore lista de saudação no armazenamento local hello e registre marcas correspondentes Olá com seu hub de notificação. Quando as categorias são alteradas, registro de saudação é recriado com novas categorias de saudação.

Seu aplicativo agora é capaz de toostore um conjunto de categorias no armazenamento local no dispositivo hello e registrar com o hub de notificação Olá sempre que as alterações do usuário Olá Olá seleção de categorias.

## <a name="register-for-notifications"></a>Registrar-se para receber notificações
Estas etapas se registrar com o hub de notificação de saudação na inicialização usando as categorias de saudação que foram armazenadas no armazenamento local.

> [!NOTE]
> Como canal Olá URI atribuído pelo Olá serviço de notificação do Windows (WNS) pode ser alterado a qualquer momento, você deve registrar para notificações frequentemente tooavoid falhas de notificação. Este exemplo registra para notificação sempre que o aplicativo hello for iniciado. Para aplicativos que são executados com frequência, mais de uma vez por dia, você poderá provavelmente Ignorar largura de banda do registro toopreserve se menos de um dia se passou desde o registro anterior hello.
> 
> 

1. Saudação de arquivo e atualização App.xaml.cs Olá abrir **InitNotificationsAsync** saudação do método toouse `notifications` toosubscribe classe baseadas em categorias.
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    Isso torna-se de que sempre que o aplicativo hello é iniciado, ele recupera as categorias de saudação do armazenamento local e solicita um registro para estas categorias. Olá **InitNotificationsAsync** método foi criado como parte da saudação [começar com Hubs de notificação] [ get-started] tutorial.
2. No arquivo de projeto MainPage.xaml.cs hello, adicionar Olá toohello de código a seguir *OnNavigatedTo* método:
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldToggle.IsOn = true;
            if (categories.Contains("Politics")) PoliticsToggle.IsOn = true;
            if (categories.Contains("Business")) BusinessToggle.IsOn = true;
            if (categories.Contains("Technology")) TechnologyToggle.IsOn = true;
            if (categories.Contains("Science")) ScienceToggle.IsOn = true;
            if (categories.Contains("Sports")) SportsToggle.IsOn = true;
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
   
    ![][19]
3. Envie uma nova notificação de saudação back-end em uma saudação maneiras a seguir:
   
   * **Aplicativo de console:** iniciar o aplicativo de console hello.
   * **Java/PHP:** execute seu aplicativo/script.
     
     As notificações para categorias de saudação selecionada aparecem como notificações do sistema.
     
     ![][14]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, nós aprendemos como toobroadcast últimas notícias por categoria. Considere a concluir uma saudação tutoriais que realçam outros cenários avançados de Hubs de notificação a seguir:

* [Use as notícias mais recentes toobroadcast localizada de Hubs de notificação]
  
    Saiba como Olá tooexpand últimas notícias aplicativo tooenable enviar localizado notificações.

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[Use as notícias mais recentes toobroadcast localizada de Hubs de notificação]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
