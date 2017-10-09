---
title: aaaAzure gerenciamento de dispositivo IoT com o Gerenciador de Hub IOT | Microsoft Docs
description: "Use a ferramenta CLI de Gerenciador de Hub IOT de saudação para gerenciamento de dispositivos do Azure IoT Hub, apresentando métodos diretos hello e opções de gerenciamento do hello duas propriedades desejadas."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gerenciamento de dispositivos iot do azure, gerenciamento de dispositivos hub iot do azure, iot de gerenciamento de dispositivos, gerenciamento de dispositivos hub iot
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a>Usar o iothub-explorer para o gerenciamento de dispositivos Hub IoT do Azure

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[Gerenciador de Hub IOT](https://github.com/azure/iothub-explorer) é uma ferramenta CLI que são executados em um identidades de dispositivo de toomanage do computador host no registro do hub IoT. Ela vem com opções de gerenciamento que você pode usar tooperform várias tarefas.

| Opção de gerenciamento          | Tarefa                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Métodos diretos             | Tornar um dispositivo para atuar como iniciar ou parar o envio de mensagens ou a reinicialização do dispositivo hello.                                        |
| Propriedades desejadas do gêmeo    | Colocar um dispositivo em alguns estados, como definir um LED toogreen ou configuração de telemetria Olá enviar intervalo (minutos) too30.         |
| Propriedades relatadas do gêmeo   | Obter Olá relatou o estado de um dispositivo. Por exemplo, o dispositivo Olá relata Olá que LED estiver piscando agora.                                    |
| Marcações do gêmeo                  | Armazenar os metadados específicos do dispositivo na nuvem hello. Por exemplo, Olá local de implantação de uma máquina de vendas.                         |
| Mensagens da nuvem para o dispositivo   | Dispositivo de tooa de notificações de envio. Por exemplo, "é muito provável que toorain hoje. Não se esqueça de um conjunto de toobring."              |
| Consultas de dispositivo gêmeo        | Consulta tooretrieve de twins todos os dispositivos com condições arbitrárias, como identificar os dispositivos de saudação que estão disponíveis para uso. |

Para obter mais explicações sobre as diferenças de saudação e orientação sobre como usar essas opções, consulte [orientação de comunicação do dispositivo para nuvem](iot-hub-devguide-d2c-guidance.md) e [orientação de comunicação de nuvem para dispositivo](iot-hub-devguide-c2d-guidance.md).

> [!NOTE]
> Dispositivos gêmeos são documentos JSON que armazenam informações do estado do dispositivo (metadados, configurações e condições). IoT Hub mantém duas um dispositivo de cada dispositivo que se conecta tooit. Para obter mais informações sobre dispositivos gêmeos, consulte [Introdução aos dispositivos gêmeos](iot-hub-node-node-twin-getstarted.md).

## <a name="what-you-learn"></a>O que você aprenderá

Você aprenderá a usar o iothub-explorer com várias opções de gerenciamento em seu computador de desenvolvimento.

## <a name="what-you-do"></a>O que fazer

Execute o iothub-explorer com várias opções de gerenciamento.

## <a name="what-you-need"></a>O que você precisa

- Tutorial [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluída que abrange Olá requisitos a seguir:
  - Uma assinatura ativa do Azure.
  - Um hub IoT do Azure em sua assinatura.
  - Um aplicativo cliente que envia o hub do mensagens tooyour IoT do Azure.
- Verifique se que o dispositivo está em execução com o aplicativo de cliente hello durante este tutorial.
- iothub-explorer, [Instalar iothub-explorer](https://github.com/azure/iothub-explorer) no computador de desenvolvimento.

## <a name="connect-tooyour-iot-hub"></a>Conecte tooyour IoT hub

Conecte-se tooyour IoT hub executando Olá comando a seguir:

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a>Usar o iothub-explorer com métodos diretos

Invocar Olá `start` método hello dispositivo toosend mensagens tooyour IoT hub de aplicativos executando Olá comando a seguir:

```bash
iothub-explorer device-method <your device Id> start
```

Invocar Olá `stop` método hello dispositivo aplicativo toostop enviar mensagens tooyour IoT hub executando Olá comando a seguir:

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a>Usar o iothub-explorer com as propriedades desejadas do gêmeo

Definir um intervalo de propriedade desejados = 3000 executando Olá comando a seguir:

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

Essa propriedade pode ser lida pelo dispositivo.

## <a name="use-iothub-explorer-with-twins-reported-properties"></a>Usar o iothub-explorer com as propriedades relatadas do gêmeo

Obtenham hello relatadas propriedades de dispositivo de saudação executando Olá comando a seguir:

```bash
iothub-explorer get-twin <your device id>
```

Uma das propriedades de saudação é $metadata. $lastUpdated que mostra Olá última vez em que o dispositivo envia ou recebe uma mensagem.

## <a name="use-iothub-explorer-with-twins-tags"></a>Usar o iothub-explorer com marcações do gêmeo

Exibir marcas hello e propriedades de dispositivo de saudação executando Olá comando a seguir:

```bash
iothub-explorer get-twin <your device id>
```

Adicionar uma função de campo = dispositivo toohello de temperatura e umidade executando Olá comando a seguir:

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a>Usar o iothub-explorer para enviar mensagens da nuvem para o dispositivo

Envie um dispositivo de toohello de mensagem "Hello World" executando Olá comando a seguir:

```bash
iothub-explorer send <device-id> "Hello World"
```

Consulte [usar o Gerenciador de Hub IOT toosend e receber mensagens entre o dispositivo e o IoT Hub](iot-hub-explorer-cloud-device-messaging.md) para um cenário real de usar esse comando.

## <a name="use-iothub-explorer-with-device-twins-queries"></a>Usar o iothub-explorer com consultas de dispositivos gêmeos

Dispositivos com uma marca de função de consulta = 'temperatura e umidade' executando Olá comando a seguir:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

Consultar todos os dispositivos, exceto aqueles com uma marca de função = 'temperatura e umidade' executando Olá comando a seguir:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a>Próximas etapas

Você aprendeu como toouse hub IOT-explorer com várias opções de gerenciamento.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
