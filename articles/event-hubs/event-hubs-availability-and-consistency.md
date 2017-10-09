---
title: "aaaAvailability e a consistência nos Hubs de eventos do Azure | Microsoft Docs"
description: "Como tooprovide Olá máximo de disponibilidade e a consistência com Hubs de eventos do Azure usando partições."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a>Disponibilidade e consistência nos Hubs de Eventos

## <a name="overview"></a>Visão geral
Hubs de eventos do Azure usa um [particionamento modelo](event-hubs-features.md#partitions) tooimprove paralelização dentro de um hub de evento único e disponibilidade. Por exemplo, se um hub de eventos tem quatro partições, e um essas partições é movido de um servidor tooanother em uma operação de balanceamento de carga, você ainda pode enviar e receber de três outras partições. Além disso, ter mais partições permite que você toohave leitores simultâneos mais processar seus dados, melhorando a taxa de transferência agregada. Noções básicas sobre as implicações de saudação de particionamento e a ordenação em um sistema distribuído é um aspecto crítico de design da solução.

toohelp explicam a compensação de saudação entre pedidos e disponibilidade, consulte Olá [Teorema de CAP](https://en.wikipedia.org/wiki/CAP_theorem), também conhecido como Teorema do Brewer. Este Teorema discute escolha Olá entre consistência, disponibilidade e tolerância a partição.

O teorema de Brewer define a consistência e a disponibilidade como a seguir:
* Tolerância de partição: Olá a capacidade de um toocontinue do sistema de processamento de dados processamento de dados mesmo se ocorrer uma falha de partição.
* Disponibilidade: um nó sem falha retorna uma resposta razoável dentro de um período razoável (sem erros nem tempos limites).
* Consistência: uma leitura é garantida tooreturn hello mais recente na gravação para um determinado cliente.

## <a name="partition-tolerance"></a>Tolerância a partição
Os Hubs de Eventos são criados sobre um modelo de dados particionado. Você pode configurar o número de saudação de partições em seu hub de eventos durante a instalação, mas você não pode alterar esse valor posteriormente. Como você deve usar partições com Hubs de eventos, você tem toomake uma decisão sobre a disponibilidade e a consistência de seu aplicativo.

## <a name="availability"></a>Disponibilidade
Olá tooget de maneira mais simples de Introdução com Hubs de eventos é o comportamento do toouse saudação padrão. Se você criar um novo `EventHubClient` de objeto e usar Olá `Send` método, os eventos são distribuídos automaticamente entre partições em seu hub de eventos. Esse comportamento permite Olá maior quantidade de tempo.

Para casos de uso que exigem o máximo de saudação o tempo, esse modelo é preferencial.

## <a name="consistency"></a>Consistência
Em alguns cenários, a saudação de ordenação de eventos pode ser importante. Por exemplo, talvez você queira tooprocess seu sistema back-end um comando de atualização antes de um comando de exclusão. Neste exemplo, defina a chave de partição Olá em um evento ou use um `PartitionSender` tooonly objeto enviar eventos tooa certa partição. Isso garante que, quando esses eventos são lidos da partição hello, que são lidas em ordem.

Com essa configuração, tenha em mente que, se Olá determinada partição toowhich que estiver enviando não estiver disponível, você receberá uma resposta de erro. Como um ponto de comparação, se você não tiver uma partição única tooa de afinidade, hello serviço de Hubs de eventos envia a evento toohello próxima partição disponível.

Um tooensure solução possível ordenação, maximizando o tempo, também seria tooaggregate eventos como parte de seu aplicativo de processamento de eventos. Olá tooaccomplish de maneira mais fácil isso é toostamp seu evento com uma propriedade de número de sequência personalizado. saudação de código a seguir mostra um exemplo:

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

Este exemplo envia sua tooone de evento de partições disponíveis Olá em seu hub de eventos e define o número de sequência correspondente de saudação do seu aplicativo. Essa solução requer toobe estado mantido pelo seu aplicativo de processamento, mas oferece os remetentes um ponto de extremidade que é mais provável toobe disponível.

## <a name="next-steps"></a>Próximas etapas
Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão geral do serviço dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um hub de eventos](event-hubs-create.md)
