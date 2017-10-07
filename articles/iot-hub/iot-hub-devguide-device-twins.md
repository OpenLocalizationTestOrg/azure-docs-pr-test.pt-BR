---
title: twins de dispositivo do Azure IoT Hub aaaUnderstand | Microsoft Docs
description: "Guia do desenvolvedor - usar dispositivo twins toosynchronize os dados de estado e a configuração entre os dispositivos e o IoT Hub"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a>Entender e usar dispositivos gêmeos no Hub IoT
## <a name="overview"></a>Visão geral
*Dispositivos gêmeos* são documentos JSON que armazenam informações do estado do dispositivo (metadados, configurações e condições). IoT Hub mantém duas um dispositivo de cada dispositivo que você se conecte tooIoT Hub. Este artigo descreve:

* Olá estrutura de duas de dispositivo Olá: *marcas*, *desejado* e *relatado propriedades*, e
* operações de saudação que aplicativos de dispositivo e de back-end pode executar em twins de dispositivo.

> [!NOTE]
> Atualmente, twins de dispositivo são acessíveis somente de dispositivos que se conectam tooIoT Hub usando o protocolo MQTT hello. Consulte toohello [suporte MQTT] [ lnk-devguide-mqtt] artigo para obter instruções sobre como tooconvert existente dispositivo aplicativo toouse MQTT.
> 
> 

### <a name="when-toouse"></a>Quando toouse
Use os dispositivos gêmeos para:

* Armazenar os metadados específicos do dispositivo na nuvem hello. Por exemplo, Olá local de implantação de uma máquina de vendas.
* Relate informações de estado atual, como recursos disponíveis e condições do aplicativo do dispositivo. Por exemplo, um dispositivo está conectado tooyour IoT hub via celular ou Wi-Fi.
* Sincronize o estado de saudação de fluxos de trabalho de longa duração entre o aplicativo de dispositivo e aplicativo de back-end. Por exemplo, quando Olá solução novamente final Especifica Olá novo tooinstall de versão de firmware e relatórios de aplicativos de dispositivo Olá Olá várias fases do processo de atualização de saudação.
* Consultar os metadados, a configuração ou o estado do seu dispositivo.

Consulte também[orientação de comunicação do dispositivo para nuvem] [ lnk-d2c-guidance] para obter orientação sobre como usar propriedades relatadas, mensagens de dispositivo para nuvem ou carregamento de arquivo.
Consulte também[orientação de comunicação de nuvem para dispositivo] [ lnk-c2d-guidance] para obter orientação sobre como usar as propriedades desejadas, métodos diretos ou mensagens de nuvem para dispositivo.

## <a name="device-twins"></a>Dispositivos gêmeos
Dispositivos gêmeos armazenam informações relacionadas ao dispositivo que:

* Termina de dispositivo e de volta pode usar a configuração e as condições de dispositivo toosynchronize.
* back-end de solução Olá use tooquery e operações de execução longa de destino.

ciclo de vida de saudação de duas um dispositivo é vinculado correspondente toohello [identidade do dispositivo][lnk-identity]. Os dispositivos gêmeos são criados e excluídos implicitamente quando uma nova identidade de dispositivo é criada ou excluída no Hub IoT.

Um dispositivo gêmeo é um documento JSON que inclui:

* **Marcas**. Uma seção do documento JSON Olá Olá back-end solução pode ler e gravar. Marcas não são visíveis toodevice aplicativos.
* **Propriedades desejadas**. Usada junto com a configuração do dispositivo toosynchronize propriedades relatado ou condições. Propriedades desejadas só podem ser definidas pela solução de saudação volta final e podem ser lido pelo aplicativo de dispositivo de saudação. aplicativo de dispositivo Olá também pode ser notificado em tempo real de alterações em Propriedades de saudação desejada.
* **Propriedades reportadas**. Usada junto com a configuração do dispositivo toosynchronize propriedades desejadas ou condições. Propriedades relatadas só pode ser definidas por aplicativo para dispositivo hello e podem ser leitura e consultadas pelo back-end de solução hello.

Além disso, raiz de saudação do documento JSON Olá dispositivo duas contém propriedades somente leitura de saudação de identidade de dispositivo correspondente Olá armazenados em Olá [registro identidade][lnk-identity].

![][img-twin]

saudação de exemplo a seguir mostra uma documento JSON de duas do dispositivo:

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

Na raiz do objeto hello, é Olá propriedades do sistema e objetos de contêiner para `tags` e `reported` e `desired` propriedades. Olá `properties` contêiner contém alguns elementos somente leitura (`$metadata`, `$etag`, e `$version`) descrito no hello [dispositivo duas metadados] [ lnk-twin-metadata] e [ Simultaneidade otimista] [ lnk-concurrency] seções.

