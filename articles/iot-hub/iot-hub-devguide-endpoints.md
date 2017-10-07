---
title: pontos de extremidade de Azure IoT Hub aaaUnderstand | Microsoft Docs
description: "Guia do desenvolvedor ‑ Informações de referência sobre pontos de extremidade do Hub IoT voltados para o dispositivo e para o serviço."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 57ba52ae-19c6-43e4-bc6c-d8a5c2476e95
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 8647f15d2f2a050ad5799ea82f4d2d46db0dbec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-endpoints"></a>Referência - Pontos de extremidade do Hub IoT

## <a name="iot-hub-names"></a>Nomes de Hub IoT

Você pode encontrar o nome de saudação do hub IoT Olá que hospeda os pontos de extremidade no portal de saudação em Olá **visão geral** folha. Por padrão, o nome DNS de saudação de um hub IoT parece com: `{your iot hub name}.azure-devices.net`.

Você pode usar um nome DNS personalizado para o hub IoT de toocreate de DNS do Azure. Para obter mais informações, consulte [configurações de domínio personalizado tooprovide usam o DNS do Azure para um serviço do Azure](../dns/dns-custom-domain.md#azure-iot).

## <a name="list-of-built-in-iot-hub-endpoints"></a>Lista de pontos de extremidade internos do Hub IoT

IoT Hub do Azure é um serviço de multilocatário que expõe atores de toovarious sua funcionalidade. Olá diagrama a seguir mostra Olá vários pontos de extremidade que expõe IoT Hub.

![Pontos de extremidade do Hub IoT][img-endpoints]

Olá lista a seguir descreve os pontos de extremidade de saudação:

* **Provedor de recursos**. Olá provedor de recursos de IoT Hub expõe um [do Azure Resource Manager] [ lnk-arm] interface. Essa interface permite toocreate de proprietários de assinatura do Azure e excluir hubs IoT e propriedades de hub IoT tooupdate. Propriedades de IoT Hub controlam [políticas de segurança de nível de hub][lnk-accesscontrol], ao contrário do controle de acesso toodevice e funcionais opções para mensagens de nuvem para dispositivo e o dispositivo para a nuvem. Olá provedor de recursos de IoT Hub também permite que você muito[exportar identidades de dispositivo][lnk-importexport].
* **Gerenciamento de identidades dos dispositivos**. Cada hub IoT expõe um conjunto de identidades de dispositivo de toomanage de pontos de extremidade de REST de HTTP (criar, recuperar, atualizar e excluir). [As identidades do dispositivo][lnk-device-identities] são usadas para controle de acesso e autenticação do dispositivo.
* **Gerenciamento do dispositivo gêmeo**. Cada hub IoT expõe um conjunto de tooquery de ponto de extremidade de REST de HTTP e a atualização voltados para o serviço [twins dispositivo] [ lnk-twins] (atualização de marcas e propriedades).
* **Gerenciamento de trabalhos**. Cada hub IoT expõe um conjunto de tooquery de ponto de extremidade de REST de HTTP voltados para o serviço e gerenciar [trabalhos][lnk-jobs].
* **Pontos de extremidade do dispositivo**. Para cada dispositivo no registro de identidade hello, o IoT Hub expõe um conjunto de pontos de extremidade:

  * *Enviar mensagens do dispositivo para a nuvem*. Um dispositivo usa esse ponto de extremidade muito[enviar mensagens de dispositivo para nuvem][lnk-d2c].
  * *Receber mensagens da nuvem para o dispositivo*. Um dispositivo usa esse tooreceive de ponto de extremidade direcionado [mensagens de nuvem para dispositivo][lnk-c2d].
  * *Inicie os uploads de arquivos*. Um dispositivo usa esse ponto de extremidade tooreceive um URI de SAS do armazenamento do Azure do IoT Hub muito[carregar um arquivo][lnk-upload].
  * *Recupere e atualize as propriedades do dispositivo gêmeo*. Um dispositivo usa esse ponto de extremidade tooaccess seu [duas dispositivo][lnk-twins]de propriedades.
  * *Receber solicitações de métodos diretos*. Um dispositivo usa esse toolisten de ponto de extremidade para [método direto][lnk-methods]de solicitações.

    Estes pontos de extremidade são expostos usando os protocolos [MQTT v3.1.1][lnk-mqtt], HTTP 1.1 e [AMQP 1.0][lnk-amqp]. O AMQP também está disponível sobre [WebSockets][lnk-websockets] na porta 443.

    Olá pontos de extremidade twins e métodos do dispositivo estão disponíveis somente quando você usa Olá [v MQTT 3.1.1] [ lnk-mqtt] protocolo.

* **Pontos de extremidade do serviço**. Cada hub IoT expõe um conjunto de pontos de extremidade para sua toocommunicate de back-end de solução com seus dispositivos. Com uma exceção, esses pontos de extremidade só são expostos usando Olá [AMQP] [ lnk-amqp] protocolo. ponto de extremidade de invocação de método Hello é exposto pela Olá protocolo HTTP.
  
  * *Receber mensagens do dispositivo para a nuvem*. Esse ponto de extremidade é compatível com os [Hubs de Eventos do Azure][lnk-event-hubs]. Um serviço back-end pode usá-lo Olá tooread [mensagens de dispositivo para nuvem] [ lnk-d2c] enviados por seus dispositivos. Você pode criar pontos de extremidade personalizados em seu hub IoT no ponto de extremidade internos adição toothis.
  * *Enviar mensagens da nuvem para o dispositivo e receber confirmações de entrega*. Esses pontos de extremidade permitem toosend de back-end sua solução confiável [mensagens de nuvem para dispositivo][lnk-c2d], e tooreceive Olá confirmações de entrega ou expiração correspondentes.
  * *Receba notificações de arquivo*. Esse ponto de extremidade de mensagens permite que você tooreceive as notificações quando seus dispositivos carreguem com êxito um arquivo. 
  * *Invocação direta de método*. Esse ponto de extremidade permite que um serviço back-end tooinvoke um [método direto] [ lnk-methods] em um dispositivo.
  * *Eventos de monitoramento de operações de recebimento*. Esse ponto de extremidade permite operações de tooreceive eventos de monitoramento, se seu IoT hub tiver sido configurado tooemit-los. Para obter mais informações, consulte [Monitoramento de operações do Hub IoT][lnk-operations-mon].

Olá [SDKs do Azure IoT] [ lnk-sdks] descreve Olá tooaccess de várias maneiras esses pontos de extremidade.

Todos os pontos de extremidade de IoT Hub usam Olá [TLS] [ lnk-tls] protocolo e nenhum ponto de extremidade nunca é exposta em canais descriptografados/não segura.

## <a name="custom-endpoints"></a>Pontos de extremidade personalizados

Você pode vincular os serviços do Azure existentes em seu tooact de hub IoT assinatura tooyour como pontos de extremidade para roteamento de mensagens. Esses agem como pontos de extremidade de serviço e são usados como "coletores" para rotas de mensagens. Dispositivos não podem gravar diretamente toohello mais pontos de extremidade. toolearn mais informações sobre rotas de mensagens, consulte a entrada de guia do desenvolvedor de saudação em [enviando e recebendo mensagens com o hub IoT][lnk-devguide-messaging].

IoT Hub atualmente suporta Olá serviços do Azure como pontos de extremidade adicionais a seguir:

* Hubs de Eventos
* Filas de barramento de serviço
* Tópicos do Service Bus

IoT Hub precisa de pontos de extremidade de serviço do acesso de gravação toothese toowork de roteamento da mensagem. Se você configurar os pontos de extremidade por meio de saudação portal do Azure, as permissões necessárias Olá são adicionadas para você. Certifique-se de que configurar a taxa de transferência serviços toosupport Olá esperado. Quando você primeiro configure sua solução de IoT, você pode precisa toomonitor seus pontos de extremidade adicionais e faça os ajustes necessários para a carga real Olá.

Se uma mensagem corresponde a várias rotas que apontam toohello mesmo ponto de extremidade de IoT Hub fornece o ponto de extremidade do mensagem toothat apenas uma vez. Portanto, você pode fazer não necessidade tooconfigure eliminação de duplicação no tópico ou fila do barramento de serviço. Em filas particionados, a afinidade de partição garante a ordenação das mensagens.

> [!NOTE]
> As filas e os tópicos do Barramento de Serviço utilizados como pontos de extremidade do Hub IoT não devem ter **Sessões** nem **Detecção Duplicada** habilitadas. Se qualquer uma dessas opções estiver habilitada, o ponto de extremidade de saudação aparece como **inacessível** em Olá portal do Azure.

Para Olá limites no número de saudação de pontos de extremidade, você pode adicionar, consulte [cotas e limitação][lnk-devguide-quotas].

## <a name="field-gateways"></a>Gateways de campo

Em uma solução IoT, um *gateway de campo* fica entre os dispositivos e os pontos de extremidade do hub IoT. É geralmente localizado tooyour fechar dispositivos. Os dispositivos se comunicar diretamente com o gateway de campo hello usando um protocolo com suporte de dispositivos de saudação. gateway de campo de saudação conecta tooan ponto de extremidade de IoT Hub usando um protocolo com suporte pelo IoT Hub. Um gateway de campo pode ser um dispositivo de hardware dedicado ou em um computador de baixa capacidade que executam o software do gateway personalizado.

Você pode usar [Azure IoT borda] [ lnk-iot-edge] tooimplement um gateway de campo. Borda de IoT oferece funcionalidade como multiplexação comunicações de vários dispositivos para Olá mesma conexão de IoT Hub.

## <a name="next-steps"></a>Próximas etapas

Outros tópicos de referência neste Guia do desenvolvedor do Hub IoT incluem:

* [Linguagem de consulta do Hub IoT para dispositivos gêmeos, trabalhos e roteamento de mensagens][lnk-devguide-query]
* [Cotas e limitações][lnk-devguide-quotas]
* [Suporte ao MQTT do Hub IoT][lnk-devguide-mqtt]

[lnk-iot-edge]: https://github.com/Azure/iot-edge

[img-endpoints]: ./media/iot-hub-devguide-endpoints/endpoints.png
[lnk-amqp]: https://www.amqp.org/
[lnk-mqtt]: http://mqtt.org/
[lnk-websockets]: https://tools.ietf.org/html/rfc6455
[lnk-arm]: ../azure-resource-manager/resource-group-overview.md
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/

[lnk-tls]: https://tools.ietf.org/html/rfc5246


[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-accesscontrol]: iot-hub-devguide-security.md#access-control-and-permissions
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-device-identities]: iot-hub-devguide-identity-registry.md
[lnk-upload]: iot-hub-devguide-file-upload.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md

[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[lnk-operations-mon]: iot-hub-operations-monitoring.md
