---
title: arquivos de aaaUpload de tooAzure dispositivos IoT Hub com .NET | Microsoft Docs
description: "Como tooupload arquivos de uma dispositivo toohello nuvem usando o dispositivo IoT do Azure SDK para .NET. Os arquivos carregados são armazenados em um contêiner de Azure Storage Blob."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: elioda
ms.openlocfilehash: 07d555f6ba8b067bbd3233bc8eebaa220ad2388b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a>Carregar arquivos de seu dispositivo toohello nuvem com o IoT Hub usando .NET

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Este tutorial baseia-se em código Olá Olá [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-csharp-csharp-c2d.md) tooshow tutorial você como toouse Olá recursos de carregamento de arquivo do IoT Hub. Ele mostra como:

- Fornecer com segurança um URI de blob do Azure a um dispositivo para carregamento de um arquivo.
- Use Olá IoT Hub arquivo carregamento notificações tootrigger processar o arquivo de saudação em seu back-end do aplicativo.

Olá [começar com o IoT Hub](iot-hub-csharp-csharp-getstarted.md) e [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-csharp-csharp-c2d.md) tutoriais mostram Olá dispositivo para nuvem e nuvem para dispositivo mensagens funcionalidade básica de IoT Hub. Olá [mensagens de dispositivo para nuvem processo](iot-hub-csharp-csharp-process-d2c.md) tutorial descreve um mensagens de dispositivo para nuvem maneira tooreliably repositório no armazenamento de BLOBs do Azure. No entanto, em alguns cenários você não pode mapear facilmente dados Olá que enviam seus dispositivos em Olá relativamente pequeno dispositivo para nuvem mensagens de IoT Hub aceita. Por exemplo:

* Arquivos grandes que contêm imagens
* Vídeos
* Dados de vibração amostrados a alta frequência
* Alguma forma de dados pré-processados

Esses arquivos normalmente são processadas na nuvem hello usando ferramentas como em lote [do Azure Data Factory](../data-factory/index.md) ou hello [Hadoop](../hdinsight/index.md) pilha. Quando você precisar tooupload arquivos de um dispositivo, você ainda pode usar segurança hello e a confiabilidade do IoT Hub.

Olá final deste tutorial você executadas dois aplicativos de console .NET:

