---
title: "aaaUse Azure IoT Hub direcionar métodos (Java) | Microsoft Docs"
description: "Como toouse Azure IoT Hub direta métodos. Use dispositivo IoT do Azure de saudação SDK para Java tooimplement um aplicativo de dispositivo simulado que inclui um método direto e hello SDK do serviço de IoT do Azure para Java tooimplement um aplicativo de serviço que invoca o método direto hello."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a>Usar métodos diretos (Java)

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Neste tutorial, você cria dois aplicativos de console do Java:

* **método Invoke de direct**, um aplicativo de back-end de Java que chama um método no aplicativo do dispositivo simulado hello e exibe a resposta de saudação.
* **dispositivo simulado**, um aplicativo Java que simula um dispositivo conectado tooyour IoT hub com a identidade do dispositivo Olá você criar. Este aplicativo responde toohello chamada direta de back-end hello.

> [!NOTE]
> Para obter informações sobre Olá SDKs que você pode usar toobuild toorun de aplicativos em dispositivos e o back-end de solução, consulte [SDKs do Azure IoT][lnk-hub-sdks].

toocomplete neste tutorial, você precisa:

* Java SE 8. <br/> [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Java para este tutorial no Windows ou Linux.
* Maven 3.  <br/> [Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall [Maven] [ lnk-maven] para este tutorial no Windows ou Linux.
* [Versão do Node.js 0.10.0 ou posterior](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado

Nesta seção, você deve criar um aplicativo de console de Java que responde tooa método chamado pela solução de saudação volta final.

1. Crie uma pasta vazia chamada iot-java-direct-method.

1. Na pasta de iot java direct-método-Olá, crie um projeto de Maven chamado **dispositivo simulado** usando Olá comando no prompt de comando a seguir. saudação de comando a seguir é um comando longo, único:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. No prompt de comando, navegue pasta do dispositivo simulado toohello.

1. Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta do dispositivo simulado hello e adicione Olá dependências toohello a seguir **dependências** nó. Essa dependência permite que você toouse Olá cliente de dispositivo iot pacote em toocommunicate seu aplicativo com o hub IoT:

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

1. Usando um editor de texto, abra o arquivo de simulated-device\src\main\java\com\mycompany\app\App.java de saudação.

1. Adicione o seguinte Olá **importar** arquivo de toohello instruções:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe. Substituindo `{youriothubname}` com seu nome de hub IoT, e `{yourdevicekey}` com valor de chave de dispositivo do hello gerado na Olá *criar uma identidade de dispositivo* seção:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Este aplicativo de exemplo usa Olá **protocolo** variável quando ele cria uma **DeviceClient** objeto. Atualmente, toouse direta métodos que você deve usar o protocolo de MQTT saudação.

1. tooreturn um hub IoT de tooyour de código de status, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. invocações de método direto Olá toohandle de saudação solução back-end, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. toocreate um **DeviceClient** e escutar para invocações de método direto, adicione um **principal** método toohello **aplicativo** classe:

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. Salve e feche o arquivo de simulated-device\src\main\java\com\mycompany\app\App.java Olá

1. Criar hello **dispositivo simulado** aplicativo e corrigir os erros. No prompt de comando, navegue pasta do dispositivo simulado toohello e execução hello comando a seguir:

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a>Chama um método direto em um dispositivo

Nesta seção, você deve criar um aplicativo de console de Java que invoca um método direto e, em seguida, exibe a resposta de saudação. Este aplicativo de console se conecta tooyour método direto do IoT Hub tooinvoke hello.

1. Na pasta de iot java direct-método-Olá, crie um projeto de Maven chamado **invocar direct-método** usando Olá comando no prompt de comando a seguir. saudação de comando a seguir é um comando longo, único:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. No prompt de comando, navegue toohello invoke-direct-método pasta.

1. Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta de invoke-direct-método hello e adicione Olá toohello de dependência a seguir **dependências** nó. Esta dependência habilita você toouse Olá iot-serviço-pacote do cliente no toocommunicate seu aplicativo com o hub IoT:

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

1. Usando um editor de texto, abra o arquivo de invoke-direct-method\src\main\java\com\mycompany\app\App.java de saudação.

1. Adicione o seguinte Olá **importar** arquivo de toohello instruções:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe. Substituir `{youriothubconnectionstring}` com a cadeia de conexão de hub IoT anotado na Olá *criar um IoT Hub* seção:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. método de hello tooinvoke no dispositivo simulado de hello, adicionar Olá toohello de código a seguir **principal** método:

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. Salve e feche o arquivo de invoke-direct-method\src\main\java\com\mycompany\app\App.java Olá

1. Criar hello **invocar direct-método** aplicativo e corrigir os erros. No prompt de comando, navegue toohello invoke-direct-método pasta e execução hello comando a seguir:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Executar aplicativos Olá

Agora você está pronto toorun Olá os aplicativos de console.

1. Em um prompt de comando na pasta do dispositivo simulado hello, execute Olá escutando chamadas de método do seu hub IoT de toobegin de comando a seguir:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub de Java simulados toolisten do aplicativo de dispositivo para chamadas de método direto][8]

1. Em um prompt de comando na pasta de invocar direta método-Olá, execute Olá toocall de comando a seguir um método no seu dispositivo simulado do seu hub IoT:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Toocall de aplicativo de serviço do IoT Hub de Java um método direto][7]

1. dispositivo simulado Olá responde a chamada de método direto toohello:

    ![Aplicativo de dispositivo simulado Java IoT Hub responde toohello chamada de método direto][9]

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello. Você usou esse dispositivo identidade tooenable Olá simulado dispositivo aplicativo tooreact toomethods invocado pela nuvem hello. Você também criou um aplicativo que chama métodos no dispositivo hello e exibe a resposta de saudação do dispositivo de saudação.

tooexplore outros cenários de IoT, consulte [agendar trabalhos em vários dispositivos][lnk-devguide-jobs].

toolearn como tooextend seu método de solução e agenda IoT chama em vários dispositivos, consulte Olá [agenda e trabalhos de difusão] [ lnk-tutorial-jobs] tutorial.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
