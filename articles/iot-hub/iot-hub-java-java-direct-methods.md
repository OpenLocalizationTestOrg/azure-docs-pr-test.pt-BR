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
# <a name="use-direct-methods-java"></a><span data-ttu-id="41f3b-104">Usar métodos diretos (Java)</span><span class="sxs-lookup"><span data-stu-id="41f3b-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="41f3b-105">Neste tutorial, você cria dois aplicativos de console do Java:</span><span class="sxs-lookup"><span data-stu-id="41f3b-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="41f3b-106">**método Invoke de direct**, um aplicativo de back-end de Java que chama um método no aplicativo do dispositivo simulado hello e exibe a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="41f3b-106">**invoke-direct-method**, a Java back-end app that calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="41f3b-107">**dispositivo simulado**, um aplicativo Java que simula um dispositivo conectado tooyour IoT hub com a identidade do dispositivo Olá você criar.</span><span class="sxs-lookup"><span data-stu-id="41f3b-107">**simulated-device**, a Java app that simulates a device connecting tooyour IoT hub with hello device identity you create.</span></span> <span data-ttu-id="41f3b-108">Este aplicativo responde toohello chamada direta de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="41f3b-108">This app responds toohello direct invoked from hello back end.</span></span>

> [!NOTE]
> <span data-ttu-id="41f3b-109">Para obter informações sobre Olá SDKs que você pode usar toobuild toorun de aplicativos em dispositivos e o back-end de solução, consulte [SDKs do Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="41f3b-109">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="41f3b-110">toocomplete neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="41f3b-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="41f3b-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="41f3b-111">Java SE 8.</span></span> <br/> <span data-ttu-id="41f3b-112">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Java para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="41f3b-112">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="41f3b-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="41f3b-113">Maven 3.</span></span>  <br/> <span data-ttu-id="41f3b-114">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall [Maven] [ lnk-maven] para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="41f3b-114">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="41f3b-115">[Versão do Node.js 0.10.0 ou posterior](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="41f3b-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="41f3b-116">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="41f3b-116">Create a simulated device app</span></span>

<span data-ttu-id="41f3b-117">Nesta seção, você deve criar um aplicativo de console de Java que responde tooa método chamado pela solução de saudação volta final.</span><span class="sxs-lookup"><span data-stu-id="41f3b-117">In this section, you create a Java console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="41f3b-118">Crie uma pasta vazia chamada iot-java-direct-method.</span><span class="sxs-lookup"><span data-stu-id="41f3b-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="41f3b-119">Na pasta de iot java direct-método-Olá, crie um projeto de Maven chamado **dispositivo simulado** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="41f3b-119">In hello iot-java-direct-method folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="41f3b-120">saudação de comando a seguir é um comando longo, único:</span><span class="sxs-lookup"><span data-stu-id="41f3b-120">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="41f3b-121">No prompt de comando, navegue pasta do dispositivo simulado toohello.</span><span class="sxs-lookup"><span data-stu-id="41f3b-121">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="41f3b-122">Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta do dispositivo simulado hello e adicione Olá dependências toohello a seguir **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="41f3b-122">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="41f3b-123">Essa dependência permite que você toouse Olá cliente de dispositivo iot pacote em toocommunicate seu aplicativo com o hub IoT:</span><span class="sxs-lookup"><span data-stu-id="41f3b-123">This dependency enables you toouse hello iot-device-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="41f3b-124">Você pode verificar a versão mais recente de saudação do **cliente de dispositivo iot** usando [pesquisa Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="41f3b-124">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="41f3b-125">Adicione o seguinte Olá **criar** nó após Olá **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="41f3b-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="41f3b-126">Esta configuração instrui Maven toouse Java toobuild 1.8 Olá aplicativo:</span><span class="sxs-lookup"><span data-stu-id="41f3b-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="41f3b-127">Salve e feche o arquivo de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="41f3b-127">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="41f3b-128">Usando um editor de texto, abra o arquivo de simulated-device\src\main\java\com\mycompany\app\App.java de saudação.</span><span class="sxs-lookup"><span data-stu-id="41f3b-128">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="41f3b-129">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="41f3b-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="41f3b-130">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="41f3b-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="41f3b-131">Substituindo `{youriothubname}` com seu nome de hub IoT, e `{yourdevicekey}` com valor de chave de dispositivo do hello gerado na Olá *criar uma identidade de dispositivo* seção:</span><span class="sxs-lookup"><span data-stu-id="41f3b-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="41f3b-132">Este aplicativo de exemplo usa Olá **protocolo** variável quando ele cria uma **DeviceClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="41f3b-132">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="41f3b-133">Atualmente, toouse direta métodos que você deve usar o protocolo de MQTT saudação.</span><span class="sxs-lookup"><span data-stu-id="41f3b-133">Currently, toouse direct methods you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="41f3b-134">tooreturn um hub IoT de tooyour de código de status, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="41f3b-134">tooreturn a status code tooyour IoT hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="41f3b-135">invocações de método direto Olá toohandle de saudação solução back-end, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="41f3b-135">toohandle hello direct method invocations from hello solution back end, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="41f3b-136">toocreate um **DeviceClient** e escutar para invocações de método direto, adicione um **principal** método toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="41f3b-136">toocreate a **DeviceClient** and listen for direct method invocations, add a **main** method toohello **App** class:</span></span>

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

1. <span data-ttu-id="41f3b-137">Salve e feche o arquivo de simulated-device\src\main\java\com\mycompany\app\App.java Olá</span><span class="sxs-lookup"><span data-stu-id="41f3b-137">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="41f3b-138">Criar hello **dispositivo simulado** aplicativo e corrigir os erros.</span><span class="sxs-lookup"><span data-stu-id="41f3b-138">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="41f3b-139">No prompt de comando, navegue pasta do dispositivo simulado toohello e execução hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="41f3b-139">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="41f3b-140">Chama um método direto em um dispositivo</span><span class="sxs-lookup"><span data-stu-id="41f3b-140">Call a direct method on a device</span></span>

<span data-ttu-id="41f3b-141">Nesta seção, você deve criar um aplicativo de console de Java que invoca um método direto e, em seguida, exibe a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="41f3b-141">In this section, you create a Java console app that invokes a direct method and then displays hello response.</span></span> <span data-ttu-id="41f3b-142">Este aplicativo de console se conecta tooyour método direto do IoT Hub tooinvoke hello.</span><span class="sxs-lookup"><span data-stu-id="41f3b-142">This console app connects tooyour IoT Hub tooinvoke hello direct method.</span></span>

1. <span data-ttu-id="41f3b-143">Na pasta de iot java direct-método-Olá, crie um projeto de Maven chamado **invocar direct-método** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="41f3b-143">In hello iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using hello following command at your command prompt.</span></span> <span data-ttu-id="41f3b-144">saudação de comando a seguir é um comando longo, único:</span><span class="sxs-lookup"><span data-stu-id="41f3b-144">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="41f3b-145">No prompt de comando, navegue toohello invoke-direct-método pasta.</span><span class="sxs-lookup"><span data-stu-id="41f3b-145">At your command prompt, navigate toohello invoke-direct-method folder.</span></span>

1. <span data-ttu-id="41f3b-146">Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta de invoke-direct-método hello e adicione Olá toohello de dependência a seguir **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="41f3b-146">Using a text editor, open hello pom.xml file in hello invoke-direct-method folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="41f3b-147">Esta dependência habilita você toouse Olá iot-serviço-pacote do cliente no toocommunicate seu aplicativo com o hub IoT:</span><span class="sxs-lookup"><span data-stu-id="41f3b-147">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="41f3b-148">Você pode verificar a versão mais recente de saudação do **cliente de serviço iot** usando [pesquisa Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="41f3b-148">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="41f3b-149">Adicione o seguinte Olá **criar** nó após Olá **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="41f3b-149">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="41f3b-150">Esta configuração instrui Maven toouse Java toobuild 1.8 Olá aplicativo:</span><span class="sxs-lookup"><span data-stu-id="41f3b-150">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="41f3b-151">Salve e feche o arquivo de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="41f3b-151">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="41f3b-152">Usando um editor de texto, abra o arquivo de invoke-direct-method\src\main\java\com\mycompany\app\App.java de saudação.</span><span class="sxs-lookup"><span data-stu-id="41f3b-152">Using a text editor, open hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="41f3b-153">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="41f3b-153">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="41f3b-154">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="41f3b-154">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="41f3b-155">Substituir `{youriothubconnectionstring}` com a cadeia de conexão de hub IoT anotado na Olá *criar um IoT Hub* seção:</span><span class="sxs-lookup"><span data-stu-id="41f3b-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. <span data-ttu-id="41f3b-156">método de hello tooinvoke no dispositivo simulado de hello, adicionar Olá toohello de código a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="41f3b-156">tooinvoke hello method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="41f3b-157">Salve e feche o arquivo de invoke-direct-method\src\main\java\com\mycompany\app\App.java Olá</span><span class="sxs-lookup"><span data-stu-id="41f3b-157">Save and close hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="41f3b-158">Criar hello **invocar direct-método** aplicativo e corrigir os erros.</span><span class="sxs-lookup"><span data-stu-id="41f3b-158">Build hello **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="41f3b-159">No prompt de comando, navegue toohello invoke-direct-método pasta e execução hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="41f3b-159">At your command prompt, navigate toohello invoke-direct-method folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="41f3b-160">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="41f3b-160">Run hello apps</span></span>

<span data-ttu-id="41f3b-161">Agora você está pronto toorun Olá os aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="41f3b-161">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="41f3b-162">Em um prompt de comando na pasta do dispositivo simulado hello, execute Olá escutando chamadas de método do seu hub IoT de toobegin de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="41f3b-162">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub de Java simulados toolisten do aplicativo de dispositivo para chamadas de método direto][8]

1. <span data-ttu-id="41f3b-164">Em um prompt de comando na pasta de invocar direta método-Olá, execute Olá toocall de comando a seguir um método no seu dispositivo simulado do seu hub IoT:</span><span class="sxs-lookup"><span data-stu-id="41f3b-164">At a command prompt in hello invoke-direct-method folder, run hello following command toocall a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Toocall de aplicativo de serviço do IoT Hub de Java um método direto][7]

1. <span data-ttu-id="41f3b-166">dispositivo simulado Olá responde a chamada de método direto toohello:</span><span class="sxs-lookup"><span data-stu-id="41f3b-166">hello simulated device responds toohello direct method call:</span></span>

    ![Aplicativo de dispositivo simulado Java IoT Hub responde toohello chamada de método direto][9]

## <a name="next-steps"></a><span data-ttu-id="41f3b-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41f3b-168">Next steps</span></span>

<span data-ttu-id="41f3b-169">Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="41f3b-169">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="41f3b-170">Você usou esse dispositivo identidade tooenable Olá simulado dispositivo aplicativo tooreact toomethods invocado pela nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="41f3b-170">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="41f3b-171">Você também criou um aplicativo que chama métodos no dispositivo hello e exibe a resposta de saudação do dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="41f3b-171">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span>

<span data-ttu-id="41f3b-172">tooexplore outros cenários de IoT, consulte [agendar trabalhos em vários dispositivos][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="41f3b-172">tooexplore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="41f3b-173">toolearn como tooextend seu método de solução e agenda IoT chama em vários dispositivos, consulte Olá [agenda e trabalhos de difusão] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="41f3b-173">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
