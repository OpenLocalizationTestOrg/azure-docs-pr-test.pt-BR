---
title: "Introdução ao armazenamento de blobs e aos serviços conectados do Visual Studio (ASP.NET Core) | Microsoft Docs"
description: "Como começar a usar o Armazenamento de Blobs do Azure em um projeto do ASP.NET Core no Visual Studio após a criação de uma conta de armazenamento usando os serviços conectados do Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: e725015c8be7ecfa908f0ae75986b73f218fa3ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="146bc-103">Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="146bc-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="146bc-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="146bc-104">Overview</span></span>
<span data-ttu-id="146bc-105">Este artigo descreve como começar a usar o armazenamento de Blobs do Azure no Visual Studio após a criação ou referência de uma conta de armazenamento do Azure em um projeto do ASP.NET Core usando o diálogo Adicionar Serviços Conectados do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="146bc-105">This article describes how to get started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="146bc-106">Armazenamento de Blob do Azure é um serviço para armazenar grandes quantidades de dados não estruturados que podem ser acessados de qualquer lugar do mundo por meio de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="146bc-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="146bc-107">Um único blob pode ter qualquer tamanho.</span><span class="sxs-lookup"><span data-stu-id="146bc-107">A single blob can be any size.</span></span> <span data-ttu-id="146bc-108">Blobs podem ser coisas como imagens, arquivos de áudio e vídeo, dados brutos e arquivos de documentos.</span><span class="sxs-lookup"><span data-stu-id="146bc-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="146bc-109">Este artigo descreve como começar a usar o armazenamento de blobs depois de criar uma conta de armazenamento do Azure usando a caixa de diálogo **Adicionar Serviços Conectados** do Visual Studio em um projeto do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="146bc-109">This article describes how to get started with blob storage after you create an Azure storage account by using the Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="146bc-110">Assim como arquivos residem em pastas, blobs de armazenamento residem em contêineres.</span><span class="sxs-lookup"><span data-stu-id="146bc-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="146bc-111">Após ter criado um armazenamento, crie um ou mais contêineres no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="146bc-111">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="146bc-112">Por exemplo, em um armazenamento chamado "Scrapbook", você pode criar contêineres no armazenamento chamados "imagens" para armazenar fotos e "áudio" para armazenar arquivos de áudio.</span><span class="sxs-lookup"><span data-stu-id="146bc-112">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="146bc-113">Depois de criar os contêineres, você poderá carregar arquivos de blob individuais para eles.</span><span class="sxs-lookup"><span data-stu-id="146bc-113">After you create the containers, you can upload individual blob files to them.</span></span> <span data-ttu-id="146bc-114">Consulte [Introdução ao Armazenamento de Blobs do Azure usando .NET](storage-dotnet-how-to-use-blobs.md) para obter mais informações sobre como manipular blobs com programação.</span><span class="sxs-lookup"><span data-stu-id="146bc-114">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="146bc-115">Acessar contêineres de blob em código</span><span class="sxs-lookup"><span data-stu-id="146bc-115">Access blob containers in code</span></span>
<span data-ttu-id="146bc-116">Para acessar programaticamente blobs em projetos do ASP.NET Core, você precisará adicionar os itens a seguir, se eles ainda não existirem.</span><span class="sxs-lookup"><span data-stu-id="146bc-116">To programmatically access blobs in ASP.NET Core projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="146bc-117">Adicione as seguintes declarações de namespace de código à parte superior de qualquer arquivo C# no qual você queira acessar o armazenamento do Azure por meio de programação.</span><span class="sxs-lookup"><span data-stu-id="146bc-117">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="146bc-118">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="146bc-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="146bc-119">Use o seguinte código para obter a sua cadeia de conexão de armazenamento e informações sobre a conta de armazenamento da configuração do serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="146bc-119">Use the following code to get your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="146bc-120">**OBSERVAÇÃO:** use todo esse código acima antes do código nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="146bc-120">**NOTE:** Use all of the above code in front of the code in the following sections.</span></span>
3. <span data-ttu-id="146bc-121">Use um objeto **CloudBlobClient** para obter uma referência **CloudBlobContainer** a um contêiner existente em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="146bc-121">Use a **CloudBlobClient** object to get a **CloudBlobContainer** reference to an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="146bc-122">Criar um contêiner no código</span><span class="sxs-lookup"><span data-stu-id="146bc-122">Create a container in code</span></span>
<span data-ttu-id="146bc-123">Você também pode usar o **CloudBlobClient** para criar um contêiner na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="146bc-123">You can also use the **CloudBlobClient** to create a container in your storage account.</span></span> <span data-ttu-id="146bc-124">Basta adicionar uma chamada para **CreateIfNotExistsAsync** , como no seguinte código:</span><span class="sxs-lookup"><span data-stu-id="146bc-124">All you need to do is to add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="146bc-125">**OBSERVAÇÃO:** as APIs que executam chamadas para o armazenamento do Azure no ASP.NET Core são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="146bc-125">**NOTE:** The APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="146bc-126">Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="146bc-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="146bc-127">O código a seguir pressupõe que os métodos de programação assíncrona estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="146bc-127">The code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="146bc-128">Se quiser tornar os arquivos dentro do contêiner disponíveis a todos, basta definir o contêiner como público usando o seguinte código.</span><span class="sxs-lookup"><span data-stu-id="146bc-128">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="146bc-129">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="146bc-129">Upload a blob into a container</span></span>
<span data-ttu-id="146bc-130">Para carregar um arquivo de blob para um contêiner, obtenha uma referência de contêiner e use-a para obter uma referência de blob.</span><span class="sxs-lookup"><span data-stu-id="146bc-130">To upload a blob file into a container, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="146bc-131">Depois que tiver uma referência de blob, você poderá carregar qualquer fluxo de dados nele chamando o método **UploadFromStreamAsync** .</span><span class="sxs-lookup"><span data-stu-id="146bc-131">After you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="146bc-132">Essa operação criará o blob, caso ele não exista ou o substituirá, caso ele já exista.</span><span class="sxs-lookup"><span data-stu-id="146bc-132">This operation creates the blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="146bc-133">O exemplo a seguir mostra como carregar um blob em um contêiner e pressupõe que o contêiner já tenha sido criado.</span><span class="sxs-lookup"><span data-stu-id="146bc-133">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="146bc-134">Listar os blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="146bc-134">List the blobs in a container</span></span>
<span data-ttu-id="146bc-135">Para listar blobs em um contêiner, primeiro obtenha uma referência ao contêiner.</span><span class="sxs-lookup"><span data-stu-id="146bc-135">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="146bc-136">Depois, você pode usar o método **ListBlobsSegmentedAsync** do contêiner para recuperar os blobs e/ou diretórios nele contidos.</span><span class="sxs-lookup"><span data-stu-id="146bc-136">You can then call the container's **ListBlobsSegmentedAsync** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="146bc-137">Para acessar o conjunto avançado de propriedades e de métodos para um **IListBlobItem** retornado, você deverá convertê-lo em um objeto **CloudBlockBlob**, **CloudPageBlob** ou **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="146bc-137">To access the rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="146bc-138">Se o tipo de blob for desconhecido, você poderá usar uma verificação de tipo para determinar em qual outro tipo convertê-lo.</span><span class="sxs-lookup"><span data-stu-id="146bc-138">If you don't know the blob type, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="146bc-139">O código a seguir demonstra como recuperar e apresentar a saída do URI de cada item no contêiner.</span><span class="sxs-lookup"><span data-stu-id="146bc-139">The following code demonstrates how to retrieve and output the URI of each item in a container.</span></span>

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
        {
            if (item.GetType() == typeof(CloudBlockBlob))
            {
                CloudBlockBlob blob = (CloudBlockBlob)item;
                Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);
            }

            else if (item.GetType() == typeof(CloudPageBlob))
            {
                CloudPageBlob pageBlob = (CloudPageBlob)item;

                Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);
            }

            else if (item.GetType() == typeof(CloudBlobDirectory))
            {
                CloudBlobDirectory directory = (CloudBlobDirectory)item;

                Console.WriteLine("Directory: {0}", directory.Uri);
            }
        }
    } while (token != null);

