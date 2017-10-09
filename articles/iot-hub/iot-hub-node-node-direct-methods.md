---
title: "aaaAzure IoT Hub direcionar métodos (nó) | Microsoft Docs"
description: "Como toouse Azure IoT Hub direta métodos. Você pode usar hello Azure IoT SDKs para tooimplement Node. js, um aplicativo de dispositivo simulado que inclui um método direto e um aplicativo de serviço que invoca o método direto hello."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a>Usar métodos diretos no dispositivo IoT com o Node.js
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

No final da saudação deste tutorial, você tem dois aplicativos de console Node. js:

* **CallMethodOnDevice.js**, que chama um método no aplicativo do dispositivo simulado hello e exibe a resposta de saudação.
* **SimulatedDevice.js**, que se conecta tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente e responde toohello método chamado pela nuvem hello.

> [!NOTE]
> artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun ambos os aplicativos em dispositivos e o back-end da solução.
> 
> 

toocomplete neste tutorial, você precisa Olá a seguir:

* Node.js versão 0.10.x ou posterior.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado
Nesta seção, você deve criar um aplicativo de console Node. js que responde tooa método chamado pela nuvem hello.

1. Crie uma nova pasta vazia denominada **simulateddevice**. Em Olá **simulateddevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **simulateddevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** pacote do SDK do dispositivo e **azure iot dispositivo-mqtt**pacote:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Usando um editor de texto, crie um novo **SimulatedDevice.js** arquivo hello **simulateddevice** pasta.
4. Adicione o seguinte Olá `require` instruções no hello início da saudação **SimulatedDevice.js** arquivo:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Adicionar um **connectionString** variável e use-toocreate uma **DeviceClient** instância. Substituir **{string de conexão do dispositivo}** com a cadeia de conexão de dispositivo Olá gerado na Olá *criar uma identidade de dispositivo* seção:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Adicione Olá seguinte método de saudação do tooimplement de função no dispositivo hello:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Abrir o hub IoT do hello conexão tooyour e começar a inicializar Olá método ouvinte:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Salve e feche o hello **SimulatedDevice.js** arquivo.

> [!NOTE]
> coisas tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (como tentativas de conexão), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].
> 
> 

## <a name="call-a-method-on-a-device"></a>Chamar um método em um dispositivo
Nesta seção, você deve criar um aplicativo de console Node. js que chama um método no aplicativo do dispositivo simulado hello e, em seguida, exibe a resposta de saudação.

1. Crie uma nova pasta vazia denominada **callmethodondevice**. Em Olá **callmethodondevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **callmethodondevice** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote:
   
    ```
    npm install azure-iothub --save
    ```
3. Usando um editor de texto, crie um **CallMethodOnDevice.js** arquivo hello **callmethodondevice** pasta.
4. Adicione o seguinte Olá `require` instruções no hello início da saudação **CallMethodOnDevice.js** arquivo:
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. Adicione Olá após a declaração de variável e substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub para o hub:
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. Crie Olá cliente tooopen Olá conexão tooyour IoT hub.
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. Adicione Olá função tooinvoke Olá dispositivo método e impressão Olá dispositivo resposta toohello console a seguir:
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. Salve e feche o hello **CallMethodOnDevice.js** arquivo.

## <a name="run-hello-apps"></a>Executar aplicativos Olá
Agora você está pronto toorun Olá aplicativos.

1. Em um prompt de comando no hello **simulateddevice** pasta, execute Olá escutando chamadas de método do seu IoT Hub de toostart de comando a seguir:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. Em um prompt de comando no hello **callmethodondevice** pasta, execute Olá toobegin comando seu hub IoT de monitoramento a seguir:
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. Você verá dispositivo Olá reagir toohello método imprimindo mensagem de saudação e o aplicativo hello chamado resposta de Olá Olá método exibição do dispositivo hello:
   
    ![][9]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello. Você usou esse dispositivo identidade tooenable Olá simulado dispositivo aplicativo tooreact toomethods invocado pela nuvem hello. Você também criou um aplicativo que chama métodos no dispositivo hello e exibe a resposta de saudação do dispositivo de saudação. 

toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:

* [Introdução ao Hub IoT]
* [Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]

toolearn como tooextend seu método de solução e agenda IoT chama em vários dispositivos, consulte Olá [agenda e trabalhos de difusão] [ lnk-tutorial-jobs] tutorial.

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Introdução ao Hub IoT]: iot-hub-node-node-getstarted.md
