---
title: Como usar o armazenamento de Blobs do Azure (armazenamento de objeto) do Python | Microsoft Docs
description: "Armazene dados não estruturados na nuvem com o armazenamento de blobs do Azure (armazenamento de objeto)."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 1cab8407be6fc8932b68e50d0c301e8ea37ea3ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-blob-storage-from-python"></a><span data-ttu-id="29ea0-103">Como usar o armazenamento de Blob do Azure no Python</span><span class="sxs-lookup"><span data-stu-id="29ea0-103">How to use Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="29ea0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="29ea0-104">Overview</span></span>
<span data-ttu-id="29ea0-105">O Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="29ea0-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="29ea0-106">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29ea0-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="29ea0-107">O Armazenamento de Blobs também é chamado de armazenamento de objetos.</span><span class="sxs-lookup"><span data-stu-id="29ea0-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="29ea0-108">Este artigo mostra como executar cenários comuns usando o armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="29ea0-108">This article will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="29ea0-109">Os exemplos são escritos em Python e usam o [Microsoft Azure Storage SDK for Python](SDK do Armazenamento do Microsoft Azure para Python).</span><span class="sxs-lookup"><span data-stu-id="29ea0-109">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="29ea0-110">Os cenários abrangidos incluem carregar, listar, baixar e excluir blobs.</span><span class="sxs-lookup"><span data-stu-id="29ea0-110">The scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="29ea0-111">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="29ea0-111">Create a container</span></span>
<span data-ttu-id="29ea0-112">Com base no tipo de blob que você deseja usar, crie um objeto **BlockBlobService**, **AppendBlobService** ou **PageBlobService**.</span><span class="sxs-lookup"><span data-stu-id="29ea0-112">Based on the type of blob you would like to use, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="29ea0-113">O código a seguir usa um objeto **BlockBlobService** .</span><span class="sxs-lookup"><span data-stu-id="29ea0-113">The following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="29ea0-114">Adicione o seguinte na parte superior de qualquer arquivo Python no qual você deseja acessar o Armazenamento de Blobs de Blocos do Azure com programação.</span><span class="sxs-lookup"><span data-stu-id="29ea0-114">Add the following near the top of any Python file in which you wish to programmatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="29ea0-115">O código a seguir cria um objeto **BlockBlobService** usando o nome da conta de armazenamento e a chave de conta.</span><span class="sxs-lookup"><span data-stu-id="29ea0-115">The following code creates a **BlockBlobService** object using the storage account name and account key.</span></span>  <span data-ttu-id="29ea0-116">Substitua “myaccount” e “mykey” pelo nome da sua conta e sua chave.</span><span class="sxs-lookup"><span data-stu-id="29ea0-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="29ea0-117">No exemplo de código a seguir, você poderá usar um objeto **BlockBlobService** para criar o contêiner, se ele não existir.</span><span class="sxs-lookup"><span data-stu-id="29ea0-117">In the following code example, you can use a **BlockBlobService** object to create the container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="29ea0-118">Por padrão, o novo contêiner é particular; portanto, você deve especificar sua chave de acesso de armazenamento (como anteriormente) para baixar blobs desse contêiner.</span><span class="sxs-lookup"><span data-stu-id="29ea0-118">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span> <span data-ttu-id="29ea0-119">Se deseja disponibilizar os blobs dentro do contêiner para todas as pessoas, você pode criar o contêiner e passar o nível de acesso público usando o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="29ea0-119">If you want to make the blobs within the container available to everyone, you can create the container and pass the public access level using the following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="29ea0-120">Como alternativa, você pode modificar um contêiner após você tê-lo criado usando o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="29ea0-120">Alternatively, you can modify a container after you have created it using the following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="29ea0-121">Após essa alteração, qualquer pessoa na Internet pode ver blobs em um contêiner público, mas apenas você pode modificar ou excluí-los.</span><span class="sxs-lookup"><span data-stu-id="29ea0-121">After this change, anyone on the Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="29ea0-122">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="29ea0-122">Upload a blob into a container</span></span>
<span data-ttu-id="29ea0-123">Para criar um blob de blocos e carregar dados, use os métodos **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** ou **create\_blob\_from\_text**.</span><span class="sxs-lookup"><span data-stu-id="29ea0-123">To create a block blob and upload data, use the **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="29ea0-124">Esses são métodos de alto nível que realizam a separação por partes necessária quando o tamanho do arquivo excede 64 MB.</span><span class="sxs-lookup"><span data-stu-id="29ea0-124">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="29ea0-125">**create\_blob\_from\_path** carrega o conteúdo de um arquivo do caminho especificado e **create\_blob\_from\_stream** carrega o conteúdo de um arquivo/fluxo já aberto.</span><span class="sxs-lookup"><span data-stu-id="29ea0-125">**create\_blob\_from\_path** uploads the contents of a file from the specified path, and **create\_blob\_from\_stream** uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="29ea0-126">**create\_blob\_from\_bytes** carrega uma matriz de bytes e **create\_blob\_from\_text** carrega o valor do texto especificado usando a codificação especificada (padronizada para UTF-8).</span><span class="sxs-lookup"><span data-stu-id="29ea0-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="29ea0-127">O exemplo a seguir carrega o conteúdo do arquivo **sunset.png** no blob **myblob**.</span><span class="sxs-lookup"><span data-stu-id="29ea0-127">The following example uploads the contents of the **sunset.png** file into the **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="29ea0-128">Listar os blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="29ea0-128">List the blobs in a container</span></span>
<span data-ttu-id="29ea0-129">Para listar os blobs em um contêiner, use o método **list\_blobs**.</span><span class="sxs-lookup"><span data-stu-id="29ea0-129">To list the blobs in a container, use the **list\_blobs** method.</span></span> <span data-ttu-id="29ea0-130">Esse método retorna um gerador.</span><span class="sxs-lookup"><span data-stu-id="29ea0-130">This method returns a generator.</span></span> <span data-ttu-id="29ea0-131">O código a seguir produz o **nome** de cada blob em um contêiner para o console.</span><span class="sxs-lookup"><span data-stu-id="29ea0-131">The following code outputs the **name** of each blob in a container to the console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="29ea0-132">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="29ea0-132">Download blobs</span></span>
<span data-ttu-id="29ea0-133">Para baixar dados de um blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes** ou **get\_blob\_to\_text**.</span><span class="sxs-lookup"><span data-stu-id="29ea0-133">To download data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="29ea0-134">Esses são métodos de alto nível que realizam a separação por partes necessária quando o tamanho do arquivo excede 64 MB.</span><span class="sxs-lookup"><span data-stu-id="29ea0-134">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="29ea0-135">O exemplo a seguir demonstra como usar **get\_blob\_to\_path** para baixar o conteúdo do blob **myblob** e armazená-lo no arquivo **out-sunset.png**.</span><span class="sxs-lookup"><span data-stu-id="29ea0-135">The following example demonstrates using **get\_blob\_to\_path** to download the contents of the **myblob** blob and store it to the **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="29ea0-136">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="29ea0-136">Delete a blob</span></span>
<span data-ttu-id="29ea0-137">Finalmente, para excluir um blob, chame **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="29ea0-137">Finally, to delete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="29ea0-138">Gravar um blob de anexo</span><span class="sxs-lookup"><span data-stu-id="29ea0-138">Writing to an append blob</span></span>
<span data-ttu-id="29ea0-139">Um blob de acréscimo é otimizado para operações de acréscimo, como o registro em log.</span><span class="sxs-lookup"><span data-stu-id="29ea0-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="29ea0-140">Como um blob de blocos, um blob de acréscimo é composto por blocos; no entanto, quando você adiciona um novo bloco a um blob de acréscimo, ele sempre é acrescentado ao fim do blob.</span><span class="sxs-lookup"><span data-stu-id="29ea0-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="29ea0-141">Não é possível atualizar ou excluir um bloco existente em um blob de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="29ea0-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="29ea0-142">As IDs de bloco de um blob de acréscimo não ficam expostas como em um blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="29ea0-142">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="29ea0-143">Cada bloco em um blob de acréscimo pode ter um tamanho diferente, até no máximo 4 MB, e um blob de acréscimo pode incluir no máximo 50.000 blocos.</span><span class="sxs-lookup"><span data-stu-id="29ea0-143">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="29ea0-144">O tamanho máximo de um blob de acréscimo, portanto, é de pouco mais de 195 GB (4 MB x 50.000 blocos).</span><span class="sxs-lookup"><span data-stu-id="29ea0-144">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="29ea0-145">O exemplo a seguir cria um novo blob de anexo e acrescenta alguns dados a ele, simulando uma operação simples de registro em log.</span><span class="sxs-lookup"><span data-stu-id="29ea0-145">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# The same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="29ea0-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="29ea0-146">Next steps</span></span>
<span data-ttu-id="29ea0-147">Agora que você aprendeu os conceitos básicos do armazenamento de Blobs, siga estes links para saber mais.</span><span class="sxs-lookup"><span data-stu-id="29ea0-147">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="29ea0-148">Centro de desenvolvedores do Python</span><span class="sxs-lookup"><span data-stu-id="29ea0-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="29ea0-149">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="29ea0-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="29ea0-150">[Blog da equipe de Armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="29ea0-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="29ea0-151">[Microsoft Azure Storage SDK for Python]</span><span class="sxs-lookup"><span data-stu-id="29ea0-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog da equipe de Armazenamento do Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python
