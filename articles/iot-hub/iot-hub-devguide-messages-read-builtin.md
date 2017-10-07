---
title: aaaUnderstand hello Azure IoT Hub interno ponto de extremidade | Microsoft Docs
description: "Guia do desenvolvedor - descreve como toouse Olá interno, mensagens de dispositivo para nuvem compatível com o evento Hub endpoint toread."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a>Ler mensagens de dispositivo para a nuvem de ponto de extremidade internos Olá

Por padrão, as mensagens são roteadas toohello internos voltados para o serviço endpoint (**mensagens de eventos**), que é compatível com [Hubs de eventos][lnk-event-hubs]. Esse ponto de extremidade está exposta somente usando Olá [AMQP] [ lnk-amqp] protocolo na porta 5671. Um hub IoT expõe Olá seguintes propriedades tooenable toocontrol você Olá compatível com o evento Hub mensagens ponto de extremidade integrado **mensagens de eventos**.

| Propriedade            | Descrição |
| ------------------- | ----------- |
| **Contagem de partição** | Defina essa propriedade no número de saudação toodefine criação de [partições] [ lnk-event-hub-partitions] para inclusão de eventos de dispositivo para a nuvem. |
| **Período de retenção**  | Esta propriedade especifica por quanto tempo, em dias, as mensagens são retidas pelo Hub IoT. saudação padrão é um dia, mas pode ser aumentada tooseven dias. |

IoT Hub também permite que você toomanage grupos de consumidores no hello internos dispositivo para nuvem receber o ponto de extremidade.

Por padrão, todas as mensagens que não coincidem explicitamente uma regra de roteamento de mensagem são gravadas toohello ponto de extremidade internos. Se você desabilitar esta rota de fallback, as mensagens que não corresponderão explicitamente a nenhuma regra de roteamento de mensagem são descartadas.

Você pode modificar o tempo de retenção de saudação programaticamente por meio de saudação [APIs REST de provedor de recursos do IoT Hub][lnk-resource-provider-apis], ou usando Olá [portal do Azure] [ lnk-management-portal].

IoT Hub expõe Olá **mensagens de eventos** mensagens de dispositivo para nuvem saudação tooread recebidas pelo seu hub de serviços de ponto de extremidade interno para o back-end. Esse ponto de extremidade é um evento de Hub compatível, que permite que você toouse qualquer serviço de Hubs de eventos de Olá Olá mecanismos oferece suporte para leitura de mensagens.

## <a name="read-from-hello-built-in-endpoint"></a>Leitura do ponto de extremidade internos Olá

Quando você usa Olá [SDK do barramento de serviço do Azure para .NET] [ lnk-servicebus-sdk] ou hello [Hubs de eventos - evento processador Host][lnk-eventprocessorhost], você pode usar qualquer conexão de IoT Hub cadeias de caracteres com as permissões corretas hello. Em seguida, use **mensagens de eventos** como nome do Hub de eventos de saudação.

Quando você usa SDKs (ou integrações de produto) que não estiver ciente de IoT Hub, você deve recuperar um ponto de extremidade compatível com o evento Hub e um nome compatível com o evento Hub das configurações de Hub IoT Olá Olá [portal do Azure] [ lnk-management-portal]:

1. Na folha de hub do IoT hello, clique em **pontos de extremidade**.
1. Em Olá **pontos de extremidade internos** seção, clique em **eventos**. Olá, folha contém Olá valores a seguir: **ponto de extremidade de Hub de eventos-compatível com**, **nome compatível com o evento Hub**, **partições**, **detempoderetenção**, e **grupos de consumidores**.

    ![Configurações de dispositivo para a nuvem][img-eventhubcompatible]

Olá IoT Hub SDK requer Olá nome de ponto de extremidade de IoT Hub, que é **mensagens de eventos** conforme Olá **pontos de extremidade** folha.

Se Olá SDK que você está usando requer um **Hostname** ou **Namespace** valor, remova o esquema de saudação da saudação **ponto de extremidade compatível com o evento Hub**. Por exemplo, se o ponto de extremidade compatível com o evento Hub é **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, Olá **Hostname** seria  **Hub IOT ns-myiothub 1234.servicebus.windows.net**e hello **Namespace** seria **ns hub IOT-1234 myiothub**.

Você pode usar qualquer política de acesso compartilhado que tenha Olá **ServiceConnect** toohello de tooconnect de permissões especificado de Hub de eventos.

Se você precisar toobuild uma cadeia de caracteres de conexão do Hub de eventos usando as informações anteriores Olá, use o saudação padrão a seguir:

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

Olá SDKs e integrações que você pode usar com pontos de extremidade compatível com o evento Hub IoT Hub expõe inclui os itens Olá Olá lista a seguir:

* [Cliente Java dos Hubs de Eventos](https://github.com/hdinsight/eventhubs-client).
* [Spout do Apache Storm](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md). Você pode exibir uma saudação [spout origem](https://github.com/apache/storm/tree/master/external/storm-eventhubs) no GitHub.
* [Integração do Apache Spark](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre pontos de extremidade do Hub IoT, confira [Pontos de extremidade do Hub IoT][lnk-endpoints].

Olá [começar] [ lnk-get-started] tutoriais mostram como mensagens de dispositivo para nuvem toosend de simulados dispositivos e leem mensagens de saudação do ponto de extremidade internos hello. Para obter mais detalhes, consulte Olá [mensagens de dispositivo para nuvem processo IoT Hub usando rotas] [ lnk-d2c-tutorial] tutorial.

Se você quiser tooroute seu dispositivo para nuvem mensagens toocustom pontos de extremidade, consulte [usar rotas de mensagens e pontos de extremidade personalizados para mensagens de dispositivo para nuvem][lnk-custom].

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/
