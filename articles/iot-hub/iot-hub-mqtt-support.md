---
title: aaaUnderstand suporte do Azure IoT Hub MQTT | Microsoft Docs
description: "Desenvolvedor guiá - suporte para dispositivos que se conectam tooan IoT Hub voltados para o dispositivo usando o ponto de extremidade Olá protocolo MQTT. Inclui informações sobre suporte interno ao MQTT Olá SDKs de dispositivo IoT do Azure."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a>Se comunicar com o hub IoT usando o protocolo MQTT Olá

IoT Hub permite que dispositivos toocommunicate com hello Hub IoT dispositivo pontos de extremidade usando Olá [v MQTT 3.1.1] [ lnk-mqtt-org] protocolo porta 8883 ou v 3.1.1 MQTT com o protocolo WebSocket na porta 443. IoT Hub requer que todos os toobe de comunicação do dispositivo protegida usando SSL/TLS (assim, IoT Hub não oferece suporte a conexões não seguras pela porta 1883).

## <a name="connecting-tooiot-hub"></a>Conectando tooIoT Hub

Um dispositivo pode usar hub de IoT Olá MQTT protocolo tooconnect tooan usando bibliotecas Olá Olá [SDKs do Azure IoT] [ lnk-device-sdks] ou usando o protocolo de MQTT saudação diretamente.

## <a name="using-hello-device-sdks"></a>Usando o dispositivo Olá SDKs

[Dispositivo SDKs] [ lnk-device-sdks] Olá que suporte o protocolo MQTT estão disponíveis para Java, Node.js, C, c# e Python. usar o dispositivo de saudação SDKs saudação padrão cadeia de caracteres tooestablish um hub de IoT tooan conexão do IoT Hub conexão. toouse Olá MQTT protocolo, parâmetro de protocolo de cliente hello deve ser definido muito**MQTT**. Por padrão, o dispositivo Olá SDKs conectar tooan IoT Hub com hello **CleanSession** sinalizador definido muito**0** e usar **QoS 1** para troca de mensagens com o hub IoT de saudação.

Quando um dispositivo está conectado tooan hub IoT, dispositivo Olá SDKs forneça métodos que habilitar Olá dispositivo toosend mensagens tooand receber mensagens de um hub IoT.

Olá tabela a seguir contém links toocode exemplos para cada idioma suportado e especifica Olá parâmetro toouse tooestablish tooIoT uma conexão Hub usando o protocolo MQTT hello.

| idioma | Parâmetro do protocolo |
| --- | --- |
| [Node.js][lnk-sample-node] |azure-iot-device-mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a>Migrando um aplicativo de dispositivo do AMQP tooMQTT

Se você estiver usando Olá [dispositivo SDKs][lnk-device-sdks], alternando de usar o AMQP tooMQTT requer a alteração do parâmetro de protocolo hello na inicialização do cliente hello como mencionado anteriormente.

Ao fazer isso, certifique-se de saudação toocheck itens a seguir:

* AMQP retorna erros para várias condições, enquanto MQTT encerra a conexão de saudação. Como resultado, sua lógica de manipulação de exceções pode exigir algumas alterações.
* MQTT não oferece suporte a saudação *rejeitar* operações quando receber [mensagens de nuvem para dispositivo][lnk-messaging]. Se seu aplicativo de back-end precisa tooreceive uma resposta do aplicativo para dispositivo hello, considere o uso de [direto métodos][lnk-methods].

## <a name="using-hello-mqtt-protocol-directly"></a>Usando o protocolo de MQTT saudação diretamente
Se um dispositivo não é possível usar o dispositivo Olá SDKs, ele ainda possa se conectar pontos de extremidade do dispositivo público toohello usando o protocolo de MQTT saudação na porta 8883. Em Olá **conectar** dispositivo de saudação do pacote deve usar Olá valores a seguir:

