---
title: "aaaGet de Introdução ao Azure notificação Hubs para aplicativos universais do Windows plataforma | Microsoft Docs"
description: "Neste tutorial, você aprenderá como toouse Hubs de notificação do Azure toopush notificações tooa aplicativo da plataforma Universal do Windows."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a>Introdução aos Hubs de Notificação para aplicativos da Plataforma Universal do Windows
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Visão geral
Este tutorial mostra como aplicativo de Windows UWP (plataforma Universal) tooa notificações por push de toouse toosend de Hubs de notificação do Azure.

Neste tutorial, você deve criar um aplicativo da Windows Store em branco que recebe notificações por push usando Olá Windows Push Notification Service (WNS). Quando você terminar, você será capaz de toouse sua toobroadcast de hub de notificação por push notificações tooall Olá a dispositivos que executam seu aplicativo.

## <a name="before-you-begin"></a>Antes de começar
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

código de saudação concluído para este tutorial pode ser encontrado no GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial requer o seguinte hello:

* [Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) ou posterior
* [Ferramentas de Desenvolvimento de Aplicativos Universais do Windows instaladas](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* Uma conta ativa do Azure  <br/>Se não tiver uma conta, você poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).
* Uma conta ativa da Windows Store

A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos da Plataforma Universal do Windows.

## <a name="register-your-app-for-hello-windows-store"></a>Registrar seu aplicativo para saudação da Windows Store
aplicativos de tooUWP de notificações de push toosend, você deve associar toohello seu aplicativo da Windows Store. Em seguida, você deve configurar sua toointegrate de hub de notificação com WNS.