### <a name="reported-property-example"></a>Exemplo da propriedade reportada
No exemplo anterior de saudação, duas de dispositivo Olá contém um `batteryLevel` propriedade é relatada pelo aplicativo de dispositivo de saudação. Essa propriedade torna possível tooquery e operar em dispositivos com base no nível de bateria relatado última hello. Outros exemplos incluem hello dispositivo app reporting recursos do dispositivo ou opções de conectividade.

> [!NOTE]
> Propriedades relatadas simplificam cenários onde o back-end de solução hello está interessada em Olá conhecido último valor de uma propriedade. Use [mensagens de dispositivo para nuvem] [ lnk-d2c] se back-end de solução Olá precisa tooprocess telemetria do dispositivo no formulário de saudação de sequências de eventos de marca, como a série temporal.

### <a name="desired-property-example"></a>Exemplo da propriedade desejada
No exemplo anterior de saudação, Olá `telemetryConfig` duas dispositivo desejado e relatadas propriedades são usadas pelo back-end de solução hello e configuração de telemetria de Olá Olá dispositivo aplicativo toosynchronize para este dispositivo. Por exemplo:

1. back-end de solução Olá define a propriedade de saudação desejada com o valor de configuração de saudação desejada. Aqui é parte de saudação do documento hello com o conjunto de propriedades de saudação desejado:
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. aplicativo de dispositivo de saudação é notificado sobre alteração de Olá imediatamente se conectado, ou em Olá primeiro se reconectar. Olá aplicativo de dispositivo reporta configuração Olá atualizado (ou uma condição de erro usando Olá `status` propriedade). Aqui está parte Olá Olá relatado propriedades:
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. back-end de solução Olá pode acompanhar Olá resultados da operação de configuração de saudação em vários dispositivos, por [consultando] [ lnk-query] twins do dispositivo.

> [!NOTE]
> trechos de código anteriores Hello são exemplos, otimizado para legibilidade, de uma maneira tooencode uma configuração de dispositivo e seu status. IoT Hub não impõe um esquema específico para duas de dispositivo de saudação desejado e relatado propriedades em twins de dispositivo de saudação.
> 
> 

Você pode usar operações de execução longa toosynchronize twins como atualizações de firmware. Para obter mais informações sobre como toouse propriedades toosynchronize e rastrear uma operação de longa duração em todos os dispositivos, consulte [uso desejado dispositivos de tooconfigure propriedades][lnk-twin-properties].

## <a name="back-end-operations"></a>Operações de back-end
back-end de solução Olá opera em duas de dispositivo hello usando Olá operações atômicas, expostas por meio de HTTP a seguir:

1. **Recuperar dispositivo gêmeo por id**. Essa operação retorna Olá dispositivo duas documento, inclusive as marcas e desejado, relatado e as propriedades do sistema.
2. **Atualizar parcialmente o dispositivo gêmeo**. Esta operação permite marcas de Olá Olá solução back-end toopartially atualização ou as propriedades desejadas em duas um dispositivo. atualização parcial Olá é expressa como um documento JSON que adiciona ou atualiza qualquer propriedade. Propriedades definidas muito`null` são removidos. Olá exemplo a seguir cria uma nova propriedade desejada com o valor `{"newProperty": "newValue"}`, substitui o valor existente de saudação do `existingProperty` com `"otherNewValue"`e remove `otherOldProperty`. Nenhuma outra alteração é feitas tooexisting desejado propriedades ou marcas:
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. **Substituir propriedades desejadas**. Esta operação habilita Olá solução back-end toocompletely substituir todas as propriedades desejadas existentes e substituir por um novo documento JSON para `properties/desired`.
4. **Substituir marcas**. Esta operação habilita Olá solução back-end toocompletely substituir todas as marcas existentes e substituir por um novo documento JSON para `tags`.
5. **Receba notificações gêmeas**. Esta operação permite toobe de back-end de solução Olá notificado quando duas Olá é modificada. toodo assim, sua solução de IoT precisa de uma rota de toocreate e tooset Olá fonte de dados igual muito*twinChangeEvents*. Por padrão, nenhuma notificação gêmea é enviada, ou seja, nenhuma dessas rotas existe previamente. Se a taxa de saudação de alteração é muito alta ou por outros motivos, como falhas internas, Olá IoT Hub pode enviar apenas uma notificação que contém todas as alterações. Portanto, se seu aplicativo precisar de auditoria e registro em log confiáveis de todos os estados intermediários, ainda será recomendável que você use mensagens D2C. mensagem de notificação de duas Olá inclui propriedades e corpo.

    - Propriedades

    | Nome | Valor |
    | --- | --- |
    $content-type | aplicativo/json |
    $iothub-enqueuedtime |  Hora de envio da notificação de saudação |
    $iothub-message-source | twinChangeEvents |
    $content-encoding | utf-8 |
    deviceId | ID do dispositivo Olá |
    hubName | Nome do Hub IoT |
    operationTimestamp | Carimbo de data/hora [ISO8601] da operação |
    iothub-message-schema | deviceLifecycleNotification |
    opType | "replaceTwin" ou "updateTwin" |

    Propriedades do sistema de mensagens são prefixadas com hello `'$'` símbolo.

    - Corpo
        
    Esta seção inclui todas as alterações de duas Olá em um formato JSON. Ele usa o mesmo formato de saudação como um patch, com a diferença de saudação que ele pode conter todas as seções de duas: marcas, properties.reported, properties.desired e que contém elementos hello "$metadata". Por exemplo,
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

