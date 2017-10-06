---
title: "entidades de mensagens de barramento de serviço do Azure de encaminhamento aaaAuto | Microsoft Docs"
description: "Como toochain um barramento de serviço fila ou assinatura tooanother fila ou um tópico."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a>Encadeando entidades do Barramento de Serviço com o encaminhamento automático

Olá barramento de serviço *encaminhamento automático* recurso permite que você toochain uma fila ou assinatura tooanother fila ou um tópico que faz parte da saudação mesmo namespace. Quando o encaminhamento automático está habilitado, barramento de serviço automaticamente remove as mensagens que são colocadas na primeira fila de saudação ou assinatura (origem) e as coloca na fila segundo hello ou tópico (destino). Observe que é possível toosend uma entidade de destino toohello mensagem diretamente. Além disso, não é possível toochain uma subfila, tal como uma fila de mensagens mortas, tooanother fila ou tópico.

## <a name="using-auto-forwarding"></a>Usando o encaminhamento automático
Você pode habilitar o encaminhamento automático definindo Olá [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] ou [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] propriedades em Olá [QueueDescription] [ QueueDescription] ou [SubscriptionDescription] [ SubscriptionDescription] objetos origem hello, como Olá exemplo a seguir.

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

entidade de destino Olá deve existir no tempo de saudação Olá fonte entidade é criada. Se a entidade de destino Olá não existir, o barramento de serviço retorna uma exceção quando toocreate frequentes Olá entidade de origem.

Você pode usar o encaminhamento automático tooscale-out de um tópico individual. Saudação de limites de barramento de serviço [número de assinaturas em um determinado tópico](service-bus-quotas.md) too2, 000. Você pode acomodar outras assinaturas criando tópicos de segundo nível. Observe que mesmo se você não estiver vinculado Olá limitação no número de saudação de assinaturas, adicionar tópicos de segundo nível pode melhorar o barramento de serviço Olá produtividade geral do seu tópico.

![Cenário de encaminhamento automático][0]

Você também pode usar o encaminhamento automático toodecouple remetentes dos destinatários. Por exemplo, considere um sistema ERP composto por três módulos: processamento de pedidos, gerenciamento de estoque e gerenciamento de relacionamentos com o cliente. Cada um desses módulos gera mensagens que são enfileiradas em um tópico correspondente. Alice e Bob é representantes de vendas interessados em todas as mensagens relacionadas tootheir clientes. tooreceive as mensagens, Alice e Bob cria uma fila pessoal e uma assinatura em cada um dos tópicos ERP Olá que encaminham automaticamente todas as filas de tootheir de mensagens.

![Cenário de encaminhamento automático][1]

Se a Eliane tirar férias, sua fila pessoal, em vez de tópico ERP hello, preenchido. Nesse cenário, porque um representante de vendas não recebeu as mensagens, nenhum dos tópicos ERP Olá atingiu a cota.

## <a name="auto-forwarding-considerations"></a>Considerações sobre o encaminhamento automático

Se entidade de destino Olá acumula muitas mensagens e excede a cota de hello, ou entidade de destino hello está desabilitada, entidade de origem Olá adiciona mensagens de saudação tooits [fila de mensagens mortas](service-bus-dead-letter-queues.md) até que haja espaço no destino Olá (ou entidade de saudação é reativada). Essas mensagens continuará toolive na fila de mensagens mortas hello, para que você deve receber e processá-los da fila de mensagens mortas Olá explicitamente.

Ao encadear tópicos individuais tooobtain um tópico composto com diversas assinaturas, é recomendável que você tenha um número moderado de assinaturas no tópico de primeiro nível hello e diversas assinaturas nos tópicos de segundo nível hello. Por exemplo, um tópico de primeiro nível com 20 assinaturas, cada uma delas encadeada tooa tópico de segundo nível com 200 assinaturas, permite mais rendimento do que um tópico de primeiro nível com 200 assinaturas, cada uma encadeada tooa tópico de segundo nível com 20 assinaturas .

O Barramento de Serviço cobra uma operação por cada mensagem encaminhada. Por exemplo, enviando um tópico de mensagem de tooa com 20 assinaturas, cada um deles configurado tooauto encaminhar mensagens tooanother fila ou tópico, é cobrada como 21 operações se todas as assinaturas de primeiro nível recebem uma cópia da mensagem de saudação.

toocreate uma assinatura encadeada tooanother fila ou tópico, o criador de saudação de assinatura Olá deve ter **gerenciar** permissões na origem hello e entidade de destino hello. Enviar somente requer um tópico de origem toohello mensagens **enviar** permissões no tópico de origem hello.

## <a name="next-steps"></a>Próximas etapas

Para obter informações detalhadas sobre o encaminhamento automático, consulte Olá tópicos de referência a seguir:

* [ForwardTo][QueueDescription.ForwardTo]
* [QueueDescription][QueueDescription]
* [SubscriptionDescription][SubscriptionDescription]

toolearn mais informações sobre aprimoramentos de desempenho do barramento de serviço, consulte 

* [Práticas recomendadas para melhorias de desempenho usando o Sistema de Mensagens do Barramento de Serviço](service-bus-performance-improvements.md)
* [Entidades de mensagens particionadas][Partitioned messaging entities].

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
