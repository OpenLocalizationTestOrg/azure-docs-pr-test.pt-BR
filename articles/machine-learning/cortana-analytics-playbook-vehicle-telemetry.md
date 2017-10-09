---
title: "integridade de veículo aaaPredict e orientar hábitos - Azure | Microsoft Docs"
description: "Usar recursos de saudação do insights de previsão e em tempo real de inteligência Cortana toogain na integridade do veículo e orientar hábitos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a>Manual da solução de análise de telemetria do veículo
Isso **menu** toohello capítulos neste guia estratégico de links. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a>Visão geral
Computadores superusuários tem sido movido do laboratório hello e agora são estacionadas em nosso garagem! Esses automóveis ponta contêm uma grande variedade de sensores, dando-lhes Olá capacidade tootrack e monitoram milhões de eventos por segundo. Esperamos que por 2020, a maioria desses carros será foram toohello conectado à Internet. Imagine tocar nessa riqueza de segurança dos dados tooprovide maior, confiabilidade e uma experiência melhor uma! A Microsoft tornou esse sonho uma realidade por meio do Cortana Intelligence.

Inteligência de Cortana da Microsoft é uma grande de dados totalmente gerenciados e análise conjunto avançado que permite que você tootransform seus dados em ação inteligente. Queremos toointroduce toohello Cortana Intelligence veículo telemetria análise de solução de modelo. Esta solução demonstra como revendedores de carro, automóveis fabricantes e companhias podem usar recursos de saudação do Cortana Intelligence toogain em tempo real e hábitos de previsão ideias sobre a integridade de veículo e referências. 

solução de saudação é implementada como um [padrão de arquitetura de lambda](https://en.wikipedia.org/wiki/Lambda_architecture) mostrando todo o potencial da plataforma de inteligência Cortana Olá para hello em tempo real e processamento em lote. solução de saudação: 

* fornece um simulador de Telemática do Veículo
* aproveita os Hubs De eventos para a ingestão de milhões de eventos de telemetria simulados do veículo no Azure 
* usa as informações em tempo real do Stream Analytics toogain na integridade do veículo
* persistir dados saudação no armazenamento de longo prazo para análises mais ricas de lote. 
* tira proveito de aprendizado de máquina para detecção de anomalias em tempo real e processamento toogain previsão insights do lote.
* aproveita o HDInsight tootransform dados em escala e coordenação de toohandle da fábrica de dados, agendamento, gerenciamento de recursos e monitoramento do pipeline de processamento de lote Olá 
* fornece essa solução a um painel avançado para os dados em tempo real e as visualizações da análise preditiva usando Power BI

## <a name="architecture"></a>Arquitetura
![Diagrama de arquitetura da solução](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figura 1 – Arquitetura da Solução de Análise da Telemetria do Veículo*

Essa solução inclui o seguinte Olá **componentes Intelligence Cortana** e apresenta sua integração de tooend final:

* **Hubs de Eventos** para a ingestão de milhões de eventos de telemetria do veículo no Azure.
* **Stream Analytics** para obter informações em tempo real sobre a integridade do veículo e persistir esses dados no armazenamento de longo prazo para uma análise de lote mais avançada.
* **Aprendizado de máquina** para detecção de anomalias em tempo real e insights previsão toogain de processamento em lotes.
* **HDInsight** tootransform utilizou dados em grande escala
* **Fábrica de dados** manipula orquestração, agendamento, gerenciamento de recursos e o monitoramento do pipeline de processamento de lote hello.
* **PowerBI** fornece essa solução a um painel avançado para os dados em tempo real e as visualizações da análise preditiva.

Essa solução acessa duas **fontes de dados**diferentes: 

* **Simulados veículo sinais e diagnóstico**: um simulador de telematics veículo emite sinais que correspondem a toohello estado de veículo hello e hello direcionando padrão em um determinado ponto no tempo e informações de diagnóstico. 
* **Catálogo de veículo**: um conjunto de dados de referência que contém um mapeamento de toomodel VIN.

