---
title: armazenamento de blob aaaHow toouse (armazenamento de objeto) de C++ | Microsoft Docs
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
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
ms.openlocfilehash: 0d7e7436a109ef54fc07cc238c03cfc7cf2caac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a><span data-ttu-id="f0046-103">Como toouse armazenamento de Blob de C++</span><span class="sxs-lookup"><span data-stu-id="f0046-103">How toouse Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="f0046-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f0046-104">Overview</span></span>
<span data-ttu-id="f0046-105">Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="f0046-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="f0046-106">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0046-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="f0046-107">Armazenamento de blob também é chamado tooas armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="f0046-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="f0046-108">Este guia demonstra como os cenários comuns de tooperform usando Olá serviço de armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0046-108">This guide will demonstrate how tooperform common scenarios using hello Azure Blob storage service.</span></span> <span data-ttu-id="f0046-109">exemplos de saudação são escritos em C++ e usam Olá [biblioteca de cliente de armazenamento do Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="f0046-109">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="f0046-110">Olá cenários abordados incluem **Carregando**, **listando**, **baixando**, e **excluindo** blobs.</span><span class="sxs-lookup"><span data-stu-id="f0046-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="f0046-111">Destino dessa guia Olá biblioteca de cliente de armazenamento do Azure para a versão 1.0.0 de C++ e acima.</span><span class="sxs-lookup"><span data-stu-id="f0046-111">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="f0046-112">Olá recomendado versão é a biblioteca de cliente de armazenamento 2.2.0, que está disponível por meio de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="f0046-112">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="f0046-113">Criar um aplicativo em C++</span><span class="sxs-lookup"><span data-stu-id="f0046-113">Create a C++ application</span></span>
<span data-ttu-id="f0046-114">Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo C++.</span><span class="sxs-lookup"><span data-stu-id="f0046-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="f0046-115">toodo assim, você precisará tooinstall hello biblioteca de cliente de armazenamento do Azure para C++ e criar uma conta de armazenamento do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0046-115">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="f0046-116">Olá tooinstall biblioteca de cliente de armazenamento do Azure para C++, você pode usar o hello métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0046-116">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="f0046-117">**Linux:** siga instruções Olá fornecidas em Olá [biblioteca de cliente de armazenamento do Azure para C++ Leiame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.</span><span class="sxs-lookup"><span data-stu-id="f0046-117">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="f0046-118">**Windows:** no Visual Studio, clique em **Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="f0046-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="f0046-119">Digite o seguinte Olá comando em Olá [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f0046-119">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="f0046-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="f0046-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="f0046-121">Configurar seu aplicativo tooaccess armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="f0046-121">Configure your application tooaccess Blob Storage</span></span>
<span data-ttu-id="f0046-122">Adicione a seguinte Olá incluem superior de toohello de instruções do arquivo de C++ de saudação onde você deseja toouse Olá armazenamento do Azure APIs tooaccess blobs:</span><span class="sxs-lookup"><span data-stu-id="f0046-122">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="f0046-123">Configurar uma cadeia de conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f0046-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="f0046-124">Um cliente de armazenamento do Azure usa um pontos de extremidade de toostore de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f0046-124">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="f0046-125">Quando em execução em um aplicativo cliente, você deve fornecer a cadeia de conexão de armazenamento Olá no hello formato a seguir, usando o nome de saudação da chave de acesso do armazenamento seu armazenamento conta e Olá Olá conta de armazenamento listada no hello [Portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="f0046-125">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="f0046-126">Para obter informações sobre as contas de armazenamento e as chaves de acesso, consulte [Sobre as Contas de Armazenamento do Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="f0046-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="f0046-127">Este exemplo mostra como você pode declarar uma cadeia de caracteres de conexão do campo estático toohold hello:</span><span class="sxs-lookup"><span data-stu-id="f0046-127">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="f0046-128">tootest seu aplicativo no seu computador local do Windows, você pode usar o hello Microsoft Azure [emulador de armazenamento](storage-use-emulator.md) que é instalada com hello [SDK do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f0046-128">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="f0046-129">emulador de armazenamento Olá é um utilitário que simula os serviços de Blob, fila e tabela de saudação disponíveis no Azure em sua máquina de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="f0046-129">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="f0046-130">Olá exemplo a seguir mostra como você pode declarar um emulador de armazenamento local do campo estático toohold Olá cadeia de caracteres conexão tooyour:</span><span class="sxs-lookup"><span data-stu-id="f0046-130">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="f0046-131">emulador de armazenamento do Azure toostart hello, selecione Olá **iniciar** Olá botão ou pressione **Windows** chave.</span><span class="sxs-lookup"><span data-stu-id="f0046-131">toostart hello Azure storage emulator, Select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="f0046-132">Comece digitando **emulador de armazenamento do Azure**e selecione **emulador de armazenamento do Microsoft Azure** da lista de saudação de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f0046-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="f0046-133">Olá exemplos a seguir pressupõem que você usou uma cadeia de conexão de armazenamento esses dois métodos tooget hello.</span><span class="sxs-lookup"><span data-stu-id="f0046-133">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="f0046-134">Recuperar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="f0046-134">Retrieve your connection string</span></span>
<span data-ttu-id="f0046-135">Você pode usar o hello **cloud_storage_account** classe toorepresent suas informações de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f0046-135">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="f0046-136">tooretrieve informações de cadeia de caracteres de conexão de armazenamento Olá da conta de armazenamento, você pode usar o hello **analisar** método.</span><span class="sxs-lookup"><span data-stu-id="f0046-136">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="f0046-137">Em seguida, obtenha uma referência tooa **cloud_blob_client** classe que permite a você tooretrieve objetos que representam os contêineres e blobs armazenados em Olá serviço de armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="f0046-137">Next, get a reference tooa **cloud_blob_client** class as it allows you tooretrieve objects that represent containers and blobs stored within hello Blob Storage Service.</span></span> <span data-ttu-id="f0046-138">Olá código a seguir cria um **cloud_blob_client** objeto usando o objeto de conta de armazenamento Olá recuperamos acima:</span><span class="sxs-lookup"><span data-stu-id="f0046-138">hello following code creates a **cloud_blob_client** object using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="f0046-139">Como criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="f0046-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="f0046-140">Este exemplo mostra como toocreate um contêiner se ele ainda não existir:</span><span class="sxs-lookup"><span data-stu-id="f0046-140">This example shows how toocreate a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="f0046-141">Por padrão, novo contêiner de saudação é privado e você deve especificar seus blobs de toodownload chave de acesso de armazenamento desse contêiner.</span><span class="sxs-lookup"><span data-stu-id="f0046-141">By default, hello new container is private and you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="f0046-142">Toomake Olá arquivos se (blobs) em Olá contêiner disponível tooeveryone, você pode definir Olá contêiner toobe pública usando Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0046-142">If you want toomake hello files (blobs) within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="f0046-143">Qualquer pessoa na Internet de saudação pode ver os blobs em um contêiner público, mas você pode modificar ou excluí-los somente se você tiver a chave de acesso apropriadas de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0046-143">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="f0046-144">Como: carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="f0046-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="f0046-145">O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="f0046-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="f0046-146">Na maioria Olá dos casos, blob de blocos é hello recomendado toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="f0046-146">In hello majority of cases, block blob is hello recommended type toouse.</span></span>  

<span data-ttu-id="f0046-147">tooupload um blob de blocos de tooa de arquivo, obtenha uma referência de contêiner e usá-lo tooget uma referência de blob de bloco.</span><span class="sxs-lookup"><span data-stu-id="f0046-147">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="f0046-148">Quando você tem uma referência de blob, você pode carregar qualquer fluxo de dados tooit Olá chamada **upload_from_stream** método.</span><span class="sxs-lookup"><span data-stu-id="f0046-148">Once you have a blob reference, you can upload any stream of data tooit by calling hello **upload_from_stream** method.</span></span> <span data-ttu-id="f0046-149">Esta operação criará blob Olá se ele anteriormente não existe ou substituí-lo se ele existir.</span><span class="sxs-lookup"><span data-stu-id="f0046-149">This operation will create hello blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="f0046-150">Olá mostrado no exemplo a seguir como tooupload um blob em um contêiner e supõe que esse contêiner Olá já foi criado.</span><span class="sxs-lookup"><span data-stu-id="f0046-150">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="f0046-151">Como alternativa, você pode usar o hello **upload_from_file** tooupload método um blob de blocos de tooa do arquivo.</span><span class="sxs-lookup"><span data-stu-id="f0046-151">Alternatively, you can use hello **upload_from_file** method tooupload a file tooa block blob.</span></span>

## <a name="how-to-list-hello-blobs-in-a-container"></a><span data-ttu-id="f0046-152">Como: lista Olá blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="f0046-152">How to: List hello blobs in a container</span></span>
<span data-ttu-id="f0046-153">blobs de saudação toolist em um contêiner, primeiro obtenha uma referência de contêiner.</span><span class="sxs-lookup"><span data-stu-id="f0046-153">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="f0046-154">Você pode usar do contêiner Olá **list_blobs** blobs de saudação do método tooretrieve e/ou diretórios dentro dele.</span><span class="sxs-lookup"><span data-stu-id="f0046-154">You can then use hello container's **list_blobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="f0046-155">tooaccess Olá rico conjunto de propriedades e métodos para uma retornado **list_blob_item**, você deve chamar hello **list_blob_item.as_blob** método tooget um **cloud_blob** objeto, ou hello **list_blob.as_directory** método tooget um objeto cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="f0046-155">tooaccess hello rich set of properties and methods for a returned **list_blob_item**, you must call hello **list_blob_item.as_blob** method tooget a  **cloud_blob** object, or hello **list_blob.as_directory** method tooget a  cloud_blob_directory object.</span></span> <span data-ttu-id="f0046-156">Olá código a seguir demonstra como tooretrieve e saída Olá URI de cada item em Olá **meu contêiner de exemplo** contêiner:</span><span class="sxs-lookup"><span data-stu-id="f0046-156">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
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

<span data-ttu-id="f0046-157">Para obter mais detalhes sobre a lista de operações, consulte [Listar recursos de Armazenamento do Azure em C++](storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="f0046-157">For more details on listing operations, see [List Azure Storage Resources in C++](storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="f0046-158">Como: baixar blobs</span><span class="sxs-lookup"><span data-stu-id="f0046-158">How to: Download blobs</span></span>
<span data-ttu-id="f0046-159">blobs toodownload, recuperar uma referência de blob e, em seguida, chamar hello **download_to_stream** método.</span><span class="sxs-lookup"><span data-stu-id="f0046-159">toodownload blobs, first retrieve a blob reference and then call hello **download_to_stream** method.</span></span> <span data-ttu-id="f0046-160">Olá, exemplo a seguir usa Olá **download_to_stream** método tootransfer Olá conteúdo tooa fluxo objeto blob que, em seguida, você pode persistir o arquivo local tooa.</span><span class="sxs-lookup"><span data-stu-id="f0046-160">hello following example uses hello **download_to_stream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="f0046-161">Como alternativa, você pode usar o hello **download_to_file** conteúdo de saudação do método toodownload um tooa do arquivo de blob.</span><span class="sxs-lookup"><span data-stu-id="f0046-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a blob tooa file.</span></span>
<span data-ttu-id="f0046-162">Além disso, você também pode usar Olá **download_text** conteúdo de saudação do método toodownload de um blob como uma cadeia de caracteres de texto.</span><span class="sxs-lookup"><span data-stu-id="f0046-162">In addition, you can also use hello **download_text** method toodownload hello contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="f0046-163">Como: excluir blobs</span><span class="sxs-lookup"><span data-stu-id="f0046-163">How to: Delete blobs</span></span>
<span data-ttu-id="f0046-164">toodelete um blob, primeiro obter uma referência de blob e, em seguida, chamar hello **delete_blob** método nele.</span><span class="sxs-lookup"><span data-stu-id="f0046-164">toodelete a blob, first get a blob reference and then call hello **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="f0046-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f0046-165">Next steps</span></span>
<span data-ttu-id="f0046-166">Agora que você aprendeu as Noções básicas de saudação do armazenamento de blob, siga essas toolearn links mais sobre o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0046-166">Now that you've learned hello basics of blob storage, follow these links toolearn more about Azure Storage.</span></span>  

* [<span data-ttu-id="f0046-167">Como toouse armazenamento de fila de C++</span><span class="sxs-lookup"><span data-stu-id="f0046-167">How toouse Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="f0046-168">Como toouse o armazenamento de tabela do C++</span><span class="sxs-lookup"><span data-stu-id="f0046-168">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="f0046-169">Listar recursos de Armazenamento do Azure em C++</span><span class="sxs-lookup"><span data-stu-id="f0046-169">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="f0046-170">Referência da Biblioteca de Cliente de Armazenamento para C++</span><span class="sxs-lookup"><span data-stu-id="f0046-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="f0046-171">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f0046-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="f0046-172">Transferência de dados com hello AzCopy utilitário de linha de comando</span><span class="sxs-lookup"><span data-stu-id="f0046-172">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)

