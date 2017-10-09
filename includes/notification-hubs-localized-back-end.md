



Quando você enviar notificações de modelo, que você só precisa de um conjunto de propriedades de tooprovide, em nosso caso enviaremos conjunto Olá das propriedades que contém a versão localizada de saudação do hello notícias, por exemplo:

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


Esta seção mostra como toosend notificações usando um aplicativo de console

Olá incluído código difusões tooboth Windows Store e dispositivos iOS, pois Olá back-end pode transmitir tooany de dispositivos de saudação com suporte.

### <a name="toosend-notifications-using-a-c-console-app"></a>notificações de toosend usando um aplicativo de console c#
Modificar Olá `SendTemplateNotificationAsync` método no aplicativo de console Olá criado anteriormente com hello código a seguir. Observe como neste caso, há toosend sem necessidade de várias notificações para localidades diferentes e plataformas.

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


Observe que essa chamada simple fornecer informação localizada Olá notícias muito**todos os** seus dispositivos, independentemente da plataforma hello, como o Hub de notificação desenvolve e fornece Olá correto de dispositivos de saudação tooall carga nativo assinado tooa de marca específica.

### <a name="sending-hello-notification-with-mobile-services"></a>Enviar notificação de saudação com serviços móveis
No Agendador seu serviço móvel, você pode usar o hello script a seguir:

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


