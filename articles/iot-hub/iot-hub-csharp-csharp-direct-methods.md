---
title: "aaaUse Azure IoT Hub direcionar métodos (.NET/.NET) | Microsoft Docs"
description: "Como toouse Azure IoT Hub direta métodos. Use dispositivo IoT do Azure de saudação SDK para .NET tooimplement um aplicativo de dispositivo simulado que inclui um método direto e hello serviço IoT do Azure SDK para .NET tooimplement um aplicativo de serviço que invoca o método direto hello."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a>Usar métodos diretos (.NET/.NET)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Neste tutorial, estamos indo toodevelop dois .NET os aplicativos de console:

* **CallMethodOnDevice**, um aplicativo de back-end, que chama um método no aplicativo do dispositivo simulado hello e exibe a resposta de saudação.
* **SimulateDeviceMethods**, um aplicativo de console que simula um dispositivo conectado tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente e responde toohello método chamado pela nuvem hello.

> [!NOTE]
> artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun ambos os aplicativos em dispositivos e o back-end da solução.
> 
> 

toocomplete neste tutorial, você precisa:

* Visual Studio 2015 ou Visual Studio 2017.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Identidade do dispositivo Olá toocreate programaticamente em vez disso, leia seção correspondente Olá Olá [conecte seu dispositivo simulado tooyour IoT hub que usando o .NET] [ lnk-device-identity-csharp] artigo.


## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado
Nesta seção, você deve criar um aplicativo de console .NET que responde tooa método chamado pela solução de saudação volta final.

1. No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto. Projeto de saudação do nome **SimulateDeviceMethods**.
   
    ![Novo aplicativo de dispositivo Visual C# Windows clássico][img-createdeviceapp]
    
1. No Gerenciador de soluções, clique com botão direito Olá **SimulateDeviceMethods** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .
1. Em Olá **NuGet Package Manager** janela, selecione **procurar** e procure **microsoft.azure.devices.client**. Selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices.Client** empacotar e aceitar os termos de uso do hello. Este procedimento faz o download, instala e adiciona uma referência toohello [dispositivo IoT do Azure SDK] [ lnk-nuget-client-sdk] NuGet pacote e suas dependências.
   
    ![Aplicativo de cliente de janela do Gerenciador de Pacotes NuGet][img-clientnuget]
1. Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. Adicionar Olá toohello campos a seguir **programa** classe. Substitua o valor de espaço reservado de saudação com cadeia de conexão do dispositivo Olá observado na seção anterior hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Adicione Olá seguinte tooimplement Olá ao método direto no dispositivo hello:

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. Finalmente, adicione Olá toohello de código a seguir **principal** método tooopen Olá conexão tooyour IoT hub e inicializar Olá método ouvinte:
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. Olá Gerenciador de soluções do Visual Studio, com o botão direito sua solução e clique em **definir projetos de inicialização...** . Selecione **único projeto de inicialização**e, em seguida, selecione Olá **SimulateDeviceMethods** projeto no menu suspenso de saudação.        

> [!NOTE]
> coisas tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (como tentativas de conexão), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Chama um método direto em um dispositivo
Nesta seção, você deve criar um aplicativo de console .NET que chama um método no aplicativo do dispositivo simulado hello e, em seguida, exibe a resposta de saudação.

1. No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto. Certifique-se de versão do .NET Framework Olá é 4.5.1 ou posterior. Projeto de saudação do nome **CallMethodOnDevice**.
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createserviceapp]
2. No Gerenciador de soluções, clique com botão direito Olá **CallMethodOnDevice** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .
3. Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello. Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.
   
    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]

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

1. Olá Gerenciador de soluções do Visual Studio, com o botão direito sua solução e clique em **definir projetos de inicialização...** . Selecione **único projeto de inicialização**e, em seguida, selecione Olá **CallMethodOnDevice** projeto no menu suspenso de saudação.

## <a name="run-hello-applications"></a>Executar aplicativos Olá
Agora você está pronto toorun aplicativos de saudação.

1. Execute o aplicativo de dispositivo de .NET Olá **SimulateDeviceMethods**. Ele deve iniciar a escuta para chamadas de método do seu Hub IoT: 

    ![Execução de aplicativo de dispositivo][img-deviceapprun]
1. Agora esse dispositivo hello está conectado e esperando para invocações de método, execute Olá .NET **CallMethodOnDevice** método do aplicativo tooinvoke hello no aplicativo do dispositivo simulado hello. Você deve ver a resposta do dispositivo Olá gravada no console de saudação.
   
    ![Execução de aplicativo de serviço][img-serviceapprun]
1. dispositivo Hello, em seguida, reage toohello método imprimindo esta mensagem:
   
    ![Método direto invocado no dispositivo Olá][img-directmethodinvoked]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello. Você usou esse dispositivo identidade tooenable Olá simulado dispositivo aplicativo tooreact toomethods invocado pela nuvem hello. Você também criou um aplicativo que chama métodos no dispositivo hello e exibe a resposta de saudação do dispositivo de saudação. 

toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:

* [Introdução ao Hub IoT]
* [Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]

toolearn como tooextend seu método de solução e agenda IoT chama em vários dispositivos, consulte Olá [agenda e trabalhos de difusão] [ lnk-tutorial-jobs] tutorial.

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Introdução ao Hub IoT]: iot-hub-node-node-getstarted.md
