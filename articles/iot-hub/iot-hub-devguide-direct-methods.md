---
title: "métodos de direcionar aaaUnderstand Azure IoT Hub | Microsoft Docs"
description: "Guia do desenvolvedor - use métodos diretos tooinvoke código em seus dispositivos de um aplicativo de serviço."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a>Entender e chamar métodos diretos do Hub IoT
## <a name="overview"></a>Visão geral
IoT Hub oferece métodos diretos de tooinvoke de capacidade nos dispositivos da nuvem de saudação. Métodos diretos representam uma interação de solicitação-resposta com um tooan semelhante dispositivo HTTP chamadas em que elas foram bem-sucedidas ou falham imediatamente (após um tempo limite especificado pelo usuário). Isso é útil para cenários onde Olá ação imediata é diferente dependendo se o dispositivo de saudação foi capaz de toorespond, como o envio de um dispositivo do SMS wake-up tooa se um dispositivo estiver offline (sendo mais caro do que uma chamada de método SMS).

Cada método de dispositivo tem como alvo um único dispositivo. [Trabalhos] [ lnk-devguide-jobs] fornecem uma maneira tooinvoke métodos diretos em vários dispositivos e agendar a invocação de método para dispositivos desconectados.

Qualquer pessoa com permissões de **conectar serviço** no Hub IoT pode invocar um método em um dispositivo.

### <a name="when-toouse"></a>Quando toouse
Métodos diretos seguem um padrão de solicitação-resposta e destinam-se para as comunicações que exigem a confirmação imediata de seus resultados, controle geralmente interativo do dispositivo hello, por exemplo tooturn em um ventilador.

Consulte também[orientação de comunicação de nuvem para dispositivo] [ lnk-c2d-guidance] em caso de dúvida, entre usando as propriedades desejadas, direcionar métodos ou mensagens de nuvem para dispositivo.

## <a name="method-lifecycle"></a>Ciclo de vida do método
Métodos diretos são implementados no dispositivo hello e podem exigir a zero ou mais entradas no toocorrectly de carga do método hello instanciar. Você invoca um método direto por meio de um URI voltado para serviços (`{iot hub}/twins/{device id}/methods/`). Um dispositivo recebe métodos diretos por meio de um tópico MQTT específico ao dispositivo (`$iothub/methods/POST/{method name}/`). Podemos pode oferecer suporte a métodos diretos em protocolos de rede de lado do dispositivo adicionais no futuro de saudação.

> [!NOTE]
> Quando você invoca um método em um dispositivo, valores e nomes de propriedade só podem conter US-ASCII imprimível alfanumérico, exceto qualquer em Olá conjunto a seguir: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

Direcionar métodos são síncronos e o êxito ou falha após o período de tempo limite da saudação (padrão: 30 segundos, definível pelo backup too3600 segundos). Métodos diretos são úteis em cenários interativos onde deseja que um dispositivo tooact se e somente se o dispositivo de hello está online e recebendo comandos, como ativar a luz de um telefone. Nesses cenários, você deseja toosee uma falha ou sucesso imediato para que serviço de nuvem Olá possa agir no resultado de saudação assim que possível. dispositivo Olá pode retornar alguns corpo da mensagem como resultado do método hello, mas ele não é necessário para Olá método toodo para. Não há nenhuma garantia quanto à ordenação ou semântica de simultaneidade nas chamadas de método.

Método direto são somente para HTTP do lado de nuvem hello e somente MQTT do lado do dispositivo de saudação.

carga de saudação para método solicitações e respostas é um documento JSON para cima too8KB.

## <a name="reference-topics"></a>Tópicos de referência:
Olá seguintes tópicos de referência fornecem mais informações sobre como usar métodos diretos.

## <a name="invoke-a-direct-method-from-a-back-end-app"></a>Invocar um método direto de um aplicativo back-end
### <a name="method-invocation"></a>Invocação de método
Invocações de método direto em um dispositivo são chamadas HTTP, que compreendem:

* Olá *URI* toohello específico de dispositivo (`{iot hub}/twins/{device id}/methods/`)
* Olá POST *método*
* *Cabeçalhos* que contêm autorização hello, ID, o tipo de conteúdo e a codificação do conteúdo de solicitação
* JSON transparente *corpo* em Olá formato a seguir:

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

Tempo limite em segundos. Se o tempo limite não for definida, o padrão é too30 segundos.

### <a name="response"></a>Resposta
aplicativo de back-end Olá recebe uma resposta que consiste em:

* *Código de status HTTP*, que é usado para erros provenientes do hello IoT Hub, inclusive um erro 404 para dispositivos que não estão conectados
* *Cabeçalhos* que contêm Olá ETag, ID, o tipo de conteúdo e a codificação do conteúdo de solicitação
* JSON *corpo* em Olá formato a seguir:

```
{
    "status" : 201,
    "payload" : {...}
}
```

   Ambos `status` e `body` são fornecidos pelo dispositivo hello e usado toorespond com código de status do dispositivo hello e/ou descrição.

## <a name="handle-a-direct-method-on-a-device"></a>Tratar um método direto em um dispositivo
### <a name="method-invocation"></a>Invocação de método
Dispositivos recebem solicitações de método direto no tópico MQTT hello:`$iothub/methods/POST/{method name}/?$rid={request id}`

corpo da saudação qual dispositivo Olá recebe é em Olá formato a seguir:

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

As solicitações de método são QoS 0.

### <a name="response"></a>Resposta
dispositivo Olá envia respostas muito`$iothub/methods/res/{status}/?$rid={request id}`, onde:

* Olá `status` propriedade é status fornecido pelo dispositivo de saudação de execução do método.
* Olá `$rid` propriedade é Olá solicitação ID de invocação de método hello recebida do IoT Hub.

corpo de saudação é definido pelo dispositivo hello e pode ser qualquer status.

## <a name="additional-reference-material"></a>Material de referência adicional
Outros tópicos de referência Olá guia do desenvolvedor de IoT Hub incluem:

* [Pontos de extremidade de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos de extremidade que expõe a cada hub IoT para operações de tempo de execução e gerenciamento.
* [Limitação e cotas] [ lnk-quotas] descreve cotas Olá que se aplicam a toohello serviço de IoT Hub e Olá limitação tooexpect de comportamento quando você usar o serviço de saudação.
* [SDKs do Azure de dispositivo e serviço IoT] [ lnk-sdks] listas Olá SDKs, você pode usar ao desenvolver aplicativos do dispositivo e o serviço que interagem com o IoT Hub de vários idiomas.
* [Linguagem de consulta de IoT Hub para twins do dispositivo, trabalhos e roteamento de mensagens] [ lnk-query] descreve Olá linguagem de consulta de IoT Hub, você pode usar informações de tooretrieve de IoT Hub sobre seus trabalhos e twins do dispositivo.
* [Suporte de IoT Hub MQTT] [ lnk-devguide-mqtt] fornece mais informações sobre o suporte de IoT Hub para o protocolo MQTT hello.

## <a name="next-steps"></a>Próximas etapas
Agora, você aprendeu como métodos de toouse direto, você pode estar interessado em Olá tópico de guia do desenvolvedor de IoT Hub a seguir:

* [Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]

Se você quiser tootry alguns dos conceitos de saudação descritos neste artigo, você pode estar interessado em Olá seguindo o tutorial de IoT Hub:

* [Usar métodos diretos][lnk-methods-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
