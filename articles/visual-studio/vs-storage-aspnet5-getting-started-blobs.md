---
title: "aaaGet de Introdução ao armazenamento de blob e o Visual Studio serviços conectados (ASP.NET Core) | Microsoft Docs"
description: "Como tooget iniciado usando o armazenamento de BLOBs do Azure em um projeto do Visual Studio ASP.NET Core depois de ter criado uma conta de armazenamento usando o Visual Studio conectada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8eedf331896b21658c7b30a68a4391d8d60cd729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="384ee-103">Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="384ee-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="384ee-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="384ee-104">Overview</span></span>
<span data-ttu-id="384ee-105">Este artigo descreve como tooget iniciado usando o armazenamento de BLOBs do Azure no Visual Studio depois que você criou ou referenciado uma conta de armazenamento do Azure em um projeto do ASP.NET Core usando Olá Visual Studio conectado de diálogo Adicionar serviços.</span><span class="sxs-lookup"><span data-stu-id="384ee-105">This article describes how tooget started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="384ee-106">Armazenamento de BLOBs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="384ee-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="384ee-107">Um único blob pode ter qualquer tamanho.</span><span class="sxs-lookup"><span data-stu-id="384ee-107">A single blob can be any size.</span></span> <span data-ttu-id="384ee-108">Blobs podem ser coisas como imagens, arquivos de áudio e vídeo, dados brutos e arquivos de documentos.</span><span class="sxs-lookup"><span data-stu-id="384ee-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="384ee-109">Este artigo descreve como tooget iniciada com o armazenamento de blob depois de criar uma conta de armazenamento do Azure usando o Visual Studio de saudação **adicionar serviços conectados** caixa de diálogo em um projeto do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="384ee-109">This article describes how tooget started with blob storage after you create an Azure storage account by using hello Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="384ee-110">Assim como arquivos residem em pastas, blobs de armazenamento residem em contêineres.</span><span class="sxs-lookup"><span data-stu-id="384ee-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="384ee-111">Depois de criar um armazenamento, você cria um ou mais contêineres no armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="384ee-111">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="384ee-112">Por exemplo, em um armazenamento chamado "Livro de recortes", você pode criar contêineres em armazenamento Olá chamado imagens de toostore "imagens" e outro chamado "áudio" toostore arquivos de áudio.</span><span class="sxs-lookup"><span data-stu-id="384ee-112">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="384ee-113">Depois de criar contêineres de saudação, você pode carregar toothem de arquivos de blob individuais.</span><span class="sxs-lookup"><span data-stu-id="384ee-113">After you create hello containers, you can upload individual blob files toothem.</span></span> <span data-ttu-id="384ee-114">Consulte [Introdução ao Armazenamento de Blobs do Azure usando .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) para obter mais informações sobre como manipular blobs com programação.</span><span class="sxs-lookup"><span data-stu-id="384ee-114">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="384ee-115">Acessar contêineres de blob em código</span><span class="sxs-lookup"><span data-stu-id="384ee-115">Access blob containers in code</span></span>
<span data-ttu-id="384ee-116">tooprogrammatically acessar blobs em projetos do ASP.NET Core, é necessário tooadd Olá itens, a seguir se eles não ainda estiver presentes.</span><span class="sxs-lookup"><span data-stu-id="384ee-116">tooprogrammatically access blobs in ASP.NET Core projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="384ee-117">Adicione Olá código declarações de namespace toohello superior de qualquer arquivo c# no qual você deseja acesso tooprogrammatically armazenamento do Azure a seguir.</span><span class="sxs-lookup"><span data-stu-id="384ee-117">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="384ee-118">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="384ee-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="384ee-119">Use Olá tooget de código a seguir, sua cadeia de caracteres de conexão de armazenamento e as informações de conta de armazenamento da configuração de serviço do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="384ee-119">Use hello following code tooget your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="384ee-120">**Observação:** Use todos Olá acima código código Olá Olá seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="384ee-120">**NOTE:** Use all of hello above code in front of hello code in hello following sections.</span></span>
3. <span data-ttu-id="384ee-121">Use um **CloudBlobClient** objeto tooget um **CloudBlobContainer** contêiner existente do tooan de referência em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="384ee-121">Use a **CloudBlobClient** object tooget a **CloudBlobContainer** reference tooan existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="384ee-122">Criar um contêiner no código</span><span class="sxs-lookup"><span data-stu-id="384ee-122">Create a container in code</span></span>
<span data-ttu-id="384ee-123">Você também pode usar o hello **CloudBlobClient** toocreate um contêiner na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="384ee-123">You can also use hello **CloudBlobClient** toocreate a container in your storage account.</span></span> <span data-ttu-id="384ee-124">Você só precisa toodo é tooadd uma chamada muito**CreateIfNotExistsAsync** como Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="384ee-124">All you need toodo is tooadd a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="384ee-125">**Observação:** Olá APIs que executam chamadas tooAzure armazenamento no núcleo do ASP.NET são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="384ee-125">**NOTE:** hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="384ee-126">Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="384ee-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="384ee-127">código de saudação abaixo supõe que os métodos de programação assíncrona estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="384ee-127">hello code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="384ee-128">arquivos de saudação toomake dentro Olá contêiner disponível tooeveryone, você pode definir Olá contêiner toobe pública usando Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="384ee-128">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="384ee-129">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="384ee-129">Upload a blob into a container</span></span>
<span data-ttu-id="384ee-130">tooupload um arquivo de blob em um contêiner, obtenha uma referência de contêiner e usá-lo tooget uma referência de blob.</span><span class="sxs-lookup"><span data-stu-id="384ee-130">tooupload a blob file into a container, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="384ee-131">Depois de ter uma referência de blob, você pode carregar qualquer fluxo de dados tooit Olá chamada **UploadFromStreamAsync** método.</span><span class="sxs-lookup"><span data-stu-id="384ee-131">After you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="384ee-132">Essa operação cria blob Olá se ele não ainda estiver lá, ou substituí-lo se ele existir.</span><span class="sxs-lookup"><span data-stu-id="384ee-132">This operation creates hello blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="384ee-133">Olá mostrado no exemplo a seguir como tooupload um blob em um contêiner e supõe que esse contêiner Olá já foi criado.</span><span class="sxs-lookup"><span data-stu-id="384ee-133">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="384ee-134">Saudação de listar blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="384ee-134">List hello blobs in a container</span></span>
<span data-ttu-id="384ee-135">blobs de saudação toolist em um contêiner, primeiro obtenha uma referência de contêiner.</span><span class="sxs-lookup"><span data-stu-id="384ee-135">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="384ee-136">Em seguida, você pode chamar do contêiner Olá **ListBlobsSegmentedAsync** blobs de saudação do método tooretrieve e/ou diretórios dentro dele.</span><span class="sxs-lookup"><span data-stu-id="384ee-136">You can then call hello container's **ListBlobsSegmentedAsync** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="384ee-137">tooaccess Olá rico conjunto de propriedades e métodos para uma retornado **IListBlobItem**, você deve converter tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objeto.</span><span class="sxs-lookup"><span data-stu-id="384ee-137">tooaccess hello rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="384ee-138">Se você não souber o blob de saudação tipo, você pode usar um toodetermine de verificação de tipo que toocast-o para.</span><span class="sxs-lookup"><span data-stu-id="384ee-138">If you don't know hello blob type, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="384ee-139">saudação de código a seguir demonstra como tooretrieve e saída Olá URI de cada item em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="384ee-139">hello following code demonstrates how tooretrieve and output hello URI of each item in a container.</span></span>

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

