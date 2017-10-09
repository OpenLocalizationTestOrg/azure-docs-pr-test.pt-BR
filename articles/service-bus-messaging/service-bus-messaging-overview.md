---
title: "Visão geral da mensagem do Service Bus aaaAzure | Microsoft Docs"
description: "Descrição de sistema de mensagens do Barramento de Serviço e Retransmissão do Azure"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f99766cb-8f4b-4baf-b061-4b1e2ae570e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: ede2904e11544d8f9428a2d657dcc77dacd95ac4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-flexible-data-delivery-in-hello-cloud"></a>Mensagens do barramento de serviço: entrega de dados flexível em nuvem Olá
O Barramento de Serviço do Microsoft Azure é um serviço de entrega de informações confiáveis. finalidade de saudação do serviço é toomake comunicação mais fácil. Quando dois ou mais participantes deseja informações de tooexchange, eles precisam de um facilitador de comunicação. O Barramento de Serviço é um mecanismo de comunicação agenciado ou de terceiros. Isso é semelhante correios tooa em Olá, mundo físico. Postal serviços tornam muito fácil toosend diferentes tipos de letras e pacotes com uma variedade de garantias de entrega, em qualquer lugar no Olá, mundo.

Semelhante toohello correios letras, barramento de serviço de entrega é entrega flexível de informações da saudação remetente e destinatário hello. serviço de mensagens de saudação garante que o informações Olá seja entregue mesmo se partes Olá dois estiver nunca ambos online no hello ao mesmo tempo, ou se eles não estão disponíveis em Olá exato mesmo tempo. Dessa forma, mensagens é semelhante toosending uma letra, enquanto não orientadas comunicação é semelhante tooplacing uma chamada telefônica (ou como uma chamada telefônica usada toobe - antes da chamada em espera e o chamador ID, que são muito mais mensagens orientadas).

remetente de mensagem de saudação também pode exigir uma variedade de características de entrega, inclusive transações, detecção de duplicidades, com base em tempo de expiração e envio em lote. Esses padrões também têm analogias postais: repetir a entrega, assinatura exigida, alteração de endereço ou recuperação.

O Barramento de Serviço dá suporte a dois padrões distintos de sistema de mensagens: *Retransmissão do Azure* e *Sistema de Mensagens do Barramento de Serviço*.

## <a name="azure-relay"></a>Retransmissão do Azure
Olá [retransmissão WCF](../service-bus-relay/relay-what-is-it.md) componente de retransmissão do Azure é um serviço centralizado (mas altamente com balanceamento de carga) que oferece suporte a uma variedade de protocolos de transporte e padrões de serviços Web. Isso inclui SOAP, WS-* e até REST. Olá [serviço de retransmissão](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md) fornece uma variedade de opções de conectividade de retransmissão e pode ajudar a negociar conexões diretas de ponto a ponto quando possível. Barramento de serviço é otimizado para desenvolvedores de .NET que usam Olá Windows Communication Foundation (WCF), ambos com tooperformance de relação e a usabilidade, e fornece acesso completo tooits serviço de retransmissão por meio de interfaces SOAP e REST. Isso torna possível para qualquer programação SOAP e REST toointegrate de ambiente com o barramento de serviço.

serviço de retransmissão Olá suporta tradicional unidirecional de mensagens, mensagens de solicitação/resposta e mensagens ponto a ponto. Ele também dá suporte a distribuição de eventos no escopo da Internet tooenable publicação / assinatura cenários e comunicação do soquete bidirecional para eficiência de aumento de ponto a ponto. No padrão de mensagens de saudação retransmitida, um serviço local conecta-se o serviço de retransmissão toohello por meio de uma porta de saída e cria um soquete bidirecional para comunicação vinculada endereço de reunião em particular de tooa. cliente de Hello, em seguida, pode se comunicar com o serviço de local de saudação enviando mensagens do serviço de retransmissão toohello direcionando o endereço de reunião hello. serviço de retransmissão Hello "retransmitirá" serviço de local de toohello mensagens através do soquete bidirecional Olá já em vigor. Olá cliente não precisa de um serviço de local de toohello de conexão direta, nem é necessária de it tooknow onde Olá serviço reside e Olá local serviço não precisa de nenhuma porta de entrada aberta no firewall hello.

Iniciar conexão Olá entre o serviço local e serviço de retransmissão hello, usando um conjunto de associações de "retransmissão" do WCF. Em segundo plano hello, associações de retransmissão Olá mapeiam tootransport associação elementos projetados toocreate WCF canal componentes que se integram ao barramento de serviço na nuvem de saudação.

Retransmissão do WCF fornece muitos benefícios, mas requer Olá servidor e cliente tooboth estar online ao mesmo tempo em ordem toosend e receber mensagens de saudação. Isso não é ideal para comunicações no estilo HTTP, no qual Olá solicitações não podem ser normalmente vida útil longa, nem para clientes que se conectam eventualmente, como navegadores, aplicativos móveis e assim por diante. O sistema de mensagens agenciado oferece suporte à comunicação separada e tem suas próprias vantagens; clientes e servidores podem se conectar quando necessário e executar suas operações de maneira assíncrona.

## <a name="brokered-messaging"></a>Sistema de mensagens agenciado
Em contraste toohello retransmissão esquema, barramento de serviço do sistema de mensagens, ou [mensagens orientadas](service-bus-queues-topics-subscriptions.md) pode ser pensada como assíncronas ou "temporariamente desacoplado". Os produtores (remetentes) e os consumidores (destinatários) não há toobe online Olá simultaneamente. infraestrutura de mensagens de saudação confiável armazena mensagens em um "agente" (como uma fila) até que a parte consumidora hello está pronto tooreceive-los. Isso permite que os componentes de saudação do hello distribuída application toobe desconectado, voluntariamente; ou Por exemplo, para manutenção ou devido a falha do componente tooa, sem afetar o sistema inteiro hello. Além disso, o aplicativo de recebimento Olá pode ter somente toocome online durante determinadas horas do dia hello, como um sistema de gerenciamento de estoque que só é toorun necessária no final de saudação do dia de trabalho de saudação.

componentes principais do Hello da infraestrutura de mensagens orientadas Olá barramento de serviço são filas, tópicos e assinaturas.  Olá principal diferença é que tópicos oferecem suporte a recursos de publicação/assinatura que podem ser usados para sofisticadas com base em conteúdo de roteamento e entrega lógica, incluindo enviando toomultiple destinatários. Esses componentes permitem novos cenários de sistema de mensagens assíncrono, como separação temporal, publicação/assinatura e balanceamento de carga. Para saber mais sobre essas entidades de sistema de mensagens, consulte [Filas, tópicos e assinaturas do Barramento de Serviço](service-bus-queues-topics-subscriptions.md).

Com a infraestrutura de retransmissão do WCF hello, Olá mensagens orientadas recurso é fornecido para programadores do WCF e do .NET Framework e também por REST.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o sistema de mensagens do barramento de serviço, consulte Olá tópicos a seguir.

* [Conceitos fundamentais do barramento de serviço](service-bus-fundamentals-hybrid-solutions.md)
* [Filas, tópicos e assinaturas do Barramento de Serviço](service-bus-queues-topics-subscriptions.md)
* [Como as filas do barramento de serviço toouse](service-bus-dotnet-get-started-with-queues.md)
* [Como toouse Service Bus tópicos e assinaturas](service-bus-dotnet-how-to-use-topics-subscriptions.md)

