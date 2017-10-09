---
title: "aaaAzure Premium do barramento de serviço e o sistema de mensagens padrão preços camadas visão geral | Microsoft Docs"
description: "Camadas de sistema de mensagens Premium e Standard do Barramento de Serviço"
services: service-bus-messaging
documentationcenter: .net
author: djrosanova
manager: timlt
editor: 
ms.assetid: e211774d-821c-4d79-8563-57472d746c58
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: darosa;sethm
ms.openlocfilehash: 4eea5d86d342e858f50450308fb3d96a7a80b49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a>Camadas de sistema de mensagens Premium e Standard do Barramento de Serviço

O Sistema de Mensagens do Barramento de Serviço, que inclui entidades como filas e tópicos, combina recursos corporativos de mensagens com rica semântica de assinatura para publicação na escala de nuvem. Mensagens do barramento de serviço é usado como o backbone de comunicação Olá muitas soluções sofisticadas de nuvem.

Olá *Premium* endereços de camada do sistema de mensagens do barramento de serviço comum solicitações de clientes em escala, desempenho e disponibilidade para aplicativos de missão crítica. Embora os conjuntos de recursos de saudação são quase idênticos, essas duas camadas de sistema de mensagens do barramento de serviço são tooserve projetado diferentes casos de uso.

Algumas diferenças de alto nível são realçadas em Olá a tabela a seguir.

| Premium | Standard |
| --- | --- |
| Alta taxa de transferência |Taxa de transferência variável |
| Desempenho previsível |Latência variável |
| Preço fixo |Preço pré-pago variável |
| Carga de trabalho de tooscale de capacidade para cima e para baixo |N/D |
| Tamanho da mensagem too1 MB |Tamanho da mensagem too256 KB |

**Mensagens do Service Bus Premium** fornece isolamento no nível de CPU e memória de saudação do recurso para que cada carga de trabalho do cliente é executada em isolamento. Esse contêiner de recurso é chamado de *unidade do sistema de mensagens*. Cada namespace premium é alocado para pelo menos uma unidade do sistema de mensagens. Você pode adquirir 1, 2 ou 4 unidades do sistema de mensagens para cada namespace Premium do Barramento de serviço. Uma única carga de trabalho ou uma entidade pode abranger várias unidades de sistema de mensagens e número de saudação de unidades de sistema de mensagens pode ser alterado conforme o desejado, embora a cobrança é em encargos de taxa de 24 horas ou diária. resultado de saudação é desempenho previsível e reproduzível para sua solução com base no barramento de serviço.

Esse desempenho não é apenas o mais previsível e disponível, mas também o mais rápido. Mensagens do Service Bus Premium se baseia no mecanismo de armazenamento Olá introduzido no [Hubs de eventos do Azure](https://azure.microsoft.com/services/event-hubs/). Com o sistema de mensagens Premium, é muito mais rápido do que com a camada padrão Olá pico de desempenho.

## <a name="premium-messaging-technical-differences"></a>Diferenças técnicas do sistema de mensagens Premium

Olá seções a seguir discutem algumas diferenças entre as camadas de mensagens padrão e Premium.

### <a name="partitioned-queues-and-topics"></a>Filas e tópicos particionados

Filas e tópicos particionados têm suporte no Sistema de Mensagens Premium; na verdade essas entidades são particionadas sempre (e não podem ser desabilitadas). No entanto, Premium particionado filas e tópicos não funcionam Olá Olá a mesma forma como no camadas Standard e Basic do barramento de serviço de mensagens. Não Premium mensagens usa SQL como um repositório de dados e não tem Olá competição possível de recursos associada a uma plataforma compartilhada. Como resultado, o particionamento não é necessário tooimprove desempenho. Além disso, a contagem de partição Olá foi alterada de 16 partições em partições too2 padrão de mensagens Premium. Ter duas partições garante a disponibilidade e é um número mais apropriado para o ambiente de tempo de execução Premium Olá. 

Com o sistema de mensagens Premium, quando você especifica o tamanho de saudação de uma entidade com [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes), que tamanho é dividido igualmente entre partições Olá 2, diferentemente de [padrão particionada entidades](service-bus-partitioning.md#standard) no qual Olá tamanho total é 16 vezes tamanho especificado de saudação. 

Para saber mais sobre o particionamento, confira as [Filas e tópicos particionados](service-bus-partitioning.md).

### <a name="express-entities"></a>Entidades expressas

Como o sistema de mensagens Premium é executado em um ambiente de tempo de execução totalmente isolado, não há suporte para as entidades expressas em namespaces Premium. Para obter mais informações sobre o recurso express hello, consulte Olá [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) propriedade.

Se você tiver código em execução em tooport padrão de mensagens e desejar que ele camada Premium de toohello, verifique se Olá [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) propriedade for definida muito**false** (Olá valor padrão).

## <a name="get-started-with-premium-messaging"></a>Introdução ao sistema de mensagens Premium

Introdução ao sistema de mensagens Premium é simples e processo de saudação é semelhante toothat do sistema de mensagens padrão. Comece [criando um namespace](service-bus-create-namespace-portal.md). Verifique se você selecionou **Premium** em **Tipo de preços**.

![criar-premium-namespace][create-premium-namespace]

Você também pode criar um [Namespace Premium usando modelos do Azure Resource Manager](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).


## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre mensagens do Service Bus, consulte Olá tópicos a seguir.

* [Introdução ao Sistema de Mensagens Premium do Barramento de Serviço do Azure (postagem de blog)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Introdução ao Sistema de Mensagens Premium do Barramento de Serviço do Azure (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Visão geral do Sistema de Mensagens do Barramento de Serviço](service-bus-messaging-overview.md)
* [Como as filas do barramento de serviço toouse](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