<span data-ttu-id="384ee-140">Há-outros conteúdos de saudação toolist maneiras de um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="384ee-140">There are others ways toolist hello contents of a blob container.</span></span> <span data-ttu-id="384ee-141">Consulte [Introdução ao Armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="384ee-141">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="384ee-142">Baixar um blob</span><span class="sxs-lookup"><span data-stu-id="384ee-142">Download a blob</span></span>
<span data-ttu-id="384ee-143">toodownload um blob, primeiro obter um blob de toohello de referência e, em seguida, chamar hello **DownloadToStreamAsync** método.</span><span class="sxs-lookup"><span data-stu-id="384ee-143">toodownload a blob, first get a reference toohello blob, and then call hello **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="384ee-144">Olá, exemplo a seguir usa Olá **DownloadToStreamAsync** método tootransfer Olá conteúdo tooa fluxo objeto blob que você pode salvar como um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="384ee-144">hello following example uses hello **DownloadToStreamAsync** method tootransfer hello blob contents tooa stream object that you can then save as a local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="384ee-145">Existem outras maneiras toosave blobs como arquivos.</span><span class="sxs-lookup"><span data-stu-id="384ee-145">There are other ways toosave blobs as files.</span></span> <span data-ttu-id="384ee-146">Consulte [Introdução ao Armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="384ee-146">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="384ee-147">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="384ee-147">Delete a blob</span></span>
<span data-ttu-id="384ee-148">toodelete um blob, primeiro obter um blob de toohello de referência e, em seguida, chamar hello **DeleteAsync** método nele.</span><span class="sxs-lookup"><span data-stu-id="384ee-148">toodelete a blob, first get a reference toohello blob, and then call hello **DeleteAsync** method on it.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="384ee-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="384ee-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

