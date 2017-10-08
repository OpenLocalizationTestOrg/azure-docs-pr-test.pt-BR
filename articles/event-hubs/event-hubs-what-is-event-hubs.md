---
title: "aaaWhat Hubs de eventos do Azure e usá-lo por | Microsoft Docs"
description: "Visão geral e introdução tooAzure Hubs de eventos - inclusão de telemetria de escala de nuvem de sites, aplicativos e dispositivos"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a>O que são Hubs de Eventos?

Os Hubs de Evento do Azure são um plataforma de transmissão de dados altamente dimensionável e um serviço de ingestão de dados capaz de receber e processar milhões de eventos por segundo. Os Hubs de Eventos podem processar e armazenar eventos, dados ou telemetria produzidos pelos dispositivos e software distribuídos. Os dados enviados tooan hub de eventos pode ser transformado e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de envio em lote/armazenamento. Com hello capacidade tooprovide [recursos de publicação / assinatura](https://msdn.microsoft.com/library/aa560414.aspx) com baixa latência e em grande escala, Hubs de eventos serve como Olá "no painel" para dados grandes.

## <a name="why-use-event-hubs"></a>Por que usar Hubs de Eventos?

Os eventos de Hubs de Eventos e os recursos de manipulação de telemetria o tornam especialmente útil para:

* Instrumentação de aplicativos
* Experiência do usuário ou o processamento de fluxo de trabalho
* Cenários de IoT (Internet das coisas)

Por exemplo, os Hubs de Eventos habilitam o rastreamento de comportamentos em aplicativos móveis, informações do tráfego de web farms, captura de eventos de jogos em jogos de console ou telemetria coletada de máquinas industriais, veículos conectados ou outros dispositivos.

## <a name="azure-event-hubs-overview"></a>Visão geral dos Hubs de Eventos do Azure

função comum que os Hubs de eventos desempenham em arquiteturas de solução Hello é hello "porta da frente" para um pipeline de eventos, geralmente chamada um *ingestor de eventos*. Um ingestor de eventos é um componente ou serviço que fica entre a produção de hello do evento consumidores toodecouple de um fluxo de eventos do consumo Olá desses eventos e editores de eventos. Olá figura a seguir ilustra essa arquitetura:

![Hubs de Eventos](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

Os Hubs de Eventos fornecem recurso de manipulação de fluxo de mensagens, mas têm características que são diferentes das mensagens corporativas tradicionais. Os recursos de Hubs de Eventos são criados em torno de cenários de alta produtividade e de processamento de eventos. Como tal, os Hubs de eventos é diferente do [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) mensagens e não implementa alguns dos recursos de saudação que estão disponíveis para [mensagens do barramento de serviço](/azure/service-bus-messaging/) entidades, como tópicos.

## <a name="event-hubs-features"></a>Recursos de Hubs de Eventos

Hubs de eventos contém Olá principais elementos a seguir:

- [**Editores/produtores de eventos**](event-hubs-features.md#event-publishers): uma entidade que envia o hub de eventos de tooan de dados. Um evento é publicado por meio de AMQP 1.0 ou HTTPS.
- [**Capturar**](event-hubs-features.md#capture): permite que os Hubs de eventos toocapture fluxo de dados e armazená-lo em uma conta de armazenamento de BLOBs do Azure.
- [**Partições**](event-hubs-features.md#partitions): permite que cada consumidor tooonly ler um subconjunto específico ou partição, de Olá fluxo de eventos.
- [**Tokens SAS**](event-hubs-features.md#sas-tokens): identifica e autentica o publicador do evento hello.
- [**Consumidores de evento**](event-hubs-features.md#event-consumers): qualquer entidade que leia dados de evento de um hub de eventos. Os consumidores do evento se conectam por meio de AMQP 1.0. 
- [**Grupos de consumidores**](event-hubs-features.md#consumer-groups): fornece cada múltiplo consumindo o aplicativo com uma exibição separada saudação do fluxo de eventos, permitindo que os consumidores tooact independentemente.
- [**Unidades de produtividade**](event-hubs-features.md#capacity): unidades de capacidade pré-adquiridas. Uma única partição tem uma escala máxima de 1 unidade de transferência.

Para obter detalhes técnicos sobre esses e outros recursos de Hubs de eventos, consulte Olá [visão geral dos recursos de Hubs de eventos](event-hubs-features.md). 

## <a name="next-steps"></a>Próximas etapas

Para obter informações sobre preços de Hubs de Evento, consulte [Preços de Hubs de Evento](https://azure.microsoft.com/pricing/details/event-hubs/).

Para obter mais informações sobre Hubs de eventos, visite Olá links a seguir:

* Introdução com um [Tutorial de Hubs de Eventos](event-hubs-dotnet-standard-getstarted-send.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)
* [Aplicativos de exemplo que usam Hub de Eventos](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

