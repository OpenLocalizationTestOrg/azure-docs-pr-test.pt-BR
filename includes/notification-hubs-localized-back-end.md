



<span data-ttu-id="b721e-101">Quando você enviar notificações de modelo, que você só precisa de um conjunto de propriedades de tooprovide, em nosso caso enviaremos conjunto Olá das propriedades que contém a versão localizada de saudação do hello notícias, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b721e-101">When you send template notifications you only need tooprovide a set of properties, in our case we will send hello set of properties containing hello localized version of hello current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="b721e-102">Esta seção mostra como toosend notificações usando um aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="b721e-102">This section shows how toosend notifications using a console app</span></span>

<span data-ttu-id="b721e-103">Olá incluído código difusões tooboth Windows Store e dispositivos iOS, pois Olá back-end pode transmitir tooany de dispositivos de saudação com suporte.</span><span class="sxs-lookup"><span data-stu-id="b721e-103">hello included code broadcasts tooboth Windows Store and iOS devices, since hello backend can broadcast tooany of hello supported devices.</span></span>

### <a name="toosend-notifications-using-a-c-console-app"></a><span data-ttu-id="b721e-104">notificações de toosend usando um aplicativo de console c#</span><span class="sxs-lookup"><span data-stu-id="b721e-104">toosend notifications using a C# console app</span></span>
<span data-ttu-id="b721e-105">Modificar Olá `SendTemplateNotificationAsync` método no aplicativo de console Olá criado anteriormente com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="b721e-105">Modify hello `SendTemplateNotificationAsync` method in hello console app you previously created with hello following code.</span></span> <span data-ttu-id="b721e-106">Observe como neste caso, há toosend sem necessidade de várias notificações para localidades diferentes e plataformas.</span><span class="sxs-lookup"><span data-stu-id="b721e-106">Notice how in this case there is no need toosend multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending hello notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and hello proper tags will receive hello notifications. 
            // This includes APNS, GCM, WNS, and MPNS template registrations.
            Dictionary<string, string> templateParams = new Dictionary<string, string>();

            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};
            var locales = new string[] { "English", "French", "Mandarin" };

            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";

                // Sending localized News for each tag too...
                foreach( var locale in locales)
                {
                    string key = "News_" + locale;

                    // Your real localized news content would go here.
                    templateParams[key] = "Breaking " + category + " News in " + locale + "!";
                }

                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
        }


<span data-ttu-id="b721e-107">Observe que essa chamada simple fornecer informação localizada Olá notícias muito**todos os** seus dispositivos, independentemente da plataforma hello, como o Hub de notificação desenvolve e fornece Olá correto de dispositivos de saudação tooall carga nativo assinado tooa de marca específica.</span><span class="sxs-lookup"><span data-stu-id="b721e-107">Note that this simple call will deliver hello localized piece of news too**all** your devices, irrespective of hello platform, as your Notification Hub builds and delivers hello correct native payload tooall hello devices subscribed tooa specific tag.</span></span>

### <a name="sending-hello-notification-with-mobile-services"></a><span data-ttu-id="b721e-108">Enviar notificação de saudação com serviços móveis</span><span class="sxs-lookup"><span data-stu-id="b721e-108">Sending hello notification with Mobile Services</span></span>
<span data-ttu-id="b721e-109">No Agendador seu serviço móvel, você pode usar o hello script a seguir:</span><span class="sxs-lookup"><span data-stu-id="b721e-109">In your Mobile Service scheduler, you can use hello following script:</span></span>

    var azure = require('azure');
    var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string with full access>');
    var notification = {
            "News_English": "World News in English!",
            "News_French": "World News in French!",
            "News_Mandarin", "World News in Mandarin!"
    }
    notificationHubService.send('World', notification, function(error) {
        if (!error) {
            console.warn("Notification successful");
        }
    });


