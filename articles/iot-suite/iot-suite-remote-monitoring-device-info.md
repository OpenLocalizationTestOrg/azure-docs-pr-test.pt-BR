---
title: "metadados de informações de aaaDevice em Olá solução de monitoramento remoto | Microsoft Docs"
description: "Uma descrição do hello Azure IoT pré-configurado solução de monitoramento remoto e sua arquitetura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a>Metadados de informações de dispositivo no hello solução pré-configurada de monitoramento remoto

Olá solução pré-configurada de monitoramento remoto do Azure IoT Suite demonstra uma abordagem para o gerenciamento de metadados do dispositivo. Este artigo descreve a abordagem de saudação esta solução usa tooenable toounderstand você:

* Qual solução de saudação do dispositivo metadados armazena.
* Como solução Olá gerencia Olá metadados do dispositivo.

## <a name="context"></a>Contexto

Olá monitoramento remoto pré-configurado solução usa [Azure IoT Hub] [ lnk-iot-hub] tooenable toohello de dados de toosend seus dispositivos na nuvem. solução de saudação armazena informações sobre os dispositivos em três locais diferentes:

| Local | Informações armazenadas | Implementação |
| -------- | ------------------ | -------------- |
| Registro de identidade | Id do dispositivo, chaves de autenticação,estado habilitado | TooIoT interno de Hub |
| Dispositivos gêmeos | Metadados: propriedades relatadas, propriedades desejadas, marcas | TooIoT interno de Hub |
| Banco de Dados Cosmos | Histórico de comandos e de métodos | Personalizada para a solução |

IoT Hub inclui um [registro de identidade do dispositivo] [ lnk-identity-registry] toomanage acessar tooan IoT hub e usa [twins dispositivo] [ lnk-device-twin] toomanage metadados do dispositivo . Também há um *registro do dispositivo* remoto específico da solução de monitoramento que armazena o histórico de comandos e de métodos. Olá usos de solução de monitoramento remoto um [Cosmos DB] [ lnk-docdb] tooimplement de banco de dados um repositório personalizado para o histórico de comando e método.

> [!NOTE]
> Olá solução pré-configurada de monitoramento remoto mantém o registro de identidade de dispositivo de saudação em sincronia com informações de saudação no banco de dados de banco de dados do Cosmos hello. Ambos usam Olá mesmo toouniquely de id de dispositivo identificar cada dispositivo conectado tooyour IoT hub.

## <a name="device-metadata"></a>Metadados de dispositivo

IoT Hub mantém um [duas dispositivo] [ lnk-device-twin] para cada dispositivo simulado e físico conectado tooa remota de solução de monitoramento. solução de saudação usa dispositivo twins toomanage Olá metadados associados a dispositivos. Duas um dispositivo é um documento JSON mantido pelo IoT Hub e solução de saudação usa Olá API de Hub IoT toointeract com twins de dispositivo.

Um dispositivo gêmeo armazena três tipos de metadados:

- *Relatado propriedades* são enviadas tooan IoT hub por um dispositivo. No hello remota de solução de monitoramento, dispositivos simulados enviam propriedades relatadas na inicialização e na resposta muito**alterar o estado do dispositivo** comandos e métodos. Você pode exibir propriedades relatadas no hello **lista de dispositivos** e **detalhes do dispositivo** no portal de solução de saudação. As propriedades relatadas são somente leitura.
- *Propriedades desejadas* são recuperadas do hub IoT de saudação pelos dispositivos. É responsabilidade de saudação do hello dispositivo toomake alterar qualquer configuração necessária no dispositivo de saudação. Também é responsabilidade de saudação do hub de toohello back Olá dispositivo tooreport Olá alteração como uma propriedade relatada. Você pode definir um valor de propriedade desejado por meio do portal de solução de saudação.
- *Marcas* só existem em duas de dispositivo hello e nunca são sincronizadas com um dispositivo. Você pode definir valores de marca no portal de solução hello e usá-los quando você filtrar Olá lista de dispositivos. solução de Olá também usa um toodisplay de ícone marca tooidentify Olá para um dispositivo no portal de solução de saudação.

Exemplo relatado propriedades dos dispositivos Olá simulado incluem fabricante, modelo, latitude e longitude. Lista de retorno também Olá dispositivos simulada dos métodos com suporte como uma propriedade relatada.

> [!NOTE]
> Olá dispositivo simulado código só usa Olá **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** Olá de tooupdate propriedades desejadas relatado propriedades enviadas de volta tooIoT Hub. Todas as outras solicitações de alteração de propriedade desejadas são ignoradas.