* **SimulatedDevice**, uma versão modificada do aplicativo hello criado no hello [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial. Este aplicativo carrega um toostorage de arquivo usando um URI de SAS fornecido pelo seu hub IoT.
* **ReadFileUploadNotification**, que recebe notificações de carregamento de arquivo de seu Hub IoT.

> [!NOTE]
> O Hub IoT é compatível com muitas plataformas de dispositivo e linguagens (incluindo C, Java e Javascript) por meio dos SDKs do dispositivo IoT do Azure. Consulte toohello [Centro de desenvolvedores do Azure IoT] para obter instruções passo a passo sobre como tooconnect tooAzure seu dispositivo IoT Hub.

toocomplete neste tutorial, você precisa Olá a seguir:

* Visual Studio 2015 ou Visual Studio 2017
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Carregar um arquivo de um aplicativo de dispositivo

Nesta seção, você modificar o aplicativo para dispositivo Olá criado na [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive mensagens de nuvem para dispositivo do hub IoT de saudação.

1. No Visual Studio, clique com botão direito Olá **SimulatedDevice** de projeto, clique em **adicionar**e, em seguida, clique em **Item existente**. Navegue tooan arquivo de imagem e incluí-lo em seu projeto. Este tutorial assume imagem Olá é chamada `image.jpg`.

1. Clique na imagem de saudação e, em seguida, clique em **propriedades**. Verifique se **copiar tooOutput diretório** está definido muito**copiar sempre**.

    ![][1]

1. Em Olá **Program.cs** de arquivo, adicione Olá seguindo as instruções na parte superior de saudação do arquivo hello:

    ```csharp
    using System.IO;
    ```

1. Adicionar Olá após o método toohello **programa** classe:

    ```csharp
    private static async void SendToBlobAsync()
    {
        string fileName = "image.jpg";
        Console.WriteLine("Uploading file: {0}", fileName);
        var watch = System.Diagnostics.Stopwatch.StartNew();

        using (var sourceData = new FileStream(@"image.jpg", FileMode.Open))
        {
            await deviceClient.UploadToBlobAsync(fileName, sourceData);
        }

        watch.Stop();
        Console.WriteLine("Time tooupload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    Olá `UploadToBlobAsync` método usa o nome de arquivo hello e origem do fluxo de toobe de arquivo hello carregados e manipula Olá toostorage de carregamento. aplicativo de console Olá exibe Olá tempo arquivo de saudação tooupload.

1. Adicionar Olá seguinte método em Olá **principal** método antes de saudação `Console.ReadLine()` linha:

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> Para simplificar, este tutorial não implementa nenhuma política de repetição. No código de produção, você deve implementar políticas de repetição (por exemplo, a retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].

## <a name="receive-a-file-upload-notification"></a>Receber uma notificação de upload de arquivo

Nesta seção, você escreverá um aplicativo de console do .NET que recebe mensagens de notificação de upload de arquivo do Hub IoT.

1. Na solução atual do Visual Studio hello, criar um projeto do Visual c# Windows usando Olá **aplicativo de Console** modelo de projeto. Projeto de saudação do nome **ReadFileUploadNotification**.

    ![Novo projeto no Visual Studio][2]

1. No Gerenciador de soluções, clique com botão direito Olá **ReadFileUploadNotification** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .

1. Em Olá **NuGet Package Manager** janela, procure **Microsoft.Azure.Devices**, clique em **instalar**e aceite os termos de uso do hello.

    Essa ação baixa, instala e adiciona uma referência toohello [pacote de NuGet do SDK do serviço de Azure IoT] em Olá **ReadFileUploadNotification** projeto.

1. Em Olá **Program.cs** de arquivo, adicione Olá seguindo as instruções na parte superior de saudação do arquivo hello:

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. Adicionar Olá toohello campos a seguir **programa** classe. Substituir valor de espaço reservado de saudação com a cadeia de conexão do hello IoT hub do [começar com o IoT Hub]:

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. Adicionar Olá após o método toohello **programa** classe:

    ```csharp
    private async static void ReceiveFileUploadNotificationAsync()
    {
        var notificationReceiver = serviceClient.GetFileNotificationReceiver();

        Console.WriteLine("\nReceiving file upload notification from service");
        while (true)
        {
            var fileUploadNotification = await notificationReceiver.ReceiveAsync();
            if (fileUploadNotification == null) continue;

            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("Received file upload noticiation: {0}", string.Join(", ", fileUploadNotification.BlobName));
            Console.ResetColor();

            await notificationReceiver.CompleteAsync(fileUploadNotification);
        }
    }
    ```

    Observe que esse padrão de recebimento é Olá mensagens de nuvem para dispositivo tooreceive usado um mesmo do aplicativo de dispositivo de saudação.

1. Finalmente, adicione Olá toohello linhas a seguir **principal** método:

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Executar aplicativos Olá

Agora você está pronto toorun aplicativos de saudação.

1. No Visual Studio, clique com o botão direito para a solução e selecione **Definir projetos de inicialização**. Selecione **vários projetos de inicialização**, em seguida, selecione Olá **iniciar** ação para **ReadFileUploadNotification** e **SimulatedDevice**.

1. Pressione **F5**. Ambos os aplicativos devem ser iniciados. Você deve ver o carregamento Olá concluída no aplicativo de console e Olá a mensagem de notificação de carregamento Olá recebida por outro aplicativo de console. Você pode usar o hello [portal do Azure] ou Visual Studio Server Explorer toocheck presença Olá Olá carregado o arquivo em sua conta de armazenamento do Azure.

    ![][50]

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

<!-- Links -->

[portal do Azure]: https://portal.azure.com/

[Centro de desenvolvedores do Azure IoT]: http://www.azure.com/develop/iot

[tratamento de falhas transitórias]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[pacote de NuGet do SDK do serviço de Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
