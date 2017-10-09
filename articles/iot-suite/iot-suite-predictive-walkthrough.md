---
title: "instruções passo a passo de manutenção de aaaPredictive | Microsoft Docs"
description: "Um passo a passo de manutenção preditiva do hello Azure IoT pré-configurado solução."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 900d6351019489a8e2f4b98908364e3bd14975c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a>Passo a passo da solução pré-configurada de manutenção preditiva

Olá manutenção preditiva pré-configurado é uma solução de ponta a ponta para um cenário de negócios que prevê o ponto de saudação em que uma falha é provavelmente toooccur. Você pode usar essa solução pré-configurada de forma pró-ativa para atividades como a manutenção de otimização. solução Olá combina os principais serviços do Azure IoT Suite, como o IoT Hub, análise de fluxo e um [aprendizado de máquina do Azure] [ lnk-machine-learning] espaço de trabalho. Este espaço de trabalho contém um modelo, com base em um conjunto de dados público do exemplo hello toopredict vida útil restante (regra) de um mecanismo de aeronave. solução de saudação totalmente implementa o cenário de negócios IoT hello como ponto de partida para você tooplan e implementar uma solução que atenda aos seus requisitos de negócios específicos.

## <a name="logical-architecture"></a>Arquitetura lógica

Olá diagrama a seguir descreve os componentes lógicos de saudação da solução Olá pré-configurados:

![][img-architecture]

itens de saudação azul são provisionados na região Olá onde você implantou a solução Olá pré-configurado de serviços do Azure. Olá a lista de saudação de regiões em que você pode implantar a solução de saudação pré-configurado exibirá [página provisionamento][lnk-azureiotsuite].

item de saudação verde é um dispositivo simulado que representa um mecanismo de aeronave. Você pode aprender mais sobre esses dispositivos simulados no hello seção a seguir.

Olá, cinzas itens representam os componentes que implementam *gerenciamento de dispositivo* recursos. a versão atual Olá de solução de manutenção preditiva pré-configurado Olá não provisionar esses recursos. toolearn mais sobre o gerenciamento de dispositivos, consulte toohello [solução pré-configurada de monitoramento remoto][lnk-remote-monitoring].

## <a name="simulated-devices"></a>Dispositivos simulados

Solução Olá pré-configurado, um dispositivo simulado representa um mecanismo de aeronave. solução de saudação é configurada com dois mecanismos que mapeiam aeronave único tooa. Cada mecanismo emite quatro tipos de telemetria: Sensor 9, Sensor 11, Sensor 14 e 15 Sensor fornecem dados de saudação necessários para Olá aprendizado de máquina modelo toocalculate hello regra para o mecanismo de saudação. Cada dispositivo simulado envia Olá telemetria mensagens tooIoT Hub a seguir:

*Contagem de ciclos*. Um ciclo representa um voo concluído com uma duração entre duas e dez horas. Durante o voo hello, dados de telemetria são capturados a cada meia hora.

*Telemetria*. Há quatro sensores que representam os atributos do motor. sensores de saudação genericamente são rotulados Sensor 9, Sensor 11, Sensor 14 e 15 Sensor. Esses quatro sensores representam resultados úteis do telemetria suficiente tooobtain de modelo de regra de saudação. modelo de saudação usado na solução de saudação pré-configurado é criado de um conjunto de dados público que inclui dados do sensor do mecanismo real. Para obter mais informações sobre como o modelo de saudação foi criado Olá original no conjunto de dados, consulte Olá [modelo Galeria manutenção preditiva Intelligence Cortana][lnk-cortana-analytics].

dispositivos Olá simulado podem manipular Olá comandos enviados de hub IoT de saudação na solução Olá a seguir:

| Command | Descrição |
| --- | --- |
| StartTelemetry |Controles Olá estado de simulação de saudação.<br/>Inicia Olá dispositivo enviar Telemetria |
| StopTelemetry |Controles Olá estado de simulação de saudação.<br/>Paradas Olá enviar telemetria de dispositivo |

O Hub IoT fornece reconhecimento de comando do dispositivo.

## <a name="azure-stream-analytics-job"></a>Trabalho do Stream Analytics do Azure

**Trabalho: Telemetria** opera em Olá dispositivo telemetria fluxo de entrada usando duas instruções:

* Olá primeiro seleciona toda a telemetria de dispositivos hello e envia esse armazenamento tooblob de dados. Aqui, ele é visualizado no Olá web app.
* Olá segundo calcula sensor médio valores em uma janela deslizante de dois minutos e envia esses dados por meio de tooan de hub de evento Olá **processador de eventos**.

## <a name="event-processor"></a>Processador de eventos
Olá **host de processador de evento** é executado em um trabalho de Web do Azure. Olá **processador de eventos** usa valores de média de sensor de saudação de um ciclo completo. Ele, em seguida, passa esses valores tooan API que expõe Olá regra do toocalculate treinado para um mecanismo de. Olá API é exposta por um espaço de trabalho do aprendizado de máquina é provisionado como parte da solução de saudação.

## <a name="machine-learning"></a>Machine Learning
componente de aprendizado de máquina Olá usa um modelo derivado dos dados coletados de mecanismos de aeronave real. Você pode navegar toohello o espaço de trabalho de aprendizado de máquina do bloco Olá Olá [azureiotsuite.com] [ lnk-azureiotsuite] página para sua solução provisionada. Hello está disponível quando Olá solução no hello **pronto** estado.


## <a name="next-steps"></a>Próximas etapas
Agora você viu componentes-chave de solução de manutenção preditiva pré-configurado Olá Olá, talvez você queira toocustomize-lo. Veja [Orientação sobre como personalizar soluções pré-configuradas][lnk-customize].

Você também pode explorar alguns Olá outros recursos e capacidades de soluções do IoT Suite pré-configurado hello:

* [Perguntas frequentes sobre o IoT Suite][lnk-faq]
* [Segurança de IoT da saudação de plano de fundo para cima][lnk-security-groundup]

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/