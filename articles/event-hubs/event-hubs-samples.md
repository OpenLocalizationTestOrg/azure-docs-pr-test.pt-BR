---
title: exemplos de Hubs de eventos aaaAzure | Microsoft Docs
description: Exemplos de Hubs de Eventos do Azure
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a>Exemplos de Hubs de Eventos 

conjunto de amostras de Hubs de eventos do Azure Hello demonstra os principais recursos [Hubs de eventos do Azure](/azure/event-hubs/). Este artigo categoriza e descreve Olá exemplos disponíveis, com links tooeach.

Em tempo de saudação da redação deste artigo, exemplos de Hubs de eventos estão localizados em vários lugares diferentes:

- [Exemplos de código do desenvolvedor do MSDN](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples)

Para obter mais informações sobre as diferentes versões de saudação do .NET Framework, consulte [estruturas e destinos](/dotnet/articles/standard/frameworks).

Mais exemplos será adicionado ao longo do tempo, então verifique novamente com frequência para atualizações.

## <a name="net-standard"></a>.NET Standard

Olá exemplos a seguir demonstram como toosend e receber eventos usando Olá [cliente Hubs de eventos](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) para Olá [biblioteca .NET padrão](/dotnet/articles/standard/library).

### <a name="send-events"></a>Enviar eventos 

Olá [começar a enviar](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) exemplo mostra como o aplicativo que envia o hub de eventos de tooan eventos de console toowrite um núcleo do .NET.

### <a name="receive-events"></a>Receber eventos 

Olá [começar a receber com hello Host de processador de evento](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) exemplo é um aplicativo de console .NET Core que recebe mensagens de um hub de eventos usando Olá Host de processador de evento.

## <a name="net-framework"></a>.NET Framework   

Esses exemplos demonstram vários outros recursos de Hubs de eventos do Azure, direcionando Olá [biblioteca do .NET Framework](/dotnet/framework/index).
 
### <a name="notify-users-of-events-received"></a>Notificar os usuários de eventos recebidos

Olá [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) exemplo notifica os usuários dos dados recebidos de sensores ou outros sistemas.

### <a name="get-started-with-event-hubs"></a>Introdução aos Hubs de Eventos 

Olá [guia de Introdução do evento Hubs](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) demonstra os recursos básicos de saudação de Hubs de eventos, como toocreate um hub de eventos, enviar o hub de eventos de tooan de eventos e consumir eventos usando Olá [Host de processador de evento](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).

### <a name="scale-out-event-processing"></a>Processamento de eventos de escala horizontal 

Olá [expansão de processamento de eventos](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) demonstra como Olá toouse [Host de processador de evento](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute carga de trabalho de saudação do consumo de fluxo de Hubs de eventos. Ele mostra como Olá tooimplement **EventProcessor** e **EventProcessorFactory** fluxo de eventos objetos toomanage hello. 

###  <a name="pull-data-from-sql-into-an-event-hub"></a>Efetuar pull de dados do SQL para um hub de eventos

Olá [de dados do SQL puxando](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) exemplo mostra como toopull dados de um SQL de tabela e por push tooan hub de eventos, toouse como uma entrada em aplicativos analíticos downstream.

### <a name="pull-web-data-into-an-event-hub"></a>Efetuar pull de dados da Web para um hub de eventos 

Olá [importar dados de Olá web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) exemplo mostra como os dados toopull do público feeds (como Olá feed de informações de tráfego do departamento de transporte) e por push tooan hub de eventos.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre as versões do .NET Framework visitando Olá links a seguir:

- [Estruturas e destinos](/dotnet/articles/standard/frameworks)
- [.NET Framework 4.6 e 4.5](/dotnet/framework/index)

Você pode aprender mais sobre os Hubs de eventos Olá artigos a seguir:

- [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
- [Criar um hub de eventos](event-hubs-create.md)
- [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)