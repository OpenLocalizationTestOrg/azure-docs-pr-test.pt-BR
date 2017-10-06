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
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a><span data-ttu-id="b5fe4-104">Conecte seu dispositivo simulado tooyour IoT hub que usando o nó</span><span class="sxs-lookup"><span data-stu-id="b5fe4-104">Connect your simulated device tooyour IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="b5fe4-105">No final da saudação deste tutorial, você tem três aplicativos de console Node. js:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-105">At hello end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="b5fe4-106">**CreateDeviceIdentity.js**, que cria uma identidade de dispositivo e de segurança da chave tooconnect seu aplicativo de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="b5fe4-107">**ReadDeviceToCloudMessages.js**, que exibe a telemetria de saudação enviada pelo seu aplicativo de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-107">**ReadDeviceToCloudMessages.js**, which displays hello telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="b5fe4-108">**SimulatedDevice.js**, que conecta tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente e envia uma mensagem de telemetria a cada segundo usando Olá protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-108">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="b5fe4-109">artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun ambos os aplicativos em dispositivos e o back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="b5fe4-110">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b5fe4-111">Node.js versão 0.10.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="b5fe4-112">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-112">An active Azure account.</span></span> <span data-ttu-id="b5fe4-113">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="b5fe4-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="b5fe4-114">Você criou seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-114">You have now created your IoT hub.</span></span> <span data-ttu-id="b5fe4-115">Você tem Olá nome de host do IoT Hub e Olá cadeia de caracteres de conexão de IoT Hub que você precisa toocomplete restante Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-115">You have hello IoT Hub host name and hello IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="b5fe4-116">Criar uma identidade do dispositivo</span><span class="sxs-lookup"><span data-stu-id="b5fe4-116">Create a device identity</span></span>
<span data-ttu-id="b5fe4-117">Nesta seção, você deve criar um aplicativo de console Node. js que cria uma identidade de dispositivo no registro de identidade Olá em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-117">In this section, you create a Node.js console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="b5fe4-118">Um dispositivo só pode se conectar a tooIoT hub se ela possui uma entrada no registro de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-118">A device can only connect tooIoT hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="b5fe4-119">Para obter mais informações, consulte Olá **registro identidade** seção Olá [guia do desenvolvedor de IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="b5fe4-119">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="b5fe4-120">Quando você executa esse aplicativo de console, ele gera uma ID de dispositivo exclusivo e chave que seu dispositivo possa usar tooidentify em si, quando ele envia o dispositivo para nuvem mensagens tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-120">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="b5fe4-121">Crie uma nova pasta vazia denominada **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="b5fe4-122">Em Olá **createdeviceidentity** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-122">In hello **createdeviceidentity** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="b5fe4-123">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-123">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b5fe4-124">O prompt de comando no hello **createdeviceidentity** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote do SDK do serviço:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-124">At your command prompt in hello **createdeviceidentity** folder, run hello following command tooinstall hello **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="b5fe4-125">Usando um editor de texto, crie um **CreateDeviceIdentity.js** arquivo hello **createdeviceidentity** pasta.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-125">Using a text editor, create a **CreateDeviceIdentity.js** file in hello **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="b5fe4-126">Adicione o seguinte Olá `require` instrução no início de saudação do hello **CreateDeviceIdentity.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-126">Add hello following `require` statement at hello start of hello **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="b5fe4-127">Adicionar Olá toohello de código a seguir **CreateDeviceIdentity.js** de arquivo e substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá você criou na seção anterior saudação de:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-127">Add hello following code toohello **CreateDeviceIdentity.js** file and replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="b5fe4-128">Adicione Olá uma definição do dispositivo no registro de identidade Olá em seu hub IoT de toocreate de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-128">Add hello following code toocreate a device definition in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="b5fe4-129">Esse código cria um dispositivo se Olá ID do dispositivo não existe no registro de identidade hello, caso contrário ele retornará a chave de saudação do dispositivo existente hello:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-129">This code creates a device if hello device ID does not exist in hello identity registry, otherwise it returns hello key of hello existing device:</span></span>
   
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

7. <span data-ttu-id="b5fe4-130">Salve e feche o arquivo **CreateDeviceIdentity.js** .</span><span class="sxs-lookup"><span data-stu-id="b5fe4-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="b5fe4-131">Olá toorun **createdeviceidentity** aplicativo, executar Olá comando no prompt de comando Olá na pasta de createdeviceidentity Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-131">toorun hello **createdeviceidentity** application, execute hello following command at hello command prompt in hello createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="b5fe4-132">Anote Olá **ID do dispositivo** e **chave dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-132">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="b5fe4-133">É necessário mais tarde esses valores quando você cria um aplicativo que se conecta tooIoT Hub como um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-133">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="b5fe4-134">Olá registro de identidade de IoT Hub armazena apenas o hub IoT toohello de proteger o acesso do dispositivo identidades tooenable.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-134">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="b5fe4-135">Ele armazena toouse IDs e chaves de dispositivo como credenciais de segurança e um sinalizador habilitado/desabilitado que você pode usar o acesso de toodisable para um dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-135">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="b5fe4-136">Se seu aplicativo precisa toostore outros metadados específicos do dispositivo, ele deve usar um repositório específico do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-136">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="b5fe4-137">Para obter mais informações, consulte Olá [guia do desenvolvedor de IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="b5fe4-137">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="b5fe4-138">Receber mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="b5fe4-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="b5fe4-139">Nesta seção, você cria um aplicativo de console do Node.js que lê as mensagens do dispositivo para a nuvem a partir do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="b5fe4-140">Um hub IoT expõe um [Hubs de eventos][lnk-event-hubs-overview]-tooenable de ponto de extremidade compatível tooread mensagens de dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="b5fe4-141">coisas tookeep simples, este tutorial cria um leitor básico que não é adequado para uma implantação de alta taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-141">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="b5fe4-142">Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial mostra como o dispositivo para nuvem tooprocess mensagens em escala.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-142">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="b5fe4-143">Olá [Introdução aos Hubs de eventos] [ lnk-eventhubs-tutorial] tutorial fornece informações adicionais sobre como tooprocess mensagens de Hubs de eventos e é aplicável toohello pontos de extremidade compatível com o evento de Hub IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-143">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="b5fe4-144">Olá, ponto de extremidade compatível com o evento Hub para ler mensagens de dispositivo para nuvem sempre usa protocolo AMQP de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-144">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="b5fe4-145">Crie uma pasta vazia denominada **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="b5fe4-146">Em Olá **readdevicetocloudmessages** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-146">In hello **readdevicetocloudmessages** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="b5fe4-147">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-147">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b5fe4-148">O prompt de comando no hello **readdevicetocloudmessages** pasta, execute Olá Olá de tooinstall de comando a seguir **hubs de eventos do azure** pacote:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-148">At your command prompt in hello **readdevicetocloudmessages** folder, run hello following command tooinstall hello **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="b5fe4-149">Usando um editor de texto, crie um **ReadDeviceToCloudMessages.js** arquivo hello **readdevicetocloudmessages** pasta.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in hello **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="b5fe4-150">Adicione o seguinte Olá `require` instruções no hello início da saudação **ReadDeviceToCloudMessages.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-150">Add hello following `require` statements at hello start of hello **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="b5fe4-151">Adicione Olá após a declaração de variável e substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub para o hub:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-151">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="b5fe4-152">Adicione Olá duas funções que imprimir saída toohello console a seguir:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-152">Add hello following two functions that print output toohello console:</span></span>
   
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
7. <span data-ttu-id="b5fe4-153">Adicionar Olá Olá de toocreate de código a seguir **EventHubClient**, abra Olá conexão tooyour IoT Hub e criar um receptor para cada partição.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-153">Add hello following code toocreate hello **EventHubClient**, open hello connection tooyour IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="b5fe4-154">Este aplicativo usa um filtro ao criar um receptor de forma que hello destinatário lê apenas as mensagens enviadas tooIoT Hub depois receptor Olá começa a ser executado.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-154">This application uses a filter when it creates a receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="b5fe4-155">Esse filtro é útil em um ambiente de teste para ver apenas Olá conjunto atual de mensagens.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-155">This filter is useful in a test environment so you see just hello current set of messages.</span></span> <span data-ttu-id="b5fe4-156">Em um ambiente de produção, seu código deve ter certeza de que ele processa todas as mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-156">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="b5fe4-157">Para obter mais informações, consulte Olá [como tooprocess mensagens de dispositivo para a nuvem de IoT Hub] [ lnk-process-d2c-tutorial] tutorial:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-157">For more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
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
8. <span data-ttu-id="b5fe4-158">Salve e feche o hello **ReadDeviceToCloudMessages.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-158">Save and close hello **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b5fe4-159">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="b5fe4-159">Create a simulated device app</span></span>
<span data-ttu-id="b5fe4-160">Nesta seção, você deve criar um aplicativo de console Node. js que simula um dispositivo que envia o hub de IoT tooan mensagens de dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="b5fe4-161">Crie uma pasta vazia denominada **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="b5fe4-162">Em Olá **simulateddevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-162">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="b5fe4-163">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-163">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b5fe4-164">O prompt de comando no hello **simulateddevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** pacote do SDK do dispositivo e **azure iot dispositivo-mqtt**pacote:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-164">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="b5fe4-165">Usando um editor de texto, crie um **SimulatedDevice.js** arquivo hello **simulateddevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-165">Using a text editor, create a **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="b5fe4-166">Adicione o seguinte Olá `require` instruções no hello início da saudação **SimulatedDevice.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-166">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="b5fe4-167">Adicionar um **connectionString** variável e use-toocreate uma **cliente** instância.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-167">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="b5fe4-168">Substituir **{youriothostname}** com nome de saudação do hub IoT de saudação criado Olá *criar um IoT Hub* seção.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-168">Replace **{youriothostname}** with hello name of hello IoT hub you created hello *Create an IoT Hub* section.</span></span> <span data-ttu-id="b5fe4-169">Substituir **{yourdevicekey}** com valor de chave de dispositivo do hello gerado na Olá *criar uma identidade de dispositivo* seção:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-169">Replace **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="b5fe4-170">Adicione Olá a seguir da saída de toodisplay de função de aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-170">Add hello following function toodisplay output from hello application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="b5fe4-171">Criar um retorno de chamada e usar Olá **setInterval** função toosend um hub de IoT tooyour mensagens por segundo:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-171">Create a callback and use hello **setInterval** function toosend a message tooyour IoT hub every second:</span></span>
   
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
8. <span data-ttu-id="b5fe4-172">Abra Olá conexão tooyour IoT Hub e iniciar o envio de mensagens:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-172">Open hello connection tooyour IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="b5fe4-173">Salve e feche o hello **SimulatedDevice.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-173">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="b5fe4-174">coisas tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-174">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b5fe4-175">No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="b5fe4-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-hello-apps"></a><span data-ttu-id="b5fe4-176">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="b5fe4-176">Run hello apps</span></span>
<span data-ttu-id="b5fe4-177">Agora você está pronto toorun Olá aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-177">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="b5fe4-178">Em um prompt de comando no hello **readdevicetocloudmessages** pasta, execute Olá toobegin comando seu hub IoT de monitoramento a seguir:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-178">At a command prompt in hello **readdevicetocloudmessages** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Mensagens de dispositivo para nuvem toomonitor do aplicativo de serviço de IoT Hub Node. js][7]
2. <span data-ttu-id="b5fe4-180">Em um prompt de comando no hello **simulateddevice** pasta, execute Olá toobegin comando Enviar hub IoT do telemetria dados tooyour a seguir:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-180">At a command prompt in hello **simulateddevice** folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Mensagens de dispositivo para nuvem toosend do aplicativo de dispositivos de IoT Hub Node. js][8]
3. <span data-ttu-id="b5fe4-182">Olá **uso** lado a lado no hello [portal do Azure] [ lnk-portal] mostra Olá número de mensagens enviadas toohello IoT hub:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-182">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>
   
    ![Azure portal uso bloco mostra o número de mensagens enviadas tooIoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="b5fe4-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b5fe4-184">Next steps</span></span>
<span data-ttu-id="b5fe4-185">Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-185">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="b5fe4-186">Você usou este dispositivo identidade tooenable Olá simulado dispositivo aplicativo toosend mensagens de dispositivo para nuvem toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-186">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="b5fe4-187">Você também criou um aplicativo que exibe mensagens de saudação recebidas pelo hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-187">You also created an app that displays hello messages received by hello IoT hub.</span></span> 

<span data-ttu-id="b5fe4-188">toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="b5fe4-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="b5fe4-189">[Conectando o dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="b5fe4-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="b5fe4-190">[Introdução ao gerenciamento de dispositivo][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="b5fe4-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="b5fe4-191">[Introdução ao Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="b5fe4-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="b5fe4-192">toolearn como tooextend seu IoT solução e o processo de dispositivo para nuvem mensagens em grande escala, consulte Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="b5fe4-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
