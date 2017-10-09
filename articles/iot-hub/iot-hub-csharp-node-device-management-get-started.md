---
title: "aaaGet de Introdução ao gerenciamento de dispositivos do Azure IoT Hub (.NET/nó) | Microsoft Docs"
description: "Como tooinitiate de gerenciamento de dispositivo de Azure IoT Hub toouse um dispositivo remoto reinicializar. Você usar o dispositivo de IoT do Azure de saudação SDK para Node.js tooimplement um aplicativo de dispositivo simulado que inclui um método direto e hello serviço IoT do Azure SDK para .NET tooimplement um aplicativo de serviço que invoca o método direto hello."
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
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a>Introdução ao gerenciamento de dispositivos (.NET/Node)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Este tutorial mostra como:

* Use Olá toocreate portal do Azure um IoT Hub e criar uma identidade de dispositivo em seu hub IoT.
* Crie um aplicativo de dispositivo simulado contendo um método direto que reinicia o dispositivo. Métodos diretos são chamados de nuvem hello.
* Crie um aplicativo de console .NET que chama o método direto de reinicialização Olá no aplicativo do dispositivo simulado Olá por meio de seu hub IoT.

No final da saudação deste tutorial, você tem um aplicativo de dispositivo do console Node. js e um aplicativo de back-end do console .NET (c#):

**dmpatterns_getstarted_device.js**, que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente, recebe um método direto de reinicialização, simula uma reinicialização física e relata o tempo para a última reinicialização do Olá Olá.

**TriggerReboot**, que chama um método direto no aplicativo do dispositivo simulado hello, exibe a resposta de saudação e exibe Olá atualizado relatado propriedades.

toocomplete neste tutorial, você precisa Olá a seguir:

* Visual Studio 2015 ou Visual Studio 2017.
* Node.js versão 0.12.x ou posterior. <br/>  [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node. js para este tutorial no Windows ou Linux.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Disparar uma reinicialização remota no dispositivo hello usando um método direto
Nesta seção, você criará um aplicativo do console .NET (usando C#) que inicia uma reinicialização remota em um dispositivo usando um método direto. aplicativo Hello usa Olá de toodiscover hora da última reinicialização do dispositivo duas consultas para o dispositivo.

1. No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto tooa novo usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto. Certifique-se de versão do .NET Framework Olá é 4.5.1 ou posterior. Projeto de saudação do nome **TriggerReboot**.

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]

2. No Gerenciador de soluções, clique com botão direito Olá **TriggerReboot** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.
3. Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello. Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.

    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
4. Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. Adicionar Olá toohello campos a seguir **programa** classe. Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello e o dispositivo de destino de saudação.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. Adicionar Olá após o método toohello **programa** classe.  Este dispositivo duas do código obtém Olá para Olá Olá dispositivo e saídas de reinicialização relatado propriedades.
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. Adicionar Olá após o método toohello **programa** classe.  Esse código inicia Olá reinicialização no dispositivo hello usando um método direto.

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. Finalmente, adicione Olá toohello linhas a seguir **principal** método:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. Compile a solução de saudação.

## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado
Nesta seção, você irá

* Criar um aplicativo de console do Node. js que responde tooa método direto chamado pela nuvem Olá
* Disparar uma reinicialização do dispositivo simulado
* Olá Use relatado propriedades tooenable dispositivos duas consultas tooidentify dispositivos e quando eles reiniciado pela última vez

1. Criar uma nova pasta vazia denominada **manageddevice**.  Em Olá **manageddevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.  Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **manageddevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** pacote do SDK do dispositivo e **azure iot dispositivo-mqtt**pacote:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Usando um editor de texto, crie um novo **dmpatterns_getstarted_device.js** arquivo hello **manageddevice** pasta.
4. Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **dmpatterns_getstarted_device.js** arquivo:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Adicionar um **connectionString** variável e use-toocreate uma **cliente** instância.  Substitua a cadeia de caracteres de conexão de saudação com a cadeia de caracteres de conexão do dispositivo.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Adicionar Olá seguinte função tooimplement Olá ao método direto no dispositivo Olá
   
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
7. Adicione o seguinte Olá hub IoT do tooopen Olá conexão tooyour de código e iniciar o ouvinte de método direto de saudação:
   
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
8. Salve e feche o hello **dmpatterns_getstarted_device.js** arquivo.
   
> [!NOTE]
> coisas tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].


## <a name="run-hello-apps"></a>Executar aplicativos Olá
Agora você está pronto toorun Olá aplicativos.

1. No prompt de comando de saudação de saudação **manageddevice** pasta, execute Olá toobegin comando escuta para o método direto de reinicialização Olá a seguir.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Aplicativo de console Olá execução c# **TriggerReboot**. Saudação de atalho **TriggerReboot** projeto, selecione **depurar**e, em seguida, selecione **iniciar nova instância**.

3. Consulte o hello dispositivo resposta toohello método direto no console de saudação.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/