---
title: "notificações de push aaaSending com Hubs de notificação do Azure no Windows Phone | Microsoft Docs"
description: "Neste tutorial, você aprenderá como notificações de toopush de Hubs de notificação do Azure toouse tooa Windows Phone 8 ou o aplicativo do Windows Phone 8.1 Silverlight."
services: notification-hubs
documentationcenter: windows
keywords: "notificação por push,notificação por push,envio por push do windows phone"
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a>Enviar notificações por push com os Hubs de Notificação do Azure no Windows Phone
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Visão geral
> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).
> 
> 

Este tutorial mostra como aplicativo de Windows Phone 8 ou Windows Phone 8.1 Silverlight tooa notificações de envio de toouse toosend de Hubs de notificação do Azure. Se você estiver direcionando o Windows Phone 8.1 (não Silverlight), consulte toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) versão.
Neste tutorial, você deve criar um aplicativo do Windows Phone 8 em branco que recebe notificações por push usando Olá Microsoft Push Notification Service (MPNS). Quando você terminar, você será capaz de toouse sua toobroadcast de hub de notificação por push notificações tooall Olá a dispositivos que executam seu aplicativo.

> [!NOTE]
> Olá notificação Hubs Windows Phone SDK não dá suporte ao uso Olá Windows Push Notification Service (WNS) com aplicativos do Windows Phone 8.1 Silverlight. toouse WNS (em vez de MPNS) com aplicativos do Windows Phone 8.1 Silverlight, siga Olá [Hubs de notificação - Windows Phone Silverlight tutorial], que usa APIs REST.
> 
> 

tutorial de saudação demonstra o cenário de difusão simples hello usando Hubs de notificação.

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial requer o seguinte hello:

* [Visual Studio 2012 Express para Windows Phone]ou uma versão posterior.

A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Windows Phone 8.

## <a name="create-your-notification-hub"></a>Criar seu Hub de Notificação
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Clique em Olá <b>Notification Services</b> seção (dentro de <i>configurações</i>), clique em <b>Windows Phone (MPNS)</b> e, em seguida, clique em hello <b>habilitar por push não autenticadas </b> caixa de seleção.</p>
</li>
</ol>

&emsp;&emsp;![Portal do Azure - habilitar notificações por push não autenticadas](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

O hub é agora notificação toosend criado e configurado não autenticado para Windows Phone.

> [!NOTE]
> Este tutorial usa MPNS no modo não autenticado. Modo não autenticado MPNS vem com restrições em que você pode enviar tooeach canal de notificações. Oferece suporte a Hubs de notificação [MPNS autenticado modo](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) , permitindo-lhe tooupload seu certificado.
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a>Conectando o hub de notificação do aplicativo toohello
1. No Visual Studio, crie um novo aplicativo de console do Windows Phone 8.
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    No Visual Studio 2013 Atualização 2 ou posterior, você cria um aplicativo do Windows Phone Silverlight.
   
    ![Visual Studio - Novo Projeto - Aplicativo em branco - Windows Phone Silverlight][11]
2. No Visual Studio, clique com botão direito solução hello e, em seguida, clique em **gerenciar pacotes NuGet**.
   
    Isso exibe o saudação **gerenciar pacotes NuGet** caixa de diálogo.
3. Procurar `WindowsAzure.Messaging.Managed` e clique em **instalar**e aceite os termos de uso do hello.
   
    ![Visual Studio - Gerenciador de Pacotes do NuGet][20]
   
    Isso baixa, instala e adiciona uma biblioteca da referência toohello mensagens do Azure para Windows usando Olá <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pacote WindowsAzure.Messaging.Managed NuGet</a>.
4. Abra o arquivo de saudação App.xaml.cs e adicione o seguinte Olá `using` instruções:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. Adicionar Olá seguinte código na parte superior de saudação do **Application_Launching** método em App.xaml.cs:
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > Olá valor **MyPushChannel** é um índice que é usado toolookup um canal existente no hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) coleção. Se não houver uma, crie uma nova entrada com esse nome.
   > 
   > 
   
    Certifique-se de tooinsert Olá nome de sua cadeia de conexão de hub e hello chamado **DefaultListenSharedAccessSignature** que você obteve na seção anterior hello.
    Esse código recupera o URI do canal Olá para o aplicativo de saudação do MPNS e, em seguida, registra esse URI de canal com seu hub de notificação. Ela também garante que esse canal Olá que URI é registrado no hub de notificação, que cada aplicativo de saudação do tempo é iniciado.
   
   > [!NOTE]
   > Este tutorial envia um dispositivo de toohello de notificação do sistema. Quando você enviar uma notificação de bloco, em vez disso, você deve chamar hello **BindToShellTile** método no canal de saudação. toosupport notificações de notificação do sistema e lado a lado, chamar **BindToShellTile** e **BindToShellToast**.
   > 
   > 
