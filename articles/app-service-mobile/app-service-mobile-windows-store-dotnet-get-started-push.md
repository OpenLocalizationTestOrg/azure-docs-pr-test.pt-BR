---
title: "aplicativo do Windows UWP (plataforma Universal) do aaaAdd push notificações tooyour | Microsoft Docs"
description: "Saiba como toouse aplicativos de celular do serviço de aplicativo do Azure e Hubs de notificação do Azure toosend aplicativo por push notificações tooyour Windows UWP (plataforma Universal)."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a>Adicionar aplicativo do Windows de tooyour de notificações de push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Visão geral
Neste tutorial, você adiciona toohello de notificações por push [início rápido do Windows](app-service-mobile-windows-store-dotnet-get-started.md) de projeto para que uma notificação por push seja enviada toohello dispositivo toda vez que um registro é inserido.

Se você não usar Olá baixar o projeto de servidor de início rápido, será necessário Olá o pacote de extensão de notificação por push. Consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.

## <a name="configure-hub"></a>Configurar um novo Hub de Notificações
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a>Registrar seu aplicativo para notificações por push
Você precisa toosubmit toohello seu aplicativo da Windows Store e configurar sua toointegrate de projeto de servidor com serviços de notificação do Windows (WNS) toosend push.

1. No Visual Studio Solution Explorer, projeto de aplicativo UWP de saudação com o botão direito, clique em **repositório** > **associar aplicativo hello repositório...** .

    ![Associar aplicativo com a Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. No Assistente de saudação, clique em **próximo**, entrar com sua conta da Microsoft, digite um nome para seu aplicativo na **reservar um novo nome de aplicativo**, em seguida, clique em **reserva**.
3. Após o registro do aplicativo hello novo nome de aplicativo criado com êxito, selecione hello, clique em **próximo**e, em seguida, clique em **associar**. Isso adiciona o manifesto do aplicativo hello necessárias da Windows Store registro informações toohello.  
4. Navegue toohello [Centro de desenvolvimento do Windows](https://dev.windows.com/en-us/overview), entrar com sua conta da Microsoft, clique em novo registro de aplicativo hello em **meus aplicativos**, em seguida, expanda **serviços**  >  **Notificações por push**.
5. Em Olá **notificações por Push** , clique em **site de serviços do Live** em **serviços móveis do Microsoft Azure**.
6. Na página de registro hello, tome nota do valor de saudação em **segredos do aplicativo** e hello **SID do pacote**, que é seguida usará tooconfigure seu back-end do aplicativo móvel.

    ![Associar aplicativo com a Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > SID de pacote e segredo de saudação do cliente são credenciais de segurança importantes. Não compartilhe esses valores com ninguém nem os distribua com seu aplicativo. Olá **Id do aplicativo** é usado com a autenticação do hello secreta tooconfigure Account da Microsoft.
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a>Configurar notificações por push do hello back-end toosend
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <a id="update-service"></a>Olá server toosend push notificações de atualização
Use o procedimento de saudação abaixo que corresponde ao tipo de projeto de back-end&mdash;ou [back-end .NET](#dotnet) ou [Node. js back-end](#nodejs).

### <a name="dotnet"></a>Projeto de back-end .NET
1. No Visual Studio, clique com botão direito Olá servidor e clique em **gerenciar pacotes NuGet**, procure Microsoft.Azure.NotificationHubs e clique em **instalar**. Isso instala a biblioteca de cliente Olá Hubs de notificação.
2. Expanda **controladores**, abra TodoItemController.cs e adicione Olá seguinte usando instruções:

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

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Esse código informa toosend de hub de notificação Olá uma notificação por push após um novo item de inserção.
4. Republicar o projeto do servidor de saudação.

### <a name="nodejs"></a>Projeto de back-end Node.js
1. Se você ainda não fez isso, [baixar o projeto de início rápido de saudação](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) ou use outro Olá [editor online no portal do Azure de saudação](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Substitua o código existente de saudação no arquivo de todoitem.js Olá com os seguintes hello:

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
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

    Envia uma notificação WNS do sistema que contém item.text hello quando um novo item de tarefas é inserido.
3. Ao editar o arquivo hello no computador local, republicar o projeto do servidor de saudação.

## <a id="update-app"></a>Adicionar aplicativo de tooyour de notificações por push
Em seguida, seu aplicativo deve se registrar para notificações por push na inicialização. Quando você já habilitou a autenticação, certifique-se de que o usuário Olá entrar antes de tentar tooregister para notificações por push.

1. Olá abrir **App.xaml.cs** arquivo de projeto e adicione o seguinte Olá `using` instruções:

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. Em Olá mesmo arquivo, adicione o seguinte Olá **InitNotificationsAsync** toohello de definição de método **aplicativo** classe:

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    Esse código recupera Olá ChannelURI para o aplicativo de saudação do WNS e registra esse ChannelURI com seu aplicativo do aplicativo do serviço móvel.
3. Na parte superior de saudação do hello **OnLaunched** manipulador de eventos **App.xaml.cs**, adicionar Olá **async** definição de método modificador toohello e adicione a seguinte Olá chamar novotoohello **InitNotificationsAsync** método, como no exemplo a seguir de saudação:

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    Isso garante que Olá que channeluri curta duração é registrado sempre que o aplicativo hello é iniciado.
4. Recompile seu projeto de aplicativo da UWP. Seu aplicativo agora está pronto tooreceive notificações do sistema.

## <a id="test"></a>Testar notificações por push no seu aplicativo
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <a id="more"></a>Próximas etapas
Saiba mais sobre as notificações por push:

* [Como toouse Olá gerenciada do cliente para aplicativos móveis do Azure](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  Modelos oferecem envios de plataforma cruzada toosend flexibilidade e envios localizados. Saiba como tooregister modelos.
* [Diagnosticar problemas com notificações por push](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  há vários motivos por que as notificações podem ser abandonadas ou não irem terminar nos dispositivos. Este tópico mostra como tooanalyze e descobrir raiz Olá causam falhas de notificação por push.

Considere a possibilidade de continuar tooone de saudação tutoriais a seguir:

* [Adicionar autenticação tooyour aplicativo](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Saiba como tooauthenticate usuários do seu aplicativo com um provedor de identidade.
* [Habilitar sincronização offline para seu aplicativo](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Saiba como off-line tooadd dão suporte ao seu aplicativo usar um back-end do aplicativo móvel. Sincronização offline permite que os usuários finais toointeract com um aplicativo móvel&mdash;exibindo, adicionando ou modificando dados&mdash;mesmo quando não há nenhuma conexão de rede.

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
