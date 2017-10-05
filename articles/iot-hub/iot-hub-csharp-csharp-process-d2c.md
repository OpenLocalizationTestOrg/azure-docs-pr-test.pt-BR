---
title: Processar mensagens do dispositivo para nuvem do Hub IoT do Azure usando rotas (.Net) | Microsoft Docs
description: "Como processar mensagens do dispositivo para nuvem do Hub IoT usando regras de direcionamento e pontos de extremidade personalizados para enviar mensagens para outros serviços de back-end."
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
ms.openlocfilehash: 1d2b52ea005ab520bf294efa603512c00a92ee63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="1a446-103">Processar mensagens do dispositivo para nuvem do Hub IoT usando rotas (.NET)</span><span class="sxs-lookup"><span data-stu-id="1a446-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="1a446-104">Este tutorial baseia-se no tutorial [Introdução ao Hub IoT] .</span><span class="sxs-lookup"><span data-stu-id="1a446-104">This tutorial builds on the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="1a446-105">O tutorial:</span><span class="sxs-lookup"><span data-stu-id="1a446-105">The tutorial:</span></span>

* <span data-ttu-id="1a446-106">Mostra como usar regras de roteamento do para enviar mensagens de dispositivo à nuvem de maneira fácil, com base em configuração.</span><span class="sxs-lookup"><span data-stu-id="1a446-106">Shows you how to use routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="1a446-107">Ilustra como isolar mensagens interativas que exigem ação imediata no back-end da solução para processamento adicional.</span><span class="sxs-lookup"><span data-stu-id="1a446-107">Illustrates how to isolate interactive messages that require immediate action from the solution back end for further processing.</span></span> <span data-ttu-id="1a446-108">Por exemplo, um dispositivo pode enviar uma mensagem de alarme que dispara e insere um tíquete em um sistema CRM.</span><span class="sxs-lookup"><span data-stu-id="1a446-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="1a446-109">Por outro lado, as mensagens de ponto de dados, como telemetria de temperatura, são enviadas ao mecanismo de análise.</span><span class="sxs-lookup"><span data-stu-id="1a446-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="1a446-110">No final deste tutorial, você executará três aplicativos de console .NET:</span><span class="sxs-lookup"><span data-stu-id="1a446-110">At the end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="1a446-111">**SimulatedDevice**, uma versão modificada do aplicativo criado no tutorial [Introdução ao Hub IoT], que envia mensagens de ponto de dados do dispositivo para a nuvem a cada segundo e mensagens interativas do dispositivo para a nuvem a cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="1a446-111">**SimulatedDevice**, a modified version of the app created in the [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="1a446-112">**ReadDeviceToCloudMessages**, que exibe a telemetria não crítica enviada pelo aplicativo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1a446-112">**ReadDeviceToCloudMessages** that displays the non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="1a446-113">**ReadCriticalQueue** retira da fila as mensagens críticas enviadas pelo seu aplicativo de dispositivo de uma fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="1a446-113">**ReadCriticalQueue** de-queues the critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="1a446-114">Essa fila é conectada ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1a446-114">This queue is attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="1a446-115">O Hub IoT tem suporte de SDK para várias plataformas de dispositivo e linguagens, incluindo C, Java e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1a446-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="1a446-116">Para saber como substituir o dispositivo simulado neste tutorial por um dispositivo físico, confira o [Centro de desenvolvedores do Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="1a446-116">To learn how to replace the simulated device in this tutorial with a physical device, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="1a446-117">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="1a446-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="1a446-118">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1a446-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="1a446-119">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a446-119">An active Azure account.</span></span> <br/><span data-ttu-id="1a446-120">Se você não tem uma conta, pode criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="1a446-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="1a446-121">Você também precisa ter um conhecimento básico do [Armazenamento do Azure] e do [Barramento de Serviço do Azure].</span><span class="sxs-lookup"><span data-stu-id="1a446-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="1a446-122">Enviar mensagens interativas</span><span class="sxs-lookup"><span data-stu-id="1a446-122">Send interactive messages</span></span>

<span data-ttu-id="1a446-123">Modifique o aplicativo de dispositivo criado no tutorial [Introdução ao Hub IoT] para enviar ocasionalmente mensagens interativas.</span><span class="sxs-lookup"><span data-stu-id="1a446-123">Modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send interactive messages.</span></span>

<span data-ttu-id="1a446-124">No Visual Studio, no projeto **SimulatedDevice**, substitua o método `SendDeviceToCloudMessagesAsync` pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a446-124">In Visual Studio, in the **SimulatedDevice** project, replace the `SendDeviceToCloudMessagesAsync` method with the following code:</span></span>

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

<span data-ttu-id="1a446-125">Isso adiciona aleatoriamente a propriedade `"level": "critical"` às mensagens enviadas pelo dispositivo, que simula uma mensagem que exige ação imediata do back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="1a446-125">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the solution back-end.</span></span> <span data-ttu-id="1a446-126">O aplicativo do dispositivo passa essas informações nas propriedades da mensagem, e não no corpo da mensagem, de modo que o Hub IoT pode rotear a mensagem para o destino apropriado.</span><span class="sxs-lookup"><span data-stu-id="1a446-126">The device app passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="1a446-127">Você pode usar as propriedades a fim de direcionar as mensagens para vários cenários, incluindo processamento de ampliação, além do exemplo de afunilamento mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="1a446-127">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="1a446-128">Para simplificar, esse tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="1a446-128">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1a446-129">No código de produção, você deve implementar políticas de repetição, como uma retirada exponencial, como sugerido no artigo [Tratamento de falhas transitórias]do MSDN.</span><span class="sxs-lookup"><span data-stu-id="1a446-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-to-a-queue-in-your-iot-hub"></a><span data-ttu-id="1a446-130">Rotear mensagens para uma fila em seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="1a446-130">Route messages to a queue in your IoT hub</span></span>

<span data-ttu-id="1a446-131">Nesta seção, você:</span><span class="sxs-lookup"><span data-stu-id="1a446-131">In this section, you:</span></span>

* <span data-ttu-id="1a446-132">Criará uma fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="1a446-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="1a446-133">A conectará ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1a446-133">Connect it to your IoT hub.</span></span>
* <span data-ttu-id="1a446-134">Configurará seu Hub IoT para enviar mensagens para a fila com base na presença de uma propriedade na mensagem.</span><span class="sxs-lookup"><span data-stu-id="1a446-134">Configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span>

<span data-ttu-id="1a446-135">Para saber mais sobre como processar mensagens das filas do Barramento de Serviço, confira [Introdução às filas][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="1a446-135">For more information about how to process messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="1a446-136">Crie uma fila do Barramento de Serviço conforme descrito em [Introdução às filas][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="1a446-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="1a446-137">A fila deve estar na mesma assinatura e região que o seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1a446-137">The queue must be in the same subscription and region as your IoT hub.</span></span> <span data-ttu-id="1a446-138">Anote o namespace e o nome da fila.</span><span class="sxs-lookup"><span data-stu-id="1a446-138">Make a note of the namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a446-139">As filas do Barramento de Serviço e os tópicos utilizados como pontos de extremidade do Hub IoT não devem ter **Sessões** nem **Detecção Duplicada** habilitadas.</span><span class="sxs-lookup"><span data-stu-id="1a446-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="1a446-140">Se qualquer uma dessas opções estiver habilitada, o ponto de extremidade aparecerá como **Inacessível** no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a446-140">If either of those options are enabled, the endpoint appears as **Unreachable** in the Azure portal.</span></span>

2. <span data-ttu-id="1a446-141">No Portal do Azure, abra o Hub IoT e clique em **Pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="1a446-141">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Pontos de extremidade no Hub IoT][30]

3. <span data-ttu-id="1a446-143">Na folha **Pontos de extremidade**, clique em **Adicionar** na parte superior para adicionar a fila ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1a446-143">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="1a446-144">Chame o ponto de extremidade de **CriticalQueue** e use o menu suspenso para selecionar **Fila do Barramento de Serviço**, o namespace do Barramento de Serviço no qual suas filas estão e o nome da sua fila.</span><span class="sxs-lookup"><span data-stu-id="1a446-144">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="1a446-145">Quando terminar, clique em **Salvar** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1a446-145">When you are done, click **Save** at the bottom.</span></span>
    
    ![Adicionando um ponto de extremidade][31]
    
4. <span data-ttu-id="1a446-147">Agora clique em **Rotas** no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1a446-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="1a446-148">Clique em **Adicionar** na parte superior da folha para criar uma regra que encaminhe mensagens para a fila que você acabou de adicionar.</span><span class="sxs-lookup"><span data-stu-id="1a446-148">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="1a446-149">Selecione **DeviceTelemetry** como a fonte dos dados.</span><span class="sxs-lookup"><span data-stu-id="1a446-149">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="1a446-150">Insira `level="critical"` como a condição e escolha a fila que acabou de adicionar como um ponto de extremidade personalizado como o ponto de extremidade de regra do direcionamento.</span><span class="sxs-lookup"><span data-stu-id="1a446-150">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="1a446-151">Quando terminar, clique em **Salvar** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1a446-151">When you are done, click **Save** at the bottom.</span></span>
    
    ![Adicionando uma rota][32]
    
    <span data-ttu-id="1a446-153">Verifique se a rota de fallback está definida como **ATIVADA**.</span><span class="sxs-lookup"><span data-stu-id="1a446-153">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="1a446-154">Essa é a configuração padrão para um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1a446-154">This value is the default configuration for an IoT hub.</span></span>
    
    ![Rota de fallback][33]

## <a name="read-from-the-queue-endpoint"></a><span data-ttu-id="1a446-156">Ler no ponto de extremidade da fila</span><span class="sxs-lookup"><span data-stu-id="1a446-156">Read from the queue endpoint</span></span>

<span data-ttu-id="1a446-157">Nesta seção, você lê as mensagens no ponto de extremidade da fila.</span><span class="sxs-lookup"><span data-stu-id="1a446-157">In this section, you read the messages from the queue endpoint.</span></span>

1. <span data-ttu-id="1a446-158">No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# à solução atual usando o modelo de projeto **Aplicativo do Console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="1a446-158">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="1a446-159">Dê ao projeto o nome de **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="1a446-159">Name the project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="1a446-160">No Gerenciador de Soluções, clique com o botão direito no projeto **ReadCriticalQueue** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1a446-160">In Solution Explorer, right-click the **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="1a446-161">Esta operação faz com que a janela **Gerenciador de Pacotes NuGet** seja exibida.</span><span class="sxs-lookup"><span data-stu-id="1a446-161">This operation displays the **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="1a446-162">Pesquise por **WindowsAzure.ServiceBus**, clique em **Instalar** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="1a446-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept the terms of use.</span></span> <span data-ttu-id="1a446-163">Essa operação baixa, instala e adiciona uma referência ao Barramento de Serviço do Azure, com todas as suas dependências.</span><span class="sxs-lookup"><span data-stu-id="1a446-163">This operation downloads, installs, and adds a reference to the Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="1a446-164">Adicione a seguinte instrução **using** à parte superior do arquivo **Program.cs**:</span><span class="sxs-lookup"><span data-stu-id="1a446-164">Add the following **using** statements at the top of the **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="1a446-165">Por fim, adicione as seguintes linhas ao método **Main** .</span><span class="sxs-lookup"><span data-stu-id="1a446-165">Finally, add the following lines to the **Main** method.</span></span> <span data-ttu-id="1a446-166">Substitua a cadeia de conexão por permissões **Escutar** para a fila:</span><span class="sxs-lookup"><span data-stu-id="1a446-166">Substitute the connection string with **Listen** permissions for the queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C to exit.\n");
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

## <a name="run-the-applications"></a><span data-ttu-id="1a446-167">Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="1a446-167">Run the applications</span></span>
<span data-ttu-id="1a446-168">Agora você está pronto para executar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1a446-168">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="1a446-169">No Visual Studio, no Gerenciador de Soluções, clique com o botão direito do mouse na solução e selecione **Definir Projetos de Inicialização**.</span><span class="sxs-lookup"><span data-stu-id="1a446-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="1a446-170">Selecione **Vários projetos de inicialização** e selecione **Iniciar** como a ação para os projetos **ReadDeviceToCloudMessages**, **SimulatedDevice** e **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="1a446-170">Select **Multiple startup projects**, then select **Start** as the action for the **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="1a446-171">Pressione **F5** para iniciar os três aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="1a446-171">Press **F5** to start the three console apps.</span></span> <span data-ttu-id="1a446-172">O aplicativo **ReadDeviceToCloudMessages** tem somente mensagens não críticas enviadas do aplicativo **SimulatedDevice** e o aplicativo **ReadCriticalQueue** tem somente mensagens críticas.</span><span class="sxs-lookup"><span data-stu-id="1a446-172">The **ReadDeviceToCloudMessages** app has only non-critical messages sent from the **SimulatedDevice** application, and the **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Três aplicativos de console][50]

## <a name="next-steps"></a><span data-ttu-id="1a446-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1a446-174">Next steps</span></span>
<span data-ttu-id="1a446-175">Neste tutorial, você aprendeu a expedir confiavelmente mensagens do dispositivo para nuvem usando a funcionalidade de roteamento de mensagens do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1a446-175">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="1a446-176">O tutorial [Como enviar mensagens da nuvem para o dispositivo com o Hub IoT][lnk-c2d] mostra como enviar mensagens da solução de back-end para seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="1a446-176">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="1a446-177">Para ver exemplos de soluções completas que usam o Hub IoT, veja [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="1a446-177">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="1a446-178">Para saber mais sobre como desenvolver soluções com o Hub IoT, consulte o [Guia do desenvolvedor do Hub IoT].</span><span class="sxs-lookup"><span data-stu-id="1a446-178">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="1a446-179">Para saber mais sobre o roteamento de mensagens no Hub IoT, confira [Enviar e receber mensagens com o Hub IoT][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="1a446-179">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
<span data-ttu-id="1a446-180">[Armazenamento do Azure]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="1a446-180">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="1a446-181">[Barramento de Serviço do Azure]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="1a446-181">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>
<span data-ttu-id="1a446-182">[Guia do desenvolvedor do Hub IoT]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="1a446-182">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="1a446-183">[Introdução ao Hub IoT]: iot-hub-csharp-csharp-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="1a446-183">[Get started with IoT Hub]: iot-hub-csharp-csharp-getstarted.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="1a446-184">[Centro de desenvolvedores do Azure IoT]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="1a446-184">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="1a446-185">[Tratamento de falhas transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="1a446-185">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
