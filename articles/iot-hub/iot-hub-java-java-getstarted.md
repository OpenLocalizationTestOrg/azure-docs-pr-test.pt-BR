---
title: "aaaGet de Introdução ao Azure IoT Hub (Java) | Microsoft Docs"
description: "Saiba como o dispositivo para nuvem toosend mensagens tooAzure IoT Hub usando IoT SDKs para Java. Criar dispositivo simulado e tooregister de aplicativos de serviço de seu dispositivo, enviar mensagens e ler mensagens de hub IoT."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a><span data-ttu-id="ee113-104">Conecte seu dispositivo tooyour IoT hub que utilizado Java</span><span class="sxs-lookup"><span data-stu-id="ee113-104">Connect your device tooyour IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="ee113-105">No final da saudação deste tutorial, você tem três aplicativos de console de Java:</span><span class="sxs-lookup"><span data-stu-id="ee113-105">At hello end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="ee113-106">**criar dispositivo-identidade**, que cria uma identidade de dispositivo e de segurança da chave tooconnect seu aplicativo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ee113-106">**create-device-identity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="ee113-107">**mensagens de leitura-d2c**, que exibe a telemetria de saudação enviada pelo seu aplicativo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ee113-107">**read-d2c-messages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="ee113-108">**dispositivo simulado**, que conecta tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente e envia uma mensagem de telemetria a cada segundo usando Olá protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="ee113-108">**simulated-device**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="ee113-109">artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun ambos os aplicativos em dispositivos e o back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="ee113-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both apps toorun on devices and your solution back end.</span></span>

<span data-ttu-id="ee113-110">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee113-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ee113-111">Olá mais recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="ee113-111">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="ee113-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="ee113-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="ee113-113">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee113-113">An active Azure account.</span></span> <span data-ttu-id="ee113-114">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="ee113-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="ee113-115">Como etapa final, anote Olá **chave primária** valor.</span><span class="sxs-lookup"><span data-stu-id="ee113-115">As a final step, make a note of hello **Primary key** value.</span></span> <span data-ttu-id="ee113-116">Em seguida, clique em **pontos de extremidade** e hello **eventos** ponto de extremidade interno.</span><span class="sxs-lookup"><span data-stu-id="ee113-116">Then click **Endpoints** and hello **Events** built-in endpoint.</span></span> <span data-ttu-id="ee113-117">Em Olá **propriedades** folha, anote Olá **nome compatível com o evento Hub** e hello **ponto de extremidade compatível com o evento Hub** endereço.</span><span class="sxs-lookup"><span data-stu-id="ee113-117">On hello **Properties** blade, make a note of hello **Event Hub-compatible name** and hello **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="ee113-118">Você precisa desses três valores quando cria o aplicativo **read-d2c-messages**.</span><span class="sxs-lookup"><span data-stu-id="ee113-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Folha Mensagens do Hub IoT do Portal do Azure][6]

<span data-ttu-id="ee113-120">Você criou seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ee113-120">You have now created your IoT hub.</span></span> <span data-ttu-id="ee113-121">Você tem Olá nome de host do IoT Hub, cadeia de caracteres de conexão de IoT Hub, chave primária de Hub IoT, nome do Hub de eventos-compatível e ponto de extremidade compatível com o evento Hub é necessário toocomplete neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="ee113-121">You have hello IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need toocomplete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="ee113-122">Criar uma identidade do dispositivo</span><span class="sxs-lookup"><span data-stu-id="ee113-122">Create a device identity</span></span>
<span data-ttu-id="ee113-123">Nesta seção, você deve criar um aplicativo de console de Java que cria uma identidade de dispositivo no registro de identidade Olá em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ee113-123">In this section, you create a Java console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="ee113-124">Um dispositivo não pode se conectar a tooIoT hub, a menos que ele tenha uma entrada no registro de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="ee113-124">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="ee113-125">Para obter mais informações, consulte Olá **registro identidade** seção Olá [guia do desenvolvedor de IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="ee113-125">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="ee113-126">Quando você executa esse aplicativo de console, ele gera uma ID de dispositivo exclusivo e chave que seu dispositivo possa usar tooidentify em si, quando ele envia o dispositivo para nuvem mensagens tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ee113-126">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="ee113-127">Crie uma pasta vazia chamada iot-java-get-started.</span><span class="sxs-lookup"><span data-stu-id="ee113-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="ee113-128">Na pasta iot java-get-iniciado hello, crie um projeto de Maven chamado **identidade criar de dispositivo** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="ee113-128">In hello iot-java-get-started folder, create a Maven project called **create-device-identity** using hello following command at your command prompt.</span></span> <span data-ttu-id="ee113-129">Observe que este é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="ee113-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="ee113-130">No prompt de comando, navegue toohello pasta de identidade criar de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ee113-130">At your command prompt, navigate toohello create-device-identity folder.</span></span>

