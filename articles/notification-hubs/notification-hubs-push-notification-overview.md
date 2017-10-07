---
title: "aaaAzure Hubs de notificação"
description: "Saiba como tooadd envio recursos de notificação com Hubs de notificação do Azure."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: 
ms.assetid: fcfb0ce8-0e19-4fa8-b777-6b9f9cdda178
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 1/17/2017
ms.author: yuaxu
ms.openlocfilehash: 78ce34b6b094b560c8002ab9652f7ba4563c5c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs"></a>Hubs de Notificação do Azure
## <a name="overview"></a>Visão geral
Os Hubs de Notificação do Azure fornecem um mecanismo de envio por push fácil de usar, multiplataforma e dimensionável. Com uma chamada de API de plataforma cruzada único, você pode facilmente enviar plataforma móvel de tooany de notificações de push personalizados e de destino de qualquer back-end de nuvem ou local.

Os Hubs de Notificação funcionam bem tanto para cenários empresariais quanto para cenários de consumidor. Aqui temos alguns exemplos de como os consumidores usam os Hubs de Notificação:

* Envie as últimas notícias notificações toomillions com baixa latência.
* Envie cupons com base no local toointerested segmentos de usuário.
* Envie notificações de evento toousers ou grupos para os aplicativos de mídia/esportes/Finanças/jogos.
* Enviar por push toocustomers de mercado e tooengage tooapps conteúdo promocional.
* Para notificar os usuários sobre eventos corporativos, como novas mensagens e itens de trabalho.
* Para enviar códigos para Autenticação Multifator.

## <a name="what-are-push-notifications"></a>O que são notificações por push?
Notificações por push são uma forma de comunicação do aplicativo para o usuário na qual os usuários de aplicativos móveis recebem notificações sobre determinadas informações desejadas, geralmente em uma caixa de diálogo ou pop-up. Em geral, os usuários podem escolher tooview ou ignorar a mensagem de saudação e escolher antiga Olá abrirá Olá aplicativo móvel que tinha comunicada notificação hello.

As notificações por push são fundamentais para os aplicativos direcionados ao consumidor no aumento da interação e do uso do aplicativo e para os aplicativos empresariais na comunicação de informações atualizadas da empresa. É melhor comunicação de usuário de aplicativo hello porque ele é consumo de energia para dispositivos móveis, flexíveis para remetentes de notificações hello e disponíveis enquanto os aplicativos correspondentes não estão ativos.

