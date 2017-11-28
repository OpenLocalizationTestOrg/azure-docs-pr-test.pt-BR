---
title: Carregar arquivos de dispositivos para o Hub IoT do Azure com Java | Microsoft Docs
description: "Como carregar arquivos de um dispositivo para a nuvem usando o SDK do dispositivo IoT do Azure para Java. Os arquivos carregados são armazenados em um contêiner de Azure Storage Blob."
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
ms.openlocfilehash: c917a3b3e16f1e84f202d6c87a04faf642266701
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub"></a><span data-ttu-id="1478d-104">Carregar arquivos do seu dispositivo para a nuvem com o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="1478d-104">Upload files from your device to the cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="1478d-105">Este tutorial baseia-se no código do tutorial [Enviar mensagens da nuvem para o dispositivo com o Hub IoT](iot-hub-java-java-c2d.md) para mostrar como usar os [recursos de upload de arquivo do Hub IoT](iot-hub-devguide-file-upload.md) para carregar um arquivo para o [armazenamento de blobs do Azure](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="1478d-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial to show you how to use the [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) to upload a file to [Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="1478d-106">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="1478d-106">The tutorial shows you how to:</span></span>

- <span data-ttu-id="1478d-107">Fornecer com segurança um URI de blob do Azure a um dispositivo para carregamento de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="1478d-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="1478d-108">Usar as notificações de carregamento de arquivo do Hub IoT para disparar o processamento do arquivo no back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1478d-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="1478d-109">Os tutoriais [Introdução ao Hub IoT](iot-hub-java-java-getstarted.md) e [Enviar mensagens da nuvem para o dispositivo com o Hub IoT](iot-hub-java-java-c2d.md) mostram a funcionalidade básica de mensagens do dispositivo para a nuvem e da nuvem para o dispositivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1478d-109">The [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="1478d-110">O tutorial [Processar mensagens do dispositivo para a nuvem](iot-hub-java-java-process-d2c.md) descreve uma forma de armazenamento confiável das mensagens do dispositivo para a nuvem no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="1478d-110">The [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="1478d-111">No entanto, em alguns cenários você não pode mapear facilmente os dados que seus dispositivos enviam em mensagens relativamente menores do dispositivo para a nuvem que o Hub IoT aceita.</span><span class="sxs-lookup"><span data-stu-id="1478d-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="1478d-112">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1478d-112">For example:</span></span>

* <span data-ttu-id="1478d-113">Arquivos grandes que contêm imagens</span><span class="sxs-lookup"><span data-stu-id="1478d-113">Large files that contain images</span></span>
* <span data-ttu-id="1478d-114">Vídeos</span><span class="sxs-lookup"><span data-stu-id="1478d-114">Videos</span></span>
* <span data-ttu-id="1478d-115">Dados de vibração amostrados a alta frequência</span><span class="sxs-lookup"><span data-stu-id="1478d-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="1478d-116">Alguma forma de dados pré-processados.</span><span class="sxs-lookup"><span data-stu-id="1478d-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="1478d-117">Esses arquivos normalmente são processados em lote na nuvem usando ferramentas como o [Azure Data Factory](../data-factory/index.md) ou a pilha do [Hadoop](../hdinsight/index.md).</span><span class="sxs-lookup"><span data-stu-id="1478d-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/index.md) or the [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="1478d-118">Quando você precisar carregar arquivos de um dispositivo, ainda poderá usar a segurança e a confiabilidade do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1478d-118">When you need to upland files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="1478d-119">No final deste tutorial, você executará dois aplicativos do console Java:</span><span class="sxs-lookup"><span data-stu-id="1478d-119">At the end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="1478d-120">**simulated-device**, uma versão modificada do aplicativo criado no tutorial [Enviar mensagens da nuvem para o dispositivo com o Hub IoT].</span><span class="sxs-lookup"><span data-stu-id="1478d-120">**simulated-device**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="1478d-121">Esse aplicativo carrega um arquivo no armazenamento usando um URI SAS fornecido pelo seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1478d-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="1478d-122">**read-file-upload-notification**, que recebe notificações de upload de arquivo do seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1478d-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="1478d-123">O Hub IoT dá suporte a muitas plataformas de dispositivo e linguagens (incluindo C, .NET e Javascript) por meio dos SDKs do dispositivo IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="1478d-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="1478d-124">Confira a [Central de Desenvolvedores do IoT do Azure] para obter instruções passo a passo sobre como conectar seu dispositivo ao Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="1478d-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="1478d-125">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="1478d-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="1478d-126">A versão mais recente do [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="1478d-126">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="1478d-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="1478d-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="1478d-128">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="1478d-128">An active Azure account.</span></span> <span data-ttu-id="1478d-129">(Se você não tiver uma conta, poderá criar uma [conta gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="1478d-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="1478d-130">Carregar um arquivo de um aplicativo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="1478d-130">Upload a file from a device app</span></span>

<span data-ttu-id="1478d-131">Nesta seção, você modifica o aplicativo de dispositivo criado em [Enviar mensagens da nuvem para o dispositivo com o Hub IoT](iot-hub-java-java-c2d.md) para carregar um arquivo para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1478d-131">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) to upload a file to IoT hub.</span></span>

1. <span data-ttu-id="1478d-132">Copie um arquivo de imagem para a pasta `simulated-device` e renomeie-o como `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="1478d-132">Copy an image file to the `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="1478d-133">Usando um editor de texto, abra o arquivo `simulated-device\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="1478d-133">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="1478d-134">Adicione a declaração de variável para a classe **Aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="1478d-134">Add the variable declaration to the **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="1478d-135">Para processar mensagens de retorno de chamada de status de upload de arquivo, adicione a seguinte classe aninhada à classe **Aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="1478d-135">To process file upload status callback messages, add the following nested class to the **App** class:</span></span>

    ```java
    // Define a callback method to print status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to file upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="1478d-136">Para carregar imagens para o IoT Hub, adicione o seguinte método à classe de **Aplicativo** para carregar imagens para o Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="1478d-136">To upload images to IoT Hub, add the following method to the **App** class to upload images to IoT Hub:</span></span>

    ```java
    // Use IoT Hub to upload a file asynchronously to Azure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="1478d-137">Modifique o método **principal** para chamar o método **uploadFile** conforme mostrado no trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="1478d-137">Modify the **main** method to call the **uploadFile** method as shown in the following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get the filename and start the upload.
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

1. <span data-ttu-id="1478d-138">Use o seguinte comando para criar o aplicativo **simulated-device** e verificar se há erros:</span><span class="sxs-lookup"><span data-stu-id="1478d-138">Use the following command to build the **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="1478d-139">Receber uma notificação de upload de arquivo</span><span class="sxs-lookup"><span data-stu-id="1478d-139">Receive a file upload notification</span></span>

<span data-ttu-id="1478d-140">Nesta seção, você criará um aplicativo de console Java que receba mensagens de notificação de upload de arquivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1478d-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="1478d-141">É necessário ter a cadeia de conexão **iothubowner** para o Hub IoT concluir esta seção.</span><span class="sxs-lookup"><span data-stu-id="1478d-141">You need the **iothubowner** connection string for your IoT Hub to complete this section.</span></span> <span data-ttu-id="1478d-142">Você pode encontrar a cadeia de conexão no [portal do Azure](https://portal.azure.com/) na folha **Política de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="1478d-142">You can find the connection string in the [Azure portal](https://portal.azure.com/) on the **Shared access policy** blade.</span></span>

1. <span data-ttu-id="1478d-143">Crie um projeto Maven chamado **read-file-upload-notification** usando o seguinte comando no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="1478d-143">Create a Maven project called **read-file-upload-notification** using the following command at your command prompt.</span></span> <span data-ttu-id="1478d-144">Observe que esse é um comando único e longo:</span><span class="sxs-lookup"><span data-stu-id="1478d-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="1478d-145">No prompt de comando, navegue até a nova pasta `read-file-upload-notification`.</span><span class="sxs-lookup"><span data-stu-id="1478d-145">At your command prompt, navigate to the new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="1478d-146">Usando um editor de texto, abra o arquivo `pom.xml` na pasta `read-file-upload-notification` e adicione a dependência a seguir ao nó **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="1478d-146">Using a text editor, open the `pom.xml` file in the `read-file-upload-notification` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="1478d-147">A adição da dependência permite que você use o pacote **iothub-java-service-client** no aplicativo para se comunicar com o serviço do Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="1478d-147">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="1478d-148">Você pode verificar a versão mais recente do **iot-service-client** usando a [pesquisa do Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="1478d-148">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="1478d-149">Salve e feche o arquivo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="1478d-149">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="1478d-150">Usando um editor de texto, abra o arquivo `read-file-upload-notification\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="1478d-150">Using a text editor, open the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="1478d-151">Adicione as seguintes instruções **import** ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="1478d-151">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="1478d-152">Adicione as seguintes variáveis no nível da classe à classe **App** :</span><span class="sxs-lookup"><span data-stu-id="1478d-152">Add the following class-level variables to the **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="1478d-153">Para imprimir informações sobre o upload do arquivo para o console, adicione a seguinte classe aninhada à classe **Aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="1478d-153">To print information about the file upload to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Create a thread to receive file upload notifications.
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

1. <span data-ttu-id="1478d-154">Para iniciar o thread que escuta notificações de upload de arquivo, adicione o seguinte código ao método **principal**:</span><span class="sxs-lookup"><span data-stu-id="1478d-154">To start the thread that listens for file upload notifications, add the following code to the **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from the ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start the thread to receive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER to exit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="1478d-155">Salve e feche o arquivo `read-file-upload-notification\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="1478d-155">Save and close the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="1478d-156">Use o seguinte comando para criar o aplicativo **read-file-upload-notification** e verificar se há erros:</span><span class="sxs-lookup"><span data-stu-id="1478d-156">Use the following command to build the **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-the-applications"></a><span data-ttu-id="1478d-157">Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="1478d-157">Run the applications</span></span>

<span data-ttu-id="1478d-158">Agora você está pronto para executar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1478d-158">Now you are ready to run the applications.</span></span>

<span data-ttu-id="1478d-159">Em um prompt de comando na pasta `read-file-upload-notification`, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1478d-159">At a command prompt in the `read-file-upload-notification` folder, run the following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="1478d-160">Em um prompt de comando na pasta `simulated-device`, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1478d-160">At a command prompt in the `simulated-device` folder, run the following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="1478d-161">A captura de tela a seguir mostra a saída do aplicativo **simulated-device**:</span><span class="sxs-lookup"><span data-stu-id="1478d-161">The following screenshot shows the output from the **simulated-device** app:</span></span>

![Saída do aplicativo simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="1478d-163">A captura de tela a seguir mostra a saída do aplicativo **read-file-upload-notification**:</span><span class="sxs-lookup"><span data-stu-id="1478d-163">The following screenshot shows the output from the **read-file-upload-notification** app:</span></span>

![Saída do aplicativo read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="1478d-165">Você pode usar o portal para exibir o arquivo carregado no contêiner de armazenamento configurado:</span><span class="sxs-lookup"><span data-stu-id="1478d-165">You can use the portal to view the uploaded file in the storage container you configured:</span></span>

![Arquivo carregado](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="1478d-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1478d-167">Next steps</span></span>

<span data-ttu-id="1478d-168">Neste tutorial, você aprendeu a usar os recursos de carregamento de arquivo do Hub IoT para simplificar os carregamentos de arquivos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="1478d-168">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="1478d-169">Você pode continuar explorando os recursos e cenários do Hub IoT com os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="1478d-169">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="1478d-170">[Criar um Hub IoT de modo programático][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="1478d-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="1478d-171">[Introdução ao SDK de C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="1478d-171">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="1478d-172">[SDKs do Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="1478d-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="1478d-173">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="1478d-173">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="1478d-174">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="1478d-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Central de Desenvolvedores do IoT do Azure]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


