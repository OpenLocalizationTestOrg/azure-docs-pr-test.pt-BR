---
title: "aaaGet de Introdução ao armazenamento de blob e o Visual Studio serviços conectados (serviços de nuvem) | Microsoft Docs"
description: "Como tooget iniciado usando o armazenamento de BLOBs do Azure em um projeto de serviço de nuvem no Visual Studio depois de conectar-se a conta de armazenamento tooa usando o Visual Studio conectada a serviços"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 62fb7fcff0a90008859ebe23755f13ef0555e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="0c012-103">Introdução ao Armazenamento de Blob do Azure e aos serviços conectados do Visual Studio (projetos de serviços de nuvem)</span><span class="sxs-lookup"><span data-stu-id="0c012-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="0c012-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0c012-104">Overview</span></span>
<span data-ttu-id="0c012-105">Este artigo descreve como tooget iniciada com o armazenamento de Blob do Azure após a criação ou referenciado uma conta de armazenamento do Azure usando o Visual Studio de saudação **adicionar serviços conectados** projeto dos serviços de caixa de diálogo em uma nuvem do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0c012-105">This article describes how tooget started with Azure Blob Storage after you created or referenced an Azure Storage account by using hello Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="0c012-106">Mostraremos como tooaccess e criar contêineres de blob e como tarefas comuns de tooperform deseja carregar, listar e baixar blobs.</span><span class="sxs-lookup"><span data-stu-id="0c012-106">We'll show you how tooaccess and create blob containers, and how tooperform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="0c012-107">exemplos de saudação são escritos em C\# e usar Olá [biblioteca de cliente de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c012-107">hello samples are written in C\# and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="0c012-108">Armazenamento de BLOBs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0c012-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="0c012-109">Um único blob pode ter qualquer tamanho.</span><span class="sxs-lookup"><span data-stu-id="0c012-109">A single blob can be any size.</span></span> <span data-ttu-id="0c012-110">Blobs podem ser coisas como imagens, arquivos de áudio e vídeo, dados brutos e arquivos de documentos.</span><span class="sxs-lookup"><span data-stu-id="0c012-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="0c012-111">Assim como arquivos residem em pastas, blobs de armazenamento residem em contêineres.</span><span class="sxs-lookup"><span data-stu-id="0c012-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="0c012-112">Depois de criar um armazenamento, você cria um ou mais contêineres no armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="0c012-112">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="0c012-113">Por exemplo, em um armazenamento chamado "Livro de recortes", você pode criar contêineres em armazenamento Olá chamado imagens de toostore "imagens" e outro chamado "áudio" toostore arquivos de áudio.</span><span class="sxs-lookup"><span data-stu-id="0c012-113">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="0c012-114">Depois de criar contêineres de saudação, você pode carregar toothem de arquivos de blob individuais.</span><span class="sxs-lookup"><span data-stu-id="0c012-114">After you create hello containers, you can upload individual blob files toothem.</span></span>