Todos os Olá anterior suporte a operações [simultaneidade otimista] [ lnk-concurrency] e exigem Olá **ServiceConnect** permissão, conforme definido no hello [segurança ] [ lnk-security] artigo.

Além disso, operações toothese, solução de saudação fazer final pode:

* Consultar twins de dispositivo hello usando Olá tipo SQL [linguagem de consulta de IoT Hub][lnk-query].
* Executar operações em conjuntos grandes de gêmeos de dispositivo usando [trabalhos][lnk-jobs].

## <a name="device-operations"></a>Operações de dispositivo
aplicativo de dispositivo Olá opera em duas de dispositivo hello usando Olá operações atômicas a seguir:

1. **Recuperar dispositivo gêmeo**. Essa operação retorna um documento de duas dispositivo hello (incluindo marcas e desejado, relatado e propriedades do sistema) para Olá dispositivo conectado no momento.
2. **Atualizar parcialmente as propriedades reportadas**. Esta operação habilita Olá parcial atualização de saudação relatado propriedades de dispositivo de saudação conectado no momento. Saudação de usa essa operação Atualizar JSON mesmo formato que Olá solução back usos para uma atualização parcial de propriedades desejadas.
3. **Observar as propriedades desejadas**. dispositivo conectado no momento da saudação pode escolher toobe notificado das propriedades de toohello desejado atualizações quando eles ocorrem. Olá receberá Olá mesmo formulário de atualização (substituição parcial ou completa) executado pelo back-end de solução hello.

Todas as operações anteriores de Olá exigem Olá **DeviceConnect** permissão, conforme definido no hello [segurança] [ lnk-security] artigo.

Olá [dispositivo IoT do Azure SDKs] [ lnk-sdks] tornar fácil toouse Olá anterior de operações de várias plataformas e idiomas. Mais informações sobre detalhes de saudação de primitivos de IoT Hub para sincronização de propriedades desejadas podem ser encontradas em [fluxo de reconexão do dispositivo][lnk-reconnection].

> [!NOTE]
> Atualmente, twins de dispositivo são acessíveis somente de dispositivos que se conectam tooIoT Hub usando o protocolo MQTT hello.
> 
> 

## <a name="reference-topics"></a>Tópicos de referência:
Hello seguinte referência tópicos fornecem mais informações sobre o controle hub de IoT tooyour de acesso.

## <a name="tags-and-properties-format"></a>Formato de marcas e propriedades
Marcas, propriedades desejadas e relatadas são objetos JSON com hello restrições a seguir:

* Todas as chaves em objetos JSON são cadeias de caracteres UNICODE UTF-8 de 64 bytes que diferenciam maiúsculas de minúsculas. Os caracteres permitidos excluir caracteres de controle UNICODE (segmentos C0 e C1) e `'.'`, `' '` e `'$'`.
* Todos os valores de objetos JSON podem ser dos seguintes tipos de JSON de saudação: booleano, número, cadeia de caracteres, objeto. Não há permissão para matrizes.
* Todos os objetos JSON em marcações, propriedades desejadas e reportadas podem ter uma profundidade máxima de 5. Por exemplo, Olá após o objeto é válido:

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* Todos os valores de cadeia de caracteres podem ter no máximo 512 bytes de comprimento.

## <a name="device-twin-size"></a>Tamanho do dispositivo gêmeo
IoT Hub impõe um limite de tamanho de 8KB em valores de saudação do `tags`, `properties/desired`, e `properties/reported`, exceto elementos somente leitura.
Olá tamanho é calculado pela contagem de todos os caracteres UNICODE de excluindo controlam caracteres (segmentos C0 e C1) e o espaço `' '` quando ele for exibido fora de uma constante de cadeia de caracteres.
IoT Hub rejeitada com um erro de todas as operações que deve aumentar o tamanho de saudação desses documentos acima do limite de saudação.

