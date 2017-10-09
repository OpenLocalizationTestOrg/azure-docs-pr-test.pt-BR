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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a>Carregar arquivos de seu dispositivo toohello nuvem com o IoT Hub

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Este tutorial baseia-se em código Olá Olá [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-java-java-c2d.md) tooshow tutorial você como Olá toouse [arquivo de recursos de carregamento do IoT Hub](iot-hub-devguide-file-upload.md) tooupload um arquivo muito[ Armazenamento de BLOBs do Azure](../storage/index.md). Olá tutorial mostra como para:

- Fornecer com segurança um URI de blob do Azure a um dispositivo para carregamento de um arquivo.
- Use Olá IoT Hub arquivo carregamento notificações tootrigger processar o arquivo de saudação em seu back-end do aplicativo.

Olá [começar com o IoT Hub](iot-hub-java-java-getstarted.md) e [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-java-java-c2d.md) tutoriais mostram Olá dispositivo para nuvem e nuvem para dispositivo mensagens funcionalidade básica de IoT Hub. Olá [mensagens de dispositivo para nuvem processo](iot-hub-java-java-process-d2c.md) tutorial descreve um mensagens de dispositivo para nuvem maneira tooreliably repositório no armazenamento de BLOBs do Azure. No entanto, em alguns cenários você não pode mapear facilmente dados Olá que enviam seus dispositivos em Olá relativamente pequeno dispositivo para nuvem mensagens de IoT Hub aceita. Por exemplo:

* Arquivos grandes que contêm imagens
* Vídeos
* Dados de vibração amostrados a alta frequência
* Alguma forma de dados pré-processados.

Esses arquivos normalmente são processadas na nuvem hello usando ferramentas como em lote [do Azure Data Factory](../data-factory/index.md) ou hello [Hadoop](../hdinsight/index.md) pilha. Quando você precisar tooupland arquivos de um dispositivo, você ainda pode usar segurança hello e a confiabilidade do IoT Hub.

Olá final deste tutorial você executadas dois aplicativos de console de Java:

* **dispositivo simulado**, uma versão modificada do aplicativo hello criado no tutorial Olá [mensagens de envio de nuvem para dispositivo com o IoT Hub]. Este aplicativo carrega um toostorage de arquivo usando um URI de SAS fornecido pelo seu hub IoT.
* **read-file-upload-notification**, que recebe notificações de upload de arquivo do seu Hub IoT.

> [!NOTE]
> O Hub IoT dá suporte a muitas plataformas de dispositivo e linguagens (incluindo C, .NET e Javascript) por meio dos SDKs do dispositivo IoT do Azure. Consulte toohello [Centro de desenvolvedores do Azure IoT] para obter instruções passo a passo sobre como tooconnect tooAzure seu dispositivo IoT Hub.

toocomplete neste tutorial, você precisa Olá a seguir:

* Olá mais recente [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Uma conta ativa do Azure. (Se você não tiver uma conta, poderá criar uma [conta gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.)

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Carregar um arquivo de um aplicativo de dispositivo

Nesta seção, você modificar o aplicativo para dispositivo Olá criado na [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-java-java-c2d.md) tooupload um hub de tooIoT do arquivo.

1. Copiar um toohello do arquivo de imagem `simulated-device` pasta e renomeie- `myimage.png`.

1. Usando um editor de texto, abra Olá `simulated-device\src\main\java\com\mycompany\app\App.java` arquivo.

1. Adicionar Olá declaração de variável toohello **aplicativo** classe:

    ```java
    private static String fileName = "myimage.png";
    ```

1. tooprocess mensagens de retorno de chamada de status de carregamento de arquivo, adicione o seguinte Olá aninhados classe toohello **aplicativo** classe:

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. tooupload imagens tooIoT Hub, adicionar Olá após o método toohello **aplicativo** tooupload classe imagens tooIoT Hub:

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

1. Modificar Olá **principal** saudação do método toocall **uploadFile** método conforme Olá trecho de código a seguir:

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

1. Olá toobuild do comando de uso a seguir de saudação **dispositivo simulado** aplicativo e verifique se há erros:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a>Receber uma notificação de upload de arquivo

Nesta seção, você criará um aplicativo de console Java que receba mensagens de notificação de upload de arquivo do Hub IoT.

Você precisa Olá **iothubowner** cadeia de conexão do seu IoT Hub toocomplete nesta seção. Você pode encontrar a cadeia de caracteres de conexão Olá no hello [portal do Azure](https://portal.azure.com/) em Olá **política de acesso compartilhado** folha.

1. Crie um projeto Maven chamado **leitura-arquivo de carregamento de notificação** usando Olá comando no prompt de comando a seguir. Observe que esse é um comando único e longo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. No prompt de comando, navegue toohello novo `read-file-upload-notification` pasta.

1. Usando um editor de texto, abra Olá `pom.xml` arquivo hello `read-file-upload-notification` pasta e adicione Olá seguir dependência toohello **dependências** nó. Adicionando a dependência do hello permite Olá toouse **hub IOT-serviço-cliente java** pacote no toocommunicate seu aplicativo com o serviço de hub IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Você pode verificar a versão mais recente de saudação do **cliente de serviço iot** usando [pesquisa Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Salve e feche o hello `pom.xml` arquivo.

1. Usando um editor de texto, abra Olá `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` arquivo.

1. Adicione o seguinte Olá **importar** arquivo de toohello instruções:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. Adicionar Olá seguintes variáveis de nível de classe toohello **aplicativo** classe:

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. tooprint informações sobre o console de toohello de carregamento de arquivo hello, adicione o seguinte de saudação aninhados classe toohello **aplicativo** classe:

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

1. thread de saudação toostart que escuta as notificações de carregamento de arquivo, adicione Olá toohello de código a seguir **principal** método:

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

1. Salve e feche o hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` arquivo.

1. Olá toobuild do comando de uso a seguir de saudação **leitura-arquivo de carregamento de notificação** aplicativo e verifique se há erros:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Executar aplicativos Olá

Agora você está pronto toorun aplicativos de saudação.

Em um prompt de comando no hello `read-file-upload-notification` pasta, execute o comando a seguir de saudação:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

Em um prompt de comando no hello `simulated-device` pasta, execute o comando a seguir de saudação:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

Olá, seguinte captura de tela mostra a saída Olá de saudação **dispositivo simulado** aplicativo:

![Saída do aplicativo simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

Olá, seguinte captura de tela mostra a saída Olá de saudação **leitura-arquivo de carregamento de notificação** aplicativo:

![Saída do aplicativo read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

Você pode usar o hello tooview portal Olá carregado arquivo no contêiner de armazenamento de saudação configurado:

![Arquivo carregado](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como toouse Olá transferência recursos do IoT Hub toosimplify arquivo carregamentos de dispositivos. Você pode continuar tooexplore IoT hub recursos e cenários com hello artigos a seguir:

* [Criar um Hub IoT de modo programático][lnk-create-hub]
* [Introdução tooC SDK][lnk-c-sdk]
* [SDKs do Azure IoT][lnk-sdks]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Simulando um dispositivo com IoT Edge][lnk-iotedge]

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


