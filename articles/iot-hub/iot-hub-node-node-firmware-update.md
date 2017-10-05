---
title: "Atualização de firmware do dispositivo com o Hub IoT do Azure (Node) | Microsoft Docs"
description: "Como usar o gerenciamento de dispositivos no Hub IoT do Azure para iniciar uma atualização de firmware do dispositivo. Use os SDKs do IoT do Azure para Node.js para implementar um aplicativo de dispositivo simulado e um aplicativo de serviço que dispara a atualização do firmware."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 350cf1cbec8847d1bbf29814435502af6f098e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="aaf66-104">Usar o gerenciamento de dispositivos para iniciar uma atualização de firmware do dispositivo (Node/Node)</span><span class="sxs-lookup"><span data-stu-id="aaf66-104">Use device management to initiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="aaf66-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="aaf66-105">Introduction</span></span>
<span data-ttu-id="aaf66-106">No tutorial [Introdução ao gerenciamento de dispositivo][lnk-dm-getstarted], você viu como usar os primitivos [dispositivo gêmeo][lnk-devtwin] e [métodos diretos][lnk-c2dmethod] para reiniciar remotamente um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aaf66-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="aaf66-107">Este tutorial usa os mesmos primitivos do Hub IoT, fornece orientações e mostra como fazer uma atualização de firmware simulada de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="aaf66-107">This tutorial uses the same IoT Hub primitives and provides guidance and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="aaf66-108">Esse padrão é usado na implementação da atualização de firmware para o dispositivo de exemplo Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="aaf66-108">This pattern is used in the firmware update implementation for the Intel Edison device sample.</span></span>

