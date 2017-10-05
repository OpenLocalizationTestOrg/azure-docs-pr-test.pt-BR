---
title: Agendar trabalhos com o Hub IoT do Azure (Java) | Microsoft Docs
description: "Como agendar um trabalho do Hub IoT do Azure para invocar um método direto e definir uma propriedade desejada em vários dispositivos. Use o SDK do dispositivo IoT do Azure para Java para implementar os aplicativos de dispositivo e o SDK do serviço do IoT do Azure para Java para implementar um aplicativo de serviço que executa o trabalho."
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
ms.openlocfilehash: 003a548ef2da2921a699df1aa9f7aee366d341ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="5f717-104">Agendar e difundir trabalhos (Java)</span><span class="sxs-lookup"><span data-stu-id="5f717-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="5f717-105">Use o Hub IoT do Azure para agendar e controlar os trabalhos que atualizam milhões de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5f717-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="5f717-106">Use trabalhos para:</span><span class="sxs-lookup"><span data-stu-id="5f717-106">Use jobs to:</span></span>

* <span data-ttu-id="5f717-107">Atualizar as propriedades desejadas</span><span class="sxs-lookup"><span data-stu-id="5f717-107">Update desired properties</span></span>
* <span data-ttu-id="5f717-108">Marcas de atualização</span><span class="sxs-lookup"><span data-stu-id="5f717-108">Update tags</span></span>
* <span data-ttu-id="5f717-109">Chamar métodos diretos</span><span class="sxs-lookup"><span data-stu-id="5f717-109">Invoke direct methods</span></span>

