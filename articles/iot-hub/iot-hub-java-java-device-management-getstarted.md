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
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="6dccf-104">Introdução ao gerenciamento de dispositivos (Java)</span><span class="sxs-lookup"><span data-stu-id="6dccf-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="6dccf-105">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="6dccf-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="6dccf-106">Use Olá toocreate portal do Azure um IoT Hub e criar uma identidade de dispositivo em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6dccf-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="6dccf-107">Crie um aplicativo de dispositivo simulado que implementa um dispositivo de saudação tooreboot método direto.</span><span class="sxs-lookup"><span data-stu-id="6dccf-107">Create a simulated device app that implements a direct method tooreboot hello device.</span></span> <span data-ttu-id="6dccf-108">Métodos diretos são chamados de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="6dccf-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="6dccf-109">Crie um aplicativo que invoca o método direto de reinicialização de saudação no aplicativo do dispositivo simulado Olá por meio de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6dccf-109">Create an app that invokes hello reboot direct method in hello simulated device app through your IoT hub.</span></span> <span data-ttu-id="6dccf-110">Este aplicativo e monitores Olá relatadas propriedades de saudação dispositivo toosee quando Olá operação de reinicialização é concluída.</span><span class="sxs-lookup"><span data-stu-id="6dccf-110">This app then monitors hello reported properties from hello device toosee when hello reboot operation is complete.</span></span>

<span data-ttu-id="6dccf-111">No final da saudação deste tutorial, você tem dois aplicativos de console de Java:</span><span class="sxs-lookup"><span data-stu-id="6dccf-111">At hello end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="6dccf-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="6dccf-112">**simulated-device**.</span></span> <span data-ttu-id="6dccf-113">Este aplicativo:</span><span class="sxs-lookup"><span data-stu-id="6dccf-113">This app:</span></span>

* <span data-ttu-id="6dccf-114">Conecta-se tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6dccf-114">Connects tooyour IoT hub with hello device identity created earlier.</span></span>
* <span data-ttu-id="6dccf-115">Recebe uma chamada de método direto de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="6dccf-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="6dccf-116">Simula uma reinicialização física.</span><span class="sxs-lookup"><span data-stu-id="6dccf-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="6dccf-117">Relatórios Olá hora da última reinicialização Olá através de uma propriedade relatada.</span><span class="sxs-lookup"><span data-stu-id="6dccf-117">Reports hello time of hello last reboot through a reported property.</span></span>

<span data-ttu-id="6dccf-118">**disparar reinicialização**.</span><span class="sxs-lookup"><span data-stu-id="6dccf-118">**trigger-reboot**.</span></span> <span data-ttu-id="6dccf-119">Este aplicativo:</span><span class="sxs-lookup"><span data-stu-id="6dccf-119">This app:</span></span>