3. <span data-ttu-id="ee113-131">Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta de identidade criar de dispositivo hello e adicione Olá toohello de dependência a seguir **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="ee113-131">Using a text editor, open hello pom.xml file in hello create-device-identity folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="ee113-132">Esta dependência habilita você toouse Olá iot-serviço-pacote de cliente em seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="ee113-132">This dependency enables you toouse hello iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ee113-133">Você pode verificar a versão mais recente de saudação do **cliente de serviço iot** usando [pesquisa Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="ee113-133">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="ee113-134">Salve e feche o arquivo de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="ee113-134">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="ee113-135">Usando um editor de texto, abra o arquivo de create-device-identity\src\main\java\com\mycompany\app\App.java de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee113-135">Using a text editor, open hello create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="ee113-136">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="ee113-136">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="ee113-137">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe, substituindo **{yourhubconnectionstring}** com hello valor seu mencionado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="ee113-137">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** with hello value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="ee113-138">Modificar assinatura Olá Olá **principal** tooinclude método hello exceções da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ee113-138">Modify hello signature of hello **main** method tooinclude hello exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="ee113-139">Adicionar Olá código a seguir como corpo de saudação do hello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="ee113-139">Add hello following code as hello body of hello **main** method.</span></span> <span data-ttu-id="ee113-140">Esse código cria um dispositivo denominado *javadevice* no registro de identidade do Hub IoT, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="ee113-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="ee113-141">Ele exibe, em seguida, Olá ID do dispositivo e a chave que é necessário mais tarde:</span><span class="sxs-lookup"><span data-stu-id="ee113-141">It then displays hello device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. <span data-ttu-id="ee113-142">Salve e feche o arquivo de App.java hello.</span><span class="sxs-lookup"><span data-stu-id="ee113-142">Save and close hello App.java file.</span></span>

11. <span data-ttu-id="ee113-143">Olá toobuild **identidade criar de dispositivo** aplicativo usando o Maven, executar Olá seguinte comando no prompt de comando Olá na pasta do hello identidade criar de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="ee113-143">toobuild hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="ee113-144">Olá toorun **identidade criar de dispositivo** aplicativo usando o Maven, executar Olá seguinte comando no prompt de comando Olá na pasta do hello identidade criar de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="ee113-144">toorun hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="ee113-145">Anote Olá **ID do dispositivo** e **chave dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ee113-145">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="ee113-146">É necessário mais tarde esses valores quando você cria um aplicativo que se conecta tooIoT Hub como um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ee113-146">You need these values later when you create an app that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="ee113-147">Olá registro de identidade de IoT Hub armazena apenas o hub IoT toohello de proteger o acesso do dispositivo identidades tooenable.</span><span class="sxs-lookup"><span data-stu-id="ee113-147">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="ee113-148">Ele armazena toouse IDs e chaves de dispositivo como credenciais de segurança e um sinalizador habilitado/desabilitado que você pode usar o acesso de toodisable para um dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="ee113-148">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="ee113-149">Se seu aplicativo precisa toostore outros metadados específicos do dispositivo, ele deve usar um repositório específico do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee113-149">If your app needs toostore other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="ee113-150">Para obter mais informações, consulte Olá [guia do desenvolvedor de IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="ee113-150">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="ee113-151">Receber mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="ee113-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="ee113-152">Nesta seção, você cria um aplicativo do console do Java que lê mensagens do dispositivo para a nuvem do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ee113-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="ee113-153">Um hub IoT expõe um [Hub de eventos][lnk-event-hubs-overview]-tooenable de ponto de extremidade compatível tooread mensagens de dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="ee113-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="ee113-154">coisas tookeep simples, este tutorial cria um leitor básico que não é adequado para uma implantação de alta taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="ee113-154">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="ee113-155">Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial mostra como o dispositivo para nuvem tooprocess mensagens em escala.</span><span class="sxs-lookup"><span data-stu-id="ee113-155">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="ee113-156">Olá [Introdução aos Hubs de eventos] [ lnk-eventhubs-tutorial] tutorial fornece informações adicionais sobre como tooprocess mensagens de Hubs de eventos e é aplicável toohello pontos de extremidade compatível com o evento de Hub IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ee113-156">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="ee113-157">Olá, ponto de extremidade compatível com o evento Hub para ler mensagens de dispositivo para nuvem sempre usa protocolo AMQP de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee113-157">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="ee113-158">Na pasta de iot java-get-iniciado Olá criado na Olá *criar uma identidade de dispositivo* seção, crie um projeto Maven chamado **mensagens de d2c leitura** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="ee113-158">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **read-d2c-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="ee113-159">Observe que este é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="ee113-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="ee113-160">No prompt de comando, navegue toohello pasta de leitura de d2c de mensagens.</span><span class="sxs-lookup"><span data-stu-id="ee113-160">At your command prompt, navigate toohello read-d2c-messages folder.</span></span>

