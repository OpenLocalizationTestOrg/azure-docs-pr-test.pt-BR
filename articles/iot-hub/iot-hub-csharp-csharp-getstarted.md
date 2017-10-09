---
title: aaaGet iniciado com o Azure IoT Hub (.NET) | Microsoft Docs
description: "Saiba como o dispositivo para nuvem toosend mensagens tooAzure IoT Hub usando IoT SDKs para .NET. Criar dispositivo simulado e tooregister de aplicativos de serviço de seu dispositivo, enviar mensagens e ler mensagens de hub IoT."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a>Conecte o dispositivo tooyour IoT hub que usando o .NET

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

No final da saudação deste tutorial, você tem três aplicativos de console .NET:

* **CreateDeviceIdentity**, que cria uma identidade de dispositivo e de segurança da chave tooconnect seu aplicativo de dispositivo.
* **ReadDeviceToCloudMessages**, que exibe a telemetria de saudação enviada pelo seu aplicativo de dispositivo.
* **SimulatedDevice**, que se conecta tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente e envia uma mensagem de telemetria por segundo usando o protocolo de MQTT saudação.

Você pode baixar ou clonar a solução do Visual Studio hello, que contém três aplicativos de saudação do Github.

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> Para obter informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun de aplicativos em dispositivos e sua solução back-end, consulte [SDKs do Azure IoT][lnk-hub-sdks].

toocomplete neste tutorial, você precisa Olá a seguir:

* Visual Studio 2015 ou Visual Studio 2017.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Agora você criou seu hub IoT e você tem o nome de host de saudação e a cadeia de caracteres de conexão de IoT Hub que você precisa toocomplete restante Olá deste tutorial.

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a>Receber mensagens do dispositivo para a nuvem
Nesta seção, você cria um aplicativo do console do .NET que lê mensagens do dispositivo para a nuvem do Hub IoT. Um hub IoT expõe um [Hubs de eventos do Azure][lnk-event-hubs-overview]-tooenable de ponto de extremidade compatível tooread mensagens de dispositivo para a nuvem. coisas tookeep simples, este tutorial cria um leitor básico que não é adequado para uma implantação de alta taxa de transferência. toolearn como o dispositivo para nuvem tooprocess mensagens em grande escala, consulte Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial. Para obter mais informações sobre como tooprocess mensagens de Hubs de eventos, consulte Olá [Introdução aos Hubs de eventos] [ lnk-eventhubs-tutorial] tutorial. (Este tutorial é aplicável toohello compatível com o evento de Hub IoT Hub pontos de extremidade).

> [!NOTE]
> Olá, ponto de extremidade compatível com o evento Hub para ler mensagens de dispositivo para nuvem sempre usa protocolo AMQP de saudação.

1. No Visual Studio, adicionar uma Visual C# Windows clássico Desktop projeto toohello solução atual, usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto. Certifique-se de versão do .NET Framework Olá é 4.5.1 ou posterior. Projeto de saudação do nome **ReadDeviceToCloudMessages**.

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][10a]

2. No Gerenciador de soluções, clique com botão direito Olá **ReadDeviceToCloudMessages** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.

3. Em Olá **NuGet Package Manager** janela, procure **windowsazure. ServiceBus**, selecione **instalar**e aceite os termos de uso do hello. Este procedimento faz o download, instala e adiciona uma referência muito[Azure Service Bus][lnk-servicebus-nuget], com todas as suas dependências. Este pacote permite que o ponto de extremidade de saudação do aplicativo tooconnect toohello compatível com o evento Hub em seu hub IoT.

4. Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. Adicionar Olá toohello campos a seguir **programa** classe. Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá criado na seção "Criar um hub IoT" de saudação.

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. Adicionar Olá após o método toohello **programa** classe:

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    Esse método usa um **EventHubReceiver** partições de recebimento de mensagens de tooreceive de instância de todos os Olá IoT hub dispositivo para a nuvem. Observe como você passar um `DateTime.Now` parâmetro quando você cria Olá **EventHubReceiver** do objeto, para que ele receba apenas as mensagens enviadas após ele ser iniciado. Esse filtro é útil em um ambiente de teste para que possa ver o conjunto atual de saudação de mensagens. Em um ambiente de produção, seu código deve ter certeza de que ele processa todas as mensagens de saudação. Para obter mais informações, consulte o tutorial Olá [como tooprocess mensagens de dispositivo para a nuvem de IoT Hub][lnk-process-d2c-tutorial].

