---
title: "aaaGet de Introdução ao Azure IoT Hub (Java) | Microsoft Docs"
description: "Saiba como o dispositivo para nuvem toosend mensagens tooAzure IoT Hub usando IoT SDKs para Java. Criar dispositivo simulado e tooregister de aplicativos de serviço de seu dispositivo, enviar mensagens e ler mensagens de hub IoT."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a>Conecte seu dispositivo tooyour IoT hub que utilizado Java
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

No final da saudação deste tutorial, você tem três aplicativos de console de Java:

* **criar dispositivo-identidade**, que cria uma identidade de dispositivo e de segurança da chave tooconnect seu aplicativo de dispositivo.
* **mensagens de leitura-d2c**, que exibe a telemetria de saudação enviada pelo seu aplicativo de dispositivo.
* **dispositivo simulado**, que conecta tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente e envia uma mensagem de telemetria a cada segundo usando Olá protocolo MQTT.

> [!NOTE]
> artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun ambos os aplicativos em dispositivos e o back-end da solução.

toocomplete neste tutorial, você precisa Olá a seguir:

* Olá mais recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 
* [Maven 3](https://maven.apache.org/install.html) 
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Como etapa final, anote Olá **chave primária** valor. Em seguida, clique em **pontos de extremidade** e hello **eventos** ponto de extremidade interno. Em Olá **propriedades** folha, anote Olá **nome compatível com o evento Hub** e hello **ponto de extremidade compatível com o evento Hub** endereço. Você precisa desses três valores quando cria o aplicativo **read-d2c-messages**.

![Folha Mensagens do Hub IoT do Portal do Azure][6]

Você criou seu Hub IoT. Você tem Olá nome de host do IoT Hub, cadeia de caracteres de conexão de IoT Hub, chave primária de Hub IoT, nome do Hub de eventos-compatível e ponto de extremidade compatível com o evento Hub é necessário toocomplete neste tutorial.

## <a name="create-a-device-identity"></a>Criar uma identidade do dispositivo
Nesta seção, você deve criar um aplicativo de console de Java que cria uma identidade de dispositivo no registro de identidade Olá em seu hub IoT. Um dispositivo não pode se conectar a tooIoT hub, a menos que ele tenha uma entrada no registro de identidade hello. Para obter mais informações, consulte Olá **registro identidade** seção Olá [guia do desenvolvedor de IoT Hub][lnk-devguide-identity]. Quando você executa esse aplicativo de console, ele gera uma ID de dispositivo exclusivo e chave que seu dispositivo possa usar tooidentify em si, quando ele envia o dispositivo para nuvem mensagens tooIoT Hub.

1. Crie uma pasta vazia chamada iot-java-get-started. Na pasta iot java-get-iniciado hello, crie um projeto de Maven chamado **identidade criar de dispositivo** usando Olá comando no prompt de comando a seguir. Observe que este é um comando único e longo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. No prompt de comando, navegue toohello pasta de identidade criar de dispositivo.

3. Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta de identidade criar de dispositivo hello e adicione Olá toohello de dependência a seguir **dependências** nó. Esta dependência habilita você toouse Olá iot-serviço-pacote de cliente em seu aplicativo:

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

5. Usando um editor de texto, abra o arquivo de create-device-identity\src\main\java\com\mycompany\app\App.java de saudação.

6. Adicione o seguinte Olá **importar** arquivo de toohello instruções:

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe, substituindo **{yourhubconnectionstring}** com hello valor seu mencionado anteriormente:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. Modificar assinatura Olá Olá **principal** tooinclude método hello exceções da seguinte maneira:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. Adicionar Olá código a seguir como corpo de saudação do hello **principal** método. Esse código cria um dispositivo denominado *javadevice* no registro de identidade do Hub IoT, caso ele ainda não exista. Ele exibe, em seguida, Olá ID do dispositivo e a chave que é necessário mais tarde:

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. Salve e feche o arquivo de App.java hello.

11. Olá toobuild **identidade criar de dispositivo** aplicativo usando o Maven, executar Olá seguinte comando no prompt de comando Olá na pasta do hello identidade criar de dispositivo:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. Olá toorun **identidade criar de dispositivo** aplicativo usando o Maven, executar Olá seguinte comando no prompt de comando Olá na pasta do hello identidade criar de dispositivo:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. Anote Olá **ID do dispositivo** e **chave dispositivo**. É necessário mais tarde esses valores quando você cria um aplicativo que se conecta tooIoT Hub como um dispositivo.

> [!NOTE]
> Olá registro de identidade de IoT Hub armazena apenas o hub IoT toohello de proteger o acesso do dispositivo identidades tooenable. Ele armazena toouse IDs e chaves de dispositivo como credenciais de segurança e um sinalizador habilitado/desabilitado que você pode usar o acesso de toodisable para um dispositivo individual. Se seu aplicativo precisa toostore outros metadados específicos do dispositivo, ele deve usar um repositório específico do aplicativo. Para obter mais informações, consulte Olá [guia do desenvolvedor de IoT Hub][lnk-devguide-identity].

## <a name="receive-device-to-cloud-messages"></a>Receber mensagens do dispositivo para a nuvem

Nesta seção, você cria um aplicativo do console do Java que lê mensagens do dispositivo para a nuvem do Hub IoT. Um hub IoT expõe um [Hub de eventos][lnk-event-hubs-overview]-tooenable de ponto de extremidade compatível tooread mensagens de dispositivo para a nuvem. coisas tookeep simples, este tutorial cria um leitor básico que não é adequado para uma implantação de alta taxa de transferência. Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial mostra como o dispositivo para nuvem tooprocess mensagens em escala. Olá [Introdução aos Hubs de eventos] [ lnk-eventhubs-tutorial] tutorial fornece informações adicionais sobre como tooprocess mensagens de Hubs de eventos e é aplicável toohello pontos de extremidade compatível com o evento de Hub IoT Hub.

> [!NOTE]
> Olá, ponto de extremidade compatível com o evento Hub para ler mensagens de dispositivo para nuvem sempre usa protocolo AMQP de saudação.

1. Na pasta de iot java-get-iniciado Olá criado na Olá *criar uma identidade de dispositivo* seção, crie um projeto Maven chamado **mensagens de d2c leitura** usando Olá comando no prompt de comando a seguir. Observe que este é um comando único e longo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. No prompt de comando, navegue toohello pasta de leitura de d2c de mensagens.

3. Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta de leitura de d2c de mensagens de saudação e adicione Olá seguir dependência toohello **dependências** nó. Esta dependência habilita um pacote de cliente eventhubs Olá toouse em tooread seu aplicativo de ponto de extremidade de Hub de eventos-compatível com hello:

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. Salve e feche o arquivo de pom.xml hello.

5. Usando um editor de texto, abra o arquivo de read-d2c-messages\src\main\java\com\mycompany\app\App.java de saudação.

6. Adicione o seguinte Olá **importar** arquivo de toohello instruções:

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. Adicionar Olá toohello variável de nível de classe a seguir **aplicativo** classe. Substituir **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, e **{youreventhubcompatiblename}** com valores hello você anotou anteriormente:

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. Adicione o seguinte Olá **receiveMessages** método toohello **aplicativo** classe. Esse método cria um **EventHubClient** tooconnect toohello compatível com o evento Hub extremidade da instância e, em seguida, assincronamente cria um **PartitionReceiver** tooread de instância de um Hub de eventos partição. Ele loops continuamente e imprime os detalhes da mensagem de saudação até que o aplicativo hello termina.

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > Esse método usa um filtro quando ele cria receptor Olá para que hello destinatário lê apenas as mensagens enviadas tooIoT Hub depois receptor Olá começa a ser executado. Essa técnica é útil em um ambiente de teste para poder ver o conjunto atual de saudação de mensagens. Em um ambiente de produção, seu código deve certificar-se de que ele processa todas as mensagens de saudação - para obter mais informações, consulte Olá [como tooprocess mensagens de dispositivo para a nuvem de IoT Hub] [ lnk-process-d2c-tutorial] tutorial.

9. Modificar assinatura Olá Olá **principal** tooinclude método hello exceção da seguinte maneira:

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. Adicionar Olá toohello de código a seguir **principal** método hello **aplicativo** classe. Esse código cria Olá dois **EventHubClient** e **PartitionReceiver** instâncias e permite que você tooclose Olá aplicativo quando você concluiu o processamento de mensagens:

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > Esse código supõe que você criou seu hub IoT na camada (gratuita) do hello F1. Um hub IoT gratuito tem duas partições chamadas "0" e "1".

11. Salve e feche o arquivo de App.java hello.

12. Olá toobuild **mensagens de d2c leitura** aplicativo usando o Maven, executar o seguinte comando no prompt de comando Olá na pasta de leitura de d2c de mensagens de saudação do hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a>Criar um aplicativo de dispositivo
Nesta seção, você deve criar um aplicativo de console de Java que simula um dispositivo que envia o hub de IoT tooan mensagens de dispositivo para a nuvem.

1. Na pasta de iot java-get-iniciado Olá criado na Olá *criar uma identidade de dispositivo* seção, crie um projeto Maven chamado **dispositivo simulado** usando Olá comando no prompt de comando a seguir. Observe que este é um comando único e longo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. No prompt de comando, navegue pasta do dispositivo simulado toohello.

3. Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta do dispositivo simulado hello e adicione Olá dependências toohello a seguir **dependências** nó. Esta dependência habilita você toouse Olá hub IOT-java-pacote de cliente em toocommunicate seu aplicativo com o hub IoT e tooserialize tooJSON de objetos Java:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > Você pode verificar a versão mais recente de saudação do **cliente de dispositivo iot** usando [pesquisa Maven][lnk-maven-device-search].

4. Salve e feche o arquivo de pom.xml hello.

5. Usando um editor de texto, abra o arquivo de simulated-device\src\main\java\com\mycompany\app\App.java de saudação.

6. Adicione o seguinte Olá **importar** arquivo de toohello instruções:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe. Substituindo **{youriothubname}** com seu nome de hub IoT, e **{yourdevicekey}** com valor de chave de dispositivo do hello gerado na Olá *criar uma identidade de dispositivo* seção:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    Este aplicativo de exemplo usa Olá **protocolo** variável quando ele cria uma **DeviceClient** objeto. Você pode usar qualquer toocommunicate de protocolo hello MQTT, AMQP ou HTTP com o IoT Hub.

8. Adicione seguinte Olá aninhados **TelemetryDataPoint** classe dentro Olá **aplicativo** dados de telemetria de saudação toospecify o dispositivo envia tooyour IoT hub de classe:

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. Adicione seguinte Olá aninhados **EventCallback** classe dentro Olá **aplicativo** classe toodisplay Olá confirmação status Olá hub IoT retorna ao processar uma mensagem de saudação aplicativo de dispositivo. Este método também notifica o thread principal de saudação no aplicativo hello quando a mensagem de saudação foi processada:
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. Adicione seguinte Olá aninhados **MessageSender** classe dentro Olá **aplicativo** classe. Olá **executar** método nesta classe gera IoT hub do exemplo telemetria dados toosend tooyour e aguarda uma confirmação antes de enviar a mensagem de saudação do seguinte:

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
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

    Esse método envia uma nova mensagem de dispositivo para nuvem um segundo após o hub IoT de saudação confirma a mensagem de saudação do anterior. mensagem de saudação contém um objeto serializado para JSON com deviceId hello e gerado aleatoriamente números toosimulate um sensor de temperatura e um sensor de umidade.

11. Substituir saudação **principal** método com hello código que cria um hub IoT do thread toosend mensagens de dispositivo para nuvem tooyour a seguir:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. Salve e feche o arquivo de App.java hello.

13. Olá toobuild **dispositivo simulado** aplicativo usando o Maven, executar Olá comando no prompt de comando Olá na pasta do dispositivo simulado Olá a seguir:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> coisas tookeep simples, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].

