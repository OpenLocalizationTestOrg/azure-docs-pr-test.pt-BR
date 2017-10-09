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
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a><span data-ttu-id="7b728-104">Conecte o dispositivo tooyour IoT hub que usando o .NET</span><span class="sxs-lookup"><span data-stu-id="7b728-104">Connect your device tooyour IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="7b728-105">No final da saudação deste tutorial, você tem três aplicativos de console .NET:</span><span class="sxs-lookup"><span data-stu-id="7b728-105">At hello end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="7b728-106">**CreateDeviceIdentity**, que cria uma identidade de dispositivo e de segurança da chave tooconnect seu aplicativo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7b728-106">**CreateDeviceIdentity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="7b728-107">**ReadDeviceToCloudMessages**, que exibe a telemetria de saudação enviada pelo seu aplicativo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7b728-107">**ReadDeviceToCloudMessages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="7b728-108">**SimulatedDevice**, que se conecta tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente e envia uma mensagem de telemetria por segundo usando o protocolo de MQTT saudação.</span><span class="sxs-lookup"><span data-stu-id="7b728-108">**SimulatedDevice**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second by using hello MQTT protocol.</span></span>

<span data-ttu-id="7b728-109">Você pode baixar ou clonar a solução do Visual Studio hello, que contém três aplicativos de saudação do Github.</span><span class="sxs-lookup"><span data-stu-id="7b728-109">You can download or clone hello Visual Studio solution, which contains hello three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="7b728-110">Para obter informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun de aplicativos em dispositivos e sua solução back-end, consulte [SDKs do Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="7b728-110">For information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="7b728-111">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b728-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="7b728-112">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7b728-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="7b728-113">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b728-113">An active Azure account.</span></span> <span data-ttu-id="7b728-114">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="7b728-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="7b728-115">Agora você criou seu hub IoT e você tem o nome de host de saudação e a cadeia de caracteres de conexão de IoT Hub que você precisa toocomplete restante Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="7b728-115">You have now created your IoT hub, and you have hello host name and IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="7b728-116">Receber mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="7b728-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="7b728-117">Nesta seção, você cria um aplicativo do console do .NET que lê mensagens do dispositivo para a nuvem do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7b728-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="7b728-118">Um hub IoT expõe um [Hubs de eventos do Azure][lnk-event-hubs-overview]-tooenable de ponto de extremidade compatível tooread mensagens de dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="7b728-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="7b728-119">coisas tookeep simples, este tutorial cria um leitor básico que não é adequado para uma implantação de alta taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="7b728-119">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="7b728-120">toolearn como o dispositivo para nuvem tooprocess mensagens em grande escala, consulte Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="7b728-120">toolearn how tooprocess device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="7b728-121">Para obter mais informações sobre como tooprocess mensagens de Hubs de eventos, consulte Olá [Introdução aos Hubs de eventos] [ lnk-eventhubs-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="7b728-121">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="7b728-122">(Este tutorial é aplicável toohello compatível com o evento de Hub IoT Hub pontos de extremidade).</span><span class="sxs-lookup"><span data-stu-id="7b728-122">(This tutorial is applicable toohello IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="7b728-123">Olá, ponto de extremidade compatível com o evento Hub para ler mensagens de dispositivo para nuvem sempre usa protocolo AMQP de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b728-123">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="7b728-124">No Visual Studio, adicionar uma Visual C# Windows clássico Desktop projeto toohello solução atual, usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="7b728-124">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="7b728-125">Certifique-se de versão do .NET Framework Olá é 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7b728-125">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="7b728-126">Projeto de saudação do nome **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="7b728-126">Name hello project **ReadDeviceToCloudMessages**.</span></span>

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][10a]

2. <span data-ttu-id="7b728-128">No Gerenciador de soluções, clique com botão direito Olá **ReadDeviceToCloudMessages** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7b728-128">In Solution Explorer, right-click hello **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="7b728-129">Em Olá **NuGet Package Manager** janela, procure **windowsazure. ServiceBus**, selecione **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="7b728-129">In hello **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="7b728-130">Este procedimento faz o download, instala e adiciona uma referência muito[Azure Service Bus][lnk-servicebus-nuget], com todas as suas dependências.</span><span class="sxs-lookup"><span data-stu-id="7b728-130">This procedure downloads, installs, and adds a reference too[Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="7b728-131">Este pacote permite que o ponto de extremidade de saudação do aplicativo tooconnect toohello compatível com o evento Hub em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7b728-131">This package enables hello application tooconnect toohello Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="7b728-132">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="7b728-132">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="7b728-133">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="7b728-133">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="7b728-134">Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá criado na seção "Criar um hub IoT" de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b728-134">Replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="7b728-135">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="7b728-135">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="7b728-136">Esse método usa um **EventHubReceiver** partições de recebimento de mensagens de tooreceive de instância de todos os Olá IoT hub dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="7b728-136">This method uses an **EventHubReceiver** instance tooreceive messages from all hello IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="7b728-137">Observe como você passar um `DateTime.Now` parâmetro quando você cria Olá **EventHubReceiver** do objeto, para que ele receba apenas as mensagens enviadas após ele ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="7b728-137">Notice how you pass a `DateTime.Now` parameter when you create hello **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="7b728-138">Esse filtro é útil em um ambiente de teste para que possa ver o conjunto atual de saudação de mensagens.</span><span class="sxs-lookup"><span data-stu-id="7b728-138">This filter is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="7b728-139">Em um ambiente de produção, seu código deve ter certeza de que ele processa todas as mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b728-139">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="7b728-140">Para obter mais informações, consulte o tutorial Olá [como tooprocess mensagens de dispositivo para a nuvem de IoT Hub][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="7b728-140">For more information, see hello tutorial [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="7b728-141">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="7b728-141">Finally, add hello following lines toohello **Main** method:</span></span>

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

## <a name="create-a-device-app"></a><span data-ttu-id="7b728-142">Criar um aplicativo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="7b728-142">Create a device app</span></span>

<span data-ttu-id="7b728-143">Nesta seção, você deve criar um aplicativo de console .NET que simula um dispositivo que envia o hub de IoT tooan mensagens de dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="7b728-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="7b728-144">No Visual Studio, adicionar uma Visual C# Windows clássico Desktop projeto toohello solução atual, usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="7b728-144">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="7b728-145">Certifique-se de versão do .NET Framework Olá é 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7b728-145">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="7b728-146">Projeto de saudação do nome **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="7b728-146">Name hello project **SimulatedDevice**.</span></span>

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][10b]

2. <span data-ttu-id="7b728-148">No Gerenciador de soluções, clique com botão direito Olá **SimulatedDevice** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7b728-148">In Solution Explorer, right-click hello **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="7b728-149">Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **Microsoft.Azure.Devices.Client**, selecione **instalar** Olá tooinstall **Microsoft.Azure.Devices.Client** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="7b728-149">In hello **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="7b728-150">Este procedimento faz o download, instala e adiciona uma referência toohello [pacote NuGet do SDK do Azure IoT dispositivo] [ lnk-device-nuget] e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="7b728-150">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="7b728-151">Adicione o seguinte Olá `using` instrução na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="7b728-151">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="7b728-152">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="7b728-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="7b728-153">Substituir `{iot hub hostname}` com nome de host do hello IoT hub recuperado na seção de "Criar um hub IoT" hello.</span><span class="sxs-lookup"><span data-stu-id="7b728-153">Substitute `{iot hub hostname}` with hello IoT hub host name you retrieved in hello "Create an IoT hub" section.</span></span> <span data-ttu-id="7b728-154">Substituir `{device key}` com a chave do dispositivo Olá recuperado na seção de "Criar uma identidade de dispositivo" hello.</span><span class="sxs-lookup"><span data-stu-id="7b728-154">Substitute `{device key}` with hello device key you retrieved in hello "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="7b728-155">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="7b728-155">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="7b728-156">Esse método envia uma nova mensagem de dispositivo para a nuvem a cada segundo.</span><span class="sxs-lookup"><span data-stu-id="7b728-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="7b728-157">mensagem de saudação contém um objeto serializado para JSON, com a ID de dispositivo hello e gerado aleatoriamente números toosimulate um sensor de temperatura e um sensor de umidade.</span><span class="sxs-lookup"><span data-stu-id="7b728-157">hello message contains a JSON-serialized object, with hello device ID and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="7b728-158">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="7b728-158">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="7b728-159">Por padrão, Olá **criar** método em um aplicativo do .NET Framework cria um **DeviceClient** instância que usa Olá AMQP protocolo toocommunicate com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b728-159">By default, hello **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses hello AMQP protocol toocommunicate with IoT Hub.</span></span> <span data-ttu-id="7b728-160">Olá toouse protocolo HTTP ou MQTT, usar a substituição de saudação de saudação **criar** método que permite que o protocolo de saudação toospecify.</span><span class="sxs-lookup"><span data-stu-id="7b728-160">toouse hello MQTT or HTTP protocol, use hello override of hello **Create** method that enables you toospecify hello protocol.</span></span> <span data-ttu-id="7b728-161">UWP e PCL clientes usam o protocolo HTTP de saudação por padrão.</span><span class="sxs-lookup"><span data-stu-id="7b728-161">UWP and PCL clients use hello HTTP protocol by default.</span></span> <span data-ttu-id="7b728-162">Se você usar o protocolo de saudação HTTP, você também deve adicionar Olá **Microsoft.AspNet.WebApi.Client** saudação do NuGet pacote tooyour projeto tooinclude **System.Net.Http.Formatting** namespace.</span><span class="sxs-lookup"><span data-stu-id="7b728-162">If you use hello HTTP protocol, you should also add hello **Microsoft.AspNet.WebApi.Client** NuGet package tooyour project tooinclude hello **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="7b728-163">Este tutorial apresenta Olá etapas toocreate um IoT Hub aplicativo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7b728-163">This tutorial takes you through hello steps toocreate an IoT Hub device app.</span></span> <span data-ttu-id="7b728-164">Você também pode usar o hello [serviço conectado de Azure IoT Hub] [ lnk-connected-service] aplicativo de dispositivo do Visual Studio extensão tooadd Olá necessárias de código tooyour.</span><span class="sxs-lookup"><span data-stu-id="7b728-164">You can also use hello [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension tooadd hello necessary code tooyour device app.</span></span>

> [!NOTE]
> <span data-ttu-id="7b728-165">coisas tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="7b728-165">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="7b728-166">No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="7b728-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="7b728-167">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="7b728-167">Run hello apps</span></span>

<span data-ttu-id="7b728-168">Agora você está pronto toorun Olá aplicativos.</span><span class="sxs-lookup"><span data-stu-id="7b728-168">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="7b728-169">No Visual Studio, no Gerenciador de Soluções, clique com o botão direito na solução e clique em **Definir Projetos de Inicialização**.</span><span class="sxs-lookup"><span data-stu-id="7b728-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="7b728-170">Selecione **vários projetos de inicialização**e, em seguida, selecione **iniciar** como ação Olá para ambos os Olá **ReadDeviceToCloudMessages** e **SimulatedDevice** projetos.</span><span class="sxs-lookup"><span data-stu-id="7b728-170">Select **Multiple startup projects**, and then select **Start** as hello action for both hello **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Propriedades do projeto de inicialização][41]

2. <span data-ttu-id="7b728-172">Pressione **F5** toostart ambos os aplicativos em execução.</span><span class="sxs-lookup"><span data-stu-id="7b728-172">Press **F5** toostart both apps running.</span></span> <span data-ttu-id="7b728-173">Olá a saída do console do hello **SimulatedDevice** mensagens de saudação do aplicativo mostra seu aplicativo de dispositivo envia tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7b728-173">hello console output from hello **SimulatedDevice** app shows hello messages your device app sends tooyour IoT hub.</span></span> <span data-ttu-id="7b728-174">Olá a saída do console do hello **ReadDeviceToCloudMessages** aplicativo mostra mensagens de saudação que recebe o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7b728-174">hello console output from hello **ReadDeviceToCloudMessages** app shows hello messages that your IoT hub receives.</span></span>

    ![Saída de console dos aplicativos][42]

3. <span data-ttu-id="7b728-176">Olá **uso** lado a lado no hello [portal do Azure] [ lnk-portal] mostra Olá número de mensagens enviadas toohello IoT hub:</span><span class="sxs-lookup"><span data-stu-id="7b728-176">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Bloco Uso do portal do Azure][43]

## <a name="next-steps"></a><span data-ttu-id="7b728-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b728-178">Next steps</span></span>

<span data-ttu-id="7b728-179">Neste tutorial, configurado um hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub do hello IoT.</span><span class="sxs-lookup"><span data-stu-id="7b728-179">In this tutorial, you configured an IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="7b728-180">Você usou esse dispositivo identidade tooenable Olá dispositivo toosend mensagens de dispositivo para nuvem toohello IoT hub de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="7b728-180">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="7b728-181">Você também criou um aplicativo que exibe mensagens de saudação recebidas pelo hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b728-181">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="7b728-182">toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="7b728-182">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="7b728-183">[Conectando o dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="7b728-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="7b728-184">[Introdução ao gerenciamento de dispositivo][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="7b728-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="7b728-185">[Introdução ao IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="7b728-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="7b728-186">toolearn como tooextend seu IoT solução e o processo de dispositivo para nuvem mensagens em grande escala, consulte Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="7b728-186">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

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
