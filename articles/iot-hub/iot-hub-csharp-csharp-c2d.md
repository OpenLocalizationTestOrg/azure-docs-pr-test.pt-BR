---
title: Mensagens da nuvem para o dispositivo com o Hub IoT do Azure (.NET)| Microsoft Docs
description: "Como enviar mensagens da nuvem para o dispositivo para um dispositivo de um Hub IoT do Azure usando os SDKs do IoT do Azure para .NET. Você modifica um aplicativo de dispositivo para receber mensagens da nuvem para o dispositivo e modificar um aplicativo de back-end para enviá-las."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: 3f5f83671054c30afde3d7f18ff0edcdb8f78a01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="send-messages-from-the-cloud-to-your-device-with-iot-hub-net"></a><span data-ttu-id="36ffb-104">Enviar mensagens de nuvem para seu dispositivo com o Hub IoT (.NET)</span><span class="sxs-lookup"><span data-stu-id="36ffb-104">Send messages from the cloud to your device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="36ffb-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="36ffb-105">Introduction</span></span>
<span data-ttu-id="36ffb-106">O Hub IoT do Azure é um serviço totalmente gerenciado que ajuda a permitir comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end de solução.</span><span class="sxs-lookup"><span data-stu-id="36ffb-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="36ffb-107">O tutorial [Introdução ao Hub IoT] mostra como criar um hub IoT, provisionar uma identidade do dispositivo nele e codificar um aplicativo do dispositivo que envie mensagens do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="36ffb-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="36ffb-108">Esse tutorial se baseia na [Introdução ao Hub IoT].</span><span class="sxs-lookup"><span data-stu-id="36ffb-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="36ffb-109">Ele mostra como:</span><span class="sxs-lookup"><span data-stu-id="36ffb-109">It shows you how to:</span></span>