## <a name="run-hello-apps"></a>Executar aplicativos Olá

Agora você está pronto toorun Olá aplicativos.

1. Em um prompt de comando na pasta de leitura d2c hello, execute Olá toobegin comando primeira partição Olá em seu hub IoT de monitoramento a seguir:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Mensagens do dispositivo para nuvem toomonitor de aplicativo de serviço de Java IoT Hub][7]

2. Em um prompt de comando na pasta do dispositivo simulado hello, execute Olá toobegin comando Enviar hub IoT do telemetria dados tooyour a seguir:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Mensagens do dispositivo para nuvem toosend de aplicativo de dispositivo de IoT Hub de Java][8]

3. Olá **uso** lado a lado no hello [portal do Azure] [ lnk-portal] mostra Olá número de mensagens enviadas toohello IoT hub:

    ![Azure portal uso bloco mostra o número de mensagens enviadas tooIoT Hub][43]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello. Você usou esse dispositivo identidade tooenable Olá dispositivo toosend mensagens de dispositivo para nuvem toohello IoT hub de aplicativos. Você também criou um aplicativo que exibe mensagens de saudação recebidas pelo hub IoT de saudação.

toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:

* [Conectando o dispositivo][lnk-connect-device]
* [Introdução ao gerenciamento de dispositivo][lnk-device-management]
* [Introdução ao Azure IoT Edge][lnk-iot-edge]

toolearn como tooextend seu IoT solução e o processo de dispositivo para nuvem mensagens em grande escala, consulte Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
