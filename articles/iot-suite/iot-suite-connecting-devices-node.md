---
title: aaaConnect um dispositivo usando o Node. js | Microsoft Docs
description: "Descreve como tooconnect toohello um dispositivo do Azure IoT Suite pré-configurados de solução de monitoramento remota usando um aplicativo escrito em Node. js."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: fc50a33f-9fb9-42d7-b1b8-eb5cff19335e
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 80bf2b70f15f539bfce4f135d533c46dd2b3f5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a>Conecte-se a sua solução pré-configurada (Node.js) de monitoramento remoto de toohello de dispositivo
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a>Criar uma solução de exemplo do Node.js

Certifique-se de que o Node.js versão 0.11.5 ou posterior esteja instalado no computador de desenvolvimento. Você pode executar `node --version` na versão de Olá Olá linha de comando toocheck.

1. Crie uma pasta chamada **RemoteMonitoring** no computador de desenvolvimento. Navegue toothis pasta em seu ambiente de linha de comando.

1. Saudação de execução a seguir comandos toodownload e instalar pacotes de saudação é necessário que o aplicativo de exemplo hello toocomplete:

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Em Olá **RemoteMonitoring** pasta, crie um arquivo chamado **remote_monitoring.js**. Abra esse arquivo em um editor de texto.

1. Em Olá **remote_monitoring.js** de arquivo, adicione o seguinte Olá `require` instruções:

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. Adicionar Olá declarações de variáveis a seguir após Olá `require` instruções. Substituir valores de espaço reservado de saudação [Id do dispositivo] e [chave do dispositivo] com valores anotados para seu dispositivo no painel solução de monitoramento remoto hello. Use Olá Hostname de Hub IoT do hello solução painel tooreplace [nome do hub IOT]. Por exemplo, se o nome de host do Hub IoT for **contoso.azure-devices.net**, substitua [Nome do HubIoT] por **contoso**:

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. Adicione Olá toodefine variáveis a seguir alguns dados de telemetria base:

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. Adicione Olá resultados de operação de tooprint de função auxiliar a seguir:

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. Adicione Olá auxiliar função toouse toorandomize Olá telemetria valores a seguir:

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. Adicionar Olá após a definição de saudação **DeviceInfo** envia de dispositivo de saudação do objeto durante a inicialização:

    ```nodejs
    var deviceMetaData = {
        'ObjectType': 'DeviceInfo',
        'IsSimulatedDevice': 0,
        'Version': '1.0',
        'DeviceProperties': {
            'DeviceID': deviceId,
            'HubEnabledState': 1
        }
    };
    ```

1. Adicione Olá seguinte definição para duas de dispositivo Olá relatado valores. Essa definição inclui descrições dos métodos de direto Olá Olá dispositivo oferece suporte a:

    ```nodejs
    var reportedProperties = {
        "Device": {
            "DeviceState": "normal",
            "Location": {
                "Latitude": 47.642877,
                "Longitude": -122.125497
            }
        },
        "Config": {
            "TemperatureMeanValue": 56.7,
            "TelemetryInterval": 45
        },
        "System": {
            "Manufacturer": "Contoso Inc.",
            "FirmwareVersion": "2.22",
            "InstalledRAM": "8 MB",
            "ModelNumber": "DB-14",
            "Platform": "Plat 9.75",
            "Processor": "i3-9",
            "SerialNumber": "SER99"
        },
        "Location": {
            "Latitude": 47.642877,
            "Longitude": -122.125497
        },
        "SupportedMethods": {
            "Reboot": "Reboot hello device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file"
        },
    }
    ```

1. Adicionar Olá Olá de toohandle de função a seguir **reinicializar** direcionar a chamada de método:

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete hello response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. Adicionar Olá Olá de toohandle de função a seguir **InitiateFirmwareUpdate** direcionar a chamada de método. Esse método direto usa um local de saudação do parâmetro toospecify de toodownload de imagem de firmware de saudação e inicia Olá atualizar o firmware no dispositivo Olá assíncrona:

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete hello response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here tooperform hello firmware update asynchronously
    }
    ```

1. Adicione Olá código toocreate uma instância do cliente a seguir:

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Adicione Olá código a seguir:

    * Abrir conexão hello.
    * Enviar Olá **DeviceInfo** objeto.
    * Configure um manipulador para as propriedades desejadas.
    * Envie as propriedades relatadas.
    * Registre manipuladores para métodos diretos hello.
    * Comece a enviar a telemetria.

    ```nodejs
    client.open(function (err) {
        if (err) {
            printErrorFor('open')(err);
        } else {
            console.log('Sending device metadata:\n' + JSON.stringify(deviceMetaData));
            client.sendEvent(new Message(JSON.stringify(deviceMetaData)), printErrorFor('send metadata'));

            // Create device twin
            client.getTwin(function(err, twin) {
                if (err) {
                    console.error('Could not get device twin');
                } else {
                    console.log('Device twin created');

                    twin.on('properties.desired', function(delta) {
                        console.log('Received new desired properties:');
                        console.log(JSON.stringify(delta));
                    });

                    // Send reported properties
                    twin.properties.reported.update(reportedProperties, function(err) {
                        if (err) throw err;
                        console.log('twin state reported');
                    });

                    // Register handlers for direct methods
                    client.onDeviceMethod('Reboot', onReboot);
                    client.onDeviceMethod('InitiateFirmwareUpdate', onInitiateFirmwareUpdate);
                }
            });

            // Start sending telemetry
            var sendInterval = setInterval(function () {
                temperature += generateRandomIncrement();
                externalTemperature += generateRandomIncrement();
                humidity += generateRandomIncrement();

                var data = JSON.stringify({
                    'DeviceID': deviceId,
                    'Temperature': temperature,
                    'Humidity': humidity,
                    'ExternalTemperature': externalTemperature
                });

                console.log('Sending device event data:\n' + data);
                client.sendEvent(new Message(data), printErrorFor('send event'));
            }, 5000);

            client.on('error', function (err) {
                printErrorFor('client')(err);
                if (sendInterval) clearInterval(sendInterval);
                client.close(printErrorFor('client.close'));
            });
        }
    });
    ```

1. Salvar Olá alterações toohello **remote_monitoring.js** arquivo.

1. Olá executar comandos em um aplicativo de exemplo de saudação do prompt de comando toolaunch a seguir:
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
