---
title: "Introdução ao armazenamento de blobs e aos serviços conectados do Visual Studio (serviços de nuvem) | Microsoft Docs"
description: "Como começar a usar o armazenamento de Blob do Azure em um projeto de serviço de nuvem no Visual Studio após a conexão a uma conta de armazenamento usando os serviços conectados do Visual Studio"
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
ms.openlocfilehash: e154c81ef3765a3c006b3c27a979be881f14d0ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="a422c-103">Introdução ao Armazenamento de Blob do Azure e aos serviços conectados do Visual Studio (projetos de serviços de nuvem)</span><span class="sxs-lookup"><span data-stu-id="a422c-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="a422c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a422c-104">Overview</span></span>
<span data-ttu-id="a422c-105">Este artigo descreve como começar a usar o Armazenamento de Blobs do Azure depois de ter criado ou referenciado uma conta de Armazenamento do Azure usando a caixa de diálogo **Adicionar Serviços Conectados** do Visual Studio em um projeto de serviços de nuvem do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a422c-105">This article describes how to get started with Azure Blob Storage after you created or referenced an Azure Storage account by using the Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="a422c-106">Mostraremos como acessar e criar contêineres de blob e como executar tarefas comuns, como carregamento, listagem e download de blobs.</span><span class="sxs-lookup"><span data-stu-id="a422c-106">We'll show you how to access and create blob containers, and how to perform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="a422c-107">Os exemplos são escritos em C\# e usam a [Biblioteca de Cliente do Armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="a422c-107">The samples are written in C\# and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="a422c-108">O Armazenamento de Blob do Azure é um serviço para armazenar grandes quantidades de dados não estruturados que podem ser acessados de qualquer lugar do mundo por meio de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a422c-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="a422c-109">Um único blob pode ter qualquer tamanho.</span><span class="sxs-lookup"><span data-stu-id="a422c-109">A single blob can be any size.</span></span> <span data-ttu-id="a422c-110">Blobs podem ser coisas como imagens, arquivos de áudio e vídeo, dados brutos e arquivos de documentos.</span><span class="sxs-lookup"><span data-stu-id="a422c-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="a422c-111">Assim como arquivos residem em pastas, blobs de armazenamento residem em contêineres.</span><span class="sxs-lookup"><span data-stu-id="a422c-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="a422c-112">Após ter criado um armazenamento, crie um ou mais contêineres no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a422c-112">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="a422c-113">Por exemplo, em um armazenamento chamado "Scrapbook", você pode criar contêineres no armazenamento chamados "imagens" para armazenar fotos e "áudio" para armazenar arquivos de áudio.</span><span class="sxs-lookup"><span data-stu-id="a422c-113">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="a422c-114">Depois de criar os contêineres, você poderá carregar arquivos de blob individuais para eles.</span><span class="sxs-lookup"><span data-stu-id="a422c-114">After you create the containers, you can upload individual blob files to them.</span></span>

