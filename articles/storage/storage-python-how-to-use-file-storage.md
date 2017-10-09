---
title: aaaDevelop para armazenamento de arquivo do Azure com Python | Microsoft Docs
description: "Saiba como aplicativos de Python toodevelop e serviços que usam toostore de armazenamento do Azure arquivo dados de arquivos."
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
ms.openlocfilehash: 45623e6dbec6f140cedc4e58e56a93fb4af9054e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="c2e27-103">Desenvolvimento para o Armazenamento de Arquivos do Azure com Python</span><span class="sxs-lookup"><span data-stu-id="c2e27-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="c2e27-104">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="c2e27-104">About this tutorial</span></span>
<span data-ttu-id="c2e27-105">Este tutorial demonstra Noções básicas de saudação do uso de aplicativos do Python toodevelop ou serviços que usam dados de arquivo de toostore de armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e27-105">This tutorial will demonstrate hello basics of using Python toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="c2e27-106">Neste tutorial, vamos criar um aplicativo de console simples e mostram como ações básicas de tooperform com armazenamento Python e o arquivo do Azure:</span><span class="sxs-lookup"><span data-stu-id="c2e27-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="c2e27-107">Criar Compartilhamentos de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="c2e27-107">Create Azure File shares</span></span>
* <span data-ttu-id="c2e27-108">Criar diretórios</span><span class="sxs-lookup"><span data-stu-id="c2e27-108">Create directories</span></span>
* <span data-ttu-id="c2e27-109">Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="c2e27-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="c2e27-110">Carregar, baixar e excluir um arquivo</span><span class="sxs-lookup"><span data-stu-id="c2e27-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="c2e27-111">Como armazenamento de arquivo do Azure pode ser acessado via SMB, é possível toowrite aplicativos simples que acessar o compartilhamento de arquivo do Azure hello usando funções e classes de e/s do Python padrão hello.</span><span class="sxs-lookup"><span data-stu-id="c2e27-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Python I/O classes and functions.</span></span> <span data-ttu-id="c2e27-112">Este artigo descreve como aplicativos toowrite que usam Olá SDK de Python do armazenamento do Azure, que usa Olá [armazenamento de arquivo do Azure API REST](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure o armazenamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="c2e27-112">This article will describe how toowrite applications that use hello Azure Storage Python SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

