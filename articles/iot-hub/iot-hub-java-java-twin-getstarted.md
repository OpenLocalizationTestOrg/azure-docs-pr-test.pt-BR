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
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="86e63-104">Introdução ao dispositivos gêmeos (Java)</span><span class="sxs-lookup"><span data-stu-id="86e63-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="86e63-105">Neste tutorial, você cria dois aplicativos de console do Java:</span><span class="sxs-lookup"><span data-stu-id="86e63-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="86e63-106">**add-tags-query**, um aplicativo de back-end Java que adiciona dispositivos gêmeos de marcas e consultas.</span><span class="sxs-lookup"><span data-stu-id="86e63-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="86e63-107">**dispositivo simulado**, um aplicativo de dispositivo de Java que que conecta tooyour IoT hub e relatórios sua condição de conectividade usando uma propriedade relatada.</span><span class="sxs-lookup"><span data-stu-id="86e63-107">**simulated-device**, a Java device app that that connects tooyour IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="86e63-108">artigo Olá [SDKs do Azure IoT](iot-hub-devguide-sdks.md) fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.</span><span class="sxs-lookup"><span data-stu-id="86e63-108">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

<span data-ttu-id="86e63-109">toocomplete neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="86e63-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="86e63-110">Olá mais recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="86e63-110">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="86e63-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="86e63-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="86e63-112">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="86e63-112">An active Azure account.</span></span> <span data-ttu-id="86e63-113">(Se você não tiver uma conta, poderá criar uma [conta gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="86e63-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="86e63-114">Se você preferir a identidade do dispositivo Olá toocreate programaticamente, ler a seção correspondente Olá Olá [conectar seu hub IoT de tooyour de dispositivo usando o Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artigo.</span><span class="sxs-lookup"><span data-stu-id="86e63-114">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="86e63-115">Criar aplicativo de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="86e63-115">Create hello service app</span></span>

<span data-ttu-id="86e63-116">Nesta seção, você cria um aplicativo Java que adiciona metadados local como duas de dispositivo de toohello uma marca no IoT Hub associada **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="86e63-116">In this section, you create a Java app that adds location metadata as a tag toohello device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="86e63-117">primeiro, o aplicativo Hello consulta hub IoT para dispositivos localizados em Olá dos EUA e, em seguida, para dispositivos que se reportam a uma conexão de rede de celular.</span><span class="sxs-lookup"><span data-stu-id="86e63-117">hello app first queries IoT hub for devices located in hello US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="86e63-118">No computador de desenvolvimento, crie uma pasta vazia chamada `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="86e63-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="86e63-119">Em Olá `iot-java-twin-getstarted` pasta, crie um projeto Maven chamado **adicionar marcas-consulta** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="86e63-119">In hello `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using hello following command at your command prompt.</span></span> <span data-ttu-id="86e63-120">Observe que este é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="86e63-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="86e63-121">No prompt de comando, navegue toohello `add-tags-query` pasta.</span><span class="sxs-lookup"><span data-stu-id="86e63-121">At your command prompt, navigate toohello `add-tags-query` folder.</span></span>

1. <span data-ttu-id="86e63-122">Usando um editor de texto, abra Olá `pom.xml` arquivo hello `add-tags-query` pasta e adicione Olá seguir dependência toohello **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="86e63-122">Using a text editor, open hello `pom.xml` file in hello `add-tags-query` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="86e63-123">Esta dependência habilita Olá toouse **cliente de serviço iot** pacote no toocommunicate seu aplicativo com o hub IoT:</span><span class="sxs-lookup"><span data-stu-id="86e63-123">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="86e63-124">Você pode verificar a versão mais recente de saudação do **cliente de serviço iot** usando [pesquisa Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="86e63-124">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="86e63-125">Adicione o seguinte Olá **criar** nó após Olá **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="86e63-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="86e63-126">Esta configuração instrui Maven toouse Java toobuild 1.8 Olá aplicativo:</span><span class="sxs-lookup"><span data-stu-id="86e63-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="86e63-127">Salve e feche o hello `pom.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="86e63-127">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="86e63-128">Usando um editor de texto, abra Olá `add-tags-query\src\main\java\com\mycompany\app\App.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="86e63-128">Using a text editor, open hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="86e63-129">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="86e63-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="86e63-130">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="86e63-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="86e63-131">Substituir `{youriothubconnectionstring}` com a cadeia de conexão de hub IoT anotado na Olá *criar um IoT Hub* seção:</span><span class="sxs-lookup"><span data-stu-id="86e63-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="86e63-132">Saudação de atualização **principal** seguinte de saudação do método assinatura tooinclude `throws` cláusula:</span><span class="sxs-lookup"><span data-stu-id="86e63-132">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="86e63-133">Adicionar Olá toohello de código a seguir **principal** saudação do método toocreate **DeviceTwin** e **DeviceTwinDevice** objetos.</span><span class="sxs-lookup"><span data-stu-id="86e63-133">Add hello following code toohello **main** method toocreate hello **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="86e63-134">Olá **DeviceTwin** a comunicação com o hub IoT Olá alças do objeto.</span><span class="sxs-lookup"><span data-stu-id="86e63-134">hello **DeviceTwin** object handles hello communication with your IoT hub.</span></span> <span data-ttu-id="86e63-135">Olá **DeviceTwinDevice** objeto representa duas de dispositivo Olá com suas propriedades e marcas:</span><span class="sxs-lookup"><span data-stu-id="86e63-135">hello **DeviceTwinDevice** object represents hello device twin with its properties and tags:</span></span>

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="86e63-136">Adicione o seguinte Olá `try/catch` bloquear toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="86e63-136">Add hello following `try/catch` block toohello **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="86e63-137">Olá tooupdate **região** e **planta** marcas de duas do dispositivo em duas seu dispositivo, adicione Olá Olá código a seguir `try` bloco:</span><span class="sxs-lookup"><span data-stu-id="86e63-137">tooupdate hello **region** and **plant** device twin tags in your device twin, add hello following code in hello `try` block:</span></span>

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

1. <span data-ttu-id="86e63-138">twins de dispositivo tooquery Olá no hub IoT, adicionar Olá toohello de código a seguir `try` bloco após código Olá adicionado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="86e63-138">tooquery hello device twins in IoT hub, add hello following code toohello `try` block after hello code you added in hello previous step.</span></span> <span data-ttu-id="86e63-139">código de saudação executa duas consultas.</span><span class="sxs-lookup"><span data-stu-id="86e63-139">hello code runs two queries.</span></span> <span data-ttu-id="86e63-140">Cada consulta retorna um máximo de 100 dispositivos:</span><span class="sxs-lookup"><span data-stu-id="86e63-140">Each query returns a maximum of 100 devices:</span></span>

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

1. <span data-ttu-id="86e63-141">Salve e feche o hello `add-tags-query\src\main\java\com\mycompany\app\App.java` arquivo</span><span class="sxs-lookup"><span data-stu-id="86e63-141">Save and close hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="86e63-142">Criar hello **adicionar marcas-consulta** aplicativo e corrigir os erros.</span><span class="sxs-lookup"><span data-stu-id="86e63-142">Build hello **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="86e63-143">No prompt de comando, navegue toohello `add-tags-query` pasta e execução hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="86e63-143">At your command prompt, navigate toohello `add-tags-query` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="86e63-144">Criar um aplicativo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="86e63-144">Create a device app</span></span>

<span data-ttu-id="86e63-145">Nesta seção, você deve criar um aplicativo de console de Java que define um valor de propriedade relatado enviada tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="86e63-145">In this section, you create a Java console app that sets a reported property value that is sent tooIoT Hub.</span></span>

1. <span data-ttu-id="86e63-146">Em Olá `iot-java-twin-getstarted` pasta, crie um projeto Maven chamado **dispositivo simulado** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="86e63-146">In hello `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="86e63-147">Observe que este é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="86e63-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="86e63-148">No prompt de comando, navegue toohello `simulated-device` pasta.</span><span class="sxs-lookup"><span data-stu-id="86e63-148">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="86e63-149">Usando um editor de texto, abra Olá `pom.xml` arquivo hello `simulated-device` pasta e adicione Olá seguir dependências toohello **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="86e63-149">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="86e63-150">Esta dependência habilita Olá toouse **cliente de dispositivo iot** pacote no toocommunicate seu aplicativo com o hub IoT:</span><span class="sxs-lookup"><span data-stu-id="86e63-150">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="86e63-151">Você pode verificar a versão mais recente de saudação do **cliente de dispositivo iot** usando [pesquisa Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="86e63-151">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="86e63-152">Adicione o seguinte Olá **criar** nó após Olá **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="86e63-152">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="86e63-153">Esta configuração instrui Maven toouse Java toobuild 1.8 Olá aplicativo:</span><span class="sxs-lookup"><span data-stu-id="86e63-153">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="86e63-154">Salve e feche o hello `pom.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="86e63-154">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="86e63-155">Usando um editor de texto, abra Olá `simulated-device\src\main\java\com\mycompany\app\App.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="86e63-155">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="86e63-156">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="86e63-156">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="86e63-157">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="86e63-157">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="86e63-158">Substituindo `{youriothubname}` com seu nome de hub IoT, e `{yourdevicekey}` com valor de chave de dispositivo do hello gerado na Olá *criar uma identidade de dispositivo* seção:</span><span class="sxs-lookup"><span data-stu-id="86e63-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="86e63-159">Este aplicativo de exemplo usa Olá **protocolo** variável quando ele cria uma **DeviceClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="86e63-159">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="86e63-160">Atualmente, toouse dispositivo duas recursos você deve usar o protocolo de MQTT saudação.</span><span class="sxs-lookup"><span data-stu-id="86e63-160">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="86e63-161">Adicionar Olá toohello de código a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="86e63-161">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="86e63-162">Crie um toocommunicate de cliente de dispositivo com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="86e63-162">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="86e63-163">Criar um **dispositivo** toostore Olá dispositivo duas propriedades do objeto.</span><span class="sxs-lookup"><span data-stu-id="86e63-163">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="86e63-164">Adicionar Olá toohello de código a seguir **principal** método toocreate um **connectivityType** relatados de propriedade e enviá-lo tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="86e63-164">Add hello following code toohello **main** method toocreate a **connectivityType** reported property and send it tooIoT Hub:</span></span>

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

1. <span data-ttu-id="86e63-165">Adicionar Olá após o final do código toohello de saudação **principal** método.</span><span class="sxs-lookup"><span data-stu-id="86e63-165">Add hello following code toohello end of hello **main** method.</span></span> <span data-ttu-id="86e63-166">Aguardando Olá **Enter** chave permite que o tempo para o IoT Hub tooreport Olá status Olá dispositivo duas operações:</span><span class="sxs-lookup"><span data-stu-id="86e63-166">Waiting for hello **Enter** key allows time for IoT Hub tooreport hello status of hello device twin operations:</span></span>

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="86e63-167">Salve e feche o hello `simulated-device\src\main\java\com\mycompany\app\App.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="86e63-167">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="86e63-168">Criar hello **dispositivo simulado** aplicativo e corrigir os erros.</span><span class="sxs-lookup"><span data-stu-id="86e63-168">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="86e63-169">No prompt de comando, navegue toohello `simulated-device` pasta e execução hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="86e63-169">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="86e63-170">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="86e63-170">Run hello apps</span></span>

<span data-ttu-id="86e63-171">Agora você está pronto toorun Olá os aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="86e63-171">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="86e63-172">Em um prompt de comando no hello `add-tags-query` pasta, execute Olá Olá de toorun de comando a seguir **adicionar marcas-consulta** do serviço de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="86e63-172">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Valores de marca de tooupdate de aplicativo de serviço de IoT Hub de Java e executar consultas de dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="86e63-174">Você pode ver Olá **planta** e **região** marcas adicionadas toohello duas de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="86e63-174">You can see hello **plant** and **region** tags added toohello device twin.</span></span> <span data-ttu-id="86e63-175">Olá primeira consulta retorna seu dispositivo, mas Olá segundo não.</span><span class="sxs-lookup"><span data-stu-id="86e63-175">hello first query returns your device, but hello second does not.</span></span>

1. <span data-ttu-id="86e63-176">Em um prompt de comando no hello `simulated-device` pasta, execute Olá Olá de tooadd de comando a seguir **connectivityType** relatado duas de dispositivo de toohello de propriedade:</span><span class="sxs-lookup"><span data-stu-id="86e63-176">At a command prompt in hello `simulated-device` folder, run hello following command tooadd hello **connectivityType** reported property toohello device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![cliente de dispositivo Olá adiciona hello * * connectivityType * * relatado propriedade](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="86e63-178">Em um prompt de comando no hello `add-tags-query` pasta, execute Olá Olá de toorun de comando a seguir **adicionar marcas-consulta** uma segunda vez do serviço de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="86e63-178">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Valores de marca de tooupdate de aplicativo de serviço de IoT Hub de Java e executar consultas de dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="86e63-180">Agora seu dispositivo enviou Olá **connectivityType** tooIoT propriedade Hub, a segunda consulta de saudação retorna seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="86e63-180">Now your device has sent hello **connectivityType** property tooIoT Hub, hello second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86e63-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86e63-181">Next steps</span></span>

<span data-ttu-id="86e63-182">Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="86e63-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="86e63-183">Você adicionou o metadados do dispositivo como marcas de um aplicativo de back-end e gravou informações de conectividade do dispositivo do dispositivo aplicativo tooreport em duas de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="86e63-183">You added device metadata as tags from a back-end app, and wrote a device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="86e63-184">Você também aprendeu como tooquery Olá informações do dispositivo duas usando linguagem de consulta do tipo SQL IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="86e63-184">You also learned how tooquery hello device twin information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="86e63-185">Saudação de uso toolearn de recursos a seguir como a:</span><span class="sxs-lookup"><span data-stu-id="86e63-185">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="86e63-186">Enviar telemetria de dispositivos com hello [começar com o IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="86e63-186">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="86e63-187">Controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário) com hello [usar métodos diretos](iot-hub-java-java-direct-methods.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="86e63-187">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
