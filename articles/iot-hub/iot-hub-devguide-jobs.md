---
title: trabalhos de Azure IoT Hub aaaUnderstand | Microsoft Docs
description: "Guia do desenvolvedor - agendar trabalhos toorun em vários dispositivos conectados tooyour IoT hub. Os trabalhos podem atualizar marcações e propriedades desejadas e invocar métodos diretos em vários dispositivos."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>Agendar trabalhos em vários dispositivos
## <a name="overview"></a>Visão geral
Conforme descrito em artigos anteriores, o Hub IoT do Azure permite diversos blocos de construção ([marcas e propriedades do dispositivo gêmeo][lnk-twin-devguide] e [métodos diretos][lnk-dev-methods]).  Normalmente, os aplicativos de back-end habilitar tooupdate de operadores e administradores do dispositivo e interagem com dispositivos IoT em massa e em um horário agendado.  Trabalhos encapsulam a execução de saudação do dispositivo duas atualizações e métodos diretos de um conjunto de dispositivos em um tempo de agendamento.  Por exemplo, um operador seria usar um aplicativo de back-end que iniciar e acompanhar um trabalho tooreboot um conjunto de dispositivos na criação de cada vez que não seriam toohello interrupções operações de criação de saudação 43 e andar 3.

### <a name="when-toouse"></a>Quando toouse
Considere usar trabalhos quando: uma solução tooschedule de necessidades de back-end e acompanhar andamento qualquer Olá atividades a seguir em um conjunto de dispositivos:

* Atualizar as propriedades desejadas
* Marcas de atualização
* Chamar métodos diretos

## <a name="job-lifecycle"></a>Ciclo de vida do trabalho
Trabalhos são iniciados pelo back-end de solução hello e mantidos pelo IoT Hub.  Você pode iniciar um trabalho por meio de um URI voltado para o serviço (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) e consultar o andamento de um trabalho em execução por meio de um URI voltado para o serviço (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).  Depois que um trabalho é iniciado, consultando trabalhos habilita o status de saudação de toorefresh do hello aplicativo de back-end de trabalhos em execução.

> [!NOTE]
> Quando você inicia um trabalho, valores e nomes de propriedade só podem conter US-ASCII imprimível alfanumérico, exceto qualquer em Olá conjunto a seguir: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

## <a name="reference-topics"></a>Tópicos de referência:
Olá tópicos de referência a seguir fornece mais informações sobre como usar trabalhos.

## <a name="jobs-tooexecute-direct-methods"></a>Métodos diretos de tooexecute trabalhos
Olá, seguinte é Olá HTTP 1.1 detalhes de solicitação para executar um [método direto] [ lnk-dev-methods] em um conjunto de dispositivos usando um trabalho:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
condição de consulta Olá também pode ser em um único dispositivo Id ou em uma lista de Ids de dispositivo conforme mostrado abaixo

**Exemplos**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
A [Linguagem de consulta de Hub IoT][lnk-query] aborda a linguagem de consulta de Hub IoT em detalhes adicionais.

## <a name="jobs-tooupdate-device-twin-properties"></a>Trabalhos tooupdate duas propriedades
a seguir Olá é detalhes da solicitação de saudação do HTTP 1.1 para atualizar as propriedades do dispositivo duas usando um trabalho:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a>Consultar o andamento dos trabalhos
Olá seguinte é hello detalhes da solicitação HTTP 1.1 para [consultar trabalhos][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

Olá continuationToken é fornecido pela resposta de saudação.  

## <a name="jobs-properties"></a>Propriedades dos trabalhos
a seguir Olá é uma lista de propriedades e descrições correspondentes, que podem ser usadas durante a consulta para trabalhos ou os resultados do trabalho.

| Propriedade | Descrição |
| --- | --- |
| **jobId** |Aplicativo fornecido ID de trabalho hello. |
| **startTime** |Hora de início do aplicativo fornecido (ISO 8601) para o trabalho de saudação. |
| **endTime** |IoT Hub fornecido Data (ISO 8601) para quando Olá trabalho concluído. Válido somente depois que o trabalho Olá atinge o estado de saudação 'concluído'. |
| **tipo** |Tipos de trabalhos: |
| **scheduledUpdateTwin**: tooupdate um trabalho usado um conjunto de propriedades desejadas ou marcas. | |
| **scheduledDeviceMethod**: tooinvoke um trabalho usado um método de dispositivo em um conjunto de twins do dispositivo. | |
| **status** |Estado atual do trabalho de saudação. Valores possíveis para o status: |
| **pendente** : agendado e aguardando toobe captados pelo serviço de trabalho de saudação. | |
| **agendado** : agendado para uma hora no futuro de saudação. | |
| **executando**: trabalho ativo no momento. | |
| **cancelado**: o trabalho foi cancelado. | |
| **falha**: o trabalho falhou. | |
| **concluído**: o trabalho foi concluído. | |
| **deviceJobStatistics** |Estatísticas sobre a execução do trabalho hello. |

Propriedades **deviceJobStatistics**.

| Propriedade | Descrição |
| --- | --- |
| **deviceJobStatistics.deviceCount** |Número de dispositivos no trabalho de saudação. |
| **deviceJobStatistics.failedCount** |Número de dispositivos em que o trabalho de saudação falhou. |
| **deviceJobStatistics.succeededCount** |Número de dispositivos em que o trabalho de saudação teve êxito. |
| **deviceJobStatistics.runningCount** |Número de dispositivos que estão executando o trabalho de saudação. |
| **deviceJobStatistics.pendingCount** |Número de dispositivos que estão aguardando o trabalho de saudação toorun. |

### <a name="additional-reference-material"></a>Material de referência adicional
Outros tópicos de referência Olá guia do desenvolvedor de IoT Hub incluem:

* [Pontos de extremidade de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos de extremidade que expõe a cada hub IoT para operações de tempo de execução e gerenciamento.
* [Limitação e cotas] [ lnk-quotas] descreve cotas Olá que se aplicam a toohello serviço de IoT Hub e Olá limitação tooexpect de comportamento quando você usar o serviço de saudação.
* [SDKs do Azure de dispositivo e serviço IoT] [ lnk-sdks] listas Olá SDKs de vários idiomas você pode usar ao desenvolver aplicativos de dispositivo e o serviço que interagem com o IoT Hub.
* [Linguagem de consulta de IoT Hub para twins do dispositivo, trabalhos e roteamento de mensagens] [ lnk-query] descreve Olá linguagem de consulta de IoT Hub, você pode usar informações de tooretrieve de IoT Hub sobre seus trabalhos e twins do dispositivo.
* [Suporte de IoT Hub MQTT] [ lnk-devguide-mqtt] fornece mais informações sobre o suporte de IoT Hub para o protocolo MQTT hello.

## <a name="next-steps"></a>Próximas etapas
Se você quiser tootry alguns dos conceitos de saudação descritos neste artigo, você pode estar interessado em Olá seguindo o tutorial de IoT Hub:

* [Agendar e transmitir trabalhos][lnk-jobs-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
