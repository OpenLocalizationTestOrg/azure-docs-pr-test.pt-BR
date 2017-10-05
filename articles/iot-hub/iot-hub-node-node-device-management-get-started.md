---
title: "Introdução ao gerenciamento de dispositivo do Hub IoT do Azure (Node) | Microsoft Docs"
description: "Como usar o gerenciamento de dispositivos do Hub IoT para iniciar uma reinicialização do dispositivo remoto. Use o SDK do IoT do Azure para Node.js para implementar um aplicativo de dispositivo simulado que inclui um método direto e um aplicativo de serviço que invoca o método direto."
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
ms.openlocfilehash: 332a3e62cb1ef75e2c6dd5562ee799465c401128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="a85a1-104">Introdução ao gerenciamento de dispositivos (Node)</span><span class="sxs-lookup"><span data-stu-id="a85a1-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="a85a1-105">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="a85a1-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="a85a1-106">Usar o portal do Azure para criar um Hub IoT e criar uma identidade de dispositivo em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a85a1-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="a85a1-107">Crie um aplicativo de dispositivo simulado contendo um método direto que reinicia o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a85a1-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="a85a1-108">Métodos diretos são invocados da nuvem.</span><span class="sxs-lookup"><span data-stu-id="a85a1-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="a85a1-109">Criar um aplicativo de console Node.js que chama um método direto de reinicialização no aplicativo de dispositivo simulado por meio do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a85a1-109">Create a Node.js console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="a85a1-110">Ao fim deste tutorial, você terá dois aplicativos de console do Node.js:</span><span class="sxs-lookup"><span data-stu-id="a85a1-110">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="a85a1-111">**dmpatterns_getstarted_device.js**, que conecta seu hub IoT com a identidade do dispositivo criada anteriormente, recebe um método direto de reinicialização, simula uma reinicialização física e informa a hora da última reinicialização.</span><span class="sxs-lookup"><span data-stu-id="a85a1-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="a85a1-112">**dmpatterns_getstarted_service.js**, que chama um método direto no aplicativo do dispositivo simulado, exibe a resposta e exibe as propriedades relatadas atualizadas.</span><span class="sxs-lookup"><span data-stu-id="a85a1-112">**dmpatterns_getstarted_service.js**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="a85a1-113">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="a85a1-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="a85a1-114">Node.js versão 0.12.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a85a1-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="a85a1-115">[Preparar o ambiente de desenvolvimento][lnk-dev-setup] descreve como instalar o Node.js para este tutorial no Windows ou no Linux.</span><span class="sxs-lookup"><span data-stu-id="a85a1-115">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a85a1-116">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a85a1-116">An active Azure account.</span></span> <span data-ttu-id="a85a1-117">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="a85a1-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a85a1-118">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="a85a1-118">Create a simulated device app</span></span>
<span data-ttu-id="a85a1-119">Nesta seção, você irá</span><span class="sxs-lookup"><span data-stu-id="a85a1-119">In this section, you will</span></span>

