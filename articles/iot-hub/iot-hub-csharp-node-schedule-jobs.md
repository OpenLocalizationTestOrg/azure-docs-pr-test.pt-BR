---
title: "trabalhos de aaaSchedule com o Azure IoT Hub (.NET/nó) | Microsoft Docs"
description: "Como tooschedule um Azure IoT Hub trabalho tooinvoke um método direto em vários dispositivos. Você pode usar dispositivo IoT do Azure de saudação SDK para aplicativos de dispositivos do Node. js tooimplement Olá simulado e hello serviço IoT do Azure SDK para .NET tooimplement um trabalho de saudação de toorun de aplicativo de serviço."
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
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a>Agendar e difundir trabalhos (.NET/Node.js)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Use trabalhos Azure IoT Hub tooschedule e rastrear que atualizam milhões de dispositivos. Use trabalhos para:

* Atualizar as propriedades desejadas
* Marcas de atualização
* Chamar métodos diretos

Um trabalho envolve uma dessas ações e rastreia Olá execução em um conjunto de dispositivos que é definido por uma consulta de duas do dispositivo. Por exemplo, um aplicativo de back-end pode usar um trabalho tooinvoke um método direto em 10.000 dispositivos que reinicia dispositivos hello. Você especifica o conjunto de saudação de dispositivos com uma consulta de duas do dispositivo e agenda Olá trabalho toorun no futuro. Olá trabalho rastreia progresso como cada um dos dispositivos de saudação receber e executar o método direto de reinicialização hello.

toolearn mais sobre cada um desses recursos, consulte:

* Duas do dispositivo e propriedades: [Introdução ao twins dispositivo] [ lnk-get-started-twin] e [Tutorial: como dispositivo toouse macros propriedades][lnk-twin-props]
* Métodos diretos: [Guia do desenvolvedor do Hub IoT – métodos diretos][lnk-dev-methods] e [Tutorial: Usar métodos diretos][lnk-c2d-methods]

Este tutorial mostra como:

* Criar um aplicativo de dispositivo que implementa um método chamado **lockDoor** que pode ser chamado pelo aplicativo de back-end de saudação. aplicativo de dispositivo Olá também recebe alterações de propriedade desejados do aplicativo de back-end de saudação.
* Criar um aplicativo de back-end que cria uma saudação do trabalho toocall **lockDoor** método direto em vários dispositivos. Outro trabalho envia toomultiple dispositivos de atualizações de propriedade desejados.

No final da saudação deste tutorial, você tem um aplicativo de dispositivo do console Node. js e um aplicativo de back-end do console .NET (c#):

**simDevice.js** que se conecta tooyour IoT hub, implementa Olá **lockDoor** direcionar o método e manipula desejado alterações de propriedade.

**ScheduleJob** que usa a saudação de toocall trabalhos **lockDoor** direta duas de dispositivo de saudação do método e atualização desejado propriedades em vários dispositivos.

toocomplete neste tutorial, você precisa Olá a seguir:

* Visual Studio 2015 ou Visual Studio 2017.
* Node.js versão 0.12.x ou posterior. artigo Olá [preparar seu ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node. js para este tutorial no Windows ou Linux.
* Uma conta ativa do Azure. Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a>Agendar trabalhos para chamar um método direto e enviar atualizações ao dispositivo gêmeo

Nesta seção, você cria um console aplicativo .NET (usando o c#) que usa a saudação de toocall trabalhos **lockDoor** método direto e enviar toomultiple dispositivos de atualizações de propriedade desejados.

1. No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto. Projeto de saudação do nome **ScheduleJob**.

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]

1. No Gerenciador de soluções, clique com botão direito Olá **ScheduleJob** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .
1. Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello. Esta etapa baixa, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.

    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. Adicione o seguinte Olá `using` instrução se não estiver presente em instruções de padrão de saudação.

    ```csharp
    using System.Threading.Tasks;
    ```

1. Adicionar Olá toohello campos a seguir **programa** classe. Substitua o espaço reservado de saudação com hello cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello.

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. Adicionar Olá após o método toohello **programa** classe:

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. Adicionar Olá após o método toohello **programa** classe:

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. Adicionar Olá após o método toohello **programa** classe:

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. Finalmente, adicione Olá toohello linhas a seguir **principal** método:

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. Olá Gerenciador de soluções, abra o hello **projetos de inicialização definido...**  e certifique-se de saudação **ação** para **ScheduleJob** projeto é **iniciar**. Compile a solução de saudação.

## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado

Nesta seção, você cria um aplicativo de console Node. js que responde tooa método direto chamado pela nuvem hello, o que dispara uma reinicialização do dispositivo simulado e usa Olá relatado propriedades tooenable dispositivos duas consultas tooidentify dispositivos e quando eles reiniciado pela última vez.

1. Crie uma nova pasta vazia denominada **simDevice**.  Em Olá **simDevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.  Aceite todos os padrões de saudação:

    ```cmd/sh
    npm init
    ```

1. O prompt de comando no hello **simDevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** e **azure iot-dispositivo mqtt** pacotes:

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Usando um editor de texto, crie um novo **simDevice.js** arquivo hello **simDevice** pasta.

1. Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **simDevice.js** arquivo:

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. Adicionar um **connectionString** variável e use-toocreate uma **cliente** instância. Verifique os espaços reservados de saudação tooreplace-se de que a instalação de tooyour apropriado de valores.

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Adicionar Olá Olá de toohandle de função a seguir **lockDoor** método.

    ```nodejs
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

1. Adicionar Olá após código tooregister Olá manipulador Olá **lockDoor** método.

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. Salve e feche o hello **simDevice.js** arquivo.

> [!NOTE]
> coisas tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].

## <a name="run-hello-apps"></a>Executar aplicativos Olá

Agora você está pronto toorun Olá aplicativos.

1. No prompt de comando de saudação de saudação **simDevice** pasta, execute Olá toobegin comando escuta para o método direto de reinicialização Olá a seguir.

    ```cmd/sh
    node simDevice.js
    ```

1. Aplicativo de console Olá execução c# **ScheduleJob** clicando em Olá **ScheduleJob** projeto, selecionando **depurar** e **iniciar nova instância**.

1. Você verá a saída de saudação do dispositivo e aplicativos de back-end.

    ![Executar aplicativos de saudação tooschedule trabalhos][img-schedulejobs]

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você usou um trabalho tooschedule um dispositivo de tooa método direto e atualização de saudação das propriedades do duas do dispositivo hello.

toocontinue guia de Introdução com padrões de gerenciamento de IoT Hub e o dispositivo como remoto pela atualização de firmware ar hello, leia [Tutorial: como toodo um atualização do firmware][lnk-fwupdate].

toocontinue guia de Introdução ao IoT Hub, consulte [guia de Introdução com borda IoT][lnk-iot-edge].

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
