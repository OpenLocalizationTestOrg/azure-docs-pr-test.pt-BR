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
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="79a19-104">Enviar mensagens da nuvem para o dispositivo com o Hub IoT (Nó)</span><span class="sxs-lookup"><span data-stu-id="79a19-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="79a19-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="79a19-105">Introduction</span></span>
<span data-ttu-id="79a19-106">O Hub IoT do Azure é um serviço totalmente gerenciado que ajuda a permitir comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end de solução.</span><span class="sxs-lookup"><span data-stu-id="79a19-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="79a19-107">Olá [começar com o IoT Hub] tutorial mostra como toocreate um hub IoT, provisionar uma identidade de dispositivo nele e código de um aplicativo de dispositivo simulado que envia mensagens de dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="79a19-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="79a19-108">Esse tutorial se baseia na [começar com o IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="79a19-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="79a19-109">Ele mostra como:</span><span class="sxs-lookup"><span data-stu-id="79a19-109">It shows you how to:</span></span>

* <span data-ttu-id="79a19-110">Sua solução back-end, envie mensagens de nuvem para dispositivo tooa único dispositivo por meio de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="79a19-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="79a19-111">Receber mensagens da nuvem para o dispositivo em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="79a19-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="79a19-112">De sua solução back-end, solicitar confirmação de entrega (*comentários*) para mensagens enviadas tooa dispositivo do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="79a19-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="79a19-113">Você pode encontrar mais informações sobre mensagens de nuvem para dispositivo em Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="79a19-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="79a19-114">No final da saudação deste tutorial, você deve executar dois aplicativos de console Node. js:</span><span class="sxs-lookup"><span data-stu-id="79a19-114">At hello end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="79a19-115">**SimulatedDevice**, uma versão modificada do aplicativo hello criado no [começar com o IoT Hub], que se conecta tooyour IoT hub e recebe mensagens de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="79a19-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="79a19-116">**SendCloudToDeviceMessage**, que envia um aplicativo de dispositivo simulado toohello mensagem de nuvem para dispositivo por meio de IoT Hub e, em seguida, recebe a sua confirmação de entrega.</span><span class="sxs-lookup"><span data-stu-id="79a19-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="79a19-117">O Hub IoT tem suporte a SDK para várias plataformas de dispositivo e linguagens (incluindo C, Java e Javascript) nos SDKs do dispositivo IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="79a19-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="79a19-118">Para obter instruções passo a passo sobre como tooconnect do seu dispositivo toothis tutorial código e geralmente tooAzure IoT Hub, consulte Olá [Centro de desenvolvedores do Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="79a19-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="79a19-119">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="79a19-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="79a19-120">Node.js versão 0.10.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="79a19-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="79a19-121">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="79a19-121">An active Azure account.</span></span> <span data-ttu-id="79a19-122">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="79a19-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="79a19-123">Receber mensagens no aplicativo de dispositivo simulado Olá</span><span class="sxs-lookup"><span data-stu-id="79a19-123">Receive messages in hello simulated device app</span></span>
<span data-ttu-id="79a19-124">Nesta seção, você modificar o aplicativo de dispositivo simulado Olá criado na [começar com o IoT Hub] tooreceive mensagens de nuvem para dispositivo do hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="79a19-124">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="79a19-125">Usando um editor de texto, abra o arquivo de SimulatedDevice.js de saudação.</span><span class="sxs-lookup"><span data-stu-id="79a19-125">Using a text editor, open hello SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="79a19-126">Modificar Olá **connectCallback** toohandle mensagens enviadas do IoT Hub de função.</span><span class="sxs-lookup"><span data-stu-id="79a19-126">Modify hello **connectCallback** function toohandle messages sent from IoT Hub.</span></span> <span data-ttu-id="79a19-127">Neste exemplo, o dispositivo Olá sempre chama Olá **completa** toonotify IoT Hub que ele processou a mensagem de saudação de função.</span><span class="sxs-lookup"><span data-stu-id="79a19-127">In this example, hello device always invokes hello **complete** function toonotify IoT Hub that it has processed hello message.</span></span> <span data-ttu-id="79a19-128">A nova versão de hello **connectCallback** função aparência Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="79a19-128">Your new version of hello **connectCallback** function looks like hello following snippet:</span></span>
   
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
   > <span data-ttu-id="79a19-129">Se você usar HTTP em vez de MQTT ou AMQP como transporte hello, Olá **DeviceClient** instância procura de mensagens de IoT Hub com pouca frequência (menor que a cada 25 minutos).</span><span class="sxs-lookup"><span data-stu-id="79a19-129">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="79a19-130">Para obter mais informações sobre as diferenças de saudação entre suporte MQTT, AMQP e HTTP e a limitação de Hub IoT, consulte Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="79a19-130">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="79a19-131">Envie uma mensagem da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="79a19-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="79a19-132">Nesta seção, você deve criar um aplicativo de console Node. js que envia mensagens de nuvem para dispositivo toohello dispositivo simulado aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79a19-132">In this section, you create a Node.js console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="79a19-133">Necessário Olá ID do dispositivo do dispositivo Olá adicionado no hello [começar com o IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="79a19-133">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="79a19-134">Você também precisa hello cadeia de caracteres de conexão de IoT Hub para o hub que você pode encontrar no hello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="79a19-134">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="79a19-135">Crie uma pasta vazia denominada **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="79a19-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="79a19-136">Em Olá **sendcloudtodevicemessage** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="79a19-136">In hello **sendcloudtodevicemessage** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="79a19-137">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="79a19-137">Accept all hello defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="79a19-138">O prompt de comando no hello **sendcloudtodevicemessage** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote:</span><span class="sxs-lookup"><span data-stu-id="79a19-138">At your command prompt in hello **sendcloudtodevicemessage** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="79a19-139">Usando um editor de texto, crie um **SendCloudToDeviceMessage.js** arquivo hello **sendcloudtodevicemessage** pasta.</span><span class="sxs-lookup"><span data-stu-id="79a19-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in hello **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="79a19-140">Adicione o seguinte Olá `require` instruções no hello início da saudação **SendCloudToDeviceMessage.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="79a19-140">Add hello following `require` statements at hello start of hello **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="79a19-141">Adicionar Olá código a seguir muito**SendCloudToDeviceMessage.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="79a19-141">Add hello following code too**SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="79a19-142">Substitua o valor de espaço reservado hello "{iot hub conexão string}" hello cadeia de caracteres de conexão de IoT Hub hub Olá criado na saudação de [começar com o IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="79a19-142">Replace hello "{iot hub connection string}" placeholder value with hello IoT Hub connection string for hello hub you created in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="79a19-143">Substitua espaço reservado de hello "{id do dispositivo}" com a ID de dispositivo saudação do dispositivo Olá adicionado no hello [começar com o IoT Hub] tutorial:</span><span class="sxs-lookup"><span data-stu-id="79a19-143">Replace hello "{device id}" placeholder with hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="79a19-144">Adicione Olá console toohello do função tooprint operação resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="79a19-144">Add hello following function tooprint operation results toohello console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="79a19-145">Adicione Olá console toohello mensagens de comentários do função tooprint entrega a seguir:</span><span class="sxs-lookup"><span data-stu-id="79a19-145">Add hello following function tooprint delivery feedback messages toohello console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="79a19-146">Adicione seguinte Olá código toosend um dispositivo de tooyour de mensagem e lidar com mensagem de saudação do comentários quando o dispositivo Olá confirma a mensagem de saudação do nuvem para dispositivo:</span><span class="sxs-lookup"><span data-stu-id="79a19-146">Add hello following code toosend a message tooyour device and handle hello feedback message when hello device acknowledges hello cloud-to-device message:</span></span>
   
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
9. <span data-ttu-id="79a19-147">Salve e feche o arquivo **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="79a19-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="79a19-148">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="79a19-148">Run hello applications</span></span>
<span data-ttu-id="79a19-149">Agora você está pronto toorun aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="79a19-149">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="79a19-150">No prompt de comando de saudação de saudação **simulateddevice** pasta, execute o seguinte Olá comando toosend telemetria tooIoT Hub e toolisten para mensagens de nuvem para dispositivo:</span><span class="sxs-lookup"><span data-stu-id="79a19-150">At hello command prompt in hello **simulateddevice** folder, run hello following command toosend telemetry tooIoT Hub and toolisten for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Execute o aplicativo de dispositivo simulado Olá][img-simulated-device]
2. <span data-ttu-id="79a19-152">Em um prompt de comando no hello **sendcloudtodevicemessage** pasta, execute Olá toosend de comando a seguir uma mensagem de nuvem para dispositivo e aguarde para comentários de confirmação de saudação:</span><span class="sxs-lookup"><span data-stu-id="79a19-152">At a command prompt in hello **sendcloudtodevicemessage** folder, run hello following command toosend a cloud-to-device message and wait for hello acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Execute o comando de nuvem para dispositivo do hello aplicativo toosend Olá][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="79a19-154">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="79a19-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="79a19-155">No código de produção, você deve implementar políticas de repetição (por exemplo, a retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].</span><span class="sxs-lookup"><span data-stu-id="79a19-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="79a19-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79a19-156">Next steps</span></span>
<span data-ttu-id="79a19-157">Neste tutorial, você aprendeu como toosend e receber mensagens de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="79a19-157">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="79a19-158">exemplos de toosee de soluções completas de ponta a ponta que usam o IoT Hub, consulte [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="79a19-158">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="79a19-159">toolearn mais sobre como desenvolver soluções com o IoT Hub, consulte Olá [guia do desenvolvedor de IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="79a19-159">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

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