## <a name="device-twin-metadata"></a>Metadados do dispositivo gêmeo
IoT Hub mantém Olá carimbo de hora da última atualização Olá para cada objeto JSON em duas dispositivo desejado e relatado propriedades. Olá carimbos de hora estão em UTC e codificado em Olá [ISO8601] formato `YYYY-MM-DDTHH:MM:SS.mmmZ`.
Por exemplo:

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

Essa informação é mantida em todas as atualizações de toopreserve (folhas de saudação não apenas da saudação estrutura JSON) níveis que remover chaves de objeto.

## <a name="optimistic-concurrency"></a>Simultaneidade otimista
Marcas, propriedades desejadas e reportadas oferecem suporte à simultaneidade otimista.
Marcas de tem uma ETag, como por [RFC7232], que representa a representação da marca hello. Você pode usar ETags em operações de atualização condicional de consistência de tooensure Olá solução back-end.

Duas dispositivo desejado e relatado propriedades não tem ETags, mas tem um `$version` valor garantia toobe incremental. Da mesma forma tooan ETag, versão Olá pode ser usado por Olá atualizando consistência de tooenforce parte de atualizações. Por exemplo, um aplicativo de dispositivo para um relatado propriedade ou hello solução back-end para a propriedade desejada.

Versões também são úteis quando um agente observando (como o aplicativo de dispositivo Olá observando propriedades Olá desejado) necessário reconciliar corridas entre o resultado de saudação de uma operação de recuperação e uma notificação de atualização. Olá seção [fluxo de reconexão do dispositivo] [ lnk-reconnection] fornece mais informações.

## <a name="device-reconnection-flow"></a>Fluxo de reconexão do dispositivo
O Hub IoT não preserva notificações de atualização de propriedades desejadas para dispositivos desconectados. Ele segue que um dispositivo que está se conectando deve recuperar o documento de propriedades desejada completo de Olá, no toosubscribing de adição para notificações de atualização. Considerando a possibilidade de saudação de corridas entre notificações de atualização e de recuperação completa, deve ser garantida Olá fluxo a seguir:

1. Aplicativo de dispositivo se conecta tooan IoT hub.
2. O aplicativo de dispositivo se inscreve para as notificações de atualização de propriedades desejadas .
3. Aplicativo de dispositivo recupera o documento completo de saudação para propriedades desejadas.

aplicativo de dispositivo Olá pode ignorar todas as notificações com `$version` menor ou igual a versão Olá Olá documento de recuperados completo. Essa abordagem é possível porque o Hub IoT garante que as versões sempre aumentam.

> [!NOTE]
> Essa lógica já foi implementada no hello [dispositivo IoT do Azure SDKs][lnk-sdks]. Essa descrição é útil apenas se Olá aplicativo de dispositivo não é possível usar qualquer um dos SDKs de dispositivo de IoT do Azure e deve programar diretamente a interface MQTT Olá.
> 
> 

## <a name="additional-reference-material"></a>Material de referência adicional
Outros tópicos de referência Olá guia do desenvolvedor de IoT Hub incluem:

* Olá [pontos de extremidade de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos de extremidade que expõe a cada hub IoT para operações de tempo de execução e gerenciamento.
* Olá [limitação e cotas] [ lnk-quotas] descreve cotas Olá que se aplicam a toohello serviço de IoT Hub e Olá limitação tooexpect de comportamento quando você usar o serviço de saudação.
* Olá [SDKs de dispositivo e serviço de Azure IoT] [ lnk-sdks] listas de artigo Olá vários SDKs de idioma, você pode usar ao desenvolver aplicativos do dispositivo e o serviço que interagem com o IoT Hub.
* Olá [linguagem de consulta de IoT Hub para twins do dispositivo, trabalhos e roteamento de mensagens] [ lnk-query] descreve Olá linguagem de consulta de IoT Hub, você pode usar informações de tooretrieve de IoT Hub sobre seus trabalhos e twins do dispositivo .
* Olá [suporte de IoT Hub MQTT] [ lnk-devguide-mqtt] artigo fornece mais informações sobre o suporte de IoT Hub de protocolo de MQTT saudação.

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu sobre twins do dispositivo, você pode estar interessado em Olá tópicos do guia de desenvolvedor de IoT Hub a seguir:

* [Invocar um método direto em um dispositivo][lnk-methods]
* [Agendar trabalhos em vários dispositivos][lnk-jobs]

Se você quiser tootry alguns dos conceitos de saudação descritos neste artigo, você pode estar interessado em Olá tutoriais de IoT Hub a seguir:

* [Como toouse Olá duas do dispositivo][lnk-twin-tutorial]
* [Como o dispositivo toouse macros propriedades][lnk-twin-properties]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
