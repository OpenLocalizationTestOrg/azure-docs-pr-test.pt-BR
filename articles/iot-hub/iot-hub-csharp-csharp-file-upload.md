---
title: Carregar arquivos de dispositivos para o Hub IoT do Azure com .NET | Microsoft Docs
description: "Como carregar arquivos de um dispositivo para a nuvem usando o SDK do dispositivo IoT do Azure para .NET. Os arquivos carregados são armazenados em um contêiner de Azure Storage Blob."
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
ms.openlocfilehash: b45d85d0d77cf47f36cb793bc8c0dbe2d5c12634
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub-using-net"></a><span data-ttu-id="45491-104">Carregar arquivos do seu dispositivo para a nuvem com o Hub IoT usando .NET</span><span class="sxs-lookup"><span data-stu-id="45491-104">Upload files from your device to the cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="45491-105">Este tutorial se baseia no código do tutorial [Como enviar mensagens da nuvem para o dispositivo com o Hub IoT](iot-hub-csharp-csharp-c2d.md) para mostrar como usar os recursos de carregamento de arquivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="45491-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial to show you how to use the file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="45491-106">Ele mostra como:</span><span class="sxs-lookup"><span data-stu-id="45491-106">It shows you how to:</span></span>

- <span data-ttu-id="45491-107">Fornecer com segurança um URI de blob do Azure a um dispositivo para carregamento de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="45491-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="45491-108">Usar as notificações de carregamento de arquivo do Hub IoT para disparar o processamento do arquivo no back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="45491-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="45491-109">Os tutoriais [Introdução ao Hub IoT](iot-hub-csharp-csharp-getstarted.md) e [Enviar mensagens da nuvem para o dispositivo com o Hub IoT](iot-hub-csharp-csharp-c2d.md) mostram a funcionalidade básica de mensagens do dispositivo para a nuvem e da nuvem para o dispositivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="45491-109">The [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="45491-110">O tutorial [Processar mensagens do dispositivo para a nuvem](iot-hub-csharp-csharp-process-d2c.md) descreve uma forma de armazenamento confiável das mensagens do dispositivo para a nuvem no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="45491-110">The [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="45491-111">No entanto, em alguns cenários você não pode mapear facilmente os dados que seus dispositivos enviam em mensagens relativamente menores do dispositivo para a nuvem que o Hub IoT aceita.</span><span class="sxs-lookup"><span data-stu-id="45491-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="45491-112">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="45491-112">For example:</span></span>

* <span data-ttu-id="45491-113">Arquivos grandes que contêm imagens</span><span class="sxs-lookup"><span data-stu-id="45491-113">Large files that contain images</span></span>
* <span data-ttu-id="45491-114">Vídeos</span><span class="sxs-lookup"><span data-stu-id="45491-114">Videos</span></span>
* <span data-ttu-id="45491-115">Dados de vibração amostrados a alta frequência</span><span class="sxs-lookup"><span data-stu-id="45491-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="45491-116">Alguma forma de dados pré-processados</span><span class="sxs-lookup"><span data-stu-id="45491-116">Some form of preprocessed data</span></span>

<span data-ttu-id="45491-117">Esses arquivos normalmente são processados em lote na nuvem usando ferramentas como o [Azure Data Factory](../data-factory/index.md) ou a pilha do [Hadoop](../hdinsight/index.md).</span><span class="sxs-lookup"><span data-stu-id="45491-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/index.md) or the [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="45491-118">Quando você precisar carregar arquivos de um dispositivo, ainda poderá usar a segurança e a confiabilidade do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="45491-118">When you need to upload files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="45491-119">No final deste tutorial, você executará dois aplicativos do console .NET:</span><span class="sxs-lookup"><span data-stu-id="45491-119">At the end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="45491-120">**SimulatedDevice**, uma versão modificada do aplicativo criado no tutorial [Como enviar mensagens da nuvem para o dispositivo com o Hub IoT](iot-hub-csharp-csharp-c2d.md).</span><span class="sxs-lookup"><span data-stu-id="45491-120">**SimulatedDevice**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="45491-121">Esse aplicativo carrega um arquivo no armazenamento usando um URI SAS fornecido pelo seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="45491-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="45491-122">**ReadFileUploadNotification**, que recebe notificações de carregamento de arquivo de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="45491-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="45491-123">O Hub IoT é compatível com muitas plataformas de dispositivo e linguagens (incluindo C, Java e Javascript) por meio dos SDKs do dispositivo IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="45491-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="45491-124">Confira a [Central de Desenvolvedores do IoT do Azure] para obter instruções passo a passo sobre como conectar seu dispositivo ao Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="45491-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="45491-125">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="45491-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="45491-126">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="45491-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="45491-127">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="45491-127">An active Azure account.</span></span> <span data-ttu-id="45491-128">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="45491-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="45491-129">Carregar um arquivo de um aplicativo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="45491-129">Upload a file from a device app</span></span>

<span data-ttu-id="45491-130">Nesta seção, você modifica o aplicativo do dispositivo criado em [Enviar mensagens da nuvem para o dispositivo com o Hub IoT](iot-hub-csharp-csharp-c2d.md) para receber mensagens da nuvem para o dispositivo do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="45491-130">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="45491-131">No Visual Studio, clique com o botão direito no projeto **SimulatedDevice**, clique em **Adicionar** e, em seguida, clique em **Item Existente**.</span><span class="sxs-lookup"><span data-stu-id="45491-131">In Visual Studio, right-click the **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="45491-132">Navegue até um arquivo de imagem e inclua-o no projeto.</span><span class="sxs-lookup"><span data-stu-id="45491-132">Navigate to an image file and include it in your project.</span></span> <span data-ttu-id="45491-133">Este tutorial pressupõe que a imagem é denominada `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="45491-133">This tutorial assumes the image is named `image.jpg`.</span></span>

1. <span data-ttu-id="45491-134">Clique com o botão direito do mouse na imagem e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="45491-134">Right-click on the image, and then click **Properties**.</span></span> <span data-ttu-id="45491-135">Verifique se **Copiar para o Diretório de Saída** está definido como **Copiar sempre**.</span><span class="sxs-lookup"><span data-stu-id="45491-135">Make sure that **Copy to Output Directory** is set to **Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="45491-136">No arquivo **Program.cs** , adicione as seguintes instruções na parte superior do arquivo:</span><span class="sxs-lookup"><span data-stu-id="45491-136">In the **Program.cs** file, add the following statements at the top of the file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="45491-137">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="45491-137">Add the following method to the **Program** class:</span></span>

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
        Console.WriteLine("Time to upload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    <span data-ttu-id="45491-138">O método `UploadToBlobAsync` usa o nome de arquivo e a fonte de transmissão do arquivo a ser carregado e manipula o upload para o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="45491-138">The `UploadToBlobAsync` method takes in the file name and stream source of the file to be uploaded and handles the upload to storage.</span></span> <span data-ttu-id="45491-139">O aplicativo de console exibe o tempo necessário para carregar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="45491-139">The console app displays the time it takes to upload the file.</span></span>

1. <span data-ttu-id="45491-140">Adicione o seguinte método ao método **Main**, logo antes da linha `Console.ReadLine()`:</span><span class="sxs-lookup"><span data-stu-id="45491-140">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="45491-141">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="45491-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="45491-142">No código de produção, implemente políticas de repetição (como uma retirada exponencial), conforme sugestão no artigo [Transient Fault Handling](Tratamento de Falhas Transitórias) do MSDN.</span><span class="sxs-lookup"><span data-stu-id="45491-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="45491-143">Receber uma notificação de upload de arquivo</span><span class="sxs-lookup"><span data-stu-id="45491-143">Receive a file upload notification</span></span>

<span data-ttu-id="45491-144">Nesta seção, você escreverá um aplicativo de console do .NET que recebe mensagens de notificação de upload de arquivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="45491-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="45491-145">Na solução atual do Visual Studio, crie um projeto do Visual C# do Windows usando o modelo de projeto do **Aplicativo do Console** .</span><span class="sxs-lookup"><span data-stu-id="45491-145">In the current Visual Studio solution, create a Visual C# Windows project by using the **Console Application** project template.</span></span> <span data-ttu-id="45491-146">Nomeie o projeto **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="45491-146">Name the project **ReadFileUploadNotification**.</span></span>

    ![Novo projeto no Visual Studio][2]

1. <span data-ttu-id="45491-148">No Gerenciador de Soluções, clique com o botão direito no projeto **ReadFileUploadNotification** e, em seguida, clique em **Gerenciar Pacotes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="45491-148">In Solution Explorer, right-click the **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="45491-149">Na janela **Gerenciador de Pacotes NuGet**, procure **Microsoft.Azure.Devices**, clique em **Instalar** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="45491-149">In the **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span>

    <span data-ttu-id="45491-150">Essa ação baixa, instala e adiciona uma referência ao [pacote NuGet do SDK do serviço IoT do Azure] no projeto **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="45491-150">This action downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package] in the **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="45491-151">No arquivo **Program.cs** , adicione as seguintes instruções na parte superior do arquivo:</span><span class="sxs-lookup"><span data-stu-id="45491-151">In the **Program.cs** file, add the following statements at the top of the file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="45491-152">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="45491-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="45491-153">Substitua os valores de espaço reservado pela cadeia de conexão do Hub IoT da [Introdução ao Hub IoT]:</span><span class="sxs-lookup"><span data-stu-id="45491-153">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="45491-154">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="45491-154">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="45491-155">É importante lembrar que o padrão de recebimento é o mesmo usado para receber mensagens da nuvem para o dispositivo do aplicativo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="45491-155">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>

1. <span data-ttu-id="45491-156">Por fim, adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="45491-156">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter to exit\n");
    Console.ReadLine();
    ```

## <a name="run-the-applications"></a><span data-ttu-id="45491-157">Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="45491-157">Run the applications</span></span>

<span data-ttu-id="45491-158">Agora você está pronto para executar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="45491-158">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="45491-159">No Visual Studio, clique com o botão direito para a solução e selecione **Definir projetos de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="45491-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="45491-160">Selecione **Vários projetos de inicialização**, em seguida, selecione a ação **Iniciar** para **ReadFileUploadNotification** e **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="45491-160">Select **Multiple startup projects**, then select the **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="45491-161">Pressione **F5**.</span><span class="sxs-lookup"><span data-stu-id="45491-161">Press **F5**.</span></span> <span data-ttu-id="45491-162">Ambos os aplicativos devem ser iniciados.</span><span class="sxs-lookup"><span data-stu-id="45491-162">Both applications should start.</span></span> <span data-ttu-id="45491-163">Você deve ver o carregamento concluído em um aplicativo de console e a mensagem de notificação do carregamento sendo recebida pelo outro aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="45491-163">You should see the upload completed in one console app and the upload notification message received by the other console app.</span></span> <span data-ttu-id="45491-164">Você pode usar o [Portal do Azure] ou o Gerenciador de Servidores do Visual Studio para verificar a presença do arquivo carregado em sua conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="45491-164">You can use the [Azure portal] or Visual Studio Server Explorer to check for the presence of the uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="45491-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="45491-165">Next steps</span></span>

<span data-ttu-id="45491-166">Neste tutorial, você aprendeu a usar os recursos de carregamento de arquivo do Hub IoT para simplificar os carregamentos de arquivos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="45491-166">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="45491-167">Você pode continuar explorando os recursos e cenários do Hub IoT com os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="45491-167">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="45491-168">[Criar um Hub IoT de modo programático][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="45491-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="45491-169">[Introdução ao SDK de C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="45491-169">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="45491-170">[SDKs do Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="45491-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="45491-171">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="45491-171">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="45491-172">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="45491-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

<span data-ttu-id="45491-173">[Portal do Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="45491-173">[Azure portal]: https://portal.azure.com/</span></span>

<span data-ttu-id="45491-174">[Central de Desenvolvedores do IoT do Azure]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="45491-174">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>

<span data-ttu-id="45491-175">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="45491-175">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="45491-176">[pacote NuGet do SDK do serviço IoT do Azure]: https://www.nuget.org/packages/Microsoft.Azure.Devices/</span><span class="sxs-lookup"><span data-stu-id="45491-176">[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
