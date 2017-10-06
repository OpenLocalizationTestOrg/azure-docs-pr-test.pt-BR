---
title: "aaaGet de Introdução ao Azure IoT Hub (nó) | Microsoft Docs"
description: "Saiba como dispositivo para nuvem toosend mensagens tooAzure IoT Hub usando IoT SDKs para Node. js. Criar dispositivo simulado e tooregister de aplicativos de serviço de seu dispositivo, enviar mensagens e ler mensagens de hub IoT."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a>Conecte seu dispositivo simulado tooyour IoT hub que usando o nó
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

No final da saudação deste tutorial, você tem três aplicativos de console Node. js:

* **CreateDeviceIdentity.js**, que cria uma identidade de dispositivo e de segurança da chave tooconnect seu aplicativo de dispositivo simulado.
* **ReadDeviceToCloudMessages.js**, que exibe a telemetria de saudação enviada pelo seu aplicativo de dispositivo simulado.
* **SimulatedDevice.js**, que conecta tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente e envia uma mensagem de telemetria a cada segundo usando Olá protocolo MQTT.

> [!NOTE]
> artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun ambos os aplicativos em dispositivos e o back-end da solução.
> 
> 

toocomplete neste tutorial, você precisa Olá a seguir:

* Node.js versão 0.10.x ou posterior.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Você criou seu Hub IoT. Você tem Olá nome de host do IoT Hub e Olá cadeia de caracteres de conexão de IoT Hub que você precisa toocomplete restante Olá deste tutorial.

## <a name="create-a-device-identity"></a>Criar uma identidade do dispositivo
Nesta seção, você deve criar um aplicativo de console Node. js que cria uma identidade de dispositivo no registro de identidade Olá em seu hub IoT. Um dispositivo só pode se conectar a tooIoT hub se ela possui uma entrada no registro de identidade hello. Para obter mais informações, consulte Olá **registro identidade** seção Olá [guia do desenvolvedor de IoT Hub][lnk-devguide-identity]. Quando você executa esse aplicativo de console, ele gera uma ID de dispositivo exclusivo e chave que seu dispositivo possa usar tooidentify em si, quando ele envia o dispositivo para nuvem mensagens tooIoT Hub.

1. Crie uma nova pasta vazia denominada **createdeviceidentity**. Em Olá **createdeviceidentity** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **createdeviceidentity** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote do SDK do serviço:
   
    ```
    npm install azure-iothub --save
    ```
3. Usando um editor de texto, crie um **CreateDeviceIdentity.js** arquivo hello **createdeviceidentity** pasta.
4. Adicione o seguinte Olá `require` instrução no início de saudação do hello **CreateDeviceIdentity.js** arquivo:
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. Adicionar Olá toohello de código a seguir **CreateDeviceIdentity.js** de arquivo e substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá você criou na seção anterior saudação de: 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. Adicione Olá uma definição do dispositivo no registro de identidade Olá em seu hub IoT de toocreate de código a seguir. Esse código cria um dispositivo se Olá ID do dispositivo não existe no registro de identidade hello, caso contrário ele retornará a chave de saudação do dispositivo existente hello:
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. Salve e feche o arquivo **CreateDeviceIdentity.js** .
8. Olá toorun **createdeviceidentity** aplicativo, executar Olá comando no prompt de comando Olá na pasta de createdeviceidentity Olá a seguir:
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. Anote Olá **ID do dispositivo** e **chave dispositivo**. É necessário mais tarde esses valores quando você cria um aplicativo que se conecta tooIoT Hub como um dispositivo.

> [!NOTE]
> Olá registro de identidade de IoT Hub armazena apenas o hub IoT toohello de proteger o acesso do dispositivo identidades tooenable. Ele armazena toouse IDs e chaves de dispositivo como credenciais de segurança e um sinalizador habilitado/desabilitado que você pode usar o acesso de toodisable para um dispositivo individual. Se seu aplicativo precisa toostore outros metadados específicos do dispositivo, ele deve usar um repositório específico do aplicativo. Para obter mais informações, consulte Olá [guia do desenvolvedor de IoT Hub][lnk-devguide-identity].
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a>Receber mensagens do dispositivo para a nuvem
Nesta seção, você cria um aplicativo de console do Node.js que lê as mensagens do dispositivo para a nuvem a partir do Hub IoT. Um hub IoT expõe um [Hubs de eventos][lnk-event-hubs-overview]-tooenable de ponto de extremidade compatível tooread mensagens de dispositivo para a nuvem. coisas tookeep simples, este tutorial cria um leitor básico que não é adequado para uma implantação de alta taxa de transferência. Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial mostra como o dispositivo para nuvem tooprocess mensagens em escala. Olá [Introdução aos Hubs de eventos] [ lnk-eventhubs-tutorial] tutorial fornece informações adicionais sobre como tooprocess mensagens de Hubs de eventos e é aplicável toohello pontos de extremidade compatível com o evento de Hub IoT Hub.

