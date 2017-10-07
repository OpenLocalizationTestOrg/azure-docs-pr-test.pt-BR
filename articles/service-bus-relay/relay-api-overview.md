---
title: "Visão geral da API de retransmissão aaaAzure | Microsoft Docs"
description: "Visão geral das APIs de Retransmissão do Azure disponíveis"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a>APIs de Retransmissão disponíveis

## <a name="runtime-apis"></a>APIs de tempo de execução

Olá tabela a seguir lista todos os clientes de tempo de execução de retransmissão disponíveis no momento.

Olá [informações adicionais](#additional-information) seção contém mais informações sobre o status de saudação de cada biblioteca de tempo de execução.

| Linguagem/plataforma | Recurso disponível | Pacote de cliente | Repositório |
| --- | --- | --- | --- |
| .NET Standard | Conexões Híbridas | [Microsoft.Azure.Relay](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [GitHub](https://github.com/azure/azure-relay-dotnet) |
| .NET Framework | Retransmissão de WCF | [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | N/D |
| Nó | Conexões Híbridas | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [GitHub](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a>Informações adicionais

#### <a name="net"></a>.NET
ecossistema do .NET Olá tem vários tempos de execução, portanto, há várias bibliotecas .NET para Hubs de eventos. biblioteca .NET padrão Olá pode ser executada usando o .NET Core ou saudação do .NET Framework, enquanto a biblioteca do .NET Framework Olá só pode ser executada em um ambiente do .NET Framework. Para saber mais sobre o .NET Framework, veja [versões da estrutura](/dotnet/articles/standard/frameworks#framework-versions).

## <a name="next-steps"></a>Próximas etapas
toolearn mais informações sobre a retransmissão do Azure, visite esses links:
* [O que é Retransmissão do Azure?](relay-what-is-it.md)
* [Perguntas frequentes sobre retransmissão](relay-faq.md)