Um documento JSON de metadados do dispositivo informações armazenado no banco de dados Cosmos DB do registro de dispositivo de Olá tem Olá estrutura a seguir:

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> Informações de dispositivo também podem incluir metadados toodescribe Olá telemetria Olá dispositivo envia tooIoT Hub. solução de monitoramento remoto Olá usa essa toocustomize de metadados de telemetria como painel Olá exibe [telemetria dinâmica][lnk-dynamic-telemetry].

## <a name="lifecycle"></a>Ciclo de vida

Quando você cria primeiro um dispositivo no portal de solução hello, solução de saudação cria uma entrada de saudação comando de toostore de banco de dados do banco de dados do Cosmos e histórico de método. Neste ponto, a solução de Olá também cria uma entrada para o dispositivo de saudação no registro de identidade do dispositivo hello, que gera Olá chaves Olá dispositivo usa tooauthenticate com o IoT Hub. Ele também cria um dispositivo gêmeo.

Quando um dispositivo conectado pela primeira solução toohello, ele envia propriedades relatadas e uma mensagem de informações do dispositivo. Olá informou valores de propriedade são salvas automaticamente em duas de dispositivo de saudação. Olá relatado propriedades incluem o fabricante do dispositivo hello, número do modelo, número de série e uma lista de métodos com suporte. mensagem de informações de dispositivo de saudação inclui a lista de saudação de comandos Olá Olá dispositivo dá suporte à incluindo informações sobre quaisquer parâmetros de comando. Quando a solução Olá recebe essa mensagem, ele atualiza informações do dispositivo Olá no banco de dados de banco de dados do Cosmos hello.

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a>Exibir e editar informações de dispositivo no portal de solução de saudação

lista de dispositivos no portal de solução Olá Olá exibe Olá seguintes propriedades de dispositivo como colunas por padrão: **Status**, **DeviceId**, **fabricante**, **Número modelo**, **número de série**, **Firmware**, **plataforma**, **processador**e  **Instalado RAM**. Você pode personalizar colunas Olá clicando **editor coluna**. Olá propriedades do dispositivo **Latitude** e **Longitude** da unidade local Olá Olá mapa do Bing no painel de saudação.

![Editor de colunas na lista de dispositivos][img-device-list]

Em Olá **detalhes do dispositivo** painel no portal de solução hello, você pode editar as propriedades desejadas e marcas (relatado propriedades são somente leitura).

![Painel de detalhes do dispositivo][img-device-edit]

Você pode usar tooremove um dispositivo do portal de solução de saudação de sua solução. Quando você remover um dispositivo, solução de Olá remove a entrada do dispositivo de saudação do registro de identidade e, em seguida, exclui duas de dispositivo de saudação. solução Olá também remove o dispositivo de toohello relacionados de informações do banco de dados de banco de dados do Cosmos hello. Antes de remover um dispositivo, você deverá desabilitá-lo.

![Remover o dispositivo][img-device-remove]

## <a name="device-information-message-processing"></a>Processamento de mensagens de informações de dispositivo

As mensagens de informações sobre um dispositivo enviadas por um dispositivo são diferentes das mensagens de telemetria. Mensagens de informações do dispositivo incluem comandos Olá a que um dispositivo pode responder e qualquer histórico de comandos. IoT Hub em si não tem conhecimento de metadados de saudação contido em uma mensagem de informações do dispositivo e processos Olá mensagem de saudação mesma forma que processa qualquer mensagem do dispositivo para a nuvem. Na solução de monitoramento remoto de saudação um [Azure Stream Analytics] [ lnk-stream-analytics] trabalho (ASA) lê mensagens de saudação do IoT Hub. Olá **DeviceInfo** análise de fluxo de trabalho filtros para mensagens que contêm **"ObjectType": "DeviceInfo"** e encaminha-toohello **EventProcessorHost** host instância que é executado em um trabalho da web. Lógica em Olá **EventProcessorHost** instância usa o registro de banco de dados do Cosmos Olá dispositivo id toofind Olá para Olá dispositivo e atualização Olá registro específico.

> [!NOTE]
> Uma mensagem de informações de dispositivo é uma mensagem padrão do dispositivo para a nuvem. solução de saudação faz distinção entre mensagens de informações de dispositivo e telemetria por meio de consultas ASA.

## <a name="next-steps"></a>Próximas etapas

Agora você terminou a aprender como você pode personalizar soluções Olá pré-configurados, você pode explorar alguns dos Olá outros recursos e capacidades de soluções do IoT Suite pré-configurado hello:

* [Visão geral da solução pré-configurada de manutenção preditiva][lnk-predictive-overview]
* [Perguntas frequentes sobre o IoT Suite][lnk-faq]
* [Segurança de IoT da saudação de plano de fundo para cima][lnk-security-groundup]

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
