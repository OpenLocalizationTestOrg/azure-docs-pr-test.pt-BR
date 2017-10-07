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
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a>Use o gerenciamento de dispositivo tooinitiate uma atualização de firmware do dispositivo (nó nó)
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Introdução
Em Olá [Introdução ao gerenciamento de dispositivo] [ lnk-dm-getstarted] tutorial, você viu como Olá toouse [duas dispositivo] [ lnk-devtwin] e [direto métodos] [ lnk-c2dmethod] tooremotely primitivos reinicializar um dispositivo. Este tutorial usa Olá mesmas primitivas de IoT Hub e fornece diretrizes e mostra como toodo uma ponta a ponta simulados atualização de firmware.  Esse padrão é usado na implementação de atualização de firmware de saudação para exemplo de dispositivo Intel Edison hello.

Este tutorial mostra como:

* Crie um aplicativo de console Node. js que chama o método direto do hello firmwareUpdate no aplicativo do dispositivo simulado Olá por meio de seu hub IoT.
* Criar um aplicativo de dispositivo simulado que implementa um método direto **firmwareUpdate**. Esse método inicia um processo de vários estágio que aguarda a imagem do firmware toodownload hello, baixa a imagem do firmware hello e finalmente se aplica a imagem do firmware hello. Durante cada fase da atualização hello, Olá dispositivo usa Olá relatado propriedades tooreport em andamento.

No final da saudação deste tutorial, você tem dois aplicativos de console Node. js:

**dmpatterns_fwupdate_service.js**, que chama um método direto no aplicativo do dispositivo simulado hello, exibe a resposta hello e periodicamente (cada 500 ms) exibe Olá atualizado relatado propriedades.

**dmpatterns_fwupdate_device.js**, que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente, recebe um método firmwareUpdate, é executado por meio de um processo de vários estados toosimulate uma atualização de firmware, incluindo: aguardando Olá Baixar imagem, baixando a nova imagem de saudação e finalmente aplicar imagem de saudação.

toocomplete neste tutorial, você precisa Olá a seguir:

* Node.js versão 0.12.x ou posterior. <br/>  [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node. js para este tutorial no Windows ou Linux.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

Siga Olá [Introdução ao gerenciamento de dispositivo](iot-hub-node-node-device-management-get-started.md) artigo toocreate seu hub IoT e obter sua cadeia de caracteres de conexão de IoT Hub.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Disparar uma atualização de firmware remota no dispositivo hello usando um método direto
Nesta seção, você criará um aplicativo do console Node.js que inicia uma atualização remota de firmware em um dispositivo. aplicativo Hello usa uma atualização de saudação do método direto tooinitiate e usa dispositivo duas consultas tooperiodically obter status de saudação de atualização de firmware active hello.

1. Crie uma pasta vazia denominada **triggerfwupdateondevice**.  Em Olá **triggerfwupdateondevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.  Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **triggerfwupdateondevice** pasta, execute Olá Olá de tooinstall de comando a seguir **hub de iot do azure** e **azure iot-dispositivo mqtt** dispositivo Pacotes do SDK:
   
    ```
    npm install azure-iothub --save
    ```
3. Usando um editor de texto, crie um **dmpatterns_getstarted_service.js** arquivo hello **triggerfwupdateondevice** pasta.
4. Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **dmpatterns_getstarted_service.js** arquivo:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Adicione Olá declarações de variáveis a seguir e substitua os valores de espaço reservado de saudação:
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. Adicionar a seguinte Olá toofind de função e exibe valor Olá Olá firmwareUpdate relatados de propriedade.
   
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
7. Adicione Olá função tooinvoke Olá firmwareUpdate método tooreboot Olá dispositivo de destino a seguir:
   
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
8. Finalmente, a seguir Olá Adicionar função sequência de atualização de firmware do toocode toostart hello e iniciar periodicamente mostrando Olá relatado propriedades:
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. Salve e feche o hello **dmpatterns_fwupdate_service.js** arquivo.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Executar aplicativos Olá
Agora você está pronto toorun Olá aplicativos.

1. No prompt de comando de saudação de saudação **manageddevice** pasta, execute Olá toobegin comando escuta para o método direto de reinicialização Olá a seguir.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. No prompt de comando de saudação de saudação **triggerfwupdateondevice** pasta, execute Olá após o comando tootrigger Olá remoto reinicializar e consultar para saudação do hello dispositivo duas toofind reinicialize última hora.
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. Consulte o hello dispositivo resposta toohello método direto no console de saudação.

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você usou um método direto de tootrigger remoto atualização de firmware em um dispositivo e Olá usado o progresso de saudação de toofollow propriedades de atualização de firmware de saudação relatado.

toolearn como tooextend seu método de solução e agenda IoT chama em vários dispositivos, consulte Olá [agenda e trabalhos de difusão] [ lnk-tutorial-jobs] tutorial.

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
