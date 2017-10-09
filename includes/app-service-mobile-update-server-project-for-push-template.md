<span data-ttu-id="724d8-101">Nesta seção, você atualizar código no seu toosend de projeto de back-end de aplicativos móveis existente uma notificação por push sempre que um novo item é adicionado.</span><span class="sxs-lookup"><span data-stu-id="724d8-101">In this section, you update code in your existing Mobile Apps back-end project toosend a push notification every time a new item is added.</span></span> <span data-ttu-id="724d8-102">Isso é alimentado por Olá [modelo](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) recurso de Hubs de notificação do Azure, permitindo que os envios de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="724d8-102">This is powered by hello [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="724d8-103">Olá vários clientes são registrados para notificações por push usando modelos, e um envio por push universal único pode receber tooall plataformas de cliente.</span><span class="sxs-lookup"><span data-stu-id="724d8-103">hello various clients are registered for push notifications using templates, and a single universal push can get tooall client platforms.</span></span>

<span data-ttu-id="724d8-104">Escolha uma saudação procedimentos a seguir que corresponde ao tipo de projeto de back-end&mdash;ou [.NET back-end](#dotnet) ou [Node. js back-end](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="724d8-104">Choose one of hello following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="724d8-105"><a name="dotnet"></a>Projeto de back-end do .NET</span><span class="sxs-lookup"><span data-stu-id="724d8-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="724d8-106">No Visual Studio, clique com botão direito Olá servidor e clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="724d8-106">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="724d8-107">Procure `Microsoft.Azure.NotificationHubs` e então clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="724d8-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="724d8-108">Isso instala a biblioteca de Hubs de notificação hello para enviar notificações de back-end.</span><span class="sxs-lookup"><span data-stu-id="724d8-108">This installs hello Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="724d8-109">No projeto do servidor de saudação, abra **controladores** > **TodoItemController.cs**e adicione Olá seguinte usando instruções:</span><span class="sxs-lookup"><span data-stu-id="724d8-109">In hello server project, open **Controllers** > **TodoItemController.cs**, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="724d8-110">Em Olá **PostTodoItem** método, adicione Olá código a seguir após a chamada de saudação muito**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="724d8-110">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>  

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending hello message so that all template registrations that contain "messageParam"
        // will receive hello notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added toohello list.";

        try
        {
            // Send hello push notification and log hello results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="724d8-111">Isso envia uma notificação de modelo que contém o item de saudação. Texto quando um novo item é inserido.</span><span class="sxs-lookup"><span data-stu-id="724d8-111">This sends a template notification that contains hello item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="724d8-112">Republicar o projeto do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="724d8-112">Republish hello server project.</span></span>

### <span data-ttu-id="724d8-113"><a name="nodejs"></a>Projeto de back-end do Node.js</span><span class="sxs-lookup"><span data-stu-id="724d8-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="724d8-114">Se você ainda não fez isso, [baixar o projeto de back-end de início rápido de saudação](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), ou use outro Olá [editor online no portal do Azure de saudação](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="724d8-114">If you haven't already done so, [download hello quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="724d8-115">Substitua o código existente de saudação em todoitem.js com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="724d8-115">Replace hello existing code in todoitem.js with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a template notification.
                    context.push.send(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="724d8-116">Isso envia uma notificação de modelo que contém a saudação item.text quando um novo item é inserido.</span><span class="sxs-lookup"><span data-stu-id="724d8-116">This sends a template notification that contains hello item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="724d8-117">Ao editar o arquivo hello no computador local, republicar o projeto do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="724d8-117">When editing hello file on your local computer, republish hello server project.</span></span>
