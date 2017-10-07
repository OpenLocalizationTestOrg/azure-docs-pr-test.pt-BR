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
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a><span data-ttu-id="d3cbc-103">Use as notícias mais recentes toosend localizada de Hubs de notificação</span><span class="sxs-lookup"><span data-stu-id="d3cbc-103">Use Notification Hubs toosend localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3cbc-104">C# da Windows Store</span><span class="sxs-lookup"><span data-stu-id="d3cbc-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="d3cbc-105">iOS</span><span class="sxs-lookup"><span data-stu-id="d3cbc-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="d3cbc-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d3cbc-106">Overview</span></span>
<span data-ttu-id="d3cbc-107">Este tópico mostra como Olá toouse **modelo** recurso de Hubs de notificação do Azure toobroadcast últimas notificações de notícias que foram localizadas por idioma e dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-107">This topic shows you how toouse hello **template** feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="d3cbc-108">Neste tutorial você iniciar com hello aplicativo da Windows Store criado no [toosend de Hubs de notificação de uso últimas notícias].</span><span class="sxs-lookup"><span data-stu-id="d3cbc-108">In this tutorial you start with hello Windows Store app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="d3cbc-109">Ao concluir, que você será capaz de tooregister para categorias que você está interessado, especificar um idioma no qual notificações de saudação tooreceive e receber apenas as notificações por push para categorias de saudação selecionada nesse idioma.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="d3cbc-110">Há um cenário de toothis duas partes:</span><span class="sxs-lookup"><span data-stu-id="d3cbc-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="d3cbc-111">Olá aplicativo da Windows Store permite que cliente dispositivos toospecify um idioma e toodifferent toosubscribe recentes categorias de notícias;</span><span class="sxs-lookup"><span data-stu-id="d3cbc-111">hello Windows Store app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="d3cbc-112">back-end Hello transmite notificações hello, usando Olá **marca** e **modelo** recursos de Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3cbc-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d3cbc-113">Prerequisites</span></span>
<span data-ttu-id="d3cbc-114">Você já deve ter concluído Olá [toosend de Hubs de notificação de uso últimas notícias] tutorial e ter o código de saudação disponível, porque este tutorial baseia-se diretamente ao código.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="d3cbc-115">O Visual Studio 2012 ou posterior também é necessário.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="d3cbc-116">Conceitos de modelo</span><span class="sxs-lookup"><span data-stu-id="d3cbc-116">Template concepts</span></span>
<span data-ttu-id="d3cbc-117">Em [toosend de Hubs de notificação de uso últimas notícias] você criou um aplicativo usado **marcas** toonotifications toosubscribe para categorias diferentes de notícias.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="d3cbc-118">No entanto, muitos aplicativos são destinados a vários mercados e requerem localização.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="d3cbc-119">Isso significa que o conteúdo de saudação do hello as próprias notificações têm toobe localizado e entregue toohello conjunto correto de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="d3cbc-120">Este tópico mostraremos como Olá toouse **modelo** localizadas de recurso de Hubs de notificação tooeasily entregar notificações das últimas notícias.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="d3cbc-121">Observação: uma maneira toosend localizado notificações é toocreate várias versões de cada marca.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="d3cbc-122">Por exemplo, toosupport em inglês, francês e inglês Mandarim, temos três marcas diferentes de notícias do mundo: "world_en", "world_fr" e "world_ch".</span><span class="sxs-lookup"><span data-stu-id="d3cbc-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="d3cbc-123">Podemos teria toosend uma versão localizada do hello world notícias tooeach dessas marcas.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="d3cbc-124">Neste tópico usamos a proliferação de saudação tooavoid modelos de marcas e o requisito de saudação de enviar várias mensagens.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="d3cbc-125">Em um nível alto, os modelos são uma maneira toospecify como um dispositivo específico deve receber uma notificação.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="d3cbc-126">modelo Olá Especifica o formato de carga exata de saudação referindo tooproperties que fazem parte da mensagem de saudação enviada pelo seu back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="d3cbc-127">Em nosso caso, enviaremos uma mensagem independente de localidade contendo todos os idiomas com suporte:</span><span class="sxs-lookup"><span data-stu-id="d3cbc-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="d3cbc-128">Em seguida, podemos irá garantir que dispositivos registrar com um modelo que refere-se a propriedade de toohello correta.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="d3cbc-129">Por exemplo, um aplicativo da Windows Store que deseja tooreceive uma mensagem de notificação do sistema simples registrará para Olá modelo com todas as marcas correspondentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3cbc-129">For instance, a Windows Store app that wants tooreceive a simple toast message will register for hello following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="d3cbc-130">Os modelos são um recurso muito avançado sobre o qual você pode aprender em nosso artigo [Modelos](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="d3cbc-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="hello-app-user-interface"></a><span data-ttu-id="d3cbc-131">interface de usuário do aplicativo Hello</span><span class="sxs-lookup"><span data-stu-id="d3cbc-131">hello app user interface</span></span>
<span data-ttu-id="d3cbc-132">Agora vamos modificar Olá últimas notícias aplicativo que você criou no tópico Olá [toosend de Hubs de notificação de uso últimas notícias] toosend localizado notícias mais recentes usando modelos.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="d3cbc-133">Em seu aplicativo da Windows Store:</span><span class="sxs-lookup"><span data-stu-id="d3cbc-133">In your Windows Store app:</span></span>

