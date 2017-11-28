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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="6323a-103">Usar Hubs de notificação toosend últimas notícias</span><span class="sxs-lookup"><span data-stu-id="6323a-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="6323a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6323a-104">Overview</span></span>
<span data-ttu-id="6323a-105">Este tópico mostra como toouse Hubs de notificação do Azure toobroadcast últimas notícias notificações tooa Windows Store ou aplicativo do Windows Phone 8.1 (não Silverlight).</span><span class="sxs-lookup"><span data-stu-id="6323a-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="6323a-106">Se você estiver direcionando o Windows Phone 8.1 Silverlight, consulte toohello [do Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) versão.</span><span class="sxs-lookup"><span data-stu-id="6323a-106">If you are targeting Windows Phone 8.1 Silverlight, please refer toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="6323a-107">Ao concluir, será ser capaz de tooregister para quebrar novas categorias que você está interessado e receber notificações de envio apenas para essas categorias.</span><span class="sxs-lookup"><span data-stu-id="6323a-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="6323a-108">Esse cenário é um padrão comum para muitos aplicativos onde notificações têm toogroups toobe enviada de usuários que têm sido declarado anteriormente interesse em-los, por exemplo, leitor de RSS, aplicativos para ventiladores de música e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="6323a-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="6323a-109">Cenários de transmissão são habilitados, incluindo um ou mais *marcas* ao criar um registro no hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6323a-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="6323a-110">Quando as notificações são enviadas tooa marca, todos os dispositivos que foram registrados para marca de saudação receberão a notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6323a-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="6323a-111">Como as marcas são simplesmente cadeias de caracteres, eles não têm toobe provisionado com antecedência.</span><span class="sxs-lookup"><span data-stu-id="6323a-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="6323a-112">Para obter mais informações sobre marcas, consulte muito[expressões de marca e roteamento de Hubs de notificação](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="6323a-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6323a-113">Windows Store e a versão de projetos do Windows Phone 8.1 e versões anteriores não têm suporte no Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="6323a-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="6323a-114">Para saber mais, confira [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="6323a-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6323a-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6323a-115">Prerequisites</span></span>
<span data-ttu-id="6323a-116">Este tópico se baseia no aplicativo hello criado na [começar com Hubs de notificação][get-started].</span><span class="sxs-lookup"><span data-stu-id="6323a-116">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="6323a-117">Antes de iniciar o tutorial, você deve primeiro concluir a [Introdução aos Hubs de Notificação][get-started].</span><span class="sxs-lookup"><span data-stu-id="6323a-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="6323a-118">Adicionar aplicativo de toohello de seleção de categoria</span><span class="sxs-lookup"><span data-stu-id="6323a-118">Add category selection toohello app</span></span>
<span data-ttu-id="6323a-119">Olá primeira etapa é tooadd Olá da interface do usuário tooyour existente principal página de elementos que permitem Olá usuário tooselect categorias tooregister.</span><span class="sxs-lookup"><span data-stu-id="6323a-119">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="6323a-120">categorias de saudação selecionadas por um usuário são armazenadas no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6323a-120">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="6323a-121">Quando o aplicativo hello é iniciado, um registro de dispositivo é criado em seu hub de notificação com categorias de saudação selecionada como marcas.</span><span class="sxs-lookup"><span data-stu-id="6323a-121">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="6323a-122">Abra o arquivo de projeto do hello MainPage. XAML e Olá cópia Olá código a seguir **grade** elemento:</span><span class="sxs-lookup"><span data-stu-id="6323a-122">Open hello MainPage.xaml project file, then copy hello following code in hello **Grid** element:</span></span>
   
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
2. <span data-ttu-id="6323a-123">Olá clique com botão direito **compartilhado** do projeto e adicione uma nova classe chamada **notificações**, adicionar Olá **pública** modificador toohello definição da classe, em seguida, adicionar Olá após **usando** instruções toohello novo arquivo de código:</span><span class="sxs-lookup"><span data-stu-id="6323a-123">Right click hello **Shared** project and add a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="6323a-124">De código a seguir de saudação de cópia em Olá novo **notificações** classe:</span><span class="sxs-lookup"><span data-stu-id="6323a-124">Copy hello following code into hello new **Notifications** class:</span></span>
   
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
   
    <span data-ttu-id="6323a-125">Essa classe usa categorias de saudação do hello armazenamento local toostore de notícias este dispositivo tem tooreceive.</span><span class="sxs-lookup"><span data-stu-id="6323a-125">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="6323a-126">Observe que, em vez de chamar hello *RegisterNativeAsync* método chamamos *RegisterTemplateAsync* tooregister para categorias de saudação usando um registro do modelo.</span><span class="sxs-lookup"><span data-stu-id="6323a-126">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync* tooregister for hello categories using a template registration.</span></span> 
   
    <span data-ttu-id="6323a-127">Nós também fornecemos um nome para o modelo de saudação ("simpleWNSTemplateExample"), porque que talvez desejemos tooregister mais de um modelo (por exemplo uma notificações do sistema) e outra para blocos e precisamos tooname em ordem tooupdate capaz de toobe ou excluí-los.</span><span class="sxs-lookup"><span data-stu-id="6323a-127">We also provide a name for hello template ("simpleWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="6323a-128">Observe que, se um dispositivo registra vários modelos com hello mesma marca, uma mensagem de entrada direcionando que marca resultará em várias notificações entregues dispositivo toohello (um para cada modelo).</span><span class="sxs-lookup"><span data-stu-id="6323a-128">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="6323a-129">Esse comportamento é útil quando hello mesma mensagem lógica tem tooresult em várias notificações visuais, por exemplo, mostrar uma notificação e uma notificação do sistema em um aplicativo da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="6323a-129">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="6323a-130">Para obter mais informações sobre o uso de modelos, consulte [Modelos](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="6323a-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="6323a-131">No arquivo de projeto App.xaml.cs hello, adicionar Olá toohello de propriedade a seguir **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="6323a-131">In hello App.xaml.cs project file, add hello following property toohello **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="6323a-132">Esta propriedade é usada toocreate e acesso uma **notificações** instância.</span><span class="sxs-lookup"><span data-stu-id="6323a-132">This property is used toocreate and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="6323a-133">Olá acima código, substitua Olá `<hub name>` e `<connection string with listen access>` espaços reservados com seu hub nome e hello conexão cadeia de notificação para *DefaultListenSharedAccessSignature* que você obteve anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6323a-133">In hello above code, replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6323a-134">Porque as credenciais que são distribuídas com um aplicativo cliente não são seguras em geral, você só deve distribuir chave Olá para acesso de escuta com o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="6323a-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="6323a-135">Escutar permite acesso que tooregister seu aplicativo para notificações, mas os registros existentes não pode ser modificada e não não possível enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="6323a-135">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="6323a-136">chave de acesso completo de saudação é usada em um serviço de back-end seguro para enviar notificações e alterar os registros existentes.</span><span class="sxs-lookup"><span data-stu-id="6323a-136">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="6323a-137">Em seu MainPage.xaml.cs, adicione Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="6323a-137">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="6323a-138">No arquivo de projeto MainPage.xaml.cs hello, adicione Olá método a seguir:</span><span class="sxs-lookup"><span data-stu-id="6323a-138">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="6323a-139">Esse método cria uma lista de categorias e usa Olá **notificações** classe toostore lista de saudação no armazenamento local hello e registre marcas correspondentes Olá com seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="6323a-139">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="6323a-140">Quando as categorias são alteradas, registro de saudação é recriado com novas categorias de saudação.</span><span class="sxs-lookup"><span data-stu-id="6323a-140">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="6323a-141">Seu aplicativo agora é capaz de toostore um conjunto de categorias no armazenamento local no dispositivo hello e registrar com o hub de notificação Olá sempre que as alterações do usuário Olá Olá seleção de categorias.</span><span class="sxs-lookup"><span data-stu-id="6323a-141">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="6323a-142">Registrar-se para receber notificações</span><span class="sxs-lookup"><span data-stu-id="6323a-142">Register for notifications</span></span>
<span data-ttu-id="6323a-143">Estas etapas se registrar com o hub de notificação de saudação na inicialização usando as categorias de saudação que foram armazenadas no armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="6323a-143">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="6323a-144">Como canal Olá URI atribuído pelo Olá serviço de notificação do Windows (WNS) pode ser alterado a qualquer momento, você deve registrar para notificações frequentemente tooavoid falhas de notificação.</span><span class="sxs-lookup"><span data-stu-id="6323a-144">Because hello channel URI assigned by hello Windows Notification Service (WNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="6323a-145">Este exemplo registra para notificação sempre que o aplicativo hello for iniciado.</span><span class="sxs-lookup"><span data-stu-id="6323a-145">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="6323a-146">Para aplicativos que são executados com frequência, mais de uma vez por dia, você poderá provavelmente Ignorar largura de banda do registro toopreserve se menos de um dia se passou desde o registro anterior hello.</span><span class="sxs-lookup"><span data-stu-id="6323a-146">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="6323a-147">Saudação de arquivo e atualização App.xaml.cs Olá abrir **InitNotificationsAsync** saudação do método toouse `notifications` toosubscribe classe baseadas em categorias.</span><span class="sxs-lookup"><span data-stu-id="6323a-147">Open hello App.xaml.cs file and update hello **InitNotificationsAsync** method toouse hello `notifications` class toosubscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="6323a-148">Isso torna-se de que sempre que o aplicativo hello é iniciado, ele recupera as categorias de saudação do armazenamento local e solicita um registro para estas categorias.</span><span class="sxs-lookup"><span data-stu-id="6323a-148">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="6323a-149">Olá **InitNotificationsAsync** método foi criado como parte da saudação [começar com Hubs de notificação] [ get-started] tutorial.</span><span class="sxs-lookup"><span data-stu-id="6323a-149">hello **InitNotificationsAsync** method was created as part of hello [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="6323a-150">No arquivo de projeto MainPage.xaml.cs hello, adicionar Olá toohello de código a seguir *OnNavigatedTo* método:</span><span class="sxs-lookup"><span data-stu-id="6323a-150">In hello MainPage.xaml.cs project file, add hello following code toohello *OnNavigatedTo* method:</span></span>
   
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
   
    <span data-ttu-id="6323a-151">Esta página principal do hello atualizações com base no status de saudação do previamente salvo categorias.</span><span class="sxs-lookup"><span data-stu-id="6323a-151">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="6323a-152">aplicativo Hello agora está concluído e pode armazenar um conjunto de categorias em Olá dispositivo local de armazenamento usado tooregister com o hub de notificação Olá sempre que as alterações do usuário Olá Olá seleção de categorias.</span><span class="sxs-lookup"><span data-stu-id="6323a-152">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="6323a-153">Em seguida, definiremos um back-end que pode enviar categoria notificações toothis aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6323a-153">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="6323a-154">Enviando notificações marcadas</span><span class="sxs-lookup"><span data-stu-id="6323a-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="6323a-155">Execute o aplicativo hello e geram notificações</span><span class="sxs-lookup"><span data-stu-id="6323a-155">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="6323a-156">No Visual Studio, pressione F5 toocompile e iniciar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6323a-156">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="6323a-157">Observe que o aplicativo hello de que interface do usuário fornece um conjunto alterna que permite que você escolha Olá categorias toosubscribe para.</span><span class="sxs-lookup"><span data-stu-id="6323a-157">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="6323a-158">Habilite uma ou mais alternâncias de categorias e depois clique em **Assinar**.</span><span class="sxs-lookup"><span data-stu-id="6323a-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="6323a-159">aplicativo Hello converte categorias Olá selecionado em marcas e solicita um novo registro de dispositivo para marcas de saudação selecionada do hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6323a-159">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="6323a-160">Olá categorias registradas são retornadas e exibidas em uma caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6323a-160">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="6323a-161">Envie uma nova notificação de saudação back-end em uma saudação maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="6323a-161">Send a new notification from hello backend in one of hello following ways:</span></span>
   
   * <span data-ttu-id="6323a-162">**Aplicativo de console:** iniciar o aplicativo de console hello.</span><span class="sxs-lookup"><span data-stu-id="6323a-162">**Console app:** start hello console app.</span></span>
   * <span data-ttu-id="6323a-163">**Java/PHP:** execute seu aplicativo/script.</span><span class="sxs-lookup"><span data-stu-id="6323a-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="6323a-164">As notificações para categorias de saudação selecionada aparecem como notificações do sistema.</span><span class="sxs-lookup"><span data-stu-id="6323a-164">Notifications for hello selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="6323a-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6323a-165">Next steps</span></span>
<span data-ttu-id="6323a-166">Neste tutorial, nós aprendemos como toobroadcast últimas notícias por categoria.</span><span class="sxs-lookup"><span data-stu-id="6323a-166">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="6323a-167">Considere a concluir uma saudação tutoriais que realçam outros cenários avançados de Hubs de notificação a seguir:</span><span class="sxs-lookup"><span data-stu-id="6323a-167">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="6323a-168">[Use as notícias mais recentes toobroadcast localizada de Hubs de notificação]</span><span class="sxs-lookup"><span data-stu-id="6323a-168">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="6323a-169">Saiba como Olá tooexpand últimas notícias aplicativo tooenable enviar localizado notificações.</span><span class="sxs-lookup"><span data-stu-id="6323a-169">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

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