* <span data-ttu-id="0c012-115">Para obter mais informações sobre a manipulação de bobs com programação, consulte a [Introdução ao Armazenamento de Blobs do Azure usando .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="0c012-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="0c012-116">Para obter informações gerais sobre o Armazenamento do Azure, consulte a [documentação do Armazenamento](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="0c012-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="0c012-117">Para obter informações gerais sobre os Serviços de Nuvem do Azure, consulte a [documentação dos Serviços de Nuvem](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="0c012-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="0c012-118">Para saber mais sobre como programar aplicativos ASP.NET, consulte [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="0c012-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="0c012-119">Acessar contêineres de blob em código</span><span class="sxs-lookup"><span data-stu-id="0c012-119">Access blob containers in code</span></span>
<span data-ttu-id="0c012-120">tooprogrammatically acessar blobs em projetos de serviço de nuvem, você precisa de saudação tooadd itens, a seguir se eles não ainda estiver presentes.</span><span class="sxs-lookup"><span data-stu-id="0c012-120">tooprogrammatically access blobs in cloud service projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="0c012-121">Adicione Olá código declarações de namespace toohello superior de qualquer arquivo c# no qual você deseja acesso tooprogrammatically armazenamento do Azure a seguir.</span><span class="sxs-lookup"><span data-stu-id="0c012-121">Add hello following code namespace declarations toohello top of any C# file in which you wish tooprogrammatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="0c012-122">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0c012-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="0c012-123">Saudação de uso tooget de código a seguir Olá sua cadeia de caracteres de conexão de armazenamento e as informações de conta de armazenamento da configuração de serviço do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c012-123">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="0c012-124">Obter um **CloudBlobClient** tooreference um contêiner existente na sua conta de armazenamento do objeto.</span><span class="sxs-lookup"><span data-stu-id="0c012-124">Get a **CloudBlobClient** object tooreference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="0c012-125">Obter um **CloudBlobContainer** tooreference um contêiner de blob específico do objeto.</span><span class="sxs-lookup"><span data-stu-id="0c012-125">Get a **CloudBlobContainer** object tooreference a specific blob container.</span></span>
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="0c012-126">Use todo código Olá mostrado no procedimento anterior de saudação na frente do código Olá mostrado Olá seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="0c012-126">Use all of hello code shown in hello previous procedure in front of hello code shown in hello following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="0c012-127">Criar um contêiner no código</span><span class="sxs-lookup"><span data-stu-id="0c012-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="0c012-128">Algumas APIs que executam chamadas tooAzure armazenamento no ASP.NET são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="0c012-128">Some APIs that perform calls out tooAzure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="0c012-129">Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="0c012-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="0c012-130">código Olá Olá exemplo a seguir supõe que você esteja usando métodos de programação assíncrona.</span><span class="sxs-lookup"><span data-stu-id="0c012-130">hello code in hello following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="0c012-131">toocreate um contêiner na conta de armazenamento, tudo o que você precisa toodo é adicionar uma chamada muito**CreateIfNotExistsAsync** como Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c012-131">toocreate a container in your storage account, all you need toodo is add a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="0c012-132">arquivos de saudação toomake dentro Olá contêiner disponível tooeveryone, você pode definir Olá contêiner toobe pública usando Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="0c012-132">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="0c012-133">Qualquer pessoa na Internet de saudação pode ver os blobs em um contêiner público, mas você pode modificar ou excluí-los somente se você tiver a chave de acesso apropriadas de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c012-133">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="0c012-134">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="0c012-134">Upload a blob into a container</span></span>
<span data-ttu-id="0c012-135">O Armazenamento do Azure dá suporte a blobs de blocos e a blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="0c012-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="0c012-136">Na maioria Olá dos casos, blob de blocos é hello recomendado toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="0c012-136">In hello majority of cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="0c012-137">tooupload um blob de blocos de tooa de arquivo, obtenha uma referência de contêiner e usá-lo tooget uma referência de blob de bloco.</span><span class="sxs-lookup"><span data-stu-id="0c012-137">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="0c012-138">Quando você tem uma referência de blob, você pode carregar qualquer fluxo de dados tooit Olá chamada **UploadFromStream** método.</span><span class="sxs-lookup"><span data-stu-id="0c012-138">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="0c012-139">Essa operação cria blob Olá se ela não existia anteriormente ou substituí-lo se ele existir.</span><span class="sxs-lookup"><span data-stu-id="0c012-139">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="0c012-140">Olá mostrado no exemplo a seguir como tooupload um blob em um contêiner e supõe que esse contêiner Olá já foi criado.</span><span class="sxs-lookup"><span data-stu-id="0c012-140">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="0c012-141">Saudação de listar blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="0c012-141">List hello blobs in a container</span></span>
<span data-ttu-id="0c012-142">blobs de saudação toolist em um contêiner, primeiro obtenha uma referência de contêiner.</span><span class="sxs-lookup"><span data-stu-id="0c012-142">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="0c012-143">Você pode usar do contêiner Olá **ListBlobs** blobs de saudação do método tooretrieve e/ou diretórios dentro dele.</span><span class="sxs-lookup"><span data-stu-id="0c012-143">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="0c012-144">tooaccess Olá rico conjunto de propriedades e métodos para uma retornado **IListBlobItem**, você deve converter tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objeto.</span><span class="sxs-lookup"><span data-stu-id="0c012-144">tooaccess hello rich set of properties and methods for a  returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="0c012-145">Se o tipo de saudação for desconhecido, você pode usar um toodetermine de verificação de tipo que toocast-o para.</span><span class="sxs-lookup"><span data-stu-id="0c012-145">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="0c012-146">Olá código a seguir demonstra como tooretrieve e saída Olá URI de cada item em Olá **fotos** contêiner:</span><span class="sxs-lookup"><span data-stu-id="0c012-146">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **photos** container:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, false))
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

