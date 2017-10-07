---
title: "atualização de firmware aaaDevice com o Azure IoT Hub (.NET/nó) | Microsoft Docs"
description: "Como atualizar o gerenciamento de dispositivos de toouse no Azure IoT Hub tooinitiate um firmware do dispositivo. Use o dispositivo de IoT do Azure de saudação SDK para Node.js tooimplement um aplicativo de dispositivo simulado e Olá serviço IoT do Azure SDK para .NET tooimplement um aplicativo de serviço que dispara a atualização de firmware de saudação."
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
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a>Use o gerenciamento de dispositivo tooinitiate uma atualização de firmware do dispositivo (.NET/nó)
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Introdução
Em Olá [Introdução ao gerenciamento de dispositivo] [ lnk-dm-getstarted] tutorial, você viu como Olá toouse [duas dispositivo] [ lnk-devtwin] e [direto métodos] [ lnk-c2dmethod] tooremotely primitivos reinicializar um dispositivo. Este tutorial usa Olá mesmas primitivas de Hub IoT e mostra como toodo uma ponta a ponta simulados atualização de firmware.  Esse padrão é usado na implementação de atualização de firmware Olá Olá [exemplo de implementação de dispositivo de Pi framboesa][lnk-rpi-implementation].

Este tutorial mostra como:

* Crie um aplicativo de console .NET que chama o método direto do hello firmwareUpdate no aplicativo do dispositivo simulado Olá por meio de seu hub IoT.
* Criar um aplicativo de dispositivo simulado que implementa um método direto **firmwareUpdate**. Esse método inicia um processo de vários estágio que aguarda a imagem do firmware toodownload hello, baixa a imagem do firmware hello e finalmente se aplica a imagem do firmware hello. Durante cada fase da atualização hello, Olá dispositivo usa Olá relatado propriedades tooreport em andamento.

No final da saudação deste tutorial, você tem um aplicativo de dispositivo do console Node. js e um aplicativo de back-end do console .NET (c#):

**dmpatterns_fwupdate_service.js**, que chama um método direto no aplicativo do dispositivo simulado hello, exibe a resposta hello e periodicamente (cada 500 ms) exibe Olá atualizado relatado propriedades.

**TriggerFWUpdate**, que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente, recebe um método firmwareUpdate, é executado por meio de um processo de vários estados toosimulate uma atualização de firmware, incluindo: aguardando o download da imagem Olá, Baixando Olá nova imagem e finalmente aplicar imagem de saudação.

toocomplete neste tutorial, você precisa Olá a seguir:

* Visual Studio 2015 ou Visual Studio 2017.
* Node.js versão 0.12.x ou posterior. <br/>  [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node. js para este tutorial no Windows ou Linux.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

Siga Olá [Introdução ao gerenciamento de dispositivo](iot-hub-csharp-node-device-management-get-started.md) artigo toocreate seu hub IoT e obter sua cadeia de caracteres de conexão de IoT Hub.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Disparar uma atualização de firmware remota no dispositivo hello usando um método direto
Nesta seção, você criará um aplicativo do console .NET (usando C#) que inicia uma atualização remota de firmware em um dispositivo. aplicativo Hello usa uma atualização de saudação do método direto tooinitiate e usa dispositivo duas consultas tooperiodically obter status de saudação de atualização de firmware active hello.

1. No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto. Projeto de saudação do nome **TriggerFWUpdate**.

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]

1. No Gerenciador de soluções, clique com botão direito Olá **TriggerFWUpdate** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .
1. Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello. Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.

    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. Adicionar Olá toohello campos a seguir **programa** classe. Substitua Olá Olá de vários valores de espaço reservado com cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello e hello Id do dispositivo.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. Adicionar Olá após o método toohello **programa** classe:
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. Adicionar Olá após o método toohello **programa** classe:

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. Finalmente, adicione Olá toohello linhas a seguir **principal** método:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. Olá Gerenciador de soluções, abra o hello **projetos de inicialização definido...**  e certifique-se de saudação **ação** para **TriggerFWUpdate** projeto é **iniciar**.

1. Compile a solução de saudação.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Executar aplicativos Olá
Agora você está pronto toorun Olá aplicativos.

1. No prompt de comando de saudação de saudação **manageddevice** pasta, execute Olá toobegin comando escuta para o método direto de reinicialização Olá a seguir.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. No Visual Studio, clique em Olá **TriggerFWUpdate** aplicativo de console toohello c# projectRun, selecione **depurar** e **iniciar nova instância**.

3. Consulte o hello dispositivo resposta toohello método direto no console de saudação.

    ![Firmware atualizado com êxito][img-fwupdate]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você usou um método direto de tootrigger remoto atualização de firmware em um dispositivo e Olá usado o progresso de saudação de toofollow propriedades de atualização de firmware de saudação relatado.

toolearn como tooextend seu método de solução e agenda IoT chama em vários dispositivos, consulte Olá [agenda e trabalhos de difusão] [ lnk-tutorial-jobs] tutorial.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/