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
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="a3fe9-104">Agendar e difundir trabalhos (Java)</span><span class="sxs-lookup"><span data-stu-id="a3fe9-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="a3fe9-105">Use trabalhos Azure IoT Hub tooschedule e rastrear que atualizam milhões de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="a3fe9-106">Use trabalhos para:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-106">Use jobs to:</span></span>

* <span data-ttu-id="a3fe9-107">Atualizar as propriedades desejadas</span><span class="sxs-lookup"><span data-stu-id="a3fe9-107">Update desired properties</span></span>
* <span data-ttu-id="a3fe9-108">Marcas de atualização</span><span class="sxs-lookup"><span data-stu-id="a3fe9-108">Update tags</span></span>
* <span data-ttu-id="a3fe9-109">Chamar métodos diretos</span><span class="sxs-lookup"><span data-stu-id="a3fe9-109">Invoke direct methods</span></span>

<span data-ttu-id="a3fe9-110">Um trabalho envolve uma dessas ações e rastreia Olá a execução de um conjunto de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-110">A job wraps one of these actions and tracks hello execution against a set of devices.</span></span> <span data-ttu-id="a3fe9-111">Uma consulta de duas do dispositivo define o conjunto de saudação de dispositivos Olá trabalho é executado em relação.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-111">A device twin query defines hello set of devices hello job executes against.</span></span> <span data-ttu-id="a3fe9-112">Por exemplo, um aplicativo de back-end pode usar um trabalho tooinvoke um método direto em 10.000 dispositivos que reinicia dispositivos hello.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-112">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="a3fe9-113">Você especifica o conjunto de saudação de dispositivos com uma consulta de duas do dispositivo e agenda Olá trabalho toorun no futuro.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-113">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="a3fe9-114">Olá trabalho rastreia progresso como cada um dos dispositivos de saudação receber e executar o método direto de reinicialização hello.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-114">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="a3fe9-115">toolearn mais sobre cada um desses recursos, consulte:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-115">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="a3fe9-116">Dispositivo gêmeo e propriedades: [Introdução a dispositivos gêmeos](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="a3fe9-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="a3fe9-117">Métodos diretos: [Guia do desenvolvedor do Hub IoT – métodos diretos](iot-hub-devguide-direct-methods.md) e [Tutorial: Usar métodos diretos](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="a3fe9-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="a3fe9-118">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="a3fe9-119">Crie um aplicativo de dispositivo que implemente um método chamado **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="a3fe9-120">aplicativo de dispositivo Olá também recebe alterações de propriedade desejados do aplicativo de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-120">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="a3fe9-121">Criar um aplicativo de back-end que cria uma saudação do trabalho toocall **lockDoor** método direto em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-121">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="a3fe9-122">Outro trabalho envia toomultiple dispositivos de atualizações de propriedade desejados.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-122">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="a3fe9-123">No final da saudação deste tutorial, você tem um aplicativo de dispositivo do console de java e um aplicativo de back-end do console de java:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-123">At hello end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="a3fe9-124">**dispositivo simulado** que se conecta tooyour IoT hub, implementa Olá **lockDoor** direcionar o método e manipula desejado alterações de propriedade.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-124">**simulated-device** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="a3fe9-125">**Agendar trabalhos** que usam Olá de toocall trabalhos **lockDoor** direta duas de dispositivo de saudação do método e atualização desejado propriedades em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-125">**schedule-jobs** that use jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="a3fe9-126">artigo Olá [SDKs do Azure IoT](iot-hub-devguide-sdks.md) fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-126">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3fe9-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a3fe9-127">Prerequisites</span></span>

<span data-ttu-id="a3fe9-128">toocomplete neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-128">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="a3fe9-129">Olá mais recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="a3fe9-129">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="a3fe9-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="a3fe9-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="a3fe9-131">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-131">An active Azure account.</span></span> <span data-ttu-id="a3fe9-132">(Se você não tiver uma conta, poderá criar uma [conta gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="a3fe9-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="a3fe9-133">Se você preferir a identidade do dispositivo Olá toocreate programaticamente, ler a seção correspondente Olá Olá [conectar seu hub IoT de tooyour de dispositivo usando o Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artigo.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-133">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="a3fe9-134">Você também pode usar o hello [Gerenciador de Hub IOT](https://github.com/Azure/iothub-explorer) ferramenta tooadd um hub do dispositivo tooyour IoT.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-134">You can also use hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool tooadd a device tooyour IoT hub.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="a3fe9-135">Criar aplicativo de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="a3fe9-135">Create hello service app</span></span>

<span data-ttu-id="a3fe9-136">Nesta seção, você cria um aplicativo de console Java que usa trabalhos para:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="a3fe9-137">Chamar hello **lockDoor** método direto em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-137">Call hello **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="a3fe9-138">Envie propriedades desejadas toomultiple dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-138">Send desired properties toomultiple devices.</span></span>

<span data-ttu-id="a3fe9-139">aplicativo hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-139">toocreate hello app:</span></span>

1. <span data-ttu-id="a3fe9-140">No computador de desenvolvimento, crie uma pasta vazia chamada `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="a3fe9-141">Em Olá `iot-java-schedule-jobs` pasta, crie um projeto Maven chamado **agendar trabalhos** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-141">In hello `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using hello following command at your command prompt.</span></span> <span data-ttu-id="a3fe9-142">Observe que este é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="a3fe9-143">No prompt de comando, navegue toohello `schedule-jobs` pasta.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-143">At your command prompt, navigate toohello `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="a3fe9-144">Usando um editor de texto, abra Olá `pom.xml` arquivo hello `schedule-jobs` pasta e adicione Olá seguir dependência toohello **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-144">Using a text editor, open hello `pom.xml` file in hello `schedule-jobs` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="a3fe9-145">Esta dependência habilita Olá toouse **cliente de serviço iot** pacote no toocommunicate seu aplicativo com o hub IoT:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-145">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="a3fe9-146">Você pode verificar a versão mais recente de saudação do **cliente de serviço iot** usando [pesquisa Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="a3fe9-146">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="a3fe9-147">Adicione o seguinte Olá **criar** nó após Olá **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-147">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="a3fe9-148">Esta configuração instrui Maven toouse Java toobuild 1.8 Olá aplicativo:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-148">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="a3fe9-149">Salve e feche o hello `pom.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="a3fe9-150">Usando um editor de texto, abra Olá `schedule-jobs\src\main\java\com\mycompany\app\App.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-150">Using a text editor, open hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="a3fe9-151">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-151">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="a3fe9-152">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-152">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="a3fe9-153">Substituir `{youriothubconnectionstring}` com a cadeia de conexão de hub IoT anotado na Olá *criar um IoT Hub* seção:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="a3fe9-154">Adicionar Olá toohello do método a seguir **aplicativo** classe tooschedule uma saudação do trabalho tooupdate **construção** e **Floor** propriedades em duas de dispositivo Olá desejadas:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-154">Add hello following method toohello **App** class tooschedule a job tooupdate hello **Building** and **Floor** desired properties in hello device twin:</span></span>

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

1. <span data-ttu-id="a3fe9-155">tooschedule uma saudação do trabalho toocall **lockDoor** método, adicionar Olá após o método toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-155">tooschedule a job toocall hello **lockDoor** method, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="a3fe9-156">toomonitor um trabalho, adicionar Olá após o método toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-156">toomonitor a job, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="a3fe9-157">tooquery para obter detalhes de saudação de trabalhos Olá executou, adicione Olá método a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-157">tooquery for hello details of hello jobs you ran, add hello following method:</span></span>

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

1. <span data-ttu-id="a3fe9-158">Saudação de atualização **principal** seguinte de saudação do método assinatura tooinclude `throws` cláusula:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-158">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="a3fe9-159">toorun e monitor de dois trabalhos em sequência, adicionar Olá toohello de código a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-159">toorun and monitor two jobs sequentially, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="a3fe9-160">Salve e feche o hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` arquivo</span><span class="sxs-lookup"><span data-stu-id="a3fe9-160">Save and close hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="a3fe9-161">Criar hello **agendar trabalhos** aplicativo e corrigir os erros.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-161">Build hello **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="a3fe9-162">No prompt de comando, navegue toohello `schedule-jobs` pasta e execução hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-162">At your command prompt, navigate toohello `schedule-jobs` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="a3fe9-163">Criar um aplicativo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="a3fe9-163">Create a device app</span></span>

<span data-ttu-id="a3fe9-164">Nesta seção, você deve criar um aplicativo de console de Java identificadores Olá propriedades desejadas enviadas da chamada de método direto Olá IoT Hub e implementa.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-164">In this section, you create a Java console app that handles hello desired properties sent from IoT Hub and implements hello direct method call.</span></span>

1. <span data-ttu-id="a3fe9-165">Em Olá `iot-java-schedule-jobs` pasta, crie um projeto Maven chamado **dispositivo simulado** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-165">In hello `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="a3fe9-166">Observe que este é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="a3fe9-167">No prompt de comando, navegue toohello `simulated-device` pasta.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-167">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="a3fe9-168">Usando um editor de texto, abra Olá `pom.xml` arquivo hello `simulated-device` pasta e adicione Olá seguir dependências toohello **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-168">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="a3fe9-169">Esta dependência habilita Olá toouse **cliente de dispositivo iot** pacote no toocommunicate seu aplicativo com o hub IoT:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-169">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="a3fe9-170">Você pode verificar a versão mais recente de saudação do **cliente de dispositivo iot** usando [pesquisa Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="a3fe9-170">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="a3fe9-171">Adicione o seguinte Olá **criar** nó após Olá **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-171">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="a3fe9-172">Esta configuração instrui Maven toouse Java toobuild 1.8 Olá aplicativo:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-172">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="a3fe9-173">Salve e feche o hello `pom.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-173">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="a3fe9-174">Usando um editor de texto, abra Olá `simulated-device\src\main\java\com\mycompany\app\App.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-174">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="a3fe9-175">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-175">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="a3fe9-176">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-176">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="a3fe9-177">Substituindo `{youriothubname}` com seu nome de hub IoT, e `{yourdevicekey}` com valor de chave de dispositivo do hello gerado na Olá *criar uma identidade de dispositivo* seção:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="a3fe9-178">Este aplicativo de exemplo usa Olá **protocolo** variável quando ele cria uma **DeviceClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-178">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="a3fe9-179">Atualmente, toouse dispositivo duas recursos você deve usar o protocolo de MQTT saudação.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-179">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="a3fe9-180">tooprint dispositivo duas notificações toohello console, adicione o seguinte Olá aninhados classe toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-180">tooprint device twin notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="a3fe9-181">tooprint direta método notificações toohello console, adicione o seguinte Olá aninhados classe toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-181">tooprint direct method notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="a3fe9-182">chamadas de método direto toohandle de IoT Hub, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-182">toohandle direct method calls from IoT Hub, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="a3fe9-183">Saudação de atualização **principal** seguinte de saudação do método assinatura tooinclude `throws` cláusula:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-183">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="a3fe9-184">Adicionar Olá toohello de código a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-184">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="a3fe9-185">Crie um toocommunicate de cliente de dispositivo com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-185">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="a3fe9-186">Criar um **dispositivo** toostore Olá dispositivo duas propriedades do objeto.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-186">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="a3fe9-187">Serviços de cliente de dispositivo de saudação toostart, adicionar Olá toohello de código a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-187">toostart hello device client services, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="a3fe9-188">toowait de saudação do hello usuário toopress **Enter** chave antes de desligar, adicione Olá após o final do código toohello de saudação **principal** método:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-188">toowait for hello user toopress hello **Enter** key before shutting down, add hello following code toohello end of hello **main** method:</span></span>

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="a3fe9-189">Salve e feche o hello `simulated-device\src\main\java\com\mycompany\app\App.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-189">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="a3fe9-190">Criar hello **dispositivo simulado** aplicativo e corrigir os erros.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-190">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="a3fe9-191">No prompt de comando, navegue toohello `simulated-device` pasta e execução hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-191">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="a3fe9-192">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="a3fe9-192">Run hello apps</span></span>

<span data-ttu-id="a3fe9-193">Agora você está pronto toorun Olá os aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-193">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="a3fe9-194">Em um prompt de comando no hello `simulated-device` pasta, execute o hello aplicativo de dispositivo do comando toostart Olá escuta de alterações de propriedade desejados e chamadas de método direto a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-194">At a command prompt in hello `simulated-device` folder, run hello following command toostart hello device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Olá dispositivo cliente é iniciado](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="a3fe9-196">Em um prompt de comando no hello `schedule-jobs` pasta, execute Olá Olá de toorun de comando a seguir **agendar trabalhos** toorun dois trabalhos do aplicativo de serviço.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-196">At a command prompt in hello `schedule-jobs` folder, run hello following command toorun hello **schedule-jobs** service app toorun two jobs.</span></span> <span data-ttu-id="a3fe9-197">Olá primeiro define valores de propriedade Olá desejado, chamadas de segundo Olá Olá método direto:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-197">hello first sets hello desired property values, hello second calls hello direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![O serviço de aplicativo de Hub IoT Java cria dois trabalhos](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="a3fe9-199">Olá dispositivo aplicativo lida com a alteração da propriedade Olá desejado e chamada de método direto de saudação:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-199">hello device app handles hello desired property change and hello direct method call:</span></span>

    ![cliente de dispositivo Olá responde toohello alterações](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="a3fe9-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a3fe9-201">Next steps</span></span>

<span data-ttu-id="a3fe9-202">Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-202">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="a3fe9-203">Você criou um aplicativo de back-end toorun dois trabalhos.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-203">You created a back-end app toorun two jobs.</span></span> <span data-ttu-id="a3fe9-204">trabalho primeiro Olá definir valores de propriedade desejados e trabalho de segundo Olá chamou um método direto.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-204">hello first job set desired property values, and hello second job called a direct method.</span></span>

<span data-ttu-id="a3fe9-205">Saudação de uso toolearn de recursos a seguir como a:</span><span class="sxs-lookup"><span data-stu-id="a3fe9-205">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="a3fe9-206">Enviar telemetria de dispositivos com hello [começar com o IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-206">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="a3fe9-207">Controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário) com hello [usar métodos diretos](iot-hub-java-java-direct-methods.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3fe9-207">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
