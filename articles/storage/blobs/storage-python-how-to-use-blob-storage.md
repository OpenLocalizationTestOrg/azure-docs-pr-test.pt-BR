---
title: aaaHow toouse o armazenamento de BLOBs do Azure (armazenamento de objeto) do Python | Microsoft Docs
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
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
ms.openlocfilehash: 8f9ca93e52b030384e28a739d2f1c6b610be094a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a><span data-ttu-id="97cc0-103">Como toouse armazenamento de BLOBs do Azure do Python</span><span class="sxs-lookup"><span data-stu-id="97cc0-103">How toouse Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="97cc0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="97cc0-104">Overview</span></span>
<span data-ttu-id="97cc0-105">Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="97cc0-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="97cc0-106">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97cc0-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="97cc0-107">Armazenamento de blob também é chamado tooas armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="97cc0-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="97cc0-108">Este artigo mostra como tooperform cenários comuns de usar o armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="97cc0-108">This article will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="97cc0-109">exemplos de saudação são escritos em Python e usar Olá [Microsoft Azure Storage SDK para Python].</span><span class="sxs-lookup"><span data-stu-id="97cc0-109">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="97cc0-110">cenários de saudação abordados incluem carregar, listar, baixar e exclusão de blobs.</span><span class="sxs-lookup"><span data-stu-id="97cc0-110">hello scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="97cc0-111">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="97cc0-111">Create a container</span></span>
<span data-ttu-id="97cc0-112">Com base no tipo de saudação do blob que deseja toouse, crie um **BlockBlobService**, **AppendBlobService**, ou **PageBlobService** objeto.</span><span class="sxs-lookup"><span data-stu-id="97cc0-112">Based on hello type of blob you would like toouse, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="97cc0-113">código a seguir Olá usa um **BlockBlobService** objeto.</span><span class="sxs-lookup"><span data-stu-id="97cc0-113">hello following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="97cc0-114">Adicione a seguinte Olá superior de saudação de qualquer arquivo Python no qual você deseja acesso tooprogrammatically armazenamento de Blob de bloco do Azure.</span><span class="sxs-lookup"><span data-stu-id="97cc0-114">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="97cc0-115">Olá código a seguir cria um **BlockBlobService** objeto usando a chave de nome e uma conta de conta de armazenamento do hello.</span><span class="sxs-lookup"><span data-stu-id="97cc0-115">hello following code creates a **BlockBlobService** object using hello storage account name and account key.</span></span>  <span data-ttu-id="97cc0-116">Substitua “myaccount” e “mykey” pelo nome da sua conta e sua chave.</span><span class="sxs-lookup"><span data-stu-id="97cc0-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="97cc0-117">Olá exemplo de código a seguir, você pode usar um **BlockBlobService** toocreate Olá contêiner se ele não existir.</span><span class="sxs-lookup"><span data-stu-id="97cc0-117">In hello following code example, you can use a **BlockBlobService** object toocreate hello container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="97cc0-118">Por padrão, novo contêiner de saudação é privado, portanto, você deve especificar sua chave de acesso de armazenamento (como feito anteriormente) blobs toodownload desse contêiner.</span><span class="sxs-lookup"><span data-stu-id="97cc0-118">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span> <span data-ttu-id="97cc0-119">Se você quiser toomake blobs Olá Olá contêiner disponível tooeveryone, você pode criar contêiner de saudação e passar o nível de acesso público hello usando Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="97cc0-119">If you want toomake hello blobs within hello container available tooeveryone, you can create hello container and pass hello public access level using hello following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="97cc0-120">Como alternativa, você pode modificar um contêiner depois que você criou usando a saudação de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="97cc0-120">Alternatively, you can modify a container after you have created it using hello following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="97cc0-121">Após essa alteração, qualquer pessoa na Internet de saudação pode ver os blobs em um contêiner público, mas somente você pode modificar ou excluí-los.</span><span class="sxs-lookup"><span data-stu-id="97cc0-121">After this change, anyone on hello Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="97cc0-122">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="97cc0-122">Upload a blob into a container</span></span>
<span data-ttu-id="97cc0-123">toocreate um blob de bloco e carregar dados, use Olá **criar\_blob\_de\_caminho**, **criar\_blob\_de\_fluxo**, **criar\_blob\_de\_bytes** ou **criar\_blob\_de\_texto** métodos.</span><span class="sxs-lookup"><span data-stu-id="97cc0-123">toocreate a block blob and upload data, use hello **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="97cc0-124">Eles são métodos de alto nível que executam o agrupamento necessário hello quando o tamanho de saudação de dados Olá exceder 64 MB.</span><span class="sxs-lookup"><span data-stu-id="97cc0-124">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="97cc0-125">**criar\_blob\_de\_caminho** carregamentos Olá conteúdo de um arquivo do caminho especificado hello e **criar\_blob\_de\_fluxo** carregamentos Olá conteúdo de um arquivo já aberto/fluxo.</span><span class="sxs-lookup"><span data-stu-id="97cc0-125">**create\_blob\_from\_path** uploads hello contents of a file from hello specified path, and **create\_blob\_from\_stream** uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="97cc0-126">**criar\_blob\_de\_bytes** carrega uma matriz de bytes, e **criar\_blob\_de\_texto** carrega Olá especificado valor de texto usando Olá especificado codificação (padrões tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="97cc0-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="97cc0-127">Olá, exemplo a seguir carrega conteúdo Olá Olá **sunset.png** arquivo hello **myblob** blob.</span><span class="sxs-lookup"><span data-stu-id="97cc0-127">hello following example uploads hello contents of hello **sunset.png** file into hello **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="97cc0-128">Saudação de listar blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="97cc0-128">List hello blobs in a container</span></span>
<span data-ttu-id="97cc0-129">blobs de saudação toolist em um contêiner, use Olá **lista\_blobs** método.</span><span class="sxs-lookup"><span data-stu-id="97cc0-129">toolist hello blobs in a container, use hello **list\_blobs** method.</span></span> <span data-ttu-id="97cc0-130">Esse método retorna um gerador.</span><span class="sxs-lookup"><span data-stu-id="97cc0-130">This method returns a generator.</span></span> <span data-ttu-id="97cc0-131">Olá, código a seguir gera Olá **nome** de cada blob em um console de toohello do contêiner.</span><span class="sxs-lookup"><span data-stu-id="97cc0-131">hello following code outputs hello **name** of each blob in a container toohello console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="97cc0-132">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="97cc0-132">Download blobs</span></span>
<span data-ttu-id="97cc0-133">toodownload dados de um blob, use **obter\_blob\_para\_caminho**, **obter\_blob\_para\_fluxo**, **obter\_blob\_para\_bytes**, ou **obter\_blob\_para\_texto**.</span><span class="sxs-lookup"><span data-stu-id="97cc0-133">toodownload data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="97cc0-134">Eles são métodos de alto nível que executam o agrupamento necessário hello quando o tamanho de saudação de dados Olá exceder 64 MB.</span><span class="sxs-lookup"><span data-stu-id="97cc0-134">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="97cc0-135">Olá exemplo a seguir demonstra o uso de **obter\_blob\_para\_caminho** conteúdo toodownload Olá Olá **myblob** blob e armazená-lo toohello **out sunset.png** arquivo.</span><span class="sxs-lookup"><span data-stu-id="97cc0-135">hello following example demonstrates using **get\_blob\_to\_path** toodownload hello contents of hello **myblob** blob and store it toohello **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="97cc0-136">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="97cc0-136">Delete a blob</span></span>
<span data-ttu-id="97cc0-137">Finalmente, toodelete um blob, chame **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="97cc0-137">Finally, toodelete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="97cc0-138">Blob de acréscimo tooan de gravação</span><span class="sxs-lookup"><span data-stu-id="97cc0-138">Writing tooan append blob</span></span>
<span data-ttu-id="97cc0-139">Um blob de acréscimo é otimizado para operações de acréscimo, como o registro em log.</span><span class="sxs-lookup"><span data-stu-id="97cc0-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="97cc0-140">Como um blob de bloco, um blob de acréscimo é composto por blocos, mas quando você adiciona um novo blob de acréscimo de tooan de bloco, é sempre anexado toohello final de blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="97cc0-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="97cc0-141">Não é possível atualizar ou excluir um bloco existente em um blob de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="97cc0-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="97cc0-142">IDs de bloco Olá para um blob de acréscimo não são expostos como eles são para um blob de bloco.</span><span class="sxs-lookup"><span data-stu-id="97cc0-142">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="97cc0-143">Cada bloco em um blob de acréscimo pode ter um tamanho diferente, o máximo de tooa de 4 MB, e um blob de acréscimo pode incluir até 50.000 blocos.</span><span class="sxs-lookup"><span data-stu-id="97cc0-143">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="97cc0-144">tamanho máximo de saudação de um blob de acréscimo, portanto, é um pouco mais de 195 GB (4 MB X 50.000 blocos).</span><span class="sxs-lookup"><span data-stu-id="97cc0-144">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="97cc0-145">exemplo Hello abaixo cria um novo blob de acréscimo e acrescenta alguns tooit de dados, com uma simulação de uma operação de log simples.</span><span class="sxs-lookup"><span data-stu-id="97cc0-145">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="97cc0-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97cc0-146">Next steps</span></span>
<span data-ttu-id="97cc0-147">Agora que você aprendeu as Noções básicas de saudação do armazenamento de Blob, siga essas toolearn links mais.</span><span class="sxs-lookup"><span data-stu-id="97cc0-147">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="97cc0-148">Centro de desenvolvedores do Python</span><span class="sxs-lookup"><span data-stu-id="97cc0-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="97cc0-149">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="97cc0-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="97cc0-150">[Blog da equipe de Armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="97cc0-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="97cc0-151">[Microsoft Azure Storage SDK para Python]</span><span class="sxs-lookup"><span data-stu-id="97cc0-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog da equipe de Armazenamento do Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK para Python]: https://github.com/Azure/azure-storage-python
