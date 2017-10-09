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
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="7bff7-104">Introdução ao gerenciamento de dispositivos (Node)</span><span class="sxs-lookup"><span data-stu-id="7bff7-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="7bff7-105">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="7bff7-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="7bff7-106">Use Olá toocreate portal do Azure um IoT Hub e criar uma identidade de dispositivo em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7bff7-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="7bff7-107">Crie um aplicativo de dispositivo simulado contendo um método direto que reinicia o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7bff7-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="7bff7-108">Métodos diretos são chamados de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="7bff7-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="7bff7-109">Crie um aplicativo de console Node. js que chama o método direto de reinicialização Olá no aplicativo do dispositivo simulado Olá por meio de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7bff7-109">Create a Node.js console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="7bff7-110">No final da saudação deste tutorial, você tem dois aplicativos de console Node. js:</span><span class="sxs-lookup"><span data-stu-id="7bff7-110">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="7bff7-111">**dmpatterns_getstarted_device.js**, que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente, recebe um método direto de reinicialização, simula uma reinicialização física e relata o tempo para a última reinicialização do Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="7bff7-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="7bff7-112">**dmpatterns_getstarted_service.js**, que chama um método direto no aplicativo do dispositivo simulado hello, exibe a resposta de saudação e exibe Olá atualizado relatado propriedades.</span><span class="sxs-lookup"><span data-stu-id="7bff7-112">**dmpatterns_getstarted_service.js**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="7bff7-113">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="7bff7-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="7bff7-114">Node.js versão 0.12.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7bff7-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="7bff7-115">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node. js para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="7bff7-115">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="7bff7-116">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="7bff7-116">An active Azure account.</span></span> <span data-ttu-id="7bff7-117">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="7bff7-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="7bff7-118">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="7bff7-118">Create a simulated device app</span></span>
<span data-ttu-id="7bff7-119">Nesta seção, você irá</span><span class="sxs-lookup"><span data-stu-id="7bff7-119">In this section, you will</span></span>

* <span data-ttu-id="7bff7-120">Criar um aplicativo de console do Node. js que responde tooa método direto chamado pela nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="7bff7-120">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="7bff7-121">Disparar uma reinicialização do dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="7bff7-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="7bff7-122">Olá Use relatado propriedades tooenable dispositivos duas consultas tooidentify dispositivos e quando eles reiniciado pela última vez</span><span class="sxs-lookup"><span data-stu-id="7bff7-122">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="7bff7-123">Crie uma pasta vazia denominada **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="7bff7-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="7bff7-124">Em Olá **manageddevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7bff7-124">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="7bff7-125">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="7bff7-125">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7bff7-126">O prompt de comando no hello **manageddevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** pacote do SDK do dispositivo e **azure iot dispositivo-mqtt**pacote:</span><span class="sxs-lookup"><span data-stu-id="7bff7-126">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="7bff7-127">Usando um editor de texto, crie um **dmpatterns_getstarted_device.js** arquivo hello **manageddevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="7bff7-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="7bff7-128">Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **dmpatterns_getstarted_device.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="7bff7-128">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="7bff7-129">Adicionar um **connectionString** variável e use-toocreate uma **cliente** instância.</span><span class="sxs-lookup"><span data-stu-id="7bff7-129">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="7bff7-130">Substitua a cadeia de caracteres de conexão de saudação com a cadeia de caracteres de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7bff7-130">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="7bff7-131">Adicionar Olá seguinte função tooimplement Olá ao método direto no dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="7bff7-131">Add hello following function tooimplement hello direct method on hello device</span></span>
   
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
7. <span data-ttu-id="7bff7-132">Abra o hub IoT do hello conexão tooyour e iniciar o ouvinte de método direto hello:</span><span class="sxs-lookup"><span data-stu-id="7bff7-132">Open hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="7bff7-133">Salve e feche o hello **dmpatterns_getstarted_device.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="7bff7-133">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="7bff7-134">coisas tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="7bff7-134">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="7bff7-135">No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="7bff7-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="7bff7-136">Disparar uma reinicialização remota no dispositivo hello usando um método direto</span><span class="sxs-lookup"><span data-stu-id="7bff7-136">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="7bff7-137">Nesta seção, você criará um aplicativo do console Node.js que inicia uma reinicialização remota em um dispositivo usando um método direto.</span><span class="sxs-lookup"><span data-stu-id="7bff7-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="7bff7-138">aplicativo Hello usa Olá de toodiscover hora da última reinicialização do dispositivo duas consultas para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7bff7-138">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="7bff7-139">Crie uma pasta vazia denominada **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="7bff7-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="7bff7-140">Em Olá **triggerrebootondevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7bff7-140">In hello **triggerrebootondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="7bff7-141">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="7bff7-141">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7bff7-142">O prompt de comando no hello **triggerrebootondevice** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote do SDK do dispositivo e **azure iot dispositivo-mqtt** pacote:</span><span class="sxs-lookup"><span data-stu-id="7bff7-142">At your command prompt in hello **triggerrebootondevice** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="7bff7-143">Usando um editor de texto, crie um **dmpatterns_getstarted_service.js** arquivo hello **triggerrebootondevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="7bff7-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="7bff7-144">Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **dmpatterns_getstarted_service.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="7bff7-144">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="7bff7-145">Adicione Olá declarações de variáveis a seguir e substitua os valores de espaço reservado de saudação:</span><span class="sxs-lookup"><span data-stu-id="7bff7-145">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="7bff7-146">Adicione Olá função tooinvoke Olá dispositivo método tooreboot Olá dispositivo de destino a seguir:</span><span class="sxs-lookup"><span data-stu-id="7bff7-146">Add hello following function tooinvoke hello device method tooreboot hello target device:</span></span>
   
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
7. <span data-ttu-id="7bff7-147">Adicione seguinte Olá função tooquery para dispositivo hello e obter Olá último tempo de reinicialização:</span><span class="sxs-lookup"><span data-stu-id="7bff7-147">Add hello following function tooquery for hello device and get hello last reboot time:</span></span>
   
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
8. <span data-ttu-id="7bff7-148">Adicione Olá seguintes funções de saudação do código toocall que disparam Olá reinicialize método direto e consultar Olá última tempo de reinicialização:</span><span class="sxs-lookup"><span data-stu-id="7bff7-148">Add hello following code toocall hello functions that trigger hello reboot direct method and query for hello last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="7bff7-149">Salve e feche o hello **dmpatterns_getstarted_service.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="7bff7-149">Save and close hello **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="7bff7-150">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="7bff7-150">Run hello apps</span></span>
<span data-ttu-id="7bff7-151">Agora você está pronto toorun Olá aplicativos.</span><span class="sxs-lookup"><span data-stu-id="7bff7-151">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="7bff7-152">No prompt de comando de saudação de saudação **manageddevice** pasta, execute Olá toobegin comando escuta para o método direto de reinicialização Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="7bff7-152">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="7bff7-153">No prompt de comando de saudação de saudação **triggerrebootondevice** pasta, execute Olá após o comando tootrigger Olá remoto reinicializar e consultar para saudação do hello dispositivo duas toofind reinicialize última hora.</span><span class="sxs-lookup"><span data-stu-id="7bff7-153">At hello command prompt in hello **triggerrebootondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="7bff7-154">Consulte o hello dispositivo resposta toohello método direto no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="7bff7-154">You see hello device response toohello direct method in hello console.</span></span>

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