* <span data-ttu-id="36ffb-110">Da sua solução de back-end, envie mensagens da nuvem para o dispositivo em um único dispositivo por meio do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36ffb-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="36ffb-111">Receber mensagens da nuvem para o dispositivo em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="36ffb-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="36ffb-112">Da sua solução de back-end, solicite confirmação de entrega (*comentários*) para as mensagens enviadas a um dispositivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36ffb-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="36ffb-113">É possível encontrar mais informações sobre as mensagens da nuvem para o dispositivo no [Guia do Desenvolvedor do Hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="36ffb-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="36ffb-114">No final deste tutorial, você executará dois aplicativos do console .NET:</span><span class="sxs-lookup"><span data-stu-id="36ffb-114">At the end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="36ffb-115">**SimulatedDevice**, uma versão modificada do aplicativo criado na [Introdução ao Hub IoT], que se conecta a seu hub IoT e recebe mensagens da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="36ffb-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="36ffb-116">**SendCloudToDevice**, que envia uma mensagem da nuvem para o dispositivo ao aplicativo do dispositivo por meio do Hub IoT e recebe sua confirmação de entrega.</span><span class="sxs-lookup"><span data-stu-id="36ffb-116">**SendCloudToDevice**, which sends a cloud-to-device message to the device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="36ffb-117">O Hub IoT tem suporte a SDK para várias plataformas de dispositivo e linguagens (incluindo C, Java e Javascript) nos [SDKs do dispositivo IoT do Azure].</span><span class="sxs-lookup"><span data-stu-id="36ffb-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="36ffb-118">Para obter instruções passo a passo sobre como conectar seu dispositivo ao código deste tutorial e, em geral, ao Hub IoT do Azure, veja o [Guia do desenvolvedor do Hub IoT].</span><span class="sxs-lookup"><span data-stu-id="36ffb-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="36ffb-119">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="36ffb-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="36ffb-120">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="36ffb-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="36ffb-121">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="36ffb-121">An active Azure account.</span></span> <span data-ttu-id="36ffb-122">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="36ffb-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-device-app"></a><span data-ttu-id="36ffb-123">Receber mensagens no aplicativo do dispositivo</span><span class="sxs-lookup"><span data-stu-id="36ffb-123">Receive messages in the device app</span></span>
<span data-ttu-id="36ffb-124">Nesta seção, você modificará o aplicativo do dispositivo criado na [Introdução ao Hub IoT] para receber mensagens da nuvem para o dispositivo do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36ffb-124">In this section, you'll modify the device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="36ffb-125">No Visual Studio, no projeto **SimulatedDevice**, adicione o método a seguir à classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="36ffb-125">In Visual Studio, in the **SimulatedDevice** project, add the following method to the **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud to device messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    <span data-ttu-id="36ffb-126">O método `ReceiveAsync` retorna de forma assíncrona a mensagem recebida no momento em que ela é recebida pelo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="36ffb-126">The `ReceiveAsync` method asynchronously returns the received message at the time that it is received by the device.</span></span> <span data-ttu-id="36ffb-127">Ela retorna *null* após um período de tempo limite especificável (nesse caso, será usado o padrão de um minuto).</span><span class="sxs-lookup"><span data-stu-id="36ffb-127">It returns *null* after a specifiable timeout period (in this case, the default of one minute is used).</span></span> <span data-ttu-id="36ffb-128">Quando o aplicativo recebe *null*, ele deve continuar aguardando novas mensagens.</span><span class="sxs-lookup"><span data-stu-id="36ffb-128">When the app receives a *null*, it should continue to wait for new messages.</span></span> <span data-ttu-id="36ffb-129">Esse requisito é o motivo da linha `if (receivedMessage == null) continue`.</span><span class="sxs-lookup"><span data-stu-id="36ffb-129">This requirement is the reason for the `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="36ffb-130">A chamada para `CompleteAsync()` notifica o Hub IoT de que a mensagem foi processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="36ffb-130">The call to `CompleteAsync()` notifies IoT Hub that the message has been successfully processed.</span></span> <span data-ttu-id="36ffb-131">A mensagem pode ser removida da fila do dispositivo com segurança.</span><span class="sxs-lookup"><span data-stu-id="36ffb-131">The message can be safely removed from the device queue.</span></span> <span data-ttu-id="36ffb-132">Se ocorreu algo que impediu que o aplicativo do dispositivo concluísse o processamento da mensagem, o Hub IoT a entrega novamente.</span><span class="sxs-lookup"><span data-stu-id="36ffb-132">If something happened that prevented the device app from completing the processing of the message, IoT Hub delivers it again.</span></span> <span data-ttu-id="36ffb-133">Também é importante que a lógica de processamento de mensagem no aplicativo do dispositivo seja *idempotente*, de modo que receber a mesma mensagem várias vezes produza o mesmo resultado.</span><span class="sxs-lookup"><span data-stu-id="36ffb-133">It is then important that message processing logic in the device app is *idempotent*, so that receiving the same message multiple times produces the same result.</span></span> <span data-ttu-id="36ffb-134">Um aplicativo também pode abandonar temporariamente uma mensagem, o que resulta em um Hub IoT reter a mensagem na fila para consumo futuro.</span><span class="sxs-lookup"><span data-stu-id="36ffb-134">An application can also temporarily abandon a message, which results in IoT hub retaining the message in the queue for future consumption.</span></span> <span data-ttu-id="36ffb-135">Ou, o aplicativo pode rejeitar uma mensagem, que a remove permanentemente da fila.</span><span class="sxs-lookup"><span data-stu-id="36ffb-135">Or, the application can reject a message, which permanently removes the message from the queue.</span></span> <span data-ttu-id="36ffb-136">Para saber mais sobre o ciclo de vida da mensagem da nuvem para o dispositivo, veja o [Guia do desenvolvedor do Hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="36ffb-136">For more information about the cloud-to-device message lifecycle, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="36ffb-137">Ao usar HTTP em vez de MQTT ou AMQP como transporte, o método `ReceiveAsync` é retornado imediatamente.</span><span class="sxs-lookup"><span data-stu-id="36ffb-137">When using HTTP instead of MQTT or AMQP as a transport, the `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="36ffb-138">O padrão com suporte para mensagens da nuvem para o dispositivo com o HTTP são dispositivos conectados intermitentemente que verificam mensagens com pouca frequência (menos do que a cada 25 minutos).</span><span class="sxs-lookup"><span data-stu-id="36ffb-138">The supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="36ffb-139">Emitir mais recebimentos de HTTP resulta na limitação das solicitações pelo Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36ffb-139">Issuing more HTTP receives results in IoT Hub throttling the requests.</span></span> <span data-ttu-id="36ffb-140">Para obter mais informações sobre as diferenças entre o suporte do MQTT, AMQP e HTTP e a limitação do Hub IoT, consulte o [Guia do Desenvolvedor do Hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="36ffb-140">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="36ffb-141">Adicione o seguinte método ao método **Main**, logo antes da linha `Console.ReadLine()`:</span><span class="sxs-lookup"><span data-stu-id="36ffb-141">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="36ffb-142">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="36ffb-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="36ffb-143">No código de produção, implemente políticas de repetição (como uma retirada exponencial), conforme sugestão no artigo [Tratamento de Falhas Transitórias]do MSDN.</span><span class="sxs-lookup"><span data-stu-id="36ffb-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="36ffb-144">Envie uma mensagem da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="36ffb-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="36ffb-145">Nesta seção, você escreve um aplicativo de console .NET que envia mensagens da nuvem para o dispositivo ao aplicativo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="36ffb-145">In this section, you write a .NET console app that sends cloud-to-device messages to the device app.</span></span>

1. <span data-ttu-id="36ffb-146">Na solução do Visual Studio atual, crie um projeto de Aplicativo da Área de Trabalho do Visual C# usando o modelo de projeto do **Aplicativo do Console**.</span><span class="sxs-lookup"><span data-stu-id="36ffb-146">In the current Visual Studio solution, create a Visual C# Desktop App project by using the **Console Application** project template.</span></span> <span data-ttu-id="36ffb-147">Nomeie o projeto **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="36ffb-147">Name the project **SendCloudToDevice**.</span></span>
   
    ![Novo projeto no Visual Studio][20]
2. <span data-ttu-id="36ffb-149">No Gerenciador de Soluções, clique com o botão direito do mouse na solução e, então, clique em **Gerenciar Pacotes NuGet para Solução...**.</span><span class="sxs-lookup"><span data-stu-id="36ffb-149">In Solution Explorer, right-click the solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="36ffb-150">Essa ação abre a janela **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="36ffb-150">This action opens the **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="36ffb-151">Pesquise por **Microsoft.Azure.Devices**, clique em **Instalar** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="36ffb-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span> 
   
    <span data-ttu-id="36ffb-152">Isso baixa, instala e adiciona uma referência ao [pacote NuGet do SDK do serviço IoT do Azure].</span><span class="sxs-lookup"><span data-stu-id="36ffb-152">This downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="36ffb-153">Adicione a seguinte instrução `using` na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="36ffb-153">Add the following `using` statement at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="36ffb-154">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="36ffb-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="36ffb-155">Substitua os valores de espaço reservado pela cadeia de conexão do Hub IoT da [Introdução ao Hub IoT]:</span><span class="sxs-lookup"><span data-stu-id="36ffb-155">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="36ffb-156">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="36ffb-156">Add the following method to the **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud to device message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="36ffb-157">Esse método envia uma nova mensagem da nuvem para o dispositivo ao dispositivo com a ID `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="36ffb-157">This method sends a new cloud-to-device message to the device with the ID, `myFirstDevice`.</span></span> <span data-ttu-id="36ffb-158">Altere este parâmetro somente se o tiver modificado com base no usado em [Introdução ao Hub IoT].</span><span class="sxs-lookup"><span data-stu-id="36ffb-158">Change this parameter only if you modified it from the one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="36ffb-159">Por fim, adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="36ffb-159">Finally, add the following lines to the **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key to send a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="36ffb-160">No Visual Studio, clique com o botão direito do mouse na solução e selecione **Definir Projetos de inicialização...**. Selecione **Vários projetos de inicialização** e, em seguida, selecione a ação **Iniciar** para **ProcessDeviceToCloudMessages**, **SimulatedDevice** e **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="36ffb-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select the **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="36ffb-161">Pressione **F5**.</span><span class="sxs-lookup"><span data-stu-id="36ffb-161">Press **F5**.</span></span> <span data-ttu-id="36ffb-162">Todos os três aplicativos devem ser iniciados.</span><span class="sxs-lookup"><span data-stu-id="36ffb-162">All three applications should start.</span></span> <span data-ttu-id="36ffb-163">Selecione as janelas **SendCloudToDevice** e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="36ffb-163">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="36ffb-164">Você deve ver a mensagem que está sendo recebida pelo aplicativo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="36ffb-164">You should see the message being received by the device app.</span></span>
   
   ![Aplicativo recebendo mensagens][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="36ffb-166">Receber comentários de entrega</span><span class="sxs-lookup"><span data-stu-id="36ffb-166">Receive delivery feedback</span></span>
<span data-ttu-id="36ffb-167">É possível solicitar confirmações de entrega (ou expiração) de Hub IoT para cada mensagem da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="36ffb-167">It is possible to request delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="36ffb-168">Essa opção permite que o back-end da solução informe a lógica de repetição ou de compensação facilmente.</span><span class="sxs-lookup"><span data-stu-id="36ffb-168">This option enables the solution back end to easily inform retry or compensation logic.</span></span> <span data-ttu-id="36ffb-169">Para saber mais sobre os comentários da nuvem para o dispositivo, veja o [Guia do desenvolvedor do Hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="36ffb-169">For more information about cloud-to-device feedback, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="36ffb-170">Nesta seção, você modificará o aplicativo **SendCloudToDevice** para solicitar comentários e recebê-lo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36ffb-170">In this section, you modify the **SendCloudToDevice** app to request feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="36ffb-171">No Visual Studio, no projeto **SendCloudToDevice**, adicione o método a seguir à classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="36ffb-171">In Visual Studio, in the **SendCloudToDevice** project, add the following method to the **Program** class.</span></span>
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    <span data-ttu-id="36ffb-172">É importante lembrar que o padrão de recebimento é o mesmo usado para receber mensagens da nuvem para o dispositivo do aplicativo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="36ffb-172">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>
2. <span data-ttu-id="36ffb-173">Adicione o seguinte método ao método **Main**, logo após a linha `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)`:</span><span class="sxs-lookup"><span data-stu-id="36ffb-173">Add the following method in the **Main** method, right after the `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="36ffb-174">Para solicitar comentários sobre a entrega da mensagem da nuvem para o dispositivo, você deve especificar uma propriedade no método **SendCloudToDeviceMessageAsync** .</span><span class="sxs-lookup"><span data-stu-id="36ffb-174">To request feedback for the delivery of your cloud-to-device message, you have to specify a property in the **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="36ffb-175">Adicione a seguinte linha, logo após a linha `var commandMessage = new Message(...);` :</span><span class="sxs-lookup"><span data-stu-id="36ffb-175">Add the following line, right after the `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="36ffb-176">Execute os aplicativos pressionando **F5**.</span><span class="sxs-lookup"><span data-stu-id="36ffb-176">Run the apps by pressing **F5**.</span></span> <span data-ttu-id="36ffb-177">Você deve ver todos os três aplicativos serem iniciados.</span><span class="sxs-lookup"><span data-stu-id="36ffb-177">You should see all three applications start.</span></span> <span data-ttu-id="36ffb-178">Selecione as janelas **SendCloudToDevice** e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="36ffb-178">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="36ffb-179">Você deve ver a mensagem sendo recebida pelo aplicativo do dispositivo e, depois de alguns segundos, a mensagem de comentários sendo recebida pelo aplicativo **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="36ffb-179">You should see the message being received by the device app, and after a few seconds, the feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![Aplicativo recebendo mensagens][22]

> [!NOTE]
> <span data-ttu-id="36ffb-181">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="36ffb-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="36ffb-182">No código de produção, implemente políticas de repetição (como uma retirada exponencial), conforme sugestão no artigo [Tratamento de Falhas Transitórias]do MSDN.</span><span class="sxs-lookup"><span data-stu-id="36ffb-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="36ffb-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="36ffb-183">Next steps</span></span>
<span data-ttu-id="36ffb-184">Neste tutorial você aprendeu a enviar e receber mensagens da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="36ffb-184">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="36ffb-185">Para ver exemplos de soluções completas que usam o Hub IoT, consulte [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="36ffb-185">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="36ffb-186">Para saber mais sobre como desenvolver soluções com o Hub IoT, consulte o [Guia do desenvolvedor do Hub IoT].</span><span class="sxs-lookup"><span data-stu-id="36ffb-186">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[pacote NuGet do SDK do serviço IoT do Azure]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[Tratamento de Falhas Transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[Guia do desenvolvedor do Hub IoT]: iot-hub-devguide.md
[Introdução ao Hub IoT]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[SDKs do dispositivo IoT do Azure]: iot-hub-devguide-sdks.md