---
title: "atualização de firmware aaaDevice com o Azure IoT Hub (nó) | Microsoft Docs"
description: "Como atualizar o gerenciamento de dispositivos de toouse no Azure IoT Hub tooinitiate um firmware do dispositivo. Você pode usar hello Azure IoT SDKs para Node. js tooimplement um aplicativo de dispositivo simulado e um aplicativo de serviço que dispara a atualização de firmware de saudação."
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
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="b9a2d-104">Use o gerenciamento de dispositivo tooinitiate uma atualização de firmware do dispositivo (nó nó)</span><span class="sxs-lookup"><span data-stu-id="b9a2d-104">Use device management tooinitiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="b9a2d-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="b9a2d-105">Introduction</span></span>
<span data-ttu-id="b9a2d-106">Em Olá [Introdução ao gerenciamento de dispositivo] [ lnk-dm-getstarted] tutorial, você viu como Olá toouse [duas dispositivo] [ lnk-devtwin] e [direto métodos] [ lnk-c2dmethod] tooremotely primitivos reinicializar um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="b9a2d-107">Este tutorial usa Olá mesmas primitivas de IoT Hub e fornece diretrizes e mostra como toodo uma ponta a ponta simulados atualização de firmware.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-107">This tutorial uses hello same IoT Hub primitives and provides guidance and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="b9a2d-108">Esse padrão é usado na implementação de atualização de firmware de saudação para exemplo de dispositivo Intel Edison hello.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-108">This pattern is used in hello firmware update implementation for hello Intel Edison device sample.</span></span>

<span data-ttu-id="b9a2d-109">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="b9a2d-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="b9a2d-110">Crie um aplicativo de console Node. js que chama o método direto do hello firmwareUpdate no aplicativo do dispositivo simulado Olá por meio de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-110">Create a Node.js console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="b9a2d-111">Criar um aplicativo de dispositivo simulado que implementa um método direto **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="b9a2d-112">Esse método inicia um processo de vários estágio que aguarda a imagem do firmware toodownload hello, baixa a imagem do firmware hello e finalmente se aplica a imagem do firmware hello.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="b9a2d-113">Durante cada fase da atualização hello, Olá dispositivo usa Olá relatado propriedades tooreport em andamento.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="b9a2d-114">No final da saudação deste tutorial, você tem dois aplicativos de console Node. js:</span><span class="sxs-lookup"><span data-stu-id="b9a2d-114">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="b9a2d-115">**dmpatterns_fwupdate_service.js**, que chama um método direto no aplicativo do dispositivo simulado hello, exibe a resposta hello e periodicamente (cada 500 ms) exibe Olá atualizado relatado propriedades.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="b9a2d-116">**dmpatterns_fwupdate_device.js**, que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente, recebe um método firmwareUpdate, é executado por meio de um processo de vários estados toosimulate uma atualização de firmware, incluindo: aguardando Olá Baixar imagem, baixando a nova imagem de saudação e finalmente aplicar imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-116">**dmpatterns_fwupdate_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="b9a2d-117">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9a2d-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b9a2d-118">Node.js versão 0.12.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="b9a2d-119">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node. js para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-119">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="b9a2d-120">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-120">An active Azure account.</span></span> <span data-ttu-id="b9a2d-121">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="b9a2d-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="b9a2d-122">Siga Olá [Introdução ao gerenciamento de dispositivo](iot-hub-node-node-device-management-get-started.md) artigo toocreate seu hub IoT e obter sua cadeia de caracteres de conexão de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-122">Follow hello [Get started with device management](iot-hub-node-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="b9a2d-123">Disparar uma atualização de firmware remota no dispositivo hello usando um método direto</span><span class="sxs-lookup"><span data-stu-id="b9a2d-123">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="b9a2d-124">Nesta seção, você criará um aplicativo do console Node.js que inicia uma atualização remota de firmware em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="b9a2d-125">aplicativo Hello usa uma atualização de saudação do método direto tooinitiate e usa dispositivo duas consultas tooperiodically obter status de saudação de atualização de firmware active hello.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-125">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="b9a2d-126">Crie uma pasta vazia denominada **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="b9a2d-127">Em Olá **triggerfwupdateondevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-127">In hello **triggerfwupdateondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="b9a2d-128">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="b9a2d-128">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b9a2d-129">O prompt de comando no hello **triggerfwupdateondevice** pasta, execute Olá Olá de tooinstall de comando a seguir **hub de iot do azure** e **azure iot-dispositivo mqtt** dispositivo Pacotes do SDK:</span><span class="sxs-lookup"><span data-stu-id="b9a2d-129">At your command prompt in hello **triggerfwupdateondevice** folder, run hello following command tooinstall hello **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="b9a2d-130">Usando um editor de texto, crie um **dmpatterns_getstarted_service.js** arquivo hello **triggerfwupdateondevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="b9a2d-131">Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **dmpatterns_getstarted_service.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="b9a2d-131">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="b9a2d-132">Adicione Olá declarações de variáveis a seguir e substitua os valores de espaço reservado de saudação:</span><span class="sxs-lookup"><span data-stu-id="b9a2d-132">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="b9a2d-133">Adicionar a seguinte Olá toofind de função e exibe valor Olá Olá firmwareUpdate relatados de propriedade.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-133">Add hello following function toofind and display hello value of hello firmwareUpdate reported property.</span></span>
   
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
7. <span data-ttu-id="b9a2d-134">Adicione Olá função tooinvoke Olá firmwareUpdate método tooreboot Olá dispositivo de destino a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9a2d-134">Add hello following function tooinvoke hello firmwareUpdate method tooreboot hello target device:</span></span>
   
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
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="b9a2d-135">Finalmente, a seguir Olá Adicionar função sequência de atualização de firmware do toocode toostart hello e iniciar periodicamente mostrando Olá relatado propriedades:</span><span class="sxs-lookup"><span data-stu-id="b9a2d-135">Finally, Add hello following function toocode toostart hello firmware update sequence and start periodically showing hello reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="b9a2d-136">Salve e feche o hello **dmpatterns_fwupdate_service.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-136">Save and close hello **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="b9a2d-137">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="b9a2d-137">Run hello apps</span></span>
<span data-ttu-id="b9a2d-138">Agora você está pronto toorun Olá aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-138">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="b9a2d-139">No prompt de comando de saudação de saudação **manageddevice** pasta, execute Olá toobegin comando escuta para o método direto de reinicialização Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-139">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="b9a2d-140">No prompt de comando de saudação de saudação **triggerfwupdateondevice** pasta, execute Olá após o comando tootrigger Olá remoto reinicializar e consultar para saudação do hello dispositivo duas toofind reinicialize última hora.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-140">At hello command prompt in hello **triggerfwupdateondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="b9a2d-141">Consulte o hello dispositivo resposta toohello método direto no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-141">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9a2d-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9a2d-142">Next steps</span></span>
<span data-ttu-id="b9a2d-143">Neste tutorial, você usou um método direto de tootrigger remoto atualização de firmware em um dispositivo e Olá usado o progresso de saudação de toofollow propriedades de atualização de firmware de saudação relatado.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-143">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="b9a2d-144">toolearn como tooextend seu método de solução e agenda IoT chama em vários dispositivos, consulte Olá [agenda e trabalhos de difusão] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="b9a2d-144">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
