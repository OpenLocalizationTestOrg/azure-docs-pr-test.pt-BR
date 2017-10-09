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
# <a name="schedule-and-broadcast-jobs-node"></a>Agendar e transmitir trabalhos (Node)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

IoT Hub do Azure é um serviço totalmente gerenciado que permite que um aplicativo de back-end toocreate e trabalhos de controle que agenda e atualizar milhões de dispositivos.  Trabalhos podem ser usados para Olá ações a seguir:

* Atualizar as propriedades desejadas
* Marcas de atualização
* Chamar métodos diretos

Conceitualmente, um trabalho envolve uma dessas ações e rastreia Olá progresso da execução de um conjunto de dispositivos, que é definido por uma consulta de duas do dispositivo.  Por exemplo, um aplicativo de back-end pode usar um trabalho tooinvoke um método de reinicialização em 10.000 dispositivos, especificado por uma consulta de duas do dispositivo e agendadas no futuro.  Esse aplicativo, em seguida, pode controlar o andamento como cada um desses dispositivos recebem e executar o método de reinicialização hello.

Saiba mais sobre cada um desses recursos nestes artigos:

* Duas do dispositivo e propriedades: [Introdução ao twins dispositivo] [ lnk-get-started-twin] e [Tutorial: como dispositivo toouse macros propriedades][lnk-twin-props]
* métodos diretos: [Guia do desenvolvedor do Hub IoT – métodos diretos][lnk-dev-methods] e [Tutorial: métodos diretos][lnk-c2d-methods]

Este tutorial mostra como:

* Criar um aplicativo de dispositivo simulado que tem um método que permite **lockDoor** que pode ser chamado pelo back-end de solução hello.
* Criar um aplicativo de console Node. js que Olá chamadas **lockDoor** método direto no aplicativo do dispositivo simulado hello usando uma saudação de trabalho e atualizações desejado propriedades usando um trabalho do dispositivo.

No final da saudação deste tutorial, você tem dois aplicativos de console Node. js:

**simDevice.js**, que conecta tooyour IoT hub com identidade do dispositivo hello e recebe um **lockDoor** método direto.

**scheduleJobService.js**, que chama um método direto no dispositivo de Olá Olá dispositivo simulado aplicativo e atualizar propriedades desejadas de duas, usando um trabalho.

toocomplete neste tutorial, você precisa Olá a seguir:

* Node.js versão 0.12.x ou posterior. <br/>  [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node. js para este tutorial no Windows ou Linux.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado
Nesta seção, você cria um aplicativo de console Node. js que responde tooa método direto chamado pela nuvem hello, o que dispara uma reinicialização do dispositivo simulado e usa Olá relatado propriedades tooenable dispositivos duas consultas tooidentify dispositivos e quando eles reiniciado pela última vez.

1. Crie uma nova pasta vazia denominada **simDevice**.  Em Olá **simDevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.  Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **simDevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** pacote do SDK do dispositivo e **azure iot-dispositivo mqtt** pacote:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Usando um editor de texto, crie um novo **simDevice.js** arquivo hello **simDevice** pasta.
4. Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **simDevice.js** arquivo:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Adicionar um **connectionString** variável e use-toocreate uma **cliente** instância.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Adicionar Olá Olá de toohandle de função a seguir **lockDoor** método.
   
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
7. Adicionar Olá após código tooregister Olá manipulador Olá **lockDoor** método.
   
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
8. Salve e feche o hello **simDevice.js** arquivo.

> [!NOTE]
> coisas tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a>Agendar trabalhos para chamar um método direto e atualizar as propriedades do dispositivo gêmeo
Nesta seção, você cria um aplicativo de console Node. js que inicia um remoto **lockDoor** em um dispositivo usando as propriedades de um direto método e atualização Olá dispositivo duas.

1. Crie uma nova pasta vazia denominada **scheduleJobService**.  Em Olá **scheduleJobService** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.  Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **scheduleJobService** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote do SDK do dispositivo e **azure iot dispositivo-mqtt**pacote:
   
    ```
    npm install azure-iothub uuid --save
    ```
3. Usando um editor de texto, crie um novo **scheduleJobService.js** arquivo hello **scheduleJobService** pasta.
4. Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **dmpatterns_gscheduleJobServiceetstarted_service.js** arquivo:
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. Adicione Olá declarações de variáveis a seguir e substitua os valores de espaço reservado de saudação:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. Adicione Olá função que será usado toomonitor Olá execução do trabalho de saudação a seguir:
   
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
7. Adicione Olá trabalho de saudação de tooschedule de código que chama o método de dispositivo hello a seguir:
   
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
8. Adicione Olá duas do código tooschedule Olá trabalho tooupdate Olá dispositivo a seguir:
   
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
9. Salve e feche o hello **scheduleJobService.js** arquivo.

## <a name="run-hello-applications"></a>Executar aplicativos Olá
Agora você está pronto toorun aplicativos de saudação.

1. No prompt de comando de saudação de saudação **simDevice** pasta, execute Olá toobegin comando escuta para o método direto de reinicialização Olá a seguir.
   
    ```
    node simDevice.js
    ```
2. No prompt de comando de saudação de saudação **scheduleJobService** pasta, execute Olá após o comando tootrigger Olá trabalhos toolock Olá portas e atualização Olá duas
   
    ```
    node scheduleJobService.js
    ```
3. Consulte o hello dispositivo resposta toohello método direto no console de saudação.

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você usou um trabalho tooschedule um dispositivo de tooa método direto e atualização de saudação das propriedades do duas do dispositivo hello.

toocontinue guia de Introdução ao IoT Hub e padrões de gerenciamento de dispositivo como remoto pela atualização de firmware de ar hello, consulte:

[Tutorial: Como toodo um atualização do firmware][lnk-fwupdate]

toocontinue guia de Introdução ao IoT Hub, consulte [guia de Introdução ao Azure IoT borda][lnk-iot-edge].

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