> [!NOTE]
> Olá, ponto de extremidade compatível com o evento Hub para ler mensagens de dispositivo para nuvem sempre usa protocolo AMQP de saudação.
> 
> 

1. Crie uma pasta vazia denominada **readdevicetocloudmessages**. Em Olá **readdevicetocloudmessages** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **readdevicetocloudmessages** pasta, execute Olá Olá de tooinstall de comando a seguir **hubs de eventos do azure** pacote:
   
    ```
    npm install azure-event-hubs --save
    ```
3. Usando um editor de texto, crie um **ReadDeviceToCloudMessages.js** arquivo hello **readdevicetocloudmessages** pasta.
4. Adicione o seguinte Olá `require` instruções no hello início da saudação **ReadDeviceToCloudMessages.js** arquivo:
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. Adicione Olá após a declaração de variável e substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub para o hub:
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. Adicione Olá duas funções que imprimir saída toohello console a seguir:
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. Adicionar Olá Olá de toocreate de código a seguir **EventHubClient**, abra Olá conexão tooyour IoT Hub e criar um receptor para cada partição. Este aplicativo usa um filtro ao criar um receptor de forma que hello destinatário lê apenas as mensagens enviadas tooIoT Hub depois receptor Olá começa a ser executado. Esse filtro é útil em um ambiente de teste para ver apenas Olá conjunto atual de mensagens. Em um ambiente de produção, seu código deve ter certeza de que ele processa todas as mensagens de saudação. Para obter mais informações, consulte Olá [como tooprocess mensagens de dispositivo para a nuvem de IoT Hub] [ lnk-process-d2c-tutorial] tutorial:
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. Salve e feche o hello **ReadDeviceToCloudMessages.js** arquivo.

## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado
Nesta seção, você deve criar um aplicativo de console Node. js que simula um dispositivo que envia o hub de IoT tooan mensagens de dispositivo para a nuvem.

1. Crie uma pasta vazia denominada **simulateddevice**. Em Olá **simulateddevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **simulateddevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** pacote do SDK do dispositivo e **azure iot dispositivo-mqtt**pacote:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Usando um editor de texto, crie um **SimulatedDevice.js** arquivo hello **simulateddevice** pasta.
4. Adicione o seguinte Olá `require` instruções no hello início da saudação **SimulatedDevice.js** arquivo:
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. Adicionar um **connectionString** variável e use-toocreate uma **cliente** instância. Substituir **{youriothostname}** com nome de saudação do hub IoT de saudação criado Olá *criar um IoT Hub* seção. Substituir **{yourdevicekey}** com valor de chave de dispositivo do hello gerado na Olá *criar uma identidade de dispositivo* seção:
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. Adicione Olá a seguir da saída de toodisplay de função de aplicativo hello:
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Criar um retorno de chamada e usar Olá **setInterval** função toosend um hub de IoT tooyour mensagens por segundo:
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
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
8. Abra Olá conexão tooyour IoT Hub e iniciar o envio de mensagens:
   
    ```
    client.open(connectCallback);
    ```
9. Salve e feche o hello **SimulatedDevice.js** arquivo.

> [!NOTE]
> coisas tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].
> 
> 

## <a name="run-hello-apps"></a>Executar aplicativos Olá
Agora você está pronto toorun Olá aplicativos.

1. Em um prompt de comando no hello **readdevicetocloudmessages** pasta, execute Olá toobegin comando seu hub IoT de monitoramento a seguir:
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Mensagens de dispositivo para nuvem toomonitor do aplicativo de serviço de IoT Hub Node. js][7]
2. Em um prompt de comando no hello **simulateddevice** pasta, execute Olá toobegin comando Enviar hub IoT do telemetria dados tooyour a seguir:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Mensagens de dispositivo para nuvem toosend do aplicativo de dispositivos de IoT Hub Node. js][8]
3. Olá **uso** lado a lado no hello [portal do Azure] [ lnk-portal] mostra Olá número de mensagens enviadas toohello IoT hub:
   
    ![Azure portal uso bloco mostra o número de mensagens enviadas tooIoT Hub][43]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello. Você usou este dispositivo identidade tooenable Olá simulado dispositivo aplicativo toosend mensagens de dispositivo para nuvem toohello hub IoT. Você também criou um aplicativo que exibe mensagens de saudação recebidas pelo hub IoT de saudação. 

toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:

* [Conectando o dispositivo][lnk-connect-device]
* [Introdução ao gerenciamento de dispositivo][lnk-device-management]
* [Introdução ao Azure IoT Edge][lnk-iot-edge]

toolearn como tooextend seu IoT solução e o processo de dispositivo para nuvem mensagens em grande escala, consulte Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