* <span data-ttu-id="6dccf-120">Chama um método direto no aplicativo do dispositivo simulado hello.</span><span class="sxs-lookup"><span data-stu-id="6dccf-120">Calls a direct method in hello simulated device app.</span></span>
* <span data-ttu-id="6dccf-121">Exibe a chamada do método direto Olá resposta toohello enviada pelo dispositivo simulado Olá</span><span class="sxs-lookup"><span data-stu-id="6dccf-121">Displays hello response toohello direct method call sent by hello simulated device</span></span>
* <span data-ttu-id="6dccf-122">Olá exibe atualizado relatado propriedades.</span><span class="sxs-lookup"><span data-stu-id="6dccf-122">Displays hello updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="6dccf-123">Para obter informações sobre Olá SDKs que você pode usar toobuild toorun de aplicativos em dispositivos e o back-end de solução, consulte [SDKs do Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="6dccf-123">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="6dccf-124">toocomplete neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="6dccf-124">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="6dccf-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="6dccf-125">Java SE 8.</span></span> <br/> <span data-ttu-id="6dccf-126">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Java para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="6dccf-126">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="6dccf-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="6dccf-127">Maven 3.</span></span>  <br/> <span data-ttu-id="6dccf-128">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall [Maven] [ lnk-maven] para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="6dccf-128">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="6dccf-129">[Versão do Node.js 0.10.0 ou posterior](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="6dccf-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="6dccf-130">Disparar uma reinicialização remota no dispositivo hello usando um método direto</span><span class="sxs-lookup"><span data-stu-id="6dccf-130">Trigger a remote reboot on hello device using a direct method</span></span>

<span data-ttu-id="6dccf-131">Nesta seção, você cria um aplicativo de console Java que:</span><span class="sxs-lookup"><span data-stu-id="6dccf-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="6dccf-132">Invoca o método direto de reinicialização de saudação no aplicativo do dispositivo simulado Olá.</span><span class="sxs-lookup"><span data-stu-id="6dccf-132">Invokes hello reboot direct method in hello simulated device app.</span></span>
1. <span data-ttu-id="6dccf-133">Exibe a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="6dccf-133">Displays hello response.</span></span>
1. <span data-ttu-id="6dccf-134">Olá sondagens relatado propriedades enviadas do hello dispositivo toodetermine quando Olá reinicialização seja concluída.</span><span class="sxs-lookup"><span data-stu-id="6dccf-134">Polls hello reported properties sent from hello device toodetermine when hello reboot is complete.</span></span>

<span data-ttu-id="6dccf-135">Este aplicativo de console se conecta tooyour IoT Hub método direto do tooinvoke hello e hello leitura relatadas propriedades.</span><span class="sxs-lookup"><span data-stu-id="6dccf-135">This console app connects tooyour IoT Hub tooinvoke hello direct method and read hello reported properties.</span></span>

1. <span data-ttu-id="6dccf-136">Crie uma pasta vazia chamada dm-get-started.</span><span class="sxs-lookup"><span data-stu-id="6dccf-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="6dccf-137">Na pasta dm get iniciado hello, crie um projeto de Maven chamado **gatilho reinicialização** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="6dccf-137">In hello dm-get-started folder, create a Maven project called **trigger-reboot** using hello following command at your command prompt.</span></span> <span data-ttu-id="6dccf-138">a seguir Olá mostra um comando longo, único:</span><span class="sxs-lookup"><span data-stu-id="6dccf-138">hello following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="6dccf-139">No prompt de comando, navegue toohello gatilho reinicialização pasta.</span><span class="sxs-lookup"><span data-stu-id="6dccf-139">At your command prompt, navigate toohello trigger-reboot folder.</span></span>

1. <span data-ttu-id="6dccf-140">Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta de reinicialização de gatilho hello e adicione Olá toohello de dependência a seguir **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="6dccf-140">Using a text editor, open hello pom.xml file in hello trigger-reboot folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="6dccf-141">Esta dependência habilita você toouse Olá iot-serviço-pacote do cliente no toocommunicate seu aplicativo com o hub IoT:</span><span class="sxs-lookup"><span data-stu-id="6dccf-141">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="6dccf-142">Você pode verificar a versão mais recente de saudação do **cliente de serviço iot** usando [pesquisa Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="6dccf-142">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="6dccf-143">Adicione o seguinte Olá **criar** nó após Olá **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="6dccf-143">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="6dccf-144">Esta configuração instrui Maven toouse Java toobuild 1.8 Olá aplicativo:</span><span class="sxs-lookup"><span data-stu-id="6dccf-144">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="6dccf-145">Salve e feche o arquivo de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="6dccf-145">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="6dccf-146">Usando um editor de texto, abra o arquivo de origem trigger-reboot\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="6dccf-146">Using a text editor, open hello trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="6dccf-147">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="6dccf-147">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="6dccf-148">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="6dccf-148">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="6dccf-149">Substituir `{youriothubconnectionstring}` com a cadeia de conexão de hub IoT anotado na Olá *criar um IoT Hub* seção:</span><span class="sxs-lookup"><span data-stu-id="6dccf-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="6dccf-150">tooimplement um thread que lê Olá relatado propriedades de duas de dispositivo de saudação a cada 10 segundos, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="6dccf-150">tooimplement a thread that reads hello reported properties from hello device twin every 10 seconds, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="6dccf-151">método direto do tooinvoke hello reinicialização no dispositivo simulado de hello, adicionar Olá toohello de código a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="6dccf-151">tooinvoke hello reboot direct method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="6dccf-152">toostart Olá thread toopoll Olá relatadas propriedades do dispositivo simulado hello, adicione Olá toohello de código a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="6dccf-152">toostart hello thread toopoll hello reported properties from hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="6dccf-153">tooenable toostop Olá aplicativo, adicione Olá toohello de código a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="6dccf-153">tooenable you toostop hello app, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="6dccf-154">Salve e feche o arquivo de trigger-reboot\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="6dccf-154">Save and close hello trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="6dccf-155">Criar hello **gatilho reinicialização** aplicativos de back-end e corrigir os erros.</span><span class="sxs-lookup"><span data-stu-id="6dccf-155">Build hello **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="6dccf-156">No prompt de comando, navegue toohello gatilho reinicialização pasta e execução hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6dccf-156">At your command prompt, navigate toohello trigger-reboot folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="6dccf-157">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="6dccf-157">Create a simulated device app</span></span>

<span data-ttu-id="6dccf-158">Nesta seção, você cria um aplicativo de console Java que simula um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6dccf-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="6dccf-159">aplicativo Hello escuta para chamada de método direto de reinicialização de saudação do seu hub IoT e responde imediatamente a chamada toothat.</span><span class="sxs-lookup"><span data-stu-id="6dccf-159">hello app listens for hello reboot direct method call from your IoT hub and immediately responds toothat call.</span></span> <span data-ttu-id="6dccf-160">Olá aplicativo então dormem durante um processo de reinicialização de saudação toosimulate antes de usar uma saudação de toonotify propriedade relatado **gatilho reinicialização** aplicativo de back-end que Olá reinicialização for concluído.</span><span class="sxs-lookup"><span data-stu-id="6dccf-160">hello app then sleeps for a while toosimulate hello reboot process before it uses a reported property toonotify hello **trigger-reboot** back-end app that hello reboot is complete.</span></span>

1. <span data-ttu-id="6dccf-161">Na pasta dm get iniciado hello, crie um projeto de Maven chamado **dispositivo simulado** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="6dccf-161">In hello dm-get-started folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="6dccf-162">a seguir Olá é um comando longo, único:</span><span class="sxs-lookup"><span data-stu-id="6dccf-162">hello following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="6dccf-163">No prompt de comando, navegue pasta do dispositivo simulado toohello.</span><span class="sxs-lookup"><span data-stu-id="6dccf-163">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="6dccf-164">Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta do dispositivo simulado hello e adicione Olá toohello de dependência a seguir **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="6dccf-164">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="6dccf-165">Esta dependência habilita você toouse Olá iot-serviço-pacote do cliente no toocommunicate seu aplicativo com o hub IoT:</span><span class="sxs-lookup"><span data-stu-id="6dccf-165">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="6dccf-166">Você pode verificar a versão mais recente de saudação do **cliente de dispositivo iot** usando [pesquisa Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="6dccf-166">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="6dccf-167">Adicione o seguinte Olá **criar** nó após Olá **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="6dccf-167">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="6dccf-168">Esta configuração instrui Maven toouse Java toobuild 1.8 Olá aplicativo:</span><span class="sxs-lookup"><span data-stu-id="6dccf-168">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="6dccf-169">Salve e feche o arquivo de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="6dccf-169">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="6dccf-170">Usando um editor de texto, abra o arquivo de origem simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="6dccf-170">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="6dccf-171">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="6dccf-171">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="6dccf-172">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="6dccf-172">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="6dccf-173">Substituir `{yourdeviceconnectionstring}` com a cadeia de conexão de dispositivo Olá observado em hello *criar uma identidade de dispositivo* seção:</span><span class="sxs-lookup"><span data-stu-id="6dccf-173">Replace `{yourdeviceconnectionstring}` with hello device connection string you noted in hello *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="6dccf-174">tooimplement um manipulador de retorno de chamada para eventos de status de método direto, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="6dccf-174">tooimplement a callback handler for direct method status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="6dccf-175">tooimplement um manipulador de retorno de chamada para eventos de status do dispositivo duas, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="6dccf-175">tooimplement a callback handler for device twin status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="6dccf-176">tooimplement um manipulador de retorno de chamada para eventos de propriedade, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="6dccf-176">tooimplement a callback handler for property events, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="6dccf-177">tooimplement uma reinicialização do dispositivo thread toosimulate hello, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="6dccf-177">tooimplement a thread toosimulate hello device reboot, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="6dccf-178">thread de saudação ficará suspenso por cinco segundos e, em seguida, define Olá **lastReboot** relatado propriedade:</span><span class="sxs-lookup"><span data-stu-id="6dccf-178">hello thread sleeps for five seconds and then sets hello **lastReboot** reported property:</span></span>

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

1. <span data-ttu-id="6dccf-179">método direto do hello tooimplement no dispositivo Olá, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="6dccf-179">tooimplement hello direct method on hello device, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="6dccf-180">Quando o aplicativo simulado Olá recebe uma chamada toohello **reinicializar** método direto, ele retorna um chamador de toohello de confirmação e, em seguida, inicia uma saudação do thread tooprocess reinicializar:</span><span class="sxs-lookup"><span data-stu-id="6dccf-180">When hello simulated app receives a call toohello **reboot** direct method, it returns an acknowledgement toohello caller and then starts a thread tooprocess hello reboot:</span></span>

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

1. <span data-ttu-id="6dccf-181">Modificar assinatura Olá Olá **principal** saudação do método toothrow exceções a seguir:</span><span class="sxs-lookup"><span data-stu-id="6dccf-181">Modify hello signature of hello **main** method toothrow hello following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="6dccf-182">tooinstantiate um **DeviceClient**, adicionar Olá toohello de código a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="6dccf-182">tooinstantiate a **DeviceClient**, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="6dccf-183">toostart escuta para chamadas de método direto, adicionar Olá toohello de código a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="6dccf-183">toostart listening for direct method calls, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="6dccf-184">tooshut para baixo o simulador do dispositivo hello, adicionar Olá toohello de código a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="6dccf-184">tooshut down hello device simulator, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="6dccf-185">Salve e feche o arquivo de simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="6dccf-185">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="6dccf-186">Criar hello **dispositivo simulado** aplicativo de back-end e corrigir os erros.</span><span class="sxs-lookup"><span data-stu-id="6dccf-186">Build hello **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="6dccf-187">No prompt de comando, navegue pasta do dispositivo simulado toohello e execução hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6dccf-187">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="6dccf-188">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="6dccf-188">Run hello apps</span></span>

<span data-ttu-id="6dccf-189">Agora você está pronto toorun Olá aplicativos.</span><span class="sxs-lookup"><span data-stu-id="6dccf-189">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="6dccf-190">Em um prompt de comando na pasta do dispositivo simulado hello, execute Olá aguardando chamadas de método de reinicialização do seu hub IoT de toobegin de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6dccf-190">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub de Java simulados toolisten do aplicativo de dispositivo para chamadas de método direto de reinicialização][1]

1. <span data-ttu-id="6dccf-192">No prompt de comando na pasta de reinicialização de gatilho hello, execute Olá a seguir do método de reinicialização do comando toocall hello em seu dispositivo simulado de seu hub IoT:</span><span class="sxs-lookup"><span data-stu-id="6dccf-192">At a command prompt in hello trigger-reboot folder, run hello following command toocall hello reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Saudação de toocall de aplicativo de serviço de IoT Hub de Java reinicializar método direto][2]

1. <span data-ttu-id="6dccf-194">dispositivo simulado Olá responde toohello chamada de método direto de reinicialização:</span><span class="sxs-lookup"><span data-stu-id="6dccf-194">hello simulated device responds toohello reboot direct method call:</span></span>

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