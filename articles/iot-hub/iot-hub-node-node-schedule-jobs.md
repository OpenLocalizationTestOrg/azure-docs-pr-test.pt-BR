---
title: "trabalhos de aaaSchedule com o Azure IoT Hub (nó) | Microsoft Docs"
description: "Como tooschedule um Azure IoT Hub trabalho tooinvoke um método direto em vários dispositivos. Você pode usar hello Azure IoT SDKs para aplicativos de dispositivos do Node. js tooimplement Olá simulado e um trabalho de saudação de toorun de aplicativo de serviço."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="2b93a-104">Agendar e transmitir trabalhos (Node)</span><span class="sxs-lookup"><span data-stu-id="2b93a-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="2b93a-105">IoT Hub do Azure é um serviço totalmente gerenciado que permite que um aplicativo de back-end toocreate e trabalhos de controle que agenda e atualizar milhões de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="2b93a-105">Azure IoT Hub is a fully managed service that enables a back-end app toocreate and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="2b93a-106">Trabalhos podem ser usados para Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b93a-106">Jobs can be used for hello following actions:</span></span>

* <span data-ttu-id="2b93a-107">Atualizar as propriedades desejadas</span><span class="sxs-lookup"><span data-stu-id="2b93a-107">Update desired properties</span></span>
* <span data-ttu-id="2b93a-108">Marcas de atualização</span><span class="sxs-lookup"><span data-stu-id="2b93a-108">Update tags</span></span>
* <span data-ttu-id="2b93a-109">Chamar métodos diretos</span><span class="sxs-lookup"><span data-stu-id="2b93a-109">Invoke direct methods</span></span>

<span data-ttu-id="2b93a-110">Conceitualmente, um trabalho envolve uma dessas ações e rastreia Olá progresso da execução de um conjunto de dispositivos, que é definido por uma consulta de duas do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2b93a-110">Conceptually, a job wraps one of these actions and tracks hello progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="2b93a-111">Por exemplo, um aplicativo de back-end pode usar um trabalho tooinvoke um método de reinicialização em 10.000 dispositivos, especificado por uma consulta de duas do dispositivo e agendadas no futuro.</span><span class="sxs-lookup"><span data-stu-id="2b93a-111">For example, a back-end app can use a job tooinvoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="2b93a-112">Esse aplicativo, em seguida, pode controlar o andamento como cada um desses dispositivos recebem e executar o método de reinicialização hello.</span><span class="sxs-lookup"><span data-stu-id="2b93a-112">That application can then track progress as each of those devices receive and execute hello reboot method.</span></span>