* Para Olá **ClientId** campo, use Olá **deviceId**.
* Para Olá **Username** campo, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, onde {iothubhostname} é Olá CName completa de hub IoT de saudação.

    Por exemplo, se hello nome do seu hub IoT é **contoso.azure devices.net** e se o nome de saudação do seu dispositivo é **MyDevice01**, Olá completo **Username** campo deve conter `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* Para Olá **senha** campo, use um token SAS. formato de saudação do hello token SAS é Olá mesmo como para Olá HTTP e protocolos AMQP:<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.

    Para obter mais informações sobre como toogenerate tokens SAS, consulte a seção de dispositivo de saudação do [tokens de segurança usando IoT Hub][lnk-sas-tokens].

    Durante o teste, você também pode usar o hello [explorer dispositivo] [ lnk-device-explorer] tooquickly ferramenta gerar um token SAS que você pode copiar e colar no seu próprio código:

  1. Vá toohello **gerenciamento** guia **Gerenciador de dispositivo**.
  2. Clique em **Token SAS** (parte superior direita).
  3. Em **SASTokenForm**, selecione o dispositivo em Olá **DeviceID** lista suspensa. Defina o **TTL**.
  4. Clique em **gerar** toocreate seu token.

     token SAS que é gerado Hello tem esta estrutura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

     Olá parte esse token toouse como Olá **senha** tooconnect campo usando MQTT é: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

Para MQTT se conectar e desconectar pacotes, IoT Hub emite um evento em Olá **operações de monitoramento** canal com informações adicionais que podem ajudá-lo tootroubleshoot problemas de conectividade.

### <a name="sending-device-to-cloud-messages"></a>Enviando mensagens de dispositivo para nuvem

Depois de fazer uma conexão bem-sucedida, um dispositivo pode enviar mensagens tooIoT Hub usando `devices/{device_id}/messages/events/` ou `devices/{device_id}/messages/events/{property_bag}` como um **o nome do tópico**. Olá `{property_bag}` elemento permite que mensagens de saudação toosend do dispositivo com propriedades adicionais em um formato codificado de url. Por exemplo:

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> Isso `{property_bag}` elemento usa Olá a mesma codificação que cadeias de caracteres de consulta no protocolo de saudação HTTP.
>
>

também pode usar o aplicativo de dispositivo Olá `devices/{device_id}/messages/events/{property_bag}` como Olá **será o nome do tópico** toodefine *será mensagens* toobe encaminhada como uma mensagem de telemetria.

- O Hub IoT não dá suporte a mensagens de QoS 2. Se um aplicativo de dispositivo publica uma mensagem com **QoS 2**, IoT Hub fecha a conexão de rede de saudação.
- O Hub IoT não persiste mensagens de retenção. Se um dispositivo envia uma mensagem de saudação **RETER** sinalizador definido too1, IoT Hub adiciona Olá **x-opt-reter** mensagem de toohello de propriedade do aplicativo. Nesse caso, em vez da saudação persistente reter a mensagem, o IoT Hub transmite toohello aplicativo de back-end.
- O Hub IoT oferece suporte apenas a uma conexão MQTT ativa por dispositivo. Qualquer conexão MQTT novo em nome hello mesma ID de dispositivo faz com que o IoT Hub conexão existente do toodrop hello.

Para obter mais informações, consulte [Guia do desenvolvedor do sistema de mensagens][lnk-messaging].

### <a name="receiving-cloud-to-device-messages"></a>Recebendo mensagens da nuvem para o dispositivo

mensagens de tooreceive de IoT Hub, um dispositivo deve assinar usando `devices/{device_id}/messages/devicebound/#` como um **tópico filtro**. Olá curinga multinível  **#**  Olá filtro de tópico é usado somente tooallow Olá propriedades adicionais do dispositivo tooreceive no nome do tópico hello. IoT Hub não permite o uso de saudação do hello  **#**  ou **?** para filtragem de subtópicos. Como o IoT Hub não é um agente de mensagens geral pub-sub, suporta apenas nomes de tópico Olá documentado e filtros de tópico.

