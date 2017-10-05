---
title: "Usar Hubs de notificação para enviar as últimas notícias (Windows Phone)"
description: "Use Hubs de notificação do Azure para usar a etiqueta (marca) nos registros e para enviar as últimas notícias para um aplicativo do Windows Phone."
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
ms.openlocfilehash: 3a6a69bf555c7267d3fbeb03ff6c03054991960f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="2191e-103">Usar hubs de notificação para enviar notícias recentes</span><span class="sxs-lookup"><span data-stu-id="2191e-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="2191e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2191e-104">Overview</span></span>
<span data-ttu-id="2191e-105">Este tópico mostra como usar os Hubs de Notificação do Azure para transmitir notificações de últimas notícias para um aplicativo do Windows Phone 8.0/8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="2191e-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="2191e-106">Se você estiver selecionando o aplicativo da Windows Store ou do Windows Phone 8.1, por favor refira-se à versão [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) .</span><span class="sxs-lookup"><span data-stu-id="2191e-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer to to the [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="2191e-107">Ao concluir, você poderá se registrar nas categorias de últimas notícias que desejar e receber notificações por push apenas para essas categorias.</span><span class="sxs-lookup"><span data-stu-id="2191e-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="2191e-108">Esse cenário é um padrão comum para muitos aplicativos nos quais as notificações precisam ser enviadas para grupos de usuários que tenham anteriormente expressado seu interesse por elas; por ex., leitor de RSS, aplicativos para fãs de música, etc.</span><span class="sxs-lookup"><span data-stu-id="2191e-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="2191e-109">Os cenários de transmissão são habilitados por meio da inclusão de uma ou mais *marcas* durante a criação de um registro no hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="2191e-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="2191e-110">Quando as notificações são enviadas para um rótulo, todos os dispositivos que foram registrados para o rótulo receberão a notificação.</span><span class="sxs-lookup"><span data-stu-id="2191e-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="2191e-111">Como os rótulos são simplesmente cadeias de caracteres, eles não precisam ser provisionados com antecedência.</span><span class="sxs-lookup"><span data-stu-id="2191e-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="2191e-112">Para obter mais informações sobre marcas, consulte [Expressões de Marca e Roteamento dos Hubs de Notificação](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="2191e-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2191e-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2191e-113">Prerequisites</span></span>
<span data-ttu-id="2191e-114">Este tópico se baseia no aplicativo criado em [Introdução aos Hubs de Notificação].</span><span class="sxs-lookup"><span data-stu-id="2191e-114">This topic builds on the app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="2191e-115">Antes de iniciar o tutorial, você deve primeiro concluir a [Introdução aos Hubs de Notificação].</span><span class="sxs-lookup"><span data-stu-id="2191e-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="2191e-116">Adicionar a seleção de categorias ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="2191e-116">Add category selection to the app</span></span>
<span data-ttu-id="2191e-117">A primeira etapa é adicionar os elementos da interface do usuário na página principal existente que permitem ao usuário selecionar categorias para o registro.</span><span class="sxs-lookup"><span data-stu-id="2191e-117">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="2191e-118">As categorias selecionadas por um usuário são armazenadas no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2191e-118">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="2191e-119">Quando o aplicativo é iniciado, o registro do dispositivo é criado no seu hub de notificação com as categorias selecionadas como rótulos.</span><span class="sxs-lookup"><span data-stu-id="2191e-119">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="2191e-120">Abra o arquivo de projeto MainPage.xaml e substitua os elementos **Grid** chamados `TitlePanel` e `ContentPanel` pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="2191e-120">Open the MainPage.xaml project file, then replace the **Grid** elements named `TitlePanel` and `ContentPanel` with the following code:</span></span>
   
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
2. <span data-ttu-id="2191e-121">No projeto, crie uma nova classe denominada **Notificações**, adicione o modificador **público** à definição de classe e depois adicione as seguintes instruções **de uso** para o novo arquivo de código:</span><span class="sxs-lookup"><span data-stu-id="2191e-121">In the project, create a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="2191e-122">Copie o seguinte código para a nova classe **Notificações** :</span><span class="sxs-lookup"><span data-stu-id="2191e-122">Copy the following code into the new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task to complete registration in the ChannelUriUpdated event handler
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
   
                // This is optional, used to receive notifications while the app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete the registrationTask here.  
            // If it is null, the registrationTask will be completed in the ChannelUriUpdated event handler.
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
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // The stored categories tags are passed with the template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used to receive notifications while the app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out the information that was part of the message.
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
   
            // Display a dialog of all the fields in the toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="2191e-123">Essa classe usa o armazenamento isolado para armazenar as categorias de notícias que este dispositivo deverá receber.</span><span class="sxs-lookup"><span data-stu-id="2191e-123">This class uses the isolated storage to store the categories of news that this device is to receive.</span></span> <span data-ttu-id="2191e-124">Além disso, ela contém métodos para se registrar nessas categorias usando um registro de notificações de [modelo](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="2191e-124">It also contains methods to register for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="2191e-125">No arquivo de projeto App.xaml.cs, adicione a propriedade a seguir à classe **Aplicativo** .</span><span class="sxs-lookup"><span data-stu-id="2191e-125">In the App.xaml.cs project file, add the following property to the **App** class.</span></span> <span data-ttu-id="2191e-126">Substitua os espaços reservados `<hub name>` e `<connection string with listen access>` pelo nome de seu hub de notificação e a cadeia de conexão para *DefaultListenSharedAccessSignature* obtidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2191e-126">Replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="2191e-127">Como as credenciais que são distribuídas com um aplicativo cliente não são geralmente seguras, você só deve distribuir a chave para acesso de escuta com o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="2191e-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="2191e-128">O acesso de escuta permite que seu aplicativo se registre para receber notificações, mas os registros existentes não podem ser modificados e as notificações não podem ser enviadas.</span><span class="sxs-lookup"><span data-stu-id="2191e-128">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="2191e-129">A chave de acesso completo é usada em um serviço back-end protegido para enviar notificações e alterar os registros existentes.</span><span class="sxs-lookup"><span data-stu-id="2191e-129">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="2191e-130">Em MainPage.xaml.cs, adicione a seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="2191e-130">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="2191e-131">No arquivo de projeto MainPage.xaml.cs, adicione o seguinte método:</span><span class="sxs-lookup"><span data-stu-id="2191e-131">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
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
   
    <span data-ttu-id="2191e-132">Esse método cria uma lista de categorias e usa a classe **Notificações** para armazenar a lista no armazenamento local e registrar os rótulos correspondentes com o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="2191e-132">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="2191e-133">Quando as categorias são alteradas, o registro é recriado com as novas categorias.</span><span class="sxs-lookup"><span data-stu-id="2191e-133">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="2191e-134">Seu aplicativo agora é capaz de armazenar um conjunto de categorias no armazenamento local do dispositivo e registrar com o hub de notificação, sempre que o usuário alterar a seleção de categorias.</span><span class="sxs-lookup"><span data-stu-id="2191e-134">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="2191e-135">Registrar-se para receber notificações</span><span class="sxs-lookup"><span data-stu-id="2191e-135">Register for notifications</span></span>
<span data-ttu-id="2191e-136">Estas etapas registram com o hub de notificação na inicialização, usando as categorias que foram armazenadas no armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="2191e-136">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="2191e-137">Como o URI do canal atribuído pelo MPNS (Serviço de Notificação por Push da Microsoft) pode mudar a qualquer momento, você deve se registrar para receber notificações com frequência para evitar falhas de notificação.</span><span class="sxs-lookup"><span data-stu-id="2191e-137">Because the channel URI assigned by the Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="2191e-138">Este exemplo registra notificações cada vez que o aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="2191e-138">This example registers for notifications every time that the app starts.</span></span> <span data-ttu-id="2191e-139">Para os aplicativos que são executados com frequência, mais de uma vez por dia, é possível ignorar o registro para preservar a largura de banda se tiver passado menos de um dia desde o registro anterior.</span><span class="sxs-lookup"><span data-stu-id="2191e-139">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="2191e-140">Abra o arquivo App.xaml.cs e adicione o modificador **async** ao método **Application_Launching** localize e substitua o código do registro de Hubs de Notificação que você adicionou na [Introdução aos Hubs de Notificação] pela seguinte linha de código:</span><span class="sxs-lookup"><span data-stu-id="2191e-140">Open the App.xaml.cs file and add the **async** modifier to **Application_Launching** method and replace the Notification Hubs registration code that you added in [Get started with Notification Hubs] with the following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="2191e-141">Isso garante que o aplicativo recupere as categorias do armazenamento local e solicite um registro para essas categorias toda vez que ele for iniciado.</span><span class="sxs-lookup"><span data-stu-id="2191e-141">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="2191e-142">No arquivo de projeto MainPage.xaml.cs, adicione o seguinte código que implementa o método **OnNavigatedTo** :</span><span class="sxs-lookup"><span data-stu-id="2191e-142">In the MainPage.xaml.cs project file, add the following code that implements the **OnNavigatedTo** method:</span></span>
   
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
   
    <span data-ttu-id="2191e-143">Isso atualiza a página principal com base no status de categorias salvas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2191e-143">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="2191e-144">O aplicativo agora está completo e pode armazenar um conjunto de categorias no armazenamento local do dispositivo utilizado para registrá-las com o hub de notificação, sempre que o usuário alterar a seleção de categorias.</span><span class="sxs-lookup"><span data-stu-id="2191e-144">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="2191e-145">Em seguida, definiremos um back-end que possa enviar notificações de categoria para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2191e-145">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="2191e-146">Enviando notificações marcadas</span><span class="sxs-lookup"><span data-stu-id="2191e-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="2191e-147">Executar o aplicativo e gerar notificações</span><span class="sxs-lookup"><span data-stu-id="2191e-147">Run the app and generate notifications</span></span>
1. <span data-ttu-id="2191e-148">No Visual Studio, pressione F5 para compilar e iniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2191e-148">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="2191e-149">Observe que a interface do usuário do aplicativo fornece um conjunto de alternâncias que permite escolher as categorias nas quais você poderá assinar.</span><span class="sxs-lookup"><span data-stu-id="2191e-149">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="2191e-150">Habilite uma ou mais alternâncias de categorias e depois clique em **Assinar**.</span><span class="sxs-lookup"><span data-stu-id="2191e-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="2191e-151">O aplicativo converte as categorias selecionadas em rótulos e solicita um novo registro do dispositivo para os rótulos selecionados do hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="2191e-151">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="2191e-152">As categorias registradas são retornadas e exibidas em uma caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2191e-152">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="2191e-153">Depois de receber uma confirmação de que a assinatura de suas categorias está concluída, execute o aplicativo de console para enviar notificações para cada categoria.</span><span class="sxs-lookup"><span data-stu-id="2191e-153">After receiving a confirmation that your categories were subscription completed, run the console app to send notifications for each categories.</span></span> <span data-ttu-id="2191e-154">Confirme que você receba apenas uma notificação para as categorias nas quais você se inscreveu.</span><span class="sxs-lookup"><span data-stu-id="2191e-154">Verify you only receive a notification for the categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="2191e-155">Você concluiu este tópico.</span><span class="sxs-lookup"><span data-stu-id="2191e-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how to broadcast breaking news by category. Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs to broadcast localized breaking news]

    Learn how to expand the breaking news app to enable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how to push notifications to specific authenticated users. This is a good solution for sending notifications only to specific users.
-->

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
<span data-ttu-id="2191e-156">[Introdução aos Hubs de Notificação]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span><span class="sxs-lookup"><span data-stu-id="2191e-156">[Get started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span></span>
[Use Notification Hubs to broadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Phone]: ??