<span data-ttu-id="0c012-147">Conforme mostrado no exemplo de código anterior Olá, serviço de blob Olá tem conceito de saudação de diretórios em contêineres, também.</span><span class="sxs-lookup"><span data-stu-id="0c012-147">As shown in hello previous code sample, hello blob service has hello concept of directories within containers, as well.</span></span> <span data-ttu-id="0c012-148">Isso é para que você possa organizar seus blobs em uma estrutura mais semelhante a uma pasta.</span><span class="sxs-lookup"><span data-stu-id="0c012-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="0c012-149">Por exemplo, considere Olá após o conjunto de blobs de bloco em um contêiner chamado **fotos**:</span><span class="sxs-lookup"><span data-stu-id="0c012-149">For example, consider hello following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="0c012-150">Quando você chama **ListBlobs** no contêiner de saudação (como no exemplo anterior de saudação), coleção Olá retornada contém **CloudBlobDirectory** e **CloudBlockBlob** objetos que representam diretórios hello e blobs presentes no nível superior de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c012-150">When you call **ListBlobs** on hello container (as in hello previous sample), hello collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="0c012-151">Aqui está a saída resultante hello:</span><span class="sxs-lookup"><span data-stu-id="0c012-151">Here is hello resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="0c012-152">Opcionalmente, você pode definir Olá **UseFlatBlobListing** parâmetro de saudação **ListBlobs** método **true**.</span><span class="sxs-lookup"><span data-stu-id="0c012-152">Optionally, you can set hello **UseFlatBlobListing** parameter of of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="0c012-153">Isso resulta no retorno de cada blob como um **CloudBlockBlob**, independentemente do diretório.</span><span class="sxs-lookup"><span data-stu-id="0c012-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="0c012-154">Aqui está a chamada de saudação muito**ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="0c012-154">Here is hello call too**ListBlobs**:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="0c012-155">e estes são os resultados de saudação:</span><span class="sxs-lookup"><span data-stu-id="0c012-155">and here are hello results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="0c012-156">Para obter mais informações, consulte [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c012-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="0c012-157">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="0c012-157">Download blobs</span></span>
<span data-ttu-id="0c012-158">blobs toodownload, recuperar uma referência de blob e, em seguida, chamar hello **os métodos DownloadToStream** método.</span><span class="sxs-lookup"><span data-stu-id="0c012-158">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="0c012-159">Olá, exemplo a seguir usa Olá **os métodos DownloadToStream** método tootransfer Olá conteúdo tooa fluxo objeto blob que, em seguida, você pode persistir o arquivo local tooa.</span><span class="sxs-lookup"><span data-stu-id="0c012-159">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="0c012-160">Você também pode usar o hello **os métodos DownloadToStream** conteúdo de saudação do método toodownload de um blob como uma cadeia de caracteres de texto.</span><span class="sxs-lookup"><span data-stu-id="0c012-160">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="0c012-161">Excluir blobs</span><span class="sxs-lookup"><span data-stu-id="0c012-161">Delete blobs</span></span>
<span data-ttu-id="0c012-162">toodelete um blob, primeiro obter uma referência de blob e, em seguida, chame o **excluir** método.</span><span class="sxs-lookup"><span data-stu-id="0c012-162">toodelete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="0c012-163">Listar blobs em páginas de maneira assíncrona</span><span class="sxs-lookup"><span data-stu-id="0c012-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="0c012-164">Se estiver listando um grande número de blobs ou desejar toocontrol Olá número de resultados de que retorno em uma operação de listagem, você pode listar blobs em páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="0c012-164">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="0c012-165">Este exemplo mostra como tooreturn resulta em páginas de forma assíncrona, para que a execução não é bloqueada durante a espera tooreturn um grande conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="0c012-165">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="0c012-166">Este exemplo mostra uma simples listagem do blob, mas você também pode executar uma lista hierárquica, definindo Olá **useFlatBlobListing** parâmetro hello **ListBlobsSegmentedAsync** método muito **False**.</span><span class="sxs-lookup"><span data-stu-id="0c012-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello **useFlatBlobListing** parameter of hello **ListBlobsSegmentedAsync** method too**false**.</span></span>

<span data-ttu-id="0c012-167">Como o método de exemplo hello chama um método assíncrono, ela deve ser precedida por hello **async** palavra-chave e ele devem retornar um **tarefa** objeto.</span><span class="sxs-lookup"><span data-stu-id="0c012-167">Because hello sample method calls an asynchronous method, it must be prefaced with hello **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="0c012-168">Olá await palavra-chave especificada para Olá **ListBlobsSegmentedAsync** método suspende a execução do método de exemplo hello até Olá listagem tarefa ser concluída.</span><span class="sxs-lookup"><span data-stu-id="0c012-168">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get hello continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a><span data-ttu-id="0c012-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0c012-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