Hello dispositivo não recebe as mensagens de IoT Hub, até que ele tenha assinado com êxito ponto de extremidade específico do dispositivo de tooits, representado pelo Olá `devices/{device_id}/messages/devicebound/#` filtro de tópico. Depois de assinatura bem-sucedida foi estabelecida, o dispositivo Olá começa a receber mensagens de somente de nuvem para dispositivo que foram enviadas tooit após o tempo de saudação de assinatura de saudação. Se o dispositivo de saudação se conecta com **CleanSession** sinalizador definido muito**0**, assinatura de saudação é persistente entre as diferentes sessões. Olá nesse caso, a próxima vez que ele se conecta com **CleanSession 0** dispositivo Olá recebe mensagens pendentes que foram enviadas tooit enquanto estava desconectado. Se o dispositivo Olá usa **CleanSession** sinalizador definido muito**1** , não recebe as mensagens de IoT Hub até que ele assina tooits ponto de extremidade do dispositivo.

IoT Hub entrega mensagens com hello **o nome do tópico** `devices/{device_id}/messages/devicebound/`, ou `devices/{device_id}/messages/devicebound/{property_bag}` se houver quaisquer propriedades de mensagem. `{property_bag}` contém pares de chave/valor codificados de URL das propriedades da mensagem. Apenas as propriedades de aplicativo e as propriedades do sistema definível pelo usuário (como **messageId** ou **correlationId**) são incluídos no conjunto de propriedades de saudação. Nomes de propriedade do sistema têm o prefixo de saudação  **$** , propriedades do aplicativo usam o nome da propriedade original Olá sem prefixo.

Quando um aplicativo de dispositivo assina tópico tooa com **QoS 2**, IoT Hub concede o nível máximo QoS 1 em Olá **SUBACK** pacote. Depois disso, o IoT Hub oferece dispositivo toohello de mensagens usando a QoS 1.

### <a name="retrieving-a-device-twins-properties"></a>Recuperando as propriedades de um dispositivo gêmeo

Primeiro, um dispositivo assina muito`$iothub/twin/res/#`, respostas da operação de saudação tooreceive. Em seguida, ele envia uma mensagem vazia tootopic `$iothub/twin/GET/?$rid={request id}`, com um valor preenchido para **id da solicitação**. serviço hello, em seguida, envia uma mensagem de resposta que contém dados de duas dispositivo Olá no tópico `$iothub/twin/res/{status}/?$rid={request id}`, usando Olá mesmo  **id da solicitação** como solicitação de saudação.

A ID da solicitação pode ser qualquer valor válido de um valor da propriedade de mensagem, de acordo com o [Guia do desenvolvedor do sistema de mensagens do Hub IoT][lnk-messaging] e o status é validado como um inteiro.
corpo da resposta de Olá contém uma seção de propriedades de saudação do duas de dispositivo de saudação:

corpo de saudação da entrada de registro de identidade Olá limitado toohello membro de "propriedades", por exemplo:

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

Olá códigos de status possíveis são:

|Status | Descrição |
| ----- | ----------- |
| 200 | Sucesso |
| 429 | Número excessivo de solicitações (limitado), de acordo com a [Limitação do Hub IoT][lnk-quotas] |
| 5** | Erros do servidor |

Para obter mais informações, consulte [Guia do desenvolvedor de dispositivos gêmeos][lnk-devguide-twin].

### <a name="update-device-twins-reported-properties"></a>Atualizar as propriedades relatadas do dispositivo gêmeo

Olá sequência a seguir descreve como um dispositivo atualiza Olá relatado propriedades em duas de dispositivo Olá no IoT Hub:

1. Um dispositivo deve se inscrever inicialmente toohello `$iothub/twin/res/#` respostas da operação do tópico tooreceive saudação do IoT Hub.

