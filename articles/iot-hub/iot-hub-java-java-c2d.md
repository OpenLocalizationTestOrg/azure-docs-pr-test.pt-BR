---
title: Mensagens da nuvem para o dispositivo com o Hub IoT do Azure (Java)| Microsoft Docs
description: "Como enviar mensagens da nuvem para o dispositivo para um dispositivo de um Hub IoT do Azure usando os SDKs do IoT do Azure para Java. Modifique um aplicativo de dispositivo simulado para receber mensagens da nuvem para o dispositivo e modificar um aplicativo de back-end para enviá-las."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: f5e3ac46f4d144b12e2ab7fcfb456665ff6cc68f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="410c0-104">Enviar mensagens da nuvem para o dispositivo com o Hub IoT (Java)</span><span class="sxs-lookup"><span data-stu-id="410c0-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="410c0-105">O Hub IoT do Azure é um serviço totalmente gerenciado que ajuda a permitir comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end de solução.</span><span class="sxs-lookup"><span data-stu-id="410c0-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="410c0-106">O tutorial [Introdução ao Hub IoT] mostra como criar um Hub IoT, provisionar uma identidade do dispositivo nele e codificar um aplicativo do dispositivo simulado que envia mensagens do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="410c0-106">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="410c0-107">Esse tutorial se baseia na [Introdução ao Hub IoT].</span><span class="sxs-lookup"><span data-stu-id="410c0-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="410c0-108">Ele mostra como:</span><span class="sxs-lookup"><span data-stu-id="410c0-108">It shows you how to:</span></span>