3. <span data-ttu-id="ee113-161">Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta de leitura de d2c de mensagens de saudação e adicione Olá seguir dependência toohello **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="ee113-161">Using a text editor, open hello pom.xml file in hello read-d2c-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="ee113-162">Esta dependência habilita um pacote de cliente eventhubs Olá toouse em tooread seu aplicativo de ponto de extremidade de Hub de eventos-compatível com hello:</span><span class="sxs-lookup"><span data-stu-id="ee113-162">This dependency enables you toouse hello eventhubs-client package in your app tooread from hello Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="ee113-163">Salve e feche o arquivo de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="ee113-163">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="ee113-164">Usando um editor de texto, abra o arquivo de read-d2c-messages\src\main\java\com\mycompany\app\App.java de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee113-164">Using a text editor, open hello read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="ee113-165">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="ee113-165">Add hello following **import** statements toohello file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="ee113-166">Adicionar Olá toohello variável de nível de classe a seguir **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="ee113-166">Add hello following class-level variable toohello **App** class.</span></span> <span data-ttu-id="ee113-167">Substituir **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, e **{youreventhubcompatiblename}** com valores hello você anotou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="ee113-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with hello values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="ee113-168">Adicione o seguinte Olá **receiveMessages** método toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="ee113-168">Add hello following **receiveMessages** method toohello **App** class.</span></span> <span data-ttu-id="ee113-169">Esse método cria um **EventHubClient** tooconnect toohello compatível com o evento Hub extremidade da instância e, em seguida, assincronamente cria um **PartitionReceiver** tooread de instância de um Hub de eventos partição.</span><span class="sxs-lookup"><span data-stu-id="ee113-169">This method creates an **EventHubClient** instance tooconnect toohello Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance tooread from an Event Hub partition.</span></span> <span data-ttu-id="ee113-170">Ele loops continuamente e imprime os detalhes da mensagem de saudação até que o aplicativo hello termina.</span><span class="sxs-lookup"><span data-stu-id="ee113-170">It loops continuously and prints hello message details until hello app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="ee113-171">Esse método usa um filtro quando ele cria receptor Olá para que hello destinatário lê apenas as mensagens enviadas tooIoT Hub depois receptor Olá começa a ser executado.</span><span class="sxs-lookup"><span data-stu-id="ee113-171">This method uses a filter when it creates hello receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="ee113-172">Essa técnica é útil em um ambiente de teste para poder ver o conjunto atual de saudação de mensagens.</span><span class="sxs-lookup"><span data-stu-id="ee113-172">This technique is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="ee113-173">Em um ambiente de produção, seu código deve certificar-se de que ele processa todas as mensagens de saudação - para obter mais informações, consulte Olá [como tooprocess mensagens de dispositivo para a nuvem de IoT Hub] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="ee113-173">In a production environment, your code should make sure that it processes all hello messages - for more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="ee113-174">Modificar assinatura Olá Olá **principal** tooinclude método hello exceção da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ee113-174">Modify hello signature of hello **main** method tooinclude hello exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="ee113-175">Adicionar Olá toohello de código a seguir **principal** método hello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="ee113-175">Add hello following code toohello **main** method in hello **App** class.</span></span> <span data-ttu-id="ee113-176">Esse código cria Olá dois **EventHubClient** e **PartitionReceiver** instâncias e permite que você tooclose Olá aplicativo quando você concluiu o processamento de mensagens:</span><span class="sxs-lookup"><span data-stu-id="ee113-176">This code creates hello two **EventHubClient** and **PartitionReceiver** instances and enables you tooclose hello app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="ee113-177">Esse código supõe que você criou seu hub IoT na camada (gratuita) do hello F1.</span><span class="sxs-lookup"><span data-stu-id="ee113-177">This code assumes you created your IoT hub in hello F1 (free) tier.</span></span> <span data-ttu-id="ee113-178">Um hub IoT gratuito tem duas partições chamadas "0" e "1".</span><span class="sxs-lookup"><span data-stu-id="ee113-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="ee113-179">Salve e feche o arquivo de App.java hello.</span><span class="sxs-lookup"><span data-stu-id="ee113-179">Save and close hello App.java file.</span></span>

