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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a><span data-ttu-id="38836-104">Carregar arquivos de seu dispositivo toohello nuvem com o IoT Hub usando .NET</span><span class="sxs-lookup"><span data-stu-id="38836-104">Upload files from your device toohello cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="38836-105">Este tutorial baseia-se em código Olá Olá [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-csharp-csharp-c2d.md) tooshow tutorial você como toouse Olá recursos de carregamento de arquivo do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="38836-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial tooshow you how toouse hello file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="38836-106">Ele mostra como:</span><span class="sxs-lookup"><span data-stu-id="38836-106">It shows you how to:</span></span>

- <span data-ttu-id="38836-107">Fornecer com segurança um URI de blob do Azure a um dispositivo para carregamento de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="38836-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="38836-108">Use Olá IoT Hub arquivo carregamento notificações tootrigger processar o arquivo de saudação em seu back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38836-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="38836-109">Olá [começar com o IoT Hub](iot-hub-csharp-csharp-getstarted.md) e [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-csharp-csharp-c2d.md) tutoriais mostram Olá dispositivo para nuvem e nuvem para dispositivo mensagens funcionalidade básica de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="38836-109">hello [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="38836-110">Olá [mensagens de dispositivo para nuvem processo](iot-hub-csharp-csharp-process-d2c.md) tutorial descreve um mensagens de dispositivo para nuvem maneira tooreliably repositório no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="38836-110">hello [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="38836-111">No entanto, em alguns cenários você não pode mapear facilmente dados Olá que enviam seus dispositivos em Olá relativamente pequeno dispositivo para nuvem mensagens de IoT Hub aceita.</span><span class="sxs-lookup"><span data-stu-id="38836-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="38836-112">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="38836-112">For example:</span></span>

* <span data-ttu-id="38836-113">Arquivos grandes que contêm imagens</span><span class="sxs-lookup"><span data-stu-id="38836-113">Large files that contain images</span></span>
* <span data-ttu-id="38836-114">Vídeos</span><span class="sxs-lookup"><span data-stu-id="38836-114">Videos</span></span>
* <span data-ttu-id="38836-115">Dados de vibração amostrados a alta frequência</span><span class="sxs-lookup"><span data-stu-id="38836-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="38836-116">Alguma forma de dados pré-processados</span><span class="sxs-lookup"><span data-stu-id="38836-116">Some form of preprocessed data</span></span>

<span data-ttu-id="38836-117">Esses arquivos normalmente são processadas na nuvem hello usando ferramentas como em lote [do Azure Data Factory](../data-factory/index.md) ou hello [Hadoop](../hdinsight/index.md) pilha.</span><span class="sxs-lookup"><span data-stu-id="38836-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="38836-118">Quando você precisar tooupload arquivos de um dispositivo, você ainda pode usar segurança hello e a confiabilidade do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="38836-118">When you need tooupload files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="38836-119">Olá final deste tutorial você executadas dois aplicativos de console .NET:</span><span class="sxs-lookup"><span data-stu-id="38836-119">At hello end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="38836-120">**SimulatedDevice**, uma versão modificada do aplicativo hello criado no hello [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="38836-120">**SimulatedDevice**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="38836-121">Este aplicativo carrega um toostorage de arquivo usando um URI de SAS fornecido pelo seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="38836-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="38836-122">**ReadFileUploadNotification**, que recebe notificações de carregamento de arquivo de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="38836-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="38836-123">O Hub IoT é compatível com muitas plataformas de dispositivo e linguagens (incluindo C, Java e Javascript) por meio dos SDKs do dispositivo IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="38836-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="38836-124">Consulte toohello [Centro de desenvolvedores do Azure IoT] para obter instruções passo a passo sobre como tooconnect tooAzure seu dispositivo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="38836-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="38836-125">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="38836-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="38836-126">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="38836-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="38836-127">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="38836-127">An active Azure account.</span></span> <span data-ttu-id="38836-128">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="38836-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="38836-129">Carregar um arquivo de um aplicativo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="38836-129">Upload a file from a device app</span></span>

