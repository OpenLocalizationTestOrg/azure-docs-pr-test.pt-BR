---
title: "aaaOverview do Azure Insights de série de tempo | Microsoft Docs"
description: "Introdução tooAzure análise de série de tempo, um novo serviço para análise de dados de série de tempo e soluções de IoT"
keywords: 
services: tsi
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: 
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: omravi
ms.openlocfilehash: 8c022bf1fae88eddab3dbebc7bb36cc15a785172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-time-series-insights"></a>O que é o Azure Time Series Insights

O Azure Insights de série de tempo é um serviço de nuvem gerenciados com componentes de visualização que tornam mais fácil tooingest, análise e armazenamento, armazenar, explorar e analisar bilhões de eventos simultaneamente. O Azure Time Series Insights oferece uma visão global dos dados, permitindo que você valide rapidamente suas Soluções de IoT e evite o tempo de inatividade dispendioso ajudando você a descobrir tendências ocultas e anomalias e realizar análises de causa raiz em tempo quase real. Informações da série de tempo recebe dados de série temporal de agentes de evento (por exemplo, Hubs IoT ou Hubs de eventos), Olá dados dos índices e desativa os dados com base em uma política de retenção configurável. Os usuários consomem dados de saudação por meio de um intuitiva UX ou APIs REST de consulta.

![Visão geral da Análise de Séries Temporais](media/overview/time-series-insights-overview-flow.png)

## <a name="primary-scenarios"></a>Principais cenários

* Monitorar e validar soluções de IoT em minutos.
* Visualizar e analisar dados IoT em escala.
* Acelerar a detecção de anomalias e análise de causas raiz.
* Criar uma exibição global de vários dispositivos, plantas e dados.

## <a name="capabilities-and-benefits"></a>Recursos e benefícios

* **Fácil tooget iniciado**: Insights de série de tempo do Azure não exige nenhuma preparação de dados inicial e é inacreditavelmente rápido. Conecte-se toobillions de eventos no Azure IoT Hub ou Hub de eventos em minutos. Uma vez conectado, visualizem e interajam com dados em segundos tooquickly validar suas soluções de IoT. Informações da série de tempo é fácil toouse; Você pode interagir com os dados sem escrever uma única linha de código.  Não há nenhum novo toolearn de idioma; Informações da série de tempo fornece uma superfície de consulta de texto livre granular para usuários avançados e aponte e clique exploração para todos.

* **Perto da informações em tempo real**: informações da série de tempo pode acomodar centenas de milhões de eventos de sensor por dia, com latência de um minuto para que você possa reagir toochanges rapidamente. O Time Series Insights ajuda você a realizar análises profundas em seus dados de sensor ajudando-o a identificar tendências e anomalias rapidamente, realize facilmente análises complexas de causas raiz e evitar um tempo de inatividade dispendioso. Habilitando a correlação entre os dados históricos e em tempo real, informações da série de tempo ajuda desbloquear ocultas tendências nos dados de saudação.

* **Crie soluções personalizadas**: Integre a Análise de Séries Temporais do Azure aos seus aplicativos existentes ou crie novas soluções personalizadas com as APIs de consulta REST da Análise de Séries Temporais. Criar e compartilhar personalizado modos de exibição que você pode compartilhar para outros tooexplore suas descobertas.

* **Escalabilidade**: informações da série de tempo é projetado toosupport IoT em escala. Na visualização, ela pode ingresso de 1 milhão too100 abrangem milhões de eventos por dia, com uma retenção padrão de 31 dias. Você pode visualizar e analisar os fluxos de dados ativos quase em tempo real, juntamente com grandes quantidades de dados de histórico. Mais adiante, taxas de entrada e retenção aumentará tooaccommodate escala empresarial em constante evolução.

## <a name="time-series-insights-glossary"></a>Glossário do Time Series Insights

* **Ambiente**: Um é um recurso do Azure com capacidade de entrada e armazenamento.  Os clientes provisionar ambientes por meio do portal do Azure com sua capacidade necessária de saudação.
* **Origem de Evento**: Uma Origem de Evento é derivada de um agente de evento, como o Hubs de Eventos do Azure.  Informações da série de tempo se conecta diretamente tooEvent fontes, ingestão de fluxo de dados de saudação sem gravar qualquer código. Atualmente, a Análise de Séries Temporais dá suporte a Hubs de Eventos do Azure e a Hubs IoT do Azure.
* **Dados de referência**: tempo série Insights fornece aos usuários dados de série de tempo Olá capacidade toojoin com dados de referência.  Os dados de referência podem incluir metadados sobre dispositivos ou outros dados estáticos que não são alterados com tanta frequência. Informações da série de tempo une dados de referência de saudação com fluxos de dados, permitindo que os usuários toovisualize e analisar esses dados em quase em tempo real.
