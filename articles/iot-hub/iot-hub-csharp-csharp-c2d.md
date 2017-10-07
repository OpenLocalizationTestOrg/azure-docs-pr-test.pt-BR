---
title: mensagens de aaaCloud para o dispositivo com o Azure IoT Hub (.NET) | Microsoft Docs
description: "Como toosend de nuvem para dispositivo mensagens tooa dispositivo de um hub IoT do Azure usando Olá SDKs de IoT do Azure para .NET. Modificar as mensagens de nuvem para dispositivo um dispositivo aplicativo tooreceive e modificar as mensagens de nuvem para dispositivo um aplicativo de back-end toosend hello."
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
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a><span data-ttu-id="0b081-104">Enviar mensagens de dispositivo de tooyour Olá nuvem com o Hub IoT (.NET)</span><span class="sxs-lookup"><span data-stu-id="0b081-104">Send messages from hello cloud tooyour device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="0b081-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="0b081-105">Introduction</span></span>
<span data-ttu-id="0b081-106">O Hub IoT do Azure é um serviço totalmente gerenciado que ajuda a permitir comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end de solução.</span><span class="sxs-lookup"><span data-stu-id="0b081-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="0b081-107">Olá [começar com o IoT Hub] tutorial mostra como toocreate um hub IoT, provisionar uma identidade de dispositivo nele e código de um aplicativo de dispositivo que envia mensagens de dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="0b081-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="0b081-108">Esse tutorial se baseia na [começar com o IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="0b081-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="0b081-109">Ele mostra como:</span><span class="sxs-lookup"><span data-stu-id="0b081-109">It shows you how to:</span></span>

* <span data-ttu-id="0b081-110">Sua solução back-end, envie mensagens de nuvem para dispositivo tooa único dispositivo por meio de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0b081-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="0b081-111">Receber mensagens da nuvem para o dispositivo em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b081-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="0b081-112">De sua solução back-end, solicitar confirmação de entrega (*comentários*) para mensagens enviadas tooa dispositivo do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0b081-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="0b081-113">Você pode encontrar mais informações sobre mensagens de nuvem para dispositivo em Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="0b081-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="0b081-114">No final da saudação deste tutorial, você deve executar dois aplicativos de console do .NET:</span><span class="sxs-lookup"><span data-stu-id="0b081-114">At hello end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="0b081-115">**SimulatedDevice**, uma versão modificada do aplicativo hello criado no [começar com o IoT Hub], que se conecta tooyour IoT hub e recebe mensagens de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b081-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="0b081-116">**SendCloudToDevice**, que envia um aplicativo de dispositivo de toohello de mensagem de nuvem para dispositivo por meio de IoT Hub e, em seguida, recebe a sua confirmação de entrega.</span><span class="sxs-lookup"><span data-stu-id="0b081-116">**SendCloudToDevice**, which sends a cloud-to-device message toohello device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="0b081-117">O Hub IoT tem suporte a SDK para várias plataformas de dispositivo e linguagens (incluindo C, Java e Javascript) nos [SDKs do dispositivo IoT do Azure].</span><span class="sxs-lookup"><span data-stu-id="0b081-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="0b081-118">Para obter instruções passo a passo sobre como tooconnect do seu dispositivo toothis tutorial código e geralmente tooAzure IoT Hub, consulte Olá [guia do desenvolvedor de IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="0b081-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="0b081-119">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b081-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="0b081-120">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0b081-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="0b081-121">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b081-121">An active Azure account.</span></span> <span data-ttu-id="0b081-122">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="0b081-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-device-app"></a><span data-ttu-id="0b081-123">Receber mensagens no aplicativo de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="0b081-123">Receive messages in hello device app</span></span>
<span data-ttu-id="0b081-124">Nesta seção, você modificará o aplicativo para dispositivo Olá criado na [começar com o IoT Hub] tooreceive mensagens de nuvem para dispositivo do hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b081-124">In this section, you'll modify hello device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="0b081-125">No Visual Studio, no hello **SimulatedDevice** de projeto, adicione Olá após o método toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="0b081-125">In Visual Studio, in hello **SimulatedDevice** project, add hello following method toohello **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
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
   
    <span data-ttu-id="0b081-126">Olá `ReceiveAsync` método retorna de maneira assíncrona mensagem recebida em tempo de saudação são recebidos pelo dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b081-126">hello `ReceiveAsync` method asynchronously returns hello received message at hello time that it is received by hello device.</span></span> <span data-ttu-id="0b081-127">Ele retorna *nulo* após um período de tempo limite especificáveis (nesse caso, padrão de saudação de um minuto é usado).</span><span class="sxs-lookup"><span data-stu-id="0b081-127">It returns *null* after a specifiable timeout period (in this case, hello default of one minute is used).</span></span> <span data-ttu-id="0b081-128">Quando o aplicativo hello recebe um *nulo*, deveria continuar toowait novas mensagens.</span><span class="sxs-lookup"><span data-stu-id="0b081-128">When hello app receives a *null*, it should continue toowait for new messages.</span></span> <span data-ttu-id="0b081-129">Esse requisito é motivo Olá Olá `if (receivedMessage == null) continue` linha.</span><span class="sxs-lookup"><span data-stu-id="0b081-129">This requirement is hello reason for hello `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="0b081-130">Olá chamada muito`CompleteAsync()` notifica o IoT Hub essa mensagem de saudação foi processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="0b081-130">hello call too`CompleteAsync()` notifies IoT Hub that hello message has been successfully processed.</span></span> <span data-ttu-id="0b081-131">mensagem de saudação com segurança pode ser removida da fila de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b081-131">hello message can be safely removed from hello device queue.</span></span> <span data-ttu-id="0b081-132">Se algo acontecer esse aplicativo de dispositivo Olá impedido de concluir o processamento de mensagem de saudação hello, IoT Hub entrega novamente.</span><span class="sxs-lookup"><span data-stu-id="0b081-132">If something happened that prevented hello device app from completing hello processing of hello message, IoT Hub delivers it again.</span></span> <span data-ttu-id="0b081-133">Em seguida, é importante que lógica Olá dispositivo aplicativo de processamento de mensagens for *idempotente*, de modo que receber Olá mesma mensagem várias vezes produz Olá mesmo resultado.</span><span class="sxs-lookup"><span data-stu-id="0b081-133">It is then important that message processing logic in hello device app is *idempotent*, so that receiving hello same message multiple times produces hello same result.</span></span> <span data-ttu-id="0b081-134">Um aplicativo pode também temporariamente abandonar uma mensagem, o que resulta em um hub IoT mantém a mensagem de saudação na fila de saudação para consumo futuro.</span><span class="sxs-lookup"><span data-stu-id="0b081-134">An application can also temporarily abandon a message, which results in IoT hub retaining hello message in hello queue for future consumption.</span></span> <span data-ttu-id="0b081-135">Ou, o aplicativo hello pode rejeitar uma mensagem, que remove permanentemente a mensagem de saudação da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b081-135">Or, hello application can reject a message, which permanently removes hello message from hello queue.</span></span> <span data-ttu-id="0b081-136">Para obter mais informações sobre o ciclo de vida de mensagem de nuvem para dispositivo Olá, consulte Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="0b081-136">For more information about hello cloud-to-device message lifecycle, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0b081-137">Ao usar HTTP em vez de MQTT ou AMQP como transporte, Olá `ReceiveAsync` método retorna imediatamente.</span><span class="sxs-lookup"><span data-stu-id="0b081-137">When using HTTP instead of MQTT or AMQP as a transport, hello `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="0b081-138">padrão de saudação com suporte para mensagens de nuvem para dispositivo com HTTP é dispositivos conectados intermitentemente que verifiquem mensagens raramente (menor cada 25 minutos).</span><span class="sxs-lookup"><span data-stu-id="0b081-138">hello supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="0b081-139">Emitir HTTP mais recebe os resultados em solicitações de saudação de limitação de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0b081-139">Issuing more HTTP receives results in IoT Hub throttling hello requests.</span></span> <span data-ttu-id="0b081-140">Para obter mais informações sobre as diferenças de saudação entre suporte MQTT, AMQP e HTTP e a limitação de Hub IoT, consulte Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="0b081-140">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="0b081-141">Adicionar Olá seguinte método em Olá **principal** método antes de saudação `Console.ReadLine()` linha:</span><span class="sxs-lookup"><span data-stu-id="0b081-141">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="0b081-142">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="0b081-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="0b081-143">No código de produção, você deve implementar políticas de repetição (por exemplo, a retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].</span><span class="sxs-lookup"><span data-stu-id="0b081-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="0b081-144">Envie uma mensagem da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="0b081-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="0b081-145">Nesta seção, você pode escrever um aplicativo de console .NET que envia mensagens de nuvem para dispositivo toohello dispositivo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0b081-145">In this section, you write a .NET console app that sends cloud-to-device messages toohello device app.</span></span>

1. <span data-ttu-id="0b081-146">Na solução atual do Visual Studio hello, criar um projeto de aplicativo de área de trabalho do Visual C# usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="0b081-146">In hello current Visual Studio solution, create a Visual C# Desktop App project by using hello **Console Application** project template.</span></span> <span data-ttu-id="0b081-147">Projeto de saudação do nome **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="0b081-147">Name hello project **SendCloudToDevice**.</span></span>
   
    ![Novo projeto no Visual Studio][20]
2. <span data-ttu-id="0b081-149">No Gerenciador de soluções, clique com botão direito solução hello e, em seguida, clique em **gerenciar pacotes NuGet para solução...** .</span><span class="sxs-lookup"><span data-stu-id="0b081-149">In Solution Explorer, right-click hello solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="0b081-150">Essa ação abre Olá **gerenciar pacotes NuGet** janela.</span><span class="sxs-lookup"><span data-stu-id="0b081-150">This action opens hello **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="0b081-151">Procurar **Microsoft.Azure.Devices**, clique em **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="0b081-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span> 
   
    <span data-ttu-id="0b081-152">Isso baixa, instala e adiciona uma referência toohello [pacote de NuGet do SDK do serviço de Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="0b081-152">This downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="0b081-153">Adicione o seguinte Olá `using` instrução na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="0b081-153">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="0b081-154">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="0b081-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="0b081-155">Substituir valor de espaço reservado de saudação com a cadeia de conexão do hello IoT hub do [começar com o IoT Hub]:</span><span class="sxs-lookup"><span data-stu-id="0b081-155">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="0b081-156">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="0b081-156">Add hello following method toohello **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="0b081-157">Esse método envia um novo dispositivo toohello mensagem de nuvem para dispositivo com a ID de saudação `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="0b081-157">This method sends a new cloud-to-device message toohello device with hello ID, `myFirstDevice`.</span></span> <span data-ttu-id="0b081-158">Altere este parâmetro somente se ele tenha sido modificado de saudação usado no [começar com o IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="0b081-158">Change this parameter only if you modified it from hello one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="0b081-159">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="0b081-159">Finally, add hello following lines toohello **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="0b081-160">No Visual Studio, clique com o botão direito do mouse na solução e selecione **Definir Projetos de inicialização...**. Selecione **vários projetos de inicialização**, em seguida, selecione Olá **iniciar** ação para **ReadDeviceToCloudMessages**, **SimulatedDevice**, e **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="0b081-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select hello **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="0b081-161">Pressione **F5**.</span><span class="sxs-lookup"><span data-stu-id="0b081-161">Press **F5**.</span></span> <span data-ttu-id="0b081-162">Todos os três aplicativos devem ser iniciados.</span><span class="sxs-lookup"><span data-stu-id="0b081-162">All three applications should start.</span></span> <span data-ttu-id="0b081-163">Selecione Olá **SendCloudToDevice** windows e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0b081-163">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="0b081-164">Você deve ver a mensagem de saudação sendo recebida pelo aplicativo de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b081-164">You should see hello message being received by hello device app.</span></span>
   
   ![Aplicativo recebendo mensagens][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="0b081-166">Receber comentários de entrega</span><span class="sxs-lookup"><span data-stu-id="0b081-166">Receive delivery feedback</span></span>
<span data-ttu-id="0b081-167">É confirmações de entrega (ou expiração) toorequest possíveis de IoT Hub para cada mensagem de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b081-167">It is possible toorequest delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="0b081-168">Essa opção permite Olá solução back-end tooeasily informam a lógica de repetição ou compensação.</span><span class="sxs-lookup"><span data-stu-id="0b081-168">This option enables hello solution back end tooeasily inform retry or compensation logic.</span></span> <span data-ttu-id="0b081-169">Para obter mais informações sobre seus comentários de nuvem para dispositivo, consulte Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="0b081-169">For more information about cloud-to-device feedback, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="0b081-170">Nesta seção, você modificar Olá **SendCloudToDevice** comentários toorequest do aplicativo e recebê-las de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0b081-170">In this section, you modify hello **SendCloudToDevice** app toorequest feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="0b081-171">No Visual Studio, no hello **SendCloudToDevice** de projeto, adicione Olá após o método toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="0b081-171">In Visual Studio, in hello **SendCloudToDevice** project, add hello following method toohello **Program** class.</span></span>
   
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
   
    <span data-ttu-id="0b081-172">Observe que esse padrão de recebimento é Olá mensagens de nuvem para dispositivo tooreceive usado um mesmo do aplicativo de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b081-172">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>
2. <span data-ttu-id="0b081-173">Adicionar Olá seguinte método em Olá **principal** método logo após Olá `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` linha:</span><span class="sxs-lookup"><span data-stu-id="0b081-173">Add hello following method in hello **Main** method, right after hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="0b081-174">comentários toorequest para entrega de saudação da mensagem de nuvem para dispositivo, você tem toospecify uma propriedade em Olá **SendCloudToDeviceMessageAsync** método.</span><span class="sxs-lookup"><span data-stu-id="0b081-174">toorequest feedback for hello delivery of your cloud-to-device message, you have toospecify a property in hello **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="0b081-175">Adicionar Olá a seguinte linha, à direita após Olá `var commandMessage = new Message(...);` linha:</span><span class="sxs-lookup"><span data-stu-id="0b081-175">Add hello following line, right after hello `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="0b081-176">Executar aplicativos Olá pressionando **F5**.</span><span class="sxs-lookup"><span data-stu-id="0b081-176">Run hello apps by pressing **F5**.</span></span> <span data-ttu-id="0b081-177">Você deve ver todos os três aplicativos serem iniciados.</span><span class="sxs-lookup"><span data-stu-id="0b081-177">You should see all three applications start.</span></span> <span data-ttu-id="0b081-178">Selecione Olá **SendCloudToDevice** windows e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0b081-178">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="0b081-179">Você deve ver Olá mensagem sendo recebidas pelo aplicativo de dispositivo hello e após alguns segundos, Olá mensagem comentários recebida pelo seu **SendCloudToDevice** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0b081-179">You should see hello message being received by hello device app, and after a few seconds, hello feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![Aplicativo recebendo mensagens][22]

> [!NOTE]
> <span data-ttu-id="0b081-181">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="0b081-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="0b081-182">No código de produção, você deve implementar políticas de repetição (por exemplo, a retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].</span><span class="sxs-lookup"><span data-stu-id="0b081-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0b081-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0b081-183">Next steps</span></span>
<span data-ttu-id="0b081-184">Neste tutorial, você aprendeu como toosend e receber mensagens de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b081-184">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="0b081-185">exemplos de toosee de soluções completas de ponta a ponta que usam o IoT Hub, consulte [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="0b081-185">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="0b081-186">toolearn mais sobre como desenvolver soluções com o IoT Hub, consulte Olá [guia do desenvolvedor de IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="0b081-186">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[pacote de NuGet do SDK do serviço de Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[tratamento de falhas transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[guia do desenvolvedor de IoT Hub]: iot-hub-devguide.md
[começar com o IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[SDKs do dispositivo IoT do Azure]: iot-hub-devguide-sdks.md