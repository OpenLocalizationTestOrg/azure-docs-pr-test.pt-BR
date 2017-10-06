---
title: "passo a passo de solução de monitoramento pré-configurado aaaRemote | Microsoft Docs"
description: "Uma descrição do hello Azure IoT pré-configurado solução de monitoramento remoto e sua arquitetura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a>Passo a passo da solução pré-configurada de monitoramento remoto

Olá monitoramento remoto do IoT Suite [pré-configurado solução] [ lnk-preconfigured-solutions] é uma implementação de uma ponta a ponta solução para várias máquinas em execução em locais remotos de monitoramento. Olá combina serviços do Azure chave tooprovide uma implementação genérica do cenário de negócios hello. Você pode usar a solução hello como ponto de partida para sua própria implementação e [personalizar] [ lnk-customize] -toomeet seus próprios requisitos comerciais específicos.

Este artigo o orienta por meio de alguns dos elementos principais de saudação do hello tooenable de solução de monitoramento remoto toounderstand como ele funciona. Esse conhecimento ajuda a:

* Solucione problemas na solução de saudação.
* Planejar como toocustomize toohello solução toomeet necessidades específicas. 
* Criar sua própria solução IoT que usa os serviços do Azure.

## <a name="logical-architecture"></a>Arquitetura lógica

Olá diagrama a seguir descreve os componentes lógicos de saudação da solução Olá pré-configurados:

![Arquitetura lógica](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a>Dispositivos simulados

Solução Olá pré-configurado, dispositivo simulado Olá representa um dispositivo de resfriamento (como uma construção ar condicionado ou unidade de manuseio de ar de recurso). Quando você implanta a solução Olá pré-configurados, você provisionar automaticamente quatro dispositivos simulados que são executados em um [Azure WebJob][lnk-webjobs]. dispositivos de saudação simulada tornam mais fácil para você tooexplore Olá comportamento de solução de saudação sem Olá necessidade toodeploy quaisquer dispositivos físicos. toodeploy um dispositivo físico real, consulte Olá [conectar sua solução pré-configurada de monitoramento remoto de toohello dispositivo] [ lnk-connect-rm] tutorial.

### <a name="device-to-cloud-messages"></a>Mensagens do dispositivo para a nuvem

Cada dispositivo simulado pode enviar Olá tooIoT tipos de mensagem Hub a seguir:

| Mensagem | Descrição |
| --- | --- |
| Inicialização |Quando o dispositivo Olá é iniciado, ele envia um **informações do dispositivo** mensagem que contém informações sobre o próprio toohello back-end. Esses dados incluem a id do dispositivo hello e uma lista de comandos de saudação e métodos Olá dispositivo suporta. |
| Presença |Um dispositivo envia periodicamente uma **presença** tooreport da mensagem se o dispositivo Olá pode detectar a presença de saudação de um sensor. |
| Telemetria |Um dispositivo envia periodicamente uma **telemetria** mensagem que informa simulados valores de temperatura hello e umidade coletados de dispositivo de saudação do simulados sensores. |

> [!NOTE]
> solução de saudação armazena a lista de saudação de comandos com suporte pelo dispositivo de saudação em um banco de dados do banco de dados do Cosmos e não em duas de dispositivo de saudação.

### <a name="properties-and-device-twins"></a>Propriedades e dispositivos gêmeos

dispositivos simulados Hello enviam Olá toohello de propriedades de dispositivo a seguir [duas] [ lnk-device-twins] no hub IoT de saudação como *relatado propriedades*. envios de dispositivo Hello relatado propriedades na inicialização e na resposta tooa **alterar estado do dispositivo** método ou comando.

| Propriedade | Finalidade |
| --- | --- |
| Config.TelemetryInterval | Dispositivo de saudação de frequência (segundos) envia a Telemetria |
| Config.TemperatureMeanValue | Especifica o valor médio de saudação de telemetria de temperatura Olá simulado |
| Device.DeviceID |ID que é fornecido ou atribuído quando um dispositivo é criado na solução Olá |
| Device.DeviceState | Estado relatado pelo dispositivo Olá |
| Device.CreatedTime |Dispositivo de saudação do tempo foi criado na solução de saudação |
| Device.StartupTime |Dispositivo de saudação do tempo foi iniciado |
| Device.LastDesiredPropertyChange |número de versão de saudação da propriedade desejada do último Olá alterar |
| Device.Location.Latitude |Local da Latitude do dispositivo Olá |
| Device.Location.Longitude |Local de longitude do dispositivo Olá |
| System.Manufacturer |Fabricante do dispositivo |
| System.ModelNumber |Número do modelo de dispositivo de saudação |
| System.SerialNumber |Número de série do dispositivo Olá |
| System.FirmwareVersion |Versão atual do firmware no dispositivo Olá |
| System.Platform |Arquitetura da plataforma de dispositivo Olá |
| System.Processor |Dispositivo de saudação em execução do processador |
| System.InstalledRAM |Quantidade de RAM instalada no dispositivo Olá |

simulador Olá propaga essas propriedades em dispositivos simuladas com valores de exemplo. Cada vez simulador Olá inicializa um dispositivo simulado, dispositivo Olá reporta Olá metadados predefinidos tooIoT Hub como propriedades relatadas. Propriedades relatadas só podem ser atualizadas por dispositivo hello. toochange uma propriedade relatada, definir uma propriedade desejada no portal de solução. É responsabilidade de saudação do dispositivo hello:

1. Recupere periodicamente as propriedades desejadas de hub IoT de saudação.
2. Atualize sua configuração com o valor da propriedade Olá desejado.
3. Envie novo hub de toohello back valor hello como uma propriedade relatada.

No painel de solução hello, você pode usar *propriedades desejadas* tooset propriedades em um dispositivo usando Olá [duas dispositivo][lnk-device-twins]. Normalmente, um dispositivo lê um valor de propriedade desejados do hello hub tooupdate que seu estado interno e Olá relatório alterar novamente como uma propriedade relatada.

> [!NOTE]
> Olá dispositivo simulado código só usa Olá **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** Olá de tooupdate propriedades desejadas relatado propriedades enviadas de volta tooIoT Hub. Todas as outras solicitações de alteração de propriedade desejados são ignoradas no dispositivo simulado hello.

### <a name="methods"></a>Métodos

Olá simulados dispositivos podem manipular Olá métodos a seguir ([direto métodos][lnk-direct-methods]) chamado a partir do portal de solução de saudação por meio de hub IoT de saudação:

| Método | Descrição |
| --- | --- |
| InitiateFirmwareUpdate |Instrui o hello dispositivo tooperform uma atualização de firmware |
| Reboot |Instrui o hello dispositivo tooreboot |
| FactoryReset |Instrui o hello dispositivo tooperform redefinição de fábrica |

Alguns métodos usam tooreport propriedades relatado em andamento. Por exemplo, Olá **InitiateFirmwareUpdate** método simula a atualização de saudação em execução assíncrona no dispositivo de saudação. método Hello retorna imediatamente no dispositivo Olá, interromper a tarefa assíncrona Olá fazer atualizações de status toosend toohello solução dashboard usando relatado propriedades.

### <a name="commands"></a>Comandos

dispositivos Olá simulado podem manipular Olá comandos (mensagens de nuvem para dispositivo) enviados do portal de solução de saudação por meio de hub IoT de saudação a seguir:

| Command | Descrição |
| --- | --- |
| PingDevice |Envia um *ping* toohello dispositivo toocheck está ativo |
| StartTelemetry |Inicia Olá dispositivo enviar Telemetria |
| StopTelemetry |Dispositivo de saudação para de enviar Telemetria |
| ChangeSetPointTemp |Altera o valor de ponto de conjunto de saudação em torno da qual Olá dados aleatórios são gerados |
| DiagnosticTelemetry |Gatilhos Olá simulador de dispositivo toosend um valor de telemetria adicionais (externalTemp) |
| ChangeDeviceState |Altera uma propriedade estendida estado dispositivo hello e envia mensagens de informações de dispositivo Olá Olá dispositivo |

> [!NOTE]
> Para obter uma comparação desses comandos (mensagens da nuvem para o dispositivo) e métodos (métodos diretos), consulte [Orientação para comunicações entre o dispositivo e a nuvem][lnk-c2d-guidance].

## <a name="iot-hub"></a>Hub IoT

Olá [hub IoT] [ lnk-iothub] consome dados enviados de dispositivos de saudação em nuvem hello e torna disponível toohello trabalhos de análise de fluxo do Azure (ASA). Cada trabalho ASA fluxo usa um IoT Hub consumidor grupo tooread Olá fluxo separado de mensagens de seus dispositivos.

Olá hub IoT na solução Olá também:

- Mantém um registro de identidade que armazena ids de saudação e chaves de autenticação de todos os dispositivos de saudação permitidos tooconnect toohello portal. Você pode habilitar e desabilitar dispositivos por meio do registro de identidade hello.
- Envia comandos tooyour dispositivos em nome do portal de solução de saudação.
- Chama os métodos em seus dispositivos em nome do portal de solução de saudação.
- Mantém dispositivos gêmeos para todos os dispositivos registrados. Duas um dispositivo armazena valores de propriedade Olá relatados por um dispositivo. Duas um dispositivo também armazena as propriedades desejadas, definidas no portal de solução de Olá para Olá dispositivo tooretrieve ao próximo se conectar.
- Agendamentos de trabalhos tooset propriedades para vários dispositivos ou chamar métodos em vários dispositivos.

## <a name="azure-stream-analytics"></a>Stream Analytics do Azure

Na solução de monitoramento remoto de saudação [Azure Stream Analytics] [ lnk-asa] (ASA) envia mensagens de dispositivo recebidas pelos componentes de saudação IoT hub tooother back-end para processamento ou armazenamento. Trabalhos ASA diferentes executam funções específicas com base no conteúdo de saudação das mensagens de saudação.

**Tarefa 1: Informações sobre o dispositivo** filtra as mensagens de informações de dispositivo de fluxo de mensagem de entrada hello e envia o ponto de extremidade do tooan Hub de eventos. Um dispositivo envia mensagens de informações de dispositivo durante a inicialização e na resposta tooa **SendDeviceInfo** comando. Esta tarefa usa Olá tooidentify de definição de consulta a seguir **informações do dispositivo** mensagens:

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

Esse trabalho envia seu Hub de eventos de tooan de saída para processamento adicional.

**Trabalho 2: as Regras** avaliam os valores de telemetria da temperatura e da umidade de entrada em relação aos limites de cada dispositivo. Valores de limite são definidos no editor de regras de saudação disponível no portal de solução de saudação. Cada par de dispositivo/valor é armazenado por carimbo de data/hora em um blob que o Stream Analytics lê como **Dados de Referência**. trabalho de saudação compara qualquer valor não vazio com limite de conjunto de saudação para dispositivo hello. Se ele exceder Olá ' >' condição, a saída do trabalho de saudação um **alarme** evento que indica que esse limite Olá for excedido e fornece dispositivo hello, valor e valores de carimbo de hora. Esta tarefa usa Olá mensagens telemetria de tooidentify de definição de consulta que devem disparar um alarme a seguir:

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

Olá trabalho envia seu Hub de eventos de tooan de saída para processamento adicional e evita que os detalhes de cada armazenamento de alerta tooblob onde portal de solução Olá pode ler as informações de alerta de saudação.

**Tarefa 3: Telemetria** opera em fluxo telemetria dispositivo de saudação entrada de duas maneiras. Olá primeiro envia todas as mensagens de telemetria Olá dispositivos toopersistent do armazenamento de blob para armazenamento de longo prazo. Olá segundo calcula umidade média, mínima e máxima de valores em uma janela deslizante de cinco minutos e envia esse armazenamento tooblob de dados. portal de solução Olá lê dados de telemetria de saudação de gráficos de saudação de toopopulate de armazenamento de blob. Esta tarefa usa Olá definição de consulta a seguir:

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a>Hubs de Eventos

Olá **informações do dispositivo** e **regras** trabalhos ASA saída seu dados tooEvent Hubs tooreliably forward em toohello **processador de eventos** em execução no hello WebJob.

## <a name="azure-storage"></a>Armazenamento do Azure

solução de saudação usa toopersist de armazenamento de BLOBs do Azure todos os dados de telemetria bruto e resumidos Olá dos dispositivos de saudação na solução de saudação. portal de saudação lê dados de telemetria de saudação de gráficos de saudação de toopopulate de armazenamento de blob. toodisplay alertas, portal de solução de saudação lê dados saudação do armazenamento de blob que registra quando Olá de valores excedidos telemetria configurado valores de limite. solução de saudação também usa valores de limite de saudação do blob storage toorecord definido no portal de solução de saudação.

## <a name="webjobs"></a>Trabalhos Web

Além disso toohosting simuladores de dispositivo hello, Olá WebJobs na solução Olá também Olá host **processador de eventos** em execução em um trabalho Web do Azure que manipula as respostas de comando. Ele usa o comando resposta mensagens tooupdate Olá comando histórico de dispositivo (armazenado no banco de dados de banco de dados do Cosmos Olá).

## <a name="cosmos-db"></a>Banco de Dados Cosmos

solução de saudação usa um banco de dados do Cosmos banco de dados toostore saber Olá dispositivos conectados toohello solução. Essas informações incluem o histórico de saudação de comandos enviados toodevices do portal de solução hello e métodos invocados a partir do portal de solução de saudação.

## <a name="solution-portal"></a>Portal de solução

portal de solução de saudação é um aplicativo web implantado como parte da solução Olá pré-configurado. páginas de chave Olá no portal de solução de saudação são painel hello e lista de dispositivos de saudação.

### <a name="dashboard"></a>Painel

Esta página no aplicativo web de saudação usa os controles de javascript do PowerBI (consulte [repositório PowerBI-visuals](https://www.github.com/Microsoft/PowerBI-visuals)) dados de telemetria Olá toovisualize de dispositivos de saudação. solução de saudação usa Olá ASA telemetria trabalho toowrite Olá telemetria tooblob armazenamento de dados.

### <a name="device-list"></a>Lista de dispositivos

Nessa página no portal de solução hello, você pode:

* Provisione um novo dispositivo. Essa ação define a id de dispositivo exclusivo hello e gera a chave de autenticação hello. Ele grava informações sobre Olá tooboth de dispositivo Olá registro de identidade de IoT Hub e o banco de dados de banco de dados do Cosmos de solução específica Olá.
* Gerencie propriedades de dispositivo. Esta ação inclui a exibição de propriedades existentes e a atualização com novas propriedades.
* Envie o dispositivo de tooa de comandos.
* Exibir o histórico do comando Olá para um dispositivo.
* Habilite e desabilite dispositivos.

## <a name="next-steps"></a>Próximas etapas

Olá, seguir postagens de blog do TechNet fornecem mais detalhes sobre Olá solução pré-configurada de monitoramento remoto:

* [Monitoramento remoto do IoT Suite - em Olá bastidores-](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (Adicionando dispositivos ativos e simulados)](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

Você pode continuar a guia de Introdução com IoT Suite lendo Olá artigos a seguir:

* [Conecte-se a sua solução pré-configurada de monitoramento remoto de toohello de dispositivo][lnk-connect-rm]
* [Permissões no site de azureiotsuite.com Olá][lnk-permissions]

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