1. Um dispositivo envia uma mensagem que contém a saudação dispositivo duas atualização toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` tópico. Essa mensagem inclui um valor de **id da solicitação**.

1. Olá serviço, em seguida, envia uma mensagem de resposta que contém Olá novo valor de ETag para Olá a coleção de propriedades relatado no tópico `$iothub/twin/res/{status}/?$rid={request id}`. Essa mensagem de resposta usa Olá mesmo **id da solicitação** como solicitação de saudação.

Olá corpo da mensagem de solicitação contém um documento JSON, que fornece novos valores para as propriedades relatadas (podem ser modificado sem propriedades ou metadados).
Cada membro no documento JSON Olá atualizações ou Adicionar membro correspondente Olá no documento do duas do dispositivo hello. Um membro definido muito`null`, exclusões Olá membro de saudação que contém o objeto. Por exemplo:

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

Olá códigos de status possíveis são:

|Status | Descrição |
| ----- | ----------- |
| 200 | Sucesso |
| 400 | Solicitação inválida. JSON malformado |
| 429 | Número excessivo de solicitações (limitado), de acordo com a [Limitação do Hub IoT][lnk-quotas] |
| 5** | Erros do servidor |

Para obter mais informações, consulte [Guia do desenvolvedor de dispositivos gêmeos][lnk-devguide-twin].

### <a name="receiving-desired-properties-update-notifications"></a>Recebendo notificações de atualização de propriedades desejadas

Quando um dispositivo estiver conectado, o IoT Hub envia o tópico de toohello notificações `$iothub/twin/PATCH/properties/desired/?$version={new version}`, que contêm o conteúdo de Olá Olá atualização executada pelo back-end de solução hello. Por exemplo:

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

Para atualizações de propriedade `null` valores significa que Olá JSON do objeto membro está sendo excluído.


> [!IMPORTANT] 
> O Hub IoT gera notificações de alteração somente quando os dispositivos estão conectados. Verifique se Olá de tooimplement [fluxo de reconexão do dispositivo] [ lnk-devguide-twin-reconnection] tookeep Olá desejado propriedades sincronizadas entre o IoT Hub e o aplicativo de dispositivo de saudação.

Para obter mais informações, consulte [Guia do desenvolvedor de dispositivos gêmeos][lnk-devguide-twin].

### <a name="respond-tooa-direct-method"></a>Método direto tooa de responder

Primeiro, um dispositivo tem toosubscribe muito`$iothub/methods/POST/#`. IoT Hub envia o tópico do método solicitações toohello `$iothub/methods/POST/{method name}/?$rid={request id}`, com um corpo vazio ou JSON válido.

toorespond, dispositivo Olá envia uma mensagem com um JSON válido ou um tópico do corpo vazio toohello `$iothub/methods/res/{status}/?$rid={request id}`, onde **id da solicitação** tem toomatch Olá um na mensagem de solicitação de saudação e **status** tem toobe um número inteiro .

Para obter mais informações, consulte [Guia do desenvolvedor do método direto][lnk-methods].

### <a name="additional-considerations"></a>Considerações adicionais

Como uma consideração final, se você precisar de comportamento de protocolo MQTT toocustomize Olá no lado de nuvem hello, você deve revisar Olá [gateway de protocolo do Azure IoT] [ lnk-azure-protocol-gateway] que permite a você toodeploy de alto desempenho gateway de protocolo personalizado que interage diretamente com o IoT Hub. gateway do protocolo Hello IoT do Azure permite que você toocustomize Olá protocolo tooaccommodate brownfield MQTT implantações de dispositivos ou outros protocolos personalizados. Essa abordagem exige, no entanto, que você execute e opere um gateway de protocolo personalizado.

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre o protocolo MQTT hello, consulte Olá [documentação MQTT][lnk-mqtt-docs].

toolearn mais sobre como planejar sua implantação do IoT Hub, consulte:

* [Catálogo de dispositivos Azure Certified para IoT][lnk-devices]
* [Suporte a protocolos adicionais][lnk-protocols]
* [Comparar com Hubs de Eventos][lnk-compare]
* [Escala, alta disponibilidade e recuperação de desastre][lnk-scaling]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Guia do desenvolvedor do Hub IoT][lnk-devguide]
* [Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
