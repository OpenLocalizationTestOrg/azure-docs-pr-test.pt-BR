---
title: aaaGet iniciado com twins de dispositivo do Azure IoT Hub (Java) | Microsoft Docs
description: "Como toouse Azure IoT Hub dispositivo twins tooadd marcas e, em seguida, use uma consulta de IoT Hub. Você pode usar dispositivo IoT do Azure de saudação SDK para aplicativo de dispositivo do Java tooimplement hello e hello SDK do serviço de IoT do Azure para Java tooimplement um aplicativo de serviço que adiciona marcas hello e executa Olá consulta de IoT Hub."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a>Introdução ao dispositivos gêmeos (Java)

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Neste tutorial, você cria dois aplicativos de console do Java:

* **add-tags-query**, um aplicativo de back-end Java que adiciona dispositivos gêmeos de marcas e consultas.
* **dispositivo simulado**, um aplicativo de dispositivo de Java que que conecta tooyour IoT hub e relatórios sua condição de conectividade usando uma propriedade relatada.

> [!NOTE]
> artigo Olá [SDKs do Azure IoT](iot-hub-devguide-sdks.md) fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.

toocomplete neste tutorial, você precisa:

* Olá mais recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Uma conta ativa do Azure. (Se você não tiver uma conta, poderá criar uma [conta gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Se você preferir a identidade do dispositivo Olá toocreate programaticamente, ler a seção correspondente Olá Olá [conectar seu hub IoT de tooyour de dispositivo usando o Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artigo.

## <a name="create-hello-service-app"></a>Criar aplicativo de serviço Olá

Nesta seção, você cria um aplicativo Java que adiciona metadados local como duas de dispositivo de toohello uma marca no IoT Hub associada **myDeviceId**. primeiro, o aplicativo Hello consulta hub IoT para dispositivos localizados em Olá dos EUA e, em seguida, para dispositivos que se reportam a uma conexão de rede de celular.

1. No computador de desenvolvimento, crie uma pasta vazia chamada `iot-java-twin-getstarted`.

1. Em Olá `iot-java-twin-getstarted` pasta, crie um projeto Maven chamado **adicionar marcas-consulta** usando Olá comando no prompt de comando a seguir. Observe que este é um comando único e longo:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. No prompt de comando, navegue toohello `add-tags-query` pasta.

1. Usando um editor de texto, abra Olá `pom.xml` arquivo hello `add-tags-query` pasta e adicione Olá seguir dependência toohello **dependências** nó. Esta dependência habilita Olá toouse **cliente de serviço iot** pacote no toocommunicate seu aplicativo com o hub IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Você pode verificar a versão mais recente de saudação do **cliente de serviço iot** usando [pesquisa Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

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

1. Salve e feche o hello `pom.xml` arquivo.

1. Usando um editor de texto, abra Olá `add-tags-query\src\main\java\com\mycompany\app\App.java` arquivo.

1. Adicione o seguinte Olá **importar** arquivo de toohello instruções:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe. Substituir `{youriothubconnectionstring}` com a cadeia de conexão de hub IoT anotado na Olá *criar um IoT Hub* seção:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. Saudação de atualização **principal** seguinte de saudação do método assinatura tooinclude `throws` cláusula:

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. Adicionar Olá toohello de código a seguir **principal** saudação do método toocreate **DeviceTwin** e **DeviceTwinDevice** objetos. Olá **DeviceTwin** a comunicação com o hub IoT Olá alças do objeto. Olá **DeviceTwinDevice** objeto representa duas de dispositivo Olá com suas propriedades e marcas:

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. Adicione o seguinte Olá `try/catch` bloquear toohello **principal** método:

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. Olá tooupdate **região** e **planta** marcas de duas do dispositivo em duas seu dispositivo, adicione Olá Olá código a seguir `try` bloco:

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. twins de dispositivo tooquery Olá no hub IoT, adicionar Olá toohello de código a seguir `try` bloco após código Olá adicionado na etapa anterior hello. código de saudação executa duas consultas. Cada consulta retorna um máximo de 100 dispositivos:

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. Salve e feche o hello `add-tags-query\src\main\java\com\mycompany\app\App.java` arquivo

1. Criar hello **adicionar marcas-consulta** aplicativo e corrigir os erros. No prompt de comando, navegue toohello `add-tags-query` pasta e execução hello comando a seguir:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Criar um aplicativo de dispositivo

Nesta seção, você deve criar um aplicativo de console de Java que define um valor de propriedade relatado enviada tooIoT Hub.

1. Em Olá `iot-java-twin-getstarted` pasta, crie um projeto Maven chamado **dispositivo simulado** usando Olá comando no prompt de comando a seguir. Observe que este é um comando único e longo:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. No prompt de comando, navegue toohello `simulated-device` pasta.

1. Usando um editor de texto, abra Olá `pom.xml` arquivo hello `simulated-device` pasta e adicione Olá seguir dependências toohello **dependências** nó. Esta dependência habilita Olá toouse **cliente de dispositivo iot** pacote no toocommunicate seu aplicativo com o hub IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Você pode verificar a versão mais recente de saudação do **cliente de dispositivo iot** usando [pesquisa Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

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

1. Salve e feche o hello `pom.xml` arquivo.

1. Usando um editor de texto, abra Olá `simulated-device\src\main\java\com\mycompany\app\App.java` arquivo.

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
    ```

    Este aplicativo de exemplo usa Olá **protocolo** variável quando ele cria uma **DeviceClient** objeto. Atualmente, toouse dispositivo duas recursos você deve usar o protocolo de MQTT saudação.

1. Adicionar Olá toohello de código a seguir **principal** método:
    * Crie um toocommunicate de cliente de dispositivo com o IoT Hub.
    * Criar um **dispositivo** toostore Olá dispositivo duas propriedades do objeto.

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. Adicionar Olá toohello de código a seguir **principal** método toocreate um **connectivityType** relatados de propriedade e enviá-lo tooIoT Hub:

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. Adicionar Olá após o final do código toohello de saudação **principal** método. Aguardando Olá **Enter** chave permite que o tempo para o IoT Hub tooreport Olá status Olá dispositivo duas operações:

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. Salve e feche o hello `simulated-device\src\main\java\com\mycompany\app\App.java` arquivo.

1. Criar hello **dispositivo simulado** aplicativo e corrigir os erros. No prompt de comando, navegue toohello `simulated-device` pasta e execução hello comando a seguir:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Executar aplicativos Olá

Agora você está pronto toorun Olá os aplicativos de console.

1. Em um prompt de comando no hello `add-tags-query` pasta, execute Olá Olá de toorun de comando a seguir **adicionar marcas-consulta** do serviço de aplicativo:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Valores de marca de tooupdate de aplicativo de serviço de IoT Hub de Java e executar consultas de dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    Você pode ver Olá **planta** e **região** marcas adicionadas toohello duas de dispositivo. Olá primeira consulta retorna seu dispositivo, mas Olá segundo não.

1. Em um prompt de comando no hello `simulated-device` pasta, execute Olá Olá de tooadd de comando a seguir **connectivityType** relatado duas de dispositivo de toohello de propriedade:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![cliente de dispositivo Olá adiciona hello * * connectivityType * * relatado propriedade](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. Em um prompt de comando no hello `add-tags-query` pasta, execute Olá Olá de toorun de comando a seguir **adicionar marcas-consulta** uma segunda vez do serviço de aplicativo:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Valores de marca de tooupdate de aplicativo de serviço de IoT Hub de Java e executar consultas de dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    Agora seu dispositivo enviou Olá **connectivityType** tooIoT propriedade Hub, a segunda consulta de saudação retorna seu dispositivo.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello. Você adicionou o metadados do dispositivo como marcas de um aplicativo de back-end e gravou informações de conectividade do dispositivo do dispositivo aplicativo tooreport em duas de dispositivo de saudação. Você também aprendeu como tooquery Olá informações do dispositivo duas usando linguagem de consulta do tipo SQL IoT Hub hello.

Saudação de uso toolearn de recursos a seguir como a:

* Enviar telemetria de dispositivos com hello [começar com o IoT Hub](iot-hub-java-java-getstarted.md) tutorial.
* Controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário) com hello [usar métodos diretos](iot-hub-java-java-direct-methods.md) tutorial.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