<span data-ttu-id="aaf66-109">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="aaf66-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="aaf66-110">Criar um aplicativo de console Node.js que chama o método direto firmwareUpdate no aplicativo de dispositivo simulado por meio do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aaf66-110">Create a Node.js console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="aaf66-111">Criar um aplicativo de dispositivo simulado que implementa um método direto **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="aaf66-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="aaf66-112">Esse método inicia um processo de várias etapas que aguarda o download, baixa e aplica a imagem do firmware.</span><span class="sxs-lookup"><span data-stu-id="aaf66-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="aaf66-113">Durante cada etapa da atualização, o dispositivo usa as propriedades relatadas para informar sobre o progresso.</span><span class="sxs-lookup"><span data-stu-id="aaf66-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="aaf66-114">Ao fim deste tutorial, você terá dois aplicativos de console do Node.js:</span><span class="sxs-lookup"><span data-stu-id="aaf66-114">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="aaf66-115">**dmpatterns_fwupdate_service.js**, que chama um método direto no aplicativo do dispositivo simulado, exibe a resposta e periodicamente (a cada 500 ms) exibe as propriedades relatadas atualizadas.</span><span class="sxs-lookup"><span data-stu-id="aaf66-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="aaf66-116">**dmpatterns_fwupdate_device.js**, que se conecta ao seu Hub IoT com a identidade do dispositivo criada anteriormente, recebe um método direto firmwareUpdate, é executado por meio de um processo de vários estados para simular uma atualização de firmware, incluindo: aguardar o download da imagem, baixar a nova imagem e aplicar a imagem.</span><span class="sxs-lookup"><span data-stu-id="aaf66-116">**dmpatterns_fwupdate_device.js**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="aaf66-117">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="aaf66-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="aaf66-118">Node.js versão 0.12.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="aaf66-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="aaf66-119">[Preparar o ambiente de desenvolvimento][lnk-dev-setup] descreve como instalar o Node.js para este tutorial no Windows ou no Linux.</span><span class="sxs-lookup"><span data-stu-id="aaf66-119">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="aaf66-120">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf66-120">An active Azure account.</span></span> <span data-ttu-id="aaf66-121">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="aaf66-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="aaf66-122">Consulte o artigo [Introdução ao gerenciamento de dispositivo](iot-hub-node-node-device-management-get-started.md) para criar seu hub IoT e obter a cadeia de conexão dele.</span><span class="sxs-lookup"><span data-stu-id="aaf66-122">Follow the [Get started with device management](iot-hub-node-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="aaf66-123">Disparar uma atualização de firmware remoto no dispositivo usando um método direto</span><span class="sxs-lookup"><span data-stu-id="aaf66-123">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="aaf66-124">Nesta seção, você criará um aplicativo do console Node.js que inicia uma atualização remota de firmware em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aaf66-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="aaf66-125">O aplicativo utiliza um método direto para iniciar a atualização e usa consultas em dispositivos gêmeos para receber periodicamente o status da atualização do firmware ativo.</span><span class="sxs-lookup"><span data-stu-id="aaf66-125">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="aaf66-126">Crie uma pasta vazia denominada **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="aaf66-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="aaf66-127">Na pasta **triggerfwupdateondevice**, crie um arquivo package.json usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="aaf66-127">In the **triggerfwupdateondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="aaf66-128">Aceite todos os padrões:</span><span class="sxs-lookup"><span data-stu-id="aaf66-128">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="aaf66-129">No prompt de comando na pasta **triggerfwupdateondevice**, execute o seguinte comando para instalar os pacotes do SDK do Dispositivo **azure-iot-hub** e **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="aaf66-129">At your command prompt in the **triggerfwupdateondevice** folder, run the following command to install the **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="aaf66-130">Usando um editor de texto, crie um arquivo **dmpatterns_getstarted_service.js** na pasta **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="aaf66-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="aaf66-131">Adicione as seguintes instruções "require" no início do arquivo **dmpatterns_getstarted_service.js**:</span><span class="sxs-lookup"><span data-stu-id="aaf66-131">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="aaf66-132">Adicione as seguintes declarações de variável e substitua os valores de espaço reservado:</span><span class="sxs-lookup"><span data-stu-id="aaf66-132">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="aaf66-133">Adicione a seguinte função para localizar e exibir o valor da propriedade relatada firmwareUpdate.</span><span class="sxs-lookup"><span data-stu-id="aaf66-133">Add the following function to find and display the value of the firmwareUpdate reported property.</span></span>
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. <span data-ttu-id="aaf66-134">Adicione a seguinte função para invocar o método firmwareUpdate para reiniciar o dispositivo de destino:</span><span class="sxs-lookup"><span data-stu-id="aaf66-134">Add the following function to invoke the firmwareUpdate method to reboot the target device:</span></span>
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start the firmware update on the device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="aaf66-135">Por fim, adicione a seguinte função ao código para iniciar a sequência de atualização do firmware e começar a mostrar periodicamente as propriedades relatadas:</span><span class="sxs-lookup"><span data-stu-id="aaf66-135">Finally, Add the following function to code to start the firmware update sequence and start periodically showing the reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="aaf66-136">Salve e feche o arquio **dmpatterns_fwupdate_service.js**.</span><span class="sxs-lookup"><span data-stu-id="aaf66-136">Save and close the **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="aaf66-137">Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="aaf66-137">Run the apps</span></span>
<span data-ttu-id="aaf66-138">Agora você está pronto para executar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="aaf66-138">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="aaf66-139">No prompt de comando da pasta **manageddevice**, execute o seguinte comando para iniciar a escutar o método direto de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="aaf66-139">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="aaf66-140">No prompt de comando da pasta **triggerfwupdateondevice**, execute o seguinte comando para disparar a reinicialização e a consulta remota para o dispositivo gêmeo localizar o tempo de reinicialização mais recente.</span><span class="sxs-lookup"><span data-stu-id="aaf66-140">At the command prompt in the **triggerfwupdateondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="aaf66-141">Você verá a resposta do dispositivo para o método direto no console.</span><span class="sxs-lookup"><span data-stu-id="aaf66-141">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaf66-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aaf66-142">Next steps</span></span>
<span data-ttu-id="aaf66-143">Neste tutorial, você usou um método direto para disparar uma atualização remota de firmware em um dispositivo e utilizou as propriedades relatadas para acompanhar o andamento da atualização do firmware.</span><span class="sxs-lookup"><span data-stu-id="aaf66-143">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="aaf66-144">Para saber como estender sua solução de IoT e agendar chamadas de método em vários dispositivos, confira o tutorial [Agendar e difundir trabalhos][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="aaf66-144">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