7. Finalmente, adicione Olá toohello linhas a seguir **principal** método:

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a>Criar um aplicativo de dispositivo

Nesta seção, você deve criar um aplicativo de console .NET que simula um dispositivo que envia o hub de IoT tooan mensagens de dispositivo para a nuvem.

1. No Visual Studio, adicionar uma Visual C# Windows clássico Desktop projeto toohello solução atual, usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto. Certifique-se de versão do .NET Framework Olá é 4.5.1 ou posterior. Projeto de saudação do nome **SimulatedDevice**.

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][10b]

2. No Gerenciador de soluções, clique com botão direito Olá **SimulatedDevice** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.

3. Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **Microsoft.Azure.Devices.Client**, selecione **instalar** Olá tooinstall **Microsoft.Azure.Devices.Client** empacotar e aceitar os termos de uso do hello. Este procedimento faz o download, instala e adiciona uma referência toohello [pacote NuGet do SDK do Azure IoT dispositivo] [ lnk-device-nuget] e suas dependências.

4. Adicione o seguinte Olá `using` instrução na parte superior de saudação do hello **Program.cs** arquivo:

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. Adicionar Olá toohello campos a seguir **programa** classe. Substituir `{iot hub hostname}` com nome de host do hello IoT hub recuperado na seção de "Criar um hub IoT" hello. Substituir `{device key}` com a chave do dispositivo Olá recuperado na seção de "Criar uma identidade de dispositivo" hello.

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. Adicionar Olá após o método toohello **programa** classe:

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    Esse método envia uma nova mensagem de dispositivo para a nuvem a cada segundo. mensagem de saudação contém um objeto serializado para JSON, com a ID de dispositivo hello e gerado aleatoriamente números toosimulate um sensor de temperatura e um sensor de umidade.

7. Finalmente, adicione Olá toohello linhas a seguir **principal** método:

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    Por padrão, Olá **criar** método em um aplicativo do .NET Framework cria um **DeviceClient** instância que usa Olá AMQP protocolo toocommunicate com o IoT Hub. Olá toouse protocolo HTTP ou MQTT, usar a substituição de saudação de saudação **criar** método que permite que o protocolo de saudação toospecify. UWP e PCL clientes usam o protocolo HTTP de saudação por padrão. Se você usar o protocolo de saudação HTTP, você também deve adicionar Olá **Microsoft.AspNet.WebApi.Client** saudação do NuGet pacote tooyour projeto tooinclude **System.Net.Http.Formatting** namespace.

Este tutorial apresenta Olá etapas toocreate um IoT Hub aplicativo do dispositivo. Você também pode usar o hello [serviço conectado de Azure IoT Hub] [ lnk-connected-service] aplicativo de dispositivo do Visual Studio extensão tooadd Olá necessárias de código tooyour.

> [!NOTE]
> coisas tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].

## <a name="run-hello-apps"></a>Executar aplicativos Olá

Agora você está pronto toorun Olá aplicativos.

1. No Visual Studio, no Gerenciador de Soluções, clique com o botão direito na solução e clique em **Definir Projetos de Inicialização**. Selecione **vários projetos de inicialização**e, em seguida, selecione **iniciar** como ação Olá para ambos os Olá **ReadDeviceToCloudMessages** e **SimulatedDevice** projetos.

    ![Propriedades do projeto de inicialização][41]

2. Pressione **F5** toostart ambos os aplicativos em execução. Olá a saída do console do hello **SimulatedDevice** mensagens de saudação do aplicativo mostra seu aplicativo de dispositivo envia tooyour IoT hub. Olá a saída do console do hello **ReadDeviceToCloudMessages** aplicativo mostra mensagens de saudação que recebe o hub IoT.

    ![Saída de console dos aplicativos][42]

3. Olá **uso** lado a lado no hello [portal do Azure] [ lnk-portal] mostra Olá número de mensagens enviadas toohello IoT hub:

    ![Bloco Uso do portal do Azure][43]

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, configurado um hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub do hello IoT. Você usou esse dispositivo identidade tooenable Olá dispositivo toosend mensagens de dispositivo para nuvem toohello IoT hub de aplicativos. Você também criou um aplicativo que exibe mensagens de saudação recebidas pelo hub IoT de saudação.

toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:

* [Conectando o dispositivo][lnk-connect-device]
* [Introdução ao gerenciamento de dispositivo][lnk-device-management]
* [Introdução ao IoT Edge][lnk-iot-edge]

toolearn como tooextend seu IoT solução e o processo de dispositivo para nuvem mensagens em grande escala, consulte Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