<span data-ttu-id="38836-130">Nesta seção, você modificar o aplicativo para dispositivo Olá criado na [enviar mensagens de nuvem para dispositivo com o IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive mensagens de nuvem para dispositivo do hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="38836-130">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="38836-131">No Visual Studio, clique com botão direito Olá **SimulatedDevice** de projeto, clique em **adicionar**e, em seguida, clique em **Item existente**.</span><span class="sxs-lookup"><span data-stu-id="38836-131">In Visual Studio, right-click hello **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="38836-132">Navegue tooan arquivo de imagem e incluí-lo em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="38836-132">Navigate tooan image file and include it in your project.</span></span> <span data-ttu-id="38836-133">Este tutorial assume imagem Olá é chamada `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="38836-133">This tutorial assumes hello image is named `image.jpg`.</span></span>

1. <span data-ttu-id="38836-134">Clique na imagem de saudação e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="38836-134">Right-click on hello image, and then click **Properties**.</span></span> <span data-ttu-id="38836-135">Verifique se **copiar tooOutput diretório** está definido muito**copiar sempre**.</span><span class="sxs-lookup"><span data-stu-id="38836-135">Make sure that **Copy tooOutput Directory** is set too**Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="38836-136">Em Olá **Program.cs** de arquivo, adicione Olá seguindo as instruções na parte superior de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="38836-136">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="38836-137">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="38836-137">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="38836-138">Olá `UploadToBlobAsync` método usa o nome de arquivo hello e origem do fluxo de toobe de arquivo hello carregados e manipula Olá toostorage de carregamento.</span><span class="sxs-lookup"><span data-stu-id="38836-138">hello `UploadToBlobAsync` method takes in hello file name and stream source of hello file toobe uploaded and handles hello upload toostorage.</span></span> <span data-ttu-id="38836-139">aplicativo de console Olá exibe Olá tempo arquivo de saudação tooupload.</span><span class="sxs-lookup"><span data-stu-id="38836-139">hello console app displays hello time it takes tooupload hello file.</span></span>

1. <span data-ttu-id="38836-140">Adicionar Olá seguinte método em Olá **principal** método antes de saudação `Console.ReadLine()` linha:</span><span class="sxs-lookup"><span data-stu-id="38836-140">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="38836-141">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="38836-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="38836-142">No código de produção, você deve implementar políticas de repetição (por exemplo, a retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias].</span><span class="sxs-lookup"><span data-stu-id="38836-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="38836-143">Receber uma notificação de upload de arquivo</span><span class="sxs-lookup"><span data-stu-id="38836-143">Receive a file upload notification</span></span>

<span data-ttu-id="38836-144">Nesta seção, você escreverá um aplicativo de console do .NET que recebe mensagens de notificação de upload de arquivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="38836-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="38836-145">Na solução atual do Visual Studio hello, criar um projeto do Visual c# Windows usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="38836-145">In hello current Visual Studio solution, create a Visual C# Windows project by using hello **Console Application** project template.</span></span> <span data-ttu-id="38836-146">Projeto de saudação do nome **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="38836-146">Name hello project **ReadFileUploadNotification**.</span></span>

    ![Novo projeto no Visual Studio][2]

1. <span data-ttu-id="38836-148">No Gerenciador de soluções, clique com botão direito Olá **ReadFileUploadNotification** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="38836-148">In Solution Explorer, right-click hello **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="38836-149">Em Olá **NuGet Package Manager** janela, procure **Microsoft.Azure.Devices**, clique em **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="38836-149">In hello **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span>

    <span data-ttu-id="38836-150">Essa ação baixa, instala e adiciona uma referência toohello [pacote de NuGet do SDK do serviço de Azure IoT] em Olá **ReadFileUploadNotification** projeto.</span><span class="sxs-lookup"><span data-stu-id="38836-150">This action downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package] in hello **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="38836-151">Em Olá **Program.cs** de arquivo, adicione Olá seguindo as instruções na parte superior de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="38836-151">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="38836-152">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="38836-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="38836-153">Substituir valor de espaço reservado de saudação com a cadeia de conexão do hello IoT hub do [começar com o IoT Hub]:</span><span class="sxs-lookup"><span data-stu-id="38836-153">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="38836-154">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="38836-154">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="38836-155">Observe que esse padrão de recebimento é Olá mensagens de nuvem para dispositivo tooreceive usado um mesmo do aplicativo de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="38836-155">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>

1. <span data-ttu-id="38836-156">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="38836-156">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="38836-157">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="38836-157">Run hello applications</span></span>

<span data-ttu-id="38836-158">Agora você está pronto toorun aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="38836-158">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="38836-159">No Visual Studio, clique com o botão direito para a solução e selecione **Definir projetos de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="38836-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="38836-160">Selecione **vários projetos de inicialização**, em seguida, selecione Olá **iniciar** ação para **ReadFileUploadNotification** e **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="38836-160">Select **Multiple startup projects**, then select hello **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="38836-161">Pressione **F5**.</span><span class="sxs-lookup"><span data-stu-id="38836-161">Press **F5**.</span></span> <span data-ttu-id="38836-162">Ambos os aplicativos devem ser iniciados.</span><span class="sxs-lookup"><span data-stu-id="38836-162">Both applications should start.</span></span> <span data-ttu-id="38836-163">Você deve ver o carregamento Olá concluída no aplicativo de console e Olá a mensagem de notificação de carregamento Olá recebida por outro aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="38836-163">You should see hello upload completed in one console app and hello upload notification message received by hello other console app.</span></span> <span data-ttu-id="38836-164">Você pode usar o hello [portal do Azure] ou Visual Studio Server Explorer toocheck presença Olá Olá carregado o arquivo em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="38836-164">You can use hello [Azure portal] or Visual Studio Server Explorer toocheck for hello presence of hello uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="38836-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="38836-165">Next steps</span></span>

<span data-ttu-id="38836-166">Neste tutorial, você aprendeu como toouse Olá transferência recursos do IoT Hub toosimplify arquivo carregamentos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="38836-166">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="38836-167">Você pode continuar tooexplore IoT hub recursos e cenários com hello artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="38836-167">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="38836-168">[Criar um Hub IoT de modo programático][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="38836-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="38836-169">[Introdução tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="38836-169">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="38836-170">[SDKs do Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="38836-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="38836-171">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="38836-171">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="38836-172">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="38836-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

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