* <span data-ttu-id="410c0-109">Da sua solução de back-end, envie mensagens da nuvem para o dispositivo em um único dispositivo por meio do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="410c0-109">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="410c0-110">Receber mensagens da nuvem para o dispositivo em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="410c0-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="410c0-111">Da sua solução de back-end, solicite confirmação de entrega (*comentários*) para as mensagens enviadas a um dispositivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="410c0-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="410c0-112">É possível encontrar mais informações sobre as mensagens da nuvem para o dispositivo no [Guia do Desenvolvedor do Hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="410c0-112">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="410c0-113">No final deste tutorial, você executará dois aplicativos de console do Java:</span><span class="sxs-lookup"><span data-stu-id="410c0-113">At the end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="410c0-114">**simulated-device**, uma versão modificada do aplicativo criado na [Introdução ao Hub IoT], que se conecta a seu Hub IoT e recebe mensagens da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="410c0-114">**simulated-device**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="410c0-115">**send-c2d-messages**, que envia uma mensagem da nuvem ao aplicativo do dispositivo simulado por meio do Hub IoT e recebe sua confirmação de entrega.</span><span class="sxs-lookup"><span data-stu-id="410c0-115">**send-c2d-messages**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="410c0-116">O Hub IoT tem suporte a SDK para várias plataformas de dispositivo e linguagens (incluindo C, Java e Javascript) nos SDKs do dispositivo IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="410c0-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="410c0-117">Para obter instruções passo a passo sobre como conectar seu dispositivo ao código deste tutorial e, em geral, ao Hub IoT do Azure, veja o [Centro de Desenvolvedores do IoT do Azure].</span><span class="sxs-lookup"><span data-stu-id="410c0-117">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="410c0-118">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="410c0-118">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="410c0-119">Uma versão de trabalho completa do tutorial [Introdução ao Hub IoT](iot-hub-java-java-getstarted.md) ou [Processar mensagens do dispositivo para a nuvem do Hub IoT](iot-hub-java-java-process-d2c.md).</span><span class="sxs-lookup"><span data-stu-id="410c0-119">A complete working version of the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="410c0-120">A versão mais recente do [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="410c0-120">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="410c0-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="410c0-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="410c0-122">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="410c0-122">An active Azure account.</span></span> <span data-ttu-id="410c0-123">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="410c0-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="410c0-124">Receber mensagens no aplicativo do dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="410c0-124">Receive messages in the simulated device app</span></span>

<span data-ttu-id="410c0-125">Nesta seção, você modifica o aplicativo do dispositivo simulado criado na [Introdução ao Hub IoT] para receber mensagens da nuvem para o dispositivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="410c0-125">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="410c0-126">Usando um editor de texto, abra o arquivo simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="410c0-126">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="410c0-127">Adicione a classe **MessageCallback** a seguir como uma classe aninhada dentro da class **App**.</span><span class="sxs-lookup"><span data-stu-id="410c0-127">Add the following **MessageCallback** class as a nested class inside the **App** class.</span></span> <span data-ttu-id="410c0-128">O método **execute** é invocado quando o dispositivo recebe uma mensagem do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="410c0-128">The **execute** method is invoked when the device receives a message from IoT Hub.</span></span> <span data-ttu-id="410c0-129">Neste exemplo, o dispositivo sempre notifica o Hub IoT que concluiu a mensagem:</span><span class="sxs-lookup"><span data-stu-id="410c0-129">In this example, the device always notifies the IoT hub that it has completed the message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="410c0-130">Modifique o método **main** para criar uma instância **AppMessageCallback** e chame o método **setMessageCallback** antes de abrir o cliente da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="410c0-130">Modify the **main** method to create an **AppMessageCallback** instance and call the **setMessageCallback** method before it opens the client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="410c0-131">Se você usar HTTP em vez de MQTT ou AMQP como transporte, a instância **DeviceClient** verificará se há mensagens do Hub IoT com pouca frequência (menos de cada 25 minutos).</span><span class="sxs-lookup"><span data-stu-id="410c0-131">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="410c0-132">Para obter mais informações sobre as diferenças entre o suporte do MQTT, AMQP e HTTP e a limitação do Hub IoT, consulte o [Guia do Desenvolvedor do Hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="410c0-132">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="410c0-133">Para compilar o aplicativo **simulated-device** usando o Maven, execute o comando a seguir no prompt de comando na pasta simulated-device:</span><span class="sxs-lookup"><span data-stu-id="410c0-133">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="410c0-134">Envie uma mensagem da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="410c0-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="410c0-135">Nesta seção, você criará um aplicativo do console do Java que envia mensagens da nuvem para o dispositivo para o aplicativo do dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="410c0-135">In this section, you create a Java console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="410c0-136">Você precisa da ID do dispositivo que você adicionou no tutorial [Introdução ao Hub IoT].</span><span class="sxs-lookup"><span data-stu-id="410c0-136">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="410c0-137">A cadeia de conexão do Hub IoT também é necessária e você pode encontrá-la no [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="410c0-137">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="410c0-138">Crie um projeto Maven chamado **send-c2d-messages** usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="410c0-138">Create a Maven project called **send-c2d-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="410c0-139">Observe que esse é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="410c0-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="410c0-140">No prompt de comando, navegue até a nova pasta send-c2d-messages.</span><span class="sxs-lookup"><span data-stu-id="410c0-140">At your command prompt, navigate to the new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="410c0-141">Usando um editor de texto, abra o arquivo pom.xml na pasta send-c2d-messages e adicione a dependência a seguir ao nó **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="410c0-141">Using a text editor, open the pom.xml file in the send-c2d-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="410c0-142">A adição da dependência permite que você use o pacote **iothub-java-service-client** no aplicativo para se comunicar com o serviço do Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="410c0-142">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="410c0-143">Você pode verificar a versão mais recente do **iot-service-client** usando a [pesquisa Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="410c0-143">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="410c0-144">Salve e feche o arquivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="410c0-144">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="410c0-145">Usando um editor de texto, abra o arquivo send-c2d-messages\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="410c0-145">Using a text editor, open the send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="410c0-146">Adicione as seguintes instruções **import** ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="410c0-146">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="410c0-147">Adicione as seguintes variáveis do nível da classe à classe **App**, substituindo **{cadeiadeconexãodoseuhub}** e **{iddoseudispositivo}** pelos valores anotados anteriormente:</span><span class="sxs-lookup"><span data-stu-id="410c0-147">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with the values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="410c0-148">Substitua o método **main** pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="410c0-148">Replace the **main** method with the following code.</span></span> <span data-ttu-id="410c0-149">Esse código se conecta ao hub IoT, envia uma mensagem ao dispositivo e aguarda uma confirmação de que o dispositivo recebeu e processou a mensagem:</span><span class="sxs-lookup"><span data-stu-id="410c0-149">This code connects to your IoT hub, sends a message to your device, and then waits for an acknowledgment that the device received and processed the message:</span></span>
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud to device message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent to device");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="410c0-150">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="410c0-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="410c0-151">No código de produção, implemente políticas de repetição (como uma retirada exponencial), conforme sugestão no artigo [Transient Fault Handling](Tratamento de Falhas Transitórias) do MSDN.</span><span class="sxs-lookup"><span data-stu-id="410c0-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="410c0-152">Para compilar o aplicativo **simulated-device** usando o Maven, execute o comando a seguir no prompt de comando na pasta simulated-device:</span><span class="sxs-lookup"><span data-stu-id="410c0-152">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-the-applications"></a><span data-ttu-id="410c0-153">Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="410c0-153">Run the applications</span></span>

<span data-ttu-id="410c0-154">Agora você está pronto para executar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="410c0-154">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="410c0-155">Em um prompt de comando na pasta do dispositivo simulado, execute o seguinte comando para iniciar o envio de dados de telemetria para seu Hub IoT e escutar mensagens da nuvem para o dispositivo enviadas do hub:</span><span class="sxs-lookup"><span data-stu-id="410c0-155">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry to your IoT hub and to listen for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Executar um aplicativo de dispositivo simulado][img-simulated-device]

2. <span data-ttu-id="410c0-157">Em um prompt de comando na pasta send-c2d-messages, execute o seguinte comando para enviar uma mensagem da nuvem para o dispositivo e esperar uma confirmação de comentário:</span><span class="sxs-lookup"><span data-stu-id="410c0-157">At a command prompt in the send-c2d-messages folder, run the following command to send a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Executar o comando para enviar a mensagem da nuvem para o dispositivo][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="410c0-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="410c0-159">Next steps</span></span>

<span data-ttu-id="410c0-160">Neste tutorial você aprendeu a enviar e receber mensagens da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="410c0-160">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="410c0-161">Para ver exemplos de soluções completas que usam o Hub IoT, consulte [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="410c0-161">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="410c0-162">Para saber mais sobre como desenvolver soluções com o Hub IoT, consulte o [Guia do desenvolvedor do Hub IoT].</span><span class="sxs-lookup"><span data-stu-id="410c0-162">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

<span data-ttu-id="410c0-163">[Introdução ao Hub IoT]: iot-hub-java-java-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="410c0-163">[Get started with IoT Hub]: iot-hub-java-java-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="410c0-164">[Guia do desenvolvedor do Hub IoT]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="410c0-164">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="410c0-165">[Centro de Desenvolvedores do IoT do Azure]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="410c0-165">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
<span data-ttu-id="410c0-166">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="410c0-166">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="410c0-167">[Portal do Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="410c0-167">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="410c0-168">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="410c0-168">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22