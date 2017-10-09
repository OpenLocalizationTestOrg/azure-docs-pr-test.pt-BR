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
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a>Enviar mensagens da nuvem para o dispositivo com o Hub IoT (Java)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

O Hub IoT do Azure é um serviço totalmente gerenciado que ajuda a permitir comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end de solução. Olá [começar com o IoT Hub] tutorial mostra como toocreate um hub IoT, provisionar uma identidade de dispositivo nele e código de um aplicativo de dispositivo simulado que envia mensagens de dispositivo para a nuvem.

Esse tutorial se baseia na [começar com o IoT Hub]. Ele mostra como:

* Sua solução back-end, envie mensagens de nuvem para dispositivo tooa único dispositivo por meio de IoT Hub.
* Receber mensagens da nuvem para o dispositivo em um dispositivo.
* De sua solução back-end, solicitar confirmação de entrega (*comentários*) para mensagens enviadas tooa dispositivo do IoT Hub.

Você pode encontrar mais informações sobre mensagens de nuvem para dispositivo em Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].

No final da saudação deste tutorial, você deve executar dois aplicativos de console de Java:

* **dispositivo simulado**, uma versão modificada do aplicativo hello criado no [começar com o IoT Hub], que se conecta tooyour IoT hub e recebe mensagens de nuvem para dispositivo.
* **enviar mensagens de c2d**, que envia um aplicativo de dispositivo simulado toohello mensagem de nuvem para dispositivo por meio de IoT Hub e, em seguida, recebe a sua confirmação de entrega.

> [!NOTE]
> O Hub IoT tem suporte a SDK para várias plataformas de dispositivo e linguagens (incluindo C, Java e Javascript) nos SDKs do dispositivo IoT do Azure. Para obter instruções passo a passo sobre como tooconnect do seu dispositivo toothis tutorial código e geralmente tooAzure IoT Hub, consulte Olá [Centro de desenvolvedores do Azure IoT].

toocomplete neste tutorial, você precisa Olá a seguir:

* Uma versão completa do trabalho de saudação [começar com o IoT Hub](iot-hub-java-java-getstarted.md) ou [mensagens de dispositivo para nuvem processo IoT Hub](iot-hub-java-java-process-d2c.md) tutorial.
* Olá mais recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

## <a name="receive-messages-in-hello-simulated-device-app"></a>Receber mensagens no aplicativo de dispositivo simulado Olá

Nesta seção, você modificar o aplicativo de dispositivo simulado Olá criado na [começar com o IoT Hub] tooreceive mensagens de nuvem para dispositivo do hub IoT de saudação.

1. Usando um editor de texto, abra o arquivo de simulated-device\src\main\java\com\mycompany\app\App.java de saudação.

2. Adicione o seguinte Olá **MessageCallback** uma classe aninhada dentro de saudação **aplicativo** classe. Olá **executar** método é invocado quando o dispositivo Olá recebe uma mensagem de IoT Hub. Neste exemplo, o dispositivo Olá sempre notifica o hub IoT de saudação que concluiu a mensagem de saudação:

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. Modificar Olá **principal** método toocreate um **AppMessageCallback** Olá instância e chamar **setMessageCallback** método antes de ele abre o cliente de saudação da seguinte maneira:

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > Se você usar HTTP em vez de MQTT ou AMQP como transporte hello, Olá **DeviceClient** instância procura de mensagens de IoT Hub com pouca frequência (menor que a cada 25 minutos). Para obter mais informações sobre as diferenças de saudação entre suporte MQTT, AMQP e HTTP e a limitação de Hub IoT, consulte Olá [guia do desenvolvedor de IoT Hub][IoT Hub developer guide - C2D].

4. Olá toobuild **dispositivo simulado** aplicativo usando o Maven, executar Olá comando no prompt de comando Olá na pasta do dispositivo simulado Olá a seguir:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a>Envie uma mensagem da nuvem para o dispositivo

Nesta seção, você deve criar um aplicativo de console de Java que envia mensagens de nuvem para dispositivo toohello dispositivo simulado aplicativo. Necessário Olá ID do dispositivo do dispositivo Olá adicionado no hello [começar com o IoT Hub] tutorial. Você também precisa hello cadeia de caracteres de conexão de IoT Hub para o hub que você pode encontrar no hello [portal do Azure].

1. Crie um projeto Maven chamado **enviar mensagens de c2d** usando Olá comando no prompt de comando a seguir. Observe que esse é um comando único e longo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. No prompt de comando, navegue toohello nova pasta de envio de c2d de mensagens.

3. Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta de envio de c2d de mensagens de saudação e adicione Olá seguir dependência toohello **dependências** nó. Adicionando a dependência do hello permite Olá toouse **hub IOT-serviço-cliente java** pacote no toocommunicate seu aplicativo com o serviço de hub IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Você pode verificar a versão mais recente de saudação do **cliente de serviço iot** usando [pesquisa Maven][lnk-maven-service-search].

4. Salve e feche o arquivo de pom.xml hello.

5. Usando um editor de texto, abra o arquivo de send-c2d-messages\src\main\java\com\mycompany\app\App.java de saudação.

6. Adicione o seguinte Olá **importar** arquivo de toohello instruções:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe, substituindo **{yourhubconnectionstring}** e **{yourdeviceid}** com hello valores seu mencionado anteriormente:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. Substituir saudação **principal** método com hello código a seguir. Esse código conecta tooyour IoT hub, envia um dispositivo de tooyour de mensagem e aguarda uma confirmação de mensagem hello dispositivo Olá recebidos e processados:
   
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
    > Para simplificar, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, a retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].


9. Olá toobuild **dispositivo simulado** aplicativo usando o Maven, executar Olá comando no prompt de comando Olá na pasta do dispositivo simulado Olá a seguir:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Executar aplicativos Olá

Agora você está pronto toorun aplicativos de saudação.

1. Em um prompt de comando na pasta do dispositivo simulado hello, execute Olá toobegin comando Enviar hub de IoT telemetria tooyour e toolisten para mensagens de nuvem para dispositivo enviadas de seu hub a seguir:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Execute o aplicativo de dispositivo simulado Olá][img-simulated-device]

2. Em um prompt de comando na pasta de envio de c2d de mensagens de saudação, execute Olá toosend de comando a seguir, uma mensagem de nuvem para dispositivo e aguarde uma confirmação de comentários:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Execute a mensagem de nuvem para dispositivo saudação comando toosend Olá][img-send-command]

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como toosend e receber mensagens de nuvem para dispositivo. 

exemplos de toosee de soluções completas de ponta a ponta que usam o IoT Hub, consulte [Azure IoT Suite].

toolearn mais sobre como desenvolver soluções com o IoT Hub, consulte Olá [guia do desenvolvedor de IoT Hub].

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