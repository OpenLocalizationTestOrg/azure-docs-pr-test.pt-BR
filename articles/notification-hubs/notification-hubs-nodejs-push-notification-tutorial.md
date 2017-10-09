---
title: "notificações de push aaaSending com Hubs de notificação do Azure e Node. js"
description: "Saiba como toouse Hubs de notificação toosend notificações por push de um aplicativo Node. js."
keywords: "notificação por push, notificações por push,push do node.js,push do ios"
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a>Enviar notificações por push com os Hubs de Notificação do Azure e o Node.js
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a>Visão geral
> [!IMPORTANT]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).
> 
> 

Este guia mostrará como toosend notificações por push com ajuda Olá hubs de notificação do Azure diretamente de um aplicativo Node. js. 

cenários de saudação abordados incluem a remessa tooapplications de notificações por push em Olá plataformas a seguir:

* Android
* iOS
* Windows Phone
* Plataforma Universal do Windows 

Para obter mais informações sobre hubs de notificação, consulte Olá [próximas etapas](#next) seção.

## <a name="what-are-notification-hubs"></a>O que são Hubs de Notificação?
Hubs de notificação do Azure oferecem uma infraestrutura fácil de usar, multiplataforma e dimensionável para enviar por push a dispositivos de toomobile de notificações. Para obter detalhes sobre a infraestrutura de serviço hello, consulte Olá [Hubs de notificação do Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) página.

## <a name="create-a-nodejs-application"></a>Criar um aplicativo Node.js
a primeira etapa Olá neste tutorial está criando um novo aplicativo Node. js em branco. Para obter instruções sobre como criar um aplicativo Node. js, consulte [criar e implantar um aplicativo de Node. js tooAzure Site da Web][nodejswebsite], [serviço de nuvem do Node. js] [ Node.js Cloud Service] usando o Windows PowerShell, ou [Site com WebMatrix].

## <a name="configure-your-application-toouse-notification-hubs"></a>Configurar seu aplicativo tooUse os Hubs de notificação
toouse Hubs de notificação do Azure, você precisa toodownload e use Olá Node. js [pacote do azure](https://www.npmjs.com/package/azure), que inclui um conjunto interno de bibliotecas auxiliar que se comunicam com serviços da REST Olá push notificação.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Usar o pacote de saudação do Gerenciador de pacote de nó (NPM) tooobtain
1. Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Linux) e navegue toohello pasta em que você criou seu aplicativo em branco .
2. Tipo **npm instalar azure sb** na janela de comando hello.
3. Você pode executar manualmente Olá **ls** ou **dir** tooverify de comando que um **nó\_módulos** pasta foi criada. Dentro dessa pasta, localize Olá **azure** pacote, que contém as bibliotecas de saudação necessário tooaccess Olá Hub de notificação.

> [!NOTE]
> Você pode aprender mais sobre a instalação de NPM em oficial Olá [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm). 
> 
> 

### <a name="import-hello-module"></a>Módulo de saudação de importação
Usando um editor de texto, adicionar Olá após toohello superior de saudação **server.js** arquivo de aplicativo hello:

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a>Instalar uma conexão do hub de notificação do Azure
Olá **NotificationHubService** objeto permite que você trabalhe com hubs de notificação. Olá código a seguir cria um **NotificationHubService** objeto para o hub de nofication Olá denominado **hubname**. Adicioná-lo superior de saudação do hello **server.js** arquivo depois de módulo de saudação do azure Olá instrução tooimport:

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

Olá conexão **connectionstring** valor pode ser obtido da saudação [Portal do Azure] executando Olá etapas a seguir:

1. No painel de navegação esquerdo hello, clique em **procurar**.
2. Selecione **Hubs de notificação**e, em seguida, localizar Olá hub de desejar toouse para exemplo hello. Você pode consultar toohello [tutorial guia de Introdução do Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) se precisar de ajuda para criar um novo Hub de notificação.
3. Escolha a opção **Configurações**.
4. Clique em **Políticas de Acesso**. Você verá as duas cadeias de conexão de acesso compartilhado e completo.

![Portal do Azure - Hubs de Notificação](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> Você também pode recuperar a cadeia de caracteres de conexão de saudação usando Olá **Get-AzureSbNamespace** cmdlet fornecido pelo [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou hello **sb azure namespace Mostrar** com Olá [Azure Interface de linha de comando (CLI do Azure)](../cli-install-nodejs.md).
> 
> 

## <a name="general-architecture"></a>Arquitetura geral
Olá **NotificationHubService** objeto expõe Olá instâncias de objeto para enviar por push notificações toospecific dispositivos e aplicativos a seguir:

* **Android** -usar Olá **GcmService** objeto, que está disponível em **notificationHubService.gcm**
* **iOS** -usar Olá **ApnsService** objeto, que é acessível no **notificationHubService.apns**
* **Windows Phone** -usar Olá **MpnsService** objeto, que está disponível em **notificationHubService.mpns**
* **Plataforma universal do Windows** -usar Olá **WnsService** objeto, que está disponível em **notificationHubService.wns**

### <a name="how-to-send-push-notifications-tooandroid-applications"></a>Como: enviar por push a aplicativos de tooAndroid de notificações
Olá **GcmService** objeto fornece um **enviar** método que pode ser usado toosend push notificações tooAndroid aplicativos. Olá **enviar** método aceita Olá parâmetros a seguir:

* **Marcas** -Olá identificador de marca. Se nenhuma marca for fornecida, notificação de saudação será enviada tooall clientes.
* **Carga** -Olá carga brutos da cadeia de caracteres ou JSON da mensagem.
* **Retorno de chamada** -Olá a função de retorno de chamada.

Para obter mais informações sobre o formato de carga hello, consulte Olá **carga** seção Olá [implementando GCM Server](http://developer.android.com/google/gcm/server.html#payload) documento.

Olá, código a seguir usa Olá **GcmService** instância exposta pelo Olá **NotificationHubService** toosend um tooall de notificação por push registrado clientes.

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a>Como: enviar por push a aplicativos de tooiOS de notificações
Mesmo assim como acontece com aplicativos do Android descrito acima, Olá **ApnsService** objeto fornece um **enviar** método que pode ser usado toosend push notificações tooiOS aplicativos. Olá **enviar** método aceita Olá parâmetros a seguir:

* **Marcas** -Olá identificador de marca. Se nenhuma marca for fornecida, notificação de saudação será enviada tooall clientes.
* **Carga** - Olá JSON da mensagem ou carga da cadeia de caracteres.
* **Retorno de chamada** -Olá a função de retorno de chamada.

Para o formato de carga de saudação de mais informações, consulte Olá **carga de notificação** seção Olá [Local e o guia de programação de notificação por Push](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) documento.

Olá, código a seguir usa Olá **ApnsService** instância exposta pelo Olá **NotificationHubService** toosend um alerta de mensagem tooall clientes:

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a>Como: enviar por push a aplicativos de telefone tooWindows notificações
Olá **MpnsService** objeto fornece um **enviar** método que pode ser usado toosend push notificações tooWindows aplicativos de telefone. Olá **enviar** método aceita Olá parâmetros a seguir:

* **Marcas** -Olá identificador de marca. Se nenhuma marca for fornecida, notificação de saudação será enviada tooall clientes.
* **Carga** -Olá carga XML da mensagem.
* **TargetName** - `toast` para notificações ‘toast’. `token` para notificações de bloco.
* **NotificationClass** -Olá prioridade de notificação de saudação. Consulte Olá **elementos de cabeçalho HTTP** seção Olá [notificações por Push de um servidor](http://msdn.microsoft.com/library/hh221551.aspx) documento para obter valores válidos.
* **Options** : cabeçalhos de solicitação opcionais.
* **Retorno de chamada** -Olá a função de retorno de chamada.

Para obter uma lista de válido **TargetName**, **NotificationClass** e opções de cabeçalho, confira Olá [notificações por Push de um servidor](http://msdn.microsoft.com/library/hh221551.aspx) página.

Olá, código de exemplo a seguir usa Olá **MpnsService** instância exposta pelo Olá **NotificationHubService** toosend uma notificação por push do sistema:

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a>Como: enviar por push a aplicativos de plataforma do Windows (UWP) tooUniversal notificações
Olá **WnsService** objeto fornece um **enviar** método que pode ser usados toosend push notificações tooUniversal plataforma Windows aplicativos.  Olá **enviar** método aceita Olá parâmetros a seguir:

* **Marcas** -Olá identificador de marca. Se nenhuma marca for fornecida, notificação de saudação será enviada clientes tooall registrado.
* **Carga** -carga da mensagem XML hello.
* **Tipo** -Olá tipo de notificação.
* **Options** : cabeçalhos de solicitação opcionais.
* **Retorno de chamada** -Olá a função de retorno de chamada.

Para obter uma lista de tipos e de cabeçalhos de solicitação válidos, veja [Solicitação de serviço e cabeçalhos de resposta de notificação por push](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).

Olá, código a seguir usa Olá **WnsService** instância exposta pelo Olá **NotificationHubService** toosend um aplicativo UWP tooa de notificação do sistema por push:

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a>Próximas etapas
trechos de código de exemplo do Hello acima permitem que você tooeasily compilação serviço infraestrutura toodeliver push notificações tooa ampla variedade de dispositivos. Agora que você aprendeu as Noções básicas de saudação do uso de Hubs de notificação com Node. js, siga essas toolearn links mais informações sobre como você pode estender esses recursos adicionais.

* Consulte Olá referência do MSDN para [Hubs de notificação do Azure](https://msdn.microsoft.com/library/azure/jj927170.aspx).
* Visite Olá [SDK do Azure para o nó] repositório no GitHub para obter mais exemplos e detalhes de implementação.

[SDK do Azure para o nó]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[Site com WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Portal do Azure]: https://portal.azure.com