12. <span data-ttu-id="ee113-180">Olá toobuild **mensagens de d2c leitura** aplicativo usando o Maven, executar o seguinte comando no prompt de comando Olá na pasta de leitura de d2c de mensagens de saudação do hello:</span><span class="sxs-lookup"><span data-stu-id="ee113-180">toobuild hello **read-d2c-messages** app using Maven, execute hello following command at hello command prompt in hello read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="ee113-181">Criar um aplicativo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="ee113-181">Create a device app</span></span>
<span data-ttu-id="ee113-182">Nesta seção, você deve criar um aplicativo de console de Java que simula um dispositivo que envia o hub de IoT tooan mensagens de dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="ee113-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="ee113-183">Na pasta de iot java-get-iniciado Olá criado na Olá *criar uma identidade de dispositivo* seção, crie um projeto Maven chamado **dispositivo simulado** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="ee113-183">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="ee113-184">Observe que este é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="ee113-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="ee113-185">No prompt de comando, navegue pasta do dispositivo simulado toohello.</span><span class="sxs-lookup"><span data-stu-id="ee113-185">At your command prompt, navigate toohello simulated-device folder.</span></span>

3. <span data-ttu-id="ee113-186">Usando um editor de texto, abra o arquivo de pom.xml de saudação na pasta do dispositivo simulado hello e adicione Olá dependências toohello a seguir **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="ee113-186">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="ee113-187">Esta dependência habilita você toouse Olá hub IOT-java-pacote de cliente em toocommunicate seu aplicativo com o hub IoT e tooserialize tooJSON de objetos Java:</span><span class="sxs-lookup"><span data-stu-id="ee113-187">This dependency enables you toouse hello iothub-java-client package in your app toocommunicate with your IoT hub and tooserialize Java objects tooJSON:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ee113-188">Você pode verificar a versão mais recente de saudação do **cliente de dispositivo iot** usando [pesquisa Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="ee113-188">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="ee113-189">Salve e feche o arquivo de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="ee113-189">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="ee113-190">Usando um editor de texto, abra o arquivo de simulated-device\src\main\java\com\mycompany\app\App.java de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee113-190">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="ee113-191">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="ee113-191">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="ee113-192">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="ee113-192">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="ee113-193">Substituindo **{youriothubname}** com seu nome de hub IoT, e **{yourdevicekey}** com valor de chave de dispositivo do hello gerado na Olá *criar uma identidade de dispositivo* seção:</span><span class="sxs-lookup"><span data-stu-id="ee113-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="ee113-194">Este aplicativo de exemplo usa Olá **protocolo** variável quando ele cria uma **DeviceClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="ee113-194">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="ee113-195">Você pode usar qualquer toocommunicate de protocolo hello MQTT, AMQP ou HTTP com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ee113-195">You can use either hello MQTT, AMQP, or HTTP protocol toocommunicate with IoT Hub.</span></span>