<span data-ttu-id="2b93a-113">Saiba mais sobre cada um desses recursos nestes artigos:</span><span class="sxs-lookup"><span data-stu-id="2b93a-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="2b93a-114">Duas do dispositivo e propriedades: [Introdução ao twins dispositivo] [ lnk-get-started-twin] e [Tutorial: como dispositivo toouse macros propriedades][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="2b93a-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="2b93a-115">métodos diretos: [Guia do desenvolvedor do Hub IoT – métodos diretos][lnk-dev-methods] e [Tutorial: métodos diretos][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="2b93a-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="2b93a-116">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="2b93a-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="2b93a-117">Criar um aplicativo de dispositivo simulado que tem um método que permite **lockDoor** que pode ser chamado pelo back-end de solução hello.</span><span class="sxs-lookup"><span data-stu-id="2b93a-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by hello solution back end.</span></span>
* <span data-ttu-id="2b93a-118">Criar um aplicativo de console Node. js que Olá chamadas **lockDoor** método direto no aplicativo do dispositivo simulado hello usando uma saudação de trabalho e atualizações desejado propriedades usando um trabalho do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2b93a-118">Create a Node.js console app that calls hello **lockDoor** direct method in hello simulated device app using a job and updates hello desired properties using a device job.</span></span>

<span data-ttu-id="2b93a-119">No final da saudação deste tutorial, você tem dois aplicativos de console Node. js:</span><span class="sxs-lookup"><span data-stu-id="2b93a-119">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="2b93a-120">**simDevice.js**, que conecta tooyour IoT hub com identidade do dispositivo hello e recebe um **lockDoor** método direto.</span><span class="sxs-lookup"><span data-stu-id="2b93a-120">**simDevice.js**, which connects tooyour IoT hub with hello device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="2b93a-121">**scheduleJobService.js**, que chama um método direto no dispositivo de Olá Olá dispositivo simulado aplicativo e atualizar propriedades desejadas de duas, usando um trabalho.</span><span class="sxs-lookup"><span data-stu-id="2b93a-121">**scheduleJobService.js**, which calls a direct method in hello simulated device app and update hello device twin's desired properties using a job.</span></span>

<span data-ttu-id="2b93a-122">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b93a-122">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="2b93a-123">Node.js versão 0.12.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2b93a-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="2b93a-124">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node. js para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="2b93a-124">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="2b93a-125">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b93a-125">An active Azure account.</span></span> <span data-ttu-id="2b93a-126">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="2b93a-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="2b93a-127">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="2b93a-127">Create a simulated device app</span></span>
<span data-ttu-id="2b93a-128">Nesta seção, você cria um aplicativo de console Node. js que responde tooa método direto chamado pela nuvem hello, o que dispara uma reinicialização do dispositivo simulado e usa Olá relatado propriedades tooenable dispositivos duas consultas tooidentify dispositivos e quando eles reiniciado pela última vez.</span><span class="sxs-lookup"><span data-stu-id="2b93a-128">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="2b93a-129">Crie uma nova pasta vazia denominada **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="2b93a-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="2b93a-130">Em Olá **simDevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="2b93a-130">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="2b93a-131">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="2b93a-131">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2b93a-132">O prompt de comando no hello **simDevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** pacote do SDK do dispositivo e **azure iot-dispositivo mqtt** pacote:</span><span class="sxs-lookup"><span data-stu-id="2b93a-132">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="2b93a-133">Usando um editor de texto, crie um novo **simDevice.js** arquivo hello **simDevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="2b93a-133">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>
4. <span data-ttu-id="2b93a-134">Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **simDevice.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="2b93a-134">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="2b93a-135">Adicionar um **connectionString** variável e use-toocreate uma **cliente** instância.</span><span class="sxs-lookup"><span data-stu-id="2b93a-135">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="2b93a-136">Adicionar Olá Olá de toohandle de função a seguir **lockDoor** método.</span><span class="sxs-lookup"><span data-stu-id="2b93a-136">Add hello following function toohandle hello **lockDoor** method.</span></span>
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. <span data-ttu-id="2b93a-137">Adicionar Olá após código tooregister Olá manipulador Olá **lockDoor** método.</span><span class="sxs-lookup"><span data-stu-id="2b93a-137">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="2b93a-138">Salve e feche o hello **simDevice.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="2b93a-138">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="2b93a-139">coisas tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="2b93a-139">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="2b93a-140">No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="2b93a-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="2b93a-141">Agendar trabalhos para chamar um método direto e atualizar as propriedades do dispositivo gêmeo</span><span class="sxs-lookup"><span data-stu-id="2b93a-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="2b93a-142">Nesta seção, você cria um aplicativo de console Node. js que inicia um remoto **lockDoor** em um dispositivo usando as propriedades de um direto método e atualização Olá dispositivo duas.</span><span class="sxs-lookup"><span data-stu-id="2b93a-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update hello device twin's properties.</span></span>

1. <span data-ttu-id="2b93a-143">Crie uma nova pasta vazia denominada **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="2b93a-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="2b93a-144">Em Olá **scheduleJobService** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="2b93a-144">In hello **scheduleJobService** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="2b93a-145">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="2b93a-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2b93a-146">O prompt de comando no hello **scheduleJobService** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote do SDK do dispositivo e **azure iot dispositivo-mqtt**pacote:</span><span class="sxs-lookup"><span data-stu-id="2b93a-146">At your command prompt in hello **scheduleJobService** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="2b93a-147">Usando um editor de texto, crie um novo **scheduleJobService.js** arquivo hello **scheduleJobService** pasta.</span><span class="sxs-lookup"><span data-stu-id="2b93a-147">Using a text editor, create a new **scheduleJobService.js** file in hello **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="2b93a-148">Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **dmpatterns_gscheduleJobServiceetstarted_service.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="2b93a-148">Add hello following 'require' statements at hello start of hello **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="2b93a-149">Adicione Olá declarações de variáveis a seguir e substitua os valores de espaço reservado de saudação:</span><span class="sxs-lookup"><span data-stu-id="2b93a-149">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="2b93a-150">Adicione Olá função que será usado toomonitor Olá execução do trabalho de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b93a-150">Add hello following function that will be used toomonitor hello execution of hello job:</span></span>
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. <span data-ttu-id="2b93a-151">Adicione Olá trabalho de saudação de tooschedule de código que chama o método de dispositivo hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b93a-151">Add hello following code tooschedule hello job that calls hello device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. <span data-ttu-id="2b93a-152">Adicione Olá duas do código tooschedule Olá trabalho tooupdate Olá dispositivo a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b93a-152">Add hello following code tooschedule hello job tooupdate hello device twin:</span></span>
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. <span data-ttu-id="2b93a-153">Salve e feche o hello **scheduleJobService.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="2b93a-153">Save and close hello **scheduleJobService.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="2b93a-154">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="2b93a-154">Run hello applications</span></span>
<span data-ttu-id="2b93a-155">Agora você está pronto toorun aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b93a-155">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="2b93a-156">No prompt de comando de saudação de saudação **simDevice** pasta, execute Olá toobegin comando escuta para o método direto de reinicialização Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="2b93a-156">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="2b93a-157">No prompt de comando de saudação de saudação **scheduleJobService** pasta, execute Olá após o comando tootrigger Olá trabalhos toolock Olá portas e atualização Olá duas</span><span class="sxs-lookup"><span data-stu-id="2b93a-157">At hello command prompt in hello **scheduleJobService** folder, run hello following command tootrigger hello jobs toolock hello door and update hello twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="2b93a-158">Consulte o hello dispositivo resposta toohello método direto no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b93a-158">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b93a-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b93a-159">Next steps</span></span>
<span data-ttu-id="2b93a-160">Neste tutorial, você usou um trabalho tooschedule um dispositivo de tooa método direto e atualização de saudação das propriedades do duas do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="2b93a-160">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="2b93a-161">toocontinue guia de Introdução ao IoT Hub e padrões de gerenciamento de dispositivo como remoto pela atualização de firmware de ar hello, consulte:</span><span class="sxs-lookup"><span data-stu-id="2b93a-161">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, see:</span></span>

<span data-ttu-id="2b93a-162">[Tutorial: Como toodo um atualização do firmware][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="2b93a-162">[Tutorial: How toodo a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="2b93a-163">toocontinue guia de Introdução ao IoT Hub, consulte [guia de Introdução ao Azure IoT borda][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="2b93a-163">toocontinue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
