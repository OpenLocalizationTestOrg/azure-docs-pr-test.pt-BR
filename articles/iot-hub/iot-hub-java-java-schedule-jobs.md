---
title: trabalhos de aaaSchedule com o Azure IoT Hub (Java) | Microsoft Docs
description: "Como tooschedule um Azure IoT Hub tooinvoke um método direto de trabalho e definir uma propriedade desejada em vários dispositivos. Você pode usar dispositivo IoT do Azure de saudação SDK para aplicativos de dispositivos do Java tooimplement Olá simulado e hello SDK do serviço de IoT do Azure para Java tooimplement um trabalho de saudação de toorun de aplicativo de serviço."
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
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: b1b05fa56c3ce96af0b33d4cca0dd54da0f4e927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a>Agendar e difundir trabalhos (Java)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Use trabalhos Azure IoT Hub tooschedule e rastrear que atualizam milhões de dispositivos. Use trabalhos para:

* Atualizar as propriedades desejadas
* Marcas de atualização
* Chamar métodos diretos

Um trabalho envolve uma dessas ações e rastreia Olá a execução de um conjunto de dispositivos. Uma consulta de duas do dispositivo define o conjunto de saudação de dispositivos Olá trabalho é executado em relação. Por exemplo, um aplicativo de back-end pode usar um trabalho tooinvoke um método direto em 10.000 dispositivos que reinicia dispositivos hello. Você especifica o conjunto de saudação de dispositivos com uma consulta de duas do dispositivo e agenda Olá trabalho toorun no futuro. Olá trabalho rastreia progresso como cada um dos dispositivos de saudação receber e executar o método direto de reinicialização hello.

toolearn mais sobre cada um desses recursos, consulte:

* Dispositivo gêmeo e propriedades: [Introdução a dispositivos gêmeos](iot-hub-java-java-twin-getstarted.md)
* Métodos diretos: [Guia do desenvolvedor do Hub IoT – métodos diretos](iot-hub-devguide-direct-methods.md) e [Tutorial: Usar métodos diretos](iot-hub-java-java-direct-methods.md)

Este tutorial mostra como:

* Crie um aplicativo de dispositivo que implemente um método chamado **lockDoor**. aplicativo de dispositivo Olá também recebe alterações de propriedade desejados do aplicativo de back-end de saudação.
* Criar um aplicativo de back-end que cria uma saudação do trabalho toocall **lockDoor** método direto em vários dispositivos. Outro trabalho envia toomultiple dispositivos de atualizações de propriedade desejados.

No final da saudação deste tutorial, você tem um aplicativo de dispositivo do console de java e um aplicativo de back-end do console de java:

**dispositivo simulado** que se conecta tooyour IoT hub, implementa Olá **lockDoor** direcionar o método e manipula desejado alterações de propriedade.

**Agendar trabalhos** que usam Olá de toocall trabalhos **lockDoor** direta duas de dispositivo de saudação do método e atualização desejado propriedades em vários dispositivos.

> [!NOTE]
> artigo Olá [SDKs do Azure IoT](iot-hub-devguide-sdks.md) fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, você precisa:

* Olá mais recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Uma conta ativa do Azure. (Se você não tiver uma conta, poderá criar uma [conta gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Se você preferir a identidade do dispositivo Olá toocreate programaticamente, ler a seção correspondente Olá Olá [conectar seu hub IoT de tooyour de dispositivo usando o Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artigo. Você também pode usar o hello [Gerenciador de Hub IOT](https://github.com/Azure/iothub-explorer) ferramenta tooadd um hub do dispositivo tooyour IoT.

## <a name="create-hello-service-app"></a>Criar aplicativo de serviço Olá

Nesta seção, você cria um aplicativo de console Java que usa trabalhos para:

* Chamar hello **lockDoor** método direto em vários dispositivos.
* Envie propriedades desejadas toomultiple dispositivos.

aplicativo hello toocreate:

1. No computador de desenvolvimento, crie uma pasta vazia chamada `iot-java-schedule-jobs`.

1. Em Olá `iot-java-schedule-jobs` pasta, crie um projeto Maven chamado **agendar trabalhos** usando Olá comando no prompt de comando a seguir. Observe que este é um comando único e longo:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. No prompt de comando, navegue toohello `schedule-jobs` pasta.

1. Usando um editor de texto, abra Olá `pom.xml` arquivo hello `schedule-jobs` pasta e adicione Olá seguir dependência toohello **dependências** nó. Esta dependência habilita Olá toouse **cliente de serviço iot** pacote no toocommunicate seu aplicativo com o hub IoT:

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

1. Usando um editor de texto, abra Olá `schedule-jobs\src\main\java\com\mycompany\app\App.java` arquivo.

1. Adicione o seguinte Olá **importar** arquivo de toohello instruções:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe. Substituir `{youriothubconnectionstring}` com a cadeia de conexão de hub IoT anotado na Olá *criar um IoT Hub* seção:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. Adicionar Olá toohello do método a seguir **aplicativo** classe tooschedule uma saudação do trabalho tooupdate **construção** e **Floor** propriedades em duas de dispositivo Olá desejadas:

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule hello update twin job toorun now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. tooschedule uma saudação do trabalho toocall **lockDoor** método, adicionar Olá após o método toohello **aplicativo** classe:

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now toocall hello lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set too5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. toomonitor um trabalho, adicionar Olá após o método toohello **aplicativo** classe:

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check hello job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. tooquery para obter detalhes de saudação de trabalhos Olá executou, adicione Olá método a seguir:

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using hello time hello jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over hello list of jobs and print hello details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. Saudação de atualização **principal** seguinte de saudação do método assinatura tooinclude `throws` cláusula:

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. toorun e monitor de dois trabalhos em sequência, adicionar Olá toohello de código a seguir **principal** método:

    ```java
    // Record hello start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query tooshow hello job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. Salve e feche o hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` arquivo

1. Criar hello **agendar trabalhos** aplicativo e corrigir os erros. No prompt de comando, navegue toohello `schedule-jobs` pasta e execução hello comando a seguir:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Criar um aplicativo de dispositivo

Nesta seção, você deve criar um aplicativo de console de Java identificadores Olá propriedades desejadas enviadas da chamada de método direto Olá IoT Hub e implementa.

1. Em Olá `iot-java-schedule-jobs` pasta, crie um projeto Maven chamado **dispositivo simulado** usando Olá comando no prompt de comando a seguir. Observe que este é um comando único e longo:

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
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Este aplicativo de exemplo usa Olá **protocolo** variável quando ele cria uma **DeviceClient** objeto. Atualmente, toouse dispositivo duas recursos você deve usar o protocolo de MQTT saudação.

1. tooprint dispositivo duas notificações toohello console, adicione o seguinte Olá aninhados classe toohello **aplicativo** classe:

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. tooprint direta método notificações toohello console, adicione o seguinte Olá aninhados classe toohello **aplicativo** classe:

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. chamadas de método direto toohandle de IoT Hub, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. Saudação de atualização **principal** seguinte de saudação do método assinatura tooinclude `throws` cláusula:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. Adicionar Olá toohello de código a seguir **principal** método:
    * Crie um toocommunicate de cliente de dispositivo com o IoT Hub.
    * Criar um **dispositivo** toostore Olá dispositivo duas propriedades do objeto.

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object toomanage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. Serviços de cliente de dispositivo de saudação toostart, adicionar Olá toohello de código a seguir **principal** método:

    ```java
    try {
      // Open hello DeviceClient
      // Start hello device twin services
      // Subscribe toodirect method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. toowait de saudação do hello usuário toopress **Enter** chave antes de desligar, adicione Olá após o final do código toohello de saudação **principal** método:

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. Salve e feche o hello `simulated-device\src\main\java\com\mycompany\app\App.java` arquivo.

1. Criar hello **dispositivo simulado** aplicativo e corrigir os erros. No prompt de comando, navegue toohello `simulated-device` pasta e execução hello comando a seguir:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Executar aplicativos Olá

Agora você está pronto toorun Olá os aplicativos de console.

1. Em um prompt de comando no hello `simulated-device` pasta, execute o hello aplicativo de dispositivo do comando toostart Olá escuta de alterações de propriedade desejados e chamadas de método direto a seguir:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Olá dispositivo cliente é iniciado](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. Em um prompt de comando no hello `schedule-jobs` pasta, execute Olá Olá de toorun de comando a seguir **agendar trabalhos** toorun dois trabalhos do aplicativo de serviço. Olá primeiro define valores de propriedade Olá desejado, chamadas de segundo Olá Olá método direto:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![O serviço de aplicativo de Hub IoT Java cria dois trabalhos](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. Olá dispositivo aplicativo lida com a alteração da propriedade Olá desejado e chamada de método direto de saudação:

    ![cliente de dispositivo Olá responde toohello alterações](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello. Você criou um aplicativo de back-end toorun dois trabalhos. trabalho primeiro Olá definir valores de propriedade desejados e trabalho de segundo Olá chamou um método direto.

Saudação de uso toolearn de recursos a seguir como a:

* Enviar telemetria de dispositivos com hello [começar com o IoT Hub](iot-hub-java-java-getstarted.md) tutorial.
* Controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário) com hello [usar métodos diretos](iot-hub-java-java-direct-methods.md) tutorial.
