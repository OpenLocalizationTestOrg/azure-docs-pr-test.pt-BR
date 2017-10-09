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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="00bad-103">Conecte-se a sua solução pré-configurada (Node.js) de monitoramento remoto de toohello de dispositivo</span><span class="sxs-lookup"><span data-stu-id="00bad-103">Connect your device toohello remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="00bad-104">Criar uma solução de exemplo do Node.js</span><span class="sxs-lookup"><span data-stu-id="00bad-104">Create a node.js sample solution</span></span>

<span data-ttu-id="00bad-105">Certifique-se de que o Node.js versão 0.11.5 ou posterior esteja instalado no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="00bad-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="00bad-106">Você pode executar `node --version` na versão de Olá Olá linha de comando toocheck.</span><span class="sxs-lookup"><span data-stu-id="00bad-106">You can run `node --version` at hello command line toocheck hello version.</span></span>

1. <span data-ttu-id="00bad-107">Crie uma pasta chamada **RemoteMonitoring** no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="00bad-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="00bad-108">Navegue toothis pasta em seu ambiente de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="00bad-108">Navigate toothis folder in your command-line environment.</span></span>

1. <span data-ttu-id="00bad-109">Saudação de execução a seguir comandos toodownload e instalar pacotes de saudação é necessário que o aplicativo de exemplo hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="00bad-109">Run hello following commands toodownload and install hello packages you need toocomplete hello sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="00bad-110">Em Olá **RemoteMonitoring** pasta, crie um arquivo chamado **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="00bad-110">In hello **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="00bad-111">Abra esse arquivo em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="00bad-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="00bad-112">Em Olá **remote_monitoring.js** de arquivo, adicione o seguinte Olá `require` instruções:</span><span class="sxs-lookup"><span data-stu-id="00bad-112">In hello **remote_monitoring.js** file, add hello following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="00bad-113">Adicionar Olá declarações de variáveis a seguir após Olá `require` instruções.</span><span class="sxs-lookup"><span data-stu-id="00bad-113">Add hello following variable declarations after hello `require` statements.</span></span> <span data-ttu-id="00bad-114">Substituir valores de espaço reservado de saudação [Id do dispositivo] e [chave do dispositivo] com valores anotados para seu dispositivo no painel solução de monitoramento remoto hello.</span><span class="sxs-lookup"><span data-stu-id="00bad-114">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="00bad-115">Use Olá Hostname de Hub IoT do hello solução painel tooreplace [nome do hub IOT].</span><span class="sxs-lookup"><span data-stu-id="00bad-115">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="00bad-116">Por exemplo, se o nome de host do Hub IoT for **contoso.azure-devices.net**, substitua [Nome do HubIoT] por **contoso**:</span><span class="sxs-lookup"><span data-stu-id="00bad-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="00bad-117">Adicione Olá toodefine variáveis a seguir alguns dados de telemetria base:</span><span class="sxs-lookup"><span data-stu-id="00bad-117">Add hello following variables toodefine some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="00bad-118">Adicione Olá resultados de operação de tooprint de função auxiliar a seguir:</span><span class="sxs-lookup"><span data-stu-id="00bad-118">Add hello following helper function tooprint operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="00bad-119">Adicione Olá auxiliar função toouse toorandomize Olá telemetria valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="00bad-119">Add hello following helper function toouse toorandomize hello telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="00bad-120">Adicionar Olá após a definição de saudação **DeviceInfo** envia de dispositivo de saudação do objeto durante a inicialização:</span><span class="sxs-lookup"><span data-stu-id="00bad-120">Add hello following definition for hello **DeviceInfo** object hello device sends on startup:</span></span>

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

1. <span data-ttu-id="00bad-121">Adicione Olá seguinte definição para duas de dispositivo Olá relatado valores.</span><span class="sxs-lookup"><span data-stu-id="00bad-121">Add hello following definition for hello device twin reported values.</span></span> <span data-ttu-id="00bad-122">Essa definição inclui descrições dos métodos de direto Olá Olá dispositivo oferece suporte a:</span><span class="sxs-lookup"><span data-stu-id="00bad-122">This definition includes descriptions of hello direct methods hello device supports:</span></span>

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

1. <span data-ttu-id="00bad-123">Adicionar Olá Olá de toohandle de função a seguir **reinicializar** direcionar a chamada de método:</span><span class="sxs-lookup"><span data-stu-id="00bad-123">Add hello following function toohandle hello **Reboot** direct method call:</span></span>

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

1. <span data-ttu-id="00bad-124">Adicionar Olá Olá de toohandle de função a seguir **InitiateFirmwareUpdate** direcionar a chamada de método.</span><span class="sxs-lookup"><span data-stu-id="00bad-124">Add hello following function toohandle hello **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="00bad-125">Esse método direto usa um local de saudação do parâmetro toospecify de toodownload de imagem de firmware de saudação e inicia Olá atualizar o firmware no dispositivo Olá assíncrona:</span><span class="sxs-lookup"><span data-stu-id="00bad-125">This direct method uses a parameter toospecify hello location of hello firmware image toodownload, and initiates hello firmware update on hello device asynchronously:</span></span>

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

1. <span data-ttu-id="00bad-126">Adicione Olá código toocreate uma instância do cliente a seguir:</span><span class="sxs-lookup"><span data-stu-id="00bad-126">Add hello following code toocreate a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="00bad-127">Adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="00bad-127">Add hello following code to:</span></span>

    * <span data-ttu-id="00bad-128">Abrir conexão hello.</span><span class="sxs-lookup"><span data-stu-id="00bad-128">Open hello connection.</span></span>
    * <span data-ttu-id="00bad-129">Enviar Olá **DeviceInfo** objeto.</span><span class="sxs-lookup"><span data-stu-id="00bad-129">Send hello **DeviceInfo** object.</span></span>
    * <span data-ttu-id="00bad-130">Configure um manipulador para as propriedades desejadas.</span><span class="sxs-lookup"><span data-stu-id="00bad-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="00bad-131">Envie as propriedades relatadas.</span><span class="sxs-lookup"><span data-stu-id="00bad-131">Send reported properties.</span></span>
    * <span data-ttu-id="00bad-132">Registre manipuladores para métodos diretos hello.</span><span class="sxs-lookup"><span data-stu-id="00bad-132">Register handlers for hello direct methods.</span></span>
    * <span data-ttu-id="00bad-133">Comece a enviar a telemetria.</span><span class="sxs-lookup"><span data-stu-id="00bad-133">Start sending telemetry.</span></span>

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

1. <span data-ttu-id="00bad-134">Salvar Olá alterações toohello **remote_monitoring.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="00bad-134">Save hello changes toohello **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="00bad-135">Olá executar comandos em um aplicativo de exemplo de saudação do prompt de comando toolaunch a seguir:</span><span class="sxs-lookup"><span data-stu-id="00bad-135">Run hello following command at a command prompt toolaunch hello sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
