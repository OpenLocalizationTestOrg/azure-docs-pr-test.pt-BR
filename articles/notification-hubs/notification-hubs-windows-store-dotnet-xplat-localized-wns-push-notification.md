---
title: "aaaNotification Hubs localizado últimas notícias Tutorial"
description: "Saiba como toouse toosend de Hubs de notificação do Azure localizado notificações das últimas notícias."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: c454f5a3-a06b-45ac-91c7-f91210889b25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d273a6b384df311dea7b76ca83ccd94d9a989c4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a>Use as notícias mais recentes toosend localizada de Hubs de notificação
> [!div class="op_single_selector"]
> * [C# da Windows Store](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Visão geral
Este tópico mostra como Olá toouse **modelo** recurso de Hubs de notificação do Azure toobroadcast últimas notificações de notícias que foram localizadas por idioma e dispositivo. Neste tutorial você iniciar com hello aplicativo da Windows Store criado no [toosend de Hubs de notificação de uso últimas notícias]. Ao concluir, que você será capaz de tooregister para categorias que você está interessado, especificar um idioma no qual notificações de saudação tooreceive e receber apenas as notificações por push para categorias de saudação selecionada nesse idioma.

Há um cenário de toothis duas partes:

* Olá aplicativo da Windows Store permite que cliente dispositivos toospecify um idioma e toodifferent toosubscribe recentes categorias de notícias;
* back-end Hello transmite notificações hello, usando Olá **marca** e **modelo** recursos de Hubs de notificação do Azure.

## <a name="prerequisites"></a>Pré-requisitos
Você já deve ter concluído Olá [toosend de Hubs de notificação de uso últimas notícias] tutorial e ter o código de saudação disponível, porque este tutorial baseia-se diretamente ao código.

O Visual Studio 2012 ou posterior também é necessário.

## <a name="template-concepts"></a>Conceitos de modelo
Em [toosend de Hubs de notificação de uso últimas notícias] você criou um aplicativo usado **marcas** toonotifications toosubscribe para categorias diferentes de notícias.
No entanto, muitos aplicativos são destinados a vários mercados e requerem localização. Isso significa que o conteúdo de saudação do hello as próprias notificações têm toobe localizado e entregue toohello conjunto correto de dispositivos.
Este tópico mostraremos como Olá toouse **modelo** localizadas de recurso de Hubs de notificação tooeasily entregar notificações das últimas notícias.

Observação: uma maneira toosend localizado notificações é toocreate várias versões de cada marca. Por exemplo, toosupport em inglês, francês e inglês Mandarim, temos três marcas diferentes de notícias do mundo: "world_en", "world_fr" e "world_ch". Podemos teria toosend uma versão localizada do hello world notícias tooeach dessas marcas. Neste tópico usamos a proliferação de saudação tooavoid modelos de marcas e o requisito de saudação de enviar várias mensagens.

Em um nível alto, os modelos são uma maneira toospecify como um dispositivo específico deve receber uma notificação. modelo Olá Especifica o formato de carga exata de saudação referindo tooproperties que fazem parte da mensagem de saudação enviada pelo seu back-end do aplicativo. Em nosso caso, enviaremos uma mensagem independente de localidade contendo todos os idiomas com suporte:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Em seguida, podemos irá garantir que dispositivos registrar com um modelo que refere-se a propriedade de toohello correta. Por exemplo, um aplicativo da Windows Store que deseja tooreceive uma mensagem de notificação do sistema simples registrará para Olá modelo com todas as marcas correspondentes a seguir:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



Os modelos são um recurso muito avançado sobre o qual você pode aprender em nosso artigo [Modelos](notification-hubs-templates-cross-platform-push-messages.md) . 

## <a name="hello-app-user-interface"></a>interface de usuário do aplicativo Hello
Agora vamos modificar Olá últimas notícias aplicativo que você criou no tópico Olá [toosend de Hubs de notificação de uso últimas notícias] toosend localizado notícias mais recentes usando modelos.

Em seu aplicativo da Windows Store:

Altere sua tooinclude MainPage. XAML uma combobox de localidade:

    <Grid Margin="120, 58, 120, 80"  
            Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
        <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top"/>
        <ComboBox Name="Locale" HorizontalAlignment="Left" VerticalAlignment="Center" Width="200" Grid.Row="1" Grid.Column="0">
            <x:String>English</x:String>
            <x:String>French</x:String>
            <x:String>Mandarin</x:String>
        </ComboBox>
        <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="2" Grid.Column="0"/>
        <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="3" Grid.Column="0"/>
        <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="4" Grid.Column="0"/>
        <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="2" Grid.Column="1"/>
        <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="3" Grid.Column="1"/>
        <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="4" Grid.Column="1"/>
        <Button Content="Subscribe" HorizontalAlignment="Center" Grid.Row="5" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
    </Grid>

## <a name="building-hello-windows-store-client-app"></a>Criar aplicativo de cliente de armazenamento do Windows hello
1. Em sua classe de notificações, adicionar um tooyour de parâmetro de localidade *StoreCategoriesAndSubscribe* e *SubscribeToCateories* métodos.
   
        public async Task<Registration> StoreCategoriesAndSubscribe(string locale, IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            ApplicationData.Current.LocalSettings.Values["locale"] = locale;
            return await SubscribeToCategories(categories);
        }
   
        public async Task<Registration> SubscribeToCategories(string locale, IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration. This makes supporting notifications across other platforms much easier.
            // Using hello localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    Observe que, em vez de chamar hello *RegisterNativeAsync* método chamamos *RegisterTemplateAsync*: estamos estiver registrando um formato de notificação específico no qual Olá modelo depende da localidade hello. Nós também fornecemos um nome para o modelo de saudação ("localizedWNSTemplateExample"), porque que talvez desejemos tooregister mais de um modelo (por exemplo uma notificações do sistema) e outra para blocos e precisamos tooname em ordem tooupdate capaz de toobe ou excluí-los.
   
    Observe que, se um dispositivo registra vários modelos com hello mesma marca, uma mensagem de entrada direcionando que marca resultará em várias notificações entregues dispositivo toohello (um para cada modelo). Esse comportamento é útil quando hello mesma mensagem lógica tem tooresult em várias notificações visuais, por exemplo, mostrar uma notificação e uma notificação do sistema em um aplicativo da Windows Store.
2. Adicione Olá método tooretrieve Olá armazenado local a seguir:
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. Em seu MainPage.xaml.cs, o botão Atualizar manipulador de clique por recuperação Olá o valor atual da caixa de combinação de localidade hello e fornecendo classe notificações do toohello chamada toohello, conforme mostrado:
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var locale = (string)Locale.SelectedItem;
   
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(locale,
                 categories);
   
            var dialog = new MessageDialog("Locale: " + locale + " Subscribed to: " + 
                string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
4. Por fim, do arquivo App.xaml.cs não tooupdate-se de que seu `InitNotificationsAsync` tooretrieve método hello localidade e usá-lo ao assinar:
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a>Enviar notificações localizadas de seu back-end
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[hello app user interface]: #ui
[Building hello Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[toosend de Hubs de notificação de uso últimas notícias]: /manage/services/notification-hubs/breaking-news-dotnet

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