6. No Gerenciador de soluções, expanda **propriedades**, abra Olá `WMAppManifest.xml` de arquivo, clique em Olá **recursos** guia e certifique-se de que Olá **ID_CAP_PUSH_NOTIFICATION** recurso é verificado.
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. Olá pressione `F5` toorun chave Olá aplicativo.
   
    Será exibida uma mensagem de registro no aplicativo hello.
8. Aplicativo hello fechar.  
   
   > [!NOTE]
   > tooreceive uma notificação por push do sistema, o aplicativo hello não deve estar executando em primeiro plano da saudação.
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a>Enviar notificações por push de seu back-end
Você pode enviar notificações por push usando os Hubs de notificação de qualquer back-end por meio de saudação público <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interface REST</a>. Neste tutorial, você envia notificações por push usando um aplicativo de console .NET. 

Para obter um exemplo de como toosend notificações por push de um back-end ASP.NET WebAPI integrado com Hubs de notificação, consulte [notificação Hubs notificar os usuários do Azure com o back-end .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).  

Para obter um exemplo de como as notificações por push de toosend usando Olá [APIs REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), check-out [como toouse Hubs de notificação do Java](notification-hubs-java-push-notification-tutorial.md) e [como toouse Hubs de notificação do PHP](notification-hubs-php-push-notification-tutorial.md) .

1. Solução de saudação com o botão direito, selecione **adicionar** e **novo projeto...** e, em seguida, em **Visual C#**, clique em **Windows** e **aplicativo de Console**e clique em **Okey**.
   
       ![Visual Studio - New Project - Console Application][6]
   
    Isso adiciona uma novo Visual C# console toohello solução de aplicativo. Você também pode fazer isso em uma solução separada.
2. Clique em **Ferramentas**, em **Gerenciador de Pacotes da Biblioteca** e em **Console do Gerenciador de Pacotes**.
   
    Isso exibe o saudação Package Manager Console.
3. Em hello **Package Manager Console** janela, Olá do conjunto **projeto padrão** tooyour novo projeto de aplicativo de console e na janela de console hello, execute Olá comando a seguir:
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   Isso adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet de Hubs Microsoft.Azure.Notification</a>.
4. Olá abrir `Program.cs` de arquivo e adicione o seguinte Olá `using` instrução:
   
        using Microsoft.Azure.NotificationHubs;
5. Em Olá `Program` classe, adicione o seguinte método de saudação:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    Verifique se Olá de tooreplace `<hub name>` espaço reservado com o nome de saudação do hub de notificação de saudação que aparece no portal de saudação. Além disso, substitua espaço reservado de cadeia de caracteres de conexão Olá Olá cadeia de conexão chamada **DefaultFullSharedAccessSignature** que você obteve na seção hello "Configurar seu hub de notificação".
   
   > [!NOTE]
   > Certifique-se de que você use a cadeia de caracteres de conexão de saudação com **completo** acessar, não **escutar** acesso. cadeia de caracteres de acesso de escuta Olá não tem as notificações por push de toosend de permissões.
   > 
   > 
6. Adicionar Olá a seguinte linha no seu `Main` método:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Com o Windows Phone emulador em execução e seu projeto de aplicativo de console do aplicativo hello fechado, defina como saudação padrão o projeto de inicialização em pressione Olá `F5` toorun chave Olá aplicativo.
   
    Você receberá uma notificação do sistema por push. Tocando em faixa de notificação do sistema Olá carrega o aplicativo hello.

Você encontrará todas as cargas de possíveis Olá Olá [catálogo de sistema] e [catálogo bloco] tópicos no MSDN.

## <a name="next-steps"></a>Próximas etapas
Neste exemplo simples, você transmitida tooall de notificações por push seus dispositivos Windows Phone 8. 

Em ordem tootarget usuários específicos, consulte toohello [usar Hubs de notificação toopush notificações toousers] tutorial. 

Se você desejar toosegment os usuários, grupos de interesse, você pode ler [toosend de Hubs de notificação de uso últimas notícias]. 

Saiba mais sobre como Hubs de notificação toouse [orientação de Hubs de notificação].

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express para Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[orientação de Hubs de notificação]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[usar Hubs de notificação toopush notificações toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend de Hubs de notificação de uso últimas notícias]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[catálogo de sistema]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[catálogo bloco]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[Hubs de notificação - Windows Phone Silverlight tutorial]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