<span data-ttu-id="d3cbc-134">Altere sua tooinclude MainPage. XAML uma combobox de localidade:</span><span class="sxs-lookup"><span data-stu-id="d3cbc-134">Change your MainPage.xaml tooinclude a locale combobox:</span></span>

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

## <a name="building-hello-windows-store-client-app"></a><span data-ttu-id="d3cbc-135">Criar aplicativo de cliente de armazenamento do Windows hello</span><span class="sxs-lookup"><span data-stu-id="d3cbc-135">Building hello Windows Store client app</span></span>
1. <span data-ttu-id="d3cbc-136">Em sua classe de notificações, adicionar um tooyour de parâmetro de localidade *StoreCategoriesAndSubscribe* e *SubscribeToCateories* métodos.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-136">In your Notifications class, add a locale parameter tooyour  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
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
   
    <span data-ttu-id="d3cbc-137">Observe que, em vez de chamar hello *RegisterNativeAsync* método chamamos *RegisterTemplateAsync*: estamos estiver registrando um formato de notificação específico no qual Olá modelo depende da localidade hello.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-137">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which hello template depends on hello locale.</span></span> <span data-ttu-id="d3cbc-138">Nós também fornecemos um nome para o modelo de saudação ("localizedWNSTemplateExample"), porque que talvez desejemos tooregister mais de um modelo (por exemplo uma notificações do sistema) e outra para blocos e precisamos tooname em ordem tooupdate capaz de toobe ou excluí-los.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-138">We also provide a name for hello template ("localizedWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="d3cbc-139">Observe que, se um dispositivo registra vários modelos com hello mesma marca, uma mensagem de entrada direcionando que marca resultará em várias notificações entregues dispositivo toohello (um para cada modelo).</span><span class="sxs-lookup"><span data-stu-id="d3cbc-139">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="d3cbc-140">Esse comportamento é útil quando hello mesma mensagem lógica tem tooresult em várias notificações visuais, por exemplo, mostrar uma notificação e uma notificação do sistema em um aplicativo da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="d3cbc-140">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="d3cbc-141">Adicione Olá método tooretrieve Olá armazenado local a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3cbc-141">Add hello following method tooretrieve hello stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="d3cbc-142">Em seu MainPage.xaml.cs, o botão Atualizar manipulador de clique por recuperação Olá o valor atual da caixa de combinação de localidade hello e fornecendo classe notificações do toohello chamada toohello, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="d3cbc-142">In your MainPage.xaml.cs, update your button click handler by retrieving hello current value of hello Locale combo box and providing it toohello call toohello Notifications class, as shown:</span></span>
   
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
4. <span data-ttu-id="d3cbc-143">Por fim, do arquivo App.xaml.cs não tooupdate-se de que seu `InitNotificationsAsync` tooretrieve método hello localidade e usá-lo ao assinar:</span><span class="sxs-lookup"><span data-stu-id="d3cbc-143">Finally, in your App.xaml.cs file, make sure tooupdate your `InitNotificationsAsync` method tooretrieve hello locale and use it when subscribing:</span></span>
   
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

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="d3cbc-144">Enviar notificações localizadas de seu back-end</span><span class="sxs-lookup"><span data-stu-id="d3cbc-144">Send localized notifications from your back-end</span></span>
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
