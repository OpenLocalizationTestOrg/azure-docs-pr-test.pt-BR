---
title: Desenvolvimento para o Armazenamento de Arquivos do Azure com Python | Microsoft Docs
description: "Saiba como desenvolver aplicativos e serviços Python que usam o Armazenamento de Arquivos do Azure para armazenar dados de arquivo."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: a1a37266908277b54e7b42d85b9b4873af77e622
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="11653-103">Desenvolvimento para o Armazenamento de Arquivos do Azure com Python</span><span class="sxs-lookup"><span data-stu-id="11653-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="11653-104">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="11653-104">About this tutorial</span></span>
<span data-ttu-id="11653-105">Este tutorial demonstrará as noções básicas para usar o Python para desenvolver aplicativos ou serviços que usam o Armazenamento de Arquivos do Azure para armazenar dados de arquivo.</span><span class="sxs-lookup"><span data-stu-id="11653-105">This tutorial will demonstrate the basics of using Python to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="11653-106">Neste tutorial, criaremos um aplicativo de console simples e mostraremos como executar ações básicas com Python e o Armazenamento de Arquivos do Azure:</span><span class="sxs-lookup"><span data-stu-id="11653-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="11653-107">Criar Compartilhamentos de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="11653-107">Create Azure File shares</span></span>
* <span data-ttu-id="11653-108">Criar diretórios</span><span class="sxs-lookup"><span data-stu-id="11653-108">Create directories</span></span>
* <span data-ttu-id="11653-109">Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="11653-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="11653-110">Carregar, baixar e excluir um arquivo</span><span class="sxs-lookup"><span data-stu-id="11653-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="11653-111">Como o Armazenamento de Arquivos do Azure pode ser acessado via SMB, é possível criar aplicativos simples que acessam o Compartilhamento de Arquivos do Azure usando as classes e funções padrão de E/S do Python.</span><span class="sxs-lookup"><span data-stu-id="11653-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Python I/O classes and functions.</span></span> <span data-ttu-id="11653-112">Este artigo descreverá como criar aplicativos que usam o SDK do Python do Armazenamento do Azure, que usa a [API REST do Armazenamento de Arquivos do Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) para se comunicar com o Armazenamento de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="11653-112">This article will describe how to write applications that use the Azure Storage Python SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

