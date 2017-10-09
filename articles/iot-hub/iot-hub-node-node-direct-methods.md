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
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="f55cf-104">Usar métodos diretos no dispositivo IoT com o Node.js</span><span class="sxs-lookup"><span data-stu-id="f55cf-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="f55cf-105">No final da saudação deste tutorial, você tem dois aplicativos de console Node. js:</span><span class="sxs-lookup"><span data-stu-id="f55cf-105">At hello end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="f55cf-106">**CallMethodOnDevice.js**, que chama um método no aplicativo do dispositivo simulado hello e exibe a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55cf-106">**CallMethodOnDevice.js**, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="f55cf-107">**SimulatedDevice.js**, que se conecta tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente e responde toohello método chamado pela nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="f55cf-107">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="f55cf-108">artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun ambos os aplicativos em dispositivos e o back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="f55cf-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="f55cf-109">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55cf-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="f55cf-110">Node.js versão 0.10.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f55cf-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="f55cf-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="f55cf-111">An active Azure account.</span></span> <span data-ttu-id="f55cf-112">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="f55cf-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="f55cf-113">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="f55cf-113">Create a simulated device app</span></span>
<span data-ttu-id="f55cf-114">Nesta seção, você deve criar um aplicativo de console Node. js que responde tooa método chamado pela nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="f55cf-114">In this section, you create a Node.js console app that responds tooa method called by hello cloud.</span></span>

1. <span data-ttu-id="f55cf-115">Crie uma nova pasta vazia denominada **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="f55cf-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="f55cf-116">Em Olá **simulateddevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="f55cf-116">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="f55cf-117">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="f55cf-117">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f55cf-118">O prompt de comando no hello **simulateddevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** pacote do SDK do dispositivo e **azure iot dispositivo-mqtt**pacote:</span><span class="sxs-lookup"><span data-stu-id="f55cf-118">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="f55cf-119">Usando um editor de texto, crie um novo **SimulatedDevice.js** arquivo hello **simulateddevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="f55cf-119">Using a text editor, create a new **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="f55cf-120">Adicione o seguinte Olá `require` instruções no hello início da saudação **SimulatedDevice.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="f55cf-120">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="f55cf-121">Adicionar um **connectionString** variável e use-toocreate uma **DeviceClient** instância.</span><span class="sxs-lookup"><span data-stu-id="f55cf-121">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="f55cf-122">Substituir **{string de conexão do dispositivo}** com a cadeia de conexão de dispositivo Olá gerado na Olá *criar uma identidade de dispositivo* seção:</span><span class="sxs-lookup"><span data-stu-id="f55cf-122">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="f55cf-123">Adicione Olá seguinte método de saudação do tooimplement de função no dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="f55cf-123">Add hello following function tooimplement hello method on hello device:</span></span>
   
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
7. <span data-ttu-id="f55cf-124">Abrir o hub IoT do hello conexão tooyour e começar a inicializar Olá método ouvinte:</span><span class="sxs-lookup"><span data-stu-id="f55cf-124">Open hello connection tooyour IoT hub and start initialize hello method listener:</span></span>
   
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
8. <span data-ttu-id="f55cf-125">Salve e feche o hello **SimulatedDevice.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="f55cf-125">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="f55cf-126">coisas tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="f55cf-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="f55cf-127">No código de produção, você deve implementar políticas de repetição (como tentativas de conexão), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="f55cf-127">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="f55cf-128">Chamar um método em um dispositivo</span><span class="sxs-lookup"><span data-stu-id="f55cf-128">Call a method on a device</span></span>
<span data-ttu-id="f55cf-129">Nesta seção, você deve criar um aplicativo de console Node. js que chama um método no aplicativo do dispositivo simulado hello e, em seguida, exibe a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55cf-129">In this section, you create a Node.js console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="f55cf-130">Crie uma nova pasta vazia denominada **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="f55cf-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="f55cf-131">Em Olá **callmethodondevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="f55cf-131">In hello **callmethodondevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="f55cf-132">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="f55cf-132">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f55cf-133">O prompt de comando no hello **callmethodondevice** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote:</span><span class="sxs-lookup"><span data-stu-id="f55cf-133">At your command prompt in hello **callmethodondevice** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="f55cf-134">Usando um editor de texto, crie um **CallMethodOnDevice.js** arquivo hello **callmethodondevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="f55cf-134">Using a text editor, create a **CallMethodOnDevice.js** file in hello **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="f55cf-135">Adicione o seguinte Olá `require` instruções no hello início da saudação **CallMethodOnDevice.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="f55cf-135">Add hello following `require` statements at hello start of hello **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="f55cf-136">Adicione Olá após a declaração de variável e substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub para o hub:</span><span class="sxs-lookup"><span data-stu-id="f55cf-136">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="f55cf-137">Crie Olá cliente tooopen Olá conexão tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f55cf-137">Create hello client tooopen hello connection tooyour IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="f55cf-138">Adicione Olá função tooinvoke Olá dispositivo método e impressão Olá dispositivo resposta toohello console a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55cf-138">Add hello following function tooinvoke hello device method and print hello device response toohello console:</span></span>
   
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
8. <span data-ttu-id="f55cf-139">Salve e feche o hello **CallMethodOnDevice.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="f55cf-139">Save and close hello **CallMethodOnDevice.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="f55cf-140">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="f55cf-140">Run hello apps</span></span>
<span data-ttu-id="f55cf-141">Agora você está pronto toorun Olá aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f55cf-141">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="f55cf-142">Em um prompt de comando no hello **simulateddevice** pasta, execute Olá escutando chamadas de método do seu IoT Hub de toostart de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55cf-142">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="f55cf-143">Em um prompt de comando no hello **callmethodondevice** pasta, execute Olá toobegin comando seu hub IoT de monitoramento a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55cf-143">At a command prompt in hello **callmethodondevice** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="f55cf-144">Você verá dispositivo Olá reagir toohello método imprimindo mensagem de saudação e o aplicativo hello chamado resposta de Olá Olá método exibição do dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="f55cf-144">You will see hello device react toohello method by printing out hello message and hello application which called hello method display hello response from hello device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="f55cf-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f55cf-145">Next steps</span></span>
<span data-ttu-id="f55cf-146">Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="f55cf-146">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="f55cf-147">Você usou esse dispositivo identidade tooenable Olá simulado dispositivo aplicativo tooreact toomethods invocado pela nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="f55cf-147">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="f55cf-148">Você também criou um aplicativo que chama métodos no dispositivo hello e exibe a resposta de saudação do dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55cf-148">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="f55cf-149">toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="f55cf-149">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="f55cf-150">[Introdução ao Hub IoT]</span><span class="sxs-lookup"><span data-stu-id="f55cf-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="f55cf-151">[Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="f55cf-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="f55cf-152">toolearn como tooextend seu método de solução e agenda IoT chama em vários dispositivos, consulte Olá [agenda e trabalhos de difusão] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="f55cf-152">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
