---
title: "aaaGet de Introdução ao gerenciamento de dispositivos do Azure IoT Hub (nó) | Microsoft Docs"
description: "Como toouse tooinitiate de gerenciamento de dispositivo do IoT Hub um dispositivo remoto reinicializar. Use hello Azure IoT SDK para Node.js tooimplement um aplicativo de dispositivo simulado que inclui um método direto e um aplicativo de serviço que invoca o método direto hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a>Introdução ao gerenciamento de dispositivos (Node)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Este tutorial mostra como:

* Use Olá toocreate portal do Azure um IoT Hub e criar uma identidade de dispositivo em seu hub IoT.
* Crie um aplicativo de dispositivo simulado contendo um método direto que reinicia o dispositivo. Métodos diretos são chamados de nuvem hello.
* Crie um aplicativo de console Node. js que chama o método direto de reinicialização Olá no aplicativo do dispositivo simulado Olá por meio de seu hub IoT.

No final da saudação deste tutorial, você tem dois aplicativos de console Node. js:

**dmpatterns_getstarted_device.js**, que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente, recebe um método direto de reinicialização, simula uma reinicialização física e relata o tempo para a última reinicialização do Olá Olá.

**dmpatterns_getstarted_service.js**, que chama um método direto no aplicativo do dispositivo simulado hello, exibe a resposta de saudação e exibe Olá atualizado relatado propriedades.

toocomplete neste tutorial, você precisa Olá a seguir:

* Node.js versão 0.12.x ou posterior. <br/>  [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node. js para este tutorial no Windows ou Linux.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado
Nesta seção, você irá

* Criar um aplicativo de console do Node. js que responde tooa método direto chamado pela nuvem Olá
* Disparar uma reinicialização do dispositivo simulado
* Olá Use relatado propriedades tooenable dispositivos duas consultas tooidentify dispositivos e quando eles reiniciado pela última vez

1. Crie uma pasta vazia denominada **manageddevice**.  Em Olá **manageddevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.  Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **manageddevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** pacote do SDK do dispositivo e **azure iot dispositivo-mqtt**pacote:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Usando um editor de texto, crie um **dmpatterns_getstarted_device.js** arquivo hello **manageddevice** pasta.
4. Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **dmpatterns_getstarted_device.js** arquivo:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Adicionar um **connectionString** variável e use-toocreate uma **cliente** instância.  Substitua a cadeia de caracteres de conexão de saudação com a cadeia de caracteres de conexão do dispositivo.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Adicionar Olá seguinte função tooimplement Olá ao método direto no dispositivo Olá
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Abra o hub IoT do hello conexão tooyour e iniciar o ouvinte de método direto hello:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. Salve e feche o hello **dmpatterns_getstarted_device.js** arquivo.

> [!NOTE]
> coisas tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Disparar uma reinicialização remota no dispositivo hello usando um método direto
Nesta seção, você criará um aplicativo do console Node.js que inicia uma reinicialização remota em um dispositivo usando um método direto. aplicativo Hello usa Olá de toodiscover hora da última reinicialização do dispositivo duas consultas para o dispositivo.

1. Crie uma pasta vazia denominada **triggerrebootondevice**.  Em Olá **triggerrebootondevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.  Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **triggerrebootondevice** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote do SDK do dispositivo e **azure iot dispositivo-mqtt** pacote:
   
    ```
    npm install azure-iothub --save
    ```
3. Usando um editor de texto, crie um **dmpatterns_getstarted_service.js** arquivo hello **triggerrebootondevice** pasta.
4. Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **dmpatterns_getstarted_service.js** arquivo:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Adicione Olá declarações de variáveis a seguir e substitua os valores de espaço reservado de saudação:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. Adicione Olá função tooinvoke Olá dispositivo método tooreboot Olá dispositivo de destino a seguir:
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. Adicione seguinte Olá função tooquery para dispositivo hello e obter Olá último tempo de reinicialização:
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. Adicione Olá seguintes funções de saudação do código toocall que disparam Olá reinicialize método direto e consultar Olá última tempo de reinicialização:
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. Salve e feche o hello **dmpatterns_getstarted_service.js** arquivo.

## <a name="run-hello-apps"></a>Executar aplicativos Olá
Agora você está pronto toorun Olá aplicativos.

1. No prompt de comando de saudação de saudação **manageddevice** pasta, execute Olá toobegin comando escuta para o método direto de reinicialização Olá a seguir.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. No prompt de comando de saudação de saudação **triggerrebootondevice** pasta, execute Olá após o comando tootrigger Olá remoto reinicializar e consultar para saudação do hello dispositivo duas toofind reinicialize última hora.
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. Consulte o hello dispositivo resposta toohello método direto no console de saudação.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