<span data-ttu-id="146bc-140">Existem outras maneiras de listar o conteúdo de um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="146bc-140">There are others ways to list the contents of a blob container.</span></span> <span data-ttu-id="146bc-141">Consulte [Introdução ao Armazenamento de Blobs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="146bc-141">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="146bc-142">Baixar um blob</span><span class="sxs-lookup"><span data-stu-id="146bc-142">Download a blob</span></span>
<span data-ttu-id="146bc-143">Para baixar um blob, obtenha primeiro uma referência ao blob e depois chame o método **DownloadToStreamAsync** .</span><span class="sxs-lookup"><span data-stu-id="146bc-143">To download a blob, first get a reference to the blob, and then call the **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="146bc-144">O exemplo a seguir usa o método **DownloadToStreamAsync** para transferir o conteúdo do blob para um objeto de fluxo que pode então ser salvo como um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="146bc-144">The following example uses the **DownloadToStreamAsync** method to transfer the blob contents to a stream object that you can then save as a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="146bc-145">Existem outras maneiras de salvar blobs como arquivos.</span><span class="sxs-lookup"><span data-stu-id="146bc-145">There are other ways to save blobs as files.</span></span> <span data-ttu-id="146bc-146">Consulte [Introdução ao Armazenamento de Blobs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="146bc-146">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="146bc-147">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="146bc-147">Delete a blob</span></span>
<span data-ttu-id="146bc-148">Para excluir um blob, obtenha primeiro uma referência ao blob e depois chame o método **DeleteAsync** nele.</span><span class="sxs-lookup"><span data-stu-id="146bc-148">To delete a blob, first get a reference to the blob, and then call the **DeleteAsync** method on it.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="146bc-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="146bc-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