8. <span data-ttu-id="ee113-196">Adicione seguinte Olá aninhados **TelemetryDataPoint** classe dentro Olá **aplicativo** dados de telemetria de saudação toospecify o dispositivo envia tooyour IoT hub de classe:</span><span class="sxs-lookup"><span data-stu-id="ee113-196">Add hello following nested **TelemetryDataPoint** class inside hello **App** class toospecify hello telemetry data your device sends tooyour IoT hub:</span></span>

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. <span data-ttu-id="ee113-197">Adicione seguinte Olá aninhados **EventCallback** classe dentro Olá **aplicativo** classe toodisplay Olá confirmação status Olá hub IoT retorna ao processar uma mensagem de saudação aplicativo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ee113-197">Add hello following nested **EventCallback** class inside hello **App** class toodisplay hello acknowledgement status that hello IoT hub returns when it processes a message from hello device app.</span></span> <span data-ttu-id="ee113-198">Este método também notifica o thread principal de saudação no aplicativo hello quando a mensagem de saudação foi processada:</span><span class="sxs-lookup"><span data-stu-id="ee113-198">This method also notifies hello main thread in hello app when hello message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="ee113-199">Adicione seguinte Olá aninhados **MessageSender** classe dentro Olá **aplicativo** classe.</span><span class="sxs-lookup"><span data-stu-id="ee113-199">Add hello following nested **MessageSender** class inside hello **App** class.</span></span> <span data-ttu-id="ee113-200">Olá **executar** método nesta classe gera IoT hub do exemplo telemetria dados toosend tooyour e aguarda uma confirmação antes de enviar a mensagem de saudação do seguinte:</span><span class="sxs-lookup"><span data-stu-id="ee113-200">hello **run** method in this class generates sample telemetry data toosend tooyour IoT hub and waits for an acknowledgement before sending hello next message:</span></span>

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
            System.out.println("Sending: " + msgStr);
    
            Object lockobj = new Object();
            EventCallback callback = new EventCallback();
            client.sendEventAsync(msg, callback, lockobj);
    
            synchronized (lockobj) {
              lockobj.wait();
            }
            Thread.sleep(1000);
          }
        } catch (InterruptedException e) {
          System.out.println("Finished.");
        }
      }
    }
    ```

    <span data-ttu-id="ee113-201">Esse método envia uma nova mensagem de dispositivo para nuvem um segundo após o hub IoT de saudação confirma a mensagem de saudação do anterior.</span><span class="sxs-lookup"><span data-stu-id="ee113-201">This method sends a new device-to-cloud message one second after hello IoT hub acknowledges hello previous message.</span></span> <span data-ttu-id="ee113-202">mensagem de saudação contém um objeto serializado para JSON com deviceId hello e gerado aleatoriamente números toosimulate um sensor de temperatura e um sensor de umidade.</span><span class="sxs-lookup"><span data-stu-id="ee113-202">hello message contains a JSON-serialized object with hello deviceId and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="ee113-203">Substituir saudação **principal** método com hello código que cria um hub IoT do thread toosend mensagens de dispositivo para nuvem tooyour a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee113-203">Replace hello **main** method with hello following code that creates a thread toosend device-to-cloud messages tooyour IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="ee113-204">Salve e feche o arquivo de App.java hello.</span><span class="sxs-lookup"><span data-stu-id="ee113-204">Save and close hello App.java file.</span></span>

13. <span data-ttu-id="ee113-205">Olá toobuild **dispositivo simulado** aplicativo usando o Maven, executar Olá comando no prompt de comando Olá na pasta do dispositivo simulado Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee113-205">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="ee113-206">coisas tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="ee113-206">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ee113-207">No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="ee113-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="ee113-208">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="ee113-208">Run hello apps</span></span>

<span data-ttu-id="ee113-209">Agora você está pronto toorun Olá aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ee113-209">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="ee113-210">Em um prompt de comando na pasta de leitura d2c hello, execute Olá toobegin comando primeira partição Olá em seu hub IoT de monitoramento a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee113-210">At a command prompt in hello read-d2c folder, run hello following command toobegin monitoring hello first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Mensagens do dispositivo para nuvem toomonitor de aplicativo de serviço de Java IoT Hub][7]

2. <span data-ttu-id="ee113-212">Em um prompt de comando na pasta do dispositivo simulado hello, execute Olá toobegin comando Enviar hub IoT do telemetria dados tooyour a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee113-212">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Mensagens do dispositivo para nuvem toosend de aplicativo de dispositivo de IoT Hub de Java][8]

3. <span data-ttu-id="ee113-214">Olá **uso** lado a lado no hello [portal do Azure] [ lnk-portal] mostra Olá número de mensagens enviadas toohello IoT hub:</span><span class="sxs-lookup"><span data-stu-id="ee113-214">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure portal uso bloco mostra o número de mensagens enviadas tooIoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="ee113-216">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee113-216">Next steps</span></span>
<span data-ttu-id="ee113-217">Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="ee113-217">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="ee113-218">Você usou esse dispositivo identidade tooenable Olá dispositivo toosend mensagens de dispositivo para nuvem toohello IoT hub de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ee113-218">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="ee113-219">Você também criou um aplicativo que exibe mensagens de saudação recebidas pelo hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee113-219">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="ee113-220">toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="ee113-220">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="ee113-221">[Conectando o dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="ee113-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="ee113-222">[Introdução ao gerenciamento de dispositivo][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="ee113-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="ee113-223">[Introdução ao Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="ee113-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="ee113-224">toolearn como tooextend seu IoT solução e o processo de dispositivo para nuvem mensagens em grande escala, consulte Olá [processar mensagens de dispositivo para nuvem] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="ee113-224">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
