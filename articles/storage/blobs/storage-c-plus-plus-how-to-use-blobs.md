---
title: Como usar o armazenamento de blobs (armazenamento de objeto) do C++ | Microsoft Docs
description: "Armazene dados não estruturados na nuvem com o armazenamento de blobs do Azure (armazenamento de objeto)."
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: daf480b7be78dc001712010eac6386d4744c3c1d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-c"></a><span data-ttu-id="1a62c-103">Como usar o Armazenamento de Blob em C++</span><span class="sxs-lookup"><span data-stu-id="1a62c-103">How to use Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="1a62c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1a62c-104">Overview</span></span>
<span data-ttu-id="1a62c-105">O Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="1a62c-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="1a62c-106">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1a62c-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="1a62c-107">O Armazenamento de Blobs também é chamado de armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="1a62c-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="1a62c-108">Este guia demonstra como executar cenários comuns usando oServiço de armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a62c-108">This guide will demonstrate how to perform common scenarios using the Azure Blob storage service.</span></span> <span data-ttu-id="1a62c-109">Os exemplos são escritos em C++ e usam a [Biblioteca do Cliente de Armazenamento do Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="1a62c-109">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="1a62c-110">Os cenários abrangidos incluem **carregamento**, **listagem**, **download** e **exclusão** de blobs.</span><span class="sxs-lookup"><span data-stu-id="1a62c-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="1a62c-111">Este guia tem como alvo a Biblioteca do Cliente de Armazenamento do Azure para C++, versão 1.0.0 e superior.</span><span class="sxs-lookup"><span data-stu-id="1a62c-111">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="1a62c-112">A versão recomendada é a Biblioteca de Clientes de Armazenamento 2.2.0, que está disponível via [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="1a62c-112">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="1a62c-113">Criar um aplicativo em C++</span><span class="sxs-lookup"><span data-stu-id="1a62c-113">Create a C++ application</span></span>
<span data-ttu-id="1a62c-114">Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo C++.</span><span class="sxs-lookup"><span data-stu-id="1a62c-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="1a62c-115">Para isso, você precisará instalar a Biblioteca do Cliente de Armazenamento do Azure para C++ e criar uma conta de armazenamento do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a62c-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="1a62c-116">Para instalar a Biblioteca do Cliente de Armazenamento do Azure para C++, você pode usar os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="1a62c-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="1a62c-117">**Linux:** siga as instruções dadas na página README da [Biblioteca do Cliente de Armazenamento do Azure para C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="1a62c-117">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="1a62c-118">**Windows:** no Visual Studio, clique em **Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="1a62c-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="1a62c-119">Digite o seguinte comando no console do [Gerenciador de Pacotes do NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1a62c-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="1a62c-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="1a62c-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="1a62c-121">Configurar seu aplicativo para acessar o Armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="1a62c-121">Configure your application to access Blob Storage</span></span>
<span data-ttu-id="1a62c-122">Adicione as seguintes instruções include à parte superior do arquivo C++ no qual deseja usar as APIs de armazenamento do Azure para acessar os blobs:</span><span class="sxs-lookup"><span data-stu-id="1a62c-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="1a62c-123">Configurar uma cadeia de conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="1a62c-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="1a62c-124">Um cliente de armazenamento do Azure usa uma cadeia de conexão para armazenar pontos de extremidade e credenciais para acessar serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="1a62c-124">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="1a62c-125">Ao ser executado em um aplicativo cliente, é necessário fornecer a cadeia de conexão de armazenamento no formato a seguir, usando o nome da sua conta de armazenamento e a chave de acesso de armazenamento da conta de armazenamento listada no [Portal do Azure](https://portal.azure.com) para os valores *AccountName* e *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="1a62c-125">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="1a62c-126">Para obter informações sobre as contas de armazenamento e as chaves de acesso, consulte [Sobre as Contas de Armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1a62c-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="1a62c-127">Este exemplo mostra como você pode declarar um campo estático para armazenar a cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="1a62c-127">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="1a62c-128">Para testar seu aplicativo no computador local do Windows, você pode usar o emulador de armazenamento do [Microsoft Azure](../storage-use-emulator.md) que é instalado com o [SDK do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1a62c-128">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="1a62c-129">O emulador de armazenamento é um utilitário que simula os serviços Blob, fila e tabela disponíveis no Azure em sua máquina de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="1a62c-129">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="1a62c-130">Este exemplo mostra como você pode declarar um campo estático para manter a cadeia de conexão em seu emulador de armazenamento local:</span><span class="sxs-lookup"><span data-stu-id="1a62c-130">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="1a62c-131">Para iniciar o emulador de armazenamento do Azure, selecione o botão **Iniciar** ou pressione a tecla **Windows**.</span><span class="sxs-lookup"><span data-stu-id="1a62c-131">To start the Azure storage emulator, Select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="1a62c-132">Comece digitando **Emulador de Armazenamento do Azure** e selecione **Emulador de Armazenamento do Microsoft Azure** na lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1a62c-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="1a62c-133">Os exemplos abaixo pressupõem que você usou um desses dois métodos para obter a cadeia de conexão do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1a62c-133">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="1a62c-134">Recuperar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="1a62c-134">Retrieve your connection string</span></span>
<span data-ttu-id="1a62c-135">É possível usar a classe **cloud_storage_account** para representar as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1a62c-135">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="1a62c-136">Para recuperar as informações da conta de armazenamento na cadeia de conexão de armazenamento, você pode usar o método **Analisar** .</span><span class="sxs-lookup"><span data-stu-id="1a62c-136">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="1a62c-137">Em seguida, obtenha uma referência para uma classe **cloud_blob_client** que permita recuperar os objetos que representam os contêineres e os blobs armazenados no serviço de armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="1a62c-137">Next, get a reference to a **cloud_blob_client** class as it allows you to retrieve objects that represent containers and blobs stored within the Blob Storage Service.</span></span> <span data-ttu-id="1a62c-138">O código a seguir cria um objeto **cloud_blob_client** usando o objeto da conta de armazenamento que recuperamos acima:</span><span class="sxs-lookup"><span data-stu-id="1a62c-138">The following code creates a **cloud_blob_client** object using the storage account object we retrieved above:</span></span>  

```cpp
// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="1a62c-139">Como criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="1a62c-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="1a62c-140">Este exemplo mostra como criar um contêiner se ele ainda não existir:</span><span class="sxs-lookup"><span data-stu-id="1a62c-140">This example shows how to create a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create the blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference to a container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create the container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="1a62c-141">Por padrão, o novo contêiner é privado e você deve especificar sua chave de acesso do armazenamento para baixar blobs desse contêiner.</span><span class="sxs-lookup"><span data-stu-id="1a62c-141">By default, the new container is private and you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="1a62c-142">Se você quiser disponibilizar os arquivos (blobs) dentro do contêiner para todas as pessoas, poderá definir o contêiner como público usando o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="1a62c-142">If you want to make the files (blobs) within the container available to everyone, you can set the container to be public using the following code:</span></span>  

```cpp
// Make the blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="1a62c-143">Qualquer pessoa na Internet pode ver blobs em um contêiner público, mas você só pode modificar ou excluí-los se tiver a chave de acesso apropriada.</span><span class="sxs-lookup"><span data-stu-id="1a62c-143">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="1a62c-144">Como: carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="1a62c-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="1a62c-145">O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="1a62c-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="1a62c-146">Na maioria dos casos, o blob de blocos é o tipo recomendado.</span><span class="sxs-lookup"><span data-stu-id="1a62c-146">In the majority of cases, block blob is the recommended type to use.</span></span>  

<span data-ttu-id="1a62c-147">Para carregar um arquivo em um blob de blocos, obtenha uma referência de contêiner e use-a para obter uma referência de blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="1a62c-147">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="1a62c-148">Depois de ter uma referência do blob, você pode carregar qualquer fluxo de dados para ele chamando o método **upload_from_stream**.</span><span class="sxs-lookup"><span data-stu-id="1a62c-148">Once you have a blob reference, you can upload any stream of data to it by calling the **upload_from_stream** method.</span></span> <span data-ttu-id="1a62c-149">Essa operação criará o blob, caso ele não exista, ou o substituirá, caso ele já exista.</span><span class="sxs-lookup"><span data-stu-id="1a62c-149">This operation will create the blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="1a62c-150">O exemplo a seguir mostra como carregar um blob em um contêiner e pressupõe que o contêiner já tenha sido criado.</span><span class="sxs-lookup"><span data-stu-id="1a62c-150">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite the "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite the "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference to a blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="1a62c-151">Como alternativa, você pode usar o método **upload_from_file** para carregar um arquivo em um blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="1a62c-151">Alternatively, you can use the **upload_from_file** method to upload a file to a block blob.</span></span>

## <a name="how-to-list-the-blobs-in-a-container"></a><span data-ttu-id="1a62c-152">Como: listar os blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="1a62c-152">How to: List the blobs in a container</span></span>
<span data-ttu-id="1a62c-153">Para listar blobs em um contêiner, primeiro obtenha uma referência ao contêiner.</span><span class="sxs-lookup"><span data-stu-id="1a62c-153">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="1a62c-154">Você pode usar o método **list_blobs** do contêiner para recuperar os blobs e/ou diretórios dentro dele.</span><span class="sxs-lookup"><span data-stu-id="1a62c-154">You can then use the container's **list_blobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="1a62c-155">Para acessar o conjunto avançado de propriedades e métodos para um **list_blob_item** retornado, você deve chamar o método **list_blob_item.as_blob** para obter um objeto **cloud_blob** ou o método **list_blob.as_directory** para obter um objeto cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="1a62c-155">To access the rich set of properties and methods for a returned **list_blob_item**, you must call the **list_blob_item.as_blob** method to get a  **cloud_blob** object, or the **list_blob.as_directory** method to get a  cloud_blob_directory object.</span></span> <span data-ttu-id="1a62c-156">O código a seguir demonstra como recuperar e apresentar a URI de cada item no contêiner **my-sample-container** :</span><span class="sxs-lookup"><span data-stu-id="1a62c-156">The following code demonstrates how to retrieve and output the URI of each item in the **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

<span data-ttu-id="1a62c-157">Para obter mais detalhes sobre a lista de operações, consulte [Listar recursos de Armazenamento do Azure em C++](../storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="1a62c-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="1a62c-158">Como: baixar blobs</span><span class="sxs-lookup"><span data-stu-id="1a62c-158">How to: Download blobs</span></span>
<span data-ttu-id="1a62c-159">Para baixar blobs, primeiro recupere uma referência do blob, em seguida, chame o método **download_to_stream**.</span><span class="sxs-lookup"><span data-stu-id="1a62c-159">To download blobs, first retrieve a blob reference and then call the **download_to_stream** method.</span></span> <span data-ttu-id="1a62c-160">O exemplo a seguir usa o método **download_to_stream** para transferir o conteúdo do blob para um objeto de fluxo que você pode persistir em um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="1a62c-160">The following example uses the **download_to_stream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents to a file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="1a62c-161">Como alternativa, você pode usar o método **download_to_file** para baixar o conteúdo de um blob em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="1a62c-161">Alternatively, you can use the **download_to_file** method to download the contents of a blob to a file.</span></span>
<span data-ttu-id="1a62c-162">Você também pode usar o método **download_text** para baixar o conteúdo de um blob como uma cadeia de texto.</span><span class="sxs-lookup"><span data-stu-id="1a62c-162">In addition, you can also use the **download_text** method to download the contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download the contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="1a62c-163">Como: excluir blobs</span><span class="sxs-lookup"><span data-stu-id="1a62c-163">How to: Delete blobs</span></span>
<span data-ttu-id="1a62c-164">Para excluir um blob, primeiro obtenha uma referência do blob e, em seguida, chame o método **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="1a62c-164">To delete a blob, first get a blob reference and then call the **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete the blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="1a62c-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1a62c-165">Next steps</span></span>
<span data-ttu-id="1a62c-166">Agora que você aprendeu os conceitos básicos do armazenamento de blobs, siga estes links para saber mais sobre o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a62c-166">Now that you've learned the basics of blob storage, follow these links to learn more about Azure Storage.</span></span>  

* [<span data-ttu-id="1a62c-167">Como usar o Armazenamento de Filas do C++</span><span class="sxs-lookup"><span data-stu-id="1a62c-167">How to use Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="1a62c-168">Como usar o Armazenamento de Tabelas do C++</span><span class="sxs-lookup"><span data-stu-id="1a62c-168">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="1a62c-169">Listar recursos de Armazenamento do Azure em C++</span><span class="sxs-lookup"><span data-stu-id="1a62c-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="1a62c-170">Referência da Biblioteca de Cliente de Armazenamento para C++</span><span class="sxs-lookup"><span data-stu-id="1a62c-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="1a62c-171">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="1a62c-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="1a62c-172">Transferir dados com o utilitário de linha de comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="1a62c-172">Transfer data with the AzCopy command-line utility</span></span>](../storage-use-azcopy.md)

