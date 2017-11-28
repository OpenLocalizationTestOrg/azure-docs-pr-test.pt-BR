---
title: aaaProcess mensagens de dispositivo para a nuvem do Azure IoT Hub (Java) | Microsoft Docs
description: "Como tooprocess mensagens de dispositivo para a nuvem de IoT Hub usando regras de roteamento e pontos de extremidade personalizados toodispatch mensagens tooother serviços de back-end."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="48914-103">Processar mensagens do Hub IoT do dispositivo para nuvem (Java)</span><span class="sxs-lookup"><span data-stu-id="48914-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="48914-104">O Hub IoT do Azure é um serviço totalmente gerenciado que permite comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="48914-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="48914-105">Outros tutoriais ([começar com o IoT Hub] e [enviar mensagens de nuvem para dispositivo com o IoT Hub][lnk-c2d]) mostram como toouse Olá básica dispositivo para nuvem e nuvem para dispositivo funcionalidade de mensagens do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="48914-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how toouse hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="48914-106">Este tutorial baseia-se em código Olá mostrado a saudação [começar com o IoT Hub] tutorial e mostra como toouse mensagem roteamento tooprocess de mensagens de dispositivo para a nuvem de forma escalonável.</span><span class="sxs-lookup"><span data-stu-id="48914-106">This tutorial builds on hello code shown in hello [Get started with IoT Hub] tutorial, and shows you how toouse message routing tooprocess device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="48914-107">tutorial de saudação ilustra como tooprocess mensagens que requerem ação imediata da solução Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="48914-107">hello tutorial illustrates how tooprocess messages that require immediate action from hello solution back end.</span></span> <span data-ttu-id="48914-108">Por exemplo, um dispositivo pode enviar uma mensagem de alarme que dispara e insere um tíquete em um sistema CRM.</span><span class="sxs-lookup"><span data-stu-id="48914-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="48914-109">Por outro lado, as mensagens de ponto de dados simplesmente são alimentadas no mecanismo de análise.</span><span class="sxs-lookup"><span data-stu-id="48914-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="48914-110">Por exemplo, a telemetria de temperatura de um dispositivo que é toobe armazenado para análise posterior é uma mensagem de ponto de dados.</span><span class="sxs-lookup"><span data-stu-id="48914-110">For example, temperature telemetry from a device that is toobe stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="48914-111">No final da saudação deste tutorial, você deve executar três aplicativos de console de Java:</span><span class="sxs-lookup"><span data-stu-id="48914-111">At hello end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="48914-112">**dispositivo simulado**, uma versão modificada do aplicativo hello criado no hello [começar com o IoT Hub] tutorial, envia mensagens de dispositivo para a nuvem de ponto de dados por segundo, e mensagens de dispositivo para nuvem interativa cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="48914-112">**simulated-device**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="48914-113">Esse aplicativo usa Olá AMQP protocolo toocommunicate com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="48914-113">This app uses hello AMQP protocol toocommunicate with IoT Hub.</span></span>
* <span data-ttu-id="48914-114">**mensagens de d2c leitura** exibe telemetria Olá enviada pelo seu aplicativo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="48914-114">**read-d2c-messages** displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="48914-115">**leitura crítica fila** filas de mensagens de saudação crítico de saudação do barramento do serviço fila anexada toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="48914-115">**read-critical-queue** de-queues hello critical messages from hello Service Bus queue attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="48914-116">O Hub IoT tem suporte de SDK para várias plataformas de dispositivo e linguagens, incluindo C, Java e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="48914-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="48914-117">Para obter instruções sobre como tooreplace Olá dispositivo neste tutorial com um dispositivo físico, e como tooconnect dispositivos tooan IoT Hub, consulte Olá [Centro de desenvolvedores do Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="48914-117">For instructions on how tooreplace hello device in this tutorial with a physical device, and how tooconnect devices tooan IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="48914-118">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="48914-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="48914-119">Uma versão completa do trabalho de saudação [começar com o IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="48914-119">A complete working version of hello [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="48914-120">Olá mais recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="48914-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="48914-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="48914-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="48914-122">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="48914-122">An active Azure account.</span></span> <span data-ttu-id="48914-123">(Se você não possui uma conta, é possível criar uma [conta gratuita] [lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="48914-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="48914-124">Você também precisa ter um conhecimento básico do [Armazenamento do Azure] e do [Barramento de Serviço do Azure].</span><span class="sxs-lookup"><span data-stu-id="48914-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="48914-125">Enviar mensagens interativas de um aplicativo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="48914-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="48914-126">Nesta seção, você modificar Olá dispositivo aplicativo que você criou no hello [começar com o IoT Hub] toooccasionally tutorial enviar mensagens que exigem processamento imediato.</span><span class="sxs-lookup"><span data-stu-id="48914-126">In this section, you modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="48914-127">Use um arquivo de simulated-device\src\main\java\com\mycompany\app\App.java texto editor tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="48914-127">Use a text editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="48914-128">Esse arquivo contém código Olá Olá **dispositivo simulado** aplicativo que você criou no hello [começar com o IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="48914-128">This file contains hello code for hello **simulated-device** app you created in hello [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="48914-129">Substituir saudação **MessageSender** classe com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="48914-129">Replace hello **MessageSender** class with hello following code:</span></span>

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
                    System.out.println("Sending: " + msgStr);

                    Object lockobj = new Object();
                    EventCallback callback = new EventCallback();
                    client.sendEventAsync(msg, callback, lockobj);

                    synchronized (lockobj) {
                        lockobj.wait();
                    }
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Finished.");
            }
        }
    }
    ```
   
    <span data-ttu-id="48914-130">Este método adiciona aleatoriamente propriedade Olá `"level": "critical"` toomessages enviadas pelo dispositivo hello, que simula uma mensagem que requer uma ação imediata pelo back-end do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="48914-130">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello application back-end.</span></span> <span data-ttu-id="48914-131">aplicativo Hello transmite essas informações nas propriedades de mensagem de saudação, em vez de no corpo da mensagem de saudação, para que o IoT Hub pode rotear o destino da mensagem apropriada Olá mensagem toohello.</span><span class="sxs-lookup"><span data-stu-id="48914-131">hello application passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="48914-132">Você pode usar mensagens de tooroute de propriedades de mensagem para vários cenários, incluindo frio-caminho de processamento, além de exemplo de afunilamento toohello mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="48914-132">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot path example shown here.</span></span>

2. <span data-ttu-id="48914-133">Salve e feche o arquivo de simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="48914-133">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="48914-134">Para a mesma Olá de simplicidade, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="48914-134">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="48914-135">No código de produção, você deve implementar uma política de repetição como retirada exponencial, conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].</span><span class="sxs-lookup"><span data-stu-id="48914-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="48914-136">Olá toobuild **dispositivo simulado** aplicativo usando o Maven, executar Olá comando no prompt de comando Olá na pasta do dispositivo simulado Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="48914-136">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a><span data-ttu-id="48914-137">Adicionar uma IoT de tooyour fila em hub e rota a tooit mensagens</span><span class="sxs-lookup"><span data-stu-id="48914-137">Add a queue tooyour IoT hub and route messages tooit</span></span>

<span data-ttu-id="48914-138">Nesta seção, você cria uma fila do barramento de serviço, conectá-lo tooyour IoT hub e configurar seu IoT hub toosend mensagens toohello fila com base na presença de saudação de uma propriedade na mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="48914-138">In this section, you create a Service Bus queue, connect it tooyour IoT hub, and configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span> <span data-ttu-id="48914-139">Para obter mais informações sobre como tooprocess mensagens das filas do barramento de serviço, consulte [começar com filas][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="48914-139">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="48914-140">Crie uma fila do Barramento de Serviço conforme descrito em [Introdução às filas][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="48914-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="48914-141">Faça uma anotação de nome de namespace e fila hello.</span><span class="sxs-lookup"><span data-stu-id="48914-141">Make a note of hello namespace and queue name.</span></span>

2. <span data-ttu-id="48914-142">Olá portal do Azure, abra seu hub IoT em e clique em **pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="48914-142">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Pontos de extremidade no Hub IoT][30]

3. <span data-ttu-id="48914-144">Em Olá **pontos de extremidade** folha, clique em **adicionar** em Olá tooadd superior hub IoT de tooyour de fila.</span><span class="sxs-lookup"><span data-stu-id="48914-144">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="48914-145">O ponto de extremidade do nome hello **CriticalQueue** e usar Olá suspensas tooselect **fila do barramento de serviço**, Olá namespace de barramento de serviço no qual reside a fila e Olá nome da fila.</span><span class="sxs-lookup"><span data-stu-id="48914-145">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="48914-146">Quando terminar, clique em **salvar** na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="48914-146">When you are done, click **Save** at hello bottom.</span></span>

    ![Adicionando um ponto de extremidade][31]

4. <span data-ttu-id="48914-148">Agora clique em **Rotas** no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="48914-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="48914-149">Clique em **adicionar** na parte superior de saudação do hello folha toocreate uma regra de roteamento que roteia mensagens toohello fila apenas adicionada.</span><span class="sxs-lookup"><span data-stu-id="48914-149">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="48914-150">Selecione **DeviceTelemetry** como fonte de saudação de dados.</span><span class="sxs-lookup"><span data-stu-id="48914-150">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="48914-151">Digite `level="critical"` como condição Olá e escolha fila Olá que você acabou de adicionar como um ponto de extremidade personalizado como ponto de extremidade de regra de roteamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="48914-151">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="48914-152">Quando terminar, clique em **salvar** na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="48914-152">When you are done, click **Save** at hello bottom.</span></span>

    ![Adicionando uma rota][32]

    <span data-ttu-id="48914-154">Certifique-se de rota fallback hello está definida muito**ON**.</span><span class="sxs-lookup"><span data-stu-id="48914-154">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="48914-155">Essa configuração é a configuração padrão de saudação de um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="48914-155">This setting is hello default configuration of an IoT hub.</span></span>

    ![Rota de fallback][33]

## <a name="optional-read-from-hello-queue-endpoint"></a><span data-ttu-id="48914-157">(Opcional) Ler a partir do ponto de extremidade de fila Olá</span><span class="sxs-lookup"><span data-stu-id="48914-157">(Optional) Read from hello queue endpoint</span></span>

<span data-ttu-id="48914-158">Opcionalmente, você pode ler mensagens de saudação do ponto de extremidade de fila Olá, seguindo as instruções de saudação do [começar com filas][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="48914-158">You can optionally read hello messages from hello queue endpoint by following hello instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="48914-159">Nome hello aplicativo **leitura crítica fila**.</span><span class="sxs-lookup"><span data-stu-id="48914-159">Name hello app **read-critical-queue**.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="48914-160">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="48914-160">Run hello applications</span></span>

<span data-ttu-id="48914-161">Agora você está três aplicativos de saudação de toorun pronto.</span><span class="sxs-lookup"><span data-stu-id="48914-161">Now you are ready toorun hello three applications.</span></span>

1. <span data-ttu-id="48914-162">Olá toorun **mensagens de d2c leitura** aplicativo, em um prompt de comando ou o shell navegue toohello leitura d2c pasta e executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="48914-162">toorun hello **read-d2c-messages** application, in a command prompt or shell navigate toohello read-d2c folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Executar read-d2c-messages][readd2c]

2. <span data-ttu-id="48914-164">Olá toorun **leitura crítica fila** aplicativo, em um prompt de comando ou o shell de navegar a pasta de leitura crítica fila toohello e execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="48914-164">toorun hello **read-critical-queue** application, in a command prompt or shell navigate toohello read-critical-queue folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Executar read-critical-messages][readqueue]

3. <span data-ttu-id="48914-166">Olá toorun **dispositivo simulado** aplicativo, em um prompt de comando ou o shell navegue pasta do dispositivo simulado toohello e executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="48914-166">toorun hello **simulated-device** app, in a command prompt or shell navigate toohello simulated-device folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Executar simulated-device][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="48914-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48914-168">Next steps</span></span>

<span data-ttu-id="48914-169">Neste tutorial, você aprendeu como tooreliably expedir as mensagens de dispositivo para nuvem usando a funcionalidade de roteamento de mensagem de saudação do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="48914-169">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="48914-170">Olá [como mensagens de nuvem para dispositivo toosend com o IoT Hub] [ lnk-c2d] mostra como toosend mensagens tooyour dispositivos de back-end sua solução.</span><span class="sxs-lookup"><span data-stu-id="48914-170">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="48914-171">exemplos de toosee de soluções completas de ponta a ponta que usam o IoT Hub, consulte [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="48914-171">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="48914-172">toolearn mais sobre como desenvolver soluções com o IoT Hub, consulte Olá [guia do desenvolvedor de IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="48914-172">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="48914-173">toolearn mais sobre o roteamento de mensagens no IoT Hub, consulte [enviar e receber mensagens com o IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="48914-173">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[Armazenamento do Azure]: https://azure.microsoft.com/documentation/services/storage/
[Barramento de Serviço do Azure]: https://azure.microsoft.com/documentation/services/service-bus/

[guia do desenvolvedor de IoT Hub]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[começar com o IoT Hub]: iot-hub-java-java-getstarted.md
[Centro de desenvolvedores do Azure IoT]: https://azure.microsoft.com/develop/iot
[tratamento de falhas transitórias]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Tratamento de Falhas Transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
