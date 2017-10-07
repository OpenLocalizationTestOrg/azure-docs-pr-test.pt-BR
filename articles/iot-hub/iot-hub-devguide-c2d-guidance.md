---
title: "Opções de aaaAzure IoT Hub de nuvem para dispositivo | Microsoft Docs"
description: "Guia do desenvolvedor - orientações sobre quando toouse direciona métodos, propriedades desejadas de duas do dispositivo ou mensagens de nuvem para dispositivo para comunicações de nuvem para dispositivo."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: bb95445054fa2711e34fc1d928c3665e0246c81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-to-device-communications-guidance"></a>Diretrizes de comunicações da nuvem para o dispositivo
IoT Hub fornece três opções para o aplicativo de back-end do dispositivo aplicativos tooexpose funcionalidade tooa:

* [Direcionar métodos] [ lnk-methods] para comunicações que exigem a confirmação imediata do resultado de saudação. Direcionar métodos é muitas vezes usado para controle interativo de dispositivos, como ativar um ventilador.
* [Propriedades desejado pelo duas] [ lnk-twins] para comandos de longa execução objetivo desejado de dispositivo de saudação do tooput em um determinado estado. Por exemplo, o conjunto Olá telemetria enviar intervalo (minutos) too30.
* [Mensagens de nuvem para dispositivo] [ lnk-c2d] para o aplicativo de dispositivo toohello notificações unidirecional.

Aqui está uma comparação detalhada das Olá várias opções de comunicação de dispositivo para nuvem.

|  | Métodos diretos | Propriedades desejadas do gêmeo | Mensagens da nuvem para o dispositivo |
| ---- | ------- | ---------- | ---- |
| Cenário | Comandos que exigem confirmação imediata, por exemplo, ligar um ventilador. | Comandos de longa execução se destina a dispositivos de saudação tooput em um determinado estado desejado. Por exemplo, o conjunto Olá telemetria enviar intervalo (minutos) too30. | Aplicativo de dispositivo de toohello notificações unidirecional. |
| Fluxo de dados | Bidirecional. aplicativo de dispositivo Olá pode responder toohello método imediatamente. back-end de solução Olá recebe o resultado de saudação contextualmente toohello solicitação. | Unidirecional. Olá dispositivo aplicativo recebe uma notificação de alteração de propriedade hello. | Unidirecional. Olá dispositivo aplicativo recebe a mensagem de saudação
| Durabilidade | Dispositivos desconectados não são contatados. back-end de solução Olá é notificado que o dispositivo Olá não está conectado. | Valores de propriedade são preservados em duas de dispositivo de saudação. O dispositivo lerá na próxima reconexão. Valores de propriedade são recuperáveis com hello [linguagem de consulta de IoT Hub][lnk-query]. | As mensagens podem ser mantidas pelo IoT Hub para backup too48 horas. |
| Destinos | Dispositivo único usando **deviceId**, ou vários dispositivos usando [jobs][lnk-jobs]. | Dispositivo único usando **deviceId**, ou vários dispositivos usando [jobs][lnk-jobs]. | Dispositivo único por **deviceId**. |
| Tamanho | As solicitações de too8KB e respostas de 8KB. | O tamanho máximo desejado das propriedades é de 8 KB. | As mensagens de too64KB. |
| Frequência | Alta. Para saber mais, confira [Limites do Hub IoT][lnk-quotas]. | Média. Para saber mais, confira [Limites do Hub IoT][lnk-quotas]. | Baixa. Para saber mais, confira [Limites do Hub IoT][lnk-quotas]. |
| Protocolo | Disponível atualmente somente ao usar MQTT. | Disponível atualmente somente ao usar MQTT. | Disponível em todos os protocolos. O dispositivo deve sondar ao usar HTTP. |

Saiba como o toouse direcionar os métodos, propriedades desejadas e mensagens de nuvem para dispositivo em Olá tutoriais a seguir:

* [Usar métodos diretos][lnk-methods-tutorial] para método diretos;
* [Usar propriedades desejadas tooconfigure dispositivos][lnk-twin-properties], para duas de dispositivo do desejado, propriedades 
* [Enviar mensagens da nuvem para o dispositivo][lnk-c2d-tutorial], para mensagens da nuvem para o dispositivo.

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