* <span data-ttu-id="a85a1-120">Criar um aplicativo de console do Node.js que responde a um método direto chamado pela nuvem</span><span class="sxs-lookup"><span data-stu-id="a85a1-120">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="a85a1-121">Disparar uma reinicialização do dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="a85a1-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="a85a1-122">Usar as propriedades relatadas para habilitar consultas de dispositivo gêmeo para identificar dispositivos e a última reinicialização</span><span class="sxs-lookup"><span data-stu-id="a85a1-122">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="a85a1-123">Crie uma pasta vazia denominada **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="a85a1-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="a85a1-124">Na pasta **manageddevice**, crie um arquivo package.json usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="a85a1-124">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="a85a1-125">Aceite todos os padrões:</span><span class="sxs-lookup"><span data-stu-id="a85a1-125">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a85a1-126">No prompt de comando na pasta **manageddevice**, execute o seguinte comando para instalar o pacote **azure-iot-device** do SDK do Dispositivo e o pacote **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="a85a1-126">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="a85a1-127">Usando um editor de texto, crie um arquivo **dmpatterns_getstarted_device.js** na pasta **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="a85a1-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="a85a1-128">Adicione as seguintes instruções ‘require’ no início do arquivo **dmpatterns_getstarted_device.js**:</span><span class="sxs-lookup"><span data-stu-id="a85a1-128">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="a85a1-129">Adicione uma variável **connectionString** e use-a para criar um **Cliente** do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a85a1-129">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="a85a1-130">Substitua a cadeia de conexão de dispositivo pela cadeia de conexão do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a85a1-130">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="a85a1-131">Adicione a seguinte função para implementar o método direto no dispositivo</span><span class="sxs-lookup"><span data-stu-id="a85a1-131">Add the following function to implement the direct method on the device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
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
7. <span data-ttu-id="a85a1-132">Abra a conexão com o Hub IoT e inicie o ouvinte do método direto:</span><span class="sxs-lookup"><span data-stu-id="a85a1-132">Open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="a85a1-133">Salve e feche o arquivo **dmpatterns_getstarted_device.js**.</span><span class="sxs-lookup"><span data-stu-id="a85a1-133">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="a85a1-134">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="a85a1-134">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="a85a1-135">No código de produção, implemente políticas de repetição (como uma retirada exponencial), como sugerido no artigo [Tratamento de falhas transitórias][lnk-transient-faults] do MSDN.</span><span class="sxs-lookup"><span data-stu-id="a85a1-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="a85a1-136">Disparar uma reinicialização remota no dispositivo usando um método direto</span><span class="sxs-lookup"><span data-stu-id="a85a1-136">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="a85a1-137">Nesta seção, você criará um aplicativo do console Node.js que inicia uma reinicialização remota em um dispositivo usando um método direto.</span><span class="sxs-lookup"><span data-stu-id="a85a1-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="a85a1-138">O aplicativo usa consultas de dispositivo gêmeo para descobrir o último horário de reinicialização para esse dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a85a1-138">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="a85a1-139">Crie uma pasta vazia denominada **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="a85a1-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="a85a1-140">Na pasta **triggerrebootondevice**, crie um arquivo package.json usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="a85a1-140">In the **triggerrebootondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="a85a1-141">Aceite todos os padrões:</span><span class="sxs-lookup"><span data-stu-id="a85a1-141">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a85a1-142">No prompt de comando, na pasta **triggerrebootondevice**, execute o seguinte comando para instalar o pacote **azure-iothub** do SDK do Dispositivo e o pacote **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="a85a1-142">At your command prompt in the **triggerrebootondevice** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="a85a1-143">Usando um editor de texto, crie um arquivo **dmpatterns_getstarted_service.js** na pasta **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="a85a1-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="a85a1-144">Adicione as seguintes instruções "require" no início do arquivo **dmpatterns_getstarted_service.js**:</span><span class="sxs-lookup"><span data-stu-id="a85a1-144">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="a85a1-145">Adicione as seguintes declarações de variável e substitua os valores de espaço reservado:</span><span class="sxs-lookup"><span data-stu-id="a85a1-145">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="a85a1-146">Adicione a seguinte função para invocar o método do dispositivo para reiniciar o dispositivo de destino:</span><span class="sxs-lookup"><span data-stu-id="a85a1-146">Add the following function to invoke the device method to reboot the target device:</span></span>
   
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
                console.log("Successfully invoked the device to reboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="a85a1-147">Adicione a seguinte função para consultar o dispositivo e obter a hora da última reinicialização:</span><span class="sxs-lookup"><span data-stu-id="a85a1-147">Add the following function to query for the device and get the last reboot time:</span></span>
   
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
                console.log('Waiting for device to report last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="a85a1-148">Adicione o seguinte código para chamar as funções que dispararão o método direto de reinicialização e consultarão a hora da última reinicialização:</span><span class="sxs-lookup"><span data-stu-id="a85a1-148">Add the following code to call the functions that trigger the reboot direct method and query for the last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="a85a1-149">Salve e feche o arquivo **dmpatterns_getstarted_service.js**.</span><span class="sxs-lookup"><span data-stu-id="a85a1-149">Save and close the **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="a85a1-150">Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="a85a1-150">Run the apps</span></span>
<span data-ttu-id="a85a1-151">Agora você está pronto para executar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a85a1-151">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="a85a1-152">No prompt de comando da pasta **manageddevice**, execute o seguinte comando para iniciar a escutar o método direto de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="a85a1-152">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="a85a1-153">No prompt de comando da pasta **triggerrebootondevice**, execute o seguinte comando para disparar a reinicialização e a consulta remota para o dispositivo gêmeo localizar o tempo de reinicialização mais recente.</span><span class="sxs-lookup"><span data-stu-id="a85a1-153">At the command prompt in the **triggerrebootondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="a85a1-154">Você verá a resposta do dispositivo para o método direto no console.</span><span class="sxs-lookup"><span data-stu-id="a85a1-154">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