1. Se você não estiver registrado seu aplicativo, navegar toohello [Centro de desenvolvimento do Windows](https://dev.windows.com/overview), entrar com sua conta da Microsoft e, em seguida, clique em **criar um novo aplicativo**.

2. Digite um nome para seu aplicativo e clique em **Reservar nome do aplicativo**. Isso cria um novo registro da Windows Store para seu aplicativo.

3. No Visual Studio, crie um novo projeto do Visual c# aplicativos da Windows Store usando Olá Universal do Windows **aplicativo em branco** modelo e clique em **Okey**.

4. Aceite os padrões de saudação para destino hello e versões de plataforma mínimas.

5. No Gerenciador de soluções, projeto de aplicativo da Windows Store com o botão direito hello, clique em **repositório**e, em seguida, clique em **associar aplicativo hello repositório...** . Olá **associar seu aplicativo com hello da Windows Store** assistente é exibido.

6. No Assistente de saudação, entre com sua conta da Microsoft.

7. Clique em aplicativo hello que você registrou na etapa 2, clique em **próximo**e, em seguida, clique em **associar**. Isso adiciona o manifesto do aplicativo hello necessárias da Windows Store registro informações toohello.

8. Em Olá [Centro de desenvolvimento do Windows](http://dev.windows.com/overview) para seu novo aplicativo, clique em **serviços**, clique em **notificações por Push**e, em seguida, clique em **WNS/MPNS**.

9. Clique em **Nova Notificação**.

10. Clique no modelo **Em branco (Notificação do sistema)** e depois clique em **OK**.

11. Insira um **Nome** para a notificação e uma mensagem de **Contexto** Visual. Em seguida, clique em **Salvar como rascunho**.

12. Navegue toohello [Portal de registro de aplicativo](http://apps.dev.microsoft.com) e faça logon.

13. Clique no nome de seu aplicativo. Anote Olá **segredo do aplicativo** senha e hello **identificador de segurança (SID) do pacote** localizado em Olá **da Windows Store** configurações da plataforma.

     > [AZURE.WARNING]
    SID de pacote e segredo do aplicativo Hello são credenciais de segurança importantes. Não compartilhe esses valores com ninguém nem os distribua com seu aplicativo.

## <a name="configure-your-notification-hub"></a>Configurar seu Hub de Notificação
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Selecione Olá <b>Notification Services</b> opção e hello <b>Windows (WNS)</b> opção. Em seguida, digite Olá <b>segredo do aplicativo</b> senha no hello <b>chave de segurança</b> campo. Insira seu <b>SID do pacote</b> valor que você obteve do WNS na seção anterior hello e, em seguida, clique em <b>salvar</b>.</p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

O hub de notificação agora é toowork configurado com WNS, e ter Olá tooregister de cadeias de caracteres de conexão de seu aplicativo e enviar notificações.

## <a name="connect-your-app-toohello-notification-hub"></a>Conecte-se o seu hub de notificação do aplicativo toohello
1. No Visual Studio, clique com botão direito solução hello e, em seguida, clique em **gerenciar pacotes NuGet**.
   
    Isso exibe o saudação **gerenciar pacotes NuGet** caixa de diálogo.
2. Procurar `WindowsAzure.Messaging.Managed` e clique em **instalar**e aceite os termos de uso do hello.
   
    ![][20]
   
    Isso baixa, instala e adiciona uma biblioteca da referência toohello mensagens do Azure para Windows usando Olá <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pacote WindowsAzure.Messaging.Managed NuGet</a>.
3. Abrir o arquivo de projeto do hello App.xaml.cs e adicione o seguinte Olá `using` instruções. 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. Também no App.xaml.cs, adicione a seguir Olá **InitNotificationsAsync** toohello de definição de método **aplicativo** classe:
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    Esse código recupera o URI do canal Olá para o aplicativo de saudação do WNS e, em seguida, registra esse URI de canal com seu hub de notificação.
   
   > [!NOTE]
   > Verifique se tooreplace Olá espaço reservado de "o nome do hub" com o nome de saudação do hub de notificação de saudação que aparece no hello Portal do Azure. Também substitua espaço reservado de cadeia de caracteres de conexão Olá Olá **DefaultListenSharedAccessSignature** cadeia de caracteres de conexão que você obteve da saudação **políticas de acesso** página do Hub de notificação em um seção anterior.
   > 
   > 
5. Na parte superior de saudação do hello **OnLaunched** manipulador de eventos em App.xaml.cs, adicionar Olá chamada toohello novos a seguir **InitNotificationsAsync** método:
   
        InitNotificationsAsync();
   
    Isso garante que esse canal Olá que URI é registrado no hub de notificação, que cada aplicativo de saudação do tempo é iniciado.
6. Olá pressione **F5** toorun chave Olá aplicativo. Uma caixa de diálogo pop-up que contém a chave de registro de saudação é exibida.

Seu aplicativo agora está pronto tooreceive notificações do sistema.

## <a name="send-notifications"></a>Enviar notificações
Você pode testar rapidamente a receber notificações em seu aplicativo pelo envio de notificações em Olá [Portal do Azure](https://portal.azure.com/) usando Olá **teste enviar** botão no hub de notificação hello, conforme mostrado na tela hello abaixo.

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

Notificações por push normalmente são enviadas em um serviço de back-end como Serviços Móveis ou ASP.NET usando uma biblioteca compatível. Você também pode usar o hello API REST diretamente as mensagens de notificação de toosend se uma biblioteca não está disponível para o back-end. 

Neste tutorial, nós manter a simplicidade e demonstrar a testar seu aplicativo de cliente por meio do envio de notificações usando Olá SDK .NET para hubs de notificação em um aplicativo de console, em vez de um serviço de back-end. É recomendável Olá [usar Hubs de notificação toopush notificações toousers] tutorial como a próxima etapa hello para enviar notificações de um back-end do ASP.NET. No entanto, a saudação abordagens a seguir pode ser usada para enviar notificações:

* **Interface REST**: você pode dar suporte à notificação em qualquer plataforma de back-end usando Olá [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **SDK .NET de Hubs de notificação do Microsoft Azure**: em Olá Gerenciador de pacotes do Nuget para Visual Studio, execute [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [como toouse Hubs de notificação do Node. js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Aplicativos móveis do Azure**: para obter um exemplo de como toosend notificações de um aplicativo móvel do Azure que esteja integrado com Hubs de notificação, consulte [adicionar notificações de push para aplicativos móveis](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: para obter um exemplo de como as notificações de toosend usando Olá APIs REST, consulte "como toouse Hubs de notificação do Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-console-app"></a>(Opcional) Enviar notificações de um aplicativo de console
notificações de toosend usando um aplicativo de console .NET siga estas etapas. 

1. Solução de saudação com o botão direito, selecione **adicionar** e **novo projeto...** e, em seguida, em **Visual C#**, clique em **Windows** e **aplicativo de Console**e clique em **Okey**.
   
    Isso adiciona uma novo Visual C# console toohello solução de aplicativo. Você também pode fazer isso em uma solução separada.

2. No Visual Studio, clique em **Ferramentas**, em **Gerenciador de Pacotes NuGet** e em **Console do Gerenciador de Pacotes**.
   
    Isso exibe o saudação Package Manager Console no Visual Studio.
3. Olá janela do Console do Gerenciador de pacotes, definido Olá **projeto padrão** tooyour novo projeto de aplicativo de console e na janela de console hello, execute Olá comando a seguir:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Isso adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet de Hubs Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Abra o arquivo Program.cs de saudação e adicione o seguinte de saudação `using` instrução:
   
        using Microsoft.Azure.NotificationHubs;
5. Em Olá **programa** classe, adicione o seguinte método de saudação:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > Certifique-se de que você use a cadeia de caracteres de conexão de saudação com **completo** acessar, não **escutar** acesso. cadeia de caracteres de acesso de escuta Olá não tem as notificações de toosend de permissões.
   > 
   > 
6. Adicionar Olá Olá linhas a seguir **principal** método:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Clique em projeto de aplicativo de console Olá no Visual Studio e clique em **definir como projeto de inicialização** tooset como projeto de inicialização de saudação. Em seguida, pressione Olá **F5** aplicativo hello de toorun da chave.
   
    Você receberá uma notificação do sistema em todos os dispositivos registrados. Faixa de notificação do sistema Olá clicando ou tocando carrega o aplicativo hello.

Você pode encontrar todas as cargas de saudação com suporte no hello [catálogo de sistema], [catálogo bloco], e [visão geral de notificação] tópicos no MSDN.

## <a name="next-steps"></a>Próximas etapas
Neste exemplo simples, você enviadas notificações difusão tooall seus dispositivos do Windows usando o portal de saudação ou um aplicativo de console. É recomendável Olá [usar Hubs de notificação toopush notificações toousers] tutorial como a próxima etapa de saudação. Ele lhe mostrará como toosend notificações de um back-end do ASP.NET usando marcas tootarget determinados usuários.

Se você quiser toosegment os usuários, grupos de interesse, consulte [toosend de Hubs de notificação de uso últimas notícias]. 

toolearn obter mais informações sobre Hubs de notificação, consulte [orientação de Hubs de notificação](notification-hubs-push-notification-overview.md).

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[usar Hubs de notificação toopush notificações toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend de Hubs de notificação de uso últimas notícias]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[catálogo de sistema]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[catálogo bloco]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[visão geral de notificação]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
