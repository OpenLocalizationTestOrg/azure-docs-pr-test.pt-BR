---
title: Conectar um dispositivo usando o Node.js | Microsoft Docs
description: "Descreve como conectar um dispositivo à solução pré-configurada de monitoramento remoto do Azure IoT Suite usando um aplicativo escrito em Node.js."
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
ms.openlocfilehash: 6459b6196eb7f4a083b67e5a421bcc0d51d39e5c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="95361-103">Conectar seu dispositivo à solução pré-configurada de monitoramento remoto (Node.js)</span><span class="sxs-lookup"><span data-stu-id="95361-103">Connect your device to the remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="95361-104">Criar uma solução de exemplo do Node.js</span><span class="sxs-lookup"><span data-stu-id="95361-104">Create a node.js sample solution</span></span>

<span data-ttu-id="95361-105">Certifique-se de que o Node.js versão 0.11.5 ou posterior esteja instalado no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="95361-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="95361-106">Você pode executar `node --version` na linha de comando para verificar a versão.</span><span class="sxs-lookup"><span data-stu-id="95361-106">You can run `node --version` at the command line to check the version.</span></span>

1. <span data-ttu-id="95361-107">Crie uma pasta chamada **RemoteMonitoring** no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="95361-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="95361-108">Navegue até essa pasta no ambiente de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="95361-108">Navigate to this folder in your command-line environment.</span></span>

1. <span data-ttu-id="95361-109">Execute os seguintes comandos para baixar e instalar os pacotes de que você precisa para executar o aplicativo de exemplo:</span><span class="sxs-lookup"><span data-stu-id="95361-109">Run the following commands to download and install the packages you need to complete the sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="95361-110">Na pasta **RemoteMonitoring**, crie um arquivo chamado **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="95361-110">In the **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="95361-111">Abra esse arquivo em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="95361-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="95361-112">No arquivo **remote_monitoring.js**, adicione as seguintes instruções `require`:</span><span class="sxs-lookup"><span data-stu-id="95361-112">In the **remote_monitoring.js** file, add the following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="95361-113">Adicione as declarações de variável a seguir após as instruções `require` .</span><span class="sxs-lookup"><span data-stu-id="95361-113">Add the following variable declarations after the `require` statements.</span></span> <span data-ttu-id="95361-114">Substitua os valores do espaço reservado [Device Id] e [Device Key] pelos valores que você anotou para o seu dispositivo no painel da solução de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="95361-114">Replace the placeholder values [Device Id] and [Device Key] with values you noted for your device in the remote monitoring solution dashboard.</span></span> <span data-ttu-id="95361-115">Use o nome de host do Hub IoT do painel da solução para substituir [IoTHub Name].</span><span class="sxs-lookup"><span data-stu-id="95361-115">Use the IoT Hub Hostname from the solution dashboard to replace [IoTHub Name].</span></span> <span data-ttu-id="95361-116">Por exemplo, se o nome de host do Hub IoT for **contoso.azure-devices.net**, substitua [Nome do HubIoT] por **contoso**:</span><span class="sxs-lookup"><span data-stu-id="95361-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="95361-117">Adicione as seguintes variáveis para definir alguns dados base de telemetria:</span><span class="sxs-lookup"><span data-stu-id="95361-117">Add the following variables to define some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="95361-118">Adicione a seguinte função auxiliar para imprimir os resultados da operação:</span><span class="sxs-lookup"><span data-stu-id="95361-118">Add the following helper function to print operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="95361-119">Adicione a seguinte função auxiliar para usar para tornar os valores de telemetria aleatórios:</span><span class="sxs-lookup"><span data-stu-id="95361-119">Add the following helper function to use to randomize the telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="95361-120">Adicione a seguinte definição para o objeto **DeviceInfo** que o dispositivo envia na inicialização:</span><span class="sxs-lookup"><span data-stu-id="95361-120">Add the following definition for the **DeviceInfo** object the device sends on startup:</span></span>

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

1. <span data-ttu-id="95361-121">Adicione a definição a seguir para os valores relatados para o dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="95361-121">Add the following definition for the device twin reported values.</span></span> <span data-ttu-id="95361-122">Essa definição inclui descrições dos métodos diretos aos quais dispositivo dá suporte:</span><span class="sxs-lookup"><span data-stu-id="95361-122">This definition includes descriptions of the direct methods the device supports:</span></span>

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
            "Reboot": "Reboot the device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI to specifiy the URI of the firmware file"
        },
    }
    ```

1. <span data-ttu-id="95361-123">Adicione a seguinte função para lidar com a chamada de método direta **Reboot**:</span><span class="sxs-lookup"><span data-stu-id="95361-123">Add the following function to handle the **Reboot** direct method call:</span></span>

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete the response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. <span data-ttu-id="95361-124">Adicione a função a seguir para lidar com a chamada de método direta **InitiateFirmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="95361-124">Add the following function to handle the **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="95361-125">Esse método direto usa um parâmetro para especificar o local da imagem do firmware a ser baixado e inicia a atualização do firmware no dispositivo de forma assíncrona:</span><span class="sxs-lookup"><span data-stu-id="95361-125">This direct method uses a parameter to specify the location of the firmware image to download, and initiates the firmware update on the device asynchronously:</span></span>

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete the response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here to perform the firmware update asynchronously
    }
    ```

1. <span data-ttu-id="95361-126">Adicione o seguinte código para criar uma instância do cliente:</span><span class="sxs-lookup"><span data-stu-id="95361-126">Add the following code to create a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="95361-127">Adicione o seguinte código a:</span><span class="sxs-lookup"><span data-stu-id="95361-127">Add the following code to:</span></span>

    * <span data-ttu-id="95361-128">Abra a conexão.</span><span class="sxs-lookup"><span data-stu-id="95361-128">Open the connection.</span></span>
    * <span data-ttu-id="95361-129">Enviar o objeto **DeviceInfo**.</span><span class="sxs-lookup"><span data-stu-id="95361-129">Send the **DeviceInfo** object.</span></span>
    * <span data-ttu-id="95361-130">Configure um manipulador para as propriedades desejadas.</span><span class="sxs-lookup"><span data-stu-id="95361-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="95361-131">Envie as propriedades relatadas.</span><span class="sxs-lookup"><span data-stu-id="95361-131">Send reported properties.</span></span>
    * <span data-ttu-id="95361-132">Registre manipuladores para os métodos diretos.</span><span class="sxs-lookup"><span data-stu-id="95361-132">Register handlers for the direct methods.</span></span>
    * <span data-ttu-id="95361-133">Comece a enviar a telemetria.</span><span class="sxs-lookup"><span data-stu-id="95361-133">Start sending telemetry.</span></span>

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

1. <span data-ttu-id="95361-134">Salve as alterações no arquivo **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="95361-134">Save the changes to the **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="95361-135">Execute o seguinte comando no prompt de comando para iniciar o aplicativo de exemplo:</span><span class="sxs-lookup"><span data-stu-id="95361-135">Run the following command at a command prompt to launch the sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