### <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="11653-113">Configurar seu aplicativo para usar o Armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="11653-113">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="11653-114">Adicione o seguinte próximo à parte superior de qualquer arquivo de origem Python no qual você deseja acessar o Armazenamento do Azure com programação.</span><span class="sxs-lookup"><span data-stu-id="11653-114">Add the following near the top of any Python source file in which you wish to programmatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a><span data-ttu-id="11653-115">Configurar uma conexão com o Armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="11653-115">Set up a connection to Azure File storage</span></span> 
<span data-ttu-id="11653-116">O objeto `FileService` permite que você trabalhe com compartilhamentos, diretórios e arquivos.</span><span class="sxs-lookup"><span data-stu-id="11653-116">The `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="11653-117">O código a seguir cria um objeto `FileService` usando o nome da conta de armazenamento e a chave de conta.</span><span class="sxs-lookup"><span data-stu-id="11653-117">The following code creates a `FileService` object using the storage account name and account key.</span></span> <span data-ttu-id="11653-118">Substitua `<myaccount>` e `<mykey>` pelo nome e pela chave da sua conta.</span><span class="sxs-lookup"><span data-stu-id="11653-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="11653-119">Criar um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="11653-119">Create an Azure File share</span></span>
<span data-ttu-id="11653-120">No exemplo de código a seguir, é possível usar um objeto `FileService` para criar o compartilhamento, se ele não existir.</span><span class="sxs-lookup"><span data-stu-id="11653-120">In the following code example, you can use a `FileService` object to create the share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="11653-121">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="11653-121">Create a directory</span></span>
<span data-ttu-id="11653-122">Você também pode organizar o armazenamento colocando arquivos em subdiretórios em vez de manter todos eles no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="11653-122">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="11653-123">O Armazenamento de Arquivos do Azure permite que você crie quantos diretórios a conta permitir.</span><span class="sxs-lookup"><span data-stu-id="11653-123">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="11653-124">O código a seguir criará um subdiretório chamado **sampledir** no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="11653-124">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="11653-125">Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="11653-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="11653-126">Para listar os arquivos e diretórios em um compartilhamento, use o método **list\_directories\_and\_files**.</span><span class="sxs-lookup"><span data-stu-id="11653-126">To list the files and directories in a share, use the **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="11653-127">Esse método retorna um gerador.</span><span class="sxs-lookup"><span data-stu-id="11653-127">This method returns a generator.</span></span> <span data-ttu-id="11653-128">O código a seguir produz o **nome** de cada arquivo e diretório em um compartilhamento para o console.</span><span class="sxs-lookup"><span data-stu-id="11653-128">The following code outputs the **name** of each file and directory in a share to the console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="11653-129">Carregar um arquivo</span><span class="sxs-lookup"><span data-stu-id="11653-129">Upload a file</span></span> 
<span data-ttu-id="11653-130">Um Compartilhamento de Arquivos do Azure contém, no mínimo, um diretório raiz em que os arquivos podem residir.</span><span class="sxs-lookup"><span data-stu-id="11653-130">Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="11653-131">Nesta seção, você aprenderá a carregar um arquivo do armazenamento local para o diretório raiz de um compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="11653-131">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="11653-132">Para criar um arquivo e carregar dados, use os métodos `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` ou `create_file_from_text`.</span><span class="sxs-lookup"><span data-stu-id="11653-132">To create a file and upload data, use the `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="11653-133">Esses são métodos de alto nível que realizam a separação por partes necessária quando o tamanho do arquivo excede 64 MB.</span><span class="sxs-lookup"><span data-stu-id="11653-133">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="11653-134">`create_file_from_path` carrega o conteúdo de um arquivo do caminho especificado e `create_file_from_stream` carrega o conteúdo de um arquivo/fluxo já aberto.</span><span class="sxs-lookup"><span data-stu-id="11653-134">`create_file_from_path` uploads the contents of a file from the specified path, and `create_file_from_stream` uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="11653-135">`create_file_from_bytes` carrega uma matriz de bytes e `create_file_from_text` carrega o valor do texto especificado usando a codificação especificada (padronizada para UTF-8).</span><span class="sxs-lookup"><span data-stu-id="11653-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="11653-136">O exemplo a seguir carrega o conteúdo do arquivo **sunset.png** no arquivo **myfile**.</span><span class="sxs-lookup"><span data-stu-id="11653-136">The following example uploads the contents of the **sunset.png** file into the **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="11653-137">Baixar um arquivo</span><span class="sxs-lookup"><span data-stu-id="11653-137">Download a file</span></span>
<span data-ttu-id="11653-138">Para baixar dados de um arquivo, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes` ou `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="11653-138">To download data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="11653-139">Esses são métodos de alto nível que realizam a separação por partes necessária quando o tamanho do arquivo excede 64 MB.</span><span class="sxs-lookup"><span data-stu-id="11653-139">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="11653-140">O exemplo a seguir demonstra como usar `get_file_to_path` para baixar o conteúdo do arquivo **myfile** e armazená-lo no arquivo **out-sunset.png**.</span><span class="sxs-lookup"><span data-stu-id="11653-140">The following example demonstrates using `get_file_to_path` to download the contents of the **myfile** file and store it to the **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="11653-141">Excluir um arquivo</span><span class="sxs-lookup"><span data-stu-id="11653-141">Delete a file</span></span>
<span data-ttu-id="11653-142">Por fim, para excluir um arquivo, chame `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="11653-142">Finally, to delete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="11653-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11653-143">Next steps</span></span>
<span data-ttu-id="11653-144">Agora que você aprendeu como manipular o Armazenamento de Arquivos do Azure com o Python, siga estes links para saber mais.</span><span class="sxs-lookup"><span data-stu-id="11653-144">Now that you've learned how to manipulate Azure File storage with Python, follow these links to learn more.</span></span>

* [<span data-ttu-id="11653-145">Centro de desenvolvedores do Python</span><span class="sxs-lookup"><span data-stu-id="11653-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="11653-146">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="11653-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="11653-147">SDK do Armazenamento do Microsoft Azure para Python</span><span class="sxs-lookup"><span data-stu-id="11653-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)