### <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="c2e27-113">Configurar seu aplicativo toouse armazenamento de arquivo do Azure</span><span class="sxs-lookup"><span data-stu-id="c2e27-113">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="c2e27-114">Adicione a seguinte Olá superior Olá qualquer Python do arquivo de origem no qual você deseja acesso tooprogrammatically armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e27-114">Add hello following near hello top of any Python source file in which you wish tooprogrammatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a><span data-ttu-id="c2e27-115">Configurar uma conexão tooAzure armazenamento de arquivo</span><span class="sxs-lookup"><span data-stu-id="c2e27-115">Set up a connection tooAzure File storage</span></span> 
<span data-ttu-id="c2e27-116">Olá `FileService` objeto permite que você trabalhe com compartilhamentos, diretórios e arquivos.</span><span class="sxs-lookup"><span data-stu-id="c2e27-116">hello `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="c2e27-117">Olá código a seguir cria um `FileService` objeto usando a chave de nome e uma conta de conta de armazenamento do hello.</span><span class="sxs-lookup"><span data-stu-id="c2e27-117">hello following code creates a `FileService` object using hello storage account name and account key.</span></span> <span data-ttu-id="c2e27-118">Substitua `<myaccount>` e `<mykey>` pelo nome e pela chave da sua conta.</span><span class="sxs-lookup"><span data-stu-id="c2e27-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="c2e27-119">Criar um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="c2e27-119">Create an Azure File share</span></span>
<span data-ttu-id="c2e27-120">Olá exemplo de código a seguir, você pode usar um `FileService` compartilhamento de saudação do objeto toocreate se ele não existir.</span><span class="sxs-lookup"><span data-stu-id="c2e27-120">In hello following code example, you can use a `FileService` object toocreate hello share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="c2e27-121">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="c2e27-121">Create a directory</span></span>
<span data-ttu-id="c2e27-122">Você também pode organizar o armazenamento, colocando arquivos nos subdiretórios em vez de ter todos eles no diretório raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2e27-122">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="c2e27-123">Armazenamento de arquivo do Azure permite que você toocreate como permitir que vários diretórios como será sua conta.</span><span class="sxs-lookup"><span data-stu-id="c2e27-123">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="c2e27-124">saudação de código abaixo cria um subdiretório chamado **sampledir** no diretório raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2e27-124">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="c2e27-125">Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="c2e27-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="c2e27-126">arquivos de saudação do toolist e diretórios em um compartilhamento, use Olá **lista\_diretórios\_e\_arquivos** método.</span><span class="sxs-lookup"><span data-stu-id="c2e27-126">toolist hello files and directories in a share, use hello **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="c2e27-127">Esse método retorna um gerador.</span><span class="sxs-lookup"><span data-stu-id="c2e27-127">This method returns a generator.</span></span> <span data-ttu-id="c2e27-128">Olá, código a seguir gera Olá **nome** de cada arquivo e diretório em um console de toohello de compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="c2e27-128">hello following code outputs hello **name** of each file and directory in a share toohello console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="c2e27-129">Carregar um arquivo</span><span class="sxs-lookup"><span data-stu-id="c2e27-129">Upload a file</span></span> 
<span data-ttu-id="c2e27-130">Arquivo do Azure compartilhamento contém em Olá muito menos, um diretório raiz onde os arquivos podem residir.</span><span class="sxs-lookup"><span data-stu-id="c2e27-130">Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="c2e27-131">Nesta seção, você aprenderá como o diretório de um compartilhamento de raiz tooupload um arquivo do armazenamento local para hello.</span><span class="sxs-lookup"><span data-stu-id="c2e27-131">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="c2e27-132">toocreate um arquivo e carregar dados, use Olá `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` ou `create_file_from_text` métodos.</span><span class="sxs-lookup"><span data-stu-id="c2e27-132">toocreate a file and upload data, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="c2e27-133">Eles são métodos de alto nível que executam o agrupamento necessário hello quando o tamanho de saudação de dados Olá exceder 64 MB.</span><span class="sxs-lookup"><span data-stu-id="c2e27-133">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="c2e27-134">`create_file_from_path`carregamentos Olá conteúdo de um arquivo do caminho especificado hello e `create_file_from_stream` carregamentos Olá conteúdo de um arquivo já aberto/fluxo.</span><span class="sxs-lookup"><span data-stu-id="c2e27-134">`create_file_from_path` uploads hello contents of a file from hello specified path, and `create_file_from_stream` uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="c2e27-135">`create_file_from_bytes`carrega uma matriz de bytes, e `create_file_from_text` carregamentos Olá especificado valor de texto usando Olá especificado codificação (padrões tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="c2e27-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="c2e27-136">Olá, exemplo a seguir carrega conteúdo Olá Olá **sunset.png** arquivo hello **myfile** arquivo.</span><span class="sxs-lookup"><span data-stu-id="c2e27-136">hello following example uploads hello contents of hello **sunset.png** file into hello **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="c2e27-137">Baixar um arquivo</span><span class="sxs-lookup"><span data-stu-id="c2e27-137">Download a file</span></span>
<span data-ttu-id="c2e27-138">toodownload dados de um arquivo, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, ou `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="c2e27-138">toodownload data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="c2e27-139">Eles são métodos de alto nível que executam o agrupamento necessário hello quando o tamanho de saudação de dados Olá exceder 64 MB.</span><span class="sxs-lookup"><span data-stu-id="c2e27-139">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="c2e27-140">Olá exemplo a seguir demonstra o uso de `get_file_to_path` conteúdo toodownload Olá Olá **myfile** de arquivos e armazená-lo toohello **sunset.png fora** arquivo.</span><span class="sxs-lookup"><span data-stu-id="c2e27-140">hello following example demonstrates using `get_file_to_path` toodownload hello contents of hello **myfile** file and store it toohello **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="c2e27-141">Excluir um arquivo</span><span class="sxs-lookup"><span data-stu-id="c2e27-141">Delete a file</span></span>
<span data-ttu-id="c2e27-142">Finalmente, toodelete um arquivo, chame `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="c2e27-142">Finally, toodelete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="c2e27-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2e27-143">Next steps</span></span>
<span data-ttu-id="c2e27-144">Agora que você aprendeu como toomanipulate armazenamento de arquivo do Azure com o Python, siga essas toolearn links mais.</span><span class="sxs-lookup"><span data-stu-id="c2e27-144">Now that you've learned how toomanipulate Azure File storage with Python, follow these links toolearn more.</span></span>

* [<span data-ttu-id="c2e27-145">Centro de desenvolvedores do Python</span><span class="sxs-lookup"><span data-stu-id="c2e27-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="c2e27-146">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c2e27-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="c2e27-147">SDK do Armazenamento do Microsoft Azure para Python</span><span class="sxs-lookup"><span data-stu-id="c2e27-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)