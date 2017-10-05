---
title: "Introdução ao Armazenamento de Blobs do Azure (armazenamento de objetos) usando o .NET | Microsoft Docs"
description: "Armazene dados não estruturados na nuvem com o armazenamento de blobs do Azure (armazenamento de objeto)."
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
ms.openlocfilehash: 8393b2dc32f01cac301c713c2ae9f0ab7226ea37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="94ba9-103">Introdução ao Armazenamento de Blobs do Azure usando o .NET</span><span class="sxs-lookup"><span data-stu-id="94ba9-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="94ba9-104">O Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="94ba9-104">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="94ba9-105">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="94ba9-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="94ba9-106">O Armazenamento de Blobs também é chamado de armazenamento de objetos.</span><span class="sxs-lookup"><span data-stu-id="94ba9-106">Blob storage is also referred to as object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="94ba9-107">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="94ba9-107">About this tutorial</span></span>
<span data-ttu-id="94ba9-108">Este tutorial mostra como gravar código .NET para alguns cenários comuns usando o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="94ba9-108">This tutorial shows how to write .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="94ba9-109">Os cenários incluem upload, listagem, download e exclusão de blobs.</span><span class="sxs-lookup"><span data-stu-id="94ba9-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="94ba9-110">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="94ba9-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="94ba9-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="94ba9-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="94ba9-112">Biblioteca do Cliente de Armazenamento do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="94ba9-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="94ba9-113">Gerenciador de Configurações do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="94ba9-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="94ba9-114">[Uma conta do Armazenamento do Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="94ba9-114">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="94ba9-115">Mais exemplos</span><span class="sxs-lookup"><span data-stu-id="94ba9-115">More samples</span></span>
<span data-ttu-id="94ba9-116">Para obter exemplos adicionais usando o Armazenamento de Blobs, confira [Introdução ao Armazenamento de Blobs do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="94ba9-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="94ba9-117">Você pode baixar o aplicativo de exemplo e executá-lo ou procurar o código no GitHub.</span><span class="sxs-lookup"><span data-stu-id="94ba9-117">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="94ba9-118">Adicionar diretivas using</span><span class="sxs-lookup"><span data-stu-id="94ba9-118">Add using directives</span></span>
<span data-ttu-id="94ba9-119">Adicione as seguintes diretivas **using** à parte superior do arquivo `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="94ba9-119">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="94ba9-120">Analisar a cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="94ba9-120">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-blob-service-client"></a><span data-ttu-id="94ba9-121">Criar o cliente do serviço Blob</span><span class="sxs-lookup"><span data-stu-id="94ba9-121">Create the Blob service client</span></span>
<span data-ttu-id="94ba9-122">A classe **CloudBlobClient** permite que você recupere contêineres e blobs armazenados no Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="94ba9-122">The **CloudBlobClient** class enables you to retrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="94ba9-123">Veja uma maneira de criar o cliente de serviço:</span><span class="sxs-lookup"><span data-stu-id="94ba9-123">Here's one way to create the service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="94ba9-124">Agora você está pronto para escrever um código que lê e grava dados no Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="94ba9-124">Now you are ready to write code that reads data from and writes data to Blob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="94ba9-125">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="94ba9-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="94ba9-126">Este exemplo mostra como criar um contêiner caso ele ainda não exista:</span><span class="sxs-lookup"><span data-stu-id="94ba9-126">This example shows how to create a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="94ba9-127">Por padrão, o novo contêiner é privado, o que significa que você deve especificar sua chave de acesso de armazenamento para baixar blobs desse contêiner.</span><span class="sxs-lookup"><span data-stu-id="94ba9-127">By default, the new container is private, meaning that you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="94ba9-128">Para disponibilizar os arquivos do contêiner para todos, você pode definir o contêiner como público usando o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="94ba9-128">If you want to make the files within the container available to everyone, you can set the container to be public using the following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="94ba9-129">Qualquer pessoa na Internet pode ver blobs em um contêiner público.</span><span class="sxs-lookup"><span data-stu-id="94ba9-129">Anyone on the Internet can see blobs in a public container.</span></span> <span data-ttu-id="94ba9-130">No entanto, você só poderá modificá-los ou excluí-los se tiver a chave de acesso da conta apropriada ou uma assinatura de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="94ba9-130">However, you can modify or delete them only if you have the appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="94ba9-131">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="94ba9-131">Upload a blob into a container</span></span>
<span data-ttu-id="94ba9-132">O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="94ba9-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="94ba9-133">Na maioria dos casos, o blob de blocos é o tipo recomendado.</span><span class="sxs-lookup"><span data-stu-id="94ba9-133">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="94ba9-134">Para carregar um arquivo em um blob de blocos, obtenha uma referência de contêiner e use-a para obter uma referência de blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="94ba9-134">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="94ba9-135">Quando tiver uma referência de blob, poderá transferir qualquer fluxo de dados para ele, chamando o método **UploadFromStream** .</span><span class="sxs-lookup"><span data-stu-id="94ba9-135">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="94ba9-136">Essa operação criará o blob, caso ele não exista, ou o substituirá, caso ele já exista.</span><span class="sxs-lookup"><span data-stu-id="94ba9-136">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="94ba9-137">O exemplo a seguir mostra como carregar um blob em um contêiner e pressupõe que o contêiner já tenha sido criado.</span><span class="sxs-lookup"><span data-stu-id="94ba9-137">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite the "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="94ba9-138">Listar os blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="94ba9-138">List the blobs in a container</span></span>
<span data-ttu-id="94ba9-139">Para listar blobs em um contêiner, primeiro obtenha uma referência ao contêiner.</span><span class="sxs-lookup"><span data-stu-id="94ba9-139">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="94ba9-140">Você pode usar o método **ListBlobs** do contêiner para recuperar os blobs e/ou diretórios dentro dele.</span><span class="sxs-lookup"><span data-stu-id="94ba9-140">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="94ba9-141">Para acessar o conjunto avançado de propriedades e de métodos para um **IListBlobItem** retornado, você deverá convertê-lo em um objeto **CloudBlockBlob**, **CloudPageBlob** ou **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="94ba9-141">To access the  rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="94ba9-142">Se o tipo for desconhecido, você poderá usar uma verificação de tipo para determinar no qual convertê-lo.</span><span class="sxs-lookup"><span data-stu-id="94ba9-142">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="94ba9-143">O código a seguir demonstra como recuperar e apresentar a saída do URI de cada item no contêiner _photos_:</span><span class="sxs-lookup"><span data-stu-id="94ba9-143">The following code demonstrates how to retrieve and output the URI of each item in the _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within the container and output the length and URI.
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

<span data-ttu-id="94ba9-144">Ao incluir informações de caminho nos nomes de blob, você poderá criar uma estrutura de diretório virtual que pode organizar e percorrer como faria com um sistema de arquivos tradicional.</span><span class="sxs-lookup"><span data-stu-id="94ba9-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="94ba9-145">A estrutura do diretório é somente virtual: os somente os recursos disponíveis no armazenamento de Blobs são contêineres e blobs.</span><span class="sxs-lookup"><span data-stu-id="94ba9-145">The directory structure is virtual only--the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="94ba9-146">No entanto, a biblioteca de cliente de armazenamento oferece um objeto **CloudBlobDirectory** para fazer referência a um diretório virtual e simplificar o processo de trabalhar com blobs organizados dessa maneira.</span><span class="sxs-lookup"><span data-stu-id="94ba9-146">However, the storage client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="94ba9-147">Por exemplo, considere o seguinte conjunto de blobs de blocos em um contêiner chamado *photos*:</span><span class="sxs-lookup"><span data-stu-id="94ba9-147">For example, consider the following set of block blobs in a container named *photos*:</span></span>

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

<span data-ttu-id="94ba9-148">Quando você chama **ListBlobs** no contêiner *photos* (como no trecho de código acima), uma listagem hierárquica é retornada.</span><span class="sxs-lookup"><span data-stu-id="94ba9-148">When you call **ListBlobs** on the *photos* container (as in the preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="94ba9-149">Ela contém os objetos **CloudBlobDirectory** e **CloudBlockBlob**, que representam os diretórios e blobs no contêiner, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="94ba9-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing the directories and blobs in the container, respectively.</span></span> <span data-ttu-id="94ba9-150">A saída resultante é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="94ba9-150">The resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="94ba9-151">Opcionalmente, você pode definir o parâmetro **UseFlatBlobListing** do método **ListBlobs** como **true**.</span><span class="sxs-lookup"><span data-stu-id="94ba9-151">Optionally, you can set the **UseFlatBlobListing** parameter of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="94ba9-152">Nesse caso, cada blob no contêiner é retornado como um objeto **CloudBlockBlob** .</span><span class="sxs-lookup"><span data-stu-id="94ba9-152">In this case, every blob in the container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="94ba9-153">A chamada a **ListBlobs** para retornar uma lista simples se parece com esta:</span><span class="sxs-lookup"><span data-stu-id="94ba9-153">The call to **ListBlobs** to return a flat listing looks like this:</span></span>

```csharp
// Loop over items within the container and output the length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="94ba9-154">e os resultados se parecem com estes:</span><span class="sxs-lookup"><span data-stu-id="94ba9-154">and the results look like this:</span></span>

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

## <a name="download-blobs"></a><span data-ttu-id="94ba9-155">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="94ba9-155">Download blobs</span></span>
<span data-ttu-id="94ba9-156">Para baixar blobs, primeiro recupere uma referência a um blob e, em seguida, chame o método **DownloadToStream** .</span><span class="sxs-lookup"><span data-stu-id="94ba9-156">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="94ba9-157">O exemplo a seguir usa o método **DownloadToStream** para transferir o conteúdo do blob para um objeto de fluxo que você pode persistir em um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="94ba9-157">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents to a file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="94ba9-158">Você também pode usar o método **DownloadToStream** para baixar o conteúdo de um blob como uma cadeia de texto.</span><span class="sxs-lookup"><span data-stu-id="94ba9-158">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="94ba9-159">Excluir blobs</span><span class="sxs-lookup"><span data-stu-id="94ba9-159">Delete blobs</span></span>
<span data-ttu-id="94ba9-160">Para excluir um blob, primeiro obtenha uma referência de blob e depois chame o método **Delete** nela.</span><span class="sxs-lookup"><span data-stu-id="94ba9-160">To delete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete the blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="94ba9-161">Listar blobs em páginas de maneira assíncrona</span><span class="sxs-lookup"><span data-stu-id="94ba9-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="94ba9-162">Se você está listando uma grande quantidade de blobs ou se deseja controlar o número de resultados retornados em uma operação de listagem, pode listar os blobs em páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="94ba9-162">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="94ba9-163">Este exemplo mostra como retornar resultados em páginas de forma assíncrona, para que a execução não fique bloqueada enquanto espera para retornar um grande conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="94ba9-163">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="94ba9-164">Este exemplo mostra uma listagem de blob simples, mas você também pode realizar uma listagem hierárquica, configurando o parâmetro _useFlatBlobListing_ do método **ListBlobsSegmentedAsync** como _falso_.</span><span class="sxs-lookup"><span data-stu-id="94ba9-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the _useFlatBlobListing_ parameter of the **ListBlobsSegmentedAsync** method to _false_.</span></span>

<span data-ttu-id="94ba9-165">Como o método de exemplo chama um método assíncrono, ele deve ser precedido pela palavra-chave _async_ e retornar um objeto **Task**.</span><span class="sxs-lookup"><span data-stu-id="94ba9-165">Because the sample method calls an asynchronous method, it must be prefaced with the _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="94ba9-166">A palavra-chave await especificada para o método **ListBlobsSegmentedAsync** suspende a execução do método de exemplo até que a tarefa de listagem seja concluída.</span><span class="sxs-lookup"><span data-stu-id="94ba9-166">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs to the console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
    //When the continuation token is null, the last page has been returned and execution can exit the loop.
    do
    {
        //This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get the continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="94ba9-167">Gravar um blob de anexo</span><span class="sxs-lookup"><span data-stu-id="94ba9-167">Writing to an append blob</span></span>
<span data-ttu-id="94ba9-168">Um blob de acréscimo é otimizado para operações de acréscimo, como o registro em log.</span><span class="sxs-lookup"><span data-stu-id="94ba9-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="94ba9-169">Como um blob de blocos, um blob de acréscimo é composto por blocos; no entanto, quando você adiciona um novo bloco a um blob de acréscimo, ele sempre é acrescentado ao fim do blob.</span><span class="sxs-lookup"><span data-stu-id="94ba9-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="94ba9-170">Não é possível atualizar ou excluir um bloco existente em um blob de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="94ba9-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="94ba9-171">As IDs de bloco de um blob de acréscimo não ficam expostas como em um blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="94ba9-171">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="94ba9-172">Cada bloco em um blob de acréscimo pode ter um tamanho diferente, até no máximo 4 MB, e um blob de acréscimo pode incluir no máximo 50.000 blocos.</span><span class="sxs-lookup"><span data-stu-id="94ba9-172">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="94ba9-173">O tamanho máximo de um blob de acréscimo, portanto, é de pouco mais de 195 GB (4 MB x 50.000 blocos).</span><span class="sxs-lookup"><span data-stu-id="94ba9-173">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="94ba9-174">O exemplo a seguir cria um novo blob de acréscimo e acrescenta alguns dados a ele, simulando uma operação simples de registro em log.</span><span class="sxs-lookup"><span data-stu-id="94ba9-174">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```csharp
//Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create the container if it does not already exist.
container.CreateIfNotExists();

//Get a reference to an append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create the append blob. Note that if the blob already exists, the CreateOrReplace() method will overwrite it.
//You can check whether the blob exists to avoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data to the end of the append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read the append blob to the console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="94ba9-175">Para saber mais sobre as diferenças entre os três tipos de blobs, confira [Noções gerais sobre blobs de blocos, blobs de páginas e blobs de acréscimo](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) .</span><span class="sxs-lookup"><span data-stu-id="94ba9-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about the differences between the three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="94ba9-176">Gerenciamento da segurança de blobs</span><span class="sxs-lookup"><span data-stu-id="94ba9-176">Managing security for blobs</span></span>
<span data-ttu-id="94ba9-177">Por padrão, o Armazenamento do Azure mantém seus dados seguros limitando o acesso ao proprietário da conta, que possui as chaves de acesso à conta.</span><span class="sxs-lookup"><span data-stu-id="94ba9-177">By default, Azure Storage keeps your data secure by limiting access to the account owner, who is in possession of the account access keys.</span></span> <span data-ttu-id="94ba9-178">Quando você precisa compartilhar dados de blob em sua conta de armazenamento, é importante fazer isso sem comprometer a segurança de suas chaves de acesso à conta.</span><span class="sxs-lookup"><span data-stu-id="94ba9-178">When you need to share blob data in your storage account, it is important to do so without compromising the security of your account access keys.</span></span> <span data-ttu-id="94ba9-179">Além disso, você pode criptografar os dados de blob para garantir que eles fiquem seguros durante a transmissão e no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="94ba9-179">Additionally, you can encrypt blob data to ensure that it is secure going over the wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-to-blob-data"></a><span data-ttu-id="94ba9-180">Controle do acesso a dados de blob</span><span class="sxs-lookup"><span data-stu-id="94ba9-180">Controlling access to blob data</span></span>
<span data-ttu-id="94ba9-181">Por padrão, os dados de blob em sua conta de armazenamento só podem ser acessados pelo proprietário da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="94ba9-181">By default, the blob data in your storage account is accessible only to storage account owner.</span></span> <span data-ttu-id="94ba9-182">A autenticação de solicitações no Armazenamento de Blobs requer a chave de acesso da conta, por padrão.</span><span class="sxs-lookup"><span data-stu-id="94ba9-182">Authenticating requests against Blob storage requires the account access key by default.</span></span> <span data-ttu-id="94ba9-183">No entanto, talvez você queira disponibilizar determinados dados de blobs para outros usuários.</span><span class="sxs-lookup"><span data-stu-id="94ba9-183">However, you may wish to make certain blob data available to other users.</span></span> <span data-ttu-id="94ba9-184">Você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="94ba9-184">You have two options:</span></span>

* <span data-ttu-id="94ba9-185">**Acesso anônimo:** você pode tornar um contêiner ou seus blobs publicamente disponíveis para acesso anônimo.</span><span class="sxs-lookup"><span data-stu-id="94ba9-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="94ba9-186">Confira [Gerenciar o acesso de leitura anônimo aos contêineres e blobs](storage-manage-access-to-resources.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="94ba9-186">See [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="94ba9-187">**Assinaturas de acesso compartilhado:** você pode fornecer aos clientes uma SAS (assinatura de acesso compartilhado), que fornece acesso delegado a um recurso em sua conta de armazenamento, com permissões e em um intervalo que você especifica.</span><span class="sxs-lookup"><span data-stu-id="94ba9-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access to a resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="94ba9-188">Confira [Usando Assinaturas de Acesso Compartilhado (SAS)](storage-dotnet-shared-access-signature-part-1.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="94ba9-188">See [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="94ba9-189">Criptografia de dados de blobs</span><span class="sxs-lookup"><span data-stu-id="94ba9-189">Encrypting blob data</span></span>
<span data-ttu-id="94ba9-190">O Armazenamento do Azure dá suporte à criptografia de dados de blobs no cliente e no servidor:</span><span class="sxs-lookup"><span data-stu-id="94ba9-190">Azure Storage supports encrypting blob data both at the client and on the server:</span></span>

* <span data-ttu-id="94ba9-191">**Criptografia no cliente:** a Biblioteca de Cliente de Armazenamento para .NET dá suporte à criptografia de dados em aplicativos clientes antes de fazer o carregamento no Armazenamento do Azure e à descriptografia de dados durante o download para o cliente.</span><span class="sxs-lookup"><span data-stu-id="94ba9-191">**Client-side encryption:** The Storage Client Library for .NET supports encrypting data within client applications before uploading to Azure Storage, and decrypting data while downloading to the client.</span></span> <span data-ttu-id="94ba9-192">A biblioteca também dá suporte à integração com o Cofre de Chaves do Azure para o gerenciamento de chaves de contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="94ba9-192">The library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="94ba9-193">Confira [Criptografia no cliente com o .NET para o Armazenamento do Microsoft Azure](storage-client-side-encryption.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="94ba9-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](storage-client-side-encryption.md) for more information.</span></span> <span data-ttu-id="94ba9-194">Confira também [Tutorial: Criptografar e descriptografar blobs no Armazenamento do Microsoft Azure usando o Cofre de Chaves do Azure](storage-encrypt-decrypt-blobs-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="94ba9-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="94ba9-195">**Criptografia no servidor**: o Armazenamento do Azure agora dá suporte à criptografia no servidor.</span><span class="sxs-lookup"><span data-stu-id="94ba9-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="94ba9-196">Confira [Criptografia do Serviço de Armazenamento do Azure para dados em repouso (Visualização)](storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="94ba9-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](storage-service-encryption.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="94ba9-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="94ba9-197">Next steps</span></span>
<span data-ttu-id="94ba9-198">Agora que você aprendeu os conceitos básicos do armazenamento de Blobs, siga estes links para saber mais.</span><span class="sxs-lookup"><span data-stu-id="94ba9-198">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="94ba9-199">Gerenciador do Armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="94ba9-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="94ba9-200">O [MASE (Gerenciador de Armazenamento do Microsoft Azure)](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que possibilita o trabalho visual com dados do Armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="94ba9-200">[Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="94ba9-201">Exemplos de Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="94ba9-201">Blob storage samples</span></span>
* [<span data-ttu-id="94ba9-202">Introdução ao Armazenamento de Blobs do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="94ba9-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="94ba9-203">Referência do Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="94ba9-203">Blob storage reference</span></span>
* [<span data-ttu-id="94ba9-204">Referência à Biblioteca de Cliente de Armazenamento para .NET</span><span class="sxs-lookup"><span data-stu-id="94ba9-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="94ba9-205">Referência da API REST</span><span class="sxs-lookup"><span data-stu-id="94ba9-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="94ba9-206">Guias conceituais</span><span class="sxs-lookup"><span data-stu-id="94ba9-206">Conceptual guides</span></span>
* [<span data-ttu-id="94ba9-207">Transferir dados com o utilitário de linha de comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="94ba9-207">Transfer data with the AzCopy command-line utility</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="94ba9-208">Introdução ao Armazenamento de arquivos para .NET</span><span class="sxs-lookup"><span data-stu-id="94ba9-208">Get started with File storage for .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="94ba9-209">Como usar o armazenamento de blobs do Azure com o SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="94ba9-209">How to use Azure blob storage with the WebJobs SDK</span></span>](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
