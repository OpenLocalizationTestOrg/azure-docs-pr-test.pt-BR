---
title: mensagens de aaaCloud para o dispositivo com o Azure IoT Hub (Java) | Microsoft Docs
description: Como toosend de nuvem para dispositivo mensagens tooa dispositivo de um hub IoT do Azure usando hello Azure IoT SDKs para Java. Modificar as mensagens de nuvem para dispositivo um dispositivo simulado aplicativo tooreceive e modificar as mensagens de nuvem para dispositivo um aplicativo de back-end toosend hello.
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
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="46e7d-104">Enviar mensagens da nuvem para o dispositivo com o Hub IoT (Java)</span><span class="sxs-lookup"><span data-stu-id="46e7d-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="46e7d-105">O Hub IoT do Azure é um serviço totalmente gerenciado que ajuda a permitir comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end de solução.</span><span class="sxs-lookup"><span data-stu-id="46e7d-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="46e7d-106">Olá [começar com o IoT Hub] tutorial mostra como toocreate um hub IoT, provisionar uma identidade de dispositivo nele e código de um aplicativo de dispositivo simulado que envia mensagens de dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="46e7d-106">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="46e7d-107">Esse tutorial se baseia na [começar com o IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="46e7d-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="46e7d-108">Ele mostra como:</span><span class="sxs-lookup"><span data-stu-id="46e7d-108">It shows you how to:</span></span>

* <span data-ttu-id="46e7d-109">Sua solução back-end, envie mensagens de nuvem para dispositivo tooa único dispositivo por meio de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="46e7d-109">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="46e7d-110">Receber mensagens da nuvem para o dispositivo em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="46e7d-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="46e7d-111">De sua solução back-end, solicitar confirmação de entrega (*comentários*) para mensagens enviadas tooa dispositivo do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="46e7d-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="46e7d-112">Você pode encontrar mais informações sobre mensagens de nuvem para dispositivo em Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="46e7d-112">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="46e7d-113">No final da saudação deste tutorial, você deve executar dois aplicativos de console de Java:</span><span class="sxs-lookup"><span data-stu-id="46e7d-113">At hello end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="46e7d-114">**dispositivo simulado**, uma versão modificada do aplicativo hello criado no [começar com o IoT Hub], que se conecta tooyour IoT hub e recebe mensagens de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="46e7d-114">**simulated-device**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="46e7d-115">**enviar mensagens de c2d**, que envia um aplicativo de dispositivo simulado toohello mensagem de nuvem para dispositivo por meio de IoT Hub e, em seguida, recebe a sua confirmação de entrega.</span><span class="sxs-lookup"><span data-stu-id="46e7d-115">**send-c2d-messages**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="46e7d-116">O Hub IoT tem suporte a SDK para várias plataformas de dispositivo e linguagens (incluindo C, Java e Javascript) nos SDKs do dispositivo IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="46e7d-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="46e7d-117">Para obter instruções passo a passo sobre como tooconnect do seu dispositivo toothis tutorial código e geralmente tooAzure IoT Hub, consulte Olá [Centro de desenvolvedores do Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="46e7d-117">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="46e7d-118">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="46e7d-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="46e7d-119">Uma versão completa do trabalho de saudação [começar com o IoT Hub](iot-hub-java-java-getstarted.md) ou [mensagens de dispositivo para nuvem processo IoT Hub](iot-hub-java-java-process-d2c.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="46e7d-119">A complete working version of hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="46e7d-120">Olá mais recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="46e7d-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="46e7d-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="46e7d-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="46e7d-122">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="46e7d-122">An active Azure account.</span></span> <span data-ttu-id="46e7d-123">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="46e7d-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="46e7d-124">Receber mensagens no aplicativo de dispositivo simulado Olá</span><span class="sxs-lookup"><span data-stu-id="46e7d-124">Receive messages in hello simulated device app</span></span>

<span data-ttu-id="46e7d-125">Nesta seção, você modificar o aplicativo de dispositivo simulado Olá criado na [começar com o IoT Hub] tooreceive mensagens de nuvem para dispositivo do hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="46e7d-125">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="46e7d-126">Usando um editor de texto, abra o arquivo de simulated-device\src\main\java\com\mycompany\app\App.java de saudação.</span><span class="sxs-lookup"><span data-stu-id="46e7d-126">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="46e7d-127">Adicione o seguinte Olá **MessageCallback** uma classe aninhada dentro de saudação **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="46e7d-127">Add hello following **MessageCallback** class as a nested class inside hello **App** class.</span></span> <span data-ttu-id="46e7d-128">Olá **executar** método é invocado quando o dispositivo Olá recebe uma mensagem de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="46e7d-128">hello **execute** method is invoked when hello device receives a message from IoT Hub.</span></span> <span data-ttu-id="46e7d-129">Neste exemplo, o dispositivo Olá sempre notifica o hub IoT de saudação que concluiu a mensagem de saudação:</span><span class="sxs-lookup"><span data-stu-id="46e7d-129">In this example, hello device always notifies hello IoT hub that it has completed hello message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="46e7d-130">Modificar Olá **principal** método toocreate um **AppMessageCallback** Olá instância e chamar **setMessageCallback** método antes de ele abre o cliente de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="46e7d-130">Modify hello **main** method toocreate an **AppMessageCallback** instance and call hello **setMessageCallback** method before it opens hello client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="46e7d-131">Se você usar HTTP em vez de MQTT ou AMQP como transporte hello, Olá **DeviceClient** instância procura de mensagens de IoT Hub com pouca frequência (menor que a cada 25 minutos).</span><span class="sxs-lookup"><span data-stu-id="46e7d-131">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="46e7d-132">Para obter mais informações sobre as diferenças de saudação entre suporte MQTT, AMQP e HTTP e a limitação de Hub IoT, consulte Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="46e7d-132">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="46e7d-133">Olá toobuild **dispositivo simulado** aplicativo usando o Maven, executar Olá comando no prompt de comando Olá na pasta do dispositivo simulado Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="46e7d-133">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="46e7d-134">Envie uma mensagem da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="46e7d-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="46e7d-135">Nesta seção, você deve criar um aplicativo de console de Java que envia mensagens de nuvem para dispositivo toohello dispositivo simulado aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46e7d-135">In this section, you create a Java console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="46e7d-136">Necessário Olá ID do dispositivo do dispositivo Olá adicionado no hello [começar com o IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="46e7d-136">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="46e7d-137">Você também precisa hello cadeia de caracteres de conexão de IoT Hub para o hub que você pode encontrar no hello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="46e7d-137">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="46e7d-138">Crie um projeto Maven chamado **enviar mensagens de c2d** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="46e7d-138">Create a Maven project called **send-c2d-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="46e7d-139">Observe que esse é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="46e7d-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="46e7d-140">No prompt de comando, navegue toohello nova pasta de envio de c2d de mensagens.</span><span class="sxs-lookup"><span data-stu-id="46e7d-140">At your command prompt, navigate toohello new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="46e7d-141">Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta de envio de c2d de mensagens de saudação e adicione Olá seguir dependência toohello **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="46e7d-141">Using a text editor, open hello pom.xml file in hello send-c2d-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="46e7d-142">Adicionando a dependência do hello permite Olá toouse **hub IOT-serviço-cliente java** pacote no toocommunicate seu aplicativo com o serviço de hub IoT:</span><span class="sxs-lookup"><span data-stu-id="46e7d-142">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="46e7d-143">Você pode verificar a versão mais recente de saudação do **cliente de serviço iot** usando [pesquisa Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="46e7d-143">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="46e7d-144">Salve e feche o arquivo de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="46e7d-144">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="46e7d-145">Usando um editor de texto, abra o arquivo de send-c2d-messages\src\main\java\com\mycompany\app\App.java de saudação.</span><span class="sxs-lookup"><span data-stu-id="46e7d-145">Using a text editor, open hello send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="46e7d-146">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="46e7d-146">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="46e7d-147">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe, substituindo **{yourhubconnectionstring}** e **{yourdeviceid}** com hello valores seu mencionado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="46e7d-147">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with hello values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="46e7d-148">Substituir saudação **principal** método com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="46e7d-148">Replace hello **main** method with hello following code.</span></span> <span data-ttu-id="46e7d-149">Esse código conecta tooyour IoT hub, envia um dispositivo de tooyour de mensagem e aguarda uma confirmação de mensagem hello dispositivo Olá recebidos e processados:</span><span class="sxs-lookup"><span data-stu-id="46e7d-149">This code connects tooyour IoT hub, sends a message tooyour device, and then waits for an acknowledgment that hello device received and processed hello message:</span></span>
   
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
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
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
    > <span data-ttu-id="46e7d-150">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="46e7d-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="46e7d-151">No código de produção, você deve implementar políticas de repetição (por exemplo, a retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].</span><span class="sxs-lookup"><span data-stu-id="46e7d-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="46e7d-152">Olá toobuild **dispositivo simulado** aplicativo usando o Maven, executar Olá comando no prompt de comando Olá na pasta do dispositivo simulado Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="46e7d-152">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="46e7d-153">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="46e7d-153">Run hello applications</span></span>

<span data-ttu-id="46e7d-154">Agora você está pronto toorun aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="46e7d-154">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="46e7d-155">Em um prompt de comando na pasta do dispositivo simulado hello, execute Olá toobegin comando Enviar hub de IoT telemetria tooyour e toolisten para mensagens de nuvem para dispositivo enviadas de seu hub a seguir:</span><span class="sxs-lookup"><span data-stu-id="46e7d-155">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry tooyour IoT hub and toolisten for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Execute o aplicativo de dispositivo simulado Olá][img-simulated-device]

2. <span data-ttu-id="46e7d-157">Em um prompt de comando na pasta de envio de c2d de mensagens de saudação, execute Olá toosend de comando a seguir, uma mensagem de nuvem para dispositivo e aguarde uma confirmação de comentários:</span><span class="sxs-lookup"><span data-stu-id="46e7d-157">At a command prompt in hello send-c2d-messages folder, run hello following command toosend a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Execute a mensagem de nuvem para dispositivo saudação comando toosend Olá][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="46e7d-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46e7d-159">Next steps</span></span>

<span data-ttu-id="46e7d-160">Neste tutorial, você aprendeu como toosend e receber mensagens de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="46e7d-160">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="46e7d-161">exemplos de toosee de soluções completas de ponta a ponta que usam o IoT Hub, consulte [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="46e7d-161">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="46e7d-162">toolearn mais sobre como desenvolver soluções com o IoT Hub, consulte Olá [guia do desenvolvedor de IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="46e7d-162">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[começar com o IoT Hub]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[guia do desenvolvedor de IoT Hub]: iot-hub-devguide.md
[Centro de desenvolvedores do Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[tratamento de falhas transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portal do Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22