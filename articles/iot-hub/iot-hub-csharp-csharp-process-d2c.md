---
title: mensagens de dispositivo para a nuvem do Azure IoT Hub aaaProcess usando rotas (.Net) | Microsoft Docs
description: "Como tooprocess mensagens de dispositivo para a nuvem de IoT Hub usando regras de roteamento e pontos de extremidade personalizados toodispatch mensagens tooother serviços de back-end."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="ebe71-103">Processar mensagens do dispositivo para nuvem do Hub IoT usando rotas (.NET)</span><span class="sxs-lookup"><span data-stu-id="ebe71-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="ebe71-104">Este tutorial baseia-se em Olá [começar com o IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="ebe71-104">This tutorial builds on hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="ebe71-105">tutorial de saudação:</span><span class="sxs-lookup"><span data-stu-id="ebe71-105">hello tutorial:</span></span>

* <span data-ttu-id="ebe71-106">Mostra como roteamento toouse as regras de mensagens de dispositivo para nuvem toodispatch de forma fácil, com base em configuração.</span><span class="sxs-lookup"><span data-stu-id="ebe71-106">Shows you how toouse routing rules toodispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="ebe71-107">Ilustra como tooisolate mensagens interativo que requerem ação imediata da solução Olá back-end para processamento adicional.</span><span class="sxs-lookup"><span data-stu-id="ebe71-107">Illustrates how tooisolate interactive messages that require immediate action from hello solution back end for further processing.</span></span> <span data-ttu-id="ebe71-108">Por exemplo, um dispositivo pode enviar uma mensagem de alarme que dispara e insere um tíquete em um sistema CRM.</span><span class="sxs-lookup"><span data-stu-id="ebe71-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="ebe71-109">Por outro lado, as mensagens de ponto de dados, como telemetria de temperatura, são enviadas ao mecanismo de análise.</span><span class="sxs-lookup"><span data-stu-id="ebe71-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="ebe71-110">No final da saudação deste tutorial, você deve executar três aplicativos de console do .NET:</span><span class="sxs-lookup"><span data-stu-id="ebe71-110">At hello end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="ebe71-111">**SimulatedDevice**, uma versão modificada do aplicativo hello criado no hello [começar com o IoT Hub] tutorial envia mensagens de dispositivo para a nuvem de ponto de dados por segundo, e mensagens de dispositivo para nuvem interativa cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="ebe71-111">**SimulatedDevice**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="ebe71-112">**ReadDeviceToCloudMessages** exibe Olá não críticos telemetria enviada pelo seu aplicativo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ebe71-112">**ReadDeviceToCloudMessages** that displays hello non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="ebe71-113">**ReadCriticalQueue** filas de mensagens críticas de saudação enviadas pelo seu aplicativo de dispositivo de uma fila do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="ebe71-113">**ReadCriticalQueue** de-queues hello critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="ebe71-114">Essa fila é anexado toohello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ebe71-114">This queue is attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="ebe71-115">O Hub IoT tem suporte de SDK para várias plataformas de dispositivo e linguagens, incluindo C, Java e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ebe71-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="ebe71-116">toolearn como tooreplace Olá dispositivo simulado neste tutorial com um dispositivo físico, consulte Olá [Centro de desenvolvedores do Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="ebe71-116">toolearn how tooreplace hello simulated device in this tutorial with a physical device, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="ebe71-117">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ebe71-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ebe71-118">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ebe71-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="ebe71-119">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebe71-119">An active Azure account.</span></span> <br/><span data-ttu-id="ebe71-120">Se você não tem uma conta, pode criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ebe71-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="ebe71-121">Você também precisa ter um conhecimento básico do [Armazenamento do Azure] e do [Barramento de Serviço do Azure].</span><span class="sxs-lookup"><span data-stu-id="ebe71-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="ebe71-122">Enviar mensagens interativas</span><span class="sxs-lookup"><span data-stu-id="ebe71-122">Send interactive messages</span></span>

<span data-ttu-id="ebe71-123">Modificar Olá dispositivo aplicativo que você criou no hello [começar com o IoT Hub] toooccasionally tutorial enviar mensagens interativas.</span><span class="sxs-lookup"><span data-stu-id="ebe71-123">Modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send interactive messages.</span></span>

<span data-ttu-id="ebe71-124">No Visual Studio, no hello **SimulatedDevice** de projeto, substitua Olá `SendDeviceToCloudMessagesAsync` método com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ebe71-124">In Visual Studio, in hello **SimulatedDevice** project, replace hello `SendDeviceToCloudMessagesAsync` method with hello following code:</span></span>

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

<span data-ttu-id="ebe71-125">Este método adiciona aleatoriamente propriedade Olá `"level": "critical"` toomessages enviadas pelo dispositivo hello, que simula uma mensagem que requer uma ação imediata pela solução de saudação back-end.</span><span class="sxs-lookup"><span data-stu-id="ebe71-125">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello solution back-end.</span></span> <span data-ttu-id="ebe71-126">aplicativo de dispositivo Olá transmite essas informações nas propriedades de mensagem de saudação, em vez de no corpo da mensagem de saudação, para que o IoT Hub pode rotear o destino da mensagem apropriada Olá mensagem toohello.</span><span class="sxs-lookup"><span data-stu-id="ebe71-126">hello device app passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="ebe71-127">Você pode usar mensagens de tooroute de propriedades de mensagem para vários cenários, incluindo frio-caminho de processamento, além de exemplo de caminho hot toohello mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="ebe71-127">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="ebe71-128">Para a mesma Olá de simplicidade, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="ebe71-128">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ebe71-129">No código de produção, você deve implementar uma política de repetição como retirada exponencial, conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].</span><span class="sxs-lookup"><span data-stu-id="ebe71-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a><span data-ttu-id="ebe71-130">Fila de mensagens tooa de rota em seu hub IoT</span><span class="sxs-lookup"><span data-stu-id="ebe71-130">Route messages tooa queue in your IoT hub</span></span>

<span data-ttu-id="ebe71-131">Nesta seção, você:</span><span class="sxs-lookup"><span data-stu-id="ebe71-131">In this section, you:</span></span>

* <span data-ttu-id="ebe71-132">Criará uma fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="ebe71-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="ebe71-133">Conecte-o tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ebe71-133">Connect it tooyour IoT hub.</span></span>
* <span data-ttu-id="ebe71-134">Configure seu IoT hub toosend mensagens toohello fila com base na presença de saudação de uma propriedade na mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebe71-134">Configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span>

<span data-ttu-id="ebe71-135">Para obter mais informações sobre como tooprocess mensagens das filas do barramento de serviço, consulte [começar com filas][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="ebe71-135">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="ebe71-136">Crie uma fila do Barramento de Serviço conforme descrito em [Introdução às filas][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="ebe71-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="ebe71-137">Olá fila deve ser no hello mesma assinatura e região, como o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ebe71-137">hello queue must be in hello same subscription and region as your IoT hub.</span></span> <span data-ttu-id="ebe71-138">Faça uma anotação de nome de namespace e fila hello.</span><span class="sxs-lookup"><span data-stu-id="ebe71-138">Make a note of hello namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ebe71-139">As filas e os tópicos do Barramento de Serviço utilizados como pontos de extremidade do Hub IoT não devem ter **Sessões** nem **Detecção Duplicada** habilitadas.</span><span class="sxs-lookup"><span data-stu-id="ebe71-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="ebe71-140">Se qualquer uma dessas opções estiver habilitada, o ponto de extremidade de saudação aparece como **inacessível** em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebe71-140">If either of those options are enabled, hello endpoint appears as **Unreachable** in hello Azure portal.</span></span>

2. <span data-ttu-id="ebe71-141">Olá portal do Azure, abra seu hub IoT em e clique em **pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="ebe71-141">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Pontos de extremidade no Hub IoT][30]

3. <span data-ttu-id="ebe71-143">Em Olá **pontos de extremidade** folha, clique em **adicionar** em Olá tooadd superior hub IoT de tooyour de fila.</span><span class="sxs-lookup"><span data-stu-id="ebe71-143">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="ebe71-144">O ponto de extremidade do nome hello **CriticalQueue** e usar Olá suspensas tooselect **fila do barramento de serviço**, Olá namespace de barramento de serviço no qual reside a fila e Olá nome da fila.</span><span class="sxs-lookup"><span data-stu-id="ebe71-144">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="ebe71-145">Quando terminar, clique em **salvar** na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ebe71-145">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Adicionando um ponto de extremidade][31]
    
4. <span data-ttu-id="ebe71-147">Agora clique em **Rotas** no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ebe71-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="ebe71-148">Clique em **adicionar** na parte superior de saudação do hello folha toocreate uma regra de roteamento que roteia mensagens toohello fila apenas adicionada.</span><span class="sxs-lookup"><span data-stu-id="ebe71-148">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="ebe71-149">Selecione **DeviceTelemetry** como fonte de saudação de dados.</span><span class="sxs-lookup"><span data-stu-id="ebe71-149">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="ebe71-150">Digite `level="critical"` como condição Olá e escolha fila Olá que você acabou de adicionar como um ponto de extremidade personalizado como ponto de extremidade de regra de roteamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebe71-150">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="ebe71-151">Quando terminar, clique em **salvar** na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ebe71-151">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Adicionando uma rota][32]
    
    <span data-ttu-id="ebe71-153">Certifique-se de rota fallback hello está definida muito**ON**.</span><span class="sxs-lookup"><span data-stu-id="ebe71-153">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="ebe71-154">Esse valor é a configuração padrão de saudação para um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ebe71-154">This value is hello default configuration for an IoT hub.</span></span>
    
    ![Rota de fallback][33]

## <a name="read-from-hello-queue-endpoint"></a><span data-ttu-id="ebe71-156">Ler a partir do ponto de extremidade de fila Olá</span><span class="sxs-lookup"><span data-stu-id="ebe71-156">Read from hello queue endpoint</span></span>

<span data-ttu-id="ebe71-157">Nesta seção, você pode ler mensagens de saudação do ponto de extremidade de fila hello.</span><span class="sxs-lookup"><span data-stu-id="ebe71-157">In this section, you read hello messages from hello queue endpoint.</span></span>

1. <span data-ttu-id="ebe71-158">No Visual Studio, adicionar uma Visual C# Windows clássico Desktop projeto toohello solução atual, usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="ebe71-158">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="ebe71-159">Projeto de saudação do nome **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="ebe71-159">Name hello project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="ebe71-160">No Gerenciador de soluções, clique com botão direito Olá **ReadCriticalQueue** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ebe71-160">In Solution Explorer, right-click hello **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="ebe71-161">Essa operação exibe Olá **NuGet Package Manager** janela.</span><span class="sxs-lookup"><span data-stu-id="ebe71-161">This operation displays hello **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="ebe71-162">Procurar **windowsazure. ServiceBus**, clique em **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="ebe71-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="ebe71-163">Esta operação baixa, instala e adiciona uma referência toohello barramento de serviço do Azure, com todas as suas dependências.</span><span class="sxs-lookup"><span data-stu-id="ebe71-163">This operation downloads, installs, and adds a reference toohello Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="ebe71-164">Adicione o seguinte Olá **usando** instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="ebe71-164">Add hello following **using** statements at hello top of hello **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="ebe71-165">Finalmente, adicione Olá toohello linhas a seguir **principal** método.</span><span class="sxs-lookup"><span data-stu-id="ebe71-165">Finally, add hello following lines toohello **Main** method.</span></span> <span data-ttu-id="ebe71-166">Substitua a cadeia de caracteres de conexão de saudação com **escutar** permissões para Olá fila:</span><span class="sxs-lookup"><span data-stu-id="ebe71-166">Substitute hello connection string with **Listen** permissions for hello queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="ebe71-167">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="ebe71-167">Run hello applications</span></span>
<span data-ttu-id="ebe71-168">Agora você está pronto toorun aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebe71-168">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="ebe71-169">No Visual Studio, no Gerenciador de Soluções, clique com o botão direito do mouse na solução e selecione **Definir Projetos de Inicialização**.</span><span class="sxs-lookup"><span data-stu-id="ebe71-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="ebe71-170">Selecione **vários projetos de inicialização**, em seguida, selecione **iniciar** como ação Olá Olá **ReadDeviceToCloudMessages**, **SimulatedDevice**, e **ReadCriticalQueue** projetos.</span><span class="sxs-lookup"><span data-stu-id="ebe71-170">Select **Multiple startup projects**, then select **Start** as hello action for hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="ebe71-171">Pressione **F5** toostart Olá três aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="ebe71-171">Press **F5** toostart hello three console apps.</span></span> <span data-ttu-id="ebe71-172">Olá **ReadDeviceToCloudMessages** aplicativo tem apenas as mensagens não críticos enviadas Olá **SimulatedDevice** aplicativo e hello **ReadCriticalQueue** aplicativo tem apenas mensagens críticas.</span><span class="sxs-lookup"><span data-stu-id="ebe71-172">hello **ReadDeviceToCloudMessages** app has only non-critical messages sent from hello **SimulatedDevice** application, and hello **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Três aplicativos de console][50]

