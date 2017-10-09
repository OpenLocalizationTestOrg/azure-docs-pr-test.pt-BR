---
title: arquivos de aaaUpload de tooAzure dispositivos IoT Hub com Java | Microsoft Docs
description: "Como tooupload arquivos de uma dispositivo toohello nuvem usando o dispositivo IoT do Azure SDK para Java. Os arquivos carregados são armazenados em um contêiner de Azure Storage Blob."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: e305fe61bf7ca0aeb2c092bc2c7efebdc78d4f68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a><span data-ttu-id="536ee-104">Carregar arquivos de seu dispositivo toohello nuvem com o IoT Hub</span><span class="sxs-lookup"><span data-stu-id="536ee-104">Upload files from your device toohello cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="536ee-105">Este tutorial baseia-se em código Olá Olá [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-java-java-c2d.md) tooshow tutorial você como Olá toouse [arquivo de recursos de carregamento do IoT Hub](iot-hub-devguide-file-upload.md) tooupload um arquivo muito[ Armazenamento de BLOBs do Azure](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="536ee-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial tooshow you how toouse hello [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) tooupload a file too[Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="536ee-106">Olá tutorial mostra como para:</span><span class="sxs-lookup"><span data-stu-id="536ee-106">hello tutorial shows you how to:</span></span>

- <span data-ttu-id="536ee-107">Fornecer com segurança um URI de blob do Azure a um dispositivo para carregamento de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="536ee-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="536ee-108">Use Olá IoT Hub arquivo carregamento notificações tootrigger processar o arquivo de saudação em seu back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="536ee-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="536ee-109">Olá [começar com o IoT Hub](iot-hub-java-java-getstarted.md) e [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-java-java-c2d.md) tutoriais mostram Olá dispositivo para nuvem e nuvem para dispositivo mensagens funcionalidade básica de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="536ee-109">hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="536ee-110">Olá [mensagens de dispositivo para nuvem processo](iot-hub-java-java-process-d2c.md) tutorial descreve um mensagens de dispositivo para nuvem maneira tooreliably repositório no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="536ee-110">hello [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="536ee-111">No entanto, em alguns cenários você não pode mapear facilmente dados Olá que enviam seus dispositivos em Olá relativamente pequeno dispositivo para nuvem mensagens de IoT Hub aceita.</span><span class="sxs-lookup"><span data-stu-id="536ee-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="536ee-112">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="536ee-112">For example:</span></span>

* <span data-ttu-id="536ee-113">Arquivos grandes que contêm imagens</span><span class="sxs-lookup"><span data-stu-id="536ee-113">Large files that contain images</span></span>
* <span data-ttu-id="536ee-114">Vídeos</span><span class="sxs-lookup"><span data-stu-id="536ee-114">Videos</span></span>
* <span data-ttu-id="536ee-115">Dados de vibração amostrados a alta frequência</span><span class="sxs-lookup"><span data-stu-id="536ee-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="536ee-116">Alguma forma de dados pré-processados.</span><span class="sxs-lookup"><span data-stu-id="536ee-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="536ee-117">Esses arquivos normalmente são processadas na nuvem hello usando ferramentas como em lote [do Azure Data Factory](../data-factory/index.md) ou hello [Hadoop](../hdinsight/index.md) pilha.</span><span class="sxs-lookup"><span data-stu-id="536ee-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="536ee-118">Quando você precisar tooupland arquivos de um dispositivo, você ainda pode usar segurança hello e a confiabilidade do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="536ee-118">When you need tooupland files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="536ee-119">Olá final deste tutorial você executadas dois aplicativos de console de Java:</span><span class="sxs-lookup"><span data-stu-id="536ee-119">At hello end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="536ee-120">**dispositivo simulado**, uma versão modificada do aplicativo hello criado no tutorial Olá [mensagens de envio de nuvem para dispositivo com o IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="536ee-120">**simulated-device**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="536ee-121">Este aplicativo carrega um toostorage de arquivo usando um URI de SAS fornecido pelo seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="536ee-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="536ee-122">**read-file-upload-notification**, que recebe notificações de upload de arquivo do seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="536ee-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="536ee-123">O Hub IoT dá suporte a muitas plataformas de dispositivo e linguagens (incluindo C, .NET e Javascript) por meio dos SDKs do dispositivo IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="536ee-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="536ee-124">Consulte toohello [Centro de desenvolvedores do Azure IoT] para obter instruções passo a passo sobre como tooconnect tooAzure seu dispositivo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="536ee-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="536ee-125">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="536ee-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="536ee-126">Olá mais recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="536ee-126">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="536ee-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="536ee-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="536ee-128">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="536ee-128">An active Azure account.</span></span> <span data-ttu-id="536ee-129">(Se você não tiver uma conta, poderá criar uma [conta gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="536ee-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="536ee-130">Carregar um arquivo de um aplicativo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="536ee-130">Upload a file from a device app</span></span>

<span data-ttu-id="536ee-131">Nesta seção, você modificar o aplicativo para dispositivo Olá criado na [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-java-java-c2d.md) tooupload um hub de tooIoT do arquivo.</span><span class="sxs-lookup"><span data-stu-id="536ee-131">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tooupload a file tooIoT hub.</span></span>

1. <span data-ttu-id="536ee-132">Copiar um toohello do arquivo de imagem `simulated-device` pasta e renomeie- `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="536ee-132">Copy an image file toohello `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="536ee-133">Usando um editor de texto, abra Olá `simulated-device\src\main\java\com\mycompany\app\App.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="536ee-133">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="536ee-134">Adicionar Olá declaração de variável toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="536ee-134">Add hello variable declaration toohello **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="536ee-135">tooprocess mensagens de retorno de chamada de status de carregamento de arquivo, adicione o seguinte Olá aninhados classe toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="536ee-135">tooprocess file upload status callback messages, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="536ee-136">tooupload imagens tooIoT Hub, adicionar Olá após o método toohello **aplicativo** tooupload classe imagens tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="536ee-136">tooupload images tooIoT Hub, add hello following method toohello **App** class tooupload images tooIoT Hub:</span></span>

    ```java
    // Use IoT Hub tooupload a file asynchronously tooAzure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="536ee-137">Modificar Olá **principal** saudação do método toocall **uploadFile** método conforme Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="536ee-137">Modify hello **main** method toocall hello **uploadFile** method as shown in hello following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get hello filename and start hello upload.
      String fullFileName = System.getProperty("user.dir") + File.separator + fileName;
      uploadFile(fullFileName);
      System.out.println("File upload started with success");
    }
    catch (Exception e)
    {
      System.out.println("Exception uploading file: " + e.getCause() + " \nERROR: " + e.getMessage());
    }

    MessageSender sender = new MessageSender();
    ```

1. <span data-ttu-id="536ee-138">Olá toobuild do comando de uso a seguir de saudação **dispositivo simulado** aplicativo e verifique se há erros:</span><span class="sxs-lookup"><span data-stu-id="536ee-138">Use hello following command toobuild hello **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="536ee-139">Receber uma notificação de upload de arquivo</span><span class="sxs-lookup"><span data-stu-id="536ee-139">Receive a file upload notification</span></span>

<span data-ttu-id="536ee-140">Nesta seção, você criará um aplicativo de console Java que receba mensagens de notificação de upload de arquivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="536ee-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="536ee-141">Você precisa Olá **iothubowner** cadeia de conexão do seu IoT Hub toocomplete nesta seção.</span><span class="sxs-lookup"><span data-stu-id="536ee-141">You need hello **iothubowner** connection string for your IoT Hub toocomplete this section.</span></span> <span data-ttu-id="536ee-142">Você pode encontrar a cadeia de caracteres de conexão Olá no hello [portal do Azure](https://portal.azure.com/) em Olá **política de acesso compartilhado** folha.</span><span class="sxs-lookup"><span data-stu-id="536ee-142">You can find hello connection string in hello [Azure portal](https://portal.azure.com/) on hello **Shared access policy** blade.</span></span>

1. <span data-ttu-id="536ee-143">Crie um projeto Maven chamado **leitura-arquivo de carregamento de notificação** usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="536ee-143">Create a Maven project called **read-file-upload-notification** using hello following command at your command prompt.</span></span> <span data-ttu-id="536ee-144">Observe que esse é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="536ee-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="536ee-145">No prompt de comando, navegue toohello novo `read-file-upload-notification` pasta.</span><span class="sxs-lookup"><span data-stu-id="536ee-145">At your command prompt, navigate toohello new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="536ee-146">Usando um editor de texto, abra Olá `pom.xml` arquivo hello `read-file-upload-notification` pasta e adicione Olá seguir dependência toohello **dependências** nó.</span><span class="sxs-lookup"><span data-stu-id="536ee-146">Using a text editor, open hello `pom.xml` file in hello `read-file-upload-notification` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="536ee-147">Adicionando a dependência do hello permite Olá toouse **hub IOT-serviço-cliente java** pacote no toocommunicate seu aplicativo com o serviço de hub IoT:</span><span class="sxs-lookup"><span data-stu-id="536ee-147">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="536ee-148">Você pode verificar a versão mais recente de saudação do **cliente de serviço iot** usando [pesquisa Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="536ee-148">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="536ee-149">Salve e feche o hello `pom.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="536ee-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="536ee-150">Usando um editor de texto, abra Olá `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="536ee-150">Using a text editor, open hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="536ee-151">Adicione o seguinte Olá **importar** arquivo de toohello instruções:</span><span class="sxs-lookup"><span data-stu-id="536ee-151">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="536ee-152">Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="536ee-152">Add hello following class-level variables toohello **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="536ee-153">tooprint informações sobre o console de toohello de carregamento de arquivo hello, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="536ee-153">tooprint information about hello file upload toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Create a thread tooreceive file upload notifications.
    private static class ShowFileUploadNotifications implements Runnable {
      public void run() {
        try {
          while (true) {
            System.out.println("Recieve file upload notifications...");
            FileUploadNotification fileUploadNotification = fileUploadNotificationReceiver.receive();
            if (fileUploadNotification != null) {
              System.out.println("File Upload notification received");
              System.out.println("Device Id : " + fileUploadNotification.getDeviceId());
              System.out.println("Blob Uri: " + fileUploadNotification.getBlobUri());
              System.out.println("Blob Name: " + fileUploadNotification.getBlobName());
              System.out.println("Last Updated : " + fileUploadNotification.getLastUpdatedTimeDate());
              System.out.println("Blob Size (Bytes): " + fileUploadNotification.getBlobSizeInBytes());
              System.out.println("Enqueued Time: " + fileUploadNotification.getEnqueuedTimeUtcDate());
            }
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="536ee-154">thread de saudação toostart que escuta as notificações de carregamento de arquivo, adicione Olá toohello de código a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="536ee-154">toostart hello thread that listens for file upload notifications, add hello following code toohello **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from hello ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start hello thread tooreceive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER tooexit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="536ee-155">Salve e feche o hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="536ee-155">Save and close hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="536ee-156">Olá toobuild do comando de uso a seguir de saudação **leitura-arquivo de carregamento de notificação** aplicativo e verifique se há erros:</span><span class="sxs-lookup"><span data-stu-id="536ee-156">Use hello following command toobuild hello **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="536ee-157">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="536ee-157">Run hello applications</span></span>

<span data-ttu-id="536ee-158">Agora você está pronto toorun aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="536ee-158">Now you are ready toorun hello applications.</span></span>

<span data-ttu-id="536ee-159">Em um prompt de comando no hello `read-file-upload-notification` pasta, execute o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="536ee-159">At a command prompt in hello `read-file-upload-notification` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="536ee-160">Em um prompt de comando no hello `simulated-device` pasta, execute o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="536ee-160">At a command prompt in hello `simulated-device` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="536ee-161">Olá, seguinte captura de tela mostra a saída Olá de saudação **dispositivo simulado** aplicativo:</span><span class="sxs-lookup"><span data-stu-id="536ee-161">hello following screenshot shows hello output from hello **simulated-device** app:</span></span>

![Saída do aplicativo simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="536ee-163">Olá, seguinte captura de tela mostra a saída Olá de saudação **leitura-arquivo de carregamento de notificação** aplicativo:</span><span class="sxs-lookup"><span data-stu-id="536ee-163">hello following screenshot shows hello output from hello **read-file-upload-notification** app:</span></span>

![Saída do aplicativo read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="536ee-165">Você pode usar o hello tooview portal Olá carregado arquivo no contêiner de armazenamento de saudação configurado:</span><span class="sxs-lookup"><span data-stu-id="536ee-165">You can use hello portal tooview hello uploaded file in hello storage container you configured:</span></span>

![Arquivo carregado](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="536ee-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="536ee-167">Next steps</span></span>

<span data-ttu-id="536ee-168">Neste tutorial, você aprendeu como toouse Olá transferência recursos do IoT Hub toosimplify arquivo carregamentos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="536ee-168">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="536ee-169">Você pode continuar tooexplore IoT hub recursos e cenários com hello artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="536ee-169">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="536ee-170">[Criar um Hub IoT de modo programático][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="536ee-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="536ee-171">[Introdução tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="536ee-171">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="536ee-172">[SDKs do Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="536ee-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="536ee-173">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="536ee-173">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="536ee-174">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="536ee-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Centro de desenvolvedores do Azure IoT]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


