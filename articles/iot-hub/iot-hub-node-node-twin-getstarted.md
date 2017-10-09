---
title: "aaaGet iniciado com twins de dispositivo do Azure IoT Hub (nó) | Microsoft Docs"
description: "Como toouse Azure IoT Hub dispositivo twins tooadd marcas e, em seguida, use uma consulta de IoT Hub. Use hello Azure IoT SDKs para aplicativo de dispositivo simulado Node. js tooimplement hello e um aplicativo de serviço que adiciona marcas hello e executa Olá consulta de IoT Hub."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a>Introdução aos dispositivos gêmeos (Node)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

No final de saudação deste tutorial, você terá dois aplicativos de console Node. js:

* **AddTagsAndQuery.js**, um aplicativo de back-end Node.js que adiciona marcas e consultas aos dispositivos gêmeos.
* **TwinSimulatedDevice.js**, um aplicativo Node. js que simula um dispositivo que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente e sua condição de conectividade de relatórios.

> [!NOTE]
> artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.
> 
> 

toocomplete este tutorial, você precisa seguir hello:

* Node.js versão 0.10.x ou posterior.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Criar aplicativo de serviço Olá
Nesta seção, você cria um aplicativo de console Node. js que adiciona associada duas de dispositivo local metadados toohello **myDeviceId**. Em seguida, consultas twins de dispositivo Olá armazenadas no hub IoT de saudação selecionando Olá dispositivos localizados em Olá nos e hello, em seguida, aqueles que estão se comunicando uma conexão de celular.

1. Crie uma nova pasta vazia denominada **addtagsandqueryapp**. Em Olá **addtagsandqueryapp** pasta, crie um novo arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **addtagsandqueryapp** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote:
   
    ```
    npm install azure-iothub --save
    ```
3. Usando um editor de texto, crie um novo **AddTagsAndQuery.js** arquivo hello **addtagsandqueryapp** pasta.
4. Adicionar Olá toohello de código a seguir **AddTagsAndQuery.js** de arquivo e substituir Olá **{string de conexão de hub iot}** espaço reservado com hello cadeia de caracteres de conexão de IoT Hub copiadas quando você criar o hub:
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    Olá **registro** objeto expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do serviço de saudação. código anterior Olá primeiro inicializa Olá **registro** do objeto, em seguida, recupera Olá duas de dispositivo para **myDeviceId**e finalmente atualiza as marcas com informações de localização de saudação desejada.
   
    Após Olá atualizar Olá marcas-Olá chamadas **queryTwins** função.
5. Adicionar Olá após código final Olá **AddTagsAndQuery.js** tooimplement Olá **queryTwins** função:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    código anterior Olá executa duas consultas: Olá primeiro seleciona apenas twins de dispositivo de saudação de dispositivos localizados em Olá **Redmond43** fábrica Olá segundo refina Olá consulta tooselect somente Olá dispositivos e também são conectados por meio rede de celular.
   
    Observe que Olá o código anterior, quando ele cria Olá **consulta** de objeto, especifica um número máximo de documentos retornados. Olá **consulta** objeto contém um **hasMoreResults** propriedade booleana que você pode usar o hello tooinvoke **nextAsTwin** métodos tooretrieve todos os resultados de várias vezes. Um método chamado **next** está disponível para os resultados que não são de dispositivos gêmeos, por exemplo, resultados de consultas de agregação.
6. Execute o aplicativo hello com:
   
        node AddTagsAndQuery.js
   
    Você deve ver um dispositivo nos resultados de Olá Olá consulta pedindo para todos os dispositivos localizados no **Redmond43** e nenhuma consulta Olá que restringe Olá resultados toodevices que usam uma rede de celular.
   
    ![][1]

Na próxima seção, Olá você criar um aplicativo de dispositivo com informações de conectividade de saudação e resultado da consulta de saudação na seção anterior Olá Olá a alterações.

## <a name="create-hello-device-app"></a>Criar aplicativo de dispositivo Olá
Nesta seção, você cria um aplicativo de console Node. js que conecta o hub tooyour como **myDeviceId**e, em seguida, as atualizações duas seu dispositivo do relatado informações Olá toocontain das propriedades que ele está conectado usando uma rede de celular.

> [!NOTE]
> Neste momento, twins de dispositivo são acessíveis somente de dispositivos que se conectam tooIoT Hub usando o protocolo MQTT hello. Consulte toohello [suporte MQTT] [ lnk-devguide-mqtt] artigo para obter instruções sobre como tooconvert existente dispositivo aplicativo toouse MQTT.
> 
> 

1. Crie uma nova pasta vazia denominada **reportconnectivity**. Em Olá **reportconnectivity** pasta, crie um novo arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **reportconnectivity** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure**, e **azure iot-dispositivo mqtt** pacote :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Usando um editor de texto, crie um novo **ReportConnectivity.js** arquivo hello **reportconnectivity** pasta.
4. Adicionar Olá toohello de código a seguir **ReportConnectivity.js** de arquivo e substituir Olá **{string de conexão do dispositivo}** espaço reservado com cadeia de conexão do dispositivo Olá copiadas quando você criou Olá **myDeviceId** identidade do dispositivo:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    Olá **cliente** objeto expõe todos os métodos de saudação exigem toointeract com twins de dispositivo do dispositivo hello. Olá código anterior, depois que ele inicializa Olá **cliente** objeto recupera Olá duas de dispositivo para **myDeviceId** e atualiza sua propriedade relatada com informações de conectividade de saudação.
5. Executar o aplicativo de dispositivo Olá
   
        node ReportConnectivity.js
   
    Você verá uma mensagem de saudação `twin state reported`.
6. Agora que hello dispositivo relatado suas informações de conectividade, ele aparecerá em ambas as consultas. Vá em Olá **addtagsandqueryapp** Olá pasta e executar consultas novamente:
   
        node AddTagsAndQuery.js
   
    Desta vez, **myDeviceId** deve aparecer em ambos os resultados da consulta.
   
    ![][3]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello. Você adicionou o metadados do dispositivo como marcas de um aplicativo de back-end e gravou informações de conectividade do dispositivo do dispositivo simulado aplicativo tooreport em duas de dispositivo de saudação. Você também aprendeu como tooquery essas informações usando a linguagem de consulta do tipo SQL IoT Hub hello.

Saudação de uso toolearn de recursos a seguir como a:

* Enviar telemetria de dispositivos com hello [começar com o IoT Hub] [ lnk-iothub-getstarted] tutorial,
* Configurar dispositivos com propriedades desejadas de duas dispositivo Olá [uso desejado dispositivos de tooconfigure propriedades] [ lnk-twin-how-to-configure] tutorial,
* controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário), com hello [usar métodos diretos] [ lnk-methods-tutorial] tutorial.

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
