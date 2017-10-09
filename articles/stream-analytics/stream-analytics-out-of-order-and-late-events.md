---
title: aaaHandling ordem de eventos e lateness com o Azure Stream Analytics | Microsoft Docs
description: Saiba como o Stream Analytics funciona com eventos fora de ordem ou atrasados nos fluxos de dados.
keywords: fora de ordem, atraso, eventos
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Manipulação da ordem dos eventos do Azure Stream Analytics

Em um fluxo de dados temporais dos eventos, cada evento é registrado com o tempo de saudação Olá evento é recebido. Algumas condições podem causar fluxos de eventos toooccasionally receber alguns eventos em uma ordem diferente do qual eles foram enviados. Um simple TCP retransmitir ou até mesmo uma defasagem horária entre hello enviando dispositivo e hello recebendo hub de eventos pode causar esse toooccur. Eventos de "Pontuação" também são adicionados tooreceived fluxos de eventos, tempo de saudação tooadvance na ausência de saudação de entradas de eventos. Eles são necessários em cenários como "Notificar-me quando nenhum logon ocorrer por três minutos".

Os fluxos de entrada que não estão em ordem são:
* Classificados (e, portanto, **atrasados**).
* Ajustada pelo sistema hello, de acordo com a política de usuário especificado de tooa.


## <a name="lateness-tolerance"></a>Tolerância de atraso
O Stream Analytics tolera esses tipos de cenários. O Stream Analytics tem tratamento para eventos "fora de ordem" e "em atraso". Ele trata esses eventos em Olá maneiras a seguir:

* Os eventos que chegam fora de ordem, mas dentro Olá definir tolerância são **reordenadas por data/hora**.
* Os eventos que chegam após o tempo de tolerância são **removidos ou ajustados**.
    * **Ajustado**: toohave tooappear ajustada acessou hello mais recente de tempo aceitável.
    * **Removidos**: descartados.

![Manipulação de eventos do Stream Analytics](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a>Reduzir o número de saudação de eventos fora de ordem

Uma vez que o Stream Analytics aplica uma transformação temporal quando processa eventos de entrada (por exemplo, para agregações com janela ou uniões temporais), ele classifica eventos de entrada pela ordem do carimbo de data/hora.

Quando for hello "timestamp por" palavra-chave **não** usado, o tempo de enfileiramento de evento de Hubs de eventos do Azure Olá é usado por padrão. Hubs de eventos garante monotonicidade do hello timestamp em cada partição do hub de eventos de saudação. Eles também garantem que os eventos de todas as partições sejam mesclados na ordem do carimbo de data/hora. Essas duas garantias dos Hubs de Eventos asseguram que não haja eventos fora de ordem.

Às vezes, é importante para o carimbo de hora você toouse saudação do remetente. Nesse caso, um carimbo de hora de carga do evento Olá é escolhido usando "timestamp por". Nesses cenários, uma ou mais fontes de ordem incorreta podem ser introduzidas:

* Os produtores de eventos têm defasagem horária. Isso é comum quando produtores são de diferentes computadores, pois eles têm relógios diferentes.
* Há um atraso de rede da fonte de saudação do hub de eventos Olá eventos toohello destino.
* As defasagens horárias existem entre partições do hub de eventos. O Stream Analytics primeiro classifica os eventos de todas as partições do hub de eventos pela hora de enfileiramento do evento. Em seguida, ele examina TDS Olá para ordenação incorreta desses eventos.

Na guia de configuração do hello, você verá Olá padrões a seguir:

![Manipulação de eventos fora de ordem do Stream Analytics](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

Se você usar 0 segundos como a janela de tolerância de fora de ordem de hello, está afirmando que todos os eventos estão na ordem todo o tempo de saudação. Fontes de saudação três de ordenação incorreta desses eventos, é improvável que isso é verdadeiro. 

Análise de fluxo de tooallow toocorrect misorder um evento, você pode especificar uma janela de tolerância de fora de ordem diferente de zero. Eventos de buffers de análise de fluxo toothat janela e, em seguida, reorganiza-los usando Olá carimbo de hora que você escolheu. Ele aplica transformação temporal hello. Você pode começar com uma janela de 3 segundos e ajustar Olá valor tooreduce Olá quantos eventos de tempo ajustado. 

Um efeito colateral do buffer de saudação é saída de hello **atrasado por Olá mesmo período de tempo**. Você pode ajustar Olá valor tooreduce Olá quantos eventos fora de ordem e reduzir a latência de saudação do trabalho.

## <a name="get-help"></a>Obter ajuda
Para obter mais ajuda, teste nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooStream análise](stream-analytics-introduction.md)
* [Introdução ao Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência da linguagem de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST de gerenciamento do Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)