<span data-ttu-id="5f717-110">Um trabalho encapsula uma dessas ações e controla a execução em um conjunto de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5f717-110">A job wraps one of these actions and tracks the execution against a set of devices.</span></span> <span data-ttu-id="5f717-111">Uma consulta dispositivo gêmeo define o conjunto de dispositivos para os quais o trabalho é executado.</span><span class="sxs-lookup"><span data-stu-id="5f717-111">A device twin query defines the set of devices the job executes against.</span></span> <span data-ttu-id="5f717-112">Por exemplo, um aplicativo de back-end pode usar um trabalho para invocar um método direto em 10.000 dispositivos que reinicie os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5f717-112">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="5f717-113">Você especifica o conjunto de dispositivos com uma consulta de dispositivo gêmeo e agenda o trabalho para execução futura.</span><span class="sxs-lookup"><span data-stu-id="5f717-113">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="5f717-114">O trabalho controla o andamento conforme cada um dos dispositivos recebe e executa o método direto de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="5f717-114">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="5f717-115">Para saber mais sobre cada uma dessas capacidades, consulte:</span><span class="sxs-lookup"><span data-stu-id="5f717-115">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="5f717-116">Dispositivo gêmeo e propriedades: [Introdução a dispositivos gêmeos](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="5f717-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="5f717-117">Métodos diretos: [Guia do desenvolvedor do Hub IoT – métodos diretos](iot-hub-devguide-direct-methods.md) e [Tutorial: Usar métodos diretos](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="5f717-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="5f717-118">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="5f717-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="5f717-119">Crie um aplicativo de dispositivo que implemente um método chamado **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="5f717-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="5f717-120">O aplicativo de dispositivo também recebe as alterações de propriedade desejadas do aplicativo de back-end.</span><span class="sxs-lookup"><span data-stu-id="5f717-120">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="5f717-121">Criar um aplicativo de back-end que gere um trabalho para chamar o método direto **lockDoor** em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5f717-121">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="5f717-122">Outro trabalho envia as atualizações de propriedade desejadas para vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5f717-122">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="5f717-123">Ao final deste tutorial, você terá um aplicativo de dispositivo de console Java e um aplicativo de back-end do console Java:</span><span class="sxs-lookup"><span data-stu-id="5f717-123">At the end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="5f717-124">**simulated-device**, que se conecta ao seu hub IoT, implementa o método direto **lockDoor** e manipula as alterações de propriedade desejadas.</span><span class="sxs-lookup"><span data-stu-id="5f717-124">**simulated-device** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="5f717-125">**schedule-jobs**, que usa trabalhos para chamar o método direto **lockDoor** e atualizar as propriedades desejadas do dispositivo gêmeo em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5f717-125">**schedule-jobs** that use jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="5f717-126">O artigo [SDKs de IoT do Azure](iot-hub-devguide-sdks.md) apresenta informações sobre os SDKs de IoT do Azure que você pode usar para criar dispositivos e aplicativos de back-end.</span><span class="sxs-lookup"><span data-stu-id="5f717-126">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f717-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5f717-127">Prerequisites</span></span>

<span data-ttu-id="5f717-128">Para concluir este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="5f717-128">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="5f717-129">A versão mais recente do [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="5f717-129">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="5f717-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="5f717-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="5f717-131">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f717-131">An active Azure account.</span></span> <span data-ttu-id="5f717-132">(Se você não tiver uma conta, poderá criar uma [conta gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="5f717-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="5f717-133">Se você preferir criar a identidade do dispositivo programaticamente, leia a seção correspondente no artigo [Conectar seu dispositivo ao seu Hub IoT usando Java](iot-hub-java-java-getstarted.md#create-a-device-identity).</span><span class="sxs-lookup"><span data-stu-id="5f717-133">If you prefer to create the device identity programmatically, read the corresponding section in the [Connect your device to your IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="5f717-134">Você também pode usar a ferramenta [Gerenciador de Hubs IoT](https://github.com/Azure/iothub-explorer) para adicionar um dispositivo ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5f717-134">You can also use the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to add a device to your IoT hub.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="5f717-135">Criar o aplicativo do serviço</span><span class="sxs-lookup"><span data-stu-id="5f717-135">Create the service app</span></span>

<span data-ttu-id="5f717-136">Nesta seção, você cria um aplicativo de console Java que usa trabalhos para:</span><span class="sxs-lookup"><span data-stu-id="5f717-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="5f717-137">Chamar o método direto **lockDoor** em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5f717-137">Call the **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="5f717-138">Enviar as propriedades desejadas para vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5f717-138">Send desired properties to multiple devices.</span></span>

<span data-ttu-id="5f717-139">Para criar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="5f717-139">To create the app:</span></span>

1. <span data-ttu-id="5f717-140">No computador de desenvolvimento, crie uma pasta vazia chamada `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="5f717-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="5f717-141">Na pasta `iot-java-schedule-jobs`, crie um projeto Maven chamado **schedule-jobs** usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="5f717-141">In the `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using the following command at your command prompt.</span></span> <span data-ttu-id="5f717-142">Observe que este é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="5f717-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="5f717-143">No prompt de comando, navegue até a pasta `schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="5f717-143">At your command prompt, navigate to the `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="5f717-144">Usando um editor de texto, abra o arquivo `pom.xml` na pasta `schedule-jobs` e adicione a dependência a seguir ao nó **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="5f717-144">Using a text editor, open the `pom.xml` file in the `schedule-jobs` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="5f717-145">Essa dependência permite que você use o pacote **iot-service-client** em seu aplicativo para se comunicar com seu hub IoT:</span><span class="sxs-lookup"><span data-stu-id="5f717-145">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="5f717-146">Você pode verificar a versão mais recente do **iot-service-client** usando a [pesquisa do Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="5f717-146">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="5f717-147">Adicione o seguinte nó **buid** após o nó **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="5f717-147">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="5f717-148">Esta configuração instrui o Maven a usar Java 1.8 para compilar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="5f717-148">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="5f717-149">Salve e feche o arquivo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="5f717-149">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="5f717-150">Usando um editor de texto, abra o arquivo `schedule-jobs\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="5f717-150">Using a text editor, open the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="5f717-151">Adicione as seguintes instruções **import** ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="5f717-151">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="5f717-152">Adicione as seguintes variáveis no nível da classe à classe **App** .</span><span class="sxs-lookup"><span data-stu-id="5f717-152">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="5f717-153">Substitua `{youriothubconnectionstring}` pela cadeia de conexão do hub IoT anotada na seção *Criar um Hub IoT*:</span><span class="sxs-lookup"><span data-stu-id="5f717-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long the job is permitted to run without
    // completing its work on the set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="5f717-154">Adicione o método a seguir à classe **Aplicativo** para agendar um trabalho para atualizar as propriedades **Prédio** e **Andar** desejadas no dispositivo gêmeo:</span><span class="sxs-lookup"><span data-stu-id="5f717-154">Add the following method to the **App** class to schedule a job to update the **Building** and **Floor** desired properties in the device twin:</span></span>

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule the update twin job to run now
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

1. <span data-ttu-id="5f717-155">Para agendar um trabalho para chamar o método **lockDoor**, adicione o método a seguir à classe **Aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="5f717-155">To schedule a job to call the **lockDoor** method, add the following method to the **App** class:</span></span>

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now to call the lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set to 5 seconds.
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

1. <span data-ttu-id="5f717-156">Para monitorar um trabalho, adicione o seguinte método à classe **Aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="5f717-156">To monitor a job, add the following method to the **App** class:</span></span>

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check the job result until it's completed
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

1. <span data-ttu-id="5f717-157">Para consultar detalhes dos trabalhos que você executou, adicione o seguinte método:</span><span class="sxs-lookup"><span data-stu-id="5f717-157">To query for the details of the jobs you ran, add the following method:</span></span>

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using the time the jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over the list of jobs and print the details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. <span data-ttu-id="5f717-158">Atualize a assinatura do método **principal** para incluir a seguinte cláusula `throws`:</span><span class="sxs-lookup"><span data-stu-id="5f717-158">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="5f717-159">Para executar e monitorar dois trabalhos em sequência, adicione o seguinte código ao método **main**:</span><span class="sxs-lookup"><span data-stu-id="5f717-159">To run and monitor two jobs sequentially, add the following code to the **main** method:</span></span>

    ```java
    // Record the start time
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

    // Run a query to show the job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. <span data-ttu-id="5f717-160">Salve e feche o arquivo `schedule-jobs\src\main\java\com\mycompany\app\App.java`</span><span class="sxs-lookup"><span data-stu-id="5f717-160">Save and close the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="5f717-161">Compile o aplicativo **schedule-jobs** e corrija eventuais erros.</span><span class="sxs-lookup"><span data-stu-id="5f717-161">Build the **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="5f717-162">No prompt de comando, navegue até a pasta `schedule-jobs` e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5f717-162">At your command prompt, navigate to the `schedule-jobs` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="5f717-163">Criar um aplicativo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="5f717-163">Create a device app</span></span>

<span data-ttu-id="5f717-164">Nesta seção, você deve criar um aplicativo de console de Java que manipule as propriedades desejadas enviadas do Hub IoT e implemente a chamada de método direto.</span><span class="sxs-lookup"><span data-stu-id="5f717-164">In this section, you create a Java console app that handles the desired properties sent from IoT Hub and implements the direct method call.</span></span>

1. <span data-ttu-id="5f717-165">Na pasta `iot-java-schedule-jobs`, crie um projeto Maven denominado **simulated-device** usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="5f717-165">In the `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="5f717-166">Observe que este é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="5f717-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="5f717-167">No prompt de comando, navegue até a pasta `simulated-device`.</span><span class="sxs-lookup"><span data-stu-id="5f717-167">At your command prompt, navigate to the `simulated-device` folder.</span></span>

1. <span data-ttu-id="5f717-168">Usando um editor de texto, abra o arquivo `pom.xml` na pasta `simulated-device` e adicione as dependências a seguir ao nó de **dependências**.</span><span class="sxs-lookup"><span data-stu-id="5f717-168">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="5f717-169">Essa dependência permite que você use o pacote **iot-device-client** em seu aplicativo para se comunicar com seu hub IoT:</span><span class="sxs-lookup"><span data-stu-id="5f717-169">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="5f717-170">Você pode verificar a versão mais recente do **iot-device-client** usando a [pesquisa do Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="5f717-170">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="5f717-171">Adicione o seguinte nó **buid** após o nó **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="5f717-171">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="5f717-172">Esta configuração instrui o Maven a usar Java 1.8 para compilar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="5f717-172">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="5f717-173">Salve e feche o arquivo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="5f717-173">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="5f717-174">Usando um editor de texto, abra o arquivo `simulated-device\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="5f717-174">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="5f717-175">Adicione as seguintes instruções **import** ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="5f717-175">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="5f717-176">Adicione as seguintes variáveis no nível da classe à classe **App** .</span><span class="sxs-lookup"><span data-stu-id="5f717-176">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="5f717-177">Substituir `{youriothubname}` pelo nome do hub IoT e `{yourdevicekey}` pelo valor da chave do dispositivo gerado na seção *Criar uma identidade do dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="5f717-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="5f717-178">Este aplicativo de exemplo usa a variável **protocol** quando cria uma instância de um objeto **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="5f717-178">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="5f717-179">No momento, para usar recursos de dispositivos gêmeos, você deve usar o protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="5f717-179">Currently, to use device twin features you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="5f717-180">Para imprimir notificações do dispositivo gêmeo para o console, adicione a seguinte classe aninhada à classe **App**:</span><span class="sxs-lookup"><span data-stu-id="5f717-180">To print device twin notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to device twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="5f717-181">Para imprimir notificações do método direto para o console, adicione a seguinte classe aninhada à classe **App**:</span><span class="sxs-lookup"><span data-stu-id="5f717-181">To print direct method notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to direct method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="5f717-182">Para manipular chamadas de método direto do Hub IoT, adicione a seguinte classe aninhada à classe **App**:</span><span class="sxs-lookup"><span data-stu-id="5f717-182">To handle direct method calls from IoT Hub, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="5f717-183">Atualize a assinatura do método **principal** para incluir a seguinte cláusula `throws`:</span><span class="sxs-lookup"><span data-stu-id="5f717-183">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="5f717-184">Adicione o seguinte código ao método **principal** para:</span><span class="sxs-lookup"><span data-stu-id="5f717-184">Add the following code to the **main** method to:</span></span>
    * <span data-ttu-id="5f717-185">Criar um cliente de dispositivo para se comunicar com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5f717-185">Create a device client to communicate with IoT Hub.</span></span>
    * <span data-ttu-id="5f717-186">Criar um objeto **Dispositivo** para armazenar as propriedades do dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="5f717-186">Create a **Device** object to store the device twin properties.</span></span>

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object to manage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="5f717-187">Para iniciar os serviços de cliente do dispositivo, adicione o seguinte código ao método **main**:</span><span class="sxs-lookup"><span data-stu-id="5f717-187">To start the device client services, add the following code to the **main** method:</span></span>

    ```java
    try {
      // Open the DeviceClient
      // Start the device twin services
      // Subscribe to direct method calls
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

1. <span data-ttu-id="5f717-188">Para aguardar o usuário pressionar a tecla **Enter** antes de desligar, adicione o seguinte código ao final do método **main**:</span><span class="sxs-lookup"><span data-stu-id="5f717-188">To wait for the user to press the **Enter** key before shutting down, add the following code to the end of the **main** method:</span></span>

    ```java
    // Close the app
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="5f717-189">Salve e feche o arquivo `simulated-device\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="5f717-189">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="5f717-190">Compile o aplicativo **simulated-device** e corrija os erros.</span><span class="sxs-lookup"><span data-stu-id="5f717-190">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="5f717-191">No prompt de comando, navegue até a pasta `simulated-device` e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5f717-191">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="5f717-192">Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="5f717-192">Run the apps</span></span>

<span data-ttu-id="5f717-193">Agora você está pronto para executar os aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="5f717-193">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="5f717-194">Em um prompt de comando na pasta `simulated-device`, execute o seguinte comando para iniciar o aplicativo de dispositivo escutando alterações de propriedade desejadas e chamadas de método direto:</span><span class="sxs-lookup"><span data-stu-id="5f717-194">At a command prompt in the `simulated-device` folder, run the following command to start the device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![O cliente do dispositivo é iniciado](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="5f717-196">Em um prompt de comando na pasta `schedule-jobs`, execute o comando a seguir para executar o aplicativo de serviço **schedule-jobs** para executar dois trabalhos.</span><span class="sxs-lookup"><span data-stu-id="5f717-196">At a command prompt in the `schedule-jobs` folder, run the following command to run the **schedule-jobs** service app to run two jobs.</span></span> <span data-ttu-id="5f717-197">O primeiro define os valores de propriedade desejados, o segundo chama o método direto:</span><span class="sxs-lookup"><span data-stu-id="5f717-197">The first sets the desired property values, the second calls the direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![O serviço de aplicativo de Hub IoT Java cria dois trabalhos](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="5f717-199">O aplicativo de dispositivo manipula a alteração da propriedade desejada e a chamada de método direto:</span><span class="sxs-lookup"><span data-stu-id="5f717-199">The device app handles the desired property change and the direct method call:</span></span>

    ![O dispositivo cliente responde às alterações](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="5f717-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5f717-201">Next steps</span></span>

<span data-ttu-id="5f717-202">Neste tutorial, você configurou um novo hub IoT no portal do Azure e depois criou uma identidade do dispositivo no Registro de identidade do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5f717-202">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="5f717-203">Você criou um aplicativo de back-end para executar os dois trabalhos.</span><span class="sxs-lookup"><span data-stu-id="5f717-203">You created a back-end app to run two jobs.</span></span> <span data-ttu-id="5f717-204">O primeiro trabalho definiu valores de propriedade desejados e o segundo trabalho chamou um método direto.</span><span class="sxs-lookup"><span data-stu-id="5f717-204">The first job set desired property values, and the second job called a direct method.</span></span>

<span data-ttu-id="5f717-205">Veja os recursos a seguir para saber como:</span><span class="sxs-lookup"><span data-stu-id="5f717-205">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="5f717-206">Envie telemetria de dispositivos com o tutorial [Introdução ao Hub IoT](iot-hub-java-java-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="5f717-206">Send telemetry from devices with the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="5f717-207">Controle dispositivos interativamente (como ativar uma ventoinha de um aplicativo controlado pelo usuário) com o tutorial [Usar métodos diretos](iot-hub-java-java-direct-methods.md).</span><span class="sxs-lookup"><span data-stu-id="5f717-207">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