* <span data-ttu-id="a422c-115">Para obter mais informações sobre a manipulação de bobs com programação, consulte a [Introdução ao Armazenamento de Blobs do Azure usando .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="a422c-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="a422c-116">Para obter informações gerais sobre o Armazenamento do Azure, consulte a [documentação do Armazenamento](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="a422c-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="a422c-117">Para obter informações gerais sobre os Serviços de Nuvem do Azure, consulte a [documentação dos Serviços de Nuvem](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="a422c-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="a422c-118">Para saber mais sobre como programar aplicativos ASP.NET, consulte [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="a422c-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="a422c-119">Acessar contêineres de blob em código</span><span class="sxs-lookup"><span data-stu-id="a422c-119">Access blob containers in code</span></span>
<span data-ttu-id="a422c-120">Para acessar de modo programático blobs em projetos de serviço de nuvem, você precisa adicionar os itens a seguir, se eles ainda não existirem.</span><span class="sxs-lookup"><span data-stu-id="a422c-120">To programmatically access blobs in cloud service projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="a422c-121">Adicione as seguintes declarações de namespace de código à parte superior de qualquer arquivo C# no qual você deseja acessar o Armazenamento do Azure por meio de programação.</span><span class="sxs-lookup"><span data-stu-id="a422c-121">Add the following code namespace declarations to the top of any C# file in which you wish to programmatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="a422c-122">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a422c-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a422c-123">Use o seguinte código para obter a sua cadeia de conexão de armazenamento e informações de conta de armazenamento da configuração do serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="a422c-123">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="a422c-124">Obtenha um objeto **CloudBlobClient** para fazer referência a um contêiner existente na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a422c-124">Get a **CloudBlobClient** object to reference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="a422c-125">Obtenha um objeto **CloudBlobContainer** para fazer referência a um contêiner de blob específico.</span><span class="sxs-lookup"><span data-stu-id="a422c-125">Get a **CloudBlobContainer** object to reference a specific blob container.</span></span>
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="a422c-126">Use todo o código mostrado no procedimento anterior na frente do código mostrado nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="a422c-126">Use all of the code shown in the previous procedure in front of the code shown in the following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="a422c-127">Criar um contêiner no código</span><span class="sxs-lookup"><span data-stu-id="a422c-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="a422c-128">Algumas APIs que executam chamadas para o Armazenamento do Azure no ASP.NET são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="a422c-128">Some APIs that perform calls out to Azure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="a422c-129">Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="a422c-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="a422c-130">O código no exemplo a seguir pressupõe que você esteja usando os métodos de programação assíncrona.</span><span class="sxs-lookup"><span data-stu-id="a422c-130">The code in the following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="a422c-131">Para criar um contêiner na sua conta de armazenamento, basta adicionar uma chamada para **CreateIfNotExistsAsync** , como no seguinte código:</span><span class="sxs-lookup"><span data-stu-id="a422c-131">To create a container in your storage account, all you need to do is add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="a422c-132">Se quiser tornar os arquivos dentro do contêiner disponíveis a todos, basta definir o contêiner como público usando o seguinte código.</span><span class="sxs-lookup"><span data-stu-id="a422c-132">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="a422c-133">Qualquer pessoa na Internet pode ver blobs em um contêiner público, mas você só pode modificar ou excluí-los se tiver a chave de acesso apropriada.</span><span class="sxs-lookup"><span data-stu-id="a422c-133">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="a422c-134">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="a422c-134">Upload a blob into a container</span></span>
<span data-ttu-id="a422c-135">O Armazenamento do Azure dá suporte a blobs de blocos e a blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="a422c-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="a422c-136">Na maioria dos casos, o blob de blocos é o tipo recomendado a ser usado.</span><span class="sxs-lookup"><span data-stu-id="a422c-136">In the majority of cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="a422c-137">Para carregar um arquivo em um blob de blocos, obtenha uma referência de contêiner e use-a para obter uma referência de blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="a422c-137">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="a422c-138">Quando tiver uma referência de blob, poderá transferir qualquer fluxo de dados para ele, chamando o método **UploadFromStream** .</span><span class="sxs-lookup"><span data-stu-id="a422c-138">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="a422c-139">Essa operação criará o blob, caso ele não exista, ou o substituirá, caso ele já exista.</span><span class="sxs-lookup"><span data-stu-id="a422c-139">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="a422c-140">O exemplo a seguir mostra como carregar um blob em um contêiner e pressupõe que o contêiner já tenha sido criado.</span><span class="sxs-lookup"><span data-stu-id="a422c-140">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Retrieve a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="a422c-141">Listar os blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="a422c-141">List the blobs in a container</span></span>
<span data-ttu-id="a422c-142">Para listar blobs em um contêiner, primeiro obtenha uma referência ao contêiner.</span><span class="sxs-lookup"><span data-stu-id="a422c-142">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="a422c-143">Você pode usar o método **ListBlobs** do contêiner para recuperar os blobs e/ou diretórios dentro dele.</span><span class="sxs-lookup"><span data-stu-id="a422c-143">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="a422c-144">Para acessar o conjunto avançado de propriedades e de métodos para um **IListBlobItem** retornado, você deverá convertê-lo em um objeto **CloudBlockBlob**, **CloudPageBlob** ou **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="a422c-144">To access the rich set of properties and methods for a  returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="a422c-145">Se o tipo for desconhecido, você poderá usar uma verificação de tipo para determinar no qual convertê-lo.</span><span class="sxs-lookup"><span data-stu-id="a422c-145">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="a422c-146">O código a seguir demonstra como recuperar e apresentar a saída do URI de cada item no contêiner **photos** :</span><span class="sxs-lookup"><span data-stu-id="a422c-146">The following code demonstrates how to retrieve and output the URI of each item in the **photos** container:</span></span>

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

<span data-ttu-id="a422c-147">Como mostrado no exemplo de código anterior, o serviço Blob também tem o conceito de diretórios dentro de contêineres.</span><span class="sxs-lookup"><span data-stu-id="a422c-147">As shown in the previous code sample, the blob service has the concept of directories within containers, as well.</span></span> <span data-ttu-id="a422c-148">Isso é para que você possa organizar seus blobs em uma estrutura mais semelhante a uma pasta.</span><span class="sxs-lookup"><span data-stu-id="a422c-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="a422c-149">Por exemplo, considere o seguinte conjunto de blobs de blocos em um contêiner chamado **photos**:</span><span class="sxs-lookup"><span data-stu-id="a422c-149">For example, consider the following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="a422c-150">Quando você chama **ListBlobs** no contêiner (como no exemplo anterior), a coleção retornada conterá os objetos **CloudBlobDirectory** e **CloudBlockBlob** que representam os diretórios e os blobs contidos no nível superior.</span><span class="sxs-lookup"><span data-stu-id="a422c-150">When you call **ListBlobs** on the container (as in the previous sample), the collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="a422c-151">Veja a saída resultante:</span><span class="sxs-lookup"><span data-stu-id="a422c-151">Here is the resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="a422c-152">Opcionalmente, você pode definir o parâmetro **UseFlatBlobListing** do método **ListBlobs** como **true**.</span><span class="sxs-lookup"><span data-stu-id="a422c-152">Optionally, you can set the **UseFlatBlobListing** parameter of of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="a422c-153">Isso resulta no retorno de cada blob como um **CloudBlockBlob**, independentemente do diretório.</span><span class="sxs-lookup"><span data-stu-id="a422c-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="a422c-154">Veja abaixo a chamada para **ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="a422c-154">Here is the call to **ListBlobs**:</span></span>

    // Loop over items within the container and output the length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="a422c-155">e os resultados:</span><span class="sxs-lookup"><span data-stu-id="a422c-155">and here are the results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="a422c-156">Para obter mais informações, consulte [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="a422c-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="a422c-157">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="a422c-157">Download blobs</span></span>
<span data-ttu-id="a422c-158">Para baixar blobs, primeiro recupere uma referência a um blob e, em seguida, chame o método **DownloadToStream** .</span><span class="sxs-lookup"><span data-stu-id="a422c-158">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="a422c-159">O exemplo a seguir usa o método **DownloadToStream** para transferir o conteúdo do blob para um objeto de fluxo que você pode persistir em um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="a422c-159">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents to a file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="a422c-160">Você também pode usar o método **DownloadToStream** para baixar o conteúdo de um blob como uma cadeia de texto.</span><span class="sxs-lookup"><span data-stu-id="a422c-160">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

    // Get a reference to a blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="a422c-161">Excluir blobs</span><span class="sxs-lookup"><span data-stu-id="a422c-161">Delete blobs</span></span>
<span data-ttu-id="a422c-162">Para excluir um blob, obtenha primeiro uma referência ao blob e depois chame o método **Delete** .</span><span class="sxs-lookup"><span data-stu-id="a422c-162">To delete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="a422c-163">Listar blobs em páginas de maneira assíncrona</span><span class="sxs-lookup"><span data-stu-id="a422c-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="a422c-164">Se você está listando uma grande quantidade de blobs ou se deseja controlar o número de resultados retornados em uma operação de listagem, pode listar os blobs em páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="a422c-164">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="a422c-165">Este exemplo mostra como retornar resultados em páginas de forma assíncrona, para que a execução não fique bloqueada enquanto espera para retornar um grande conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="a422c-165">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="a422c-166">Este exemplo mostra uma listagem de blob simples, mas você também pode realizar uma listagem hierárquica, configurando o parâmetro **useFlatBlobListing** do método **ListBlobsSegmentedAsync** como **falso**.</span><span class="sxs-lookup"><span data-stu-id="a422c-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the **useFlatBlobListing** parameter of the **ListBlobsSegmentedAsync** method to **false**.</span></span>

<span data-ttu-id="a422c-167">Como o método de exemplo chama um método assíncrono, ele deve ser precedido pela palavra-chave **async** e retornar um objeto **Task**.</span><span class="sxs-lookup"><span data-stu-id="a422c-167">Because the sample method calls an asynchronous method, it must be prefaced with the **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="a422c-168">A palavra-chave await especificada para o método **ListBlobsSegmentedAsync** suspende a execução do método de exemplo até que a tarefa de listagem seja concluída.</span><span class="sxs-lookup"><span data-stu-id="a422c-168">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs to the console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
        // When the continuation token is null, the last page has been returned and execution can exit the loop.
        do
        {
            // This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
            // or by calling a different overload.
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

## <a name="next-steps"></a><span data-ttu-id="a422c-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a422c-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

