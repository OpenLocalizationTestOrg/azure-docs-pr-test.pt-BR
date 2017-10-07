---
title: "aaaUse Azure IoT Hub direcionar métodos (.NET/nó) | Microsoft Docs"
description: "Como toouse Azure IoT Hub direta métodos. Você usar o dispositivo de IoT do Azure de saudação SDK para Node.js tooimplement um aplicativo de dispositivo simulado que inclui um método direto e hello serviço IoT do Azure SDK para .NET tooimplement um aplicativo de serviço que invoca o método direto hello."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a>Usar métodos diretos para (.NET/Node)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Neste tutorial, vamos toodevelop .NET e um aplicativo de console Node. js:

* **CallMethodOnDevice.sln**, um aplicativo de back-end .NET, que chama um método no aplicativo do dispositivo simulado hello e exibe a resposta de saudação.
* **SimulatedDevice.js**, um aplicativo Node. js, que simula um dispositivo conectado tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente e responde toohello método chamado pela nuvem hello.

> [!NOTE]
> artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun ambos os aplicativos em dispositivos e o back-end da solução.
> 
> 

toocomplete neste tutorial, você precisa:

* Visual Studio 2015 ou Visual Studio 2017.
* Node.js versão 0.10.x ou posterior.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado
Nesta seção, você deve criar um aplicativo de console Node. js que responde tooa método chamado pela solução de saudação volta final.

1. Crie uma nova pasta vazia denominada **simulateddevice**. Em Olá **simulateddevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação:
   
    ```
    npm init
    ```
2. O prompt de comando no hello **simulateddevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** e **azure iot-dispositivo mqtt** pacotes:
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Usando um editor de texto, crie um arquivo no hello **simulateddevice** pasta e nomeie-o **SimulatedDevice.js**.
4. Adicione o seguinte Olá `require` instruções no hello início da saudação **SimulatedDevice.js** arquivo:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Adicionar um **connectionString** variável e use-toocreate uma **DeviceClient** instância. Substituir **{string de conexão do dispositivo}** com a cadeia de conexão de dispositivo Olá gerado na Olá *criar uma identidade de dispositivo* seção:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Adicione Olá seguinte função tooimplement Olá ao método direto no dispositivo hello:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Abra o hub IoT do hello conexão tooyour e inicializar o ouvinte de método hello:
   
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
8. Salve e feche o hello **SimulatedDevice.js** arquivo.

> [!NOTE]
> coisas tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (como tentativas de conexão), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Chama um método direto em um dispositivo
Nesta seção, você deve criar um aplicativo de console .NET que chama um método no aplicativo do dispositivo simulado hello e, em seguida, exibe a resposta de saudação.

1. No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto. Certifique-se de versão do .NET Framework Olá é 4.5.1 ou posterior. Projeto de saudação do nome **CallMethodOnDevice**.
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][10]
2. No Gerenciador de soluções, clique com botão direito Olá **CallMethodOnDevice** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .
3. Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello. Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.
   
    ![Janela do Gerenciador de Pacotes NuGet][11]

4. Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. Adicionar Olá toohello campos a seguir **programa** classe. Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Adicionar Olá após o método toohello **programa** classe:
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    Este método invoca um método direto com o nome `writeLine` em Olá `myDeviceId` dispositivo. Em seguida, ele grava resposta Olá fornecida pelo dispositivo Olá no console de saudação. Observe como é possível toospecify um valor de tempo limite para Olá dispositivo toorespond.
7. Finalmente, adicione Olá toohello linhas a seguir **principal** método:
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a>Executar aplicativos Olá
Agora você está pronto toorun aplicativos de saudação.

1. Olá Gerenciador de soluções do Visual Studio, com o botão direito sua solução e clique em **definir projetos de inicialização...** . Selecione **único projeto de inicialização**e, em seguida, selecione Olá **CallMethodOnDevice** projeto no menu suspenso de saudação.

2. Em um prompt de comando no hello **simulateddevice** pasta, execute Olá escutando chamadas de método do seu IoT Hub de toostart de comando a seguir:
   
    ```
    node SimulatedDevice.js
    ```
   Aguarde Olá simulado tooopen de dispositivo:![][7]
3. Agora esse dispositivo hello está conectado e esperando para invocações de método, execute Olá .NET **CallMethodOnDevice** método do aplicativo tooinvoke hello no aplicativo do dispositivo simulado hello. Você deve ver a resposta do dispositivo Olá gravada no console de saudação.
   
    ![][8]
4. dispositivo Hello, em seguida, reage toohello método imprimindo esta mensagem:
   
    ![][9]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello. Você usou esse dispositivo identidade tooenable Olá simulado dispositivo aplicativo tooreact toomethods invocado pela nuvem hello. Você também criou um aplicativo que chama métodos no dispositivo hello e exibe a resposta de saudação do dispositivo de saudação. 

toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:

* [Introdução ao Hub IoT]
* [Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]

toolearn como tooextend seu método de solução e agenda IoT chama em vários dispositivos, consulte Olá [agenda e trabalhos de difusão] [ lnk-tutorial-jobs] tutorial.

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Introdução ao Hub IoT]: iot-hub-node-node-getstarted.md
