---
title: "aaaGet de Introdução ao armazenamento de BLOBs do Azure (armazenamento de objeto) usando .NET | Microsoft Docs"
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 3df0cf14b69d85cdc2f62cc3c8b901be102fa026
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="b1024-103">Introdução ao Armazenamento de Blobs do Azure usando o .NET</span><span class="sxs-lookup"><span data-stu-id="b1024-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="b1024-104">Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="b1024-104">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="b1024-105">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b1024-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="b1024-106">Armazenamento de blob também é chamado tooas armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="b1024-106">Blob storage is also referred tooas object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="b1024-107">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="b1024-107">About this tutorial</span></span>
<span data-ttu-id="b1024-108">Este tutorial mostra como toowrite .NET código em alguns cenários comuns usando o armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1024-108">This tutorial shows how toowrite .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="b1024-109">Os cenários incluem upload, listagem, download e exclusão de blobs.</span><span class="sxs-lookup"><span data-stu-id="b1024-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="b1024-110">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="b1024-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="b1024-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b1024-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="b1024-112">Biblioteca do Cliente de Armazenamento do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="b1024-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="b1024-113">Gerenciador de Configurações do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="b1024-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="b1024-114">[Uma conta do Armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="b1024-114">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="b1024-115">Mais exemplos</span><span class="sxs-lookup"><span data-stu-id="b1024-115">More samples</span></span>
<span data-ttu-id="b1024-116">Para obter exemplos adicionais usando o Armazenamento de Blobs, confira [Introdução ao Armazenamento de Blobs do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="b1024-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="b1024-117">Você pode baixar o aplicativo de exemplo hello e executá-lo ou procurar Olá código no GitHub.</span><span class="sxs-lookup"><span data-stu-id="b1024-117">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="b1024-118">Adicionar diretivas using</span><span class="sxs-lookup"><span data-stu-id="b1024-118">Add using directives</span></span>
<span data-ttu-id="b1024-119">Adicione o seguinte Olá **usando** superior de toohello de diretivas de saudação `Program.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="b1024-119">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="b1024-120">Analisar a cadeia de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="b1024-120">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a><span data-ttu-id="b1024-121">Criar o cliente do serviço Blob Olá</span><span class="sxs-lookup"><span data-stu-id="b1024-121">Create hello Blob service client</span></span>
<span data-ttu-id="b1024-122">Olá **CloudBlobClient** classe permite que você tooretrieve contêineres e blobs armazenados no armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="b1024-122">hello **CloudBlobClient** class enables you tooretrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="b1024-123">Aqui está o cliente do serviço Olá toocreate unidirecional:</span><span class="sxs-lookup"><span data-stu-id="b1024-123">Here's one way toocreate hello service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="b1024-124">Agora você está pronto toowrite código lê e grava o armazenamento de tooBlob de dados.</span><span class="sxs-lookup"><span data-stu-id="b1024-124">Now you are ready toowrite code that reads data from and writes data tooBlob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="b1024-125">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="b1024-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="b1024-126">Este exemplo mostra como toocreate um contêiner se ele ainda não existir:</span><span class="sxs-lookup"><span data-stu-id="b1024-126">This example shows how toocreate a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="b1024-127">Por padrão, o novo contêiner de saudação é privado, o que significa que você deve especificar seus blobs de toodownload chave de acesso de armazenamento desse contêiner.</span><span class="sxs-lookup"><span data-stu-id="b1024-127">By default, hello new container is private, meaning that you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="b1024-128">Se você quiser toomake arquivos Olá Olá contêiner disponível tooeveryone, você pode definir Olá contêiner toobe pública usando Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="b1024-128">If you want toomake hello files within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="b1024-129">Qualquer pessoa na Internet de saudação pode ver os blobs em um contêiner público.</span><span class="sxs-lookup"><span data-stu-id="b1024-129">Anyone on hello Internet can see blobs in a public container.</span></span> <span data-ttu-id="b1024-130">No entanto, você pode modificar ou excluí-los somente se você tiver a chave de acesso de conta apropriada de saudação ou uma assinatura de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="b1024-130">However, you can modify or delete them only if you have hello appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="b1024-131">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="b1024-131">Upload a blob into a container</span></span>
<span data-ttu-id="b1024-132">O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="b1024-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="b1024-133">Na maioria dos casos, o blob de blocos é hello recomendado toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="b1024-133">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="b1024-134">tooupload um blob de blocos de tooa de arquivo, obtenha uma referência de contêiner e usá-lo tooget uma referência de blob de bloco.</span><span class="sxs-lookup"><span data-stu-id="b1024-134">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="b1024-135">Quando você tem uma referência de blob, você pode carregar qualquer fluxo de dados tooit Olá chamada **UploadFromStream** método.</span><span class="sxs-lookup"><span data-stu-id="b1024-135">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="b1024-136">Essa operação cria blob Olá se ela não existia anteriormente ou substituí-lo se ele existir.</span><span class="sxs-lookup"><span data-stu-id="b1024-136">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="b1024-137">Olá mostrado no exemplo a seguir como tooupload um blob em um contêiner e supõe que esse contêiner Olá já foi criado.</span><span class="sxs-lookup"><span data-stu-id="b1024-137">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="b1024-138">Saudação de listar blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="b1024-138">List hello blobs in a container</span></span>
<span data-ttu-id="b1024-139">blobs de saudação toolist em um contêiner, primeiro obtenha uma referência de contêiner.</span><span class="sxs-lookup"><span data-stu-id="b1024-139">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="b1024-140">Você pode usar do contêiner Olá **ListBlobs** blobs de saudação do método tooretrieve e/ou diretórios dentro dele.</span><span class="sxs-lookup"><span data-stu-id="b1024-140">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="b1024-141">tooaccess Olá rico conjunto de propriedades e métodos para uma retornado **IListBlobItem**, você deve converter tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objeto.</span><span class="sxs-lookup"><span data-stu-id="b1024-141">tooaccess hello  rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="b1024-142">Se o tipo de saudação for desconhecido, você pode usar um toodetermine de verificação de tipo que toocast-o para.</span><span class="sxs-lookup"><span data-stu-id="b1024-142">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="b1024-143">Olá código a seguir demonstra como tooretrieve e saída Olá URI de cada item em Olá _fotos_ contêiner:</span><span class="sxs-lookup"><span data-stu-id="b1024-143">hello following code demonstrates how tooretrieve and output hello URI of each item in hello _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

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
```

<span data-ttu-id="b1024-144">Ao incluir informações de caminho nos nomes de blob, você poderá criar uma estrutura de diretório virtual que pode organizar e percorrer como faria com um sistema de arquivos tradicional.</span><span class="sxs-lookup"><span data-stu-id="b1024-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="b1024-145">estrutura de diretórios de saudação é virtual--Olá somente os recursos disponíveis no armazenamento de Blob são contêineres e blobs.</span><span class="sxs-lookup"><span data-stu-id="b1024-145">hello directory structure is virtual only--hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="b1024-146">No entanto, a biblioteca de cliente de armazenamento Olá oferece um **CloudBlobDirectory** objeto de diretório virtual do toorefer tooa e simplificar o processo de saudação do trabalho com blobs são organizados dessa maneira.</span><span class="sxs-lookup"><span data-stu-id="b1024-146">However, hello storage client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="b1024-147">Por exemplo, considere Olá após o conjunto de blobs de bloco em um contêiner chamado *fotos*:</span><span class="sxs-lookup"><span data-stu-id="b1024-147">For example, consider hello following set of block blobs in a container named *photos*:</span></span>

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

<span data-ttu-id="b1024-148">Quando você chama **ListBlobs** em Olá *fotos* contêiner (como Olá precede o trecho de código), uma lista hierárquica é retornada.</span><span class="sxs-lookup"><span data-stu-id="b1024-148">When you call **ListBlobs** on hello *photos* container (as in hello preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="b1024-149">Ele contém ambos **CloudBlobDirectory** e **CloudBlockBlob** objetos, que representam diretórios hello e blobs no contêiner hello, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="b1024-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing hello directories and blobs in hello container, respectively.</span></span> <span data-ttu-id="b1024-150">saída resultante Olá aparência:</span><span class="sxs-lookup"><span data-stu-id="b1024-150">hello resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="b1024-151">Opcionalmente, você pode definir Olá **UseFlatBlobListing** parâmetro hello **ListBlobs** método **true**.</span><span class="sxs-lookup"><span data-stu-id="b1024-151">Optionally, you can set hello **UseFlatBlobListing** parameter of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="b1024-152">Nesse caso, cada blob no contêiner de saudação é retornado como um **CloudBlockBlob** objeto.</span><span class="sxs-lookup"><span data-stu-id="b1024-152">In this case, every blob in hello container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="b1024-153">Olá chamada muito**ListBlobs** tooreturn uma lista simples tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="b1024-153">hello call too**ListBlobs** tooreturn a flat listing looks like this:</span></span>

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="b1024-154">e resultados de saudação ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="b1024-154">and hello results look like this:</span></span>

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a><span data-ttu-id="b1024-155">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="b1024-155">Download blobs</span></span>
<span data-ttu-id="b1024-156">blobs toodownload, recuperar uma referência de blob e, em seguida, chamar hello **os métodos DownloadToStream** método.</span><span class="sxs-lookup"><span data-stu-id="b1024-156">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="b1024-157">Olá, exemplo a seguir usa Olá **os métodos DownloadToStream** método tootransfer Olá conteúdo tooa fluxo objeto blob que, em seguida, você pode persistir o arquivo local tooa.</span><span class="sxs-lookup"><span data-stu-id="b1024-157">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="b1024-158">Você também pode usar o hello **os métodos DownloadToStream** conteúdo de saudação do método toodownload de um blob como uma cadeia de caracteres de texto.</span><span class="sxs-lookup"><span data-stu-id="b1024-158">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="b1024-159">Excluir blobs</span><span class="sxs-lookup"><span data-stu-id="b1024-159">Delete blobs</span></span>
<span data-ttu-id="b1024-160">toodelete um blob, primeiro obter uma referência de blob e, em seguida, chame o **excluir** método nele.</span><span class="sxs-lookup"><span data-stu-id="b1024-160">toodelete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="b1024-161">Listar blobs em páginas de maneira assíncrona</span><span class="sxs-lookup"><span data-stu-id="b1024-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="b1024-162">Se estiver listando um grande número de blobs ou desejar toocontrol Olá número de resultados de que retorno em uma operação de listagem, você pode listar blobs em páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="b1024-162">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="b1024-163">Este exemplo mostra como tooreturn resulta em páginas de forma assíncrona, para que a execução não é bloqueada durante a espera tooreturn um grande conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="b1024-163">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="b1024-164">Este exemplo mostra uma simples listagem do blob, mas você também pode executar uma lista hierárquica, definindo Olá _useFlatBlobListing_ parâmetro hello **ListBlobsSegmentedAsync** too_false_ de método.</span><span class="sxs-lookup"><span data-stu-id="b1024-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello _useFlatBlobListing_ parameter of hello **ListBlobsSegmentedAsync** method too_false_.</span></span>

<span data-ttu-id="b1024-165">Como o método de exemplo hello chama um método assíncrono, ela deve ser precedida por hello _async_ palavra-chave e ele devem retornar um **tarefa** objeto.</span><span class="sxs-lookup"><span data-stu-id="b1024-165">Because hello sample method calls an asynchronous method, it must be prefaced with hello _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="b1024-166">Olá await palavra-chave especificada para Olá **ListBlobsSegmentedAsync** método suspende a execução do método de exemplo hello até Olá listagem tarefa ser concluída.</span><span class="sxs-lookup"><span data-stu-id="b1024-166">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
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
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="b1024-167">Blob de acréscimo tooan de gravação</span><span class="sxs-lookup"><span data-stu-id="b1024-167">Writing tooan append blob</span></span>
<span data-ttu-id="b1024-168">Um blob de acréscimo é otimizado para operações de acréscimo, como o registro em log.</span><span class="sxs-lookup"><span data-stu-id="b1024-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="b1024-169">Como um blob de bloco, um blob de acréscimo é composto por blocos, mas quando você adiciona um novo blob de acréscimo de tooan de bloco, é sempre anexado toohello final de blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1024-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="b1024-170">Não é possível atualizar ou excluir um bloco existente em um blob de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="b1024-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="b1024-171">IDs de bloco Olá para um blob de acréscimo não são expostos como eles são para um blob de bloco.</span><span class="sxs-lookup"><span data-stu-id="b1024-171">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="b1024-172">Cada bloco em um blob de acréscimo pode ter um tamanho diferente, o máximo de tooa de 4 MB, e um blob de acréscimo pode incluir até 50.000 blocos.</span><span class="sxs-lookup"><span data-stu-id="b1024-172">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="b1024-173">tamanho máximo de saudação de um blob de acréscimo, portanto, é um pouco mais de 195 GB (4 MB X 50.000 blocos).</span><span class="sxs-lookup"><span data-stu-id="b1024-173">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="b1024-174">exemplo Hello abaixo cria um novo blob de acréscimo e acrescenta alguns tooit de dados, com uma simulação de uma operação de log simples.</span><span class="sxs-lookup"><span data-stu-id="b1024-174">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="b1024-175">Consulte [Compreendendo Blobs de bloco, Blobs de página e Blobs de acréscimo](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) para obter mais informações sobre as diferenças de saudação entre tipos de saudação três de blobs.</span><span class="sxs-lookup"><span data-stu-id="b1024-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about hello differences between hello three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="b1024-176">Gerenciamento da segurança de blobs</span><span class="sxs-lookup"><span data-stu-id="b1024-176">Managing security for blobs</span></span>
<span data-ttu-id="b1024-177">Por padrão, o armazenamento do Azure mantém seus dados seguros, limitando o acesso toohello proprietário da conta, que está em posse das chaves de acesso de conta hello.</span><span class="sxs-lookup"><span data-stu-id="b1024-177">By default, Azure Storage keeps your data secure by limiting access toohello account owner, who is in possession of hello account access keys.</span></span> <span data-ttu-id="b1024-178">Quando você precisar de dados de blob tooshare na sua conta de armazenamento, é importante toodo caso sem comprometer a segurança de saudação de suas chaves de acesso da conta.</span><span class="sxs-lookup"><span data-stu-id="b1024-178">When you need tooshare blob data in your storage account, it is important toodo so without compromising hello security of your account access keys.</span></span> <span data-ttu-id="b1024-179">Além disso, você pode criptografar tooensure de dados de blob que é seguro vai conexão hello e no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1024-179">Additionally, you can encrypt blob data tooensure that it is secure going over hello wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a><span data-ttu-id="b1024-180">Controlando acesso tooblob dados</span><span class="sxs-lookup"><span data-stu-id="b1024-180">Controlling access tooblob data</span></span>
<span data-ttu-id="b1024-181">Por padrão, os dados de blob de saudação em sua conta de armazenamento são acessível somente toostorage conta o proprietário.</span><span class="sxs-lookup"><span data-stu-id="b1024-181">By default, hello blob data in your storage account is accessible only toostorage account owner.</span></span> <span data-ttu-id="b1024-182">Autenticar solicitações em relação ao armazenamento de Blob exige a chave de acesso de conta Olá por padrão.</span><span class="sxs-lookup"><span data-stu-id="b1024-182">Authenticating requests against Blob storage requires hello account access key by default.</span></span> <span data-ttu-id="b1024-183">No entanto, você poderá toomake determinados usuários tooother disponíveis de dados de blob.</span><span class="sxs-lookup"><span data-stu-id="b1024-183">However, you may wish toomake certain blob data available tooother users.</span></span> <span data-ttu-id="b1024-184">Você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="b1024-184">You have two options:</span></span>

* <span data-ttu-id="b1024-185">**Acesso anônimo:** você pode tornar um contêiner ou seus blobs publicamente disponíveis para acesso anônimo.</span><span class="sxs-lookup"><span data-stu-id="b1024-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="b1024-186">Consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](storage-manage-access-to-resources.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="b1024-186">See [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="b1024-187">**Assinaturas de acesso compartilhado:** podem fornecer aos clientes com uma assinatura de acesso compartilhado (SAS), que fornece acesso delegado tooa recursos em sua conta de armazenamento, com as permissões que você especificar e em um intervalo que você especificar.</span><span class="sxs-lookup"><span data-stu-id="b1024-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access tooa resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="b1024-188">Confira [Usando Assinaturas de Acesso Compartilhado (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="b1024-188">See [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="b1024-189">Criptografia de dados de blobs</span><span class="sxs-lookup"><span data-stu-id="b1024-189">Encrypting blob data</span></span>
<span data-ttu-id="b1024-190">Armazenamento do Azure oferece suporte à criptografia de dados de blob no cliente hello e no servidor de saudação:</span><span class="sxs-lookup"><span data-stu-id="b1024-190">Azure Storage supports encrypting blob data both at hello client and on hello server:</span></span>

* <span data-ttu-id="b1024-191">**Criptografia do lado do cliente:** Olá biblioteca de cliente de armazenamento para .NET oferece suporte a criptografia de dados em aplicativos cliente antes de carregar tooAzure armazenamento e a descriptografia de dados durante o download toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="b1024-191">**Client-side encryption:** hello Storage Client Library for .NET supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="b1024-192">biblioteca de saudação também oferece suporte à integração com o Cofre de chaves do Azure para gerenciamento de chaves de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b1024-192">hello library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="b1024-193">Confira [Criptografia no cliente com o .NET para o Armazenamento do Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="b1024-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span> <span data-ttu-id="b1024-194">Confira também [Tutorial: Criptografar e descriptografar blobs no Armazenamento do Microsoft Azure usando o Cofre de Chaves do Azure](storage-encrypt-decrypt-blobs-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="b1024-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="b1024-195">**Criptografia no servidor**: o Armazenamento do Azure agora dá suporte à criptografia no servidor.</span><span class="sxs-lookup"><span data-stu-id="b1024-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="b1024-196">Confira [Criptografia do Serviço de Armazenamento do Azure para dados em repouso (Visualização)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b1024-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1024-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b1024-197">Next steps</span></span>
<span data-ttu-id="b1024-198">Agora que você aprendeu as Noções básicas de saudação do armazenamento de Blob, siga essas toolearn links mais.</span><span class="sxs-lookup"><span data-stu-id="b1024-198">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="b1024-199">Gerenciador do Armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b1024-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="b1024-200">[Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="b1024-200">[Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="b1024-201">Exemplos de Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="b1024-201">Blob storage samples</span></span>
* [<span data-ttu-id="b1024-202">Introdução ao Armazenamento de Blobs do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="b1024-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="b1024-203">Referência do Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="b1024-203">Blob storage reference</span></span>
* [<span data-ttu-id="b1024-204">Referência à Biblioteca de Cliente de Armazenamento para .NET</span><span class="sxs-lookup"><span data-stu-id="b1024-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="b1024-205">Referência da API REST</span><span class="sxs-lookup"><span data-stu-id="b1024-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="b1024-206">Guias conceituais</span><span class="sxs-lookup"><span data-stu-id="b1024-206">Conceptual guides</span></span>
* [<span data-ttu-id="b1024-207">Transferência de dados com hello AzCopy utilitário de linha de comando</span><span class="sxs-lookup"><span data-stu-id="b1024-207">Transfer data with hello AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="b1024-208">Introdução ao Armazenamento de arquivos para .NET</span><span class="sxs-lookup"><span data-stu-id="b1024-208">Get started with File storage for .NET</span></span>](../files/storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="b1024-209">Como toouse Azure blob storage com hello SDK do WebJobs</span><span class="sxs-lookup"><span data-stu-id="b1024-209">How toouse Azure blob storage with hello WebJobs SDK</span></span>](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