Saiba mais sobre as notificações por push em algumas plataformas populares:
* [iOS](https://developer.apple.com/notifications/)
* [Android](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [Windows](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a>Como as notificações por push funcionam
As notificações por push são fornecidas por meio de infraestruturas específicas à plataforma chamadas de *Sistemas de Notificação de Plataforma* (PNS). Eles oferecem funcionalidades de push barebone toodelivery dispositivo de tooa de mensagem com um fornecido manipular e não tem nenhuma interface comum. toosend uma notificação de clientes de tooall em Olá iOS, Android e Windows versões de um aplicativo, desenvolvedor Olá deve trabalhar com APNS (Apple Push Notification Service), FCM (Firebase mensagens de nuvem) e WNS (serviço de notificação do Windows), durante o envio em lote Olá envia.

Em um alto nível, é assim que o push funciona:

1. aplicativo de cliente Olá decide que ele deseja tooreceive envia, portanto, Olá contatos correspondente PNS tooretrieve seu identificador exclusivo e temporário push. tipo de identificador de saudação depende do sistema hello (WNS, por exemplo tem URIs enquanto APNS tem tokens).
2. aplicativo de cliente Olá armazena esse identificador no back-end do aplicativo hello ou provedor.
3. toosend uma notificação por push, back-end do aplicativo hello contata Olá PNS usando Olá identificador tootarget um aplicativo de cliente específico.
4. Olá PNS encaminha especificado pelo identificador de saudação de dispositivo de saudação notificação toohello.

![][0]

## <a name="hello-challenges-of-push-notifications"></a>Olá desafios de notificações por Push
Enquanto PNSes são eficientes, deixam desenvolvedor do aplicativo de toohello muito trabalho em ordem tooimplement mesmo push notificação cenários comuns, como difusão ou enviar por push os usuários toosegmented de notificações.

Push é um dos hello mais recursos solicitados móvel em serviços em nuvem, porque requer que seu trabalho complexas infra-estruturas de lógica de negócios principal toohello relacionados do aplicativo. Alguns dos desafios base Olá são:

* **Dependência de plataforma**: 

  * Olá back-end precisa toohave complexa e difícil de manter a lógica de dependente de plataforma toosend notificações toodevices em várias plataformas que não são unificados de PNSes.
* **Escala**:

  * De acordo com as diretrizes de PNS, os tokens de dispositivo deverão ser atualizados sempre que o aplicativo for iniciado. Isso significa Olá back-end está lidando com uma grande quantidade de tráfego de banco de dados tokens de acesso e apenas tookeep Olá atualizadas. Quando o número de saudação de dispositivos aumenta toohundreds e milhares de milhões, custo de saudação da criação e manutenção dessa infraestrutura é grande.
  * Mais PNSes não dão suporte a difusão toomultiple dispositivos. Isso significa que uma simple tooa difusão resultados de milhões de dispositivos em milhões de chamadas toohello PNSes. Escalar essa quantidade de tráfego com latência mínima é uma tarefa difícil.
* **Roteamento**:
  
  * Embora PNSes fornecer toodevices de mensagens de toosend uma forma, a maioria das notificações de aplicativos são destinadas a usuários ou grupos de interesse. Isso significa Olá back-end deve manter dispositivos de tooassociate um registro com grupos de interesse, usuários, propriedades, etc. Essa sobrecarga aumenta os custos toohello toomarket e manutenção de tempo de um aplicativo.

## <a name="why-use-notification-hubs"></a>Por que usar Hubs de Notificação?
Os Hubs de Notificação eliminam todas as complexidades associadas à habilitação de notificação por push por sua conta. Sua infraestrutura de notificação por push multiplataforma e dimensionável reduz os códigos de push e simplifica o seu back-end. Com Hubs de notificação, os dispositivos são simplesmente responsáveis por seus identificadores PNS Registrando um hub, enquanto o back-end de saudação envia mensagens toousers ou grupos de interesse, como mostrado na figura a seguir de saudação:

![][1]

Hubs de notificação é o mecanismo de push prontos para uso com hello vantagens a seguir:

* **Plataformas cruzadas**

  * Suporte para todas as plataformas de push principais, incluindo iOS, Android, Windows e Kindle e Baidu.
  * Uma interface toopush tooall plataformas comuns em formatos específicos de plataforma ou independente de plataforma sem trabalho específico de plataforma.
  * Gerenciamento de identificador de dispositivo em um só local.
* **Back-ends cruzados**
  
  * Em nuvem ou local
  * .NET, Node.js, Java, etc.
* **Conjunto avançado de padrões de entrega**:

  * *Difusão tooone ou várias plataformas*: você pode transmitir instantaneamente toomillions de dispositivos em plataformas com uma única chamada de API.
  * *Enviar por push toodevice*: você pode direcionar dispositivos de tooindividual de notificações.
  * *Enviar por push toouser*: marcas e modelos de recursos ajudam a alcançar todos os dispositivos de plataforma cruzada de um usuário.
  * *Enviar por push toosegment com marcas dinâmicas*: marcas recurso ajuda a dispositivos de segmento e por push toothem de acordo com as necessidades tooyour, se você estiver enviando tooone segmento ou uma expressão de segmentos (por exemplo, ativo e reside em Seattle não novo usuário). Em vez de ser restrito toopub-sub, você pode atualizar as marcas de dispositivo em qualquer lugar e a qualquer momento.
  * *Notificações por push localizadas*: recurso de modelos que ajuda você a alcançar uma localização sem afetar o código de back-end.
  * *Push silenciosa*: pode permite padrão de envio para recepção Olá enviando notificações silenciosa toodevices e dispará-los toocomplete determinados recebe ou ações.
  * *Agendado push*: você pode agendar toosend notificações a qualquer momento.
  * *Direcionar push*: você pode ignorar o registro de dispositivos com nosso serviço e a lista de tooa envio em lote de identificadores de dispositivo diretamente.
  * *Notificações por push personalizadas*: as variáveis de envio a dispositivo ajudam você a enviar notificações por push personalizadas específicas para o dispositivo com pares de valor-chave personalizados.
* **Telemetria avançada**
  
  * Telemetria de push, o dispositivo, o erro e operação geral está disponível no hello portal do Azure e programaticamente.
  * Por mensagem telemetria rastreia cada push do serviço solicitação inicial chamada tooour com êxito em lote Olá envia.
  * Comentários de sistema de notificação de plataforma comunica-se todos os comentários dos sistemas de notificação Platfom tooassist na depuração.
* **Escalabilidade** 
  
  * Envie mensagens rápida toomillions de dispositivos sem fragmentação rearquitetura ou dispositivo.
* **Segurança**

  * Segredo de acesso compartilhado (SAS) ou autenticação federada.

## <a name="integration-with-app-service-mobile-apps"></a>Integração com Aplicativos Móveis do Serviço de Aplicativo
toofacilitate uma experiência perfeita e unificar em serviços do Azure, [aplicativo de serviço móvel aplicativos] tem suporte interno para notificações por push usando os Hubs de notificação. [aplicativo de serviço móvel aplicativos] oferece uma plataforma de desenvolvimento de aplicativos móveis altamente escalonável, globalmente disponíveis para os desenvolvedores corporativos e integradores de sistema que oferece um conjunto avançado de recursos toomobile desenvolvedores.

Os desenvolvedores de aplicativos móveis podem usar Hubs de notificação com hello fluxo de trabalho a seguir:

1. Recuperar o identificador de PNS do dispositivo
2. Registrar o dispositivo com Hubs de Notificação por meio da conveniente API de registro do SDK do cliente de Aplicativos Móveis
   * Observe que os aplicativos móveis removem imediatamente todas as marcas nos registros para fins de segurança. Trabalhar com Hubs de notificação do seu back-end diretamente tooassociate marcas com dispositivos.
3. Enviar notificações do seu back-end de aplicativo com Hubs de notificação

Aqui estão alguns conveniências colocadas toodevelopers com essa integração:

* **SDK de cliente de aplicativos móveis**: esses SDKs de multi-plataforma fornecem APIs simples para o registro e fale toohello hub de notificação vinculado com o aplicativo móvel Olá automaticamente. Os desenvolvedores não precisam toodig por meio de credenciais de Hubs de notificação e trabalhar com um serviço adicional.

  * *Enviar por push toouser*: Olá SDKs automaticamente marca Olá dado dispositivo com aplicativos móveis autenticado ID de usuário tooenable push toouser cenário.
  * *Enviar por push toodevice*: Olá SDKs usam automaticamente Olá ID de instalação de aplicativos móveis como GUID tooregister com Hubs de notificação, salvando os desenvolvedores problemas de saudação de manter vários GUIDs de serviço.
* **Modelo de instalação**: aplicativos móveis funciona com Hubs de notificação mais recentes push modelo toorepresent todas as propriedades associadas a um dispositivo em uma instalação de JSON que se alinha com serviços de notificação por Push e é fácil toouse enviar por push.
* **Flexibilidade**: os desenvolvedores podem escolher sempre toowork com Hubs de notificação diretamente até mesmo com a integração de saudação em vigor.
* **Experiência em integrada [portal do Azure]**: Push como um recurso é representado visualmente em aplicativos móveis e os desenvolvedores podem trabalhar facilmente com o hub de notificação associado Olá por meio de aplicativos móveis.

## <a name="next-steps"></a>Próximas etapas
Você pode encontrar mais informações sobre Hubs de Notificação nestes tópicos:

* **[Como os clientes usam os Hubs de Notificação]**
* **[Tutoriais e guias de Hubs de notificação]**
* **Tutoriais de introdução aos Hubs de Notificação**: [iOS], [Android], [Windows Universal], [Windows Phone], [Kindle], [Xamarin.iOS], [Xamarin.Android]

[0]: ./media/notification-hubs-overview/registration-diagram.png
[1]: ./media/notification-hubs-overview/notification-hub-diagram.png
[Como os clientes usam os Hubs de Notificação]: http://azure.microsoft.com/services/notification-hubs
[Tutoriais e guias de Hubs de notificação]: http://azure.microsoft.com/documentation/services/notification-hubs
[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started
[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started
[Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started
[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started
[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started
[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started
[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started
[Microsoft.WindowsAzure.Messaging.NotificationHub]: http://msdn.microsoft.com/library/microsoft.windowsazure.messaging.notificationhub.aspx
[Microsoft.ServiceBus.Notifications]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.aspx
[aplicativo de serviço móvel aplicativos]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/
[templates]: notification-hubs-templates-cross-platform-push-messages.md
[portal do Azure]: https://portal.azure.com
[tags]: (http://msdn.microsoft.com/library/azure/dn530749.aspx)
