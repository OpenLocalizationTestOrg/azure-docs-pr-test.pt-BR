---
title: "Visão geral da API de Hubs de evento aaaAzure | Microsoft Docs"
description: "Visão geral das APIs de Hubs de Eventos do Azure disponíveis"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a>APIs de Hubs de Eventos disponíveis

## <a name="runtime-apis"></a>APIs de tempo de execução

a seguir Olá é uma descrição de todos os clientes de tempo de execução de Hubs de eventos do Azure disponíveis no momento. Embora algumas dessas bibliotecas também incluem a funcionalidade de gerenciamento limitado, também há [bibliotecas específicas](#management-apis) dedicado toomanagement operações. foco principal Olá essas bibliotecas é toosend e receber mensagens de um hub de eventos.

Consulte [informações adicionais](#additional-information) para obter mais detalhes sobre o status atual de saudação de cada biblioteca de tempo de execução.

| Linguagem/plataforma | Pacote de cliente | Pacote EventProcessorHost | Repositório |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [GitHub](https://github.com/azure/azure-event-hubs-dotnet) |
| .NET Framework | [NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | N/D |
| Java | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [GitHub](https://github.com/Azure/azure-event-hubs-java) |
| Nó | [NPM](https://www.npmjs.com/package/azure-event-hubs) | N/D | [GitHub](https://github.com/Azure/azure-event-hubs-node) |
| C | N/D | N/D | [GitHub](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a>Informações adicionais

#### <a name="net"></a>.NET
ecossistema do .NET Olá tem vários tempos de execução, portanto, há várias bibliotecas .NET para Hubs de eventos. biblioteca .NET padrão Olá pode ser executada usando o .NET Core ou saudação do .NET Framework, enquanto a biblioteca do .NET Framework Olá só pode ser executada em um ambiente do .NET Framework. Para saber mais sobre o .NET Framework, veja [versões da estrutura](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).

#### <a name="node"></a>Nó

biblioteca de Node. js Hello está atualmente em visualização e é mantida como um projeto por funcionários da Microsoft e colaboradores externos. Todas as contribuições, incluindo código-fonte são bem-vindas e serão analisadas.

## <a name="management-apis"></a>APIs de gerenciamento

a seguir Olá é uma lista de todas as bibliotecas específicas de gerenciamento disponíveis no momento. Nenhuma dessas bibliotecas contêm operações de tempo de execução e são o único propósito de saudação do gerenciamento de entidades de Hubs de eventos.

| Linguagem/plataforma | Pacote de gerenciamento | Repositório |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a>Próximas etapas
Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um hub de eventos](event-hubs-create.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)