



<span data-ttu-id="2f344-101">Ao enviar notificações de modelos, você só precisa fornecer um conjunto de propriedades. No nosso caso, enviaremos o conjunto de propriedades contendo a versão localizada das notícias atuais, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2f344-101">When you send template notifications you only need to provide a set of properties, in our case we will send the set of properties containing the localized version of the current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="2f344-102">Esta seção mostra como enviar notificações usando um aplicativo do console</span><span class="sxs-lookup"><span data-stu-id="2f344-102">This section shows how to send notifications using a console app</span></span>

<span data-ttu-id="2f344-103">O código incluído transmite a dispositivos Windows Store e iOS, como o back-end pode transmitir para qualquer um dos dispositivos com suporte.</span><span class="sxs-lookup"><span data-stu-id="2f344-103">The included code broadcasts to both Windows Store and iOS devices, since the backend can broadcast to any of the supported devices.</span></span>

### <a name="to-send-notifications-using-a-c-console-app"></a><span data-ttu-id="2f344-104">Para enviar notificações usando um aplicativo de console C#</span><span class="sxs-lookup"><span data-stu-id="2f344-104">To send notifications using a C# console app</span></span>
<span data-ttu-id="2f344-105">Modifique o método `SendTemplateNotificationAsync` no aplicativo de console que você criou anteriormente, com o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="2f344-105">Modify the `SendTemplateNotificationAsync` method in the console app you previously created with the following code.</span></span> <span data-ttu-id="2f344-106">Observe como nesse caso não é necessário enviar várias notificações para localidades e plataformas diferentes.</span><span class="sxs-lookup"><span data-stu-id="2f344-106">Notice how in this case there is no need to send multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define the notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending the notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and the proper tags will receive the notifications. 
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


<span data-ttu-id="2f344-107">Observe que esta simples chamada entregará a notícia correta localizada a **todos** os dispositivos, independentemente da plataforma, enquanto o Hub de Notificação cria e entrega a carga de trabalho nativa correta a todos os dispositivos inscritos em uma marca específica.</span><span class="sxs-lookup"><span data-stu-id="2f344-107">Note that this simple call will deliver the localized piece of news to **all** your devices, irrespective of the platform, as your Notification Hub builds and delivers the correct native payload to all the devices subscribed to a specific tag.</span></span>

### <a name="sending-the-notification-with-mobile-services"></a><span data-ttu-id="2f344-108">Enviando a notificação com Serviços Móveis</span><span class="sxs-lookup"><span data-stu-id="2f344-108">Sending the notification with Mobile Services</span></span>
<span data-ttu-id="2f344-109">No Agendador de serviço móvel, você pode usar o script a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f344-109">In your Mobile Service scheduler, you can use the following script:</span></span>

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


