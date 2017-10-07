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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="ac7cb-103">Usar Hubs de notificação toosend últimas notícias</span><span class="sxs-lookup"><span data-stu-id="ac7cb-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="ac7cb-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ac7cb-104">Overview</span></span>
<span data-ttu-id="ac7cb-105">Este tópico mostra como Hubs de notificação do Azure toouse toobroadcast últimas notícias notificações tooa Windows Phone 8.0/8.1 Silverlight aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="ac7cb-106">Se você estiver direcionando da Windows Store ou aplicativo do Windows Phone 8.1, consulte tootoohello [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) versão.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer tootoohello [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="ac7cb-107">Ao concluir, será ser capaz de tooregister para quebrar novas categorias que você está interessado e receber notificações de envio apenas para essas categorias.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="ac7cb-108">Esse cenário é um padrão comum para muitos aplicativos onde notificações têm toogroups toobe enviada de usuários que têm sido declarado anteriormente interesse neles, por exemplo, o leitor de RSS, aplicativos para ventiladores de música, etc.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="ac7cb-109">Cenários de transmissão são habilitados, incluindo um ou mais *marcas* ao criar um registro no hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="ac7cb-110">Quando as notificações são enviadas tooa marca, todos os dispositivos que foram registrados para marca de saudação receberão a notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="ac7cb-111">Como as marcas são simplesmente cadeias de caracteres, eles não têm toobe provisionado com antecedência.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="ac7cb-112">Para obter mais informações sobre marcas, consulte muito[expressões de marca e roteamento de Hubs de notificação](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="ac7cb-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac7cb-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ac7cb-113">Prerequisites</span></span>
<span data-ttu-id="ac7cb-114">Este tópico se baseia no aplicativo hello criado na [começar com Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="ac7cb-114">This topic builds on hello app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="ac7cb-115">Antes de iniciar o tutorial, você deve primeiro concluir a [começar com Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="ac7cb-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="ac7cb-116">Adicionar aplicativo de toohello de seleção de categoria</span><span class="sxs-lookup"><span data-stu-id="ac7cb-116">Add category selection toohello app</span></span>
<span data-ttu-id="ac7cb-117">Olá primeira etapa é tooadd Olá da interface do usuário tooyour existente principal página de elementos que permitem Olá usuário tooselect categorias tooregister.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-117">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="ac7cb-118">categorias de saudação selecionadas por um usuário são armazenadas no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-118">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="ac7cb-119">Quando o aplicativo hello é iniciado, um registro de dispositivo é criado em seu hub de notificação com categorias de saudação selecionada como marcas.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-119">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="ac7cb-120">Abrir o arquivo de projeto do hello MainPage. XAML e substitua Olá **grade** elementos nomeados `TitlePanel` e `ContentPanel` com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac7cb-120">Open hello MainPage.xaml project file, then replace hello **Grid** elements named `TitlePanel` and `ContentPanel` with hello following code:</span></span>
   
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
2. <span data-ttu-id="ac7cb-121">No projeto de hello, crie uma nova classe chamada **notificações**, adicionar Olá **pública** toohello modificador definição da classe e adicione o seguinte Olá **usando** instruções toohello novo arquivo de código:</span><span class="sxs-lookup"><span data-stu-id="ac7cb-121">In hello project, create a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="ac7cb-122">De código a seguir de saudação de cópia em Olá novo **notificações** classe:</span><span class="sxs-lookup"><span data-stu-id="ac7cb-122">Copy hello following code into hello new **Notifications** class:</span></span>
   
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

    <span data-ttu-id="ac7cb-123">Essa classe usa hello isolado armazenamento toostore Olá categorias de notícias este dispositivo está tooreceive.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-123">This class uses hello isolated storage toostore hello categories of news that this device is tooreceive.</span></span> <span data-ttu-id="ac7cb-124">Ele também contém métodos tooregister para estas categorias usando uma [modelo](notification-hubs-templates-cross-platform-push-messages.md) registro de notificação.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-124">It also contains methods tooregister for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="ac7cb-125">No arquivo de projeto App.xaml.cs hello, adicionar Olá toohello de propriedade a seguir **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-125">In hello App.xaml.cs project file, add hello following property toohello **App** class.</span></span> <span data-ttu-id="ac7cb-126">Substituir saudação `<hub name>` e `<connection string with listen access>` espaços reservados com seu hub nome e hello conexão cadeia de notificação para *DefaultListenSharedAccessSignature* que você obteve anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-126">Replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="ac7cb-127">Porque as credenciais que são distribuídas com um aplicativo cliente não são seguras em geral, você só deve distribuir chave Olá para acesso de escuta com o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="ac7cb-128">Escutar permite acesso que tooregister seu aplicativo para notificações, mas os registros existentes não pode ser modificada e não não possível enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-128">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="ac7cb-129">chave de acesso completo de saudação é usada em um serviço de back-end seguro para enviar notificações e alterar os registros existentes.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-129">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="ac7cb-130">Em seu MainPage.xaml.cs, adicione Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="ac7cb-130">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="ac7cb-131">No arquivo de projeto MainPage.xaml.cs hello, adicione Olá método a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac7cb-131">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="ac7cb-132">Esse método cria uma lista de categorias e usa Olá **notificações** classe toostore lista de saudação no armazenamento local hello e registre marcas correspondentes Olá com seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-132">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="ac7cb-133">Quando as categorias são alteradas, registro de saudação é recriado com novas categorias de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-133">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="ac7cb-134">Seu aplicativo agora é capaz de toostore um conjunto de categorias no armazenamento local no dispositivo hello e registrar com o hub de notificação Olá sempre que as alterações do usuário Olá Olá seleção de categorias.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-134">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="ac7cb-135">Registrar-se para receber notificações</span><span class="sxs-lookup"><span data-stu-id="ac7cb-135">Register for notifications</span></span>
<span data-ttu-id="ac7cb-136">Estas etapas se registrar com o hub de notificação de saudação na inicialização usando as categorias de saudação que foram armazenadas no armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-136">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="ac7cb-137">Como canal Olá URI atribuído pelo Olá serviço de notificação por Push da Microsoft (MPNS) pode ser alterado a qualquer momento, você deve registrar para notificações frequentemente tooavoid falhas de notificação.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-137">Because hello channel URI assigned by hello Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="ac7cb-138">Este exemplo registra para notificações sempre que o aplicativo hello for iniciado.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-138">This example registers for notifications every time that hello app starts.</span></span> <span data-ttu-id="ac7cb-139">Para aplicativos que são executados com frequência, mais de uma vez por dia, você poderá provavelmente Ignorar largura de banda do registro toopreserve se menos de um dia se passou desde o registro anterior hello.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-139">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="ac7cb-140">Abrir o arquivo de App.xaml.cs hello e adicione Olá **async** modificador muito**Application_Launching** método e substituir Olá Hubs de notificação código de registro que você adicionou na [começar com Hubs de notificação] com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac7cb-140">Open hello App.xaml.cs file and add hello **async** modifier too**Application_Launching** method and replace hello Notification Hubs registration code that you added in [Get started with Notification Hubs] with hello following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="ac7cb-141">Isso torna-se de que sempre que o aplicativo hello é iniciado, ele recupera as categorias de saudação do armazenamento local e solicita um registro para estas categorias.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-141">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="ac7cb-142">No arquivo de projeto MainPage.xaml.cs hello, adicionar Olá seguindo o código que implementa Olá **OnNavigatedTo** método:</span><span class="sxs-lookup"><span data-stu-id="ac7cb-142">In hello MainPage.xaml.cs project file, add hello following code that implements hello **OnNavigatedTo** method:</span></span>
   
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
   
    <span data-ttu-id="ac7cb-143">Esta página principal do hello atualizações com base no status de saudação do previamente salvo categorias.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-143">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="ac7cb-144">aplicativo Hello agora está concluído e pode armazenar um conjunto de categorias em Olá dispositivo local de armazenamento usado tooregister com o hub de notificação Olá sempre que as alterações do usuário Olá Olá seleção de categorias.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-144">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="ac7cb-145">Em seguida, definiremos um back-end que pode enviar categoria notificações toothis aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-145">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="ac7cb-146">Enviando notificações marcadas</span><span class="sxs-lookup"><span data-stu-id="ac7cb-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="ac7cb-147">Execute o aplicativo hello e geram notificações</span><span class="sxs-lookup"><span data-stu-id="ac7cb-147">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="ac7cb-148">No Visual Studio, pressione F5 toocompile e iniciar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-148">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="ac7cb-149">Observe que o aplicativo hello de que interface do usuário fornece um conjunto alterna que permite que você escolha Olá categorias toosubscribe para.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-149">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="ac7cb-150">Habilite uma ou mais alternâncias de categorias e depois clique em **Assinar**.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="ac7cb-151">aplicativo Hello converte categorias Olá selecionado em marcas e solicita um novo registro de dispositivo para marcas de saudação selecionada do hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-151">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="ac7cb-152">Olá categorias registradas são retornadas e exibidas em uma caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-152">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="ac7cb-153">Depois de receber uma confirmação de que suas categorias foram assinatura concluída, execute notificações de toosend de aplicativo hello console para cada categorias.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-153">After receiving a confirmation that your categories were subscription completed, run hello console app toosend notifications for each categories.</span></span> <span data-ttu-id="ac7cb-154">Verifique se que você só receberá uma notificação para categorias de saudação que você se inscreveu.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-154">Verify you only receive a notification for hello categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="ac7cb-155">Você concluiu este tópico.</span><span class="sxs-lookup"><span data-stu-id="ac7cb-155">You have completed this topic.</span></span>

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

