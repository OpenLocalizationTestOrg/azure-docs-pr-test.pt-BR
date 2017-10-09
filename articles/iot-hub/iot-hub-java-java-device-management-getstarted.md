---
title: "aaaGet de Introdução ao gerenciamento de dispositivos do Azure IoT Hub (Java) | Microsoft Docs"
description: "Como tooinitiate de gerenciamento de dispositivo de Azure IoT Hub toouse um dispositivo remoto reinicializar. Use dispositivo IoT do Azure de saudação SDK para Java tooimplement um aplicativo de dispositivo simulado que inclui um método direto e hello SDK do serviço de IoT do Azure para Java tooimplement um aplicativo de serviço que invoca o método direto hello."
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a>Introdução ao gerenciamento de dispositivos (Java)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Este tutorial mostra como:

* Use Olá toocreate portal do Azure um IoT Hub e criar uma identidade de dispositivo em seu hub IoT.
* Crie um aplicativo de dispositivo simulado que implementa um dispositivo de saudação tooreboot método direto. Métodos diretos são chamados de nuvem hello.
* Crie um aplicativo que invoca o método direto de reinicialização de saudação no aplicativo do dispositivo simulado Olá por meio de seu hub IoT. Este aplicativo e monitores Olá relatadas propriedades de saudação dispositivo toosee quando Olá operação de reinicialização é concluída.

No final da saudação deste tutorial, você tem dois aplicativos de console de Java:

**simulated-device**. Este aplicativo:

* Conecta-se tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente.
* Recebe uma chamada de método direto de reinicialização.
* Simula uma reinicialização física.
* Relatórios Olá hora da última reinicialização Olá através de uma propriedade relatada.

**disparar reinicialização**. Este aplicativo:

* Chama um método direto no aplicativo do dispositivo simulado hello.
* Exibe a chamada do método direto Olá resposta toohello enviada pelo dispositivo simulado Olá
* Olá exibe atualizado relatado propriedades.

> [!NOTE]
> Para obter informações sobre Olá SDKs que você pode usar toobuild toorun de aplicativos em dispositivos e o back-end de solução, consulte [SDKs do Azure IoT][lnk-hub-sdks].

toocomplete neste tutorial, você precisa:

* Java SE 8. <br/> [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Java para este tutorial no Windows ou Linux.
* Maven 3.  <br/> [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall [Maven] [ lnk-maven] para este tutorial no Windows ou Linux.
* [Versão do Node.js 0.10.0 ou posterior](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Disparar uma reinicialização remota no dispositivo hello usando um método direto

Nesta seção, você cria um aplicativo de console Java que:

1. Invoca o método direto de reinicialização de saudação no aplicativo do dispositivo simulado Olá.
1. Exibe a resposta de saudação.
1. Olá sondagens relatado propriedades enviadas do hello dispositivo toodetermine quando Olá reinicialização seja concluída.

Este aplicativo de console se conecta tooyour IoT Hub método direto do tooinvoke hello e hello leitura relatadas propriedades.

1. Crie uma pasta vazia chamada dm-get-started.

1. Na pasta dm get iniciado hello, crie um projeto de Maven chamado **gatilho reinicialização** usando Olá comando no prompt de comando a seguir. a seguir Olá mostra um comando longo, único:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. No prompt de comando, navegue toohello gatilho reinicialização pasta.

1. Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta de reinicialização de gatilho hello e adicione Olá toohello de dependência a seguir **dependências** nó. Esta dependência habilita você toouse Olá iot-serviço-pacote do cliente no toocommunicate seu aplicativo com o hub IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Você pode verificar a versão mais recente de saudação do **cliente de serviço iot** usando [pesquisa Maven][lnk-maven-service-search].

1. Adicione o seguinte Olá **criar** nó após Olá **dependências** nó. Esta configuração instrui Maven toouse Java toobuild 1.8 Olá aplicativo:

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. Salve e feche o arquivo de pom.xml hello.

1. Usando um editor de texto, abra o arquivo de origem trigger-reboot\src\main\java\com\mycompany\app\App.java hello.

1. Adicione o seguinte Olá **importar** arquivo de toohello instruções:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe. Substituir `{youriothubconnectionstring}` com a cadeia de conexão de hub IoT anotado na Olá *criar um IoT Hub* seção:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. tooimplement um thread que lê Olá relatado propriedades de duas de dispositivo de saudação a cada 10 segundos, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. método direto do tooinvoke hello reinicialização no dispositivo simulado de hello, adicionar Olá toohello de código a seguir **principal** método:

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. toostart Olá thread toopoll Olá relatadas propriedades do dispositivo simulado hello, adicione Olá toohello de código a seguir **principal** método:

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. tooenable toostop Olá aplicativo, adicione Olá toohello de código a seguir **principal** método:

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. Salve e feche o arquivo de trigger-reboot\src\main\java\com\mycompany\app\App.java hello.

1. Criar hello **gatilho reinicialização** aplicativos de back-end e corrigir os erros. No prompt de comando, navegue toohello gatilho reinicialização pasta e execução hello comando a seguir:

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado

Nesta seção, você cria um aplicativo de console Java que simula um dispositivo. aplicativo Hello escuta para chamada de método direto de reinicialização de saudação do seu hub IoT e responde imediatamente a chamada toothat. Olá aplicativo então dormem durante um processo de reinicialização de saudação toosimulate antes de usar uma saudação de toonotify propriedade relatado **gatilho reinicialização** aplicativo de back-end que Olá reinicialização for concluído.

1. Na pasta dm get iniciado hello, crie um projeto de Maven chamado **dispositivo simulado** usando Olá comando no prompt de comando a seguir. a seguir Olá é um comando longo, único:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. No prompt de comando, navegue pasta do dispositivo simulado toohello.

1. Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta do dispositivo simulado hello e adicione Olá toohello de dependência a seguir **dependências** nó. Esta dependência habilita você toouse Olá iot-serviço-pacote do cliente no toocommunicate seu aplicativo com o hub IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Você pode verificar a versão mais recente de saudação do **cliente de dispositivo iot** usando [pesquisa Maven][lnk-maven-device-search].

1. Adicione o seguinte Olá **criar** nó após Olá **dependências** nó. Esta configuração instrui Maven toouse Java toobuild 1.8 Olá aplicativo:

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. Salve e feche o arquivo de pom.xml hello.

1. Usando um editor de texto, abra o arquivo de origem simulated-device\src\main\java\com\mycompany\app\App.java hello.

1. Adicione o seguinte Olá **importar** arquivo de toohello instruções:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe. Substituir `{yourdeviceconnectionstring}` com a cadeia de conexão de dispositivo Olá observado em hello *criar uma identidade de dispositivo* seção:

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. tooimplement um manipulador de retorno de chamada para eventos de status de método direto, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. tooimplement um manipulador de retorno de chamada para eventos de status do dispositivo duas, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. tooimplement um manipulador de retorno de chamada para eventos de propriedade, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. tooimplement uma reinicialização do dispositivo thread toosimulate hello, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe. thread de saudação ficará suspenso por cinco segundos e, em seguida, define Olá **lastReboot** relatado propriedade:

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. método direto do hello tooimplement no dispositivo Olá, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe. Quando o aplicativo simulado Olá recebe uma chamada toohello **reinicializar** método direto, ele retorna um chamador de toohello de confirmação e, em seguida, inicia uma saudação do thread tooprocess reinicializar:

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. Modificar assinatura Olá Olá **principal** saudação do método toothrow exceções a seguir:

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. tooinstantiate um **DeviceClient**, adicionar Olá toohello de código a seguir **principal** método:

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. toostart escuta para chamadas de método direto, adicionar Olá toohello de código a seguir **principal** método:

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. tooshut para baixo o simulador do dispositivo hello, adicionar Olá toohello de código a seguir **principal** método:

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. Salve e feche o arquivo de simulated-device\src\main\java\com\mycompany\app\App.java hello.

1. Criar hello **dispositivo simulado** aplicativo de back-end e corrigir os erros. No prompt de comando, navegue pasta do dispositivo simulado toohello e execução hello comando a seguir:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Executar aplicativos Olá

Agora você está pronto toorun Olá aplicativos.

1. Em um prompt de comando na pasta do dispositivo simulado hello, execute Olá aguardando chamadas de método de reinicialização do seu hub IoT de toobegin de comando a seguir:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub de Java simulados toolisten do aplicativo de dispositivo para chamadas de método direto de reinicialização][1]

1. No prompt de comando na pasta de reinicialização de gatilho hello, execute Olá a seguir do método de reinicialização do comando toocall hello em seu dispositivo simulado de seu hub IoT:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Saudação de toocall de aplicativo de serviço de IoT Hub de Java reinicializar método direto][2]

1. dispositivo simulado Olá responde toohello chamada de método direto de reinicialização:

    ![Aplicativo de dispositivo simulado Java IoT Hub responde toohello chamada de método direto][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22