---
title: "mensagens de aaaCloud para o dispositivo com o Azure IoT Hub (nó) | Microsoft Docs"
description: Como toosend de nuvem para dispositivo mensagens tooa dispositivo de um hub IoT do Azure usando hello Azure IoT SDKs para Node. js. Modificar as mensagens de nuvem para dispositivo um dispositivo simulado aplicativo tooreceive e modificar as mensagens de nuvem para dispositivo um aplicativo de back-end toosend hello.
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a>Enviar mensagens da nuvem para o dispositivo com o Hub IoT (Nó)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Introdução
O Hub IoT do Azure é um serviço totalmente gerenciado que ajuda a permitir comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end de solução. Olá [começar com o IoT Hub] tutorial mostra como toocreate um hub IoT, provisionar uma identidade de dispositivo nele e código de um aplicativo de dispositivo simulado que envia mensagens de dispositivo para a nuvem.

Esse tutorial se baseia na [começar com o IoT Hub]. Ele mostra como:

* Sua solução back-end, envie mensagens de nuvem para dispositivo tooa único dispositivo por meio de IoT Hub.
* Receber mensagens da nuvem para o dispositivo em um dispositivo.
* De sua solução back-end, solicitar confirmação de entrega (*comentários*) para mensagens enviadas tooa dispositivo do IoT Hub.

Você pode encontrar mais informações sobre mensagens de nuvem para dispositivo em Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].

No final da saudação deste tutorial, você deve executar dois aplicativos de console Node. js:

* **SimulatedDevice**, uma versão modificada do aplicativo hello criado no [começar com o IoT Hub], que se conecta tooyour IoT hub e recebe mensagens de nuvem para dispositivo.
* **SendCloudToDeviceMessage**, que envia um aplicativo de dispositivo simulado toohello mensagem de nuvem para dispositivo por meio de IoT Hub e, em seguida, recebe a sua confirmação de entrega.

> [!NOTE]
> O Hub IoT tem suporte a SDK para várias plataformas de dispositivo e linguagens (incluindo C, Java e Javascript) nos SDKs do dispositivo IoT do Azure. Para obter instruções passo a passo sobre como tooconnect do seu dispositivo toothis tutorial código e geralmente tooAzure IoT Hub, consulte Olá [Centro de desenvolvedores do Azure IoT].
> 
> 

toocomplete neste tutorial, você precisa Olá a seguir:

* Node.js versão 0.10.x ou posterior.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

## <a name="receive-messages-in-hello-simulated-device-app"></a>Receber mensagens no aplicativo de dispositivo simulado Olá
Nesta seção, você modificar o aplicativo de dispositivo simulado Olá criado na [começar com o IoT Hub] tooreceive mensagens de nuvem para dispositivo do hub IoT de saudação.

1. Usando um editor de texto, abra o arquivo de SimulatedDevice.js de saudação.
2. Modificar Olá **connectCallback** toohandle mensagens enviadas do IoT Hub de função. Neste exemplo, o dispositivo Olá sempre chama Olá **completa** toonotify IoT Hub que ele processou a mensagem de saudação de função. A nova versão de hello **connectCallback** função aparência Olá trecho de código a seguir:
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
   
   > [!NOTE]
   > Se você usar HTTP em vez de MQTT ou AMQP como transporte hello, Olá **DeviceClient** instância procura de mensagens de IoT Hub com pouca frequência (menor que a cada 25 minutos). Para obter mais informações sobre as diferenças de saudação entre suporte MQTT, AMQP e HTTP e a limitação de Hub IoT, consulte Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a>Envie uma mensagem da nuvem para o dispositivo
Nesta seção, você deve criar um aplicativo de console Node. js que envia mensagens de nuvem para dispositivo toohello dispositivo simulado aplicativo. Necessário Olá ID do dispositivo do dispositivo Olá adicionado no hello [começar com o IoT Hub] tutorial. Você também precisa hello cadeia de caracteres de conexão de IoT Hub para o hub que você pode encontrar no hello [portal do Azure].

1. Crie uma pasta vazia denominada **sendcloudtodevicemessage**. Em Olá **sendcloudtodevicemessage** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação:
   
    ```shell
    npm init
    ```
2. O prompt de comando no hello **sendcloudtodevicemessage** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote:
   
    ```shell
    npm install azure-iothub --save
    ```
3. Usando um editor de texto, crie um **SendCloudToDeviceMessage.js** arquivo hello **sendcloudtodevicemessage** pasta.
4. Adicione o seguinte Olá `require` instruções no hello início da saudação **SendCloudToDeviceMessage.js** arquivo:
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. Adicionar Olá código a seguir muito**SendCloudToDeviceMessage.js** arquivo. Substitua o valor de espaço reservado hello "{iot hub conexão string}" hello cadeia de caracteres de conexão de IoT Hub hub Olá criado na saudação de [começar com o IoT Hub] tutorial. Substitua espaço reservado de hello "{id do dispositivo}" com a ID de dispositivo saudação do dispositivo Olá adicionado no hello [começar com o IoT Hub] tutorial:
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. Adicione Olá console toohello do função tooprint operação resultados a seguir:
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Adicione Olá console toohello mensagens de comentários do função tooprint entrega a seguir:
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. Adicione seguinte Olá código toosend um dispositivo de tooyour de mensagem e lidar com mensagem de saudação do comentários quando o dispositivo Olá confirma a mensagem de saudação do nuvem para dispositivo:
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. Salve e feche o arquivo **SendCloudToDeviceMessage.js** .

## <a name="run-hello-applications"></a>Executar aplicativos Olá
Agora você está pronto toorun aplicativos de saudação.

1. No prompt de comando de saudação de saudação **simulateddevice** pasta, execute o seguinte Olá comando toosend telemetria tooIoT Hub e toolisten para mensagens de nuvem para dispositivo:
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Execute o aplicativo de dispositivo simulado Olá][img-simulated-device]
2. Em um prompt de comando no hello **sendcloudtodevicemessage** pasta, execute Olá toosend de comando a seguir uma mensagem de nuvem para dispositivo e aguarde para comentários de confirmação de saudação:
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Execute o comando de nuvem para dispositivo do hello aplicativo toosend Olá][img-send-command]
   
   > [!NOTE]
   > Para simplificar, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, a retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].
   > 
   > 

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como toosend e receber mensagens de nuvem para dispositivo. 

exemplos de toosee de soluções completas de ponta a ponta que usam o IoT Hub, consulte [Azure IoT Suite].

toolearn mais sobre como desenvolver soluções com o IoT Hub, consulte Olá [guia do desenvolvedor de IoT Hub].

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[começar com o IoT Hub]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[guia do desenvolvedor de IoT Hub]: iot-hub-devguide.md
[Centro de desenvolvedores do Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[tratamento de falhas transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portal do Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
