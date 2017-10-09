Nesta seção, você atualizar código no seu toosend de projeto de back-end de aplicativos móveis existente uma notificação por push sempre que um novo item é adicionado. Isso é alimentado por Olá [modelo](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) recurso de Hubs de notificação do Azure, permitindo que os envios de plataforma cruzada. Olá vários clientes são registrados para notificações por push usando modelos, e um envio por push universal único pode receber tooall plataformas de cliente.

Escolha uma saudação procedimentos a seguir que corresponde ao tipo de projeto de back-end&mdash;ou [.NET back-end](#dotnet) ou [Node. js back-end](#nodejs).

### <a name="dotnet"></a>Projeto de back-end do .NET
1. No Visual Studio, clique com botão direito Olá servidor e clique em **gerenciar pacotes NuGet**. Procure `Microsoft.Azure.NotificationHubs` e então clique em **Instalar**. Isso instala a biblioteca de Hubs de notificação hello para enviar notificações de back-end.
2. No projeto do servidor de saudação, abra **controladores** > **TodoItemController.cs**e adicione Olá seguinte usando instruções:

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. Em Olá **PostTodoItem** método, adicione Olá código a seguir após a chamada de saudação muito**InsertAsync**:  

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

    Isso envia uma notificação de modelo que contém o item de saudação. Texto quando um novo item é inserido.
4. Republicar o projeto do servidor de saudação.

### <a name="nodejs"></a>Projeto de back-end do Node.js
1. Se você ainda não fez isso, [baixar o projeto de back-end de início rápido de saudação](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), ou use outro Olá [editor online no portal do Azure de saudação](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Substitua o código existente de saudação em todoitem.js com os seguintes hello:

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

    Isso envia uma notificação de modelo que contém a saudação item.text quando um novo item é inserido.
3. Ao editar o arquivo hello no computador local, republicar o projeto do servidor de saudação.
