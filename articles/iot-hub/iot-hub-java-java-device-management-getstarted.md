---
title: "Introdução ao gerenciamento de dispositivo do Hub IoT do Azure (Java) | Microsoft Docs"
description: "Como usar o gerenciamento de dispositivos do Hub IoT do Azure para iniciar uma reinicialização do dispositivo remoto. Use o SDK do dispositivo IoT do Azure para Java para implementar um aplicativo de dispositivo simulado que inclui um método direto e o SDK do serviço do Azure IoT para Java para implementar um aplicativo de serviço que invoca o método direto."
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
ms.openlocfilehash: c75635f366f5ced4bf91792d1a905dd6aab8ed79
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="44400-104">Introdução ao gerenciamento de dispositivos (Java)</span><span class="sxs-lookup"><span data-stu-id="44400-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="44400-105">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="44400-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="44400-106">Usar o portal do Azure para criar um Hub IoT e criar uma identidade de dispositivo em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="44400-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="44400-107">Crie um aplicativo de dispositivo simulado que implementa um método direto para reiniciar o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="44400-107">Create a simulated device app that implements a direct method to reboot the device.</span></span> <span data-ttu-id="44400-108">Métodos diretos são invocados da nuvem.</span><span class="sxs-lookup"><span data-stu-id="44400-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="44400-109">Crie um aplicativo que chama o método de reinicialização direta no aplicativo de dispositivo simulado por meio do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="44400-109">Create an app that invokes the reboot direct method in the simulated device app through your IoT hub.</span></span> <span data-ttu-id="44400-110">Esse aplicativo monitora as propriedades relatadas do dispositivo para ver quando a operação de reinicialização é concluída.</span><span class="sxs-lookup"><span data-stu-id="44400-110">This app then monitors the reported properties from the device to see when the reboot operation is complete.</span></span>

<span data-ttu-id="44400-111">Ao fim deste tutorial, você tem dois aplicativos de console do Java:</span><span class="sxs-lookup"><span data-stu-id="44400-111">At the end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="44400-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="44400-112">**simulated-device**.</span></span> <span data-ttu-id="44400-113">Este aplicativo:</span><span class="sxs-lookup"><span data-stu-id="44400-113">This app:</span></span>

* <span data-ttu-id="44400-114">Conecta-se ao hub IoT com a identidade de dispositivo criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="44400-114">Connects to your IoT hub with the device identity created earlier.</span></span>
* <span data-ttu-id="44400-115">Recebe uma chamada de método direto de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="44400-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="44400-116">Simula uma reinicialização física.</span><span class="sxs-lookup"><span data-stu-id="44400-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="44400-117">Relata a hora da última reinicialização por meio de uma propriedade relatada.</span><span class="sxs-lookup"><span data-stu-id="44400-117">Reports the time of the last reboot through a reported property.</span></span>

<span data-ttu-id="44400-118">**disparar reinicialização**.</span><span class="sxs-lookup"><span data-stu-id="44400-118">**trigger-reboot**.</span></span> <span data-ttu-id="44400-119">Este aplicativo:</span><span class="sxs-lookup"><span data-stu-id="44400-119">This app:</span></span>

