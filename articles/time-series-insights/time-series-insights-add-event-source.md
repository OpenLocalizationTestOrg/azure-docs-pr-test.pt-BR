---
title: "aaaAdd um ambiente de Azure Insights de série de tempo do evento fonte tooyour | Microsoft Docs"
description: "Neste tutorial, você se conectar a um ambiente de informações da série de tempo do evento fonte tooyour"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Criar uma fonte de evento para o seu ambiente de informações da série de tempo usando o portal do Ibiza Olá

Uma Origem de Evento da Análise de Séries Temporais é derivada de um agente de evento, como o Hubs de Eventos do Azure. Informações da série de tempo se conecta diretamente fontes tooEvent, ingestão de fluxo de dados de saudação sem a necessidade dos usuários toowrite uma única linha de código. Atualmente, a Análise de Séries Temporais dá suporte a Hubs de Eventos do Azure e a Hubs IoT do Azure. Em Olá futuras, mais fontes de evento serão adicionadas.

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a>Etapas tooadd um ambiente de tooyour de origem do evento

1.  Entrar toohello [portal do Ibiza](https://portal.azure.com).
2.  Clique em "Todos os recursos" no menu de saudação no lado esquerdo de saudação do portal do Ibiza hello.
3.  Selecione o seu ambiente de Análise de Séries Temporais.

  ![Criar origem do evento de informações da série de tempo de saudação](media/add-event-source/getstarted-create-event-source-1.png)

4.  Selecione "Origens de Evento", clique em "+ Adicionar".

  ![Criar fonte de evento de informações da série de tempo Olá - detalhes](media/add-event-source/getstarted-create-event-source-2.png)

5.  Especifique o nome de saudação de origem do evento hello. Esse nome é associado a todos os eventos dessa origem de evento e está disponível no momento da consulta.
6.  Selecione um hub de eventos da lista de saudação de recursos do Hub de eventos na assinatura atual hello. Caso contrário, escolha a opção de importação "configurações do Hub de eventos fornecem manualmente" toospecify um hub de eventos em outra assinatura. Os eventos devem ser publicados no formato JSON.
7.  Selecione a política que tem permissão no hub de eventos de saudação de leitura.
8.  Especifique o grupo de consumidores do hub de eventos.

  > [!IMPORTANT]
  > Verifique se esse grupo de consumidores não é usado por qualquer outro serviço (como um trabalho do Stream Analytics ou outro ambiente de Análise de Séries Temporais). Se o grupo de consumidores é usado por outros serviços, leia a operação é afetada negativamente para esse ambiente e Olá outros serviços. Se você estiver usando "$Default" como o grupo de consumidores hello, isso pode levar a reutilização de toopotential por outros leitores.

9.  Clique em “Criar”.

Após a criação da origem do evento hello, Insights de série de tempo iniciará automaticamente o fluxo de dados em seu ambiente.

## <a name="next-steps"></a>Próximas etapas

* [Enviar eventos](time-series-insights-send-events.md) toohello origem do evento
* Exibir seu ambiente no [Portal de Análise de Séries Temporais](https://insights.timeseries.azure.com)
