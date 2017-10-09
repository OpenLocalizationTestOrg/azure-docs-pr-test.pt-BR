---
title: "métricas de aaaUse toomonitor Azure IoT Hub | Microsoft Docs"
description: "Como monitorar e toouse Azure IoT Hub métricas tooassess Olá integridade geral dos seus hubs de IoT."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a47108fd-f994-4105-b21d-5b8f697b699c
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7d045013fb0229f488e72c93a6f668048b9d5c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-iot-hub-metrics"></a>Entender as métricas de Hub IoT
Métricas de IoT Hub oferecem melhor dados sobre o estado de saudação de recursos do Azure IoT Olá na sua assinatura do Azure. Habilitar as métricas de IoT Hub você tooassess Olá integridade geral de saudação serviço IoT Hub e dispositivos Olá conectado tooit. Estatísticas de voltado ao usuário são importantes, porque elas ajudam a ver o que está acontecendo com os problemas de causa raiz IoT hub e ajuda sem a necessidade de toocontact suporte do Azure.

As métricas são habilitadas por padrão. Você pode exibir as métricas de IoT Hub de saudação portal do Azure.

## <a name="how-tooview-iot-hub-metrics"></a>Como tooview métricas de IoT Hub
1. Crie um Hub IoT. Você pode encontrar instruções sobre como toocreate um hub IoT Olá [começar] [ lnk-get-started] guia.
2. Abra a folha de saudação do seu hub IoT. A partir daí, clique em **métricas**.
   
    ![][1]
3. Na folha de métricas hello, você pode exibir métricas Olá para o hub IoT e criar exibições personalizadas de suas métricas. Você pode escolher toosend seu ponto de extremidade de Hubs de eventos de tooan de dados de métricas ou uma conta de armazenamento do Azure clicando em **as configurações de diagnóstico**.
   
    ![][2]

## <a name="iot-hub-metrics-and-how-toouse-them"></a>Métricas de IoT Hub e como toouse-los
IoT Hub fornece várias métricas toogive você uma visão geral da integridade de saudação do hub e Olá número total de dispositivos de conexão. Você pode combinar as informações de várias métricas toopaint uma panorama do estado de saudação do hub IoT de saudação. Olá a tabela a seguir descreve as métricas de saudação que controla cada hub IoT e como cada métrica relacionada toohello geral o status de Olá hub IoT.