* <span data-ttu-id="44400-120">Chama um método direto no aplicativo de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="44400-120">Calls a direct method in the simulated device app.</span></span>
* <span data-ttu-id="44400-121">Exibe a resposta à chamada de método direto enviada pelo dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="44400-121">Displays the response to the direct method call sent by the simulated device</span></span>
* <span data-ttu-id="44400-122">Exibe as propriedades relatadas atualizadas.</span><span class="sxs-lookup"><span data-stu-id="44400-122">Displays the updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="44400-123">Para saber mais sobre os SDKs que você pode usar para compilar aplicativos executados em dispositivos e no back-end da solução, veja [SDKs de IoT do Azure][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="44400-123">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="44400-124">Para concluir este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="44400-124">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="44400-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="44400-125">Java SE 8.</span></span> <br/> <span data-ttu-id="44400-126">[Preparar o ambiente de desenvolvimento][lnk-dev-setup] descreve como instalar o Java para este tutorial no Windows ou no Linux.</span><span class="sxs-lookup"><span data-stu-id="44400-126">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="44400-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="44400-127">Maven 3.</span></span>  <br/> <span data-ttu-id="44400-128">[Preparar o ambiente de desenvolvimento][lnk-dev-setup] descreve como instalar o [Maven][lnk-maven] para este tutorial no Windows ou no Linux.</span><span class="sxs-lookup"><span data-stu-id="44400-128">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="44400-129">[Versão do Node.js 0.10.0 ou posterior](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="44400-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="44400-130">Disparar uma reinicialização remota no dispositivo usando um método direto</span><span class="sxs-lookup"><span data-stu-id="44400-130">Trigger a remote reboot on the device using a direct method</span></span>

<span data-ttu-id="44400-131">Nesta seção, você cria um aplicativo de console Java que:</span><span class="sxs-lookup"><span data-stu-id="44400-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="44400-132">Invoca um método direto de reinicialização no aplicativo de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="44400-132">Invokes the reboot direct method in the simulated device app.</span></span>
1. <span data-ttu-id="44400-133">Exibe a resposta.</span><span class="sxs-lookup"><span data-stu-id="44400-133">Displays the response.</span></span>
1. <span data-ttu-id="44400-134">Sonda as propriedades relatadas enviadas do dispositivo para determinar quando a reinicialização está concluída.</span><span class="sxs-lookup"><span data-stu-id="44400-134">Polls the reported properties sent from the device to determine when the reboot is complete.</span></span>

<span data-ttu-id="44400-135">Esse aplicativo de console se conecta ao Hub IoT para invocar o método direto e ler as propriedades relatadas.</span><span class="sxs-lookup"><span data-stu-id="44400-135">This console app connects to your IoT Hub to invoke the direct method and read the reported properties.</span></span>

1. <span data-ttu-id="44400-136">Crie uma pasta vazia chamada dm-get-started.</span><span class="sxs-lookup"><span data-stu-id="44400-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="44400-137">Na pasta dm-get-started, crie um projeto Maven chamado **trigger-reboot** usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="44400-137">In the dm-get-started folder, create a Maven project called **trigger-reboot** using the following command at your command prompt.</span></span> <span data-ttu-id="44400-138">Veja a seguir um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="44400-138">The following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="44400-139">No prompt de comando, navegue até a pasta trigger-reboot.</span><span class="sxs-lookup"><span data-stu-id="44400-139">At your command prompt, navigate to the trigger-reboot folder.</span></span>

1. <span data-ttu-id="44400-140">Usando um editor de texto, abra o arquivo pom.xml na pasta trigger-reboot e adicione a dependência a seguir ao nó **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="44400-140">Using a text editor, open the pom.xml file in the trigger-reboot folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="44400-141">Essa dependência permite que você use o pacote iot-service-client em seu aplicativo para se comunicar com seu hub IoT:</span><span class="sxs-lookup"><span data-stu-id="44400-141">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="44400-142">Você pode verificar a versão mais recente do **iot-service-client** usando a [pesquisa Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="44400-142">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="44400-143">Adicione o seguinte nó **buid** após o nó **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="44400-143">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="44400-144">Esta configuração instrui o Maven a usar Java 1.8 para compilar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="44400-144">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="44400-145">Salve e feche o arquivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="44400-145">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="44400-146">Usando um editor de texto, abra o arquivo de origem trigger-reboot\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="44400-146">Using a text editor, open the trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="44400-147">Adicione as seguintes instruções **import** ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="44400-147">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="44400-148">Adicione as seguintes variáveis no nível da classe à classe **App** .</span><span class="sxs-lookup"><span data-stu-id="44400-148">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="44400-149">Substitua `{youriothubconnectionstring}` pela cadeia de conexão do hub IoT anotada na seção *Criar um Hub IoT*:</span><span class="sxs-lookup"><span data-stu-id="44400-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="44400-150">Para implementar um thread que lê as propriedades relatadas do dispositivo gêmeo a cada 10 segundos, adicione a seguinte classe aninhada à classe de **Aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="44400-150">To implement a thread that reads the reported properties from the device twin every 10 seconds, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="44400-151">Para invocar o método direto de reinicialização do dispositivo simulado, adicione o seguinte código ao método **principal**:</span><span class="sxs-lookup"><span data-stu-id="44400-151">To invoke the reboot direct method on the simulated device, add the following code to the **main** method:</span></span>

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

1. <span data-ttu-id="44400-152">Para iniciar o thread para sondar as propriedades relatadas do dispositivo simulado, adicione o seguinte código ao método **principal**:</span><span class="sxs-lookup"><span data-stu-id="44400-152">To start the thread to poll the reported properties from the simulated device, add the following code to the **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="44400-153">Para que você possa interromper o aplicativo, adicione o seguinte código ao método **principal**:</span><span class="sxs-lookup"><span data-stu-id="44400-153">To enable you to stop the app, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press ENTER to exit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="44400-154">Salve e feche o arquivo trigger-reboot\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="44400-154">Save and close the trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="44400-155">Criar o aplicativo de back-end **trigger-reboot** e corrigir os erros.</span><span class="sxs-lookup"><span data-stu-id="44400-155">Build the **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="44400-156">No prompt de comando, navegue até a pasta trigger-reboot e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="44400-156">At your command prompt, navigate to the trigger-reboot folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="44400-157">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="44400-157">Create a simulated device app</span></span>

<span data-ttu-id="44400-158">Nesta seção, você cria um aplicativo de console Java que simula um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="44400-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="44400-159">O aplicativo escuta a chamada de método direto de reinicialização do hub IoT e responde imediatamente à chamada.</span><span class="sxs-lookup"><span data-stu-id="44400-159">The app listens for the reboot direct method call from your IoT hub and immediately responds to that call.</span></span> <span data-ttu-id="44400-160">Em seguida, o aplicativo é suspenso durante algum tempo para simular o processo de reinicialização antes de usar uma propriedade relatada para notificar o aplicativo de back-end **trigger-reboot** de que a reinicialização foi concluída.</span><span class="sxs-lookup"><span data-stu-id="44400-160">The app then sleeps for a while to simulate the reboot process before it uses a reported property to notify the **trigger-reboot** back-end app that the reboot is complete.</span></span>

1. <span data-ttu-id="44400-161">Na pasta dm-get-started, crie um projeto Maven denominado **simulated-device** usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="44400-161">In the dm-get-started folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="44400-162">Veja a seguir um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="44400-162">The following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="44400-163">No prompt de comando, navegue até a pasta simulated-device.</span><span class="sxs-lookup"><span data-stu-id="44400-163">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="44400-164">Usando um editor de texto, abra o arquivo pom.xml na pasta simulated-device e adicione a dependência a seguir ao nó **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="44400-164">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="44400-165">Essa dependência permite que você use o pacote iot-service-client em seu aplicativo para se comunicar com seu hub IoT:</span><span class="sxs-lookup"><span data-stu-id="44400-165">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="44400-166">Você pode verificar a versão mais recente do **iot-device-client** usando a [pesquisa Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="44400-166">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="44400-167">Adicione o seguinte nó **buid** após o nó **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="44400-167">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="44400-168">Esta configuração instrui o Maven a usar Java 1.8 para compilar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="44400-168">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="44400-169">Salve e feche o arquivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="44400-169">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="44400-170">Usando um editor de texto, abra o arquivo de origem simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="44400-170">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="44400-171">Adicione as seguintes instruções **import** ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="44400-171">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="44400-172">Adicione as seguintes variáveis no nível da classe à classe **App** .</span><span class="sxs-lookup"><span data-stu-id="44400-172">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="44400-173">Substitua `{yourdeviceconnectionstring}` pela cadeia de conexão de dispositivo anotada na seção *Criar uma identidade de dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="44400-173">Replace `{yourdeviceconnectionstring}` with the device connection string you noted in the *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="44400-174">Para implementar um manipulador de retorno de chamada para eventos de status do método direto, adicione a seguinte classe aninhada à classe de **Aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="44400-174">To implement a callback handler for direct method status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="44400-175">Para implementar um manipulador de retorno de chamada para eventos de status de dispositivo gêmeo, adicione a seguinte classe aninhada à classe de **Aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="44400-175">To implement a callback handler for device twin status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded to device twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="44400-176">Para implementar um manipulador de retorno de chamada para eventos de propriedade, adicione a seguinte classe aninhada à classe de **Aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="44400-176">To implement a callback handler for property events, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="44400-177">Para implementar um thread para simular a reinicialização do dispositivo, adicione a seguinte classe aninhada à classe de **Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="44400-177">To implement a thread to simulate the device reboot, add the following nested class to the **App** class.</span></span> <span data-ttu-id="44400-178">O thread é suspenso por cinco segundos e define a propriedade relatada **lastReboot**:</span><span class="sxs-lookup"><span data-stu-id="44400-178">The thread sleeps for five seconds and then sets the **lastReboot** reported property:</span></span>

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

1. <span data-ttu-id="44400-179">Para implementar o método direto no dispositivo, adicione a seguinte classe aninhada à classe de **Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="44400-179">To implement the direct method on the device, add the following nested class to the **App** class.</span></span> <span data-ttu-id="44400-180">Quando o aplicativo simulado recebe uma chamada para o método direto **reinicializar**, ele retorna uma confirmação para o chamador e inicia um thread para processar a reinicialização:</span><span class="sxs-lookup"><span data-stu-id="44400-180">When the simulated app receives a call to the **reboot** direct method, it returns an acknowledgement to the caller and then starts a thread to process the reboot:</span></span>

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

1. <span data-ttu-id="44400-181">Modifique a assinatura do método **principal** para lançar as seguintes exceções:</span><span class="sxs-lookup"><span data-stu-id="44400-181">Modify the signature of the **main** method to throw the following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="44400-182">Para instanciar um **DeviceClient**, adicione o seguinte código ao método **principal**:</span><span class="sxs-lookup"><span data-stu-id="44400-182">To instantiate a **DeviceClient**, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="44400-183">Para começar a escutar chamadas de método diretas, adicione o seguinte código ao método **principal**:</span><span class="sxs-lookup"><span data-stu-id="44400-183">To start listening for direct method calls, add the following code to the **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed to direct methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="44400-184">Para desligar o simulador de dispositivo, adicione o seguinte código ao método **principal**:</span><span class="sxs-lookup"><span data-stu-id="44400-184">To shut down the device simulator, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="44400-185">Salve e feche o arquivo simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="44400-185">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="44400-186">Crie o aplicativo de back-end **simulated-device** e corrija os erros.</span><span class="sxs-lookup"><span data-stu-id="44400-186">Build the **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="44400-187">No prompt de comando, navegue até a pasta simulated-device e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="44400-187">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="44400-188">Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="44400-188">Run the apps</span></span>

<span data-ttu-id="44400-189">Agora você está pronto para executar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="44400-189">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="44400-190">Em um prompt de comando, na pasta simulated-device, execute o seguinte comando para começar a escutar chamadas de método de reinicialização de seu Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="44400-190">At a command prompt in the simulated-device folder, run the following command to begin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Aplicativo de dispositivo simulado de Java do Hub IoT para escutar chamadas de método direto de reinicialização][1]

1. <span data-ttu-id="44400-192">Em um prompt de comando na pasta trigger-reboot, execute o seguinte comando para chamar o método de reinicialização no dispositivo simulado do Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="44400-192">At a command prompt in the trigger-reboot folder, run the following command to call the reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Serviço de aplicativo Java do Hub IoT para chamar o método de reinicialização direta][2]

1. <span data-ttu-id="44400-194">O dispositivo simulado responde à chamada de método direto de reinicialização:</span><span class="sxs-lookup"><span data-stu-id="44400-194">The simulated device responds to the reboot direct method call:</span></span>

    ![O aplicativo de dispositivo simulado Java do Hub IoT responde à chamada de método direto][3]

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