## <a name="next-steps"></a><span data-ttu-id="ebe71-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ebe71-174">Next steps</span></span>
<span data-ttu-id="ebe71-175">Neste tutorial, você aprendeu como tooreliably expedir as mensagens de dispositivo para nuvem usando a funcionalidade de roteamento de mensagem de saudação do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ebe71-175">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="ebe71-176">Olá [como mensagens de nuvem para dispositivo toosend com o IoT Hub] [ lnk-c2d] mostra como toosend mensagens tooyour dispositivos de back-end sua solução.</span><span class="sxs-lookup"><span data-stu-id="ebe71-176">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="ebe71-177">exemplos de toosee de soluções completas de ponta a ponta que usam o IoT Hub, consulte [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="ebe71-177">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="ebe71-178">toolearn mais sobre como desenvolver soluções com o IoT Hub, consulte Olá [guia do desenvolvedor de IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="ebe71-178">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="ebe71-179">toolearn mais sobre o roteamento de mensagens no IoT Hub, consulte [enviar e receber mensagens com o IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="ebe71-179">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Armazenamento do Azure]: https://azure.microsoft.com/documentation/services/storage/
[Barramento de Serviço do Azure]: https://azure.microsoft.com/documentation/services/service-bus/
[guia do desenvolvedor de IoT Hub]: iot-hub-devguide.md
[começar com o IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Centro de desenvolvedores do Azure IoT]: https://azure.microsoft.com/develop/iot
[tratamento de falhas transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