|Métrica|Nome de exibição da métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Tentativas de envio de mensagem de telemetria|Contagem|Total|Número de telemetria do dispositivo para nuvem mensagens tentativa toobe enviados tooyour IoT hub|
|d2c.telemetry.ingress.success|Mensagens de telemetria enviadas|Contagem|Total|Número de mensagens de telemetria do dispositivo para nuvem enviado com sucesso tooyour IoT hub|
|c2d.commands.egress.complete.success|Comandos concluídos|Contagem|Total|Número de comandos de nuvem para dispositivo foi concluída com êxito pelo dispositivo Olá|
|c2d.commands.egress.abandon.success|Comandos abandonados|Contagem|Total|Número de comandos de nuvem para dispositivo abandonado por dispositivo Olá|
|c2d.commands.egress.reject.success|Comandos rejeitados|Contagem|Total|Número de comandos de nuvem para dispositivo rejeitadas pelo dispositivo Olá|
|devices.totalDevices|Total de dispositivos|Contagem|Total|Número de dispositivos registrados tooyour IoT hub|
|devices.connectedDevices.allProtocol|Dispositivos conectados|Contagem|Total|Número de dispositivos conectados tooyour IoT hub|
|d2c.telemetry.egress.success|Mensagens de telemetria entregues|Contagem|Total|Número de vezes que as mensagens foram gravadas tooendpoints (total)|
|d2c.telemetry.egress.dropped|Mensagens descartadas|Contagem|Total|Número de mensagens descartadas porque eles não correspondeu a todas as rotas e rota fallback Olá foi desabilitada|
|d2c.telemetry.egress.orphaned|Mensagens órfãs|Contagem|Total|Contagem de saudação de mensagens não corresponde a nenhuma rota incluindo rota fallback Olá|
|d2c.telemetry.egress.invalid|Mensagens inválidas|Contagem|Total|Olá contagem de mensagens não entregues devido tooincompatibility com ponto de extremidade Olá|
|d2c.telemetry.egress.fallback|Mensagens que correspondem à condição de fallback|Contagem|Total|Número de mensagens gravadas fallback toohello de ponto de extremidade|
|d2c.endpoints.egress.eventHubs|Mensagens entregues tooEvent pontos de extremidade de Hub|Contagem|Total|Número de vezes que as mensagens foram pontos de extremidade de Hub tooEvent gravado com êxito|
|d2c.endpoints.latency.eventHubs|Latência de mensagem para pontos de extremidade do Hub de Eventos|Milissegundos|Média|latência média de saudação entre entrada de mensagem e o hub IoT do mensagem entrada toohello em um ponto de extremidade de Hub de eventos, em milissegundos|
|d2c.endpoints.egress.serviceBusQueues|Mensagens entregues tooService pontos de extremidade de fila do barramento|Contagem|Total|Número de vezes que as mensagens foram pontos de extremidade de fila do barramento tooService gravado com êxito|
|d2c.endpoints.latency.serviceBusQueues|Latência de mensagem para pontos de extremidade da Fila do Barramento de Serviço|Milissegundos|Média|latência média de saudação entre entrada de mensagem e o hub IoT do mensagem entrada toohello em um ponto de extremidade de fila do barramento de serviço, em milissegundos|
|d2c.endpoints.egress.serviceBusTopics|Mensagens entregues tooService pontos de extremidade de tópico de barramento|Contagem|Total|Número de vezes que as mensagens foram pontos de extremidade de tópico de barramento tooService gravado com êxito|
|d2c.endpoints.latency.serviceBusTopics|Latência de mensagem para pontos de extremidade de Tópico do Barramento de Serviço|Milissegundos|Média|latência média de saudação entre entrada de mensagem e o hub IoT do mensagem entrada toohello em um ponto de extremidade de tópico do barramento de serviço, em milissegundos|
|d2c.endpoints.egress.builtIn.events|Mensagens entregues de ponto de extremidade toohello internos (mensagens e eventos)|Contagem|Total|Número de vezes que as mensagens foram ponto de extremidade internos do toohello gravado com êxito (mensagens e eventos)|
|d2c.Endpoints.Latency.builtIn.Events|Latência de mensagem para o ponto de extremidade Olá internos (mensagens e eventos)|Milissegundos|Média|latência média Olá entre entrada de mensagem e o hub IoT do mensagem entrada toohello em Olá internos ponto de extremidade (mensagens de eventos), em milissegundos |
|d2c.twin.read.success|Leituras de gêmeos dos dispositivos bem-sucedidas|Contagem|Total|Contagem de saudação de êxito todas as leituras de duas iniciada pelo dispositivo.|
|d2c.twin.read.failure|Leituras de gêmeos dos dispositivos com falhas|Contagem|Total|Contagem de saudação de todos os falha leituras duas iniciada pelo dispositivo.|
|d2c.twin.read.size|Tamanho da resposta das leituras de gêmeos dos dispositivos|Bytes|Média|Média de Hello, min e max de todos os bem-sucedida iniciada pelo dispositivo macros leituras.|
|d2c.twin.update.success|Atualizações de gêmeos dos dispositivos bem-sucedidas|Contagem|Total|Contagem de Olá de bem-sucedida de todas as atualizações de duas iniciada pelo dispositivo.|
|d2c.twin.update.failure|Atualizações de gêmeos dos dispositivos com falhas|Contagem|Total|Contagem de saudação de todos os falha iniciada pelo dispositivo duas atualizações.|
|d2c.twin.update.size|Tamanho das atualizações de gêmeos dos dispositivos|Bytes|Média|Olá média, mínimo e tamanho máximo de todos os bem-sucedida iniciada pelo dispositivo macros atualizações.|
|c2d.methods.success|Invocações de método diretas bem-sucedidas|Contagem|Total|Contagem de saudação com êxito todas as chamadas de método direto.|
|c2d.methods.failure|Invocações de método diretas com falhas|Contagem|Total|Contagem de saudação de todos os falhas de chamadas de método direto.|
|c2d.methods.requestSize|Tamanho da solicitação das invocações de método diretas|Bytes|Média|Média de Hello, min e max de todos os bem-sucedida direcionam solicitações de método.|
|c2d.methods.responseSize|Tamanho da resposta das invocações de método diretas|Bytes|Média|Média de saudação, min e max de todas as respostas de método direto com êxito.|
|c2d.twin.read.success|Leituras de gêmeos de back-end bem-sucedidas|Contagem|Total|Contagem de saudação de êxito todas as leituras de duas iniciada pelo back-end.|
|c2d.twin.read.failure|Leituras de gêmeos de back-end com falhas|Contagem|Total|Contagem de saudação de todos os falha leituras duas iniciada pelo back-end.|
|c2d.twin.read.size|Tamanho da resposta das leituras de gêmeos de back-end|Bytes|Média|Média de Hello, min e max de todos os bem-sucedida iniciada pelo back-end macros leituras.|
|c2d.twin.update.success|Atualizações de gêmeos de back-end bem-sucedidas|Contagem|Total|Contagem de saudação de bem-sucedida de todas as atualizações de duas iniciada pelo back-end.|
|c2d.twin.update.failure|Atualizações de gêmeos de back-end com falhas|Contagem|Total|Contagem de saudação de todos os falha iniciada pelo back-end duas atualizações.|
|c2d.twin.update.size|Tamanho das atualizações de gêmeos de back-end|Bytes|Média|Olá média, mínimo e tamanho máximo de todos os bem-sucedida iniciada pelo back-end macros atualizações.|
|twinQueries.success|Consultas de gêmeos bem-sucedidas|Contagem|Total|Contagem de saudação de todas as consultas de duas bem-sucedida.|
|twinQueries.failure|Consultas de gêmeos com falhas|Contagem|Total|Contagem de saudação de todas as consultas de duas com falha.|
|twinQueries.resultSize|Tamanho do resultado das consultas de gêmeos|Bytes|Média|Média de Hello, mínimo e máximo de tamanho do resultado da saudação de todas as consultas de duas bem-sucedida.|
|jobs.createTwinUpdateJob.success|Criações de trabalhos de atualização de gêmeos bem-sucedidas|Contagem|Total|Contagem de saudação da criação com êxito todos os trabalhos de atualização de duas.|
|jobs.createTwinUpdateJob.failure|Criações de trabalhos de atualização de gêmeos com falhas|Contagem|Total|Contagem de saudação de todos os Falha na criação de trabalhos de atualização de duas.|
|jobs.createDirectMethodJob.success|Criações de trabalhos de invocação de método bem-sucedidas|Contagem|Total|Contagem de saudação da criação com êxito todos os trabalhos de invocação de método direto.|
|jobs.createDirectMethodJob.failure|Criações de trabalhos de invocação de método com falhas|Contagem|Total|Contagem de saudação de todos os Falha na criação de trabalhos de invocação de método direto.|
|jobs.listJobs.success|Trabalhos de toolist chamadas com êxito|Contagem|Total|Contagem de saudação de todos os trabalhos de toolist chamadas com êxito.|
|jobs.listJobs.failure|Chamadas com falha toolist trabalhos|Contagem|Total|Contagem de saudação de todos os trabalhos de toolist de chamadas com falha.|
|jobs.cancelJob.success|Cancelamentos de trabalho bem-sucedidos|Contagem|Total|Contagem de saudação do bem-sucedida de todas as chamadas toocancel um trabalho.|
|jobs.cancelJob.failure|Cancelamentos de trabalho com falhas|Contagem|Total|Contagem de saudação de todas as chamadas com falha toocancel um trabalho.|
|jobs.queryJobs.success|Consultas de trabalho bem-sucedidas|Contagem|Total|Contagem de saudação de todos os trabalhos de tooquery chamadas com êxito.|
|jobs.queryJobs.failure|Consultas de trabalho com falhas|Contagem|Total|Contagem de saudação de todos os trabalhos de tooquery de chamadas com falha.|
|jobs.completed|Trabalhos concluídos|Contagem|Total|Contagem de saudação de todos os trabalhos concluídos.|
|jobs.failed|Trabalhos com falha|Contagem|Total|Contagem de saudação de todos os trabalhos com falha.|

## <a name="next-steps"></a>Próximas etapas
Agora que você já viu uma visão geral das métricas de IoT Hub, siga este toolearn link mais sobre como gerenciar o Azure IoT Hub:

* [Monitoramento de operações][lnk-monitor]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Guia do desenvolvedor do Hub IoT][lnk-devguide]
* [Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-metrics/enable-metrics-1.png
[2]: media/iot-hub-metrics/enable-metrics-2.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-operations-monitoring]: iot-hub-operations-monitoring.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
